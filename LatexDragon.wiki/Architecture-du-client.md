# Architecture du client

### Architecture d'électron
Le client utilise le framework [electron](https://electron.atom.io). Electron étant basé sur chromium utilise une architecture similaire, càd que l'application est contrôlée par un processus principal et que chacune des fenêtre de l'application est son propre processus. Ci-dessous est un schéma qui explique de façon basique l'architecture d'electron, pour plus d'information sur le fonctionnement d'electron et les fonctionnalité des processus référez-vous à la [documentation d'electron](https://electron.atom.io/docs/).

![electron](https://drive.google.com/uc?export=view&id=0BwI3BqLCkW55OThKWlUwYTd5R2s)

### Fonctionnement général

Le client utilisant electron est divisé en plusieurs processus, le processus main est gérer par le fichier main.js (défini dans package.json), ce processus est responsable de créer les fenêtres de l'application et aussi de communiquer avec les autres processus utilisant ipc, il contient donc quelques fonction pour créer des fenêtres et principalement des event listener.


La fenêtre principal de l'application est est gérer par index.html qui contient le squelette de la page càd le menu, les boutons de contrôle de l'application et d'autres éléments gadget. Le contenu de la page est contenu dans les fichier html du dossier /html.


L'Application marche utilisant un système "d'onglets", chaque onglet est composé d'un fichier html présent dans le dossier /html et éventuellement d'un fichier js dans /js/handlers qui est sous la forme d'un module CommonJS contenant toutes les fonctions qui gère les fonctionnalités de la page.
Ces onglets/pages sont chargé grâce à la fonction `application.requestHtml()` qui envoie une requête pour récupérer le fichier html.
Une fois la requête complète la fonction `application.loadHtml()` append le fichier html à l’élément `<div class=”main”>` du fichier index.html et appelle la fonction responsable d'initialiser le handler du fichier html pour mettre en place tous les events handlers. L'handler n'est pas obligatoire, un onglet peut ne pas avoir d'handler.

![onglets](https://drive.google.com/uc?export=view&id=0BwI3BqLCkW55dDkwS3Fxdm5RTVE)

A l'heure actuel l'application dispose de 6 "onglets":
* L'onglet 'HOME' est la page d'accueil de l'application et est l'onglet charger au démarrage de l'app.
* L'onglet 'HELP' est la page d'aide, cette page explique le fonctionnement de l'application.
* L'onglet 'SETTINGS' est la page qui permet de changer les différents paramètres de l'application.
* L'onglet 'GAME' est la page de jeu de l'application, c'est dans cette onglet que ce déroule une ou plusieurs parties.
* L'onglet 'GAMEMODE' permet de sélectionner le type de partie que l'on veut lors de la création d'une partie.
* L'onglet 'GAMERULESET' permet de sélectionner le type de règles de la partie et la formule avec laquelle on souhaite jouer.

### L'objet Application

L'objet application s'occupe de gérer le bon fonctionnement de l'application, c'est en quelque sorte le noyau de l’application. Il s'occupe de gérer l'état des onglets, charger les onglets, et contient des fonctions permettant d'afficher des notifications ou des popup et contient les paramètres et parties en cours de l'application. L'objet Application dispose d'une seul instance qui est créer lors de l'export du module application, de cette façon n'importe quelle script chargeant le module application dispose de la même instance d'Application.

### L'objet Request

L'objet Request est indispensable au fonctionnement de l'application, cet objet est un wraper de la fonction `$.ajax()` de jQuery qui est elle même un wrapper de l'objet `XMLHttpRequest`. Cet objet permet l'envoie de requêtes asynchrone et est utiliser pour communiquer avec le serveur, mais aussi pour charger les onglets (On peut aussi utiliser le module 'fs' pour ce cas là).

Toutes les requêtes sont défini dans le fichier EnumHelper.js permettant la création de requêtes rapidement avec la fonction `Request.buildRequest()`.

### Module EnumHelper

Le module EnumHelper est un tableau contenant des informations nécessaire au fonctionnement de l'application. Il contient la liste de toutes les requêtes défini par leur nom et contient aussi la liste des handlers pour les onglets.


### Module utils

Le module utils contient des fonctions qui n'ont pas de place ailleurs et sont du type utilitaire. L'une des fonction les plus utiles est la fonction `typesetMath()` qui permet d'appeler MathJax pour convertir le texte LaTex de la page.