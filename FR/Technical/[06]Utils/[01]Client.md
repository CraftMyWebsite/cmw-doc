La classe `Client` permet la récupération des informations du client

### Importer le namespace
`use CMW\Utils\Client;`

La classe `Client` fait partie du namespace `CMW\Utils` et propose des méthodes statiques pour récupérer des informations relatives au client HTTP, telles que son adresse IP et son user-agent. Elle utilise les fonctions PHP natives telles que `filter_var` et `preg_match` pour valider les données.

### Méthode `getIp()`

Cette méthode statique permet de récupérer l'adresse IP du client.

```php
$ip = Client::getIp();
echo $ip; // Affichera l'IP du client, ou "0.0.0.0" si non valide`
```

### Méthode `getUserAgent()`

Cette méthode statique permet de récupérer le user-agent du client.

```php
$userAgent = Client::getUserAgent();
echo $userAgent; // Affichera le user-agent ou "INVALID" s'il est incorrect
```

### Utilisation générale

La classe Client est utile pour les développeurs souhaitant obtenir des informations précises et valides sur les utilisateurs d'une application, en traitant et validant automatiquement les données du client HTTP.

### Exemple d'utilisation globale :

```php
$ip = Client::getIp();
$userAgent = Client::getUserAgent();

echo "Client IP: " . $ip;
echo "User Agent: " . $userAgent;
```