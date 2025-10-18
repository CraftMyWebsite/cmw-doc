# Health Report

## Qu'est-ce qu'un Health Report ?

Le Health Report est un rapport technique qui collecte des informations non sensibles sur votre site CraftMyWebsite. Il permet à l'équipe de support de diagnostiquer rapidement les problèmes techniques sans accéder directement à votre serveur.

Le rapport contient :
- Version de PHP et extensions installées
- Configuration du serveur
- Informations sur le CMS
- Version de la base de données
- Liste des packages installés
- Liste des thèmes installés

## Sécurité

**Important :**
- N'envoyez votre Health Report **uniquement** à l'équipe officielle de CraftMyWebsite
- Supprimez vos Health Reports une fois le support terminé
- Ne partagez jamais publiquement votre rapport (forums, réseaux sociaux, etc.)

Bien que les informations soient non sensibles, elles peuvent révéler des détails sur votre configuration qui pourraient être exploités.

## Générer un Health Report

1. Connectez-vous à votre tableau de bord administrateur
2. Accédez à **Paramètres → Sécurité**
3. Dans la section **Health Report**, cliquez sur **Générer**
4. Le rapport s'affiche directement sur la page

## Emplacement du fichier

Les Health Reports sont stockés dans :
```
App/Storage/Reports/report_YYYY-MM-DD_HHhMMmSSs.txt
```

Exemple : `App/Storage/Reports/report_2025-10-18_11h18m50s.txt`

## Supprimer un Health Report

Une fois votre problème résolu, pensez à supprimer le fichier généré avec le bouton **Supprimer** sur la page du rapport.

