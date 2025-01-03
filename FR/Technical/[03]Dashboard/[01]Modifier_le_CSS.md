# À quoi ça sert ?

Ajouter la compilation de Tailwind CSS permet de mettre à jour continuellement la feuille de style CORE tout en conservant les fonctionnalités de compilation de Tailwind CSS.

# Sur quoi cela agit-il ?

Le compilateur effectue le traitement pour produire le fichier `style.css` à partir des éléments suivants :

- Les vues situées dans `/Admin/Resources`
- Les vues situées dans `/App/Package/**/Views`
- Le générateur CSS dans `/Admin/Tailwind/cssgenerator.html`
- Et compile le CSS trouvé dans les fichiers HTML, PHP et JS

Il est important de noter que l'entrée principale du projet se trouve dans :
`/Admin/Tailwind/tailwindInput.css`

# Comment l'utiliser ?

Cela n'est pas obligatoire, sauf si vous souhaitez améliorer le CSS du panneau d'administration de CraftMyWebsite.

### Dans votre espace de travail (IDE) :
- Pour initialiser le projet, vous devrez exécuter la commande (une seule fois) :
```bash
  npm install
```
- Lorsque vous avez besoin d'appliquer des modifications dans le CSS CORE, exécutez la commande :
```bash
  npm run tw-core
```

Nous avons spécifié le numéro de build "tw-core" pour éviter toute interférence avec la compilation des thèmes utilisant également Tailwind CSS.

::: info
Avec cette configuration :
Vous pouvez utiliser le CORE pour compiler vos thèmes : cette partie sera abordée plus tard.
:::

::: info
N'oubliez pas de faire une Pull-Request sur le CORE pour en faire bénéficier de vos changements à tous les utilisateurs
:::
