---
title: 'Archiv: Neuheiten bei hybrider MDM | Microsoft-Dokumentation'
description: "Archiv der früheren Features der Verwaltung mobiler Geräte, die für Hybridbereitstellungen mit System Center Configuration Manager und Intune verfügbar sind"
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: 086b350005e9665e8b91c11e664563f9687aca27

---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Frühere Hybridfeatures mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieser Artikel bietet Details zu früheren Features für die Verwaltung mobiler Geräte (MDM), die für Hybridbereitstellungen mit System Center Configuration Manager und Intune verfügbar sind.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Kompatibilität mit Configuration Manager-Versionen  

 Jeder Abschnitt dieses Artikels listet Hybridfeatures in drei verschiedenen Kategorien auf. Verwenden Sie die folgenden Anleitungen, um die Kompatibilität der Features in jeder Kategorie mit verschiedenen Versionen von Configuration Manager zu bestimmen:  

|Featurekategorien|
|-|  
|**Neuheiten in Microsoft Intune** – Im Allgemeinen sollten alle in dieser Kategorie aufgelisteten Features mit allen Configuration Manager-Releases, einschließlich Configuration Manager-Releases von System Center 2012 R2, zusammenarbeiten, da für diese Features nur der Intune-Dienst erforderlich ist, aber keine zusätzliche Funktionalität in Configuration Manager.<br /><br /> **Neuheiten in Configuration Manager Technical Preview** – Alle in dieser Kategorie aufgelisteten Features arbeiten nur mit dem angegebenen Technical Preview-Release zusammen. Um diese Features zu testen, müssen Sie die in der Featurebeschreibung angegebene Technical Preview-Version installieren. Weitere Informationen finden Sie unter [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Neuheiten in Configuration Manager (Current Branch)** – Alle in dieser Kategorie aufgelisteten Features arbeiten nur mit der angegebenen Version von Configuration Manager (Current Branch) zusammen, z.B. Version 1511 oder 1602. Wenn Sie eine ältere Version von Configuration Manager für die Hybridbereitstellung verwenden, müssen Sie ein Upgrade auf die in der Featurebeschreibung angegebene Configuration Manager-Version (Current Branch) ausführen. Weitere Informationen finden Sie unter [Upgrade auf System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## <a name="new-hybrid-features-in-june-2016"></a>Neue Hybridfeatures im Juni 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune
Die folgenden im Juni 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **Intune-Dienstintegrität** Dienstintegritätsinformationen für Intune wurden an einen zentralen Speicherort mit anderen Microsoft-Diensten verschoben. Diese Informationen finden Sie jetzt im Office 365-Verwaltungsportal unter „Dienstintegrität“. Weitere Informationen finden Sie in diesem [Blogbeitrag](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Verbesserte Windows 10 Enterprise-Datenrichtlinienkonfiguration**

  Intune bietet nun verbesserte Benutzerfreundlichkeit beim Konfigurieren von Windows 10 Information Protection. Die Verbesserungen umfassen bessere Methoden zum Erstellen von App-Regeln, Angeben der Definition der Netzwerkgrenze und andere Windows Information Protection-Einstellungen. Weitere Informationen finden Sie unter [Create a Windows Information Protection (WIP) policy using Microsoft Intune (Erstellen einer Windows Information Protection-Richtlinie (WIP) mit Microsoft Intune)](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Cisco ISE-Netzwerk-Zugriffssteuerungsrichtlinie für Intune**

  Kunden, die Cisco Identity Service Engine (ISE) 2.1 und außerdem Microsoft Intune verwenden, können eine Netzwerkzugriffssteuerungsrichtlinie in ISE festlegen. Bei Verwendung dieser Richtlinie müssen Geräte, die über WLAN oder VPN eine Verbindung mit dem Netzwerk herstellen müssen, die folgenden Bedingungen erfüllen, bevor sie Zugriff erhalten:

  - Verwaltung durch Intune
  - Kompatibilität mit allen bereitgestellten Intune-Konformitätsrichtlinien

  Endbenutzer nicht konformer Geräte werden aufgefordert, sich zu registrieren und etwaige Kompatibilitätsprobleme zu beheben, um Zugriff zu erhalten.

- **Bedingter Zugriff für Browser**

  Sie können eine Richtlinie für bedingten Zugriff für Exchange Online und SharePoint Online festlegen, sodass nur von unterstützten Webbrowsern auf verwalteten und kompatiblen IOS- und Android-Geräten aus auf sie zugegriffen werden kann. Endbenutzer, die versuchen, sich bei Outlook Web Access- (OWA-) und SharePoint-Standorten mit IOS- und Android-Geräten anzumelden, werden aufgefordert, ihr Gerät bei Intune zu registrieren und alle Nichtkompatibilitätsprobleme zu beheben, bevor eine vollständige Anmeldung möglich ist. Weitere Informationen finden Sie unter

  * [Restrict email access to Exchange Online and new Exchange Online Dedicated with Intune (Beschränken des E-Mail-Zugriffs auf Exchange Online und das neue Exchange Online Dedicated mit Intune)](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restrict access to SharePoint Online with Microsoft Intune (Beschränken des Zugriffs auf SharePoint Online mit Microsoft Intune)](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online unterstützt den bedingten Zugriff**

  Sie können eine Richtlinie für bedingten Zugriff für Dynamics CRM Online festlegen, damit nur verwaltete und kompatible IOS- und Android-Geräte darauf zugreifen können. Endbenutzer, die sich bei der Dynamics CRM Mobile-App für iOS und Android anmelden möchten, werden aufgefordert, sich bei Intune zu registrieren und alle Nichtkompatibilitätsprobleme zu beheben, bevor die Anmeldung abgeschlossen werden kann. Weitere Informationen finden Sie unter [Restrict access to Dynamics CRM Online with Microsoft Intune (Beschränken des Zugriffs auf Dynamics CRM Online mit Microsoft Intune)](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune).

- **Updates der Android-Unternehmensportal-App**

  Intune verfügt nun über die folgenden neuen Richtlinien, die sich auf Android Unternehmensportal-Benutzer auswirken:   

  Richtlinie  |Auswirkungen für Benutzer  
  ---------|---------
  Geräte müssen die Installation von Apps aus unbekannten Quellen verhindern (Android 4.0+)     |  Endbenutzer mit Geräten mit Android 4.0 oder höher sehen die Meldung „Die Installation von unbekannten Quellen muss deaktiviert sein“. Benutzer müssen auf ihren Geräten zu **Einstellungen > Sicherheit** wechseln und **Unbekannte Quellen** deaktivieren. Über einen Link in der Konformitätsmeldung erhalten Benutzer weitere Informationen über die Meldung und den Grund dafür, dass sie die Einstellung deaktivieren müssen.
  Geräte müssen die Installation von Apps aus unbekannten Quellen verhindern (Android 4.0+)  |    Endbenutzer mit Android 4.0 oder höher erhalten die Meldung „Gerät auf Sicherheitsbedrohungen überprüfen“. Benutzer müssen auf ihren Geräten zu **Einstellungen > Google > Sicherheit** wechseln und **Gerät auf Sicherheitsbedrohungen überprüfen** aktivieren. Über einen Link in der Konformitätsmeldung erhalten Benutzer weitere Informationen über die Nachricht und den Grund dafür, dass sie die Einstellung aktivieren müssen.     
  Das USB-Debuggen muss deaktiviert sein (Android 4.2+)  | Endbenutzer mit Geräten mit Android 4.2 oder höher sehen die Meldung „Das USB-Debuggen muss deaktiviert sein“. Benutzer müssen auf ihren Geräten zu **Einstellungen > Entwickleroptionen** wechseln und **USB-Debuggen** deaktivieren. Über einen Link in der Konformitätsmeldung erhalten Benutzer weitere Informationen über die Meldung und den Grund dafür, dass sie die Einstellung deaktivieren müssen.
  Niedrigste zulässige Android-Sicherheitspatchebene (Android 6.0+)  | Endbenutzer mit Android Version 6.0 oder höher erhalten die Meldung „Dieses Gerät weist nicht die mindestens erforderliche Ebene für Android-Sicherheitspatches auf“. Benutzer müssen die erforderlichen Sicherheitspatches installieren. Über einen Link in der Konformitätsmeldung erhalten Benutzer Informationen darüber, wie sie den erforderlichen Sicherheitspatch installieren und prüfen können, welchen Sicherheitspatch sie derzeit installiert haben.

- **Updates der iOS-Unternehmensportal-App**

  * Wenn Endbenutzer Branchen-Apps installieren, profitieren sie nun von einer verbesserten, benutzerfreundlichen App-Installation. Wenn die App-Installation lange dauert, können die Benutzer ihr Gerät manuell synchronisieren, um die Fortsetzung des Synchronisierungsprozesses zu erzwingen. Die Endbenutzeranweisungen finden Sie unter „Sync your iOS device manually (Manuelles Synchronisieren des iOS-Geräts)“.
  * Die Microsoft Windows Intune-Unternehmensportal-App für iOS wurde aktualisiert und unterstützt nun iOS-Version 8.0 und höher. Dieses Update bedeutet, dass Endbenutzer die Unternehmensportal-App nur installieren und neue Geräte in Intune nur registrieren können, wenn auf dem Gerät iOS Version 8.0 oder höher ausgeführt wird. Benutzer, die bereits Geräte registriert haben, auf denen eine nicht unterstützte Version von iOS ausgeführt wird, können weiterhin die auf ihrem Gerät vorhandene Unternehmensportal-App verwenden.


### <a name="new-in-1606-technical-preview"></a>Neuheiten in 1606 Technical Preview
Die folgenden neuen Features vom Juni 2016 sind in Hybridbereitstellungen mit Intune und Configuration Manager Technical Preview 1606 verfügbar.

- **Automatisches Kategorisieren von Geräten in Sammlungen**

  Sie können Gerätekategorien erstellen, mit denen Geräte automatisch in Gerätesammlungen platziert werden, wenn Sie Configuration Manager mit Intune verwenden. Benutzer müssen eine Gerätekategorie auswählen, wenn sie ein Gerät in Intune registrieren. Sie können außerdem die Kategorie eines Geräts in der Configuration Manager-Konsole ändern. Weitere Informationen finden Sie unter [Automatisches Kategorisieren von Geräten in Sammlungen](/sccm/core/get-started/capabilities-in-technical-preview-1606.md#dmp_category) in [Funktionen in Technical Preview 1606 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606.md).

  > [!IMPORTANT]
  > Diese Funktion wird vom Microsoft Intune-Release vom Juni 2016 unterstützt. Stellen Sie sicher, dass Sie auf dieses Release aktualisiert haben, bevor Sie die Verfahren ausprobieren.

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)
Im Juni 2016 wurden keine neuen Hybridfeatures für Configuration Manager (Current Branch) eingeführt.

##  <a name="new-hybrid-features-in-may-2016"></a>Neue Hybridfeatures im Mai 2016  

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune  
 Die folgenden im Mai 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **MAM SDK: Unterstützung der PIN-Längenkonfiguration**

  Sie können jetzt die Länge der PIN für MAM-Apps ähnlich wie bei einer Geräte-ID angeben. Hierfür müssen Endbenutzer die neuen Einschränkungen einhalten, die Sie festlegen. Der PIN-Bildschirm wird für die längere Eingabe geringfügig geändert. Weitere Informationen finden Sie unter [MAM policy settings for Android (MAM-Richtlinieneinstellungen für Android)](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings) und [MAM policy settings for iOS (MAM-Richtlinieneinstellungen für iOS)](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype for Business für iOS und Android**

  Sie können jetzt [MAM ohne Registrierungsrichtlinien](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune) auf Skype for Business anwenden. Sobald sich die Benutzer angemeldet haben, werden die MAM-Richtlinien angewendet.  

- **Neue Apps für die Verwaltung mit MAM-Richtlinien verfügbar**

  Die Microsoft Word-, Excel- und PowerPoint-Apps für Android können mit MAM-Richtlinien auf Geräten verknüpft werden, die nicht bei Intune registriert sind. Eine vollständige Liste der unterstützten Apps finden Sie im Mobilanwendungskatalog von Microsoft Intune auf der Seite [Microsoft Intune-Anwendungspartner](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx).  

- **Android-Unternehmensportal-App: Popupbenachrichtigungen für Endbenutzer**

  Popupbenachrichtigungen von der Android-Unternehmensportal-App werden angezeigt, wenn Endbenutzer ihre Geräte über das Unternehmensportal registrieren oder entfernen.  

- **Unternehmensportal-Website: Geräte-ID-Banner bietet Endbenutzern weitere Informationen**

  Endbenutzer können das Gerät, das sie ausgewählt haben, bei Verwendung der Unternehmensportal-Website jetzt leichter finden. Wenn das falsche Gerät ausgewählt ist, können sie das korrekte Gerät auswählen, indem sie auf den Link **Hier tippen** im Banner der Startseite tippen.  


### <a name="new-in-1605-technical-preview"></a>Neuheiten in 1605 Technical Preview  
 Die folgenden neuen Features vom Mai 2016 sind in Hybridbereitstellungen mit Intune und Configuration Manager Technical Preview 1605 verfügbar. Diese Features setzen voraus, dass Sie die Configuration Manager-Konsole zum Konfigurieren und Verwalten verwenden.  

- **Per App ausgelöstes VPN für Windows 10-Geräte**

  Für Windows 10-Geräte, die mithilfe von Configuration Manager mit Intune verwaltet werden, können Sie eine Liste von Apps hinzufügen, die automatisch eine VPN-Verbindung öffnen, die Sie über die Configuration Manager-Verwaltungskonsole konfiguriert haben. Weitere Informationen finden Sie unter [Per App ausgelöstes VPN für Windows 10-Geräte](/sccm/core/get-started/capabilities-in-technical-preview-1605) in [Funktionen in Technical Preview 1605 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **Benutzerfreundlichere Remotegeräteaktionen**

  Die Ausführung von Remotegeräteaktionen über die Configuration Manager-Konsole wurde benutzerfreundlicher gestaltet und verbessert.

  Häufig verwendete Aktionen, wie z.B. **Abkoppeln/Zurücksetzen**, **Kennung zurücksetzen**, **Remotesperre** und **Aktivierungssperre umgehen**, befinden sich nun im Menü **Remotegeräteaktionen**, auf das Sie über den Arbeitsbereich **Bestand und Kompatibilität** zugreifen.

  Weitere Informationen finden Sie unter [Benutzerfreundlichere Remotegeräteaktionen](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) in [Funktionen in Technical Preview 1605 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Windows Store für Unternehmen-Apps**

  Im [Windows Store für Unternehmen](https://www.microsoft.com/en-us/business-store) können Sie Apps für Ihre Organisation finden und entweder einzeln oder per Volumenlizenz erwerben. Indem Sie den Store mit Configuration Manager verbinden, können Sie per Volumenlizenz erworbene Apps aus der Configuration Manager-Konsole verwalten. Weitere Informationen finden Sie unter [Windows Store für Unternehmen-Apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) in [Funktionen in Technical Preview 1605 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Allgemeine Verbesserungen für per Volumenlizenz erworbene Apps**

  Per Volumenlizenz erworbene Apps aus dem Windows Store für Unternehmen und dem iOS App-Store wurden in der gleichen Ansicht, **Lizenzinformationen für Store-Apps**, konsolidiert. Außerdem wurde die Art und Weise, wie Sie per Volumenlizenz erworbene Apps für iOS erstellen, verbessert. Weitere Informationen finden Sie unter [Allgemeine Verbesserungen für per Volumenlizenz erworbene Apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) in [Funktionen in Technical Preview 1605 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Vorabdeklarieren von firmeneigenen Geräten mit IMEI- oder iOS-Seriennummer**

  Sie können nun firmeneigene Geräte identifizieren, indem Sie deren IMEI-Nummern (International Station Mobile Equipment Identity) importieren. Sie können eine CSV-Datei (comma-separated values, durch Trennzeichen getrennte Datei) hochladen, die die IMEI-Nummern der Geräte enthält, oder Geräteinformationen manuell eingeben.  Sie können auch die Seriennummern für iOS-Geräte importieren.  Weitere Informationen finden Sie unter [Vorabdeklarieren von firmeneigenen Geräten mit IMEI- oder iOS-Seriennummer](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) in [Funktionen in Technical Preview 1605 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Windows Information Protection (WIP)**

  Sie können Konfigurationselemente erstellen, mit denen Sie Ihre Windows Information Protection-Richtlinien (WIP) bereitstellen können und z.B. Ihre geschützten Apps und Ihre WIP-Schutzebene wählen und Unternehmensdaten im Netzwerk suchen können. Weitere Informationen zu WIP finden Sie in den folgenden Themen:  

  -   [Schützen von Unternehmensdaten mit Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Create and deploy a Windows Information Protection (WIP) policy using System Center Configuration Manager (Erstellen und Bereitstellen einer Windows Information Protection-Richtlinie (WIP) mithilfe von System Center Configuration Manager)](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)  
 Im Mai 2016 wurden keine neuen Hybridfeatures für Configuration Manager (Current Branch) eingeführt.  

##  <a name="new-hybrid-features-in-april-2016"></a>Neue Hybridfeatures im April 2016  

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune  
 Die folgenden im April 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.  

- **MAM-Benutzerkompatibilität**

  Sie können nun den Status der Anwendungsverwaltungsrichtlinien für alle Benutzer in Ihrem Azure Active Directory-Mandanten (AAD) anzeigen.  Weitere Informationen finden Sie unter [Überwachen der Verwaltungsrichtlinien für mobile Apps mit Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) in der Intune-Bibliothek.  

- **MAM-Steuerelemente, um die Synchronisierung von Kontakten zu verhindern (Android)**

  Eine neue Einstellung ist verfügbar, mit der Sie verhindern können, dass eine Anwendung Kontakte mit dem nativen Adressbuch auf Android-Geräten synchronisiert. Diese neue Einstellung wird anfänglich von der Outlook-Anwendung auf Android-Geräten unterstützt. Weitere Informationen finden Sie unter [Erstellen und Bereitstellen von Richtlinien zur Verwaltung mobiler Apps mit Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) in der Intune-Bibliothek.  

- **Verbesserungen der Unternehmensportal-Website**

  Wenn Windows 10 Mobile- und Windows Phone 8.1-Benutzer Branchen-Apps installieren, sehen sie nun die folgenden neuen Status, die ihnen weitere Details über den Status ihrer Installation bieten:  

  -   **Warten auf Gerätesynchronisierung** – Der Benutzer hat auf „Installieren“ getippt, und das Gerät versucht nun, eine Synchronisierung mit der Intune-Infrastruktur auszuführen. Die Synchronisierung ist erforderlich, bevor die Installation abgeschlossen werden kann. Die Meldung „Warten auf Gerätesynchronisierung“ ist zudem ein Link, auf den der Benutzer tippen kann, um Anweisungen zur manuellen Synchronisierung mit Intune anzuzeigen, falls der Synchronisierungsprozess lange dauert oder angehalten wird.  

  -   **Wird heruntergeladen** – Die Downloadanforderung wird verarbeitet, und das Gerät lädt die App herunter und installiert sie.  

- **Verbesserungen der Android-Unternehmensportal-App**

  Benutzer, die ihre Geräte nicht in Intune registriert und nicht das richtige Zertifikat installiert haben, sind nicht in der Lage, sich bei der Android-Unternehmensportal-App anzumelden, und sehen die Meldung „Sie können sich nicht anmelden, da dem Gerät ein erforderliches Zertifikat fehlt“. Die Meldung enthält einen Link „Problembehebung“, auf den Benutzer tippen können, um Anweisungen für die Installation des Zertifikats anzuzeigen. Die Schritte, die die Endbenutzer zur Behebung dieses Problems durchführen, finden Sie unter [Your device is missing a required certificate (Dem Gerät fehlt ein erforderliches Zertifikat)](/intune/enduser/using-your-android-device-with-intune) in der Intune-Bibliothek.  

- **Verbesserungen der iOS-Unternehmensportal-App**

  Unterstützung wurde für die Aktion „Zum Aktualisieren ziehen“ hinzugefügt, die den Inhalt auf der Startseite aktualisieren soll. Dazu gehören aufgeführte Apps, aufgeführte Geräte und IT-Kontaktinformationen. Die Aktion „Zum Aktualisieren ziehen“ prüft Kompatibilitäts- oder Richtlinieninformationen nicht. Sie können diese Informationen prüfen, indem Sie die Kachel für das aktuelle Gerät auswählen und auf die Schaltfläche **Synchronisierung** tippen.  

- **Verbesserungen für die Windows 10 Mobile- und Windows Phone 8.1-Unternehmensportal-App**

  Wenn Endbenutzer Branchen-Apps installieren, profitieren sie nun von einer verbesserten, benutzerfreundlichen App-Installation. Wenn die App-Installation lange dauert, können die Benutzer ihr Gerät manuell synchronisieren, um die Fortsetzung des Synchronisierungsprozesses zu erzwingen. Die Endbenutzeranweisungen finden Sie unter [Sync your device manually to speed up app installations (Manuelles Synchronisieren des Geräts zum Beschleunigen von App-Installationen)](/intune/enduser/using-your-windows-device-with-intune) in der Intune-Bibliothek.  

###  <a name="new-in-1604-technical-preview"></a>Neuheiten in 1604 Technical Preview
 Die folgenden neuen Features vom April 2016 sind in Hybridbereitstellungen mit Intune und Configuration Manager Technical Preview 1604 verfügbar. Diese Features setzen voraus, dass Sie die Configuration Manager-Konsole zum Konfigurieren und Verwalten verwenden.  

- **Suchen, Verwalten und Verteilen von Windows Store für Unternehmen-Apps für Windows 10-Geräte über die Configuration Manager-Konsole**


  Unterstützung für Windows Store für Unternehmen ist in Configuration Manager Technical Preview 1604 verfügbar, damit Sie Apps für die von Ihnen verwalteten Windows 10-Geräte suchen, verwalten und verteilen können. Einzelheiten finden Sie unter [Verwalten von per Volumenlizenz aus dem Windows Store für Unternehmen erworbenen Apps](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) in [Funktionen in Technical Preview 1604 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **SmartLock-Einstellung für Android-Geräte**

  Eine neue Einstellung wurde dem Konfigurationselement „Android und Samsung KNOX Standard“ hinzugefügt. Mit dieser Einstellung können Sie das SmartLock-Feature auf kompatiblen Android-Geräten steuern.  Mit dieser Einstellung können Sie verhindern, dass Endbenutzer Smart Lock konfigurieren. Weitere Informationen finden Sie unter [SmartLock-Einstellung für Android-Geräte](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) in [Funktionen in Technical Preview 1604 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md).  

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)  
 Im April 2016 wurden keine neuen Hybridfeatures für Configuration Manager (Current Branch) eingeführt.  

##  <a name="new-hybrid-features-in-march-2016"></a>Neue Hybridfeatures im März 2016  

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune  
 Die folgenden im März 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.  

- **MAM-Steuerelemente, um die Synchronisierung von Kontakten zu verhindern (iOS)**

  Eine neue Einstellung ist verfügbar, mit der Sie verhindern können, dass eine Anwendung Kontakte mit dem nativen Adressbuch auf iOS-Geräten synchronisiert. Diese neue Einstellung wird von der Outlook-Anwendung auf iOS-Geräten unterstützt. Weitere Einzelheiten zu diesen und anderen Einstellungen finden Sie unter [Create and deploy MAM policies (Erstellen und Bereitstellen von MAM-Richtlinien)](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) in der Intune-Bibliothek.  

- **Skype for Business Online unterstützt den bedingten Zugriff**

  Sie können eine Richtlinie für bedingten Zugriff für Skype for Business Online festlegen, damit nur verwaltete und kompatible IOS- und Android-Geräte darauf zugreifen können.  Einzelheiten finden Sie unter [Manage access to Skype for Business Online (Verwalten des Zugriffs auf Skype for Business Online)](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) in der Intune-Bibliothek.  

- **Unterstützung für iOS 9.3**

  Am Montag, den 21. März, hat Apple die Verfügbarkeit von iOS 9.3 bekannt gegeben. Alle derzeit für die Verwaltung von iOS-Geräten verfügbaren Intune-Features werden auch weiterhin problemlos unterstützt, wenn die Benutzer ein Upgrade ihrer Geräte auf iOS 9.3 durchführen.  

- **Windows-App-Pakete direkt über die Unternehmensportal-Website verfügbar**

  Benutzer von Windows 8-, Windows 8.1- und Windows RT-PCs können jetzt Windows-App-Pakete (mit der Erweiterung „.appx“) direkt über die Unternehmensportal-Website installieren. Zuvor mussten Sie die Unternehmensportal-App bereitstellen, oder die Benutzer mussten die Unternehmensportal-App auf ihren Geräten installieren, um Apps zu installieren.  

- **Benutzer können ihr Gerät über die Unternehmensportal-Website remote sperren**

  Eine neue Option „Remotesperre“ wurde der Unternehmensportal-Website hinzugefügt, damit Benutzer ihr Gerät remote über das Portal sperren können, wenn es verloren ging oder gestohlen wurde.  

- **Profitieren Sie von der „Öffnen in“-Verwaltung für Geräte, die in einer Drittanbieter-MDM-Lösung angemeldet sind**

  Sie können über Ihren Drittanbieter der Verwaltung mobiler Geräte (MDM) von der „Öffnen in“-Verwaltung von iOS profitieren. Sie können die Einschränkungen in den Konfigurationsprofileinstellungen festlegen und die App mithilfe der MDM-Software bereitstellen. Wenn der Benutzer die verwaltete App installiert, werden die Einschränkungen angewendet. Lesen Sie die Details [Microsoft Intune-Richtlinien für die Verwaltung von mobilen Apps und iOS-Feature „Öffnen in“](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) in der Intune-Bibliothek.  

- **Microsoft-Apps, die MAM unterstützen**

  Die Liste der Microsoft-Apps, die Sie mit Verwaltungsrichtlinien für mobile Anwendungen von Intune verwenden können, wurde aktualisiert und enthält nun die neuesten Apps (nur für Geräte, die bei Intune registriert sind).  

- **Bereitstellen von Adobe Reader für Microsoft Intune auf Intune-verwalteten iOS-Geräten in Ihrem Unternehmen**

  Die Adobe Reader-App für iOS kann jetzt auf registrierten Geräten mit der Verwaltungsrichtlinie für mobile Anwendungen von Intune verwaltet werden.  

- Die Rights Management-Freigabe-App wird für Android unterstützt.

  IT-Administratoren können Verwaltungsrichtlinien für mobile Anwendungen bereitstellen, damit Endbenutzer Bilder, AV- und PDF-Dateien sicherer unabhängig davon anzeigen können, ob die IT die Geräte mit Intune verwaltet.  

- **Verbesserungen der Android- und iOS-Unternehmensportal-App**

  -   Wenn Ihre Benutzer eine App starten, die durch die Verwaltung mobiler Anwendungen (MAM) verwaltet wird, sehen sie eine Meldung, die sie darüber informiert, dass die App von ihrem Unternehmen verwaltet wird. Die Benutzer können nun auf eine Link „Weitere Informationen“ tippen, um weitere Informationen zur Bedeutung von „verwalteten Apps“ abzurufen. Sie können auch auf „Nicht mehr anzeigen“ tippen, damit die Meldung nicht mehr angezeigt wird, wenn sie die App starten.  

  -   Neue Bildschirme wurden hinzugefügt, um den Benutzer durch den Registrierungsprozess zu führen und darüber zu informieren, weshalb sich Benutzer registrieren sollten und was IT-Administratoren auf ihren registrierten Geräten sehen können und was nicht.  

  -   Registrierungsfehlermeldungen werden nun in der Unternehmensportal-App angezeigt.  

### <a name="new-in-configuration-manager-technical-preview"></a>Neuheiten in Configuration Manager Technical Preview  
 Im März 2016 wurden keine neuen Hybridfeatures für Configuration Manager Technical Preview eingeführt.  

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)  
 Die folgenden neuen Features vom März 2016 sind in Hybridbereitstellungen mit Intune und Configuration Manager (Current Branch) Version 1602 verfügbar. Diese Features setzen voraus, dass Sie die Configuration Manager-Konsole zum Konfigurieren und Verwalten verwenden.  

- **Richtlinien zur Konfiguration von iOS-Apps**

  In Version 1602 von Configuration Manager (Current Branch) können Sie App-Konfigurationsrichtlinien verwenden, um Einstellungen anzugeben, die beim Ausführen einer iOS-App durch den Benutzer erforderlich sein können. Weitere Einzelheiten finden Sie unter [Configure iOS apps with app configuration policies in System Center Configuration Manager (Konfigurieren von iOS-Apps mit Konfigurationsrichtlinien für Apps in System Center Configuration Manager)](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  

- **Verwalten von per Volumenlizenz erworbenen iOS-Apps**

  In Version 1602 von Configuration Manager (Current Branch) können Sie Apps bereitstellen und verwalten, die über das Apple Volume-Purchase Program (VPP) erworben wurden, indem die Lizenzinformationen aus dem App Store importiert werden und nachverfolgt wird, wie viele Lizenzen Sie verwendet haben. Weitere Informationen finden Sie unter [Manage volume-purchased iOS apps with System Center Configuration Manager (Verwalten von iOS-Apps, die über ein Volumenprogramm erworben wurden, mit System Center Configuration Manager)](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Automatische Erstellung von mobilen Office-Apps**

  Ab Version 1602 von Configuration Manager (Current Branch) werden die folgenden mobilen Microsoft Office-Apps für Android und iOS erstellt, wenn Sie ein Upgrade von Version 1511 durchführen:  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (nur iOS)  
  -   Microsoft Outlook  

  Sie finden diese Apps im Knoten „Anwendungen“ der Configuration Manager-Konsole. Weitere Informationen zum Bereitstellen von Anwendungen finden Sie unter [Bereitstellen von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Einstellungen für den Kioskmodus für Android Samsung KNOX Standard-Geräte**

  Über den Kioskmodus können Sie ein Gerät sperren, damit nur bestimmte Features funktionieren.  Ab Version 1602 von Configuration Manager (Current Branch) können Sie jetzt Einstellungen für den Kioskmodus für Samsung KNOX Standard-Geräte angeben. Einzelheiten finden Sie unter [Erstellen von Konfigurationselementen für Android- und Samsung KNOX Standard-Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **iOS-Aktivierungssperre**

  Ab Version 1602 von Configuration Manager (Current Branch) können Sie die iOS-Aktivierungssperre verwalten, ein Feature der App „Mein iPhone suchen“ für iOS 7.1 und höher. Die Aktivierungssperre wird automatisch aktiviert, wenn die iPhone-App „Mein iPhone suchen“ auf einem Gerät verwendet wird.  Einzelheiten finden Sie unter [Manage iOS Activation Lock Bypass with System Center Configuration Manager (Verwalten der iOS-Aktivierungssperre-Umgehung mit System Center Configuration Manager)](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock).  



<!--HONumber=Dec16_HO3-->


