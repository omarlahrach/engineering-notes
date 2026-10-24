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

Un programme est un fichier sur le disque. Il contient des instructions destinées au cpu. Tant qu'il n'est pas exécuté, il ne consomme ni cpu ni ram.

Quand le noyau l'exécute, ça devient un processus.

## Processus

Un processus est un programme en cours d'exécution.

Le noyau lit le programme sur le disque, le charge en ram, et fait exécuter ses instructions par le cpu. Chaque processus reçoit un identifiant unique attribué par le noyau, le *PID* (*process id*). Le noyau isole la ram de chaque processus : l'un n'accède pas à celle d'un autre.