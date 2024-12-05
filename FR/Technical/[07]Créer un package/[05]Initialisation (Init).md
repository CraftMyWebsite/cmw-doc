L'initialisation est une étape cruciale lors de la création d'un package pour le CMS. Elle permet de configurer correctement la base de données, les permissions et la désinstallation du package. Le répertoire Init contient trois fichiers clés qui sont automatiquement pris en charge lors de l'installation du package via l'interface administrateur ou le **Market** du CMS.

Les fichiers d'initialisation sont les suivants :

- **init.sql** : Ce fichier contient les commandes SQL pour créer les tables nécessaires à votre package.
- **Permissions.php** : Ce fichier gère les permissions associées à votre package.
- **uninstall.sql** : Ce fichier gère la suppression des tables lors de la désinstallation du package.
  
Ces fichiers sont automatiquement injectés et intégrés lors de l'installation du package. Toutefois, lors de l'installation manuelle, les développeurs doivent exécuter eux-mêmes les commandes SQL et flush les permissions depuis l'interface d'administration.

### Le Fichier init.sql

Le fichier init.sql permet de créer les tables nécessaires à votre package dans la base de données. Dans notre exemple, nous créons une table **cmw_example** pour stocker les questions et réponses d'un système de FAQ.

::: warning
Nommez toujours vos tables : `cmw_X` ne pas respecter ceci peut entrainer un refus lors de la publication de votre package sur le marketplace !
:::

**Exemple de contenu pour init.sql :**
```sql
CREATE TABLE IF NOT EXISTS `cmw_example`
(
    `example_id`       INT          AUTO_INCREMENT PRIMARY KEY,
    `example_question` TEXT         NOT NULL,
    `example_response` TEXT         NOT NULL,
    `example_user_id`  INT          NOT NULL,
    CONSTRAINT fk_example_example_user_id FOREIGN KEY (example_user_id)
    REFERENCES cmw_users (user_id) ON UPDATE CASCADE ON DELETE CASCADE
) ENGINE = InnoDB
  CHARACTER SET = utf8mb4
  COLLATE = utf8mb4_unicode_ci;
```

**Détails :**
- **example_id** : L'identifiant unique de la question.
- **example_question** : Le texte de la question.
- **example_response** : La réponse associée à la question.
- **example_user_id** : Référence à l'utilisateur ayant créé la question (relation avec la table cmw_users).

### Le Fichier Permissions.php
Le fichier **Permissions.php** permet de définir les permissions spécifiques à votre package. Ces permissions sont essentielles pour contrôler l'accès aux différentes fonctionnalités du package, comme la création, l'édition ou la suppression de questions et réponses.

```php
<?php

namespace CMW\Permissions\Example;

use CMW\Manager\Lang\LangManager;
use CMW\Manager\Permission\IPermissionInit;
use CMW\Manager\Permission\PermissionInitType;

class Permissions implements IPermissionInit
{
    public function permissions(): array
    {
        return [
            new PermissionInitType(
                code: 'example.show',
                description: LangManager::translate('example.permissions.show'),
            ),
            new PermissionInitType(
                code: 'example.create',
                description: LangManager::translate('example.permissions.create'),
            ),
            new PermissionInitType(
                code: 'example.edit',
                description: LangManager::translate('example.permissions.edit'),
            ),
            new PermissionInitType(
                code: 'example.delete',
                description: LangManager::translate('example.permissions.delete'),
            ),
        ];
    }
}
```

**Détails des permissions :**
- **example.show** : Permet d'afficher les questions et réponses.
- **example.create** : Permet de créer de nouvelles questions.
- **example.edit** : Permet de modifier les questions existantes.
- **example.delete** : Permet de supprimer des questions.

### Le Fichier uninstall.sql
Le fichier uninstall.sql est exécuté lors de la désinstallation du package pour supprimer les tables associées à celui-ci.

**Exemple de contenu pour uninstall.sql :**
```sql
DROP TABLE IF EXISTS `cmw_example`;
```

**Détails :**
Cette commande `DROP TABLE` supprime la table **cmw_example** si elle existe, assurant ainsi que toutes les données associées au package sont supprimées lors de la désinstallation.

---

### Installation via le Market
Lorsque vous installez un package via le Market du CMS, tout le processus d'initialisation est géré automatiquement. Cela inclut :

- L'exécution de init.sql pour créer les tables en base de données.
- L'injection des permissions définies dans Permissions.php.
- La gestion de la désinstallation via uninstall.sql.

### Installation manuelle
Dans le cas d'une installation manuelle, voici les étapes à suivre :

- **Intégrer le SQL** : Vous devez exécuter manuellement les commandes SQL contenues dans init.sql sur votre base de données.
- **Flush des permissions** : Rendez-vous dans l'interface administrateur et effectuez un flush des permissions pour que celles définies dans Permissions.php soient prises en compte.

### Conclusion
L'initialisation d'un package est essentielle pour assurer que les tables, permissions et scripts de désinstallation soient correctement configurés et fonctionnels. Lorsque vous développez un package, assurez-vous que ces fichiers sont bien définis et que toutes les étapes d'installation et de désinstallation sont couvertes, qu'il s'agisse d'une installation via le Market ou d'une installation manuelle.