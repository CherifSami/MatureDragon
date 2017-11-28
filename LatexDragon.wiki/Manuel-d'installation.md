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

# Installation du serveur

Cloner le dépôt :

`git clone -b server https://github.com/CherifSami/LatexDragon`

Compillation avec avec *gradle*:
> `gradle build`

Compillation avec *gradlew*:
> `./gradlew`
