### Explication
**ImagesManager** gère le téléchargement, la suppression et la gestion des images. Elle permet de gérer différents types de fichiers d'images et offre plusieurs fonctionnalités autour des images, comme l'upload, la suppression, et le traitement de métadonnées.

### Méthodes principales

`uploadMultiple($files, $dirName)`
- Cette méthode permet de télécharger plusieurs fichiers en appelant la méthode `upload()` pour chaque fichier.
- Elle retourne un tableau contenant les noms des fichiers qui ont été téléchargés.

`upload($file, $dirName, $keepName, $customName)`
- **Paramètres** :
  - `$file` : Le fichier image à télécharger.
  - `$dirName` : Le répertoire de destination pour l'image.
  - `$keepName` : Si `true`, garde le nom original du fichier, sinon un nom aléatoire est généré.
  - `$customName` : Permet de spécifier un nom personnalisé pour le fichier.
- **Fonctionnement** :
  - La méthode vérifie si le fichier est valide et s'il est dans un format autorisé via la variable `$allowedTypes`.
  - Si tout est en ordre, elle crée un nom de fichier (aléatoire, personnalisé ou original).
  - Elle copie ensuite l'image vers le répertoire de téléchargement (`Public/Uploads/`) et supprime ses métadonnées pour alléger le fichier (comme les informations EXIF, XMP, etc.).
- **Gestion des erreurs** : Des exceptions sont levées si le fichier n'est pas valide, trop volumineux, ou si l'opération d'upload échoue.

`deleteImage($imageName, $dirName)`
- Cette méthode permet de supprimer une image spécifique du répertoire Public/Uploads/.

### Exemple d'utilisation :

Stockage d'une image :
```php
$imageName = ImagesManager::upload([$file], 'dirName', ?$keepName, ?"customName");
```

**Exemple concret :**

Stockage :
```php
$image = $_FILES['image'];
$imageName = ImagesManager::upload($image, 'Folder');
```

Suppression :
```php
ImagesManager::deleteImage($image, 'Folder');
```

::: warning
Lors de l'ajout n'oubliez pas de stocker son nom en base de données !

Lors de la suppression n'oubliez pas de la supprimer de votre base de données !
:::