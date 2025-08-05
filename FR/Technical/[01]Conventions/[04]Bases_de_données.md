### 🐍 Nom des tables et colonnes

- Utilisez systématiquement le format **`snake_case`**.
    - ✅ Exemple : `cmw_votes_votepoints`
- Tous les noms de **tables** et **colonnes** doivent être rédigés **en anglais uniquement**.
- Chaque table **doit obligatoirement commencer** par le préfixe `cmw_`.
    - ✅ Exemple : `cmw_users`

### 🔐 Contraintes

- **Toute table doit posséder au minimum une clé primaire.**
- **Les colonnes contenant des valeurs numériques complexes** (ex : `tinyint`) doivent être **commentées** pour en expliquer la signification.

### 🧠 Rappel du nom de la table dans les colonnes

Pour chaque colonne :

- Si **ce n’est pas une clé étrangère** → le nom de la colonne doit référencer **la table actuelle**.
- Si **c’est une clé étrangère** → la colonne doit référencer **la table étrangère**.

📌 **Format recommandé :**  
`cmw_<tableName>_<columnName>`

#### ✅ Exemples :

| Type de colonne     | Exemple                         |
|---------------------|---------------------------------|
| Colonne normale     | `cmw_users_username`            |
| Clé étrangère       | `cmw_articles_user_id`          |
