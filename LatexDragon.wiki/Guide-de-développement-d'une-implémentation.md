Cette page contient toutes les informations qu'il vous faut pour développer vous même votre propre programme Java à partir du noyau de Kraken-Free-Dragon.

1) Import du projet
-

Votre première tâche est d'importer le projet depuis git sur votre IDE favori.

Si vous souhaiter abandonner toute l'implémentation qui a été faite par notre équipe avec javaFx, supprimez les packages : 
- view.implementation (mais pas view)
- controller

Ces packages contiennent un code d'exemple d'implémentation qui pourra vous être utile. Cependant, si vous souhaitez développer votre propre implémentation, il est nécessaire de les mettre de coté pour éviter tout conflit et alléger votre projet.

2) Implémenter une view.GraphicExpressionFactory
-

Cette interface décrit une factory qui génère les équivalents graphiques des expressions Unaires, Primaires et Binaires. Si vous ne reconnaissez pas ces termes, je vous recommande la lecture de la page explicative du fonctionnement global du programme.
En résumé, implémenter cette interface dans une classe qui sera capable de construire morceau par morceau la représentation graphique de la formule (dans notre implémentation, par le biais de Group de JavaFx).

Voici les fonctions de l'interface : 

public Object generateBinaryExpression(Expression expression, String type, Object first, Object second);
	
public Object generateUnaryExpression(Expression expression, String type, Object sub);
	
public Object generatePrimaryExpression(Expression expression, String type, String name);

Ces trois fonctions çi-dessus vous permettrons de générer les équivalents graphiques des différents types de noeuds présents dans l'arbre de la formule.

public Object generateRuleExpression(Rule rule);

Cette fonction permet de générer un type graphique particulier, celui qui correspond à une règle. Cette fonction peut ne pas vous être utile en fonction de la nature de votre implémentation. Voir plus bas.

public void init();

Cette fonction est automatiquement appelée lors de l'étape 3 et vous fournit une occasion d'initialiser les ressources éventuelles de votre factory.

3) Initialiser le moteur Kraken-Free-Dragon
-

Il est nécessaire d'initialiser le moteur au début de la durée de vie de votre programme (par exemple, au début du main).
Pour cela, créez un objet de classe model.KrakenTree. Il s'agit la classe contenant et manipulant la formule.
En appelant le constructeur KrakenTree(GraphicExpressionFactory factory) en donnant en argument la classe créée en 2), le moteur sera initialisé correctement.

Il est important de ne garder qu'une seule instance de l'objet KrakenTree, celui-çi contenant l'arbre de la formule.

4) Initialiser les règles et la formule de base
-

Si vous avez lu la page expliquant le fonctionnement du programme, vous savez qu'il est important que le noyau dispose d'un ensemble de règles.
Pour ce faire, soyez assurés d'avoir utilisé l'un des fichiers scripts dans res/model/initialisation/
Pour que la classe G2 soit bien compilée. Afin de lire les règles à partir d'un fichier texte, utiliser la fonction : 

G2.readRules(new FileInputStream(new File("mesRègles.txt")));

En remplaçant bien sûr le nom par le plus adéquat dans votre situation.

Enfin, il vous faut initialiser l'état de la formule sous traitement contenue dans votre instance de l'objet KrakenTree. Pour ce faire, utilisez la fonction : 

public void setRoot(Expression root);

Vous pouvez utiliser un objet expression pré-initialisé, où par exemple (et c'est le cas dans notre implémentation) la lire depuis un autre fichier texte afin d'en laissez le soin à l'utilisateur. Pour cela, il faut réutiliser la classe G2 de la sorte : 

Expression expr = G2.readExpression(new FileInputStream(new File("maFormule.txt")));

Cette expression peut directement être placée à la racine du KrakenTree.

5) Interagir avec la formule
-

Si vous avez lu la page décrivant le fonctionnement du programme, vous saurez que l'on interagit avec la formule du Kraken-Free-Dragon grâce à des inputs prédéfinis.
Ces inputs sont prédéfinis par l'implémentation et non par le moteur. Ce qui vous permet de définir autant de types d'inputs que vous voudrez.
Ces types doivent cependant être consistants, puisqu'ils doivent être définis proprement dans les règles (voir la page décrivant la configuration des règles).

Afin d'effectuer une action sur l'arbre, il faut d'abord savoir quelle liste de règles est applicable. Pour cela, utiliser l'une de ces fonctions : 

public static Pair<Expression, List<Rule>> processInput(String input_type, Expression expr);
public static Pair<Expression, List<Rule>> processInput(String input_type, List<Expression> exprs);

Contenues dans KrakenTree. Ces fonctions sont statiques et ne nécessitent donc pas de référence à l'objet KrakenTree.

Ces fonctions prennent en paramètres : 
- une chaîne de caractère décrivant le type l'action : dans notre implémentation cela peut être "left_click", "right_click", etc.
- Une liste des noeuds de l'arbre qui sont concernés par l'action. La première version de la fonction permet de ne pas avoir à manipuler une liste lorsqu'un seul noeud est concerné.

Ces fonctions renvoient un objet de type Pair. Cet objet contient deux autres objets, qui sont : 
- Le noeud racine sur lequel les règles s'appliquent
- La liste des règles applicables à la racine

Si la liste de règles est vide, c'est qu'aucune règle ne correspond au contexte.

Cependant, si une ou plusieurs règles sont renvoyées, vous pouvez choisir de les appliquer sur l'arbre. Pour cela, munissez vous de votre instance de la classe KrakenTree et appellez la fonction : 

public void applicRule(Expression expression, Rule rule);

En donnant en premier paramètre l'expression renvoyée dans l'objet Pair suivi en second paramètre de la règle choisie.

Bien sûr, lorsque la fonction processInput renvoie plusieurs règles possibles, il est important de faire un choix. Ce choix est laissé aux soins de l'implémentation. Dans l'implémentation présentée sur ce Git, ce choix est transféré à l'utilisateur via l'affichage des règles possibles sous forme d'une liste. C'est ici que la fonction generateRuleExpression de GraphicExpressionFactory devient utile, nous permettant d'obtenir les équivalents graphiques des règles pour les afficher à l'écran.

6) Obtenir un affichage
-

Que vous choisissiez d'afficher votre formule dans une console, dans un fichier .xml ou dans une interface graphique, il est important de pouvoir obtenir un affichage correspondant à votre formule et de pouvoir l'actualiser au fur et à mesure des modifications.

Pour générer un objet graphique correspondant à la formule contenue dans le KrakenTree, vous devez d'abord récupérer l'expression racine grâce à la fonction de KrakenTree : 

public Expression getRoot();

Puis, à partir de cet objet Expression, il est possible de générer un objet graphique avec : 

Object generateExpression();

Cette fonction renvoie un objet généralisé puisque son type dépend de votre implémentation.

Note explicative : cette fonction produit de manière récursive un objet graphique correspondant à votre arbre entier. Vous choisissez comment vos expressions binaires, unaires et primaires se transforment grâce aux fonctions de votre implémentation de l'interface GraphicExpressionFactory. Un exemple est disponible dans notre implémentation sous le nom de view.implemetation.graphicConfigurationParser.GraphicConfiguration.