# Compte-rendu TP-02

## 1. Secure Shell

### 1.2 Authentification par clef / G´en´eration de clefs

`ssh-keygen` pour générer une clé privée et publique

Mauvaise idée de ne pas mettre de passphrase dans un cas réel :
Si quelqu'un a accès a notre clé privée, il aussi probablement accès à la clé publique qui est sur la machine.
L'avantage de la "passhprase" est que si une personne est capable de lire notre clé privée, elle ne peux pas l'utiliser car protéger par cette dite passphrase.

### 1.3 Authentification par clef / Connection serveur

`ssh-copy-id root@IP` : pour copier la clé privé/public de la machine hote vers la VM.

### 1.4 Authentification par clef : depuis la machine

Dans le fichier ssh
`ssh -i id_rsa root@IP`

### 1.5 Sécuriser

Pour sécuriser l'accès à la machine, la prochédure :

- Se connecter à sa machine virtuelle
- vi /etc/ssh/ssh_config
- Après que le fichier se soit ouvert -> modifier la ligne `permitAuthentication`
- Relancer ssh avec `systemctl restart ssh`

#### Attaque de type brute-force-ssh

Une attaque par force brute utilise une approche par essais et erreurs pour deviner systématiquement les informations de connexion, les informations d'identification et les clés de cryptage. L'attaquant soumet des combinaisons de noms d'utilisateur et de mots de passe jusqu'à ce qu'il obtienne la bonne combinaison.

## 2. Processus

### 2.1 Etude des processus UNIX

##### 1

1. Commande ps

   `ps -eo user,pid,%cpu,%mem,stat,start,time,command`

2. Que signigie TIME :

Temps CPU cumulé, utilisateur plus système. Le format d'affichage est normalement « MMM:SS », mais peutêtre déplacé vers la droite si des processus ont cumulé plus de 999 minutes de temps CPU.

3. Processus ayant le plus utilisé le processeur

Top car il est fonctionnel (affiche les données qui se rafraichissent toutes les 3 secondes).

4. Premier processus lancé;

systemd

5. L'heure à laquelle la machine à démarrer

Il y a la commande `uptime`, et on peut aussi utiliser `who -b`

6. Nombre approximatif de processus créés depuis le démarrage (“boot”)

En utilisant la commande : `ps -o pid | tail -1`

##### 2

Pour afficher le PPID d'un processus : `ps axo ppid`
Pour afficher la liste ordonnée de tous les processus ancêtres de la commande ps en cours d’exécution : `ps -e --sort=-pid`

##### 4

Pour trier par "resident memory" :

- cliquer sur f lorsqu'on est dans top
- f pour afficher une liste d'élémént pour modifier les données affichées dans top, l'élément RSS correspond a "Resident memory"
- espace pour le sélectionner
- q pour revenir dans top

Le proccessus le plus gourmand top => car en cours `top`
`man top` => Affiche des informations triés concernant les processus.

`Top z` pour changer la couleur du terminal;
`Top x` pour mettre en avant le tri

`htop` : interactive process viewer => permet de scroller verticalement et horizontallement, et intéragir avec la souris. On peut observer tout les processus en route sur le système.

## 3. Arrêt d'un processus

Donner le droit d'éxécution au fichier sh
`chmod +x *.sh`
Pour lancer le script
`./date.sh`
`./date-toto.sh`

Ensuite il suffit de récupérer le pid et de lancer la command
`ps kill -9 PID`
`ps` : command utilisé pour lister les informtations à propos des processus en cours.
`kill -9` : command utilisé pour envoyer un au processus pour l'arrêter. Le signal '-9' est un signe spécial pour forcer la fermeture du processus.
`PID`: concernce le processus ID qu'on souhaite fermer.

## 4. Les tubes

`cat` : concaténer de fichiers et imprimer sur la sortie standard
`tee` : read from standard input and write to standard output and files read from standard input and write to standard output and files

`cat` est utilisé pour afficher le contenu de fichier, alors que `tee` est utilisé pour capturé et simultanément affiché. Elles servent différentes utilisations et ne sont pas interchangeables.

`ls | cat` : liste les dossiers et fichiers du dossier courant. Donc si je suis dans le dossier Developer, je vais lister les dossiers et fichiers de ce dernier.

`ls -l | cat > liste` : Permet de créer un fichier un nouveau fichier appelé name.

`ls -l | tee liste` : Pert de voir le détail des dossier listé dans le terminal et le meme détails des dossiers enregistré dans le fichier liste grâce à tee qui récupére et ecris dans le fichier liste.

` ls -l | tee liste | wc -l` : Permet de voir un nombre dans le terminal représentant le nombre de dossiers et de fichiers du fichier courant.
Permet aussi de sauvegarder le nombre dans le fichier liste grâce a `tee`
