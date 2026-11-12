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

La machine exécute le logiciel.

Ce n'est pas une idée abstraite : c'est l'appareil sous vos yeux ou sous vos doigts — un PC, un téléphone, une tablette, un serveur.

Pour le faire, elle s'appuie sur quatre composants :

- **CPU** — *Central Processing Unit*, le processeur. Il exécute les instructions.
- **RAM** — *Random Access Memory*, la mémoire vive. Elle retient l'information pendant l'exécution. Sans courant, ce contenu disparaît.
- **Disque** — il conserve le logiciel, et le reste de l'information, après l'arrêt.
- **Réseau** — il relie une machine à une autre.

À travers le réseau, la machine qui contacte est le client. La machine qui reste disponible et qui répond est le serveur.

Ces composants ne sont pas utilisés directement par chaque programme. Un programme particulier les contrôle : le noyau. Section suivante.

# Noyau

**Kernel** — *noyau*

- Le noyau est un programme.
- Il contrôle l'accès au CPU, à la RAM, au disque et au réseau.
- Les autres programmes ne touchent pas ces composants directement.
- Ils passent par le noyau : chaque demande est un *appel système* (*system call*).

**Rôle**

- Accorder ou refuser l'accès au matériel.
- Allouer de la RAM.
- Lire et écrire sur le disque.
- Échanger sur le réseau.

Le noyau est le cœur d'un ensemble plus large : le système d'exploitation. Section suivante.

# Système d'exploitation

**Operating system (OS)** — *système d'exploitation*

Sans système d'exploitation, la machine ne vous offre ni écran d'accueil, ni explorateur, ni moyen simple d'ouvrir un site ou une application.

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

- Ce sont des **programmes**, donc du logiciel.
- Explorateur, bureau ou écran d'accueil, réglages : ils font partie de l'OS.
- Le navigateur fourni avec le système est aussi un programme. C'est une application : vous pouvez en installer un autre.

**Composition**

- L'OS est un logiciel : un ensemble de programmes.
- Son cœur est le noyau.
- Vous cliquez dans l'explorateur. L'explorateur demande au noyau d'accéder au disque.
- Chaque OS a son noyau. Les programmes passent par lui pour toucher au CPU, à la RAM, au disque et au réseau.

Dans chaque composant contrôlé par le noyau, l'information est représentée par des bits. Section suivante.

# Bit

**Bit** — *binary digit*, chiffre binaire

- C'est l'unité avec laquelle chaque composant représente l'information.
- Un bit a deux états : `0` ou `1`.

**Support**

- Le bit est toujours `0` ou `1`. Le support change selon le composant.
- **CPU** : une tension. Haute pour `1`, basse pour `0`.
- **RAM** : une charge dans un condensateur, réservoir électrique minuscule. Présente pour `1`, absente pour `0`.
- **Disque magnétique** : l'orientation d'une zone aimantée. Un sens pour `1`, le sens opposé pour `0`.

**Capacité**

- Un bit encode un choix à deux réponses : `oui` ou `non`, `0` ou `1`.
- Avec `n` bits, il existe `2ⁿ` choix distincts. Plus l'information demande de variantes, plus il faut de bits pour la représenter sans ambiguïté.

Le groupe de huit bits s'appelle un octet. Section suivante.

# Octet

**Octet** — *byte*

- Un octet regroupe huit bits.
- Huit n'est pas imposé par les mathématiques : c'est un compromis retenu par l'industrie.
- Il offre `2⁸`, donc `256`, combinaisons, de `00000000` à `11111111`, suffisent pour une unité pratique de stockage et d'échange.
- Dans l'usage courant, *byte* désigne un octet.

**Sens**

- Les huit bits n'indiquent pas, à eux seuls, ce qu'ils représentent.
- Le même motif `01000001` peut encoder des contenus différents selon la règle de lecture appliquée.

**Usage**

- Les composants manipulent l'information par octets.
- Une information peut occuper un ou plusieurs octets consécutifs.

La RAM range ces octets. Section suivante.

# RAM

**RAM** — *Random Access Memory*, mémoire vive

- La RAM conserve les octets pendant le traitement décrit dans le flux de l'informatique.
- Elle est organisée en cases d'un octet chacune.
- Elle est volatile : sans courant, son contenu disparaît.

**Accès**

- Le CPU lit des octets en RAM pour les traiter.
- Il écrit des octets en RAM pour conserver le résultat d'une opération.
- *Random access* : accéder à un octet ne dépend pas de sa position ; le temps d'accès reste du même ordre.

Chaque octet en RAM porte une adresse qui le désigne. Section suivante.

# Adresse

**Address** — *adresse*

- La RAM est une suite de cases. Chaque case contient un octet.
- Chaque case a un numéro : son adresse.
- Exemple : l'adresse `1000` désigne la case numéro `1000`, pas le contenu `01000001` qui peut s'y trouver.

**Rôle**

- L'adresse sert au CPU pour demander un octet précis : « donne l'octet de la case `1000` » ou « écris cet octet dans la case `1000` ».
- Le numéro n'est pas collé à l'intérieur de l'octet. C'est le CPU qui indique quel numéro il veut ; la RAM répond avec l'octet de cette case.

**Adresse comme information**

- Une adresse peut elle-même être conservée en RAM, à une autre case : « l'octet utile est à la case `1000` ».
- On le détaillera avec les pointeurs.

**Numérotation**

- Les numéros se suivent : `0`, `1`, `2`, `3`…
- Une information qui tient sur plusieurs octets occupe plusieurs cases voisines : adresse de départ et nombre d'octets.

**Sens**

- La case ne dit pas si l'octet est un caractère, un nombre ou autre chose.
- La règle qui dit comment interpréter les octets porte un nom : le type. Section suivante.