La classe `Redirect` permet la gestion des redirections

La classe Redirect dans le namespace CMW\Utils fournit des méthodes statiques pour gérer les redirections HTTP dans une application web. Elle intègre des fonctionnalités pour rediriger vers des pages internes, des routes spécifiques, des pages d'administration et des pages d'erreur.

### Importer le namespace
`use CMW\Utils\Redirect;`

### Méthode `redirect()`
Cette méthode redirige vers une URL ou une route spécifique.
```php
Redirect::redirect('dashboard', ['user', '123']);
// Redirige vers la route "dashboard" avec les paramètres "user" et "123"
```

### Méthode `forceInternalRedirect()`
Cette méthode force une redirection interne vers une URL spécifique.
```php
Redirect::forceInternalRedirect('login', ['error', 'invalid']);
// Redirige vers "/login/error/invalid"
```

### Méthode `redirectToAdmin()`
Redirige vers une page d'administration après vérification que l'utilisateur est connecté en tant qu'administrateur.

```php
Redirect::redirectToAdmin('dashboard');
// Redirige vers la page "cmw-admin/dashboard" si l'utilisateur est administrateur
```

### Méthode `errorPage()`
Redirige vers une page d'erreur spécifique.
```php
Redirect::errorPage(404);
// Redirige vers la page d'erreur 404
```

### Méthode `redirectToHome()`
Redirige vers la page d'accueil du site.
```php
Redirect::redirectToHome();
```

### Méthode `emulateRoute()`
Simule l'appel d'une route spécifique sans redirection réelle.
```php
Redirect::emulateRoute('dashboard');
// Simule l'appel de la route "dashboard"
```

### Méthode `redirectPreviousRoute()`
Redirige l'utilisateur vers la page précédente.
```php
Redirect::redirectPreviousRoute();
```

---

La classe `Redirect` est un outil puissant pour gérer les redirections dans une application web. Elle permet de rediriger les utilisateurs vers des pages spécifiques, de gérer les routes internes et externes, ainsi que de simuler des routes ou rediriger vers des pages d'erreur ou d'administration.