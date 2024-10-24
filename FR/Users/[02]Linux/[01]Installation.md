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
  
### Étape 4 : Installer PHP-8.3 et les extensions requises

#### Debian (10, 11, and 12) :
```bash
# Save existing php package list to packages.txt file
sudo dpkg -l | grep php | tee packages.txt

# Add Ondrej's repo source and signing key along with dependencies
sudo apt install apt-transport-https
sudo curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
sudo apt update
```

#### Ubuntu (20.04, 22.04, et 24.04) :
```bash
## Save existing php package list to packages.txt file
sudo dpkg -l | grep php | tee packages.txt

# Add Ondrej's PPA
sudo add-apt-repository ppa:ondrej/php # Press enter when prompted.
sudo apt update
```

Installez PHP et les extensions nécessaires.
```bash
sudo apt install php8.3 php8.3-mysql php8.3-gd php8.3-curl php8.3-pdo php8.3-mbstring php8.3-zip -y
```

Vérifier votre version php :
```bash
php -v
```
Devrais vous renvoyer :
```bash
PHP 8.3.12 (cli) (built: Sep 27 2024 03:53:05) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.3.12, Copyright (c) Zend Technologies
    with Zend OPcache v8.3.12, Copyright (c), by Zend Technologies
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
cd /var/www/html
sudo wget https://raw.githubusercontent.com/CraftMyWebsite/cmw-installer/main/install.php
```

Définissez les permissions appropriées pour les fichiers et répertoires.
```bash
sudo chown -R www-data:www-data /var/www/html
sudo find /var/www/html -type d -exec chmod 755 {} \;
sudo find /var/www/html -type f -exec chmod 644 {} \;
```

### Étape 8 : Terminer l'installation via le navigateur
Ouvrez votre navigateur et accédez à http://votre_ip_ou_nom_de_domaine/install.php. Suivez les instructions de l'assistant d'installation de CraftMyWebsite pour terminer la configuration.
