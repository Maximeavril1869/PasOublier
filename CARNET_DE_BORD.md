# Carnet de bord : PasOublier

Journal de toutes les opérations réalisées. À relire pour savoir où en est le projet.

## État actuel

Version 1.1 (tri manuel ajouté) développée et testée en navigateur simulé. En attente de validation sur iPhone par l'utilisateur.

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

### 2026-11-23 : version 1.1
- Demande : tri manuel des tâches à effectuer.
- Décisions validées avec l'utilisateur : tri dans Réglages (Aujourd'hui reprend cet ordre) ; boutons flèches ↑ ↓ (pas de glisser-déposer) ; tri des tâches dans chaque moment ET des moments entre eux.
- Code : `moveItem()` dans `index.html` (échange avec le voisin du même moment pour les tâches) ; l'ordre est celui des tableaux `S.moments` / `S.tasks`, donc sauvegardé et restauré avec le reste, sans changement de format de données.
- Numéro de version affiché en bas de Réglages (constante `APP_VERSION`). Cache du service worker passé à v3.
- Tests automatisés en navigateur headless mobile : monter/descendre, butées (boutons grisés), tri des moments, persistance après rechargement, ordre repris dans Aujourd'hui : OK, aucune erreur JS.

## Reste à faire / idées

- Validation par l'utilisateur sur iPhone (installation sur l'écran d'accueil).
- Vérifier que GitHub Pages est activé sur le dépôt.
- Idées non retenues pour l'instant : alertes, géolocalisation (limites iOS).
