## 🧱 Structure générale

Chaque fichier `config.settings.php` retourne un tableau de `EditorMenu`, contenant chacun un ensemble de `EditorValue`.

```php
new EditorMenu(
    title: 'Accueil',
    key: 'home',
    scope: null,
    requiredPackage: null,
    values: [
        new EditorValue(...),
        // etc.
    ]
)
```

## 🎛️ Types disponibles (`EditorType`)

| Type          | Constante              | Description                        |
|---------------|------------------------|------------------------------------|
| Texte         | `TEXT`                 | Champ texte simple                 |
| Zone de texte | `TEXTAREA`             | Champ multilignes (ex: long texte) |
| Zone HTML     | `HTML`                 | Champ HTMl                         |
| Nombre        | `NUMBER`               | Champ numérique                    |
| Icon          | `FONTAWESOMEPICKER`    | Sélectionne une icon FontAwesome   |
| Booléen       | `BOOLEAN`              | Case à cocher                      |
| Couleur       | `COLOR`                | Picker de couleur                  |
| Image         | `IMAGE`                | Importer une image                 |
| CSS libre     | `CSS`                  | Code CSS direct                    |
| Liste         | `SELECT`               | Liste déroulante                   |
| Curseur       | `RANGE`                | Slider personnalisable             |

---

## 🎨 Exemples d'utilisation dans les vues

### 🔍 Remplacer un texte dynamiquement
```html
<h1 data-cmw="header:site_title"></h1>
```

### 🌈 Appliquer une couleur dynamique
```html
<span data-cmw-style="color:header:text_color"></span>
```

### 🖌️ Appliquer des classes dynamiques (ex: font, layout)
```html
<body data-cmw-class="global:main_font header:grid_layout"></body>
```

### 🚀 Gérer un attribut dynamique (ex: image)
```html
<img data-cmw-attr="src:global:site_image alt:global:image_alt">
```

### 📉 Afficher ou masquer un bloc
```html
<div data-cmw-visible="header:show_title">...</div>
```

---

## 🧪 Exemple concret

```php
new EditorValue(
    title: 'Titre de la page',
    themeKey: 'home_title',
    defaultValue: 'Bienvenue',
    type: EditorType::TEXT
),

new EditorValue(
    title: 'Image du logo',
    themeKey: 'logo',
    defaultValue: 'assets/logo.png',
    type: EditorType::IMAGE
)

new EditorValue(
    title: 'Taille du logo',
    themeKey: 'site_image_width',
    defaultValue: '40',
    type: EditorType::RANGE,
    rangeOptions: [
        new EditorRangeOptions(min: 0, max: 256,step: 1,suffix: 'px')
    ]
),

new EditorValue(
    title: 'Police d\'écriture',
    themeKey: 'main_font',
    defaultValue: 'font-montserrat',
    type: EditorType::SELECT,
    selectOptions: [
    new EditorSelectOptions(value: 'font-angkor', text: 'Angkor'),
    ...
    new EditorSelectOptions(value: 'font-silkscreen', text: 'silkscreen'),
    ]
),
```

---

## 📌 Clés obligatoires dans chaque `EditorValue`

- `title` : Nom affiché dans l’UI
- `themeKey` : Clé unique qui sera utilisée dans le HTML `data-cmw`
- `defaultValue` : Valeur initiale appliquée
- `type` : Type de champ

Certains types ont des options complémentaires :

- `SELECT` → `selectOptions: [EditorSelectOptions]`
- `RANGE` → `rangeOptions: EditorRangeOptions(min, max, step, prefix, suffix)`
