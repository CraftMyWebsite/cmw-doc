La classe `Website` permet la gestion des informations et métadonnées du site web

### Importer le namespace
`use CMW\Utils\Website;`

La classe `Website` dans le namespace `CMW\Utils` fournit des méthodes statiques permettant de gérer les métadonnées du site web (titre, description, en-têtes personnalisés), ainsi que diverses fonctionnalités liées à l'URL du site, aux redirections et à l'affichage de contenus spécifiques comme le logo ou le favicon.

### Méthode `setTitle()`
Cette méthode permet de définir le titre de la page.
```php
Website::setTitle('Page d\'accueil');
```

### Méthode `getTitle()`
Cette méthode permet d'obtenir le titre de la page, avec la possibilité d'inclure le nom du site.
```php
$title = Website::getTitle();
// Retourne "Nom du site | Page d'accueil"
```

### Méthode `setDescription()`
Cette méthode permet de définir la description de la page.
```php
Website::setDescription('Description de la page d\'accueil');
```

### Méthode `getDescription()`

Cette méthode permet d'obtenir la description de la page.
```php
$description = Website::getDescription();
```

### Méthode `setCustomHeader()`
Cette méthode permet de définir un en-tête personnalisé pour la page.
```php
Website::setCustomHeader('<meta name="author" content="CraftMyWebsite">');
```

### Méthode `getCustomHeader()`
Cette méthode permet d'obtenir l'en-tête personnalisé défini pour la page.
```php
$customHeader = Website::getCustomHeader();
```

### Méthode `getProtocol()`
Cette méthode permet d'obtenir le protocole utilisé par le site (HTTP ou HTTPS).
```php
$protocol = Website::getProtocol();
```

### Méthode `getUrl()`
Cette méthode permet d'obtenir l'URL complète du site, y compris le protocole et le sous-dossier si défini.
```php
$url = Website::getUrl();
```

### Méthode `refresh()`
Cette méthode permet d'actualiser la page actuelle.
```php
Website::refresh();
```

### Méthode `isCurrentPage()`
Cette méthode permet de vérifier si une URL correspond à la page actuelle (utile pour les barres de navigation actives).
```php
$isActive = Website::isCurrentPage('/contact');
```

### Méthode `isContainingRoute()`

Cette méthode vérifie si l'URL actuelle contient une route spécifique.
```php
$isInRoute = Website::isContainingRoute('admin');
```

### Méthode `getWebsiteName()`
Cette méthode permet de récupérer le nom du site web.
```php
$websiteName = Website::getWebsiteName();
```

### Méthode `getWebsiteDescription()`
Cette méthode permet de récupérer la description du site web.
```php
$websiteDescription = Website::getWebsiteDescription();
```

### Méthode `getLogoPath()`
Cette méthode permet de récupérer le chemin du logo du site.
```php
$logoPath = Website::getLogoPath();
```

### Méthode `getFavicon()`
Cette méthode permet de récupérer le chemin du favicon du site.
```php
$favicon = Website::getFavicon();
```

---
La classe `Website` fournit un ensemble de méthodes pratiques pour gérer les informations dynamiques du site web, comme le titre, la description, et les en-têtes personnalisés, ainsi que pour gérer des actions liées à l'URL et à l'affichage des métadonnées du site.