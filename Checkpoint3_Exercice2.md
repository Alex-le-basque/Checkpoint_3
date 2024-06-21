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

## Q.2.3.2 Quel type de système de stockage ils utilisent ?

## Q.2.3.3 Ajouter un nouveau disque de 8,00 Gio au serveur et réparer le volume RAID

## Q.2.3.4 Ajouter un nouveau volume logique LVM de 2 Gio qui servira à héberger des sauvegardes. Ce volume doit être monté automatiquement à chaque démarrage dans l'emplacement par défaut : /var/lib/bareos/storage.

## Q.2.3.5 Combien d'espace disponible reste-t-il dans le groupe de volume ?

# Partie 4 : Sauvegardes

## Q.2.4.1 Expliquer succinctement les rôles respectifs des 3 composants bareos installés sur la VM.

# Partie 5 : Filtrage et analyse réseau

## Q.2.5.1 Quelles sont actuellement les règles appliquées sur Netfilter ?

## Q.2.5.2 Quels types de communications sont autorisées ?

## Q.2.5.3 Quels types sont interdit ?

##Q.2.5.4 Sur nftables, ajouter les règles nécessaires pour autoriser bareos à communiquer avec les clients bareos potentiellement présents sur l'ensemble des machines du réseau local sur lequel se trouve le serveur.
