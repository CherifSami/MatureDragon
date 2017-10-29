###Le fichier clear.sh
Permet de supprimer les classes qui sont générées automatiquement par javacc.

###Specification.java
Une spécification est le descriptif d'une expression de différents types (primaire,unaire,binaire).
Specification.java est une interface qui est implémentée par SpecificationPrimaire, SpecificationUnaire et SpecificationBinaire.

###SpecificationPrimaire.java
Une spécification primaire représente un littéral (un nombre, une variable...) et est donc représentée par son nom (name) et une expression réguliere (RegEx). 



###SpecificationUnaire.java
Une spécification unaire représente un opérateur qui s'applique sur une unique expression et est donc représentée par son nom (name), son symbole gauche (leftSymbol) si il existe et son symbole droit (rightSymbol) si il existe.
Par exemple les parenthèses sont unaires tout comme l'opérateur factoriel ( ! en temps que symbole droit, pas de symbole gauche ) ou encore l'opérateur not ( ! en temps que symbole gauche, pas de symbole droit ).


###SpecificationBinaire.java
Une spécification binaire représente un opérateur qui s'applique sur deux expressions et est représentée par son nom (name), son symbole (symbol) et sa priorité (priority). La priorité d'un opérateur binaire le situe par rapport aux autres opérateurs et permet de construire l'arbre correctement. Par exemple, l'opérateur PLUS a une priorité plus faible que l'opérateur FOIS, car en mathématiques le fois l'emporte sur le plus. 

###GenerGrammarRules.java
Cette classe nous permet de générer automatiquement grammaire2.jj, à partir des opérateurs définis via operators.cfg et interprétés par grammaire1.jj.
grammaire2.jj est la grammaire qui s'occupera de reconnaître une expression bien formée. 

###Main.java
Le Main nous permet de lire le résultat de grammaire1.jj, et de le donner à GenerGrammarRules, ainsi que de remplir notre liste de configurations de règles.