CMWLink est le plugin officiel de CraftMyWebsite fournis pour faire fonctionner votre site avec vos serveurs minecraft

***Fonctionnel sur Spigot, Bungeecord et Velocity***

Ce plugin peut fonctionner avec 3 packages :
- Minecraft
- Shop
- Votes

---

### Etape 1 : Prérequis

Pour le fonctionnement du plugin le package de votre jeu ce doit d'être installé en premier lieu !

Vous devez donc au préalable installé le __package Minecraft__ sur votre site.

### Etape 2 : Téléchargement de CraftMyWebsiteLink et de ses dépendances

Téléchargez le plugin sur le [market de CraftMyWebsite](https://craftmywebsite.fr/market/details/cmw-link)

Installez les dépendances dont vous avez besoin.

### Etape 3 : Installation sur votre serveur

Glissez le plugin CraftMyWebsiteLink dans le dossier plugins de votre serveur minecraft

![Image plugin install](Assets/Img/CMWLink/Link1.png "FTP install plugin")

Redémarrer votre serveur, puis ouvrez le dossier du plugin

![Image plugin install](Assets/Img/CMWLink/Link2.png "FTP install plugin")

Rendez-vous dans "Packages" et insérer la dépendance "Votes" (dans cet documentation)

![Image plugin install](Assets/Img/CMWLink/Link3.png "FTP install plugin")

Redémarrer votre serveur 

### Etape 4 : Configuration du plugin

Rendez–vous sur votre site dans le package Minecraft

![Image panel Minecraft](Assets/Img/CMWLink/Link4.png "Panel Admin")

Renseignez les informations nécessaires

![Image panel Minecraft](Assets/Img/CMWLink/Link5.png "Panel ADD CMWLink")

Pour changer le port ouvrez le fichier settings.json à la racine du plugin 

![Image FTP ](Assets/Img/CMWLink/Link6.png "Panel settings.json CMWLink")

Le plugin propose ceci : (à utiliser si vous n'avez pas le choix)

![Image Port default ](Assets/Img/CMWLink/Link7.png "Port default CMWLink")

Une fois le port renseigné **redémarré à nouveau votre serveur**

Puis ajouter le serveur sur votre site 

Vous pouvez vérifier la liaison en cliquant sur :


![Image Port default ](Assets/Img/CMWLink/Link8.png "Port default CMWLink")

une popup vous donnera le résultat de connexion avec votre serveur Minecraft ainsi que d'un check 

![Image Port default ](Assets/Img/CMWLink/Link9.jpg "Port default CMWLink")

### Etape 5 : Utilisation sur Bungeecord/Velocity 

Veillez à mettre dans le settings.json la ligne 8 "useProxy" sur "true" **uniquement pour une utilisation sur Bungeecord ou Velocity**

![Image Port default ](Assets/Img/CMWLink/Link10.png "Port default CMWLink")
