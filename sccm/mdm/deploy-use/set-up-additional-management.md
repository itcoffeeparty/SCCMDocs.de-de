---
title: Einrichten zusätzlicher Verwaltung
titleSuffix: Configuration Manager
description: Einrichten zusätzlicher Verwaltung unter Verwendung des System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a61dffbdd9b04d3e872e23f88ddc0ac864f99d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>Einrichten zusätzlicher Verwaltung unter Verwendung des System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

(Optional) Sie können eine zusätzliche Verwaltung einrichten, bevor Geräte registriert werden. Diese Verwaltungslösungen können nach der Registrierung von Geräten erstellt und bereitgestellt werden, obwohl viele Organisationen Geräte bevorzugt bereitstellen, wenn sie in die Verwaltung eingebunden sind.

**Konfigurationselemente** ermöglichen Ihnen, Einstellungen, wie z.B. Erfordern einer PIN oder Erfordern von Verschlüsselung auf registrierten Geräten, auf der Grundlage der Geräteplattform zu verwalten:
- [Windows 10- und Windows 8.1-Geräte](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Windows Phone-Geräte](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [iOS- und Macintosh-Geräte](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Android- und Samsung KNOX Standard-Geräte](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

**Anwendungen** können auf verwalteten Geräten bereitgestellt werden:
- [iOS-Anwendungen](creating-ios-applications.md)
- [Macintosh-Anwendungen](../../apps/get-started/creating-mac-computer-applications.md)
- [Windows-PC-Anwendungen](../../apps/get-started/creating-windows-applications.md)
- [Windows Phone-Anwendungen](creating-windows-phone-applications.md)
- [Android-Anwendungen](creating-android-applications.md)

**Bedingter Zugriff** ermöglicht die Verwaltung des Zugriffs auf Unternehmensressourcen, einschließlich:  
- [E-Mail-Zugriff](manage-email-access.md)
- [SharePoint-Zugriff](manage-sharepoint-online-access.md)
- [Skype for Business-Zugriff](manage-skype-for-business-online-access.md)
- [Dynamics CRM Online](manage-dynamics-crm-online-access.md)

**Mehrstufige Authentifizierung (Multi-factor Authentication, MFA)** erfordert mehr als eine Überprüfungsmethode, die den Anmeldungen und Transaktionen von Benutzern eine wichtige zweite Sicherheitsebene hinzufügt.
Bisher haben Sie MFA für Intune-Registrierungen entweder in der Intune-Konsole oder der Configuration Manager-Konsole festgelegt. Melden Sie sich nun beim [Microsoft Azure-Portal](https://manage.windowsazure.com) mit Ihren Intune-Anmeldeinformationen an und konfigurieren die MFA-Einstellungen über Azure AD. Weitere Informationen finden Sie unter [Multi-Factor Authentication für Intune-Geräteregistrierungen](https://aka.ms/mfa_ad).

> [!div class="button"]
[< Vorheriger Schritt](enable-platform-enrollment.md) [Nächster Schritt >](verify-mdm-configuration.md)
