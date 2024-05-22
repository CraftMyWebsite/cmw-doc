## Conventions - Bases de données

Les *tables* & les *colonnes* sont à écrire en **snake_case**
Exemple → `cmw_votes_votepoints`

Le nom des colonnes / tables est à écrire impérativement en **anglais**!

De plus il est important de commenter les colonnes qui contiennent des valeurs numériques difficilement 
compréhensibles sans documentation, comme les tinyint.

Toutes les tables doivent avoir comme prefixe `cmw_`, exemple: `cmw_users`

Toute table doit posséder au **minimum** une contrainte de clé primaire.

Il est important de rappeler le nom de la table dans votre colonne.

- Si la colonne n’est pas une colonne étrangère, il faudra référer le nom de la table actuelle.
- Si la colonne est une colonne étrangère (possédant une contrainte de clé étrangère), il faudra renseigner le nom de la table étrangère.

⇒ Composition : `cmw_tableName_columnName`