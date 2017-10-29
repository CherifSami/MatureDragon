Développement du serveur

# Précision sur le serveur

Le serveur utilise TomcatApache ainsi que l'api Jersey il est peut être intéressant d'aller faire un tour [ici](http://tomcat.apache.org/tomcat-7.0-doc/index.html) 

# S'y retrouver dans le code

Hormis la branche TOM toutes les sources du programme ce trouve dans le dossier src/main/java/libreDragon/
une explication de la composition de ces sources ce trouve [ici](https://github.com/huacayacauh/LatexDragon/wiki/Architecture-du-serveur). 
Donc si vous voulez ajouter ou modifier le comportement des requêtes vous devez vous orienter vers le package api. Par contre si vous voulez modifier la génération de l'objet graphique là il faudra aller dans le package latexParser. Pour la lecture des fichier de configuration comme le fichier de règles vous devez vous tourner vers le package ruleParser. Et enfin si vous voulez modifier le comportement ou la façon de traiter les expression en mémoire il faudra aller jusqu'au package model.

# Ajouts d'une requête 

L'ajout d'une requête est plutôt simple. Pour cela il suffit de créer une classe dans le package apide la forme suivante : 

````
import javax.ws.rs.GET;
import javax.ws.rs.POST;
import javax.ws.rs.Path;
import javax.ws.rs.PathParam;
import javax.ws.rs.Produces;
import javax.ws.rs.core.MediaType;

@Path("/monurl")
public class requete {

    @GET
    @Path("/{id}")
    @Produces()
    public String answer( @PathParam("id") int id ) {
        return "Mon message lié a l'id";
    }    
}
````
Cette classe représente une requête disponible a l'url : http://localhost:8080/LibreDragon/api/monurl . Elle nécessite un argument passer a l'aide de l'url par exemple si le client fais la requête http://localhost:8080/LibreDragon/api/monurl/5 id sera égal à 5. Vous n'avez plus cas prévoir un traitement dans la méthode answer. 

On peut retrouver un tutoriel plus complet qui explique même comment faire pour implémenter son propre serveur [ici](http://www.supinfo.com/articles/single/1498-creer-une-api-java-avec-jersey-jackson).
