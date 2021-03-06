# Übersicht
## [Was ist die hybride Verwaltung mobiler Geräte (MDM)?](understand/hybrid-mobile-device-management.md)
## [Auswählen von Intune Standalone oder der hybriden Verwaltung mobiler Geräte (MDM)](understand/choose-between-standalone-intune-and-hybrid-mobile-device-management.md)
## [Neues bei der hybriden Verwaltung mobiler Geräte](understand/whats-new-in-hybrid-mobile-device-management.md)

# [Planung und Entwurf](plan-design/plan-hybrid-mobile-device-management.md)
## [Unterstützte Geräteplattformen](plan-design/supported-device-platforms-for-hybrid.md)
## [Registrierungsmethoden für Geräte](plan-design/device-enrollment-methods.md)

# [Erste Schritte](deploy-use/setup-hybrid-mdm.md)
## [Erstellen einer MDM-Sammlung](deploy-use/create-mdm-collection.md)
## [Anforderungen an den Domänennamen](deploy-use/confirm-dns.md)
## [Konfigurieren des Intune-Abonnements](deploy-use/configure-intune-subscription.md)
## [Hinzufügen von Geschäftsbedingungen](deploy-use/terms-and-conditions.md)
## [Erstellen eines Dienstverbindungspunkts](deploy-use/create-service-connection-point.md)
## [Aktivieren der Plattformregistrierung](deploy-use/enable-platform-enrollment.md)
### [iOS und Mac](deploy-use/enroll-hybrid-ios-mac.md)
### [Windows](deploy-use/enroll-hybrid-windows.md)
### [Android](deploy-use/enroll-hybrid-android.md)
## [Einrichten zusätzlicher Verwaltung](deploy-use/set-up-additional-management.md)
## [Überprüfen der MDM-Konfiguration](deploy-use/verify-mdm-configuration.md)

# Vorgehensweise:
## [Registrieren von (BYOD) Benutzergeräten](deploy-use/enroll-user-owned-devices.md)
## [Registrieren firmeneigener iOS-Geräte](deploy-use/enroll-company-owned-devices.md)
### [iOS DEP-Registrierung](deploy-use/ios-device-enrollment-program-for-hybrid.md)
### [Apple Configurator-Registrierung](deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)
### [Geräteregistrierungs-Manager](deploy-use/enroll-devices-with-device-enrollment-manager.md)
### [Vorabdeklarieren von Hardware-IDs](deploy-use/predeclare-devices-with-hardware-id.md)
### [Verwalten der iOS-Aktivierungssperre](deploy-use/manage-ios-activation-lock.md)
### [Affinität zwischen Benutzer und Gerät](deploy-use/user-affinity-for-hybrid-managed-devices.md)

## [Abkoppeln/Zurücksetzen, Sperren, Zurücksetzen von Geräten](deploy-use/wipe-lock-reset-devices.md)
## [Konfigurieren der Hardwareinventur](deploy-use/mobile-device-hardware-inventory-hybrid.md)
## [Konfigurieren der Softwareinventur](deploy-use/software-inventory-mobile-devices.md)

## [Verwalten der Kompatibilitätseinstellungen](deploy-use/manage-compliance-settings.md)
### [Windows 8.1 und Windows 10](deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
### [Windows Phone](deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
### [iOS und Mac OS X](deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
### [Android- und Samsung KNOX Standard](deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)
### [Android for Work](deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client.md)

## [Synchronisieren von Intune-registrierten Geräten](deploy-use/sync-intune-device.md)

## [Verwalten von Anwendungen](deploy-use/management-tasks-applications.md)
### [Erstellen von iOS-Anwendungen](deploy-use/creating-ios-applications.md)
### [Richtlinien zur Konfiguration von iOS-Apps](deploy-use/configure-ios-apps-with-app-configuration-policies.md)
### [Per Volumenlizenz erworbene Apps](deploy-use/manage-volume-purchased-ios-apps.md)
### [Erstellen von Windows Phone-Anwendungen](deploy-use/creating-windows-phone-applications.md)
### [Erstellen von Android-Anwendungen](deploy-use/creating-android-applications.md)
### [Richtlinien zur Konfiguration von Android-Apps](deploy-use/configure-android-apps-with-app-configuration-policies.md)
### [Verwaltungsrichtlinien für mobile Anwendungen](deploy-use/protect-apps-using-mam-policies.md)
### [Managed Browser-Richtlinien](deploy-use/manage-internet-access-using-managed-browser-policies.md)
### [Apps aus Microsoft Store für Unternehmen](deploy-use/windows-store-for-business.md)

## [Verwalten eines Intune-Abonnements](deploy-use/manage-intune-subscriptions.md)
## [Change your MDM authority (Ändern Ihrer MDM-Autorität)](deploy-use/change-mdm-authority.md)
## [Start migrating from hybrid MDM to Intune standalone (Starten der Migration von der Verwaltung mobiler Geräte zu eigenständigem Intune)](deploy-use/migrate-hybridmdm-to-intunesa.md) 
### [Import Configuration Manager data to Microsoft Intune (Importieren der Configuration Manager-Daten in Microsoft Intune)](deploy-use/migrate-import-data.md)
### [Prepare Intune for user migration (Vorbereiten von Intune für die Benutzermigration)](deploy-use/migrate-prepare-intune.md)
### [Change the MDM authority for specific users (mixed MDM authority) (Ändern der MDM-Autorität für bestimmte Benutzer (gemischte MDM-Autorität))](deploy-use/migrate-mixed-authority.md)
### [Change your MDM authority (Ändern Ihrer MDM-Autorität)](deploy-use/migrate-change-mdm-authority.md)

## Verwalten des Zugriffs auf Ressourcen
### [Erstellen von WLAN-Profilen](deploy-use/create-wifi-profiles.md)
### [Erstellen von PFX-Zertifikatprofilen](deploy-use/create-pfx-certificate-profiles.md)
### [Importieren der PFX-Zertifikatprofilen](deploy-use/import-pfx-certificate-profiles.md)
### [VPN-Profile](deploy-use/create-vpn-profiles.md)
### [Erstellen von E-Mail-Profilen](deploy-use/create-exchange-activesync-profiles.md)
### [Windows Hello for Business-Einstellungen](deploy-use/windows-hello-for-business-settings.md)

## [Verwalten des bedingten Zugriffs](deploy-use/manage-access-to-services.md)
### [Kompatibilitätsrichtlinie für Geräte](deploy-use/device-compliance-policies.md)
#### [Aktionen bei Nichtkonformität](deploy-use/actions-for-noncompliance.md)
### [Erstellen einer Kompatibilitätsrichtlinie für Geräte](deploy-use/create-compliance-policy.md)
### [Verwalten des E-Mail-Zugriffs](deploy-use/manage-email-access.md)
### [Verwalten des Zugriffs auf SharePoint Online](deploy-use/manage-sharepoint-online-access.md)
### [Verwalten des Zugriffs auf Skype for Business Online](deploy-use/manage-skype-for-business-online-access.md)
### [Verwalten des Dynamics CRM Online-Zugriffs](deploy-use/manage-dynamics-crm-online-access.md)
### [Verwalten des PC-Zugriffs auf O365-Dienste](deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)

## [Verwalten des Zugriffs basierend auf dem Geräterisiko](deploy-use/mobile-threat-defense.md)
### [Lookout in Configuration Manager](deploy-use/lookout-mobile-threat-defense-in-configuration-manager.md)
#### [Einrichten von Lookout Mobile Thread Defense](deploy-use/set-up-your-subscription-with-lookout.md)
#### [Aktivieren von Lookout in Intune](deploy-use/enable-lookout-connection-in-intune.md)
#### [Bereitstellen von Lookout für Arbeits-Apps](deploy-use/configure-and-deploy-lookout-for-work-apps.md)
#### [Erstellen einer Lookout-Konformitätsrichtlinie](deploy-use/enable-device-threat-protection-rule-compliance-policy.md)
#### [Behandeln von Problemen bei der Lookout-Integration](deploy-use/troubleshoot-lookout-integration.md)
#### [Mobile Threat Defense überwachen](deploy-use/monitor-mobile-threat-defense-compliance.md)

# Lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM)
## [Was ist die lokalen Verwaltung mobiler Geräte?](understand/manage-mobile-devices-with-on-premises-infrastructure.md)
## [Planen für die lokale Verwaltung mobiler Geräte](plan-design/plan-on-premises-mdm.md)

## [Installationsschritte](get-started/preparation-steps-for-on-premises-mdm.md)
### [Einrichten des Intune-Abonnements](get-started/set-up-intune-subscription-on-premises-mdm.md)
### [Installieren lokaler Rollen](get-started/install-site-system-roles-for-on-premises-mdm.md)
### [Einrichten von Zertifikaten](get-started/set-up-certificates-on-premises-mdm.md)
### [Einrichten für die Registrierung](get-started/set-up-device-enrollment-on-premises-mdm.md)

## [Registrieren von Geräten für die lokale Verwaltung mobiler Geräte](deploy-use/enroll-devices-on-premises-mdm.md)
### [Benutzerregistrierung](deploy-use/user-enroll-devices-on-premises-mdm.md)
### [Massenregistrierung](deploy-use/bulk-enroll-devices-on-premises-mdm.md)
## [Verwalten von Geräten](deploy-use/onprem-manage-devices.md)
## [Verwalten von Anwendungen](deploy-use/onprem-manage-applications.md)
## [Schützen von Daten und Geräten](deploy-use/onprem-protect-data-devices.md)

# [Geräteverwaltung mit Exchange](deploy-use/manage-mobile-devices-with-exchange-activesync.md)
