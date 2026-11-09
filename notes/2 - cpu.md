# CPU

## Définition

- *CPU* signifie *Central Processing Unit*.
- En français : **processeur**.
- C'est le composant qui **exécute les instructions** du programme chargé en RAM par le noyau.
- Il ne garde pas tout le programme en permanence à l'intérieur de lui. Il lit une instruction, l'exécute, puis passe à la suivante.

À l'intérieur, le CPU est divisé en plusieurs parties. Section suivante.

## Composant

**Control unit** — *unité de contrôle*

- Enchaîne les étapes d'exécution.
- Indique quelle instruction lire en RAM.
- Décide quand passer à l'instruction suivante.

**ALU** — *Arithmetic Logic Unit*, unité arithmétique et logique

- Effectue les calculs : addition, soustraction, comparaison.
- Ne choisit pas quelle instruction lire : elle calcule ce qu'on lui demande.

**Register** — *registre*

- Petits emplacements **dans** le CPU.
- Très rapides, en nombre limité.
- Conservent temporairement une valeur pendant un calcul.
- Le CPU y place une valeur lue en RAM avant d'opérer.

Les registers sont dans le CPU. La RAM est à l'extérieur.

Ces trois parties coopèrent selon un enchaînement fixe. Section suivante.