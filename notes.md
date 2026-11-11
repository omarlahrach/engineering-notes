# Information

**Contenu**

- L'information est un contenu qu'on peut nommer et réutiliser.
- Elle est discrète (symbole, nombre…) ou numérisée (son, image…).
- Les exemples ci-dessous illustrent des formes courantes de ce contenu.

**Exemples — valeurs discrètes**

- `42` — un nombre entier
- `3.14` — un nombre décimal
- `A` — un caractère
- `Bonjour` — un texte
- `2026-11-10` — une date
- `14:30` — une heure
- `oui` / `non` — un booléen
- `rouge` ou `#FF0000` — une couleur

**Exemples — médias numérisés**

- un extrait musical — un son
- une photo — une image
- une séquence filmée — une vidéo

**Propriétés**

- On peut le recopier sans le déformer.
- On peut le modifier selon une règle.
- On peut le conserver ou l'envoyer à distance.

Ce contenu traité automatiquement s'appelle l'information automatique : l'informatique. Section suivante.

# Informatique

**Définition**

- L'informatique est l'information automatique.
- Une machine enchaîne recopier, modifier, conserver et envoyer, sans répéter chaque étape à la main.

**Flux**

- Entrée : de l'information.
- Traitement : des opérations sur cette information.
- Sortie : de l'information transformée ou conservée.

Ce flux s'exécute sur une machine. Section suivante.

# Machine

Une machine est un ordinateur. Elle porte le flux de l'informatique : entrée, traitement, sortie.

- **CPU** — *Central Processing Unit*, le processeur. Il exécute le traitement : recopier et modifier l'information selon une règle.

- **RAM** — *Random Access Memory*, la mémoire vive. Elle retient l'information pendant le traitement. Tant que le courant passe, elle la garde accessible. Sans courant, ce contenu disparaît.

- **Disque** — il conserve l'information après l'arrêt de la machine, ce que la RAM ne garde pas.

- **Réseau** — il envoie l'information d'une machine à une autre.

À travers le réseau, la machine qui contacte est le client. La machine qui reste disponible et qui répond est le serveur.

Dans chaque composant, l'information est représentée par des bits. Section suivante.

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