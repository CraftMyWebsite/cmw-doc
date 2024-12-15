# Construction de l'image Docker avec docker-compose

### Étape 1 : Cloner le répertoire

```bash
git clone https://github.com/CraftMyWebsite/cmw-core.git craftmywebsite
cd craftmywebsite
```

### Étape 2 : Construction du conteneur

```bash
docker-compose up --build
```

### Étape 3 : Accéder à votre site CraftMyWebsite
- Votre application est maintenant accessible à l'adresse [http://localhost:80](http://localhost:80)
- Acceptez le contrat de licence

### Étape 4 : Configuration de CraftMyWebsite
- **Informations de connexion à la base de données**
    - Hôte de la base de données : `db`
    - Port de la base de données : `3306`
    - Nom de la base de données : `cmw`
    - Utilisateur de la base de données : `user`
    - Mot de passe de la base de données : `cmw_user_password`


### Accès à phpMyAdmin
Allez sur [http://localhost:8090](http://localhost:8090) et connectez-vous avec les identifiants suivants :
- Utilisateur : `root`
- Mot de passe : `cmw_root_password`

### Liens utiles
- [Dockerfile](https://github.com/CraftMyWebsite/cmw-core/blob/main/Dockerfile)
- [Docker compose](https://github.com/CraftMyWebsite/cmw-core/blob/main/compose.yaml)
