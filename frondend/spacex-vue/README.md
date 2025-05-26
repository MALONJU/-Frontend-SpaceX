# Eventify Frontend - Application Vue.js

## À propos

Interface utilisateur moderne de l'application Eventify, construite avec Vue 3, TypeScript et Vite. Cette interface permet aux utilisateurs de gérer des événements, des réservations et des catégories de manière intuitive et responsive.

## Technologies

- Vue.js 3 avec Composition API
- TypeScript pour un typage fort
- Vite comme outil de build
- Vue Router pour la navigation
- Pinia pour la gestion d'état
- Axios pour les requêtes HTTP
- SCSS pour le styling
- ESLint + Prettier pour le formatage du code

## Prérequis

- Node.js (v14.x ou supérieur)
- npm ou yarn
- Backend Eventify en cours d'exécution

## Installation

1. Cloner le projet :
```bash
git clone [URL_DU_REPO]
cd frondend/spacex-vue
```

2. Installer les dépendances :
```bash
npm install
# ou
yarn install
```

3. Configurer les variables d'environnement :
```bash
cp .env.example .env.local
```

4. Lancer le serveur de développement :
```bash
npm run dev
# ou
yarn dev
```

## Structure du Projet

```
src/
├── assets/          # Images, styles, fonts
├── components/      # Composants réutilisables
├── views/           # Pages de l'application
├── router/          # Configuration des routes
├── store/           # State management avec Pinia
├── services/        # Services API et utilitaires
├── types/           # Types TypeScript
└── utils/           # Fonctions utilitaires
```

## Composants Principaux

### Pages (Views)
- `HomeView.vue` - Page d'accueil
- `EventsView.vue` - Liste des événements
- `EventDetailView.vue` - Détails d'un événement
- `ProfileView.vue` - Profil utilisateur
- `AdminDashboard.vue` - Dashboard administrateur

### Composants
- `EventCard.vue` - Carte d'événement
- `EventForm.vue` - Formulaire de création/édition
- `CategorySelector.vue` - Sélecteur de catégories
- `ReservationForm.vue` - Formulaire de réservation
- `AuthForms.vue` - Formulaires d'authentification

## Fonctionnalités

1. **Authentification**
   - Inscription
   - Connexion
   - Gestion du profil

2. **Gestion des Événements**
   - Liste des événements
   - Création d'événements
   - Modification d'événements
   - Suppression d'événements
   - Filtrage et recherche

3. **Réservations**
   - Création de réservations
   - Gestion des réservations
   - Historique des réservations

4. **Interface Administrative**
   - Gestion des utilisateurs
   - Gestion des catégories
   - Tableau de bord statistique

## Scripts Disponibles

```bash
# Développement
npm run dev

# Build production
npm run build

# Linting
npm run lint

# Tests
npm run test
```

## Bonnes Pratiques

1. **Architecture**
   - Composants atomiques
   - Composition API
   - TypeScript strict
   - Props et Events typés

2. **State Management**
   - Stores Pinia modulaires
   - Actions asynchrones
   - State persistant

3. **Performance**
   - Lazy loading des routes
   - Optimisation des images
   - Mise en cache

4. **UX/UI**
   - Design responsive
   - Thème sombre/clair
   - Animations fluides
   - Feedback utilisateur

## Tests

```bash
# Exécuter les tests unitaires
npm run test:unit

# Exécuter les tests e2e
npm run test:e2e
```

## Déploiement

1. Construire l'application :
```bash
npm run build
```

2. Les fichiers de production seront générés dans le dossier `dist/`

3. Configurer le serveur web :
   - Configurer les redirections vers index.html
   - Activer la compression gzip
   - Configurer les en-têtes de cache

## Contribution

1. Fork le projet
2. Créer une branche (`git checkout -b feature/AmazingFeature`)
3. Commit les changements (`git commit -m 'Add some AmazingFeature'`)
4. Push vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

## Ressources

- [Documentation Vue.js](https://vuejs.org/)
- [Documentation TypeScript](https://www.typescriptlang.org/)
- [Documentation Vite](https://vitejs.dev/)
- [Documentation Pinia](https://pinia.vuejs.org/)
- [Vue Router](https://router.vuejs.org/)

## Licence

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.
