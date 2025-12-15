## Services du Projet PKF Internet Banking Transaction Service (pkf-ib-be-transaction-service)

### 78. TransactionService
**Rôle principal :** Gestion complète des transactions bancaires
**Fonctionnalités :**
- Récupération des transactions avec pagination et filtrage avancé
- Gestion des transactions pour utilisateurs, sous-utilisateurs et administrateurs
- Calcul des revenus et dépenses avec statistiques financières
- Analyse des dépenses par catégorie avec pourcentages
- Vue d'ensemble financière avec graphiques temporels
- Recherche de transactions par ID avec contrôle d'accès
- Génération de rapports de transactions pour périodes spécifiques
- Ajout d'informations d'opération (créateur, validateurs) aux transactions
- Validation des plages de dates et gestion des fuseaux horaires
- Contrôle d'accès aux comptes masqués selon configuration

### 79. TransactionSynchronizer
**Rôle principal :** Synchronisation des transactions avec le système CBS
**Fonctionnalités :**
- Synchronisation paresseuse (lazy) et empressée (eager) des transactions
- Gestion des opérations de synchronisation avec intervalles configurables
- Récupération par lots des transactions depuis le CBS avec gestion des dates
- Suppression des transactions non-historiques avant resynchronisation
- Mise à jour du statut des opérations financières après synchronisation
- Gestion sécurisée des opérations de synchronisation avec gestion des conflits
- Synchronisation initiale avec historique configurable
- Traitement asynchrone des synchronisations pour optimiser les performances

### 80. AccountService
**Rôle principal :** Gestion des comptes bancaires dans le contexte transactionnel
**Fonctionnalités :**
- Récupération des informations de compte par ID
- Validation de l'existence des comptes pour les transactions
- Recherche de comptes multiples avec validation d'existence
- Conversion des entités compte en DTOs pour les services

### 81. SubscriptionBillService
**Rôle principal :** Gestion des factures d'abonnement et paiements
**Fonctionnalités :**
- Mise à jour automatique des transactions pour factures payées manuellement
- Détection et traitement des factures payées via synchronisation CBS
- Génération automatique de nouvelles factures après paiement
- Gestion des factures expirées avec annulation automatique
- Envoi de notifications pour factures impayées
- Génération de PDF de factures avec support multilingue
- Envoi asynchrone de factures par email avec pièces jointes
- Création d'URLs de connexion spécifiques selon le type d'utilisateur
- Gestion des devises multiples pour la facturation

### 82. TransactionCategoryService
**Rôle principal :** Gestion des catégories de transactions
**Fonctionnalités :**
- Récupération de toutes les catégories avec mise en cache
- Recherche de catégories par ID et par nom
- Validation de l'existence des catégories
- Support de la catégorisation automatique des transactions

### 83. TransactionDownloadService
**Rôle principal :** Gestion des téléchargements de transactions
**Fonctionnalités :**
- Création de liens de téléchargement temporaires pour transactions
- Génération de PDF de transactions individuelles
- Gestion de l'expiration des liens de téléchargement
- Nettoyage automatique des téléchargements expirés
- Contrôle d'accès pour les téléchargements de transactions
- Suppression automatique après téléchargement pour sécurité

### 84. EmailService
**Rôle principal :** Service d'envoi d'emails pour les transactions
**Fonctionnalités :**
- Envoi asynchrone d'emails via l'adaptateur CBS
- Support des pièces jointes (PDF de factures, rapports)
- Gestion multilingue des emails
- Intégration avec le système de notification bancaire

### 85. UserAccountService
**Rôle principal :** Gestion des accès aux comptes utilisateur
**Fonctionnalités :**
- Validation des droits d'accès aux comptes pour transactions
- Gestion des permissions pour sous-utilisateurs et utilisateurs principaux
- Contrôle d'accès basé sur les relations parent-enfant
- Validation des accès multiples pour opérations par lots
- Support de la lecture étendue pour sous-utilisateurs selon configuration

## Services Internes

### 86. TransactionInternalService
**Rôle principal :** API interne pour synchronisation des transactions
**Fonctionnalités :**
- Synchronisation forcée des transactions via API interne
- Interface pour autres services nécessitant des données transactionnelles
- Gestion des requêtes de synchronisation inter-services

## Services de Rapports

### 87. TransactionReportService
**Rôle principal :** Génération de rapports de transactions
**Fonctionnalités :**
- Génération de rapports détaillés par période
- Export de données transactionnelles en différents formats
- Rapports personnalisés selon les critères utilisateur
- Agrégation de données pour analyses financières

## Services PDF

### 88. PDFTransactionService
**Rôle principal :** Génération de documents PDF pour transactions
**Fonctionnalités :**
- Création de PDF pour transactions individuelles
- Formatage professionnel avec en-têtes bancaires
- Support multilingue pour les documents
- Intégration des logos et éléments de branding

### 89. PDFSubscriptionBillService
**Rôle principal :** Génération de PDF pour factures d'abonnement
**Fonctionnalités :**
- Création de factures PDF détaillées
- Inclusion des informations de paiement et échéances
- Formatage selon les standards comptables
- Personnalisation selon le type d'abonnement

## Services de Statistiques

### 90. BaseStatisticService
**Rôle principal :** Service de base pour calculs statistiques
**Fonctionnalités :**
- Fonctionnalités communes pour analyses statistiques
- Calculs de base pour métriques financières
- Utilitaires pour agrégations de données

### 91. StatisticTransactionService
**Rôle principal :** Statistiques avancées des transactions
**Fonctionnalités :**
- Analyse des tendances de transactions
- Calculs de moyennes et médianes
- Statistiques par catégorie et période
- Métriques de performance financière
- Comparaisons périodiques et analyses de croissance

## Services de Planification

### 92. SubscriptionBillScheduler
**Rôle principal :** Planification automatique des factures d'abonnement
**Fonctionnalités :**
- Génération automatique des factures périodiques
- Traitement des paiements en attente
- Gestion des échéances et rappels
- Mise à jour des statuts d'abonnement

### 93. TransactionDownloadScheduler
**Rôle principal :** Nettoyage des téléchargements expirés
**Fonctionnalités :**
- Suppression automatique des liens de téléchargement expirés
- Optimisation de l'espace de stockage
- Maintenance de la sécurité des téléchargements

## Services Utilitaires

### 94. AppUtils
**Rôle principal :** Utilitaires communs pour l'application
**Fonctionnalités :**
- Génération de valeurs uniques pour références
- Utilitaires de formatage et conversion
- Fonctions communes partagées entre services

Ce service de transactions constitue le cœur du système de gestion financière PKF Internet Banking, gérant l'ensemble du cycle de vie des transactions depuis leur synchronisation avec le CBS jusqu'à leur présentation aux utilisateurs, en passant par la génération de rapports et la facturation automatique.