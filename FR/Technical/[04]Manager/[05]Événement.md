### Explication
**Event** est un système d'événements et d'écouteurs dans un contexte fournis. Voici une explication des différentes parties :

### Comment ça fonctionne dans l'ensemble ?
- Un événement est défini en créant une classe qui hérite de `AbstractEvent`. 
- Des méthodes dans d'autres classes peuvent être marquées avec l'attribut `Listener`, ce qui les lie à un événement particulier. 
- Lorsqu'un événement est émis via `Emitter::send()`, tous les écouteurs associés à cet événement sont appelés dans l'ordre de priorité. 
- Si l'un des écouteurs appelle `stopPropagation()`, la propagation de l'événement s'arrête, et les écouteurs suivants ne sont pas exécutés.
  
### Exemple d'utilisation :

Un événement "RegisterEvent" pourrait être créé, avec plusieurs méthodes marquées avec l'attribut `Listener`. Lorsqu'un utilisateur s'enregistre, l'événement "RegisterEvent" est émis automatiquement, et chaque méthode liée à cet événement, par exemple, votre package pourrait facilement envoyer un email de bienvenue ou ajouter des points de fidélité...
Renseignez-vous donc sur les différents Event déjà existant

**En voici quelques-uns déjà existant :**

- **Package Users :**
  - DeleteUserAccountEvent
  - LoginEvent
  - LogoutEvent
  - RegisterEvent
- **Package Shop :**
    - ShopAddCatEvent
    - ShopAddItemEvent
    - ShopDeleteCatEvent
    - ShopDeleteItemEvent
    - ShopEditCatEvent
    - ShopEditItemEvent
    - ShopPaymentCancelEvent
    - ShopPaymentCompleteEvent
    - ...
  
---
### Exemple de cas concret :

Nous allons créer un événement : à chaque fois qu'un utilisateur créer un compte, puis dans un second temps, nous allons appeler cet événement pour réaliser différente opération quand un utilisateur s'enregistre.

### Package parent (Users ici) :
Le package "parent" est celui qui créer et applique l'événement

#### 1- Création d'un événement :
Dans notre cas, nous sommes donc dans le package Users, il nous faut donc un dossier **Events** (App/Package/Users/**Events**) nous créons l'événement **RegisterEvent.php** dans ce dossier Event
```php
<?php

namespace CMW\Event\Users;

use CMW\Manager\Events\AbstractEvent;

/**
 * La classe RegisterEvent représente un événement spécifique lié à l'enregistrement des utilisateurs.
 * Elle hérite de la classe abstraite AbstractEvent qui définit la structure de base des événements.
 */
class RegisterEvent extends AbstractEvent
{
    /**
     * Cette méthode renvoie le nom de l'événement.
     * Ici, elle est implémentée pour retourner un nom unique 'RegisterEvent-Users-CraftMyWebsite'.
     * 
     * Le choix d'un nom de cet événement inclut non seulement le nom de l'action ('RegisterEvent'),
     * mais aussi un contexte plus large ('Users' et 'CraftMyWebsite'), ce qui permet d'éviter
     * des conflits ou des collisions avec d'autres événements portant un nom similaire.
     * 
     * Ce choix est particulièrement important dans des systèmes complexes où des événements
     * peuvent avoir des noms semblables.
     * 
     * @return string Le nom unique de l'événement.
     */
    public function getName(): string
    {
        return 'RegisterEvent-Users-CraftMyWebsite';  // évitez donc les noms trop simples :)
    }
}
```
#### 2- Appel de l'événement
Une fois l'événement créé, il faut maintenant que notre package puisse appliquer les écoute faites sur cet événement :

Dans cet exemple, nous l'appliquons à l'enregistrement utilisateur on se rend donc dans (App/Package/Users/Controllers/**UsersController.php**)

On édite la fonction qui enregistre l'utilisateur :

```php
#[Link('/register', Link::POST)]
private function registerPost(): void
{
    /* ... Partie précédente du code ...*/
    Emitter::send(RegisterEvent::class, $userId);
    /* ... Partie suivante du code ...*/
}
```
Dans ce cas, nous fournissons une variable `$userId` (mixed) que nous utiliserons plus tard.

### Package utilisant l'événement (Forum ici) :

Dans notre controller, nous appelons l'événement précédemment mis en place :
```php
#[Listener(eventName: RegisterEvent::class, times: 0, weight: 1)]
public static function onRegister(mixed $userId): void
{
    //Méthode à exécuter quand l'événement est écouté
    ForumPermissionRoleModel::getInstance()->addUserForumDefaultRoleOnRegister($userId);
    ForumUserBlockedModel::getInstance()->addDefaultBlockOnRegister($userId);
}
```
Vous avez donc pu constater que j'utilise la précédente variable `$userId` pour faire savoir à mon controller Forum quel utilisateur appel cet événement.
Mais `$userId` pourrait être n'importe quel variable ou ne même ne pas être utilisé.

---

### A savoir !
::: info
Le package peut à la fois le créer l'appliquer et l'écouter, vous n'êtes pas obligé d'avoir un package parent, mais vos événements pourrons être utilisés par d'autres packages, c'est pourquoi il se peut que votre package soit une dépendance pour un autre package et inversement, c'est pourquoi il est important de biens remplir ce type d'informations dans **Package.php** :
```php
public function requiredPackages(): array
{
    return ['Users', '...'];
}
```
:::
