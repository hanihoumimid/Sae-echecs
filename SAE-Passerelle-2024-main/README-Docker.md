# Application d'Échecs - Configuration Docker

Cette application d'échecs utilise Docker pour containeriser le backend Spring Boot et le frontend Vue.js.

## Architecture

- **Backend** : Application Spring Boot avec Gradle (port 8080)
- **Frontend** : Application Vue.js avec Vite, servie par nginx (port 80)

## Prérequis

- Docker
- Docker Compose

## Instructions d'utilisation

### 1. Construction et démarrage des conteneurs

```bash
# Se placer dans le répertoire racine du projet
cd SAE-Passerelle-2024-main

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

### 4. Développement

Pour le développement, vous pouvez également utiliser les commandes suivantes :

#### Backend (dans le dossier Chess)
```bash
cd Chess
./gradlew bootRun
```

#### Frontend (dans le dossier front)
```bash
cd front
npm install
npm run dev
```

## Structure des fichiers Docker

- `docker-compose.yml` : Orchestration des services
- `Chess/Dockerfile` : Configuration du backend Spring Boot
- `front/Dockerfile` : Configuration du frontend Vue.js
- `front/nginx.conf` : Configuration nginx pour servir l'application
- `.dockerignore` : Fichiers exclus des builds Docker

## Ports utilisés

- **80** : Frontend (nginx)
- **8080** : Backend (Spring Boot)

## Variables d'environnement

Le backend utilise le profil Spring `docker` par défaut. Vous pouvez modifier les variables d'environnement dans le fichier `docker-compose.yml`. 