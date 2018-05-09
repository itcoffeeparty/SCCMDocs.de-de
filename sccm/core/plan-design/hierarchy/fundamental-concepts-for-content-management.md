---
title: Grundlagen der Inhaltsverwaltung
titleSuffix: Configuration Manager
description: Verwenden Sie Tools und Optionen in Configuration Manager, um den Inhalt zu verwalten, den Sie bereitstellen.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5dfe33e7182eae158c15afb848d3a9f1702678ba
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Grundlegende Konzepte für die Inhaltsverwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Configuration Manager unterstützt ein robustes System von Tools und Optionen zum Verwalten der Inhalte, die Sie als Anwendungen, Pakete, Softwareupdates und Betriebssysteme bereitstellen. Configuration Manager speichert den Inhalt jeweils auf Standortservern und Verteilungspunkten. Diese Inhalte erfordern bei der Übertragung zwischen den Standorten einen großen Anteil der Netzwerkbandbreite. Zur effektiven Planung und Verwendung der Inhaltsverwaltungsinfrastruktur ist es empfehlenswert, die verfügbaren Optionen und Konfigurationen zu kennen. Wägen Sie dann ab, wie Sie diese am besten an Ihre Anforderungen an die Netzwerkumgebung und die Bereitstellung von Inhalten anzupassen.  

> [!TIP]    
> Weitere Informationen über den Prozess zur Inhaltsverteilung und Hilfe zur Diagnose und Behebung von allgemeinen Problemen bei der Inhaltsverteilung finden Sie unter [Verstehen und behandeln Content-Verteilung in Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Die nachstehenden Artikeln werden als Schlüsselkonzepte für die Inhaltsverwaltung behandelt. Wenn für ein Konzept zusätzliche oder komplexe Informationen erforderlich sind, werden Links bereitgestellt, die Sie zu diesen Details leiten.



## <a name="accounts-used-for-content-management"></a>Für das Content Management verwendete Konten  
 Die folgenden Konten können mit dem Content Management verwendet werden:  

-   **Netzwerkzugriffskonto** – Wird von Clients verwendet, um die Verbindung zu einem Verteilungspunkt herzustellen und auf Inhalte zuzugreifen. Das Computerkonto wird standardmäßig zuerst ausprobiert.  

     Dieses Konto wird auch von Pullverteilungspunkten verwendet, um Inhalte von einem Quellverteilungspunkt in einer Remotegesamtstruktur herunterzuladen.  

-   **Paketzugriffskonto** – Standardmäßig gewährt Configuration Manager den generischen Zugriffskonten „Benutzer“ und „Administratoren“ Zugriff auf Inhalte auf einem Verteilungspunkt. Sie können jedoch weitere Berechtigungen konfigurieren, um den Zugriff zu beschränken.   

-   **Multicastverbindungskonto**: Wird für Betriebssystembereitstellungen verwendet.  

Weitere Informationen zu diesen Konten finden Sie unter [Verwalten von Konten für den Zugriff auf Inhalt](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).



## <a name="bandwidth-throttling-and-scheduling"></a>Zeitplanung und Einschränkung der Bandbreite  
 Sowohl Einschränkung als auch Zeitplanung sind Optionen, mit denen Sie steuern können, wann Inhalte von einem Standortserver an Verteilungspunkte verteilt werden. Diese Funktionen sind mit der Bandbreitensteuerung für dateibasierte Replikation von Standort zu Standort vergleichbar, stehen damit aber in keinem direkten Zusammenhang.  

 Weitere Informationen finden Sie unter [Verwalten der Netzwerkbandbreite für Inhalt](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="binary-differential-replication"></a>Binäre differenzielle Replikation  
 Die binäre differenzielle Replikation (BDR) ist eine Voraussetzung für Verteilungspunkte. Sie wird manchmal auch als Deltareplikation bezeichnet. Wenn Sie Updates für Inhalte verteilen, die zuvor an andere Standorte oder an Remoteverteilungspunkte verteilt wurden, wird die BDR automatisch verwendet, um die Bandbreite zu reduzieren.  

 Die BDR minimiert die Netzwerkbandbreite, die zum Senden von Updates für verteilten Inhalt verwendet wird. Sie sendet nur den neuen oder geänderten Inhalt anstatt des gesamten Inhalts der Quelldateien, wenn diese Dateien geändert werden.  

 Wenn die BDR verwendet wird, werden in Configuration Manager die Änderungen ermittelt, die an Quelldateien für jeden zuvor verteilten Inhaltssatz vorgenommen wurden.  

-   Wenn Dateien im Quellinhalt geändert werden, wird vom Standort eine neue inkrementelle Version des Inhalts erstellt. Anschließend werden nur die geänderten Dateien auf Zielstandorte und Verteilungspunkte repliziert. Eine Datei wird als geändert angesehen, wenn Sie sie umbenannt oder verschoben haben oder den Inhalt geändert haben. Wenn Sie beispielsweise eine Treiberdatei für ein Treiberpaket, das Sie zuvor an mehrere Standorte verteilt haben, ersetzen, wird nur die geänderte Treiberdatei repliziert.  

-   Von Configuration Manager werden bis zu fünf inkrementelle Versionen eines Inhaltssatzes unterstützt, bevor der gesamte Inhaltssatz erneut gesendet wird. Nach der fünften Aktualisierung führt die nächste Änderung am Inhaltssatz dazu, dass vom Standort eine neue Version des Inhaltssatzes erstellt wird. Configuration Manager verteilt dann die neue Version des Inhaltssatzes, um den früheren Satz und die inkrementellen Versionen zu ersetzen. Nach der Verteilung des neuen Inhaltssatzes werden anschließende inkrementelle Änderungen an den Quelldateien erneut durch die BDR repliziert.  

BDR wird zwischen übergeordneten und untergeordneten Standorten in einer Hierarchie unterstützt. Innerhalb eines Standorts wird BDR zwischen dem Standortserver und dessen regulären Verteilungspunkten unterstützt. Von Pullverteilungspunkten und cloudbasierten Verteilungspunkten wird jedoch die BDR zum Übertragen von Inhalten nicht unterstützt. Pullverteilungspunkte unterstützen Deltas auf Dateiebene und das Übertragen neuer Dateien, aber keine Blöcke in einer Datei.

Für Anwendungen wird immer die binäre differenzielle Replikation verwendet. Die BDR ist für Pakete optional und standardmäßig nicht aktiviert. Damit Sie die BDR für Pakete verwenden können, müssen Sie diese Funktion für jedes Paket aktivieren. Wählen Sie die Option **Binäre differenzielle Replikation aktivieren** aus, wenn Sie ein Paket erstellen oder bearbeiten.   



## <a name="branchcache"></a>BranchCache  
 [BranchCache](/windows-server/networking/branchcache/branchcache) ist eine Windows-Technologie. Clients, die BranchCache unterstützen und eine von Ihnen für Branch-Cache konfigurierte Bereitstellung heruntergeladen haben, fungieren anschließend als Inhaltsquelle für andere Clients mit aktivierter BranchCache-Funktion.  

 Sie verfügen beispielsweise über einen Verteilungspunkt, der Windows Server 2012 oder höher ausführt und als BranchCache-Sever konfiguriert ist. Wenn der erste BranchCache-fähige Client Inhalt von diesem Server anfordert, lädt er diesen Inhalt herunter und speichert ihn zwischen.  

- Dieser Clientcomputer stellt den Inhalt dann für weitere Clients mit aktivierter BranchCache-Funktion im gleichen Subnetz zur Verfügung, die den Inhalt ebenfalls zwischenspeichern.  
- Andere Clients, die sich im gleichen Subnetz befinden, müssen den Inhalt vom Verteilungspunkt nicht herunterladen.  
- Der Inhalt ist für spätere Übertragungen über mehrere Clients verteilt.  



## <a name="delivery-optimization"></a>Übermittlungsoptimierung
<!-- 1324696 -->
Sie verwenden Configuration Manager-Begrenzungsgruppen, um die Inhaltsverteilung über Ihr gesamtes Unternehmensnetzwerk und Remotebüros hinweg zu definieren und zu regulieren. [Windows-Übermittlungsoptimierung](/windows/deployment/update/waas-delivery-optimization) ist eine cloudbasierte Peer-zu-Peer-Technologie zum gemeinsamen Nutzen von Inhalten auf Windows 10-Geräten. Ab Version 1802 können Sie die Übermittlungsoptimierung so konfigurieren, dass bei der Freigabe von Inhalten für Peers Ihre Begrenzungsgruppen verwendet werden. Clienteinstellungen legen die Begrenzungsgruppen-ID als Gruppen-ID für die Übermittlungsoptimierung auf dem Client fest. Wenn der Client mit dem Übermittlungsoptimierungs-Clouddienst kommuniziert, wird diese ID zum Ermitteln von Peers verwendet, auf denen sich der gewünschte Inhalt befindet. Weitere Informationen finden Sie unter den Clienteinstellungen für die [Übermittlungsoptimierung](/sccm/core/clients/deploy/about-client-settings#delivery-optimization).



## <a name="peer-cache"></a>Peercache
Der Clientpeercache unterstützt Sie beim Verwalten von Bereitstellungen von Inhalten an Clients an Remotestandorten. Der Peercache ist eine integrierte Configuration Manager-Lösung, mit deren Hilfe Clients Inhalte für andere Clients direkt aus ihrem lokalen Cache freigeben können.

Nachdem Sie Clienteinstellungen bereitgestellt haben, die der Peercache für eine Sammlung aktivieren, können Mitglieder dieser Sammlung als Peerinhaltsquelle für andere Clients in der gleichen Begrenzungsgruppe fungieren.

Weitere Informationen finden Sie unter [Peer Cache for Configuration Manager clients (Peercache für Configuration Manager-Clients)](/sccm/core/plan-design/hierarchy/client-peer-cache).



## <a name="windows-pe-peer-cache"></a>Windows PE-Peercache
Wenn Sie ein neues Betriebssystem mit Configuration Manager bereitstellen, können Computer, die die Tasksequenz ausführen, den Windows PE-Peercache verwenden. Es wird Inhalt aus einer Peercachequelle anstatt aus einem Verteilungspunkt heruntergeladen. Auf diese Weise können Sie WAN-Datenverkehr in Zweigstellenszenarios minimieren, wenn kein lokaler Verteilungspunkt vorhanden ist.

Weitere Informationen finden Sie unter [Windows PE-Peercache](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).



## <a name="client-locations"></a>Clientstandorte  
 Clients können auf Inhalte der folgenden Standorte zugreifen:  

-   **Intranet** (lokal):  

    -   Verteilungspunkte können HTTP oder HTTPs verwenden.  

    -   Ein cloudbasierter Verteilungspunkt wird nur dann für ein Fallback verwendet, wenn keine lokalen Verteilungspunkte verfügbar sind.  

-   **Internet**:  

    -   Verteilungspunkte müssen HTTPS akzeptieren.  

    -   Ein cloudbasierter Verteilungspunkt kann für ein Fallback verwendet werden.  

-   **Arbeitsgruppe**:  

    -   Verteilungspunkte müssen HTTPS akzeptieren.  

    -   Ein cloudbasierter Verteilungspunkt kann für ein Fallback verwendet werden.  



## <a name="content-library"></a>Inhaltsbibliothek  
 Die Inhaltsbibliothek ist der Inhaltsspeicher mit einer Instanz in Configuration Manager. Durch diese Bibliothek wird die Gesamtgröße des Inhalts verringert, den Sie verteilen.  

- Weitere Informationen zur [Inhaltsbibliothek](../../../core/plan-design/hierarchy/the-content-library.md).
- Verwenden Sie das [Inhaltsbibliothek-Bereinigungstool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) für die Entfernung von Inhalt, der nicht mehr einer Anwendung zugeordnet ist.  



## <a name="distribution-points"></a>Verteilungspunkte  
 Configuration Manager verwendet Verteilungspunkte, um Dateien zu speichern, die zum Ausführen von Software auf Clientcomputern erforderlich sind. Für die Clients ist zum Herunterladen der Dateien mit den von Ihnen bereitgestellten Inhalten ein Zugriff auf mindestens einen Verteilungspunkt erforderlich.  

 Der (nicht spezialisierte) Basisverteilungspunkt wird häufig als Standardverteilungspunkt bezeichnet. Es gibt zwei Variationen auf dem Standardverteilungspunkt, die besondere Aufmerksamkeit erhalten:  

-   **Pullverteilungspunkt** – Eine Variante eines Verteilungspunkts, bei der der Verteilungspunkt Inhalt von einem anderen Verteilungspunkt (einem Quellverteilungspunkt) erhält. Dies ähnelt dem Prozess, wie Clients Inhalt von Verteilungspunkten herunterladen. Pullverteilungspunkte können Ihnen dabei helfen, Engpässe bei der Netzwerkbandbreite zu vermeiden, die auftreten, wenn der Standortserver Inhalt an jeden Verteilungspunkt direkt verteilen muss. [Verwenden eines Pullverteilungspunkts](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)

-   **Cloudbasierter Verteilungspunkt** – Eine Variante eines in Microsoft Azure installierten Verteilungspunkts. [Learn how to use a cloud-based distribution point (Verwenden eines cloudbasierten Verteilungspunkts)](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  


Standardverteilungspunkte unterstützen eine Reihe von Konfigurationen und Features:  

- Verwenden Sie Steuerelemente wie **Zeitpläne** oder **Bandbreiteneinschränkung**, um diese Übertragung zu überwachen.  
- Verwenden Sie auch andere Optionen, darunter **vorab bereitgestellten Inhalt** und **Pullverteilungspunkte**, um die Netzwerknutzung zu reduzieren und zu steuern. 
- **BranchCache**, **Peercache** und **Übermittlungsoptimierung** sind Peer-zu-Peer-Technologien, um die Netzwerkbandbreite zu reduzieren, die zur Bereitstellung von Inhalt verwendet wird.  
- Für Betriebssystembereitstellungen gibt es unterschiedliche Konfigurationen, z.B. **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** und **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**.
- Optionen für **mobile Geräte**   
  
  
Cloudbasierte und Pullverteilungspunkte unterstützen viele gleiche Konfigurationen, jede Verteilungspunktvariante weist aber spezifische Einschränkungen auf.  



## <a name="distribution-point-groups"></a>Verteilungspunktgruppen  
 Verteilungspunktgruppen sind logische Gruppierung von Verteilungspunkten, die die Inhaltsverteilung vereinfachen können.  

 Weitere Informationen finden Sie unter [Verwalten von Verteilungspunktgruppen](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).



## <a name="distribution-point-priority"></a>Verteilungspunktpriorität  
 Der Wert der Verteilungspunktpriorität basiert darauf, wie lange die Übertragung vorheriger Bereitstellungen auf diesen Verteilungspunkt gedauert hat.  

-   Dieser Wert ist selbstoptimierend. Er wird auf jedem Verteilungspunkt festgelegt, damit Configuration Manager ermöglicht wird, Inhalt schneller an mehr Verteilungspunkte zu verteilen.  

-   Wenn Sie Inhalt an mehrere Verteilungspunkte gleichzeitig oder an eine Verteilungspunktgruppe verteilen, sendet der Standort zunächst den Inhalt an den Server mit der höchsten Priorität. Anschließend wird der gleiche Inhalt an einen Verteilungspunkt mit einer niedrigeren Priorität gesendet.  

-   Mit der Priorität eines Verteilungspunkts wird die Paketverteilungspriorität nicht ersetzt. Die Paketpriorität bleibt der entscheidende Faktor, wenn der Standort unterschiedliche Inhalte sendet.  

Sie besitzen z.B. ein Paket, das über eine hohe Paketpriorität verfügt. Sie verteilen es an einen Server mit einer niedrigen Verteilungspriorität. Dieses Paket mit hoher Priorität wird immer vor einem Paket mit niedriger Priorität umgewandelt. Die Paketpriorität gilt auch, wenn der Standort Pakete mit niedriger Priorität an Server mit höheren Verteilungspunktprioritäten verteilt.

Durch die hohe Priorität eines Pakets wird sichergestellt, dass Inhalt von Configuration Manager an die Verteilungspunkte übertragen wird, bevor Pakete mit niedrigerer Priorität gesendet werden.  

> [!NOTE]  
>  Bei Pullverteilungspunkten wird das Konzept der Priorität außerdem verwendet, um die Sequenz von deren Quellverteilungspunkten zu ordnen.  
>   
>  -   Die Verteilungspunktpriorität für Inhaltsübertragungen an den Sever unterscheidet sich von der Priorität, die von Pullverteilungspunkt verwendet wird. Pullverteilungspunkte verwenden Ihre Priorität, wenn sie nach Inhalt von suchen.  
>  -   Weitere Informationen finden Sie unter [Use a pull-distribution point (Verwenden eines Verteilungspunkts)](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  



## <a name="fallback"></a>Fallback  
 In Configuration Manager-Current Branch hat sich einiges dahingehend verändert, dass Clients einen Verteilungspunkt finden, der Inhalte enthält, einschließlich Fallbacks. 

Clients, die keine Inhalte eines Verteilungspunkts finden können, der ihrer aktuellen Begrenzungsgruppe zugeordnet ist, führen einen Fallback aus, um Quellspeicherorte zu verwenden, die benachbarten Begrenzungsgruppen zugeordnet sind. Damit eine benachbarte Begrenzungsgruppe für Fallbacks verwendet werden kann, muss eine Beziehung zu der aktuellen Begrenzungsgruppe des Clients definiert sein. Diese Beziehung muss eine konfigurierte Zeitspanne enthalten. Diese Zeitspanne muss abgelaufen sein, bevor ein Client, der lokal keinen Inhalt findet, Inhaltsquellen der benachbarten Begrenzungsgruppe in seine Suche mit aufnehmen kann.

Die Konzepte der bevorzugten Verteilungspunkte werden nicht mehr verwendet, und Einstellungen für die Option **Allow fallback source locations for content** (Fallbackspeicherorte für Inhalt zulassen) sind nicht mehr verfügbar oder erzwungen.

Weitere Informationen finden Sie unter [Begrenzungsgruppen](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
Fallback settings are related to the use of **preferred distribution points** and to content source locations that are used by clients.

-   By default, clients only download content from a preferred distribution point (one that is associated with the client's boundary groups).  

-   However, when a distribution point is configured with **Allow clients to use this site system as a fallback source location for content**, that distribution point is only offered as a valid content source to any client that can't get a deployment from one of its preferred distribution points.  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="network-bandwidth"></a>Netzwerkbandbreite  
 Zum Verwalten der beim Verteilen von Inhalt verwendeten Menge an Netzwerkbandbreite stehen Ihnen die folgenden Optionen zur Verfügung:  

-   **Vorab bereitgestellter Inhalt**: Übertragung von Inhalt an einen Verteilungspunkt, ohne dass Inhalt im Netzwerk verteilt wird.  

-   **Zeitplanung und Einschränkung** – Konfigurationen, mit denen Sie steuern, wann und wie Inhalt an Verteilungspunkte verteilt wird.  

Weitere Informationen finden Sie unter [Verwalten der Netzwerkbandbreite für Inhalt](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="network-connection-speed-to-content-source"></a>Geschwindigkeit der Netzwerkverbindung zur Inhaltsquelle  
 Einige Dinge haben sich mit Configuration Manager-Current Branch dahingehend geändert, dass Clients einen Verteilungspunkt finden, der Inhalte enthält. Zu den Änderungen gehört z.B. die Netzwerkgeschwindigkeit zu einer Inhaltsquelle. 

Netzwerkgeschwindigkeiten die einen Verteilungspunkt als **Schnell** oder **Langsam** definieren, werden nicht mehr verwendet. Stattdessen wird jedes Standortsystem, das einer Begrenzungsgruppe zugeordnet ist, auf die gleiche Weise behandelt.

Weitere Informationen finden Sie unter [Begrenzungsgruppen](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
 You can configure the network connection speed of each distribution point in a boundary group:  

-   Clients use this value when they connect to the distribution point.

-   By default, the network connection speed is configured as **Fast**, but it can also be set as **Slow**.  

-   The **network connection speed**, along with the configuration of a deployment, determine if a client can download content from a distribution point when the client is in an associated boundary group  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="on-demand-content-distribution"></a>Bedarfsgesteuerte Inhaltsverteilung  
 Eine bedarfsgesteuerte Inhaltsverteilung ist eine Option für die individuelle Bereitstellung von Anwendungen und Paketen. Diese Option ermöglicht die bedarfsgesteuerte Inhaltsverteilung an bevorzugte Server.  

-   Um diese Einstellung für eine Bereitstellung zu verwenden, aktivieren Sie die Option **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen**.  

-   Wenn diese Option für eine Bereitstellung aktiviert ist und ein Client diesen Inhalt anfordert, der Inhalt aber auf keinem der bevorzugten Verteilungspunkte des Clients verfügbar ist, verteilt Configuration Manager den Inhalt automatisch an die bevorzugten Verteilungspunkte des Clients.  

-   Obwohl dies bewirkt, dass Configuration Manager den Inhalt automatisch an die bevorzugten Verteilungspunkte dieses Clients verteilt, erhält der Client den Inhalt möglicherweise von anderen Verteilungspunkten, bevor die Bereitstellung an die bevorzugten Verteilungspunkte des Clients übertragen wurden. In diesem Fall ist der Inhalt auf diesem Verteilungspunkt anschließend für den nächsten Client verfügbar, der nach der Bereitstellung sucht.  

Weitere Informationen finden Sie unter [Begrenzungsgruppen](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
If you use version 1511, 1602, or 1606, see  [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) for information about the different content location and fallback scenarios.
-->



## <a name="package-transfer-manager"></a>Paketübertragungs-Manager  
 Der Paketübertragungs-Manager ist die Standortserverkomponente, die Inhalt an Verteilungspunkte auf anderen Computern überträgt.  

 Weitere Informationen finden Sie unter [Package transfer manager (Paketübertragungs-Manager)](../../../core/plan-design/hierarchy/package-transfer-manager.md).  



<!--
## Preferred distribution point  
 A preferred distribution point includes any distribution points that are associated with a client's current boundary groups.  

 You have the option to associate each distribution point with one or more boundary groups:  

-   This association helps the client identify distribution points from which it can download content.  
-   By default, clients can only download content from a preferred distribution point.  


For more information:
 - If you use version 1610 or later, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - If you use version 1511, 1602, or 1606, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).
-->



## <a name="prestage-content"></a>Vorabbereitstellen von Inhalt  
 Das Vorabbereitstellen von Inhalt ist der Vorgang zum Übertragen von Inhalt an einen Verteilungspunkt, ohne dass der Inhalt im Netzwerk verteilt wird.  

 Weitere Informationen finden Sie unter [Verwalten der Netzwerkbandbreite für Inhalt](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
