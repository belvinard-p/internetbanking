# Payment Service Documentation

## Vue d'ensemble

Le service de paiement fournit des ressources API pour traiter les transferts et les paiements dans le système bancaire PKF Internet Banking. Il s'agit d'un microservice Spring Boot qui gère toutes les opérations financières, y compris les paiements, les transferts, les prêts, les devises et les statistiques.

## Architecture

- **Framework**: Spring Boot 3
- **Java Version**: 21
- **Base de données**: PostgreSQL
- **Cache**: Redis
- **Documentation API**: OpenAPI/Swagger

## Services Principaux

### 1. Service de Paiements (`PaymentService`)

**Endpoint**: `/api/v1/payment/payments`

**Fonctionnalités**:
- Création de paiements
- Récupération des paiements par ID
- Consultation des derniers paiements
- Support des paiements récurrents

**Endpoints**:
- `POST /payments` - Créer un paiement
- `GET /payments/{id}` - Obtenir un paiement par ID
- `GET /payments/last` - Obtenir les derniers paiements

### 2. Service de Transferts (`TransferService`)

**Endpoint**: `/api/v1/payment/transfers`

**Fonctionnalités**:
- Transferts simples et multiples
- Transferts via fichier CSV
- Transferts différés/programmés
- Validation des transferts multiples
- Téléchargement de documents justificatifs

**Endpoints**:
- `POST /transfers` - Créer des transferts
- `POST /transfers/csv` - Créer des transferts via CSV
- `PUT /transfers/{id}/deferred` - Modifier un transfert différé
- `GET /transfers/deferred` - Récupérer les transferts différés
- `DELETE /transfers/{id}/deferred` - Supprimer un transfert différé
- `POST /transfers/multiple/validate` - Valider des transferts multiples
- `GET /transfers/{id}/justification-documents` - Télécharger les documents

### 3. Service de Devises (`CurrencyService`)

**Endpoint**: `/api/v1/payment/currencies`

**Fonctionnalités**:
- Consultation des taux de change
- Génération de PDF des taux de change
- Demandes d'échange de devises

**Endpoints**:
- `GET /currencies/rates` - Obtenir les taux de change
- `GET /currencies/rates/pdf` - Générer un PDF des taux

### 4. Service de Prêts (`LoanService`)

**Endpoint**: `/api/v1/payment/loans`

**Fonctionnalités**:
- Consultation des prêts
- Gestion des paiements de prêts
- Synchronisation avec le CBS

**Endpoints**:
- `GET /loans` - Récupérer tous les prêts
- `GET /loans/{id}/payments` - Obtenir les paiements d'un prêt

### 5. Service de Taxes (`TaxService`)

**Endpoint**: `/api/v1/payment/taxes`

**Fonctionnalités**:
- Validation des taxes
- Confirmation des paiements de taxes

**Endpoints**:
- `POST /taxes/validate` - Valider une taxe
- `POST /taxes/confirm-payment` - Confirmer le paiement d'une taxe

### 6. Service de Frais d'Opération (`OperationFeesService`)

**Endpoint**: `/api/v1/payment/fees`

**Fonctionnalités**:
- Calcul des frais d'opération

**Endpoints**:
- `POST /fees/calculate` - Calculer les frais d'opération

### 7. Service de Factures d'Abonnement (`SubscriptionBillService`)

**Endpoint**: `/api/v1/payment/subscription-bills`

**Fonctionnalités**:
- Consultation des factures d'abonnement
- Paiement des factures

**Endpoints**:
- `GET /subscription-bills` - Obtenir les factures d'abonnement
- `PUT /subscription-bills/{id}/pay` - Payer une facture par ID

### 8. Service de Statistiques (`StatisticService`)

**Endpoints**: 
- `/api/v1/payment/statistic/aggregator`
- `/api/v1/payment/statistic/bills`
- `/api/v1/payment/statistic/subscriptions`

**Fonctionnalités**:
- Statistiques agrégées
- Statistiques des factures
- Statistiques des abonnements

**Endpoints**:
- `GET /statistic/aggregator` - Obtenir les statistiques agrégées

### 9. Service d'Ordres SWIFT (`SwiftOrderService`)

**Endpoint**: `/api/v1/payment/swift-orders`

**Fonctionnalités**:
- Gestion des ordres de transfert SWIFT internationaux

### 10. Service de Dépôts (`DepositService`)

**Endpoint**: `/api/v1/payment/deposits`

**Fonctionnalités**:
- Gestion des types de dépôts

### 11. Services Internes

**Endpoints**:
- `/api/internal/v1/payment/funds-reservations` - Réservation de fonds
- `/api/internal/v1/payment/fees` - Frais pour clients internes
- `/api/internal/v1/payment/transfers` - Transferts internes

## Services d'Administration

### 1. Service de Produits de Prêt (`LoanProductService`)

**Fonctionnalités**:
- Gestion des produits de prêt
- Configuration des conditions de prêt

### 2. Service de Demandes d'Échange de Devises (`CurrencyExchangeRequestService`)

**Fonctionnalités**:
- Traitement des demandes d'échange de devises
- Approbation/rejet des demandes

## Fonctionnalités Transversales

### Authentification et Autorisation
- Intégration avec le service d'authentification
- Contrôle d'accès basé sur les rôles (USER, MAIN_SUB_USER, SUB_USER)
- Permissions granulaires pour chaque opération

### Notifications
- Notifications par email et SMS
- Configurable via les variables d'environnement

### Planification et Tâches Automatisées
- Synchronisation des devises
- Traitement des paiements récurrents
- Mise à jour des taux de change
- Traitement des factures automatiques

### Intégrations Externes
- **CBS Adapter**: Interface avec le système bancaire central
- **Blob Path Service**: Stockage de fichiers (Azure Blob/MinIO)
- **Settings Service**: Configuration dynamique
- **Transaction Service**: Historique des transactions
- **User Service**: Gestion des utilisateurs

### Gestion des Fichiers
- Support des documents justificatifs
- Téléchargement de fichiers CSV pour les transferts en lot
- Génération de PDF pour les rapports

### Validation et Sécurité
- Validation des données d'entrée
- Gestion des erreurs centralisée
- Logging et monitoring avec Sentry

## Configuration

### Variables d'Environnement Principales
- `PORT` - Port du service
- `DB_URL`, `DB_USERNAME`, `DB_PASSWORD` - Configuration base de données
- `REDIS_HOST`, `REDIS_PORT`, `REDIS_PASSWORD` - Configuration Redis
- `CBS_ADAPTER_URI` - URI de l'adaptateur CBS
- `AUTH_URI`, `TRANSACTION_URI`, `USER_URI` - URIs des autres services

### Fonctionnalités Configurables
- `FEATURE_SWIFT_DISABLED` - Désactiver les fonctionnalités SWIFT
- `FEATURE_NRA_DISABLED` - Désactiver les fonctionnalités de taxes
- `CROSS_CURRENCY_PAYMENT_ENABLED` - Paiements inter-devises
- `FUNDS_RESERVATION_ENABLED` - Réservation de fonds

## Surveillance et Maintenance

### Health Check
- Endpoint: `/api/v1/payment/health-check`
- Vérification de l'état du service

### Documentation API
- Swagger UI: `/payment/internal/swagger-ui.html`
- API Docs: `/payment/internal/v3/api-docs`

### Logs
- Logs rotatifs dans le répertoire `/logs`
- Configuration Log4j2 pour la gestion des logs

## Déploiement

### Docker
- Image Docker disponible
- Support Docker Compose avec dépendances

### Environnements
- Configuration par profils Spring
- Support Azure Key Vault et HashiCorp Vault

## Sécurité

### Authentification
- JWT tokens via le service d'authentification
- Validation des tokens pour les routes protégées

### Permissions
- Contrôle d'accès granulaire
- Séparation des permissions utilisateur/admin
- Support des sous-utilisateurs avec permissions limitées

### Audit
- Traçabilité des opérations financières
- Logs d'audit pour les demandes d'échange de devises