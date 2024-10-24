Les **interfaces** définissent des contrats que les classes doivent respecter. Elles sont utilisées dans le CMS pour garantir que les packages implémentent certaines méthodes et offrent des fonctionnalités spécifiques. Une interface ne contient que des signatures de méthodes, sans logique interne, et chaque package qui implémente l'interface doit définir la logique de ces méthodes.

Dans cette page, nous allons voir comment fonctionne l'interface `IRewardMethod` du package Vote, puis nous allons implémenter cette interface dans notre package Example à titre informatif.

### Interface : IRewardMethod du Package Vote
L'interface **IRewardMethod** dans le package **Vote** permet d'implémenter des méthodes de récompense supplémentaires que d'autres packages peuvent utiliser.

**Code de l'Interface IRewardMethod :**
```php
<?php

namespace CMW\Interface\Votes;

use CMW\Entity\Votes\VotesRewardsEntity;
use CMW\Entity\Votes\VotesSitesEntity;

interface IRewardMethod
{
    /**
     * @return string
     * @desc Le nom de la méthode de récompense
     * @example "Points de votes"
     */
    public function name(): string;

    /**
     * @return string
     * @desc Le nom de la variable
     */
    public function varName(): string;

    /**
     * @param ?int $rewardId
     * @return void
     * @desc Inclure les widgets de configuration pour les récompenses
     */
    public function includeRewardConfigWidgets(?int $rewardId): void;

    /**
     * @return ?string
     * @desc Action personnalisée, sinon renvoie null
     */
    public function execRewardActionLogic(): ?string;

    /**
     * @param \CMW\Entity\Votes\VotesRewardsEntity $reward
     * @param \CMW\Entity\Votes\VotesSitesEntity $site
     * @param int $userId
     * @return void
     * @desc Exécuter la logique de la récompense
     */
    public function execReward(VotesRewardsEntity $reward, VotesSitesEntity $site, int $userId): void;
}
```

**Explication :**
- **name()** : Retourne le nom de la méthode de récompense. Par exemple, pour les points de votes, cela pourrait être "Points de votes".
- **varName()** : Retourne le nom de la variable associée à la méthode de récompense, qui permet de l'identifier.
- **includeRewardConfigWidgets()** : Permet d'inclure des widgets de configuration pour paramétrer la récompense dans l'interface d'administration. 
- **execRewardActionLogic()** : Utilisée pour exécuter une logique personnalisée, si nécessaire. Sinon, elle retourne null. 
- **execReward()** : C'est la méthode principale qui exécute la logique de la récompense, en utilisant les entités VotesRewardsEntity et VotesSitesEntity, ainsi que l'ID de l'utilisateur.

### Implémentations avec l'Interface
Les contrôleurs du package Vote utilisent l'interface IRewardMethod pour charger dynamiquement les méthodes de récompense implémentées dans d'autres packages.

**Exemple de Récupération des Implémentations dans Vote :**
```php
/**
 * @return \CMW\Interface\Votes\IRewardMethod[]
 */
public function getRewardMethods(): array
{
    return Loader::loadImplementations(IRewardMethod::class);
}
```

**Explication :**
- **Loader::loadImplementations()** : Cette méthode recherche toutes les classes qui implémentent l'interface IRewardMethod dans le CMS. Cela permet au package Vote de détecter automatiquement les nouvelles méthodes de récompense ajoutées par d'autres packages.

**Utilisation d'une Méthode de Récompense par varName :**
```php
/**
 * @param string $varName
 * @return \CMW\Interface\Votes\IRewardMethod|null
 */
public function getRewardMethodByVarName(string $varName): ?IRewardMethod
{
    foreach ($this->getRewardMethods() as $rewardMethod) {
        if ($rewardMethod->varName() === $varName) {
            return $rewardMethod;
        }
    }
    return null;
}
```

**Explication :**
- Cette méthode permet de récupérer une méthode de récompense spécifique en fonction de son varName. Cela permet de gérer dynamiquement l'exécution de la récompense en fonction de l'identifiant fourni.

### Implémenter une Nouvelle Récompense dans Example
Bien que notre package Example soit conçu pour gérer des FAQ, nous allons voir comment il pourrait implémenter une nouvelle méthode de récompense pour le package Vote, à titre informatif.

Nous allons créer une implémentation de l'interface **IRewardMethod** dans le dossier `Example/Implementations/Votes/ExampleRewardImplementations.php`. Cette implémentation permettra à notre package Example de définir une nouvelle récompense utilisable dans le système de vote.

**Code de l'Implémentation :**
```php
<?php

namespace CMW\Implementation\Example\Votes;

use CMW\Entity\Votes\VotesRewardsEntity;
use CMW\Entity\Votes\VotesSitesEntity;
use CMW\Interface\Votes\IRewardMethod;
use CMW\Manager\Env\EnvManager;

class ExampleRewardImplementations implements IRewardMethod
{
    public function name(): string
    {
        return "Example";  // Le nom de la récompense
    }

    public function varName(): string
    {
        return 'Example';  // Le nom de la variable associée
    }

    public function includeRewardConfigWidgets(?int $rewardId): void
    {
        $varName = $this->varName();
        require_once EnvManager::getInstance()->getValue('DIR') . 'path/to/myconfig.config.inc.view.php';
    }

    public function execRewardActionLogic(): ?string
    {
        return null;  // Pas de logique personnalisée ici
    }

    public function execReward(VotesRewardsEntity $reward, VotesSitesEntity $site, int $userId): void
    {
        // Logique personnalisée lors de l'exécution de la récompense
        // Par exemple : ajouter des points à l'utilisateur, envoyer une notification, etc.
    }
}
```

**Explication :**
- **name()** et **varName()** : Nous définissons ici que la méthode de récompense s'appelle "Example" et que le nom de la variable associée est également "Example".
- **includeRewardConfigWidgets()** : Permet d'inclure une vue de configuration pour paramétrer la récompense. Ici, nous utilisons le gestionnaire d'environnement pour inclure un fichier de configuration personnalisé.
- **execReward()** : Cette méthode est appelée lorsque la récompense est attribuée à un utilisateur. Vous pouvez ajouter ici la logique de la récompense, comme l'ajout de points ou une autre action spécifique.

### Conclusion
Les interfaces permettent de définir des contrats entre les packages dans le CMS, garantissant que les packages qui implémentent ces interfaces respectent certaines méthodes et comportements. Dans cet exemple, nous avons vu :

- Comment fonctionne l'interface **IRewardMethod** dans le package Vote.
- Comment les contrôleurs du package Vote récupèrent les implémentations dynamiques de récompenses.
- Comment un package comme Example peut implémenter cette interface pour ajouter une nouvelle méthode de récompense.

Les interfaces sont essentielles pour rendre les packages extensibles et interopérables, permettant ainsi aux développeurs d'ajouter des fonctionnalités supplémentaires tout en respectant la modularité et les bonnes pratiques du CMS.