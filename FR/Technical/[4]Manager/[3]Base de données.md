### Explication
**DatabaseManager** gère la connexion à la base de données via PDO. Le but est de centraliser la gestion des connexions pour différents SGBD (Systèmes de Gestion de Base de Données).

::: warning
Ce manager doit uniquement être appelé dans les Models de vos packages

S'il est appelé ailleurs ceci peut être un motif de refus de votre package sur le [Market de CraftMyWebsite](https://dev.craftmywebsite.fr/market)
:::

#### Conventions d'utilisation
Voici une norme à respecter pour créer les fonctions de vos models

- Stocker l'instance du manager dans une variable : `$db = DatabaseManager::getInstance();`
- Utilisez à présent cette variable `$db` dans votre fonction

Ceci permet d'appeler l'instance une seul fois par fonction et rend votre code plus efficace et performant.

#### Exemple d'un cas simple :
```php
/**
 * Récupère la valeur d'une option dans la table `cmw_core_options` en fonction de son nom.
 *
 * @param string $option Le nom de l'option à récupérer.
 * @return string La valeur de l'option demandée.
 */
public function fetchOption(string $option): string
{
    // Obtient une instance de la base de données via DatabaseManager.
    $db = DatabaseManager::getInstance();

    // Prépare une requête SQL pour récupérer la valeur de l'option en fonction de son nom.
    $req = $db->prepare('SELECT option_value FROM cmw_core_options WHERE option_name = ?');

    // Exécute la requête en passant le nom de l'option en paramètre.
    $req->execute([$option]);

    // Récupère le résultat sous forme de tableau associatif.
    $option = $req->fetch();

    // Retourne la valeur de l'option (colonne 'option_value').
    return $option['option_value'];
}
```

#### Models
Pour en apprendre plus sur les models rendre vous dans la [section Models](https://dev.craftmywebsite.fr/docs/fr/technical/core/models)