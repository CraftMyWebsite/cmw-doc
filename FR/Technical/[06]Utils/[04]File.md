La classe `File` permet la gestion des fichiers

### Importer le namespace
`use CMW\Utils\File;`

La classe `File` dans le namespace `CMW\Utils` fournit des méthodes statiques pour interagir avec les fichiers. Elle permet d'écrire, de lire des fichiers sous forme de chaîne de caractères ou de tableau, tout en effectuant des vérifications de base pour s'assurer que les fichiers sont accessibles.

### Méthode `write()`

Cette méthode permet d'écrire du contenu dans un fichier spécifié, avec des vérifications préalables sur la lisibilité et la possibilité d'écriture du fichier.

```php
$result = File::write('/path/to/file.txt', 'Contenu du fichier');
echo $result ? 'Fichier écrit avec succès' : 'Échec de l\'écriture';
```

### Méthode `read()`
Cette méthode permet de lire le contenu d'un fichier sous forme de chaîne de caractères, avec des vérifications pour s'assurer que le fichier est lisible.
```php
$content = File::read('/path/to/file.txt');
echo $content !== false ? $content : 'Échec de la lecture';
```

### Méthode `readArray()`
Cette méthode permet de lire le contenu d'un fichier et de le retourner sous forme de tableau, chaque ligne du fichier correspondant à un élément du tableau.
```php
$contentArray = File::readArray('/path/to/file.txt');
print_r($contentArray);
```

--- 
La classe `File` facilite les opérations courantes de lecture et d'écriture de fichiers avec des vérifications préventives pour s'assurer que les fichiers sont accessibles. Elle est particulièrement utile pour éviter des erreurs liées aux permissions et à l'existence des fichiers.