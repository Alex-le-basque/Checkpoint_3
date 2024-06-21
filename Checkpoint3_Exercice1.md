# Partie 1 : Gestion des utilisateurs

## Q.1.1.1 Créer l'utilisateur Lionel Lemarchand avec les même attribut de société que Kelly Rhameur.

Depuis le serveur manager aller dans ad ds et ouvrir la console de gestion des users and computers.

Chercher Kelly Rhameur dans OU=DirectionDesRessourcesHumaines, OU=LabUsers ( que j'ai trouvé en fesaant un clic droit sur LabUsers et Find )

Faire un clic droit sur l'ojet utilisateur Kelly.Rhameur et cliquer sur Copy

Sur la première fenêtre entrer les donnée comme dans l'image ci-dessous

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20094118.png?raw=true)

Sur la deuxième fenêtre j'entre Azerty1* deux fois pour créé un mot de passe

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20094311.png?raw=true)

Puis sur la troisième image on confirme la copie en cliquant sur Finish

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20094443.png?raw=true)

Nous pouvons vérifier graphiquement si les infos ont été copier ou en tapant la commande suivant dans powershell:

`Get-ADUser -Identity "Lionel.Lemarchand" -Properties *`

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20094807.png?raw=true)


## Q.1.1.2 Créer une OU DeactivatedUsers et déplace le compte désactivé de Kelly Rhameur dedans.

Taper la commande suivant dans powershell pour créer l'OU

`New-ADOrganizationalUnit -Name "DeactivatedUsers" -Path "OU=LabUsers,DC=TSSR,DC=LAN"`

Clic droit sur l'objet utilisateur Kelly.Rhameur et cliquer sur Move pour ensuite choisir l'OU DeactivatedUsers

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20100050.png?raw=true)

Aller dans l'OU DeactivatedUsers clic droit sur l'objet utilisateur Kelly.Rhameur et cliquer sur Disable Account

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20100159.png?raw=true)

## Q.1.1.3 Modifier le groupe de l'OU dans laquelle était Kelly Rhameur en conséquence.

Retourner dans l'OU DirectionDesRessourcesHumaines faire un clic droit sur le groupe GrpUsersDirectionDesRessourcesHumaines et choisir Properties puis Managed By cliquer sur Change et chercher Lionel Lemarchand et apply et ok

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20100616.png?raw=true)

## Q.1.1.4 Créer le dossier Individuel du nouvel utilisateur et archive celui de Kelly Rhameur en le suffixant par -ARCHIVE.

Ouvrir l'explorateur de fichier, aller dans le lecteur DossierIndividuels (F:)

Renommer le dossier kelly.rhameur en kelly.rhameur-ARCHIVE

Créer un dossier en le nommant lionel.lemarchand

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20101015.png?raw=true)

# Partie 2 : Restriction utilisateurs

## Q.1.2.1 Faire en sorte que l'utilisateur Gabriel Ghul ne puisse se connecter que du lundi au vendredi, de 7h à 17h.

Trouverl'utilsateur Gabriel Ghul avec la fonction Find comme auparavant, clic droit Properties puis Account puis cliquer sur Logon Hours pour choisr ses horaire de connection de 7h à 17h du lundi au vendredi

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20101642.png?raw=true)

## Q.1.2.2 De même, bloquer sa connexion au seul ordinateur CLIENT01.

Toujours dans Account cliquer sur Log On To et taper CLIENT01 puis Add et ensuite OK

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20101751.png?raw=true)

Ne pas oublier de faire Apply avant de fermer la fenêtre Properties pour éviter la non prise en compte des changements

## Q.1.2.3 Mettre en place une stratégie de mot de passe pour durcir les comptes des utilisateurs de l'OU LabUsers.

Depuis le serveur manager cliquer sur Tools puis Group Policy Management

Créer un GPO dans LabUsers, ici je vais l'appeller Password_Rules

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20102303.png?raw=true)

Edit cette GPO en allant dans Computer Configuration / Policies / Windows Settings / Security Settings / Account Policies / Password Policy

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20102618.png?raw=true)

Ici je vais modifier le Minimum password length en mettant 12 caractères et en cochant Define this policy settings et ensuite Apply

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20102855.png?raw=true)

Ainsi que le Password must meet complecity requirements en cochant Define this policy setting et Enable et ensuite Apply

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20103109.png?raw=true)

Pour vérifier on peut aller sur la GPO créé puis Settings cliquer sur Show all et on voit les regles mise en place

![](https://github.com/Alex-le-basque/Checkpoint_3/blob/main/Ressources/Capture%20d'%C3%A9cran%202024-06-21%20103233.png?raw=true)

# Partie 3 : Lecteurs réseaux

## Q.1.3.1 Créer une GPO Drive-Mount qui monte les lecteurs E: et F: sur les clients.
