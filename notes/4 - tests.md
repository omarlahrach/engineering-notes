# Tests

## Logique

La logique métier représente les règles propres au besoin de l'application. Elle décide du résultat à partir des données reçues.

Le point d'entrée reçoit les entrées et affiche les sorties. Il ne doit pas contenir toutes les règles métier.

Séparer la logique métier des entrées-sorties permet de la réutiliser sans terminal, interface web ou base de données.

Une logique déterministe produit le même résultat pour les mêmes entrées. Elle est plus simple à vérifier et à tester.

Au début, chaque comportement peut être vérifié manuellement. Lorsque les règles et les cas possibles augmentent, répéter toutes les vérifications après chaque modification devient lent et peu fiable. Les tests automatisés résolvent cette limite. Section suivante.

## Unitaire

Un test unitaire vérifie automatiquement un comportement précis d'une unité de code isolée.

Une unité n'est pas obligatoirement une seule méthode ou une seule classe. C'est un ensemble cohérent assez petit pour être exécuté et compris indépendamment du reste du système.

Le test vérifie le contrat observable de cette unité, pas les détails internes de son implémentation. Une modification interne ne doit pas casser le test si le comportement attendu reste identique.

Un cas de test suit généralement trois étapes :

1. *Arrange* : préparer l'unité et ses données d'entrée ;
2. *Act* : exécuter le comportement à vérifier ;
3. *Assert* : comparer le résultat obtenu au résultat attendu.

Un bon test unitaire est :

- ciblé : il vérifie un comportement précis ;
- rapide : il peut être exécuté fréquemment ;
- déterministe : les mêmes conditions produisent le même résultat ;
- indépendant : son résultat ne dépend pas des autres tests ni de leur ordre ;
- isolé : il ne dépend pas réellement du réseau, d'une base de données ou du système de fichiers ;
- lisible : son nom et son échec expliquent le comportement concerné.

Les tests automatisés permettent de rejouer les comportements déjà vérifiés après chaque modification. Lorsqu'un ancien comportement est involontairement cassé, on parle de régression.

Un test ne prouve pas que le programme ne contient aucun bug. Il vérifie uniquement les cas qui ont été décrits. Les tests eux-mêmes peuvent également être incomplets ou incorrects.

Un framework de test fournit un format pour déclarer les cas, les découvrir, les exécuter et comparer leurs résultats. Dans l'écosystème Java, le framework standard pour ce rôle est JUnit.