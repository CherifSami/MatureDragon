# Qu'est-ce que LatexDragon ?
..

LatexDragon est un projet open source ayant pour but la création d'une application permettant la manipulation de formule mathématique sous la forme d'un jeu éducatif.

# Les objectifs du projet

En ce basant sur le projet [Kraken-Free-Dragon](https://github.com/pja35/Kraken-Free-Dragon) l'objectif de ce projet est de développer une interface en Latex, via MathJax, en JavaScript. Le but de ce projet est de reprendre Kraken-Free-Dragon et proposer une GUI plus travaillé que la GUI rudimentaire du projet de base.

# Outils utilisé

LatexDragon est divisé en 2 application, un serveur et un client.

Le client utilise le framework [electron](https://electron.atom.io) permettant de développer une application de bureau en utilisant les technologies du web (javascript, html, css). Le client utilise aussi les api [Bootstrap](https://getbootstrap.com/), [jQuery](https://jquery.com/) et [MathJax](https://www.mathjax.org/).

Le serveur est un serveur REST en java utilisant [Apache Tomcat](https://tomcat.apache.org/) et [Jersey](https://jersey.java.net/).
