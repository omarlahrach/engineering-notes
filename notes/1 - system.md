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

- Un processus est un programme en cours d'exécution.
- Le programme reste un fichier sur le disque.
- Le processus est ce fichier chargé et exécuté.

**Démarrage**

- Le noyau lit le programme sur le disque.
- Il le charge en RAM.
- Le CPU exécute ses instructions.

**Identité**

- Le noyau attribue à chaque processus un *PID* (*process id*).
- Ce numéro identifie le processus pendant qu'il tourne.

**Isolation**

- Le noyau sépare la RAM de chaque processus.
- Un processus n'accède pas à la RAM d'un autre.

Le CPU est le composant qui exécute les instructions chargées en RAM. Section suivante.