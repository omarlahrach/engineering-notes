# HTTP

## Protocole

HTTP (*Hypertext Transfer Protocol*) est un protocole applicatif : des règles pour le format des messages échangés entre deux programmes.

Le noyau applique IP et TCP. Il transporte des octets, sans connaître HTTP. Ce sont les programmes, comme un navigateur, `curl` ou un serveur, qui écrivent et lisent ces octets selon les règles HTTP.

L’échange suit un modèle client-serveur :

1. le client ouvre une connexion TCP vers un serveur ;
2. il envoie une requête HTTP dans ce flux ;
3. le serveur lit la requête, la traite, puis écrit une réponse HTTP ;
4. le client lit la réponse.

Le client commence toujours l’échange. Le serveur doit rester actif et écouter un port.

HTTP est sans état : chaque requête est indépendante au niveau du protocole. Une application peut conserver un état, mais elle doit le relier elle-même aux requêtes suivantes.

Avant d’envoyer une requête, le client doit savoir où joindre le serveur. Cette destination est une adresse HTTP. Section suivante.

## URL

Une URL (*Uniform Resource Locator*) indique où se trouve une ressource et comment y accéder.

Exemple : `http://localhost:8080/documents`.

Le premier morceau s’appelle le schéma. Ici `http` nomme le protocole HTTP, en TCP non chiffré. Le même format d’URL sert aussi à d’autres accès, par exemple `file` ou `mailto`.

`localhost` est la machine, traduit localement en `127.0.0.1`. `8080` est le port. Le port par défaut de HTTP est `80` : s’il est différent, il doit figurer dans l’URL. `/documents` est le chemin de la ressource.

Le noyau ouvre une connexion TCP vers `127.0.0.1:8080`. Le chemin n’appartient pas à TCP. Il est envoyé dans la requête HTTP, une fois la connexion établie.

`https` nomme le même HTTP après une couche TLS. Il n’est pas détaillé ici.

Une fois le serveur joint, le client envoie une requête. Section suivante.

## Requête

Une requête HTTP est le message envoyé par le client dans la connexion TCP.

Elle contient trois parties, dans cet ordre :

1. la ligne de requête ;
2. les en-têtes ;
3. le corps, s’il y en a un.

Une ligne vide sépare les en-têtes du corps. Sans elle, le serveur ne sait pas où s’arrêtent les en-têtes.

**Ligne**

La première ligne contient trois éléments :

- la méthode : l’intention, par exemple `GET` pour lire ou `POST` pour envoyer ;
- le chemin : la ressource visée, reprise de l’URL ;
- la version : les règles HTTP utilisées, souvent `HTTP/1.1`.

**En-têtes**

Chaque en-tête est une ligne `Nom: valeur`.

- `Host` : machine visée ;
- `Content-Type` : format du corps.

**Corps**

Le corps contient les données utiles, par exemple le texte d’un document.

Une requête peut n’avoir aucun corps, notamment un `GET`.

Le serveur répond avec un message de même famille. Section suivante.

## Réponse

Une réponse HTTP est le message renvoyé par le serveur dans la même connexion TCP.

Elle contient trois parties, dans cet ordre :

1. la ligne de statut ;
2. les en-têtes ;
3. le corps, s’il y en a un.

Une ligne vide sépare les en-têtes du corps.

**Statut**

La première ligne contient trois éléments :

- la version HTTP, souvent `HTTP/1.1` ;
- le code numérique, par exemple `200` ;
- une phrase courte, par exemple `OK`.

Le client s’appuie sur le code, pas sur la phrase.

Familles de codes :

- `2xx` : succès, `200` la requête a réussi ;
- `4xx` : erreur du client, `404` la ressource est introuvable ;
- `5xx` : erreur du serveur, `500` un traitement a échoué.

Un refus de connexion n’est pas une réponse HTTP. TCP n’a pas pu s’établir, donc aucun message HTTP n’a été échangé.

**En-têtes**

Chaque en-tête est une ligne `Nom: valeur`. `Content-Type` indique le format du corps.

**Corps**

Le corps contient le résultat, par exemple une date extraite ou un message d’erreur.

Une réponse peut n’avoir aucun corps.

Le serveur qui produit cette réponse doit rester à l’écoute d’un port. Section suivante.
