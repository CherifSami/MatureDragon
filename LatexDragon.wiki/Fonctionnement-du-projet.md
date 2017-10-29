Si vous souhaitez comprendre en détail le fonctionnement de Kraken-Free-Dragon, vous êtes sur la bonne page !

La première chose à savoir est que Kraken-Free-Dragon est en essence un noyau manipulant des expressions sous la forme d'arbres binaires et permettant la modification de ces expressions à partir d'un ensemble de règles.

Le programme complet disponible dans le répertoire git est en fait une implémentation du noyau permettant ces modifications. Nous vous présenteront sur cette page à la fois le fonctionnement du noyau et de son implémentation graphique.

Si vous savez déjà comment fonctionne le noyau et que vous voulez simplement savoir comment implémenter votre propre interface graphique, allez [ici](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Guide-de-d%C3%A9veloppement-d'une-impl%C3%A9mentation).

Le noyau
-


**L'arbre**


Le noyau a pour rôle de contenir et permettre la manipulation d'une formule sous la forme d'un arbre binaire.

Chaque nœud de cet arbre peut être : 
- Une expression primaire : un chiffre, une lettre
- Une expression unaire : des parenthèses, un non logique
- Une expression binaire : un plus, une barre de division

Ce qui rend chacun de ces type d'expression unique est le nombre de sous expression que chacun contient. En effet : 
- Une expression primaire ne contient pas de sous arbre
- Une expression unaire contient un seul sous arbre
- Une expression binaire contient deux sous arbre

Ces différents types sont implémentés par les classes model.PrimaryExpression, model.UnaryExpression et model.BinaryExpression. Toutes ces classes implémentent la classe model.Expression.

Sur ce modèle, on peut facilement représenter des objets complexes comme des équations ( 2 + 3 * sqrt ( 9 / 3^5 ) par exemple ), mais aussi et pourquoi pas des plateaux pour jouer au morpion.

Afin de manipuler facilement l'arbre de son expression, le noyau propose l'objet model.KrakenTree qui sert de racine à l'arbre de l'expression.

**Les règles**

Afin de pouvoir modifier l'arbre précédemment défini, on se propose l'objet model.Rule.

Cet objet représente une règle qui s'applique sur une arbre. Voici son fonctionnement : 
1. La règle possède un modèle d'entrée : il s'agit d'une expression sous forme d'arbre qui sert de modèle à tout arbre sur lequel on veut appliquer la règle. Par exemple, dans la règle : "1 + 1 => 2", "1 + 1" est le modèle. Tout arbre soumis à cette règle doit donc être réductible à l'arbre "1 + 1".
2. La règle possède ensuite un modèle de sortie : il s'agit d'une autre expression donnant le résultat de la règle. Par exemple, dans la règle "1 + 1 => 2", "2" est le modèle de sortie.
3. Afin de rendre les règles intéressantes, on se donne un nouveau type d'expression primaire : le type EXPRESSION. Ce type est très spécial puisqu'il permet d'englober des sous arbres lors de l'application de règles. Par exemple, dans la règle "A + A => 2 x A", les modèles d'entrée "A + A" et de sortie "2 x A" utilisent tout deux le primaire de type EXPRESSION "A". Il permet de rendre général l'utilisation des règles.

Exemples d'application de règles : 

Soit la règle n°1 : "1 + 1 => 2"
- L'application de 1 sur "1 + 1" donne "2".
- L'application de 1 sur "1 + 2" ne donne rien, car l'expression et le modèle d'entrée sont différents.

Soit la règle n°2 : "A + A => 2 x A"
- L'application de 2 sur "1 + 1" donne "2 * 1", avec A = "1"
- L'application de 2 sur "(3 + 2) + (3 + 2)" donne "2 x (3 + 2)", avec A = "(3 + 2)"
- L'application de 2 sur "(3 + 2) + (4 + 9)" ne donne rien, car A ne peut pas être "(3 + 2)" et "(4 + 9)" à la fois

Soit la règle n°3 : "(A + B) x C => A x C + B x C"
- L'application de 3 sur "(9 + (4 + 3)) x 65" donne "9 x 65 + (4 + 3 ) x 65" avec A = "9", B = "(4 + 3)" et C = "65"

Ces règles peuvent s'appliquer à partir de n'importe quel nœud de l'arbre, tant que l'expression issue de ce nœud correspond bien au modèle d'entrée de la règle.

Enfin, il est important de noter que chaque règle est associée avec un type de règle : ce type est utile lors de l'utilisation de l'interface, pour départager, par exemple, quelle règle s'applique à la pression d'un clic gauche, ou d'un clic droit.

Si vous souhaitez lire plus sur le fonctionnement de l'application d'une règle, lisez [ceci](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Fonctionnement-du-noyau-:-application-d'une-r%C3%A8gle) !

La grammaire
-

Afin de ne pas avoir à rentrer dans le code la liste des règles ainsi que les formules que l'on manipule, l'équipe à développé un outil de parsing en utilisant JavaCC. Ce dernier permet de lire directement depuis un flux de caractère une liste d'opérateurs, qui une fois interprétés, permettent de lire une liste d'expressions et de règles qui utilisent ces opérateurs.

Si vous ne connaissez pas le parsing, la partie suivante risque d'être difficile à comprendre. Nous vous conseillons de vous renseigner avant de progresser plus loin.

Le projet rend disponible dans le package model.initialisation un parseur permettant de lire une liste d'opérateur (voir [ici](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Guide-d'utilisation-des-fichiers-de-configurations-%28.cfg%29) pour la syntaxe exacte). On appelle la grammaire permettant la compréhension de ce fichier G1, ou grammaire n°1.

C'est grâce à cette liste (contenue dans un fichier texte) que nous générons G2, la grammaire n°2.

Il est important de comprendre pourquoi il y a deux grammaires différentes : la première lit les opérateurs que l'utilisateur souhaite utiliser ; la seconde utilise ces opérateurs pour lire des expressions complexes.

Par exemple : utiliser le parseur G1 sur le fichier : 

LITTERAL primaire $"([a+z])+"
PLUS binaire "+" 1

Va générer un parser G2 capable de reconnaître une infinité d'expression, comme : 
- a + b
- d
- a + toto + baba
- la + grammaire + fonctionne

On combinant les bonnes définitions d'opérateurs, on est capable de créer le support nécessaire pour créer des systèmes aux règles complexes. (Voir les exemples si vous n'êtes pas convaincus !)

Pour des informations plus précises sur les packages présents dans le projet, voir [ici](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Package-model.initialisation).

L'interface
-

L'objectif de cette partie est de vous expliquer comment fonctionne un programme qui se base sur le noyau de Kraken-Free-Dragon pour permettre la manipulation d'expressions à partir de règles.

**L'initialisation**

Le premier travail du programme est de se créer une liste de règles ainsi qu'une expression sur laquelle il va travailler. Que ce soit en écrivant en dur dans le programme, ou en les lisant à partir de fichiers textes (avec les outils décrits plus haut).

**L'opération**

Ensuite, le programme doit décider où et quand effectuer des modifications. La solution la plus évidente est de suivre les entrées de l'utilisateur. C'est ce que fait notre implémentation : elle attend les inputs de souris et choisit d'influencer l'arbre en fonction.

**Le rafraichissement**

Après avoir manipulé l'arbre, il est important d'en ré-afficher l'état.

Pour plus de détails sur le code de l'implémentation, voir [ici](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Package-view.implementation) et [ici](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Package-Controller).

Pour plus de détails sur comment implémenter un programme sur le noyau, passer [ici](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Guide-de-d%C3%A9veloppement-d'une-impl%C3%A9mentation).