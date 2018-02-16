---
title: "Neues bei der hybride Verwaltung mobiler Geräte"
titleSuffix: Configuration Manager
description: "Erfahren Sie mehr über die neuen Funktionen der Verwaltung mobiler Geräte, die für Hybridbereitstellungen mit Configuration Manager und Intune verfügbar sind."
ms.custom: na
ms.date: 02/06/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c724d9eafde6aa9abc0d3f9bfa867418046b2ecb
ms.sourcegitcommit: 389c4e5b4e9953b74c13b1689195f99c526fa737
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Neuheiten bei der hybriden Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieser Artikel bietet Details zu den neuen Features für die Verwaltung mobiler Geräte (MDM), die für Hybridbereitstellungen mit System Center Configuration Manager und Intune verfügbar sind.     

> [!Note]    
> Intune in Azure ist die von Microsoft empfohlene MDM-Lösung.     
> - Ausführliche Informationen zu neuen Funktionen und Updates in Intune Standalone finden Sie unter [Neuerungen in Microsoft Intune](https://docs.microsoft.com/intune/whats-new).    
> - Informationen zu einer Migration zu Intune Standalone finden Sie unter [Migrate hybrid MDM users and devices to Intune standalone (Migrieren von hybriden MDM-Benutzern und -Geräten zu Intune Standalone)](https://docs.microsoft.com/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).
> - Details zu UI-Updates für Intune und hybrid verwaltete MDM-Geräte finden Sie unter [Aktualisierungen für die Benutzeroberfläche für Endbenutzer-Apps in Intune](https://docs.microsoft.com/intune/whats-new-app-ui). 

##  <a name="compatibility-with-configuration-manager-versions"></a>Kompatibilität mit Configuration Manager-Versionen  
Jeder Abschnitt dieses Artikels listet Hybridfeatures in drei verschiedenen Kategorien auf. Verwenden Sie die folgenden Anleitungen, um die Kompatibilität der Features in jeder Kategorie mit verschiedenen Versionen von Configuration Manager zu ermitteln:  

|Featurekategorien|Beschreibung|
|-|-|
|**Neuheiten in Microsoft Intune** | Im Allgemeinen sollten alle in dieser Kategorie aufgeführten Features in allen Configuration Manager-Releases funktionieren. Dies umfasst auch Configuration Manager-Releases von System Center 2012 R2, da für diese Features nur der Intune-Dienst erforderlich ist und keine zusätzlichen Funktionen in Configuration Manager benötigt werden.|
|**Neuheiten in Configuration Manager Technical Preview**| Alle in dieser Kategorie aufgelisteten Features können nur mit dem angegebenen Technical Preview-Release verwendet werden. Um diese Features zu testen, müssen Sie die in der Featurebeschreibung angegebene Technical Preview-Version installieren. Weitere Informationen finden Sie unter [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Neuheiten in Configuration Manager (Current Branch)**| Alle in dieser Kategorie aufgelisteten Features können nur mit der angegebenen Version von Configuration Manager (Current Branch) verwendet werden, z.B. Version 1511 oder 1602. Wenn Sie eine ältere Version von Configuration Manager für die Hybridbereitstellung verwenden, müssen Sie ein Upgrade auf die in der Featurebeschreibung angegebene Configuration Manager-Version (Current Branch) ausführen. Weitere Informationen finden Sie unter [Upgrade auf System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|


## <a name="january-2018"></a>Januar 2018

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Genehmigen der Unternehmensportal-App für Android for Work** <!--1797090 -->    
  Wenn Ihre Organisation Android for Work verwendet, müssen Sie die Unternehmensportal-App für Android manuell genehmigen, damit diese weiterhin automatische Updates vom verwalteten Google Play-Store erhält.

- **Richtlinien für bedingten Zugriff für Intune sind nur über das Azure-Portal verfügbar**  <!-- 1737088 1634311 -->    
  Ab dieser Version müssen Sie Ihre Richtlinien für bedingten Zugriff im [Azure-Portal](https://portal.azure.com) konfigurieren und verwalten. Wählen Sie hierzu im Portal **Azure Active Directory** > **Bedingter Zugriff**. Der Einfachheit halber können Sie auch aus Intune auf dieses Blatt im Azure-Portal zugreifen. Wählen Sie hierzu **Intune** > **Zugangsberechtigung**.

- **Updates für Konformitäts-E-Mails** <!--1637547 -->    
  Wenn eine E-Mail gesendet wird, um ein nicht konformes Gerät zu melden, sind darin weitere Informationen zu diesem Gerät enthalten. 


- **Neue Funktionen für die Aktion „Lösung“ für Android-Geräte**<!--1583480-->    
  Die Unternehmensportal-App für Android erweitert die Aktion „Lösung“ für **Geräteeinstellungen aktualisieren**, um [Verschlüsselungsprobleme bei Geräten](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android) zu lösen.

- **Remote-Sperre in der Unternehmensportal-App für Windows 10 verfügbar** <!--676506-->    
  Endbenutzer können Ihre Geräte jetzt über die Unternehmensportal-App für Windows 10 über eine Remoteverbindung sperren. Dies wird nicht für das lokale Gerät angezeigt, dass sie aktiv verwenden.

- **Einfachere Behebung von Konformitätsproblemen in der Unternehmensportal-App für Windows 10** <!--676546-->    
  Endbenutzer mit Windows-Geräten können in der Unternehmensportal-App auf den Grund für die Nichtkonformität tippen. Falls möglich, werden sie direkt zu den richtigen Einstellungen in der Einstellungs-App weitergeleitet, wo Sie das Problem beheben können.

## <a name="december-2017"></a>Dezember 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Verfügbare Anwendungsbereitstellungen werden jetzt für Android Enterprise unterstützt**    
  Sie können Android Enterprise-Apps (vorher unter dem Namen „Android for Work“ bekannt) neben der Option **Erforderlich** jetzt auch als **Verfügbar** bereitstellen. Weitere Informationen finden Sie unter [Erstellen von Android-Apps mit System Center Configuration Manager](/sccm/mdm/deploy-use/creating-android-applications).


## <a name="november-2017"></a>November 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Textprotokoll aus verwalteten Apps zulässig** <!-- 1414050  -->    
  Apps, die vom Intune App SDK verwaltet werden, können SMS-Nachrichten senden.

- **Unternehmensportal-App für macOS verfügbar** <!--1541700-->    
  Das Intune-Unternehmensportal unter macOS hat eine optimierte Benutzeroberfläche, auf der alle Informationen und Konformitätsbenachrichtigungen, die Ihre Benutzer für alle registrierten Geräte benötigen, übersichtlich angezeigt werden. Und sobald das Intune-Unternehmensportal auf einem Gerät bereitgestellt wurde, werden Updates von Microsoft AutoUpdate für macOS bereitgestellt. Sie können das neue Intune-Unternehmensportal für macOS herunterladen, indem Sie sich auf einem macOS-Gerät bei der Website des Intune-Unternehmensportals anmelden.

- **Microsoft Planner ist jetzt Teil der MAM-Liste (Mobile App Management, Verwaltung mobiler Apps) mit genehmigten Apps**  <!-- 1248473 -->    
  Die Microsoft Planner-App für iOS und Android ist nun Teil der genehmigten Apps für die Verwaltung mobiler Apps (Mobile App Management, MAM). Die App kann im Azure-Portal auf dem Blatt „Intune-App-Schutz“ für alle Mandanten konfiguriert werden. Weitere Informationen finden Sie unter [MAM-Liste der genehmigten Apps](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).

- **Zugriff auf Protokolle von verwalteten Apps für iOS** <!-- 1469920 -->    
  Endbenutzer, auf deren Geräten der Managed Browser installiert ist, können jetzt auf den Verwaltungsstatus aller von Microsoft veröffentlichten Apps zugreifen und Protokolle für die Problembehandlung ihrer verwalteten iOS-Apps senden.
  
  Wie Sie den Problembehandlungsmodus im Managed Browser auf einem iOS-Gerät aktivieren, erfahren Sie unter [Zugreifen auf Protokolle von verwalteten Apps mithilfe des Managed Browsers unter iOS](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios).

- **Verbesserungen am Workflow für die Geräteeinrichtung im Unternehmensportal für iOS 2.9.0**    
  Der Workflow für die Geräteeinrichtung in der Unternehmensportal-App für iOS wurde verbessert. Die Sprache ist nun benutzerfreundlicher, und wir haben Bildschirme nach Möglichkeit zusammengeführt. Wir haben außerdem die Sprache für Ihr Unternehmen spezifischer gestaltet, indem wir Ihren Unternehmensnamen im gesamten Text des Setups verwendet haben. Dieser aktualisierte Workflow wird auf der Seite zu den [Neuerungen auf der App-Benutzeroberfläche](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017) beschrieben.

- **Aufforderungen zum Geben von Feedback zur Unternehmensportal-App für Android** <!--1165249-->    
Die Unternehmensportal-App fordert Android-Endbenutzer nun auf, Feedback zu geben. Dieses Feedback wird direkt an Microsoft gesendet und gibt Endbenutzern die Möglichkeit, die App im öffentlichen Google Play Store zu prüfen. Feedback ist nicht unbedingt erforderlich und kann problemlos abgelehnt werden, sodass die Benutzer die App weiterhin verwenden können. 

- **Informieren der Endbenutzer, welche Geräteinformationen für Windows 10-Geräte angezeigt werden** <!--1337920-->    
Auf dem Bildschirm „Gerätedetails“ der Unternehmensportal-App für Windows 10 wurde **Besitztyp** hinzugefügt. So können Benutzer weitere Informationen zum Datenschutz direkt von dieser Seite aus der Intune-Endbenutzerdokumentation erhalten. Sie finden diese Informationen auch auf dem Bildschirm **Info**.

- **Neue Aktion „Auflösen“ für Android-Geräte verfügbar** <!--1583480-->    
  Die Unternehmensportal-App für Android bietet auf der Seite _Geräteeinstellungen aktualisieren_ nun die Aktion „Auflösen“. Bei Auswahl dieser Option gelangt der Endbenutzer direkt zu der Einstellung, die dazu führt, dass sein Gerät nicht konform ist. Die Unternehmensportal-App für Android unterstützt derzeit diese Aktion für die Einstellungen [Gerätekennung](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android), [Geräteverschlüsselung](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android), [USB-Debuggen](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android) und [Unbekannte Quellen](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android). 


### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

- **Aktionen bei Nichtkonformität** <!--1321366 -->    
  Sie können nun eine zeitlich geordnete Abfolge von Aktionen konfigurieren, die auf Geräte angewendet werden, die nicht konform sind. Beispielsweise können Sie Endbenutzer nicht konformer Geräte per E-Mail benachrichtigen oder diese Geräte als nicht konform kennzeichnen. Einzelheiten finden Sie unter [Einrichten von Aktionen bei Nichtkonformität](/sccm/mdm/deploy-use/actions-for-noncompliance).

- **Neue Richtlinieneinstellungen für die Verwaltung mobiler Anwendungen** <!-- 1324760 -->    
  Die folgenden Einstellungen wurden den Richtlinieneinstellung zur Verwaltung mobiler Anwendungen hinzugefügt:
  - **Kontaktsynchronisierung deaktivieren:** Verhindert, dass die App Daten in der nativen App „Kontakte“ auf dem Gerät speichert.
  - **Drucken deaktivieren:** Verhindert, dass die App Geschäfts-, Schul- oder Unidaten druckt.

  Unter [Schützen von Apps mithilfe von App-Schutzrichtlinien in Configuration Manager](/sccm/mdm/deploy-use/protect-apps-using-mam-policies) finden Sie Informationen zu den neuen Richtlinieneinstellungen zum Schutz von Apps.

- **Unterstützung für Windows 10 ARM64-Geräte** <!-- 1355000 -->    
  Hybridszenarien für die Verwaltung mobiler Geräte (Mobile Device Management, MDM) werden auf ARM64-Geräte mit Windows 10 unterstützt, sobald diese Geräte verfügbar sind. Weitere Informationen finden Sie unter [Unterstützung für Windows 10 ARM64-Geräte](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support).

- **Verbesserte Benutzeroberfläche für VPN-Profile in der Configuration Manager-Konsole** <!-- 1318232 -->    
  Mit diesem Release haben wir den Assistenten zum Erstellen von VPN-Profilen und die VPN-Eigenschaftenseiten aktualisiert, sodass die Einstellungen der ausgewählten Plattform entsprechend angezeigt werden. Diese Funktion war zuvor in der Configuration Manager Technical Preview-Version 1709 verfügbar und steht nun in Hybridbereitstellungen mit Intune und Configuration Manager (Current Branch) der Version 1710 zur Verfügung:
  - [Verbesserte Benutzeroberfläche für VPN-Profile in der Configuration Manager-Konsole](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).


### <a name="new-in-configuration-manger-technical-preview-1711"></a>Neuerungen in Configuration Manager Technical Preview 1711

- **Neue Konformitätsrichtlinienoptionen für Windows 10** Sie können jetzt neue Optionen für Konformitätsrichtlinien für Windows 10-Geräte konfigurieren. Die neuen Einstellungen enthalten Richtlinien für Firewall, Benutzerkontensteuerung, Windows Defender Antivirus sowie Versionskontrolle für Betriebssystembuilds. Weitere Informationen finden Sie unter [Neue Konformitätsrichtlinienoptionen für Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10).


## <a name="october-2017"></a>Oktober 2017

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Neues in Configuration Manager Technical Preview 1709

- **Verbesserte Benutzeroberfläche für VPN-Profile in der Configuration Manager-Konsole** <!-- 1313282 -->     
  VPN-Profile werden jetzt nach Plattform gefiltert. Bei der Erstellung neuer VPN-Profile enthält jede unterstützte Plattform nur noch die für die Plattform geeigneten Einstellungen. Vorhandene VPN-Profile sind nicht betroffen. [In diesem Artikel](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console) erfahren Sie mehr darüber.


### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune  

- **Benutzerhilfe für die eigenständige Problembehandlung bei der Unternehmensportal-App für Android** <!-- 1573324, 1573150, 1558616, 1564878 -->      
  Die Unternehmensportal-App für Android enthält nun Anweisungen für Endbenutzer, damit sie neue Anwendungsfälle verstehen und, sofern möglich, selbst lösen.
    - Endbenutzer werden auf das [Azure Active Directory-Portal](https://account.activedirectory.windowsazure.com/r/#/profile) verwiesen, um ein Gerät zu entfernen, wenn sie die maximal erlaubte Anzahl von Geräten erreicht haben.
    - Endbenutzer erhalten schrittweise Anweisungen zum [Behandeln von Aktivierungsfehlern auf Samsung Knox-Geräten](https://go.microsoft.com/fwlink/?linkid=859718) oder zum [Ausschalten des Stromsparmodus](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). Wenn keine dieser Lösungen das Problem behebt, erhalten die Endbenutzer eine Erklärung der Vorgehensweise zum [Senden von Protokollen an Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).

- **Statusanzeige für die Geräteeinrichtung im Android-Unternehmensportal** <!--1565657-->    
  Die Unternehmensportal-App für Android zeigt eine Statusanzeige für die Geräteeinrichtung, wenn ein Benutzer sein Gerät registriert. Die Anzeige zeigt neue Zustände an beginnend mit „Ihr Gerät wird eingerichtet...“, dann „Ihr Gerät wird registriert...“, danach „Die Registrierung Ihres Geräts wird abgeschlossen...“ und schließlich „Die Einrichtung Ihres Geräts wird abgeschlossen...“.  

- **Unterstützung der zertifikatbasierten Authentifizierung im Unternehmensportal für iOS** <!--1029830-->    
  Die zertifikatbasierte Authentifizierung wird nun in der Unternehmensportal-App für iOS unterstützt. Benutzer mit CBA geben ihren Benutzernamen ein und tippen dann auf den Link „Sign in with a certificate“ (Mit einem Zertifikat anmelden). CBA wird in den Unternehmensportal-Apps für Android und Windows bereits unterstützt. Weitere Informationen dazu finden Sie auf der Seite zur [Anmeldung bei der Unternehmensportal-App](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal).

- **Verbesserungen am Workflow für die Geräteeinrichtung im Unternehmensportal** <!--1490692-->    
  Der Workflow für die Geräteeinrichtung in der Unternehmensportal-App für Android wurde verbessert. Die Sprache ist nun benutzerfreundlicher und spezifisch für unser Unternehmen. Zudem haben wir – wo es möglich war – Bildschirme vereint. Diese Änderungen werden auf der Seite zu den [Neuerungen in der App-Benutzeroberfläche](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017) beschrieben.

- **Verbesserte Betreuung bei der Anforderung des Zugriffs auf die Kontakte auf Android-Geräten** <!--1484985-->    
  Die Unternehmensportal-App für Android erfordert oftmals, dass der Benutzer die Berechtigung für Kontakte akzeptiert. Wenn ein Benutzer diesen Zugriff ablehnt, wird von jetzt an eine In-App-Benachrichtigung angezeigt, die Benutzer dazu auffordert, den bedingten Zugriff zu gewähren. 

- **Behebung von Sicherheitsproblemen bei sicherem Starten auf Android** <!--1490712-->    
  Benutzer mit Android-Geräten können in der Unternehmensportal-App auf den Grund für die Nonkonformität tippen. Falls möglich, werden sie direkt zu den richtigen Einstellungen in der Einstellungs-App weitergeleitet, wo Sie das Problem beheben können. 

- **Zusätzliche Pushbenachrichtigungen für Endbenutzer zur Unternehmensportal-App für Android Oreo** <!--1475932 -->    
  Endbenutzern werden zusätzliche Benachrichtigungen angezeigt, um Ihnen mitzuteilen, wann die Unternehmensportal-App für Android Oreo Hintergrundaufgaben wie das Abrufen von Richtlinien aus dem Intune-Dienst ausführt. Aufgrund dieser Benachrichtigungen sind Benutzer besser darüber informiert, wann die Unternehmensportal-App administrative Aufgaben auf ihren Geräten ausführt. Dies ist ein Teil der gesamten [Optimierung der Benutzeroberfläche des Unternehmensportals](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) für die Unternehmensportal-App für Android Oreo. 

- **Neues Verhalten für die Unternehmensportal-App für Android mit Arbeitsprofilen** <!--1485783-->    
  Wenn Sie ein Android for Work-Gerät mit einem Arbeitsprofil registrieren, werden Verwaltungsaufgaben auf dem Gerät über die Unternehmensportal-App im Arbeitsprofil ausgeführt. 

  Die Unternehmensportal-App für Android ist nur nützlich, wenn Sie eine für MAM aktivierte App im privaten Profil verwenden. Um die Benutzererfahrung für das Arbeitsprofil zu verbessern, wird die persönliche Unternehmensportal-App nach der Registrierung eines Arbeitsprofils in Intune automatisch ausgeblendet.

  Die Unternehmensportal-App für Android kann jederzeit im persönlichen Profil aktiviert werden, indem Sie [im Play Store nach der Unternehmensportal-App](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) suchen und auf **Aktivieren** tippen.

- **Unternehmensportal für Windows 8.1 und Windows Phone 8.1 in den nachhaltigen Modus verschieben** <!--1428681-->    
 Es wurde eine Benachrichtigung mit dem Hinweis hinzugefügt, dass die Unternehmensportal-Apps für Windows 8.1 und Windows Phone 8.1 in den nachhaltigen Modus verschoben werden. Details finden Sie unter [Benachrichtigungen](#notices).  

- **Blockieren der Registrierung nicht unterstützter Samsung KNOX-Geräte** <!-- 1490695 -->    
  Die Registrierung über die Unternehmensportal-App wird ausschließlich bei unterstützten Samsung KNOX-Geräten versucht. Um KNOX-Aktivierungsfehler zu vermeiden, die die MDM-Registrierung verhindern, wird die Geräteregistrierung nur versucht, wenn das Gerät in der von [Samsung veröffentlichten Geräteliste](https://www.samsungknox.com/knox-supported-devices/knox-workspace) enthalten ist. Einige Modellnummern von Samsung-Geräten unterstützen KNOX, andere nicht. Überprüfen Sie die Kompatibilität von KNOX mit Ihrem Geräte-Reseller vor dem Kauf und der Bereitstellung. Die vollständige Liste der überprüften Geräte finden Sie in der [Standardrichtlinieneinstellungen für Android und Samsung KNOX](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).

- **Ende des Supports für Android 4.3 und niedriger** <!--1171126, 1326920 -->    
  Eine Mitteilung zum Ablauf des Supports für Android 4.3 und niedriger wurde hinzugefügt. Details finden Sie unter [Benachrichtigungen](#notices).

- **Informieren von Benutzern darüber, welche Geräteinformationen für registrierte Geräte angezeigt werden** <!--1165314-->    
  Auf dem Bildschirm „Gerätedetails“ der Unternehmensportal-App für iOS wurde **Besitztyp** hinzugefügt. So finden Benutzer weitere Informationen zum Datenschutz direkt im Artikel [Welche Informationen erhält mein Unternehmen, wenn ich mein Gerät registriere?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune). Dies wird in naher Zukunft für alle Unternehmensportal-Apps eingeführt. Für iOS wurde dies im [September](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017) angekündigt. 


## <a name="september-2017"></a>September 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune     

- **Aktion „Aktualisieren“ zur Unternehmensportal-App für Windows 10 hinzugefügt** <!-- 1132468 -->    
    In der Unternehmensportal-App für Windows 10 können Benutzer die Daten nun aktualisieren, indem Sie sie auf „Aktualisieren“ ziehen oder indem Sie auf dem Desktop auf F5 drücken.

- **Informieren von Endbenutzern darüber, welche Geräteinformationen für iOS angezeigt werden** <!--739894-->    
    Auf dem Bildschirm „Gerätedetails“ der Unternehmensportal-App für iOS wurde **Besitztyp** hinzugefügt. So können Benutzer weitere Informationen zum Datenschutz direkt von dieser Seite aus der Intune-Endbenutzerdokumentation erhalten. Sie finden diese Informationen auch auf dem Bildschirm „Info“. 

- **Verständlichere Formulierung für die Unternehmensportal-App für Android** <!---1396349-->       
    Die Registrierung für das Unternehmensportal-App für Android wurde mit neuem Text vereinfacht, um Endbenutzern die Registrierung zu erleichtern. Wenn Sie eine benutzerdefinierte Registrierungsdokumentation verwenden, aktualisieren Sie sie gemäß der neuen Bildschirme. Beispielbilder finden Sie auf unserer Seite [Aktualisierungen für die Benutzeroberfläche für Endbenutzer-Apps in Intune](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017).

- **Der Zulassungsrichtlinie von Windows Information Protection wurde die Windows 10-Unternehmensportal-App hinzugefügt** <!-- 677129 -->    
    Die Windows 10-Unternehmensportal-App wurde aktualisiert, um Windows Informationen Protection (WIP) zu unterstützen. Die App kann der WIP-Zulassungsrichtlinie hinzugefügt werden. Dank dieser Änderung muss die App nicht mehr der Liste **Ausnahme** hinzugefügt werden. 

     Nur ein einzelnes WIP Konfigurationselement kann an ein Gerät übermittelt werden.  Wenn für zwei WIP-Konfigurationselemente das gleiche Gerät als Ziel gilt, wird keine WIP-Richtlinie angewendet.

- **Mitteilung zum Ablauf des Supports wurde für iOS 8.0 hinzugefügt**    
    Eine Mitteilung zum Ablauf des Supports für iOS 8.0 wurde hinzugefügt. Details finden Sie unter [Benachrichtigungen](#notices).

## <a name="august-2017"></a>August 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune     

- **Keine Registrierung mehr erforderlich für Benutzer des Android-Unternehmensportals und Benutzer von Apps mit App-Schutzrichtlinie** <!-- 621669 -->    
Endbenutzer können jetzt in der Android-Unternehmensportal-App nach Apps suchen, Geräte verwalten und IT-Kontaktinformationen anzeigen, ohne ihre Android-Geräte registrieren zu müssen. Neu ist auch, dass ein Endbenutzer, der bereits eine durch Intune-App-Schutzrichtlinien geschützte App verwendet und das Android-Unternehmensportal öffnet, keine Aufforderung mehr erhält, das Gerät zu registrieren.


## <a name="july-2017"></a>Juli 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Benachrichtigungen zu Ende der Unterstützung für Android und Windows Phone hinzugefügt**

    Neue Benachrichtigungen zum Ende der Unterstützung für Android- und Windows Phone-Versionen wurden hinzugefügt. Details finden Sie unter [Benachrichtigungen](#notices).


### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Die folgenden Features, die zuvor in Configuration Manager Technical Preview-Releases verfügbar waren, stehen nun in Hybridbereitstellungen mit Intune und Configuration Manager (Current Branch) Version 1706 zur Verfügung.

- [Entrust-Support für Entrust-Zertifizierungsstellen](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [Neue Richtlinieneinstellungen für die Verwaltung mobiler Anwendungen](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Updates für Freigabekonfiguration von Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [Neue Konformitätsrichtlinienregeln für Geräte](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Neue Konfigurationseinstellungen für Windows 10-Geräte, die nicht mit dem Konfigurations-Manager-Client verwaltet werden](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Cisco (IPsec)-Unterstützung für macOS-VPN-Profile](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Registrierungseinschränkungen bei Android und iOS](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 

## <a name="june-2017"></a>Juni 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Change your MDM authority (Ändern Ihrer MDM-Autorität)**

  Ab Configuration Manager Version 1610 können Sie Ihre MDM-Autorität ohne Unterstützung durch den Microsoft-Support und ohne Aufheben der Registrierung und erneutes Registrieren Ihrer vorhandenen verwalteten Geräte umstellen. Einzelheiten finden Sie unter [Umstellen der MDM-Autorität](/sccm/mdm/deploy-use/change-mdm-authority).

- **Managed Browser- und App-Proxyintegration**

  Der Intune Managed Browser lässt sich jetzt in den Azure AD-Anwendungsproxydienst integrieren, damit Benutzer auf interne Websites zugreifen können, selbst wenn sie remote arbeiten. Benutzer des Browsers geben die Website-URL wie üblich ein, woraufhin der Managed Browser die Anforderung durch das Webgateway des Anwendungsproxys leitet. Weitere Informationen finden Sie unter [Verwalten des Internetzugriffs mittels Richtlinien für Managed Browser](https://docs.microsoft.com/intune/app-configuration-managed-browser).

- **Die Unternehmensportal-App für Android bietet nun eine neue Benutzeroberfläche für App-Schutzrichtlinien**

  Als Reaktion auf das Feedback von Kunden haben wir die Unternehmensportal-App für Android durch Hinzufügen der Schaltfläche **Auf Unternehmensinhalte zugreifen** geändert. Zweck ist das Verhindern, dass Endbenutzer unnötigerweise den Registrierungsprozess durchlaufen, wenn sie lediglich auf Apps zugreifen müssen, die App-Schutzrichtlinien unterstützen, eine Funktion zur Verwaltung mobiler Anwendungen durch Intune. Diese Änderungen werden auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](https://docs.microsoft.com/intune/whats-new-app-ui) beschrieben.

- **Neue Menüaktion zum einfachen Entfernen des Unternehmensportals**

  Als Reaktion auf Benutzerfeedback wurde der Unternehmensportal-App für Android eine neue Menüaktion hinzugefügt, über die das Entfernen des Unternehmensportals von Ihrem Gerät eingeleitet wird. Über diese Aktion wird das Gerät aus der Intune-Verwaltung entfernt, damit die App vom Benutzer vom Gerät entfernt werden kann. Diese Änderungen werden auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](https://docs.microsoft.com/intune/whats-new-app-ui) und in der [Android-Endbenutzerdokumentation](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android) beschrieben.

- **Verbesserungen bei der App-Synchronisierung mit Windows 10 Creators Update**

  Die Unternehmensportal-App für Windows 10 löst jetzt automatisch eine Synchronisierung für App-Installationsanforderungen für Geräte mit Windows 10 Creators Update (Version 1703) aus. Dies reduziert das Problem, dass App-Installationen im Status „Synchronisierung ausstehend“ stecken bleiben. Darüber hinaus können Benutzer in der App manuell eine Synchronisierung auslösen. Diese Änderungen werden auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](https://docs.microsoft.com/intune/whats-new-app-ui) beschrieben.

- **Neues benutzerfreundlicheres Windows 10-Unternehmensportal**

  Die Unternehmensportal-App für Windows 10 bietet eine exemplarische Vorgehensweise für Intune für Geräte, die nicht identifiziert oder registriert wurden. Die neue Benutzeroberfläche bietet detaillierte Benutzeranweisungen für die Registrierung bei Azure Active Directory (für Funktionen mit bedingtem Zugriff erforderlich) und die MDM-Registrierung (für Geräteverwaltungsfunktionen erforderlich). Auf die exemplarische Vorgehensweise kann auf der Startseite des Unternehmensportals zugegriffen werden. Benutzer können die App weiter verwenden, auch wenn sie die Registrierung nicht abgeschlossen haben, erhalten aber eingeschränkte Funktionalität.

  Dieses Update ist nur auf Geräten mit dem Windows 10 Anniversary-Update (Build 1607) oder höher sichtbar. Diese Änderungen werden auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](https://docs.microsoft.com/intune/whats-new-app-ui) beschrieben.

- **Verbesserungen an den App-Kacheln in der Unternehmensportal-App für iOS**

  Wir haben das Design der App-Kacheln auf der Startseite entsprechend der Brandingfarbe geändert, die Sie für das Unternehmensportal festlegen. Weitere Informationen finden Sie auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Kontoauswahl nun in der Unternehmensportal-App für iOS verfügbar**

  Benutzer von iOS-Geräten wird bei der Anmeldung am Unternehmensportal möglicherweise unsere neue Kontoauswahl angezeigt, wenn sie sich bei anderen Microsoft-Apps mit ihrem Geschäfts-, Schul- oder Unikonto anmelden. Weitere Informationen finden Sie auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](https://docs.microsoft.com/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Neuerungen in Configuration Manager Technical Preview 1706

- **Neue Einstellungen für Windows-Konfigurationselemente**  <!-- 1354715 -->    

  Neue Windows-Konfigurationselemente sind verfügbar für die Einstellungskategorien Kennwort, Gerät, Speicher und Microsoft Edge. Weitere Informationen finden Sie unter [Neue Einstellungen für Windows-Konfigurationselemente](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).

- **Neue Konformitätsrichtlinienregeln für Geräte**    

  Sie können jetzt neue Optionen für Konformitätsrichtlinien konfigurieren, die zuvor nur in der eigenständigen Intune-Version verfügbar waren. Einzelheiten finden Sie unter [Verbesserungen bei Gerätekonformitätsrichtlinien](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Registrierungseinschränkungen bei Android und iOS** <!-- 1290826 -->      

  Administratoren können nun angeben, dass Benutzer private Android- oder iOS-Geräte nicht in ihrer Hybridumgebung registrieren können. Dies ermöglicht das Begrenzen registrierter Geräte auf vorab festgelegte unternehmenseigene Geräte bzw. auf iOS-Geräte, die ausschließlich mit dem Programm zur Geräteregistrierung registriert werden. Einzelheiten finden Sie unter [Registrierungseinschränkungen bei Android und iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).

- **Unterstützung für Entrust-Zertifizierungsstellen** <!-- 1350740 -->     

  Configuration Manager unterstützt jetzt Entrust-Zertifizierungsstellen. Dadurch können PFX-Zertifikate an Geräte übermittelt werden, die bei Microsoft Intune registriert sind.    

  Sie können Entrust als Zertifizierungsstelle konfigurieren, wenn Sie in Configuration Manager die Rolle „Zertifikatregistrierungspunkt“ hinzufügen. Beim Hinzufügen eines neuen Zertifikatprofils, das PFX-Zertifikate ausstellt, können Sie entweder eine Microsoft- oder Entrust-Zertifizierungsstelle auswählen.

  **Bekanntes Problem**: In der Technical Preview 1706 werden für Microsoft-Zertifizierungsstellen keine PFX-Zertifikate ausgestellt. Dies wirkt sich nicht auf importierte PFX-Zertifikate oder SCEP-Profile aus.

- **Cisco (IPsec)-Unterstützung für macOS-VPN-Profile**  <!-- 1321367 -->    

  Sie können ein macOS-VPN-Profil mit Cisco (IPsec) als Verbindungstyp erstellen. Weitere Informationen finden Sie unter [Erstellen von VPN-Profilen](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="april-2017"></a>April 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **„Meine Apps“ für Managed Browser verfügbar**

  „Meine Apps“ von Microsoft verfügt jetzt über eine bessere Unterstützung innerhalb von Managed Browser. Managed Browser-Benutzer, die keine Verwaltungsaufgaben ausführen müssen, gelangen direkt zum Dienst „Meine Apps“, wo sie auf die von ihrem Administrator bereitgestellten SaaS-Apps zugreifen können. Benutzer, die Verwaltungsaufgaben in Intune ausführen sollen, können weiterhin über das integrierte Managed Browser-Lesezeichen auf „Meine Apps“ zugreifen.

- **Neue Symbole für Managed Browser und das Unternehmensportal**

  Die Managed Browser-Symbole für die Android- und iOS-Versionen der App werden aktualisiert. Das neue Symbol enthält das aktualisierte Intune-Badge für mehr Konsistenz mit anderen Apps unter Enterprise Mobility + Sicherheit (EM+S). Das neue Symbol für Managed Browser finden Sie auf der Seite [Neuigkeiten in der Benutzeroberfläche der Intune-App](https://docs.microsoft.com/intune/whats-new-app-ui).

  Die Symbole für die Android-, iOS- und Windows-Versionen der App werden im Unternehmensportal ebenfalls aktualisiert, um die Konsistenz mit anderen Apps im EM+S zu verbessern. Diese Symbole werden schrittweise von April bis Ende Mai auf den einzelnen Plattformen veröffentlicht.

- **Anmeldungsstatusanzeige im Android-Unternehmensportal**

  Ein Update der Android-Unternehmensportal-App zeigt eine Statusanzeige für den Anmeldevorgang an, wenn der Benutzer die App startet oder fortsetzt. Die Statusanzeige durchläuft die neuen Phasen, beginnend mit „Verbindung wird aufgebaut“, „Anmeldung“ und dann „Suchen nach Sicherheitsanforderungen“, bevor dem Benutzer der Zugriff auf die App gewährt wird. Die neuen Bildschirme für die Unternehmensportal-App für Android finden Sie auf der Seite [Neuigkeiten in der Benutzeroberfläche der Intune-App](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Verhindern, dass Apps auf SharePoint Online zugreifen**

  Sie können jetzt eine Richtlinie für den App-basierten bedingten Zugriff erstellen, um Apps, auf die keine Schutzrichtlinien angewendet wurden, am Zugriff auf [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online) zu hindern. Im Szenario des App-basierten bedingten Zugriffs können Sie Apps festlegen, die über das Azure-Portal auf SharePoint Online zugreifen können sollen.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Neuheiten in Configuration Manager Technical Preview 1704

- **Konfigurieren von Android-Apps mit Konfigurationsrichtlinien für Apps**

  Sie können Konfigurationsrichtlinien für Apps in System Center Configuration Manager (Configuration Manager) verwenden, um vorkonfigurierte Einstellungen bereitzustellen, wenn ein Benutzer eine App auf Android for Work-Geräten ausführt. Konfigurationsrichtlinien für Android-Apps stehen nur auf Geräten zur Verfügung, die Android for Work ausführen, und gelten für genehmigte Apps aus dem Play for Work-Store. Informationen zum Testen dieses Features finden Sie unter [Konfigurieren von Android-Apps mit Konfigurationsrichtlinien für Apps](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).

## <a name="march-2017"></a>März 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Neue Benutzeroberfläche für die Unternehmensportal-App für Android**

  Die Benutzeroberfläche der Unternehmensportal-App für Android hat nun ein moderneres Design. Die wichtigen Updates sind:

  - Farben: Unternehmensportal-Registerkartenheader haben von der IT definierte Farben.
  - Apps: Auf der Registerkarte **Apps** wurden die Schaltflächen **Ausgewählte Apps** und **Alle Apps** aktualisiert.
  - Suche: Auf der Registerkarte **Apps** ist die Schaltfläche **Suche** eine schwebende interaktive Schaltfläche.
  - App-Navigation: In der Ansicht **Alle Apps** werden zur leichteren Navigation Registerkarten für **Ausgewählt**, **Alle** und **Kategorien** angezeigt.
  - Unterstützung: Die Registerkarten **Meine Geräte** und **An IT wenden** werden aktualisiert, um die Lesbarkeit zu verbessern.

  Weitere Informationen zu diesen Änderungen finden Sie unter [UI updates for Intune end user apps](https://docs.microsoft.com/intune/whats-new-app-ui) (Aktualisierungen der Benutzeroberfläche der Intune-Apps für Endbenutzer).

- **Signierungsskript für das Windows 10-Unternehmensportal**

  Wenn Sie die Windows 10-Unternehmensportal-App herunterladen und querladen müssen, können Sie nun ein Skript verwenden, um den App-Signierungsprozess für Ihre Organisation zu vereinfachen und zu optimieren.  Unter [Microsoft Intune Signing Script for Windows 10 Company Portal (Microsoft Intune-Signierungsskript für das Windows 10-Unternehmensportal)](https://aka.ms/win10cpscript) in der TechNet Gallery können Sie das Skript sowie die Anweisungen zu dessen Verwendung herunterladen. Weitere Informationen zu dieser Ankündigung finden Sie unter [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) (Aktualisieren Ihrer Windows 10-Unternehmensportal-App) im Blog des Intune-Supportteams.

- **Verbesserte Unterstützung für Android-Benutzer in China**

  Da der Google Play Store in China nicht zur Verfügung steht, müssen Apps für Android-Geräte von chinesischen Marketplaces abgerufen werden. Das Unternehmensportal unterstützt diesen Workflow, indem Android-Benutzer in China umgeleitet werden, um die Unternehmensportal- und Outlook-Apps aus lokalen App Stores herunterzuladen. Dies verbessert die Benutzerfreundlichkeit, wenn Richtlinien für den bedingten Zugriff sowohl für die Verwaltung mobiler Geräte als auch für die Verwaltung mobiler Anwendungen aktiviert sind. Die Unternehmensportal- und Outlook-Apps für Android sind in den folgenden chinesischen App Stores verfügbar:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Sicherstellen, dass Ihre Unternehmensportal-Apps auf dem neuesten Stand sind**

  Im Dezember 2016 haben wir ein Update veröffentlicht, das die Erzwingung für die mehrstufige Authentifizierung für eine Gruppe von Benutzern ermöglicht, wenn diese ein Gerät registrieren, auf dem iOS, Android oder Windows bzw. Windows Phone in einer höheren Version als 8.1 installiert ist. Dies funktioniert nicht ohne bestimmte Baselineversionen der Unternehmensportal-App für Android (v5.0.3419.0+) und iOS (v2.1.17+).

  Die Verwaltungsfunktionen von Intune werden kontinuierlich verbessert, und viele Verbesserungen enthalten koordinierte Updates für die Unternehmensportal-Apps auf allen unterstützten Plattformen. Daher wird empfohlen, dass Sie immer die neuesten Versionen der Unternehmensportal-Apps auf Geräten installiert haben, um die Verbesserungen in Intune zu nutzen und die bestmögliche Benutzerfreundlichkeit zu gewährleisten.

  >[!Tip]
  > Verlangen Sie von Ihren Benutzern, dass sie auf ihren Geräten die automatische App-Aktualisierung über den entsprechenden App Store aktiviert ist. Wenn Sie die Android-Unternehmensportal-App auf einer Netzwerkfreigabe bereitgestellt haben, können Sie die neueste Version aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49140) herunterladen.

- **Microsoft Teams ist nun für MAM unter iOS und Android aktiviert**

  Die Microsoft Teams-Apps für iOS und Android sind nun für die Funktionen der Verwaltung mobiler Apps (MAM) von Intune aktiviert, sodass Sie Ihren Teams ermöglichen können, frei über Geräte hinweg zu arbeiten, wobei sichergestellt wird, dass Konversationen und Unternehmensdaten jederzeit geschützt werden. Weitere Informationen finden Sie in der [Microsoft Teams-Ankündigung](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) im Enterprise Mobility and Security-Blog.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Neuheiten in Configuration Manager Technical Preview 1703

- **Zusätzliche Unterstützung für Apple Volume Purchase Program-Szenarios**

   Ab Technical Preview 1703 verfügen Sie nun über Unterstützung für die folgenden Volume Purchase Program-Szenarios (VPP):

   - Gerätelizenzierung: Apps, die die Gerätelizenzierung unterstützen und auf Gerätesammlungen bereitgestellt werden, benötigen jetzt nur eine Lizenz pro Gerät.  Zuvor mussten Sie eine Lizenz für jeden Benutzer auf einem Gerät verwenden. Weitere Informationen finden Sie unter [Bereitstellen per Volumenlizenz erworbener iOS-Apps in Gerätesammlungen](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Verwendung von mehreren VPP-Token für einen einzelnen Hybrid-Mandanten, wobei beide Token für die Verwaltung von VPP-Apps verwendet werden.
   - Verwendung von VPP Education-Token mit der Möglichkeit zur Unterscheidung zwischen Unternehmens- und Education-Token.

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Die folgenden Features, die zuvor in Configuration Manager Technical Preview-Releases verfügbar waren, stehen nun in Hybridbereitstellungen mit Intune und Configuration Manager (Current Branch) Version 1702 zur Verfügung.

- [Unterstützung für Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Kompatibilitätseinstellungen für nicht kompatible Apps](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [PFX-Zertifikat-Erstellung und -Verteilung und S/MIME-Unterstützung](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [Android- und iOS-Versionen werden nicht mehr über den Erstellungsassistenten für hybrides MDM erreicht](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Die folgenden zusätzlichen Hybridfeatures sind auch in Version 1702 von Configuration Manager (Current Branch) enthalten:

- **Verbesserter Support für Apple Volume Purchase Program (VPP)**

  - Sie können jetzt sowohl Geräten als auch Benutzern lizenzierte Apps bereitstellen. Je nachdem, inwieweit die App Gerätelizenzierungen unterstützt, wird eine entsprechende Lizenz wie folgt beansprucht:

    | Configuration Manager-Version | Unterstützt die App Gerätelizenzierung? | Typ der Bereitstellungssammlung | Beanspruchte Lizenz |
    |-|-|-|-|
    |Früher als 1702|Ja|Benutzer|Benutzerlizenz|
    |Früher als 1702|Nein|Benutzer|Benutzerlizenz|
    |Früher als 1702|Ja|Gerät|Benutzerlizenz|
    |Früher als 1702|Nein|Gerät|Benutzerlizenz|
    |1702 und höher|Ja|Benutzer|Benutzerlizenz|
    |1702 und höher|Nein|Benutzer|Benutzerlizenz|
    |1702 und höher|Ja|Gerät|Gerätelizenz|
    |1702 und höher|Nein|Gerät|Benutzerlizenz|

  - Außerdem können Sie Apps bereitstellen und nachverfolgen, die Sie in iOS Volume Purchase Program für Bildungseinrichtungen erworben haben.

  - Sie können Configuration Manager jetzt mehrere Apple VPP-Tokens zuordnen.

  Weitere Informationen zu iOS-Apps, die über ein Volumenprogramm erworben wurden, finden Sie unter [Verwalten von iOS-Apps, die über ein Volumenprogramm erworben wurden](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Support für branchenspezifische Apps im Microsoft Store für Unternehmen**

  Sie können jetzt benutzerdefinierte branchenspezifische Apps aus dem Microsoft Store für Unternehmen synchronisieren.

- **Neue Überwachungstools für Mobile Threat Defense**

    Sie haben nun neue Möglichkeiten, den Kompatibilitätsstatus mit Ihrem Dienstanbieter für Mobile Threat Defense zu überwachen.

    Weitere Informationen finden Sie unter [How to monitor Mobile Threat Defense compliance (Überwachen der Kompatibilität von Mobile Threat Defense)](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="february-2017"></a>Februar 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Modernisieren der Unternehmensportal-Website**

  Die Unternehmensportal-Website unterstützt Apps, die für Benutzer ausgelegt sind, die nicht über verwaltete Geräte verfügen. Die Website richtet sich nach anderen Microsoft-Produkten und Diensten, indem sie ein neues kontrastreiches Farbschema, dynamische Illustrationen und ein „Hamburger-Menü“ verwendet, das Helpdesk-Kontaktinformationen und Informationen zu vorhandenen verwalteten Geräte enthält. Die Zielseite wird neu angeordnet, um für Benutzer verfügbare Apps mit Karussellsteuerelementen für unterstützte und vor kurzem aktualisierte Apps hervorzuheben. Vorher-Nachher-Bilder sind auf der Seite [UI-Updates](https://docs.microsoft.com/intune/whats-new-app-ui) verfügbar.

- **Neue MDM-Serveradresse für Windows-Geräte**

  Die MDM-Serveradresse für die Registrierung von Windows- und Windows Phone-Geräten wurde von „manage.microsoft.com“ in „enrollment.manage.microsoft.com“ geändert. Benachrichtigen Sie Ihre Benutzer, dass „enrollment.manage.microsoft.com“ als Adresse des MDM-Servers verwendet werden soll, wenn sie bei der Registrierung eines Windows- oder und Windows Phone-Geräts zur Eingabe der Adresse aufgefordert werden. Dieses Update erfordert zudem, dass jeder CNAME-Eintrag im DNS, der von „EnterpriseEnrollment.contoso.com“ zu „manage.microsoft.com“ umleitet, durch einen CNAME-Eintrag im DNS ersetzt wird, der von „EnterpriseEnrollment.contoso.com“ zu „EnterpriseEnrollment-s.manage.microsoft.com“ umleitet. Weitere Informationen zu dieser Änderung finden Sie unter „http://aka.ms/intuneenrollsvrchange“.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Neuheiten in Configuration Manager Technical Preview 1702

- **Unterstützung für Android for Work**

  Sie können nun Android-Geräte mithilfe von Android for Work in hybriden MDM-Umgebungen mithilfe von Configuration Manager Technical Preview 1702 verwalten. Unterstützte Android-Geräte können jetzt als Android for Work-Geräte angemeldet werden, wodurch ein Arbeitsprofil auf dem Gerät erstellt wird, an das in Play for Work genehmigte Apps bereitgestellt werden können. Sie können auch Konfigurationselemente, Kompatibilitätsrichtlinien und Ressourcenzugriffsprofile für diese Geräte konfigurieren und bereitstellen. Weitere Informationen finden Sie unter [Unterstützung für Android for Work](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Kompatibilitätseinstellungen für nicht kompatible Apps**

  Sie können jetzt Regeln für nicht kompatible Apps für Android- und iOS-Apps in Kompatibilitätsrichtlinien erstellen. Geräte, auf denen die angegebenen Anwendungen installiert sind, werden als „nicht konform“ gekennzeichnet und verlieren den Zugriff auf Unternehmensressourcen gemäß den geltenden Richtlinien für bedingten Zugriff. Weitere Informationen finden Sie unter [Verbesserungen bei Gerätekompatibilitätsrichtlinien für bedingten Zugriff](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **PFX-Zertifikat-Erstellung und -Verteilung und S/MIME-Unterstützung**

  Sie können jetzt PFX-Zertifikate für Benutzer in einer Hybridumgebung erstellen und bereitstellen. Diese Zertifikate können dann von Geräten, die der Benutzer registriert hat, für die E-Mail-Verschlüsselung und -Entschlüsselung mit S/MIME verwendet werden. Weitere Informationen finden Sie unter [Erstellen von PFX-Zertifikaten mit S-MIME-Unterstützung](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Unterstützung für zusätzliche Einstellungen für iOS-Konfigurationen**
   
    Ihnen stehen nun 42 zusätzliche iOS-Einstellungen zur Verfügung, die Sie als Teil eines Konfigurationselements konfigurieren können. Ein Großteil der Einstellungen (insgesamt 35) wurden für überwachte iOS-Geräte hinzugefügt. Weitere Informationen finden Sie unter [New compliance settings for iOS-Geräte (Neue Kompatibilitätseinstellungen für iOS-Geräte)](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## <a name="january-2017"></a>Januar 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Android 7.1.1-Unterstützung**

  Intune unterstützt und verwaltet Android 7.1.1 jetzt vollständig.

- **Problembehandlung für inaktive iOS-Geräte oder die Verwaltungskonsole kann nicht mit ihnen kommunizieren**

  Wenn Benutzergeräte den Kontakt mit Intune verlieren, können Sie neue Problembehandlungsschritte vergeben, damit sie erneut Zugriff auf Unternehmensressourcen erhalten. Siehe [Geräte sind inaktiv oder die Verwaltungskonsole kann nicht mit ihnen kommunizieren](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Neuheiten in Configuration Manager Technical Preview 1701

- **Android- und iOS-Versionen werden nicht mehr über den Erstellungsassistenten für hybrides MDM erreicht**

  Ab Technical Preview 1701 für die hybride mobile Geräteverwaltung (MDM) müssen Sie nicht mehr bestimmte Android- und iOS-Versionen auswählen, wenn Sie neue Richtlinien und Profile für mit Intune verwaltete Geräte erstellen wollen. Durch diese Änderung können Hybridbereitstellungen schneller neue Android und iOS-Versionen unterstützen, ohne eine neue Configuration Manager-Version oder -Erweiterung zu benötigen. Weitere Informationen finden Sie unter [Android and iOS versions are no longer targetable in creation wizards (Android- und iOS-Versionen werden nicht mehr über den Erstellungsassistenten für hybrides MDM erreicht)](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="notices"></a>Benachrichtigungen

### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Unternehmensportal für Windows 8.1 und Windows Phone 8.1 in den nachhaltigen Modus verschieben 
<!--1428681-->
*6. Oktober 2017*   
 
Ab Oktober 2017 werden die Unternehmensportal-Apps für Windows 8.1 und Windows Phone 8.1 in den nachhaltigen Modus verschoben. Dies bedeutet, dass die Apps und vorhandenen Szenarios, z.B. Registrierungs- und Konformitätsprozesse, weiterhin für diese Plattformen unterstützt werden. Diese Apps sind weiterhin über vorhandene Veröffentlichungskanäle wie den Microsoft Store zum Download verfügbar. 

Im nachhaltigen Modus empfangen diese Apps nur wichtige Sicherheitsupdates. Es werden keine zusätzlichen Updates oder Funktionen für diese Apps veröffentlicht. Wenn Sie neue Funktionen installieren möchten, empfehlen wir, dass Sie die Geräte auf Windows 10 und Windows 10 Mobile aktualisieren. 

### <a name="end-of-support-for-ios-80"></a>Ende der Unterstützung für iOS 8.0 
<!---1164477--->
Verwaltete Apps und die Unternehmensportal-App für iOS erfordern iOS 9.0 oder höher für den Zugriff auf Unternehmensressourcen. Geräte, die vor September nicht aktualisiert werden, können dann nicht mehr auf das Unternehmensportal oder diese Apps zugreifen. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Erinnerung zu Plattform-Unterstützung: Grundlegende Unterstützung von Windows Phone 8.1 am 11. Juli 2017 beendet
<!-- 1327781 -->
*11. Juli 2017*

Die grundlegende Unterstützung für Windows Phone 8.1 wurde eingestellt. Die Unterstützung für Windows 8.1-PCs ist davon nicht beeinträchtigt.

Windows Phone 8.1-Geräte, die vom Intune-Dienst verwaltet werden, sind nicht unmittelbar betroffen. Dies gilt auch für Geräte, die in einer hybriden MDM registriert sind. Registrierte Geräte sind weiterhin funktionsfähig. Außerdem werden alle Richtlinien, Konfigurationen und Apps weiterhin wie gewohnt funktionieren. Beachten Sie, dass keine Verbesserungen für Windows Phone 8.1 innerhalb des Intune-Dienstes und für die Unternehmensportal-App von Windows Phone 8.1 vorgesehen sind.

Es wird empfohlen, auf geeigneten Windows Phone 8.1-Geräten möglichst bald ein Upgrade auf Windows 10 Mobile durchzuführen.  

### <a name="end-of-support-for-android-43-and-lower"></a>Ende des Supports für Android 4.3 und niedriger
<!---1171127--->
*6. Juli 2017*

Verwaltete Apps und die Unternehmensportal-App für Android erfordern Android 4.4 oder höher für den Zugriff auf Unternehmensressourcen. Geräte, die vor Anfang Oktober nicht aktualisiert werden, können dann nicht mehr auf das Unternehmensportal oder diese Apps zugreifen. Im Dezember werden alle registrierten Geräte zwangsweise außer Kraft gesetzt, sodass kein Zugriff auf Unternehmensressourcen mehr möglich ist. Wenn Sie App-Schutzrichtlinien ohne MDM verwenden, erhalten Apps erhält keine Updates, und ihre Nutzungsqualität wird im Laufe der Zeit immer stärker abnehmen.


### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 und System Center 2012 R2 Configuration Manager (RTM): Die Unterstützung für die Verwaltung von hybriden Mobilgeräten endet am 10. April 2017.
*11. Januar 2017*

Die Unterstützung für System Center 2012 Configuration Manager SP1 und System Center 2012 R2 Configuration Manager RTM endete am 12. Juli 2016. In der Folge wird die Unterstützung für die mit dem Microsoft Intune-Dienst verbundenen Versionen für Hybrid-MDM am 10. April 2017 beendet. Nach diesem Datum wird Hybrid-MDM mit diesen Versionen nicht mehr funktionieren. Verwaltete Geräte werden grundsätzlich zu nicht verwalteten Geräten, weil der Intune-Connector nicht mehr mit dem Intune-Dienst verbunden ist. Configuration Manager-Daten (z.B. Richtlinien und Anwendungen) werden nicht an Intune übertragen und Daten von verwalteten Geräten werden bis zur Ausführung eines Upgrades nicht an Configuration Manager übermittelt.

Wenn Sie eine hybride Bereitstellung mit Configuration Manager 2012 SP1 oder R2 RTM ausführen, wird die Durchführung eines Upgrades auf Configuration Manager (Current Branch) oder das letzte unterstütze Service Pack für Configuration Manager 2012 (R2 SP1 oder SP2) noch vor dem 10. April 2017 empfohlen, um eine Dienstunterbrechung zu vermeiden.

Zusätzliche Ressourcen:
-   [Upgrade auf System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [Planen von Upgrades auf System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [Planen von Upgrades auf System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Upload in Unternehmensportal für Windows Phone 8 eingestellt
*25. Oktober 2016*

Die Funktion zum Hochladen einer signierten Unternehmensportal-App wurde aus der Configuration Manager-Konsole entfernt, da die Intune-Unterstützung für Windows 8, Windows Phone 8 und Windows RT veraltet ist und die Unterstützung für das Windows Phone 8-Unternehmensportal im November endet.  Bereits registrierte Windows 8-, Windows Phone 8- und Windows RT-Geräte werden weiterhin unterstützt, aber die Registrierung zusätzlicher Geräte bei diesen Plattformen wird nicht mehr unterstützt.


### <a name="see-also"></a>Siehe auch

- [Frühere Hybrid-MDM-Features](whats-new-hybrid-archive.md)
- [Neuigkeiten für MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
