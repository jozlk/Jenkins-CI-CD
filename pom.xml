# Utilise une image de base officielle d'OpenJDK
FROM openjdk:17-jdk-slim

# Crée un répertoire pour l'application
WORKDIR /app

# Copier le fichier JAR généré dans le conteneur
COPY target/gestion-presence.jar /app/gestion-presence.jar

# Exposer le port sur lequel Spring Boot écoutera (par défaut 8081)
EXPOSE 8081

# Commande pour démarrer l'application Spring Boot
ENTRYPOINT ["java", "-jar", "/app/gestion-presence.jar"]

