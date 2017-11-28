# Client

Aprés avoir lancer le serveur,
lancer le client dans une console à partir du dossier du client :

> `./node_modules/.bin/electron .`

Ou

> `electron .`

Vous avez aussi besoin d'une connexion a internet car MathJax est récupéré sur un CDN.

# Server

Lancer le serveur avec :

> `./gradle tomcatRunWar`
ou
> `./gradlew tomcatRunWar` 

Le serveur sera lancé sur l'url `http://localhost:8080/LibreDragon` et contient aussi la documentation du serveur.
