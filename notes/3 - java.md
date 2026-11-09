# Java

## Source

Le langage Java est un langage de programmation : des règles pour écrire des instructions. Un fichier source (extension `.java`) est un programme sur le disque, écrit avec ces règles.

Le cpu n'exécute que ses propres instructions. Un `.java` n'est pas dans ce format : le noyau ne peut pas le lancer tel quel. Le source, c'est ce que l'humain lit et modifie. Ce n'est pas un processus, et ce n'est pas ce que le cpu exécute.

Pour obtenir un format que la machine pourra exécuter plus loin, le source passe par le compilateur.

## Compilateur

Un compilateur est un programme qui traduit un source vers un autre format. En Java, ce programme s'appelle `javac`. C'est un fichier sur le disque. Quand le noyau l'exécute, c'est un processus.

`javac` lit un fichier source `.java`. Il écrit un autre fichier, qui n'est plus du langage Java et qui n'est pas des instructions cpu. Ce format s'appelle le *bytecode*.

## Bytecode

Le bytecode est le format produit par le compilateur. Sur le disque, c'est un fichier `.class` : un programme. Tant qu'il n'est pas exécuté, il ne consomme ni cpu ni ram.

Ce n'est plus du source. Ce n'est pas des instructions cpu : un cpu x86 et un cpu ARM n'ont pas les mêmes instructions. Le compilateur ne vise donc pas une machine. Il vise un format unique, le bytecode.

C'est ça qui rend Java portable : le même fichier `.class` peut être copié sur une autre machine, un autre cpu. Le noyau ne peut toujours pas le lancer tout seul. Sur chaque machine, c'est la JVM qui lit ce bytecode.

## JVM

La JVM (*Java Virtual Machine*) est le processus qui exécute le bytecode. Le programme sur le disque s'appelle `java`. Une fois lancé par le noyau, c'est un processus comme les autres : PID, ram isolée, cpu. *Virtual* ici : elle exécute du bytecode ; ce n'est pas un second ordinateur dans l'ordinateur.

Le cpu de *cette* machine ne lit pas le bytecode. Ce qui s'exécute sur le cpu, ce sont toujours des instructions cpu. La JVM passe par le noyau (appels système) pour la ram, le disque et le réseau. D'où la portabilité : le bytecode est le même partout ; la JVM, elle, est faite pour la machine où elle tourne (Linux, tel cpu, etc.).

La JVM la plus courante s'appelle HotSpot. Dans le même processus, elle a un interpréteur et deux compilateurs JIT.

Comment l'interpréteur et les compilateurs JIT s'enchaînent : section suivante.

## JIT

Le JIT (*Just-In-Time*) est un compilateur **dans le processus JVM**. Même PID. Il traduit du bytecode (déjà chargé en ram) vers des instructions cpu, et garde **cette** traduction en ram.

Mécanisme :

1. Un morceau de bytecode s'exécute (une méthode, par exemple). Ce bytecode vient du `.class` chargé en ram. Le fichier sur le disque ne change jamais : le JIT n'écrit pas un `.class`.
2. L'interpréteur le lit. À chaque appel, un compteur de ce morceau augmente.
3. Tant que le compteur est bas : encore l'interpréteur. Toute méthode commence ici. Sans ça, le JIT n'a rien à traduire.
4. Le compteur dépasse un premier seuil. **C1** traduit ce bytecode en instructions cpu et les met en ram.
  C1 traduit **vite** : peu de cpu du processus pour cette traduction, code cpu encore moyen à l'exécution.
5. Les appels suivants : le cpu exécute la copie de C1. Le compteur **peut encore monter** si la méthode continue d'être beaucoup appelée.
6. Si le compteur dépasse un **second** seuil : **C2** retraduit **la même** méthode et **remplace** la copie de C1 en ram.
  C2 traduit **lentement** : beaucoup de cpu du processus **pendant** la traduction (*traduire avec C2 coûte cher*). En échange, le code cpu est **plus rapide à chaque appel** (plus d'optimisations, ex. *inlining*).
   Si après C1 la méthode n'est presque plus appelée, le second seuil n'est jamais atteint : **C2 ne tourne pas**. On ne paie pas ce cpu pour rien.

Au démarrage du processus, presque tout est encore aux étapes 2–3. D'où un début plus lent, puis ça accélère : *warmup*.

Le JIT concerne le cpu. La ram du processus JVM, c'est le GC.

## GC

GC = *garbage collector*. En français : **ramasse-miettes**. C'est un mécanisme **dans le processus JVM**.

Le *tas* (*heap*) est la zone de ram du processus où la JVM place les **objets** (les données créées avec `new`).

Le GC parcourt le tas. Il trouve les objets dont plus aucune variable (ni aucun autre objet) ne pointe. Ces objets ne servent plus. **Ensuite** il rend **leur** ram, pour qu'un prochain `new` puisse la réutiliser.

Tu n'as pas d'instruction Java pour vider un objet. Sans GC, le tas ne ferait que grandir.

Mécanisme :

1. `new` : la JVM pose l'objet dans le tas. Cette ram est prise.
2. Tant qu'on pointe encore vers lui, il reste. Le GC ne le touche pas.
3. Plus personne ne pointe vers lui : l'objet ne sert plus. Sa ram est encore prise.
4. Le GC trouve ces objets et rend leur ram.

Pendant l'étape 4, le cpu exécute le GC. Ton code Java ne tourne pas. On appelle ça une **pause**.

La taille du tas se règle **au lancement** du processus : `-Xms` (départ), `-Xmx` (plafond). Sans ça, HotSpot choisit d'après la ram de la machine. Trop petit / trop grand = par rapport à ce que l'appli alloue.

- `-Xmx` trop petit : le tas est plein trop souvent, l'étape 4 revient trop souvent, beaucoup de pauses.
- `-Xmx` trop grand : l'étape 4 est plus rare, mais un passage peut durer plus longtemps (plus de tas à parcourir).

HotSpot a plusieurs ramasse-miettes. Java 8 : *Parallel GC*. Java 9 jusqu'à Java 25 : **G1**. ZGC et Shenandoah existent, ce n'est pas le défaut. On ne les détaille pas ici.

Le GC ne gère pas la *stack*. C'est une autre zone de ram du même processus. Section suivante.

## Stack

La *stack* (en français : **pile**) est une zone de ram **dans** le processus JVM. Ce n'est pas le tas. Le GC gère le tas. Il ne gère pas la stack.

Le noyau réserve **un** bloc de ram : ça, c'est la stack. Dedans, la JVM pose des **petits blocs**, un par appel de méthode. Un petit bloc s'appelle une *frame* (cadre de pile). Il contient les variables locales et les **références**. Une référence, c'est l'adresse d'un objet. L'objet lui-même est dans le **tas**.

Exemple : `Foo foo = new Foo();`

- `new Foo()` : l'objet est dans le tas
- `foo` : la référence est dans la frame, donc **dans** la stack. Elle pointe vers le tas.

Mécanisme :

1. On entre dans une méthode : la JVM empile une frame **dans** la stack. Cette ram de stack est prise.
2. La méthode tourne. Sa frame reste au sommet.
3. La méthode finit : la JVM dépile cette frame. Cette ram de stack est libre tout de suite.
  L'objet dans le tas n'est **pas** effacé ici. Si plus aucune référence ne pointe vers lui, le GC pourra rendre la ram du tas **plus tard**. Si une autre référence existe encore, l'objet reste dans le tas.

La stack a une **taille fixe** (`-Xss`, souvent ~1 Mo). Chaque frame prend un morceau de cette taille. S'il y a trop d'appels imbriqués (ex. une méthode qui s'appelle elle-même sans fin), les frames dépassent cette taille. La JVM lance `StackOverflowError`.

Il y a **une** stack par **fil d'exécution**. Ce fil s'appelle un *thread*. Section suivante.

## Thread

Un *thread* (en français : **fil d'exécution**) est ce que le cpu exécute **dans** un processus. Le processus, c'est la boîte (PID, ram). Le thread, c'est le fil qui avance dans le code.

Un processus commence avec un thread : `main`. La JVM en crée d'autres dans **le même** PID : GC, JIT (C1, C2), etc.

Tous les threads du processus **partagent le tas**. Ils ne partagent **pas** la stack : **une stack par thread** (donc un `-Xss` par thread). D'où le coût : 200 threads ≈ 200 Mo de stacks si `-Xss` vaut 1 Mo, **en plus** du tas (`-Xmx`).

Le noyau place les threads sur les cœurs du cpu. Deux cœurs : deux threads peuvent **calculer au même instant**. Plafond = nombre de cœurs (`nproc`). Ça, c'est le **parallèle**.

S'il y a plus de threads que de cœurs, le noyau les fait tourner **à tour de rôle**. Un seul cœur avance plusieurs threads, mais pas au même instant : il commute. Plusieurs travaux sont **en cours**, sans être tous en train de calculer. Ça, c'est la **concurrence**.

Un thread qui attend (I/O) ne prend pas le cpu : le noyau peut donner le cœur à un autre thread. D'où l'intérêt d'avoir **plusieurs** threads même avec **peu** de cœurs, si le travail attend souvent.

Un thread Java **plateforme** = un thread Linux. Le PID est celui du processus. Le thread Linux a son propre id (`nid` dans un dump).

Java 8 jusqu'à Java 20 : c'est ce modèle. Java 21 jusqu'à Java 25 : les *virtual threads* existent (beaucoup de threads Java sur peu de threads Linux). On ne les détaille pas ici.

Le processus JVM, c'est le programme `java` une fois lancé par le noyau : `main`, GC, JIT, tas, stacks. `java` est un fichier sur le disque. Il n'arrive pas tout seul : il est livré dans le JDK, avec le compilateur `javac` et d'autres outils.

## JDK

Le JDK (*Java Development Kit*) est le kit que tu **installes** sur le disque.

Il contient :

- `javac` : le compilateur (source → bytecode)
- `java` : le programme qui lance la JVM
- les bibliothèques nécessaires à l'exécution
- d'autres programmes (outils), qu'on verra en les lançant

La partie « lancer sans compiler » (`java` + bibliothèques) s'appelait le JRE. Java 8 : JRE ou JDK, deux installs. Java 9 jusqu'à Java 25 : plus de JRE à part, c'est **déjà dans** le JDK. Un seul install.

Le JDK est un **dossier** sur le disque.

`JAVA_HOME` est une variable : elle stocke **le chemin** de ce dossier. des outils s'en servent pour savoir **quel** JDK utiliser.

`PATH` est une liste de dossiers. Le shell y cherche les commandes. Si `bin` de ce JDK y est, `java` et `javac` marchent. `java -version` affiche **celui** qui est trouvé en premier.

Ce kit ne sort pas de nulle part. Il est fabriqué à partir d'un **source**. Ce source s'appelle OpenJDK. Section suivante.

## OpenJDK

OpenJDK, ce n'est **pas** le dossier JDK. C'est le **projet source** : les fichiers à partir desquels on fabrique `javac`, le programme `java` (la JVM **HotSpot**), et les bibliothèques.

Ce source est **ouvert**. N'importe qui peut le compiler et le ranger en dossier. Tu ne fais pas ça à la main : un **vendeur** le fait. Le dossier qu'il livre, c'est le **JDK**.

D'où **plusieurs** JDK pour **un** OpenJDK. Même source → même Java : même `javac`, même `java`, même bytecode, même HotSpot. Un `.class` compilé avec l'un s'exécute avec l'autre.

Ce qui **change** :

- **qui** a fabriqué le dossier (`java -version` l'affiche)
- la **licence** : le droit de l'utiliser, surtout une fois en production
- **combien de temps** ce vendeur publie des correctifs

Vendeurs :

- **Oracle JDK** : kit d'Oracle (Oracle a racheté Sun, le créateur de Java). Même base OpenJDK / HotSpot. La licence n'est **pas** toujours gratuite en production : il faut la lire.
- **Eclipse Temurin** : kit de la fondation Eclipse (projet *Adoptium*). Même OpenJDK. Gratuit, y compris en production. C'est souvent celui qu'on prend si on ne veut pas Oracle.
- **Amazon Corretto** : kit d'Amazon. Même OpenJDK. Courant sur les machines Amazon.
- D'autres suivent le même principe : Microsoft, Azul Zulu, Red Hat, etc.

Tu choisis un vendeur, tu installes **son** JDK. Ce n'est pas un autre langage.

Ce JDK, c'est le Java du PC et du serveur. Java se coupe aussi selon l'**usage**. Ces coupes s'appellent des **éditions**. Section suivante.

## Éditions

Une **édition**, c'est **pour quel usage** : quelles bibliothèques sont dans le kit.

**Sun** a créé Java, puis l'a coupé en **trois** éditions. Voici les trois, et **qui les tient** aujourd'hui.

- **Java SE** (*Standard Edition*) : PC et serveur. Langage, JVM, bibliothèques de base. OpenJDK est le source de **cette** édition. Les vendeurs livrent un JDK **SE**. C'est ce qu'on utilise. **Maintenant : Oracle** (il a racheté Sun).
- **Java EE** (*Enterprise Edition*) : serveurs, **en plus** de SE. Pas un OpenJDK : tu gardes un JDK SE, tu ajoutes des bibliothèques **dessus**. **Maintenant : la fondation Eclipse**, sous le nom **Jakarta EE**. Oracle lui a donné EE. On verra ça plus tard.
- **Java ME** (*Micro Edition*) : petits appareils. Autre kit, pas OpenJDK. **Maintenant : encore Oracle**. La ligne n'est plus vraiment développée. On n'en a pas besoin.

Eclipse a **deux** rôles : Temurin = un JDK **SE** ; Jakarta EE = les bibliothèques **serveur**. Ce n'est pas le même produit.

On installe un JDK **SE**. Ce SE n'est pas figé : le langage, la JVM, les bibliothèques avancent. Chaque étape a un **numéro**. Ça s'appelle une **version**. Section suivante.

## Version

La **version**, c'est le numéro du JDK SE que tu installes.

Tu prends un JDK **21**. On dit Java 21. Dans ce dossier, `javac`, le programme `java` et les bibliothèques sont **tous** 21.

Temurin 21 et Oracle JDK 21 : deux vendeurs, **le même** Java 21.

`java -version` lit ce numéro. `javac -version` doit dire la même chose : les deux fichiers sont dans **ce** dossier.

Depuis Java 9, un nouveau numéro arrive souvent. Pour la plupart, les correctifs s'arrêtent vite. Pour **8, 11, 17, 21, 25**, ils durent **des années**. Ces versions s'appellent *LTS* (*Long Term Support*).

Tu compiles avec `javac` **8**. Tu lances avec `java` **21** : ça marche. La JVM récente comprend l'ancien bytecode. Ça s'appelle la **rétrocompatibilité**.

Tu compiles avec `javac` **21**. Tu lances avec `java` **8** : ça refuse. L'ancienne JVM ne connaît pas ce bytecode.

On ne garde pas tous les numéros. On en choisit **un**, en général un LTS.

Ce JDK-là, il faut le **mettre sur le disque**. Ça s'appelle l'**installation**. Section suivante.

## Installation

L'**installation**, c'est copier sur le disque le dossier JDK du **vendeur**, pour la **version** choisie.

Tu ne compiles pas OpenJDK. Le vendeur l'a déjà fait. Tu récupères **son** dossier : son site, ou un programme qui le télécharge pour toi.

Le dossier seul ne suffit pas. Tu branches le shell **à la main** :

1. Tu mets dans `JAVA_HOME` le chemin de **ce** dossier.
2. Tu ajoutes son `bin` au `PATH`, pour que le shell trouve `java` et `javac`.
3. Tu lances `java -version` : la version choisie, et le nom du vendeur. Puis `javac -version` : le même numéro.

S'il y a **plusieurs** JDK sur le disque, une seule ligne `bin` gagne : la **première** dans le `PATH`. `java -version` dit lequel.

Sans ce dossier, le noyau n'a pas de programme `java` à lancer. Pas de processus JVM.

`java` et `javac` sont trouvés. Reste à s'en servir sur un fichier. Section suivante.

## Lancement

Un fichier source Java porte l'extension `.java`. `javac` lit ce source et produit un ou plusieurs fichiers `.class` contenant le bytecode.

La commande `javac Nom.java` compile le fichier. Si elle réussit, elle ne produit généralement aucun message et écrit les `.class` sur le disque.

La commande `java Nom` lance une JVM et lui demande de charger la classe `Nom`. On donne un nom de classe, sans `.java` ni `.class`.

La JVM cherche cette classe dans le *classpath*. Si aucun *classpath* particulier n'est fourni, le dossier courant sert de point de départ.

Une fois la classe chargée, la JVM cherche le point d'entrée `main` et l'exécute.

Java 25 autorise aussi les *compact source files*. La classe peut ne pas être écrite explicitement : le compilateur crée une classe implicite à partir du nom du fichier. Cette forme convient aux petits programmes. Les applications structurées utilisent généralement des classes explicites, des packages et plusieurs fichiers.

Depuis Java 11, `java Nom.java` peut compiler et lancer directement un source simple. Cette forme masque le fichier `.class` intermédiaire. Dans un projet, compilation et lancement restent généralement deux étapes séparées, pilotées plus tard par un outil de build.

Dans un programme simple, le processus se termine après `main`. Plus précisément, la JVM reste vivante tant qu'au moins un thread non-*daemon* tourne.

## Package

Un *package* regroupe des types Java sous un espace de noms. Il évite les collisions entre des classes qui portent le même nom et organise une application en ensembles cohérents.

Le nom complet d'une classe combine son package et son nom. La JVM utilise ce nom complet pour retrouver son fichier `.class`.

Après compilation, l'arborescence des `.class` reproduit celle des packages. Le *classpath* ne pointe pas directement vers le package : il pointe vers la racine à partir de laquelle cette arborescence commence.

Le package non nommé convient aux programmes simples. Une application structurée utilise des packages nommés.

Avec plusieurs sources, `javac` doit connaître chaque fichier à compiler et produit une arborescence de `.class` correspondant aux packages.

Déplacer ou livrer tous ces fichiers séparément n'est pas pratique. Java permet de les regrouper dans une seule archive : le JAR. Section suivante.

## JAR

Un JAR (*Java Archive*) est une archive ZIP qui regroupe des fichiers `.class`, leurs ressources et des métadonnées. L'arborescence interne conserve celle des packages.

Un JAR de bibliothèque fournit du code à une autre application. Il n'a pas besoin de point d'entrée.

Un JAR d'application peut déclarer sa classe principale dans `META-INF/MANIFEST.MF`. Il contient alors l'information nécessaire pour savoir où commencer l'exécution.

L'outil `jar` est livré avec le JDK. Il ne compile pas les sources : il regroupe des fichiers déjà compilés.

La commande `jar --create --file application.jar -C out .` crée `application.jar` avec tout le contenu du dossier `out`.

- `--create` demande la création d'une archive ;
- `--file` indique son nom ;
- `-C out` place temporairement l'outil dans le dossier `out` ;
- `.` sélectionne tout son contenu.

L'option `--main-class` ajoute la classe principale au manifeste.

La commande `jar --list --file application.jar` affiche le contenu de l'archive sans l'extraire.

La commande `java -jar application.jar` lance une JVM, lit le manifeste et exécute la classe principale.

Un JAR contient du bytecode, pas des instructions cpu. Il nécessite donc toujours une JVM compatible.

Créer une application manuellement impose de nettoyer les anciens fichiers, compiler tous les sources, exécuter les tests puis produire l'archive. Un outil de build automatise cette chaîne.