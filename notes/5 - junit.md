# JUnit

JUnit est le framework standard de test dans l'écosystème Java. La génération actuelle est JUnit 6 et nécessite au minimum Java 17.

## Architecture

JUnit 6 est composé de trois parties :

- **Platform** : orchestre la découverte et l'exécution des moteurs de test sur la JVM ;
- **Jupiter** : fournit le modèle moderne pour écrire les tests, son système d'extensions et son moteur d'exécution ;
- **Vintage** : exécute les anciens tests JUnit 3 et 4 pendant leur migration.

Un nouveau projet utilise Jupiter. Vintage sert uniquement à maintenir temporairement une compatibilité avec d'anciens tests.

## Déclaration

Une méthode annotée avec `@Test` représente un cas de test.

Les tests sont placés sous `src/test/java`. Leur package suit généralement celui du code testé.

Une classe de test porte généralement le nom de la classe testée suivi de `Test`.

Les classes et méthodes de test n'ont pas besoin d'être `public`.

Chaque test doit vérifier un comportement précis. Son nom doit décrire le résultat attendu ou la situation vérifiée.

Annotations courantes :

- `@Test` : déclarer un test ;
- `@DisplayName` : fournir un nom lisible ;
- `@Nested` : regrouper des tests liés ;
- `@Tag` : classer les tests ;
- `@Disabled` : désactiver temporairement un test ;
- `@RepeatedTest` : répéter un test plusieurs fois.

## Cycle

Par défaut, JUnit crée une nouvelle instance de la classe de test avant chaque méthode. Les tests ne partagent donc pas automatiquement leurs champs.

JUnit fournit des annotations pour exécuter du code autour des tests :

- `@BeforeEach` : avant chaque test ;
- `@AfterEach` : après chaque test ;
- `@BeforeAll` : une fois avant tous les tests de la classe ;
- `@AfterAll` : une fois après tous les tests de la classe.

`@BeforeEach` prépare un état indépendant pour chaque test. `@AfterEach` libère les ressources créées pendant ce test.

Par défaut, les méthodes `BeforeAll` et `AfterAll` doivent être statiques.

`@TestInstance(PER_CLASS)` demande à JUnit de réutiliser une seule instance de la classe. Les méthodes `BeforeAll` et `AfterAll` peuvent alors être non statiques, mais les tests risquent davantage de partager un état mutable.

## Assertions

Une assertion compare le résultat observé au résultat attendu.

Assertions courantes :

- `assertEquals` : vérifier une égalité ;
- `assertNotEquals` : vérifier une différence ;
- `assertTrue` et `assertFalse` : vérifier une condition ;
- `assertNull` et `assertNotNull` : vérifier la présence d'une valeur ;
- `assertSame` et `assertNotSame` : comparer l'identité de deux objets ;
- `assertThrows` : vérifier qu'une exception précise est produite ;
- `assertDoesNotThrow` : vérifier l'absence d'exception ;
- `assertAll` : exécuter plusieurs assertions sans s'arrêter à la première erreur ;
- `assertTimeout` : vérifier une durée maximale.

Une assertion non satisfaite produit un échec. Une exception inattendue produit une erreur.

Un message peut être ajouté à une assertion pour expliquer le comportement attendu lorsque le test échoue.

## Paramétrage

`@ParameterizedTest` exécute le même test avec plusieurs jeux de données.

Il évite de dupliquer une méthode lorsque seule l'entrée ou la sortie attendue change.

Sources courantes :

- `@ValueSource` : liste de valeurs simples ;
- `@NullSource` : valeur nulle ;
- `@EmptySource` : valeur vide ;
- `@CsvSource` : plusieurs arguments écrits sous forme de lignes ;
- `@MethodSource` : données produites par une méthode Java ;
- `@EnumSource` : valeurs provenant d'une énumération.

Chaque jeu de données constitue une exécution distincte du test et possède son propre résultat.

## Extension

Le modèle d'extensions permet d'ajouter un comportement autour de l'exécution des tests sans modifier JUnit.

Une extension peut notamment :

- préparer ou nettoyer un environnement ;
- injecter des paramètres ;
- contrôler l'activation d'un test ;
- intercepter son exécution ;
- réagir à son résultat.

`@ExtendWith` attache une extension à une classe ou une méthode de test.

Des outils comme Mockito et Spring fournissent leurs propres extensions pour s'intégrer à JUnit Jupiter.

## Maven

JUnit n'est pas livré dans le JDK. L'artefact `junit-jupiter` doit être déclaré comme dépendance Maven avec le scope `test`.

Cet artefact regroupe notamment l'API Jupiter, les tests paramétrés et le moteur Jupiter.

Le plugin Maven Surefire exécute les tests unitaires pendant la phase `test`.

La commande `mvn test` :

1. compile le code principal ;
2. compile les tests ;
3. lance Surefire ;
4. Surefire utilise JUnit Platform ;
5. le moteur Jupiter découvre et exécute les tests.

La commande `mvn -Dtest=NomTest test` exécute une seule classe.

La commande `mvn -Dtest=NomTest#nomMethode test` exécute une seule méthode.

Les rapports sont écrits dans `target/surefire-reports`.

La dépendance JUnit et les classes de test ne sont pas incluses dans le JAR de production.