# Architecture client/serveur

Le client communique avec le serveur grâce a des requêtes. Ces requêtes sont des requêtes http GET. Le serveur reçoit ces requêtes et renvoie un objet JSON au client, une fois que le client à reçu la réponse elle est traité.



Un exemple de communication entre le client et le serveur serais un bouton dans le client qui une fois cliqué appelle la fonction envoieRequete() cette fonction créer la requête pour et l'envoie au serveur sur L’URL `http://localhost:8080/LibreDragon/api/test`.
Le serveur lui dispose d'une méthode s'occupant des requêtes de type GET pour cette URL spécifique. Cette méthode traite la requête et renvoie un objet JSON sous forme d'une chaîne de caractère.
Le client reçoit donc la réponse du serveur, la réponse est traité par la fonction reponseDuServeur() qui récupère la chaîne de caractère, la transforme en objet JSON et fait quelque chose avec.

PS: ces fonctions n’existent pas c'est juste un exemple pour illustrer comment fonctionne la communication entre le client et le serveur.

Exemple de communication client/serveur pour la création d'une partie :

![Communication](https://drive.google.com/uc?export=view&id=0BwI3BqLCkW55ZDI1UnhWWGphNDg)

Pour plus d'information sur les objets JSON consulter la page consacrer aux [objets JSON](https://github.com/huacayacauh/LatexDragon/wiki/Objets-JSON)
