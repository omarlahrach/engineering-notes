
# Notes

Ce dépôt contient mes notes d’ingénierie logicielle et ma progression vers un profil senior.

## Objectif

Comprendre chaque élément de ma stack depuis ses fondations, savoir expliquer son fonctionnement en entretien et l’utiliser correctement en production.

Ces notes servent de support de révision. Les expériences et le code du produit se trouvent dans le dépôt `cue`.

## Méthode

L’apprentissage suit toujours le même cycle :

1. construire une solution simple ;
2. rencontrer une limite réelle ;
3. observer et mesurer le problème ;
4. comprendre sa cause ;
5. introduire la technologie qui le résout ;
6. provoquer une panne ;
7. vérifier la reprise ;
8. mesurer l’amélioration.

Aucune technologie n’est ajoutée uniquement parce qu’elle est populaire.

## Organisation

- `system.md` : machine, noyau, programme et processus ;
- `java.md` : langage, compilation, JVM et exécution ;
- `maven.md` : dépendances, build, tests et packaging ;
- les prochains fichiers suivront l’ordre réel de construction de Cue.

Les notes restent générales, concises et adaptées aux révisions d’entretien. Le code et les expérimentations restent dans le projet.

## Stack

- `backend :` Java 25, Maven, Spring Boot 4, Spring Data JPA, Spring Security, REST, OpenAPI, Caffeine, Resilience4j
- `architecture :` monolithe modulaire, architecture événementielle, microservices, Apache Kafka
- `frontend :` TypeScript, Angular 18, HTML5, CSS3, SCSS
- `base :` PostgreSQL, Liquibase, Redis, pgvector
- `stockage :` S3, MinIO
- `sécurité :` OAuth 2.0, OpenID Connect, JWT, SSO, Vault
- `tests :` JUnit 5, Mockito, Testcontainers, WireMock, Gatling, SonarQube
- `ia :` OCR, Spring AI, API LLM, embeddings, RAG, évaluation
- `data :` Python, traitements batch et streaming
- `cloud :` AWS, IAM, VPC, S3, RDS, EKS, MSK
- `infrastructure :` Docker, Kubernetes, Terraform
- `livraison :` GitHub Actions, ArgoCD, JFrog
- `observabilité :` OpenTelemetry, Prometheus, Grafana, Elasticsearch, Kibana

## Parcours

1. Système
2. Java
3. Classes, packages, classpath et JAR
4. Maven
5. Logique métier et JUnit 5
6. HTTP
7. Spring Boot et monolithe modulaire
8. REST et OpenAPI
9. Mockito
10. Angular
11. Docker
12. PostgreSQL et JDBC
13. Liquibase
14. JPA et Spring Data JPA
15. Testcontainers
16. MinIO
17. Spring Security, OAuth 2.0, OpenID Connect et JWT
18. Python et OCR
19. WireMock
20. Kafka et traitement asynchrone
21. Spring AI et API LLM
22. Embeddings, pgvector et RAG
23. Évaluation de l’IA
24. Caffeine et Redis
25. Resilience4j
26. OpenTelemetry, Prometheus, Grafana, Elasticsearch et Kibana
27. Gatling et performance
28. GitHub Actions, SonarQube et JFrog
29. Architecture événementielle
30. Microservices
31. Terraform et AWS
32. Kubernetes et EKS
33. MSK et RDS
34. ArgoCD et Vault

## Problèmes

Le parcours devra notamment couvrir :

- débit et latence ;
- consommation CPU et RAM ;
- saturation de la JVM et pauses GC ;
- concurrence et parallélisme ;
- uploads volumineux ou interrompus ;
- traitements OCR lents ;
- fournisseurs externes indisponibles ;
- erreurs et hallucinations de l’IA ;
- idempotence et rejeu des messages ;
- saturation des connexions PostgreSQL ;
- cohérence du cache ;
- isolation des utilisateurs ;
- authentification et autorisation ;
- rate limiting ;
- load balancing ;
- circuit breakers ;
- pics de trafic ;
- déploiements défectueux ;
- rollback ;
- sauvegarde et restauration ;
- coûts cloud et IA.