## Explication
**FilesManager** gère le téléchargement, la suppression et la manipulation de fichiers dans `Public/Uploads/`.  
Il sécurise les uploads (anti *path traversal*, vérification MIME, taille max, contrôle d’images) et fournit aussi des helpers autour des archives **ZIP** (création, ajout, suppression) + renommage.

## Types autorisés
Les types sont validés par **MIME** : images, documents, Office/OpenDocument, archives, audio/vidéo, etc.  
Si le MIME n’est pas présent dans la liste, l’upload est refusé.

---

## Méthodes principales

### `upload($file, $dirName, $keepName, $customName): string`
Upload un fichier dans `Public/Uploads/{dirName}/` et renvoie le **nom final** (avec extension).

- **Paramètres**
  - `$file` : un tableau de type `$_FILES['...']`
  - `$dirName` : sous-dossier cible (ex: `"Invoices/2026"`)
  - `$keepName` : si `true`, conserve le nom d’origine (en évitant les collisions)
  - `$customName` : nom de base forcé (sans extension), ignoré si `$keepName = true`

- **Fonctionnement**
  - Vérifie que le fichier provient bien d’un upload (`is_uploaded_file`).
  - Bloque les tentatives de *path traversal* (`..`, `\`).
  - Crée le dossier si besoin.
  - Lit le **MIME** réel du fichier (pas l’extension du nom).
  - Vérifie la **taille** (via `getUploadMaxSizeFileSize()`).
  - Si c’est une image (`image/*`), vérifie qu’elle est décodable (`getimagesize`) pour éviter les faux fichiers.
  - Génère un nom :
    - `keepName` → nom original “nettoyé” + gestion des collisions `file (1).ext`
    - `customName` → base custom “nettoyée”
    - sinon → id aléatoire
  - Déplace le fichier (`move_uploaded_file`).
  - Pour `jpg/jpeg`, supprime les métadonnées (EXIF/XMP) via `clearMetadata`.

---

### `uploadMultiple($files, $dirName): array`
Upload plusieurs fichiers en appelant `upload()` pour chacun.

- **Retour** : tableau des noms finaux (avec extensions).

---

### `uploadAsZip($file, $dirName, $keepName, $zipName): string`
Crée un **ZIP** contenant **un seul fichier** (le fichier uploadé reste dans le ZIP, pas stocké “brut” à côté).

- **Paramètres**
  - `$file` : `$_FILES['...']`
  - `$dirName` : dossier cible
  - `$keepName` : si `true`, base le nom du zip sur le nom du fichier
  - `$zipName` : nom du zip (sans extension), optionnel

- **Fonctionnement**
  - Valide le fichier (taille + MIME autorisé).
  - Construit un nom de zip unique (`.zip`) en évitant les collisions.
  - Ajoute le fichier dans le zip avec un nom “safe”.

---

### `uploadMultipleAsZip($files, $dirName, $keepName, $zipName): string`
Crée un **ZIP** contenant plusieurs fichiers uploadés.

- **Fonctionnement**
  - Crée le zip (nom unique).
  - Valide chaque fichier (taille + MIME autorisé).
  - Ajoute les fichiers en évitant les doublons à l’intérieur du zip (`file (1).ext`, etc.).

---

### `addToExistingZip($targetZipFileName, $files, $dirName, $zipSubDir): string`
Ajoute des entrées dans un ZIP existant (déjà présent dans `Public/Uploads/{dirName}/`).

- **Paramètres**
  - `$targetZipFileName` : nom du zip (`.zip`)
  - `$files` :
    - soit un `$_FILES[...]` (upload direct)
    - soit un tableau de `$_FILES[...]`
    - soit un nom de fichier déjà présent dans `Uploads`
    - soit un tableau de noms de fichiers
  - `$zipSubDir` : sous-dossier **dans** le zip (ex: `"assets/images"`)

- **Sécurité**
  - Nettoie les noms et empêche le *path traversal* dans le zip.
  - Rend chaque entrée unique si collision (ex: `a.txt`, `a (1).txt`).

---

### `deleteFromExistingZip($zipFileName, $entries, $dirName): string`
Supprime une ou plusieurs entrées d’un ZIP existant.

- `$entries` peut être :
  - `"dossier/fichier.txt"`
  - `["fichier.txt", "dossier/fichier.txt"]`

---

### `renameFile($oldFileName, $newBaseName, $dirName): string`
Renomme un fichier dans `Public/Uploads/{dirName}/` en conservant son extension et en évitant les collisions.

- Exemple : `facture.pdf` → `facture (1).pdf` si déjà pris.

---

### `deleteFile($fileName, $dirName): void`
Supprime un fichier dans `Public/Uploads/{dirName}/`.

---

### `getFileDownloadLink($fileName, $dirName): string`
Retourne un **lien** vers le fichier (`PATH_SUBFOLDER` pris en compte).

- Retourne une string d’erreur si :
  - cible invalide (`ERROR_INVALID_FILE_TARGET`)
  - fichier introuvable (`ERROR_FILE_NOT_FOUND`)

---

### `downloadFromLink($url, $dirName): string`
Télécharge un fichier distant (uniquement **https**) et le stocke dans `Public/Uploads/{dirName}/`.

- **Points importants**
  - Refuse les URLs non-HTTPS.
  - Détecte le MIME via `finfo_buffer` sur le contenu téléchargé.
  - Refuse si type non autorisé.
  - Renvoie le nom final (id aléatoire + extension).

---

## Exemples d’utilisation

### Upload simple
```php
$file = $_FILES['file'];
$fileName = FilesManager::upload($file, 'Documents', false); // nom random
```

### Upload en conservant le nom original
```php
$file = $_FILES['file'];
$fileName = FilesManager::upload($file, 'Documents', true); // évite collisions : "doc (1).pdf"
```

### Upload avec nom personnalisé
```php
$file = $_FILES['file'];
$fileName = FilesManager::upload($file, 'Invoices/2026', false, 'facture-client-123');
```

### Upload multiple
```php
$files = $_FILES['files']; // à transformer en tableau de fichiers si besoin côté controller
$names = FilesManager::uploadMultiple($files, 'Gallery');
```

### Créer un zip avec 1 fichier
```php
$file = $_FILES['file'];
$zipName = FilesManager::uploadAsZip($file, 'Zips', false, 'mon-archive');
```

### Créer un zip avec plusieurs fichiers
```php
$files = [$file1, $file2, $file3]; // tableaux type $_FILES
$zipName = FilesManager::uploadMultipleAsZip($files, 'Zips', false, 'pack-assets');
```

### Ajouter au zip existant (depuis un upload)
```php
$zip = 'pack-assets.zip';
$file = $_FILES['file'];

FilesManager::addToExistingZip($zip, $file, 'Zips', 'images');
```

### Ajouter au zip existant (depuis des fichiers déjà dans Uploads)
```php
$zip = 'pack-assets.zip';
FilesManager::addToExistingZip($zip, ['a.pdf', 'b.png'], 'Zips', 'docs');
```

### Supprimer du zip existant
```php
FilesManager::deleteFromExistingZip('pack-assets.zip', ['docs/a.pdf', 'images/logo.png'], 'Zips');
```

### Renommer un fichier
```php
$newName = FilesManager::renameFile('facture.pdf', 'facture-client-123', 'Invoices/2026');
```

### Supprimer un fichier
```php
FilesManager::deleteFile('facture-client-123.pdf', 'Invoices/2026');
```

### Générer un lien de téléchargement
```php
$link = FilesManager::getFileDownloadLink('facture-client-123.pdf', 'Invoices/2026');
// ex: /Public/Uploads/Invoices/2026/facture-client-123.pdf
```

### Télécharger depuis un lien HTTPS
```php
$name = FilesManager::downloadFromLink('https://example.com/file.pdf', 'Imports');
```

::: warning
Pense à stocker le nom du fichier en base de données si tu en as besoin (liens, historique, etc.).

Et quand tu supprimes un fichier, pense aussi à supprimer sa référence en base.
:::
