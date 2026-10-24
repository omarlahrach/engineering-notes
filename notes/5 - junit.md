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