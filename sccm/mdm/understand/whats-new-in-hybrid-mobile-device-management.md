---
title: "Neuheiten bei der hybriden Verwaltung mobiler Geräte | Microsoft Intune |System Center Configuration Manager"
description: "Erfahren Sie mehr über die neuen Features der Verwaltung mobiler Geräte, die für Hybridbereitstellungen mit System Center Configuration Manager und Intune verfügbar sind."
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f13b38fcc4e7c55f05dbf6a7d8f516643939ba92
ms.openlocfilehash: 3525fba1b75196bddebc89e49f40cbfd3c75d9d0

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Neuheiten bei der hybriden Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieser Artikel bietet Details zu den neuen Features für die Verwaltung mobiler Geräte (MDM), die für Hybridbereitstellungen mit System Center Configuration Manager und Intune verfügbar sind.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Kompatibilität mit Configuration Manager-Versionen  

 Jeder Abschnitt dieses Artikels listet Hybridfeatures in drei verschiedenen Kategorien auf. Verwenden Sie die folgenden Anleitungen, um die Kompatibilität der Features in jeder Kategorie mit verschiedenen Versionen von Configuration Manager zu bestimmen:  

|Featurekategorien|
|-|  
|**Neuheiten in Microsoft Intune** – Im Allgemeinen sollten alle in dieser Kategorie aufgelisteten Features mit allen Configuration Manager-Releases, einschließlich Configuration Manager-Releases von System Center 2012 R2, zusammenarbeiten, da für diese Features nur der Intune-Dienst erforderlich ist, aber keine zusätzliche Funktionalität in Configuration Manager.<br /><br /> **Neuheiten in Configuration Manager Technical Preview** – Alle in dieser Kategorie aufgelisteten Features arbeiten nur mit dem angegebenen Technical Preview-Release zusammen. Um diese Features zu testen, müssen Sie die in der Featurebeschreibung angegebene Technical Preview-Version installieren. Weitere Informationen finden Sie unter [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Neuheiten in Configuration Manager (Current Branch)** – Alle in dieser Kategorie aufgelisteten Features arbeiten nur mit der angegebenen Version von Configuration Manager (Current Branch) zusammen, z.B. Version 1511 oder 1602. Wenn Sie eine ältere Version von Configuration Manager für die Hybridbereitstellung verwenden, müssen Sie ein Upgrade auf die in der Featurebeschreibung angegebene Configuration Manager-Version (Current Branch) ausführen. Weitere Informationen finden Sie unter [Upgrade auf System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## <a name="new-hybrid-features-in-october-2016"></a>Neue Hybridfeatures im Oktober 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

Die folgenden im Oktober 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **Bedingter Zugriff für die Verwaltung der mobilen Anwendung**

  Sie können den Zugriff auf Exchange Online einschränken, sodass nur Apps, die Verwaltungsrichtlinien für mobile Anwendungen von Intune unterstützen, z.B. Outlook, Zugriff haben. [Die neuen Features](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) passen perfekt zu den Verwaltungsrichtlinien für mobile Apps (Mobile App Management, MAM) von Intune, da Sie den Zugriff auf integrierte Mailclients oder andere Apps, die nicht mit den MAM-Richtlinien von Intune konfiguriert wurden, blockieren können. Dadurch wird sichergestellt, dass Ihre Benutzer auf die Daten Ihrer Organisation mit Apps zugreifen, die mit Intune MAM geschützt werden können. Sie können Ihre ersten Schritte mit den Verwaltungsrichtlinien für mobile Apps von Intune über das Azure-Portal unternehmen. Suchen Sie den neuen Abschnitt „Bedingter Zugriff“ auf dem Blatt „Einstellungen“.

-   **Intune App Wrapping Tool für Android**

  Sie können mithilfe des Intune App Wrapping Tools Ihre Apps so einstellen, dass sie die MAM-Richtlinien von Intune verwenden.

- **Android Samsung KNOX-Kompatibilität mit Intune**

  Bestimmte Modelle des Samsung Galaxy Ace-Telefons können nicht von Intune als Samsung KNOX-Geräte verwaltet werden. Wenn Sie diese Geräte bei Intune registrieren, werden sie stattdessen als Android-Standardgeräte verwaltet.

  Folgende Modellnummern sind betroffen:

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  Sie und Ihre Endbenutzer müssen keine weiteren Maßnahmen ergreifen. Weitere Informationen finden Sie auf der Samsung KNOX-Website.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Neuheiten in Configuration Manager Technical Preview 1610

Die folgenden neuen Hybridfeatures wurden im Oktober 2016 Configuration Manager Technical Preview 1610 eingeführt.

- **Richtliniensynchronisierung über die Verwaltungskonsole anfordern**

  Sie können eine Richtliniensynchronisierung auf einem registrierten mobilen Gerät über die Configuration Manager-Konsole anfordern, anstatt die Synchronisierung in der Unternehmensportal-App auf dem Gerät selbst anzufordern. Diese neue Aktion namens **Send Sync Request** (Synchronisierungsanforderung senden) finden Sie im Menü „Remotegeräteaktionen“, das bei Auswahl eines mobilen Geräts im Knoten „Geräte“ im Menüband angezeigt wird.

- **Windows Defender-Konfigurationseinstellungen**

  Sie können Windows Defender-Clienteinstellungen auf Intune-registrierten Windows 10-Computern mithilfe von Konfigurationselementen in der Configuration Manager-Konsole konfigurieren. Der Assistent für Konfigurationselemente bietet eine neue Einstellungsgruppe namens **Windows Defender**. Beachten Sie, dass dies nur auf Windows 10 Version 1511 und höher unterstützt wird.


### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Im August 2016 wurden keine neuen Hybridfeatures für Configuration Manager (Current Branch) eingeführt.

## <a name="new-hybrid-features-in-september-2016"></a>Neue Hybridfeatures im September 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

Die folgenden im September 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **Hinzufügen von „Benachrichtigungen“ zum Unternehmensportal für Android**

  Ein neues Symbol „Benachrichtigungen“ wurde dem Unternehmensportal für Android auf der Startseite hinzugefügt. Wenn Sie auf dieses Symbol tippen, gelangen Sie auf die Seite „Benachrichtigungen“, auf der Ihre Benutzer alle Elemente sehen, denen in der Unternehmens-App Beachtung geschenkt werden muss. Dazu gehören die Nichtkompatibilität von Geräten, Registrierungsupdates und die Registrierungsaktivierung. Die iOS-Unternehmensportal-App verfügt bereits über diese benutzerfreundlichen Benachrichtigungen. Aufgrund der neuen Seite „Benachrichtigungen“ wird die Seite „Setup des Unternehmenszugriffs“ nicht jedes Mal angezeigt, wenn Benutzer das Unternehmensportal starten oder fortsetzen. Voraussetzung ist jedoch, dass das Gerät bereits registriert ist. Wenn Sie eigene Endbenutzeranleitungen erstellen, sollten Sie auch Ihre Dokumentation entsprechend aktualisieren. Aktualisierte Screenshots finden Sie [hier](https://aka.ms/androidcpupdate).

- **Änderungen bei der Unterstützung der iOS-Unternehmensportal-App**

  Alle Benutzer der Microsoft Intune-Unternehmensportal-App für iOS müssen jetzt die neueste Version verwenden. Neue Benutzer können nur die neueste Version herunterladen, und aktuelle Benutzer müssen ein entsprechendes Update durchführen. Da die neueste Version iOS 8.0 oder höher erfordert, können Geräte mit älteren iOS-Versionen das Unternehmensportal erst verwenden oder sich registrieren, wenn sie ihr Gerät auf iOS 8.0 oder höher aktualisieren und dann die Unternehmensportal-App auf die neueste Version aktualisieren. Registrierte Geräte, auf den Versionen vor iOS 8.0 ausgeführt werden, werden weiterhin in der Intune-Verwaltungskonsole verwaltet und aufgeführt.

- **Schaltfläche „Feedback“ der Windows Phone 8.1-Unternehmensportal-App hinzugefügt**

  Die Windows Phone 8.1-Unternehmensportal-App ermöglicht Endbenutzern, Feedback über die App mithilfe einer neuen Schaltfläche „Feedback senden“ zu senden. Um auf die Schaltfläche zuzugreifen, tippen Benutzer auf das Drei-Punkte-Menü unten rechts auf dem Bildschirm der Unternehmensportal-App und dann auf **Feedback senden**. Das gesammelte, anonymisierte Feedback hilft Microsoft, die Benutzerfreundlichkeit der Unternehmensportal-App zu verbessern.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Neuheiten in Configuration Manager Technical Preview 1609

Die folgenden neuen Hybridfeatures wurden im Oktober 2016 für Configuration Manager Technical Preview 1609 eingeführt.

- **Zusätzliche Einstellungen und benutzerfreundlichere Konfigurationselement-Einstellungen**

  Neue Einstellungen für Android, iOS und Windows wurden hinzugefügt und nur die Einstellungen, die für die Plattformen gelten, die Sie auf der Seite „Unterstützte Plattformen“ wählen, werden im Assistenten angezeigt. Weitere Informationen finden Sie unter [New compliance settings for configuration items in TP 1609 (Neue Kompatibilitätseinstellungen für Konfigurationselement ein TP 1609)](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items).

- **Zusätzliche Einstellungen für DEP-Profile**

  TouchID, ApplePay und Zoom wurden als konfigurierbare Einstellungen in DEP-Profilen für iOS-Geräte hinzugefügt.

- **Kostenpflichtige Apps im Windows Store für Unternehmen**

  Sie können jetzt kostenpflichtige und kostenlose Apps zum Windows Store für Unternehmen hinzufügen und den Benutzern in Ihrer Organisation bereitstellen. Weitere Informationen finden Sie unter [Enhancements to Windows Store for Business in TP 1609 (Verbesserungen von Windows Store für Unternehmen in TP 1609)](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager).

- **Native connection types for Windows 10 VPN profiles (Native Verbindungstypen für Windows 10-VPN-Profile)**

  Sie können jetzt Windows 10-VPN-Profile für MDM mit Microsoft Automatic-, IKEv2- und PPTP-Verbindungstypen in der Configuration Manager-Konsole erstellen, ohne OMA-URI zu verwenden.

- **Intune-Kompatibilitätsdiagramme**

  Sie können einen schnellen Überblick über die allgemeine Gerätekompatibilität und die wichtigsten Gründe für Nichtkompatibilität mithilfe der neuen Diagramme unter dem Arbeitsbereich „Überwachung“ abrufen. Weitere Informationen finden Sie unter [Intune compliance charts in TP 1609 (Intune Compliance-Diagramme in TP 1609)](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Die folgenden neuen Features vom September 2016 sind in Hybridbereitstellungen mit Microsoft Intune und Configuration Manager Version 1606 (Current Branch) verfügbar.

- **iOS 10-Unterstützung**

  Wenn Sie Profile oder Konfigurationselemente für alle iOS-Plattformen vorgesehen haben, werden diese auch auf iOS 10 übertragen. Wir haben auch ein Update für Configuration Manager Release 1606 veröffentlicht, das Ihnen ermöglicht, Profile und Konfigurationselemente für einzelne iOS-Plattformen, einschließlich iOS 10, zu planen. Sie können das Update mit der Configuration Manager-Administratorkonsole über **Verwaltung > Übersicht > Cloud-Dienste > Updates und Wartung** installieren. Weitere Informationen über das Update finden Sie unter [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="new-hybrid-features-in-august-2016"></a>Neue Hybridfeatures im April 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

Die folgenden im August 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **Android 7-Unterstützung in der Unternehmensportal-App**

  Die Intune-Unternehmensportal-App für Android bietet „Tag 0“-Unterstützung für das neue Betriebssystem Android 7.0 für mobile Geräte.

- **Google entfernt Funktion „Kennung remote zurücksetzen“ auf Android 7.0-Geräten**

  Google entfernt die für IT-Administratoren und Endbenutzer verfügbare Funktion, die Kennung von Android 7.0-Geräten remote zurückzusetzen. Bisher konnten IT-Administratoren die Kennung von Benutzern remote zurücksetzen, und die Endbenutzer konnten ihre Kennungen über die Unternehmensportal-Website zurücksetzen.

- **Richtlinien für zulässige und blockierte Apps für Samsung KNOX-Geräte**

  Sie können nun eine benutzerdefinierte Richtlinie für Samsung KNOX-Geräte konfigurieren, mit der Sie eines der folgenden Elemente erstellen können:

  - Eine Liste von Apps, deren Ausführung auf dem Gerät blockiert wurde. Auch wenn sie installiert ist, kann eine in der Liste der blockierten Geräte definierte App nicht auf dem Gerät aktiviert werden.
  - Eine Liste der Apps, die Benutzer des Geräts aus dem Google Play Store installieren dürfen. Keine anderen Apps können aus dem Store installiert werden.

  Diese Einstellungen können nur von Geräten verwendet werden, die Samsung KNOX ausführen. Einzelheiten finden Sie unter [Use custom policies to allow and block apps for Samsung KNOX devices (Verwenden benutzerdefinierter Richtlinien, um Samsung KNOX-Geräte zuzulassen oder zu blockieren)](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Feedback-Link vom Unternehmensportal zu Microsoft**

   Die Unternehmensportal-Website ermöglicht Endbenutzern auf einen neuen Link „Feedback“ am unteren Rand der Seite zu tippen, um Feedback zu ihren Erfahrungen mit der Site an Microsoft zu senden. Das gesammelte, anonymisierte Feedback hilft Microsoft, die Benutzerfreundlichkeit der Unternehmensportal-Website zu verbessern.

- **Mindestversion von Managed Browser für iOS auf 8.0 aktualisiert**

  Die Microsoft Intune Managed Browser-App für iOS wurde aktualisiert und unterstützt nun Geräte, auf denen iOS 8.0 oder höher ausgeführt wird. Obwohl IOS 7.1-Geräte weiterhin die vorhandene Managed Browser-App verwenden können, sollten Sie die Benutzer auffordern, auf iOS 8.0 oder höher zu aktualisieren und die neuen Managed Browser-Features im vollen Umfang zu nutzen.

### <a name="new-in-configuration-manager-technical-preview"></a>Neuheiten in Configuration Manager Technical Preview

Im August 2016 wurden keine neuen Hybridfeatures für Configuration Manager Technical Preview eingeführt.

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Im August 2016 wurden keine neuen Hybridfeatures für Configuration Manager (Current Branch) eingeführt.

## <a name="new-hybrid-features-in-july-2016"></a>Neue Hybridfeatures im Juli 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

Die folgenden im Juli 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **Xamarin SDK für Intune-Apps ist verfügbar**

  Mit der Xamarin SDK-Komponente für Intune-Apps können Sie die Intune-Features für die Verwaltung mobiler Anwendungen in Ihren mit Xamarin erstellten mobilen iOS- und Android-Apps aktivieren. Sie finden die Komponente im [Xamarin Store](https://components.xamarin.com/view/Microsoft.Intune.MAM) oder auf der [Microsoft Intune-Github-Seite](https://github.com/msintuneappsdk).

- **Verbesserte Endbenutzererfahrung bei der Registrierung von Windows-Geräten**

  Wenn Sie den bedingten Zugriff verwenden, wurden die Registrierungsschritte für Windows 8.1, Windows 10 Desktop und Windows 10 Mobile auf der Unternehmensportal-Website geklärt. Benutzer sehen nun separate Schritte für die **Geräteregistrierung** und **Arbeitsplatzbereichsverknüpfung**, sodass sie den Status ihres Geräts besser verfolgen und den Prozess einfacher abschließen können, wenn ein Fehler bei der Arbeitsplatzverknüpfung auftritt. Separate Schritte sollen auch die Problembehandlung für IT-Administratoren zu vereinfachen. Wenn Endbenutzer versuchten, ein Gerät zu registrieren und alle Registrierungsschritte bis auf WPJ erfolgreich waren, wurde das registrierte Gerät bisher nicht in der Liste der für Benutzer zu identifizierenden Geräte angezeigt, was bei den Benutzern für Verwirrung sorgte.

 - **Vollständiges Zurücksetzen jetzt für Windows 10-Geräte verfügbar**

    Windows 10-PCs und Laptops, die als mobile Geräte registriert werden, können endgültig zurückgesetzt werden. Das Gerät wird dann auf seine Werkseinstellungen zurückgesetzt. Weitere Informationen finden Sie unter [How to protect your devices with remote wipe (Schützen von Geräten mithilfe von Remotezurücksetzung)](/sccm/mdm/deploy-use/wipe-lock-reset).

- **Änderungen an Geräteregistrierungsmanager-Konten in der iOS-Unternehmensportal-App**

  Zum Verbessern von Leistung und Skalierung zeigt Intune nicht mehr alle Geräteregistrierungsmanager-Geräte (Device Enrollment Manager, DEM) im Bereich „Meine Geräte“ in der iOS-Unternehmensportal-App an. Nur das lokale Gerät wird angezeigt, auf dem die App ausgeführt wird, und auch nur dann, wenn es über die Unternehmensportal-App registriert wurde.

  Der DEM-Benutzer kann Aktionen auf dem lokalen Gerät ausführen, aber die Remoteverwaltung der anderen registrierten Geräte kann nur über die Intune-Verwaltungskonsole durchgeführt werden. Darüber hinaus verwirft Intune die Verwendung von DEM-Konten mit dem Apple-Programm zur Geräteregistrierung oder dem Apple Configurator Tool als veraltet. Die beiden Registrierungsmethoden unterstützen bereits die Registrierung ohne Benutzer für freigegebene iOS-Geräte.

  Verwenden Sie DEM-Konten nur, wenn die Registrierung ohne Benutzer für gemeinsam genutzte Geräte nicht verfügbar ist. Weitere Informationen finden Sie unter [Registrieren von firmeneigenen Geräten mit dem Geräteregistrierungs-Manager in Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md).

- **Änderungen der Android-Unternehmensportal-App**

  Wenn Android-Endbenutzer von einer Fehlermeldung darüber informiert werden, dass ein erforderliches Zertifikat auf ihrem Gerät fehlt, können Sie auf die Schaltfläche „Problembehebung“ tippen und erhalten dann Anleitungen für die Installation des fehlenden Zertifikats. Wenn die Benutzer den Anleitungen folgen, aber eine weitere Fehlermeldung zu einem fehlenden Zertifikat angezeigt wird, sollten Sie sich an ihren IT-Administrator wenden und folgenden Link bereitstellen, der die Schritte enthält, mit denen IT-Administratoren das Zertifikatsproblem beheben können.

- **Installationen von quergeladenen Apps auf registrierte Android-Geräte beschränken**

  Android-Geräte können Apps nur noch dann über die Unternehmensportal-Website installieren, wenn die Geräte mithilfe der Intune-Unternehmensportal-App für Android in Intune registriert wurden.


### <a name="new-in-configuration-manager-technical-preview"></a>Neuheiten in Configuration Manager Technical Preview

Im Juli 2016 wurden keine neuen Hybridfeatures für Configuration Manager Technical Preview eingeführt.

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Die folgenden Features, die zuvor in Configuration Manager Technical Preview-Releases verfügbar waren, stehen nun in Hybridbereitstellungen mit Intune und Configuration Manager (Current Branch) Release 1606 zur Verfügung.

* Suchen, Verwalten und Verteilen von Windows Store für Unternehmen-Apps für Windows 10-Geräte über die Configuration Manager-Konsole ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   SmartLock-Einstellung für Android-Geräte ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   Per App ausgelöstes VPN für Windows 10-Geräte ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Benutzerfreundlichere Remotegeräteaktionen ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Windows Store für Unternehmen-Apps ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Allgemeine Verbesserungen für per Volumenlizenz erworbene Apps ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Windows Information Protection (WIP) ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Vorabdeklarieren von firmeneigenen Geräten mit IMEI- oder iOS-Seriennummer ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Automatisches Kategorisieren von Geräten in Sammlungen ([1606](whats-new-hybrid-archive.md#new-in-1606-technical-preview))

Informationen zu den neuen Funktionen finden Sie in der Dokumentation für das angegebene Technical Preview-Release.

## <a name="notices"></a>Benachrichtigungen

- **25. Oktober 2016: Windows Phone 8-Unternehmensportal-Upload als veraltet markiert**

  Die Funktion zum Hochladen einer signierten Unternehmensportal-App wurde aus der Configuration Manager-Konsole entfernt, da die Intune-Unterstützung für Windows 8, Windows Phone 8 und Windows RT veraltet ist und die Unterstützung für das Windows Phone 8-Unternehmensportal im November endet.  Bereits registrierte Windows 8-, Windows Phone 8- und Windows RT-Geräte werden weiterhin unterstützt, aber die Registrierung zusätzlicher Geräte bei diesen Plattformen wird nicht mehr unterstützt.


### <a name="see-also"></a>Siehe auch

- [Frühere Hybrid-MDM-Features](whats-new-hybrid-archive.md)
- [Neuigkeiten für MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)



<!--HONumber=Nov16_HO1-->

