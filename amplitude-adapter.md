# Amplitude Adapter Service Documentation

## Vue d'ensemble

Le service Amplitude Adapter est un adaptateur qui fait l'interface entre le système PKF Internet Banking et le système bancaire Amplitude. Il traduit les requêtes du système Internet Banking vers les APIs du système Amplitude et vice versa, fournissant une couche d'abstraction pour les opérations bancaires.

## Architecture

- **Framework**: Spring Boot 3
- **Java Version**: 21
- **Type**: Service d'adaptation/intégration
- **Communication**: REST APIs avec le système Amplitude

## Services Principaux

### 1. Service de Comptes (`AccountService`)

**Endpoint**: `/api/v1/cbs-adapter/accounts`

**Fonctionnalités**:
- Récupération des comptes clients
- Consultation des soldes de comptes
- Validation des numéros de comptes selon le format Amplitude

**Endpoints**:
- `GET /accounts?clientCode={code}` - Obtenir les comptes d'un client
- `POST /accounts/balance` - Obtenir les soldes de comptes

### 2. Service de Devises (`CurrencyService`)

**Endpoint**: `/api/v1/cbs-adapter/currencies`

**Fonctionnalités**:
- Liste des devises supportées par Amplitude
- Taux de change en temps réel
- Configuration de la devise de base

**Endpoints**:
- `GET /currencies` - Lister les devises supportées
- `GET /currencies/rates` - Obtenir les taux de change

### 3. Service de Banques (`BankService`)

**Endpoint**: `/api/v1/cbs-adapter/banks`

**Fonctionnalités**:
- Informations sur les banques
- Liste des agences bancaires
- Codes bancaires et identifiants

### 4. Service d'Agences (`BranchService`)

**Endpoint**: `/api/v1/cbs-adapter/branches`

**Fonctionnalités**:
- Liste des agences bancaires
- Informations détaillées sur les agences
- Localisation géographique

### 5. Service de Clients (`CustomerService`)

**Endpoint**: `/api/v1/cbs-adapter/clients`

**Fonctionnalités**:
- Informations clients
- Validation des données clients
- Gestion des profils clients
- Informations sur les comptes clients

### 6. Service de Carnets de Chèques (`CheckbookService`)

**Endpoint**: `/api/v1/cbs-adapter/checkbooks`

**Fonctionnalités**:
- Types de carnets de chèques disponibles
- Demande de carnets de chèques
- Gestion des commandes

### 7. Service de Frais d'Opération (`OperationFeesService`)

**Endpoint**: `/api/v1/cbs-adapter/fees`

**Fonctionnalités**:
- Calcul des frais d'opération
- Tarification selon le type d'opération
- Support de différents types de comptes

**Endpoints**:
- `POST /fees/calculate` - Calculer les frais d'opération

### 8. Service de Notifications (`NotificationService`)

**Endpoint**: `/api/v1/cbs-adapter/notifications`

**Fonctionnalités**:
- Envoi d'emails via SMTP
- Templates d'emails personnalisés
- Gestion des pièces jointes

**Endpoints**:
- `POST /notifications/email` - Envoyer un email

### 9. Service de Santé (`HealthService`)

**Endpoint**: `/api/v1/cbs-adapter/health-check`

**Fonctionnalités**:
- Vérification de connectivité avec Amplitude
- Monitoring automatique du système
- Status de santé du service

**Endpoints**:
- `GET /health-check` - Vérification générale du service
- `GET /health-check/cbs` - Vérification de connectivité Amplitude

### 10. Service de Paiements Récurrents (`RecurringPaymentService`)

**Fonctionnalités**:
- Gestion des paiements récurrents
- Planification automatique
- Intégration avec le système Amplitude

## Fonctionnalités Transversales

### Validation des Données
- **ValidAccountNumber**: Annotation de validation pour les numéros de comptes
- **Patterns de validation**: Formats IBAN et numéros de comptes Amplitude
- **Contraintes métier**: Validation selon les règles bancaires

### Mappers et Transformation
- **AccountMapper**: Transformation des données de comptes
- **CurrencyMapper**: Transformation des données de devises
- **BankMapper**: Transformation des données bancaires
- **CustomerMapper**: Transformation des données clients
- **ExchangeRateMapper**: Transformation des taux de change

### Sérialisation/Désérialisation
- **BigDecimalSerializer**: Gestion des montants financiers
- **GenderDeserializer**: Gestion des énumérations de genre
- **InputStreamResourceDeserializer**: Gestion des ressources de fichiers

### Gestion des Erreurs
- **CbsException**: Gestion des erreurs du système Amplitude
- **CbsLogicException**: Gestion des erreurs de logique métier
- **EmailException**: Gestion des erreurs d'envoi d'emails

## Configuration

### Variables d'Environnement Principales

#### Connexion Amplitude
- `AMPLITUDE_URL` - URL du système Amplitude
- `IS_PRODUCTION` - Indicateur d'environnement de production

#### Configuration Bancaire
- `BASE_BANK_CODE` - Code de la banque de base (défaut: 10005)
- `BASE_BANK_NAME` - Nom de la banque (défaut: Afriland First Bank)
- `BASE_CURRENCY` - Devise de base du système

#### Configuration des Comptes
- `CLIENT_ID_LENGTH` - Longueur de l'identifiant client (7)
- Patterns de validation:
  - `IBAN_PATTERN` - Format IBAN complet
  - `FULL_PATTERN` - Format numéro de compte complet
  - `ACCOUNT_NUMBER_PATTERN` - Format numéro de compte
  - `ACCOUNT_KEY_PATTERN` - Format clé de compte

#### Configuration Email
- `SMTP_HOST`, `SMTP_PORT` - Serveur SMTP
- `SMTP_USERNAME`, `SMTP_PASSWORD` - Authentification SMTP
- `SMTP_FROM_NAME` - Nom de l'expéditeur
- `SMTP_ENABLE_AUTH`, `SMTP_START_TLS` - Configuration sécurité SMTP

#### Monitoring
- `SENTRY_ENABLED` - Activation de Sentry
- `SENTRY_DSN_AMPLITUDE_ADAPTER` - DSN Sentry pour ce service

### Fonctionnalités Configurables
- **Health Check**: Vérification toutes les 2 minutes
- **Max Fraction Length**: 4 décimales pour les montants
- **Métriques Prometheus**: Exposition des métriques

## Intégrations Externes

### Système Amplitude
- **Communication**: REST APIs avec le système bancaire Amplitude
- **Formats**: JSON avec validation stricte
- **Mapping**: Transformation des données entre formats PKF et Amplitude

### Services de Notification
- **Email SMTP**: Envoi d'emails avec authentification
- **Templates**: Support de templates personnalisés
- **Pièces jointes**: Gestion des fichiers attachés

## Validation et Sécurité

### Validation des Numéros de Comptes
- **Format IBAN**: `\d{5}-\d{5}-\d{11,12}-\d{2}`
- **Format complet**: `\d{11,12}-\d{2}`
- **Numéro de compte**: `\d{11,12}`
- **Clé de compte**: `\d{2}`

### Validation des Données
- **Contraintes Jakarta**: Validation automatique des requêtes
- **Validation métier**: Règles spécifiques au domaine bancaire
- **Sanitisation**: Nettoyage des données d'entrée

## Monitoring et Observabilité

### Health Checks
- **Service**: `/api/v1/cbs-adapter/health-check`
- **Amplitude**: `/api/v1/cbs-adapter/health-check/cbs`
- **Fréquence**: Vérification automatique toutes les 2 minutes

### Métriques
- **Prometheus**: Exposition des métriques sur `/actuator/prometheus`
- **Métriques métier**: Suivi des opérations bancaires
- **Performance**: Monitoring des temps de réponse

### Logging et Monitoring
- **Sentry**: Monitoring d'erreurs optionnel
- **Log4j2**: Gestion des logs avec rotation
- **Traces**: Suivi des requêtes et réponses

## Types de Données

### Énumérations
- **AccountStatusType**: Statuts des comptes
- **Gender**: Genre des clients
- **HealthStatus**: Statuts de santé du système
- **OperationFeeType**: Types de frais d'opération
- **Periodicity**: Périodicités des opérations

### Structures de Données
- **Comptes**: Informations complètes des comptes clients
- **Devises**: Codes et taux de change
- **Clients**: Profils et informations personnelles
- **Frais**: Calculs et tarifications

## Déploiement

### Configuration par Environnement
- **Profils Spring**: Support de profils multiples
- **Variables d'environnement**: Configuration flexible
- **Production**: Indicateur spécifique pour l'environnement

### Performance
- **Virtual Threads**: Utilisation des threads virtuels Java 21
- **Connection Pooling**: Gestion optimisée des connexions
- **Cache**: Optimisation des requêtes fréquentes

## Maintenance

### Gestion des Formats
- **Patterns configurables**: Adaptation aux différents formats de comptes
- **Validation flexible**: Support de différents types de validation
- **Mapping dynamique**: Transformation adaptable des données

### Intégration Continue
- **Health Checks**: Surveillance continue de la connectivité
- **Métriques**: Monitoring des performances
- **Alertes**: Notification en cas de problème

## Différences avec ABS Adapter

Le service Amplitude Adapter se distingue de l'ABS Adapter par :
- **Système cible**: Intégration spécifique au système Amplitude
- **Formats de données**: Adaptation aux structures Amplitude
- **Fonctionnalités**: Subset focalisé sur les opérations essentielles
- **Configuration**: Paramètres spécifiques à Amplitude
- **Validation**: Règles adaptées aux contraintes Amplitude