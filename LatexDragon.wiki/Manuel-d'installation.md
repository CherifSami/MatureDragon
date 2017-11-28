# Installation du client

### Prérequis
[Node.js](https://nodejs.org/en/)

Cloner le dépôt :

>`git clone -b client https://github.com/CherifSami/LatexDragon`


l'installation de npm ça ce fait automatiquement avec nodeJs
> `sudo apt-get install python-software-properties`

aprés il faut lancer les commande sur 
https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions

Installer electron :
> `npm install electron --save-dev`

# Installation du serveur

`git clone -b server https://github.com/Jean-Phillipe/LatexDragon`

Compiler avec :
`gradle build`

Si vous avez une erreur de compilation :
`./gradlew`
