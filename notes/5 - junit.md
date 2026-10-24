# JUnit

JUnit est le framework standard de test dans l'écosystème Java. La génération actuelle est JUnit 6 et nécessite au minimum Java 17.

## Architecture

JUnit 6 est composé de trois parties :

- **Platform** : orchestre la découverte et l'exécution des moteurs de test sur la JVM ;
- **Jupiter** : fournit le modèle moderne pour écrire les tests, son système d'extensions et son moteur d'exécution ;
- **Vintage** : exécute les anciens tests JUnit 3 et 4 pendant leur migration.

Un nouveau projet utilise Jupiter. Vintage sert uniquement à maintenir temporairement une compatibilité avec d'anciens tests.