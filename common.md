## Services de la Bibliothèque Commune PKF Internet Banking (pkf-ib-be-common-lib)

### 56. SettingsService
**Rôle principal :** Gestion centralisée des paramètres et configurations dynamiques
**Fonctionnalités :**
- Initialisation des propriétés dynamiques depuis le service de paramètres
- Gestion des informations de contact bancaire (adresse, téléphones, réseaux sociaux)
- Mise à jour en temps réel des paramètres via messages de changement
- Gestion des fichiers de branding (logos, arrière-plans)
- Téléchargement et sauvegarde automatique des assets visuels
- Synchronisation des propriétés d'application avec le service externe

### 57. SettingsClient
**Rôle principal :** Client de communication avec le service de paramètres
**Fonctionnalités :**
- Récupération des paramètres depuis le service de settings
- Communication REST avec gestion d'erreurs
- Sérialisation/désérialisation des réponses de paramètres

## Clients d'Adaptateur CBS (Core Banking System)

### 58. AdapterClient
**Rôle principal :** Client principal d'accès aux services CBS
**Fonctionnalités :**
- Agrégation de tous les clients spécialisés CBS
- Point d'entrée unique pour les communications avec le système bancaire central
- Gestion centralisée des connexions aux différents modules CBS

### Clients Spécialisés CBS :

#### 59. AccountClient
**Rôle principal :** Gestion des comptes bancaires via CBS
**Fonctionnalités :**
- Récupération des informations de comptes clients
- Consultation des soldes et historiques
- Gestion des statuts de comptes

#### 60. BankClient
**Rôle principal :** Gestion des informations bancaires
**Fonctionnalités :**
- Récupération des données des banques partenaires
- Synchronisation des informations bancaires

#### 61. BranchClient
**Rôle principal :** Gestion des succursales bancaires
**Fonctionnalités :**
- Récupération des informations de succursales
- Synchronisation des données de succursales

#### 62. CheckbookClient
**Rôle principal :** Gestion des chéquiers via CBS
**Fonctionnalités :**
- Traitement des commandes de chéquiers
- Suivi des statuts de livraison

#### 63. CurrencyClient
**Rôle principal :** Gestion des devises
**Fonctionnalités :**
- Récupération des taux de change
- Gestion des devises supportées

#### 64. CustomerClient
**Rôle principal :** Gestion des clients CBS
**Fonctionnalités :**
- Recherche et récupération d'informations clients
- Validation des données clients

#### 65. TransactionClient
**Rôle principal :** Gestion des transactions bancaires
**Fonctionnalités :**
- Traitement des transactions
- Historique et suivi des opérations

#### 66. TransferClient
**Rôle principal :** Gestion des transferts bancaires
**Fonctionnalités :**
- Exécution des transferts entre comptes
- Validation et autorisation des transferts

## Clients Internes

### 67. AuthClient
**Rôle principal :** Client d'authentification interne
**Fonctionnalités :**
- Vérification des codes OTP pour différents types d'actions
- Communication avec le service d'authentification interne
- Validation des tokens et sessions

### Autres Clients Internes :

#### 68. AlertInternalClient
**Rôle principal :** Gestion interne des alertes
**Fonctionnalités :**
- Envoi d'alertes entre services
- Notification inter-services

#### 69. BlobPathFileInternalClient
**Rôle principal :** Gestion des fichiers et documents
**Fonctionnalités :**
- Upload et téléchargement de fichiers
- Gestion du stockage de documents

#### 70. UserInternalClient
**Rôle principal :** Communication interne pour les utilisateurs
**Fonctionnalités :**
- Échange d'informations utilisateur entre services
- Synchronisation des données utilisateur

## Services de Sérialisation

### 71. CustomLocalDateTimeConverter
**Rôle principal :** Conversion personnalisée des dates et heures
**Fonctionnalités :**
- Sérialisation/désérialisation des LocalDateTime
- Gestion des formats de date personnalisés

### 72. InputStreamResourceSerializer/Deserializer
**Rôle principal :** Sérialisation des ressources de flux
**Fonctionnalités :**
- Conversion des InputStreamResource en JSON
- Gestion des flux de données pour l'API

## Services de Validation

### 73. ValidAccountNumberValidator
**Rôle principal :** Validation des numéros de compte
**Fonctionnalités :**
- Validation du format des numéros de compte
- Vérification de la conformité des identifiants bancaires

### 74. PhoneValidator
**Rôle principal :** Validation des numéros de téléphone
**Fonctionnalités :**
- Validation du format des numéros de téléphone
- Vérification de la conformité internationale

### 75. FieldListValidator
**Rôle principal :** Validation des listes de champs pour rapports
**Fonctionnalités :**
- Validation des champs de rapports
- Vérification de la cohérence des données

## Services d'Autorisation

### 76. JwtTokenHandlerInterceptor
**Rôle principal :** Interception et traitement des tokens JWT
**Fonctionnalités :**
- Validation des tokens JWT dans les requêtes
- Extraction des informations d'autorisation
- Gestion de la sécurité des API

### 77. UserPayloadHolder
**Rôle principal :** Gestion du contexte utilisateur
**Fonctionnalités :**
- Stockage thread-local des informations utilisateur
- Accès sécurisé au contexte d'authentification

Cette bibliothèque commune fournit l'infrastructure de base pour tous les services PKF Internet Banking, incluant la communication avec le CBS, la gestion des paramètres, la validation des données, la sérialisation et l'autorisation. Elle assure la cohérence et la réutilisabilité des composants à travers l'ensemble de l'écosystème bancaire.