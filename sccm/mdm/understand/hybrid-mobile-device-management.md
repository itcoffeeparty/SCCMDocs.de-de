---
title: Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune
description: "Enthält Informationen zur hybriden Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 22e673122f0f664d1240c11451b7e6db78481b26
ms.openlocfilehash: 83832465e93997a2893e024c565ee00f471036d1

---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*


Sie können iOS, Windows und Android-Geräte mit Configuration Manager und Microsoft Intune verwalten. Alle Verwaltungsaufgaben werden aus der Configuration Manager-Konsole heraus verarbeitet, in der Sie die restlichen Verwaltungstasks ausführen, die über das Internet nahtlos in den Microsoft Intune-Onlinedienst integriert sind.  Sie können Configuration Manager so verwenden, dass Benutzer auf sichere und verwaltete Weise auf Unternehmensressourcen auf ihren Geräten zugreifen können. Mithilfe der Geräteverwaltung schützen Sie Unternehmensdaten, und ermöglichen es den Benutzern gleichzeitig, ihre privaten oder im Besitz des Unternehmens befindlichen Geräte anzumelden, um auf Unternehmensdaten zuzugreifen. Verwaltungsfunktionen auf Geräten:

-   Abkoppeln und Zurücksetzen von Geräten
-   Konfigurieren von Kompatibilitätseinstellungen wie Kennwörter, Sicherheit, Roaming, Verschlüsselung und Funkkommunikation
-   Bereitstellen von Branchen-Apps (line-of-business, LOB) auf Geräten
-   Bereitstellen von Apps auf Geräten, die eine Verbindung mit Windows Store, Windows Phone Store, App Store oder Google Play herstellen
-   Erfassen der Hardwareinventur
-   Erfassen der Softwareinventur mithilfe integrierter Berichte

Informationen darüber, welche neuen Funktionen für die hybride Verwaltung mobiler Geräte verfügbar sind, finden Sie unter [What's new in hybrid mobile device management (Neuigkeiten in der hybriden Verwaltung mobiler Geräte)](../understand/whats-new-in-hybrid-mobile-device-management.md).

Im vorliegenden Dokument wird vorausgesetzt, dass Sie Computer mithilfe von Configuration Manager verwalten und beabsichtigen, die Configuration Manager-Konsole mit Intune zu erweitern, um mobile Geräte zu verwalten. Die Unterschiede zwischen Intune und der hybriden Verwaltung mobiler Geräte finden Sie unter [Choose between Microsoft Intune standalone and hybrid mobile device management with System Center Configuration Manager (Auswahl zwischenMicrosoft Intune standalone und hybrider Verwaltung mobiler Geräte mit System Center Configuration Manager)](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

Nach dem Erweitern von Configuration Manager mit Intune können Sie unternehmenseigene Geräte registrieren und verwalten, oder Benutzern die Berechtigung zum Registrieren ihrer persönlichen Geräte erteilen. Mithilfe von Configuration Manager können Sie auch unternehmenseigene Geräte mit Intune verwalten.

## <a name="hybrid-mdm-enrollment"></a>Hybrid-MDM-Registrierung
Um Geräte hybrid zu verwalten, müssen diese Geräte zuerst mit dem Dienst registriert werden. Auf welche Weise Geräte registriert werden, hängt von Gerätetyp, Besitz und benötigtem Verwaltungsniveau ab. Bei der BYOD-Registrierung (Bring Your Own Device, private Geräte der Mitarbeiter) können die Benutzer ihre privaten Smartphones, Tablets oder PCs selbst registrieren. Die COD-Registrierung (Corporate-Owned Device, Firmeneigene Geräte) ermöglicht Verwaltungsszenarios wie das Remotezurücksetzen, gemeinsam verwendete Geräte oder Benutzeraffinität für ein Gerät.

 Wenn Sie [Exchange ActiveSync](#mobile-device-management-with-exchange-activesync-and-configuration-manager) entweder lokal oder in der Cloud gehostet verwenden, können Sie eine einfache Intune-Verwaltung ohne Registrierung aktivieren. Auch Windows-PCs können mit [Intune-Clientsoftware](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune) verwaltet werden.

## <a name="overview-of-device-enrollment-methods"></a>Übersicht über die Geräteregistrierungsmethoden

 In der folgenden Tabelle werden die Registrierungsmethoden zusammen mit den von ihnen unterstützten Funktionen dargestellt. Diese Funktionen beinhalten:
 - **Zurücksetzen** – Zurücksetzen des Geräts auf Werkseinstellungen, wobei alle Daten entfernt werden. [Geräte abkoppeln](../deploy-use/wipe-lock-reset-devices.md)
 - **Affinität** – Ordnet Geräte Benutzern zu. Für die Verwaltung mobiler Anwendungen (Mobile Application Management, MAM) und den bedingten Zugriff auf Unternehmensdaten erforderlich. [Benutzeraffinität](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
 - **Sperre** – Hindert Benutzer daran, das Gerät aus der Verwaltung zu entfernen. Für iOS-Geräte ist der überwachte Modus für die Sperre erforderlich. [Remotesperre](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

 **iOS-Registrierungsmethoden**

| **Methode** |  **Zurücksetzen** |  **Affinität**    |   **Sperren** | **Details** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Nein|    Ja |   Nein | [Mehr](../deploy-use/setup-hybrid-mdm.md#step-6-enable-platform-enrollment)|
|**[DEM](#dem)**|   Nein |Nein |Nein  | [Mehr](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   Ja |   Optional |  Optional|[Mehr](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB (Setup-Assistent)](#usb-sa)**| Ja |   Optional |  Nein| [Mehr](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Windows und Android-Registrierungsmethoden**

| **Methode** |  **Zurücksetzen** |  **Affinität**    |   **Sperren** | **Details**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Nein|    Ja |   Nein | [Mehr](../deploy-use/setup-hybrid-mdm.md#set-up-device-management)|
|**[DEM](#dem)**|   Nein |Nein |Nein  |[Mehr](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Eine Reihe von Fragen, die Sie beim Ermitteln der richtigen Methode unterstützen, finden Sie unter [Auswählen der Registrierungsart von Geräten](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
BYOD-Benutzer installieren die Unternehmensportal-App und registrieren ihr Gerät. Dies erlaubt Benutzern, Verbindungen mit dem Unternehmensnetzwerk herzustellen, und zur Domäne oder zu Azure Active Directory beizutreten. Das Aktivieren der BYOD-Registrierung ist eine Voraussetzung für viele COD-Szenarios der meisten Plattformen. Siehe [Einrichten der hybriden Verwaltung mobiler Geräte](../deploy-use/setup-hybrid-mdm.md). ([Zurück zur Tabelle](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>Unternehmenseigene Geräte
Unternehmenseigene Geräte (Corporate-owned devices, COD) können mit der Configuration Manager-Konsole verwaltet werden. iOS-Geräte können direkt über die von Apple bereitgestellten Tools registriert werden. Alle Gerätetypen können von einem Administrator oder Manager die unter Verwendung des Geräteregistrierungs-Managers registriert werden. Geräte mit einer IMEI-Nummer können auch als firmeneigene Geräte identifiziert und gekennzeichnet werden, um COD-Szenarios zu unterstützen.

[Registrieren firmeneigener iOS-Geräte](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>Geräteregistrierungs-Manager (DEM)
Der Geräteregistrierungs-Manager ist ein besonderes Benutzerkonto, das zum Registrieren und Verwalten mehrerer firmeneigener Geräte verwendet wird. Manager können das Unternehmensportal installieren und viele benutzerlose Geräte registrieren. Erfahren Sie mehr über [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Zurück zur Tabelle](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP (Device Enrollment Program)
Mit der Apple DEP-Verwaltung (Device Enrollment Program, Programm zur Geräteregistrierung) können Sie Richtlinien erstellen und „drahtlos“ auf iOS-Geräten bereitstellen, die mit DEP erworben wurden und verwaltet werden. Das Gerät wird beim ersten Einschalten durch den Benutzer registriert und führt dann den iOS-Setup-Assistenten aus. Diese Methode unterstützt den iOS-Modus **Überwacht**, der wiederum Folgendes ermöglicht:
   -    Gesperrte Registrierung
   -    Bedingter Zugriff
   -    Erkennung von Jailbreaks
   -    Mobile Anwendungsverwaltung

Erfahren Sie mehr über das [Geräteregistrierungsprogramm](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Zurück zur Tabelle](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB (Setup-Assistent)
Über USB verbundene Registrierung mit Setup-Assistent. Der Administrator erstellt eine Richtlinie, und exportiert sie nach Apple Configurator. Über USB angeschlossene, unternehmenseigene Geräte werden mit der Richtlinie vorbereitet. Der Administrator muss jedes Gerät per Hand registrieren. Benutzer erhalten ihre Geräte und führen den Setup-Assistenten aus, um ihr Gerät zu registrieren. Diese Methode unterstützt den iOS-Modus **Überwacht**, der wiederum Folgendes ermöglicht:
   -    Bedingter Zugriff
   -    Erkennung von Jailbreaks
   -    Mobile Anwendungsverwaltung

Erfahren Sie mehr über die [Setup Assistant enrollment with Apple Configurator (Registrierung über den Setup-Assistenten mit Apple Configurator)](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Zurück zur Tabelle](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Verwaltung mobiler Geräte mit Exchange ActiveSync und Configuration Manager
Mobile Geräte, die nicht registriert, aber mit Exchange ActiveSync (EAS) verbunden sind, können von Intune mit der MDM EAS-Richtlinie verwaltet werden. Intune verwendet Exchange Connector für die Kommunikation mit EAS, entweder lokal oder in der Cloud gehostet.

[Verwaltung mobiler Geräte mit Exchange ActiveSync und Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)


##  <a name="supported-device-platforms"></a>Unterstützte Geräteplattformen

Hybride Verwaltung mobiler Geräte in Configuration Manager kann die folgenden Plattformen für mobile Geräte verwalten:

[!INCLUDE[../includes/mdm-supported-devices](../includes/mdm-supported-devices.md)]

## <a name="next-steps"></a>Nächste Schritte
 - [Prerequisites for device enrollment( Voraussetzungen für die Geräteregistrierung)](../deploy-use/setup-hybrid-mdm.md)
 - [Manage corporate-owned devices (Verwalten firmeneigener Geräte)](../deploy-use/enroll-company-owned-devices.md)



<!--HONumber=Nov16_HO1-->


