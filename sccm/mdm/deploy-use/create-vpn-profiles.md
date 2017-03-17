---
title: VPN-Profile in System Center Configuration Manager | Microsoft-Dokumentation
description: "VPN-Profile für mobile Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 32190ec39af2cf1568b3d57c2c2f25d9ff2f9e20
ms.lasthandoff: 03/06/2017

---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>VPN-Profile für mobile Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie VPN-Profile in System Center Configuration Manager, um Benutzern mobiler Geräte in Ihrer Organisation VPN-Einstellungen bereitzustellen. Durch Bereitstellen dieser Einstellungen erleichtern Sie dem Endbenutzer das Verbinden mit Ressourcen im Unternehmensnetzwerk.  

 Sie möchten z. B. allen Geräten, auf denen das iOS-Betriebssystem ausgeführt wird, die Einstellungen zur Verfügung stellen, die zum Verbinden mit einer Dateifreigabe im Unternehmensnetzwerk erforderlich sind. Sie können ein VPN-Profil mit den zum Verbinden mit dem Unternehmensnetzwerk erforderlichen Einstellungen erstellen und dieses Profil dann für alle Benutzer mit Geräten unter iOS in der Hierarchie bereitstellen. Benutzer von iOS-Geräten sehen die VPN-Verbindung in der Liste der verfügbaren Netzwerke und können sich mühelos mit diesem Netzwerk verbinden.  

 Wenn Sie ein VPN-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen aufnehmen, darunter auch Zertifikate für die Serverüberprüfung und Clientauthentifizierung, die mit System Center Configuration Manager-Zertifikatprofilen bereitgestellt wurden. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md).  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>VPN-Profile bei der Verwendung von Configuration Manager mit Intune 
 
 Um Profile für Android-, iOS-, Windows Phone- und Windows 8.1-Geräte bereitzustellen, müssen diese Geräte bei Microsoft Intune registriert werden. Geräte auf anderen Plattformen können ebenfalls bei Intune registriert werden. Informationen zum Registrieren finden Sie unter [Verwalten von Geräten für die Verwaltung in Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). Diese Tabelle zeigt, welcher Verbindungstyp für jede Geräteplattform unterstützt wird:  

 |Verbindungstyp|iOS und Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop und Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|Ja|Ja|Nein|Nein|Nein|Nein|Ja (OMA-URI)|  
 |Pulse Secure|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
 |F5 Edge Client|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
 |Dell SonicWALL Mobile Connect|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
 |Prüfpunkt für mobiles VPN|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
 |Microsoft SSL (SSTP)|Nein|Nein|Ja|Ja|Ja|Nein|Nein|  
 |Microsoft Automatic|Nein|Nein|Ja|Ja|Ja|Nein|Ja (OMA-URI)|  
 |IKEv2|Ja (Benutzerdefinierte Richtlinie)|Nein|Ja|Ja|Ja|Ja|Ja (OMA-URI)|  
 |PPTP|Ja|Nein|Ja|Ja|Ja|Nein|Ja (OMA-URI)|  
 |L2TP|Ja|Nein|Ja|Ja|Ja|Nein|Ja (OMA-URI)|  

## <a name="create-vpn-profiles"></a>Erstellen von VPN-Profilen
Allgemeine Informationen zum Erstellen von VPN-Profilen finden Sie unter [Erstellen von VPN-Profilen in System Center Configuration Manager](../../protect/deploy-use/create-vpn-profiles.md).

###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Bei der Verwendung von Configuration Manager mit Intune verfügbare Windows 10-VPN-Features  


> [!NOTE]  
> Der Name eines VPN-Profils mit Windows 10-VPN-Features darf keine Unicode oder Sonderzeichen enthalten.


|Option|Weitere Informationen|Verbindungstyp|  
    |------------|----------------------|---------------------|  
    |**VPN beim Verbinden mit Unternehmens-WLAN-Netzwerk umgehen**|Die VPN-Verbindung wird nicht verwendet, wenn das Gerät mit dem Unternehmens-WLAN verbunden ist. Geben Sie den Namen des vertrauenswürdigen Netzwerks ein, das zum Ermitteln verwendet wird, ob das Gerät mit dem Unternehmensnetzwerk verbunden ist.|Alle|  
    |**Regeln für den Netzwerkdatenverkehr**|Legen Sie die Protokolle, die lokalen und Remoteports sowie die Adressbereiche fest, die für die VPN-Verbindung aktiviert werden sollen.<br /><br /> **Hinweis:** Wenn Sie keine Regel für den Netzwerkdatenverkehr erstellen, werden alle Protokolle, Ports und Adressbereiche aktiviert. Nachdem Sie eine Regel erstellt haben, werden nur die in dieser oder weiteren Regeln festgelegten Protokolle, Ports und Adressbereiche von der VPN-Verbindung verwendet.|Alle|  
    |**Routen**|Die Routen, welche die VPN-Verbindung verwenden. Beachten Sie, dass die Erstellung von mehr als 60 Routen Richtlinienfehler herbeiführen kann. |Alle|  
    |**DNS-Server**|Die DNS-Server, die von der VPN-Verbindung verwendet werden, nachdem die Verbindung hergestellt wurde.|Alle|  
    |**Apps, die automatisch eine Verbindung mit dem VPN herstellen**|Sie können Apps hinzufügen oder App-Listen importieren, die automatisch die VPN-Verbindung verwenden. Der App-Typ bestimmt den App-Bezeichner. Stellen Sie für eine Desktop-App den Dateipfad der App bereit. Stellen Sie für eine universelle App den Paketfamiliennamen (package family name; PFN) bereit. Informationen dazu, wie Sie den PFN einer App herausfinden, finden Sie unter [Find a package family name for per-app VPN (Suchen eines Paktefamiliennamens für Pro-App-VPN)](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |Alle|

> [!IMPORTANT]
> Es wird empfohlen, alle Listen der zugeordneten Apps zu sichern, die Sie für die Konfiguration des Pro-App-VPN kompilieren. Wenn ein nicht autorisierter Benutzer die Liste ändert und Sie die Liste in die Pro-App-VPN-Liste importieren, gewähren Sie möglicherweise VPN-Zugriff auf Apps, auf die kein Zugriff bestehen sollte. Eine Möglichkeit, die App-Listen zu sichern, besteht in der Verwendung einer Zugriffssteuerungsliste (access control list; ACL).


1.  Geben Sie auf der Seite **Authentifizierungsmethode** des Assistenten Folgendes an:  

    -   **Authentifizierungsmethode:** Wählen Sie die Authentifizierungsmethode für die VPN-Verbindung aus. Verfügbare Methoden hängen vom Verbindungstyp ab, wie in dieser Tabelle gezeigt.  

        |Authentifizierungsmethode|Unterstützte Verbindungstypen|  
        |---------------------------|--------------------------------|  
        |**Zertifikate**<br /><br /> **Hinweis:** Wenn das Clientzertifikat für die Authentifizierung bei einem RADIUS-Server, z.B. ein Netzwerkrichtlinienserver, verwendet wird, muss der alternative Antragstellername im Zertifikat auf den Benutzerprinzipalnamen festgelegt werden.|- <br />                            Cisco AnyConnect<br /><br /> – Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN|  
        |**Benutzername und Kennwort**|- <br />                            Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN|  
        |**Microsoft EAP-TTLS**|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – PPTP<br /><br /> – IKEv2<br /><br /> – L2TP|  
        |**Microsoft-gesichertes EAP (PEAP)**|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – PPTP<br /><br /> – L2TP|  
        |**Microsoft-gesichertes Kennwort (EAP-MSCHAP v2)**|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – PPTP<br /><br /> – L2TP|  
        |**Smartcard- oder anderes Zertifikat**|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – PPTP<br /><br /> – L2TP|  
        |**MSCHAP v2**|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – PPTP<br /><br /> – L2TP|  
        |**RSA SecurID** (nur iOS)|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – PPTP<br /><br /> – L2TP|  
        |**Computerzertifikate verwenden**|IKEv2|  

         Je nach ausgewählten Optionen werden Sie möglicherweise gebeten, weitere Informationen wie beispielsweise die folgenden anzugeben:  

        -   **Remember the user credentials at each logon** (Benutzeranmeldeinformationen bei jeder Anmeldung speichern): Benutzeranmeldeinformationen werden gespeichert, sodass der Benutzer sie nicht bei jeder Verbindung eingeben muss.  

        -   **Select a client certificate for client authentication** (Clientzertifikat für Clientauthentifizierung auswählen): Wählen Sie das [SCEP-Clientzertifikat aus](introduction-to-certificate-profiles.md), das Sie zuvor erstellt haben, und das zur Authentifizierung der VPN-Verbindung verwendet wird.   

            > [!NOTE]  
            >  Bei iOS-Geräten wird das von Ihnen ausgewählte SCEP-Profil in das VPN-Profil eingebettet. Bei anderen Plattformen wird eine Anwendbarkeitsregel hinzugefügt, um sicherzustellen, dass das VPN-Profil nicht installiert wird, wenn das Zertifikat nicht vorhanden oder nicht kompatibel ist.  
            >   
            >  Wenn das von Ihnen angegebene SCEP-Zertifikat nicht kompatibel ist oder nicht bereitgestellt wurde, wird das VPN-Profil nicht auf dem Gerät installiert.
            >  
            >  Geräte unter iOS unterstützen nur RSA SecurID und MSCHAP v2 als Authentifizierungsmethode, wenn der Verbindungstyp PPTP lautet. Um die Ausgabe von Fehlern zu vermeiden, stellen Sie auf Geräten unter IOS ein separates PPTP-VPN-Profil bereit.  

        - **Bedingter Zugriff**
            - Wählen Sie **Enable conditional access for this VPN connection** (Bedingten Zugriff für diese VPN-Verbindung aktivieren) aus, um sicherzustellen, dass Geräte, die eine Verbindung mit dem VPN herstellen, vor der Verbindung auf Konformität mit bedingtem Zugriff getestet werden. Weitere Informationen zu Konformitätsrichtlinien finden Sie unter [Device compliance policies in System Center Configuration Manager (Verwalten von Konformitätsrichtlinien für Geräte in System Center Configuration Manager)](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md)
            - Wählen Sie **Enable single sign-on (SSO) with alternate certificate** (Einmaliges Anmelden (SSO) mit alternativem Zertifikat aktivieren) aus, um ein anderes Zertifikat als das Zertifikat für die VPN-Authentifizierung für die Gerätekonformität auszuwählen. Wenn Sie diese Option wählen, geben Sie **EKU** (durch Komma getrennte Liste) und **Issuer Hash** (Ausstellerhash) an, um das korrekte Zertifikat auszuwählen, dass der VPN-Client suchen soll.

         - **Windows Information Protection**: Geben Sie die vom Unternehmen verwaltete Unternehmensidentität an. Diese ist normalerweise die primäre Domäne Ihres Unternehmens, z.B. *contoso.com*. Sie können mehrere Domänen angeben, die Ihrer Organisation gehören, indem Sie sie durch das Zeichen „|“ trennen. Beispiel: *contoso.com|newcontoso.com*.   
              Weitere Informationen zu Windows Information Protection finden Sie unter [Create a Windows Information Protection (WIP) policy using Microsoft Intune (Erstellen einer Windows Information Protection-Richtlinie (WIP) mit Microsoft Intune)](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Konfigurieren des bedingten Zugriffs für VPN](media/vpn-conditional-access.png)


> [!NOTE]  
> Bei manchen Authentifizierungsmethoden können Sie auf **Konfigurieren** klicken, um das Dialogfeld für Windows-Eigenschaften zu öffnen (falls die Windows-Version, unter der die Configuration Manager-Konsole ausgeführt wird, diese Authentifizierungsmethode unterstützt). Dort können Sie die Eigenschaften der Authentifizierungsmethode konfigurieren.  


1.  Aktivieren Sie auf der Seite **Proxyeinstellungen** des **Assistenten zum Erstellen von VPN-Profilen**das Kontrollkästchen **Proxyeinstellungen für dieses VPN-Profil konfigurieren** , wenn für Ihre VPN-Verbindung ein Proxyserver verwendet wird. Geben Sie dann die Proxyserverinformationen an. Weitere Informationen finden Sie in der Windows Server-Dokumentation.  

    > [!NOTE]  
    >  Auf Windows 8.1-Computern zeigt das VPN-Profil die Proxyinformationen erst an, wenn Sie mit dem betreffenden Computer eine Verbindung zu dem VPN herstellen.  


2. Konfigurieren weiterer DNS-Einstellungen (falls erforderlich)  
 Auf der Seite **Configure Automatic VPN connection (Automatische VPN-Verbindung konfigurieren)** können Sie Folgendes konfigurieren:  

    -   **Enable VPN on-demand** (VPN bedarfsgesteuert aktivieren): Verwenden Sie diese Option, wenn Sie weitere DNS-Einstellungen für Windows Phone 8.1-Geräte konfigurieren möchten. Diese Einstellung gilt nur für Windows Phone 8.1-Geräte und sollte nur auf VPN-Profilen aktiviert werden, die für Windows Phone 8.1-Geräte bereitgestellt werden.

    -   DNS-Suffixliste (nur Windows Phone 8.1-Geräte): Konfiguriert Domänen, die eine VPN-Verbindung herstellen. Fügen Sie für jede Domäne, die Sie angeben, das DNS-Suffix, die DNS-Serveradresse und eine der folgenden bedarfsgesteuerten Aktionen hinzu:  

        -   **Nie herstellen**: Es wird niemals eine VPN-Verbindung geöffnet.  

        -   **Bei Bedarf herstellen**: Es wird nur dann eine VPN-Verbindung geöffnet, wenn das Gerät eine Verbindung zu Ressourcen herstellen muss.  

        -   **Immer herstellen**: Die VPN-Verbindung wird immer geöffnet.  

    -   **Zusammenführen**: Kopiert jedes von Ihnen konfigurierte DNS-Suffixe in die **Liste vertrauenswürdiger Netzwerke**.  

    -   **Trusted network list** (Liste vertrauenswürdiger Netzwerke) (nur Windows Phone 8.1-Geräte): Geben Sie in jeder Zeile ein DNS-Suffix an. Wenn sich das Gerät in einem vertrauenswürdigen Netzwerk befindet, wird die VPN-Verbindung nicht geöffnet.  

    -   **Suffix search list** (Suffixsuchliste) (nur Windows Phone 8.1-Geräte): Geben Sie in jeder Zeile ein DNS-Suffix an. Jedes DNS-Suffix wird beim Verbinden mit einer Website unter Verwendung eines Kurznamens gesucht.  

     Beispiel: Sie geben die DNS-Suffixe **domain1.contoso.com** und **domain2.contoso.com** an und besuchen dann die URL **http://mywebsite**. Die folgenden Adressen werden gesucht.  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  Nur für Windows Phone 8.1-Geräte  
    >   
    >  Wenn die Option **Gesamten Netzwerkdatenverkehr über die VPN-Verbindung senden** ausgewählt ist und die VPN-Verbindung vollständiges Tunneln verwendet, wird beim ersten auf dem Gerät bereitgestellten Profil die VPN-Verbindung automatisch geöffnet. Wenn ein anderes Profil automatisch eine Verbindung öffnen soll, müssen Sie es auf dem Gerät als Standardprofil festlegen.  
    >   
    >  Wenn die Option **Gesamten Netzwerkdatenverkehr über die VPN-Verbindung senden** nicht ausgewählt ist und die VPN-Verbindung getrenntes Tunneln verwendet, kann eine VPN-Verbindung automatisch geöffnet werden, wenn Sie Routen oder ein verbindungsspezifisches DNS-Suffix konfigurieren.  


1. Wählen Sie auf der Seite **Unterstützte Plattformen** des **Assistenten zum Erstellen von VPN-Profilen**die Betriebssysteme aus, unter denen das VPN-Profil installiert wird, oder klicken Sie auf **Alle auswählen** , um das VPN-Profil unter allen verfügbaren Betriebssystemen zu installieren.  

2. Schließen Sie den Assistenten ab. Das neue VPN-Profil wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **VPN-Profile** angezeigt.  


**Bereitstellen:** Weitere Informationen zum Bereitstellen von VPN-Profilen finden Sie unter [Bereitstellen von WLAN-, VPN-, E-Mail- und Zertifikatprofilen](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

### <a name="next-steps"></a>Nächste Schritte  
 Die folgenden Themen helfen Ihnen beim Planen, Konfigurieren, Betreiben und Warten von VPN-Profilen in Configuration Manager.  

-   [Prerequisites for VPN profiles in System Center Configuration Manager (Voraussetzungen für VPN-Profile in System Center Configuration Manager)](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Security and privacy for VPN profiles in System Center Configuration Manager (Sicherheit und Datenschutz für VPN-Profile in System Center Configuration Manager)](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)

