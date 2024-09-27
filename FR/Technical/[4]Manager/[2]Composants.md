### Explication
Dans le système de gestion de composants, il existe deux options :

- **Utiliser les composants fournis par le CMS** : Le CMS propose une série de composants préconstruits que vous pouvez utiliser dans vos views. Ces composants sont déjà intégrés et prêts à être utilisés sans avoir besoin de modifications.

- **Créer vos propres composants dans votre thème** : Si vous souhaitez personnaliser ou ajouter des fonctionnalités spécifiques, vous pouvez créer vos propres composants au sein de votre thème. Le fichier ComponentsManager est conçu pour charger automatiquement les composants que vous avez créés dans le dossier Components de votre thème. Il suffit de définir vos composants dans ce répertoire, et le système les détectera et les utilisera.

Cela vous permet de combiner les composants natifs du CMS et vos propres créations pour une flexibilité maximale dans la personnalisation, le but de ce manager est de vous faire gagner du temps dans la création de vos thèmes, mais ne sont pas obligatoire.

### Exemple d'un composant natif :
Voyons comment ajouter un bouton :
#### 1- Importer le namespace :
`use CMW\Manager\Components\Base\ButtonComponentBase;`
#### 2- Créer le bouton :
```php
ButtonComponentBase::create()
    ->setText("Button text")
    ->setClasses("Add Custom Classes")
    ->setType("submit")
    ->render();
```

### Liste de composant natif existant :

Nous vous recommandons d'examiner le code de chaque composant afin de découvrir les méthodes, propriétés et fonctionnalités spécifiques qu'il offre. Cela vous donnera une vision complète des possibilités et vous aidera à les intégrer de manière optimale.

Pour faciliter cette exploration et l'intégration des composants, nous vous conseillons d'utiliser un IDE tel que **PHPStorm**. Cet outil est capable de générer automatiquement les besoins des composants (comme les propriétés et méthodes à implémenter) et fournit l'autocomplétion, rendant ainsi le processus de développement plus fluide et efficace. Cela vous permettra de gagner du temps tout en facilitant la compréhension du code et l'intégration des composants dans vos projets.

::: warning
N'oubliez pas d'importer les Namespaces de chaque composant que vous utilisez
:::

- a :
`AComponentBase::create()->render();`
- button :
`ButtonComponentBase::create()->render();`
- div :
`DivComponentBase::create()->render();`
- form :
`FormComponentBase::create()->render();`
- Header :
`HeaderComponentBase::create()->render();`
- Heading :
`HeadingComponentBase::create()->render();`
- hr :
`HrComponentBase::create()->render();`
- input :
`InputComponentBase::create()->render();`
- label :
`LabelComponentBase::create()->render();`

### Créer vos composants personnalisés :
Dans cet exemple, nous allons créer un compostant image, lui appliquer une classe et une taille limite par défaut qui sera modifiable, la source de l'image ainsi qu'un alt.

Sans ce cas le thème s'appel **Craftmywebsite**

- Dans votre thème créer un dossier ***Components*** (Themes/Craftmywebsite/Components)
- Dans ce dossier créer un nouveau composant **ImgComponent.php**
#### Création de la classe ImgComponent.php
```php
<?php

use CMW\Manager\Components\IComponent;

/**
 * Classe ImgComponent représentant un composant HTML d'image.
 * Hérite de IComponent, ce qui permet d'utiliser des méthodes et propriétés partagées avec d'autres composants.
 */
class ImgComponent extends IComponent
{
    // Propriétés privées de la classe définissant les attributs de l'image
    private string $src = ""; // Chemin de la source de l'image
    private string $alt = ""; // Texte alternatif de l'image
    private string $width = "200px"; // Largeur de l'image par défaut, ici définie à 200px

    /**
     * Définit l'attribut source de l'image.
     * 
     * @param string $src Chemin vers l'image
     * @return ImgComponent Retourne l'instance courante pour permettre l'appel fluide (chaining).
     */
    public function setSrc(string $src): ImgComponent
    {
        $this->src = $src; // Affecte la valeur $src à la propriété src
        return $this; // Retourne l'objet pour permettre un chaînage de méthodes
    }

    /**
     * Définit l'attribut alt (texte alternatif) de l'image.
     * 
     * @param string $alt Texte alternatif pour l'image (utile pour l'accessibilité)
     * @return ImgComponent Retourne l'instance courante pour permettre l'appel fluide (chaining).
     */
    public function setAlt(string $alt): ImgComponent
    {
        $this->alt = $alt; // Affecte la valeur $alt à la propriété alt
        return $this; // Retourne l'objet pour permettre un chaînage de méthodes
    }

    /**
     * Définit l'attribut width (largeur) de l'image.
     * 
     * @param string $width Largeur de l'image en px ou autre unité CSS
     * @return ImgComponent Retourne l'instance courante pour permettre l'appel fluide (chaining).
     */
    public function setWidth(string $width): ImgComponent
    {
        $this->width = $width; // Affecte la valeur $width à la propriété width
        return $this; // Retourne l'objet pour permettre un chaînage de méthodes
    }

    /**
     * Méthode pour afficher l'élément HTML de l'image.
     * Cette méthode surcharge la méthode render() de la classe parente IComponent.
     */
    #[\Override] public function render(): void
    {
        // Génère l'élément <img> avec les attributs définis (id, src, width, alt, classes)
        print "<img {$this->showId()} src='{$this->src}' width='{$this->width}' alt='{$this->alt}' class='{$this->classes} my-default-classes'>";
    }
}
```
#### Utilisation du composant dans les Views
Dans notre exemple nous avons créer appliqué une classe qui sera TOUJOURS présente `my-default-classes`
Nous pouvons appliqué des propriété CSS à cette classe :
```css
.my-default-classes {
    border: solid 5px black;
    border-radius: 0.9rem;
}
```
Utiliser ce compostant dans votre Views :
Dans notre cas je me place dans /Themes/Craftmywebsite/Views/Core/home.view.php et j'appel mon composant :
```php
<?php ImgComponent::create()
    ->setSrc("https://reborn.craftmywebsite.fr/Public/Themes/Craftmywebsite/Config/Default/whitemarket.png")
    ->setAlt("Test")
    ->render()
?>
```
Celui-ci va créer une image sans modifier la largeur définie par défaut à 200px.