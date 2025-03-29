# Configuration de l'envoi des mails via SMTP

L'envoi des mails dans votre application repose sur la configuration d'un serveur SMTP. Cette documentation vous guide étape par étape pour configurer correctement l'envoi des emails en utilisant OVH.  
Si vous utilisez un autre fournisseur (Google, Microsoft, Orange, etc.), vous devez récupérer les informations SMTP correspondantes auprès de votre fournisseur.

---

## Étape 1 : Récupérer les informations SMTP du fournisseur de mail

Pour configurer l'envoi des mails, vous avez besoin des informations suivantes :

- **Serveur SMTP** : L'adresse du serveur de messagerie sortant.
- **Port SMTP** : Généralement 465 (SSL), 587 (TLS) ou 25 (non sécurisé).
- **Nom d'utilisateur** : Votre adresse e-mail complète.
- **Mot de passe** : Le mot de passe associé à votre adresse e-mail.
- **Méthode de chiffrement** : SSL ou TLS recommandé.

### Informations SMTP d'OVH

Si vous utilisez OVH, voici les paramètres à renseigner :

- **Serveur SMTP** : `ssl0.ovh.net`
- **Port SMTP** : `465` (SSL) ou `587` (TLS)
- **Nom d'utilisateur** : Votre adresse e-mail complète (ex: `contact@votredomaine.com`)
- **Mot de passe** : Le mot de passe associé à votre adresse e-mail
- **Méthode de chiffrement** : SSL ou TLS

> 📌 **Note** : Pour d'autres fournisseurs, vous pouvez consulter leur documentation officielle pour obtenir ces informations.

---

## Étape 2 : Configuration dans le panel

- Rendez-vous sur votre panel
  - Paramètres -> SMTP et mails
- Complétez les informations de votre fournisseur de mail de l'étape 1

![smtp](Assets/Img/Users/Mail/1.png "smtp")

- Pensez à cocher SMTP
- Sauvegardez avant de tester !

Effectuez un test sur n'importe quelle adresse mail (votre adresse personnelle, par exemple).

![test](Assets/Img/Users/Mail/2.png "test")

Vous avez dû recevoir ceci si tout fonctionne correctement :

![preview](Assets/Img/Users/Mail/3.png "preview")

C'est terminé, le CMS est maintenant capable d'envoyer des mails.