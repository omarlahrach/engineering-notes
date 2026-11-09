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

## Cycle

**Fetch** — *récupération*

- La **control unit** lit une instruction du programme en RAM.
- Elle la place dans un **register**.

**Decode** — *décodage*

- La **control unit** interprète l'instruction.
- Elle détermine l'opération : lire, écrire, additionner, comparer.

**Execute** — *exécution*

- Si l'instruction demande un calcul, la **ALU** travaille sur les valeurs dans les **registers**.
- Si l'instruction demande une lecture en RAM, la **control unit** charge la valeur dans un **register**.

**Write back** — *écriture du résultat*

- Le résultat est écrit dans un **register** ou renvoyé en RAM.
- La **control unit** passe à l'instruction suivante du programme.

Fetch, decode, execute et write back se répètent en boucle.

Un même chip peut contenir plusieurs processeurs complets. Section suivante.

## Cœur

**Core** — *cœur*

- Un **chip** peut contenir plusieurs **cores**.
- Un core est un processeur complet : sa propre **control unit**, **ALU** et **registers**.
- Chaque core exécute son propre **cycle**, indépendamment des autres.

**Un fil**

- Un **fil d'exécution** (*thread*) est une suite d'instructions enchaînées.
- À un instant donné, il tourne sur **un seul** core.
- Quatre cores n'accélèrent **pas** ce fil unique : il ne se divise pas tout seul sur les quatre.

**Concurrence** — *concurrency*

- Plusieurs tâches **avancent** en même temps dans le programme global.
- Elles ne **calculent pas** toutes au même instant sur le CPU.
- Exemple : un core sert le fil A, puis B, puis A, puis B.
- C'est possible **même avec un seul core** : le noyau alterne.

**Parallèle** — *parallelism*

- Plusieurs tâches **calculent au même instant**.
- Chacune sur un **core** distinct.
- Exemple : core 1 sur le fil A, core 2 sur le fil B, simultanément.
- **Impossible avec un seul core** au même instant.

- Tout parallèle est concurrent.
- La concurrence n'est pas toujours parallèle.

Le CPU lit et écrit des valeurs en RAM. Section suivante.