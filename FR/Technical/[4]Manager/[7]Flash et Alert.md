### Explication
**Flash** et **Alert** mettent en œuvre un système de notifications (ou "flash messages") qui permet d'envoyer et de gérer des alertes (comme des succès, erreurs, avertissements, etc.). Ce système est conçu avec deux classes : Flash et Alert. Ces deux classes fonctionnent ensemble pour créer, stocker et récupérer des alertes pour l'utilisateur.

### Importer les namespaces
`use CMW\Manager\Flash\Alert;`

`use CMW\Manager\Flash\Flash;`

### Exemple d'utilisation

Imaginons qu'un utilisateur s'inscrive avec succès :

```php
Flash::send(Alert::SUCCESS, 'Inscription réussie', 'Votre compte a été créé avec succès.');
```

**Type d'alerte :**
- `Alert::INFO`
- `Alert::SUCCESS`
- `Alert::WARNING`
- `Alert::ERROR`

Résultat :
![Image d'alerte](Assets/Img/Technical/Manager/Flash/exemple.png)

::: info
Utilisez l'I18N !
```php
Flash::send(Alert::ERROR, LangManager::translate('core.toaster.error'), LangManager::translate('core.toaster.internalError'));
```
:::

