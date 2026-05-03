# Mapping OWASP

## FIND-001: API Key exposée
- **Catégorie OWASP**: MASVS-STORAGE
- **Référence spécifique**: V2.1
- **Justification**: Les secrets ne doivent pas être stockés en clair dans les ressources.

## FIND-002: Backup activé
- **Catégorie OWASP**: MASVS-STORAGE
- **Référence spécifique**: V2.8
- **Justification**: L'activation du backup permet l'exfiltration de données privées via ADB.

## FIND-003: Cleartext Traffic
- **Catégorie OWASP**: MASVS-NETWORK
- **Référence spécifique**: V5.1
- **Justification**: Le trafic non chiffré est vulnérable aux attaques Man-in-the-Middle.

## FIND-004: Activité exposée
- **Catégorie OWASP**: MASVS-PLATFORM
- **Référence spécifique**: V1.2
- **Justification**: Les composants internes ne doivent pas être exportés sans protection.

## FIND-005: Endpoint de debug exposé
- **Catégorie OWASP**: MASVS-CODE
- **Référence spécifique**: V3.1
- **Justification**: Le code de production ne doit pas contenir d'outils de débogage actifs.
