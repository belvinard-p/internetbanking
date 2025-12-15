# Gateway Service Documentation

## Vue d'ensemble

Le service Gateway est le point d'entrée central pour l'architecture de microservices PKF Internet Banking. Il s'agit d'une passerelle API basée sur Spring Cloud Gateway qui gère le routage, l'authentification, l'autorisation et la validation des licences pour tous les microservices du système.

## Architecture

- **Framework**: Spring Cloud Gateway (Reactive)
- **Java Version**: 21
- **Type d'application**: Reactive Web Application
- **Documentation API**: OpenAPI/Swagger centralisé

## Services Principaux

### 1. Service de Routage

Le Gateway route les requêtes vers les microservices appropriés selon des règles prédéfinies.

#### Routes Ouvertes (Non protégées)

**Service d'Authentification**:
- `/api/v1/auth/authenticate` - Authentification utilisateur
- `/api/v1/auth/register` - Inscription utilisateur
- `/api/v1/auth/send/code` - Envoi de code de vérification
- `/api/v1/auth/admin/authenticate` - Authentification admin
- `/api/v1/auth/super-admin/authenticate` - Authentification super admin
- `/api/open/v1/auth/**` - APIs publiques d'authentification

**Service de Transactions**:
- `/api/open/v1/transaction/**` - APIs publiques de transactions
- `/api/v1/transaction/transactions/download` - Téléchargement de transactions

**Service Client**:
- `/api/v1/client/health-check` - Vérification de santé

**Service de Paiement**:
- `/api/v1/payment/health-check` - Vérification de santé

**Service de Paramètres**:
- `/api/v1/settings/public/info` - Informations publiques
- `/api/v1/settings/health-check` - Vérification de santé

**Service BlobPath**:
- `/api/v1/blobpath/files/signed-url/**` - URLs signées pour fichiers

#### Routes Protégées (Authentification requise)

**Service d'Authentification**:
- `/api/v1/auth/**` - Toutes les autres APIs d'authentification

**Service de Transactions**:
- `/api/v1/transaction/**` - APIs de gestion des transactions

**Service Client**:
- `/api/v1/client/**` - APIs de gestion des clients

**Service de Paiement**:
- `/api/v1/payment/**` - APIs de gestion des paiements

**Service de Paramètres**:
- `/api/v1/settings/**` - APIs de configuration

### 2. Service d'Authentification (`AuthenticationGatewayFilterFactory`)

**Fonctionnalités**:
- Validation des tokens JWT auprès du service d'authentification
- Vérification via `/api/open/v1/auth/token/verify`
- Transmission des headers de requête pour validation

### 3. Service de Validation de Token (`TokenGatewayFilterFactory`)

**Fonctionnalités**:
- Vérification de la présence du token d'autorisation
- Validation du header `Authorization`
- Retour d'erreur HTTP 401 si token manquant

### 4. Service de Gestion des Licences (`LicenseService`)

**Fonctionnalités**:
- Validation de la validité et de l'expiration des licences
- Cache en mémoire des informations de licence
- Communication avec le service de paramètres
- Surveillance continue de l'état des licences

**Endpoints**:
- Validation automatique pour toutes les requêtes
- Routes autorisées en cas de licence expirée

### 5. Service de Contrôle Global des Licences (`LicenseGlobalFilter`)

**Fonctionnalités**:
- Contrôle de validité des licences (priorité maximale)
- Gestion des routes autorisées en cas de licence expirée
- Permissions spéciales pour les super-admins en lecture seule
- Blocage de la connexion admin si licence invalide

### 6. Service WebSocket

#### Routes WebSocket
- `/auth-websocket/**` - WebSockets d'authentification
- `/client-websocket/**` - WebSockets client avec authentification

**Fonctionnalités**:
- Support des communications temps réel
- Authentification WebSocket via `AddWSAuthorizationHeaderGatewayFilterFactory`
- Nettoyage automatique des paramètres d'autorisation

### 7. Service de Documentation API Centralisée

**Endpoint**: `/swagger-ui.html`

**Services intégrés**:
- API Gateway Service
- Auth Service (`/auth/internal/v3/api-docs`)
- Transaction Service (`/transaction/internal/v3/api-docs`)
- Client Service (`/client/internal/v3/api-docs`)
- Payment Service (`/payment/internal/v3/api-docs`)
- Settings Service (`/settings/internal/v3/api-docs`)

### 8. Service de Health Check

**Endpoint**: `/gateway/health-check`
**Réponse**: "Service is up"
**Utilisation**: Monitoring et vérification de disponibilité

### 9. Service de Gestion CORS

**Configuration**:
- Origins autorisées: `*`
- Headers autorisés: `*`
- Méthodes: GET, POST, PUT, DELETE, HEAD, OPTIONS, PATCH, TRACE
- Appliqué à tous les endpoints (`[/**]`)

## Filtres et Middleware

### Filtres de Sécurité
- **Token**: Vérification de présence du token
- **Authentication**: Validation du token JWT
- **LicenseGlobalFilter**: Contrôle des licences

### Filtres de Transformation
- **AddRequestHeader**: Ajout de headers de traçabilité
- **RemoveRequestHeader**: Suppression de headers sensibles
- **AddWSAuthorizationHeader**: Gestion des headers WebSocket

## Configuration

### Variables d'Environnement

#### Services Backend
- `AUTH_URI` - URI du service d'authentification
- `TRANSACTION_URI` - URI du service de transactions
- `CLIENT_URI` - URI du service client
- `PAYMENT_URI` - URI du service de paiement
- `SETTINGS_URI` - URI du service de paramètres
- `BLOB_PATH_URI` - URI du service BlobPath

#### WebSockets
- `AUTH_URI_WS` - URI WebSocket du service d'authentification
- `CLIENT_URI_WS` - URI WebSocket du service client

#### Configuration Générale
- `PORT` - Port du service Gateway
- `SUPPORTED_LANGUAGES` - Langues supportées (en,fr,pt)

#### Gestion des Licences
- `LICENSE_ENABLED` - Activation du contrôle de licence
- `ADMIN_LOGIN_URI` - URI de connexion admin

### Routes d'Exception pour Licence Expirée
- Authentification super-admin
- Gestion des licences
- Health checks de tous les services
- Documentation API Swagger

## Sécurité

### Authentification Multi-niveaux
1. **Validation de Token**: Vérification de présence du token JWT
2. **Authentification**: Validation du token auprès du service d'auth
3. **Licence**: Contrôle de validité de licence système

### Gestion des Permissions
- **Utilisateurs standards**: Accès selon permissions JWT
- **Super-admins**: Accès en lecture seule même avec licence expirée
- **Admins**: Blocage de connexion si licence invalide

### Headers de Sécurité
- **X-Forwarded-Header**: Ajouté pour traçabilité
- **Nettoyage**: Suppression des headers sensibles

## Gestion des Erreurs

### Types d'Exceptions
- **AuthException**: Erreurs d'authentification (401)
- **ForwardErrorException**: Erreurs de transmission vers services backend
- **InvalidLicenseException**: Erreurs de licence invalide

### Gestionnaire Global
- **GatewayControllerAdvice**: Gestion centralisée des erreurs
- **Réponses standardisées**: Format uniforme pour toutes les erreurs

## Monitoring et Observabilité

### Health Checks
- **Gateway**: `/gateway/health-check`
- **Services**: Routage vers health checks de chaque service

### Monitoring Externe
- **Sentry**: Intégration optionnelle pour monitoring d'erreurs
- **Traces**: Échantillonnage à 100% des traces

## Déploiement

### Configuration par Environnement
- **Profils Spring**: Support de profils multiples
- **Vault**: Support Azure Key Vault et HashiCorp Vault
- **Variables**: Configuration via variables d'environnement

### Haute Disponibilité
- **Reactive**: Architecture non-bloquante pour haute performance
- **Load Balancing**: Gestion automatique de la charge (`loadbalancer.use404: true`)
- **Failover**: Gestion des pannes de services backend