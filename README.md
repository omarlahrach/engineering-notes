
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
3. Classes, packages et classpath
4. Maven
5. Spring Boot
6. HTTP
7. REST et OpenAPI
8. Tests
9. Angular
10. PostgreSQL et JDBC
11. Liquibase
12. JPA et Spring Data JPA
13. MinIO
14. Sécurité
15. Python et OCR
16. Kafka
17. Spring AI et LLM
18. Embeddings, pgvector et RAG
19. Évaluation de l’IA
20. Caffeine et Redis
21. Resilience4j
22. Observabilité
23. Performance
24. Docker
25. GitHub Actions, SonarQube et JFrog
26. Architecture événementielle
27. Microservices
28. Terraform et AWS
29. Kubernetes et EKS
30. MSK, RDS, ArgoCD et Vault

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