---
title: Verwalten des SharePoint Online-Zugriffs | Microsoft-Dokumentation
description: "Hier erfahren Sie, wie Sie mit der Richtlinie für bedingten Zugriff von System Center Configuration Manager SharePoint Online zur Verwaltung des Zugriffs auf OneDrive verwenden."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
caps.latest.revision: "11"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: c564c1fc25c5156a2d9ddfa1b4123024c658bf61
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Verwalten des SharePoint Online-Zugriffs in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Verwenden Sie die Richtlinie für bedingten Zugriff von System Center Configuration Manager **SharePoint Online** zum Verwalten des Zugriffs auf OneDrive for Business-Dateien in SharePoint Online basierend auf den von Ihnen angegebenen Bedingungen.
Sie können den Zugriff auf SharePoint Online über die folgenden Apps für die aufgeführten Plattformen steuern:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android und iOS)  

-   Microsoft Word (Android und iOS)  

-   Microsoft Excel (Android und iOS)  

-   Microsoft PowerPoint (Android und iOS)  

-   Microsoft OneNote (Android und iOS)

Office-Desktopanwendungen können auf PCs, auf denen Folgendes ausgeführt wird, auf SharePoint Online zugreifen:  

-   Office-Desktop 2013 und höher mit aktivierter [moderner Authentifizierung](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) .  

-   Windows 7.0 oder Windows 8.1  

> [!NOTE]  
>  PCs müssen in eine Domäne eingebunden oder mit den in Intune festgelegten Richtlinien kompatibel sein.  



 Wenn ein bestimmten Benutzer versucht, mit einer unterstützten App wie z. B. OneDrive auf seinem Gerät eine Verbindung mit einer Datei herzustellen, erfolgt die folgende Auswertung:  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Zum Herstellen einer Verbindung mit den gewünschten Dateien muss das Gerät, auf dem OneDrive ausgeführt wird, die folgenden Voraussetzungen erfüllen:  

-   Das Gerät muss bei Microsoft Intune oder einem in die Domäne eingebundenen PC registriert sein.  

-   Das Gerät muss in Azure Active Directory registriert sein (dies erfolgt automatisch bei der Registrierung des Geräts in Intune).  

     Bei in die Domäne eingebundenen PCs müssen Sie es für eine [automatische Registrierung](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) bei Azure Active Directory einrichten.  

-   Sie müssen mit allen bereitgestellten Kompatibilitätsrichtlinien von Configuration Manager kompatibel sein  

 Der Gerätestatus wird in Azure Active Directory gespeichert. Die Anwendung gewährt oder blockiert den Zugriff auf Dateien entsprechend den von Ihnen angegebenen Bedingungen.  

 Wenn eine Bedingung nicht erfüllt wird, erhält der Benutzer bei der Anmeldung die folgenden Meldungen:  

-   Wenn das Gerät nicht bei Intune oder in Azure Active Directory registriert ist, wird eine Meldung mit Anweisungen zum Installieren der Unternehmensportal-App und zum Registrieren des Geräts angezeigt.  

-   Wenn das Gerät nicht kompatibel ist, wird eine Meldung angezeigt, die den Benutzer zum Intune-Webportal weiterleitet. Hier finden Sie Informationen über das Problem und dessen Lösung.  

- Für mobile Geräte:

  Sie können den Zugriff auf SharePoint Online verweigern, wenn der Zugriff von einem Browser von **iOS**- und **Android**-Geräten erfolgt.  Der Zugriff wird nur von unterstützten Browsern auf kompatiblen Geräten gewährt:
* Safari (iOS)
* Chrome (Android)
* Managed Browser (iOS und Android)

  Nicht unterstützte Browser werden blockiert.
-   Für PCs:  


    -   Wenn die Richtlinie das Beitreten zu einer Domäne erfordert und der PC nicht in die Domäne eingebunden ist, wird die Meldung angezeigt, dass der IT-Administrator kontaktiert werden sollte.  

    -   Wenn die Richtlinie das Beitreten zu einer Domäne oder Kompatibilität erfordert und der PC keine der Anforderungen erfüllt, wird eine Meldung mit einer Anleitung zum Installieren der Unternehmensportal-App und zur Registrierung angezeigt.  

 Sie können den Zugriff auf SharePoint Online in den folgenden Apps blockieren:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android und iOS)  

-   Microsoft Word (Android und iOS)  

-   Microsoft Excel (Android und iOS)  

-   Microsoft PowerPoint (Android und iOS)  

-   Microsoft OneNote (Android und iOS)  

## <a name="configure-conditional-access-for-sharepoint-online"></a>Konfigurieren des bedingten Zugriffs für SharePoint Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Schritt 1: Konfigurieren von Active Directory-Sicherheitsgruppen  
 Bevor Sie beginnen, konfigurieren Sie Azure Active Directory-Sicherheitsgruppen für die bedingte Zugriffsichtlinie. Sie können diese Gruppen im **Office 365 Admin Center**oder **Intune-Kontenportal**konfigurieren. Die Gruppen enthalten die Benutzer, für die die Richtlinie gelten soll oder die davon ausgeschlossen sind. Bei Benutzern, für die eine Richtlinie gelten soll, muss jedes von ihnen verwendete Gerät die Richtlinie erfüllen, damit sie auf Ressourcen zugreifen können.  

 Sie können zwei Arten von Gruppentypen in einer SharePoint Online-Richtlinie angeben:  

-   **Zielgruppen** – Gruppen von Benutzern, für die die Richtlinie gelten soll  

-   **Ausgenommene Gruppen** – Gruppen von Benutzern, die von der Richtlinie ausgenommen sind (optional)  

 Benutzer, die in beiden Gruppen enthalten sind, werden von der Richtlinie ausgenommen.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Schritt 2: Konfigurieren und Bereitstellen einer Kompatibilitätsrichtlinie  
 Wichtig ist, dass Sie für alle Geräte, für die die SharePoint Online-Richtlinie gelten soll, eine Kompatibilitätsrichtlinie erstellen und bereitstellen.  

> [!NOTE]  
>  Wenn Kompatibilitätsrichtlinien für Intune-Gruppen oder Configuration Manager-Sammlungen bereitgestellt werden, gelten bedingte Zugriffsrichtlinien für Azure Active Directory-Sicherheitsgruppen.  

 Ausführliche Informationen zum Konfigurieren der Kompatibilitätsrichtlinie finden Sie unter [Verwalten von Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Wenn Sie keine Kompatibilitätsrichtlinie bereitgestellt haben und dann die SharePoint Online-Richtlinie aktivieren, wird allen Zielgeräten der Zugriff erlaubt.  

 Wenn Sie soweit sind, fahren Sie mit **Schritt 3**fort.  

###  <a name="BKMK_OneDrive"></a> Schritt 3: Konfigurieren der SharePoint Online-Richtlinie  


 Anschließend konfigurieren Sie die Richtlinie so, dass nur verwaltete und kompatible Geräte auf SharePoint Online zugreifen dürfen. Diese Richtlinie wird in Azure Active Directory gespeichert.

 >[!NOTE]
 >Richtlinien für den bedingten Zugriff können auch in der Azure AD-Verwaltungskonsole erstellt werden. Mithilfe der Azure AD-Verwaltungskonsole können neben den anderen Richtlinien für den bedingten Zugriff wie die Multi-Factor Authentication auch die Richtlinien für den bedingten Zugriff für Intune-Geräte (als Richtlinie für den gerätebasierten bedingten Zugriff in Azure AD bezeichnet) erstellt werden. Es können auch Richtlinien für den bedingten Zugriff für von Azure AD unterstützte Unternehmensanwendungen von Drittanbietern wie Salesforce und Box festgelegt werden. Weitere Informationen finden Sie unter [How to set Azure Active Directory device-based conditional access policy for access control to Azure Active Directory connected applications (Festlegen von Azure Active Directory-Richtlinien für den gerätebasierten bedingten Zugriff zur Zugriffssteuerung bei Anwendungen, die mit Azure Active Directory verbunden sind)](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/).  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Wählen Sie **Bedingte Zugriffsrichtlinie für SharePoint Online aktivieren**aus.  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  Unter **Anwendungszugriff** können Sie den Zugriff für Outlook sowie für Apps mit moderner Authentifizierung auf Geräte beschränken, die für jede Plattform kompatibel sind.  

    > [!TIP]  
    >  Die**moderne Authentifizierung** ermöglicht das ADAL-basierte (Active Directory Authentication Library) Anmelden für Office-Clients.  
    >   
    >  -   Die ADAL-basierte Authentifizierung ermöglicht Office-Clients die Einbindung in die browserbasierte Authentifizierung (auch als passive Authentifizierung bekannt).  Der Benutzer wird zur Authentifizierung zu einer Anmeldewebseite umgeleitet.  
    > -   Diese neue Anmeldemethode ermöglicht neue Szenarien, z. B. den bedingten Zugriff, auf Grundlage der **Gerätekompatibilität** und in Abhängigkeit davon, ob eine **mehrstufige Authentifizierung** erfolgt ist.  
    >   
    >  Dieser [Artikel](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) enthält ausführlichere Informationen zur Funktionsweise der modernen Authentifizierung.  

     Bei Windows-PCs muss der PC entweder in die Domäne eingebunden oder bei Intune registriert und kompatibel sein. Sie können die folgenden Anforderungen festlegen:  

    -   **Geräte müssen in eine Domäne eingebunden oder kompatibel sein.** Dies bedeutet, dass PCs entweder in die Domäne eingebunden oder mit den in Intune festgelegten Richtlinien kompatibel sein müssen. Wenn der PC keine der Anforderungen erfüllt, wird der Benutzer aufgefordert, das Gerät bei Intune zu registrieren.  

    -   **Geräte müssen in eine Domäne eingebunden sein.** Dies bedeutet, dass die PCs für den Zugriff auf Exchange Online in die Domäne eingebunden sein müssen. Wenn der Computer in keine Domäne eingebunden ist, wird der E-Mail-Zugriff blockiert und der Benutzer aufgefordert, den IT-Administrator zu kontaktieren.  

    -   **Geräte müssen kompatibel sein.** Dies bedeutet, dass die PCs bei Intune registriert und kompatibel sein müssen. Wenn der PC nicht registriert ist, wird eine Meldung mit Anweisungen zur Registrierung angezeigt.  

4.  Unter „**Browser access** to SharePoint Online and OneDrive for Business“ (Browseraccess auf SharePoint Online und OneDrive for Business) können Sie festlegen, ob der Zugriff auf Exchange Online nur über die unterstützten Browser gewährt werden soll: Safari (iOS) und Chrome (Android). Der Zugriff über andere Browser wird blockiert.  Die gleichen Plattformbeschränkungen, die Sie für „Application access for OneDrive“ (Anwendungszugriff für OneDrive) ausgewählt haben, gelten auch hier.

    Benutzer müssen auf **Android** -Geräten den Browserzugriff aktivieren.  Der Endbenutzer muss hierzu die Option „Browserzugriff aktivieren“ wie folgt auf dem registrierten Gerät aktivieren:
    1.  Starten Sie die **Unternehmensportal-App**.
    2.  Rufen Sie die Seite **Einstellungen** über die Schaltfläche mit den drei Punkten (…) oder über die physische Menütaste auf.
    3.  Drücken Sie die Schaltfläche **Browserzugriff aktivieren** .
    4.  Melden Sie sich im Chrome-Browser von Office 365 ab, und starten Sie Chrome erneut.

    Azure Active Directory führt ein TLS-Zertifikat (Transport Layer Security) auf dem Gerät aus, um auf **iOS und Android** -Plattformen das Gerät zu identifizieren, das für den Zugriff auf den Dienst verwendet wird.  Das Gerät zeigt das Zertifikat zusammen mit einer Aufforderung an den Endbenutzer an, der das Zertifikat auswählen muss, so wie in den folgenden Screenshots gezeigt. Der Endbenutzer muss dieses Zertifikat auswählen, bevor der Browser weiterhin verwendet werden kann.

     **iOS**

     ![Screenshot der Zertifikataufforderung auf einem iPad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Android**

      ![Screenshot der Zertifikataufforderung auf einem Android-Gerät](media/mdm-browser-ca-android-cert-prompt.png)

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Links** auf **Richtlinie für bedingten Zugriff in der Intune-Konsole konfigurieren**. Sie müssen möglicherweise den Benutzernamen und das Kennwort des Kontos angeben, das zum Verbinden von Configuration Manager mit Intune verwendet wird.  

     Die Intune-Verwaltungskonsole wird geöffnet.  

5.  Klicken Sie in der [Microsoft Intune-Verwaltungskonsole](https://manage.microsoft.com)auf **Richtlinie** > **Bedingter Zugriff** > **SharePoint Online Richtlinie**.  

6.  Wählen Sie **Verhindern, dass Apps auf SharePoint Online zugreifen, wenn das Gerät nicht konform ist**.  

7.  Klicken Sie unter **Zielgruppen**auf **Ändern** , um die Active Directory-Sicherheitsgruppen auszuwählen, für die die Richtlinie gelten soll.  

8.  Klicken Sie unter **Ausgenommene Gruppen**optional auf **Ändern** , um die Active Directory-Sicherheitsgruppen auszuwählen, die von dieser Richtlinie ausgenommen werden.  

9. Klicken Sie abschließend auf **Speichern**.  

 Die Richtlinie für bedingten Zugriff wird sofort wirksam und muss nicht explizit bereitgestellt werden.  

 Unter [Verwalten des Zugriffs auf SharePoint Online mit Microsoft Intune](https://technet.microsoft.com/library/dn705844.aspx) finden Sie Informationen zum Überwachen der Richtlinie in der Intune-Konsole.  

### <a name="see-also"></a>Weitere Informationen:  

 [Verwalten des Zugriffs auf Dienste in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
