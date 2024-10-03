Le CMS permet de gérer plusieurs langues via un système de fichiers de traduction basés sur des tableaux PHP. Actuellement, seules les langues anglaise et française sont gérées, mais d'autres langues seront ajoutées à l'avenir.

### Structure des Fichiers de Traduction
Les fichiers de traduction sont stockés dans le dossier **Lang** de chaque package et sont nommés en fonction de la langue qu'ils contiennent, par exemple :
- `en.php` pour l'anglais.
- `fr.php` pour le français.

Ces fichiers contiennent des tableaux associatifs où les clés représentent les chaînes à traduire, et les valeurs représentent les traductions correspondantes.

**Exemple de Fichier de Traduction (fr.php) :**

```php
<?php

return [
    'example' => 'Exemple',
    'permissions' => [
        'show' => 'Consulter',
        'create' => 'Créer',
        'edit' => 'Éditer',
        'delete' => 'Supprimer',
    ],
];
```

Dans cet exemple, nous avons une traduction pour 'example' et des sous-traductions pour les permissions (consulter, créer, éditer, supprimer). Vous pouvez organiser vos fichiers de traduction selon vos besoins, en imbriquant les traductions dans des tableaux si nécessaire.

**Fichier en.php (Anglais) :**

```php
<?php

return [
    'example' => 'Example',
    'permissions' => [
        'show' => 'Show',
        'create' => 'Create',
        'edit' => 'Edit',
        'delete' => 'Delete',
    ],
];
```

### Utilisation du LangManager pour les Traductions
Le LangManager est utilisé pour parcourir et charger les traductions dans le CMS. Il permet de charger dynamiquement la langue en fonction du contexte (utilisateur, configuration du site, etc.) et de récupérer les chaînes de texte dans la langue appropriée.

**Exemple d'Utilisation du LangManager :**
```php
LangManager::translate('example.permissions.show');
```

**Explication :**
- `LangManager::translate('example.permissions.show')` : Cette méthode récupère la traduction associée à la clé '`example.permissions.show`' dans le fichier de langue actuel (fr.php pour le français ou en.php pour l'anglais).
  - '**example**' fait référence au package.
  - '**permissions.show**' fait référence à la traduction à l'intérieur de ce package.

### Ajout de Nouvelles Langues
Bien que le CMS ne gère actuellement que l'anglais et le français, d'autres langues peuvent être ajoutées à l'avenir en suivant la même structure :
- Créer un fichier de traduction pour chaque langue (par exemple `es.php` pour l'espagnol).
- Remplir ce fichier avec les mêmes clés de traduction, mais avec les traductions appropriées dans la nouvelle langue.

Le système est conçu pour être extensible et permettre l'ajout facile de nouvelles langues en fonction des besoins du projet.

### Variables Dynamiques dans les Traductions
Le LangManager permet également d'utiliser des variables dynamiques dans les traductions. Cela est utile pour insérer des valeurs personnalisées dans les chaînes de traduction, comme des noms d'utilisateur, des montants, etc.

**Exemple d'Utilisation**
```php
LangManager::translate('example.greeting', ['username' => 'John']);
```

**Ajout de la Traduction dans le Fichier :**
```php
// fr.php
return [
    'greeting' => 'Bonjour, :username !',
];
```

**Résultat :**
```php
Bonjour, John !
```

Dans cet exemple,
est remplacé par la valeur fournie dans le tableau de variables ['username' => 'John'].

### Conclusion
Le système **i18n** du CMS est conçu pour être flexible et extensible, permettant de gérer facilement plusieurs langues via des fichiers de traduction organisés en tableaux PHP. Le LangManager fournit une interface simple pour charger et utiliser ces traductions dans les packages.

Dans cette documentation, nous avons couvert :
- La structure des fichiers de traduction pour les langues actuelles (anglais et français).
- L'utilisation du LangManager pour charger et afficher des traductions.
- Comment ajouter des variables dynamiques aux traductions.
- La possibilité d'ajouter de nouvelles langues à l'avenir. 

Le **LangManager** facilite la gestion des traductions et permet de localiser les applications pour différents publics tout en maintenant une organisation claire et structurée.