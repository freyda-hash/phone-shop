# Utilise l'image officielle de MySQL
FROM mysql:8.0



# Copie des fichiers SQL dans le conteneur pour initialiser la base de données
COPY ./init.sql /docker-entrypoint-initdb.d/

# Expose le port MySQL
EXPOSE 3306
