### Explication
**FilterManager** contient plusieurs méthodes pour filtrer et sécuriser les données d'entrée utilisateur. Voici un aperçu et une explication des différentes méthodes :

### Importer le namespace
`use CMW\Manager\Filter\FilterManager;`

### Utilisation des fonctions globales
1. `filterUrl(string $url): string`
   - **Description**: Cette méthode prend une URL en paramètre et filtre son contenu en supprimant les parties correspondant à un schéma d'URL (protocole, domaine, etc.).
   - **Explication**: Utilise une expression régulière pour supprimer toute chaîne de type URL.
2. `filterData(string $data, int $maxLength = 128, int $filter = FILTER_UNSAFE_RAW): string`
   - **Description**: Filtre une chaîne de caractères, retire les balises PHP, limite la longueur de la chaîne et applique un filtre spécifique.
   - **Explication**: 
     - Supprime les éventuels scripts PHP présents dans la chaîne via `preg_replace`.
     - Tronque la chaîne à une longueur maximale via `mb_substr`.
     - Applique un filtre via `filter_var`, en utilisant par défaut `FILTER_UNSAFE_RAW` qui ne modifie pas la chaîne.
3. `filterMultiplesData(int $maxLength = 128, string ...$values): array`
   - **Description**: Filtre plusieurs chaînes de caractères en appliquant la méthode `filterData` à chaque chaîne.
   - **Explication**: Utilise un argument variadique (`...$values`) pour accepter plusieurs chaînes à filtrer et les traite individuellement.
4. `filterInputStringPost(string $data, ?int $maxLength = 255, mixed $orElse = false): mixed`
   - **Description**: Filtre une donnée provenant d'une requête POST. Permet de définir une valeur par défaut si la donnée n'existe pas ou est nulle.
   - **Explication**:
     - Vérifie d'abord si la donnée existe dans `$_POST` et n'est pas `null`.
     - Filtre et tronque la donnée POST à une longueur définie, si applicable.
5. `filterInputIntPost(string $data, int $maxLength = 128): int`
   - **Description**: Filtre une entrée POST en tant qu'entier, après avoir appliqué un filtre pour les nombres.
   - **Explication**: Utilise `FILTER_SANITIZE_NUMBER_INT` pour ne garder que les chiffres et retourne le résultat comme un entier.
6. `filterInputStringGet(string $data, int $maxLength = 128): string`
   - **Description**: Filtre une donnée provenant d'une requête GET en tant que chaîne de caractères.
   - **Explication**: Semblable à `filterInputStringPost`, mais pour les requêtes GET.
7. `filterInputIntGet(string $data, int $maxLength = 128): int`
   - **Description**: Filtre une donnée provenant d'une requête GET en tant qu'entier.
   - **Explication**: Similaire à `filterInputIntPost`, mais pour les requêtes GET.
8. `isEmail(string $mail): bool`
   - **Description**: Vérifie si une chaîne de caractères est une adresse email valide.
   - **Explication**: Utilise `filter_var` avec `FILTER_VALIDATE_EMAIL` pour valider l'email.
9. `prepareSqlInsert(string $data): string`
   - **Description**: Prépare une chaîne pour une insertion SQL, en particulier pour les apostrophes et les entités HTML.
   - **Explication**: Utilise `html_entity_decode` pour décoder les entités HTML et s'assure que les apostrophes sont correctement gérées avec `ENT_QUOTES`.
   

### Résumé
Cette classe est conçue pour sécuriser les données utilisateur et les filtrer avant toute utilisation, comme lors d'une insertion SQL ou d'une validation de formulaire. Elle implémente différentes méthodes pour traiter des types de données spécifiques (chaînes de caractères, entiers, emails) et peut être facilement adaptée pour s'assurer que les données manipulées dans une application sont sûres et valides.