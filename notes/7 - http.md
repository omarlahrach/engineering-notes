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

## Méthode

La méthode dit ce que le client veut faire. Le serveur décide avec le couple **méthode + chemin**, pas avec le chemin seul.

`GET /documents` lit. `POST /documents` enregistre.

**GET**

- Fait : lire
- Corps : aucun en général
- 1re fois : ne modifie rien
- Fois suivantes : ne modifie toujours rien

**POST**

- Fait : créer ou déclencher un traitement
- Corps : fréquent
- 1re fois : un effet, par exemple une ressource créée
- Fois suivantes : un nouvel effet possible, par exemple une deuxième ressource

**PUT**

- Fait : remplacer toute la ressource par le corps
- Corps : la version complète
- 1re fois : la ressource devient ce corps
- Fois suivantes : elle est déjà ce corps, rien de plus n’est ajouté

**PATCH**

- Fait : modifier une partie de la ressource
- Corps : uniquement les champs à changer
- 1re fois : ces champs changent
- Fois suivantes : selon l’opération, un nouvel effet est possible

**DELETE**

- Fait : supprimer la ressource
- Corps : aucun en général
- 1re fois : la ressource disparaît
- Fois suivantes : elle est déjà absente, rien de plus n’est supprimé

**Sûr**

Aucune modification, dès la première fois. Seul `GET` est sûr.

**Idempotent**

La 1re fois peut changer la ressource. Les fois suivantes ne la transforment plus. `GET`, `PUT` et `DELETE` sont idempotents. `POST` ne l’est pas.

La méthode dit l’intention. Les en-têtes précisent le message : format du corps, taille, machine visée. Section suivante.

## En-tête

Un en-tête HTTP est une ligne `Nom: valeur`. Il décrit le message, pas la ressource elle-même.

Les en-têtes se placent après la ligne de requête ou de statut, avant le corps. Une ligne vide les termine.

**Host**

Machine visée, obligatoire en HTTP/1.1. Exemple : `Host: localhost:8080`.

Le noyau a déjà ouvert TCP vers une IP et un port. `Host` permet au serveur de savoir quel nom a été demandé, surtout lorsqu’il gère plusieurs sites sur la même machine.

**Content-Type**

Format du corps. Exemple : `text/plain`, `application/json`.

Sans lui, le destinataire ne sait pas comment interpréter les octets du corps.

**Content-Length**

Taille du corps, en octets.

Elle dit où le corps s’arrête. Sans taille connue, le lecteur ne sait pas quand le message est complet.

**Autres**

- `Connection` : garder ou fermer la connexion TCP après la réponse ;
- `Authorization` : prouver qui envoie la requête. Plus tard.

Les en-têtes de requête décrivent ce que le client envoie. Ceux de réponse décrivent ce que le serveur renvoie. Les mêmes noms peuvent servir des deux côtés, notamment `Content-Type` et `Content-Length`.

Le transport de ces messages dépend encore de la version HTTP. Section suivante.

## Version

La version HTTP indique comment les messages sont transportés. Méthode, chemin, en-têtes, statut et corps restent les mêmes idées. Le tuyau change.

**HTTP/1.0**

- Format : texte
- Transport : TCP
- Connexion : souvent une par requête

**HTTP/1.1**

- Format : texte
- Transport : TCP
- Connexion : réutilisable pour plusieurs requêtes
- `Host` obligatoire
- Corps possible sans taille fixe, par blocs (*chunked*)

C’est encore la version la plus simple à lire : une requête ressemble au texte envoyé par `curl`.

**HTTP/2**

- Format : binaire
- Transport : TCP
- Plusieurs requêtes en parallèle sur une seule connexion

Le texte `GET /documents HTTP/1.1` n’apparaît plus tel quel sur le réseau. Les en-têtes sont compressés.

**HTTP/3**

- Format : binaire
- Transport : UDP, via QUIC
- Plusieurs requêtes en parallèle, sans bloquer tout le flux si un paquet TCP est perdu

Le client et le serveur se mettent d’accord sur une version. Si l’un ne connaît que HTTP/1.1, l’échange reste en 1.1.

`http` envoie ces messages en clair. `https` les fait passer par TLS avant TCP ou QUIC. Section suivante.

## TLS

TLS (*Transport Layer Security*) s’intercale après la connexion TCP et avant HTTP.

1. TCP ouvre le tuyau
2. TLS le verrouille
3. HTTP circule ensuite, chiffré

Le schéma `https` signifie HTTP au-dessus de TLS. Le port par défaut est `443`. `http` reste du HTTP en clair, port `80`.

**Clair**

Sans TLS, n’importe qui sur le chemin peut lire la requête et la réponse, y compris un mot de passe ou un document.

**Cadenas**

Client et serveur échangent d’abord assez d’informations pour calculer la même clé secrète. Cette clé n’est pas envoyée telle quelle. Ensuite, tous les octets sont chiffrés avec elle.

Un observateur voit du bruit. Il ne voit plus la méthode, le chemin ni le corps.

**Certificat**

Le serveur envoie un certificat : il déclare le nom du site, par exemple `exemple.com`.

Une autorité reconnue a signé ce fichier. Le client vérifie :

- la signature vient d’une autorité qu’il connaît ;
- le nom du certificat est celui de l’URL ;
- le certificat n’est pas expiré.

Si l’un de ces points échoue, aucun HTTP n’est envoyé.

**Nom**

Le certificat est lié au nom de domaine, pas au design du site.

`https://github.com` exige un certificat `github.com`. Seul celui qui contrôle ce domaine peut l’obtenir.

`https://github1.com` peut avoir un certificat valide, un cadenas, et le même habillage. TLS est correct pour ce nom. Ce n’est pas GitHub. Le client doit lire l’URL.

HTTPS garantit le chiffrement, et le dialogue avec le propriétaire du nom affiché. Il ne garantit pas que ce nom est l’entreprise à laquelle on pense.

**HTTP**

Une fois TLS en place, HTTP ne change pas : mêmes méthodes, mêmes en-têtes, mêmes statuts. Seuls les octets sur le réseau sont illisibles.

**Local**

Sur `localhost`, `http` suffit : le message ne quitte pas la machine. Dès que le réseau n’est plus de confiance, TLS est obligatoire.

HTTP définit la forme des messages échangés. Il ne définit pas quelles opérations une application expose, quelles données elle attend ni quelles réponses elle garantit. Cet ensemble forme un contrat appelé API. Section suivante.