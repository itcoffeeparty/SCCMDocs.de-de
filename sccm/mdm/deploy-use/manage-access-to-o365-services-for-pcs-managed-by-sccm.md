---
title: "Verwalten des Zugriffs auf Office 365-Dienste für verwaltete PCs"
titleSuffix: Configuration Manager
description: "Erfahren Sie, wie Sie den bedingten Zugriff für PCs konfigurieren, die von System Center Configuration Manager verwaltet werden."
ms.custom: na
ms.date: 12/19/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
caps.latest.revision: "15"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: bf38358d12c2617d924fe59bf7bf7457dfa95143
ms.sourcegitcommit: 6c2aa79924c0e7fc64ef5e9003498fc00c349db9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Verwalten des Zugriffs auf Office 365-Dienste für PCs, die von System Center Configuration Manager verwaltet werden

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1602 von Configuration Manager können Sie einen bedingten Zugriff für PCs konfigurieren, die von System Center Configuration Manager verwaltet werden.  

> [!Tip]  
> Diese Funktion wurde erstmals in Version 1602 als [Vorabfunktion](/sccm/core/servers/manage/pre-release-features) eingeführt. Ab Version 1702 ist diese Funktion keine Vorabfunktion mehr.

Informationen zum Konfigurieren des bedingten Zugriffs für Geräte, die über Microsoft Intune registriert und verwaltet werden, finden Sie unter [Verwalten des Zugriffs auf Dienste in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md). Dieser Artikel behandelt auch Geräte, die in eine Domäne eingebunden sind und nicht als konform ausgewertet werden.

## <a name="supported-services"></a>Unterstützte Dienste  

-   Exchange Online
-   SharePoint Online

## <a name="supported-pcs"></a>Unterstützte PCs  

-   Windows 7
-   Windows 8.1
-   Windows 10

## <a name="supported-windows-servers"></a>Unterstützte Windows Server-Versionen

-   2008 R2
-   2012
-   2012 R2
-   2016

    > [!IMPORTANT]
    > Bei Windows Server-Versionen, bei denen mehrere Benutzer gleichzeitig angemeldet sein können, müssen für alle angemeldeten Benutzer die gleichen Richtlinien für den bedingten Zugriff bereitgestellt werden.

## <a name="configure-conditional-access"></a>Konfigurieren des bedingten Zugriffs  
 Bevor Sie den bedingten Zugriff einrichten können, müssen Sie zunächst eine Konformitätsrichtlinie erstellen und eine Richtlinie für bedingten Zugriff konfigurieren. Wenn Sie Richtlinien für bedingten Zugriff für PCs konfigurieren, können Sie verlangen, dass die PCs der Konformitätsrichtlinie entsprechen müssen, damit sie auf Exchange Online- und SharePoint Online-Dienste zugreifen können.  

### <a name="prerequisites"></a>Erforderliche Komponenten  

-   AD FS-Synchronisierung (Active Directory Federation Services, Active Directory-Verbunddienste) sowie ein Office 365-Abonnement Das Office 365-Abonnement wird zum Einrichten von Exchange Online und SharePoint Online benötigt.  

-   Microsoft Intune-Abonnement. Das Microsoft Intune-Abonnement muss in der Configuration Manager-Konsole konfiguriert werden. Das Intune-Abonnement wird zur Weiterleitung des Konformitätszustands des Geräts an Azure Active Directory und zur Benutzerlizenzierung verwendet.  

 Die PCs müssen folgende Anforderungen erfüllen:  

-   Die[Voraussetzungen](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) für die automatische Geräteregistrierung bei Azure Active Directory müssen erfüllt sein.  

     Sie können PCs bei Azure Active Directory (Azure AD) über die Kompatibilitätsrichtlinie registrieren.  

    -   PCs unter Windows 8.1 und Windows 10 können Sie mithilfe einer Active Directory-Gruppenrichtlinie für die automatische Registrierung bei Azure AD konfigurieren.  

    -   Auf PCs unter Windows 7 müssen Sie das Geräteregistrierungs-Softwarepaket auf Ihren Windows 7-PC über System Center Configuration Manager bereitstellen. Weitere Informationen finden Sie in dem Artikel [Automatische Geräteregistrierung bei Azure Active Directory für in Domänen eingebundene Windows-Geräte](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).  

-   Auf dem PCs muss Office 2013 oder Office 2016 mit [aktivierter](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)moderner Authentifizierung verwendet werden.  

 Die folgenden Schritte gelten für Exchange Online und SharePoint Online  

### <a name="step-1-configure-compliance-policy"></a>Schritt 1: Konfigurieren von Kompatibilitätsrichtlinien  
 Erstellen Sie in der Configuration Manager-Konsole eine Kompatibilitätsrichtlinie mit den folgenden Regeln:  

-   **Registrierung in Azure Active Directory erforderlich:** Diese Regel prüft, ob das Gerät des Benutzers in Azure AD eingebunden ist. Falls nicht, wird es automatisch in Azure AD registriert. Die automatische Registrierung wird nur unter Windows 8.1 unterstützt. Stellen Sie für Windows 7-PCs eine MSI-Datei bereit, um die automatische Registrierung durchzuführen. Weitere Informationen finden Sie unter [Automatische Geräteregistrierung bei Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  

-   **Alle mit einem Stichtag älter als X Tage installierten benötigten Updates:** Diese Regel überprüft, ob das Gerät des Benutzers gemäß dem Stichtag und der Toleranzperiode, die Sie festgelegt haben, über alle erforderlichen Updates verfügt (entsprechend der Angabe in der Regel „Erforderliche automatische Updates“) und installiert automatisch alle ausstehenden Updates.  

-   **BitLocker-Laufwerkverschlüsselung erfordern:** Diese Regel prüft, ob das primäre Laufwerk (z.B. C:\\) auf dem Gerät mit BitLocker verschlüsselt ist. Wenn die Bitlocker-Verschlüsselung auf dem primären Gerät nicht aktiviert ist, wird der Zugriff auf E-Mail- und SharePoint-Dienste blockiert.  

-   **Antischadsoftware erfordern:** Diese Regel prüft, um herauszufinden, ob System Center Endpoint Protection oder Windows Defender aktiviert ist und ausgeführt wird. Falls nicht, wird der Zugriff auf E-Mail- und SharePoint-Dienste blockiert.  

-   **Vom Integritätsnachweisdienst als Fehlerfrei gemeldet:** Diese Bedingung enthält vier Unterregeln zum Vergleichen der Gerätekonformität mit dem Integritätsnachweisdienst. Weitere Informationen finden Sie unter [Integritätsnachweis](/sccm/core/servers/manage/health-attestation). 

    - **BitLocker muss auf dem Gerät aktiviert sein**
    - **Sicherer Start muss auf dem Gerät aktiviert sein** 
    - **Codeintegrität muss auf dem Gerät aktiviert sein**
    - **Antischadsoftware-Frühstart muss auf dem Gerät aktiviert sein**

>[!Tip]
> Mit Version 1710 wurden die bedingten Zugangsberechtigungskriterien für die Geräteintegritätsprüfung als vorab veröffentlichtes Feature eingeführt. Informationen zum Aktivieren dieses Features finden Sie unter [Funktionen des Vorabreleases](/sccm/core/servers/manage/pre-release-features). 

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Schritt 2: Bewerten der Auswirkungen des bedingten Zugriffs  
 Führen Sie den „Bericht zur Kompatibilität mit bedingtem Zugriff“ aus. Sie finden ihn im Abschnitt „Überwachung“ unter „Berichte“ > „Konformitäts- und Einstellungsverwaltung“. Dieser Bericht zeigt den Konformitätsstatus für alle Geräte an.  Geräten, die als nicht konform gemeldet werden, wird der Zugriff auf Exchange Online und SharePoint Online blockiert.  

 ![CA&#95;compliance&#95;report](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Konfigurieren von Active Directory-Sicherheitsgruppen  
 Je nach Art der Richtlinie weisen Sie Benutzergruppen spezielle Richtlinien für bedingten Zugriff zu. Die Gruppen beinhalten die Benutzer, für die die Richtlinie gelten soll oder die von ihr ausgeschlossen sind. Wenn eine Richtlinie für einen Benutzer gilt, muss jedes von ihm verwendete Gerät die Richtlinie erfüllen, um auf den Dienst zugreifen zu können.  

 Active Directory-Sicherheitsbenutzergruppen. Diese Benutzergruppen müssen mit Azure Active Directory synchronisiert werden. Sie können diese Gruppen auch im Office 365 Admin Center oder im Intune-Kontenportal konfigurieren.  

 Sie können für jede Richtlinie zwei Arten von Gruppen angeben :  

-   **Zielgruppen:** Benutzergruppen, auf die die Richtlinie angewendet wird Die gleiche Gruppe sollte sowohl für Konformität und die Richtlinie für bedingten Zugriff verwendet werden.  

-   **Ausgenommene Gruppen:** Benutzergruppen, die von der Richtlinie ausgenommen sind (optional)  
    Benutzer die in beiden Gruppen sind, werden von der Richtlinie ausgenommen.  

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

Benutzer können die Konformitätsinformationen im Softwarecenter ansehen. Führen Sie eine neue Richtlinienauswertung aus, nachdem Sie die Konformitätsprobleme behoben haben, wenn Sie aufgrund von Nichtkonformität blockiert werden.  


## <a name="see-also"></a>Weitere Informationen:

- [Schützen der Daten und Standortinfrastruktur mit System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)
- [Flussdiagramm der Problembehandlung beim bedingten Zugriff für Configuration Manager](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0)
