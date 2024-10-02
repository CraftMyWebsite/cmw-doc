Les **models** sont utilisés pour effectuer des opérations de base de données dans votre package. Ils permettent de manipuler les données, de les récupérer et de les structurer sous forme d'entités. Dans le cadre de notre package Example, le modèle sera utilisé pour interagir avec la table **cmw_example**.

**Nous allons voir comment utiliser le modèle pour :**
- Récupérer une entrée spécifique à partir de son ID.
- Parcourir toutes les données de la table et les transformer en entités.

### Le Model : ExampleModel
Le fichier **ExampleModel.php** se trouve dans le répertoire **/App/Package/Example/Models**. Il étend la classe AbstractModel, ce qui permet de centraliser les opérations de gestion de base de données.

```php
<?php

namespace CMW\Model\Example;

use CMW\Entity\Example\ExampleEntity;
use CMW\Manager\Database\DatabaseManager;
use CMW\Manager\Package\AbstractModel;
use CMW\Model\Users\UsersModel;

/**
 * Class @ExampleModel
 * @package Example
 * @author Zomb
 * @version 0.0.1
 */
class ExampleModel extends AbstractModel
{

    /**
     * @param $exampleId
     * @return ExampleEntity|null
     */
    public function getExampleById($exampleId): ?ExampleEntity
    {
        $sql = 'SELECT * FROM cmw_example WHERE example_id=:example_id';

        $db = DatabaseManager::getInstance();
        $res = $db->prepare($sql);

        if (!$res->execute(['example_id' => $exampleId])) {
            return null;
        }

        $res = $res->fetch();

        $user = is_null($res['example_user_id']) ? null : UsersModel::getInstance()->getUserById($res['example_user_id']);

        return new ExampleEntity(
            $res['example_id'],
            $res['example_question'],
            $res['example_response'],
            $user
        );
    }

    /**
     * @return ExampleEntity[]
     */
    public function getAllExample(): array
    {
        $sql = 'SELECT example_id FROM cmw_example';
        $db = DatabaseManager::getInstance();

        $res = $db->prepare($sql);

        if (!$res->execute()) {
            return [];
        }

        $toReturn = [];

        while ($example = $res->fetch()) {
            $toReturn[] = $this->getExampleById($example['example_id']);
        }

        return $toReturn;
    }
}
```

### Explication du Code
- **Namespace** : Le modèle est situé dans le répertoire **/App/Package/Example/Models**, et son namespace est donc `CMW\Model\Example`.
- **Héritage** : Le modèle étend la classe **AbstractModel**, ce qui permet d'hériter des fonctionnalités communes aux modèles dans le CMS.
- **DatabaseManager** : Nous utilisons le **DatabaseManager** pour gérer les interactions avec la base de données. Ce gestionnaire fournit des méthodes pratiques pour préparer et exécuter des requêtes SQL.

### Méthode : `getExampleById`
Cette méthode permet de récupérer une entrée de la table cmw_example à partir de son ID.

- **Requête SQL :**
    - La requête SQL récupère les informations d'une entrée spécifique en fonction de son **example_id**.
    - La méthode utilise `DatabaseManager::getInstance()` pour préparer et exécuter la requête SQL.

- **Récupération de l'utilisateur :**
  - Après avoir récupéré les informations de la base de données, nous obtenons également les informations de l'utilisateur lié à cette entrée en appelant la méthode `getUserById` du modèle **UsersModel**.

- **Retourne une entité :**
  - La méthode retourne une instance de ExampleEntity, qui contient les données récupérées de la base de données ainsi que l'utilisateur associé.

### Méthode : `getAllExample`
Cette méthode permet de récupérer toutes les entrées de la table cmw_example.

- **Requête SQL** :
  - La requête SQL sélectionne uniquement les example_id de toutes les entrées dans la table.
- **Parcours des résultats** :
  - Pour chaque ID récupéré, la méthode appelle `getExampleById` pour transformer chaque ligne en une instance d'**ExampleEntity**.
- **Retourne un tableau d'entités** :
  - La méthode retourne un tableau d'objets **ExampleEntity**, représentant chaque entrée dans la table.

**Utilisation d'une entité externe (UsersModel)**

Dans ce modèle, nous utilisons le **UsersModel**, un modèle natif du Core, pour récupérer les informations de l'utilisateur lié à chaque question de la FAQ. Cela permet de stocker l'utilisateur dans l'entité **ExampleEntity**.

**Remarque Importante**
Tout comme pour les entités, il est recommandé d'utiliser uniquement des models provenant de packages natifs ou du Core. Cela évite des erreurs critiques si l'utilisateur n'a pas installé certains packages.
---
### Les Models (Suite)
En plus de la récupération des données via des requêtes SQL, les **models** permettent d'effectuer des actions de création, modification et suppression de données dans la base. Dans cette section, nous allons ajouter trois nouvelles méthodes au modèle **ExampleModel** pour gérer les FAQ : ajouter, éditer et supprimer des entrées.

### Méthode : `createExample`
Cette méthode permet d'ajouter une nouvelle entrée dans la table cmw_example.

```php
/**
 * @param string $question
 * @param string $response
 * @param int $authorId
 * @return ExampleEntity|null
 */
public function createExample(string $question, string $response, int $authorId): ?ExampleEntity
{
    $var = [
        'question' => $question,
        'response' => $response,
        'author' => $authorId
    ];

    $sql = 'INSERT INTO cmw_example (example_question, example_response, example_user_id) VALUES (:question, :response, :author)';

    $db = DatabaseManager::getInstance();
    $req = $db->prepare($sql);

    if ($req->execute($var)) {
        $id = $db->lastInsertId();
        return $this->getExampleById($id);
    }

    return null;
}
```

**Explication :**
- **Paramètres :**
  - **$question** : Le texte de la question à insérer dans la base de données.
  - **$response** : La réponse associée à la question.
  - **$authorId** : L'ID de l'utilisateur créateur de la question.
  - **Requête SQL** : La méthode exécute une requête **INSERT** pour ajouter une nouvelle ligne dans la table **cmw_example**.

- **Retour** : Si l'insertion réussit, la méthode retourne l'entité créée en utilisant la méthode `getExampleById()`. Sinon, elle retourne `null`.

### Méthode : `updateExample`
Cette méthode permet de modifier une entrée existante dans la table **cmw_example**.
```php
/**
 * @param int $exampleId
 * @param string $question
 * @param string $response
 * @return ExampleEntity|null
 */
public function updateExample(int $exampleId, string $question, string $response): ?ExampleEntity
{
    $info = [
        'example_id' => $exampleId,
        'example_question' => $question,
        'example_response' => $response
    ];

    $sql = 'UPDATE cmw_example SET example_question=:example_question, example_response=:example_response WHERE example_id=:example_id';

    $db = DatabaseManager::getInstance();
    $req = $db->prepare($sql);
    
    if ($req->execute($info)) {
        return $this->getExampleById($exampleId);
    }

    return null;
}
```

**Explication :**
- **Paramètres :**
  - **$exampleId** : L'ID de l'entrée à mettre à jour.
  - **$question** : Le nouveau texte de la question.
  - **$response** : La nouvelle réponse.
  - **Requête SQL** : La méthode exécute une requête **UPDATE** pour modifier les champs **example_question** et **example_response** d'une entrée spécifique.
- **Retour** : Si la modification réussit, la méthode retourne l'entité mise à jour. Sinon, elle retourne null.

### Méthode : `deleteExample`
Cette méthode permet de supprimer une entrée de la table **cmw_example**.
```php
/**
 * @param int $exampleId
 * @return void
 */
public function deleteExample(int $exampleId): void
{
    $sql = 'DELETE FROM cmw_example WHERE example_id=:example_id';

    $db = DatabaseManager::getInstance();
    $req = $db->prepare($sql);
    $req->execute(['example_id' => $exampleId]);
}
```

**Explication :**
- **Paramètres :**
  - **$exampleId** : L'ID de l'entrée à supprimer.
  - **Requête SQL** : La méthode exécute une requête DELETE pour supprimer une entrée de la table cmw_example en fonction de son ID.
- **Retour** : Cette méthode ne retourne rien, elle effectue simplement la suppression.

Ces trois méthodes **createExample**, **updateExample**, et **deleteExample** complètent le modèle en fournissant les actions de base pour la gestion des FAQ dans la table cmw_example. Elles permettent d'ajouter, modifier et supprimer des questions et réponses facilement à travers l'interface d'administration, tout en structurant les données sous forme d'entités.

---
### Utilisation des Models dans les Contrôleurs
Les **controllers** sont responsables de la gestion des interactions utilisateur et administrateur. Ils font appel aux models pour récupérer, manipuler et afficher les données sous forme d'entités dans les vues. Nous allons voir comment utiliser les méthodes du **model ExampleModel** dans les controllers **public** et **admin** pour gérer les questions et réponses de la FAQ.

### Model dans le Contrôleur Public
Le contrôleur public est utilisé pour afficher la liste des FAQ à l'utilisateur. Nous allons récupérer toutes les questions via le modèle et les transmettre à la vue.
```php
#[Link('/example', Link::GET)]
private function frontExamplePublic(): void
{
    $examples = ExampleModel::getInstance()->getAllExample();

    $view = new View('Example', 'main');
    $view->addVariableList(['examples' => $examples]);
    $view->view();
}
```
**Explication** :
- **Récupération des FAQ** : La méthode `getAllExample()` du modèle est utilisée pour récupérer toutes les FAQ de la base de données sous forme d'un tableau d'entités ExampleEntity.
- **Passage à la vue** : Les FAQ récupérées sont ajoutées à la vue via la méthode `addVariableList()`, ce qui permet de les afficher dans la vue correspondante.

### Affichage dans la Vue public
Le fichier de la vue **Public/Themes/X/Views/Example/main.view.php** doit afficher les questions et réponses.
```php
<?php

use CMW\Utils\Website;

/* @var \CMW\Entity\Example\ExampleEntity[] $examples */

/* TITRE ET DESCRIPTION */
Website::setTitle('Example');
Website::setDescription('Des questions et réponses');
?>

<?php foreach ($examples as $example): ?>
    <h5><?= $example->getQuestion() ?></h5>
    <p><?= $example->getResponse() ?></p>
<?php endforeach; ?>
```
**Explication :**
- **Boucle sur les FAQ :** Nous bouclons sur chaque entité `ExampleEntity` dans le tableau `$examples` et affichons la question et la réponse à l'utilisateur.

### Model dans le Contrôleur Admin
Le contrôleur admin est utilisé pour gérer les FAQ depuis le panneau d'administration. Nous allons afficher la liste des FAQ avec l'intégration de **simple-datatables**, ajouter une FAQ, et traiter les actions d'édition et de suppression.

### Affichage de la Liste des FAQ

Dans le contrôleur admin, nous allons récupérer toutes les FAQ et les afficher dans une table avec simple-datatables. (nous ne verrons pas cette partie ici à vous de mettre en place le FRONT)
```php
#[Link('/manage', Link::GET, [], '/cmw-admin/example')]
private function exampleList(): void
{
    UsersController::redirectIfNotHavePermissions('core.dashboard', 'example.show');

    $examples = ExampleModel::getInstance()->getAllExample();

    View::createAdminView('Example', 'manage')
        ->addStyle('Admin/Resources/Assets/Css/simple-datatables.css')
        ->addScriptAfter('Admin/Resources/Vendors/Simple-datatables/simple-datatables.js',
            'Admin/Resources/Vendors/Simple-datatables/config-datatables.js')
        ->addVariableList(['examples' => $examples])
        ->view();
}
```

**Explication :**
- **Récupération des FAQ** : Comme pour le contrôleur public, nous utilisons la méthode `getAllExample()` pour récupérer toutes les FAQ.
- **Affichage dans la Vue** : Les FAQ sont passées à la vue, et des fichiers CSS et JS sont ajoutés pour utiliser simple-datatables afin d'afficher les données dans une table interactive.

### Gestion de l'Ajout de FAQ - POST
La méthode POST de l'ajout des FAQ dans le contrôleur admin permet de récupérer les données soumises par l'administrateur, de créer une nouvelle FAQ via le modèle et de rediriger l'utilisateur.

```php
#[NoReturn] #[Link('/manage/add', Link::POST, [], '/cmw-admin/example')]
private function exampleAddPost(): void
{
    UsersController::redirectIfNotHavePermissions('core.dashboard', 'example.create');

    [$question, $response] = Utils::filterInput('question', 'response');
    $userId = UsersModel::getCurrentUser()?->getId();

    $addedExample = ExampleModel::getInstance()->createExample($question, $response, $userId);

    if ($addedExample) {
        Flash::send(Alert::SUCCESS, "Example", $addedExample->getQuestion() . " est ajouté !");
    } else {
        Flash::send(Alert::ERROR, "Example", "Impossible d'ajouter l'exemple !");
    }

    Redirect::redirectToAdmin('example/manage');
}
```
**Explication :**
- **Récupération des Données :** Nous utilisons Utils::filterInput() pour récupérer les données soumises par l'administrateur (question et réponse).
- **Création de la FAQ :** La méthode createExample() du modèle est appelée pour insérer la nouvelle FAQ dans la base de données. Si l'insertion est réussie, une alerte de succès est affichée, sinon une alerte d'erreur est envoyée.
- **Redirection :** Après l'ajout, l'administrateur est redirigé vers la page de gestion des FAQ.

### Gestion de l'Édition - POST
```php
#[NoReturn] #[Link('/edit/:id', Link::POST, ['id' => '[0-9]+'], '/cmw-admin/example')]
private function exampleEditPost(int $id): void
{
    UsersController::redirectIfNotHavePermissions('core.dashboard', 'example.edit');

    [$question, $response] = Utils::filterInput('question', 'response');

    $updatedExample = ExampleModel::getInstance()->updateExample($id, $question, $response);

    if ($updatedExample) {
        Flash::send(Alert::SUCCESS, "Example", $updatedExample->getQuestion() . " est mis à jour !");
    } else {
        Flash::send(Alert::ERROR, "Example", "Impossible de mettre à jour l'exemple !");
    }

    Redirect::redirectToAdmin('example/manage');
}

```

### Gestion de Suppression - GET
```php
#[NoReturn] #[Link('/delete/:id', Link::GET, ['id' => '[0-9]+'], '/cmw-admin/example')]
private function exampleDelete(int $id): void
{
    UsersController::redirectIfNotHavePermissions('core.dashboard', 'example.delete');

    ExampleModel::getInstance()->deleteExample($id);

    Flash::send(Alert::SUCCESS, "Example", "L'exemple a été supprimé !");
    Redirect::redirectToAdmin('example/manage');
}
```

**Explication :**
- **Édition** : Nous utilisons la méthode `updateExample()` pour modifier une entrée existante. Les données sont récupérées via le formulaire et, en cas de succès, une alerte de mise à jour est affichée.
- **Suppression** : La méthode `deleteExample()` est utilisée pour supprimer une FAQ de la base de données. Une alerte de confirmation est affichée après suppression.


---
### Conclusion
Le **model** est un élément central pour la gestion des données en base de données. Dans ce document, nous avons montré comment récupérer des données depuis la table cmw_example et les convertir en entités via les méthodes du modèle. Nous avons également vue comment les manipuler dans nos controllers. Cela permet de structurer les données et de faciliter leur manipulation dans le package **Example**.