---
title: Neues in Version 1706
titleSuffix: Configuration Manager
description: "Enthält Details zu Änderungen und neuen Funktionen, die in Version 1706 von System Center Configuration Manager eingeführt wurden."
ms.custom: na
ms.date: 08/11/2017
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: fddb31279587df5306c07a9f23dfc4dace418ea7
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2017
---
# <a name="what39s-new-in-version-1706-of-system-center-configuration-manager"></a>Neuerungen in Version 1706 von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Das Update 1706 für System Center Configuration Manager (Current Branch) ist als konsoleninternes Update für zuvor installierte Standorte verfügbar, die Version 1606, 1610 oder 1702 ausführen.

> [!TIP]  
> Sie müssen eine Baselineversion von Configuration Manager verwenden, um einen neuen Standort zu installieren.  
>  Weitere Informationen:    
>   - [Installieren von neuen Standorten](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Installieren von Updates an Standorten](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Baseline- und Updateversionen](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Die folgenden Abschnitte enthalten Details zu Änderungen und neue Funktionen, die in Version 1706 von Configuration Manager eingeführt wurden.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated features](/sccm/core/plan-design/changes/removed-and-deprecated-features).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastruktur von Standorten

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Unterstützung für Client-Peer-Cache für Express-Installationsdateien für Windows 10 und Office 365  
<!-- 1352486 -->
Ab dieser Version unterstützt Peercache die Verteilung von Express-Installationsdateien mit Inhalt für Windows 10 und von Updatedateien für Office 365. Weiteren Konfigurationen zur Unterstützung der Änderungen sind nicht erforderlich.

### <a name="updates-for-the-data-warehouse"></a>Updates für Data Warehouse
<!-- 1277922 -->
Data Warehouse ist nun kein vorab veröffentlichtes Features mehr. Außerdem haben wir die Voraussetzungen für die Unterstützung der Datenbank in SQL Server Always On-Verfügbarkeitsgruppen und Failoverclustern aktualisiert. Weitere Informationen finden Sie unter [The Data Warehouse service point (Der Data Warehouse-Dienstpunkt)](/sccm/core/servers/manage/data-warehouse).

### <a name="accessibility-improvements"></a>Verbesserungen der Barrierefreiheit
<!-- 1253000 -->
Wir haben weitere Verbesserungen an der Barrierefreiheit für die Configuration Manager-Konsole vorgenommen. Weitere Informationen finden Sie unter [Barrierefreiheitsfunktionen](/sccm/core/understand/accessibility-features).

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>Verbesserungen für SQL Server Always On-Verfügbarkeitsgruppen
<!-- 1352094 -->
Ab dieser Version können Sie jetzt Replikate mit asynchronem Commit in den SQL Server Always On-Verfügbarkeitsgruppen verwenden, die Sie mit Configuration Manager nutzen. Dies bedeutet, dass Sie Ihren Verfügbarkeitsgruppen zusätzliche Replikate hinzufügen können, die Sie als standortexterne (Remote-) Sicherungen und bei Bedarf in einem Notfallwiederherstellungsszenario einsetzen können.  
  -   Configuration Manager unterstützt das Verwenden von Replikaten mit asynchronem Commit zum Wiederherstellen Ihres synchronen Replikats. Unter [Wiederherstellungsoptionen für die Standortdatenbank](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) finden Sie im Thema zu Sicherung und Wiederherstellung weiterführende Informationen dazu.
  -   Diese Version unterstützt kein Failover, um das Replikat mit asynchronem Commit als Standortdatenbank zu verwenden.
Weitere Informationen finden Sie unter [Vorbereiten der Verwendung von SQL Server Always On-Verfügbarkeitsgruppen](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### <a name="update-reset-tool"></a>Tool zum Zurücksetzen von Updates
<!-- 1324589 -->
Ab Version 1706 enthalten primäre Standorte von Configuration Manager und Standorte der zentralen Verwaltung das Configuration Manager-Tool **CMUpdateReset.exe** zum Zurücksetzen von Updates. Sie können dieses Tool mit jeder weiterhin unterstützten Version (Current Branch) verwenden, um Probleme zu beheben, die bei konsoleninternen Updates während des Herunterladens oder Replizierens auftreten. Weitere Informationen finden Sie unter [Update reset tool (Tool zum Zurücksetzen von Updates)](/sccm/core/servers/manage/update-reset-tool).

### <a name="high-dpi-console-support"></a>Unterstützung einer hohen DPI-Einstellung in der Konsole  
<!-- 1353476 -->
Ab dieser Version sollten Probleme damit, wie die Configuration Manager-Konsole skaliert wird und verschiedene Teile der Benutzeroberfläche bei Betrachtung auf Geräten mit hohen DPI-Einstellungen angezeigt werden (z.B. Surface Book), behoben sein.

### <a name="improved-boundary-groups-for-software-update-points"></a>Verbesserte Begrenzungsgruppen für Softwareupdatepunkte
<!-- 1324591 -->
Diese Version bietet Verbesserungen dahingehend, wie Softwareupdatepunkte mit Begrenzungsgruppen arbeiten. Im Folgenden wird das neue Ausweichverhalten zusammengefasst:
-   Für Softwareupdatepunkte gibt es nun einen konfigurierbaren Zeitraum für ein Ausweichen auf benachbarte Begrenzungsgruppen.
-   Unabhängig von der Konfiguration des Ausweichens versucht ein Client, den letzten Softwareupdatepunkt zu erreichen, den er 120 Minuten verwendet hat. Sollte dieser Server in diesen 120 Minuten nicht erreicht werden, überprüft der Client seinen Pool verfügbarer Softwareupdatepunkte auf einen neuen.
-   Nachdem der Client seinen ursprünglichen Server zwei Stunden nicht erreicht hat, wechselt er beim Kontaktieren eines neuen Softwareupdatepunkts zu einem kürzeren Zyklus. Wenn also ein Client keine Verbindung mit einem neuen Server herstellen kann, wählt er rasch den nächsten Server in seinem Pool verfügbarer Server aus und versucht, diesen zu kontaktieren.

Weitere Informationen finden Sie im Thema zu Begrenzungsgruppen unter [Softwareupdatepunkte](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) für den Current Branch.

### <a name="azure-ad-integration-with-configuration-manager"></a>Azure AD-Integration mit Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
Mit diesem Release haben wir die Integration von Configuration Manager und Azure Active Directory (Azure AD) verbessert.  Durch diese Optimierungen können Sie nun Ihre Azure-Dienste mit Configuration Manager noch effizienter konfigurieren. Außerdem ist es nun leichter, Clients und Benutzer zu verwalten , die sich über Azure AD authentifizieren.

Die verbesserte Integration ermöglicht Folgendes:  
  -   Der Assistent für Azure-Dienste bietet eine allgemeine Konfigurationsumgebung, die die einzelnen Workflows mit den folgenden Azure-Diensten ersetzt, die Sie mit Configuration Manager verwenden.
      - **Cloud Management** Ermöglichen Sie es Clients, sich mit Azure Active Directory (Azure AD) authentifizieren. Außerdem können Sie die Azure AD-Benutzermittlung konfigurieren.
      - **OMS-Connector** Verbinden Sie sich mit der Microsoft Operations Management Suite (OMS) und synchronisieren Sie Daten wie Sammlungen mit der OMS-Protokollanalyse.
      - **Upgradebereitschaft** Verbinden Sie sich mit Upgrade Readiness, um Daten zur Kompatibilität von Clientupgrades anzuzeigen.
      - **Windows Store for Business** Verbinden Sie sich mit dem Onlineshop Windows Store for Business, um Apps für Ihre Organisation zu erhalten, die Sie mit Configuration Manager bereitstellen können.


  Dies erfolgt mithilfe einer [Azure-Serverwebanwendung](/azure/azure/app-service/app-service-authentication-overview#service-to-service-authentication), um das Abonnement und Konfigurationsdetails bereitzustellen, die Sie andernfalls jedes Mal eingeben müssen, wenn Sie eine neue Configuration Manager-Komponente oder einen -Dienst mit Azure einrichten. Weitere Informationen finden Sie unter [Assistent für Azure-Dienste](/sccm/core/servers/deploy/configure/azure-services-wizard).

-   Verwenden Sie Azure AD, um Clients über das Internet für den Zugriff auf Ihre Configuration Manager-Standorte zu authentifizieren. Dadurch müssen Sie keine Clientauthentifizierungszertifikate mehr konfigurieren. Hierzu ist die Standortsystemrolle Cloud Management Gateway erforderlich. Weitere Informationen finden Sie unter [Installieren und Zuweisen von Configuration Manager-Clients über das Internet mit Authentifizierung über Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Installieren und verwalten Sie den Configuration Manager-Client auf Computern, die sich im Internet befinden. Hierzu ist die Standortsystemrolle Cloud Management Gateway erforderlich. Weitere Informationen finden Sie unter [Installieren und Zuweisen von Configuration Manager-Clients über das Internet mit Authentifizierung über Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Konfigurieren Sie die Azure AD-Benutzerermittlung.  Verwenden Sie den Assistenten für Azure-Dienste zum Konfigurieren der neuen Ermittlungsmethode. Mit dieser werden Ihre Benutzerdaten von Azure AD abgefragt. Diese Daten können Sie anschließend zusammen mit den üblichen Ermittlungsdaten verwenden.  Sowohl eine vollständige Synchronisierung als auch eine Deltasynchronisierung werden unterstützt.  Weitere Informationen finden Sie unter [Azure AD-Benutzerermittlung](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

### <a name="peer-cache-improvements"></a>Verbesserungen des Peercaches
<!-- 1252345 -->
Das Netzwerkzugriffskonto wird nun nicht mehr von Peercache verwendet, um Downloadanforderungen von Peers zu authentifizieren. Eine Einschränkung ergibt sich allerdings dann, wenn das Konto weiterhin von Clients benötigt wird. Dies ist weiterhin eine Anforderung für Clients, die Windows PE starten und anschließend auf Inhalte aus einer Peercachequelle zugreifen. Weitere Informationen finden Sie unter [Anforderungen und Überlegungen für den Peercache](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache).


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Kompatibilitätseinstellungen

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Neue Konfigurationseinstellungen für Windows 10-Geräte, die nicht mit dem Konfigurations-Manager-Client verwaltet werden
<!-- 1354715 -->
In diesem Release haben wir neue Einstellungen des Konfigurationselements für Windows 10-Geräte hinzugefügt, die bei Intune registriert sind oder lokal von Configuration Manager verwaltet werden. Die folgenden Einstellungen stehen zur Verfügung:

- **Kennwort**
    - Geräteverschlüsselung
- **Gerät**
    - Änderung der Regionseinstellungen (nur Desktop)
    - Änderung der Energie- und Energiesparmoduseinstellungen
    - Änderung der Spracheinstellungen
    - Änderung der Systemzeit
    - Änderung des Gerätenamens
- **Store**
    - Apps aus Store automatisch aktualisieren
    - Nur privaten Store verwenden
    - Store-App starten
- **Microsoft Edge**
    - Zugriff auf about:flags-Seite blockieren
    - Außerkraftsetzen von SmartScreen-Aufforderung verhindern
    - Außerkraftsetzen von SmartScreen-Aufforderung für Dateien verhindern
    - WebRTC-LocalHost-IP-Adresse
    - Standardsuchmodul
    - OpenSearch-XML-URL
    - Homepages (nur Desktop)

Einzelheiten zu allen Windows 10-Einstellungen finden Sie unter [Erstellen von Konfigurationselementen für Windows 8.1- und Windows 10-Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).

### <a name="new-device-compliance-policy-rules"></a>Neue Konformitätsrichtlinienregeln für Geräte

* **Erforderlicher Kennworttyp**. Gibt an, ob Benutzer ein alphanumerisches oder numerisches Kennwort erstellen müssen. Geben Sie für alphanumerische Kennwörter außerdem die Mindestanzahl von Zeichengruppen an, die das Kennwort enthalten muss. Die vier Zeichengruppen sind Kleinbuchstaben, Großbuchstaben, Symbole und Zahlen.

 **Unterstützt auf:**
 * Windows Phone 8+
 * Windows 8.1+
 * iOS 6+
<br></br>
* **USB-Debugging auf Gerät blockieren**. Sie müssen diese Einstellungen nicht konfigurieren, da USB-Debuggen bereits auf Android for Work-Geräten deaktiviert ist.

 **Unterstützt auf:**
 * Android 4.0+
 * Samsung KNOX Standard 4.0+
<br></br>
* **Apps von unbekannten Quellen blockieren**. Fordert an, dass Geräte die Installation von Apps aus unbekannten Quellen verhindern. Sie müssen diese Einstellung nicht konfigurieren, da Android for Work-Geräte die Installation aus unbekannten Quellen stets einschränken.

  **Unterstützt auf:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Bedrohungsüberprüfung für Apps erzwingen**. Diese Einstellung gibt an, dass die Funktion „Apps überprüfen“ auf dem Gerät aktiviert ist.

 **Unterstützt auf:**
 * Android 4.2 bis 4.4
 * Samsung KNOX Standard 4.0+

Unter [Erstellen und Bereitstellen einer Konformitätsrichtlinie für Geräte](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy) finden Sie Informationen zur Anwendung der neuen Gerätekonformitätsregeln.

## <a name="application-management"></a>Anwendungsverwaltung

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole
<!-- 1236459 -->

In Configuration Manager können Sie mithilfe von Paketen und Programmen Skripts auf Clientgeräten bereitstellen. In diesem Release haben wir neue Funktionen hinzugefügt, mit denen Sie die folgenden Aktionen ausführen können:

- Importieren von PowerShell-Skripts in Configuration Manager
- Bearbeiten von Skripts in der Configuration Manager-Konsole (nur bei nicht signierten Skripts)
- Markieren von Skripts als „Genehmigt“ oder „Abgelehnt“ zum Verbessern der Sicherheit
- Anwenden von Skripts auf Sammlungen von Windows-Client-PCs und lokal verwaltete Windows-PCs. Sie stellen Skripts nicht bereit, sondern diese werden stattdessen nahezu in Echtzeit auf Clientgeräten ausgeführt.
- Überprüfen der Ergebnisse, die vom Skript in der Configuration Manager-Konsole zurückgegeben werden

Weitere Informationen finden Sie unter [Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole](/sccm/apps/deploy-use/create-deploy-scripts).

### <a name="new-mobile-application-management-policy-settings"></a>Neue Richtlinieneinstellungen für die Verwaltung mobiler Anwendungen    
<!--1324760-->
Ab dieser Version können Sie drei neue Richtlinieneinstellungen für die Verwaltung mobiler Anwendungen verwenden:

- **Bildschirmaufnahme blockieren (Nur Android-Geräte):** Gibt an, dass die Bildschirmaufnahmefunktionen des Geräts blockiert werden, wenn Sie diese App verwenden.

Unter [Schützen von Apps mithilfe von App-Schutzrichtlinien in Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) finden Sie Informationen zu den neuen Richtlinieneinstellungen zum Schutz von Apps.


## <a name="operating-system-deployment"></a>Betriebssystembereitstellung

### <a name="hardware-inventory-collects-secure-boot-information"></a>Die Hardwareinventur sammelt Sicherer Start-Informationen
Die Hardwareinventur sammelt jetzt Informationen darüber, ob Sicherer Start auf Clients aktiviert ist. Diese Informationen werden in der **SMS_Firmware**-Klasse (eingeführt in Version 1702) gespeichert und standardmäßig in der Hardwareinventur aktiviert. Weitere Informationen zur Hardwareinventur finden Sie unter [How to configure hardware inventory (Konfigurieren der Hardwareinventur)](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

### <a name="collapsible-task-sequence-groups"></a>Reduzierbare Tasksequenzgruppen
Diese Version bietet die Möglichkeit zum Erweitern und Reduzieren von Tasksequenzgruppen. Sie können einzelne Gruppen erweitern oder reduzieren oder alle Gruppen auf einmal erweitern oder reduzieren.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Neuladen von Startimages mit der aktuellen Version von Windows PE
Beim Ausführen von **Verteilungspunkte aktualisieren** auf einem ausgewählten Startimage können Sie jetzt wahlweise die neueste Version von Windows PE neu in das Startimage laden (aus dem Installationsverzeichnis von Windows ADK). Weitere Informationen finden Sie unter [Aktualisieren von Verteilungspunkten mithilfe des Startimages](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

## <a name="software-updates"></a>Softwareupdates

### <a name="improvements-to-express-update-download-time"></a>Verkürzte Downloadzeit bei Express-Update
In dieser Version haben wir die Downloadzeit für Express-Updates deutlich reduziert. Weitere Informationen finden Sie unter [Verwalten von Expressinstallationsdateien für Windows 10-Updates](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

### <a name="manage-microsoft-surface-driver-updates"></a>Verwalten von Microsoft Surface-Treiberupdates
<!-- 1098490 -->
Sie können Configuration Manager jetzt zum Verwalten von Microsoft Surface-Treiberupdates verwenden.    


#### <a name="prerequisites"></a>Voraussetzungen
- Auf allen Softwareupdatepunkten muss Windows Server 2016 ausgeführt werden.    
- Dies ist ein Vorabfeature, das Sie zuerst aktivieren müssen, um es zu benutzen. Weitere Informationen finden Sie unter [Use pre-release features from updates](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease) (Verwenden von Vorabfeatures aus Updates).

#### <a name="to-manage-surface-driver-updates"></a>So verwalten Sie Surface-Treiberupdates

1. Aktivieren Sie „Synchronisierung für Microsoft Surface-Treiber“. Folgen Sie den Schritten unter [Konfigurieren von Klassifizierung und Produkten](/sccm/sum/get-started/configure-classifications-and-products), und aktivieren Sie auf der Registerkarte **Klassifizierungen** das Kontrollkästchen **Microsoft Surface-Treiber und Firmwareupdates einbeziehen**, um Surface-Treiber zu aktivieren.
2. [Synchronisieren Sie die Microsoft Surface-Treiber](/sccm/sum/get-started/synchronize-software-updates).
3. [Stellen Sie die synchronisierten Microsoft Surface-Treiber bereit](/sccm/sum/deploy-use/deploy-software-updates).

### <a name="configure-windows-update-for-business-deferral-policies"></a>Konfigurieren von Windows Update for Business-Zurückstellungsrichtlinien
<!-- 1290890 -->
Sie können jetzt Zurückstellungsrichtlinien für Funktions- oder Qualitätsupdates für Windows 10 für Windows 10-Geräte konfigurieren, die von Windows Update for Business direkt verwaltet werden. Sie können die Zurückstellungsrichtlinien im neuen Knoten **Windows Update for Business-Richtlinien** unter **Softwarebibliothek** > **Windows 10-Wartung** verwalten.

Weitere Informationen finden Sie unter [Integration mit Windows Update für Unternehmen in Windows 10](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).

### <a name="improved-user-notifications-for-office-365-updates"></a>Verbesserte Benutzerbenachrichtigungen zu Office 365-Updates
Verbesserungen sind erfolgt, um die Office-Klick-und-Los-Benutzerumgebung zu nutzen, wenn ein Client ein Office 365-Update installiert. Dazu gehören Popup- und In-App-Benachrichtigungen sowie ein Countdown. Weitere Informationen finden Sie unter [Verhalten bei Neustart und Client-Benachrichtigungen für Office 365-Updates](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates).

## <a name="reporting"></a>Berichterstellung

### <a name="use-windows-analytics-with-configuration-manager"></a>Verwenden von Windows Analytics mit Configuration Manager
<!-- 1318608 -->
Windows Analytics umfasst Lösungen, die Teil der Operations Management Suite sind. Mit diesen Lösungen erhalten Sie wertvolle Einblicke in den aktuellen Status Ihrer Umgebung. Die Geräte in Ihrer Umgebung senden Windows-Telemetriedaten, auf die durch das Operations Management Suite-Webportal zugegriffen werden kann. Im Fall von Upgradebereitschaft stehen die Daten direkt im Knoten „Überwachung“ in der Configuration Manager-Konsole zur Verfügung.

Weitere Informationen finden Sie unter [Verwenden von Windows Analytics mit Configuration Manager](/sccm/core/clients/manage/monitor-windows-analytics).


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Verwaltung mobiler Geräte

### <a name="updates-to-android-for-work-sharing-configuration"></a>Updates für Freigabekonfiguration von Android for Work
<!-- 1338403 -->
Mit diesem Release wurden in der Einstellungsgruppe **Arbeitsprofil** die Werte für die Einstellung **Datenfreigabe zwischen Arbeits- und persönlichem Profil zulassen** aktualisiert. Wir haben außerdem eine benutzerdefinierten Einstellung hinzugefügt, mit der das Kopieren und Einfügen zwischen Arbeitsprofilen und persönlichen Profilen blockiert werden kann.

Weitere Informationen finden Sie unter [Konfigurationselemente für Android for Work-Geräte](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client).

### <a name="android-and-ios-enrollment-restrictions"></a>Registrierungseinschränkungen bei Android und iOS
<!-- 1290826 -->
Mit diesem Release können Sie nun angeben, dass Benutzer private Android- oder iOS-Geräte nicht registrieren können. Mit neuen Einstellungen für Geräteeinschränkungen können Sie die Registrierung von Android-Geräten auf vorab deklarierte Geräte beschränken. Für iOS-Geräte können Sie die Registrierung aller Geräte mit Ausnahme derjenigen blockieren, die mit dem Apple-Programm zur Geräteregistrierung, Apple Configurator oder dem Intune-Geräteregistrierungsmanager-Konto registriert werden.
- Weitere Informationen zu Einschränkungen bei der Android-Registrierung finden Sie unter [Set up Android hybrid device management with System Center Configuration Manager and Microsoft Intune](/sccm/mdm/deploy-use/enroll-hybrid-android) (Einrichten der Android-Hybridgeräteverwaltung mit System Center Configuration Manager und Microsoft Intune).
- Weitere Informationen zu Einschränkungen bei der iOS-Registrierung finden Sie unter [Configure enrollment restrictions](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions) (Konfigurieren von Registrierungseinschränkungen).

## <a name="protect-devices"></a>Schützen von Geräten

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Einbeziehen einer Vertrauensstellung für bestimmte Dateien und Ordner in eine Device Guard-Richtlinie
<!--1324676-->
In diesem Release haben wir der Gruppenrichtlinienverwaltung mit Device Guard weitere Funktionen hinzugefügt.

Sie können jetzt einer Device Guard-Richtlinie optional eine Vertrauensstellung für bestimmte Dateien oder Ordner hinzufügen. Dies ermöglicht Ihnen Folgendes:

- Beheben von Problemen mit dem Verhalten verwalteter Installationsprogramme
- Vertrauen branchenspezifischer Apps, die nicht mit Configuration Manager bereitgestellt werden können
- Vertrauen von Apps, die in einem Betriebssystemimage für ein Betriebssystem enthalten sind

Weitere Informationen finden Sie unter [Device Guard-Verwaltung mit Configuration Manager](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
