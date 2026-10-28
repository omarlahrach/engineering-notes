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
