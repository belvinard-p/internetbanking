## Services de l'Adaptateur TEFO PKF Internet Banking (pkf-ib-be-tefo-adapter-service)

### 95. BankService
**Rôle principal :** Gestion des informations bancaires via l'adaptateur TEFO
**Fonctionnalités :**
- Récupération des données bancaires depuis le système TEFO CBS
- Transformation des réponses TEFO en format standardisé de l'adaptateur
- Mapping des structures de données bancaires entre TEFO et l'écosystème PKF
- Gestion des erreurs de communication avec le système TEFO

### 96. BranchService
**Rôle principal :** Gestion des succursales bancaires via TEFO
**Fonctionnalités :**
- Récupération des informations de succursales depuis TEFO CBS
- Conversion des données de succursales au format adaptateur standard
- Synchronisation des données de succursales avec le système central
- Mapping des codes et identifiants de succursales TEFO

### 97. CurrencyService
**Rôle principal :** Gestion des devises via l'adaptateur TEFO
**Fonctionnalités :**
- Récupération des devises supportées par le système TEFO
- Transformation des données de devises au format standardisé
- Gestion des codes de devises et taux de change TEFO
- Synchronisation des informations monétaires

### 98. SwiftCurrencyService
**Rôle principal :** Gestion des devises SWIFT via TEFO
**Fonctionnalités :**
- Récupération des devises SWIFT supportées par TEFO
- Mapping des codes de devises SWIFT internationaux
- Conversion des données SWIFT au format adaptateur
- Gestion des devises pour transferts internationaux

### 99. OAuth2TokenService
**Rôle principal :** Gestion de l'authentification OAuth2 avec TEFO
**Fonctionnalités :**
- Récupération et gestion des tokens d'accès OAuth2
- Cache Redis des tokens avec gestion de l'expiration
- Validation de la validité des tokens avant utilisation
- Renouvellement automatique des tokens expirés
- Gestion sécurisée des credentials OAuth2
- Optimisation des appels d'authentification via mise en cache

### 100. HealthService
**Rôle principal :** Surveillance de la santé du système TEFO
**Fonctionnalités :**
- Vérification de l'état de connectivité avec TEFO CBS
- Monitoring de la disponibilité des services TEFO
- Rapports de santé pour supervision système
- Détection des pannes de communication

## Services de Planification

### 101. OAuth2TokenScheduler
**Rôle principal :** Planification automatique du renouvellement des tokens OAuth2
**Fonctionnalités :**
- Renouvellement proactif des tokens avant expiration
- Gestion des tentatives de renouvellement avec backoff exponentiel
- Utilisation de verrous distribués (ShedLock) pour éviter les conflits
- Planification intelligente basée sur la durée de vie des tokens
- Gestion des échecs avec stratégie de retry configurable
- Logging détaillé des opérations de renouvellement
- Configuration flexible des intervalles de renouvellement

## Clients TEFO

### 102. BankClient
**Rôle principal :** Client de communication avec l'API bancaire TEFO
**Fonctionnalités :**
- Communication REST avec les endpoints bancaires TEFO
- Gestion des erreurs HTTP et des exceptions réseau
- Parsing des réponses JSON du système TEFO
- Logging des requêtes et réponses pour audit

### 103. BranchClient
**Rôle principal :** Client pour les services de succursales TEFO
**Fonctionnalités :**
- Appels API vers les endpoints de succursales TEFO
- Gestion des timeouts et retry automatique
- Transformation des réponses TEFO en objets Java

### 104. CurrencyClient
**Rôle principal :** Client pour les services de devises TEFO
**Fonctionnalités :**
- Récupération des données de devises via API TEFO
- Gestion des erreurs de communication monétaire
- Parsing des structures de données de devises TEFO

### 105. SwiftCurrencyClient
**Rôle principal :** Client pour les devises SWIFT TEFO
**Fonctionnalités :**
- Communication avec les endpoints SWIFT de TEFO
- Récupération des codes de devises internationaux
- Gestion des données de transferts internationaux

### 106. OAuth2Client
**Rôle principal :** Client d'authentification OAuth2 avec TEFO
**Fonctionnalités :**
- Authentification client credentials avec TEFO
- Gestion des requêtes de token OAuth2
- Parsing des réponses d'authentification
- Gestion sécurisée des credentials client
- Support des standards OAuth2 pour l'intégration TEFO

### 107. HealthClient
**Rôle principal :** Client de vérification de santé TEFO
**Fonctionnalités :**
- Appels de health check vers TEFO CBS
- Vérification de la connectivité réseau
- Monitoring de la disponibilité des services

## Gestionnaires d'Exceptions

### 108. CbsExceptionHandler
**Rôle principal :** Gestion centralisée des exceptions TEFO CBS
**Fonctionnalités :**
- Traitement uniforme des erreurs HTTP de TEFO
- Conversion des erreurs TEFO en exceptions métier
- Logging structuré des erreurs pour diagnostic
- Gestion des codes d'erreur spécifiques à TEFO
- Retry automatique pour erreurs temporaires

## Configuration et Sécurité

### 109. OAuth2Properties
**Rôle principal :** Configuration des paramètres OAuth2 pour TEFO
**Fonctionnalités :**
- Gestion des credentials OAuth2 (client_id, client_secret)
- Configuration des URLs d'authentification TEFO
- Paramètres de renouvellement automatique des tokens
- Configuration des timeouts et intervalles de retry

### 110. OAuth2HeaderRequestInterceptor
**Rôle principal :** Injection automatique des headers OAuth2
**Fonctionnalités :**
- Ajout automatique des tokens Bearer aux requêtes
- Gestion transparente de l'authentification pour tous les appels
- Renouvellement automatique des tokens expirés
- Sécurisation de toutes les communications avec TEFO

Cet adaptateur TEFO constitue la couche d'intégration spécialisée pour le système Core Banking TEFO, fournissant une interface standardisée et sécurisée pour tous les services bancaires centraux, avec une gestion robuste de l'authentification OAuth2 et une surveillance continue de la connectivité.