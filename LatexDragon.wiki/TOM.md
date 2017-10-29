# Prototype TOM
Le but de la branche serait d'utiliser la bibliothèque [TOM](http://tom.loria.fr/wiki/index.php5/Main_Page) pour remplacer le backend actuel.

On aimerait appliquer cette règle sur la formule : 2 * ( a/ 2 ) sans avoir à passer par une étape intermédiaire. C’est dans ce contexte que l’extension de langage TOM apparaît, en effet TOM peut être utilisé pour améliorer l’application des règles en générant toutes les variantes possibles d’une expression par associativité et commutativité. Ce que l’on veut c’est que lorsque le serveur test sur une expression quels sont les règles applicables ont essayes aussi sur ses variantes. Par exemple si l’on teste sur a + b les règles applicables alors on doit aussi les tester sur b + a.

Nous avons donc développé une branche expérimentale du serveur utilisant l’extension de langage TOM. Celle-ci n’as que pour but que d’illustrer une future façon de l’implémenter plus durablement. L’exemple ne gère que l’associativité et la commutativité des opérateur + et *.

On peut expliquer son fonctionnement de la façon suivante : le serveur va chercher quels sont les règles applicable sur une expression, il va l’envoyer à la machinerie TOM qui va le traduire dans sa propre représentation d’une expression. Puis dans un second temps va créer deux liste une pour chaque élément associé à l’opérateur + et l’autre à l’opérateur *.
Et enfin TOM va générer une liste de toutes les variantes possible qu’il va renvoyer au serveur. Graĉe à cette liste de variante le serveur va pouvoir agrandir la liste de règles applicables sur l’expression initiale avec les règles applicables sur les variantes.

# Installation
Il n'est pas la peine d'installer tom pour pouvoir utiliser ou modifier cette branche du serveur. L'extension de langage tom est présente dans la version serverTom sous forme de .jar et de fichier de configuration.
Malgré tout vous trouverez la méthode d'installation [ici](http://tom.loria.fr/wiki/index.php5/Documentation:Installation).

Pour obtenir la branche expérimental TOM il suffit de lancer : 

> git clone -b serverTom https://github.com/huacayacauh/LatexDragon.git

Le fonctionnement est le même que celui du serveur classique pour le lancer : 

> gradle tomcatrunwar

# Fonctionnement
Les sources de la surcouche tom sont situées dans le le dossier libredragon/model a la racine du projet.
Le fichier ExpressionApi.t contient tout les éléments tom du programme. Celui-ci va être utilisé pour générer la classe ExpressionApi.java a l'intérieur du package model.
Celle - ci peut être utilisé de la façon suivante:
> ExpressionApi a = new ExpressionApi();

On crée une instance de la machinerie TOM
> ArrayList<Expression> liste = a.run(expression);

On fournit une expression et elle nous rend une liste de ses varaintes.