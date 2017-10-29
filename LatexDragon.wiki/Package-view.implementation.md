# Ce package contient le Main qui affiche la fenêtre javafx que vous aurez à l'écran. 

## Les éléments graphiques
Chaque élément graphique que vous pourrez voir dans la fenêtre de l'application est défini dans ce package.

**UnaryGraphiqueExpression:**  Ici on définit le format visuel d'une expression unaire (factoriel, racine carrée..).

On remarque que le constructeur de cette classe possède les paramètres _decoOpen_ et _decoClose_ respectivement la décoration préfixée à l'expression, la décoration suffixée à l'expression.
Par exemple: l'opération factoriel se représente seulement avec un ! à la fin. La représentation sera donc faite avec un decoOpen vide, et un decoClose contenant "!"

De plus le paramètre _orientation_ spécifie, comme le nom l'indique, l'orientation de l'expression. Une fraction sera représenté verticalement alors qu'une addition sera horizontal.

**PrimaryGraphiqueExpression:** Ici on définit le format visuel d'une expression primaire, c'est en quelque sorte un littéral ( 'a', 'bu'..).
Cette PrimaryGraphiqueExpression servira de "brique de base" à la construction d'autres expressions plus complexes.

ex: `a + b` est une expression binaire formée de deux expressions primaires 'a' et 'b' séparées par l'opérateur '+' 
Par la suite, une expression binaire pourra servir à construire d'autres expressions binaires.

**BinaryGraphiqueExpression:** Ici, on définit le format visuel d'une expression binaire (addition, soustraction..).

Le paramètre orientation d'une expression binaire à la même fonctionnalité que pour l'expression unaire. 
Une expression binaire est formée de deux expressions séparées par un opérateur, les expressions peuvent être de type primaire, unaire ou même binaire.

**ChoiceContextMenu:** Lorsque l'on veut cliquer ou drag'n'drop sur une expression, il se peut qu'il y ait trop d'opérations possibles pour tout gérer avec la souris seulement. On définit donc ici le menu "pop-up" afin qu'il affiche des expressions et qu'il effectue des actions lors d'un clic sur chaque bouton.

**Responsive:** Ce package contient également deux fichiers css nommés: cssSmall.fxml et cssLarge.fxml.
Ces deux fichiers contiennent simplement le css de l'application. En fonction de la taille de l'écran de l'utilisateur, ou redimensionnement de la fenêtre, la feuille css correspondante est chargée par la fonction: 

`primaryStage.widthProperty().addListener(e -> {`

           `if(primaryStage.getWidth() < 600) {`
            	`scene.getStylesheets().clear();`
            	`scene.getStylesheets().add(getClass().getResource("cssSmall.fxml").toExternalForm()); `
            `}else {`
            	`scene.getStylesheets().clear();`
            	`scene.getStylesheets().add(getClass().getResource("cssLarge.fxml").toExternalForm()); `
            `}`
        `});`

Cette fonction surveille constamment tout changement de taille de la fenêtre et ajuste le css si nécessaire.