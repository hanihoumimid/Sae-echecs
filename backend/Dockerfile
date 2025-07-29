# Étape de build avec Gradle et JDK 17
FROM gradle:8.5-jdk17 AS build

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers de configuration Gradle
COPY build.gradle settings.gradle ./
COPY gradle ./gradle
COPY gradlew* ./

# Copier le code source
COPY src ./src

# Rendre gradlew exécutable
RUN chmod +x gradlew

# Construire l'application avec Gradle
RUN gradle build -x test

# Étape de production avec JRE
FROM eclipse-temurin:17-jre-alpine

# Créer un utilisateur non-root
RUN addgroup --system --gid 1001 appuser && \
    adduser --system --uid 1001 --ingroup appuser appuser

# Définir le répertoire de travail
WORKDIR /app

# Copier le JAR depuis l'étape de build
COPY --from=build /app/build/libs/*.jar app.jar

# Changer la propriété du fichier
RUN chown appuser:appuser app.jar

# Passer à l'utilisateur non-root
USER appuser

# Exposer le port 8080
EXPOSE 8080

# Commande pour démarrer l'application
ENTRYPOINT ["java", "-jar", "app.jar"] 