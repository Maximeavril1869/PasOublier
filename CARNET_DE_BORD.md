# Carnet de bord : PasOublier

Journal de toutes les opérations réalisées. À relire pour savoir où en est le projet.

## État actuel

Version 1 développée et testée en navigateur simulé. En attente de validation sur iPhone par l'utilisateur.

## Journal

### 2026-11-22
- Besoin exprimé : ne plus oublier la lumière, baisser les radiateurs, etc.
- Décisions validées avec l'utilisateur : nom `PasOublier` ; iPhone ; checklists par moment ; pas d'alertes (il a déjà une app de rappels) ; tâches saisonnières ; historique des oublis conservé.
- Création de l'app : `index.html` (interface, logique), `manifest.webmanifest`, `sw.js`, icônes.
- Contenu initial : 3 moments (maison, dormir, travail) ; une première version contenait 6 tâches d'exemple, retirées ensuite.
- Tests automatisés en navigateur headless (mobile) : cochage, « pas concerné », persistance après rechargement, historique, ajout d'une tâche saisonnière, bascule de saison (simulation de juillet) : OK, aucune erreur JS.
- Rédaction README, ARCHITECTURE, LICENSE (tous droits réservés), ce carnet.
- Publication sur la branche `main`.
- L'utilisateur crée ses tâches lui-même : suppression des tâches par défaut (l'app démarre avec les 3 moments et aucune tâche). Version du cache passée à v2.

## Reste à faire / idées

- Validation par l'utilisateur sur iPhone (installation sur l'écran d'accueil).
- Vérifier que GitHub Pages est activé sur le dépôt.
- Idées non retenues pour l'instant : alertes, géolocalisation (limites iOS).
