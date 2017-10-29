# Requêtes coté Serveur 

Le serveur et le client peuvent communiquer au moyen de requêtes. Ici nous allons les répertorier et indiquer leurs fonctionnement côté serveur. 
Lorsqu'une des requête ne peut satisfaire la demande du client elle renvoi un message d'erreur sous la forme de l'objet JSON [suivant](https://github.com/huacayacauh/LatexDragon/wiki/Objets-JSON#objet-json-info).

## Statut du serveur
Cette requête est un simple ping qui lorsque le client l'émet le serveur lui répond en lui envoyant la chaîne de caractères: "onligne".

## Début d'une session de jeu
Pour débuter une session le client va demander serveur et va devoir fournir plusieur informations comme :
 * Le mode jeu souhaité (Dans le but d'un développement futur car il est inutilisé ici).
 * L'id de la formule jouable choisie (voir la requête Liste des formules jouables).
 * Un booleen qui dit si oui ou non l'utilisateur veut jouer avec les règles créé durant les précédentes session.
Grâce à toutes ces informations le serveur créer une session de jeu et renvoie l'id de celle-ci avec un l'objet JSON [suivant](https://github.com/huacayacauh/LatexDragon/wiki/Objets-JSON#objet-json-info).

## Fermeture d'une Session de jeu
Pour fermer une session de jeu c'est à dire effacer toutes les données côté serveur. Pour cela le client n'a qu'à fournir l'id de la session qu'il veut fermer et le serveur lui renverras l'objet JSON [suivant](https://github.com/huacayacauh/LatexDragon/wiki/Objets-JSON#objet-json-info)

## Reprise d'une session de jeu
Il est possible de reprendre une session de jeu si le serveur possède encore les données la concernant. Si c'est un succès le serveur renvoie le même [objet](https://github.com/huacayacauh/LatexDragon/wiki/Objets-JSON#objet-json-info) que la requête de début de session.

## Etat du jeu
Il y a quatre façon de demander au serveur l'état du jeu mais dans tout les cas on doit fournir l'id de la session de jeu : 
 * On peut demander la formule courante de la session.
 * On peut demander la formule précédente dans l'historique des transformation de la formule.
 * On peut demander la formule suivante dans l'historique des transformation de la formule.
 * On peut demander la formule présente à un indice spécifique de l'historique des transformation de la formule.
Après l'une de ces demandes le serveur renvoi l'objet JSON [suivant](https://github.com/huacayacauh/LatexDragon/wiki/Objets-JSON#objet-de-l%C3%A9tat-du-jeu) qui contient la formule au format mathJax les règles applicables sur celles-ci et l'historique des transformation.

## Application d'une règle
Cette requête permet au client de demander au serveur d'appliquer une règle sur une expression de la formule courante. Le client doit spécifier l'id de la session de jeu, l'id de l'expression et l'id de la règle. Une fois les test usuels fait on demande au backend d'appliquer la règle sur l'expression et de l'intégrer à la formule courante.
[Ici](https://github.com/huacayacauh/LatexDragon/wiki/Fonctionnement-du-noyau-:-application-d'une-r%C3%A8gle) on peut trouver l'explication de l'application d'une règle.

## Création d'une règle
La création d'une règle ce fait a partir de l'historique des transformations de la formule. Le client fournit l'id de la session de jeu ainsi que 2 indice. Les deux sont les indices de formule dans l'historique. La formule obtenue avec le premier indice correspond au modèle  d'entrée de la règle et la deuxième formule au modèle de sortie de la règle.

## Liste des formules jouables
A travers cette requête le client peut demander au serveur quelles sont les formules jouables (le mécanisme de lecture des formules jouables est décrit [ici](www.lol.com)). Le serveur lui renvois l'objet JSON [suivant](https://github.com/huacayacauh/LatexDragon/wiki/Objets-JSON#objet-de-liste-dexpressions-jouables) qui contient la liste des expression que l'utilisateur peut choisir pour commencer la session de jeu.

## Liste des règles
Le client peut demander au serveur toutes les règles en vigueur dans une session de jeu. Pour cela il devra fournir l'id de la session en question et le serveur lui répond avec l'objet JSON [suivant](https://github.com/huacayacauh/LatexDragon/wiki/Objets-JSON#objet-json-liste-de-r%C3%A8gles) contenant toutes les règles applicables sur la session de jeu.