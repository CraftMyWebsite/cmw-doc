L'**OAuth** (Open Authorization) est un protocole d'autorisation ouvert utilisé pour accorder un accès limité à des ressources sur un serveur, sans exposer les identifiants des utilisateurs. Il permet à une application tierce d'accéder à certaines parties du compte d'un utilisateur sur une autre plateforme, en utilisant des jetons d'accès temporaires.

### Principe de fonctionnement
- **Demande d'autorisation** : L'application (le "client") demande l'autorisation à l'utilisateur pour accéder à une ressource sur une autre plateforme (le "serveur de ressources").

- **Autorisation de l'utilisateur** : L'utilisateur accorde ou refuse cette autorisation via une interface de connexion.

- **Jeton d'accès** : Si l'autorisation est accordée, le serveur d'autorisation fournit un jeton d'accès à l'application.

- **Accès aux ressources** : L'application utilise ce jeton pour accéder aux ressources de l'utilisateur sur le serveur, sans avoir besoin de connaître le mot de passe de l'utilisateur.

### Exemple d'utilisation :
Lorsqu’un utilisateur souhaite se connecter à un site via Google, l'application redirige l'utilisateur vers Google pour l'autoriser. Une fois l'autorisation donnée, l'application reçoit un jeton qui lui permet d'accéder aux informations du compte utilisateur (comme l'adresse e-mail).

### Avantages :
- **Sécurisé** : Le mot de passe n'est jamais partagé.
- **Granulaire** : L'utilisateur peut accorder un accès limité.
- **Révocable** : L'accès peut être révoqué à tout moment.

**OAuth** est souvent utilisé pour des fonctionnalités telles que l'authentification sociale ("Se connecter avec Facebook/Google") et l'intégration d'API.