---
title: "Grundlegende Konzepte für das Content Management | System Center Configuration Manager"
description: Verwenden Sie Tools und Optionen in System Center Configuration Manager, um den Inhalt zu verwalten, den Sie bereitstellen.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: 28
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 27342ef83d877c31f39bc232e3e19e37b78e62da


---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Grundlegende Konzepte für die Inhaltsverwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager unterstützt ein robustes System von Tools und Optionen zum Verwalten der Inhalte, die Sie als Anwendungen, Pakete, Softwareupdates und Betriebssysteme bereitstellen.  

 Die bereitgestellten Inhalte werden auf Standortservern und Verteilungspunkt-Standortsystemservern gespeichert. Diese Inhalte können bei der Übertragung zwischen den Standorten einen großen Anteil der Netzwerkbandbreite erfordern.  Zur effektiven Planung und Verwendung von Content Management-Infrastruktur müssen Sie die verfügbaren Optionen und Konfigurationen verstehen und anschließend überlegen, wie Sie diese anwenden, um die Anforderungen Ihrer Netzwerkumgebung und der Bereitstellung von Inhalten am besten zu erfüllen.  

Nachstehend finden Sie die Schlüsselkonzepte für die Inhaltsverwaltung. Wenn für ein Konzept zusätzliche oder komplexe Informationen erforderlich sind, werden Links bereitgestellt, die Sie zu diesen Details leiten.  

## <a name="accounts-used-for-content-management"></a>Für das Content Management verwendete Konten  
 Die folgenden Konten können mit dem Content Management verwendet werden:  

-   **Netzwerkzugriffskonto** – Wird von Clients verwendet, um die Verbindung zu einem Verteilungspunkt herzustellen und auf Inhalte zuzugreifen. Standardmäßig verwenden Clients zuerst das Computerkonto.  

     Dieses Konto wird auch von Pullverteilungspunkten verwendet, um Inhalte von einem Quellverteilungspunkt in einer Remotegesamtstruktur abzurufen.  

-   **Paketzugriffskonto** – Standardmäßig gewährt Configuration Manager den generischen Zugriffskonten „Benutzer“ und „Administratoren“ Zugriff auf Inhalte auf einem Verteilungspunkt. Sie können jedoch weitere Berechtigungen konfigurieren, um den Zugriff zu beschränken. Siehe &lt;Verwalten von Konten für den Zugriff auf Paketinhalte\>  

-   **Multicastverbindungskonto** – Wird für Betriebssystembereitstellungen verwendet  

Weitere Informationen zu diesen Konten finden Sie unter [Verwalten von Konten für den Zugriff auf Inhalt](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).

## <a name="bandwidth-throttling-and-scheduling"></a>Zeitplanung und Einschränkung der Bandbreite  
 Sowohl Einschränkung als auch Zeitplanung sind Optionen, mit denen Sie steuern können, wann Inhalte von einem Standortserver an Verteilungspunkte verteilt werden. Dies ist mit der Bandbreitensteuerung für dateibasierte Replikation von Standort zu Standort vergleichbar, steht damit aber in keinem direkten Zusammenhang.  

 Weitere Informationen finden Sie unter [Manage network bandwidth](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) (Verwalten der Netzwerkbandbreite).

## <a name="binary-differential-replication"></a>Binäre differenzielle Replikation  
 Bei der Verteilung von Aktualisierungen für Inhalte, die Sie zuvor an anderen Standorten oder einem Remoteverteilungspunkt bereitgestellt haben, wird zum Reduzieren der Netzwerkbandbreite automatisch eine Voraussetzung für Verteilungspunkte verwendet, die binäre differenzielle Replikation (BDR), manchmal auch als Deltareplikation bezeichnet.  

 BDR minimiert die Netzwerkbandbreite, die für das Senden von Aktualisierungen für verteilten Inhalt genutzt wird, indem bei jeder Änderung an Inhaltsquelldateien nur neuer oder geänderter Inhalt und nicht alle Dateien gesendet werden.  

 Wenn die binäre differenzielle Replikation verwendet wird, werden in Configuration Manager die Änderungen ermittelt, die an Quelldateien für jeden zuvor verteilten Inhaltssatz vorgenommen wurden.  

-   Wurden Dateien im Quellinhalt geändert, wird von Configuration Manager eine neue inkrementelle Version des Inhaltssatzes erstellt, und nur die geänderten Dateien werden an Zielstandorten und Verteilungspunkten repliziert. Eine Datei gilt als geändert, wenn sie umbenannt oder verschoben wurde oder wenn der Inhalt der Datei geändert wurde. Wenn Sie beispielsweise eine Treiberdatei für ein Bereitstellungspaket des Betriebssystems, das Sie zuvor an mehrere Standorte verteilt haben, ersetzen, wird nur die geänderte Treiberdatei an diesen Zielstandorten repliziert.  

-   Von Configuration Manager werden bis zu fünf inkrementelle Versionen eines Inhaltssatzes unterstützt, bevor der gesamte Inhaltssatz erneut gesendet wird. Nach der fünften Aktualisierung führt die nächste Änderung am Inhaltssatz dazu, dass von Configuration Manager eine neue Version des Inhaltssatzes erstellt wird. Configuration Manager verteilt dann die neue Version des Inhaltssatzes, um den früheren Satz und die inkrementellen Versionen zu ersetzen. Nach der Verteilung des neuen Inhaltssatzes werden anschließende inkrementelle Änderungen an den Quelldateien erneut durch binäre differenzielle Replikation repliziert.  


BDR wird zwischen übergeordneten und untergeordneten Standorten in einer Hierarchie unterstützt. Innerhalb eines Standorts wird BDR zwischen dem Standortserver und dessen Verteilungspunkten unterstützt. Diese Unterstützung umfasst Pullverteilungspunkte, cloudbasierte Verteilungspunkte sind jedoch ausgeschlossen. Von cloudbasierten Verteilungspunkten wird die binäre differenzielle Replikation zum Übertragen von Inhalten nicht unterstützt.  

Für Anwendungen wird immer die binäre differenzielle Replikation verwendet. Für Pakete ist die binäre differenzielle Replikation optional und standardmäßig nicht aktiviert. Sie müssen die Funktionalität für jedes Paket aktivieren, um die binäre differenzielle Replikation für Pakete zu verwenden. Wählen Sie dazu die Option **Binäre differenzielle Replikation aktivieren** aus, wenn Sie ein neues Paket erstellen oder wenn Sie die Registerkarte **Datenquelle** der Paketeigenschaften bearbeiten.  

## <a name="branchcache"></a>BranchCache  
 Eine Windows-Technologie, mit der Clients, die BranchCache unterstützen und eine für Branch-Cache konfigurierte Bereitstellung heruntergeladen haben, anschließend als Inhaltsquelle für andere Clients mit aktivierter BranchCache-Funktion fungieren können.  

 Beispiel: Auf einem Clientcomputer mit aktivierter BranchCache-Funktion wird Inhalt, der von einem Verteilungspunkt unter Windows Server 2012 zum ersten Mal heruntergeladen wird, zwischengespeichert, sofern der Verteilungspunkt als BranchCache-Server konfiguriert ist.  

-   Dieser Clientcomputer kann den Inhalt dann für weitere Clients mit aktivierter BranchCache-Funktion im gleichen Subnetz zur Verfügung stellen, die den Inhalt ebenfalls zwischenspeichern.  

-   Auf diese Weise muss der Inhalt von Clients im gleichen Subnetz später nicht erneut vom Verteilungspunkt heruntergeladen werden, da der Inhalt für spätere Übertragungen über mehrere Clients verteilt ist.  





## <a name="windows-pe-peer-cache"></a>Windows PE-Peercache
Beim Bereitstellen eines neuen Betriebssystems in System Center Configuration Manager können Computer, auf denen die Tasksequenz ausgeführt wird, Windows PE-Peercache verwenden, um Inhalte von einem lokalen Peer (einer Peercachequelle) abzurufen, anstatt sie von einem Verteilungspunkt herunterzuladen. Auf diese Weise können Sie WAN-Datenverkehr in Zweigstellenszenarios minimieren, wenn kein lokaler Verteilungspunkt vorhanden ist.

Weitere Informationen finden Sie unter [Windows PE-Peercache](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="client-locations"></a>Clientstandorte  
 Clients können auf Inhalte der folgenden Standorte zugreifen:  

-   **Intranet** (lokal):  

    -   Verteilungspunkte können HTTP oder HTTPs verwenden.  

    -   Ein cloudbasierter Verteilungspunkt wird nur dann für ein Fallback verwendet, wenn keine lokalen Verteilungspunkte verfügbar sind.  

-   **Internet** :  

    -   Verteilungspunkte müssen HTTPS akzeptieren.  

    -   Ein cloudbasierter Verteilungspunkt kann für ein Fallback verwendet werden.  

-   **Arbeitsgruppe**:  

    -   Verteilungspunkte müssen HTTPS akzeptieren.  

    -   Ein cloudbasierter Verteilungspunkt kann für ein Fallback verwendet werden.  



## <a name="content-library"></a>Inhaltsbibliothek  
 Der Einzelinstanz-Inhaltsspeicher, der von Configuration Manager verwendet wird, um die Gesamtgröße des kombinierten Inhaltstexts zu reduzieren, den Sie verteilen.  

Weitere Informationen zur [Inhaltsbibliothek](../../../core/plan-design/hierarchy/the-content-library.md)


## <a name="distribution-point"></a>Verteilungspunkt  
 Configuration Manager verwendet Verteilungspunkte, um Dateien zu speichern, die zum Ausführen von Software auf Clientcomputern erforderlich sind. Für die Clients ist zum Herunterladen der Dateien mit den von Ihnen bereitgestellten Inhalten ein Zugriff auf mindestens einen Verteilungspunkt erforderlich.  

 Der (nicht spezialisierte) Basisverteilungspunkt wird häufig als Standardverteilungspunkt bezeichnet.  Es gibt zwei Variationen auf dem Standardverteilungspunkt, die besondere Aufmerksamkeit erhalten:  

-   **Pullverteilungspunkt** – Eine Variante eines Verteilungspunkts, bei der der Verteilungspunkt Inhalt von einem anderen Verteilungspunkt (einem Quellverteilungspunkt) in ähnlicher Weise erhält, wie Clients Inhalte von Verteilungspunkten herunterladen. Pullverteilungspunkte können Ihnen dabei helfen, Engpässe bei der Netzwerkbandbreite zu vermeiden, die auftreten können, wenn der Standortserver Inhalt an jeden Verteilungspunkt direkt verteilen muss.  [Verwenden eines Pullverteilungspunkts mit System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

-   **Cloudbasierter Verteilungspunkt** – Eine Variante eines in Microsoft Azure installierten Verteilungspunkts. [Verwenden eines cloudbasierten Verteilungspunkts mit System Center Configuration Manager](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  


Standardverteilungspunkte unterstützen eine Reihe von Konfigurationen und Features, z. B. Einschränkung und Zeitplanung, PXE und Multicast oder vorab bereitgestellten Inhalt.  

-   Sie können Steuerelemente wie **Zeitpläne** oder **Bandbreiteneinschränkung** verwenden, um diese Übertragung zu überwachen.  

-   Sie können auch andere Optionen verwenden, einschließlich **vorab bereitgestellten Inhalt**, **Pullverteilungspunkte** oder die Nutzung von **BranchCache**, um die Netzwerkbandbreite zu reduzieren, die benötigt wird, wenn Inhalte bereitgestellt werden.  

-   Verteilungspunkte unterstützen verschiedene Konfigurationen wie **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** und **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** für die Bereitstellung von Betriebssystemen oder Konfigurationen zur Unterstützung von **mobilen Geräten**.  

 Cloudbasierte und Pullverteilungspunkte unterstützen viele gleiche Konfigurationen, jede Verteilungspunktvariante weist aber spezifische Einschränkungen auf.  

## <a name="distribution-point-group"></a>Verteilungspunktgruppe  
 Logische Gruppierung von Verteilungspunkten, die die Inhaltsverteilung vereinfachen kann.  

 Weitere Informationen finden Sie unter [Verwalten von Verteilungspunktgruppen](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).

## <a name="distribution-point-priority"></a>Verteilungspunktpriorität  
 Der Wert der Verteilungspunktpriorität basiert darauf, wie lange die Übertragung vorheriger Bereitstellungen auf diesen Verteilungspunkt gedauert hat.  

-   Dieser einem Verteilungspunkt zugewiesene Wert optimiert sich selbst und hilft Configuration Manager, Inhalt in kürzerer Zeit an mehr Verteilungspunkte zu übertragen.  

-   Wenn Sie Inhalt gleichzeitig an mehrere Verteilungspunkte oder an eine Verteilungspunktgruppe übertragen, wird der Inhalt von Configuration Manager an den Verteilungspunkt mit der höchsten Priorität gesendet, bevor der gleiche Inhalt an einen Verteilungspunkt mit einer niedrigeren Priorität gesendet wird.  

-   Dies ersetzt nicht die Verteilungspriorität für Pakete, die der entscheidende Faktor für die Abfolge bei der Übertragung verschiedener Verteilungen bleibt.  


**Beispiel:** Wenn Sie Inhalt mit einer hohen Verteilungspriorität an einen Verteilungspunkt mit einer niedrigen Verteilungspunktpriorität verteilen, wird dieses Paket mit hoher Verteilungspriorität immer vor Paketen mit einer niedrigeren Verteilungspriorität übertragen. Diese Verteilungspriorität gilt auch, wenn Pakete mit einer niedrigeren Verteilungspriorität an Verteilungspunkte mit höheren Verteilungspunktprioritäten verteilt werden. Durch die hohe Verteilungspriorität eines Pakets wird sichergestellt, dass Inhalt von Configuration Manager an die richtigen Verteilungspunkte übertragen wird, bevor Pakete mit niedrigerer Verteilungspriorität gesendet werden.  

> [!NOTE]  
>  Bei Pullverteilungspunkten wird das Konzept der Priorität außerdem verwendet, um die Sequenz von deren Quellverteilungspunkten zu ordnen.  
>   
>  -   Die Verteilungspunktpriorität für Inhaltsübertragungen an den Verteilungspunkt unterscheidet sich von der Priorität, die von Pullverteilungspunkten bei der Inhaltssuche auf Quellverteilungspunkten genutzt wird.  
> -   Weitere Informationen finden Sie unter [Verwenden eines Pullverteilungspunkts mit System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  


## <a name="fallback"></a>Fallback  
 Fallbackeinstellungen stehen im Zusammenhang mit der Verwendung von **bevorzugten Verteilungspunkten** und mit den von Clients verwendeten Quellspeicherorten für Inhalt.  

-   Standardmäßig laden Clients Inhalt nur von einem bevorzugten Verteilungspunkt herunter (einem den Begrenzungsgruppen des Clients zugeordneten Verteilungspunkt).  

-   Wenn für einen Verteilungspunkt jedoch die Option **Die Verwendung eines Fallbackquellpfads für den Inhalt durch Clients zulassen** aktiviert ist, können Clients diesen Verteilungspunkt nur als gültige Inhaltsquelle verwenden, die keine Bereitstellung von einem ihrer bevorzugten Verteilungspunkte abrufen können.  


Informationen zu den verschiedenen Inhaltsorten und Fallbackszenarien finden Sie unter [Szenarien für Quellspeicherorte für Inhalt](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).

## <a name="network-bandwidth"></a>Netzwerkbandbreite  
 Zum Verwalten der beim Verteilen von Inhalt verwendeten Menge an Netzwerkbandbreite stehen Ihnen die folgenden Optionen zur Verfügung:  

-   Verwenden von vorab bereitgestelltem Inhalt: Ein Vorgang der Übertragung von Inhalt an einen Verteilungspunkt, ohne dass auf Configuration Manager zurückgegriffen wird, um den Inhalt im Netzwerk zu verteilen.  

-   Verwenden von Zeitplanung und Einschränkung: Konfigurationen, mit denen Sie steuern, wann und wie Inhalt an Verteilungspunkte verteilt wird.  

Weitere Informationen finden Sie unter [Manage network bandwidth](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) (Verwalten der Netzwerkbandbreite).

## <a name="network-connection-speed-to-content-source"></a>Geschwindigkeit der Netzwerkverbindung zur Inhaltsquelle  
 Sie können die Netzwerkverbindungsgeschwindigkeit der einzelnen Verteilungspunkte in einer Begrenzungsgruppe konfigurieren:  

-   Dieser Wert wird von den Clients bei der Verbindung mit dem Verteilungspunkt verwendet.  

-   Für die Netzwerkverbindungsgeschwindigkeit ist standardmäßig die Einstellung **Schnell**festgelegt, es kann aber auch **Langsam**festgelegt werden.  

-   Anhand der **Netzwerkverbindungsgeschwindigkeit** und der Konfiguration einer Bereitstellung wird festgelegt, ob Inhalt von Verteilungspunkten heruntergeladen werden kann, wenn der betreffende Client Mitglied in einer zugeordneten Begrenzungsgruppe ist.  


Informationen zu den verschiedenen Inhaltsorten und Fallbackszenarien finden Sie unter [Szenarien für Quellspeicherorte für Inhalt](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

## <a name="on-demand-content-distribution"></a>Bedarfsgesteuerte Inhaltsverteilung  
 Eine Option, die Sie für einzelne Anwendungen und Pakete (Bereitstellungen) festlegen können, um die bedarfsgesteuerte Inhaltsverteilung an bevorzugte Verteilungspunkte zu aktivieren.  

-   Um diese Option für eine Bereitstellung zu verwenden, aktivieren Sie **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen**.  

-   Wenn diese Option für eine Bereitstellung aktiviert ist und ein Client diesen Inhalt anfordert, der Inhalt aber auf keinem der bevorzugten Verteilungspunkte des Clients verfügbar ist, verteilt Configuration Manager den Inhalt automatisch an die bevorzugten Verteilungspunkte des Clients.  

-   Obwohl dies bewirkt, dass Configuration Manager den Inhalt automatisch an die bevorzugten Verteilungspunkte dieses Clients verteilt, erhält der Client den Inhalt möglicherweise von anderen Verteilungspunkten, bevor die Bereitstellung an die bevorzugten Verteilungspunkte des Clients übertragen wurden. In diesem Fall ist der Inhalt auf diesem Verteilungspunkt anschließend für den nächsten Client verfügbar, der nach der Bereitstellung sucht.  


Informationen zu den verschiedenen Inhaltsorten und Fallbackszenarien finden Sie unter [Szenarien für Quellspeicherorte für Inhalt](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  


## <a name="package-transfer-manager"></a>Paketübertragungs-Manager  
 Die Standortserverkomponente, die Inhalt an Verteilungspunkte auf anderen Computern überträgt.  

 Weitere Informationen finden Sie unter [Paketübertragungs-Manager](../../../core/plan-design/hierarchy/package-transfer-manager.md).  

## <a name="preferred-distribution-point"></a>Bevorzugter Verteilungspunkt  
 Verteilungspunkte, die aktuellen Begrenzungsgruppen eines Clients zugeordnet sind.  

 Sie haben die Möglichkeit, jedem Verteilungspunkt einen oder mehrere Begrenzungsgruppen zuzuordnen:  

-   Diese Zuweisung hilft dem Client, die Verteilungspunkte zu erkennen, von denen er Inhalt herunterladen kann.  

-   Standardmäßig können Clients Inhalt nur von einem bevorzugten Verteilungspunkt herunterladen.  


Informationen zu den verschiedenen Inhaltsorten und Fallbackszenarien finden Sie unter [Szenarien für Quellspeicherorte für Inhalt](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

## <a name="prestage-content"></a>Vorabbereitstellen von Inhalt  
 Ein Vorgang der Übertragung von Inhalt an einen Verteilungspunkt, ohne dass auf Configuration Manager zurückgegriffen wird, um den Inhalt im Netzwerk zu verteilen.  

 Weitere Informationen finden Sie unter [Manage network bandwidth](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) (Verwalten der Netzwerkbandbreite).



<!--HONumber=Nov16_HO1-->

