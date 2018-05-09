---
title: Verwalten des Zugriffs auf SharePoint Online
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie mit der Richtlinie für bedingten Zugriff von System Center Configuration Manager SharePoint Online zur Verwaltung des Zugriffs auf OneDrive verwenden.
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f723110abdb94dd96fb2ed7f52af681d27fccf87
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Verwalten des SharePoint Online-Zugriffs in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Die Richtlinie für bedingten Zugriff von Configuration Manager für **SharePoint Online** verwaltet den Zugriff auf OneDrive for Business-Dateien, die in SharePoint Online gespeichert sind. Der Zugriff hängt von Bedingungen ab, die Sie angeben.
Sie können den Zugriff auf SharePoint Online über die folgenden Apps für die aufgeführten Plattformen steuern:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android und iOS)  

-   Microsoft Word (Android und iOS)  

-   Microsoft Excel (Android und iOS)  

-   Microsoft PowerPoint (Android und iOS)  

-   Microsoft OneNote (Android und iOS)

Office-Desktopanwendungen können auf PCs, auf denen Folgendes ausgeführt wird, auf SharePoint Online zugreifen:  

-   Office-Desktop 2013 und höher mit aktivierter [moderner Authentifizierung](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) .  

-   Windows 7.0 oder Windows 8.1  

> [!NOTE]  
>  PCs müssen in eine Domäne eingebunden oder mit den in Intune festgelegten Richtlinien kompatibel sein.  



 Wenn ein bestimmter Benutzer versucht, mit einer unterstützten App wie z.B. OneDrive auf seinem Gerät eine Verbindung mit einer Datei herzustellen, erfolgt die folgende Auswertung:  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Zum Herstellen einer Verbindung mit den gewünschten Dateien muss das Gerät, auf dem OneDrive ausgeführt wird, die folgenden Voraussetzungen erfüllen:  

-   Das Gerät muss bei Microsoft Intune oder einem in die Domäne eingebundenen PC registriert sein.  

-   Registrieren Sie das Gerät in Azure Active Directory (Azure AD). Diese Registrierung erfolgt automatisch, wenn das Gerät bei Intune registriert wird.  

     Bei den in die Domäne eingebundenen PCs müssen Sie es für eine [automatische Registrierung](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) bei Azure AD einrichten.  

-   Sie müssen mit allen bereitgestellten Kompatibilitätsrichtlinien von Configuration Manager kompatibel sein  

    Azure AD speichert den Gerätezustand. Entsprechend den von Ihnen angegebenen Bedingungen wird der Zugriff auf die Dateien gewährt oder blockiert.  

    Wenn eine Bedingung nicht erfüllt wird, erhält der Benutzer bei der Anmeldung eine der folgenden Meldungen:  

-   Wenn das Gerät nicht bei Intune oder in Azure AD registriert ist, wird eine Meldung mit Anweisungen zum Installieren der Unternehmensportal-App und zum Registrieren des Geräts angezeigt.  

-   Wenn das Gerät nicht kompatibel ist, wird eine Meldung angezeigt, die den Benutzer zum Webportal von Intune weiterleitet. Dort finden sie Informationen über das Problem und dessen Behebung.  

- Für mobile Geräte:

  Sie können den Zugriff auf SharePoint Online einschränken, wenn der Zugriff von einem Browser von **iOS**- und **Android**-Geräten erfolgt. Der Zugriff wird nur von unterstützten Browsern auf kompatiblen Geräten gewährt:  
    - Safari (iOS)
    - Chrome (Android)
    - Managed Browser (iOS und Android)  

    Nicht unterstützte Browser sind blockiert.  

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
 Bevor Sie beginnen, konfigurieren Sie Azure AD-Sicherheitsgruppen für die Richtlinie für bedingten Zugriff. Sie können diese Gruppen im **Office 365 Admin Center**oder **Intune-Kontenportal**konfigurieren. Die Gruppen beinhalten die Benutzer, für die die Richtlinie gelten soll, oder die davon ausgeschlossen sind. Bei Benutzern, für die eine Richtlinie gelten soll, muss jedes von ihnen verwendete Gerät die Richtlinie erfüllen, damit sie auf Ressourcen zugreifen können.  

 Sie können zwei Arten von Gruppentypen in einer SharePoint Online-Richtlinie angeben:  

-   **Zielgruppen**: Gruppen von Benutzern, für die die Richtlinie gelten soll  

-   **Ausgenommene Gruppen**: Gruppen von Benutzern, die von der Richtlinie ausgenommen sind (optional)  

 Benutzer, die in beiden Gruppen enthalten sind, werden von der Richtlinie ausgenommen.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Schritt 2: Konfigurieren und Bereitstellen einer Kompatibilitätsrichtlinie  
 Erstellen Sie für alle Geräte, für die die SharePoint Online-Richtlinie gelten soll, eine Konformitätsrichtlinie und stellen Sie sie bereit.  

> [!NOTE]   
>  Wenn Kompatibilitätsrichtlinien für Intune-Gruppen oder Configuration Manager-Sammlungen bereitgestellt werden, gelten Richtlinien für bedingten Zugriff für Azure AD-Sicherheitsgruppen.  

 Ausführliche Informationen zum Konfigurieren der Kompatibilitätsrichtlinie finden Sie unter [Verwalten von Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Wenn Sie keine Kompatibilitätsrichtlinie bereitgestellt haben und dann die SharePoint Online-Richtlinie aktivieren, wird allen Zielgeräten der Zugriff erlaubt.  

   

###  <a name="BKMK_OneDrive"></a> Schritt 3: Konfigurieren der SharePoint Online-Richtlinie  

 Anschließend konfigurieren Sie die Richtlinie so, dass nur verwaltete und konforme Geräte auf SharePoint Online zugreifen dürfen. Diese Richtlinie ist in Azure AD gespeichert.

 >[!NOTE]
 >Richtlinien für den bedingten Zugriff können auch in der Azure AD-Verwaltungskonsole erstellt werden. Mit der Azure AD-Verwaltungskonsole können Sie die Richtlinien für den bedingten Zugriff auf Intune-Geräte erstellen. Azure AD bezeichnet diese Richtlinien als gerätebasierte Richtlinie für bedingten Zugriff. Sie können auch andere Richtlinien für den bedingten Zugriff erstellen, z.B. die mehrstufige Authentifizierung. Im Portal können auch Richtlinien für den bedingten Zugriff für von Azure AD unterstützte Unternehmensanwendungen von Drittanbietern wie Salesforce und Box festgelegt werden. Weitere Informationen finden Sie unter [How to set Azure AD device-based conditional access policy for access control to Azure AD connected applications (Festlegen von Azure AD-Richtlinien für den gerätebasierten bedingten Zugriff zur Zugriffssteuerung bei Anwendungen, die mit Azure AD verbunden sind)](/azure/active-directory/active-directory-conditional-access-policy-connected-applications).  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Wählen Sie **Bedingte Zugriffsrichtlinie für SharePoint Online aktivieren** aus.  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  Unter **Anwendungszugriff** können Sie den Zugriff für Outlook sowie für Apps mit moderner Authentifizierung auf Geräte beschränken, die für jede Plattform kompatibel sind.  

    > [!TIP]  
    >  Die **moderne Authentifizierung** ermöglicht das ADAL-basierte (Active Directory Authentication Library) Anmelden für Office-Clients.  
    >   
    >  -   Die ADAL-basierte Authentifizierung ermöglicht Office-Clients die Einbindung in die browserbasierte Authentifizierung (auch als passive Authentifizierung bekannt). Der Benutzer wird zur Authentifizierung zu einer Anmeldewebseite umgeleitet.  
    > -   Diese neue Anmeldemethode ermöglicht neue Szenarios, z.B. den bedingten Zugriff auf Grundlage der **Gerätekompatibilität** und in Abhängigkeit davon, ob eine **mehrstufige Authentifizierung** erfolgt ist.  
    >   
    >  Weitere Informationen finden Sie unter [How modern authentication works for Office 2013 and Office 2016 client apps (Funktionsweise der modernen Authentifizierung für Client-Apps für Office 2013 und Office 2016)](https://support.office.com/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517).  

     Bei Windows-PCs muss der PC entweder in die Domäne eingebunden oder bei Intune registriert und kompatibel sein. Sie können die folgenden Anforderungen festlegen:  

    -   **Geräte müssen der Domäne beitreten oder kompatibel sein**: PCs müssen entweder in die Domäne eingebunden oder mit den in Intune festgelegten Richtlinien kompatibel sein. Wenn der PC keine der Anforderungen erfüllt, wird der Benutzer aufgefordert, das Gerät bei Intune zu registrieren.  

    -   **Geräte müssen der Domäne beitreten**: PCs müssen für den Zugriff auf Exchange Online in die Domäne eingebunden sein. Wenn der Computer in keine Domäne eingebunden ist, wird der E-Mail-Zugriff blockiert und der Benutzer dazu aufgefordert, den IT-Administrator zu kontaktieren.  

    -   **Geräte müssen kompatibel sein**: PCs müssen bei Intune registriert und kompatibel sein. Wenn der PC nicht registriert ist, wird eine Meldung mit Anweisungen zur Registrierung angezeigt.  

4.  Unter „**Browser access** to SharePoint Online and OneDrive for Business“ (Browseraccess auf SharePoint Online und OneDrive for Business) können Sie festlegen, ob der Zugriff auf Exchange Online nur über die unterstützten Browser gewährt werden soll: Safari (iOS) und Chrome (Android). Der Zugriff über andere Browser ist blockiert. Die gleichen Plattformbeschränkungen, die Sie für „Application access for OneDrive“ (Anwendungszugriff für OneDrive) ausgewählt haben, gelten auch hier.

    Benutzer von **Android**-Geräten müssen die Option **Browserzugriff aktivieren** wie folgt auf dem registrierten Gerät aktivieren:
    1.  Starten Sie die **Unternehmensportal-App**.
    2.  Rufen Sie die Seite **Einstellungen** über die Schaltfläche mit den drei Punkten (…) oder über die physische Menütaste auf.
    3.  Drücken Sie die Schaltfläche **Browserzugriff aktivieren** .
    4.  Melden Sie sich im Chrome-Browser von Office 365 ab, und starten Sie Chrome erneut.

    Azure AD führt ein TLS-Zertifikat auf dem Gerät aus, um auf **iOS und Android**-Plattformen das Gerät zu identifizieren, das für den Zugriff auf den Dienst verwendet wird. Das Gerät zeigt das Zertifikat mit einer Aufforderung für den Endbenutzer an, das Zertifikat auszuwählen, wie in den folgenden Screenshots dargestellt: Der Endbenutzer muss dieses Zertifikat auswählen, um den Browser weiterhin verwenden zu können.

     **iOS**

     ![Screenshot der Zertifikataufforderung auf einem iPad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Android**

      ![Screenshot der Zertifikataufforderung auf einem Android-Gerät](media/mdm-browser-ca-android-cert-prompt.png)

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Links** auf **Richtlinie für bedingten Zugriff in der Intune-Konsole konfigurieren**. Sie müssen möglicherweise den Benutzernamen und das Kennwort des Kontos angeben, das zum Verbinden von Configuration Manager mit Intune verwendet wird.  

     Die Intune-Verwaltungskonsole wird geöffnet.  

5.  Klicken Sie in der [Microsoft Intune-Verwaltungskonsole](https://manage.microsoft.com)auf **Richtlinie** > **Bedingter Zugriff** > **SharePoint Online Richtlinie**.  

6.  Wählen Sie **Verhindern, dass Apps auf SharePoint Online zugreifen, wenn das Gerät nicht konform ist**.  

7.  Klicken Sie unter **Zielgruppen** auf **Ändern**, um die Azure AD-Sicherheitsgruppen auszuwählen, für die die Richtlinie gelten soll.  

8.  Klicken Sie unter **Ausgenommene Gruppen** optional auf **Ändern**, um die Azure AD-Sicherheitsgruppen auszuwählen, die von dieser Richtlinie ausgenommen werden.  

9. Klicken Sie abschließend auf **Speichern**.  

 Die Richtlinie für bedingten Zugriff wird sofort wirksam und muss nicht explizit bereitgestellt werden.  

 Unter [Verwalten des Zugriffs auf SharePoint Online mit Microsoft Intune](/intune-classic/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune) finden Sie Informationen zum Überwachen der Richtlinie in der Intune-Konsole.  

### <a name="see-also"></a>Weitere Informationen:  

 [Verwalten des Zugriffs auf Dienste in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
