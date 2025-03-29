### Explication
**EnvManager**, gère le fichier `.env` du CMS. Ces fichiers sont utilisés pour stocker des variables d'environnement, comme les paramètres de configuration, dans un format clé-valeur.

::: warning
Ces variables d'environnement sont définie par l'équipe de CraftMyWebsite, il est fortement déconseillé de les modifier
:::

### Importer le namespace
`use CMW\Manager\Env\EnvManager;`

### Utilisation
Vous pouvez récupérer une valeur comme ceci :
```php
EnvManager::getInstance()->getValue("key");
```
Il est souvent pratique d'utiliser les clés `PATH_SUBFOLDER`, `PATH_URL`, `DIR` :

Ceci permet d'obtenir le lien d'accès complet à une ressource, très pratique dans le cas ou l'utilisateur install son site dans un sous dossier.

**Exemple de cas concret :**

Récupérer une image dans un thème (Craftmywebsite dans ce cas)
```php
<?= EnvManager::getInstance()->getValue("PATH_SUBFOLDER") ?>Public/Themes/Craftmywebsite/Config/Default/whitedash.png
```
`PATH_SUBFOLDER`, `PATH_URL` ou `DIR` renvoie ce genre de valeur :
```php
//Dossier d'installation du site :
PATH_SUBFOLDER=/

//URL complet du site :
PATH_URL=https://dev.craftmywebsite.fr/

//Emplacement du site dans l'environnement de l'utilisateur
DIR=/var/www/main/
```

### Choses à ne pas faire !
::: danger
Ne vous amusez pas à afficher ces variables d'environnement publiquement !
- SALT
- SALT_PASS
- SALT_IV
- CMW_KEY
- DB_HOST
- DB_NAME
- DB_USERNAME
- DB_PASSWORD
- DB_PORT
- SMTP_PASSWORD
- RECAPTCHA_V2_SITE_KEY
- RECAPTCHA_V2_SECRET_KEY
:::