# Information

**Information** — *information*

- L'information, c'est un fait ou un détail que l'on peut connaître, conserver, recopier ou transmettre.
- Un prix, un nom, un message, une photo : ce sont des informations.

**Formes**

Valeurs :

- un nombre : `42`, `3.14`
- un caractère ou un texte : `A`, `Bonjour`
- une date ou une heure : `2026-11-10`, `14:30`
- un choix oui / non
- une couleur : `rouge` ou `#FF0000`

Médias :

- un son
- une image
- une vidéo

**Actions**

- recopier sans déformer
- modifier selon une règle
- envoyer à distance

Traiter l'information de façon automatique, c'est l'informatique. Section suivante.

# Informatique

**Computing** — *informatique*

- L'informatique est le traitement automatique de l'information.
- Automatique : des instructions écrites à l'avance s'appliquent sans que vous fassiez chaque étape à la main.

**Flux**

- Entrée : de l'information
- Traitement : des actions sur cette information (recopier, modifier, envoyer à distance)
- Sortie : de l'information

**Exemple — connexion**

Vous saisissez un identifiant et un mot de passe, puis vous validez. Le reste se fait sans vous :

- Entrée : l'identifiant et le mot de passe
- Traitement : les comparer à ce qui est enregistré
- Sortie : accès autorisé ou accès refusé

Ces instructions sont regroupées dans un programme. Section suivante.

# Programme

**Program** — *programme*

- Un programme est une suite ordonnée d'instructions.
- Il décrit le flux de l'informatique. Il ne l'exécute pas.

**Exemple — connexion**

- Entrée : identifiant et mot de passe
- Instruction 1 : recevoir l'identifiant et le mot de passe
- Instruction 2 : les comparer à ce qui est enregistré
- Instruction 3 : autoriser l'accès, ou le refuser
- Sortie : accès autorisé ou accès refusé

Un ensemble de programmes forme un logiciel. Section suivante.

# Logiciel

**Software** — *logiciel*

Un programme décrit une suite d'instructions. Seul, il ne couvre souvent qu'une partie du travail. Pour un but complet, plusieurs programmes doivent s'accorder. Cet ensemble, c'est le **logiciel**.

**Deux cas**

Vous lancez un logiciel et vous le pilotez : lire, écrire, envoyer, régler. Derrière ce que vous voyez, plusieurs programmes se partagent le travail — afficher, enregistrer, communiquer.

Un autre logiciel tourne sans que vous le lanciez : vérifier qu'une version plus récente existe, la récupérer, la préparer. Même idée — des programmes pour un but — mais vous n'êtes pas aux commandes.

La différence n'est pas le but. C'est qui pilote : vous, ou pas.

Le logiciel que vous lancez et pilotez s'appelle une application. Section suivante.

# Application

**Application** — *application*

- Une application est un logiciel que vous lancez et pilotez.
- Vous l'ouvrez pour accomplir une tâche : lire, écrire, envoyer, jouer, consulter.

**Exemples**

- un navigateur
- une messagerie
- un traitement de texte
- un jeu vidéo
- une appli météo ou carte

**Formes**

- application mobile — sur le téléphone
- application desktop — sur le PC
- application web ou site web — dans le navigateur
- sur une console

Un jeu vidéo peut prendre chacune de ces formes.

L'application décrit quoi faire. Il faut un appareil pour l'exécuter : la machine. Section suivante.

# Machine

**Machine** — *machine*

- La machine est l'appareil qui exécute le logiciel : un PC, un téléphone, une tablette, une console, un serveur.
- Pour cela, elle s'appuie sur quatre composants :

**Composants**

- **CPU** — *Central Processing Unit*, le processeur. Il exécute les instructions.
- **RAM** — *Random Access Memory*, la mémoire vive. C'est la mémoire de travail : elle retient l'information pendant l'exécution. Sans courant, ce contenu disparaît.
- **Disque** — la mémoire de stockage : il conserve le logiciel et le reste de l'information, même après l'arrêt.
- **Réseau** — il relie une machine à une autre.

Plusieurs programmes tournent en même temps et se partagent ces composants. Un programme particulier répartit cet accès : le noyau. Section suivante.

# Noyau

**Kernel** — *noyau*

- Le noyau est un programme.
- Les autres programmes ne parlent pas directement au CPU, à la RAM, au disque ou au réseau.
- Ils passent par le noyau. Chaque demande de ce type est un *appel système* (*system call*).

**Rôle**

- Décider qui a accès à quel composant.
- Accorder ou refuser cet accès.
- Partager la RAM entre les programmes.
- Lire et écrire sur le disque.
- Faire passer l'information sur le réseau.

Le noyau est le cœur d'un ensemble plus large : le système d'exploitation. Section suivante.

# Système d'exploitation

**Operating system (OS)** — *système d'exploitation*

Sans système d'exploitation, la machine ne vous offre ni écran d'accueil, ni explorateur, ni moyen simple d'ouvrir une application.

**D'où il vient**

- Il est en général déjà installé à l'achat du PC ou du téléphone.
- Le fabricant ou l'éditeur le fournit avec la machine — ou vous l'installez ensuite.

**Exemples**

- Windows — beaucoup de PC
- macOS — les Mac
- iOS — iPhone
- Android — la plupart des autres téléphones
- Linux — de nombreux serveurs, et certains PC

**Ce que vous en voyez**

- Explorateur de fichiers
- Bureau ou écran d'accueil
- Réglages
- Souvent un navigateur fourni avec le système

**Nature de ces éléments**

- Ce sont des applications fournies avec l'OS — donc du logiciel que vous lancez et pilotez.
- Explorateur, bureau ou écran d'accueil, réglages : ils font partie de ce que l'OS vous donne.
- Le navigateur fourni avec le système est aussi une application : vous pouvez en installer un autre.

**Composition**

- L'OS est un logiciel : un ensemble de programmes.
- Son cœur est le noyau.
- Vous ouvrez l'explorateur. L'explorateur demande au noyau d'accéder au disque.
- Chaque OS a son noyau. Les programmes passent par lui pour toucher au CPU, à la RAM, au disque et au réseau.

Les applications tournent sur l'OS. Pour les écrire, on utilise un langage. Java est l'un des langages les plus utilisés pour cet objectif. Section suivante.

# Java

**Java**

- Java est un langage : un vocabulaire et des règles pour écrire des programmes.
- Il a été créé chez Sun Microsystems (James Gosling et son équipe), rendu public en 1995.
- Il est aujourd'hui porté par Oracle.
- On l'utilise pour des applications et beaucoup de serveurs.

Pour écrire et lancer un programme Java, il faut un kit d'outils : le JDK. Section suivante.

# Bit

**Bit** — *binary digit*, chiffre binaire

- Dans chaque composant, l'information est portée au plus petit niveau par des bits.
- Un bit a deux états : `0` ou `1`.

**Support**

- Le bit est toujours `0` ou `1`. Le support change selon le composant.
- **CPU** : une tension — haute pour `1`, basse pour `0`.
- **RAM** : une charge dans un condensateur (minuscule réservoir électrique) — présente pour `1`, absente pour `0`.
- **Disque magnétique** : l'orientation d'une zone aimantée — un sens pour `1`, l'autre pour `0`.

**Capacité**

- Un bit suffit pour un choix à deux réponses : `oui` / `non`, `0` / `1`.
- Avec `n` bits, il existe `2ⁿ` choix distincts.
- Plus l'information a de variantes, plus il faut de bits pour la représenter sans ambiguïté.

Un bit seul ne suffit presque jamais : un caractère, un petit nombre, une couleur demandent plusieurs choix possibles à la fois. Les machines regroupent donc les bits. Le groupe standard en compte huit : l'octet. Section suivante.

# Octet

**Octet** — *byte*

- Un octet regroupe huit bits.
- Huit n'est pas une loi mathématique : c'est le compromis retenu par l'industrie.
- Un octet offre `2⁸`, donc `256`, combinaisons — de `00000000` à `11111111`.

**Sens**

- Les huit bits ne disent pas, à eux seuls, ce qu'ils représentent.
- Le même motif `01000001` peut se lire comme le nombre `65` ou comme le caractère `A`.
- Le résultat dépend de la règle de lecture.

**Usage**

- Les composants manipulent l'information par octets.
- Une information peut occuper un ou plusieurs octets à la suite.

La RAM range ces octets. Section suivante.

# RAM

**RAM** — *Random Access Memory*, mémoire vive

- La RAM est la mémoire de travail de la machine.
- Elle range les octets pendant l'exécution.
- Elle est organisée en cases : une case, un octet.
- Elle est volatile : sans courant, son contenu disparaît.

**Accès**

- Le CPU lit des octets en RAM pour les traiter.
- Il écrit des octets en RAM pour y laisser un résultat.
- *Random access* : le temps d'accès à une case ne dépend pas de sa position.

Chaque case a un numéro qui la désigne : une adresse. Section suivante.

# Adresse

**Address** — *adresse*

- La RAM est une suite de cases. Chaque case contient un octet.
- Chaque case a un numéro : son adresse.
- L'adresse `1000` désigne la case `1000`, pas l'octet `01000001` qui peut s'y trouver.

**Rôle**

- Le CPU demande un octet par son adresse : lire la case `1000`, ou y écrire.
- Le numéro n'est pas dans l'octet. Le CPU indique le numéro ; la RAM renvoie l'octet.

**Adresse comme information**

- Une adresse peut elle-même être rangée en RAM, dans une autre case.
- Cette case dit alors où se trouve l'octet utile.

**Numérotation**

- Les numéros se suivent : `0`, `1`, `2`, `3`…
- Une information sur plusieurs octets occupe des cases voisines : adresse de départ et nombre d'octets.

La case ne porte que des octets, sans dire ce qu'ils représentent. Il faut une règle de lecture : le type. Section suivante.
