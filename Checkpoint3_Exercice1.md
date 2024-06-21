# Partie 1 : Gestion des utilisateurs

Q.1.1.1 Créer l'utilisateur Lionel Lemarchand avec les même attribut de société que Kelly Rhameur.

Depuis le serveur manager aller dans ad ds et ouvrir la console de gestion des users and computers.

Chercher Kelly Rhameur dans OU=DirectionDesRessourcesHumaines, OU=LabUsers ( que j'ai trouvé en fesaant un clic droit sur LabUsers et Find )

Faire un clic droit sur l'ojet utilisateur Kelly.Rhameur et cliquer sur Copy

Sur la première fenêtre entrer les donnée comme dans l'image ci-dessous

![]()

Sur la deuxième fenêtre j'entre Azerty1* deux fois pour créé un mot de passe

![]()

Puis sur la troisième image on confirme la copie en cliquant sur Finish

![]()

Nous pouvons vérifier graphiquement si les infos ont été copier ou en tapant la commande suivant dans powershell:

`Get-ADUser -Identity "Lionel.Lemarchand" -Properties *`

![]()


Q.1.1.2 Créer une OU DeactivatedUsers et déplace le compte désactivé de Kelly Rhameur dedans.

Q.1.1.3 Modifier le groupe de l'OU dans laquelle était Kelly Rhameur en conséquence.

Q.1.1.4 Créer le dossier Individuel du nouvel utilisateur et archive celui de Kelly Rhameur en le suffixant par -ARCHIVE.
