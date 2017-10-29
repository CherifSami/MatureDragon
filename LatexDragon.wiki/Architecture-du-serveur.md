# Architecture du serveur

Le serveur se compose de 5 module dont deux fortement lié.

## Model
Le package model contient le « backend » du serveur c’est à dire le système de gestion d’équation.
Ce système permet de représenter en mémoire une équation et d’appliquer sur celles- ci des règle de réécriture définis par l’utilisateur. Vous trouverez plus d’information sur le sytème d’équation et sur l’application de règles saisie par l’utilisateur [ici](https://github.com/huacayacauh/LatexDragon/wiki/Fonctionnement-du-projet).

## LatexParser
Ce module permet au serveur de générer des objet graphique à partir des expressions obtenus avec le module Model. Il permet de faire le pont entre des expressions représenté en mémoire dans le serveur et une chaîne de caractères compréhensible par MathJax.

![GenerateExpression](https://drive.google.com/uc?export=view&id=0BwI3BqLCkW55b1Y3M0dvZ2I3b3c)
 
## RuleParser
Le RuleParser quand à lui permet de lire des expressions à partir de fichier de configuration généralement situé dans config/. Il est donc utilisé dans la lecture de formule jouable ou bien dans la génération des règles de réécriture. 

## GenerateRuleParser
Le package GenerateRuleParser permet de créer la grammaire du rule parser. Cette grammaire sera utilisé pour générer le package RuleParser grâce à javacc.

## Api
Le serveur dispose d'un système de sessions représentant chaque partie en cours et donc permet aussi a plusieurs clients de se connecter au serveur en même temps et chacun disposant d'une partie indépendante.

Api est le module qui concentre les données du serveur ainsi que toutes les classes servant à traiter les requêtes du client.
Le centre de ce module est la classe Data qui s'occupe de la gestion des sessions on peut voir comment sont gérer les données du serveur sur lze schéma suivant. Ensuite les classes ApplyRule, GameState, CreateTheorem, FormulaList, RulesList, ServerStatus, Resume et Start contiennent les méthodes s'occupant de réceptionner les requêtes du client et les traiter (pour plus d'info sur les [requêtes](https://github.com/huacayacauh/LatexDragon/wiki/Requ%C3%AAtes-côt%C3%A9-Serveur)).
![Données du Serveur](https://drive.google.com/uc?export=view&id=0BwI3BqLCkW55b0pNVmNhZm9vYms)
