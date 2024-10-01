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

        $user = (new UsersModel())->getUserById($res['example_user_id']);

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

        while ($faq = $res->fetch()) {
            $toReturn[] = $this->getExampleById($faq['example_id']);
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

### Conclusion
Le **model** est un élément central pour la gestion des données en base de données. Dans ce document, nous avons montré comment récupérer des données depuis la table cmw_example et les convertir en entités via les méthodes du modèle. Cela permet de structurer les données et de faciliter leur manipulation dans le package **Example**.