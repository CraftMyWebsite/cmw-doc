Dans cette section, nous allons expliquer comment déclarer correctement les **namespaces** pour vos fichiers PHP en fonction de leur emplacement au sein de la structure du package. L'utilisation correcte des namespaces est essentielle pour l'organisation du code et le bon fonctionnement de l'autoloading dans le CMS.

### 1. Controllers
Lorsque vous créez un contrôleur dans votre package, le namespace doit refléter l'arborescence des dossiers. Par exemple, si votre fichier MySuperController.php se trouve dans le répertoire suivant :

`/App/Package/Example/Controllers/Admin/Test/MySuperController.php`

Le namespace devra être déclaré ainsi dans votre fichier :

```php
namespace CMW\Controller\Example\Admin\Test;
```
Il est important de respecter la hiérarchie des dossiers dans la déclaration du namespace pour que le CMS puisse localiser correctement votre classe.

Exemple de code pour un contrôleur :
```php
namespace CMW\Controller\Example\Admin\Test;

class MySuperController {
    // Votre code ici
}
```

### 2. Entities
Pour les entities, la déclaration du namespace suit également l'arborescence des dossiers. Par exemple, si votre entité MySuperEntity.php est dans le répertoire suivant :

`/App/Package/Example/Entities/Test/MySuperEntity.php`

Le namespace correspondant serait :
```php
namespace CMW\Entity\Example\Test;
```

Exemple de code pour une entité :
```php
namespace CMW\Entity\Example\Test;

class MySuperEntity {
    // Votre code ici
}
```

### 3. Modèles à la racine
Si un fichier se trouve à la racine de l'un des sous-dossiers principaux (par exemple, Models), le namespace sera plus simple. Par exemple, pour un modèle situé dans :

`/App/Package/Example/Models/MySuperModel.php`

Le namespace sera :

```php
namespace CMW\Model\Example;
```

Exemple de code pour un modèle :
```php
namespace CMW\Model\Example;

class MySuperModel {
    // Votre code ici
}
```

::: info
Ceci sont uniquement des exemples, vous pouvez placer un model dans un sous dossier et un controller à la racine !
:::

### 4. Utilisation des Namespaces et du Pattern Singleton
Dans votre architecture, au lieu d'instancier les objets via `new`, vous utilisez une approche basée sur le pattern Singleton avec la méthode `getInstance()`. Cela permet d'assurer qu'il n'y ait qu'une seule instance de chaque objet.

Lorsque vous déclarez des namespaces, il est impératif de vous assurer que les use sont correctement utilisés pour importer les classes depuis les bons namespaces. Voici un exemple de l'utilisation d'une classe dans un autre fichier :

**Exemple d'importation avec use :**
```php
namespace CMW\Controller\Example\Admin\Test;

use CMW\Model\Example\MySuperModel;

class MySuperController {
    public function handle() {
    $model = MySuperModel::getInstance()->XXX; //XXX représente la fonction ciblé de votre Model
    // Votre logique ici
    }
}
```

### Remarques Importantes :
- Le namespace doit toujours refléter la structure du répertoire.
- Si un fichier est déplacé, le namespace devra être mis à jour en conséquence.
- Les use doivent obligatoirement pointer vers les namespaces corrects pour éviter tout problème d'autoloading ou d'erreur de classe introuvable.
- L'utilisation de `getInstance()` garantit une gestion centralisée des instances, ce qui simplifie la gestion des objets partagés au sein de l'application.

### Conclusion 
Cette section vous guide dans la bonne déclaration des namespaces, garantissant une organisation claire du code et une intégration fluide avec le CMS.
Elle précise également l'importance d'utiliser le pattern Singleton pour les instanciations à travers la méthode getInstance(). Cela permet de maintenir une structure propre et performante