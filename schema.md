# PKF Internet Banking Database Schema Documentation

## Vue d'ensemble

Le schéma de base de données PKF Internet Banking est une base de données PostgreSQL complète qui gère toutes les entités et relations du système bancaire en ligne. Il utilise Liquibase pour la gestion des migrations et contient plus de 50 tables couvrant tous les aspects du système bancaire numérique.

## Architecture

- **SGBD**: PostgreSQL
- **Gestion des migrations**: Liquibase
- **Versioning**: 212+ changesets de migration
- **Audit**: Système d'audit automatique intégré
- **Sécurité**: Contrôle d'accès granulaire par service

## Domaines Fonctionnels

### 1. Gestion des Utilisateurs

#### Tables Principales
- **users** - Utilisateurs principaux du système
- **sub_user_attributes** - Attributs des sous-utilisateurs
- **admin_roles** - Rôles administrateurs
- **admin_roles_permissions** - Permissions des rôles admin
- **users_permissions** - Permissions individuelles des utilisateurs

#### Fonctionnalités
- Authentification multi-facteurs (MFA)
- Gestion des rôles et permissions
- Support des utilisateurs corporatifs
- Système de sous-utilisateurs avec validateurs
- Profils utilisateurs complets (nom, email, téléphone, adresse)
- Gestion des avatars et préférences

### 2. Authentification et Sécurité

#### Tables Principales
- **two_factor_authentications** - Authentification à deux facteurs
- **user_totp_settings** - Configuration TOTP
- **user_backup_codes** - Codes de sauvegarde
- **user_blockers** - Blocage des utilisateurs
- **user_sessions** - Sessions utilisateurs
- **devices** - Appareils enregistrés

#### Fonctionnalités
- MFA par SMS, Email et TOTP
- Codes de sauvegarde pour récupération
- Blocage automatique après échecs
- Gestion des sessions et appareils
- Audit des tentatives de connexion

### 3. Comptes et Finances

#### Tables Principales
- **accounts** - Comptes bancaires
- **users_accounts** - Association utilisateurs-comptes
- **currency** - Devises supportées
- **exchange_rates** - Taux de change
- **transactions** - Historique des transactions
- **transaction_categories** - Catégories de transactions

#### Fonctionnalités
- Multi-devises avec taux de change dynamiques
- Comptes avec limites et contraintes
- Historique complet des transactions
- Catégorisation automatique
- Soldes en temps réel
- Comptes cachés pour administration

### 4. Transferts et Paiements

#### Tables Principales
- **transfers** - Transferts entre comptes
- **payments** - Paiements vers bénéficiaires
- **recurring_payments** - Paiements récurrents
- **swift_transfers** - Transferts internationaux SWIFT
- **beneficiaries** - Bénéficiaires de paiements

#### Fonctionnalités
- Transferts internes et externes
- Paiements programmés et récurrents
- Transferts SWIFT internationaux
- Gestion des bénéficiaires
- Documents justificatifs
- Validation multi-niveaux

### 5. Opérations Financières

#### Tables Principales
- **financial_operation_histories** - Historique des opérations
- **financial_operation_orders** - Ordres d'opérations
- **user_operation_approves** - Approbations d'opérations
- **bulk_financial_operation_details** - Opérations en lot

#### Fonctionnalités
- Workflow d'approbation configurable
- Opérations en lot (CSV)
- Traçabilité complète
- Validation par plusieurs utilisateurs
- Statuts détaillés des opérations

### 6. Produits et Services

#### Tables Principales
- **packages** - Packages de services
- **package_pricing** - Tarification des packages
- **subscriptions** - Abonnements utilisateurs
- **subscriptions_bills** - Factures d'abonnement
- **products** - Produits bancaires
- **products_accounts** - Comptes de produits

#### Fonctionnalités
- Packages de services configurables
- Tarification multi-devises
- Facturation automatique
- Période de grâce
- Produits bancaires variés

### 7. Prêts et Crédits

#### Tables Principales
- **loans** - Prêts accordés
- **loan_parents** - Catégories de prêts
- **loan_products** - Produits de prêt
- **loan_payments** - Paiements de prêts

#### Fonctionnalités
- Gestion complète des prêts
- Échéanciers de paiement
- Calcul automatique des intérêts
- Suivi des remboursements
- Produits de prêt configurables

### 8. Services Spécialisés

#### Tables Principales
- **taxes** - Paiements de taxes
- **checkbook_requests** - Demandes de carnets de chèques
- **checkbook_types** - Types de carnets
- **custom_cards** - Cartes personnalisées
- **card_requests** - Demandes de cartes
- **flash_cashes** - Crédits flash

#### Fonctionnalités
- Paiement de taxes NRA
- Commande de carnets de chèques
- Cartes bancaires personnalisées
- Crédits instantanés
- Workflow d'approbation

### 9. Change et Devises

#### Tables Principales
- **currency_exchange_requests** - Demandes de change
- **currency_exchange_request_audit_logs** - Audit des changes
- **swift_currencies** - Devises SWIFT
- **deposit_types** - Types de dépôts

#### Fonctionnalités
- Demandes de change de devises
- Audit complet des taux
- Support SWIFT international
- Dépôts à terme
- Validation administrative

### 10. Support et Tickets

#### Tables Principales
- **tickets** - Tickets de support
- **internal_notes** - Notes internes
- **user_documents** - Documents utilisateurs

#### Fonctionnalités
- Système de tickets complet
- Notes internes pour support
- Gestion de documents
- Suivi des résolutions
- Communication client-support

### 11. Alertes et Notifications

#### Tables Principales
- **alerts** - Alertes système
- **user_alerts** - Alertes utilisateurs
- **statistics** - Statistiques système

#### Fonctionnalités
- Système d'alertes configurable
- Notifications personnalisées
- Statistiques en temps réel
- Métriques de performance
- Rapports automatiques

### 12. Référentiels

#### Tables Principales
- **banks** - Banques partenaires
- **branches** - Agences bancaires
- **countries** - Pays supportés
- **cbs_account_infos** - Informations CBS

#### Fonctionnalités
- Référentiel des banques
- Gestion des agences
- Support international
- Intégration CBS
- Données de référence

## Fonctionnalités Transversales

### Audit et Traçabilité
- **audit_log** - Logs d'audit automatiques
- **change_table_histories** - Historique des modifications
- Traçabilité complète des opérations
- Logs de sécurité détaillés

### Gestion des Permissions
- **permissions** - Permissions système
- **packages_permissions** - Permissions par package
- Contrôle d'accès granulaire
- Permissions par type (CLIENT/ADMIN)

### Synchronisation
- **sync_data** - Données de synchronisation
- **funds_reservations** - Réservations de fonds
- Synchronisation avec systèmes externes
- Gestion des réservations temporaires

### Téléchargements
- **transaction_downloads** - Téléchargements de transactions
- URLs temporaires sécurisées
- Expiration automatique

## Gestion des Migrations

### Liquibase
- **212+ changesets** organisés chronologiquement
- **Rollback** automatique en cas d'erreur
- **Validation** des schémas avant déploiement
- **Historique** complet des modifications

### Structure des Migrations
```
01-init-roles.sql          - Rôles initiaux
02-init.sql               - Schéma de base
03-212-*.sql              - Évolutions chronologiques
```

### Types de Migrations
- **Création de tables** - Nouvelles entités
- **Modifications de colonnes** - Évolutions de structure
- **Ajout d'index** - Optimisations de performance
- **Contraintes** - Règles de cohérence
- **Données de référence** - Données initiales

## Sécurité et Accès

### Contrôle d'Accès par Service
- **auth_service** - Authentification et utilisateurs
- **payment_service** - Paiements et transferts
- **user_service** - Gestion des utilisateurs
- **transaction_service** - Historique des transactions

### Permissions Granulaires
- **SELECT/INSERT/UPDATE/DELETE** par table
- **Colonnes spécifiques** selon les besoins
- **Contraintes de sécurité** automatiques

### Audit Automatique
- **Trigger-based auditing** sur tables sensibles
- **Logs détaillés** des modifications
- **Traçabilité utilisateur** complète

## Types de Données Spécialisés

### Énumérations PostgreSQL
- **account_status** - Statuts des comptes
- **transfer_status** - Statuts des transferts
- **payment_status** - Statuts des paiements
- **user_mfa_type** - Types de MFA
- **operation_type** - Types d'opérations
- **Et 50+ autres énumérations**

### Types JSON/JSONB
- **Métadonnées flexibles** pour extensions
- **Configuration dynamique** des produits
- **Stockage de documents** structurés

## Performance et Optimisation

### Index Stratégiques
- **Index composites** sur clés fréquentes
- **Index partiels** pour optimisations
- **Contraintes uniques** pour intégrité

### Partitioning
- **Partitioning par date** pour gros volumes
- **Archivage automatique** des anciennes données

## Maintenance et Monitoring

### Statistiques Intégrées
- **Métriques de performance** en temps réel
- **Rapports d'utilisation** automatiques
- **Alertes système** configurables

### Sauvegarde et Récupération
- **Backups automatiques** quotidiens
- **Point-in-time recovery** disponible
- **Réplication** pour haute disponibilité

## Évolution et Extensibilité

### Design Modulaire
- **Séparation par domaines** fonctionnels
- **APIs de service** bien définies
- **Extensibilité** pour nouveaux produits

### Compatibilité
- **Backward compatibility** maintenue
- **Migration progressive** des données
- **Support multi-versions** temporaire

Ce schéma de base de données constitue le cœur du système PKF Internet Banking, offrant une base solide, sécurisée et évolutive pour tous les services bancaires numériques.