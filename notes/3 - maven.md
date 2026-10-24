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

## POM

Le POM (*Project Object Model*) est la description déclarative d'un projet Maven. Il se trouve dans le fichier `pom.xml`, à la racine du projet.

Le POM ne décrit pas une suite de commandes. Il décrit ce que le projet est, ce dont il dépend et comment il doit être construit. Maven détermine ensuite les actions à exécuter.

`modelVersion` indique la version du modèle POM. La valeur `4.0.0` ne correspond pas à la version de Maven.

Un projet est identifié par trois coordonnées :

- `groupId` : organisation ou espace de noms propriétaire ;
- `artifactId` : nom du projet ;
- `version` : version de l'artefact produit.

L'ensemble `groupId:artifactId:version` identifie précisément un artefact dans l'écosystème Maven.

Le suffixe `SNAPSHOT` désigne une version encore en développement et dont le contenu peut changer. Une version publiée sans ce suffixe est considérée comme immuable.

`packaging` indique le type d'artefact à produire. S'il est absent, Maven utilise `jar`.

La section `properties` centralise des valeurs utilisées pendant le build. `maven.compiler.release` définit la version Java ciblée et `project.build.sourceEncoding` définit l'encodage des sources.

Maven combine ce POM avec ses valeurs par défaut pour former le *POM effectif* réellement utilisé pendant le build.

Le POM n'a pas besoin d'indiquer chaque chemin lorsque le projet respecte l'organisation standard de Maven. Cette organisation constitue la convention du projet. Section suivante.