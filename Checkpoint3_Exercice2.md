# Partie 1 : Gestion des utilisateurs

## Q.2.1.1 Sur le serveur, créer un compte pour ton usage personnel.

`adduser alex`

En mot de passe j'ai défini Azerty1* que j'ai du taper 2 fois

Pour le reste j'ai juste taper Enter pour laisser par défaut

Puis j'ai valider en tapant o

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20110118.png?raw=true)

## Q.2.1.2 Quelles préconisations proposes-tu concernant ce compte ?

Je recommande de lui donner le minimum de droit pour éviter différents problèmes, je pourrais lui donner un mot de passe fort, je pourrais aussi faire une surveillance des logs pour voir les connexion échouées et activité anormale

# Partie 2 : Configuration de SSH

## Q.2.2.1 Désactiver complètement l'accès à distance de l'utilisateur root.

depuis le compte root taper :

`nano /etc/ssh/sshd_config`

Chercher la ligne PermitRootLogin, la désanoté et mettre no

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20111032.png?raw=true)

Ne pas oublier de faire un :

`systemctl restart ssh`

## Q.2.2.2 Autoriser l'accès à distance à ton compte personnel uniquement.

Toujours dans le fichier sshd_config j'ai rajouter à la fin:

`AllowUsers alex`

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20111451.png?raw=true)

Ne pas oublier de faire un :

`systemctl restart ssh`

## Q.2.2.3 Mettre en place une authentification par clé valide et désactiver l'authentification par mot de passe

# Partie 3 : Analyse du stockage

## Q.2.3.1 Quels sont les systèmes de fichiers actuellement montés ?

Nous voyons du linux, ext2, LVM2, et SWAP

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20112535.png?raw=true)

## Q.2.3.2 Quel type de système de stockage ils utilisent ?

Nous voyons sur l'image ci-dessous le type de stockage sur chaque ligne après type

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20111959.png?raw=true)

## Q.2.3.3 Ajouter un nouveau disque de 8,00 Gio au serveur et réparer le volume RAID

Nou voyons que l'état du raid est degraded

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20112920.png?raw=true)

On éteint la VM
On ajoute un nouveau disque de 8GO

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20113104.png?raw=true)

On redémarre la VM

Taper `lsblk` pour voir le nouveau disque sur sdb

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20113605.png?raw=true)

Tape `fdisk /dev/sdb`

Puis n pour nouvelle partition, p pour une partition primaire, trois fois sur Enter pour laisser pas défaut

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20113909.png?raw=true)

Ensuite taper t puis FD pour passer la partition en Linux Raid et w pour quitter

Taper la commande `mdadm --add /dev/md0 /dev/sdb1` pour ajouter la nouvelle partition au raid existant

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20114454.png?raw=true)

Le statut du raid n'est plus en degraded

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20114906.png?raw=true)

## Q.2.3.4 Ajouter un nouveau volume logique LVM de 2 Gio qui servira à héberger des sauvegardes. Ce volume doit être monté automatiquement à chaque démarrage dans l'emplacement par défaut : /var/lib/bareos/storage.

En tapant la commande `vgs` nous avons les informations suivante:

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20115458.png?raw=true)

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20115710.png?raw=true)

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20120042.png?raw=true)

Taper `nano /etc/fstab`

Ajouter `/dev/cp3-vg/backup /var/lib/bareos/storage ext4 defaults 0 0` à la fin du fichier

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20120355.png?raw=true)

## Q.2.3.5 Combien d'espace disponible reste-t-il dans le groupe de volume ?

il reste 1,79g

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20120521.png?raw=true)

# Partie 4 : Sauvegardes

## Q.2.4.1 Expliquer succinctement les rôles respectifs des 3 composants bareos installés sur la VM.

bareos-dir gere et supervise les sauvegarde et restauration

bareos-sd  gere le stockage des données sauvegardé

bareos-fd est agent sur les clients qui sert à la gestion des données à sauvegardé

# Partie 5 : Filtrage et analyse réseau

## Q.2.5.1 Quelles sont actuellement les règles appliquées sur Netfilter ?

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20121230.png?raw=true)

## Q.2.5.2 Quels types de communications sont autorisées ?

loopback, tcp port 22 (ssh), icmp, icmpv6

## Q.2.5.3 Quels types sont interdit ?

Tout les autres que ceux cité au dessus par défaut

## Q.2.5.4 Sur nftables, ajouter les règles nécessaires pour autoriser bareos à communiquer avec les clients bareos potentiellement présents sur l'ensemble des machines du réseau local sur lequel se trouve le serveur.

# Partie 6 : Analyse de logs

## Q.2.6.1 Lister les 10 derniers échecs de connexion ayant eu lieu sur le serveur en indiquant pour chacun :

    La date et l'heure de la tentative
    L'adresse IP de la machine ayant fait la tentative
![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20122952.png?raw=true)












