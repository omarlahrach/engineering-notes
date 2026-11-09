# System

## Machine

Une machine, c'est un ordinateur : ton PC, ou un serveur. Elle a toujours quatre composants.

- `cpu :` il exécute des instructions, quelques milliards par seconde
- `ram :` l'espace de travail temporaire et rapide, limitée et volatile — on coupe le courant, tout disparaît
- `disque :` le stockage permanent — ce qui y est écrit survit au redémarrage, mais il est de l'ordre de mille fois plus lent que la RAM
- `réseau :` il permet de parler aux autres machines, et c'est le plus lent des quatre

Ce matériel n'est pas utilisé directement : c'est le rôle du noyau.

## Noyau

Le matériel — cpu, ram, disque, réseau — n'est accessible que via le noyau (*kernel*). Ici, c'est Linux.

Seul le noyau accède au cpu, à la ram, au disque et au réseau. Tout autre accès passe par un *appel système* : une demande adressée au noyau.

Ce que le noyau lance, c'est un programme sur le disque.

## Programme

Un programme est un fichier sur le disque. Il contient des instructions destinées au CPU. Tant qu'il n'est pas lancé, il ne consomme ni CPU ni RAM pour son exécution.

Le noyau peut le charger en RAM et lui créer un processus. Section suivante.

## Processus

**Définition**

- Un processus est un programme **chargé en RAM** et identifié par le noyau.
- Le fichier sur le disque reste un programme.
- Le processus est l'instance vivante en mémoire.

**Naissance**

- Une demande de lancement arrive au noyau.
- Le noyau crée le processus.
- Il attribue un *PID* (*process id*).
- Il alloue une zone de RAM isolée pour ce processus.
- Il lit le programme sur le disque et le charge dans cette RAM.

À ce moment, **le processus existe déjà**. Le CPU n'a pas encore exécuté la première instruction.

**Exécution**

- L'exécution commence quand le noyau donne le CPU au processus.
- Le CPU lit alors la première instruction en RAM.
- Il enchaîne les instructions suivantes tant que le processus tourne.

**Isolation**

- Chaque processus possède sa propre RAM.
- Un processus n'accède pas à la RAM d'un autre.

Le CPU exécute les instructions du processus une fois l'exécution commencée. Section suivante.