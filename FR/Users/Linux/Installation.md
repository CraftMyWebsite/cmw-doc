## Apache2, PHP et MariaDB

Ce tutoriel vous guidera à travers l'installation de CraftMyWebsite sur un serveur Linux (Ubuntu) avec Apache2, PHP et MariaDB, ainsi que les extensions PHP nécessaires.

### Étape 1 : Mettre à jour le système
Avant de commencer, assurez-vous que votre système est à jour.
```bash
sudo apt update
sudo apt upgrade -y
```

### Étape 2 : Installer Apache2
Installez le serveur web Apache2.
```bash
sudo apt install apache2 -y
```

### Étape 3 : Installer MariaDB
Installez le serveur de base de données MariaDB.
```bash
sudo apt install mariadb-server -y
```
Exécutez des commandes dans le serveur MariaDB
```bash
sudo mariadb
```
Remplacer newuser par l’utilisateur de votre choix, pour le password n’enlever pas les ‘ ’
- Création d'un utilisateur
    ```sql
    CREATE USER newuser@localhost IDENTIFIED BY 'password';
    ```
- Attribution des permissions
    ```sql
    GRANT ALL PRIVILEGES ON * . * TO newuser@localhost WITH GRANT OPTION;
    ```
- Création d'une base de données
    ```sql
    CREATE DATABASE 'cmw';
    ```
- Vous pouvez maintenant quitter
    ```bash
    quit
    ```
  
### Étape 4 : Installer PHP et les extensions requises
Installez PHP et les extensions nécessaires.
```bash
sudo apt install php php-mysql php-gd php-curl php-pdo php-json php-mbstring php-zip -y
```

### Étape 5 : Configurer Apache2 pour PHP
Assurez-vous que le module mod_rewrite et mod_headers sont activé.
```bash
sudo a2enmod rewrite
sudo a2enmod headers
```

Modifier la configuration Apache
```bash
nano /etc/apache2/apache2.conf
```

Modifier la ligne `AllowOverride None` dans la section « <Directory /var/www/> » par `AllowOverride All`

Redémarrez Apache2 pour appliquer les modifications.
```bash
sudo systemctl restart apache2
```

### Étape 7 : Télécharger et installer CraftMyWebsite
Téléchargez CraftMyWebsite depuis le site officiel ou le dépôt GitHub.
```bash
cd /var/www
rm -r html
sudo git clone https://github.com/votre-depot/craftmywebsite.git
sudo mv cmw-core html
```

Définissez les permissions appropriées pour les fichiers et répertoires.
```bash
sudo chown -R www-data:www-data /var/www/html
sudo find /var/www/html -type d -exec chmod 755 {} \;
sudo find /var/www/html -type f -exec chmod 644 {} \;
```

### Étape 8 : Terminer l'installation via le navigateur
Ouvrez votre navigateur et accédez à http://votre_ip_ou_nom_de_domaine. Suivez les instructions de l'assistant d'installation de CraftMyWebsite pour terminer la configuration.