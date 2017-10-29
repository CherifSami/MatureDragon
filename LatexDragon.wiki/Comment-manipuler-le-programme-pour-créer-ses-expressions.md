Si vous êtes sur cette page, c'est que vous cherchez à savoir le protocole permettant de démarrer Kraken-Free-Dragon avec ses propres opérateurs et expressions !

En premier lieu, il est important de savoir si le programme dispose de tous les opérateurs que vous désirez. Pour en créer de nouveaux, lisez la partie suivante.

Créer de nouveaux opérateurs
-

Afin de créer de nouveaux opérateurs, il vous faut modifier le fichier config/operators.cfg.
Pour comprendre la syntaxe de ce fichier, lisez [ceci](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Guide-d'utilisation-des-fichiers-de-configurations-%28.cfg%29).

Vous pouvez ici rajouter ou enlever des opérateurs à votre guise.

**NOTE IMPORTANTE 1 :** Vous devez fermer le programme, puis le recompiler (instructions [ici](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Recompilation-du-programme)) à chaque modification du fichier config/operators.cfg, afin que les changements soient pris en compte. Si une erreur survient, revoyez la syntaxe de votre fichier.

**NOTE IMPORTANTE 2 :** Pour chaque opérateur non primaire que vous créez, vous devez rajouter une ligne correspondante dans graphics.cfg, ou votre programme ne se lancera pas ou plantera lorsque cet opérateur tentera d'apparaître à l'écran. Pour plus de détails, voir [ici](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Guide-d'utilisation-des-fichiers-de-configurations-%28.cfg%29).

Après avoir créé vos opérateurs, vous pouvez décrire les règles qui les régissent.

Créer de nouvelles règles
-

Créer des règles est plus intuitif que de créer des opérateurs. Pour se faire vous pouvez rajouter des lignes dans le fichier config/rules.cfg. Pour la syntaxe exacte, voir [ici](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Guide-d'utilisation-des-fichiers-de-configurations-%28.cfg%29).
Vous pouvez rajouter des règles ou en enlever.

Note : la modification des règles ne nécessite pas la recompilation du programme. Vous devez cependant le redémarrer pour que les changements soient effectifs. Au cas où une erreur de syntaxe s'est glissée dans le fichier config/rules.cfg, le programme ne se lancera pas.

Une fois que vous disposez de vos règles, il est important de définir avec quelle expression le programme débutera.

Définir la formule de base
-

Encore plus simple que les opérations précédentes, il s'agit ici de n'écrire qu'une seule expression dans le fichier config/formula.cfg. Voir toujours [ici](https://github.com/Demonagon/Kraken-Free-Dragon/wiki/Guide-d'utilisation-des-fichiers-de-configurations-%28.cfg%29) pour la syntaxe.