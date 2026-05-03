# Notes d'analyse Yaazhini

## Éléments identifiés

### Élément 1: Hardcoded API Key
- **Localisation**: res/values/strings.xml
- **Description**: Clé API Google Maps exposée en clair.
- **Impact potentiel**: Utilisation non autorisée de la quote API.
- **Remédiation suggérée**: Utiliser Android Keystore ou un backend proxy.

### Élément 2: Backup activé
- **Localisation**: AndroidManifest.xml -> android:allowBackup="true"
- **Description**: La sauvegarde ADB est activée.
- **Impact potentiel**: Extraction possible des données de l'application via ADB.
- **Remédiation suggérée**: Définir android:allowBackup="false".

### Élément 3: Cleartext Traffic autorisé
- **Localisation**: AndroidManifest.xml -> android:usesCleartextTraffic="true"
- **Description**: L'application autorise les communications HTTP non chiffrées.
- **Impact potentiel**: Interception de données via MITM.
- **Remédiation suggérée**: Désactiver cleartext traffic et forcer HTTPS.

### Élément 4: Component Exported
- **Localisation**: AndroidManifest.xml -> .DebugActivity (android:exported="true")
- **Description**: Activité de débogage accessible depuis d'autres applications.
- **Impact potentiel**: Accès à des fonctionnalités de test/débogage.
- **Remédiation suggérée**: Définir exported="false" ou protéger par permission.

### Élément 5: Hardcoded Endpoint
- **Localisation**: com.example.app.NetworkClient.java
- **Description**: URL de serveur de test hardcodée: http://dev-api.internal/debug
- **Impact potentiel**: Révélation de l'infrastructure interne.
- **Remédiation suggérée**: Utiliser des fichiers de configuration par environnement.
