# Architecture de PasOublier

## Vue d'ensemble

PWA statique, sans serveur ni dépendance. Tout le code applicatif tient dans un seul fichier.

```
PasOublier/
├── index.html            Interface + logique (CSS et JS intégrés)
├── manifest.webmanifest  Métadonnées d'installation (écran d'accueil iPhone)
├── sw.js                 Service worker : fonctionnement hors ligne
├── icon-180/192/512.png  Icônes de l'app
├── README.md             Présentation
├── ARCHITECTURE.md       Ce fichier
├── CARNET_DE_BORD.md     Journal des opérations
└── LICENSE               Tous droits réservés
```

Hébergement : GitHub Pages (branche `main`, racine). Tous les chemins sont relatifs.

## Données (localStorage, clé `pasoublier.v1`)

```
{
  seq:     compteur pour générer les identifiants,
  moments: [ {id, name, icon} ],
  tasks:   [ {id, moment, label, season} ],   // season = null | {from:1..12, to:1..12}
  log:     { "AAAA-MM-JJ": { t:{idTâche:1|2}, snap:{idTâche:libellé} } }
}
```

- `t` : 1 = fait, 2 = pas concerné ; une tâche absente de `t` mais présente dans `snap` = **oubliée** (une fois le jour passé).
- `snap` : photo des tâches dues ce jour-là (avec leur libellé), pour que l'historique reste juste si on modifie ou supprime une tâche ensuite.
- Saison : `from <= to` = intervalle dans l'année ; `from > to` = intervalle à cheval sur deux années (novembre → mars).

## Logique

- `isDue(tâche, date)` : la tâche s'applique-t-elle ce mois-ci ?
- `ensureDay(clé, date)` : crée l'entrée du jour et y inscrit les tâches dues.
- Changement de jour détecté au retour au premier plan et chaque minute : la vue repart de zéro.
- Historique : calculé uniquement sur les jours passés où l'app a été ouverte (les jours sans ouverture ne comptent pas).

## Vues

| Vue | Contenu |
|---|---|
| Aujourd'hui | Cartes par moment, case à cocher, « pas concerné » |
| Historique | Oublis sur 30 jours, tâches les plus oubliées, 14 derniers jours, série |
| Réglages | Gestion moments et tâches (feuilles de saisie), sauvegarde/restauration JSON |

## Contraintes assumées

- Pas de notifications ni de géolocalisation (limites des PWA sur iOS).
- Données liées au navigateur de l'iPhone : d'où la sauvegarde par copier-coller.
- Service worker en « réseau d'abord » : les mises à jour arrivent à la prochaine ouverture avec connexion. Incrémenter `VERSION` dans `sw.js` à chaque évolution.
