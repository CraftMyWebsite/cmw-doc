### Explication
**DiscordWebhook** permet d'envoyer des notifications à un webhook Discord, en utilisant l'API webhook de Discord. Voici une explication détaillée des fonctionnalités et méthodes de cette classe :

### Attributs
- **Propriétés principales :**
  - `$url` : URL du webhook Discord.
  - `$name` : Nom de l'utilisateur ou du bot qui enverra le message.
  - `$content` : Contenu du message simple à envoyer.

- **Propriétés d'embed (structure enrichie du message) :**
  - `$title` : Titre de l'embed.
  - `$description` : Description du message.
  - `$titleLink` : Lien cliquable sur le titre.
  - `$color` : Couleur de la barre latérale de l'embed (en hexadécimal, sans le `#`).
  - `$footerText` : Texte dans le bas de l'embed (footer).
  - `$footerIconUrl` : URL de l'icône du footer.
  - `$imageUrl` : URL d'une image à inclure dans le message.
  - `$authorName` : Nom de l'auteur de l'embed.
  - `$authorUrl` : URL de l'auteur.
  - `$fields` : Champs supplémentaires pour l'embed (un tableau de données personnalisées).
  - `$tts` : Indique si le message doit être envoyé en mode texte à voix (Text-To-Speech).

### Exemple d'utilisation :
```php
$webhook = DiscordWebhook::createWebhook('https://discord.com/api/webhooks/...');
$webhook->setWebhookName('Mon Bot')
        ->setTitle('Titre de la notification')
        ->setDescription('Voici une description de la notification.')
        ->setColor('FF5733')
        ->setFooterText('Pied de page')
        ->send();
```

### Obtenir un URL Webhook Discord :
- Rendez-vous dans les paramètres de votre serveur Discord
- Dans _Applications_, cliquez sur _Intégrations_
- Cliquez sur _Nouveau Webhook_

![Image setting discord](Assets/Img/Technical/Manager/WebhookDiscord/settings.png)
- Renseignez les informations

![Image webhook discord](Assets/Img/Technical/Manager/WebhookDiscord/webhook.png)

- Copier l'URL !
### Conclusion
La classe **DiscordWebhook** est un outil flexible pour envoyer des notifications sur Discord via des webhooks. Elle permet de configurer des messages simples ou enrichis avec des embeds, et offre une interface fluide pour personnaliser les messages et les champs selon les besoins de l'application.