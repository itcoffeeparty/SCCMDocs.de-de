---
title: "Verwalten des Zugriffs auf Office 365-Dienste für verwaltete PCs | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Sie den bedingten Zugriff für PCs konfigurieren, die von System Center Configuration Manager verwaltet werden."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccdb424a-b603-4ccc-af36-558924248022
caps.latest.revision: 15
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: da5fcd65d7af8d73aa23f4a7d96cd8fc6e48f9dc


---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Verwalten des Zugriffs auf Office 365-Dienste für PCs, die von System Center Configuration Manager verwaltet werden

*Gilt für: System Center Configuration Manager (Current Branch)*



 Ab Version 1602 von Configuration Manager können Sie einen bedingten Zugriff für PCs konfigurieren, die von System Center Configuration Manager verwaltet werden.  

> [!IMPORTANT]  
>  Dieses Vorabfeature ist in Update 1602, Update 1606 und Update 1610 verfügbar. Vorab veröffentlichte Features werden in das Produkt aufgenommen, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen. Sie sollten nicht als für den Produktivbetrieb geeignet betrachtet werden. Weitere Informationen finden Sie unter [Use pre-release features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease) (Verwenden von Vorabfeatures aus Updates).
> - Nach der Installation von Update 1602 wird der Featuretyp als endgültige Version angezeigt, obwohl es sich um eine Vorabversion handelt.
> - Wenn Sie anschließend von 1602 auf 1606 aktualisieren, wird der Featuretyp als endgültige Version angezeigt, obwohl es sich weiterhin um eine Vorabversion handelt.
> - Wenn Sie von Version 1511 direkt auf 1606 aktualisieren, wird der Featuretyp als Vorabversion angezeigt.

 Informationen zum Konfigurieren des bedingten Zugriffs für bei Intune registrierte und mit Intune verwaltete Geräte oder zum Konfigurieren von PCs, die in die Domäne eingebunden sind und nicht auf Kompatibilität überprüft werden, finden Sie unter [Verwalten des Zugriffs auf Dienste in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md).  


## <a name="supported-services"></a>Unterstützte Dienste  

-   Exchange Online  

-   SharePoint Online  

## <a name="supported-pcs"></a>Unterstützte PCs  

-   Windows 7  

-   Windows 8.1  

-   Windows 10 wird noch nicht vollständig unterstützt.  Wenn Sie versuchen, den bedingten Zugriff für Windows 10-PCs festzulegen, können Probleme auftreten.  Unter [Bekannte Probleme](#bkmk_KnownIssues) finden Sie weitere Details.  

## <a name="configure-conditional-access"></a>Konfigurieren des bedingten Zugriffs  
 Bevor Sie den bedingten Zugriff einrichten können, müssen Sie zunächst eine Kompatibilitätsrichtlinie erstellen und eine Richtlinie für bedingten Zugriff konfigurieren. Wenn Sie Richtlinien für bedingten Zugriff für PCs konfigurieren, können Sie verlangen, dass die PCs der Kompatibilitätsrichtlinie entsprechen müssen, damit sie auf Exchange Online- und SharePoint Online-Dienste zugreifen können.  

### <a name="prerequisites"></a>Voraussetzungen  

-   AD FS-Synchronisierung (Active Directory Federation Services, Active Directory-Verbunddienste) sowie ein Office 365-Abonnement Das Office 365-Abonnement wird zum Einrichten von Exchange Online und SharePoint Online benötigt.  

-   Microsoft Intune-Abonnement. Das Microsoft Intune-Abonnement muss in der Configuration Manager-Konsole konfiguriert werden. Dafür wird weiterhin eine hybride Bereitstellung benötigt.  

 Die PCs müssen folgende Anforderungen erfüllen:  

-   Die[Voraussetzungen](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) für die automatische Geräteregistrierung bei Azure Active Directory müssen erfüllt sein.  

     Sie können PCs bei Azure Active Directory (Azure AD) über die Kompatibilitätsrichtlinie registrieren.  

    -   PCs unter Windows 8.1 und Windows 10 können Sie mithilfe einer Active Directory-Gruppenrichtlinie für die automatische Registrierung bei Azure AD konfigurieren.  

    -   Auf PCs unter Windows 7 müssen Sie das Geräteregistrierungs-Softwarepaket auf Ihren Windows 7-PC über System Center Configuration Manager bereitstellen. Weitere Informationen finden Sie unter dem Thema [Automatische Geräteregistrierung bei Azure Active Directory für in Domänen eingebundene Windows-Geräte](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

-   Auf dem PCs muss Office 2013 oder Office 2016 mit [aktivierter](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)moderner Authentifizierung verwendet werden.  

 Die nachfolgend beschriebenen Schritte gelten für Exchange Online und SharePoint Online.  

### <a name="step-1-configure-compliance-policy"></a>Schritt 1: Konfigurieren von Kompatibilitätsrichtlinien  
 Erstellen Sie in der Configuration Manager-Konsole eine Kompatibilitätsrichtlinie mit den folgenden Regeln:  

-   Registrierung in Azure Active Directory erforderlich: Diese Regel prüft, ob das Gerät des Benutzers in Azure AD eingebunden ist. Falls nicht, wird es automatisch in Azure AD registriert. Die automatische Registrierung wird nur unter Windows 8.1 unterstützt. Stellen Sie für Windows 7-PCs eine MSI-Datei bereit, um die automatische Registrierung durchzuführen. Weitere Informationen finden Sie unter [Automatische Geräteregistrierung bei Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

-   **Alle mit einem Stichtag älter als X Tage installierten benötigten Updates:** Diese Regel überprüft, ob das Gerät des Benutzers gemäß dem Stichtag und der Toleranzperiode, die Sie festgelegt haben, über alle erforderlichen Updates verfügt (entsprechend der Angabe in der Regel „Erforderliche automatische Updates“) und installiert automatisch alle ausstehenden Updates.  

-   **BitLocker-Laufwerkverschlüsselung erfordern:** Dies ist eine Prüfung, ob das primäre Laufwerk (z.B. C:\\) auf dem Gerät mit BitLocker verschlüsselt ist. Wenn die Bitlocker-Verschlüsselung auf dem primären Gerät nicht aktiviert ist, wird der Zugriff auf E-Mail- und SharePoint-Dienste blockiert.  

-   **Antischadsoftware erfordern:** Dies ist eine Prüfung, um herauszufinden, ob die Antischadsoftware (nur System Center Endpoint Protection oder Windows Defender) aktiviert ist und ausgeführt wird. Falls nicht, wird der Zugriff auf E-Mail- und SharePoint-Dienste blockiert.  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Schritt 2: Bewerten der Auswirkungen des bedingten Zugriffs  
 Führen Sie den „Bericht zur Kompatibilität mit bedingtem Zugriff“ aus. Sie finden ihn im Abschnitt „Überwachung“ unter „Berichte“ > „Kompatibilitäts- und Einstellungsverwaltung“. Dort wird der Kompatibilitätsstatus für alle Geräte angezeigt.  Für Geräte, die als nicht kompatibel gemeldet werden, wird der Zugriff auf Exchange Online und SharePoint Online blockiert.  

 ![CA&#95;compliance&#95;report](../media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Konfigurieren von Active Directory-Sicherheitsgruppen  
 Je nach Art der Richtlinie weisen Sie Benutzergruppen spezielle Richtlinien für bedingten Zugriff zu. Die Gruppen beinhalten die Benutzer, für die die Richtlinie gelten soll oder die davon ausgeschlossen sind. Bei Benutzern, für die eine Richtlinie gelten soll, muss jedes von ihnen verwendete Gerät die Richtlinie erfüllen, damit sie auf den Dienst zugreifen können.  

 Active Directory-Sicherheitsbenutzergruppen. Diese Benutzergruppen müssen mit Azure Active Directory synchronisiert werden. Sie können diese Gruppen auch im Office 365 Admin Center oder im Intune-Kontenportal konfigurieren.  

 Sie können für jede Richtlinie zwei Arten von Gruppen angeben :  

-   **Zielgruppen:** Benutzergruppen, auf die die Richtlinie angewendet wird Die gleiche Gruppe sollte sowohl für Konformität und die Richtlinie für bedingten Zugriff verwendet werden.  

-   **Ausgenommene Gruppen:** Benutzergruppen, die von der Richtlinie ausgenommen sind (optional)  
    Benutzer, die in beiden Gruppen enthalten sind, werden von der Richtlinie ausgenommen.  

     Es werden nur die Gruppen ausgewertet, für die die Richtlinie für bedingten Zugriff gilt.  

### <a name="step-3--create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Schritt 3:  Erstellen einer Richtlinie für bedingten Zugriff für Exchange Online und SharePoint Online  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Zum Erstellen einer Richtlinie für Exchange Online wählen Sie die Option **Richtlinie für bedingten Zugriff für Exchange Online aktivieren**aus.  

     Zum Erstellen einer Richtlinie für SharePoint Online wählen Sie die Option **Richtlinie für bedingten Zugriff für SharePoint Online aktivieren**aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Links** auf **Richtlinie für bedingten Zugriff in der Intune-Konsole konfigurieren**. Sie müssen möglicherweise den Benutzernamen und das Kennwort des Kontos angeben, das zum Verbinden von Configuration Manager mit Intune verwendet wird.  

     Die Intune-Verwaltungskonsole wird geöffnet.  

4.  Für Exchange Online klicken Sie in der Microsoft Intune-Verwaltungskonsole auf **Richtlinie > Bedingter Zugriff > Exchange Online-Richtlinie**.  

     Für SharePoint Online klicken Sie in der Microsoft Intune-Verwaltungskonsole auf **Richtlinie> Bedingter Zugriff > SharePoint Online-Richtlinie**.  

5.  Legen Sie die Anforderung für Windows-PCs auf die Option**Geräte müssen kompatibel sein**fest.  

6.  Klicken Sie unter **Zielgruppen**auf **Ändern** , um die Active Directory-Sicherheitsgruppen auszuwählen, für die die Richtlinie gelten soll.  

    > [!NOTE]  
    >  Die gleiche Sicherheitsbenutzergruppe sollte für die Bereitstellung von Konformitätsrichtlinien und die Zielgruppe für bedingte Zugriffsrichtlinien verwendet werden.  

     Klicken Sie unter **Ausgenommene Gruppen**optional auf **Ändern** , um die Active Directory-Sicherheitsgruppen auszuwählen, die von dieser Richtlinie ausgenommen werden.  

7.  Klicken Sie auf **Speichern** , um die Richtlinie zu erstellen und zu speichern.  

 Endbenutzer, die aufgrund von Nichtkompatibilität blockiert werden, erhalten im System Center Configuration Manager-Softwarecenter Informationen zur Kompatibilität. Für sie wird eine erneute Richtlinienauswertung ausgelöst, nachdem Kompatibilitätsprobleme behoben wurden.  

##  <a name="a-namebkmkknownissuesa-known-issues"></a><a name="bkmk_KnownIssues"></a> Bekannte Probleme  
 Beim Verwenden dieses Features können folgende Probleme auftreten:  

-   In diesem Update auf Version 1602 wird die 5-Tage-Kompatibilität nicht erzwungen. Auch wenn die Kompatibilitätsprüfung auf dem Gerät eines Endbenutzers vor mehr als 5 Tagen stattgefunden hat, kann dieser Endbenutzer noch auf Office 365 und SharePoint Online zugreifen.  

-   Wenn ein Gerät nicht der Kompatibilitätsrichtlinie entspricht, wird der Grund nicht automatisch angezeigt. Der Endbenutzer muss das neue Softwarecenter aufsuchen, um den Grund für die nicht vorhandene Kompatibilität zu erfahren. Der Grund wird im Abschnitt für Gerätekompatibilität des Softwarecenters angezeigt.  

-   Bei Windows 10-Benutzern treten mitunter mehrere Zugriffsfehler auf, wenn sie versuchen, auf Office 365- und/oder SharePoint Online-Ressourcen zuzugreifen. Beachten Sie, dass der bedingte Zugriff für Windows 10 nicht vollständig unterstützt wird.  

### <a name="see-also"></a>Weitere Informationen:  
 [Schützen der Daten und Standortinfrastruktur mit System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)



<!--HONumber=Dec16_HO3-->


