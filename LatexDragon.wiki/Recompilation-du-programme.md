Il faut recompiler certaines parties du programme à chaque fois qu'on veut utiliser un fichier de configuration des opérateurs different. Le fichier se trouve dans le dossier de configuration (normalement config/operators.cfg). Pour utliser une autre configuration (par example config_tic_tac_toe), on modifie la variable "configPath" dans le script de Gradle "build.gradle".

Comment recompiler ?
-
Il suffit de lancer

```
$ gradle clean
$ gradle build
```
dans la racine du projet.


Pourquoi recompiler ?
-

Afin de créer des parseurs puissants, nous utilisons la librairie JavaCC.

Celle-çi se contente de générer des fichiers .java correspondant au parseur.

Étant donné que nous sommes obligés de regénérer un parseur à chaque fois que le fichier de configuration est modifié, nous sommes contraints de recompiler ces .java en .class pour pouvoir ensuite les utiliser.