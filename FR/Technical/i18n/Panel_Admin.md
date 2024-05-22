## Internationalisation du panel admin

Les fichiers langues sont stockés dans les package comme suit:

**App/Package/Example/Lang/fr.php**

Ici, le fichier s’appelle fr.php, donc CMW comprendra que le fichier de langue sera pour la langue **Française.**

Voici la liste des langues supportées actuellement :

- Français
- Anglais

Voici un exemple de fichier lang:

```php
return [
    "helloBuddy" => "Bonjour ! Je suis une phrase normale",
    "alt" => [
	    "welcome" => "Un bienvenue dans un tableau"
    ],
	"variables" => "Des variables ? Alors, euh %name%, est ton prénom ?"
];
```

Les clés ne doivent pas comporter ni d’accents ni de caractères spéciaux ni espaces.

## Utiliser les traductions

Cet exemple nous montre, comment accéder à une traduction simple.
**Attention**, il faut toujours commencer par le nom du package, dans notre cas, c'est "example".
```php
LangManager::translate("example.alt.welcome");
```

Cet exemple nous montre, comment accéder à une traduction et utiliser une variable. 
**Attention**, vous ne devez pas écrire les % autour de la variable.
Vous pouvez bien évidement utiliser plusieurs variables dans la même traduction.
```php
LangManager::translate("example.variables", ['name' => 'Thomas']);
```