---
title: Bedingter Zugriff
titleSuffix: Configuration Manager
description: "Erfahren Sie, wie Sie den bedingten Zugriff in System Center Configuration Manager verwenden, um Ihre E-Mails und andere Dienste zu schützen."
ms.custom: na
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: "26"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: f215e1c22d40e1fe402084b665ae624bc0c21d97
ms.sourcegitcommit: 92c3f916e6bbd35b6208463ff406e0247664543a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>Verwalten des Zugriffs auf Dienste in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>Bedingter Zugriff in System Center Configuration Manager
Verwenden Sie den bedingten Zugriff, um Bedingungen zum Schutz von E-Mails und andere Diensten auf Geräten, die mit Microsoft Intune registriert sind, festzulegen.  

 Informationen zum bedingten Zugriff auf Geräte, die mit dem Configuration Manager-Client verwaltet werden, finden Sie unter [Verwalten des Zugriffs auf Office 365-Dienste für PCs, die von System Center Configuration Manager verwaltet werden](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


 Ein typischer Ablauf für bedingten Zugriff könnte wie folgt aussehen:  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Verwenden Sie den bedingten Zugriff zum Verwalten des Zugriffs auf folgende Dienste:  

-   Microsoft Exchange lokal  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated  

-   SharePoint Online  

-   Skype for Business Online

-   Dynamics CRM Online

 Um den bedingten Zugriff zu implementieren, konfigurieren Sie zwei Richtlinientypen in Configuration Manager:  

-   **Konformitätsrichtlinien** sind optionale Richtlinien, die Sie für Benutzersammlungen bereitstellen können. Mit diesen Richtlinien werden Einstellungen wie die folgenden ausgewertet:  

    -   Passwort  

    -   Verschlüsselung  

    -   Ob das Gerät per Jailbreak oder Rooting manipuliert wurde  

    -   Ob E-Mails auf dem Gerät von Configuration Manager oder einer Microsoft Intune-Richtlinie verwaltet werden  

     Ein Gerät meldet alle anwendbaren bedingten Zugriffsrichtlinien als konform, wenn Sie keine Konformitätsrichtlinie dazu bereitstellen.

-   **Richtlinien für bedingten Zugriff** gelten für einen bestimmten Dienst. Diese Richtlinien definieren Regeln, z.B. welche Azure Active Directory-Sicherheitsbenutzergruppen oder Configuration Manager-Benutzersammlungen von Richtlinien einbezogen oder ausgenommen werden sollen.  

     Sie konfigurieren die Richtlinie für den bedingten lokalen Exchange-Zugriff über die Configuration Manager-Konsole. Wenn Sie jedoch eine Exchange Online- oder SharePoint Online-Richtlinie konfigurieren, wird die Microsoft Intune-Verwaltungskonsole geöffnet, in der Sie die Richtlinie konfigurieren.  

     Im Gegensatz zu anderen Microsoft Intune- oder Configuration Manager-Richtlinien stellen Sie keine Richtlinien für den bedingten Zugriff bereit. Stattdessen konfigurieren Sie diese Richtlinien einmalig; anschließend gelten sie für alle Zielbenutzer.  

 Wenn Geräte die konfigurierten Bedingungen nicht erfüllen, erhält der Benutzer Anweisungen zum Registrieren des Geräts und zum Beheben des Gerätekonformitätsproblems.  

Bevor Sie den bedingten Zugriff verwenden können, müssen Sie sicherstellen, dass die jeweiligen Anforderungen erfüllt sind:  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Anforderungen für Exchange Online (bei Verwendung der freigegebenen Umgebung mit mehreren Mandanten)
Bedingter Zugriff auf Exchange Online unterstützt Geräte, die Folgendes ausführen:
-   Windows 8.1 und höher (bei Registrierung mit Intune)
-   Windows 7.0 oder Windows 8.1 (bei Einbindung in eine Domäne)
-   Windows Phone 8.1 und höher
-   iOS 7.1 und höher
-   Android 4.0 und höher, Samsung KNOX Standard 4.0 und höher

 **Darüber hinaus gilt**:
-   Geräte erfordern eine Verknüpfung mit dem Arbeitsplatz, wodurch das Gerät beim Azure Active Directory Device Registration Service (AAD DRS) registriert wird.<br />     
- In eine Domäne eingebundene PCs müssen automatisch über eine Gruppenrichtlinie oder MSI bei Azure Active Directory registriert werden.

  Im Abschnitt **Bedingter Zugriff für PCs** in diesem Artikel sind alle Anforderungen für die Aktivierung des bedingten Zugriffs für einen PC beschrieben.<br />     
  AAD DRS wird automatisch für Kunden von Microsoft Intune und Office 365 aktiviert. Kunden, die bereits den AD FS Device Registration Service bereitgestellt haben, sehen keine registrierten Geräte in ihrem lokalen Active Directory.
-   Verwenden Sie ein Office 365-Abonnement, das Exchange Online enthält (z.B. E3). Benutzer müssen für Exchange Online lizenziert werden.
-   Der Exchange Server-Connector ist optional und verbindet Configuration Manager mit Microsoft Exchange Online. Dieser Connector hilft Ihnen dabei, die Geräteinformationen über die Configuration Manager-Konsole zu überwachen. Weitere Informationen finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Microsoft Intune](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
Sie benötigen den Connector nicht, um Konformitätsrichtlinien oder Zugriffsrichtlinien zu verwenden. Zum Ausführen von Berichten zu den Auswirkungen des bedingten Zugriffs wird der Connector benötigt.

## <a name="requirements-for-exchange-online-dedicated"></a>Anforderungen für Exchange Online Dedicated
Bedingter Zugriff auf Exchange Online Dedicated unterstützt Geräte, die Folgendes ausführen:
-   Windows 8 und höher (bei Registrierung mit Intune)
-   Windows 7.0 oder Windows 8.1 (bei Einbindung in eine Domäne)

  Bedingter Zugriff auf PCs, die in eine Domäne eingebunden sind, nur für Mandanten in der neuen Exchange Online Dedicated-Umgebung.
-   Windows Phone 8 und höher
-   Beliebige iOS-Geräte, die einen Exchange ActiveSync-E-Mail-Client (EAS) verwenden
-   Android 4 und höher
-   Für Mandanten in der Exchange Online Dedicated-Legacyumgebung gilt Folgendes:    

  Verwenden Sie den Exchange Server-Connector, der Configuration Manager mit lokalem Microsoft Exchange verbindet. Der Connector ermöglicht Ihnen die Verwaltung von Mobilgeräten und den bedingten Zugriff. Weitere Informationen finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Microsoft Intune](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
-   Für Mandanten in der neuen Exchange Online Dedicated-Umgebung gilt Folgendes:     
  Der Exchange Server-Connector ist optional, verbindet Configuration Manager mit Microsoft Exchange Online, und hilft Ihnen bei der Verwaltung von Geräteinformationen. Weitere Informationen finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Microsoft Intune](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md). Sie benötigen den Connector nicht, um Konformitätsrichtlinien oder Zugriffsrichtlinien zu verwenden. Zum Ausführen von Berichten zu den Auswirkungen des bedingten Zugriffs wird der Connector benötigt.  

## <a name="requirements-for-exchange-on-premises"></a>Anforderungen für Microsoft Exchange lokal
Beim bedingten Zugriff auf Microsoft Exchange lokal wird Folgendes unterstützt:
-   Windows 8 und höher (bei Registrierung mit Intune)
-   Windows Phone 8 und höher
-   Systemeigene E-Mail-App unter iOS
-   Systemeigene E-Mail-App unter Android 4 oder höher
-   Microsoft Outlook-App wird nicht unterstützt (Android und iOS)

**Darüber hinaus gilt**:

- Es muss sich bei der Exchange-Version um Exchange 2010 oder höher handeln
- Exchange Server-Clientzugriffsserver-Arrays (CAS) werden unterstützt

> [!TIP]
> Wenn sich Ihre Exchange-Umgebung in einer Clientzugriffsserver-Konfiguration befindet, müssen Sie den lokalen Exchange-Connector so konfigurieren, dass er auf einen der Clientzugriffsserver zeigt.
- Verwenden Sie den Exchange Server-Connector, der Configuration Manager mit lokalem Microsoft Exchange verbindet. Der Connector ermöglicht Ihnen die Verwaltung von Mobilgeräten und den bedingten Zugriff. Weitere Informationen finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Microsoft Intune](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Stellen Sie sicher, dass Sie die neueste Version des lokalen Exchange-Connectors verwenden. Konfigurieren Sie den lokalen Exchange-Connector über die Configuration Manager-Konsole. Eine ausführliche exemplarische Vorgehensweise finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Konfigurieren Sie den Connector nur am primären Configuration Manager-Standort

- Exchange ActiveSync kann mit zertifikatbasierter Authentifizierung oder Eingabe von Anmeldeinformationen konfiguriert werden


## <a name="requirements-for-skype-for-business-online"></a>Anforderungen für Skype for Business Online
Bedingter Zugriff auf SharePoint Online unterstützt Geräte, die Folgendes ausführen:
 -   iOS 7.1 und höher
 -   Android 4,0 und höher
 -   Samsung KNOX Standard 4.0 oder höher

Aktivieren Sie die [moderne Authentifizierung](https://aka.ms/SkypeModernAuth) für Skype for Business Online. 

Alle Benutzer müssen Skype for Business Online verwenden. Wenn Sie eine Bereitstellung sowohl mit Skype for Business Online als auch Skype for Business On-Premises (Lokal) haben, wird die Richtlinie für bedingten Zugriff nicht für lokale Benutzer angewendet.

## <a name="requirements-for-sharepoint-online"></a>Anforderungen für SharePoint Online
Bedingter Zugriff auf SharePoint Online unterstützt Geräte, die Folgendes ausführen:
 -   Windows 8.1 und höher (bei Registrierung mit Intune)
 -   Windows 7.0 oder Windows 8.1 (bei Einbindung in eine Domäne)
 -   Windows Phone 8.1 und höher
 -   iOS 7.1 und höher
 -   Android 4.0 und höher, Samsung KNOX Standard 4.0 und höher

 **Darüber hinaus gilt**:
 -   Geräte erfordern eine Verknüpfung mit dem Arbeitsplatz, wodurch das Gerät beim Azure Active Directory Device Registration Service (AAD DRS) registriert wird.

 In eine Domäne eingebundene PCs müssen automatisch über eine Gruppenrichtlinie oder MSI bei Azure Active Directory registriert werden. Im Abschnitt **Bedingter Zugriff für PCs** in diesem Artikel sind alle Anforderungen für die Aktivierung des bedingten Zugriffs für einen PC beschrieben.

 AAD DRS wird automatisch für Kunden von Microsoft Intune und Office 365 aktiviert. Kunden, die bereits den AD FS Device Registration Service bereitgestellt haben, sehen keine registrierten Geräte in ihrem lokalen Active Directory.
 -   Es ist ein SharePoint Online-Abonnement erforderlich, und Benutzer müssen für SharePoint Online lizenziert sein.

 ### <a name="conditional-access-for-pcs"></a>Bedingter Zugriff für PCs

 Sie können den bedingten Zugriff für PCs konfigurieren, die Office-Desktopanwendungen ausführen und auf Exchange Online oder SharePoint Online zugreifen können. Die PCs müssen folgende Anforderungen erfüllen:
 -   Auf dem PC muss Windows 7.0 oder Windows 8.1 ausgeführt werden
 -   Der PC muss entweder in eine Domäne eingebunden oder konform sein

 Damit der PC konform ist, muss er bei Microsoft Intune registriert sein und den Richtlinien entsprechen.

 Für in die Domäne eingebundene PCs müssen Sie [das Gerät für eine automatische Registrierung](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) bei Azure Active Directory einrichten.
 -   [Die moderne Authentifizierung von Office 365 muss aktiviert sein](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)und alle neuesten Office-Updates enthalten.<br />     Die moderne Authentifizierung ermöglicht Windows-Clients mit Office 2013 eine Active Directory Authentication Library-basierte Anmeldung (ADAL) und bietet größere Sicherheit wie mehrstufige Authentifizierung und zertifikatbasierte Authentifizierung.
 -   Setup-ADFS beansprucht Regeln zum Blockieren von nicht moderner Authentifizierungsprotokolle.  

## <a name="next-steps"></a>Nächste Schritte  
 Lesen Sie die folgenden Themen, um mehr über das Konfigurieren von Konformitätsrichtlinien und Richtlinien für den bedingten Zugriff für Ihr Szenario zu erfahren:  

-   [Verwalten von Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

-   [Verwalten des E-Mail-Zugriffs in System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

-   [Verwalten des SharePoint Online-Zugriffs in System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Verwalten des Zugriffs auf Skype for Business Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>Weitere Informationen:  

 [Erste Schritte mit Kompatibilitätseinstellungen in System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)
