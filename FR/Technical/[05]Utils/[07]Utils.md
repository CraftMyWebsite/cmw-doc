La classe `Utils` fournis des outils utilitaires divers

### Importer le namespace
`use CMW\Utils\Utils;`

La classe `Utils` dans le namespace `CMW\Utils` fournit un ensemble de méthodes statiques utilitaires pour effectuer diverses manipulations de chaînes de caractères, d'ID, et de tableaux. Elle propose des outils de validation, de génération d'identifiants, de transformation de textes, et de filtrage d'entrées.

### Méthode `isValuesEmpty()`
Cette méthode permet de vérifier si des valeurs spécifiques d'un tableau sont vides.

```php
$result = Utils::isValuesEmpty(['name' => 'John', 'age' => ''], 'name', 'age');
// Retourne true car 'age' est vide
```

### Méthode `containsNullValue()`
Cette méthode vérifie si une ou plusieurs valeurs fournies sont null.

```php
$result = Utils::containsNullValue('value1', null, 'value3');
// Retourne true car l'une des valeurs est null
```

### Méthode `normalizeForSlug()`
Cette méthode permet de normaliser une chaîne de caractères pour créer un slug URL-friendly.

```php
$slug = Utils::normalizeForSlug('Mon Titre avec Accents!');
// Retourne "mon-titre-avec-accents"
```

### Méthode `removeAccents()`

Cette méthode permet de retirer les accents d'une chaîne de caractères.
```php
$text = Utils::removeAccents("école française");
// Retourne "ecole francaise"
```

### Méthode `addIfNotNull()`
Ajoute une valeur à un tableau si cette valeur n'est pas null.

```php
$array = [];
Utils::addIfNotNull($array, 'newValue');
// Ajoute 'newValue' au tableau $array
```

### Méthode `filterInput()`
Cette méthode filtre des valeurs provenant de la méthode POST.
```php
[$name, $email] = Utils::filterInput('name', 'email');
// Retourne les valeurs POST filtrées de 'name' et 'email' et le stock en variables
```

### Méthode `genId()`
Génère un identifiant aléatoire composé de lettres et de chiffres.
```php
$id = Utils::genId(8);
// Retourne un identifiant aléatoire de 8 caractères
```

### Méthode `generateUUID()`
Génère un identifiant unique (UUID) basé sur des caractères aléatoires et l'horodatage.
```php
$uuid = Utils::generateUUID();
// Retourne un identifiant unique de style UUID
```

### Méthode `generateRandomNumber()`
Génère une chaîne composée de chiffres aléatoires.
```php
$randomNumber = Utils::generateRandomNumber(6);
// Retourne un nombre aléatoire de 6 chiffres
```

### Méthode `camelToSnakeCase()`
Convertit une chaîne en snake_case à partir du format CamelCase.
```php
$snakeCase = Utils::camelToSnakeCase('thisIsCamelCase');
// Retourne "this_is_camel_case"
```

### Méthode snakeToCamelCase()
Convertit une chaîne en CamelCase à partir du format snake_case.
```php
$camelCase = Utils::snakeToCamelCase('this_is_snake_case');
// Retourne "thisIsSnakeCase"
```

---

La classe `Utils` fournit un large éventail de méthodes pour la gestion de textes, d'identifiants et de tableaux dans les applications PHP. Elle est utile pour des opérations courantes de manipulation de chaînes et de génération d'ID.