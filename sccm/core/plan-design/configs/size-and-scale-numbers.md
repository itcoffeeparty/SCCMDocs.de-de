---
title: Anpassen und Skalieren
titleSuffix: Configuration Manager
description: Ermitteln Sie die Anzahl der Standortsystemrollen und Standorte, die für die Unterstützung von Geräten in Ihrer Umgebung notwendig sind.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b995687e330fe4beca26da83ee29ddc504c38e3a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Größe und Skalierung von Zahlen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*



Jede Bereitstellung von Configuration Manager hat eine maximal zulässige Anzahl von Standorten, Standortsystemrollen und Geräten, die unterstützt werden können. Diese Zahlen sind von Ihrer Hierarchiestruktur (welche Typen und welche Anzahl von Standorten Sie verwenden) und den Standortsystemrollen abhängig, die Sie bereitstellen. Die Informationen in diesem Artikel unterstützen Sie dabei, die Anzahl von Standortsystemrollen und Standorten zu ermitteln, die für die Unterstützung der Geräte notwendig sind, die voraussichtlich verwaltet werden sollen.

Verwenden Sie die Informationen in diesem Thema zusammen mit den Informationen in den folgenden Artikeln:
-   [Empfohlene Hardware](../../../core/plan-design/configs/recommended-hardware.md)
-   [Unterstützte Betriebssysteme für Standortsystemserver](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Unterstützte Betriebssysteme für Clients und Geräte](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Voraussetzungen für Standorte und Standortsysteme](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)


Bei den hier genannten unterstützten Zahlen wird davon ausgegangen, dass die empfohlene Hardware für Configuration Manager verwendet wird. Außerdem basieren sie auf den Standardeinstellungen für alle verfügbaren Configuration Manager-Features. Wenn Sie die empfohlene Hardware nicht verwenden oder strengere benutzerdefinierte Einstellungen festgelegt haben, kann die Leistung von Standortsystemen beeinträchtigt werden. Die Standortsysteme erfüllen möglicherweise nicht den angegebenen Unterstützungsgrad. (Beispiel für strengere Clienteinstellungen: Die Hardware- oder Softwareinventur wird häufiger als die Standardeinstellung, alle sieben Tage, durchgeführt.)

##  <a name="bkmk_SiteSystemScale"></a> Standorttypen  

### <a name="central-administration-site"></a>Standort der zentralen Verwaltung  

-   Ein Standort der zentralen Verwaltung unterstützt bis zu 25 untergeordnete primäre Standorte.  


### <a name="primary-site"></a>Primärer Standort  

-   Jeder primäre Standort unterstützt bis zu 250 sekundäre Standorte.  

-   Die maximale Anzahl sekundärer Standorte pro primärem Standort wurde auf Basis von kontinuierlich verbundenen und stabilen WAN (Wide Area Network)-Verbindungen ermittelt. Für Standorte mit weniger als 500 Clients können Sie einen Verteilungspunkt anstatt eines sekundären Standorts erwägen.  

 Informationen zur Anzahl von Clients und Geräten, die von einem primären Standort unterstützt werden können, finden Sie unter [Anzahl der Clients für Standorte und Hierarchien](#bkmk_clientnumbers).  


### <a name="secondary-site"></a>Sekundärer Standort  

-   Sekundäre Standorte unterstützen keine untergeordneten Standorte.  



## <a name="bkmk_roles"></a> Standortsystemrolle    


### <a name="application-catalog-web-service-point"></a>Anwendungskatalog-Webdienstpunkt  

-   An primären Standorten können Sie mehrere Instanzen des Anwendungskatalog-Webservicepunkts installieren.  

    > [!TIP]  
    >  Es wird empfohlen, den Anwendungskatalog-Websitepunkt und den Anwendungskatalog-Webservicepunkt gemeinsam auf dem gleichen Standortsystem zu installieren, wenn die Dienste für Clients im Intranet bereitgestellt werden.  

    -   Planen Sie aus Leistungsgründen, bis zu 50.000 Clients pro Instanz zu unterstützen.  

    -   Jede Instanz dieser Standortsystemrolle unterstützt die maximale Anzahl von Clients, die von der Hierarchie unterstützt werden.  


### <a name="application-catalog-website-point"></a>Anwendungskatalog-Websitepunkt  

-   An primären Standorten können Sie mehrere Instanzen des Anwendungskatalog-Websitepunkts installieren.  

    > [!TIP]  
    >  Es wird empfohlen, den Anwendungskatalog-Websitepunkt und den Anwendungskatalog-Webservicepunkt gemeinsam auf dem gleichen Standortsystem zu installieren, wenn die Dienste für Clients im Intranet bereitgestellt werden.  

    -   Planen Sie aus Leistungsgründen, bis zu 50.000 Clients pro Instanz zu unterstützen.  

    -   Jede Instanz dieser Standortsystemrolle unterstützt die maximale Anzahl von Clients, die von der Hierarchie unterstützt werden.  


### <a name="bkmk_cmg"></a> Cloud Management Gateway

- Sie können mehrere Instanzen des Cloud Management Gateways (CMG) an primären Standorten oder dem Standort der zentralen Verwaltung installieren.  

    > [!Tip]  
    > Erstellen Sie das CMG in einer Hierarchie am Standort der zentralen Verwaltung.  

    - Ein CMG unterstützt zwischen einer und 16 Instanzen virtueller Computer (VMs) im Azure-Clouddienst.  

    - Jede CMG-VM-Instanz unterstützt 6.000 gleichzeitige Clientverbindungen. Wenn das CMG unter hoher Beanspruchung steht, da die unterstützte Anzahl der Clients überschritten wurde, werden Anforderungen weiterhin verarbeitet, jedoch möglicherweise verzögert.  

Weitere Informationen finden Sie im Artikel zur [Leistung und Skalierbarkeit des CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale).


### <a name="cloud-management-gateway-connection-point"></a>Verbindungspunkt für das Cloud Management Gateway

- Sie können an primären Standorten mehrere Instanzen des CMG-Verbindungspunkts installieren.  

- Ein CMG-Verbindungspunkt unterstützt ein CMG mit bis zu vier VM-Instanzen. Wenn das CMG über mehr als vier VM-Instanzen verfügt, fügen Sie einen zweiten CMG-Verbindungspunkt zum Lastenausgleich hinzu. Ein CMG mit 16 VM-Instanzen sollte mit vier CMG-Verbindungspunkten verknüpft sein.

Weitere Informationen finden Sie im Artikel zur [Leistung und Skalierbarkeit des CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale).


### <a name="distribution-point"></a>Verteilungspunkt  

-   Verteilungspunkte pro Standort:  

    -   An jedem primären und sekundären Standort werden bis zu 250 Verteilungspunkte unterstützt.  

    -   Jeder primäre und sekundäre Standort unterstützt bis zu 2000 zusätzliche Verteilungspunkte, die als Pullverteilungspunkte konfiguriert sind. **Beispiel:** Ein einzelner primärer Standort unterstützt 2250 Verteilungspunkte, wenn 2000 dieser Verteilungspunkte als Pullverteilungspunkte konfiguriert sind.  

    -   Jeder Verteilungspunkt unterstützt Verbindungen von bis zu 4.000 Clients.  

    -   Ein Pullverteilungspunkt verhält sich wie ein Client, wenn er auf Inhalte von einem Quellverteilungspunkt zugreift.  

-   An jedem primären Standort werden insgesamt bis zu 5.000 Verteilungspunkte unterstützt. Darin eingeschlossen sind alle Verteilungspunkte des primären Standorts und alle Verteilungspunkte, die zu den untergeordneten sekundären Standorten des primären Standorts gehören.  

-   Jeder Verteilungspunkt unterstützt eine Gesamtgröße von bis zu 10.000 Paketen und Anwendungen.  

> [!WARNING]  
>  Die tatsächliche Anzahl von Clients, die von einem Verteilungspunkt unterstützt werden können, hängt von der Netzwerkgeschwindigkeit und der Hardwarekonfiguration des Servers ab.  
>   
>  Die Anzahl von Pullverteilungspunkten, die von einem Quellverteilungspunkt unterstützt werden, hängt entsprechend von der Netzwerkgeschwindigkeit und der Hardwarekonfiguration des Quellverteilungspunkts ab. Ein weiterer Faktor ist die bereitgestellte Menge von Inhalten. Dies liegt daran, dass alle Pullverteilungspunkte – im Gegensatz zu Clients, die Inhalte an verschiedenen Punkten während der Bereitstellung anfordern – Inhalte gleichzeitig anfordern. Pullverteilungspunkte können allen verfügbaren Inhalt anfordern und nicht nur den Inhalt, der für sie gilt. Wenn die Verarbeitungslast für einen Quellverteilungspunkt zu hoch wird, kann dies zu unerwarteten Verzögerungen bei der Verteilung von Inhalten an die Zielverteilungspunkte führen.  


### <a name="fallback-status-point"></a>Fallbackstatuspunkt  

-   Von jedem Fallbackstatuspunkt können bis zu 100.000 Clients unterstützt werden.  


### <a name="management-point"></a>Verwaltungspunkt  

-   Jeder primäre Standort unterstützt bis zu 15 Verwaltungspunkte.  

    > [!TIP]  
    >  Installieren Sie Verwaltungspunkte nicht auf Servern, die über eine langsame Verbindung mit dem primären Standortserver oder Standortdatenbankserver verbunden sind.  

-   An jedem sekundären Standort wird nur ein Verwaltungspunkt unterstützt, der auf dem sekundären Standortserver installiert sein muss.  

 Informationen zur Anzahl von Clients und Geräten, die von einem Verwaltungspunkt unterstützt werden können, finden Sie in im Abschnitt [Verwaltungspunkte](#bkmk_mp) in diesem Artikel.  


### <a name="software-update-point"></a>Softwareupdatepunkt  

-   Von einem Softwareupdatepunkt, der auf dem Standortserver installiert ist, können bis zu 25.000 Clients unterstützt werden.   

-   Ein remote vom Standortserver installierter Softwareupdatepunkt kann bis zu 150.000 Clients unterstützen, wenn der Remotecomputer die WSUS-Anforderungen (Windows Server Update Services) zur Unterstützung dieser Anzahl von Clients erfüllt.  

-   Die Konfiguration von Softwareupdatepunkten als NLB-Cluster (Network Load Balancing, Netzwerklastenausgleich) wird nicht standardmäßig von Configuration Manager unterstützt. Sie können jedoch das Configuration Manager SDK verwenden, um bis zu vier Softwareupdatepunkte in einem NLB-Cluster zu konfigurieren.  



##  <a name="bkmk_clientnumbers"></a> Anzahl der Clients für Standorte und Hierarchien  
 Ermitteln Sie anhand der folgenden Informationen, wie viele Clients – und welchen Typs – Sie an einem Standort oder in einer Hierarchie unterstützen können.  


###  <a name="bkmk_cas"></a> Hierarchie mit Standort der zentralen Verwaltung  
Ein Standort der zentralen Verwaltung unterstützt eine Gesamtanzahl an Geräten, die maximal der Anzahl an Geräten entspricht, die für die folgenden drei Gruppen aufgelistet ist:  

-   700.000 Desktops (Computer, auf denen Windows, Linux und UNIX ausgeführt wird). Weitere Informationen finden Sie auch in der Unterstützung für [Embedded-Geräte](#embedded).

-   25.000 Macintosh- und Windows CE 7.0-Geräte  

-   Einen der folgenden Einträge, je nachdem, wie die Bereitstellung die Verwaltung mobiler Geräte (MDM, Mobile Device Management) unterstützt:  

    -   100.000 Geräte, die Sie mithilfe der lokalen Verwaltung mobiler Geräte verwalten  

    -   300.000 cloudbasierte Geräte  

 In einer Hierarchie können beispielsweise 700.000 Desktops, bis zu 25.000 Clients für Mac- und Windows CE 7.0-Geräte sowie bis zu 300.000 cloudbasierte Geräte bei der Integration von Microsoft Intune unterstützt werden. Das sind insgesamt 1.025.000 unterstützte Geräte. Wenn mithilfe der lokalen Verwaltung mobiler Geräte verwaltete Geräte unterstützt werden, können in dieser Hierarchie insgesamt 825.000 Geräte unterstützt werden.  

> [!IMPORTANT]  
>  In einer Hierarchie, in der für den Standort der zentralen Verwaltung eine Standardedition von SQL Server verwendet wird, werden in der Hierarchie bis zu 50.000 Desktops und Geräte unterstützt. Um mehr als 50.000 Desktop-PCs und Geräte zu unterstützen, müssen Sie eine Enterprise-Edition von SQL Server verwenden. Diese Anforderung gilt nur für einen Standort der zentralen Verwaltung. Sie gilt nicht für einen eigenständigen primären oder einen untergeordneter primärer Standort. Die verwendete SQL Server-Edition eines primären Standorts schränkt nicht die Anzahl der unterstützten Clients ein.   


 Die an einem eigenständigen primären Standort eingesetzte Edition von SQL Server beschränkt nicht die Kapazität dieses Standorts zur Unterstützung der angegebenen maximalen Anzahl von Clients.  


###  <a name="bkmk_chipri"></a> Untergeordneter primärer Standort  
Jeder untergeordnete primäre Standort in einer Hierarchie mit einem zentralen Verwaltungsstandort unterstützt die folgende Anzahl von Clients:  

-   Insgesamt 150.000 Clients und Geräte, nicht beschränkt auf bestimmte Gruppen oder Typen, solange die unterstützte Gesamtanzahl in der Hierarchie nicht überschritten wird. Weitere Informationen finden Sie auch in der Unterstützung für [Embedded-Geräte](#embedded).

Ein primärer Standort unterstützt beispielsweise 25.000 Mac- und Windows CE 7.0-Geräte. Das ist die maximale Anzahl in einer Hierarchie. Dieser primäre Standort kann zusätzlich 125.000 Desktopcomputer unterstützen. Somit beträgt die maximale Anzahl der insgesamt unterstützten Geräte für einen untergeordneten primären Standort 150.000 Geräte.


###  <a name="bkmk_pri"></a> Eigenständiger primärer Standort  
Ein eigenständiger primärer Standort unterstützt die folgende Anzahl von Geräten:  

-   175.000 Clients und Geräte insgesamt, nicht überschreiten:  

    -   150.000 Desktops (Computer, auf denen Windows, Linux und UNIX ausgeführt wird). Weitere Informationen finden Sie auch in der Unterstützung für [Embedded-Geräte](#embedded).

    -   25.000 Macintosh- und Windows CE 7.0-Geräte

    -   Einen der folgenden Einträge, je nachdem, wie die Bereitstellung die Verwaltung mobiler Geräte unterstützt:  

        -   50.000 Geräte, die mithilfe der lokalen Verwaltung mobiler Geräte verwaltet werden  

        -   150.000 cloudbasierte Geräte  


Beispielsweise können an einem eigenständigen primären Standort, an dem 150.000 Desktops und 10.000 Macintosh- oder Windows CE 7.0-Geräte unterstützt werden, nur zusätzliche 15.000 Geräte unterstützt werden. Diese Geräte können cloudbasiert oder mit der lokalen Verwaltung mobiler Geräte verwaltet werden.  


### <a name="embedded"></a> Primäre Standorte und Windows Embedded-Geräte
Primäre Standorte unterstützen Windows Embedded-Geräte, für die dateibasierte Schreibfilter (File Based Write Filter, FBWF) aktiviert sind. Wenn für eingebettete Geräte keine Schreibfilter aktiviert sind, kann ein primärer Standort eingebettete Geräte bis zur zulässigen Anzahl von Geräten für diesen Standort unterstützen. Maximal 10.000 Geräte der Gesamtzahl an unterstützten Geräten eines primären Standorts können Windows Embedded sein. Diese Geräte müssen für die Ausnahmen konfiguriert sein, die unter [Planning for client deployment to Windows Embedded devices (Planen der Clientbereitstellung auf Windows Embedded-Geräten)](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices) ausgelistet sind. Ein primärer Standort unterstützt nur 3.000 Windows Embedded-Geräte, für die EWF aktiviert ist. Für diese Geräte dürfen keine Ausnahmen konfiguriert werden.


###  <a name="bkmk_sec"></a> Sekundäre Standorte  
Sekundäre Standorte unterstützen die folgende Anzahl an Geräten:  

-   15.000 Desktops (Computer, auf denen Windows, Linux und UNIX ausgeführt wird)  


###  <a name="bkmk_mp"></a> Verwaltungspunkte  
Von jedem Verwaltungspunkt kann die folgende Anzahl von Geräten unterstützt werden:  

-   25.000 Clients und Geräte insgesamt, nicht überschreiten:  

    -   25.000 Desktops (Computer, auf denen Windows, Linux und UNIX ausgeführt wird)  

    -   Eine der folgenden Alternativen (nicht beide):  

        -   10.000 Geräte, die mithilfe der lokalen Verwaltung mobiler Geräte verwaltet werden  

        -   10.000 Macintosh- und Windows CE 7.0-Clients
