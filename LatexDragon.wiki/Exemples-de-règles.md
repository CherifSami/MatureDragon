Voici une liste descriptive des quelques exemples présents dans le projet et des consignes pour comment les tester.

Pour tester un exemple, vous devez déterminer quel dossier `config/` lui correspond (exemple, `config_tic_tac_toe/` pour le morpion), et remplacer l'actuel dossier `config/` en renommant le dossier choisit en `config/`. Puis, recompiler le programme avec `./compile.sh` à la racine du projet.

Exemple : j'ai le programme tel qu'il est quand je le télécharge depuis git.

1. Dans le dossier `FreeKraken/`, je renomme `config/` en `config_equation/`.
2. Puis, je renomme `config_tic_tac_toe/` en `config/`.
3. Enfin, je lance `./compile.sh`.
4. Mon exemple est prêt à lancer, je démarre avec `./run.sh`

Voici une liste des exemples disponibles : 

- `config/` de base, le programme est paramétré pour vous montrer une équation que vous pouvez essayer de résoudre.
- `config_simple/` contient un exemple très simple dans lequel vous pouvez cliquer sur a pour y rajouer + 1.
- `config_tic_tac_toe/` vous permet de jouer au morpion ! cliquez sur "turn" puis "applic" puis "check" pour jouer un tour.
- `config_sum/` permet de faire la somme de grand nombres. Attention, les nombres sont dans le mauvais sens !