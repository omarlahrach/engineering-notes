# API

## Origine

À mesure que les programmes grandissent, une partie du logiciel doit utiliser des capacités fournies par une autre partie.

Sans limite claire, le code utilisateur dépend de l’organisation interne du composant utilisé. Une modification interne peut alors casser tous les programmes qui en dépendent.

Pour éviter ce couplage, un composant expose un ensemble limité d’opérations. Les autres programmes utilisent ces opérations sans connaître leur implémentation. Le composant peut ainsi modifier son fonctionnement interne tant que les opérations promises restent disponibles.

Ces interfaces existaient avant Internet : une bibliothèque expose des fonctions ou des classes, et un système d’exploitation expose des opérations aux programmes. Une API n’est donc pas nécessairement distante et n’utilise pas nécessairement HTTP.

Le réseau a ensuite permis de placer les deux programmes dans des processus ou sur des machines différentes. Ils ne partagent plus directement du code : ils échangent des messages. HTTP peut transporter ces messages, mais il ne constitue pas à lui seul l’API.

Cette séparation repose sur une interface destinée aux programmes. Il faut maintenant définir précisément ce qu’elle expose. Section suivante.

## Définition

API signifie *Application Programming Interface*, ou interface de programmation.

Une API est l’interface qu’un logiciel expose pour permettre à un autre logiciel d’utiliser ses capacités. Elle forme une frontière entre deux rôles :

- le **fournisseur** expose des opérations ;
- le **consommateur** utilise ces opérations sans accéder à leur implémentation interne.

L’API n’est ni un processus ni l’implémentation. Elle décrit uniquement la partie observable : ce qu’il est possible de demander et ce que le fournisseur promet en retour.

Elle peut prendre plusieurs formes :

- une bibliothèque expose des fonctions, des classes ou des méthodes ;
- un système d’exploitation expose des opérations aux programmes ;
- un service distant expose des opérations accessibles par des messages.

Dans les deux premiers cas, l’appel peut rester dans la même machine. Dans le dernier, les programmes communiquent par un réseau, éventuellement avec HTTP.

HTTP définit comment transporter et structurer les messages. L’API définit quelles opérations précises le logiciel offre au moyen de ces messages.

Une interface ne suffit cependant pas si son comportement reste ambigu. Les opérations, les entrées, les résultats et les erreurs doivent former un contrat. Section suivante.