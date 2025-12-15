
## Services du Projet PKF Internet Banking User Service

### 29. UserService
**Rôle principal :** Gestion complète des utilisateurs finaux et administrateurs
**Fonctionnalités :**
- Récupération des informations utilisateur actuel avec contexte de sécurité
- Recherche de clients dans le système CBS (Core Banking System)
- Gestion des utilisateurs avec pagination et filtrage
- Gestion des utilisateurs bloqués et déblocage
- Gestion des administrateurs avec permissions et rôles
- Mise à jour des profils utilisateur et administrateur
- Gestion des avatars et fichiers utilisateur
- Gestion des sessions utilisateur et appareils
- Changement d'état des comptes utilisateur (activation/désactivation)
- Récupération d'informations utilisateur pour services internes

### 30. UserAccountService
**Rôle principal :** Gestion des comptes bancaires des utilisateurs
**Fonctionnalités :**
- Récupération des comptes utilisateur avec synchronisation CBS
- Gestion de l'affichage et masquage des comptes
- Mise à jour des noms de comptes personnalisés
- Gestion des permissions d'accès aux comptes pour sous-utilisateurs
- Synchronisation des soldes de comptes avec le système CBS
- Récupération d'informations détaillées des comptes clients
- Gestion des comptes par lots avec traitement asynchrone
- Validation des accès utilisateur aux comptes spécifiques

### 31. AdminUserAccountService
**Rôle principal :** Gestion administrative des comptes utilisateur
**Fonctionnalités :**
- Récupération des comptes par ID utilisateur pour administration
- Gestion du statut de masquage des comptes au niveau administratif
- Désactivation automatique de la facturation pour comptes masqués
- Notification des utilisateurs lors de modifications de comptes
- Validation de l'existence des comptes lors des mises à jour

### 32. BaseUserService
**Rôle principal :** Service de base avec fonctionnalités communes pour la gestion utilisateur
**Fonctionnalités :**
- Mise à jour des champs de base utilisateur (email, téléphone, nom d'utilisateur)
- Gestion de l'historique des modifications avec traçabilité
- Validation des permissions et autorisations
- Conversion des entités utilisateur en réponses administratives
- Récupération des sous-utilisateurs avec attributs spécifiques
- Gestion des utilisateurs corporatifs et sous-utilisateurs principaux

### 33. BankService
**Rôle principal :** Gestion des informations bancaires
**Fonctionnalités :**
- Synchronisation des données bancaires avec le système CBS
- Création et mise à jour des entités bancaires
- Gestion du cache des informations bancaires
- Comptage des banques externes et internes
- Création de la banque par défaut si inexistante

### 34. BranchService
**Rôle principal :** Gestion des succursales bancaires
**Fonctionnalités :**
- Synchronisation des succursales avec le système CBS
- Recherche de succursales par code bancaire et code succursale
- Gestion du cache des succursales avec éviction automatique
- Validation de l'existence des succursales
- Création et mise à jour des entités succursales

### 35. PackageService
**Rôle principal :** Gestion des packages de services bancaires
**Fonctionnalités :**
- Création de packages avec tarification et permissions
- Gestion des packages gratuits et payants
- Mise à jour des packages avec validation des utilisateurs actifs
- Gestion du statut des packages (actif, archivé, désactivé)
- Validation des devises et tarification multi-devises
- Gestion des permissions utilisateur liées aux packages
- Synchronisation des permissions lors des modifications de packages

### 36. ProductService
**Rôle principal :** Gestion des produits bancaires
**Fonctionnalités :**
- Création de produits avec comptes associés
- Validation des numéros de compte dans le système CBS
- Gestion du statut des produits (actif, désactivé, en attente)
- Mise à jour des produits avec validation des devises
- Gestion des comptes produits par type et devise
- Validation de l'existence d'au moins un produit actif par type

### 37. BankInfoService
**Rôle principal :** Service d'information bancaire générale
**Fonctionnalités :**
- Récupération des informations bancaires consolidées
- Gestion des détails de contact bancaire
- Fourniture d'informations système pour l'interface utilisateur

### 38. BlobFileService
**Rôle principal :** Gestion des fichiers et documents utilisateur
**Fonctionnalités :**
- Upload et stockage de fichiers dans le cloud
- Validation des types de fichiers (images, documents)
- Récupération de fichiers avec gestion des permissions
- Gestion des avatars utilisateur et documents justificatifs

### 39. BranchStatusService
**Rôle principal :** Gestion du statut des succursales
**Fonctionnalités :**
- Surveillance du statut opérationnel des succursales
- Mise à jour des statuts en temps réel
- Notification des changements de statut

### 40. ChangeTableHistoryService
**Rôle principal :** Gestion de l'historique des modifications
**Fonctionnalités :**
- Enregistrement de toutes les modifications des données sensibles
- Traçabilité des changements avec utilisateur et horodatage
- Audit des modifications pour conformité réglementaire

### 41. CurrencyService
**Rôle principal :** Gestion des devises
**Fonctionnalités :**
- Gestion des devises supportées par le système
- Conversion et calculs de change
- Validation des codes de devise alphabétiques

### 42. DetailsCache
**Rôle principal :** Gestion du cache des détails système
**Fonctionnalités :**
- Cache des informations fréquemment utilisées
- Optimisation des performances d'accès aux données
- Gestion de l'expiration et du rafraîchissement du cache

### 43. DocumentsService
**Rôle principal :** Gestion des documents utilisateur
**Fonctionnalités :**
- Upload et validation des documents d'identité
- Gestion des documents justificatifs pour ouverture de compte
- Classification et stockage sécurisé des documents

### 44. HealthCheckService
**Rôle principal :** Surveillance de la santé du système
**Fonctionnalités :**
- Vérification de l'état des services critiques
- Monitoring des connexions aux bases de données
- Rapports de santé pour les équipes d'exploitation

### 45. MainSubUserService
**Rôle principal :** Gestion des utilisateurs principaux dans les comptes corporatifs
**Fonctionnalités :**
- Création et gestion des sous-utilisateurs principaux
- Attribution des permissions et limites
- Gestion des relations hiérarchiques dans les comptes corporatifs

### 46. SessionService
**Rôle principal :** Gestion des sessions utilisateur
**Fonctionnalités :**
- Création et validation des sessions utilisateur
- Gestion des appareils et détection de nouveaux appareils
- Expiration automatique des sessions inactives
- Sécurisation des sessions avec tokens JWT

### 47. SubscriptionBillService
**Rôle principal :** Gestion de la facturation des abonnements
**Fonctionnalités :**
- Génération automatique des factures d'abonnement
- Gestion des échéances et rappels de paiement
- Traitement des paiements et mise à jour des statuts
- Génération de rapports de facturation

### 48. SubscriptionService
**Rôle principal :** Gestion des abonnements utilisateur
**Fonctionnalités :**
- Création et activation des abonnements
- Gestion des packages d'abonnement
- Renouvellement automatique des abonnements
- Suspension et résiliation des abonnements

### 49. SubUserAttributeService
**Rôle principal :** Gestion des attributs des sous-utilisateurs
**Fonctionnalités :**
- Configuration des permissions spécifiques aux sous-utilisateurs
- Gestion des limites de transaction
- Attribution des rôles et responsabilités

### 50. SubUserService
**Rôle principal :** Gestion des sous-utilisateurs
**Fonctionnalités :**
- Création de sous-utilisateurs avec permissions limitées
- Gestion des accès aux comptes pour sous-utilisateurs
- Configuration des limites et restrictions

### 51. TicketService
**Rôle principal :** Gestion du système de tickets de support
**Fonctionnalités :**
- Création et suivi des tickets de support client
- Attribution des tickets aux équipes appropriées
- Gestion du cycle de vie des tickets (ouvert, en cours, résolu, fermé)
- Communication avec les clients via le système de tickets

### 52. TransferInternalService
**Rôle principal :** Gestion des transferts internes
**Fonctionnalités :**
- Traitement des transferts entre comptes internes
- Validation des limites et permissions de transfert
- Historique et traçabilité des transferts

### 53. TwoFactorAuthService
**Rôle principal :** Gestion de l'authentification à deux facteurs
**Fonctionnalités :**
- Génération et validation des codes OTP
- Gestion des méthodes d'authentification (SMS, email, TOTP)
- Configuration des paramètres de sécurité utilisateur

### 54. UserBlockerService
**Rôle principal :** Gestion des blocages utilisateur
**Fonctionnalités :**
- Création de blocages temporaires et permanents
- Gestion des raisons de blocage
- Déblocage automatique après expiration
- Historique des blocages pour audit

### 55. UserRegistrationApproveService
**Rôle principal :** Gestion des approbations d'inscription
**Fonctionnalités :**
- Traitement des demandes d'inscription en attente
- Workflow d'approbation avec plusieurs niveaux
- Notification des décisions d'approbation
- Gestion des documents requis pour l'approbation

## Services Spécialisés par Domaine

### Services d'Alerte (Alert)
- **AlertDispatcher** : Distribution des alertes aux destinataires appropriés
- **AlertProcessingService** : Traitement et formatage des alertes
- **AlertService** : Gestion générale du système d'alertes
- **UserAlertService** : Alertes spécifiques aux utilisateurs finaux

### Services de Bénéficiaires (Beneficiary)
- **PartnerBeneficiaryService** : Gestion des bénéficiaires partenaires
- **UserBeneficiaryService** : Gestion des bénéficiaires utilisateur

### Services de Cartes (Card)
- **CardRequestService** : Traitement des demandes de cartes
- **CustomCardService** : Gestion des cartes personnalisées

### Services de Chéquiers (Checkbook)
- **CheckbookRequestService** : Traitement des demandes de chéquiers
- **CheckbookRetryableService** : Gestion des tentatives de commande de chéquiers
- **CheckbookTypeService** : Gestion des types de chéquiers disponibles

### Services de Change (Currency)
- **CurrencyExchangeRequestInternalService** : Traitement interne des demandes de change

### Services FlashCash
- **AdminFlashCashService** : Administration des services FlashCash
- **FlashCashService** : Gestion des transactions FlashCash utilisateur

### Services de Notification
- **NotificationService** : Envoi de notifications multi-canaux (email, SMS, push)

### Services PDF
- **PDFAccountDetailsBuilder** : Construction de documents PDF pour détails de compte
- **PDFAccountService** : Génération de rapports PDF de comptes
- **PDFConstants** : Constantes pour la génération PDF

### Services de Rôles (Role)
- **AdminRoleService** : Gestion des rôles administrateur
- **PermissionService** : Gestion des permissions système

### Services de Planification (Scheduler)
- **AlertScheduler** : Planification des tâches d'alerte
- **BankScheduler** : Synchronisation planifiée des données bancaires
- **BranchScheduler** : Synchronisation planifiée des succursales
- **CheckbookTypeScheduler** : Mise à jour planifiée des types de chéquiers
- **SubscriptionScheduler** : Traitement planifié des abonnements

### Services de Paramètres (Settings)
- **UserSettingsService** : Gestion des préférences utilisateur

### Services de Synchronisation (Sync)
- **UserAccountSyncService** : Synchronisation des comptes utilisateur avec CBS

### Services de Transfert (Transfer)
- **SwiftTransferInternalService** : Traitement interne des transferts SWIFT

Ce service utilisateur constitue le cœur de la gestion des utilisateurs dans l'écosystème PKF Internet Banking, offrant une gamme complète de fonctionnalités pour la gestion des comptes, la sécurité, les transactions et l'administration.