Gérer les packages compatibles, mais optionnel.

L'intégration de packages compatibles mais non obligatoires permet d'offrir des fonctionnalités supplémentaires aux utilisateurs, à condition que ces packages soient installés. Cependant, il est important de noter que la vérification manuelle de l'installation d'un package via la méthode :
```php
<?php if (PackageController::isInstalled('Contact')): ?>
    <!-- Code spécifique au package Contact -->
<?php endif; ?>
```
n'est **nécessaire que dans certains cas précis**. En effet, cette vérification est utile uniquement lorsque vous utilisez un package optionnel dans des vues qui ne sont **pas spécifiquement dédiées à ce package**.

### Cas où la vérification est nécessaire
La vérification est nécessaire **lorsque vous souhaitez intégrer du code lié à un package optionnel dans des vues génériques de votre thème**. Par exemple, si vous avez une vue globale comme un fichier `home.view.php`, `header.inc.php` ... ou une page personnalisée dans laquelle vous souhaitez inclure des éléments du package Shop, mais uniquement si ce package est installé, vous devez faire cette vérification.

Exemple d'intégration dans votre menu de navigation `header.inc.php` du lien menant vers le panier du package Shop :
```php
<?php if (PackageController::isInstalled('Shop')): ?>
    <a href="<?= Website::getProtocol() ?>://<?= $_SERVER['SERVER_NAME'] ?><?= EnvManager::getInstance()->getValue('PATH_SUBFOLDER') ?>shop/cart">
        <i class="text-lg fa-solid fa-cart-shopping"></i>
    </a>
<?php endif; ?>
```
Dans ce cas, vous affichez dans votre menu le lien vers le panier seulement si le package **Shop** est installé.

### Cas où la vérification n'est pas nécessaire

Si vous utilisez des **vues dédiées à un package**, la vérification manuelle de l'installation du package **n'est pas nécessaire**, car le CMS gère cela automatiquement. Lorsqu'un package est installé, il crée ses propres vues dans le dossier correspondant (par exemple, Views/Contact), et le CMS ne tentera d'accéder à ces vues que si le package est installé. Il n'est donc pas nécessaire d'ajouter une vérification supplémentaire dans ces fichiers.

Exemple de fonctionnement sans vérification :
- Si vous avez une vue spécifique à **Contact**, située dans **Views/Contact/main.view.php**, cette vue sera automatiquement chargée uniquement si le package Contact est installé.
- Si le package Contact n'est pas installé, le CMS n'essaiera pas de charger les vues qui y sont liées, donc aucune erreur ne sera générée.

### Conclusion
La vérification via `PackageController::isInstalled()` est utile uniquement lorsque vous souhaitez intégrer du code lié à un package optionnel dans des vues qui ne lui sont pas directement dédiées, comme dans un fichier global de votre thème. Cependant, si vous travaillez avec des vues spécifiques à un package, le CMS s'en occupe automatiquement et vous n'avez pas besoin de faire cette vérification. Cela simplifie l'intégration des packages tout en assurant une gestion propre et sans erreurs lorsque ces packages ne sont pas présents.