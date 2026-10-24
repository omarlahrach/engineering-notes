# Tests

## Logique

La logique métier représente les règles propres au besoin de l'application. Elle décide du résultat à partir des données reçues.

Le point d'entrée reçoit les entrées et affiche les sorties. Il ne doit pas contenir toutes les règles métier.

Séparer la logique métier des entrées-sorties permet de la réutiliser sans terminal, interface web ou base de données.

Une logique déterministe produit le même résultat pour les mêmes entrées. Elle est plus simple à vérifier et à tester.

Au début, chaque comportement peut être vérifié manuellement. Lorsque les règles et les cas possibles augmentent, répéter toutes les vérifications après chaque modification devient lent et peu fiable. Les tests automatisés résolvent cette limite. Section suivante.