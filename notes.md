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

Dans chaque composant, l'information est portée par des bits. Section suivante.

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

# Type

**Type**

- Le type est la règle de lecture des octets à partir d'une adresse.
- Il fixe : combien d'octets lire, comment les interpréter, quelles actions sont permises.

**Exemple**

- Même adresse `1000`, même octet `01000001`.
- Type nombre : on lit `65`.
- Type caractère : on lit `A`.
- L'octet en RAM ne change pas. Seule la règle change.

**Taille**

- Le type dit combien d'octets prendre depuis l'adresse.
- Un type peut lire 1 octet ; un autre, 4.
- À la même adresse, deux types ne lisent pas forcément la même quantité.

**Actions**

- Le type autorise ou refuse une action.
- Sur un nombre, `+ 1` a un sens.
- Sur un caractère, la même action n'a pas le même sens.

C'est le programme qui fixe le type quand il lit ou écrit en RAM. Pour écrire ce programme, on utilise un langage de programmation. Section suivante.

# Java

**Java**

- Java est un langage de programmation : un vocabulaire et des règles pour écrire des programmes.
- Il a été créé chez Sun Microsystems (James Gosling et son équipe), rendu public en 1995.
- Il est aujourd'hui porté par Oracle.
- On l'utilise pour des applications et beaucoup de serveurs.

Un programme Java s'écrit d'abord en texte. Ce texte s'appelle le code source. Section suivante.

# Code source

**Source code** — *code source*

- Le code source est le programme écrit en texte, dans le langage choisi — ici Java.
- Tu peux l'ouvrir, le lire, le modifier dans un éditeur.
- En Java, le fichier porte en général l'extension `.java`.
- Sur le disque, ce n'est encore qu'un fichier texte : pas un programme en train de tourner.

**Exemple — panier**

Tu fais des courses. Chaque article a un nom et un prix. Tu veux le total à payer.

```java
public class Cart {

    static class Product {
        String name;
        int price;

        Product(String name, int price) {
            this.name = name;
            this.price = price;
        }
    }

    static int total(Product[] products) {
        int sum = 0;
        for (int i = 0; i < products.length; i++) {
            sum = sum + products[i].price;
        }
        return sum;
    }

    public static void main(String[] args) {
        Product[] products = {
            new Product("bread", 2),
            new Product("milk", 1),
            new Product("pasta", 3)
        };
        int result = total(products);
        System.out.println(result);
    }
}
```
- Fichier : `Cart.java`
- À l'écran, une fois le parcours terminé : `6`

**Ce que cet exemple permettra de voir plus loin**

- types, classe, objet, tableau, boucle, méthode
- pile, tas, CPU, RAM
- compilation puis exécution jusqu'à l'affichage

**Limite**

- La machine n'exécute pas ce texte tel quel.
- Il faut une transformation : la compilation.

Le programme qui effectue cette transformation s'appelle un compilateur. Section suivante.

# Compilateur

**Compiler** — *compilateur*

- Le compilateur est un programme.
- Il lit le code source et le transforme en fichiers `.class`.
- Cette transformation s'appelle la *compilation*.

**Entrée et sortie**

- Entrée : `Cart.java`
- Sortie : `Cart.class` et `Cart$Product.class` — un fichier `.class` par type
- Si le source viole les règles du langage, la compilation échoue et rapporte l'erreur.

**En Java**

- Le compilateur s'appelle `javac`.
- On le lance depuis un terminal, dans le dossier où se trouve `Cart.java`.
- On écrit :

```text
javac Cart.java
```

- `javac` : le programme compilateur
- `Cart.java` : le fichier source à compiler

**Limite**

- Compiler ne lance pas le panier.
- Après `javac`, le `6` n'apparaît pas encore à l'écran.

Un fichier `.class` ne contient pas du texte Java. Il contient du bytecode. Section suivante.

# Bytecode

**Bytecode**

- Après `javac Cart.java`, `Cart.class` et `Cart$Product.class` ne contiennent plus le texte Java.
- Ils contiennent du **bytecode** : une suite d'instructions compactes, produites par le compilateur.

**Nom**

- *Byte* signifie octet.
- Chaque instruction de bytecode commence en général par un octet qui indique l'opération : charger une valeur, additionner, terminer une méthode…
- Le reste de l'instruction tient aussi sur un ou quelques octets.
- D'où le nom *bytecode* : un code fait d'octets, plus du texte comme `Cart.java`.

**Limite**

- Le CPU ne lit pas ce bytecode directement.
- Il faut un programme qui l'interprète ou le traduit vers les instructions du CPU.

Ce programme s'appelle la JVM. Section suivante.

# JVM

**JVM** — *Java Virtual Machine*, machine virtuelle Java

- La JVM est un programme.
- Elle charge le bytecode des fichiers `.class` et le fait s'exécuter.

**Commande**

- Une fois les `.class` produits :

```text
java Cart
```

- `java` démarre la JVM.
- `Cart` désigne la classe qui contient `main`.

**Rôle**

- Lire le bytecode.
- Enchaîner ce qu'il demande : calculs, objets, appel à `println`…
- Passer par l'OS et le noyau pour la mémoire, les fichiers, l'affichage.

**Portabilité**

- Le même `.class` tourne sur un autre OS si une JVM y est installée.
- On ne recompile pas `Cart.java` pour chaque machine : on y installe une JVM.

La JVM s'appuie sur des bibliothèques déjà compilées — comme `java.lang` pour `System.out`. Section suivante.

# Bibliothèque

**Library** — *bibliothèque*

- Une bibliothèque est du code déjà écrit, fourni pour être réutilisé.
- Elle est en général **déjà compilée** (fichiers `.class`).
- Tu ne la recompiles pas à chaque fois : la JVM la charge et l'associe à ton programme.
- Tu peux aussi **créer ta propre** bibliothèque : du code compilé une fois, réutilisé par plusieurs programmes.

**Dans `Cart.java`**

- La seule pièce prise dehors, c'est `System.out.println(result)`.
- `System` vient de la bibliothèque `java.lang`.
- `java.lang` est disponible automatiquement : aucun `import` n'apparaît dans le fichier.

Ces fichiers `.class` de bibliothèque sont souvent regroupés dans une archive : le JAR. Section suivante.

# JAR

**JAR** — *Java ARchive*

- Un JAR est une archive : plusieurs fichiers `.class` (et parfois d'autres fichiers) regroupés en un seul fichier `.jar`.
- Ça simplifie le partage et l'utilisation d'une bibliothèque : un fichier au lieu d'un dossier de classes.
- La JVM peut charger des classes depuis un JAR.
- Une bibliothèque que tu crées toi-même peut aussi être empaquetée en JAR.
- Pour `Cart`, aucun JAR n'est nécessaire : `Cart.class` et `java.lang` suffisent.

Sans installation dédiée, ni JVM, ni outil `jar`, ni `java.lang` ne sont sur la machine. Ces pièces — runtime, outil d'archive, bibliothèques de base — arrivent ensemble avec le JDK. Section suivante.

# JDK

**JDK** — *Java Development Kit*

- Le JDK est un **logiciel** : le kit qui regroupe tout ce qu’il faut pour écrire, compiler et exécuter un programme Java sur une machine.
- Ce n’est pas une application : tu ne lances pas « le JDK », tu utilises ses programmes (`javac`, `java`, `jar`).
- Sans ce kit, ces programmes n’existent pas ensemble sur la machine.

**Ce qu’il contient**

- `javac` : le compilateur — transforme le code source (`.java`) en bytecode (`.class`).
- `java` : la commande qui démarre une JVM pour exécuter ce bytecode.
- l’outil `jar` : regroupe des `.class` (et d’autres fichiers) dans une archive `.jar`.
- des bibliothèques de base, dont `java.lang` (`System`, etc.), déjà compilées.

**OpenJDK**

- *OpenJDK* est l’implémentation libre de référence de ce kit.
- Oracle JDK, Temurin, Corretto et d’autres en dérivent. Licence et support changent ; le contenu de base reste celui d’OpenJDK.

**Versions**

- Chaque kit porte un numéro : 8, 11, 17, 21, 25…
- Les versions **LTS** (*Long-Term Support*) sont maintenues longtemps.
- Le numéro du kit fixe jusqu’où vont le langage, le bytecode et les bibliothèques fournies.

Avec un JDK, la chaîne pour `Cart` est complète : `javac` produit les `.class`, `java` lance la JVM, `java.lang` est là pour `System.out.println` — le terminal affiche `6`. Section suivante.
