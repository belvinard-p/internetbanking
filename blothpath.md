# BlobPath Service Documentation

## Vue d'ensemble

Le service BlobPath est un service de stockage de fichiers cloud-agnostique qui fournit une interface unifiée pour stocker des fichiers sur différents backends de stockage (Microsoft Azure Blob Storage, MinIO, ou système de fichiers local). Il est conçu avec des backends pluggables et une abstraction propre, simplifiant l'intégration du stockage d'objets dans les systèmes distribués et les microservices.

## Architecture

- **Framework**: Spring Boot 3
- **Java Version**: 21
- **Type**: Service de stockage de fichiers
- **Backends supportés**: Azure Blob Storage, MinIO, Système de fichiers local
- **Pattern**: Strategy Pattern pour les différents backends

## Services Principaux

### 1. Service de Fichiers (`FileService`)

**Endpoints**:
- `/api/v1/blobpath/files` (Public)
- `/api/internal/v1/blobpath/files` (Interne)

**Fonctionnalités**:
- Upload de fichiers simples et multiples
- Téléchargement de fichiers avec détection automatique du type MIME
- Génération d'URLs signées pour accès sécurisé
- Suppression de fichiers
- Gestion des métadonnées de fichiers

#### Endpoints Publics

**Téléchargement via URL signée**:
- `GET /api/v1/blobpath/files/signed-url` - Télécharger un fichier via URL signée

#### Endpoints Internes

**Upload de fichiers**:
- `POST /api/internal/v1/blobpath/files` - Upload d'un fichier unique
- `POST /api/internal/v1/blobpath/files/multiple` - Upload de fichiers multiples

**Gestion des fichiers**:
- `GET /api/internal/v1/blobpath/files` - Télécharger un fichier
- `DELETE /api/internal/v1/blobpath/files` - Supprimer un fichier

**URLs signées**:
- `POST /api/internal/v1/blobpath/files/signed-url` - Générer une URL signée

### 2. Service de Stockage Blob (`BlobService`)

**Implémentations**:
- **AzureBlobService**: Intégration avec Azure Blob Storage
- **MinioBlobService**: Intégration avec MinIO
- **FileSystemBlobService**: Stockage sur système de fichiers local

**Fonctionnalités**:
- Upload de fichiers avec génération d'UUID
- Téléchargement de fichiers par identifiant
- Suppression de fichiers
- Gestion des conteneurs/buckets

### 3. Service de Génération d'URLs Signées (`SignedUrlGenerator`)

**Implémentations**:
- **AzureBlobSignedUrlGenerator**: URLs signées Azure
- **MinioSignedUrlGenerator**: URLs signées MinIO
- **FileSystemSignedUrlGenerator**: URLs signées pour système de fichiers

**Fonctionnalités**:
- Génération d'URLs signées avec expiration
- Validation des signatures
- Contrôle d'accès temporaire aux fichiers
- Support de différents types de disposition (inline/attachment)

### 4. Service de Santé (`HealthCheckController`)

**Endpoint**: `/api/v1/blobpath/health-check`

**Fonctionnalités**:
- Vérification de l'état du service
- Monitoring de disponibilité

## Conteneurs de Stockage

### Types de Conteneurs (`BlobContainer`)

1. **AVATAR** (`avatars`) - Photos de profil utilisateurs
2. **CUSTOM_CARD** (`custom-cards`) - Cartes personnalisées
3. **JUSTIFICATION_DOCUMENT** (`justification-documents`) - Documents justificatifs
4. **OPERATION_DOCUMENT** (`operation-documents`) - Documents d'opérations
5. **SETTING** (`settings`) - Fichiers de configuration
6. **SWIFT_TRANSFER** (`swift-transfers`) - Documents de transferts SWIFT
7. **SYSTEM_CONFIG** (`sys-config`) - Configuration système
8. **TICKET** (`tickets`) - Documents de tickets support

## Configuration par Backend

### Azure Blob Storage (Profil: `azure`)

**Variables d'environnement**:
- `AZURE_STORAGE_ACCOUNT_NAME` - Nom du compte de stockage Azure
- `AZURE_STORAGE_ACCOUNT_KEY` - Clé d'accès du compte Azure
- `SIGNED_URL_TTL` - Durée de vie des URLs signées (défaut: 1d)

**Fonctionnalités**:
- Stockage haute disponibilité
- URLs signées natives Azure
- Intégration avec l'écosystème Azure

### MinIO (Profil: `minio`)

**Variables d'environnement**:
- `MINIO_ENDPOINT` - URL du serveur MinIO
- `MINIO_ACCESS_KEY` - Clé d'accès MinIO
- `MINIO_SECRET_KEY` - Clé secrète MinIO
- `MINIO_PART_SIZE` - Taille des parties pour upload (défaut: 10MB)
- `SIGNED_URL_TTL` - Durée de vie des URLs signées (défaut: 1d)

**Fonctionnalités**:
- Compatible S3
- Déploiement on-premise
- Performance optimisée

### Système de Fichiers (Profil: `filesystem`)

**Variables d'environnement**:
- `FILESYSTEM_DESTINATION_DIR` - Répertoire de stockage
- `FILESYSTEM_URL_SIGNING_KEY` - Clé de signature des URLs
- `SIGNED_URL_TTL` - Durée de vie des URLs signées (défaut: 1d)

**Fonctionnalités**:
- Stockage local simple
- Pas de dépendances externes
- URLs signées avec HMAC

## Fonctionnalités Transversales

### Détection de Type MIME
- **TikaContentTypeDetector**: Détection automatique du type de contenu
- **Support**: Tous types de fichiers
- **Sécurité**: Validation du type de fichier

### Validation des Données
- **ValueOfEnum**: Validation des énumérations
- **Contraintes Jakarta**: Validation automatique des requêtes
- **Validation métier**: Vérification des conteneurs et identifiants

### Gestion des Erreurs
- **LocalAppException**: Exceptions spécifiques au service
- **GlobalExceptionHandler**: Gestion centralisée des erreurs
- **ApiErrorResponse**: Format standardisé des erreurs

### Utilitaires
- **AppUtils**: Utilitaires généraux et formatage
- **MimeTypeHelper**: Aide pour les types MIME
- **Base64 et UUID**: Gestion des identifiants

## Configuration Générale

### Variables d'Environnement Principales

#### Configuration Générale
- `PORT` - Port du service
- `APPLICATION_NAME` - Nom de l'application (défaut: BLOBPATH)
- `SPRING_PROFILES_ACTIVE` - Profil actif (azure/minio/filesystem)

#### Limites de Fichiers
- `MAX_FILE_SIZE` - Taille maximale par fichier (défaut: 50MB)
- `MAX_REQUEST_SIZE` - Taille maximale de requête (défaut: 50MB)

#### Timeouts
- `CONNECTION_TIMEOUT` - Timeout de connexion (défaut: 15s)
- `READ_TIMEOUT` - Timeout de lecture (défaut: 15s)

#### Monitoring
- `SENTRY_ENABLED` - Activation de Sentry (défaut: false)
- `SENTRY_DSN` - DSN Sentry pour monitoring

### URLs Signées

#### Paramètres de Signature
- `sig_id` - Identifiant du fichier
- `sig_filename` - Nom du fichier
- `sig_container_name` - Nom du conteneur
- `sig_dir` - Répertoire parent
- `sig_content_disposition` - Type de disposition (inline/attachment)
- `sig_nonce` - Nombre aléatoire pour unicité
- `sig_not_valid_before` - Date de début de validité
- `sig_expires_at` - Date d'expiration
- `sig` - Signature HMAC

#### Sécurité des URLs
- **Expiration**: Contrôle temporel d'accès
- **Signature HMAC**: Validation de l'intégrité
- **Nonce**: Protection contre la réutilisation
- **Validation temporelle**: Fenêtre de validité

## Sécurité

### Contrôle d'Accès
- **URLs signées**: Accès temporaire et sécurisé
- **Validation de signature**: Vérification HMAC
- **Expiration**: Limitation dans le temps
- **Conteneurs isolés**: Séparation logique des données

### Validation des Fichiers
- **Type MIME**: Vérification du type de contenu
- **Taille**: Limitation de la taille des fichiers
- **Nom de fichier**: Validation des caractères autorisés
- **Extension**: Contrôle des extensions de fichiers

## Monitoring et Observabilité

### Health Check
- **Endpoint**: `/api/v1/blobpath/health-check`
- **Réponse**: Message de statut du service

### Logging
- **Log4j2**: Configuration avancée des logs
- **Rotation**: Gestion automatique des fichiers de logs
- **Niveaux**: Support de différents niveaux de log

### Monitoring Externe
- **Sentry**: Monitoring d'erreurs optionnel
- **Métriques**: Suivi des performances
- **Traces**: Traçabilité des requêtes

## Déploiement

### Profils Spring
- **azure**: Déploiement avec Azure Blob Storage
- **minio**: Déploiement avec MinIO
- **filesystem**: Déploiement avec stockage local

### Configuration par Environnement
- **Variables d'environnement**: Configuration flexible
- **Profils**: Adaptation selon l'infrastructure
- **Vault**: Support Azure Key Vault et HashiCorp Vault

### Performance
- **Virtual Threads**: Utilisation des threads virtuels Java 21
- **Streaming**: Upload et download en streaming
- **Cache**: Optimisation des accès fréquents

## Cas d'Usage

### Stockage de Documents
- **Documents justificatifs**: Pièces jointes pour transferts
- **Documents d'opérations**: Reçus et confirmations
- **Documents SWIFT**: Ordres de transfert internationaux

### Gestion des Médias
- **Avatars**: Photos de profil utilisateurs
- **Cartes personnalisées**: Images de cartes bancaires
- **Assets système**: Logos et ressources graphiques

### Configuration
- **Paramètres**: Fichiers de configuration dynamique
- **Templates**: Modèles de documents
- **Ressources système**: Fichiers de configuration

## Avantages

### Flexibilité
- **Multi-backend**: Support de différents systèmes de stockage
- **Cloud-agnostique**: Indépendance vis-à-vis du fournisseur
- **Configuration**: Adaptation selon les besoins

### Sécurité
- **URLs signées**: Accès contrôlé et temporaire
- **Validation**: Vérification des types et tailles
- **Isolation**: Séparation logique des conteneurs

### Performance
- **Streaming**: Gestion efficace des gros fichiers
- **Cache**: Optimisation des accès
- **Parallélisme**: Support des uploads multiples

### Maintenance
- **Abstraction**: Interface unifiée pour tous les backends
- **Monitoring**: Surveillance intégrée
- **Logs**: Traçabilité complète des opérations