# Travailler en local avec CraftMyWebsite

::: warning

Avertissements importants
Avant de commencer, assurez-vous d'avoir :
1. **Lu les [prérequis](https://craftmywebsite.fr/docs/fr/technical/commencer/prerequis)** pour le développement avec CraftMyWebsite.
2. **Configuré votre environnement de travail**, comme expliqué dans la [documentation précédente](https://craftmywebsite.fr/docs/fr/technical/commencer/environement-de-travail).

:::

Cette page détaille la configuration locale sur **Windows 11**, en utilisant **WampServer**.

---

## Étape 1 : Télécharger et installer WampServer

1. Rendez-vous sur le site officiel de WampServer :  
   [https://www.wampserver.com/en/download-wampserver-64bits/](https://www.wampserver.com/en/download-wampserver-64bits/)
2. Téléchargez la version 64 bits et installez-la sur votre machine.
3. Une fois installé, lancez **WampServer**.

---

## Étape 2 : Configurer WampServer pour CraftMyWebsite

### 2.1 Sélectionner PHP 8.3
1. Cliquez gauche sur l'icône Wamp dans votre barre des tâches.
2. Allez dans **PHP > Version > 8.3.0**. *(Voir image 1)*  
   Si PHP 8.3 n'est pas disponible, installez-le via le gestionnaire de versions Wamp.

**Image 1 :**
![php8.3](Assets/Img/Technical/Local/php83.png "php8.3")

### 2.2 Vérifier les extensions PHP nécessaires
Assurez-vous que les extensions suivantes sont activées :
- `mysqli`
- `gd`
- `curl`
- `pdo`
- `mbstring`
- `zip`  
  *(Voir image 2)*

**Image 2 :**
![extension php](Assets/Img/Technical/Local/extensionphp.png "extension php")

### 2.3 Désactiver le `display_errors`
1. Cliquez gauche sur l'icône Wamp.
2. Allez dans **PHP > php.ini [apache module]**.
3. Recherchez la ligne `display_errors = On` et modifiez-la en `display_errors = Off`.
4. Redémarrez les services Wamp pour appliquer les modifications.

### 2.4 Activer les modules Apache nécessaires
Vérifiez que les modules suivants sont actifs :
- `headers_module`
  *(Voir image 3)*

**Image 3 :**
![module apache](Assets/Img/Technical/Local/moduleapache.png "module apache")

---

## Étape 3 : Configurer phpMyAdmin

1. Rendez-vous sur [http://localhost/phpmyadmin](http://localhost/phpmyadmin).
2. Connectez-vous avec l'identifiant `root` et sans mot de passe par défaut.  
   (Si vous souhaitez sécuriser cet accès, configurez un mot de passe root ou créez un nouvel utilisateur.)

### 3.1 Créer un nouvel utilisateur pour la base de données
1. Dans phpMyAdmin, allez dans l'onglet **Compte utilisateur**.
2. Cliquez sur **Ajouter un compte d'utilisateur**.
3. Renseignez les informations suivantes :
    - **Nom** : `local_cmw`
    - **Hôte** : `%`
    - **Mot de passe** : `db_cmw_local`
4. Cochez **Créer une base portant son nom et donner à cet utilisateur tous les privilèges sur cette base.**
5. Cliquez sur **Ajouter un utilisateur**.  
   Cet utilisateur sera utilisé pour configurer votre site.

---

## Étape 4 : Cloner le repository Core

1. Clonez le repository Core forké (voir documentation sur l'environnement de travail).
2. Placez-le dans le répertoire de votre serveur web local, par exemple :  
   `C:\wamp64\www\` *(Voir image 4)*.
3. Une fois cloné, passez sur la branche `dev`.

**Image 4 :**
![clone local](Assets/Img/Technical/Local/clonelocal.png "clone local")

---

## Étape 5 : Installation de base du site

1. Rendez-vous sur [http://localhost](http://localhost) dans votre navigateur.
2. Suivez les étapes de configuration :
    - Lors de la configuration de la base de données, utilisez :
        - **Utilisateur** : `local_cmw`
        - **Mot de passe** : `db_cmw_local`
    - Testez la connexion : une popup "Configuration fonctionnelle" devrait s'afficher. *(Voir image 5)*
3. Continuez les étapes jusqu'à l'étape 7. **Ne jamais installer de thèmes, packages ou bundles** à ce stade.
4. Créez un compte administrateur lorsque demandé.

**Image 5 :**
![setp2](Assets/Img/Technical/Local/setp2.png "setp2")

---

## Votre environnement local est prêt !

Vous pouvez désormais commencer à développer vos thèmes et packages pour CraftMyWebsite. 🚀
