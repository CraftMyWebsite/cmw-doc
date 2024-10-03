Les **vues** (views) sont responsables de l'affichage des données et de l'interface utilisateur dans le CMS. Elles sont divisées en deux catégories :

- Vues **publiques** accessibles à tous les utilisateurs.
- Vues d'**administration** accessibles uniquement via le panneau d'administration, généralement pour les utilisateurs ayant des permissions spécifiques.

Dans cette page, nous allons expliquer comment créer des **vues publiques** et **vues d'administration** dans un package, et comment les utiliser dans les **controllers**.

### Les Vues Publiques
Les vues publiques sont affichées sur le frontend du site, accessibles à tous les utilisateurs, et sont souvent stylisées selon le thème en cours.

**Exemple de Vue Publique dans un Contrôleur**

Voici un exemple de contrôleur qui affiche une vue publique pour le package Example.

Code du Contrôleur Public :
```php
#[Link('/example', Link::GET)]
private function frontExamplePublic(): void
{
    $view = new View('Example', 'main');  // Utilisation du fichier "main.view.php" dans le package Example
    $view->view();
}
```

**Explication :**
- **View('Example', 'main')** : Cette ligne indique que la vue main.view.php doit être chargée depuis le dossier Views du package Example.
- **view()** : Cette méthode permet d'afficher la vue.

**Structure des Fichiers de Vue**
Les fichiers de vue publics se trouvent généralement dans le répertoire suivant :

`Public/Themes/{NomDuTheme}/Views/{NomDuPackage}/{NomDeLaVue}.view.php`

**Exemple de Fichier de Vue main.view.php :**

```php
<?php

use CMW\Utils\Website;

/* TITRE ET DESCRIPTION */
Website::setTitle('Example');
Website::setDescription('Des questions et réponses');

?>
<h1>FAQ Example</h1>
<p>Voici un exemple de FAQ pour le package Example.</p>
```

**Explication :**
- `Website::setTitle()` et `Website::setDescription()` : Ces fonctions permettent de définir le titre et la description de la page dans le contexte du site web.
- Le contenu de la FAQ ou de la page est ensuite structuré en HTML comme dans un fichier de vue standard.

### Les Vues d'Administration
Les vues d'administration sont utilisées pour l'affichage dans le panneau d'administration du CMS. Elles sont généralement protégées par des permissions et ne sont accessibles qu'à certains utilisateurs (administrateurs, modérateurs, etc.).

**Exemple de Vue d'Administration dans un Contrôleur**

Voici un exemple de contrôleur qui affiche une vue d'administration pour le package Example.

**Code du Contrôleur Admin :**
```php
#[Link('/manage', Link::GET, [], '/cmw-admin/example')]
private function exampleList(): void
{
    View::createAdminView('Example', 'manage')
        ->view();
}
```
**Explication :**
- **View::createAdminView('Example', 'manage')** : Cette méthode crée une vue d'administration, en chargeant le fichier manage.admin.view.php depuis le dossier Views du package Example.
- **view()** : Cette méthode affiche la vue d'administration dans le panneau admin.

**Structure des Fichiers de Vue d'Administration**

Les fichiers de vue admin sont stockés dans un répertoire différent des vues publiques :

`App/Package/{NomDuPackage}/Views/{NomDeLaVue}.admin.view.php`

**Exemple de Fichier de Vue d'Administration manage.admin.view.php :**
```php
<?php

use CMW\Utils\AdminPanel;

/* TITRE ET DESCRIPTION */
$title = "Gestion des FAQs";
$description = "Gérez les questions et réponses du package Example.";

?>
<h1>Gestion des FAQs</h1>
<p>Voici la liste des questions et réponses à gérer.</p>
```

**Explication :**
`$title` et `$description` : Ces fonctions permettent de définir le titre et la description de la page d'administration.

### Gestion des Variables et Inclusion des Scripts/Styles
Les vues peuvent accepter des variables passées par le contrôleur et inclure des fichiers de scripts ou styles supplémentaires.

**Ajout de Variables à une Vue**

Vous pouvez ajouter des variables à une vue en utilisant la méthode `addVariable()` ou `addVariableList()`.

```php
#[Link('/example', Link::GET)]
private function frontExamplePublic(): void
{
    $examples = ExampleModel::getInstance()->getAllExample();  // Récupération des exemples

    $view = new View('Example', 'main');
    $view->addVariableList(['examples' => $examples]);  // Ajout des variables à la vue
    $view->view();
}
```

**Utilisation des Variables dans la Vue :**
```php
<?php

/* @var \CMW\Entity\Example\ExampleEntity[] $examples */

?>
<h1>Liste des FAQs</h1>

<?php foreach ($examples as $example): ?>
    <h5><?= $example->getQuestion() ?></h5>
    <p><?= $example->getResponse() ?></p>
<?php endforeach; ?>
```

**Inclusion des Scripts et Styles**
```php
View::createAdminView('Example', 'manage')
    ->addStyle('Admin/Resources/Assets/Css/simple-datatables.css')  // Ajout de style
    ->addScriptAfter('Admin/Resources/Vendors/Simple-datatables/simple-datatables.js',
        'Admin/Resources/Vendors/Simple-datatables/config-datatables.js')  // Ajout de script
    ->view();
```


### Conclusion
Les **vues** jouent un rôle essentiel dans la présentation des données dans le CMS. Elles sont gérées par les controllers qui les appellent et leur passent des variables. Il existe deux types principaux de vues :

- Vues **publiques** pour les utilisateurs finaux, qui sont stylisées selon le thème actuel.
- Vues d'**administration** pour les utilisateurs du panneau admin, avec des contrôles de permission.

Dans cette documentation, nous avons couvert :

- La création de vues **publiques** et leur utilisation dans les contrôleurs.
- La création de vues d'**administration** et l'ajout de styles et de scripts personnalisés.
- Comment passer des variables à une vue depuis un contrôleur et les utiliser dans la vue.

Les vues permettent de créer une interface utilisateur riche et dynamique dans vos packages.