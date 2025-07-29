# Application Vue.js + Spring Boot Dockerisée

Cette application utilise Docker pour containeriser un frontend Vue.js (Vite) et un backend Spring Boot (Gradle).

## Architecture

- **Frontend** : Application Vue.js avec Vite, servie par nginx (port 80)
- **Backend** : Application Spring Boot avec Gradle (port 8080)

## Structure du projet

```
.
├── frontend/           # Application Vue.js
│   ├── Dockerfile     # Configuration Docker pour le frontend
│   ├── nginx.conf     # Configuration nginx
│   └── .dockerignore  # Fichiers exclus du build Docker
├── backend/           # Application Spring Boot
│   ├── Dockerfile     # Configuration Docker pour le backend
│   └── .dockerignore  # Fichiers exclus du build Docker
├── docker-compose.yml # Orchestration des services
├── .gitignore        # Fichiers exclus de Git
└── README.md         # Ce fichier
```

## Prérequis

- Docker
- Docker Compose

## Instructions d'utilisation

### 1. Construction et démarrage des conteneurs

```bash
# Construire et démarrer tous les services
docker-compose up --build
```

### 2. Accès à l'application

- **Frontend** : http://localhost
- **Backend API** : http://localhost:8080

### 3. Commandes utiles

```bash
# Démarrer les services en arrière-plan
docker-compose up -d

# Arrêter les services
docker-compose down

# Voir les logs
docker-compose logs -f

# Reconstruire les images
docker-compose build --no-cache

# Nettoyer les conteneurs et images
docker-compose down --rmi all --volumes --remove-orphans
```

### 4. Développement local

Pour le développement, vous pouvez également utiliser les commandes suivantes :

#### Backend (dans le dossier backend)
```bash
cd backend
./gradlew bootRun
```

#### Frontend (dans le dossier frontend)
```bash
cd frontend
npm install
npm run dev
```

## Configuration des services

### Frontend
- **Port** : 80
- **Technologie** : Vue.js + Vite + nginx
- **Build** : Multi-stage avec Node.js 18 puis nginx:alpine

### Backend
- **Port** : 8080
- **Technologie** : Spring Boot + Gradle
- **Build** : Multi-stage avec gradle:8.5-jdk17 puis eclipse-temurin:17-jre-alpine

## Réseau

Les services communiquent via le réseau Docker `app-network`. Le frontend peut accéder au backend via l'URL `http://backend:8080`.

## Sécurité

- Le backend utilise un utilisateur non-root pour l'exécution
- Les images utilisent des distributions Alpine pour réduire la taille
- Les builds multi-stage optimisent la taille des images finales
