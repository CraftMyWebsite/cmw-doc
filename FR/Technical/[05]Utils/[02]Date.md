La classe `Date` permet la gestion des données temporelles

### Importer le namespace
`use CMW\Utils\Date;`

La classe `Date` du namespace `CMW\Utils` propose des méthodes statiques pour manipuler et formater des données temporelles comme la conversion de secondes en format de temps, et la récupération des mois, semaines et jours passés. Elle fait également appel à des fonctions PHP natives comme `date`, `idate`, et `strtotime`, ainsi qu'à des méthodes de traduction issues du `LangManager`.

### Méthode `formatDate()`
Cette méthode statique convertit une date donnée en un format spécifique, basé sur une option de configuration.
```php
$formattedDate = Date::formatDate('2024-06-18 12:13:38');
echo $formattedDate; // Affichera la date formatée selon le format spécifié dans l'option 'dateFormat'
```

### Méthode `secondsToTime()`

Cette méthode statique convertit un nombre donné de secondes en un format de temps lisible, avec les heures, minutes et secondes.

```php
$time = Date::secondsToTime(3600);
echo $time; // Affichera "1h 0m 0s"
```

### Méthode `getPastMonths()`

Cette méthode statique retourne une liste des noms des mois précédents, en commençant par le mois actuel et en remontant jusqu'à un nombre spécifié de mois.

```php
$months = Date::getPastMonths(6);
print_r($months); // Affichera un tableau des 6 derniers mois traduits
```

### Méthode `getPastWeeks()`

Cette méthode statique retourne les numéros des semaines précédentes, en partant de la semaine actuelle et en remontant jusqu'à un nombre donné de semaines.

```php
$weeks = Date::getPastWeeks(4);
print_r($weeks); // Affichera un tableau avec les numéros des 4 dernières semaines
```

### Méthode `getPastDays()`
Cette méthode statique retourne les dates des jours passés, en partant du jour actuel et en remontant jusqu'à un nombre spécifié de jours.

```php
$days = Date::getPastDays(7);
print_r($days); // Affichera un tableau avec les dates des 7 derniers jours
```

### Utilisation globale

La classe **Date** permet de manipuler les unités de temps de manière pratique, que ce soit pour formater des secondes, ou pour récupérer les informations temporelles relatives aux jours, semaines, et mois passés.

```php
$time = Date::secondsToTime(5400);
$months = Date::getPastMonths(3);
$weeks = Date::getPastWeeks(2);
$days = Date::getPastDays(5);

echo $time;          // "1h 30m 0s"
print_r($months);    // Liste des 3 derniers mois
print_r($weeks);     // Numéros des 2 dernières semaines
print_r($days);      // Dates des 5 derniers jours
```

--- 
Cette classe est utile pour gérer des informations temporelles dans les applications nécessitant des rapports, des récapitulatifs ou des visualisations de données passées.
