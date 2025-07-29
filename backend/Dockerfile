# Utiliser l'image Gradle avec JDK 17 pour le développement
FROM gradle:8.5-jdk17

# Définir le répertoire de travail
WORKDIR /app

# Copier tous les fichiers nécessaires
COPY . .

# Convertir les fins de ligne Windows en Unix et rendre gradlew exécutable
RUN sed -i 's/\r$//' gradlew && chmod +x gradlew

# Exposer le port 8080
EXPOSE 8080

# Commande pour démarrer l'application en mode développement
CMD ["./gradlew", "bootRun"]
