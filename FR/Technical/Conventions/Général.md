## Conventions - Général

Afin d'avoir un code propre, lisible et éditable par tous efficacement, il y a, dans votre code, 
des conventions à suivre et à respecter scrupuleusement.

Tout code ne respectant pas les conventions présentés et expliqué ci-dessous, 
peuvent être refusés / appelé à être modifié.

Le code entier doit être rédigé en anglais, même les commentaires de vos fonctions.

Chaque élément présenté se présentera de la forme :
**ELEMENT** : ***Convention de Nommage*** + Précision si besoin.

Chaque élément présenté doit être nommé de manière explicite et compréhensible s'il sera utilisé de manière globale,
telle une fonction ou une variable importante.

**Classes**: PascalCase - Doit débuter obligatoirement par le nom du Package + sa fonction.

**Méthodes, Fonctions, Variables, Propriétés**:  camelCase - Doit inclure le type pour chacun, **si possible**, des paramètres & sa sortie.

**Constantes**: SCREAMING_SNAKE_CASE

**FICHIERS** : [Lien de la doc pour les fichier](https://reborn.craftmywebsite.fr/docs/fr/technical/Conventions/fichiers)

**i18n**: [Lien de la doc i18n](https://reborn.craftmywebsite.fr/docs/fr/technical/i18n/panel-admin)

### Exemples :

```php
class ExempleModel extends AbstraclModel {

  const string TABLE_NAME = 'exemple_table';
  public int $exempleId;
  public string $exempleColumnName;

  public function linkWithOther(int $otherId): int {
    $params = [
        'otherId' => $otherId,
        'exempleId' => $this->exempleId
    ];
    $sql = 'INSERT INTO `TABLE_NAME`(exemple_table, other_table) VALUES (:exempleId, :otherId)';
    $db = DatabaseManager::getInstance();
    $req = $db->prepare($sql);
    return ($req->execute($params)) ? $categoryId : -1;
  }

}

```

N'hésitez pas à utiliser PHPDOCS pour chaque erreur effectuée par votre IDE, s'il ne comprend pas, 
il est possible qu'un utilisateur lambda ne comprenne pas aussi. [phpdoc.org](https://www.phpdoc.org/)

Les conventions demandées sont les plus importantes proposés par PHP, 
pour plus d'informations : [php-fig.org/psr-12](https://www.php-fig.org/psr/psr-12/).