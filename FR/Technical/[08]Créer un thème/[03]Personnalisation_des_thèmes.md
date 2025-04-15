Ce guide explique comment fonctionne le système de configuration des thèmes à travers l'éditeur visuel (Theme Editor). Vous pourrez personnaliser dynamiquement vos thèmes sans toucher au code, simplement en remplissant une structure claire et évolutive.

---

## 📁 Structure globale

La personnalisation s'appuie sur un fichier PHP contenant des objets `EditorMenu` et `EditorValue`. Chaque menu correspond à un onglet dans l'éditeur, contenant une ou plusieurs options configurables.

```php
use CMW\Manager\Theme\Editor\Entities\EditorMenu;
use CMW\Manager\Theme\Editor\Entities\EditorValue;
use CMW\Manager\Theme\Editor\Entities\EditorType;

return [
    new EditorMenu(...),
    new EditorMenu(...),
    // etc.
];
```

Chaque `EditorMenu` est affiché comme un onglet. Il contient une clé unique (`key`) et une liste de `EditorValue`, chacune représentant une option modifiable.

---

## 🛠 Configuration dynamique

Les données sont liées automatiquement à vos vues grâce à des attributs HTML `data-cmw`, facilitant une intégration propre et dynamique.

**Exemples :**

```html
<h1 data-cmw="header:title"></h1>
<img data-cmw-attr="src:global:logo alt:global:logo_alt">
<div data-cmw-style="background-color:global:main_color"></div>
```

Ces données sont injectées automatiquement dans les pages publiques, et modifiables en live dans le builder.

---

## 🚦 Bonnes pratiques

- Garder des clés (`themeKey`) uniques dans chaque menu
- Toujours définir une `defaultValue` cohérente
- Utiliser des types précis (ex: `TEXT`, `COLOR`, `BOOLEAN`...)
- Organiser les menus par logique fonctionnelle (Header, Footer, Accueil...)
- Favoriser les noms explicites (ex: `show_banner` au lieu de `visible1`)

---

## 🔗 Lien entre EditorMenu et le Builder

1. **EditorMenu** : Crée un onglet dans le builder visuel.
2. **EditorValue** : Crée un champ à remplir.
3. **data-cmw** : Fait le lien entre les valeurs et le rendu en front.

Passons à la page suivante pour Définir des options de thèmes