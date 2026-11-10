# Data

## Mémoire

**Définition**

- La mémoire vive, ou RAM, conserve les valeurs pendant l'exécution.
- Le CPU y lit et y écrit.
- Le programme chargé par le noyau s'y trouve.
- Elle est volatile : son contenu disparaît à l'extinction.

Une valeur en RAM est faite de bits. Section suivante.

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