## Le package Controller:

C'est ici que sont implémentées les méthodes qui gèrent les événements de l'application, à savoir: les clicks de souris (droite, gauche, double click) ainsi que le DragAndDrop.

### *MouseEventManager
Vous trouverez dans ce pakage les classes qui définissent les méthodes de gestion des événements souris en fonction des éléments graphiques, ainsi UnaryMouseEventManager définit la gestion des événements souris pour les expressions unaires. Chacune de ces classes implémente la classe abstraite MouseEventManager.

### *DragAndDropManager
Vous trouverez dans ce package les classes qui définissent les méthodes de gestion des événements souris pour le DragAndDrop en fonction des éléments graphiques ainsi BinaryMouseEventManager définit la gestion des événements souris pour les expressions binaires. Chacune de ces classes implémente la classe abstraite DragAndDropManager.

La classe (static) DragAndDropMemory sert de mémoire cache pendant le DragAndDrop de nos expressions. 
Exemple: lors d'un DragAndDrop de A sur B, les informations relatives aux objets A et B sont stockées dans ce fichier static, afin d'assurer que le DragAndDrop se passe comme prévu.
