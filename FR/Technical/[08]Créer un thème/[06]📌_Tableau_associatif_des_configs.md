### Important
Le tableau associatif vous permet de savoir facilement quel `EditorType` est associé à quel `data-cmw`.

Cette documentation vous fait gagner un temps précieux et vous évite bien des réflexions lorsque vous n’avez pas encore l’habitude d’utiliser le configurateur.

Vous l'aurez compris mais je vous le rappel, les `data-cmw` doivent impérativement contenir la `key` de votre `EditorMenu` suivie de la `themeKey` de votre `EditorValue` associé à ce menu, et lors de l'appel, il faut les séparer par `:`

Dans notre exemple `X` sera `key` de `EditorMenu` et `Y` sera `themeKey` de `EditorValue`

Pour rappel voici une structure basique de votre config avec `X` et `Y` :

```php
new EditorMenu(
        title: 'Menu X',
        key: 'X',
        scope: null,
        requiredPackage: null,
        values: [
            new EditorValue(
                title: 'Texte Y',
                themeKey: 'Y',
                defaultValue: '0',
                type: EditorType::TEXT,
            ),
        ]
    ),
```

::: info
**À SAVOIR !**

Si vous avez besoin d'appeler une configuration dans du code PHP, vous pouvez le faire comme ceci :
```php
ThemeModel::getInstance()->fetchConfigValue('X','Y')
```
Cependant, elle ne sera pas reconnue par le live builder de ce fait, elle ne se mettra pas à jour en live.
:::

---

## `data-cmw="X:Y"`
Permet d'appliquer du texte / contenue HTML dans des elements.

Il s'applique avec les `EditorType` :
- `TEXT`
- `TEXTAREA`
- `HTML`
- `NUMBER`
- `SELECT`

Exemple : 
```html
<!--TOUT EditorType listé précédemment-->
<p data-cmw="X:Y"></p>
```
```html
<!--TOUT EditorType listé précédemment-->
<div data-cmw="X:Y"></div>
```
```html
<!--TOUT EditorType listé précédemment-->
<span data-cmw="X:Y"></span>
```
Ceci est applicable sur n'importe quel type de balise.

---

## `data-cmw-attr="X:Y"`
Permet de manipuler des attributs HTML

Pour rappel : Un attribut HTML est une information ajoutée à une balise pour définir son comportement, son apparence ou ses données.

Pour appliquer un attribut lors de l'appel, vous devez spécifier quel type d'attribut, vous ciblez (`style`, `src`, `alt`, `href` ...)

Pour appliquer plusieurs attributs ajouter simplement un `ESPACE`

Il s'applique avec les `EditorType` :
- `TEXT`
- `IMAGE`
- `SELECT`
- `CSS` (Vous pouvez l’utiliser, mais évitez dans ce cas précis. Préférez `data-cmw-style`, plus fiable, modulable et moins cassant pour les utilisateurs finaux.)

Exemple :
```html
<!-- TEXT - CSS - SELECT EditorType listé précédemment-->
<p data-cmw-attr="style:X:Y"></p>
```
```html
<!-- IMAGE - TEXT - CSS - SELECT EditorType listé précédemment-->
<img data-cmw-attr="src:X:Y alt:X:Y">
```
```html
<!-- TEXT - SELECT EditorType listé précédemment-->
<a data-cmw-attr="href:X:Y"></a>
```
Ceci est applicable sur n'importe quel type de balise.

---

## `data-cmw-style="X:Y"`
Permet d'appliquer un ou plusieurs styles CSS prédéfinie (non cassable, fiable)

Pour appliquer un style lors de l'appel, vous devez spécifier quel type de style, vous ciblez (`color`, `background`, `font-size`, `width` ...)

Pour appliquer plusieurs styles ajouter simplement un `;`

Tips : Le style `background` gère de manière complétement autonome les **couleurs** ou **liens d'images** (voir exemple 1)

Garder à l'esprit que les style ne sont pas responsive, attention aux valeurs en `px`...

Il s'applique avec les `EditorType` :
- `TEXT`
- `COLOR`
- `IMAGE`
- `SELECT`
- `RANGE`

Exemple :
```html
<!--IMAGE - COLOR - SELECT - RANGE EditorType listé précédemment-->
<div data-cmw-style="background:X:Y" style="background: no-repeat ;background-size: cover;"></div>
```
```html
<!--TOUT EditorType listé précédemment-->
<p data-cmw-style="color:X:Y;font-size:X:Y"></p>
```

Ceci est applicable sur n'importe quel type de balise.

---

## `data-cmw-class="X:Y"`
Permet d'appliquer une ou plusieurs classes

Pour appliquer plusieurs classes ajouter simplement un `ESPACE`

Il s'applique avec les `EditorType` :
- `TEXT`
- `TEXTAREA`
- `FONTAWESOMEPICKER`
- `SELECT`
- `RANGE`

Exemple :
```html
<!-- FONTAWESOMEPICKER EditorType listé précédemment-->
<i data-cmw-class="X:Y" class="text-7xl"></i>
```
```html
<!--TOUT EditorType listé précédemment-->
<p data-cmw-class="X:Y X:Y X:Y"></p>
```

Ceci est applicable sur n'importe quel type de balise.

---

## `data-cmw-visible="X:Y"`
Affiche/masque l'élément selon une valeur booléenne

Peut-être encapsuler ou non (voir exemple).

Il s'applique avec les `EditorType` :
- `BOOLEAN`

Exemple :
```html
<p data-cmw-visible="X:Y"></p>
```
```html
<div data-cmw-visible="X:Y">
    <p>Élément 1</p>
    <p>Élément 2</p>
    <p>Élément 3</p>
</div>
```

Ceci est applicable sur n'importe quel type de balise.

---

::: info
**TIPS**

Il est possible de combiner autant de data-... que vous voulez par exemple ceci fonctionne : 

```html
<a data-cmw-visible="X:Y" data-cmw-style="color:X:Y" data-cmw-class="X:Y" data-cmw-attr="href:X:Y" data-cmw="X:Y"></a>
```

Ici, nous avons appliqué à notre balise, la possibilité de le masquer ou de l'afficher, un style de couleur, une classe, un attribut href, et un texte, le tout personnalisable.

Par contre n'appliquez JAMAIS plusieurs fois à la même config : `data-cmw-style="color:X:Y"` et `data-cmw-style="background:X:Y"` ne fonctionnerais pas.
:::