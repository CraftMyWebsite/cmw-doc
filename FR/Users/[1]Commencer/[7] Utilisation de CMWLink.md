## Configuration et utilisation du plugin CraftMyWebsiteLink
# Fonctionnel sur Spigot, Bungeecord et Velocity

Tout d’abord ce plugin fonctionne actuellement avec le package Minecraft à installer sur votre site en premier lieu ! 


### Etape 1 : Prérequis

Pour le fonctionnement du plugin le package de votre jeu ce doit d'être installé en premier lieu ! 
J'ai donc au préalable installé le __package Minecraft__ sur mon site.

### Etape 2 : Téléchargement de CraftMyWebsiteLink et de ses dépendances

[INSERER IMAGE MARKET]

Téléchargez le plugin, 

Ensuite prenez les dépendances dont vous avez besoin moi ici je vais prendre votes (pour le package votes sur mon site, il en sera de même à l’avenir pour le package shop).

### Etape 3 : Installation sur votre serveur

Glissez le plugin CraftMyWebsiteLink dans le dossier plugins de votre serveur minecraft

![Image plugin install](Assets/Img/CMWLink/Link1.png "FTP install plugin")

Redémarrer votre serveur, puis ouvrez le dossier du plugin

![Image plugin install](Assets/Img/CMWLink/Link2.png "FTP install plugin")

Puis allez dans "Packages" et insérer la dépendance "Votes" (pour moi ici)

![Image plugin install](Assets/Img/CMWLink/Link3.png "FTP install plugin")

Redémarrer votre serveur 

### Etape 4 : Configuration du plugin

Rendez – vous sur votre site dans le package Minecraft

![Image panel Minecraft](Assets/Img/CMWLink/Link4.png "Panel Admin")

Rentrer toutes les données et mettez le même port dans le plugin 

![Image panel Minecraft](Assets/Img/CMWLink/Link5.png "Panel ADD CMWLink")

Pour mettre le port ouvrez le fichier settings.json à la racine du plugin 

![Image FTP ](Assets/Img/CMWLink/Link6.png "Panel settings.json CMWLink")

**Nous conseillons d’utiliser un port ouvert fourni par votre hébergeur**

Sinon le plugin propose ceci : (à utiliser si vraiment vous n'avez pas le choix)

![Image Port default ](Assets/Img/CMWLink/Link7.png "Port default CMWLink")

Une fois le port bien rentré sur le plugin, **redémarrer à nouveau votre serveur**

Puis ajouter le serveur sur votre site 

Vous pouvez vérifier la liaison en cliquant sur 

![Image Port default ](Assets/Img/CMWLink/Link8.png "Port default CMWLink")

puis sur (une popup vous donnera le résultat)

![Image Port default ](Assets/Img/CMWLink/Link9.png "Port default CMWLink")

### Etape 5 : Utilisation sur Bungeecord/Velocity 

Veuillez à mettre dans le settings.json la ligne 8 "useProxy" sur "true"

![Image Port default ](Assets/Img/CMWLink/Link10.png "Port default CMWLink")