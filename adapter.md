# ABS Adapter Service Documentation

## Vue d'ensemble

Le service ABS Adapter est un adaptateur qui fait l'interface entre le système PKF Internet Banking et le système bancaire central (ABS - Automated Banking System). Il traduit les requêtes du système Internet Banking vers les APIs du système bancaire central et vice versa.

## Architecture

- **Framework**: Spring Boot 3
- **Java Version**: 21
- **Type**: Service d'adaptation/intégration
- **Communication**: REST APIs avec signature cryptographique

## Services Principaux

### 1. Service de Comptes (`AccountService`)

**Endpoint**: `/api/v1/cbs-adapter/accounts`

**Fonctionnalités**:
- Récupération des comptes clients
- Consultation des soldes de comptes
- Validation des numéros de comptes

**Endpoints**:
- `GET /accounts?clientCode={code}` - Obtenir les comptes d'un client
- `POST /accounts/balance` - Obtenir les soldes de comptes

### 2. Service de Transferts (`TransferService`)

**Endpoint**: `/api/v1/cbs-adapter/transfers`

**Fonctionnalités**:
- Création de transferts simples
- Création de transferts multiples
- Validation de transferts multiples
- Support des différents types de transferts (même agence, agences différentes, externe)

**Endpoints**:
- `POST /transfers` - Créer un transfert
- `POST /transfers/multiple` - Créer des transferts multiples
- `POST /transfers/multiple/validate` - Valider des transferts multiples

### 3. Service de Devises (`CurrencyService`)

**Endpoint**: `/api/v1/cbs-adapter/currencies`

**Fonctionnalités**:
- Liste des devises supportées
- Taux de change en temps réel
- Configuration des devises autorisées

**Endpoints**:
- `GET /currencies` - Lister les devises supportées
- `GET /currencies/rates` - Obtenir les taux de change

### 4. Service de Prêts (`LoanService`)

**Endpoint**: `/api/v1/cbs-adapter/loans`

**Fonctionnalités**:
- Récupération des prêts clients
- Informations détaillées sur les prêts
- Historique des paiements

**Endpoints**:
- `GET /loans?cbsClientId={id}` - Récupérer les prêts d'un client

### 5. Service de Frais d'Opération (`OperationFeesService`)

**Endpoint**: `/api/v1/cbs-adapter/fees`

**Fonctionnalités**:
- Calcul des frais d'opération
- Tarification dynamique selon le type d'opération
- Support de différents types de comptes

**Endpoints**:
- `POST /fees/calculate` - Calculer les frais d'opération

### 6. Service de Notifications (`NotificationService`)

**Endpoint**: `/api/v1/cbs-adapter/notifications`

**Fonctionnalités**:
- Envoi de SMS
- Envoi d'emails avec templates
- Support multilingue
- Gestion des pièces jointes

**Endpoints**:
- `POST /notifications/sms` - Envoyer un SMS
- `POST /notifications/email` - Envoyer un email

### 7. Service de Banques (`BankService`)

**Endpoint**: `/api/v1/cbs-adapter/banks`

**Fonctionnalités**:
- Liste des banques
- Informations sur les agences
- Codes bancaires et SWIFT

### 8. Service de Clients (`CustomerService`)

**Endpoint**: `/api/v1/cbs-adapter/clients`

**Fonctionnalités**:
- Informations clients
- Validation des données clients
- Gestion des profils clients

### 9. Service de Carnets de Chèques (`CheckbookService`)

**Endpoint**: `/api/v1/cbs-adapter/checkbooks`

**Fonctionnalités**:
- Demande de carnets de chèques
- Types de carnets disponibles
- Gestion des commandes

### 10. Service de Dépôts (`DepositService`)

**Endpoint**: `/api/v1/cbs-adapter/deposits`

**Fonctionnalités**:
- Types de dépôts disponibles
- Conditions de dépôt
- Taux d'intérêt

### 11. Service SWIFT (`SwiftService`)

**Endpoint**: `/api/v1/cbs-adapter/swift`

**Fonctionnalités**:
- Transferts internationaux SWIFT
- Devises SWIFT supportées
- Validation des ordres SWIFT

### 12. Service de Taxes (`TaxService`)

**Endpoint**: `/api/v1/cbs-adapter/tax`

**Fonctionnalités**:
- Validation des taxes NRA
- Confirmation des paiements de taxes
- Intégration avec le système fiscal

### 13. Service de Transactions (`TransactionService`)

**Endpoint**: `/api/v1/cbs-adapter/transactions`

**Fonctionnalités**:
- Historique des transactions
- Recherche de transactions
- Export de données

### 14. Service de Paiements Récurrents (`RecurringPaymentService`)

**Endpoint**: `/api/v1/cbs-adapter/recurring-payments`

**Fonctionnalités**:
- Gestion des paiements récurrents
- Planification automatique
- Annulation et modification

### 15. Service de Réservation de Fonds (`FundsReservationService`)

**Endpoint**: `/api/v1/cbs-adapter/reservations`

**Fonctionnalités**:
- Réservation de fonds pour opérations
- Libération de réservations
- Gestion des timeouts

### 16. Service de Santé (`HealthService`)

**Endpoint**: `/api/v1/cbs-adapter/health-check`

**Fonctionnalités**:
- Vérification de connectivité ABS
- Monitoring automatique
- Alertes en cas de panne

## Fonctionnalités Transversales

### Sécurité et Signature
- **SignatureService**: Signature cryptographique des requêtes ABS
- **Clé privée**: Authentification sécurisée avec le système ABS
- **Secret partagé**: Validation de l'intégrité des messages

### Gestion des Erreurs
- **CbsException**: Gestion des erreurs du système bancaire central
- **NraException**: Gestion des erreurs du système fiscal
- **EmailException**: Gestion des erreurs d'envoi d'emails

### Mappers et Transformation
- **AccountMapper**: Transformation des données de comptes
- **TransferMapper**: Transformation des données de transferts
- **CurrencyMapper**: Transformation des données de devises
- **LoanMapper**: Transformation des données de prêts
- **TransactionMapper**: Transformation des données de transactions

### Sérialisation/Désérialisation
- **BigDecimalSerializer**: Gestion des montants financiers
- **DateTimeMapper**: Gestion des dates et heures
- **EnumDeserializers**: Gestion des énumérations métier

## Configuration

### Variables d'Environnement Principales

#### Connexion ABS
- `ABS_URI` - URI du système bancaire central
- `ABS_PRIVATE_KEY` - Clé privée pour signature
- `ABS_SECRET` - Secret partagé pour authentification

#### Configuration Bancaire
- `BANK_NAME` - Nom de la banque
- `BASE_CURRENCY` - Devise de base
- `ALLOWED_CURRENCIES` - Devises autorisées

#### Codes d'Opération
- `DIFFERENT_BRANCH_TRANSFER_OPERATION_CODE` - Transfert inter-agences
- `SAME_CUSTOMER_TRANSFER_OPERATION_CODE` - Transfert même client
- `EXTERNAL_TRANSFER_OPERATION_CODE` - Transfert externe
- `SWIFT_TRANSFER_OPERATION_CODE` - Transfert SWIFT
- `TAX_OPERATION_CODE` - Opération fiscale

#### Configuration Email
- `SMTP_HOST`, `SMTP_PORT` - Serveur SMTP
- `SMTP_USERNAME`, `SMTP_PASSWORD` - Authentification SMTP
- `SMTP_FROM_EMAIL`, `SMTP_FROM_NAME` - Expéditeur par défaut

#### Cache et Stockage
- `REDIS_HOST`, `REDIS_PORT`, `REDIS_PASSWORD` - Configuration Redis
- `AZURE_STORAGE_ACCOUNT_NAME`, `AZURE_STORAGE_ACCOUNT_KEY` - Stockage Azure

### Fonctionnalités Configurables
- `DAILY_TRANSACTIONS_ENABLED` - Activation des transactions quotidiennes
- `CBS_HEALTH_CHECK_UP_MESSAGE` - Message de santé du CBS
- `CONNECTION_TIMEOUT`, `READ_TIMEOUT` - Timeouts de connexion

## Intégrations Externes

### Système Bancaire Central (ABS)
- **Communication**: REST APIs avec signature HMAC
- **Authentification**: Clé privée et secret partagé
- **Formats**: JSON avec validation stricte

### Système Fiscal (NRA)
- **Client NRA**: Intégration avec le système fiscal national
- **Validation**: Vérification des taxes en temps réel
- **Confirmation**: Paiement des obligations fiscales

### Services de Notification
- **Email**: SMTP avec templates Thymeleaf
- **SMS**: Intégration avec fournisseurs SMS
- **Multilingue**: Support français, anglais, portugais

### Stockage de Fichiers
- **Azure Blob Storage**: Stockage des documents
- **BlobPath Service**: Gestion des URLs signées

## Monitoring et Observabilité

### Health Checks
- **CBS Health Check**: Vérification toutes les 2 minutes
- **Endpoint**: `/api/v1/cbs-adapter/health-check`
- **Métriques**: Exposition Prometheus

### Logging et Monitoring
- **Sentry**: Monitoring d'erreurs optionnel
- **Log4j2**: Gestion des logs avec rotation
- **Métriques**: Exposition des métriques métier

## Sécurité

### Authentification
- **Signature HMAC**: Toutes les requêtes vers ABS sont signées
- **Validation**: Vérification de l'intégrité des réponses
- **Timeouts**: Protection contre les attaques de déni de service

### Validation des Données
- **Patterns de validation**: Numéros de comptes, montants
- **Contraintes métier**: Limites de transfert, devises autorisées
- **Sanitisation**: Nettoyage des données d'entrée

## Déploiement

### Configuration par Environnement
- **Profils Spring**: Support de profils multiples
- **Vault**: Support Azure Key Vault et HashiCorp Vault
- **Variables**: Configuration via variables d'environnement

### Performance
- **Virtual Threads**: Utilisation des threads virtuels Java 21
- **Cache Redis**: Mise en cache des données fréquentes
- **Connection Pooling**: Gestion optimisée des connexions

## Maintenance

### Codes d'Opération
- **Configuration**: Codes métier configurables par environnement
- **Mapping**: Correspondance avec les codes ABS
- **Validation**: Vérification de cohérence

### Gestion des Templates
- **Thymeleaf**: Templates d'emails dynamiques
- **Multilingue**: Support de plusieurs langues
- **Cache**: Mise en cache des templates compilés