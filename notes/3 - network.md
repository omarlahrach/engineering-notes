# Network

## Origine

Les premiers ordinateurs fonctionnaient seuls. Pour échanger des données, il fallait transporter physiquement les supports de stockage ou relier directement deux machines.

Dans les années 1960, Paul Baran et Donald Davies développent indépendamment le principe de commutation de paquets : les données sont découpées en petites unités pouvant circuler séparément sur un réseau.

ARPANET, lancé en 1969, applique ce principe pour relier plusieurs centres de recherche. Ses réseaux utilisent cependant encore des règles de communication incompatibles avec d’autres réseaux.

Dans les années 1970, Vint Cerf et Bob Kahn conçoivent TCP/IP afin de permettre à plusieurs réseaux différents de communiquer ensemble.

Le 1er janvier 1983, ARPANET adopte TCP/IP. Cette interconnexion de réseaux forme la base d’Internet.

Internet est une infrastructure permettant à des machines d’échanger des données. Le Web est créé plus tard et utilise cette infrastructure : Internet et Web ne sont donc pas synonymes.

Avant de comprendre Internet, il faut comprendre ce qu’est un réseau entre quelques machines. Section suivante.

## Définition

Un réseau est un ensemble de machines reliées afin d’échanger des données. Deux ordinateurs reliés par un câble forment déjà un réseau.

Pour communiquer, les machines ont besoin de trois éléments :

- un support physique, comme un câble ou une liaison Wi-Fi ;
- une adresse permettant d’identifier le destinataire ;
- un protocole : des règles communes pour découper, envoyer et interpréter les données.

Le programme n’accède pas directement au matériel réseau. Il demande au noyau d’appliquer ces règles : envoyer ou recevoir des données.

Les données ne circulent pas comme un seul bloc. Elles sont découpées en paquets. Chaque paquet voyage séparément, puis le destinataire reconstitue le message. Si un paquet se perd, il peut être renvoyé sans recommencer tout l’échange.

Un réseau local relie des machines proches, par exemple celles d’un appartement ou d’un bureau. Internet est l’interconnexion de beaucoup de ces réseaux.

Sur un réseau, chaque machine doit encore posséder une adresse afin que les paquets lui parviennent. Section suivante.

## Adresse

Une adresse identifie une machine sur le réseau afin que les paquets lui soient destinés.

Deux adresses coexistent :

- l’adresse **MAC** identifie une carte réseau sur le réseau local ;
- l’adresse **IP** identifie une machine pour acheminer les paquets d’un réseau à un autre.

IPv4 s’écrit avec quatre nombres compris entre 0 et 255, par exemple `192.168.1.24`.

Une même machine peut posséder plusieurs adresses IP : une pour le Wi-Fi, une pour le câble, et toujours `127.0.0.1`. Cette dernière est la boucle locale : les paquets restent dans le noyau de la machine. `localhost` désigne cette adresse.

L’adresse IP désigne la machine. Plusieurs programmes peuvent y tourner en même temps. Pour viser un programme précis, un second numéro est nécessaire : le port. Section suivante.

## Port

Le port identifie un programme sur une machine. L’adresse IP désigne la machine ; le port désigne le destinataire à l’intérieur de cette machine.

Un port est un numéro compris entre 0 et 65535. On l’écrit après l’adresse, par exemple `127.0.0.1:8080`.

Le noyau utilise ce numéro pour remettre les données au bon processus. Si aucun processus n’écoute le port demandé, la connexion est refusée.

Certains ports sont réservés par convention : `80` pour HTTP, `443` pour HTTPS, `22` pour SSH. Une application peut utiliser un autre port, souvent `8080`.

Le client possède aussi un port, attribué temporairement par le noyau, afin de recevoir la réponse.

L’association entre un programme, une adresse et un port s’appelle un socket. Section suivante.

## Socket

Un socket est le point d’accès d’un programme au réseau. Il associe un processus, une adresse et un port. Le programme l’utilise pour demander au noyau d’envoyer ou de recevoir des données.

Un serveur ouvre un socket, l’associe à une adresse et à un port, puis se met en écoute. Lorsqu’un client se connecte, le noyau crée un second socket dédié à cet échange.

Un client ouvre un socket puis demande une connexion vers l’adresse et le port du serveur.

Si aucun socket n’écoute le port demandé, le noyau refuse la connexion.

Deux processus ne peuvent pas écouter la même adresse et le même port en même temps.

Le socket transporte des octets. Il ne connaît pas le format des messages applicatifs. L’ordre, la fiabilité et la connexion de ces octets suivent le protocole de transport demandé au noyau. Section suivante.

## TCP

TCP (*Transmission Control Protocol*) est le protocole de transport que le noyau applique pour un flux d’octets ordonné et fiable.

Une connexion TCP n’est pas un câble. C’est un accord enregistré dans les deux noyaux : ports, numéros de séquence, fenêtre.

Le noyau envoie déjà des paquets isolés selon IP, sans connexion. Il utilise ces paquets pour construire ensuite l’accord TCP.

Avant d’échanger des données utiles, les deux noyaux s’envoient trois paquets IP qui portent des drapeaux TCP :

1. le noyau client envoie `SYN` : il propose de démarrer un échange ;
2. le noyau serveur répond `SYN-ACK` : il accepte ;
3. le noyau client confirme avec `ACK`.

Après ces trois paquets, les deux noyaux partagent le même état. La connexion est alors établie.

Si aucun processus n’écoute le port, le noyau refuse dès cette étape. Aucun message applicatif n’est envoyé.

Une fois la connexion établie, le noyau numérote les octets, les remet dans l’ordre, renvoie ceux qui sont perdus et contrôle le débit.

TCP ne décrit pas le format des messages applicatifs. HTTP, SSH ou d’autres protocoles s’appuient sur ce flux d’octets.

UDP est l’autre protocole de transport courant : pas de connexion, pas d’ordre, pas de retransmission. Section suivante.

## UDP

UDP (*User Datagram Protocol*) est le protocole de transport que le noyau applique pour envoyer un datagramme : un message isolé.

UDP n’ajoute pas de fiabilité à IP. Il ajoute le port, afin de viser un programme sur la machine destinataire.

Le noyau n’établit pas d’accord préalable, ne remet pas les messages dans l’ordre et ne renvoie pas un datagramme perdu.

UDP est plus léger que TCP : moins d’état dans le noyau et aucun handshake avant l’envoi. L’application doit gérer elle-même les pertes et les doublons si elle en a besoin.

TCP et UDP utilisent tous les deux une adresse et un port. Ils n’offrent pas le même contrat.

- TCP : connexion, flux ordonné, retransmission, contrôle de débit. Usage : tout doit arriver, comme une page HTTP/1.1, HTTP/2 ou une session SSH.
- UDP : pas de connexion, datagramme isolé, pas de retransmission. Usage : un paquet tardif ne sert plus, comme la voix, la vidéo live ou la position dans un jeu. DNS l’utilise aussi parce qu’une petite question peut être renvoyée par le client.

HTTP/3 s’appuie sur UDP. Il n’est pas détaillé ici.

TCP et UDP placent leurs données dans un paquet IP, qui vise une machine. Section suivante.

## IP

IP (*Internet Protocol*) est le protocole que le noyau et les routeurs appliquent pour acheminer un paquet d’une machine à une autre.

Chaque paquet porte une adresse source et une adresse destination.

Le noyau examine la destination. Si elle désigne la machine locale, le paquet reste dans le noyau. Si elle appartient au réseau local, le paquet est envoyé sur ce réseau. Sinon, il est remis à un routeur, qui le transmet au routeur suivant jusqu’à la machine cible.

IP est un service au mieux : un paquet peut être perdu, dupliqué ou arriver dans le désordre. IP ne prévoit pas de renvoi. TCP ajoute cette fiabilité. UDP ne l’ajoute pas.

IP identifie des machines, pas des programmes. Le port appartient à TCP ou à UDP.

`127.0.0.1` ne traverse aucun routeur. Internet commence lorsqu’un paquet quitte le réseau local.

Les humains retiennent des noms, pas des adresses IP. Un mécanisme doit donc traduire un nom en adresse. Section suivante.

## DNS

DNS (*Domain Name System*) traduit un nom de machine en adresse IP. Les programmes et les humains utilisent des noms ; IP n’achemine que des adresses.

Le PC envoie généralement une question à un résolveur déjà connu, souvent la box, en UDP vers le port 53. S’il a la réponse, il la renvoie. Sinon, il interroge d’autres serveurs DNS, puis répond par une ou plusieurs adresses IP.

Si la réponse ne revient pas, le client renvoie la question.

`localhost` est résolu localement vers `127.0.0.1`. Cette traduction n’emprunte pas Internet.

Le nom n’est pas une adresse. Tant qu’aucune IP n’a été obtenue, aucun paquet applicatif ne peut être acheminé vers cette machine.

Une fois l’adresse, le port et le transport connus, les programmes peuvent échanger des messages selon un format commun. HTTP est l’un de ces formats. Section suivante.