---
title: Client-Peercache
titleSuffix: Configuration Manager
description: Verwenden Sie Peercache für Quellspeicherorte für Clientinhalte beim Bereitstellen von Inhalten mit System Center Configuration Manager.
ms.custom: na
ms.date: 04/10/2018
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99eef9faf6ac66f65d16020b703e3a64d9beb9d0
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Peercache für Configuration Manager-Clients

*Gilt für: System Center Configuration Manager (Current Branch)*

<!--1101436-->
Verwenden Sie den **Peercache**, der Sie beim Verwalten von Bereitstellungen von Inhalten an Clients an Remotestandorten unterstützt. Peercache ist eine integrierte Configuration Manager-Lösung, mit deren Hilfe Clients Inhalte für andere Clients direkt aus ihrem lokalen Cache freigeben können.   

> [!TIP]  
> Diese Funktion wurde erstmals in Version 1610 als [Vorabfunktion](/sccm/core/servers/manage/pre-release-features) eingeführt. Ab Version 1710 können ist diese Funktion keine Vorabfunktion mehr.  


> [!Note]  
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen diese Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


## <a name="overview"></a>Übersicht
Ein Peercacheclient ist ein Configuration Manager-Client, der für die Verwendung von Peercache aktiviert ist. Ein Peercacheclient, der über Inhalte verfügt, die für weitere Clients freigegeben werden können, ist eine Peercachequelle.
 -  Sie verwenden Clienteinstellungen, um Clients für die Verwendung des Peercaches zu aktivieren.
 -  Zum Freigeben von Inhalten als Peercachequelle muss ein Peercacheclient folgende Voraussetzungen erfüllen:
    -  Muss in eine Domäne eingebunden sein. Ein Client, der nicht in eine Domäne eingebunden ist, kann jedoch Inhalte von einer in eine Domäne eingebundenen Peercachequelle abrufen.
    -  Muss Mitglied der aktuellen Begrenzungsgruppe des Clients sein, der die Inhalte sucht. Wenn ein Client einen Fallback ausführt, um den Inhalt einer benachbarten Begrenzungsgruppe zu suchen, werden in der Liste von Quellspeicherorten keine Peercacheclients in benachbarten Begrenzungsgruppen beinhaltet. Weitere Informationen zu aktuellen und benachbarten Begrenzungsgruppen finden Sie unter [Begrenzungsgruppen](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Alle Inhaltstypen, die im Cache eines Configuration Manager-Clients gespeichert sind, können mithilfe von Peercache für andere Clients bereitgestellt werden. Dies umfasst Office 365-Dateien und drückt Installationsdateien aus.<!--SMS.500850-->
 -  Der Peercache ersetzt nicht die Verwendung anderer Lösungen wie BranchCache. Zusammen mit anderen Lösungen bietet der Peercache mehr Optionen für das Erweitern herkömmlicher Lösungen für die Inhaltsbereitstellung, wie z.B. Verteilungspunkte. Der Peercache ist eine benutzerdefinierte Lösung, die nicht von BranchCache abhängig ist. Wenn Sie Windows BranchCache nicht aktivieren oder nutzen, funktioniert der Peercache trotzdem.

### <a name="operations"></a>Vorgänge

Stellen Sie die Clienteinstellungen einer Sammlung bereit, um den Peercache zu aktivieren. Mitglieder dieser Sammlung fungieren dann als Peerinhaltsquelle für andere Clients in derselben Begrenzungsgruppe.
 -  Ein Client, der als Peerinhaltsquelle fungiert, übermittelt eine Liste der verfügbaren zwischengespeicherten Inhalte an seinen Verwaltungspunkt.
 -  Wenn der nächste Client in der Begrenzungsgruppe diesen Inhalt abruft, wird jede Peercachequelle, die diesen Inhalt enthält und online ist, in der Liste der möglichen Inhaltsquellen angegeben. Diese Liste enthält auch die Verteilungspunkte und andere Quellspeicherorte für Inhalte in dieser Begrenzungsgruppe.
 -  Entsprechend dem normalen Prozess wählt der Client, der nach dem Inhalt sucht, eine Quelle aus der angegebenen Liste aus. Dann versucht der Client den Inhalt abzurufen.

> [!NOTE]
> Wenn ein Client einen Fallback auf eine benachbarte Begrenzungsgruppe für Inhalte ausführt, werden die Peercache-Quellspeicherorte für Inhalt aus den benachbarten Begrenzungsgruppen nicht der Liste von möglichen Quellspeicherorten für Inhalt hinzugefügt.  


Es wird empfohlen, nur Clients zu wählen, die am besten als Peercachequellen geeignet sind. Bewerten Sie die Eignung der Clients nach Attributen wie Chassistyp, Speicherplatz und Netzwerkkonnektivität. Weitere Informationen zum Auswählen der am besten geeigneten Clients zur Verwendung für Peercache finden Sie in [diesem Blog eines Microsoft-Beraters](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Eingeschränkter Zugriff auf eine Peercachequelle**  
Ab Version 1702 lehnt ein Peercache-Quellcomputer Inhaltsanforderungen ab, wenn der Peercache-Quellcomputer eine der folgenden Bedingungen erfüllt:  
  -  Niedriger Akkustand.
  -  Zum Zeitpunkt der Anforderungen des Inhalts liegt die CPU-Auslastung bei über 80 %.
  -  *AvgDiskQueueLength* der Datenträger-E/A überschreitet 10.
  -  Es gibt keine weiteren Verbindungen zum Computer.   

Konfigurieren Sie diese Einstellungen mithilfe der WMI-Klasse des Clientkonfigurationsservers für die Peerquellfunktion (*SMS_WinPEPeerCacheConfig*) im Configuration Manager SDK.

Wenn der Computer eine Anforderung von Inhalt ablehnt, sucht der anfordernde Computer in der Liste von verfügbaren Quellspeicherorten weiterhin nach Inhalt.   



### <a name="monitoring"></a>Überwachung   
Um besser zu verstehen, wann der Peercache erfolgreich verwendet wird, sehen Sie sich das Dashboard „Clientdatenquellen“ an. Siehe dazu [Dashboard „Clientdatenquellen“](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

Ab Version 1702 können Sie drei Berichte verwenden, um die Peercacheauslastung anzuzeigen. Navigieren Sie in der Konsole zu **Überwachung** > **Berichterstellung** > **Berichte**. Die Berichte haben alle den Typ **Softwareverteilung – Inhalt**:
1.  **Ablehnen von Inhalt einer Peercachequelle**:  
Mithilfe dieses Berichts erfahren Sie, wie häufig die Peercachequellen in einer Begrenzungsgruppe Inhaltsanforderungen ablehnen.
 - **Bekanntes Problem:** Wenn Sie einen Drilldown für Ergebnisse wie *MaxCPULoad* und *MaxDiskIO* durchführen, erhalten Sie möglicherweise einen Fehler, der darauf hinweist, dass der Bericht oder Angaben nicht gefunden werden können. Verwenden Sie die folgenden beiden Berichte, die die Ergebnisse direkt anzeigen, um dieses Problem zu umgehen.

2. **Ablehnen von Inhalt einer Peercachequelle durch eine Bedingung**:  
Erfahren Sie mithilfe dieses Berichts, wie Sie Angaben zur Ablehnung einer angegebenen Begrenzungsgruppe oder eines Ablehnungstyps interpretieren können. Sie können Folgendes bestimmen:

  - **Bekannte Probleme:** Sie können nicht aus verfügbaren Parametern wählen, sondern müssen diese manuell eingeben. Geben Sie die Werte für *Name der Begrenzungsgruppe* und *Rejection Type* (Ablehnungstyp) ein, so wie im ersten Bericht dargestellt. Sie können z.B. für *Rejection Type* (Ablehnungstyp) *MaxCPULoad* oder *MaxDiskIO* eingeben.

3. **Angaben zur Ablehnung von Inhalt einer Peercachequelle**:   
  Erfahren Sie mithilfe dieses Berichts, welchen Inhalt der Client angefordert hat, wenn die Anforderung abgelehnt wird.

 - **Bekannte Probleme:** Sie können nicht aus verfügbaren Parametern wählen, sondern müssen diese manuell eingeben. Geben Sie den Wert für *Rejection Type* (Ablehnungstyp) ein, wie im Bericht **Ablehnen von Inhalt einer Peercachequelle** gezeigt wird. Geben Sie dann die *Ressourcen-ID* für die Inhaltsquelle ein, über die Sie mehr Informationen sehen möchten. So finden Sie die Resource ID der Quelle des Inhalts heraus:  

    1. Machen Sie den Namen des Computers ausfindig, der als *Peercachequelle* in den Ergebnissen des Berichts **Ablehnen von Inhalt einer Peercachequelle durch eine Bedingung** angezeigt wird.  
    2. Navigieren Sie anschließend zu **Bestand und Kompatibilität** > **Geräte**, und suchen Sie nach dem Namen des Computers. Verwenden Sie den Wert aus der Spalte „Resource ID“.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Anforderungen und Überlegungen für den Peercache
-   Der Peercache wird von jedem Windows-Betriebssystem unterstützt, das als Configuration Manager-Client unterstützt wird. Nicht-Windows-Betriebssysteme werden für den Peercache nicht unterstützt.

-   Clients können nur Inhalte von Peercacheclients übertragen, die sich in ihrer aktuellen Begrenzungsgruppe befinden.

-   Vor Version 1706 muss jeder Standort, an dem Clients Peer Cache verwenden, mit einem [Netzwerkzugriffskonto](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account) konfiguriert sein. Mit einer Ausnahme ist der Account ab Version 1706 nicht mehr erforderlich. Das Ausnahmeszenario tritt ein, wenn ein Peercache-fähiger Client eine Tasksequenz aus dem Softwarecenter ausführt, die als Startimage neu startet. In diesem Szenario benötigt der Client weiterhin das Netzwerkzugriffskonto. Wenn sich der Client in Windows PE befindet, verwendet er das Netzwerkzugriffskonto, um Inhalte aus der Peercachequelle abzurufen.

    Wenn erforderlich, verwendet der Peercache-Quellcomputer das Netzwerkzugriffskonto, um Downloadanforderungen von Peers zu authentifizieren. Dieses Konto benötigt zu diesem Zweck nur Domänenbenutzerberechtigungen.

-   Die letzte Hardwareinventurübermittlung des Clients bestimmt die aktuelle Grenze einer Peercache-Inhaltsquelle. Ein Client, der zu einer anderen Begrenzungsgruppe wandert, ist für den Peercache möglicherweise weiterhin ein Mitglied seiner früheren Begrenzungsgruppe. Durch dieses Verhalten kann ein Client als Inhaltsquelle des Peercaches angeboten werden, der sich nicht an seinem unmittelbaren Netzwerkort befindet. Es wird empfohlen, Clients, die für diese Konfiguration anfällig sind, von der Teilnahme als Peercachequelle auszuschließen.
-    Ab Version 1706 überprüft der Peercacheclient zunächst, ob die Peercache-Inhaltsquelle online ist, bevor er versucht, Inhalte herunterzuladen. <!--sms.498675-->

## <a name="to-configure-client-peer-cache-client-settings"></a>So konfigurieren Sie Clienteinstellungen für Clientpeercache
Informationen über das Konfigurieren der Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](/sccm/core/clients/deploy/configure-client-settings).

Auf Peercache-fähigen Clients, die die Windows Firewall verwenden, konfiguriert Configuration Manager die Firewallports, die Sie in den Clienteinstellungen festlegen.
