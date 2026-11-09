# Data

## Bit

**Définition**

- Bit signifie *binary digit*.
- Un bit possède deux valeurs possibles : `0` ou `1`.
- `0` et `1` nomment deux états logiques ; leur signification dépend de l’usage.

**Physique**

- Le bit est une abstraction, pas un petit objet matériel.
- Le matériel le représente avec deux états physiques distinguables.
- Exemples : deux plages de tension, présence ou absence de charge, deux orientations magnétiques.
- Deux états sont utilisés parce qu’ils restent distinguables malgré de petites perturbations physiques.

**Capacité**

- Un bit permet deux combinaisons : `0`, `1`.
- Deux bits permettent quatre combinaisons : `00`, `01`, `10`, `11`.
- Avec `n` bits, il existe `2ⁿ` combinaisons possibles.

**Sens**

- Une combinaison de bits ne porte aucun sens par elle-même.
- Une règle d’interprétation lui associe une valeur.
- Un bit peut représenter un choix, un état, une partie d’un nombre ou une partie d’une instruction.
- Une valeur booléenne peut logiquement utiliser un bit, sans forcément occuper un seul bit en mémoire.

**Limite**

- Un bit seul ne suffit pas pour représenter les nombreuses valeurs manipulées par un programme.
- Les systèmes regroupent les bits.
- Le groupe standard de huit bits s’appelle un octet.

L’octet est l’unité suivante. Section suivante.

## Octet

**Définition**

- Un octet est un groupe de huit bits.
- Il possède `2⁸`, donc `256`, combinaisons possibles.
- Elles vont de `00000000` à `11111111`.
- Dans les systèmes actuels, *byte* désigne généralement un octet.

**Sens**

- Un octet identifie une combinaison parmi `256`.
- Ses bits n’indiquent pas ce qu’ils représentent.
- Le même octet `01000001` peut être lu comme le nombre `65` ou comme le caractère `A`.
- Le résultat dépend de la manière dont le programme le traite.

**Usage**

- La mémoire est organisée en octets.
- Un fichier contient une suite d’octets.
- Un flux transporte une suite d’octets.
- Une valeur peut occuper un ou plusieurs octets.

La mémoire organise ces octets afin que le programme puisse les retrouver. Section suivante.

## Mémoire

**Définition**

- La mémoire vive, ou RAM, conserve les données utilisées pendant l’exécution.
- Elle est organisée en octets.
- Chaque octet possède une adresse : un numéro qui le désigne.
- Elle est volatile : son contenu disparaît à l’extinction de la machine.

**Adresse**

- Une adresse ne contient pas de donnée ; elle indique où se trouve un octet.
- Les adresses se suivent : `0`, `1`, `2`, `3`…
- Une valeur sur plusieurs octets occupe des adresses consécutives.
- Il suffit de connaître la première adresse et la taille pour la retrouver.

**Accès**

- Le processeur lit une adresse pour obtenir des octets.
- Il écrit des octets à une adresse pour les conserver.
- Lire ne modifie pas l’octet ; écrire remplace l’ancien contenu.

**Sens**

- La mémoire conserve les octets, pas leur signification.
- Elle n’indique pas si une adresse contient un nombre, un texte ou une instruction.
- Le programme sait ce que chaque adresse contient, car il a choisi quoi y écrire.

**Processus**

- Chaque processus reçoit sa propre vue de la mémoire.
- Une adresse valide dans un processus n’a aucun sens dans un autre.
- Un processus ne peut pas lire la mémoire d’un autre processus directement.

Le programme décide comment lire les octets placés à une adresse. Cette décision s'appelle le type. Section suivante.