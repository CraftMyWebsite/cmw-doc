### Explication
**ImagesManager** gère le téléchargement, la suppression et la gestion des images. Elle permet de gérer différents types de fichiers d'images et offre plusieurs fonctionnalités autour des images, comme l'upload, la suppression, et le traitement de métadonnées.

### Méthodes principales

`convertAndUpload($file, $dirName, $targetFormat, $quality, $keepName, $customName)`

Cette méthode convertit une image dans un autre format avant de l'uploader, ce qui est utile pour optimiser le poids des fichiers ou adapter les images à différents besoins.

- **Paramètres** :
  - `$file` : Fichier image à convertir et uploader.
  - `$dirName` : Répertoire de destination pour l'image convertie.
  - `$targetFormat` : Format cible pour la conversion (par exemple, ImagesFormat::WEBP).
  - `$quality` : Qualité de l'image (en pourcentage, de 0 à 100) pour les formats compressibles.
  - `$keepName` : Si true, conserve le nom original ; sinon, un nom aléatoire est généré.
  - `$customName` : Permet de définir un nom personnalisé pour le fichier converti.

- **Fonctionnement** :
  - Appelle la méthode upload() pour uploader l'image originale.
  - Vérifie l'extension actuelle de l'image et effectue une conversion seulement si le format est différent de celui souhaité.
  - Crée l'image convertie avec la qualité spécifiée.
  - Supprime l'image originale pour garder uniquement la version convertie.

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

`uploadMultiple($files, $dirName)`
- Cette méthode permet de télécharger plusieurs fichiers en appelant la méthode `upload()` pour chaque fichier.
- Elle retourne un tableau contenant les noms des fichiers qui ont été téléchargés.

`deleteImage($imageName, $dirName)`
- Cette méthode permet de supprimer une image spécifique du répertoire Public/Uploads/.

### Exemple d'utilisation :

### Méthode favorite (`convertAndUpload`) :
```php
$image = $_FILES['image'];
$convertedImageName = ImagesManager::convertAndUpload($image, 'Folder', ImagesFormat::WEBP, 80);
```

Stockage d'une image sans conversion :
```php
$imageName = ImagesManager::upload([$file], 'dirName', ?$keepName, ?"customName");
```

Suppression :
```php
ImagesManager::deleteImage($image, 'Folder');
```

::: warning
Lors de l'ajout n'oubliez pas de stocker son nom en base de données !

Lors de la suppression n'oubliez pas de la supprimer de votre base de données !
:::