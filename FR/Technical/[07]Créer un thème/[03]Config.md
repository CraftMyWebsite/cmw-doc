Dans cette section, nous allons voir comment permettre aux créateurs de thèmes d'ajouter des options de personnalisation que les utilisateurs pourront modifier directement depuis l'interface d'administration du CMS. Ces options permettent aux utilisateurs de rendre le thème plus personnel, notamment en changeant les images, les textes, les couleurs, etc.

### Les fichiers de configuration
Le thème utilise deux fichiers principaux pour gérer la configuration :
- **config.php** : Ce fichier gère l'interface utilisateur de la configuration au sein du système d'administration du CMS. C'est ici que les options sont présentées pour être modifiées.
- **config.settings.php** : Ce fichier contient les clés modifiables ainsi que les valeurs par défaut pour les éléments du thème. Les valeurs peuvent être nulles, et les types pris en charge incluent les images, les booléens, les chaînes de caractères (strings), et les longs textes au format HTML. Ces options sont auto-gérées par le CMS.

### Exemple config.settings.php
```php
<?php

return [
    /* - - - - - - - -
        - - HEADER & GLOBAL - -
     - - - - - - - - - */
    "body_color" => "#d8a629",
    "header_img_logo" => "Config/Default/Img/logo_dark.png",

    /* - - - - - - - -
       - - HOME - -
    - - - - - - - - - */
    /* TITLE DESC */
    'home_title' => 'Home',
    /* CONTACT SECTION */
    'contact_section_active' => '1',
    'contact_section_title' => 'Contact Us',
    /* CUSTOM SECTION #1 */
    'custom_section_active_1' => '0',
    'custom_section_title_1' => 'Custom Title 1',
    'custom_section_content_1' => '<h1>Custom me</h1> <br> <p>Like HTML !</p>',


    /* - - - - - - - -
       - - CONTACT PAGE - -
    - - - - - - - - - */
    'contact_title' => 'Contact',
    'contact_description' => 'Contact description',

    /* - - - - - - - -
       - - FOOTER - -
    - - - - - - - - - */
    'footer_text' => 'Zomb make greats tuto !',
];
```

### Exemple config.php
Voici un exemple de fichier config.php qui gère l'affichage de l'interface dans l'administration pour modifier les valeurs définies dans config.settings.php :
```html
<?php use CMW\Controller\Core\PackageController;
use CMW\Model\Core\ThemeModel;

?>
<!-------------->
<!--NAVIGATION-->
<!-------------->
<div class="tab-menu">
    <ul class="tab-horizontal" data-tabs-toggle="#tab-content-config">
        <li>
            <button type="button" data-tabs-target="#tab1" role="tab">Global</button>
        </li>
        <li>
            <button type="button" data-tabs-target="#tab2" role="tab">Accueil</button>
        </li>
        <?php if (PackageController::isInstalled('Contact')): ?>
            <li>
                <button type="button" data-tabs-target="#tab3" role="tab">Contact</button>
            </li>
        <?php endif; ?>
        <li>
            <button type="button" data-tabs-target="#tab4" role="tab">Footer</button>
        </li>
    </ul>
</div>
<!-------------->
<!--CONTENUE-->
<!-------------->
<div id="tab-content-config">
    <!-- Global -->
    <div class="tab-content" id="tab1">
        <h6>Image :</h6>
        <div class="grid-2">
            <div class="flex justify-center">
                <img class="w-25" src="<?= ThemeModel::getInstance()->fetchImageLink('header_img_logo') ?>"
                     alt="Image introuvable !">
            </div>
            <div class="drop-img-area mt-4" data-input-name="header_img_logo"></div>
        </div>
        <label for="bg">Background color :</label>
        <input id="bg" type="color" name="body_color"
               value="<?= ThemeModel::getInstance()->fetchConfigValue('body_color') ?>">
    </div>

    <!-- Accueil -->
    <div class="tab-content" id="tab2">
        <label for="home_title">Page Title:</label>
        <input type="text" id="home_title" name="home_title"
               value="<?= ThemeModel::getInstance()->fetchConfigValue('home_title') ?>" required class="input">
        <hr>
        <?php if (PackageController::isInstalled('Contact')): ?>
            <div>
                <label class="toggle">
                    <h5 class="toggle-label">Contact :</h5>
                    <input type="checkbox" class="toggle-input" id="contact_section_active"
                           name="contact_section_active" <?= ThemeModel::getInstance()->fetchConfigValue('contact_section_active') ? 'checked' : '' ?>>
                    <div class="toggle-slider"></div>
                </label>
            </div>
            <label for="contact_section_title">Section title :</label>
            <input type="text" class="input" id="contact_section_title" name="contact_section_title"
                   value="<?= ThemeModel::getInstance()->fetchConfigValue('contact_section_title') ?>" required>
        <?php endif; ?>
        <hr>
        <div>
            <label class="toggle">
                <h5 class="toggle-label">Customisable 1 :</h5>
                <input type="checkbox" class="toggle-input" id="custom_section_active_1"
                       name="custom_section_active_1" <?= ThemeModel::getInstance()->fetchConfigValue('custom_section_active_1') ? 'checked' : '' ?>>
                <div class="toggle-slider"></div>
            </label>
        </div>
        <label for="custom_section_title_1">Section title :</label>
        <input type="text" class="input" id="custom_section_title_1" name="custom_section_title_1"
               value="<?= ThemeModel::getInstance()->fetchConfigValue('custom_section_title_1') ?>" required>
        <label for="custom_section_content_1">Content :</label>
        <textarea id="custom_section_content_1" name="custom_section_content_1"
                  class="tinymce"><?= ThemeModel::getInstance()->fetchConfigValue('custom_section_content_1') ?></textarea>
    </div>

    <!-- Footer -->
    <div class="tab-content" id="tab4">
        <label for="footer_text">Footer text:</label>
        <input type="text" class="input" id="footer_text" name="footer_text"
               value="<?= ThemeModel::getInstance()->fetchConfigValue('footer_text') ?>" required>
    </div>
</div>
```
### Créer des configurations
**Créer des configurations** : Pour ajouter de nouvelles options de personnalisation, il suffit d'ajouter des entrées dans le fichier `config.settings.php`. Chaque clé représente un paramètre, et sa valeur initiale peut être une chaîne de caractères, un booléen, ou un texte au format HTML.

### Enregistrer des configurations
**Enregistrer des configurations** : Lorsque les utilisateurs modifient ces options depuis l'interface d'administration, les nouvelles valeurs sont automatiquement enregistrées par le CMS dans la base de données.

Dans le fichier `config.php`, il est important de garder cette trame de base, car c'est le style du panel d'administration.
```html
<?php use CMW\Controller\Core\PackageController;
use CMW\Model\Core\ThemeModel;

?>
<!-------------->
<!--NAVIGATION-->
<!-------------->
<div class="tab-menu">
    <ul class="tab-horizontal" data-tabs-toggle="#tab-content-config">
        <li>
            <button type="button" data-tabs-target="#tab1" role="tab">Footer</button>
        </li>
    </ul>
</div>
<!-------------->
<!--CONTENUE-->
<!-------------->
<div id="tab-content-config">
    <div class="tab-content" id="tab1">
        <label for="footer_text">Footer text:</label>
        <input type="text" class="input" id="footer_text" name="footer_text"
               value="<?= ThemeModel::getInstance()->fetchConfigValue('footer_text') ?>" required>
    </div>
</div>
```
Pour ajouter de nouvel "Tab"
Créer un nouveau bouton dans la liste et remplacer `tab1` par `tab2`: 
```html
<li>
    <button type="button" data-tabs-target="#tab2" role="tab">Titre</button>
</li>
```
Puis ajouter la nouvelle section correspondante et remplacer `tab1` par `tab2` :
```html
<div class="tab-content" id="tab2">
    <p>Contenue</p>
</div>
```

Dans vos inputs il est important que le `name=""` sois égale à la clé que vous souhaitez éditer par exemple si on édite la clé `test` alors l'input ressemblera à ceci :
```html
<input type="text" class="input" name="test">
```
Ajouter la valeur de votre clé à l'input donnera finalement :
```html
<input type="text" class="input" name="test" value="<?= ThemeModel::getInstance()->fetchConfigValue('test') ?>">
```

### Afficher des configurations

::: warning
N'oubliez pas d'importer le Namespace dans vos Views

`use CMW\Model\Core\ThemeModel;`
:::

**Afficher les configurations** : Dans les vues, vous pouvez récupérer et afficher les valeurs configurées en utilisant les méthodes du modèle du thème. Par exemple :

**Récupérer une image** : 
```php
<?= ThemeModel::getInstance()->fetchImageLink('KEY') ?>
```

**Récupérer un texte / booléen** :
```php
<?= ThemeModel::getInstance()->fetchConfigValue('KEY') ?>
```

---
Cette approche permet aux créateurs de thèmes d'offrir une flexibilité maximale aux utilisateurs, tout en conservant une interface simple et intuitive pour la personnalisation dans le CMS.