---
title: Co-Verwaltung für Windows 10-Geräte
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Windows 10-Geräte mithilfe von Configuration Manager und Microsoft Intune gleichzeitig verwalten können.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/28/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 1657cbacde468ef7c54f95524e0fa9607a1a0186
ms.sourcegitcommit: e23350fe65ff99228274e465b24b5e163769f38f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/20/2018
---
# <a name="co-management-for-windows-10-devices"></a>Co-Verwaltung für Windows 10-Geräte    
 Bei den vorherigen Windows 10-Updates können Sie bereits ein Windows 10-Gerät gleichzeitig in eine lokale Active Directory-Installation (AD) und eine cloudbasierte Azure AD-Infrastruktur einbinden (Hybrid-Azure AD). Ab der Configuration Manager-Version 1710 nutzt die Co-Verwaltung diese Verbesserung und ermöglicht Ihnen, Geräte mit Windows 10-Version 1709 gleichzeitig mit Configuration Manager und Intune zu verwalten. <!-- 1350871 -->
## <a name="why-co-management"></a>Gründe für die Co-Verwaltung
Viele Kunden möchten Windows 10-Geräte genauso verwalten wie mobile Geräte: mit einer einfachen, kostengünstigen und cloudbasierten Lösung. Der Übergang von einer herkömmlichen zu einer modernen Verwaltungslösung kann jedoch eine Herausforderung sein.  
## <a name="what-is-co-management"></a>Was ist Co-Verwaltung?
Über die Co-Verwaltung können Sie Windows 10-Geräte mithilfe von Configuration Manager und Intune gleichzeitig verwalten. Diese Lösung schlägt eine Brücke von der herkömmlichen zur modernen Verwaltung und bietet Ihnen die Möglichkeit, die Umstellung Schritt für Schritt durchzuführen.

## <a name="benefits"></a>Vorteile 
- Unmittelbare Verwendung von Intune-Features 
    - Remoteaktionen
        - [Zurücksetzen auf Werkseinstellungen](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
        - [Selektives Zurücksetzen](https://docs.microsoft.com/intune/apps-selective-wipe)
        - [Geräte löschen](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
        - [Geräte neu starten](https://docs.microsoft.com/intune/device-restart)
        - [Sauber starten](https://docs.microsoft.com/intune/device-fresh-start)
    - Orchestrierung mit Intune für die folgenden Workloads:
        - [Kompatibilitätsrichtlinien](https://docs.microsoft.com/intune/device-compliance-get-started)
        - [Ressourcenzugriffsrichtlinien](https://docs.microsoft.com/intune/device-profiles)
        - [Windows Update-Richtlinien](https://docs.microsoft.com/intune/windows-update-for-business-configure)
        - [Endpoint Protection](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10) (ab Configuration Manager 1802) <!-- 1357365 -->
    
## <a name="how-to-configure-co-management"></a>Konfigurieren der Co-Verwaltung
Die Co-Verwaltung kann auf zwei Weisen realisiert werden. Eine davon ist die von Configuration Manager bereitgestellte Co-Verwaltung, bei der Windows 10-Geräte, die mit Configuration Manager verwaltet werden und in hybrides Azure AD eingebunden sind, bei Intune registriert werden. Die andere sieht von Intune bereitgestellte Geräte vor, die bei Intune angemeldet und dann mit dem Configuration Manager-Client installiert werden, um einen Co-Verwaltungsstatus zu erreichen.

### <a name="configuration-manager"></a>**Configuration Manager**
 -  Aktualisieren auf Configuration Manager, Version 1710 oder höher


### <a name="azure-active-directory"></a>**Azure Active Directory**
  - [In Azure AD eingebundene Hybridgeräte](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (in AD und Azure AD eingebunden)
  - [Aktivieren der automatischen Registrierung von Windows 10](https://docs.microsoft.com/intune/windows-enroll)


### <a name="intune"></a>**Intune**
 - [Einrichten des Intune-Abonnements](/sccm/mdm/deploy-use/configure-intune-subscription) oder https://docs.microsoft.com/en-us/intune/setup-steps
 - [Beginnen der Migration hybrider MDM-Benutzer und -Geräte zum eigenständigen Intune](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)


### <a name="enable-co-management"></a>Aktivieren der Co-Verwaltung 
 Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-management** (Co-Verwaltung). Wählen Sie im Menüband  **Configure co-management** (Co-Verwaltung konfigurieren) aus, um den **Registrierungs-Assistenten für die Co-Verwaltung** zu öffnen. 
   
1. Klicken Sie auf der Seite **Subscription** (Abonnement) auf **Sign In** (Anmelden), melden Sie sich bei Ihrem Intune-Mandanten an, und klicken Sie dann auf **Next** (Weiter).    
2. Wählen Sie auf der Seite **Enablement** (Aktivierung) Ihre Einstellung für **Automatic enrollment into Intune** (Automatische Registrierung bei Intune) aus. Kopieren Sie die Befehlszeile ggf. für Geräte, die bereits bei Intune registriert sind. 
3. Wählen Sie auf der Seite **Workloads** für die einzelnen Workloads aus, welche Gerätegruppe Sie mit Intune verwalten möchten.
4. Wählen Sie auf der Seite **Staging** eine Gerätesammlung als **Pilotsammlung** aus. Überprüfen Sie die **Zusammenfassung**, und schließen Sie den Assistenten ab. 

### <a name="upgrade-windows-10-client"></a>Aktualisieren eines Windows 10-Clients
- Upgrade auf [Windows 10, Version 1709 (auch Fall Creators Update genannt) und höher](/sccm/osd/deploy-use/manage-windows-as-a-service)

### <a name="configure-workloads-to-switch-to-intune"></a>Konfigurieren von Workloads für den Wechsel zu Intune 
Der Artikel [Verschieben von Configuration Manager-Workloads zu Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) erläutert, wie Sie bestimmte Configuration Manager-Workloads zu Intune verschieben. Der Artikel enthält auch Anweisungen zum Ändern der Gerätegruppen, für die Workloads umgestellt werden.

- **Konformitätsrichtlinien:** Konformitätsrichtlinien definieren die Regeln und Einstellungen, die ein Gerät erfüllen muss, damit es als mit bedingten Zugriffsrichtlinien konform eingestuft wird. Konformitätsrichtlinien ermöglichen Ihnen auch, Konformitätsprobleme bei Geräten unabhängig von bedingten Zugriffsrechten zu überwachen und zu beheben. Weitere Informationen finden Sie unter [Kompatibilitätsrichtlinie für Geräte](https://docs.microsoft.com/intune/device-compliance-get-started).  

- **Windows Update-Richtlinien:** Mit Windows Update for Business-Richtlinien können Sie Zurückstellungsrichtlinien für Funktionsupdates unter Windows 10 oder für Qualitätsupdates für Windows 10-Geräte konfigurieren, die direkt von Windows Update for Business verwaltet werden. Weitere Informationen finden Sie unter [Konfigurieren von Windows Update for Business-Zurückstellungsrichtlinien](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

- **Ressourcenzugriffsrichtlinien:** Mit Ressourcenzugriffsrichtlinien werden VPN-, WLAN, E-Mail- und Zertifikateinstellungen auf Geräten konfiguriert. Weitere Informationen finden Sie unter [Bereitstellen von Ressourcenzugriffsprofilen](https://docs.microsoft.com/intune/device-profiles).

- **Endpoint Protection:** Ab der Configuration Manager-Version 1802 kann die Endpoint Protection-Workload auf Intune umgestellt werden. Weitere Informationen finden Sie unter [Endpoint Protection für Microsoft Intune](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10)<!-- 1357365 --> und [Verschieben von Configuration Manager-Workloads zu Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Installieren des Configuration Manager-Clients auf den Geräten, die in Intune registriert sind
Wenn Windows 10-Geräte bei Intune registriert sind, können Sie den Configuration Manager-Client auf den Geräten ([mit einem bestimmten Befehlszeilenargument](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)) installieren, um die Clients für die Co-Verwaltung vorzubereiten. Anschließend aktivieren Sie die Co-Verwaltung über die Configuration Manager-Konsole, um bestimmte Workloads für bestimmte Windows 10-Geräte in Intune zu verschieben.
Windows 10-Geräte, die noch nicht bei Intune registriert sind, können Sie automatisch bei Azure registrieren. Bei neuen Windows 10-Geräten können Sie den Eindruck beim ersten Ausführen, der die automatische Registrierung von Geräten in Intune enthält, mit [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) konfigurieren.
 - Aktivieren Sie [Cloud Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) in Configuration Manager (nur wenn Sie den Configuration Manager-Client mit Intune installieren).

## <a name="monitor-co-management"></a>Überwachen der Co-Verwaltung
[Mithilfe des Dashboards für die Co-Verwaltung](/sccm/core/clients/manage/co-management-dashboard) können Sie die Computer überprüfen, die in Ihrer Umgebung gemeinsam verwaltet werden. Mithilfe der Diagramme können Geräte identifiziert werden, bei denen möglicherweise ein Eingriff erforderlich ist.


## <a name="next-steps"></a>Nächste Schritte
[Vorbereiten von Windows 10-Geräten für die Co-Verwaltung](co-management-prepare.md)
