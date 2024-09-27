### Explication

**SimpleCacheManager** gère un système de cache simple basé sur des fichiers JSON.

Gestion du cache par fichiers : Les fichiers de cache sont stockés dans un répertoire défini (App/Storage/Cache). Le chemin complet est construit à partir d'une valeur d'environnement.

Voici les fonctionnalités principales :

- `getCache` : Récupère le contenu d'un fichier de cache en le décodant depuis le format JSON. Si le fichier n'existe pas, retourne null.
- `storeCache` : Enregistre de nouvelles données dans un fichier de cache, après avoir créé les dossiers nécessaires et supprimé l'ancien fichier si présent.
- `cacheExist` : Vérifie simplement si un fichier de cache existe.
- `editCacheValue` : Modifie une valeur spécifique en la remplaçant par une nouvelle.
- `deleteSpecificCacheFile` : Supprime un fichier de cache spécifique.


Ce système permet d'optimiser les performances en stockant des données temporaires qui peuvent être rapidement récupérées sans recalculer.

### Importer le namespace

`use CMW\Manager\Cache\SimpleCacheManager;`

### Utiliser le manager de cache

_`getCache` retourne une valeur mixte :_
```php
SimpleCacheManager::getCache("fileName", "sub/folder");
```
---
_`storeCache` ne retourne rien :_
```php
SimpleCacheManager::storeCache("value", "fileName", "sub/folder");
```
---
_`cacheExist` retourne un booléen :_
```php
SimpleCacheManager::cacheExist("fileName", "sub/folder");
```
---
_`editCacheValue` ne retourne rien :_
```php
SimpleCacheManager::editCacheValue("valueKey", "newValue", "fileName", "sub/folder");
```
---
_`deleteSpecificCacheFile` ne retourne rien :_
```php
SimpleCacheManager::deleteSpecificCacheFile("fileName", "sub/folder");
```

### Dépannage
Stockage :
Le fichier cache est enregistrée dans `App/Storage/Cache/XXX` il est possible que celui-ci ne puisse pas s'enregistrer correctement si vous avez des problèmes d'écriture et de lecture sur ce dossier.