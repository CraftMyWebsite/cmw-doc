## Qu'est-ce que c'est ? 🧐
Ceci est un repository GitHub à forker pour créer très rapidement des thèmes avec TailwindCSS, un genre de *clone and go* avec quelques fonctionnalités de base pour bien commencer votre thème.

Ce projet est un *template*, c'est-à-dire une base sur laquelle vous pouvez travailler. Cependant, certaines modifications sont nécessaires.

Le nom du thème par défaut est **Tailwind**. À vous de choisir et de remplacer ce nom par celui que vous souhaitez.

[Consultez le repository GitHub ici](https://github.com/CraftMyWebsite/cmw-theme-tailwindcss-template)


---

## À savoir ! 📚
Ce projet **doit** être placé dans le répertoire suivant : `/Public/Themes/Xxxxx`.

Pour cela, vous devez déjà avoir le CORE configuré dans votre IDE.

---

## Contenue de cette documentation ⚙️

::: info
Il est fortement conseillé d'avoir un IDE performant et avec lequel vous êtes à l'aise.  
PhpStorm ou IntelliJ sont compatibles avec cette documentation.  
À vous de l'adapter à votre configuration.
:::

Nous partons du principe que vous avez déjà un environnement local avec le [CORE](https://github.com/CraftMyWebsite/cmw-core) mis en place et que vous avez déjà exécuté la commande :  
`npm install`

Si ce n'est pas encore le cas, référez-vous à la [documentation suivante](https://craftmywebsite.fr/docs/fr/technical/dashboard/modifier-le-css).

### Étapes à suivre :

1. **Forker ce repository dans votre environnement de travail**
2. **Modifier les besoins**
3. **Comprendre le fonctionnement**
4. **Découvrir les fonctionnalités incluses**
5. **Tester et se lancer**

---

## Comment faire 🚀

Dans notre cas, le thème s'appellera `Example`.

### 1. Forker et cloner le repository

::: warning

Attention, vous ne pouvez faire un Fork qu'une seul fois, si vous souhaitez créer plusieur thèmes veuillez suivre ces étapes :
- [Télécharger l'archive du repo](https://github.com/CraftMyWebsite/cmw-theme-tailwindcss-template/archive/refs/heads/main.zip) 
- [Créer un nouveau repo](https://github.com/new) sur votre compte GitHub
- Initialiser ce repo avec l'archive précédemment télécharger
:::

**Info :** Un Fork permet de créer un repository à partir d'un repository déjà existant. Cela vous permet de le modifier et de mettre à jour vos modifications sans interférer avec le repository initial.

- Rendez-vous sur [ce lien](https://github.com/CraftMyWebsite/cmw-theme-tailwindcss-template/fork) pour créer un Fork du repository initial.
- Choisissez une organisation ou votre profil (voir image 1).
- Donnez-lui un nom, par exemple `theme-Example` dans notre cas (voir image 1).


**Image 1 :**
![Fork le repo](Assets/Img/Technical/Tailwindcss/fork.png "Fork le repo")

- Une fois votre repository créé, rendez-vous dans votre IDE (PhpStorm dans notre cas).
- Clonez le repository `theme-Example` dans votre CORE déjà en place (voir image 2).
   - Clonez-le dans le répertoire `/Public/Theme/Example` (voir image 2).

**Image 2 :**
![Cloner le repo](Assets/Img/Technical/Tailwindcss/clone.png "Cloner le repo")

À ce stade, vous devriez avoir le thème `Example` dans `/Public/Themes` (voir image 3).

**Image 3 :**
![Liste des themes](Assets/Img/Technical/Tailwindcss/themeList.png "Liste des themes")

### 2. Modifier les besoins

Dans cette partie, nous allons devoir modifier les fichiers suivants :
- `Theme.php`
- `Resources/tailwind.config.js`
- `package.json`

**Theme.php :**
- Changez le nom du namespace par :  
  `namespace CMW\Theme\Example;`  
  (voir image 4, annotation bleue)

- Changez le nom du thème par :  
  `return 'Example';`  
  (voir image 4, annotation bleue)

- Définissez l'auteur du thème :  
  `return 'MON NOM ICI';`  
  (voir image 4, annotation bleue)

- **Bonus :** Vous pouvez changer l'image par défaut du thème :
   - Référez-vous à `function imageLink()` dans ce fichier.


**Image 4 :**
![themephp](Assets/Img/Technical/Tailwindcss/themephp.png "themephp")

**Resources/tailwind.config.js :**
- Dans le tableau `content`, mettez à jour le chemin pour qu'il corresponde à votre thème :
   - Remplacez `Tailwind` par `Example`. (voir image 5)

**Image 5 :**
![configtailwind](Assets/Img/Technical/Tailwindcss/configtailwind.png "configtailwind")

**package.json :**
- Changez le nom par `theme-example` dans notre cas (voir image 6).
- **Facultatif :** Changez la description (voir image 6).
- Modifiez l'appel du script de compilation (voir image 6) :
   - Sur cette ligne, vous avez 4 modifications à apporter :
      1. Changez le nom du script par `Example` dans notre cas.
      2. Modifiez l'emplacement des fichiers suivants :
         - `input.css`
         - `output.css`
         - La configuration de Tailwind (non visible sur le screen).  
           Remplacez-les pour qu'ils correspondent au nom de votre thème, `Example` dans notre cas.

**Explication :**
Le script `Example` permet de lancer la commande `npm run Example` pour compiler votre thème.  
Ceci doit être unique pour éviter tout conflit avec d'autres scripts.


**Image 6 :**
![package](Assets/Img/Technical/Tailwindcss/package.png "package")

Vous pouvez maintenant exécuter la commande :
```bash
npm run Example
```
Rendez-vous ensuite sur votre site à l'adresse suivante :
votre-site.com/cmw-admin/theme/theme

Vous devriez voir et être en mesure d'activer votre thème (voir image 7).

Je vous laisse aller voir le résultat par vous-même.

Note importante :
Si votre thème n'a pas de style, cela indique un problème. Je vous invite à :

Relire attentivement cette documentation ou contacter un support via Discord.

**Image 7 :**
![theme](Assets/Img/Technical/Tailwindcss/theme.png "theme")

Vous êtes maintenant prêt à compiler votre thème et pouvez vous arrêter ici dans la lecture.

Pour plus de détails, je vous invite à continuer.


### 3. Comprendre le fonctionnement
Ici, je ne vais pas expliquer l'intérêt d'utiliser le framework TailwindCSS, car j'imagine que si vous êtes là, c'est que vous savez déjà pourquoi il est bon de l'utiliser.

La commande à retenir est :
```bash
npm run NOM-DE-VOTRE-BUILD
```
`npm run Example` dans notre cas.

Celle-ci vous permet de compiler le CSS de votre thème et doit tourner en permanence. Prenez le réflexe de lancer cette commande à chaque fois que vous travaillez sur votre thème.

Cette commande va générer le CSS de votre thème dans :
```
/Public/Themes/Example/Assets/Css/style.css
```

Pour créer et générer du CSS "custom", vous pouvez l'inclure manuellement dans :`/Resources/input.css`, celui-ci sera pris en charge et compilé par TailwindCSS dans votre sortie finale (`style.css`).

Vous pouvez également étendre vos propres styles sur des propriétés déjà existantes dans `/Resources/tailwind.config.js`

Quant au `cssgenerator.html` dans `/Resources`, il est extrêmement important. Il permet, entre autres, de forcer TailwindCSS à générer des classes qui sont, par exemple, des variables pour votre configuration, mais qui ne sont pas nativement incluses dans vos pages PHP. Par exemple, dans notre cas, il force la création des polices d'écriture et des grilles (grid panels).

### 4. Features incluse

Ce template ne fournit pas qu'un environnement de départ, il vous offre également quelques petits bonus, notamment :

- **Un exemple de configuration** :
   - `/Config/config.php`
   - `/Config/config.settings.php`

- **Des polices d'écriture personnalisables** (voir le *tips* en bas de cette page).

- **La librairie [FlowBite](https://flowbite.com/docs/getting-started/introduction/)** :  
  Une bibliothèque d'éléments UI préconstruits pour accélérer le développement.

- **L'architecture de base pour bien commencer votre thème** :
   - Répertoire `/Views/*`, comprenant :
      - Quelques formulaires.
      - Autres petites fonctions utiles.

### 5. Tester et se lancer

Vous l'avez compris, vous êtes maintenant complètement prêt à vous amuser et à créer un thème dans les meilleures conditions possibles.

Vous aurez certainement besoin de consulter ces documentations pour mener à bien votre projet :
- [TailwindCSS](https://tailwindcss.com/docs/screens)
- [FlowBite](https://flowbite.com/docs/getting-started/introduction/)

**Amusez-vous bien et prenez du plaisir !**


---

## Bonus 🎁
Nous avons intégré la bibliothèque **Flowbite** pour faciliter le développement de vos thèmes avec **TailwindCSS**.

### Fonctionnalités incluses :
- **Webfonts préchargées** :  
  Une configuration administrateur dans le panel permet de changer la police utilisée.

- **Personnalisation des couleurs** :  
  Nous vous expliquons comment mettre en place des couleurs personnalisables dans le dashboard.  
  Consultez les fichiers suivants :
   - `head.inc.php` (:root)
   - `input.css`
   - `config.php`
   - `config.settings.php`

- **Switcher Light/Dark préintégré** :  
  Par défaut, il est inactif. Pour l'activer et en savoir plus, référez-vous aux fichiers suivants :
   - `head.inc.php`
   - `header.inc.php`
   - `footer.inc.php`

---

## Tips : Ajouter des polices ✏️

Pour ajouter de nouvelles polices d'écriture, suivez ces quelques étapes :

1. **Ajouter le fichier de police**  
   Copiez le fichier `Regular.ttf` de votre police dans le répertoire suivant :  
   `/Assets/Webfonts/*`.

2. **Modifier le fichier `head.inc.php`**  
   Ajoutez un lien vers votre nouvelle police en vous basant sur les exemples précédents.

3. **Configurer Tailwind CSS**  
   Ouvrez le fichier `tailwind.config.js` et, dans `theme > extend > fontFamily`, ajoutez votre police en suivant les exemples précédents.

4. **Forcer la compilation des classes**  
   Dans `cssgenerator.html`, forcez la compilation de la classe liée à votre police pour qu'elle ne soit pas ignorée. Exemple :`class="font-NewFont"`

5. **Ajouter la police dans les choix utilisateur**

   Mettez à jour `config.php` pour inclure la nouvelle police dans les options utilisateur

---

## Conclusion 🎉
Vous êtes maintenant prêt à créer votre thème avec **TailwindCSS** et **Flowbite**. Pour vous assurer que tout fonctionne, activez votre thème et vérifiez que le texte "footer" (copyright) apparaît en bas de la page. Si c'est le cas, votre projet est prêt. Sinon, rapprochez-vous du support de CraftMyWebsite sur [Discord](https://craftmywebsite.fr/discord)