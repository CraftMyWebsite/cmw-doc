### Explication
**NotificationManager** est un gestionnaire de notifications.

::: info
Pour le moment, il ne sert que pour les notifications administrateur.

[EN DEV] Il est prévue à l'avenir d'avoir un NotificationManager pour les utilisateurs ...
:::

### Exemple d'utilisation :

L'url est facultatif (dernier string) :
```php
NotificationManager::notify("Titre", "Message", "URL ADMIN ONLY");
```
---
**Exemple concret :**
```php
NotificationManager::notify('Nouvelle commande', $user->getPseudo() . ' viens de passer une commande.', 'shop/orders');
```
**Résultat :**
![Image d'alerte](Assets/Img/Technical/Manager/Notification/alert.png)

L'administrateur peut régler des options sur les notifications, vous n'avez pas à gérer ceci :

![Image settings](Assets/Img/Technical/Manager/Notification/settings.png)

---

### En résumé :
Le **NotificationManager** gère les notifications dans l'application. Il permet de créer des notifications soit en silence pour certains packages, soit avec une visibilité plus large (notification via Discord et email).