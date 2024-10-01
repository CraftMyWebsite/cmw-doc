Dans cette section, nous allons créer deux contrôleurs pour notre package Example :

- Un controller **public** pour la gestion des vues accessibles aux utilisateurs.
- Un controller **admin** pour la gestion des vues réservées à l'administrateur.

### Le Controller Public
Le fichier **ExamplePublicController.php** est utilisé pour gérer les actions publiques, accessibles à tous les utilisateurs. Ce contrôleur définit des routes qui seront utilisées pour afficher des pages publiques, comme un exemple de FAQ.

**Code du Controller Public**

```php
<?php

namespace CMW\Controller\Example\Public;

use CMW\Manager\Package\AbstractController;
use CMW\Manager\Router\Link;
use CMW\Manager\Views\View;

/**
 * Class: @ExamplePublicController
 * @package Example
 * @author Zomb
 * @version 0.0.1
 */
class ExamplePublicController extends AbstractController
{
    #[Link('/example', Link::GET)]
    private function frontExamplePublic(): void
    {
        $view = new View('Example', 'main');
        $view->view();
    }
}
```

**Explication du Code :**
- **Namespace** : Le namespace reflète l'arborescence des dossiers du contrôleur. Ici, il est situé dans /App/Package/Example/Controllers/Public.
- **Héritage** : Le contrôleur hérite de la classe AbstractController, qui permet de centraliser la logique des contrôleurs dans le CMS.
- **Route** : La route définie avec l'attribut #[Link] associe l'URL /example à la méthode frontExamplePublic. Cette route est accessible en utilisant la méthode HTTP GET.
- **View** : La méthode frontExamplePublic instancie une vue avec new View('Example', 'main') et l'affiche en appelant la méthode view().

Pour afficher la page sur https://votresite.fr/example votre thème doit dans notre cas avoir un dossier **Example** dans le dossier **Views** du thème et appel le fichier `main.view.php`

**Remarque :**
Dans ce contrôleur, nous avons simplement défini un lien vers une vue publique. Nous verrons plus tard comment récupérer et afficher des variables dans cette vue.

### Le Controller Admin
Le fichier **ExampleAdminController.php** est utilisé pour gérer les actions côté administrateur, comme l'affichage, la modification et la suppression des questions de la FAQ. Il contient des vérifications de permissions pour restreindre l'accès aux fonctionnalités administratives.
```php
<?php

namespace CMW\Controller\Example\Admin;

use CMW\Controller\Users\UsersController;
use CMW\Manager\Package\AbstractController;
use CMW\Manager\Router\Link;
use CMW\Manager\Views\View;
use CMW\Utils\Redirect;
use JetBrains\PhpStorm\NoReturn;

/**
 * Class: @ExampleAdminController
 * @package Example
 * @author Zomb
 * @version 0.0.1
 */
class ExampleAdminController extends AbstractController
{
    #[Link('/manage', Link::GET, [], '/cmw-admin/example')]
    private function exampleList(): void
    {
        UsersController::redirectIfNotHavePermissions('core.dashboard', 'example.show');

        View::createAdminView('Example', 'manage')
            ->view();
    }

    #[Link('/edit/:id', Link::GET, ['id' => '[0-9]+'], '/cmw-admin/example')]
    private function exampleEdit(int $id): void
    {
        UsersController::redirectIfNotHavePermissions('core.dashboard', 'example.edit');

        View::createAdminView('Example', 'edit')
            ->view();
    }

    #[Link('/edit/:id', Link::POST, ['id' => '[0-9]+'], '/cmw-admin/example')]
    #[NoReturn]
    private function exampleEditPost(int $id): void
    {
        UsersController::redirectIfNotHavePermissions('core.dashboard', 'example.edit');

        Redirect::redirectToAdmin('example/manage');
    }

    #[Link('/manage/add', Link::GET, [], '/cmw-admin/example')]
    private function exampleAdd(): void
    {
        UsersController::redirectIfNotHavePermissions('core.dashboard', 'example.create');

        View::createAdminView('Example', 'add')
            ->view();
    }

    #[NoReturn] #[Link('/manage/add', Link::POST, [], '/cmw-admin/example')]
    private function exampleAddPost(): void
    {
        UsersController::redirectIfNotHavePermissions('core.dashboard', 'example.create');

        Redirect::redirectToAdmin('example/manage');
    }

    #[NoReturn] #[Link('/delete/:id', Link::GET, ['id' => '[0-9]+'], '/cmw-admin/example')]
    private function exampleDelete(int $id): void
    {
        UsersController::redirectIfNotHavePermissions('core.dashboard', 'example.delete');

        Redirect::redirectToAdmin('example/manage');
    }
}
```

**Explication du Code :**
- **Namespace** : Le namespace du contrôleur admin est situé dans /App/Package/Example/Controllers/Admin.

- **Héritage** : Ce contrôleur hérite également de AbstractController.

- **Vérifications de Permissions** : Chaque action admin est protégée par des vérifications de permissions avec la méthode UsersController::redirectIfNotHavePermissions(). Ces permissions sont définies dans le fichier Permissions.php et doivent être respectées pour accéder aux différentes routes.

- **Gestion des Vues Admin** : Les vues pour l'administrateur sont générées avec la méthode View::createAdminView(). Elles sont spécifiques à l'administration et permettent de gérer les questions de la FAQ via une interface utilisateur dédiée.

- **Redirections** : Les redirections sont gérées par la classe Redirect. Par exemple, après avoir ajouté ou modifié une question, l'utilisateur est redirigé vers la page de gestion.

- **Méthodes associées aux routes** :
  - **exampleList()** : Affiche la liste des éléments à gérer.
  - **exampleEdit()** : Affiche le formulaire de modification.
  - **exampleEditPost()** : Traite la soumission du formulaire de modification.
  - **exampleAdd()** : Affiche le formulaire d'ajout.
  - **exampleAddPost()** : Traite la soumission du formulaire d'ajout.
  - **exampleDelete()** : Supprime un élément.

Pour afficher la page sur https://votresite.fr/cmw-admin/example/manage votre package doit dans notre cas avoir dans le dossier **Views** du package un fichier `manage.admin.view.php` pareil pour les autres méthodes (voir code du controller admin)

**manage.admin.view.php :**
```php
<?php

$title = "Titre de la page";
$description = "Description de la page";
?>
En dev ...
```

**Remarque :**
Ce contrôleur admin est basique, mais couvre toutes les fonctionnalités nécessaires pour gérer les questions et réponses du package FAQ, y compris l'édition, l'ajout et la suppression. Chaque action est protégée par des permissions spécifiques.

### Conclusion
Les controllers public et admin sont essentiels pour gérer les interactions utilisateur et administrateur dans le package Example. Le contrôleur public sert à afficher des informations aux utilisateurs, tandis que le contrôleur admin est utilisé pour gérer ces informations via une interface protégée par des permissions.