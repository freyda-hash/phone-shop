# Utilise l'image officielle de MySQL
FROM mysql:8.0

# Variables d'environnement pour initialiser la base de données
ENV MYSQL_ROOT_PASSWORD={MYSQL_ROOT_PASS}
ENV MYSQL_DATABASE=${DB_NAME}
ENV MYSQL_USER=${DB_USER}
ENV MYSQL_PASSWORD=${DB_PASS}

# Copie des fichiers SQL dans le conteneur pour initialiser la base de données
COPY ./init.sql /docker-entrypoint-initdb.d/

# Expose le port MySQL
EXPOSE 3306
