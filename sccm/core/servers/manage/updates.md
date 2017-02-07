---
title: Updates | Microsoft-Dokumentation
description: "Hier finden Sie Informationen zu einer konsoleninternen Dienstmethode namens **Updates und Wartung**, mit der Sie empfohlene Updates leicht finden und installieren können."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
caps.latest.revision: 51
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 816c6bd33e42b70bbafed0dea7624bc5a5421544
ms.openlocfilehash: 55d4f1805937405c4101f5b814875818d2aa72c0


---
# <a name="updates-for-system-center-configuration-manager"></a>Updates für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager verwendet eine konsoleninterne Wartungsmethode namens **Updates und Wartung**, mit der Sie empfohlene Updates für Ihre Configuration Manager-Infrastruktur leicht finden und installieren können. Diese konsoleninterne Wartungsmethode wird durch Out-of-Band-Updates ergänzt, z. B. Hotfixes, die für Kunden bestimmt sind, die möglicherweise für die jeweilige Umgebung spezifische Probleme beheben müssen.  

> [!TIP]
> Beim Verwalten des System Center Configuration Manager-Standorts und der Hierarchieinfrastruktur werden die Begriffe *Upgrade*, *Update* und *Installation* verwendet, um drei verschiedene Konzepte zu beschreiben. Erfahren Sie mehr über die Verwendung der Begriffe unter [Informationen zu Upgrade, Update und Installation für einen Standort und eine Hierarchieinfrastruktur](/sccm/core/understand/upgrade-update-install).


 **In den folgenden Themen wird erläutert, wie Sie die verschiedenen Updatetypen für System Center Configuration Manager suchen und installieren:**  

-   [Install in-console updates for System Center Configuration Manager (Installieren konsoleninterner Updates für System Center Configuration Manager)](../../../core/servers/manage/install-in-console-updates.md)  

-   [Use the Service Connection Tool for System Center Configuration Manager (Verwenden des Dienstverbindungstools für System Center Configuration Manager)](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [Use the Update Registration Tool to import hotfixes to System Center Configuration Manager (Verwenden des Tools zur Updateregistrierung, um Hotfixes in System Center Configuration Manager zu importieren)](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [Use the Hotfix Installer to install updates for System Center Configuration Manager (Verwenden des Hotfixinstallationsprogramms zum Installieren von Updates für System Center Configuration Manager)](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


Wenn Sie die Verzweigung „Technical Preview“ verwenden, finden Sie unter [Technical Preview für System Center Configuration Manager](/sccm/core/get-started/technical-preview) zusätzliche Informationen, die speziell diese Verzweigung betreffen.


##  <a name="a-namebkmkbaselinesa-baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> Baseline- und Updateversionen  
 Die erste Version von System Center Configuration Manager Current Branch ist auch als Version 1511, eine Baselineversion, bekannt. Die neuere Version 1606 wurde als Baseline veröffentlicht:  

-   Verwenden Sie die neueste Baselineversion, wenn Sie einen neuen Standort in einer neuen Hierarchie installieren.  

-   Sie müssen eine Baselineversion verwenden, um ein Upgrade von System Center 2012 Configuration Manager auszuführen.  

-   In regelmäßigen Abständen werden neue Baselineversionen veröffentlicht. Wenn Sie die neueste Baselineversion zur Installation einer neuen Hierarchie verwenden, dann vermeiden Sie die Installation einer veralteten Version von Configuration Manager, gefolgt von einem Upgrade Ihrer Infrastruktur, um sie auf den neuesten Stand zu bringen.  

Nach dem Installieren einer Baselineversion sind zusätzliche Versionen von Configuration Manager als konsoleninterne Updates verfügbar. Mit den konsoleninternen Updates wird Ihre Infrastruktur auf die neueste Version von Configuration Manager aktualisiert.  

-   Sie installieren konsoleninternen Updates, um die Version Ihres Standorts der obersten Ebene zu aktualisieren.  

-   Updates, die Sie am Standort der zentralen Verwaltung installieren, werden an untergeordneten primären Standorten automatisch installiert, es sei denn, sie werden durch ein am primären Standort konfiguriertes Wartungsfenster blockiert.  

-   Sekundäre Standorte müssen Sie manuell in der Konsole auf eine neue Version aktualisieren.  

Wenn Sie ein Update installieren, speichert das Update Installationsdateien für diese Version auf dem Standortserver in einem Ordner namens „CD.Latest“. Weitere Informationen zu diesen Dateien finden Sie unter [The CD.Latest folder for System Center Configuration Manager (Der Ordner „CD.Latest“ für System Center Configuration Manager)](../../../core/servers/manage/the-cd.latest-folder.md).  

-   Sie verwenden die Dateien im Ordner „CD.Latest“ bei der Wiederherstellung von Standorten und zum Installieren zusätzlicher Standorte in einer Hierarchie, in der keine Baselineversion mehr ausgeführt wird.  

-   Zum Installieren des ersten Standorts einer neuen Hierarchie oder zum Aktualisieren eines Standorts von System Center 2012 Configuration Manager können Sie keine Installationsdateien aus dem Ordner „CD.Latest“ verwenden.  

Einige Updates für Configuration Manager sind sowohl eine konsoleninterne Updateversion für vorhandene Infrastruktur als auch eine neue Baselineversion verfügbar.  

Die folgenden Versionen von Configuration Manager sind als Baseline- und/oder Updateversion verfügbar:  

|Version|Verfügbarkeitsdatum|[Supportenddatum](/sccm/core/servers/manage/current-branch-versions-supported) |Baseline|konsoleninternes Update|  
|-------------|-----------|------------|--------------|------------------------|  
| 1511 <br /><br /> 5.00.8325.1000|12/8/2015| 12/8/2016|Ja|Nein|  
|[1602](/sccm/core/plan-design/changes/whats-new-in-version-1602)<br /><br /> 5.00.8355.1000|3/11/2016| 3/11/2017|Nein|Ja|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)<br /><br /> 5.00.8412.1000|7/22/2016| 7/22/2017|Nein|Ja|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606) mit dem Hotfixrollup 1606 (KB3186654) </br></br>5.00.8412.1307 *(Hinweis 1)* |10/12/2016| 7/22/2017|Ja|Nein|
|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)<br /><br /> 5.00.8458.1000|18.11.2016| 11/18/2017|Nein|Ja|
*(Hinweis 1)* Dieses 1606-Baselinemedium ist als Teil des Microsoft System Center 2016- oder des System Center Configuration Manager-Release (Current Branch und Long-Term Servicing Branch 1606) verfügbar.

Um die Version Ihres Configuration Manager-Standorts zu überprüfen, wechseln Sie oben links in der Konsole, wo die neue Version des Standorts und der Konsole angezeigt wird, zu **Info zu System Center Configuration Manager** .  

##  <a name="a-namebkmkinconsolea-in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> Konsoleninterne Updates und Wartung  
 Bei Verwendung einer für die Produktionsumgebung geeigneten Installation von System Center Configuration Manager (die auch als „Current Branch“ bezeichnet wird) sind die meisten zu installierenden Updates über den Kanal „Updates und Wartung“ verfügbar. Mit dieser Methode können Sie die Updates für Ihre aktuelle Infrastrukturversion und Konfiguration ermitteln, herunterladen und zur Verfügung stellen. Dies umfasst nur Updates, die Microsoft allen Kunden empfiehlt.   
 Dazu gehören:  

-   Neue Versionen, z. B. Version 1602  

-   Updates, sie neue Features für die aktuelle Version enthalten  

-   Hotfixes, die für Ihre Version von Configuration Manager verfügbar sind und die alle Kunden installieren sollten  

Die konsoleninternen Updates bieten höhere Stabilität und beheben häufig auftretende Probleme. Sie ersetzen die Updatetypen für frühere Produktversionen, Service Packs, kumulative Updates und Hotfixes, die für alle Kunden verfügbar sind, sowie Erweiterungen für Microsoft Intune angezeigt. Diese Updates können für eine oder mehrere der folgenden Komponenten gelten:  

-   Server des primären Standorts und des Standorts der zentralen Verwaltung  

-   Standortsystemrollen und -server  

-   Instanzen des SMS-Anbieters  

-   Configuration Manager-Konsolen  

-   Configuration Manager-Clients  

Beim Synchronisieren Ihrer Dienstverbindungspunkt-Standortsystemrolle mit dem Microsoft-Clouddienst und Download Center ermittelt Configuration Manager neue Updates für Sie:  

-   Wenn der Dienstverbindungspunkt sich im Onlinemodus befindet, wird Ihr Standort täglich mit Microsoft synchronisiert, um automatisch neue Updates für Ihre Infrastruktur zu ermitteln.  Zum Herunterladen von Updates und verteilbaren Dateien für Updates verwendet der Computer, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird, den **Systemkontext** für den Zugriff auf die folgenden Internetadressen: „go.microsoft.com“ und „download.microsoft.com“. Weitere Informationen zu zusätzlichen Speicherorten, mit denen der Dienstverbindungspunkt eine Verbindung herstellt, finden Sie im Abschnitt [Erforderliche Berechtigungen für den Internetzugriff](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls) unter [Informationen zum Dienstverbindungspunkt in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   Wenn Ihr Dienstverbindungspunkt sich im Offlinemodus befindet, verwenden Sie das Dienstverbindungstool, um eine manuelle Synchronisierung mit der Microsoft-Cloud auszuführen. Weitere Informationen finden Sie unter [Use the Service Connection Tool for System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

-   Durch konsoleninterne Updates entfällt die Notwendigkeit, verfügbare Updates, Service Packs und neue Features einzeln zu suchen und zu installieren.  

-   Es werden nur die konsoleninternen Updates installiert, die Sie auswählen, und bei der Installation bestimmter Updates können Sie die einzelnen Features wählen, die Sie aktivieren und verwenden möchten. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Wenn Sie ein konsoleninternes Update installieren:  

-   Wird automatisch eine Voraussetzungsprüfung durchgeführt. Sie können diese Prüfung auch vor dem Start der Installation ausführen.  

-   Wird es am Standort der zentralen Verwaltung (falls vorhanden) und an primären Standorten automatisch installiert. Mit [Dienstfenster für Standortserver](../../../core/servers/manage/service-windows.md) können Sie steuern, wann die einzelnen primären Standortserver ihre Infrastruktur aktualisieren dürfen.  

-   Nach dem Aktualisieren eines Standortservers werden alle Standortsystemrollen (einschließlich Instanzen des SMS-Anbieters) automatisch aktualisiert. Zudem werden die Konsolenbenutzer von den Configuration Manager-Konsolen aufgefordert, nach der Installation des Updates auf dem Standort die Konsole zu aktualisieren.  

-   Wenn ein Update den Configuration Manager-Client umfasst, können Sie wählen, ob Sie das Update in der Präproduktionsumgebung testen oder sofort auf allen Clients installieren möchten.  

-   Nach der Aktualisierung eines primären Standorts werden die sekundären Standorte nicht automatisch aktualisiert. Stattdessen müssen Sie die Aktualisierung der sekundären Standorte initiieren.  

> [!NOTE]  
>  Das Produktionsrelease von System Center Configuration Manager (Current Branch), Long Term Servicing Branch und die Technical Preview für System Center Configuration Manager sind unterschiedliche Releases. Daher sind Updates für einen Branch nicht als konsoleninterne Updates für andere Branches verfügbar. Weitere Informationen zu den verschiedenen Branches finden Sie unter [Which branch of Configuration Manager should I use (Welchen Configuration Manager-Branch soll ich verwenden?)](/sccm/core/understand/which-branch-should-i-use).

##  <a name="a-namebkmkoutofbanda-out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> Out-of-Band-Hotfixes  
Einige Hotfixes werden mit eingeschränkter Verfügbarkeit veröffentlicht, um spezielle Probleme zu behandeln, oder sind für alle Kunden bestimmt, können aber nicht mit der konsoleninternen Methode installiert werden. Diese Hotfixes werden Out-of-Band bereitgestellt und vom Microsoft-Clouddienst nicht ermittelt.  

In der Regel erfahren Sie über den Microsoft-Kundendienst, einen Knowledge Base-Artikel oder den [System Center Configuration Manager-Teamblog](https://blogs.technet.microsoft.com/configmgrteam) von Out-of-Band-Updates, wenn Sie nach Lösungen für ein Problem mit Ihrer Bereitstellung von Configuration Manager suchen.  

Sie installieren diese Hotfixes manuell unter Verwendung einer der beiden folgenden Methoden:  

-   **Tool zur Updateregistrierung:** Dieses Tool importiert den Hotfix manuell in Ihre Configuration Manager-Konsole, von wo aus Sie das Update dann wie ein automatisch ermitteltes, konsoleninternes Update installieren können. Diese Methode wird für Updates mit der folgenden Dateinamenstruktur verwendet: **.update.exe**.  Der vollständige Dateiname für diese Art von Hotfix sieht in etwa folgendermaßen aus: **&lt;Produkt\>-&lt;Produktversion\>-&lt;KB-Artikel-ID\>-ConfigMgr.Update.exe**.  

     Weitere Informationen finden Sie unter [Verwenden des Tools zur Updateregistrierung, um Hotfixes in System Center Configuration Manager zu importieren](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

-   **Hotfix-Installer:** Dieses Tool wird verwendet, um einen Hotfix, der nicht mit der konsoleninternen Methode installiert werden kann, manuell zu installieren . Diese Methode wird für Hotfixes mit der folgenden Dateinamenstruktur verwendet: **&lt;Produkt\>-&lt;Produktversion\>-&lt;KB-Artikel-ID\>-&lt;Plattform\>-&lt;Sprache\>.exe**.

     Weitere Informationen finden Sie unter [Verwenden des Hotfixinstallationsprogramms zum Installieren von Updates für System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md).



<!--HONumber=Feb17_HO1-->


