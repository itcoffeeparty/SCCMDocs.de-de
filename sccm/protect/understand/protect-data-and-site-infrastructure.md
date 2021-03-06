---
title: Schützen der Daten und Standortinfrastruktur
titleSuffix: Configuration Manager
description: Erfahren Sie mehr darüber, wie Sie die Ressourcen Ihrer Organisation mit System Center Configuration Manager vor Risiken oder böswilligen Angriffen schützen.
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: e76a16fab84f5ccfcd71af4bc80913e31acdadd9
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="protect-data-and-site-infrastructure-with-system-center-configuration-manager"></a>Schützen der Daten und Standortinfrastruktur mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Sie möchten, dass Ihre Benutzer sicher auf die Ressourcen Ihrer Organisation zugreifen können, und zwar so, dass sowohl Ihre Infrastruktur als auch Ihre Daten vor Offenlegung und böswilligen Angriffen geschützt sind. In den folgenden Themen wird beschrieben, wie Sie System Center Configuration Manager (ConfigMgr bzw. SCCM) verwenden, um diesen Zugriff zu aktivieren und die Ressourcen Ihres Unternehmens zu schützen.  

-   Sie können den Aufwand Ihrer Benutzer zum Herstellen einer Verbindung mit Unternehmensressourcen minimieren, indem Sie VPN-Verbindungen mithilfe von VPN-Profilen aktivieren. Weitere Informationen finden Sie unter [VPN profiles in System Center Configuration Manager (VPN-Profile in System Center Configuration Manager)](../deploy-use/vpn-profiles.md).  

-   Über WLAN-Profile stehen eine Reihe von Tools und Ressourcen zur Verfügung, mit deren Hilfe Sie Einstellungen für Funknetzwerke für Geräte in Ihrer Organisation erstellen, bereitstellen und überwachen können. Durch Bereitstellen dieser Einstellungen erleichtern Sie den Endbenutzern das Herstellen einer Verbindung mit Unternehmens-WLANs. Weitere Informationen finden Sie unter [Wi-Fi Profiles in System Center Configuration Manager (WLAN-Profile in System Center Configuration Manager)](/sccm/protect/deploy-use/create-wifi-profiles).  

-   [Certificate profiles in System Center Configuration Manager (Zertifikatprofile in System Center Configuration Manager)](../deploy-use/introduction-to-certificate-profiles.md) wird das Bereitstellen der Zertifikate auf den Geräten Ihrer Benutzer beschrieben, die diese zum Verbinden mit Unternehmensressourcen benötigen.  

-   Mithilfe von [System Center Endpoint Protection](../deploy-use/endpoint-protection.md) können Sie Richtlinien für Antischadsoftware und die Sicherheit der Windows-Firewall für Clientcomputer verwalten.  

-   Verwenden Sie den bedingten Zugriff, um E-Mail- und andere Dienste auf Geräten, die bei Microsoft Intune registriert sind, wie unter [Manage access to services in System Center Configuration Manager (Verwalten des Zugriffs auf Dienste in System Center Configuration Manager)](../deploy-use/manage-access-to-services.md) beschrieben zu schützen.  

-   E-Mail-Profile stellen eine Reihe von Tools und Ressourcen zum Erstellen, Bereitstellen und Überwachen von E-Mail-Einstellungen auf Geräten bereit. Dies gibt Benutzern die Möglichkeit, von ihren persönlichen Geräten aus auf Unternehmens-E-Mails zuzugreifen, ohne dass eine Konfiguration ihrerseits erforderlich ist. Weitere Informationen finden Sie unter [Email profiles in System Center Configuration Manager (E-Mail-Profile in System Center Configuration Manager)](../deploy-use/introduction-to-email-profiles.md).  

-   Configuration Manager ermöglicht die Integration in Windows Hello for Business (ehemals Microsoft Passport for Work), eine alternative Anmeldemethode, die Active Directory oder ein Azure Active Directory-Konto verwendet, um ein Kennwort, eine Smartcard oder eine virtuelle Smartcard zu ersetzen. Weitere Informationen finden Sie unter [Windows Hello for Business settings in System Center Configuration Manager (Windows Hello for Business-Einstellungen in System Center Configuration Manager)](../deploy-use/windows-hello-for-business-settings.md).  
