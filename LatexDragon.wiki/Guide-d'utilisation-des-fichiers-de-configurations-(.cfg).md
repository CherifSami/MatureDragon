Notre projet comporte des fichiers de configurations permettant de créer ses propres opérateurs et règles.
Ces fichiers se trouvent dans le répertoire config.

### Comment remplir operators.cfg :
Vous devez donner le type de l'opérateur (Primaire, Unaire ou Binaire, écrit comme cela) puis, séparé par un espace, vous devez donner un nom à votre opérateur (en majuscules et composé de plus d'une lettre) .
Si vous donnez le type Primaire vous devez le faire suivre d'une expression regulière commençant par un $.

Primaire LITTERAL $(["a"-"z"])+	

Si vous donnez le type Unaire vous devez le faire suivre d'un symbole gauche (si il existe) et d'un symbole droit (si il existe) écrit entre guillemets. Si le symbole est inexistant, écrire "". 

Unaire SQRT "sqrt" ""

Si vous donnez le type binaire vous devez le faire suivre d'un unique symbole, toujours entre guillemets, puis d'un nombre qui determinera la priorité de l'opérateur.  

Binaire PLUS "+" 3

### Comment remplir graphics.cfg
Pour chaque opérateur unaire et binaire déclaré dans operators.cfg, il doit exister une description de sa représentation graphique dans graphics.cfg. Reprenons l'exemple du PLUS. Dans graphics.cfg, on aura par exemple la ligne suivante : 
PLUS h "+" ""
Selon que l'opérateur est défini en tant que binaire ou unaire, le(s) symbole(s) donné(s) se placera(ont) au milieu, avant, ou après l'expression. 
Le h (respectivement le v) détermine le placement de l'opérateur vis à vis de l'expression, c'est à dire qu'il sera placé de façon horizontale (resp. verticale). Voici un exemple pour le placement vertical : 
DIVIDE v "-" ""

### Comment remplir rules.cfg
Le fichier rules.cfg comporte une règle par ligne.
Une règle se définie par une expression qui se transforme en une autre expression par le biais d'une "action".
Une expression générique peut s'écrire avec une lettre majuscule.
A =(§left_click)=> A + 1  
- L'opérateur =(§action)=> signifie que l'on remplace l'expression de gauche par celle de droite par le biais d'une certaine action.
- L'opérateur <=(§action)=> signifie que l'on peut remplace l'expression de gauche par celle de droite par le biais d'une certaine action, ou l'inverse, c'est à dire qu'on peut également remplacer celle de droite par celle de gauche par le biais de l'action décrite.

Les actions possibles dans notre implémentation sont : 
- (§left_click)
- (§right_click)
- (§double_left_click)
- (§drag_and_drop)

### Comment remplir formula.cfg
Dans formula.cfg, il faut donner une expression bien formée, qui sera l'expression de départ au lancement de l'application.  