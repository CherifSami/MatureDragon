# Qu'est-ce que LatexDragon ?
Le projet est une application open source initialement nommée Kraken-Free-Dragon et développée en java. L’application a ensuite été reprise par l'équipe Master One Incorporate pour améliorer son interface et ses fonctionnalités. La version actuelle de l'application est nommée Latex Dragon. Le jeu permet de manipuler des équations mathématiques et les théorèmes qui y sont liés à savoir l'associativité, la factorisation et bien d’autres. L’utilisateur peut s’en servir pour résoudre des équations mathématiques et toutefois créer un ensemble de règles.

# Les objectifs du projet

En ce basant sur le projet [Kraken-Free-Dragon](https://github.com/pja35/Kraken-Free-Dragon) l'objectif de ce projet est de développer une interface en Latex, via MathJax, en JavaScript. Le but de ce projet est de reprendre Kraken-Free-Dragon et proposer une GUI plus travaillé que la GUI rudimentaire du projet de base.

# Outils utilisé

LatexDragon est divisé en 2 application, un serveur et un client.

Le client utilise le framework [electron](https://electron.atom.io) permettant de développer une application de bureau en utilisant les technologies du web (javascript, html, css). Le client utilise aussi les api [Bootstrap](https://getbootstrap.com/), [jQuery](https://jquery.com/) et [MathJax](https://www.mathjax.org/).

Le serveur est un serveur REST en java utilisant [Apache Tomcat](https://tomcat.apache.org/) et [Jersey](https://jersey.java.net/).
