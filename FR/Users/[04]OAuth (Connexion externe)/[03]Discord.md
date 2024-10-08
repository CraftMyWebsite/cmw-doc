### Étape 1 : Créer une application OAuth2 

- Pour commencer la configuration, vous devez vous rendre sur
  la [Discord Developer Portal](https://discord.com/developers/applications).
  Une fois dessus, connectez-vous.
- Sélectionnez en haut à droite **New Application** :

![Discord Developer Portal - home page](Assets/Img/Users/OAuth/Discord/1.png "Discord Developer Portal - home page")

- Renseignez un nom d'application par exemple "OAuth - monsite.fr"
- Rendez-vous dans OAuth2 (section à gauche) - **1.
- Renseignez l'URL de redirection - **2 :
  - comme ceci : `https://monsite.com/api/oauth/discord/connect` (remplacez monsite.com par votre domaine.)
- Sauvegarder les changements

![Discord Developer Portal - application page](Assets/Img/Users/OAuth/Discord/2.png "Discord Developer Portal - application page")

### Étape 2 : Activer Discord sur votre panel

- Rendez-vous sur votre panel admin
- Allez dans la section Utilisateurs > oAuth
- Activer Discord
- Récupérer sur le Panel de Discord `Client ID` et `Client Secret`
- Renseignez les informations sur voter panel
- Sauvegarder
- Tester

::: info
Si votre thème supporte les connexions oAuth, Discord sera automatiquement affiché et disponible.
:::
