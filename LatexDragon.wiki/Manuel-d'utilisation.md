# Client

Pour lancer le client taper dans une console à partir du dossier du client :

`./node_modules/.bin/electron .`

Ou

`electron .`

Si electron est installé globalement.

### Compilation/Déploiement

Installer electron-packager :

`npm install electron-packager --save-dev`

Utiliser electron-packager :

`electron-packager . LibreDragon`

Pour plus d'information consulter la documentation d'[electron](https://github.com/electron/electron/tree/master/docs) et [electron-packager](https://github.com/electron-userland/electron-packager).

**PS:** vous pouvez installer electron globalement avec :
`npm install electron -g`

Vous avez aussi besoin d'une connexion a internet car MathJax est récupéré sur un CDN.

# Server

Lancer le serveur avec :

`gradle tomcatRunWar`

Le serveur sera lancé sur l'url `http://localhost:8080/LibreDragon` et contient aussi la documentation du serveur.