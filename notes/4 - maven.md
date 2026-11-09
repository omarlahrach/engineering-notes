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

## Dépôt

Un dépôt Maven est un stockage d'artefacts. Il ne s'agit pas d'un dépôt Git : il contient des JAR, des POM et leurs métadonnées.

Chaque artefact est identifié par ses coordonnées `groupId:artifactId:version`. Ces coordonnées déterminent également son emplacement dans le dépôt.

Maven utilise d'abord le dépôt local de la machine :

`C:\Users\<utilisateur>\.m2\repository`

Ce dossier sert de cache et de stockage pour les artefacts installés localement. Il ne doit pas être ajouté au projet ni versionné.

Lorsqu'un artefact demandé n'existe pas localement, Maven le cherche dans les dépôts distants configurés.

Maven Central est le dépôt distant public utilisé par défaut. Il contient les plugins Maven et une grande partie des bibliothèques Java publiques.

Au premier build, Maven télécharge les plugins nécessaires ainsi que leurs propres dépendances. Les builds suivants réutilisent les fichiers présents dans `.m2`, ce qui explique pourquoi ils sont généralement plus rapides.

Maven télécharge également les POM des artefacts. Ces POM lui permettent de connaître leurs métadonnées et leurs dépendances.

Une version publiée sans `SNAPSHOT` est considérée comme immuable. Maven peut donc la conserver durablement dans son cache.

Une version `SNAPSHOT` peut évoluer. Maven consulte périodiquement le dépôt distant pour rechercher une version plus récente selon sa politique de mise à jour.

La commande `mvn -o package` active le mode hors ligne. Maven n'utilise alors que les artefacts déjà présents dans le dépôt local et échoue si l'un d'eux manque.

La commande `mvn -U package` force Maven à vérifier les mises à jour disponibles, notamment pour les snapshots.

La configuration globale ou utilisateur se trouve généralement dans `settings.xml`. Elle peut définir des miroirs, des proxys, des identifiants et des dépôts d'entreprise.

En entreprise, un gestionnaire comme JFrog Artifactory peut servir d'intermédiaire entre les développeurs et Maven Central. Il centralise les artefacts internes, contrôle les téléchargements et met en cache les artefacts externes.

Les plugins sont récupérés depuis ces dépôts parce qu'ils sont eux-mêmes des artefacts. Le même mécanisme permet à une application de récupérer les bibliothèques dont son code a besoin : les dépendances. Section suivante.

## Dépendance

Une dépendance est un artefact externe dont le projet a besoin pour être compilé, testé ou exécuté.

Une bibliothèque Java est généralement distribuée sous forme de JAR. Sans Maven, il faudrait télécharger ce JAR manuellement puis l'ajouter aux différents *classpaths* de `javac` et de la JVM.

Une dépendance Maven est déclarée dans la section `dependencies` du POM avec ses coordonnées :

- `groupId` : organisation qui publie l'artefact ;
- `artifactId` : nom de l'artefact ;
- `version` : version précise demandée.

Maven cherche d'abord l'artefact dans le dépôt local `.m2`. S'il est absent, il télécharge son POM et son JAR depuis un dépôt distant.

Une dépendance déclarée directement dans le POM du projet est une dépendance directe.

Le POM de cette dépendance peut lui-même déclarer d'autres dépendances. Maven les récupère récursivement : ce sont les dépendances transitives.

Grâce aux dépendances transitives, un projet n'a pas besoin de déclarer manuellement toutes les bibliothèques internes utilisées par chaque dépendance directe.

Plusieurs chemins de l'arbre peuvent demander des versions différentes du même artefact. Maven doit alors sélectionner une seule version. Par défaut, il retient généralement la déclaration la plus proche du projet dans l'arbre des dépendances.

La commande `mvn dependency:tree` affiche les dépendances directes, les dépendances transitives et les versions retenues.

Une dépendance fournit du code utilisé par le projet. Un plugin fournit une action utilisée pour construire le projet. Les deux sont des artefacts récupérés depuis des dépôts, mais ils n'ont pas le même rôle.

Toutes les dépendances ne doivent pas être disponibles pendant toutes les étapes. Maven utilise leur *scope* pour déterminer les classpaths auxquels elles appartiennent. Section suivante.

## Scope

Le *scope* indique dans quels classpaths Maven place une dépendance.

Maven distingue principalement :

- la compilation du code principal ;
- la compilation et l'exécution des tests ;
- l'exécution de l'application ;
- la transmission de la dépendance aux projets consommateurs.

Une dépendance transitive est une dépendance reçue indirectement à travers un autre artefact.

### compile

- Compilation principale : oui
- Tests : oui
- Exécution : oui
- Transitive : oui
- Usage : bibliothèque utilisée directement par l'application
- Exemple : bibliothèque JSON

`compile` est le scope par défaut. Il peut être omis dans le POM.

### test

- Compilation principale : non
- Tests : oui
- Exécution : non
- Transitive : non
- Usage : code nécessaire uniquement pour vérifier l'application
- Exemple : JUnit

Une dépendance `test` ne peut pas être importée par le code de `src/main/java` et n'est pas livrée avec l'application.

### runtime

- Compilation principale : non
- Tests : oui
- Exécution : oui
- Transitive : oui
- Usage : implémentation nécessaire uniquement lorsque l'application tourne
- Exemple : driver PostgreSQL lorsque le code compile contre l'API JDBC

Le code principal ne peut pas importer directement une classe disponible uniquement avec le scope `runtime`.

### provided

- Compilation principale : oui
- Tests : oui
- Exécution : non
- Transitive : non
- Usage : API nécessaire pour compiler, mais fournie en production par l'environnement
- Exemple : API Servlet fournie par un serveur externe

La différence avec `runtime` est inversée :

- `runtime` : absent à la compilation, présent à l'exécution ;
- `provided` : présent à la compilation, absent à l'exécution.

### system

- Compilation principale : oui
- Tests : oui
- Exécution : non
- Transitive : non
- Source : chemin local explicite vers un JAR
- Usage : cas exceptionnel, généralement à éviter

`system` rend le build dépendant des fichiers présents sur une machine et contourne les dépôts Maven.

### import

- Compilation principale : non applicable
- Tests : non applicable
- Exécution : non applicable
- Transitive : non applicable
- Usage : importer les versions gérées par un BOM

`import` s'utilise uniquement avec un POM déclaré dans `dependencyManagement`. Il n'ajoute pas directement une bibliothèque au classpath.

### Artefact

Le scope contrôle les classpaths, pas le contenu physique du JAR produit.

Un JAR Maven classique contient les classes et ressources du projet, mais pas les JAR de ses dépendances. Un plugin supplémentaire est nécessaire pour construire une archive qui les regroupe.

### Résumé

- `compile` : partout ;
- `test` : tests uniquement ;
- `runtime` : exécution, mais pas compilation principale ;
- `provided` : compilation, mais pas exécution ;
- `system` : JAR local à éviter ;
- `import` : versions d'un BOM.

Le scope organise la disponibilité des dépendances, mais il ne détermine pas le moment où chaque catégorie de tests s’exécute.

Les tests unitaires peuvent fonctionner avant la création de l’artefact. Un test nécessitant le JAR construit doit, lui, s’exécuter après la phase `package`. Maven utilise un plugin distinct pour ce besoin. Section suivante.

## Failsafe

Surefire exécute les tests unitaires pendant la phase `test`, avant la création de l’artefact.

Failsafe exécute les tests d’intégration plus tard dans le cycle de vie :

- l’objectif `integration-test` exécute les tests après `package` ;
- l’objectif `verify` vérifie leurs résultats et fait échouer le build si nécessaire.

Par convention, Failsafe découvre notamment les classes nommées `IT*`, `*IT` ou `*ITCase`. Surefire découvre principalement les classes nommées `Test*`, `*Test`, `*Tests` ou `*TestCase`.

La commande `mvn test` s’arrête avant la construction du JAR et n’exécute pas Failsafe.

La commande `mvn verify` construit l’artefact, exécute les tests d’intégration, effectue les nettoyages configurés puis vérifie leurs résultats.

Il vaut mieux demander `verify` que lancer directement `integration-test`, car les phases suivantes, notamment le nettoyage et la vérification finale, doivent également être exécutées.

Failsafe est un plugin de build, pas une dépendance de l’application. Il doit être configuré dans le POM pour être attaché au cycle de vie.

La configuration d’un plugin peut dépendre d’informations déjà connues par Maven, comme le dossier de build ou le nom final de l’artefact. Les recopier manuellement crée une duplication fragile. Maven expose ces informations sous forme de propriétés. Section suivante.

## Propriété

Une propriété Maven est une valeur nommée utilisable dans le POM avec la syntaxe `${nom}`.

Une propriété peut être déclarée dans la section `properties`, provenir du modèle du projet ou être fournie à Maven au lancement.

Le modèle expose notamment :

- `${project.groupId}` : groupe du projet ;
- `${project.artifactId}` : nom de l’artefact ;
- `${project.version}` : version du projet ;
- `${project.build.directory}` : dossier de build ;
- `${project.build.finalName}` : nom final de l’artefact sans extension.

Une valeur fournie avec `-Dnom=valeur` devient une propriété pour le build courant.

Maven résout les expressions avant de transmettre la configuration au plugin.

Une propriété Maven n’est pas automatiquement une propriété système Java. Le plugin doit explicitement la transmettre à la JVM pour que le code puisse la lire avec `System.getProperty`.

Réutiliser les propriétés du modèle évite de dupliquer les informations du POM et conserve le build lorsque le nom ou la version du projet change.

Le build exécute des tests, mais il ne décide pas du comportement attendu. Ce comportement vient de la logique du programme. Section suivante.