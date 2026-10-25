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