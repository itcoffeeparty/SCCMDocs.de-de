---
title: "Datenübertragungen | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Configuration Manager Daten zwischen Standorten verschiebt, und wie Sie die Übertragung von Daten in Ihrem Netzwerk verwalten können."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e290a5491fbd43ddf3ca8f4cf6f122ac862103d1


---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>Datenübertragungen zwischen Standorten in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager verwendet die **dateibasierte Replikation** und die **Datenbankreplikation** zur Übertragung unterschiedlicher Informationsarten zwischen den Standorten.  Die Abschnitte in diesem Thema können Ihnen dabei helfen, zu verstehen, wie Configuration Manager Daten zwischen Standorten verschiebt und wie Sie die Übertragung dieser Daten in Ihrem Netzwerk verwalten können.  


##  <a name="a-namebkmkfileroutea-file-based-replication"></a><a name="bkmk_fileroute"></a> File-based replication  
 Mithilfe der dateibasierten Replikation werden dateibasierte Daten von Configuration Manager zwischen den Standorten in Ihrer Hierarchie übertragen. Zu diesen Daten gehört Inhalt wie Anwendungen und Pakete, die Sie für Verteilungspunkte an untergeordneten Standorten bereitstellen möchten, sowie unverarbeitete Discovery Data Records (DDRs), die zur Verarbeitung an übergeordnete Standorte übertragen werden.  

 Bei der dateibasierten Kommunikation zwischen Standorten wird das **Server Message Block** -Protokoll (SMB) über **TCP/IP-Port 445**verwendet. Sie können Konfigurationen angeben, in denen die Bandbreiteneinschränkung und der Pulsmodus zur Steuerung der im Netzwerk übertragenen Datenmenge verwendet werden, und Sie können Zeitpläne angeben, um den Zeitpunkt der Datenübertragung im Netzwerk zu steuern.  

###  <a name="a-namebkmkroutesa-file-replication-routes"></a><a name="bkmk_routes"></a> Dateireplikationsrouten  
 Die folgenden Informationen unterstützen Sie bei Konfiguration und Verwendung von Dateireplikationsrouten:  

 **Dateireplikationsroute** Von jeder Dateireplikationsroute wird ein Zielstandort identifiziert, an den dateibasierte Daten übertragen werden können. Von jedem Standort wird eine einzelne Dateireplikationsroute zu einem bestimmten Zielstandort unterstützt.  

 Configuration Manager unterstützt die folgenden Konfigurationen für Dateireplikationsrouten:  

-   **Dateireplikationskonto**: Dieses Konto wird verwendet, um eine Verbindung mit dem Zielstandort herzustellen und Daten in die **SMS_SITE**-Freigabe dieses Standorts zu schreiben. Daten, die in diese Freigabe geschrieben werden, werden am Zielstandort verarbeitet. Wenn ein Standort der Hierarchie hinzugefügt wird, wird das Computerkonto des Standortservers am neuen Standort von Configuration Manager als **Dateireplikationskonto** dieses Standorts zugewiesen. Dieses Konto wird dann der Gruppe **SMS_SiteToSiteConnection_&lt;Standortcode\>** des Zielstandorts hinzugefügt. Bei dieser Gruppe handelt es sich um eine lokale Gruppe auf dem Computer, die den Zugriff auf die Freigabe **SMS_SITE** ermöglicht. Sie können dieses Konto in ein Windows-Benutzerkonto ändern. Wenn Sie das Konto ändern, achten Sie darauf, das neue Konto der Gruppe **SMS_SiteToSiteConnection_&lt;Standortcode\>** des Zielstandorts hinzuzufügen.  

    > [!NOTE]  
    >  An sekundären Standorten wird stets das Computerkonto des sekundären Standortservers als **Dateireplikationskonto**verwendet.  

-   **Zeitplan**: Sie können den Zeitplan für jede Dateireplikationsroute so konfigurieren, dass der Datentyp und der Zeitpunkt der Datenübertragung an den Zielstandort eingeschränkt werden.  

-   **Begrenzung der Datenübertragungsrate**: Sie können eine Begrenzung der Datenübertragungsrate für jede Dateireplikationsroute konfigurieren, um die bei der Datenübertragung an den Zielstandort in Anspruch genommene Netzwerkbandbreite zu steuern:  

    -   Verwenden Sie den **Pulsmodus** , um die Größe der Datenblöcke anzugeben, die an den Zielstandort gesendet werden. Sie können auch eine zeitliche Verzögerung zwischen dem Senden der einzelnen Datenblöcke angeben. Wählen Sie diese Option aus, wenn Sie Daten über Netzwerke mit sehr niedriger Bandbreite an den Zielstandort senden müssen. Dies kann beispielsweise der Fall sein, wenn eine Beschränkung vorliegt, dass unabhängig von der Geschwindigkeit der Verknüpfung oder deren Auslastung zu einem bestimmten Zeitpunkt nur alle fünf Sekunden 1 KB Daten gesendet werden dürfen und nicht alle drei Sekunden.  

    -   Wählen Sie das Optionsfeld **Begrenzt auf angegebene maximale Übertragungsraten pro Stunde** aus, damit die Datenübertragung an den Zielstandort nur in dem von Ihnen angegebenen Zeitanteil erfolgt. Wenn Sie diese Option verwenden, ermittelt Configuration Manager nicht die verfügbare Netzwerkbandbreite. Stattdessen wird die Zeit, innerhalb derer Daten gesendet werden können, in Blöcke aufgeteilt. Die Daten werden dann innerhalb eines kurzen Zeitblocks gesendet. In den darauffolgenden Zeitblöcken werden keine Daten gesendet. Wenn die Höchstrate beispielsweise auf **50 %**festgelegt ist, überträgt Configuration Manager die Daten für eine bestimmte Dauer, und für eine ebenso lange Dauer werden anschließend keine Daten übertragen. Die tatsächliche Datenmenge bzw. die Größe der Datenblöcke wird nicht verwaltet. Stattdessen wird nur die Dauer der Datenübertragung verwaltet.  

        > [!CAUTION]  
        >  Von einem Standort können standardmäßig bis zu 3 gleichzeitige Sendevorgänge **** zur Datenübertragung an einen Zielstandort verwendet werden. Wenn Sie für eine Dateireplikationsroute die Begrenzung der Datenübertragungsrate aktivieren, ist die Anzahl gleichzeitiger Sendevorgänge **** an den entsprechenden Standort auf 1 begrenzt. Dies gilt auch dann, wenn für die Option **Verfügbare Bandbreite beschränken (%)** der Wert **100 %**festgelegt ist. Wenn Sie beispielsweise für den Sender die Standardeinstellungen verwenden, wird hierdurch die Übertragungsrate an den Zielstandort auf ein Drittel der Standardkapazität reduziert.  

-   Sie können eine Dateireplikationsroute zwischen zwei sekundären Standorten zum Weiterleiten dateibasierten Inhalts zwischen diesen Standorten konfigurieren.  

Zur Verwaltung einer Dateireplikationsroute erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Hierarchiekonfiguration** und wählen **Dateireplikation**aus.  

**Sender_** An jedem Standort ist ein Sender verfügbar. Von diesem Sender wird die Netzwerkverbindung von einem Standort zu einem Zielstandort verwaltet. Der Sender kann auch verwendet werden, um Verbindungen zu mehreren Standorten gleichzeitig herzustellen. Zum Herstellen einer Verbindung mit einem Standort wird vom Sender mithilfe der Dateireplikationsroute zum Standort das Konto identifiziert, über das die Verbindungsherstellung erfolgt. Dieses Konto wird vom Sender auch dazu verwendet, Daten in die **SMS_SITE**-Freigabe des Zielstandorts zu schreiben.  

 Vom Sender werden Daten standardmäßig mithilfe von gleichzeitigen Sendevorgängen, die in der Regel als **Thread**bezeichnet werden, in den Zielstandort geschrieben. Von jedem gleichzeitigen Sendevorgang oder Thread kann ein anderes dateibasiertes Objekt an den Zielstandort übertragen werden. Nachdem der Sendevorgang für ein Objekt gestartet wurde, werden vom Sender standardmäßig so lange Datenblöcke für dieses Objekt geschrieben, bis die Übertragung des gesamten Objekts abgeschlossen ist. Anschließend kann der Sendevorgang oder Thread für ein weiteres Objekt gestartet werden.  

 Sie können die folgenden Einstellungen für einen Sender konfigurieren:  

-   **Maximale Anzahl gleichzeitiger Sendevorgänge**: Standardmäßig ist jeder Standort für fünf gleichzeitige Sendevorgänge ****konfiguriert, wobei drei dieser Sendevorgänge zur Datenübertragung an einen beliebigen Zielstandort verfügbar sind. Wenn Sie diese Anzahl erhöhen, nimmt der Datendurchsatz zwischen Standorten zu, da von Configuration Manager mehr Dateien gleichzeitig übertragen werden können. Die Erhöhung dieser Anzahl bedeutet auch höhere Anforderungen an die Netzwerkbandbreite zwischen Standorten.  

-   **Wiederholungseinstellungen**: Standardmäßig wird die Herstellung einer problematischen Verbindung zweimal im Abstand von einer Minute an jedem Standort versucht. Sie können sowohl die Anzahl der Verbindungsversuche als auch deren Abstand ändern.  

Zur Verwaltung des Senders eines Standorts erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Standortkonfiguration** . Erweitern Sie dann den Knoten **Standorte** , und klicken Sie auf die **Eigenschaften** des zu verwaltenden Standorts. Klicken Sie auf die Registerkarte **Sender** , um die Senderkonfiguration zu ändern.  

##  <a name="a-namebkmkdbrepa-database-replication"></a><a name="bkmk_dbrep"></a> Database replication  
SQL Server wird von der Configuration Manager-Datenbankreplikation dazu verwendet, Daten zu übertragen und an Standortdatenbanken ausgeführte Änderungen mit den Informationen in den Datenbanken anderer Standorte in der Hierarchie zusammenzuführen.  

-   So können an allen Standorten die gleichen Informationen gemeinsam verwendet werden.  

-   Wenn Sie einen Standort in einer Hierarchie installieren, wird automatisch eine Datenbankreplikation zwischen dem neuen Standort und dem vorgesehenen übergeordneten Standort konfiguriert.  

-   Nach Abschluss der Standortinstallation wird die Datenbankreplikation automatisch gestartet.  

Wenn Sie einer Hierarchie einen neuen Standort hinzufügen, wird an diesem neuen Standort eine generische Datenbank von Configuration Manager erstellt. Anschließend wird ein Snapshot der relevanten Daten in der Datenbank des übergeordneten Standorts erstellt und mithilfe dateibasierter Replikation an den neuen Standort übertragen. Mithilfe von BCP, eines Massenkopierprogramms für SQL Server, werden die Informationen dann in die lokale Kopie der Configuration Manager-Datenbank am neuen Standort geladen. Nach dem Laden des Snapshots wird an jedem Standort eine Datenbankreplikation mit dem anderen Standort ausgeführt.  

Daten werden von Configuration Manager mithilfe eines Datenbankreplikationsdienstes zwischen Standorten repliziert. Hierbei kommen die Änderungsnachverfolgung von SQL Server, mit der die lokale Standortdatenbank auf Änderungen hin überwacht wird, und ein **SQL Server Service Broker**, mit dem alle Änderungen auf andere Standorte repliziert werden, zum Einsatz. Für diesen Prozess wird standardmäßig **TCP/IP-Port 4022**verwendet.  

Daten, die mithilfe der Datenbankreplikation repliziert werden, werden von Configuration Manager in verschiedene Replikationsgruppen unterteilt.  

-   Für jede Replikationsgruppe gibt es einen separaten, festen Replikationszeitplan, aus dem hervorgeht, wie häufig Änderungen an den Daten in der Gruppe an andere Standorte repliziert werden.  

     Beispielsweise wird eine Konfigurationsänderung an der rollenbasierten Verwaltung rasch auf andere Standorte repliziert, um zu gewährleisten, dass diese Änderung so schnell wie möglich erzwungen wird. Bei Konfigurationsänderungen mit niedrigerer Priorität, beispielsweise Anforderungen zur Installation eines neuen sekundären Standorts, werden nachrangiger repliziert, und es kann einige Minuten dauern, bis eine solche Anforderung am primären Zielstandort angekommen ist.  

-   Sie können Folgendes für die Datenbankreplikation ändern:  

    -   **Datenbankreplikationslinks** ermöglichen es Ihnen, den Zeitpunkt des Datenverkehrs im Netzwerk gezielt zu steuern.  

    -   **Verteilte Ansichten** sind eine Konfiguration für Replikationslinks, die es ermöglicht, am Standort der zentralen Verwaltung einen direkten Zugriff auf ausgewählte Standortdaten in der Datenbank eines untergeordneten primären Standorts anzufordern.  

    -   Mit**Zeitplänen** können Sie den Zeitpunkt der Verwendung eines Replikationslink konfigurieren und festlegen, wann verschiedene Arten von Standortdaten repliziert werden.  

    -   Eine**Zusammenfassung** von Daten zum Netzwerkverkehr über Replikationslinks erfolgt standardmäßig alle 15 Minuten und wird in Berichten für die Datenbankreplikation verwendet.  

    -   **Schwellenwerte für die Datenbankreplikation** definieren, wann Links als heruntergestuft oder fehlgeschlagen gemeldet werden. Sie können auch festlegen, wann von Configuration Manager Warnungen zu Replikationslinks mit dem heruntergestuften oder fehlerhaften Status ausgelöst werden.  

Configuration Manager klassifiziert die Daten, die repliziert werden, entweder als globale Daten oder als Standortdaten über die Datenbankreplikation. Im Rahmen der Datenbankreplikation werden Änderungen an globalen Daten und Standortdaten über den Datenbankreplikationslink übertragen. Globale Daten können sowohl an einen übergeordneten als auch an einen untergeordneten Standort repliziert werden. Standortdaten werden nur an einen übergeordneten Standort repliziert. Die sogenannten lokalen Daten als dritter Datentyp werden nicht auf andere Standorte repliziert. Lokale Daten enthalten Informationen, die für andere Standorte nicht erforderlich sind:  

-   **Globale Daten**: Als globale Daten werden Objekte bezeichnet, die von Administratoren erstellt wurden und die an alle Standorte innerhalb der Hierarchie repliziert werden, wobei sekundäre Standorte nur eine Untergruppe globaler Daten wie beispielsweise globale Proxydaten erhalten. Zu den globalen Daten werden beispielsweise Softwarebereitstellungen, Softwareupdates, Sammlungsdefinitionen und rollenbasierte Verwaltungssicherheitsbereiche gezählt. Administratoren können globale Daten an Standorten der zentralen Verwaltung und an primären Standorten erstellen.  

-   **Standortdaten**: Als Standortdaten werden Betriebsinformationen bezeichnet, die von primären Configuration Manager-Standorten und den Clients, die primären Standorten unterstellt sind, erstellt werden. Standortdaten werden am Standort der zentralen Verwaltung repliziert, jedoch nicht an anderen Standorten. Zu den Standortdaten werden beispielsweise Hardwareinventurdaten, Statusmeldungen, Warnungen und die Ergebnisse von abfragebasierten Sammlungen gezählt. Standortdaten können nur am Standort der zentralen Verwaltung und an dem primären Standort, von dem sie stammen, angezeigt werden. Standardortdaten können nur an dem primären Standort geändert werden, an dem sie erstellt wurden.  

     Alle Standortdaten werden am Standort der zentralen Verwaltung repliziert. Aus diesem Grund können die Verwaltung und Berichterstattung für die gesamte Hierarchie vom Standort der zentralen Verwaltung ausgeführt werden.  

In den folgenden Abschnitten sind Konfigurationen beschrieben, die Sie zum Verwalten der Datenbankreplikation vornehmen können.  

###  <a name="a-namebkmkdblinksa-database-replication-links"></a><a name="bkmk_Dblinks"></a> Datenbankreplikationslinks  
Wenn Sie in einer Hierarchie einen neuen Standort installieren, wird von Configuration Manager ein Datenbankreplikationslink zwischen den beiden Standorten erstellt. Der neue Standort und der übergeordnete Standort werden durch einen einzelnen neu erstellten Link miteinander verbunden.  

Jeder Datenbankreplikationslink unterstützt Konfigurationen, mit denen die Datenübertragung über den Replikationslink gesteuert werden kann. Von jedem Replikationslink werden separate Konfigurationen unterstützt. Die Steuerelemente für Datenbankreplikationslinks umfassen Folgendes:  

-   Verwenden Sie verteilte Ansichten, um die Replikation ausgewählter Standortdaten von einem primären Standort zum Standort der zentralen Verwaltung zu beenden und es Letzterem zu ermöglichen, direkt auf diese Daten in der Datenbank des primären Standorts zuzugreifen.  

-   Legen Sie in einem Zeitplan fest, wann ausgewählte Standortdaten von einem untergeordneten primären Standort zum Standort der zentralen Verwaltung übertragen werden.  

-   Legen Sie fest, wann sich ein Datenbankreplikationslink im Status Heruntergestuft oder Fehler befindet.  

-   Geben Sie an, wann Warnungen zu einem fehlgeschlagenen Replikationslink ausgelöst werden sollen.  

-   Geben Sie an, wie häufig Daten zum Replikationsverkehr, der über den Replikationslink abgewickelt wird, von Configuration Manager zusammengefasst werden. Diese Daten werden in Berichten verwendet.  

Zum Konfigurieren eines Datenbankreplikationslinks müssen Sie die Eigenschaften des Links in der Configuration Manager-Konsole im Knoten **Datenbankreplikation** bearbeiten. Dieser Knoten wird sowohl im Arbeitsbereich **Überwachung** als auch unter dem Knoten **Hierarchiekonfiguration** des Arbeitsbereichs **Verwaltung** angezeigt. Sie können einen Replikationslink entweder am übergeordneten Standort oder am untergeordneten Standort des Replikationslinks bearbeiten.  

> [!TIP]  
>  Sie können Datenbankreplikationslinks über den Knoten **Datenbankreplikation** in beiden Arbeitsbereichen bearbeiten. Wenn Sie aber den Knoten **Datenbankreplikation** im Arbeitsbereich **Überwachung** verwenden, können Sie auch den Status der Datenbankreplikation für Replikationslinks anzeigen. Außerdem haben Sie Zugriff auf die Replikationslinkanalyse, mit der Sie Probleme bei der Datenbankreplikation untersuchen können.  

Informationen zum Konfigurieren von Replikationslinks finden Sie unter [Steuerelemente für die Replikation von Standortdatenbanken](#BKMK_DBRepControls). Weitere Informationen zur Überwachung der Replikation finden Sie im Abschnitt [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) des Themas [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) .  

Verwenden Sie die Informationen in den folgenden Abschnitten, um Datenbankreplikationslinks zu planen.  

###  <a name="a-namebkmkdistviewsa-distributed-views"></a><a name="bkmk_distviews"></a> Verteilte Ansichten  
Bei Verwendung verteilter Ansichten ist es möglich, am Standort der zentralen Verwaltung einen direkten Zugriff auf ausgewählte Standortdaten in der Datenbank eines untergeordneten primären Standorts anzufordern. Da ein direkter Zugriff gewährt wird, ist es nicht mehr erforderlich, diese Standortdaten vom primären Standort an den Standort der zentralen Verwaltung zu replizieren. Sie können verteilte Ansichten nur auf den von Ihnen ausgewählten Replikationslinks aktivieren, da Replikationslinks voneinander unabhängig sind. Verteilte Ansichten zwischen einem primären und einem sekundären Standort werden nicht unterstützt.  

Aus verteilten Ansichten ergeben sich die folgenden Vorteile:  

-   Verringerung der CPU-Last bei der Verarbeitung von Datenbankänderungen am Standort der zentralen Verwaltung und an primären Standorten  

-   Verringerung der Datenmengen, die über das Netzwerk an den Standort der zentralen Verwaltung übertragen werden  

-   Verbesserung der Leistung der SQL Server-Instanz, auf dem die Datenbank des Standorts der zentralen Verwaltung gehostet wird  

-   Verringerung des Speicherplatzes, der von der Datenbank am Standort der zentralen Verwaltung in Anspruch genommen wird  

Die Verwendung verteilter Ansichten bietet sich an, wenn sich ein primärer Standort im Netzwerk in der Nähe des Standorts der zentralen Verwaltung befindet und beide Standorte stets aktiviert und verbunden sind. Der Grund hierfür ist, dass die Replikation ausgewählter Daten zwischen den Standorten dank der verteilten Ansichten durch direkte Verbindungen zwischen den SQL Server-Instanzen an beiden Standorten ersetzt wird. Diese direkte Verbindung wird jedes Mal hergestellt, wenn diese Daten am Standort der zentralen Verwaltung angefordert werden. Daten, die Sie für verteilte Ansichten aktivieren, werden in der Regel angefordert, wenn Sie Berichte oder Abfragen ausführen bzw. Informationen im Ressourcen-Explorer anzeigen. Daten werden auch bei der Auswertung von Sammlungen angefordert, die auf den Standortdaten beruhende Regeln umfassen.  

Verteilte Ansichten sind standardmäßig für alle Replikationslinks deaktiviert. Bei der Aktivierung verteilter Ansichten für einen Replikationslink wählen Sie Standortdaten aus, die nicht über diesen Link an den Standort der zentralen Verwaltung repliziert werden. Gleichzeitig ermöglichen Sie es dem Standort der zentralen Verwaltung, direkt auf diese Daten in der Datenbank des untergeordneten primären Standorts zuzugreifen, der mit diesem Link verbunden ist. Sie können die folgenden Arten von Standortdaten für verteilte Ansichten konfigurieren:  

-   Hardwareinventurdaten von Clients  

-   Softwareinventurdaten und Softwaremessungsdaten von Clients  

-   Statusmeldungen von Clients, vom primären Standort und von allen sekundären Standorten  

Verteilte Ansichten sind für Administratoren, die Daten in der Configuration Manager-Konsole oder in Berichten anzeigen, nicht sichtbar. Wenn Daten angefordert werden, die für verteilte Ansichten aktiviert sind, wird von der SQL Server-Instanz, auf der die Datenbank für den Standort der zentralen Verwaltung gehostet wird, direkt auf die SQL Server-Instanz am untergeordneten primären Standort zugegriffen, um die gewünschten Informationen abzurufen. Angenommen, Sie fordern am Standort der zentralen Verwaltung über eine Configuration Manager-Konsole Hardwareinventurinformationen von zwei Standorten an, und nur an einem der Standorte ist die Hardwareinventur für eine verteilte Ansicht aktiviert. Die Inventurinformationen für Clients an dem Standort, der nicht für verteilte Ansichten konfiguriert ist, werden aus der Datenbank am Standort der zentralen Verwaltung abgerufen. Die Inventurinformationen für Clients an dem Standort, der für verteilte Ansichten konfiguriert ist, werden aus der Datenbank am untergeordneten primären Standort abgerufen. Diese Informationen werden in der Configuration Manager-Konsole bzw. in einem Bericht ohne Hinweise auf die Quelle angezeigt.  

Solange bei einem Replikationslink ein Datentyp für verteilte Ansichten aktiviert ist, werden diese Daten nicht vom untergeordneten primären Standort an den Standort der zentralen Verwaltung repliziert. Sobald verteilte Ansichten für einen Datentyp deaktiviert werden, wird die Replikation dieser Daten vom untergeordneten primären Standort an den Standort der zentralen Verwaltung im Rahmen der normalen Datenreplikation wiederaufgenommen. Allerdings müssen die Replikationsgruppen, die diese Daten enthalten, zwischen dem primären Standort und dem Standort der zentralen Verwaltung neu initialisiert werden, damit diese Daten am Standort der zentralen Verwaltung verfügbar sind. Nach der Deinstallation eines primären Standorts mit aktivierten verteilten Ansichten müssen die Daten des Standorts der zentralen Verwaltung neu initialisiert werden, damit Sie auf Daten zugreifen können, die am Standort der zentralen Verwaltung für verteilte Ansichten aktiviert waren.  

> [!IMPORTANT]  
>  Wenn Sie auf einem Replikationslink in der Hierarchie verteilte Ansichten verwenden, müssen Sie die verteilten Ansichten aller Replikationslinks deaktivieren, bevor Sie einen primären Standort deinstallieren. Weitere Informationen finden Sie unter [Uninstall a primary site that is configured with distributed views](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews).  

**Voraussetzungen und Einschränkungen für verteilte Ansichten:**  

-   Verteilte Ansichten werden nur auf Replikationslinks zwischen einem Standort der zentralen Verwaltung und einem primären Standort unterstützt.  

-  Der Standort der zentralen Verwaltung muss eine Enterprise Edition von SQL Server verwenden. Der primäre Standort verfügt nicht über diese Anforderung.

-   Am Standort der zentralen Verwaltung darf nur eine Instanz des SMS-Anbieters installiert sein, und diese Instanz muss sich auf dem Standortdatenbankserver befinden. Dies ist zur Unterstützung der Kerberos-Authentifizierung erforderlich, durch die es dem SQL Server am Standort der zentralen Verwaltung ermöglicht wird, auf den SQL Server am untergeordneten primären Standort zuzugreifen. Für den SMS-Anbieter am untergeordneten primären Standort gelten keine Einschränkungen.  

-   Am Standort der zentralen Verwaltung darf nur ein SQL Server Reporting Services-Punkt installiert sein, und dieser Punkt muss sich auf dem Standortdatenbankserver befinden. Dies ist zur Unterstützung der Kerberos-Authentifizierung erforderlich, durch die es dem SQL Server am Standort der zentralen Verwaltung ermöglicht wird, auf den SQL Server am untergeordneten primären Standort zuzugreifen.  

-   Die Standortdatenbank darf nicht auf einem SQL Server-Cluster gehostet werden.  

-   Die Standortdatenbank darf nicht auf einer SQL Server-AlwaysOn-Verfügbarkeitsgruppe gehostet werden.  

-   Für das Computerkonto des Datenbankservers am Standort der zentralen Verwaltung sind **Read** -Berechtigungen für die Standortdatenbank des primären Standorts erforderlich.  

> [!IMPORTANT]  
>  Bei einem Datenbankreplikationslink schließen verteilte Ansichten und Zeitpläne für die Datenreplikation einander aus.  

###  <a name="a-namebkmkschedulesa-schedule-transfers-of-site-data-on-database-replication-links"></a><a name="BKMK_schedules"></a> Geplante Übertragung von Standortdaten auf Datenbankreplikationslinks  
Sie können einen Zeitplan aufstellen, aus dem hervorgeht, wann ein Replikationslink verwendet wird und wann verschiedene Arten von Standortdaten repliziert werden. Auf diese Weise können Sie die Netzwerkbandbreite steuern, die beim Replizieren von Standortdaten von einem untergeordneten primären Standort an den entsprechenden Standort der zentralen Verwaltung in Anspruch genommen wird. Sie können festlegen, wann Statusmeldungen, Inventurdaten und Messungsdaten vom primären Standort repliziert werden. Zeitpläne für Standortdaten werden von Datenbankreplikationslinks sekundärer Standorte nicht unterstützt. Für die Übertragung globaler Daten kann kein Zeitplan festgelegt werden.  

Beim Festlegen eines Zeitplans für einen Datenbankreplikationslink können Sie die Übertragung ausgewählter Standortdaten vom primären Standort zum Standort der zentralen Verwaltung einschränken und unterschiedliche Zeiten für die Replikation unterschiedlicher Arten von Standortdaten konfigurieren.  

> [!IMPORTANT]  
>  Bei einem Datenbankreplikationslink schließen verteilte Ansichten und Zeitpläne für die Datenreplikation einander aus.  

###  <a name="a-namebkmksummarizedbreplicationa-summarization-of-database-replication-traffic"></a><a name="BKMK_SummarizeDBReplication"></a> Zusammenfassung des Datenbankreplikationsverkehrs  
Daten zum Netzwerkverkehr, der über die Datenbankreplikationslinks der Standorte abgewickelt wird, werden von jedem Standort regelmäßig zusammengefasst. Diese zusammengefassten Daten fließen in Berichte über die Datenbankreplikation ein. Der der über einen Replikationslink abgewickelte Netzwerkverkehr wird von beiden Standorten des Replikationslinks zusammengefasst. Die Datenzusammenfassung wird vom SQL Server ausgeführt, auf dem die Standortdatenbank gehostet wird. Nach der Datenzusammenfassung werden diese Informationen als globale Daten an andere Standorte repliziert.  

Die Zusammenfassung erfolgt standardmäßig alle 15 Minuten. Sie können die Häufigkeit, mit der der Netzwerkverkehr zusammengefasst wird, ändern. Bearbeiten Sie dazu das **Zusammenfassungsintervall** in den Eigenschaften des Datenbankreplikationslinks. Die Häufigkeit der Zusammenfassung wirkt sich auf die Informationen aus, die Sie in Berichten über die Datenbankreplikation sehen. Dieses Intervall kann auf 5 bis 60 Minuten eingestellt werden. Wenn Sie die Häufigkeit der Zusammenfassung erhöhen, steigern Sie die Verarbeitungslast des SQL Servers an jedem Standort des Replikationslinks.  

###  <a name="a-namebkmkdbrepthresholdsa-database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a> Schwellenwerte für die Datenbankreplikation  
Mit Schwellenwerten für die Datenbankreplikation wird bestimmt, wann ein Datenbankreplikationslink als heruntergestuft oder fehlerhaft gemeldet wird. Ein Link gilt standardmäßig als heruntergestuft, wenn bei 12 aufeinanderfolgenden Replikationsversuchen einer Replikationsgruppe ein Fehler auftritt. Bleiben 24 aufeinanderfolgende Versuche einer Replikationsgruppe erfolglos, wird dem Link der Status Fehler zugewiesen.  

Sie können durch benutzerdefinierte Werte bestimmen, wann ein Replikationslink von Configuration Manager als heruntergestuft oder fehlerhaft gemeldet wird. Durch Festlegen des Zeitpunkts, zu dem der Status der einzelnen Datenreplikationslinks von Configuration Manager gemeldet wird, können Sie die Integrität der Datenbankreplikation über diese Links genauer überwachen.  

Es kann vorkommen, dass einige Replikationsgruppen nicht repliziert werden können, während die Replikation anderer Replikationsgruppen weiterhin erfolgreich ist. Planen Sie daher, den Replikationsstatus eines Replikationslinks zu prüfen, wenn er zum ersten Mal als heruntergestuft gemeldet wird. Wenn bei bestimmten Replikationsgruppen wiederholt Verzögerungen auftreten, die kein Problem darstellen, oder wenn für die Netzwerkverbindung zwischen Standorten nur eine geringe Bandbreite verfügbar ist, erwägen Sie, den Wiederholungswert für den heruntergestuften oder fehlerhaften Status des Links zu ändern. Wenn Sie die Anzahl der Wiederholungen erhöhen, nach denen der Link als heruntergestuft oder fehlerhaft gilt, können Sie falsche Warnungen für bekannte Probleme verhindern und den Linkstatus genauer nachverfolgen.  

Sie müssen auch das Synchronisierungsintervall jeder Replikationsgruppe betrachten, um zu verstehen, wie häufig diese Gruppe repliziert wird. Im Knoten **Datenbankreplikation** des Arbeitsbereichs **Überwachung** können Sie das **Synchronisierungsintervall** von Replikationsgruppen auf der Registerkarte **Replikationsdetail** eines Replikationslinks anzeigen.  

Weitere Informationen zum Überwachen der Datenbankreplikation, einschließlich des Anzeigens des Replikationsstatus, finden Sie im Abschnitt [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) des Themas [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) .  

Informationen zum Konfigurieren von Schwellenwerten für die Datenbankreplikation finden Sie unter [Steuerelemente für die Replikation von Standortdatenbanken](#BKMK_DBRepControls).  

##  <a name="a-namebkmkdbrepcontrolsa-site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a> Steuerelemente für die Replikation von Standortdatenbanken  
Von jeder Standortdatenbank werden Konfigurationen unterstützt, mit denen Sie die für die Datenbankreplikation verwendete Netzwerkbandbreite steuern können. Diese Konfigurationen gelten nur für die Standortdatenbank, für die Sie die Einstellungen konfigurieren. Sie werden stets eingesetzt, wenn Daten im Rahmen einer Datenbankreplikation vom jeweiligen Standort an einen anderen Standort repliziert werden.  

Folgende Replikationssteuerelemente sind für Standortdatenbanken verfügbar:  

-   Ändern Sie den Port, der von Configuration Manager für den SQL Server Service Broker verwendet wird.  

-   Konfigurieren Sie den Zeitraum, nach dessen Ablauf der Standort aufgrund von Replikationsfehlern dazu veranlasst wird, seine Kopie der Standortdatenbank neu zu konfigurieren.  

-   Konfigurieren Sie eine Standortdatenbank so, dass die von ihr bei der Datenbankreplikation replizierten Daten komprimiert werden. Die Daten werden nur für die Übertragung zwischen Standorten komprimiert, nicht aber für die Speicherung in den Standortdatenbanken der Standorte.  

Zum Konfigurieren der Replikationssteuerelemente für eine Standortdatenbank müssen Sie die Eigenschaften der Standortdatenbank in der Configuration Manager-Konsole über den Knoten **Datenbankreplikation** bearbeiten. Dieser Knoten befindet sich unter dem Knoten **Hierarchiekonfiguration** der Arbeitsbereiche **Verwaltung** und **Überwachung**. Zur Bearbeitung der Eigenschaften der Standortdatenbank wählen Sie den Replikationslink zwischen den Standorten aus und öffnen dann entweder **Eigenschaften der übergeordneten Datenbank** oder **Eigenschaften der untergeordneten Datenbank**.  

> [!TIP]  
>  In beiden Arbeitsbereichen können Sie Steuerelemente für die Datenbankreplikation über den Knoten **Datenbankreplikation** konfigurieren. Wenn Sie aber den Knoten **Datenbankreplikation** im Arbeitsbereich **Überwachung** verwenden, können Sie auch den Status der Datenbankreplikation für einen Replikationslink anzeigen. Außerdem haben Sie Zugriff auf die Replikationslinkanalyse, mit der Sie Probleme bei der Replikation untersuchen können.  



<!--HONumber=Dec16_HO3-->


