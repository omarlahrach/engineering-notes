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