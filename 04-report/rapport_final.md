# Rapport d'analyse de sécurité mobile

## A. Informations générales
- **Date**: 2026-05-03
- **Analyste**: Ziyad Daber
- **Cible**: Application Pédagogique Mobile
- **Version/Hash**: 7e5f8c2a1d6b3e9a8c7f4d2e1b3a6c9d8e7f4a2d1c3b6e9a8c7f4d2e1b3a6c9d
- **Outils utilisés**: BeVigil v2.1.0, Yaazhini v1.3.2

## B. Résumé exécutif
L'analyse a révélé 10 constats de sécurité, dont un risque élevé lié à l'exposition d'une clé API et plusieurs risques moyens concernant la configuration réseau et la plateforme Android. Le niveau de risque global est **Moyen**. Les principales faiblesses résident dans le stockage des secrets et la configuration du manifeste Android.

## C. Top 5 constats

### 1. API Key exposée - FIND-001
- **Sévérité**: High
- **Preuve**: res/values/strings.xml
- **Impact**: Accès non autorisé aux services tiers et consommation abusive de quotas.
- **Remédiation**: Révoquer la clé et utiliser Android Keystore.
- **Référence OWASP**: MASVS-STORAGE-1

### 2. Backup activé - FIND-002
- **Sévérité**: Medium
- **Preuve**: AndroidManifest.xml (allowBackup="true")
- **Impact**: Possibilité d'extraire les données privées de l'utilisateur via ADB.
- **Remédiation**: Définir android:allowBackup="false".
- **Référence OWASP**: MASVS-STORAGE-4

### 3. Cleartext Traffic autorisé - FIND-003
- **Sévérité**: Medium
- **Preuve**: AndroidManifest.xml (usesCleartextTraffic="true")
- **Impact**: Interception des données sensibles en transit via MITM.
- **Remédiation**: Désactiver le trafic en clair et forcer HTTPS.
- **Référence OWASP**: MASVS-NETWORK-1

### 4. Activité de Debug exposée - FIND-004
- **Sévérité**: Medium
- **Preuve**: AndroidManifest.xml (.DebugActivity exported="true")
- **Impact**: Accès non autorisé à des fonctions de test internes.
- **Remédiation**: Définir exported="false".
- **Référence OWASP**: MASVS-PLATFORM-1

### 5. Endpoint de debug hardcodé - FIND-005
- **Sévérité**: Medium
- **Preuve**: com.example.app.NetworkClient.java
- **Impact**: Révélation de l'infrastructure interne et potentiels accès non autorisés.
- **Remédiation**: Supprimer les URLs de debug dans les builds de production.
- **Référence OWASP**: MASVS-CODE-1

## D. Faux positifs notables
- Aucun faux positif majeur identifié durant cette session courte.

## E. Recommandations prioritaires
1. Sécuriser les secrets en utilisant Android Keystore et supprimer les clés hardcodées.
2. Durcir la configuration du Manifest (désactiver backup et cleartext traffic).
3. Nettoyer le code de production en supprimant les activités et endpoints de débogage.

## F. Annexes
- [Exports BeVigil](../01-bevigil/bevigil_export.json)
- [Rapport Yaazhini](../02-yaazhini/yaazhini_report.txt)
- [Triage complet](../03-triage/triage.csv)
