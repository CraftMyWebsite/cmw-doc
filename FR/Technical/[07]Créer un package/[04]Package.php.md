Le fichier **Package.php** joue un rôle clé dans la définition des informations principales de votre package et de ses fonctionnalités au sein du CMS. Il permet notamment de déclarer le nom, la version, les auteurs, les dépendances et les menus associés au package. Ce fichier doit implémenter l'interface **IPackageConfig**, qui est essentielle pour que le CMS reconnaisse et configure correctement le package.

### Exemple de structure
Voici un exemple typique de la structure du fichier Package.php pour le package Example :

```php
<?php

namespace CMW\Package\Example;

use CMW\Manager\Lang\LangManager;
use CMW\Manager\Package\IPackageConfig;
use CMW\Manager\Package\PackageMenuType;
use CMW\Manager\Package\PackageSubMenuType;

class Package implements IPackageConfig
{
    public function name(): string
    {
        return 'Example';
    }

    public function version(): string
    {
        return '0.0.1';
    }

    public function authors(): array
    {
        return ['Zomb'];
    }

    public function isGame(): bool
    {
        return false;
    }

    public function isCore(): bool
    {
        return false;
    }

    public function menus(): ?array
    {
        return [
            new PackageMenuType(
                icon: 'fas fa-question-circle',
                title: LangManager::translate('example.title'),
                url: null,
                permission: null,
                subMenus: [
                    new PackageSubMenuType(
                        title: LangManager::translate('example.manage'),
                        permission: 'example.show',
                        url: 'example/manage',
                    ),
                ]
            ),
        ];
    }

    public function requiredPackages(): array
    {
        return ['Core'];
    }

    public function uninstall(): bool
    {
        // Return true, we don't need other operations for uninstall.
        return true;
    }
}

```

### Détails des méthodes
- **name()** : Retourne le nom du package. Ce nom est utilisé par le CMS pour identifier le package.
- **version()** : Retourne la version actuelle du package. Cela permet de gérer les mises à jour et les compatibilités.
- **authors()** : Retourne un tableau des auteurs du package. Ce tableau peut contenir plusieurs contributeurs.
- **isGame()** : Cette méthode permet de savoir si le package est lié à un jeu. Ici, elle retourne false car le package Example n'est pas un package de jeu.
- **isCore()** : Indique si le package fait partie du noyau du CMS. Ici, elle retourne false car le package Example n'est pas un package de base.
- **menus()** : Cette méthode définit les menus et sous-menus associés au package. Vous pouvez définir des menus avec des icônes, des permissions et des sous-menus. Les traductions sont gérées par `LangManager`.
- **requiredPackages()** : Retourne un tableau des packages requis pour le bon fonctionnement du package Example. Dans cet exemple, le package Core est requis.
- **uninstall()** : Cette méthode gère la désinstallation du package. Elle retourne `true` dans cet exemple, indiquant qu'aucune autre opération n'est nécessaire pour désinstaller le package.

### Utilisation des Menus et Permissions
L'un des aspects clés du fichier Package.php est la gestion des menus via la méthode menus(). Dans l'exemple ci-dessus, un menu avec l'icône fas fa-address-book est défini, ainsi qu'un sous-menu Settings qui nécessite la permission example.settings.

Chaque sous-menu est représenté par une instance de la classe PackageSubMenuType, qui permet de définir :
- **title** : Le titre du sous-menu.
- **permission** : La permission requise pour accéder au sous-menu.
- **url** : L'URL à laquelle le sous-menu redirige.

### Utilisation du LangManager
Le **LangManager** est utilisé ici pour traduire le titre du menu à l'aide de la fonction `LangManager::translate('example.title')`. Cela permet d'internationaliser le package et de gérer les traductions.

### Conclusion
Le fichier **Package.php** est indispensable pour définir les informations de base du package, comme son nom, sa version, ses auteurs, ainsi que ses dépendances. Il permet également de configurer les menus, les sous-menus et les permissions associés au package. Veillez à bien implémenter l'interface IPackageConfig pour que le CMS puisse charger correctement votre package et toutes ses fonctionnalités.