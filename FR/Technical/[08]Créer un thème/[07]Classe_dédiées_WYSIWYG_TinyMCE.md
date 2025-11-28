## Introduction

Lorsque les utilisateurs créent du contenu via l'éditeur TinyMCE, le CMS
applique automatiquement une classe dédiée à chaque élément HTML
généré.\
Ces classes permettent aux développeurs de thèmes de **styliser
uniquement le contenu éditorial**, sans impacter les autres éléments du
site.

Cette mécanique garantit :

-   une isolation totale du style TinyMCE ;\
-   une compatibilité avec tous les thèmes ;\
-   une uniformité des rendus entre l'administration et le front-end.

## Principe de fonctionnement

Lorsqu'un élément HTML est inséré, modifié ou collé dans l'éditeur
TinyMCE, le CMS applique automatiquement une classe sous la forme :

    <tag>-tmce

Exemples :

-   `<p>` → `p-tmce`
-   `<h1>` → `h1-tmce`
-   `<table>` → `table-tmce`
-   `<img>` → `img-tmce`

Les développeurs peuvent ainsi cibler uniquement les contenus créés via
l'éditeur, sans interférer avec le design général du site.

## Liste complète des classes générées

### Titres

| Tag      | Classe        | 
|----------|---------------|
| `<h1>`   | `h1-tmce`     | 
| `<h2>`   | `h2-tmce`     | 
| `<h3>`   | `h3-tmce`     | 
| `<h4>`   | `h4-tmce`     | 
| `<h5>`   | `h5-tmce`     | 
| `<h6>`   | `h6-tmce`     |

### Texte & structure

| Tag            | Classe            | 
|----------------|-------------------|
| `<p>`          | `p-tmce`          | 
| `<span>`       | `span-tmce`       | 
| `<strong>`     | `strong-tmce`     | 
| `<em>`         | `em-tmce`         | 
| `<blockquote>` | `blockquote-tmce` | 
| `<code>`       | `code-tmce`       |
| `<pre>`        | `pre-tmce`        |
| `<br>`         | `br-tmce`         |

### Listes

| Tag         | Classe       | 
|-------------|--------------|
| `<ul>`      | `ul-tmce`    | 
| `<ol>`      | `ol-tmce`    | 
| `<li>`      | `li-tmce`    | 


### Liens et médias

| Tag            | Classe       | 
|----------------|--------------|
| `<a>`          | `a-tmce`     | 
| `<img>`        | `img-tmce`   | 
| `<video>`      | `video-tmce` | 
| `<audio>`      | `audio-tmce` | 


### Tableaux

| Tag        | Classe       | 
|------------|--------------|
| `<table>`  | `table-tmce` | 
| `<thead>`  | `thead-tmce` | 
| `<tbody>`  | `tbody-tmce` | 
| `<tfoot>`  | `tfoot-tmce` | 
| `<tr>`     | `tr-tmce`    | 
| `<th>`     | `th-tmce`    | 
| `<td>`     | `td-tmce`    | 


### Divers

| Tag            | Classe            | 
|----------------|-------------------|
| `<hr>`         | `hr-tmce`         | 
| `<figure>`     | `figure-tmce`     | 
| `<figcaption>` | `figcaption-tmce` | 
| `<iframe>`     | `iframe-tmce`     |


## Exemple de feuille de style prête à l'emploi

``` css
/* Titres */
.h1-tmce { font-size: 2.2rem; font-weight: 700; margin: 1.5rem 0; }
.h2-tmce { font-size: 1.9rem; font-weight: 600; margin: 1.3rem 0; }
.h3-tmce { font-size: 1.6rem; font-weight: 600; margin: 1.2rem 0; }

/* Paragraphe */
.p-tmce { margin: 1rem 0; line-height: 1.6; }

/* Listes */
.ul-tmce, .ol-tmce { padding-left: 1.5rem; margin: 1rem 0; }
.li-tmce { margin: 0.4rem 0; }

/* Liens */
.a-tmce { color: var(--primary-color); text-decoration: underline; }
.a-tmce:hover { opacity: 0.8; }

/* Images */
.img-tmce { max-width: 100%; height: auto; border-radius: 6px; }

/* Blockquote */
.blockquote-tmce {
    border-left: 4px solid var(--primary-color);
    padding-left: 1rem;
    font-style: italic;
    margin: 1.5rem 0;
}

/* Code */
.code-tmce, .pre-tmce {
    background: #f4f4f4;
    padding: 0.6rem 0.9rem;
    border-radius: 5px;
    font-family: monospace;
}

/* Tableaux */
.table-tmce { width: 100%; border-collapse: collapse; margin: 1.5rem 0; }
.th-tmce, .td-tmce { border: 1px solid #ddd; padding: 0.7rem; }
.thead-tmce { background: #f0f0f0; font-weight: bold; }

/* Figures */
.figure-tmce { text-align: center; margin: 1.5rem 0; }
.figcaption-tmce { font-size: 0.9rem; opacity: 0.7; margin-top: 0.4rem; }
```

## Bonnes pratiques

-   Regroupez vos styles TinyMCE dans un fichier dédié, par exemple :\
    `editor-content.css`
-   Utilisez uniquement les classes `*-tmce` pour cibler le contenu
    éditorial.
-   Évitez d'écraser les styles globaux du thème pour garder une
    séparation propre.
-   Chargez les styles TinyMCE uniquement dans les pages où du contenu
    est affiché.

## Conclusion

Grâce à ce système de classes automatiques, les développeurs peuvent
personnaliser de manière fine et contrôlée tous les contenus créés via
TinyMCE, sans risque d'impacter le reste de l'interface du site.
