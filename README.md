# Notes

Ce dépôt est une base de connaissances durable pour maîtriser l’ingénierie logicielle, préparer les entretiens techniques et prendre de meilleures décisions en production.

## Objectif

Comprendre chaque sujet depuis ses fondations jusqu’à ses contraintes réelles :

- expliquer son fonctionnement sans réciter une définition ;
- relier chaque solution au problème qu’elle résout ;
- connaître ses limites, ses coûts et ses modes de panne ;
- comparer les alternatives et justifier un choix ;
- l’utiliser, le tester, l’observer et le dépanner en production.

L’objectif n’est pas d’accumuler des outils, mais de développer le raisonnement attendu d’un ingénieur senior.

## Principes

- Les notes restent générales et indépendantes d’un projet particulier.
- Un fichier couvre une technologie ou un grand domaine d’ingénierie.
- Une section couvre une notion cohérente de ce sujet.
- Chaque notion présente sa définition, son mécanisme, ses différences, ses limites et ses pièges importants.
- Les différences sont décrites avec un pattern constant afin de faciliter les révisions.
- Les commandes utiles sont expliquées, pas seulement listées.
- Le code, les expériences et les mesures restent dans les projets pratiques.
- Une explication simple ne doit jamais supprimer une notion nécessaire.
- Aucune technologie n’est introduite uniquement parce qu’elle est populaire.

## Structure

Les fichiers suivent le format `numéro - sujet.md`.

Le numéro conserve l’ordre dans lequel les sujets ont réellement été rencontrés. Il ne définit pas un parcours futur.

Les titres de fichiers représentent les technologies ou domaines majeurs. Leurs sections décrivent les notions qui leur appartiennent.

La stack représente le périmètre technique à maîtriser, pas un ordre d’introduction.

## Méthode

Le prochain sujet n’est pas fixé à l’avance. Il est choisi à partir de la dernière limite concrète rencontrée pendant la pratique.

Chaque fonctionnalité évolue d’une version minimale vers une version professionnelle pour le périmètre courant :

1. construire une solution simple ;
2. rencontrer une limite réelle ;
3. observer et mesurer le problème ;
4. comprendre sa cause ;
5. documenter les notions nécessaires avant d’introduire la solution ;
6. appliquer la solution minimale ;
7. provoquer ses erreurs et ses pannes ;
8. couvrir les cas limites pertinents ;
9. refactorer sans modifier le comportement ;
10. vérifier le build complet et mesurer l’amélioration.

Pour chaque comportement testable, le cycle est :

1. **Red** : écrire un test qui expose la limite et échoue ;
2. **Green** : appliquer la correction minimale qui le fait réussir ;
3. **Refactor** : améliorer le code et les tests sans changer le comportement.

Une version professionnelle ne cherche pas la complexité maximale. Elle possède un contrat clair, maîtrise ses erreurs, couvre ses risques importants et reste compréhensible et maintenable.

## Qualité

Un sujet n’est terminé que lorsque :

- le besoin ou la limite a été observé concrètement ;
- la cause peut être expliquée clairement ;
- le comportement attendu possède un contrat explicite ;
- les cas nominaux, les erreurs et les cas limites pertinents sont vérifiés ;
- les tests utiles sont automatisés et déterministes ;
- le build complet réussit depuis un état propre ;
- les compromis, limites et risques sont compris ;
- les notes sont générales, exactes et utilisables en entretien ;
- aucune complexité sans besoin réel n’a été ajoutée.

## Git

- Une section de notes produit un commit cohérent.
- Une fonctionnalité regroupe son comportement, ses tests et sa configuration nécessaire.
- `amend` corrige uniquement une erreur accidentelle du dernier commit lorsqu’il n’est pas utile de conserver cet état.
- Chaque évolution fonctionnelle stable et vérifiée produit un nouveau commit afin de conserver l’historique du projet.
- Les fichiers générés ne sont pas versionnés.
- Le build et les tests sont validés avant chaque commit de code.
- Les messages des notes suivent le format `sujet: notion`.
- Les projets utilisent les préfixes `feat`, `fix`, `refactor`, `test`, `build` et `docs`.
- Un historique partagé n’est jamais réécrit sans coordination.
- Lorsqu’une branche personnelle doit être réécrite, `--force-with-lease` est utilisé à la place de `--force`.

## Stack

- `backend :` Java 25, Maven, Spring Boot 4, Spring Data JPA, Spring Security, REST, OpenAPI, Caffeine, Resilience4j
- `architecture :` monolithe modulaire, architecture événementielle, microservices, Apache Kafka
- `frontend :` TypeScript, Angular 18, HTML5, CSS3, SCSS
- `base :` PostgreSQL, Liquibase, Redis, pgvector
- `stockage :` S3, MinIO
- `sécurité :` OAuth 2.0, OpenID Connect, JWT, SSO, Vault
- `tests :` JUnit 6, Mockito, Testcontainers, WireMock, Gatling, SonarQube
- `ia :` OCR, Spring AI, API LLM, embeddings, RAG, évaluation
- `data :` Python, traitements batch et streaming
- `cloud :` AWS, IAM, VPC, S3, RDS, EKS, MSK
- `infrastructure :` Docker, Kubernetes, Terraform
- `livraison :` GitHub Actions, ArgoCD, JFrog
- `observabilité :` OpenTelemetry, Prometheus, Grafana, Elasticsearch, Kibana

## Problèmes

La pratique devra notamment couvrir :

- débit et latence ;
- consommation CPU et RAM ;
- saturation de la JVM et pauses GC ;
- concurrence et parallélisme ;
- contention, interblocages et épuisement des threads ;
- uploads volumineux ou interrompus ;
- traitements OCR lents ;
- fournisseurs externes indisponibles ;
- erreurs et hallucinations de l’IA ;
- doublons, idempotence, ordre et rejeu des messages ;
- saturation des connexions PostgreSQL ;
- transactions concurrentes et cohérence des données ;
- cohérence du cache ;
- isolation des utilisateurs ;
- authentification et autorisation ;
- gestion des secrets ;
- rate limiting ;
- load balancing ;
- circuit breakers ;
- pics de trafic ;
- pannes partielles et reprise ;
- logs, métriques, traces et alertes ;
- déploiements défectueux ;
- rollback ;
- sauvegarde et restauration ;
- reprise après sinistre ;
- coûts du cloud et de l’IA.