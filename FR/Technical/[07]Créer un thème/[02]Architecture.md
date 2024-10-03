Dans cette section, nous allons définir l'architecture à respecter pour la création d'un thème dans le système. Chaque dossier et fichier doit suivre une nomenclature précise pour garantir une bonne organisation et une intégration correcte avec le système.

[Télécharger l'archive de l'exemple de structure de thème](Assets/Zip/Example-Theme.zip)

> L'archive téléchargeable contient tous les fichiers et dossiers de base nécessaires pour débuter la création de votre thème. Elle inclut les codes essentiels pour vous faire gagner du temps et éviter de repartir de zéro. En utilisant cette structure préconfigurée, vous pourrez rapidement configurer les éléments clés de votre thème et vous concentrer sur l'ajout de contenu et de fonctionnalités spécifiques.
Nous l'utiliserons dans les prochaines étapes de cette documentation !
> Si vous tester directement cet exemple celui-ci fonctionne directement

### Règles de nommage
- **Nom des dossiers** : Le premier caractère doit être une majuscule, tous les autres en minuscules.
- **Nom des fichiers** : Tout en minuscules. (Sauf `Theme.php`)

### Structure de base du thème
Les thèmes sont toujours situés dans le répertoire suivant :

`/Public/Themes/X`, où X représente le nom du thème. Dans notre cas, nous allons créer un thème nommé **Example**.
Mais nous n'allons pas créer de CSS pour celui-ci à vous de le créer vous même ou d'utilisez des Framework comme Bootstrap, TailwindCSS ...
### Détail de la structure
Voici la structure complète que votre thème doit respecter :

```scss
/Public/Themes/Example
│
├── /Theme.php                      (Contient les informations du thème - important)
├── /router.php                     (Voir section router.php)
│
├── /Assets
│   ├── /Css
│   ├── /Js
│   └── /Webfonts
│
├── /Config
│   ├── /Default
│   ├── /config.php
│   └── /config.settings.php
│
├── /Views
│   ├── /template.php               (Le gestionnaire du thème - important)
│   ├── /Alerts                     (Natif)
│   ├── /Contact                    (Package)
│   ├── /Core                       (Natif)
│   ├── /Errors                     (Natif)
│   ├── /Includes                   (Important)
│   ├── /Pages                      (Natif)
│   └── /Users                      (Natif)
```

### Détails des dossiers et fichiers
**1. /Theme.php** : Ce fichier est crucial, car il définit les informations du thème telles que le nom, la description et d'autres métadonnées. Il doit être présent pour que le thème soit reconnu par le système.

**2. /Assets** : Ce dossier contient tous les fichiers statiques comme les feuilles de style CSS, les scripts JavaScript et les polices web. Vous devez structurer ces fichiers sous les dossiers correspondants :
- **/Css** : Contient les fichiers CSS.
- **/Js** : Contient les fichiers JavaScript.
- **/Webfonts** : Contient les polices utilisées par le thème.

**3. /Config** : Ce dossier contient les fichiers de configuration du thème.
- **/Default** : Peut contenir des configurations par défaut comme des images ...
- **config.php** : Contient la configuration principale du thème affiché dans la partie administrateur.
- **config.settings.php** : Gère les paramètres du thème, que les utilisateurs peuvent personnaliser.

**4. /Views** : Ce dossier contient les fichiers de vue du thème, incluant la gestion du rendu des différentes parties de l'interface.
- **/template.php** : Ce fichier est essentiel, car il gère la mise en page globale du thème.
- **/Alerts**, **/Core**, **/Errors**, **/Pages**, **/Users** : Ce sont les dossiers natifs correspondant aux packages CORE.
- **/Contact** : Ce dossier correspond au package Contact, non natif au CORE, mais intégré pour cet exemple.
- **/Includes** : Contient des fichiers d'inclusion utilisés dans diverses vues (comme les en-têtes, les pieds de page, etc.).
  
::: warning
**Nom des fichiers dans les views**

Tout les fichiers PHP se trouvant dans l'architecture des Views doivent s'appeler filename.**view.php** et doivent avoir leur nom en corréspondance avec la déclaration faite dans le controller du package !

Pour ce qui est des includes, merci de respecter ces noms `footer.inc.php`, `head.inc.php` et `header.inc.php`
:::

---
::: info
**Vérification des noms des dossiers de packages**

Lorsque vous intégrez un package supplémentaire (par exemple Shop), il est crucial de vérifier le nom exact du dossier utilisé par le package dans son répertoire Views. Certains packages peuvent définir un nom spécifique pour leur dossier de vues, comme Shop dans ce cas, au lieu d’un nom générique.
:::

---
Cette architecture doit être respectée pour garantir la bonne intégration de votre thème dans le système.