---
title: "Größe und Skalierung | System Center Configuration Manager"
description: "Identifizieren Sie die Anzahl der Standortsystemrollen und Standorte, die für die Unterstützung von Geräten in Ihrer System Center Configuration Manager-Umgebung notwendig sind."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aeeb902fad7444534cafa7f9cb984ce8764471b0

---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Größe und Skalierung von Zahlen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*



Jede Bereitstellung von System Center Configuration Manager hat eine maximale Anzahl von Standorten, Standortsystemrollen und Geräten, die unterstützt werden können. Diese Zahlen sind abhängig von Ihrer Hierarchiestruktur (welche Typen und welche Anzahl von Standorten Sie verwenden), und den Standortsystemrollen, die Sie bereitstellen.  Die Informationen in den folgenden Themen unterstützen Sie dabei, die Anzahl von Standortsystemrollen und Standorten zu ermitteln, die für die Unterstützung der Geräte notwendig sind, die voraussichtlich in Ihrer Umgebung verwaltet werden.

Verwenden Sie die Informationen in diesem Thema mit den Informationen in den folgenden Artikeln:
-   [Empfohlene Hardware](../../../core/plan-design/configs/recommended-hardware.md)
-   [Unterstützte Betriebssysteme für Standortsystemserver](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Unterstützte Betriebssysteme für Clients und Geräte](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Voraussetzungen für Standorte und Standortsysteme](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)

Die unterstützen Zahlen in diesem Artikel basieren auf Verwendung der empfohlenen Hardware für Configuration Manager. Wenn Sie nicht die empfohlene Hardware verwenden, kann die Leistung von Standortsystemen beeinträchtigt werden, sodass sie möglicherweise nicht die oben genannten Unterstützungsniveaus erfüllt.

##  <a name="a-namebkmksitesystemscalea-site-types"></a><a name="bkmk_SiteSystemScale"></a> Standorttypen  
 **Standort der zentralen Verwaltung:**  

-   Ein Standort der zentralen Verwaltung unterstützt bis zu 25 untergeordnete primäre Standorte.  

**Primärer Standort:**  

-   Jeder primäre Standort unterstützt bis zu 250 sekundäre Standorte.  

-   Die maximale Anzahl sekundärer Standorte pro primärem Standort wurde auf Basis von kontinuierlich verbundenen und stabilen WAN (Wide Area Network)-Verbindungen ermittelt. Für Standorte mit weniger als 500 Clients können Sie einen Verteilungspunkt anstatt eines sekundären Standorts erwägen.  

 Informationen zur Anzahl von Clients und Geräten, die von einem primären Standort unterstützt werden können, finden Sie in diesem Thema unter [Anzahl der Clients für Standorte und Hierarchien](#bkmk_clientnumbers).  

**Sekundärer Standort:**  

-   Sekundäre Standorte unterstützen keine untergeordneten Standorte.  

-   Ein Standort der zentralen Verwaltung unterstützt bis zu 25 untergeordnete primäre Standorte.  

**Anwendungskatalog-Websitepunkt:**  

-   An primären Standorten können Sie mehrere Instanzen des Anwendungskatalog-Websitepunkts installieren.  

    > [!TIP]  
    >  Es wird empfohlen, den Anwendungskatalog-Websitepunkt und den Anwendungskatalog-Webservicepunkt gemeinsam auf dem gleichen Standortsystem zu installieren, wenn die Dienste für Clients im Intranet bereitgestellt werden.  

    -   Planen Sie aus Leistungsgründen, bis zu 50.000 Clients pro Instanz zu unterstützen.  

    -   Jede Instanz dieser Standortsystemrolle unterstützt die maximale Anzahl von Clients, die von der Hierarchie unterstützt werden.  

## <a name="a-namebkmkrolesa-site-system-roles"></a><a name="bkmk_roles"></a> Standortsystemrolle    

**Anwendungskatalog-Webdienstpunkt:**  

-   An primären Standorten können Sie mehrere Instanzen des Anwendungskatalog-Webservicepunkts installieren.  

    > [!TIP]  
    >  Es wird empfohlen, den Anwendungskatalog-Websitepunkt und den Anwendungskatalog-Webservicepunkt gemeinsam auf dem gleichen Standortsystem zu installieren, wenn die Dienste für Clients im Intranet bereitgestellt werden.  

    -   Planen Sie aus Leistungsgründen, bis zu 50.000 Clients pro Instanz zu unterstützen.  

    -   Jede Instanz dieser Standortsystemrolle unterstützt die maximale Anzahl von Clients, die von der Hierarchie unterstützt werden.  

**Verteilungspunkt:**  

-   Verteilungspunkte pro Standort:  

    -   An jedem primären und sekundären Standort werden bis zu 250 Verteilungspunkte unterstützt.  

    -   Jeder primäre und sekundäre Standort unterstützt bis zu 2.000 zusätzliche Verteilungspunkte, die als Pullverteilungspunkte konfiguriert sind. **Beispiel:** Ein einzelner primärer Standort unterstützt 2250 Verteilungspunkte, wenn 2000 dieser Verteilungspunkte als Pullverteilungspunkte konfiguriert sind.  

    -   Jeder Verteilungspunkt unterstützt Verbindungen von bis zu 4.000 Clients.  

    -   Ein Pullverteilungspunkt verhält sich wie ein Client, wenn er auf Inhalte von einem Quellverteilungspunkt zugreift.  

-   An jedem primären Standort werden insgesamt bis zu 5.000 Verteilungspunkte unterstützt. Darin eingeschlossen sind alle Verteilungspunkte des primären Standorts und alle Verteilungspunkte, die zu den untergeordneten sekundären Standorten des primären Standorts gehören.  

-   Jeder Verteilungspunkt unterstützt eine Gesamtgröße von bis zu 10.000 Paketen und Anwendungen.  

> [!WARNING]  
>  Die tatsächliche Anzahl von Clients, die von einem Verteilungspunkt unterstützt werden können, hängt von der Netzwerkgeschwindigkeit und der Hardwarekonfiguration des Verteilungspunktcomputers ab.  
>   
>  Die Anzahl von Pullverteilungspunkten, die von einem Quellverteilungspunkt unterstützt werden, hängt entsprechend von der Netzwerkgeschwindigkeit und der Hardwarekonfiguration des Quellverteilungspunkt-Computers ab. Ein weiterer Faktor ist die bereitgestellte Menge von Inhalten. Dies liegt daran, dass alle Pullverteilungspunkte zur gleichen Zeit Inhalte anfordern und zudem den gesamten verfügbaren Inhalt und nicht nur (wie ein Client) den auf sie anwendbaren Inhalt abrufen können. Darin unterscheiden sie sich von Clients, die in der Regel zu unterschiedlichen Zeiten des Bereitstellungsfensters auf Inhalte zugreifen. Wenn die Verarbeitungslast für einen Quellverteilungspunkt zu hoch wird, kann dies zu unerwarteten Verzögerungen bei der Verteilung von Inhalten an die erwarteten Verteilungspunkte in der Umgebung führen.  


**Fallbackstatuspunkt:**  

-   Von jedem Fallbackstatuspunkt können bis zu 100.000 Clients unterstützt werden.  

**Verwaltungspunkt:**  

-   Jeder primäre Standort unterstützt bis zu 15 Verwaltungspunkte.  

    > [!TIP]  
    >  Installieren Sie Verwaltungspunkte nicht auf Servern, die über eine langsame Verknüpfung vom primären Standortserver oder Standortdatenbankserver verbunden sind.  

-   An jedem sekundären Standort wird nur ein Verwaltungspunkt unterstützt, der auf dem sekundären Standortserver installiert sein muss.  

 Informationen zur Anzahl von Clients und Geräten, die von einem Verwaltungspunkt unterstützt werden können, finden Sie in diesem Thema im Abschnitt [Verwaltungspunkte](#bkmk_mp).  

**Softwareupdatepunkt:**  

-   Von einem Softwareupdatepunkt, der auf dem Standortserver installiert ist, können bis zu 25.000 Clients unterstützt werden.  

-   Ein remote vom Standortserver installierter Softwareupdatepunkt kann bis zu 150.000 Clients unterstützen, wenn der Remotecomputer die WSUS-Anforderungen zur Unterstützung dieser Anzahl von Clients erfüllt.  

-   Die Konfiguration von Softwareupdatepunkten als NLB-Cluster wird nicht standardmäßig von Configuration Manager unterstützt. Sie können jedoch das Configuration Manager SDK verwenden, um bis zu vier Softwareupdatepunkte in einem NLB-Cluster zu konfigurieren.  

##  <a name="a-namebkmkclientnumbersa-client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a> Anzahl der Clients für Standorte und Hierarchien  
 Ermitteln Sie anhand der folgenden Informationen, wie viele Clients – und welchen Typs – Sie an einem Standort oder in einer Hierarchie unterstützen können.  

###  <a name="a-namebkmkcasa-hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a> Hierarchie mit Standort der zentralen Verwaltung  
Ein Standort der zentralen Verwaltung unterstützt eine Gesamtanzahl an Geräten, die maximal der Anzahl an Geräten entspricht, die für die folgenden drei Gruppen aufgelistet ist:  

-   700.000 Desktops (Computer, auf denen Windows, Linux und UNIX ausgeführt wird)  

-   25.000 Macintosh- und Windows CE 7.0-Geräte  

-   Einen der folgenden Einträge, je nachdem, wie die Bereitstellung die Verwaltung mobiler Geräte unterstützt:  

    -   100.000 Geräte, die Sie mit einem lokalen MDM verwalten  

    -   300.000 cloudbasierte Geräte  

 In einer Hierarchie können Sie z.B. 700.000 Desktops, bis zu 25.000 Clients für Macintosh und Windows CE 7.0 sowie bis zu 300.000 cloudbasierte Geräte bei der Integration von Microsoft Intune unterstützen. Das sind insgesamt 1.025.000 Geräte.  Wenn Sie mithilfe von lokalem MDM verwaltete Geräte unterstützen, beträgt die Summe für die Hierarchie 825.000 Geräte.  

> [!IMPORTANT]  
>  In einer Hierarchie, wo der Standort der zentralen Verwaltung eine Standardedition von SQL Server verwendet, unterstützt die Hierarchie bis zu 50.000 Desktops und Geräte. Die an einem eigenständigen primären Standort eingesetzte Edition von SQL Server beschränkt nicht die Kapazität dieses Standorts zur Unterstützung der angegebenen maximalen Anzahl von Clients.  


###  <a name="a-namebkmkchipria-child-primary-site"></a><a name="bkmk_chipri"></a> Untergeordneter primärer Standort  
Jeder untergeordnete primäre Standort in einer Hierarchie mit einem zentralen Verwaltungsstandort unterstützt Folgendes:  

-   Insgesamt 150.000 Clients und Geräte, nicht beschränkt auf bestimmte Gruppen oder Typen, solange die unterstützte Gesamtanzahl in der Hierarchie nicht überschritten wird.  

Beispielsweise kann ein primärer Standort, der 25.000 Computer unterstützt, auf denen Macintosh und Windows CE 7.0 ausgeführt wird (da dies der Grenzwert für die Hierarchie ist), dann zusätzlich 125.000 Desktopcomputer unterstützen. Damit beträgt die Anzahl der unterstützten Geräte insgesamt 150.000, der Höchstwert, der von untergeordneten primären Standorten unterstützt wird.

###  <a name="a-namebkmkpria-stand-alone-primary-site"></a><a name="bkmk_pri"></a> Eigenständiger primärer Standort  
Ein eigenständiger primärer Standort unterstützt die folgende Anzahl von Geräten:  

-   175.000 Clients und Geräte insgesamt, nicht überschreiten:  

    -   150.000 Desktops (Computer, auf denen Windows, Linux und UNIX ausgeführt wird)  

    -   25.000 Macintosh- und Windows CE 7.0-Geräte  

    -   Einen der folgenden Einträge, je nachdem, wie die Bereitstellung die Verwaltung mobiler Geräte unterstützt:  

        -   50.000 Geräte, die Sie mit einem lokalen MDM verwalten  

        -   150.000 cloudbasierte Geräte  

Beispielsweise kann ein eigenständiger primärer Standort, der 150.000 Desktops und 10.000 Macintosh- oder Windows CE 7.0-Clients unterstützt, nur zusätzliche 15.000 Geräte unterstützen. Diese Geräte können cloudbasiert oder mit lokalem MDM verwaltet werden.  

###  <a name="a-namebkmkseca-secondary-sites"></a><a name="bkmk_sec"></a> Sekundäre Standorte  
Sekundäre Standorte unterstützen Folgendes:  

-   15.000 Desktops (Computer, auf denen Windows, Linux und UNIX ausgeführt wird)  

###  <a name="a-namebkmkmpa-management-points"></a><a name="bkmk_mp"></a> Verwaltungspunkte  
Jede Verwaltung kann die folgende Anzahl von Geräten unterstützen:  

-   25.000 Clients und Geräte insgesamt, nicht überschreiten:  

    -   25.000 Desktops (Computer, auf denen Windows, Linux und UNIX ausgeführt wird)  

    -   Eine der folgenden Alternativen (nicht beide):  

        -   10.000 mit lokalem MDM verwaltete Geräte  

        -   10.000 Macintosh- und Windows CE 7.0-Geräte  



<!--HONumber=Nov16_HO1-->


