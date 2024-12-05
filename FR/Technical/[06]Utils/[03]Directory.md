La classe `Directory` permet la gestion des fichiers et répertoires

### Importer le namespace
`use CMW\Utils\Directory;`

La classe `Directory` dans le namespace `CMW\Utils` offre une série de méthodes statiques pour gérer les fichiers et répertoires. Elle permet de parcourir récursivement des répertoires, de filtrer les fichiers par extension, et de manipuler des dossiers (création, suppression, etc.).

### Méthode `getFilesRecursively()`
Cette méthode permet de récupérer récursivement tous les fichiers d'un répertoire, avec la possibilité de filtrer par extension.
```php
$files = Directory::getFilesRecursively('/path/to/dir', 'txt');
print_r($files); // Liste des fichiers .txt trouvés récursivement
```

### Méthode `getElements()`
Cette méthode retourne les éléments d'un répertoire (fichiers et sous-dossiers), sauf les entrées spéciales `.` et `..`.
```php
$elements = Directory::getElements('/path/to/dir');
print_r($elements); // Liste des fichiers et dossiers présents dans le répertoire
```

### Méthode `getFiles()`
Cette méthode retourne uniquement les fichiers contenus dans un répertoire.
```php
$files = Directory::getFiles('/path/to/dir');
print_r($files); // Liste des fichiers dans le répertoire spécifié
```

### Méthode `getFolders()`
Cette méthode retourne uniquement les sous-dossiers d'un répertoire.
```php
$folders = Directory::getFolders('/path/to/dir');
print_r($folders); // Liste des sous-dossiers présents dans le répertoire
```

### Méthode `delete()`
Cette méthode permet de supprimer récursivement un répertoire et son contenu, ou un fichier.
```php
$result = Directory::delete('/path/to/dir');
echo $result ? 'Deleted successfully' : 'Failed to delete';
```

### Méthode `createFolders()`
Cette méthode permet de créer un ou plusieurs répertoires. Elle crée également les répertoires parents si nécessaire.
```php
$result = Directory::createFolders('/path/to/dir1', '/path/to/dir2');
echo $result ? 'Folders created' : 'Failed to create folders';
```

---

La classe Directory propose un ensemble complet de fonctionnalités pour parcourir, filtrer, manipuler et supprimer des fichiers et des répertoires. Elle est particulièrement utile pour les tâches de gestion des fichiers dans des applications nécessitant une interaction fréquente avec le système de fichiers.