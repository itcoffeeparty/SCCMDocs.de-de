---
title: Einrichten von hybridem MDM
titleSuffix: Configuration Manager
description: Richten Sie die Registrierung von Hybridgeräten mit Configuration Manager und Intune ein.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbc5b9abf63d95185795716cfcb9ebfaf3e2ec3d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Einrichten der hybriden Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*


Bevor Sie iOS, Windows und Android-Geräte mit Configuration Manager verwalten können, müssen sie mit Intune registriert werden. Verwenden Sie die folgenden Schritte, um die Registrierung von Hybridgeräten mit Configuration Manager und Intune einzurichten. Mithilfe der folgenden Schritte aktivieren Sie die BYOD-Registrierung (Bring Your Own Device) für Ihre Benutzer. Diese Schritte sind auch Voraussetzungen für die [Registrierung von BYOD-Geräten](enroll-hybrid-ios-mac.md) und die [Registrierung von unternehmenseigenen Geräten](enroll-company-owned-devices.md).

 |Schritte|Details|  
 |-----------|-------------|  
 |**Schritt 1:** [Erstellen einer MDM-Sammlung](create-mdm-collection.md)|Erstellen Sie eine Configuration Manager-Benutzersammlung mit Benutzern, deren Geräte registriert werden können.|  
 |**Schritt 2:** [Anforderungen an den Domänennamen](confirm-dns.md)|Bestätigen Sie, dass der Domain Name Service (DNS) Ihrer Organisation und die Active Directory-Benutzerverwaltung die MDM-Anforderungen erfüllen.|
 |**Schritt 3:** [Konfigurieren des Intune-Abonnements](configure-intune-subscription.md)|Der Intune-Dienst ermöglicht die Verwaltung von Geräten über das Internet.|  
 |**Schritt 4:** [Hinzufügen von Geschäftsbedingungen](terms-and-conditions.md)| Erstellen Sie Geschäftsbedingungen, die von Benutzern akzeptiert werden müssen, bevor die Unternehmensportal-App verwendet werden kann.|
 |**Schritt 5:** [Erstellen eines Dienstverbindungspunkts](create-service-connection-point.md)|Vom Dienstverbindungspunkt werden Einstellungen und Softwarebereitstellungsinformationen an Configuration Manager gesendet sowie Status- und Inventurmeldungen von mobilen Geräten abgerufen. |  
 |**Schritt 6:** [Aktivieren der Plattformregistrierung](enable-platform-enrollment.md)|Die MDM-Registrierung für iOS- und Windows-Geräte erfordert zusätzliche Schritte für die Kommunikation zwischen dem Dienst und Geräten. Für Android ist keine weitere Konfiguration erforderlich.|  
 |**Schritt 7:** [Einrichten zusätzlicher Verwaltung](set-up-additional-management.md)|(Optional) Richten Sie Konfigurationselemente und den bedingten Zugriff für registrierte Geräte ein.|
 |**Schritt 8:** [Überprüfen der MDM-Konfiguration](verify-mdm-configuration.md)|Zeigen Sie Protokolldateien an, um zu bestätigen, dass der Dienstverbindungspunkt erfolgreich erstellt wurde und Benutzerkonten synchronisiert werden.|

Möchten Sie Intune ohne Configuration Manager?
> [!div class="button"]
[Intune Dokumente anzeigen >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>Registrieren von Geräten
Nachdem das Hybrid-Setup abgeschlossen ist, können die Geräte im Configuration Manager auf verschiedene Arten registriert werden:
- **Unternehmenseigene Geräte (company-owned devices, COD):** [Registrieren von unternehmenseigenen Geräten](enroll-company-owned-devices.md) enthält Anleitungen für bestimmte Arten der Registrierung von unternehmenseigenen Geräten.
- **Benutzergeräte (bring your own device, BYOD):** [Enroll user-owned (BYOD) devices (Registrieren von Benutzergeräten (BYOD))](enroll-hybrid-ios-mac.md) enthält Anleitungen für verschiedene Registrierungsarten von benutzereigenen Geräten.
