# API

## Origine

À mesure que les programmes grandissent, une partie du logiciel doit utiliser des capacités fournies par une autre partie.

Sans limite claire, le code utilisateur dépend de l’organisation interne du composant utilisé. Une modification interne peut alors casser tous les programmes qui en dépendent.

Pour éviter ce couplage, un composant expose un ensemble limité d’opérations. Les autres programmes utilisent ces opérations sans connaître leur implémentation. Le composant peut ainsi modifier son fonctionnement interne tant que les opérations promises restent disponibles.

Ces interfaces existaient avant Internet : une bibliothèque expose des fonctions ou des classes, et un système d’exploitation expose des opérations aux programmes. Une API n’est donc pas nécessairement distante et n’utilise pas nécessairement HTTP.

Le réseau a ensuite permis de placer les deux programmes dans des processus ou sur des machines différentes. Ils ne partagent plus directement du code : ils échangent des messages. HTTP peut transporter ces messages, mais il ne constitue pas à lui seul l’API.

Cette séparation repose sur une interface destinée aux programmes. Il faut maintenant définir précisément ce qu’elle expose. Section suivante.