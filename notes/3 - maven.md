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

## Structure

Maven applique le principe de *convention over configuration* : lorsqu'un projet respecte une organisation connue, il n'a pas besoin de déclarer chaque chemin dans le POM.

Le dossier `src/main/java` contient les sources Java de l'application. `main` désigne le contenu livré avec l'application et `java` la racine des packages Java.

Le dossier `src/main/resources` contient les ressources de l'application. Maven les copie dans `target/classes`, puis les inclut dans l'artefact final.

Le dossier `src/test/java` contient les sources Java des tests. Maven les compile dans `target/test-classes`. Elles servent pendant le build, mais ne sont pas incluses dans le JAR de l'application.

Le dossier `src/test/resources` contient les ressources utilisées uniquement par les tests.

`src`, `main`, `test`, `java` et `resources` sont des dossiers Maven. Ils ne font pas partie du nom des packages Java.

Le package commence sous la racine `java`. Un fichier placé sous `src/main/java/io/example/app` appartient donc au package `io.example.app`.

Le dossier `target` contient tout ce que Maven génère : classes compilées, rapports de tests et artefacts. Il peut être supprimé et reconstruit, il ne doit donc pas être versionné.

Cette structure indique à Maven où trouver chaque type de fichier. Reste à déterminer dans quel ordre les traiter. Cet ordre est défini par le cycle de vie. Section suivante.

## Cycle

Maven organise le build en cycles de vie. Un cycle est une suite ordonnée de phases.

Une commande visant une phase exécute cette phase et toutes celles qui la précèdent dans le même cycle. `mvn package` ne lance donc pas uniquement `package` : il parcourt le cycle principal depuis `validate` jusqu'à `package`.

Maven possède trois cycles intégrés :

- `clean` : supprimer les résultats d'un ancien build ;
- `default` : construire, tester et publier le projet ;
- `site` : produire la documentation du projet.

Le cycle `clean` contient notamment :

- `pre-clean` : point d'extension avant le nettoyage ;
- `clean` : supprimer le dossier de build, généralement `target` ;
- `post-clean` : point d'extension après le nettoyage.

Le cycle `default` traverse les phases suivantes :

- `validate` : vérifier que le modèle du projet peut être utilisé ;
- `initialize` : préparer des propriétés ou fichiers nécessaires au build ;
- `generate-sources` : générer des sources supplémentaires ;
- `process-sources` : traiter les sources avant compilation ;
- `generate-resources` : générer des ressources ;
- `process-resources` : copier les ressources principales dans `target/classes` ;
- `compile` : compiler les sources principales dans `target/classes` ;
- `process-classes` : traiter les classes principales compilées ;
- `generate-test-sources` : générer des sources de test ;
- `process-test-sources` : traiter les sources de test ;
- `generate-test-resources` : générer des ressources de test ;
- `process-test-resources` : copier les ressources de test dans `target/test-classes` ;
- `test-compile` : compiler les tests dans `target/test-classes` ;
- `process-test-classes` : traiter les tests compilés ;
- `test` : exécuter les tests unitaires ;
- `prepare-package` : préparer le contenu à empaqueter ;
- `package` : produire l'artefact, par exemple un JAR ;
- `pre-integration-test` : préparer l'environnement des tests d'intégration ;
- `integration-test` : exécuter les tests d'intégration configurés ;
- `post-integration-test` : arrêter et nettoyer leur environnement ;
- `verify` : vérifier que l'artefact respecte les contrôles configurés ;
- `install` : copier l'artefact et son POM dans le dépôt Maven local ;
- `deploy` : publier l'artefact dans un dépôt Maven distant.

Toutes ces phases existent, mais plusieurs ne font rien tant qu'aucun outil ne leur est attaché.

La commande `mvn compile` parcourt le cycle jusqu'à la compilation principale.

La commande `mvn test` compile les sources principales et les tests, puis exécute les tests unitaires.

La commande `mvn package` exécute également les tests puis produit l'artefact. Elle ne lance pas l'application.

La commande `mvn verify` va plus loin et exécute les contrôles configurés après l'empaquetage.

La commande `mvn install` ajoute l'artefact au dépôt local afin que d'autres projets de la machine puissent l'utiliser.

La commande `mvn deploy` publie l'artefact dans un dépôt distant partagé.

`clean` appartient à un cycle différent. La commande `mvn clean package` exécute d'abord le cycle `clean` jusqu'à `clean`, puis le cycle `default` jusqu'à `package`.

`mvn package` conserve le dossier `target` existant. `mvn clean package` le supprime avant de tout reconstruire. Un build propre est particulièrement utile après la suppression ou le déplacement de sources et dans les environnements d'intégration continue.

Une phase définit un moment du build, mais elle ne réalise pas elle-même le travail. Les actions concrètes sont fournies par les objectifs de plugins attachés à cette phase. Section suivante.

## Plugin

Maven fournit le moteur du build, mais les actions concrètes sont réalisées par des plugins.

Un plugin est un JAR contenant un ou plusieurs objectifs, appelés *goals*. Chaque objectif représente une action précise.

Exemples :

- `clean:clean` supprime le dossier de build ;
- `resources:resources` copie les ressources principales ;
- `compiler:compile` compile les sources principales ;
- `compiler:testCompile` compile les tests ;
- `surefire:test` exécute les tests unitaires ;
- `jar:jar` construit un JAR.

Une phase et un objectif ne sont pas la même chose.

Une phase indique **quand** une action doit avoir lieu. Un objectif indique **quelle** action doit être exécutée.

Pour un projet dont le packaging est `jar`, Maven attache par défaut certains objectifs aux phases :

- `process-resources` → `resources:resources` ;
- `compile` → `compiler:compile` ;
- `process-test-resources` → `resources:testResources` ;
- `test-compile` → `compiler:testCompile` ;
- `test` → `surefire:test` ;
- `package` → `jar:jar`.

Une phase peut n'avoir aucun objectif, ou en recevoir plusieurs. Un plugin peut également attacher ses objectifs à de nouvelles phases.

Un objectif peut être lancé directement avec une commande comme `mvn compiler:compile`. En pratique, on préfère généralement demander une phase comme `mvn compile`, afin que Maven exécute aussi toutes les étapes précédentes nécessaires.

Les plugins du projet sont configurés dans la section `build` puis `plugins` du POM.

Comme un projet, un plugin possède un `groupId`, un `artifactId` et une `version`. Fixer explicitement sa version améliore la reproductibilité : les développeurs et la CI utilisent alors le même outil.

La section `configuration` transmet des paramètres au plugin. Le plugin JAR peut par exemple recevoir le nom de la classe principale à écrire dans le manifeste.

Maven n'intègre pas tous les plugins dans son installation. Il les télécharge selon les besoins, ce qui leur permet d'évoluer indépendamment du moteur Maven.

Pour télécharger un plugin, Maven doit savoir où le chercher et où le conserver localement. C'est le rôle des dépôts. Section suivante.