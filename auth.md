# Services Documentation - PKF Internet Banking Auth Service

## Vue d'ensemble
Ce document décrit tous les services du projet d'authentification PKF Internet Banking, leurs fonctionnalités et leurs rôles dans l'architecture globale.

## Services d'Authentification

### 1. AuthenticationService
**Rôle principal :** Gestion de l'authentification des utilisateurs finaux
**Fonctionnalités :**
- Enregistrement de nouveaux utilisateurs avec validation CBS
- Authentification des utilisateurs avec gestion MFA
- Validation des numéros de téléphone
- Vérification des codes OTP/TOTP
- Création et changement de mots de passe
- Envoi de codes de vérification
- Gestion des sessions utilisateur
- Terminaison des sessions actives

### 2. AuthenticationAdminService
**Rôle principal :** Gestion de l'authentification des administrateurs
**Fonctionnalités :**
- Enregistrement d'administrateurs avec rôles spécifiques
- Authentification des administrateurs avec validation de branche
- Gestion des tokens de rafraîchissement
- Envoi de liens de réinitialisation de mot de passe
- Réinitialisation des mots de passe utilisateur
- Génération de PDF avec identifiants utilisateur
- Changement d'état des comptes utilisateur
- Enregistrement de sous-utilisateurs par les admins

### 3. AuthenticationSuperAdminService
**Rôle principal :** Gestion de l'authentification des super-administrateurs
**Fonctionnalités :**
- Authentification des super-administrateurs
- Réinitialisation des mots de passe d'administrateurs
- Changement d'état des comptes administrateur
- Envoi de liens de réinitialisation pour super-admins
- Création de nouveaux mots de passe avec validation OTP

## Services de Gestion des Utilisateurs Corporatifs

### 4. AuthenticationMainSubUserService
**Rôle principal :** Gestion des utilisateurs principaux dans les comptes corporatifs
**Fonctionnalités :**
- Enregistrement d'utilisateurs principaux pour comptes corporatifs
- Validation des permissions et limites de création
- Gestion des attributs spécifiques aux sous-utilisateurs principaux

### 5. AuthenticationSubUserService
**Rôle principal :** Gestion des sous-utilisateurs dans les comptes corporatifs
**Fonctionnalités :**
- Enregistrement de sous-utilisateurs avec validation parentale
- Vérification des limites de création de sous-utilisateurs
- Gestion des permissions et attributs des sous-utilisateurs
- Validation des relations parent-enfant

### 6. AuthenticationCorporateService
**Rôle principal :** Services communs pour les comptes corporatifs
**Fonctionnalités :**
- Réinitialisation des mots de passe pour utilisateurs corporatifs
- Gestion des relations entre utilisateurs principaux et sous-utilisateurs

## Services d'Authentification Multi-Facteurs (MFA)

### 7. LoginTwoFactorAuthenticationService
**Rôle principal :** Gestion MFA pour les utilisateurs finaux
**Fonctionnalités :**
- Génération et envoi d'OTP par SMS/Email
- Vérification des codes OTP avec gestion des tentatives
- Gestion des blocages temporaires pour tentatives échouées
- Support des différents types d'actions (LOGIN, TRANSFER, etc.)

### 8. LoginTwoFactorAuthenticationAdminService
**Rôle principal :** Gestion MFA pour les administrateurs
**Fonctionnalités :**
- Envoi de liens de réinitialisation par email
- Validation des codes OTP pour administrateurs
- Gestion des tokens de réinitialisation avec expiration

### 9. TwoFactorAuthService
**Rôle principal :** Service générique pour la création d'OTP
**Fonctionnalités :**
- Création d'OTP pour utilisateurs spécifiques
- Envoi d'OTP par SMS et email
- Vérification des codes OTP avec validation d'action
- Support pour différents types d'actions administratives

## Services TOTP (Time-based One-Time Password)

### 10. UserTotpSettingsService
**Rôle principal :** Gestion des paramètres TOTP pour les utilisateurs
**Fonctionnalités :**
- Initialisation de la configuration TOTP
- Finalisation de la configuration avec validation
- Mise à jour du statut TOTP (actif/inactif)
- Récupération du statut TOTP utilisateur
- Suppression complète des paramètres TOTP

### 11. BackupCodeService
**Rôle principal :** Gestion des codes de sauvegarde TOTP
**Fonctionnalités :**
- Comptage des codes de sauvegarde non utilisés
- Régénération des codes de sauvegarde avec validation mot de passe
- Gestion de l'utilisation des codes de sauvegarde

## Services de Support et Utilitaires

### 12. BaseAuthenticationService
**Rôle principal :** Classe de base avec fonctionnalités communes
**Fonctionnalités :**
- Récupération du contexte de sécurité utilisateur
- Envoi d'emails d'inscription et de statut de compte
- Validation des mots de passe selon les règles définies
- Changement de mots de passe pour administrateurs
- Génération de noms d'utilisateur uniques
- Gestion des langues et locales
- Validation des branches et codes bancaires
- Vérification des accès cross-role

### 13. BaseTwoFactorAuthService
**Rôle principal :** Classe de base pour les services MFA
**Fonctionnalités :**
- Création de requêtes de messages standardisées
- Formatage des arguments pour SMS et email
- Configuration des paramètres de contact bancaire

### 14. DeviceService
**Rôle principal :** Gestion des appareils et sessions utilisateur
**Fonctionnalités :**
- Détection et enregistrement de nouveaux appareils
- Gestion du statut des appareils (nouveau/approuvé)
- Création de sessions utilisateur avec IP
- Envoi d'alertes pour nouveaux appareils
- Parsing des informations User-Agent

### 15. EmailService
**Rôle principal :** Service d'envoi d'emails
**Fonctionnalités :**
- Envoi asynchrone d'emails via l'adaptateur
- Support multilingue avec locale
- Intégration avec le client adaptateur de notifications

### 16. JwtService
**Rôle principal :** Gestion des tokens JWT
**Fonctionnalités :**
- Génération de tokens d'accès et de rafraîchissement
- Extraction des claims et validation des tokens
- Gestion de l'expiration et de la sécurité des tokens
- Support pour différents types d'utilisateurs

### 17. MessageService
**Rôle principal :** Service unifié d'envoi de messages
**Fonctionnalités :**
- Envoi combiné SMS et email avec gestion d'erreurs
- Support multilingue avec templates de messages
- Gestion des échecs partiels (SMS ou email)
- Logging des résultats d'envoi

### 18. PasswordService
**Rôle principal :** Gestion et validation des mots de passe
**Fonctionnalités :**
- Vérification des mots de passe avec gestion des tentatives
- Validation des règles de complexité
- Gestion des blocages pour tentatives échouées
- Historique des changements de mots de passe

### 19. UserBlockerService
**Rôle principal :** Gestion des blocages utilisateur
**Fonctionnalités :**
- Création de blocages temporaires avec raisons
- Vérification de l'existence de blocages actifs
- Déblocage automatique après expiration
- Gestion des différents types de blocages (login, OTP, etc.)

### 20. LoginResultService
**Rôle principal :** Gestion des résultats de connexion
**Fonctionnalités :**
- Traitement des succès de connexion
- Gestion des échecs avec compteurs de tentatives
- Création de blocages après échecs répétés
- Réinitialisation des compteurs après succès

### 21. UserAccountService
**Rôle principal :** Gestion des comptes utilisateur
**Fonctionnalités :**
- Création des associations utilisateur-compte
- Récupération des comptes clients depuis CBS
- Gestion de la visibilité des comptes
- Synchronisation avec les données bancaires

### 22. InvalidTokensCache
**Rôle principal :** Cache des tokens invalidés
**Fonctionnalités :**
- Stockage des tokens révoqués/invalidés
- Vérification de la validité des tokens
- Nettoyage automatique des tokens expirés

### 23. SubscriptionBillService
**Rôle principal :** Gestion des factures d'abonnement
**Fonctionnalités :**
- Mise à jour du statut des factures d'abonnement
- Gestion des transitions d'état des factures
- Validation des changements de statut

### 24. UserRegistrationApprovesService
**Rôle principal :** Gestion des approbations d'inscription
**Fonctionnalités :**
- Mise à jour des demandes d'approbation
- Changement de statut des inscriptions (approuvé/refusé)
- Notification des changements de statut
- Gestion des permissions d'approbation

### 25. UserRegistrationApprovesWebSocketService
**Rôle principal :** Notifications temps réel pour les inscriptions
**Fonctionnalités :**
- Envoi de notifications WebSocket pour nouvelles inscriptions
- Diffusion des mises à jour de statut d'approbation
- Gestion des connexions WebSocket administrateur

## Services Spécialisés

### 26. AdminRoleService
**Rôle principal :** Gestion des rôles administrateur
**Fonctionnalités :**
- Récupération des rôles administrateur actifs
- Validation de l'existence et du statut des rôles

### 27. PermissionService
**Rôle principal :** Gestion des permissions système
**Fonctionnalités :**
- Récupération des permissions par ID
- Validation de l'existence des permissions

### 28. PDFAdminService
**Rôle principal :** Génération de documents PDF administratifs
**Fonctionnalités :**
- Génération de documents PDF pour les administrateurs
- Création de rapports et documents officiels
- Gestion des templates PDF

---

# Services Documentation - PKF Internet Banking User Service

## Vue d'ensemble
Ce document décrit tous les services du projet de gestion des utilisateurs PKF Internet Banking, leurs fonctionnalités et leurs rôles dans l'architecture globale.

## Services de Gestion des Comptes Utilisateur

### 1. AdminUserAccountService
**Rôle principal :** Gestion des comptes utilisateur par les administrateurs
**Fonctionnalités :**
- Récupération des comptes par ID utilisateur avec gestion des sous-utilisateurs
- Mise à jour du statut de visibilité des comptes (masqués/affichés)
- Validation de l'existence de tous les comptes demandés
- Désactivation automatique de la facturation pour les comptes masqués
- Suppression des comptes des factures d'abonnement
- Notification des utilisateurs concernés par les modifications
- Mise à jour des comptes utilisateur pour l'affichage

### 2. UserAccountService
**Rôle principal :** Gestion des comptes utilisateur et synchronisation
**Fonctionnalités :**
- Récupération des comptes utilisateur avec filtrage par statut d'affichage
- Gestion des informations de compte par ID et numéro de compte
- Mise à jour des noms de comptes utilisateur
- Synchronisation des comptes utilisateur avec le système CBS
- Gestion des comptes autorisés pour les sous-utilisateurs
- Vérification des accès aux comptes
- Synchronisation des soldes de comptes avec CBS
- Récupération d'informations client depuis CBS
- Gestion par lots des informations de compte

### 3. UserService
**Rôle principal :** Service principal de gestion des utilisateurs
**Fonctionnalités :**
- Gestion des utilisateurs actuels avec informations complètes
- Recherche et récupération d'informations client depuis CBS
- Gestion des utilisateurs avec pagination et filtrage
- Gestion des utilisateurs bloqués
- Gestion des administrateurs avec historique de connexion
- Mise à jour des profils utilisateur avec validation 2FA
- Déblocage des utilisateurs avec réinitialisation des compteurs
- Mise à jour des paramètres de langue
- Gestion des avatars d'administrateur
- Changement d'état des utilisateurs (activé/désactivé)
- Récupération d'informations utilisateur pour services internes

## Services de Gestion des Sous-Utilisateurs

### 4. MainSubUserService
**Rôle principal :** Gestion des utilisateurs principaux dans les comptes corporatifs
**Fonctionnalités :**
- Recherche des utilisateurs principaux par ID parent avec pagination
- Suppression des utilisateurs principaux avec validation des contraintes
- Validation du nombre de validateurs requis
- Mise à jour des utilisateurs principaux avec vérification OTP
- Gestion des attributs spécifiques (titre de poste, nombre de validateurs)
- Nettoyage des données associées (bénéficiaires, carnets de chèques)
- Recherche administrative des utilisateurs principaux

### 5. SubUserService
**Rôle principal :** Gestion des sous-utilisateurs dans les comptes corporatifs
**Fonctionnalités :**
- Recherche des sous-utilisateurs avec contrôle d'accès
- Suppression des sous-utilisateurs avec nettoyage complet
- Mise à jour des sous-utilisateurs avec gestion des permissions
- Validation des comptes autorisés uniques
- Vérification des accès aux comptes parent
- Gestion des permissions héritées du package d'abonnement
- Mise à jour des comptes autorisés pour les sous-utilisateurs
- Vérification des droits de gestion selon la configuration

### 6. SubUserAttributeService
**Rôle principal :** Gestion des attributs des sous-utilisateurs
**Fonctionnalités :**
- Suppression des attributs de sous-utilisateur
- Recherche par ID utilisateur
- Recherche avec validation parent et statut principal
- Sauvegarde des entités d'attributs
- Vérification d'existence avec critères multiples
- Récupération groupée sous forme de map

## Services d'Information et Cache

### 7. BankInfoService
**Rôle principal :** Fourniture d'informations bancaires consolidées
**Fonctionnalités :**
- Récupération des informations bancaires depuis le cache
- Consolidation des branches, devises, banques, pays
- Fourniture des devises SWIFT et types de carnets de chèques

### 8. BankService
**Rôle principal :** Gestion des informations bancaires
**Fonctionnalités :**
- Création et synchronisation des banques depuis l'adaptateur
- Recherche par ID banque CBS
- Comptage des banques et banques externes
- Création de la banque par défaut si inexistante
- Éviction du cache lors des mises à jour

### 9. BranchService
**Rôle principal :** Gestion des agences bancaires
**Fonctionnalités :**
- Création et synchronisation des agences depuis l'adaptateur
- Recherche par ID banque et ID agence CBS avec cache
- Synchronisation des agences pour une banque donnée
- Vérification d'existence des agences
- Gestion du cache des agences

### 10. CurrencyService
**Rôle principal :** Gestion des devises
**Fonctionnalités :**
- Recherche de devises par code alphabétique avec cache
- Recherche multiple de devises par codes

### 11. DetailsCache
**Rôle principal :** Service de cache pour les données de référence
**Fonctionnalités :**
- Cache des agences avec mapping vers DTO
- Cache des devises avec mapping vers DTO
- Cache des banques avec mapping vers DTO
- Cache des pays avec mapping vers DTO
- Cache des devises SWIFT actives
- Cache des types de carnets de chèques

## Services de Gestion des Abonnements

### 12. SubscriptionService
**Rôle principal :** Gestion des abonnements utilisateur
**Fonctionnalités :**
- Mise à jour des abonnements avec validation du statut actif
- Gestion de la facturation automatique et des comptes de facturation
- Traitement des changements de package avec mise à jour des factures
- Changement de statut d'abonnement avec gestion des factures
- Résiliation et réouverture d'abonnements
- Mise à jour des permissions des sous-utilisateurs lors des changements
- Validation des comptes de facturation et devises
- Génération de rapports d'abonnement

### 13. SubscriptionBillService
**Rôle principal :** Gestion des factures d'abonnement
**Fonctionnalités :**
- Création de factures d'abonnement avec calcul des prix
- Mise à jour des prix de factures selon les packages
- Mise à jour des comptes de facturation
- Récupération des utilisateurs avec abonnements impayés
- Annulation des factures d'abonnement
- Génération de rapports de facturation avec champs personnalisables
- Gestion des dates de facturation et périodes de grâce

## Services de Gestion des Packages

### 14. PackageService
**Rôle principal :** Gestion des packages de services
**Fonctionnalités :**
- Création de packages avec validation des tarifs et permissions
- Recherche de packages avec pagination et filtrage
- Mise à jour de packages avec gestion des permissions utilisateur
- Changement de statut de packages avec validation d'utilisation
- Validation des devises et activation cross-currency
- Gestion des tarifs par devise
- Mise à jour des permissions utilisateur lors des changements
- Validation des packages gratuits en cours d'utilisation

### 15. ProductService
**Rôle principal :** Gestion des produits bancaires
**Fonctionnalités :**
- Création de produits avec validation des comptes CBS
- Récupération de produits avec filtrage par statut
- Mise à jour de produits avec validation des devises
- Changement de statut de produits avec gestion de l'unicité
- Validation des devises supportées par l'application
- Recherche de comptes produit par critères
- Validation de l'existence des numéros de compte dans CBS

## Services de Support et Tickets

### 16. TicketService
**Rôle principal :** Gestion du système de tickets de support
**Fonctionnalités :**
- Création de tickets avec gestion des fichiers joints
- Mise à jour de tickets avec validation des permissions
- Mise à jour du statut par les administrateurs
- Recherche de tickets avec filtrage par rôle
- Ajout de notes internes par les administrateurs
- Téléchargement de fichiers joints avec contrôle d'accès
- Suppression de tickets en brouillon
- Notifications automatiques aux administrateurs et clients
- Génération de numéros de tickets uniques
- Validation des fichiers et descriptions

## Services de Gestion des Documents

### 17. DocumentsService
**Rôle principal :** Gestion des documents utilisateur
**Fonctionnalités :**
- Upload de documents avec validation du type PDF
- Recherche de documents par utilisateur
- Téléchargement de documents avec contrôle d'accès
- Suppression logique de documents par les administrateurs
- Stockage dans le système de blob avec métadonnées

### 18. BlobFileService
**Rôle principal :** Gestion des fichiers dans le stockage blob
**Fonctionnalités :**
- Upload de fichiers vers différents conteneurs blob
- Validation des fichiers image (JPEG, PNG)
- Validation de la taille des fichiers
- Téléchargement de fichiers depuis le stockage blob
- Gestion des erreurs de stockage

## Services de Sécurité et Authentification

### 19. TwoFactorAuthService
**Rôle principal :** Gestion de l'authentification à deux facteurs
**Fonctionnalités :**
- Vérification des codes OTP pour différents types d'actions
- Intégration avec le service d'authentification interne

### 20. UserBlockerService
**Rôle principal :** Gestion des blocages utilisateur
**Fonctionnalités :**
- Récupération des utilisateurs bloqués actifs avec recherche
- Désactivation des blocages par utilisateur
- Pagination et tri des résultats de blocage

### 21. SessionService
**Rôle principal :** Gestion des sessions utilisateur
**Fonctionnalités :**
- Création de sessions avec détection d'appareil
- Parsing des informations User-Agent
- Extraction des données OS, navigateur et type d'appareil
- Association des sessions aux appareils

## Services de Gestion des Rôles et Permissions

### 22. UserRegistrationApproveService
**Rôle principal :** Gestion des approbations d'inscription
**Fonctionnalités :**
- Récupération des demandes d'approbation avec filtrage par branche
- Récupération des propres demandes d'approbation
- Contrôle d'accès basé sur les permissions administrateur
- Pagination et tri des demandes
- Association avec les informations d'abonnement et facturation

## Services Utilitaires et Support

### 23. ChangeTableHistoryService
**Rôle principal :** Gestion de l'historique des modifications
**Fonctionnalités :**
- Sauvegarde de l'historique des changements
- Création d'entrées d'historique avec métadonnées complètes
- Traçabilité des modifications par utilisateur et timestamp

### 24. BranchStatusService
**Rôle principal :** Fourniture du statut des agences
**Fonctionnalités :**
- Comptage des carnets de chèques non approuvés
- Comptage des tickets non résolus
- Comptage des approbations utilisateur en attente
- Filtrage par agence pour les administrateurs

### 25. HealthCheckService
**Rôle principal :** Vérification de l'état du système
**Fonctionnalités :**
- Vérification de l'état de l'adaptateur
- Retour des informations de santé du système

### 26. TransferInternalService
**Rôle principal :** Gestion des transferts internes
**Fonctionnalités :**
- Création de transferts internes vers les comptes produit
- Gestion des paiements de frais de carnets de chèques
- Intégration avec le client de transfert interne
- Logging des opérations de transfert

## Services Spécialisés par Domaine

### Services d'Alertes (alert/)
- **AlertDispatcher** : Distribution d'alertes aux administrateurs
- **AlertProcessingService** : Traitement des alertes
- **AlertService** : Gestion principale des alertes
- **UserAlertService** : Gestion des alertes utilisateur
- **WebSocket Services** : Gestion des notifications temps réel

### Services de Bénéficiaires (beneficiary/)
- **PartnerBeneficiaryService** : Gestion des bénéficiaires partenaires
- **UserBeneficiaryService** : Gestion des bénéficiaires utilisateur

### Services de Cartes (card/)
- **CardRequestService** : Gestion des demandes de cartes
- **CustomCardService** : Gestion des cartes personnalisées

### Services de Carnets de Chèques (checkbook/)
- **CheckbookRequestService** : Gestion des demandes de carnets
- **CheckbookRetryableService** : Service de retry pour carnets
- **CheckbookTypeService** : Gestion des types de carnets

### Services de Change (currency/)
- **CurrencyExchangeRequestInternalService** : Gestion des demandes de change

### Services FlashCash (flashcash/)
- **AdminFlashCashService** : Gestion administrative FlashCash
- **FlashCashService** : Service principal FlashCash

### Services de Notifications (notification/)
- **NotificationService** : Service de notifications

### Services PDF (pdf/)
- **PDFAccountDetailsBuilder** : Construction de détails PDF
- **PDFAccountService** : Service de génération PDF comptes

### Services de Rôles (role/)
- **AdminRoleService** : Gestion des rôles administrateur
- **PermissionService** : Gestion des permissions

### Services de Planification (scheduler/)
- **AlertScheduler** : Planificateur d'alertes
- **BankScheduler** : Planificateur de synchronisation banques
- **BranchScheduler** : Planificateur de synchronisation agences
- **CheckbookTypeScheduler** : Planificateur types carnets
- **SubscriptionScheduler** : Planificateur d'abonnements

### Services de Paramètres (settings/)
- **UserSettingsService** : Gestion des paramètres utilisateur

### Services de Synchronisation (sync/)
- **UserAccountSyncService** : Synchronisation des comptes utilisateur

### Services de Transfert (transfer/)
- **SwiftTransferInternalService** : Service de transferts SWIFT internes

## Architecture et Patterns

### Patterns Utilisés
- **Service Layer Pattern** : Séparation de la logique métier
- **Repository Pattern** : Abstraction de l'accès aux données
- **DTO Pattern** : Transfert de données entre couches
- **Mapper Pattern** : Conversion entre entités et DTOs
- **Cache Pattern** : Mise en cache des données de référence
- **Observer Pattern** : Notifications et alertes
- **Strategy Pattern** : Gestion des différents types de services

### Intégrations Externes
- **CBS (Core Banking System)** : Synchronisation des données bancaires
- **Adaptateur Services** : Communication avec les services externes
- **Blob Storage** : Stockage des fichiers et documents
- **Services Internes** : Communication inter-services
- **WebSocket** : Notifications temps réel

### Fonctionnalités Transversales
- **Audit et Traçabilité** : Historique des modifications
- **Sécurité** : Authentification, autorisation, 2FA
- **Cache** : Performance et réduction des appels externes
- **Validation** : Contrôles métier et techniques
- **Notifications** : Alertes et communications
- **Pagination** : Gestion des grandes listes de données
- **Filtrage et Recherche** : Critères de recherche avancés
- **Gestion d'Erreurs** : Exceptions métier personnalisées
- **Retry et Résilience** : Gestion des échecs temporaires
- **Monitoring** : Logging et métriquests PDF pour administrateurs
**Fonctionnalités :**
- Création de PDF avec identifiants utilisateur
- Formatage multilingue des documents
- Intégration des logos et arrière-plans bancaires

## Architecture et Intégrations

### Dépendances Externes
- **AdapterClient :** Intégration avec le système bancaire CBS
- **AlertInternalClient :** Envoi d'alertes aux administrateurs
- **BlobPathFileInternalClient :** Gestion des fichiers statiques
- **SettingsService :** Configuration dynamique de l'application

### Patterns Utilisés
- **Service Layer Pattern :** Séparation claire de la logique métier
- **Repository Pattern :** Accès aux données via repositories
- **Strategy Pattern :** Différentes stratégies MFA selon le type d'utilisateur
- **Template Method Pattern :** Classes de base avec méthodes communes
- **Observer Pattern :** Notifications WebSocket pour les événements

### Sécurité
- Validation stricte des permissions par rôle
- Gestion des tentatives d'accès avec blocages temporaires
- Chiffrement des mots de passe avec BCrypt
- Validation des tokens JWT avec expiration
- Protection contre les attaques par force brute
- Validation des origines pour éviter les accès cross-role

Ce système d'authentification offre une architecture robuste et sécurisée pour la gestion des utilisateurs dans un environnement bancaire multi-tenant avec support complet de l'authentification multi-facteurs.