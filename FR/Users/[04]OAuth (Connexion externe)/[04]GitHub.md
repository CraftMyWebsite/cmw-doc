### Étape 1 : Créer une autorisation OAuth2

Rendez-vous sur la page [Developer settings](https://github.com/settings/developers)

- Une fois sur la page OAuth Apps (1)
- Cliquez sur New OAuth app (2)

![GitHub Developper Setting](Assets/Img/Users/OAuth/GitHub/1.png "GitHub Developper Setting")

Renseignez les informations (voir image): 
- **Application name** : Tapez ce que vous voulez
- **Homepage URL** : Tapez l'url de votre site
- **Authorization callback URL** : Doit refléter l'url de votre site suivi de `api/oauth/github/connect`

![GitHub Register OAuth](Assets/Img/Users/OAuth/GitHub/2.png "GitHub Register OAuth")

Une fois l'application ajoutée, Générer un client secret.

Vous pouvez ensuite les renseigner dans votre interface d'administration

![GitHub Panel](Assets/Img/Users/OAuth/GitHub/3.png "GitHub Panel")


::: info
Si votre thème supporte les connexions oAuth, Discord sera automatiquement affiché et disponible.
:::
