Dans cette section, nous allons voir comment configurer votre environnement de travail pour le développement sur **CraftMyWebsite**, en utilisant **PhpStorm**. Nous expliquerons également comment ajouter des thèmes et des packages existants.

## Avant de commencer
Nous partons du principe que :
- Vous avez déjà un IDE installé (**PhpStorm**, dans ce cas).
- Votre IDE est connecté à GitHub.

### Pourquoi travailler avec le Core ?
Le **Core** n'a pas forcément besoin d'être modifié par les développeurs. Cependant, il est **indispensable** pour le développement de packages et de thèmes.  
Le Core gère des éléments fondamentaux comme :
- L'autoloading des classes.
- Les routes.
- Les fonctions de base nécessaires au fonctionnement du CMS.

Pour cette raison, vous devez impérativement disposer du Core pour travailler correctement.

---

## Étape 1 : Forker le repository Core

1. Rendez-vous sur le repository Core officiel :  
   [https://github.com/CraftMyWebsite/cmw-core](https://github.com/CraftMyWebsite/cmw-core)
2. Cliquez sur **Fork** pour créer une copie dans votre compte GitHub.
3. **Décochez l'option "Copy the main branch only"** car nous travaillons sur la branche `dev`.

---

## Étape 2 : Ajouter des thèmes et packages existants (optionnel)

Si vous souhaitez travailler sur des thèmes ou des packages existants :
1. Forkez également leurs repositories respectifs sur GitHub.
2. Vous pourrez ensuite les ajouter à votre environnement de travail.

---

## Étape 3 : Ajouter le projet forké à PhpStorm

1. Dans PhpStorm, cliquez sur **File > Project from Version Control**.
2. Collez l'URL de votre repository forké et clonez-le.  
   *(Voir image 1)*

### ⚠️ Emplacement du projet
- **Travail en local** : Placez votre projet dans le répertoire où tourne votre serveur web local. Consultez la documentation sur l'installation locale de CraftMyWebsite pour plus de détails.
- **Travail distant** : Placez le projet où vous voulez sur votre PC.

**Image 1 :**
![Cloner le repo](Assets/Img/Technical/Work/clone.png "Cloner le repo")

---

## Étape 4 : Configurer les branches Git

1. Une fois le repository cloné, passez sur la branche `dev`, qui est **la dernière version à jour**. *(Voir image 2)*
2. Pour vos modifications futures sur le Core, créez une **nouvelle branche** à partir de `dev`.  
   Cela vous permet de travailler proprement sans impacter la branche principale.

**Image 2 :**
![Branche dev](Assets/Img/Technical/Work/branche.png "Branche dev")

---

## Étape 5 : Configuration pour les serveurs web distants

Si vous travaillez sur un serveur web distant :
1. Configurez un système d'auto-déploiement pour synchroniser vos modifications locales avec le serveur. (Voir image 3)*
2. N'oubliez pas de mapper le bon emplacement de déploiement sur votre serveur distant *(Voir image 3)*
3. Dans PhpStorm :
    - Configurez l'accès FTP/SFTP pour votre serveur distant (non détaillé ici, à configurer selon vos besoins).
    - **Activez le transfert automatique** :
        - Allez dans **Tools > Deployment > Options**.
        - Activez l'option **Upload changed files automatically to the default server** :
            - Sélectionnez **On explicit save action (CTRL+S)** pour un déploiement manuel et contrôlé.

**Image 3 :**
![sftp](Assets/Img/Technical/Work/sftp.png "sftp")

---

## Étape 6 : Push régulier des modifications

Enfin, il est fortement recommandé de **push régulièrement vos modifications** sur votre repository GitHub pour :
- Sauvegarder votre travail.
- Collaborer efficacement avec d'autres développeurs.

---

En suivant ces étapes, votre environnement de travail sera prêt pour développer des packages et thèmes avec **CraftMyWebsite**. Bonne configuration et bon développement !
