## Principe

Le mode standalone permet d'exécuter des scripts PHP indépendamment du cycle de vie HTTP classique du CMS. C'est particulièrement utile pour :
- Les workers et scripts en arrière-plan
- Les tâches planifiées (cron)
- Les batchs de traitement de données

## Fonctionnement

Le bootstrap standalone charge uniquement les composants essentiels du CMS :
- Le chargement du projet
- La gestion des erreurs
- Les attributs
- La locale
- Un fichier d'environnement dédié (`.env.standalone`)

## Utilisation

### Intégration dans un script

```php
// Load Standalone Bootstrap
require 'App/Bootstrap/standalone.php';

// Votre code ici
```

### Exemple avec un worker

Créez votre worker dans votre package :

```php
// App/Package/MonPackage/Classes/Workers/Batchs/MyBatchChecker.php

require 'App/Bootstrap/standalone.php';

// Logique du batch
// Accès aux managers, modèles, etc.
```

Exécutez-le directement depuis la ligne de commande :

```shell
php App/Package/MonPackage/Classes/Workers/Batchs/MyBatchChecker.php
```

## Configuration

Le mode standalone utilise un fichier `.env.standalone` à la racine du projet. Ce fichier permet de définir des variables d'environnement spécifiques aux scripts standalone, sans impacter la configuration principale.

## Référence

Implémentation : [commit b00403a](https://github.com/CraftMyWebsite/cmw-core/commit/b00403aabb9a2214ffeb7a924670d8b86fdf94a6)

