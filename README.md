# LOCINTEL M-Pesa Bridge Android — V1.5.1 Release

Application Android de passerelle M-Pesa pour LOCINTEL Device Financing.

## Association QR

1. Dans Odoo, ouvrez **Device Financing → Configuration passerelle M-Pesa**.
2. Générez le QR d'association temporaire.
3. Dans l'application Android, utilisez **Scanner le QR Odoo**.
4. L'application échange le code temporaire contre son jeton d'appareil.
5. Autorisez ensuite l'accès Android aux notifications.

La configuration manuelle URL + jeton reste disponible en secours.

## APK Release signée avec GitHub Actions

Le workflow `.github/workflows/build-apk.yml` compile `assembleRelease` et produit :

`LOCINTEL-Mpesa-Bridge-V1.5.1-release.apk`

Avant de lancer le workflow, créez ces secrets dans :
**GitHub → Settings → Secrets and variables → Actions → New repository secret**

- `ANDROID_KEYSTORE_BASE64`
- `ANDROID_KEYSTORE_PASSWORD`
- `ANDROID_KEY_ALIAS`
- `ANDROID_KEY_PASSWORD`

Le keystore et les mots de passe ne doivent jamais être ajoutés au dépôt GitHub.

## Sécurité

- HTTPS obligatoire.
- Pas de permission générale de lecture des SMS.
- Capture via `NotificationListenerService`.
- Les notifications qui ne ressemblent pas au format M-Pesa attendu sont ignorées.
- Appairage QR temporaire côté Odoo.
- Signature Android Release stable pour les mises à jour futures.

> Important : une signature Release réduit les alertes liées aux APK de développement, mais Google Play Protect peut encore afficher un avertissement pour une application installée hors Play Store ou utilisant l'accès aux notifications. Ne désactivez pas Play Protect globalement.
