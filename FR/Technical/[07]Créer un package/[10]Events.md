Les **events** dans le CMS permettent de déclencher des actions spécifiques lorsqu'un certain événement se produit. Ils sont utiles pour rendre votre package extensible et interagir avec d'autres composants ou packages. Dans cette page, nous allons créer un event qui est émis lors de l'ajout d'une nouvelle FAQ, et voir comment d'autres packages peuvent écouter cet événement.

### Création d'un Event
Dans notre package **Example**, nous allons créer un **event** qui sera émis chaque fois qu'une nouvelle FAQ est ajoutée. Ce fichier sera placé dans le dossier **Events** du package.
```php
<?php
namespace CMW\Event\Example;

use CMW\Manager\Events\AbstractEvent;

class CreateEvent extends AbstractEvent
{
    public function getName(): string
    {
        return 'CreateEvent-Example-CraftMyWebsite';  // Évitez les noms trop simples :)
    }
}
```

**Explication :**
- **Nom de l'Event** : La méthode getName() retourne le nom unique de l'événement. Il est recommandé d'utiliser un nom descriptif et d'éviter les noms trop génériques pour éviter les conflits avec d'autres événements.
- **Héritage** : La classe CreateEvent hérite de AbstractEvent, ce qui permet au CMS de gérer cet événement avec le système d'émission d'événements.

### Émission d'un Event

L'événement doit être émis lorsque certaines actions se produisent. Dans notre exemple, l'événement sera émis lorsque l'administrateur ajoute une nouvelle FAQ dans le package Example. Nous allons modifier notre contrôleur pour inclure l'émission de cet événement.

**Ajout de l'Event dans le Contrôleur**

Nous allons ajouter l'émission de l'event `CreateEvent` dans la méthode `exampleAddPost()` du contrôleur **ExampleAdminController**.

Controller modifié :
```php
#[NoReturn] #[Link('/manage/add', Link::POST, [], '/cmw-admin/example')]
private function exampleAddPost(): void
{
    UsersController::redirectIfNotHavePermissions('core.dashboard', 'example.create');

    [$question, $response] = Utils::filterInput('question', 'response');
    $userId = UsersModel::getCurrentUser()?->getId();

    $addedExample = ExampleModel::getInstance()->createExample($question, $response, $userId);

    if ($addedExample) {
        // Émission de l'événement après l'ajout réussi de la FAQ
        Emitter::send(CreateEvent::class, $addedExample);

        Flash::send(Alert::SUCCESS, "Example", $addedExample->getQuestion() . " est ajouté !");
    } else {
        Flash::send(Alert::ERROR, "Example", "Impossible d'ajouter l'exemple !");
    }

    Redirect::redirectToAdmin('example/manage');
}
```

**Explication :**
- **Émission de l'Event** : Nous utilisons `Emitter::send()` pour émettre l'événement **CreateEvent** après que la FAQ ait été ajoutée avec succès. L'entité **ExampleEntity** de la FAQ ajoutée est passée comme paramètre à l'événement, ce qui permet de transmettre les informations de la FAQ à tout package ou composant écoutant cet événement.

---

### Écouter un Event dans un autre Package
D'autres packages peuvent écouter cet événement et agir en conséquence. Par exemple, un package peut vouloir ajouter une fonctionnalité supplémentaire lorsqu'une FAQ est ajoutée, comme l'envoi d'une notification ou la mise à jour d'une autre partie du système.

**Exemple d'Écoute d'un Event**
Pour écouter l'événement CreateEvent dans un autre package, voici comment procéder :
```php
#[Listener(eventName: CreateEvent::class, times: 0, weight: 1)]
public static function onCreateExample(ExampleEntity $addedExample): void
{
    $value = $addedExample->getQuestion();
    // Utilisez $addedExample pour effectuer des actions après l'ajout d'une FAQ
    // Par exemple, envoyer une notification ou enregistrer un log
}
```

**Explication :**
- **Listener** : L'annotation #[Listener] permet d'écouter un événement spécifique. Ici, nous écoutons l'événement CreateEvent en spécifiant le nom de l'événement dans eventName: CreateEvent::class.

- Paramètres :
  - **times** : Indique combien de fois l'écoute de l'événement doit se produire. Si la valeur est `0`, l'événement sera écouté un nombre illimité de fois.
  - **weight** : Détermine l'ordre dans lequel les événements sont écoutés. Un poids plus élevé signifie que cet événement sera écouté avant les autres avec un poids plus faible.
  - **Manipulation de l'Entité** : L'entité `ExampleEntity` est passée en paramètre à la méthode d'écoute. Vous pouvez ainsi utiliser les méthodes de cette entité pour récupérer les informations de la FAQ récemment ajoutée et effectuer des actions comme envoyer une notification ou interagir avec une autre partie de votre application.

### Conclusion

Les events offrent une grande flexibilité pour rendre votre package extensible et réactif aux actions des utilisateurs. Voici les étapes que nous avons couvertes :

- **Création d'un événement** dans le package Example qui est émis lorsqu'une nouvelle FAQ est ajoutée.
- **Émission de l'événement** dans le contrôleur admin après l'ajout d'une FAQ avec succès.
- **Écoute de l'événement** dans un autre package pour réagir à l'ajout d'une FAQ.
Ces événements permettent à votre package de déclencher des actions dans d'autres parties du CMS et rendent votre application plus modulaire et extensible.