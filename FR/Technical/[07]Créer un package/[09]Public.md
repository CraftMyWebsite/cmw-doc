Les views publiques permettent de gérer un **fallback** dans le cas où un thème ne prend pas en charge les views personnalisées déclarées dans les controllers du package. Ce mécanisme garantit que le package fonctionne correctement, même si le thème en place ne dispose pas de ses propres templates pour les fonctionnalités spécifiques du package.

### Objectifs des Views Publiques :
- **Fallback sécurisé** : Si un thème ne propose pas de views spécifiques, les views publiques s'affichent par défaut, évitant ainsi des erreurs ou un affichage incomplet.
- **Simplicité** : Ces views sont minimalistes, sans CSS externe. Elles peuvent contenir des styles directement dans les balises HTML pour une mise en forme de base.
- **Exemple pour les développeurs de thèmes** : Elles servent de référence pour créer des views personnalisées dans les thèmes tout en restant fonctionnelles et compréhensibles.

### Dans notre exemple
Nous allons créer dans le dossier **Public** du package une vue **main.view.php** 

```html
<?php

use CMW\Utils\Website;

/* @var \CMW\Entity\Example\ExampleEntity[] $examples */

/* TITRE ET DESCRIPTION */
Website::setTitle('Example');
Website::setDescription('Des questions et réponses');
?>

<?php foreach ($examples as $example): ?>
<h5><?= $example->getQuestion() ?></h5>
<p><?= $example->getResponse() ?></p>
<?php endforeach; ?>
```

### Conclusion
Les views publiques assurent un comportement par défaut du package tout en offrant aux développeurs de thèmes une base pour intégrer leurs propres templates.