## 📄 Attributs supportés

| Attribut HTML         | Description                                                          | Exemple                                                          |
|-----------------------|----------------------------------------------------------------------|------------------------------------------------------------------|
| `data-cmw`            | Remplace le texte dans l’élément                                     | `<h1 data-cmw="header:title"></h1>`                              |
| `data-cmw-attr`       | Modifie un ou plusieurs attributs HTML (`src`, `alt`, etc.)          | `<img data-cmw-attr="src:global:logo alt:global:logo_alt">`      |
| `data-cmw-style`      | Applique dynamiquement un ou plusieurs styles CSS                    | `<div data-cmw-style="background-color:global:bg"></div>`        |
| `data-cmw-class`      | Ajoute dynamiquement des classes CSS                                 | `<div data-cmw-class="header:layout global:font"></div>`         |
| `data-cmw-visible`    | Affiche/masque selon une valeur booléenne                            | `<div data-cmw-visible="footer:show"></div>`                     |
| `data-cmw-var`        | Met à jour une ou plusieurs variables CSS personnalisées (--ma-var)  | `<div data-cmw-var="--main-color:global:main_color">`            |
| `__CMW:menu:key__`    | Injecte une valeur dans du JS ou du JSON                             | `const limit = __CMW:game:max__`                                 |


## 🧪 Exemple d’intégration complète

```html
<section
  data-cmw-visible="home:show_banner"
  data-cmw-class="global:font global:padding"
  data-cmw-style="background-image:global:banner_url"

  data-cmw-var="--main-color:global:main_color --bg-color:global:bg_color"
  style="background: linear-gradient(to bottom, var(--main-color), var(--bg-color));"
>
  <h2 data-cmw="home:title"></h2>
  <p data-cmw="home:description"></p>
</section>
```

## ✅ Bonnes pratiques

- Toujours bien nommer les clés (`themeKey`) : concises et explicites
- Regrouper les options par onglet logique (header, footer...)
- Penser à la compatibilité responsive si tu ajoutes du style via `data-cmw-style`
- Utiliser data-cmw-var dès que tu manipules des var(--xxx) dans du CSS complexe (ex : linear-gradient, border, etc.)

Pour aller plus loins et vous facilitez les configurations, referez-vous à la page suivante.