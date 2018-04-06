---
title: Co-Verwaltung für Windows 10-Geräte
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Windows 10-Geräte mithilfe von Configuration Manager und Microsoft Intune gleichzeitig verwalten können.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: e4b8bd58d30cd87ffc461289edbfc5da9a684cda
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="co-management-for-windows-10-devices"></a>Co-Verwaltung für Windows 10-Geräte    
<!-- 1350871 -->
Viele Kunden möchten Windows 10-Geräte genauso verwalten wie mobile Geräte: mit einer einfachen, kostengünstigen und cloudbasierten Lösung. Der Übergang von einer herkömmlichen zu einer modernen Verwaltungslösung kann jedoch eine Herausforderung sein. In den vorherigen Windows 10-Updates können Sie bereits ein Windows 10-Gerät gleichzeitig in eine lokale Active Directory-Installation (AD) und eine cloudbasierte Azure AD-Infrastruktur einbinden (Hybrid-Azure AD). Ab der Configuration Manager-Version 1710 nutzt die Co-Verwaltung diese Verbesserung und ermöglicht Ihnen, Windows 10-Geräte mit der Version 1709 (auch als „Fall Creators Update“ bezeichnet) gleichzeitig mit Configuration Manager und Intune zu verwalten. Diese Lösung schlägt eine Brücke von der herkömmlichen zur modernen Verwaltung und bietet Ihnen die Möglichkeit, die Umstellung Schritt für Schritt durchzuführen. 

Die Co-Verwaltung kann auf zwei Weisen realisiert werden.  Eine davon ist die von Configuration Manager bereitgestellte Co-Verwaltung, bei der Windows 10-Geräte, die mit Configuration Manager verwaltet werden und in hybrides Azure AD eingebunden sind, bei Intune registriert werden. Die andere sieht von Intune bereitgestellte Geräte vor, die bei Intune angemeldet und dann mit dem Configuration Manager-Client installiert werden, um einen Co-Verwaltungsstatus zu erreichen.

## <a name="prerequisites"></a>Erforderliche Komponenten
Bevor Sie mit der Co-Verwaltung beginnen können, müssen folgende Anforderungen erfüllt sein. Zum einen gelten allgemeine Voraussetzungen und zum anderen unterschiedliche Voraussetzungen für Geräte mit installiertem Configuration Manager-Client und für Geräte, auf denen der Client nicht installiert ist.

> [!IMPORTANT]
> Co-Verwaltung wird von Windows 10 Mobile-Geräten nicht unterstützt.

### <a name="general-prerequisites"></a>Allgemeine Voraussetzungen
Hier finden Sie die allgemeinen Voraussetzungen für die Aktivierung der Co-Verwaltung:  

- Configuration Manager, Version 1710 oder höher
- Azure AD
- EMS- oder Intune-Lizenzen für alle Benutzer
- [Automatische Registrierung bei Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) aktiviert
- Intune-Abonnement &#40;die MDM-Autorität muss in Intune auf **Intune** festgelegt sein&#41;


   > [!Note]  
   > In einer hybriden MDM-Umgebung (Intune integriert in Configuration Manager) ist keine Co-Verwaltung möglich. Informationen zur Migration zu Intune Standalone finden Sie unter [Migrate hybrid MDM users and devices to Intune standalone (Migrieren hybrider MDM-Benutzer und -Geräte zu Intune Standalone)](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Zusätzliche Anforderungen an Geräte mit dem Configuration Manager-Client
- Windows 10, Version 1709 (auch Fall Creators Update genannt) und höher
- [In Azure AD eingebundene Hybridgeräte](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (in AD und Azure AD eingebunden)

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Zusätzliche Anforderungen an Geräte ohne Configuration Manager-Client
- Windows 10, Version 1709 (auch Fall Creators Update genannt) und höher
- [Cloud Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) in Configuration Manager (wenn Sie den Configuration Manager-Client mit Intune installieren)

## <a name="workloads-you-can-switch-to-intune"></a>Workloads, die Sie zu Intune verschieben können
Nach der Aktivierung der Co-Verwaltung verwaltet Configuration Manager weiterhin alle Workloads. Wenn Sie dazu bereit sind, können Sie die Verwaltung aller verfügbaren Workloads auf Intune umstellen. Sie können Intune die folgenden Workloads verwalten lassen:   

### <a name="compliance-policies"></a>Kompatibilitätsrichtlinien
Konformitätsrichtlinien definieren die Regeln und Einstellungen, die ein Gerät erfüllen muss, damit es als mit bedingten Zugriffsrichtlinien konform eingestuft wird. Konformitätsrichtlinien ermöglichen Ihnen auch, Konformitätsprobleme bei Geräten unabhängig von bedingten Zugriffsrechten zu überwachen und zu beheben. Weitere Informationen finden Sie unter [Kompatibilitätsrichtlinie für Geräte](/sccm/mdm/deploy-use/device-compliance-policies).  

### <a name="windows-update-for-business-policies"></a>Windows Update for Business-Richtlinien
Mit Windows Update for Business-Richtlinien können Sie Zurückstellungsrichtlinien für Funktionsupdates unter Windows 10 oder für Qualitätsupdates für Windows 10-Geräte konfigurieren, die direkt von Windows Update for Business verwaltet werden. Weitere Informationen finden Sie unter [Konfigurieren von Windows Update for Business-Zurückstellungsrichtlinien](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="resource-access-policies"></a>Ressourcenzugriffsrichtlinien
Mit Ressourcenzugriffsrichtlinien werden VPN-, WLAN, E-Mail- und Zertifikateinstellungen auf Geräten konfiguriert. Weitere Informationen finden Sie unter [Bereitstellen von Ressourcenzugriffsprofilen](/sccm/protect/deploy-use/deploy-wifi-vpn-email-cert-profiles).

### <a name="endpoint-protection"></a>Endpoint Protection 
<!-- 1357365 -->
Ab der Configuration Manager-Version 1802 kann der Endpoint Protection-Workload auf Intune umgestellt werden. Weitere Informationen finden Sie unter [Workloads able to be transitioned to Intune (Auf Intune umstellbare Workloads)](/sccm/core/clients/manage/co-management-switch-workloads.md#Workloads-able-to-be-transitioned-to-Intune) und [Endpoint Protection in Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).

## <a name="architectural-overview-for-co-management"></a>Architekturübersicht für die Co-Verwaltung
Die folgende Abbildung bietet eine Architekturübersicht über die Co-Verwaltung und ihre Rolle in der vorhandenen Configuration Manager- und Intune-Infrastruktur.

![Architekturabbildung der Co-Verwaltung](./media/co-management-arch.svg)

## <a name="scenarios-to-enable-co-management"></a>Szenarios zum Aktivieren der Co-Verwaltung  
Sie können die Co-Verwaltung sowohl für Windows 10-Geräte, die in Microsoft Intune registriert sind, als auch für vorhandene Windows 10-Configuration Manager-Clients aktivieren. In beiden Szenarios werden Windows 10-Geräte gleichzeitig von Configuration Manager und Intune verwaltet und in AD und Azure AD eingebunden.  

### <a name="devices-enrolled-in-intune"></a>Bei Intune registrierte Geräte  
Wenn Windows 10-Geräte bei Intune registriert sind, können Sie den Configuration Manager-Client auf den Geräten (mit einem bestimmten Befehlszeilenargument) installieren, um die Clients für die Co-Verwaltung vorzubereiten. Anschließend aktivieren Sie die Co-Verwaltung über die Configuration Manager-Konsole, um bestimmte Workloads für bestimmte Windows 10-Geräte in Intune zu verschieben.  

Windows 10-Geräte, die noch nicht bei Intune registriert sind, können Sie automatisch bei Azure registrieren. Bei neuen Windows 10-Geräten können Sie den Eindruck beim ersten Ausführen, der die automatische Registrierung von Geräten in Intune enthält, mit [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) konfigurieren.  

### <a name="configuration-manager-clients"></a>Configuration Manager-Clients
Wenn einige Ihrer Windows 10-Geräte Configuration Manager-Clients sind, können Sie diese Geräte registrieren und die Co-Verwaltung über die Configuration Manager-Konsole aktivieren. Configuration Manager registriert Geräte automatisch anhand der Azure AD-Mandanteninformationen bei Intune.  


## <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Remoteaktionen, die in Intune in Azure für co-verwaltete Geräte verfügbar sind
Wenn ein Windows 10-Gerät für die Co-Verwaltung aktiviert ist, stehen Ihnen die folgenden Remoteaktionen aus Intune in Azure zur Verfügung:  
- [Zurücksetzen auf Werkseinstellungen](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [Selektives Zurücksetzen](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Geräte löschen](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Geräte neu starten](https://docs.microsoft.com/intune/device-restart)
- [Sauber starten](https://docs.microsoft.com/intune/device-fresh-start)

## <a name="next-steps"></a>Nächste Schritte
[Vorbereiten von Windows 10-Geräten für die Co-Verwaltung](co-management-prepare.md)