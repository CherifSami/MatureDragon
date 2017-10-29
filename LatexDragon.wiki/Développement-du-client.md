# Développement du client

### Précision sur le client
Le client utilise énormément jQuery et les modules CommonJS (système de module de Node.js) donc des connaissances sur ces 2 API sont nécessaire si vous souhaitez continuer le développement de client.

Le client est simplement une interface graphique qui utilise l'API LatexDragon, rien ne vous empêche de créer votre propre client.

### S'y retrouver dans le code
Le client utilise une architecture sous forme "d'onglets"  indépendant les uns des autres avec pour points commun l'objet `Application`.

Les fichier dans le dossier js/handlers sont les fichier qui contiennent toutes les fonctions utilisé par les onglets. Le dossier html contient tous les fichier html des différents onglets.

Tous les fichier javascript sont exporter sous forme de module, les fichiers qui commence par une majuscule sont des classes (elles aussi exporter sous forme de module). Vous pouvez accéder au contenu de n'importe quel module en faisant un `const module = require('monmodule')`.

Pour plus d'informations sur ce que fait tel ou tel fichier la documentation du code source explique tout ce qu'il faut savoir.


### Modification des fonctionnalités
Le plus souvent une fonctionnalité du client est lier à un bouton ou un évènement (click, ipc..), si vous souhaitez modifié une fonctionnalité déjà existante il vous faut trouver la fonction qui est responsable de la fonctionnalité, pour ça si c'est un bouton vous pouvez regarder dans les fichier html quel fonction appelle le bouton ou si c'est un event handler vous devrez pouvoir trouver la fonction dans le fichier du module handler de l'onglet courant.

### Ajouts de fonctionnalités 
Ajouter une fonctionnalité à un onglet existant est assez simple, vous pouvez rajouter votre fonction dans le module correspondant à l'onglet et ensuite par exemple rajouter un bouton dans le fichier html qui appelle votre fonction ou utiliser la méthode init des modules handler pour ajouter votre fonction à un évènement.

### Création "d'onglets"
Si vous souhaiter créer un nouvelle onglet il faut savoir quelques choses.

Le fichier html de votre onglet doit ce trouver dans le dossier html. Ce fichier sera append à l'élément `<div class="main">` du fichier index.html.

Lorsque vous avez créer votre fichier html il faut rajouter une requête dans le module `EnumHelper` pour charger votre fichier html. Pour ce faire aller dans le fichier `EnumHelper.js` et rajouter votre requête dans l'objet `EnumHelper.REQUESTS` vous pouvez copier coller un requête déjà existante et changer le nom de la requête et le nom du fichier html charger.

Maintenant que votre requête est créer vous pouvez charger votre onglet en utilisant la fonction `requestHtml('NOM_DE_LA_REQUETE')` du module `Application`.

Pour le moment votre onglet n'a pas d'handler pour en ajouter un créer un script dans `js/handler/monongletHandler.js`
ce script doit obligatoirement disposer d'une méthode `init()` qui est appeler par le module `Application` à chaque fois qu'un onglet qui possède un handler est charger, la méthode `unload()` est appeler à chaque fois qu'un nouvel onglet est charger pour décharger le module précédent, contrairement à `init()` cette fonction est facultative.

Une fois votre handler créer il faut lui aussi l'ajouter au module `EnumHelper` pour qu'il soit charger automatiquement, comme pour votre requête aller dans le fichier `EnumHelper.js` et rajouter votre handler dans l'objet `EnumHelper.TABS`.