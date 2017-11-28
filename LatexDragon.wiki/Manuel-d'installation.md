# Installation du client

Cloner le dépôt :

>`git clone -b client https://github.com/CherifSami/LatexDragon`


l'installation de nodeJs inclus le package de npm 

> `sudo apt-get install python-software-properties`

> `curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -`

> `sudo apt-get install -y nodejs`

vous pouvez connaitre les dernières distrubutions de nodeJs sur le site officiel de [Node.js](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions)


Installation de electron :
assurez vous bien que vous etez dans le dossier du client

> `npm install electron --save-dev`

### Compilation/Déploiement


Utiliser electron-packager :

> `electron-packager . LibreDragon`

Pour plus d'information consulter la documentation d'[electron](https://github.com/electron/electron/tree/master/docs) et [electron-packager](https://github.com/electron-userland/electron-packager).

**PS:** vous pouvez installer electron globalement avec :
> `npm install electron -g`

Vous avez aussi besoin d'une connexion a internet car MathJax est récupéré sur un CDN.

# Installation du serveur

Cloner le dépôt :

`git clone -b server https://github.com/CherifSami/LatexDragon`

