# Explication des fonctionnalités

Nous allons ici expliquer comment certaine fonctionnalités du client marche plus en détails, pas toutes les fonctionnalités seront expliqué, seulement les plus importantes.

### GameState
Le module/class `GameState` s'occupe de gérer les parties côté client. Une partie est défini par un objet `Game` (GameState.js), cet objet game contient toutes les informations d'une partie.

Un objet `GameState` lui contient un tableau de `Game` représentant toutes les parties en cours, un entier `currentGame` qui représente l'indice dans le tableau de la partie en cours, un entier `maxGame` réprésentant le nombre maximum de partie et une variable `inCreation` de type `Game` qui représente une partie qui est en création et qui sera ajouté au tableau principal une fois sa création finie.

Une partie est considérer complète une fois que certain de ces champs sont compléter.

Ces parties sont stocker dans le fichier `config/gamestate.json`.

L'objet `Application` contient un objet `GameState` représentant toutes les parties en cours de l'application. Lors du démarrage de l'application cet objet vaut `null` et l'application lance une synchronisation, seulement à la fin de cette synchronisation l'objet `GameState` est initialisé.

L'objet `GameState` est initialisé par la fonction `initGameState()` qui va créer un nouvelle objet `GameState` et lire le fichier `config/gamestate.json` pour remplir le tableau de parties.

### Synchronisation
Les parties étant stocké à la fois sur le client et sur le serveur, on a besoin d'un système pour synchroniser les 2.

Le système de synchronisation est gérer par le module `synchronize` (synchronize.js), l'application va sauvegarder les l'objet GameState dans le fichier `config/gamestate.json` puis créer une tache de fond qui s'occupe de gérer la synchronisation, pendant cette synchronisation l'objet `GameState` d'`Application` vaut `null`.

Le module `synchronize` va lire le fichier `config/gamestate.json` puis pour chaque partie trouver dans le fichier, va envoyé une requête au serveur lui demandant si cette partie existe bien, si le serveur répond positivement, la partie est sauvegarder sinon elle est supprimer, une fois les requêtes fini le module va sauvegarder les partie synchronisé dans le fichier `config/gamestate.json` et envoyer un événement `synchronization-done` au processus principal pour signaler que la synchronisation est fini et un événement `boom` pour signaler au processus principal que cette tache de fond à fini son travail et qu'elle peut être détruite.

Une fois que le processus principal à reçu l'évènement `synchronization-done` il va envoyer un évènement `synchronization-done` à la fenêtre principal qui va ré-initialiser l'objet `GameState` d'`Application`.

![syncrhonisation](https://drive.google.com/uc?export=view&id=0BwI3BqLCkW55TkRTc3VnazQ2eUE)

### Tooltip
Le tooltip du jeu permet à l'utilisateur de visualiser les règles applicable au nœud de la formule sur lequel la souris est positionné et aussi d'appliquer une de ces règles à la formule.

Le tooltip peut être désactiver dans les paramètres et apparaitra seulement lorsque l'utilisateur clique droit sur un nœud de la formule.

Le tooltip marche de la façon suivante: la formule principal sur laquelle l'utilisateur interagis utilise une syntaxe LaTeX spécial qui permet lorsque MathJax converti la chaîne de caractère en LaTex d'attribuer des id aux différent nœuds de la formule. Ces ids nous permettent ainsi de différencier les nœuds.

Le tooltip est gérer par le module `mouseEventHandler` (mouseEventHandler.js) et utilise les évènements javascript `contextmenu`, `mouseover`, `mouseleave` et `mousemove` sur lequel sont bind les fonctions contenu dans le module `mouseEventHandler` (si le tooltip est désactiver dans les options seulement l'évènement `contextmenu` est utiliser).

L'évènement `contextmenu` est déclencher lorsque l'utilisateur clique droit sur un des nœuds de la formule, a ce moment là le tooltip apparait à l'écran et garde sa positon même lorsque l'utilisateur bouge la souris pour que l'utilisateur soit capable de cliquer sur les règles pour les appliquer, pour ce faire on désactive les events handlers mis en place plus tôt
pour les évènements `mouseover`, `mouseleave` et `mousemove`, lorsque l'utilisateur clique droit ou gauche ailleurs dans la fenêtre le tooltip est caché est les events handlers sont remis en place.

L'évènement `mouseover` est déclencher lorsque le pointeur de la souris entre dans un élément ou l'un de ces fils. Pour le tooltip lorsque cet évènement est déclencher le tooltip est afficher et ça position mis à jour.

L'évènement `mouseleave` est déclencher lorsque le pointeur de la souris sors dans un élément. Pour le tooltip lorsque cet évènement est déclencher le tooltip est cacher.

L'évènement `mousemove` est déclencher lorsque le pointeur de la souris bouge lorsqu'il est au dessus d'un élément. Pour le tooltip lorsque cet évènement est déclencher la position et la taille du tooltip sont mises à jour.

Le tooltip utilise les données contenu dans l'objet JSON d'état de jeu pour construire le contenu du tooltip.
La taille du tooltip est calculer dynamiquement en fonction de la taille de l'écran et de l'espace disponible, ce référer à la documentation du code source pour plus d'information sur le calcul.

Une dernière chose à savoir c'est que la formule est sous forme d'arbre, et en javascript/html lorsqu'un évènement est déclencher il remonte comme une bulle dans l'arbre de la page et dans le cas de notre tooltip c'est gênant, par exemple si on a la formule `a + b` passer la souris sur `a` va déclencher l'évènement sur `a` et ainsi afficher le tooltip des règles applicable sur `a`, sauf que l'évènement va remonter et être déclencher sur le `+` qui est parent de `a` et ainsi nous affiche les règles applicable sur `+` et non sur `a`. Pour empêcher ce problème la solution est assez simple il suffit d'appeler la fonction `event.stopPropagation()`.

### ServerStatus
Le module `serverStatus` (serverStatus.js) consiste d'un module qui ping en permanence le serveur pour savoir si il est en ligne, lorsque le statut du serveur change un évènement `server-status` est envoyé au processus principal qui à son tour envoie un évènement `server-status` à la fenêtre principal qui met à jour une variable contenu dans `Application`, le statut du serveur est sous la forme d'un booléen false = hors ligne, true = en ligne.
Si le statut du serveur passe de hors ligne à en ligne une synchronisation est automatiquement effectué.
Cette fonctionnalité est assez simple mais peut ce révéler très utile pour éviter d'envoyer des requêtes à un serveur hors ligne par exemple.

### Background process
Le processus principal (main.js) permet la création de taches de fond qui exécute du code javascript. Ces taches de fond sont tout simplement des fenêtre qui ne sont pas afficher vu que chaque fenêtre est sont propre processus, ces fenêtres sont stocké dans un tableau et sont créer grâce à la fonction `createNewBackgroundProcess` qui prend en argument une chaîne de caractère correspondant à du code javascript que la fenêtre créer va exécuter.

Ces taches de fond sont fermer automatiquement lorsque la fenêtre principal de l'application est fermé.

Un processus renderer peut demander la création d'une nouvelle tache de fond avec l'évènement `new-background-process` qui prend en paramètre le code javascript à exécuter.

A l'heure actuelle seul les modules `serverStatus` et `synchronize` sont utiliser en tant que tâches de fond.