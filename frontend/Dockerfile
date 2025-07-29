# Utiliser Node.js 18 pour le développement
FROM node:18-alpine

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers de configuration
COPY package*.json ./

# Installer les dépendances
RUN npm ci

# Copier le code source
COPY . .

# Exposer le port 5173 (port par défaut de Vite)
EXPOSE 5173

# Démarrer le serveur de développement Vite
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"] 