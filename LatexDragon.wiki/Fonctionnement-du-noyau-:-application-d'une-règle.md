Si vous êtes sur cette page, c'est que vous cherchez à savoir précisément comment fonctionne l'application d'une règle avec le noyau de Kraken-Free-Dragon.

Ce processus est relativement complexe et est découpé en plusieurs étapes.

On rappelle qu'une règle est composée d'un modèle d'entrée et d'un modèle de sortie (ou modèle de résultat).

Voici un exemple de règle : 

`A + A => 2 * A`

Cette règle, appliquée à `(a + 3) + (a + 3)`, donne `2 * (a + 3)`.

Voyons maintenant comment cela fonctionne dans le projet.

Note : dans cette page nous supposerons que vous êtes au clair avec tout ce qui se trouve sur [cette](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Fonctionnement-du-projet) page. Soyez sûrs de l'avoir consultée !

1) Construction du contexte
-

Il est important, avant de connaître les mécanismes précis de l'application d'une règle, de savoir qu'une règle s'applique toujours sur un nœud unique.

Le nœud cible de l'action est appelé contexte d'application. La règle va oublié temporairement le reste de l'arbre de l'expression pour se concentrer sur ce sous-arbre précis.

Lorsque l'on clique sur une expression dans Kraken-Free-Dragon, le contexte est assez simple à trouver : il suffit de prendre le nœud qui correspond au nœud graphique sur lequel on a cliqué. Cependant, dans le cas d'une action multi-nœud comme un cliqué glissé, il est important de choisir dans tout les cas un contexte unique qui représente fidèlement les intentions de l'utilisateur.

Dans le cas où plusieurs noeuds sont la cible d'une action, le noyau procècde à trouver <b>le noeud le plus bas de l'arbre qui soit racine du sous-arbre contenant tout les noeuds cibles</b>.

Autrement dit, il s'agit de trouver le sous-arbre qui englobe tout les noeuds ciblés, puis d'appliquer la règle au contexte de ce sous-arbre ; c'est à dire à sa racine.

Pour trouver un tel contexte, on génère ce qu'on appelle un root_path pour chaque noeud cible. Un root_path est tout simplement la liste de tout les noeuds qui constituent le chemin vers le noeud cible depuis la racine de l'arbre.

Un exemple : soit l'expression `(a + b) + c`

Ici, la racine est le "+" entre la parenthèse et c.

Le root_path de a est : racine -> plus -> parenthèse -> plus -> a

Le root_path de b est : racine -> plus -> parenthèse -> plus -> b

Le root_path de c est : racine -> plus -> c

Une fois les root_path des noeuds cibles (et uniquement des noeuds cibles) trouvés, il faut générer la sous partie la plus grande possible, commune à tout ces root_path. Cette sous-partie est appelée partie commune.

Dans l'exemple précédent, le root_path commun entre a et b est : 

root_path (a & b) : racine -> plus -> parenthèse -> plus

Puisque la partie a et b n'est pas en commun. De la même manière, on peut générer le root_path commun entre trois nœuds ou plus : 

root_path (a & b & c) : racine -> plus

Une fois cette partie commune déterminée, il suffit d'en prendre le dernier élément. Ce dernier élément est la racine la plus basse englobant tout les nœuds cibles.

Dans notre exemple `(a + b) + c`, le root_path commun de a et b est racine -> plus -> parenthèse -> plus. Ce qui signifie que le noeud le plus bas englobant a et b ensemble est le plus présent dans la parenthèse. Le sous arbre construit à partir de ce noeud est `a + b`. Le contexte est trouvé.

2) Vérification syntaxique
-

Maintenant nous disposons d'un contexte précis. Reprenons l'exemple précédent et supposons que nous effectuons une action sur a et b. Le contexte est donc `a + b`.

La première chose à faire pour appliquer une règle sur ce contexte est de vérifier si la règle s'applique syntaxiquement.

Prenons pour notre exemple la règle `A + B => B + A` qui exprime la commutativité de l'opérateur plus.

La vérification syntaxique consiste à vérifier si le contexte peut se réduire structurellement au modèle d'entrée du nœud.

Ici, il est assez simple de voir que `a + b` se réduit facilement à `A + B`. A et B sont des expressions généralistes ; elles expriment l'existence d'un sous arbre qui est ignoré pour l'utilisation de la règle. De fait, ce modèle s'applique autant à `a + b` qu'à `(a + b) + (z + y)` car on suppose à cette étape que A et B peuvent se résoudre à n'importe quel sous-arbre. Cependant, l'expression `a * b` est syntaxiquement incompatible avec le modèle `A + B`, ces expressions étant structurellement différentes.

3) Vérification sémantique
-

Une fois que le modèle et l'expression correspondent structurellement, il faut vérifier que les réductions des sous-arbres sont cohérentes.

En effet, certaines règles réutilisent des expression généralistes pour exprimer la symétrie. Par exemple : 

La règle `A + A => 2 * A` permet de résoudre deux arbres identiques à la multiplication de cet arbre par deux.

Il a été dit dans la partie précédente que les expression généralistes peuvent se résoudre à n'importe quel sous arbre ; il est ici important de vérifier malgré tout qu'une même expression généraliste est toujours réduite au même sous arbre.

Pour se faire, on dispose d'une mémoire qui va enregistrer les sous arbres qui se réduisent pour chaque expression généraliste. Si on essaye d'affecter une même expression généraliste à deux arbres différents, l'expression est invalide sémantiquement avec le modèle.

Par exemple pour la règle `A + A => 2 * A`, l'expression `a + b` est incompatible sémantiquement car A ne peut pas être a et b en même temps. Cependant, l'expression `c + c` est correcte, ainsi que l'expression `(3 + 9^5) + (3 + 9^5)`, par exemple.

Ainsi dans notre exemple récurrent de la règle `A + B => B + A` au contexte `a + b`, le contexte est sémantiquement compatible avec le modèle, avec A = a et B = b.

4) Application sur le modèle de sortie
-

Cette dernière étape est très simple une fois que l'on a constitué la mémoire de vérification sémantique.

En effet on se retrouve avec une liste qui affecte toutes les expressions généralistes à des sous-arbres précis.

Il suffit simplement de prendre de modèle de sortie de la règle, et de remplacer toutes les expression généralistes par leurs équivalents en mémoire s'il existe.

Par exemple, pour la règle `A + B => B + A` sur le contexte `a + b`, on a établit la mémoire suivante : 
- A = a
- B = b

La réécriture du modèle de sortie `B + A` sur cette mémoire donne `b + a`. On a simplement remplacé toutes les expressions généralistes par leurs équivalents.

Ainsi, l'application de `A + B => B + A` sur l'expression `a + b` donne `b + a`.

5) Remise dans le contexte général
-

Maintenant que l'on applique la règle à un contexte précis, il est important de savoir remettre le résultat dans le contexte général.

Dans notre exemple, il s'agissait à la base d'effectuer la règle `A + B => B + A` en ciblant a et b dans l'expression `(a + b) + c`. En ayant établit le contexte `a + b` pour la règle, on obtient le résultat `b + a`. On doit maintenant remplacer le contexte dans l'expression par le résultat de la règle, ce qui donne `(b + a) + c`.

Voici un résumé de l'exemple : 
- Soit l'expression `(a + b) + c`
- Soit la règle `A + B => B + A`
- On cible (a, b), ce qui donne le contexte `a + b`
- On vérifie syntaxiquement le contexte `a + b` et le modèle d'entrée `A + B`, -> OK
- On vérifie sémantiquement le contexte `a + b` et le modèle d'entrée `A + B`, -> OK avec A = a, et B = b
- On récupère la mémoire que l'on vient de construire et on l'applique au modèle de sortie. On obtient `b + a`
- On remplace l'ancien contexte par le résultat dans l'expression : `(b + a) + c`