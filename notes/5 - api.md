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

## Contrat

Le contrat d’une API rassemble les promesses observables sur lesquelles le consommateur peut compter.

Pour chaque opération, il précise :

- comment la demander ;
- quelles entrées sont obligatoires ou facultatives ;
- le type et le format de ces entrées ;
- le résultat possible ;
- les erreurs possibles ;
- les effets produits, par exemple lire, créer ou supprimer une donnée.

Le contrat ne décrit pas comment le fournisseur réalise l’opération. Son algorithme, ses classes internes ou son stockage peuvent changer sans affecter le consommateur, tant que les promesses restent respectées.

Une modification interne est donc compatible avec l’API. En revanche, supprimer une opération, rendre une entrée obligatoire ou changer le sens d’un résultat peut casser les consommateurs : le contrat a changé.

Les types du code, la documentation et les tests peuvent décrire ou vérifier ce contrat. Aucun de ces éléments ne remplace cependant le comportement réellement observable par le consommateur.

Ce contrat peut être utilisé directement dans le même processus ou traverser un réseau sous forme de messages. Le cas local est le plus direct. Section suivante.

## Locale

Une API locale est utilisée sans échange de messages sur le réseau.

Lorsqu’un programme utilise une bibliothèque, il appelle directement les fonctions ou les méthodes qu’elle expose. Le langage et son environnement transmettent les arguments, exécutent le code puis rendent le résultat.

Dans un langage typé, le compilateur peut déjà vérifier une partie du contrat :

- l’opération existe ;
- le nombre d’arguments est correct ;
- les types attendus sont respectés ;
- le type du résultat est connu.

Il ne peut pas vérifier tout le comportement, comme la signification du résultat ou les conditions qui provoquent une erreur.

Une opération du système d’exploitation constitue aussi une API locale. Elle traverse la frontière entre le programme et le noyau, mais n’utilise pas le réseau.

« Locale » ne signifie pas `localhost`. Deux processus qui communiquent avec des sockets sur `localhost` échangent quand même des messages par la pile réseau. Ils utilisent une API distante, même s’ils tournent sur la même machine.

Quand le fournisseur se trouve dans un autre processus, le consommateur ne peut plus appeler directement ses fonctions. La demande et le résultat doivent être transformés en messages. Section suivante.

## Distante

Une API distante relie un consommateur et un fournisseur exécutés dans des processus séparés. Ils peuvent se trouver sur la même machine ou sur des machines différentes.

Contrairement à un appel local, le consommateur ne peut pas appeler directement une fonction du fournisseur ni accéder à sa mémoire. Les deux processus communiquent en échangeant des messages.

Une opération distante suit ce parcours général :

1. le consommateur prépare une demande ;
2. la demande est transmise au fournisseur ;
3. le fournisseur l’interprète et exécute l’opération ;
4. il prépare un résultat ;
5. le résultat est transmis au consommateur.

Cette séparation ajoute des situations qui n’existent pas lors d’un appel local :

- le fournisseur peut être indisponible ;
- la connexion peut échouer ;
- la transmission peut être interrompue ;
- le consommateur peut dépasser son délai d’attente ;
- l’opération peut avoir été exécutée alors que sa réponse n’est jamais parvenue.

Un délai dépassé ne prouve donc pas que l’opération n’a pas eu lieu. Répéter la demande peut produire un nouvel effet si l’opération n’est pas idempotente.

Une API distante utilise des messages pour demander une opération et recevoir son résultat.

Avec HTTP, le contrat précise pour chaque opération :

- la méthode et le chemin de la requête ;
- les en-têtes et le corps attendus ;
- les codes de statut, les en-têtes et le corps possibles dans la réponse.

Une API distante exposée au moyen de requêtes et de réponses HTTP est appelée une API HTTP. Section suivante.