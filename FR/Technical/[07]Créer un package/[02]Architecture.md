Dans cette section, nous allons définir l'architecture à respecter pour la création d'un **package** dans le CMS. Il est impératif de suivre cette structure afin de garantir une organisation claire et maintenable de votre code. Chaque package est localisé dans le répertoire `/App/Package/`, avec des conventions strictes concernant la nomenclature des dossiers et des fichiers.

### Conventions de Nommage
- **Dossiers** : Le nom de chaque dossier doit commencer par une majuscule et les autres lettres doivent être en minuscule.
- **Fichiers** : Les noms de fichiers doivent suivre le format CamelCase, c'est-à-dire que chaque mot commence par une majuscule sans espace entre eux.

### Structure du Package
Chaque package se situe dans le répertoire suivant :

`/App/Package/X` où X représente le nom de votre nouveau package. Dans notre exemple, nous utiliserons Example comme nom de package.

### Détails de la structure
Voici la structure de dossier que doit respecter votre package Example :
```scss
/App/Package/Example
│
├── /Package.php                      (Contient les informations du package - important)
│
├── /Controllers
│   ├── /Admin
│   ├── /Public
│
├── /Entities
│   └── /Entitytype                   (Sous-dossiers pour gros projets)
│
├── /Events
│   └── /Eventtype                    (Sous-dossiers pour gros projets)
│
├── /Implementations
│   └── /Packageimplemented           (Nom du package implémenté - important)
│
├── /Init                             (Fichiers d'initialisation)
│
├── /Interfaces
│   └── /Interfacetype                (Sous-dossiers pour gros projets)
│
├── /Lang                             (Fichiers de localisation)
│
├── /Models
│   └── /Modeltype                    (Sous-dossiers pour gros projets)
│
├── /Public
│
├── /Views
│   └── /Viewtype                     (Sous-dossiers pour les vues spécifiques)
│
└── /README.md                        (Documentation du package)
```

### Explication de la structure :
- **/Package.php** : Fichier clé qui contient les informations du package (nom, version, dépendances).
- **/Controllers** : Séparation des contrôleurs Admin et Public pour une meilleure lisibilité du code.
- **/Entities, Events, Models, Interfaces** : Organisation en sous-dossiers pour les grands projets, afin de maintenir une structure propre.
- **/Implementations** : Définit les implémentations spécifiques, avec le nom du package implémenté, ce qui est essentiel pour le bon chargement des dépendances.
- **/Init** : Fichiers d'initialisation du package.
- **/Lang** : Gestion des fichiers de traduction et localisation.
- **/Public** : Affiche les public View si le thème ne les gère pas.
- **/Views** : Gestion des vues avec une structure hiérarchique claire pour les différents types de templates.
- **/README.md** : Fichier de documentation détaillant le package et son utilisation.

### Remarques Importantes

- **Sous-dossiers et namespaces :** Chaque sous-dossier représente un **namespace** dans votre architecture. Il est donc essentiel de bien les définir pour éviter les conflits de nommage et assurer le bon chargement des fichiers.
- **Implémentations dynamiques :** Le nom du package implémenté dans le dossier **Implementations** est crucial. Il permet au CMS de charger uniquement les implémentations nécessaires, en fonction des packages utilisés par l'utilisateur. Par exemple, si votre package implémente un package nommé `Shop` et que l'utilisateur ne l'utilise pas, le CMS n'activera pas les fonctionnalités associées à ce package.

### Conclusion
Cette structure vous permettra de développer un package propre, modulaire et extensible. Veillez à respecter scrupuleusement cette architecture pour assurer la compatibilité avec le CMS et la facilité de maintenance du code.