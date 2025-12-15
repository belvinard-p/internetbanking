## Services du Projet PKF Internet Banking Settings Service (pkf-ib-be-settings-service)

### 111. SettingsService
**Rôle principal :** Gestion centralisée des paramètres et configurations système
**Fonctionnalités :**
- Gestion des paramètres par catégorie avec pagination et filtrage
- Upload et gestion des éléments de branding (logos, arrière-plans, bannières)
- Validation des dimensions et formats d'images pour le branding
- Gestion des informations de contact bancaire (adresses, téléphones, réseaux sociaux)
- Génération d'URLs signées pour l'accès sécurisé aux fichiers
- Cache intelligent des URLs avec gestion de l'expiration
- Substitution automatique par des fichiers génériques lors de suppression
- Gestion de l'historique des paramètres avec versioning
- Support des paramètres publics et privés selon les rôles utilisateur
- Initialisation des paramètres depuis des propriétés externes

### 112. SettingsPublisherService
**Rôle principal :** Publication des changements de paramètres via Redis
**Fonctionnalités :**
- Publication des modifications de branding en temps réel
- Notification des changements d'informations de contact
- Diffusion des mises à jour d'informations bancaires
- Utilisation de Redis Pub/Sub pour la synchronisation inter-services
- Messages structurés pour différents types de changements
- Logging détaillé des publications pour audit

### 113. LicenseService
**Rôle principal :** Gestion complète des licences système
**Fonctionnalités :**
- Upload et validation des fichiers de licence chiffrés
- Décryptage des licences avec clés privées RSA
- Vérification des signatures numériques avec clés publiques
- Validation de l'émetteur et de la période de validité
- Gestion des statuts de licence (valide, expirée, invalide, inconnue)
- Cache en mémoire des licences actives pour performance
- Désactivation automatique des anciennes licences
- Suivi des notifications d'expiration envoyées
- Intégration avec le stockage de fichiers sécurisé

### 114. BankInfoService
**Rôle principal :** Gestion des informations bancaires publiques
**Fonctionnalités :**
- Gestion des URLs "À propos" de la banque
- Mise à jour des informations institutionnelles
- Publication automatique des changements d'informations bancaires
- Gestion de l'historique des modifications
- Validation des URLs et formats de données

### 115. ResourceInitializerService
**Rôle principal :** Initialisation des ressources système au démarrage
**Fonctionnalités :**
- Upload automatique des ressources génériques (logos, arrière-plans)
- Vérification de l'existence des fichiers avant upload
- Gestion des IDs fixes pour les ressources système
- Initialisation conditionnelle pour éviter les doublons
- Gestion des erreurs d'upload avec logging détaillé

### 116. UserClient
**Rôle principal :** Client pour récupération d'informations utilisateur
**Fonctionnalités :**
- Récupération des noms d'utilisateurs pour audit des modifications
- Cache des informations utilisateur pour optimiser les performances
- Formatage des noms complets utilisateur
- Gestion des erreurs de communication avec le service utilisateur
- Support des utilisateurs inexistants ou supprimés

## Services de Planification

### 117. LicenseMonitor
**Rôle principal :** Surveillance automatique des licences système
**Fonctionnalités :**
- Validation périodique des licences avec cron configurable
- Détection des licences expirées ou invalides
- Notifications automatiques par email avant expiration
- Gestion des intervalles de notification pour éviter le spam
- Support multilingue pour les notifications
- Surveillance de l'émetteur de licence pour sécurité
- Formatage des dates d'expiration selon les locales
- Gestion des erreurs de validation avec logging approprié

## Utilitaires et Validation

### 118. ImageDimensionsValidator
**Rôle principal :** Validation des dimensions d'images pour branding
**Fonctionnalités :**
- Validation des dimensions selon le type de branding
- Vérification des ratios d'aspect pour logos et bannières
- Support de différents formats d'image (PNG, JPEG)
- Configuration flexible des contraintes de taille

### 119. SettingsValueValidator
**Rôle principal :** Validation des valeurs de paramètres
**Fonctionnalités :**
- Validation des formats selon le type de valeur (URL, email, téléphone)
- Vérification de la conformité des données saisies
- Support de différents types de validation métier
- Messages d'erreur contextuels pour les utilisateurs

### 120. LicenseHelper
**Rôle principal :** Utilitaires cryptographiques pour licences
**Fonctionnalités :**
- Parsing des clés RSA publiques et privées
- Décryptage des fichiers de licence chiffrés
- Vérification des signatures numériques
- Gestion des formats de clés cryptographiques
- Utilitaires de sécurité pour l'intégrité des licences

### 121. AppUtils
**Rôle principal :** Utilitaires généraux de l'application
**Fonctionnalités :**
- Conversion des énumérations en noms lisibles
- Formatage des données pour affichage utilisateur
- Fonctions utilitaires communes partagées

## Configuration et Cache

### 122. CacheConfiguration
**Rôle principal :** Configuration du système de cache
**Fonctionnalités :**
- Configuration Redis pour cache distribué
- Gestion du cache en mémoire pour développement
- Paramétrage des TTL et politiques d'éviction
- Support de multiples implémentations de cache

### 123. CacheManagerImpl
**Rôle principal :** Implémentation du gestionnaire de cache
**Fonctionnalités :**
- Abstraction des opérations de cache
- Basculement automatique entre Redis et mémoire
- Gestion des erreurs de cache avec fallback
- Monitoring des performances de cache

## Propriétés et Configuration

### 124. LicenseProperties
**Rôle principal :** Configuration des propriétés de licence
**Fonctionnalités :**
- Gestion des clés de chiffrement et signature
- Configuration des notifications d'expiration
- Paramètres de surveillance et monitoring
- URLs et chemins des fichiers de licence

### 125. ImageDimensionsConfig
**Rôle principal :** Configuration des contraintes d'images
**Fonctionnalités :**
- Définition des dimensions autorisées par type de branding
- Configuration des ratios d'aspect acceptés
- Paramètres de validation des formats d'image

Ce service de paramètres constitue le centre de configuration de l'écosystème PKF Internet Banking, gérant tous les aspects de personnalisation, branding, licences et paramètres système avec une architecture robuste de validation, cache et notification en temps réel.