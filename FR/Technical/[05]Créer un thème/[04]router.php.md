Les routes permettent de définir des chemins spécifiques pour accéder à des pages ou à des fonctionnalités de votre site. Dans le cadre de ce CMS, il est possible de créer des routes personnalisées afin d'accéder à des pages spécifiques via des URL dédiées. Cela permet de structurer et d'organiser les différentes sections de votre site selon vos besoins.

### Créer une Route Personnalisée

Pour créer une route, vous pouvez utiliser la méthode suivante :
```php
Loader::createSimpleRoute('/hello', 'hello', 'Core');
```

**Explication de la syntaxe :**
- `'/hello'` : C'est le chemin ou l'URL que vous souhaitez associer à votre route. Dans cet exemple, la route sera accessible via `https://votresite.fr/hello`.
- `'hello'` : Il s'agit du nom du fichier de la vue que le CMS va charger. Le système va rechercher un fichier nommé `hello.view.php` dans le dossier spécifié `Core`.
- `'Core'` : Ce dernier paramètre indique dans quel package le CMS va chercher le fichier de vue. Dans cet exemple, il va chercher le fichier hello.view.php dans le dossier Views/Core.

### Fonctionnement
Lorsque l'utilisateur accède à l'URL https://votresite.fr/hello, le CMS cherche dans le dossier Views/Core un fichier nommé hello.view.php et le charge pour affichage. Cela vous permet de créer une page personnalisée accessible via une route que vous définissez.

### Un choix facultatif pour les thèmes grand public
Il est important de noter que l'utilisation de routes personnalisées est facultative et peut même être inutile lors de la création d'un thème destiné à un large public. En effet, le package Pages permet aux utilisateurs finaux de créer eux-mêmes leurs routes directement depuis l'interface d'administration du CMS, sans avoir besoin d'accéder ou de modifier le code.

Cela signifie que pour la majorité des thèmes destinés à un usage public, il n'est généralement pas nécessaire d'intégrer des routes spécifiques. Les utilisateurs auront toute la flexibilité pour créer leurs propres pages et définir les URL associées via l'interface du CMS, ce qui simplifie considérablement l'expérience utilisateur.

### Conclusion
Les routes personnalisées vous offrent la possibilité de définir des chemins spécifiques pour votre thème, mais dans le cadre d'un thème grand public, cette fonctionnalité est souvent redondante avec ce que permet déjà le package Pages. Réservez l'utilisation des routes personnalisées pour des cas spécifiques ou des projets nécessitant une structure de navigation particulière.