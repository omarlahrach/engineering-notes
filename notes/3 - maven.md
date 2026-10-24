# Maven

## Build

Un *build* est la transformation des sources d'un projet en un artefact prêt à être exécuté ou livré.

Pour une application Java, cette chaîne comprend notamment :

1. nettoyer les anciens fichiers générés ;
2. copier les ressources ;
3. compiler les sources en `.class` ;
4. compiler et exécuter les tests ;
5. regrouper le résultat dans un JAR.

Cette chaîne peut être réalisée manuellement avec les outils du JDK. Elle devient cependant répétitive et fragile lorsque le nombre de sources, de tests et de bibliothèques augmente.

Maven est un outil de build. Il décrit le projet, applique une structure commune et automatise sa construction.

Pour construire le projet, Maven doit d'abord savoir où se trouvent ses sources, quelle version de Java utiliser et quelle identité donner à l'artefact. Ces informations décrivent le projet. Section suivante.