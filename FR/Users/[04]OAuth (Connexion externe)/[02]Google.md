### Étape 1 : Créer un compte Google Cloud Console

- Pour commencer la configuration, vous devez vous rendre sur
  la [Console Google Cloud](https://console.cloud.google.com/).
  Une fois dessus, connectez-vous à votre compte Google.
- Sélectionnez un projet, sinon créez-en un.

![Google Cloud Console - Accueil](Assets/Img/Users/OAuth/Google/google_cloud_console_home.png "Google Cloud Console - Accueil")

### Étape 2 : Création identifiants

- Cliquez sur "API et services".
- Sur la barre latérale, rendez-vous dans la section "Identifiants".
- Cliquez sur "Créer des identifiants"
- Sélectionnez "ID client OAuth"

![Google Cloud Console - Identifiants](Assets/Img/Users/OAuth/Google/google_cloud_console_identifiants.png "Google Cloud Console - Identifiants")

- Si vous n'avez pas encore configuré l'écran d'autorisation, faites-le. De mon côté, il est déjà configuré.
- Sélectionnez en type d'application "Application Web"
- Le nom, mettez ce que vous voulez, l'utilisateur ne le verra pas.
- Dans la section "URI de redirection autorisés", cliquez sur "Ajouter un URI", et
  ajoutez : `https://monsite.com/api/oauth/google/connect` (remplacez monsite.com par votre domaine.)

![Google Cloud Console - Identifiants Création](Assets/Img/Users/OAuth/Google/google_cloud_console_identifiants_create.png "Google Cloud Console - Identifiants Création")

Cliquez ensuite sur Créer...

Gardez précieusement ouverte la popup "Client OAuth créé", dans l'étape suivante, on aura besoin du "ID client" et du "
Code secret du client".

### Étape 3 : Configuration de votre site

- Rendez-vous sur votre panel admin
- Allez dans la section Utilisateurs > oAuth

#### Configuration

- Activez l'ajout de Google
- Copiez votre "Client ID" et votre "Client secret" dans les champs.
- Cliquez sur sauvegarder

::: info
Si votre thème supporte les connexions OAuth, Google sera automatiquement affiché et disponible.
:::
