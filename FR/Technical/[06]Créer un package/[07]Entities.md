Les **entities** dans le CMS sont des objets qui représentent les retours de requêtes SQL sous forme d'entités reconnues par le CMS. Elles permettent de structurer les données et de les manipuler facilement dans votre application. Les entities ne se limitent pas aux résultats SQL : elles peuvent être utilisées pour représenter toute sorte d'objets métiers selon les besoins.

Dans le cadre du package Example, nous allons créer une entité capable de gérer les informations issues de la table `cmw_example`. Nous verrons plus tard comment le model interagit avec cette entité pour remplir ses données.

### L'Entity : ExampleEntity
```php
<?php

namespace CMW\Entity\Example;

use CMW\Entity\Users\UserEntity;

class ExampleEntity
{
    private int $exampleId;
    private string $question;
    private string $response;
    private UserEntity $author;

    /**
     * @param int $exampleId
     * @param string $question
     * @param string $response
     * @param \CMW\Entity\Users\UserEntity $author
     */
    public function __construct(int $exampleId, string $question, string $response, UserEntity $author)
    {
        $this->exampleId = $exampleId;
        $this->question = $question;
        $this->response = $response;
        $this->author = $author;
    }

    public function getId(): int
    {
        return $this->exampleId;
    }

    public function getQuestion(): string
    {
        return $this->question;
    }

    public function getResponse(): string
    {
        return $this->response;
    }

    public function getAuthor(): UserEntity
    {
        return $this->author;
    }
}
```

### Explication du Code

- **Namespace** : Le fichier **ExampleEntity.php** se trouve dans le répertoire **/App/Package/Example/Entities**, et le namespace correspondant est donc `CMW\Entity\Example`.
- **Propriétés** :
  - **exampleId** : Identifiant unique de l'exemple, correspondant au champ example_id dans la base de données.
  - **question** : Représente la question de la FAQ, issue de la colonne example_question dans la table cmw_example.
  - **response** : La réponse correspondante, stockée dans example_response.
  - **author** : L'instance de l'UserEntity qui représente l'auteur de la question. Cette entité est utilisée pour récupérer les informations de l'utilisateur associé (via la clé étrangère example_user_id).
- **Méthodes** :
  - **getId()** : Retourne l'identifiant unique de l'exemple.
  - **getQuestion()** : Retourne la question.
  - **getResponse()** : Retourne la réponse.
  - **getAuthor()** : Retourne l'objet UserEntity, représentant l'utilisateur ayant posé la question.

**Utilisation d'une Entité Externe (UserEntity)**
Dans cet exemple, nous utilisons une entité d'un autre package natif du Core, à savoir UserEntity. Cette entité est responsable de la gestion des utilisateurs dans le CMS et nous permet de récupérer les informations de l'auteur de la question.

::: danger
Il est fortement déconseillé d'utiliser des entities provenant de packages non **natifs du Core**. L'utilisation d'entités d'un package non installé par l'utilisateur peut entraîner des erreurs critiques si le package requis n'est pas disponible sur l'instance du CMS. Il est donc conseillé de se limiter à l'utilisation d'entités des packages natifs pour éviter ces problèmes.
:::

### Conclusion 
Cette page explique la création et l'utilisation des entities dans votre package Example. Elles permettent de structurer les données de votre table cmw_example tout en respectant les bonnes pratiques d'organisation et d'intégration avec le CMS.