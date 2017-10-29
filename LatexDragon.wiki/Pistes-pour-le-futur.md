Kraken-Free-Dragon n'est pas un projet parfait. Parmi les fonctionnalités prévues, certaines n'ont pas vu le bout du jour. Voici une liste de certaines d'entre elles : 

- Pour l'instant il n'existe que des opérateurs binaires, unaires et primaires. La manière dont fonctionnent les opérateurs binaire rend difficile la gestion pour l'utilisateur de certaines situation, comme `a + b + c + d` comme il devient difficile de distinguer la forme de l'arbre. La solution serait de permettre une visualisation plus claire de la forme de l'arbre dans l'interface, ou plus radicalement de créer un nouveau type d'expression, l'expression n-aire, faite pour se comporter comme un ensemble de deux ou plus sous arbres.
- La gestion des regex n'est pas parfait et nécessiterait une amélioration. Par exemple, l'opérateur `LITTERAL primaire §"([a-z])+"` reconnait bien `toto` et `baba` comme étant des littéraux, mais l'on est incapable pour une raison inconnue de reconnaître `toto =(§left_clic)=> baba` comme s'appliquant au littéral `toto` et seulement à ce littéral.
- Il serait intéressant de pouvoir spécifier le type d'une expression généralisée lorsque l'on écrit une règle. Par exemple, écrire `NOMBRE:A + NOMBRE:B <=(§drag_and_drop)=> NOMBRE:B + NOMBRE:A` forcerait la règle d'associativité du plus à ne fonctionner que pour des nombres.
- Il serait bon de pouvoir créer des règles qui empêchent l'application d'autres règles. Dans l'exemple du morpion, la règle qui permet de confirmer la victoire arrive toujours en parallèle de celle qui ignore la victoire en temps normal ; il serait plus pertinent de pouvoir ignorer la seconde lorsque la première se propose en rajoutant des outils lors de la création des règles.
- Il serait intéressant également de revoir entièrement l'interface graphique, pour permettre une interface plus amicale. On pourrait penser à une apparence plus proche du jeu DragonBox.
- Dans la même lignée, et dans le but de se rapprocher de DragonBox, il serait intéressant de permettre d'effectuer des règles en cascade ; l'exemple le plus simple étant le morpion, où jouer un tour demandait plus de trois ou quatre clics.


### Petits bugs
- Left click does not wait for release and thus preempts DnD
- For some reason config_simple/ will not allow for (a) as its starting formula; parenthesis seem buggy in this config

### Ajout
- (PA: reprendre lect. model/memory)
- Se passer des .sh pour être plus lisible et plus portable.
- Séparer les questions d'applicabilité, du modèle lui-même
- Clique droit
- Cibler points de départ et arrivée pour savoir quelle règle appliquer en DnD
- History, Undo
- GUI Latex
- Ajout de regle pendant jeu (théorèmes) avec marqueurs de controle pour la réinvoquer
- visualisateur/editeur des règles courantes
- invocation d'algorithmes de calcul e.g. sagemath
- unify modulo AC, i.e. rewriting done by CIME
- just have n-ary?
- keyboard enter formulae in current grammar for init or bothsides sum or...
