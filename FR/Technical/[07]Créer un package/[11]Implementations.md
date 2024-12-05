Les **implémentations** sont utilisées pour fournir des informations ou des fonctionnalités spécifiques à d'autres packages. Cela permet à un package d'intégrer ou d'utiliser des fonctionnalités de votre package. Dans notre exemple, nous allons implémenter un menu à partir du package Core dans notre package Example.

### Structure des Implémentations
Les implémentations doivent être placées dans un sous-dossier qui porte le nom du package auquel elles se rapportent. Cela permet au CMS de charger dynamiquement ces implémentations si le package cible est installé. Si ce package n'est pas installé, le CMS ne chargera pas les implémentations.

Dans notre exemple, nous allons implémenter le menu à partir du package Core, et donc la structure du dossier sera la suivante :
`Example/Implementations/Core/ExampleMenuImplementations.php`

::: warning
Le nom du sous-dossier **Core** est important car il correspond au nom du package que vous implémentez. Si le package Core n'est pas installé, le CMS ne chargera pas cette implémentation.
:::

### Exemple d'Implémentation de Menu
Nous allons maintenant voir comment implémenter un menu dans le package Core pour qu'il soit affiché dans le panneau d'administration ou dans le menu de navigation du thème de l'utilisateur.

```php
<?php

namespace CMW\Implementation\Example\Core;

use CMW\Interface\Core\IMenus;

class ExampleMenuImplementations implements IMenus
{
    public function getRoutes(): array
    {
        return [
            "Example" => 'example'
        ];
    }

    public function getPackageName(): string
    {
        return 'Example';
    }
}
```

**Explication du Code :**
- **Namespace** : Le namespace correspond à l'emplacement du fichier dans le dossier Implementations de notre package. Cela permet au CMS de retrouver l'implémentation.
- **Interface IMenus** : Cette classe implémente l'interface IMenus du package Core, qui est responsable de la gestion des menus dans le CMS. Vous devez respecter la structure de l'interface pour que l'implémentation soit reconnue par le CMS.
- **getRoutes()** :
  - Cette méthode retourne un tableau de routes qui définissent les menus à ajouter. Ici, nous ajoutons un menu nommé Example, qui pointe vers l'URL example.
  - Ces routes sont utilisées pour générer des liens dans le panneau d'administration ou le menu de navigation du site.
- **getPackageName()** :
  - Cette méthode retourne le nom du package auquel l'implémentation se rapporte, dans ce cas, Example. Cela permet de lier correctement l'implémentation à son package.

### Utilisation des Implémentations
Les implémentations peuvent servir à bien plus que l'ajout de menus. Voici quelques exemples de ce que vous pouvez implémenter dans d'autres packages :

- **Shop** : Implémentation de méthodes de paiement, de types de prix, ou de nouveaux types d'items virtuels.
- **Vote** : Implémentation de types de récompenses pour les systèmes de vote.

Les implémentations permettent donc d'étendre les fonctionnalités d'un autre package de manière modulaire. Vous pouvez vous renseigner sur les packages que vous souhaitez implémenter pour découvrir les interfaces disponibles et les fonctionnalités extensibles.

### Remarque Importante

Il est impératif de nommer correctement le sous-dossier dans Implementations. Le sous-dossier doit porter le nom du package auquel vous vous référez. Cela garantit que le CMS ne charge l'implémentation que si le package cible est installé. Si le package n'est pas installé, le CMS ignorera automatiquement cette implémentation.

Dans notre exemple :

`Example/Implementations/Core/`

Le sous-dossier Core fait référence au package Core du CMS. Cela permet d'éviter des erreurs de chargement si le package Core n'est pas présent.

### Conclusion
Les implémentations sont un moyen puissant de rendre votre package extensible et interopérable avec d'autres packages. Elles permettent d'ajouter des fonctionnalités spécifiques à d'autres packages sans dépendances lourdes. En suivant les bonnes pratiques, vous pouvez rendre votre package plus flexible et compatible avec les modules existants dans le CMS.

Dans cette documentation, nous avons couvert :

- La **structure** des implémentations et l'importance du nom du sous-dossier.
- Un **exemple** d'implémentation de menu pour le package Core.
- L'usage avancé des implémentations dans des packages comme Shop ou Vote.
Cette flexibilité rend vos packages plus modulaires et extensibles dans l'écosystème du CMS.
