---
title: Upgrade Analytics | System Center Configuration Manager
description: "Integrieren Sie Upgrade Analytics mit Configuration Manager. Greifen Sie auf Daten zur Upgradekompatibilität in Ihrer Administratorkonsole zu. Führen Sie Upgrades oder Wartungen von Geräten aus."
keywords: 
author: nbigman
ms.author: nbigman
manager: angerobe
ms.date: 11/23/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
translationtype: Human Translation
ms.sourcegitcommit: bf28164fc2594d2557db5626a6f52c32ad99a1fe
ms.openlocfilehash: fa90fa0da348e7cca186ff8066c7a9fa98c57cf5


---

# <a name="integrate-upgrade-analytics-with-system-center-configuration-manager"></a>Integrieren von Upgrade Analytics mit Configuration Manager

Mit Upgrade Analytics können Sie die Gerätebereitschaft und -kompatibilität unter Windows 10 bewerten und analysieren und dadurch einfachere und reibungslose Upgrades ermöglichen. Integrieren Sie Upgrade Analytics mit Configuration Manager, um auf Daten zur Kompatibilität von Clientupgrades in der Configuration Manager-Verwaltungskonsole zugreifen. Dort können Sie auch Geräte aus der Geräteliste für ein Upgrade oder Wartungsaufgaben auswählen.

Upgrade Analytics ist eine Lösung in der Microsoft Operations Management Suite (OMS). Erfahren Sie mehr über Upgrade Analytics in [Get started with Upgrade Analytics (Erste Schritte mit Upgrade Analytics)](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started).

## <a name="configure-clients"></a>Konfigurieren von Clients

Es gibt mehrere Konfigurationsschritte, die Sie durchführen müssen, um sicherzustellen, dass Ihre Clients für Upgrade Analytics Daten bereitstellen können:

-  Konfigurieren Sie Clienttelemetrieeinstellungen wie unter [Konfigurieren der Windows-Telemetrie in Ihrem Unternehmen](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization) beschrieben.
-  Installieren Sie den KB-Artikel, der im Abschnitt *Deploy the compatibility update and related KBs (Bereitstellen der Kompatibilitätsaktualisierung und entsprechende KB-Artikel)*des Themas [Get started with Upgrade Analytics (Erste Schritte mit Upgrade Analytics)](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) beschrieben wird.

    > [!NOTE]
    > Sie können ein Skript zur Automatisierung vieler Clientsetupaufgaben herunterladen. Weitere Informationen zu diesem Skript finden Sie im Abschnitt *Run the Upgrade Analytics deployment script (Ausführen des Bereitstellungsskripts für Upgrade Analytics)* des Themas [Get started with Upgrade Analytics (Erste Schritte mit Upgrade Analytics)](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started).

## <a name="create-a-connection-to-upgrade-analytics"></a>Erstellen einer Verbindung mit Upgrade Analytics

### <a name="prerequisites"></a>Voraussetzungen

- Um der Configuration Manager-Umgebung eine Verbindung hinzuzufügen, müssen Sie zunächst einen [Dienstverbindungspunkt](/sccm/core/servers/deploy/configure/about-the-service-connection-point) in einem [Onlinemodus](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/) konfigurieren. Wenn Sie Ihrer Umgebung eine Verbindung hinzufügen, wird auch der Microsoft Monitoring Agent auf dem Computer installiert, auf dem die Standortsystemrolle ausgeführt wird.
- Registrieren Sie Configuration Manager als „Webanwendung und/oder Web-API”-Verwaltungstool, und rufen Sie die [Client-ID dieser Registrierung](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/) ab.
- Erstellen Sie für das registrierte Verwaltungstool in Azure Active Directory einen Clientschlüssel.
- Geben Sie der registrierten Web-App im Azure-Verwaltungsportal Zugriff auf OMS, wie unter [Provide Configuration Manager with permissions to OMS (Bereitstellen von Configuration Manager mit Berechtigungen für OMS)](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms) beschrieben.

    > [!IMPORTANT]
    > Achten Sie beim Konfigurieren der OMS-Zugriffsberechtigung darauf, dass Sie die Rolle **Mitwirkender** auswählen, und weisen Sie ihr Berechtigungen für die Ressourcengruppe der registrierten App zu.

### <a name="create-the-connection"></a>Erstellen der Verbindung

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Cloud Services** > **Upgrade Analytics Connector** (Upgrade Analytics-Connector) > **Create Connection to Upgrade Analytics** (Verbindung zu Upgrade Analytics herstellen) aus, um den **Add Upgrade Analytics Connection wizard** (Assistenten zum Hinzufügen der Upgrade Analytics-Verbindung) zu starten.
3.  Geben Sie auf dem Bildschirm **Azure Active Directory** zunächst den **Mandanten**, die **Client-ID** und den **geheimen Clientschlüssel** ein, und wählen Sie anschließend **Weiter** aus.
4.  Geben Sie auf dem Bildschirm **Upgrade Analytics** die Verbindungseinstellungen ein, indem Sie Ihr **Azure-Abonnement**, die **Azure-Ressourcengruppe** und den **Operations Management Suite-Arbeitsbereich** angeben.
5.  Überprüfen Sie die Verbindungseinstellungen auf dem Bildschirm **Zusammenfassung**, und wählen Sie dann **Weiter** aus.

    > [!NOTE]
    > Sie müssen Upgrade Analytics mit dem Standort der obersten Ebene in der Hierarchie verbinden. Wenn Sie Upgrade Analytics mit einem eigenständigen primären Standort verbinden und dann Ihrer Umgebung einen Standort der zentralen Verwaltung hinzufügen, müssen Sie die OMS-Verbindung in der neuen Hierarchie löschen und neu erstellen.

### <a name="complete-upgrade-analytics-tasks"></a>Ausführen von Upgrade Analytics-Aufgaben  

Nachdem Sie die Verbindung in Configuration Manager erstellt haben, können Sie diese Aufgaben wie unter [Get started with Upgrade Analytics (Erste Schritte mit Upgrade Analytics)](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) beschrieben, ausführen.  

1. Fügen Sie dem OMS-Arbeitsbereich den Upgrade Analytics-Dienst hinzu.  
2. Generieren Sie eine kommerzielle ID.  
3. Abonnieren Sie Upgrade Analytics.   

## <a name="use-the-upgrade-analytics-deployment-script"></a>Verwenden des Bereitstellungsskript von Upgrade Analytics  

Sie können zahlreiche Aufgaben von Upgrade Analytics über das Microsoft **Upgrade Analytics-Bereitstellungsskript** automatisieren sowie Probleme mit der Freigabe von Daten lösen.  
Das Bereitstellungsskript von Upgrade Analytics bietet folgende Möglichkeiten:  

- Legt den kommerziellen ID-Schlüssel und die Schlüssel „CommercialDataOptIn“ + „RequestAllAppraiserVersions“ fest  
- Stellt sicher, dass Computernutzer für Microsoft Daten bereitstellen können  
- Überprüft, ob für den Computer ein Neustart aussteht   
- Stellt sicher, dass die neueste Version des 10.0.x-Pakets der KB installiert ist (10.0.14348 oder nachfolgenden Versionen erforderlich)  
- Aktiviert den ausführlichen Modus zur Problembehandlung (sofern aktiviert)  
- Initiiert die Sammlung von Telemetriedaten, die Microsoft für die Bewertung der Upgradebereitschaft Ihres Unternehmens benötigt  
- Wenn aktiviert, wird der Fortschritt des Skripts in einem Cmd-Fenster angezeigt und macht dadurch Probleme sichtbar (Erfolg oder Fehler für jeden Schritt) bzw. schreibt in die Protokolldatei  
  
### <a name="to-run-the-upgrade-analytics-deployment-script"></a>So führen Sie das Upgrade Analytics-Bereitstellungsskript aus  
  
1. Laden Sie das [Upgrade Analytics-Bereitstellungsskript](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409) herunter, und extrahieren Sie die Datei „UpgradeAnalytics.zip“. Die Dateien im Ordner **Diagnostics** sind nur dann erforderlich, wenn Sie das Skript im Problembehandlungsmodus ausführen möchten.  
2. Bearbeiten Sie diese Parameter in „RunConfig.bat“:  
- Speicherort für Protokollinformationen. Beispiel: % SystemDrive%\UADiagnostics. Sie können die Protokollinformationen auf einer Remotedateifreigabe oder in einem lokalen Verzeichnis speichern. Wenn das Skript die Protokolldatei für den angegebenen Pfad nicht erstellen kann, werden die Protokolldateien auf dem Laufwerk mit dem Windows-Verzeichnis erstellt.  
- Kommerzieller ID-Schlüssel  
- Standardmäßig sendet das Skript die Protokollinformationen in die Konsole und die Protokolldatei. Verwenden Sie eine der folgenden Optionen, um das Standardverhalten zu ändern:  
    - logMode = 0 Protokoll, nur in die Konsole  
    - logMode = 1 Protokoll, in die Datei und die Konsole  
    - logMode = 2 Protokolle, nur in die Datei  
    - Setzen Sie für die Problembehandlung den Eintrag **IsVerboseLogging** auf **$true**, um Protokollinformationen zu generieren, die bei der Diagnose von Problemen hilfreich sein können. Der Eintrag **IsVerboseLogging** ist standardmäßig auf **$false** eingestellt. Vergewissern Sie sich, dass der Diagnoseordner im gleichen Verzeichnis installiert ist wie das Skript, das diesen Modus verwendet.  
    - Benachrichtigen Sie Benutzer, wenn sie ihren Computer neu starten müssen. Diese Eigenschaft ist standardmäßig nicht aktiviert.  
  
3. Nachdem Sie die Parameter in „RunConfig.bat“ bearbeitet haben, führen Sie das Skript als Administrator an.  
  
  
## <a name="view-microsoft-upgrade-analytics-properties-in-configuration-manager"></a>Anzeigen der Eigenschaften von Microsoft Upgrade Analytics in Configuration Manager  
  
1.  Navigieren Sie in der Configuration Manager-Konsole zu **Cloud Services**, und wählen Sie **OMS Connector** (OMS-Connector) aus, um die Seite **OMS Connection Properties** (OMS-Verbindungseigenschaften) zu öffnen.  

2.  Auf dieser Seite befinden sich zwei Registerkarten:
  * Die Registerkarte **Azure Active Directory** zeigt **Mandant**, **Client-ID**, **Client secret key expiration** (Ablauf des geheimen Clientschlüssels) an und ermöglicht Ihnen zu **Überprüfen**, ob **Geheimer Clientschlüssel** abgelaufen ist.
  * Die Registerkarte **Upgrade Analytics** zeigt Ihr **Azure-Abonnement**, die **Azure-Ressourcengruppe** und den **Operations Management Suite-Arbeitsbereich** an.

## <a name="view-and-use-the-upgrade-information"></a>Anzeigen und verwenden der Upgradeinformationen

Nachdem Sie Upgrade Analytics mit Configuration Manager integriert haben, können Sie die Upgradebereitschaft Ihrer Kunden anzeigen und entsprechende Maßnahmen ergreifen.

1. Wählen Sie in der Configuration Manager-Konsole die Optionen **Überwachung** > **Übersicht** > **Upgrade Analytics** aus.
2. Überprüfen Sie die Daten, einschließlich des Status der Upgradebereitschaft und des Prozentsatzes an Windows-Geräten, die Telemetriedaten melden.
3. Sie können das Dashboard zum Anzeigen von Daten für Geräte in bestimmten Sammlungen filtern.
4. Sie können Geräte in einem bestimmten Upgradebereitschaftsstatus anzeigen und eine dynamische Sammlung für sie erstellen. Wenn die Geräte dazu bereit sind, können Sie ein Upgrade ausführen oder entsprechende Maßnahmen ergreifen, um sie in den passenden Bereitschaftsstatus zu versetzen.



<!--HONumber=Dec16_HO3-->


