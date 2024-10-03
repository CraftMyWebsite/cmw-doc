La classe `Log` est un outil de journalisation

La classe `Log` dans le namespace `CMW\Utils` fournit des méthodes statiques pour afficher des informations de débogage dans la console du navigateur ou pour formater des données sous forme lisible. Ces méthodes sont utiles pour le débogage pendant le développement d'une application.

### Importer le namespace
`use CMW\Utils\Log;`

### Méthode `console()`
Cette méthode permet d'afficher une donnée dans la console du navigateur à l'aide de JavaScript.
```php
Log::console('Hello, world!');
// Le texte "Hello, world!" sera affiché dans la console du navigateur
```

### Méthode `debug()`
Cette méthode permet d'afficher le contenu d'une variable ou d'un tableau de manière formatée dans le navigateur.
```php
$data = ['name' => 'John', 'age' => 30];
Log::debug($data);
// Affiche le tableau de manière lisible dans le navigateur
```

--- 
La classe `Log` fournit des outils simples mais efficaces pour le débogage dans le contexte du développement de votre application. Elle permet d'afficher facilement des informations dans la console du navigateur ou dans le corps de la page web sous un format lisible.