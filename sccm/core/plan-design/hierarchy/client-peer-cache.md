---
title: Clientpeercache | System Center Configuration Manager
description: "Verwenden Sie Peercache für Quellspeicherorte für Clientinhalte beim Bereitstellen von Inhalten mit System Center Configuration Manager."
ms.custom: na
ms.date: 1/9/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f3e8cb3a7a4c1de9b8e9866ed192a8a0a7aec106
ms.openlocfilehash: 86129a7fd5bfac676b5f03336cf97d07747b48d1

---
# <a name="peer-cache-for-configuration-manager-clients"></a>Peercache für Configuration Manager-Clients

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1610 von System Center Configuration Manager können Sie **Peercache** zum Verwalten der Bereitstellung von Inhalten für Clients an Remotestandorten verwenden. Peercache ist eine integrierte Configuration Manager-Lösung, mit deren Hilfe Clients Inhalte für andere Clients direkt aus ihrem lokalen Cache freigeben können.   

> [!TIP]  
> Peercache und das Dashboard „Clientdatenquellen“ sind vorab veröffentliche Features in Version 1610. Informationen zum Aktivieren dieser Funktionen finden Sie unter [Verwenden von vorab veröffentlichten Features von Updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

 -  Sie verwenden Clienteinstellungen, um Clients für die Verwendung des Peercaches zu aktivieren.
 -  Zur Freigabe von Inhalten müssen Peercacheclients Mitglieder der aktuellen Begrenzungsgruppe des Clients sein, der nach den Inhalten sucht. Peercacheclients in benachbarten Begrenzungsgruppen sind im Pool der verfügbaren Quellspeicherorte für Inhalt nicht enthalten, wenn ein Client ein Fallback verwendet, um nach Inhalten aus einer benachbarten Begrenzungsgruppe zu suchen. Weitere Informationen zu aktuellen und benachbarten Begrenzungsgruppen finden Sie unter [Begrenzungsgruppen](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 -  Jede Art von Inhalten, die im Cache eines Configuration Manager-Clients gespeichert sind, kann mithilfe von Peercache für andere Clients bereitgestellt werden.
 -  Peercache ersetzt nicht die Verwendung anderer Lösungen wie BranchCache, sondern wird parallel eingesetzt, um Ihnen weitere Optionen bereitzustellen und herkömmliche Lösungen für die Inhaltsbereitstellung (z.B. Verteilungspunkte) zu erweitern. Da diese benutzerdefinierte Lösung nicht von BranchCache abhängig ist, funktioniert sie auch, wenn Sie Windows BranchCache nicht aktivieren oder verwenden.

Nachdem Sie Clienteinstellungen bereitgestellt haben, die den Peercache für eine Sammlung aktivieren, können Mitglieder dieser Sammlung als Peerinhaltsquelle für andere Clients in der gleichen Begrenzungsgruppe fungieren:
 -  Ein Client, der als Peerinhaltsquelle fungiert, übermittelt eine Liste der verfügbaren zwischengespeicherten Inhalte an seinen Verwaltungspunkt.
 -  Wenn der nächste Client in dieser Begrenzungsgruppe diese Inhalte anfordert, wird jede Peercachequelle, die die Inhalte enthält, als mögliche Inhaltsquelle zusammen mit den Verteilungspunkten und anderen Quellspeicherorten für Inhalt in dieser Begrenzungsgruppe zurückgegeben.
 -  Entsprechend dem normalen Verarbeitungsprozess wählt der nach den Inhalten suchende Client eine Inhaltsquelle aus dem Pool der bereitgestellten Quellen aus und versucht dann, die Inhalte abzurufen.

> [!NOTE]
> Wenn ein Fallback auf eine benachbarte Begrenzungsgruppe für Inhalte erfolgt, werden die Peercache-Quellspeicherorte für Inhalt aus den benachbarten Begrenzungsgruppen nicht dem Pool des Clients mit möglichen Quellspeicherorten für Inhalt hinzugefügt.  

Auch wenn Sie die Teilnahme aller Clients am Peercache festlegen können, empfiehlt es sich, nur die Clients auszuwählen, die am besten als Peercachequellen geeignet sind.  Die Eignung von Clients kann anhand des Gehäusetyps, Speicherplatzes, der Netzwerkkonnektivität usw. eines Clients bewertet werden. Weitere Informationen zum Auswählen der am besten geeigneten Clients zur Verwendung für Peercache finden Sie in [diesem Blog eines Microsoft-Beraters](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

Um besser zu verstehen, wann der Peercache erfolgreich verwendet wird, sehen Sie sich das Dashboard „Clientdatenquellen“ an. Siehe dazu [Dashboard „Clientdatenquellen“](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="requirements-and-considerations-for-peer-cache"></a>Anforderungen und Überlegungen für den Peercache
- Der Peercache wird von jedem Windows-Betriebssystem unterstützt, das als Configuration Manager-Client unterstützt wird. Nicht-Windows-Betriebssysteme werden für den Peercache nicht unterstützt.

- Sie müssen Ihren Standort mit einem **Netzwerkzugriffskonto** konfigurieren, das auf jedem Client **Vollzugriff** auf den Cacheordner besitzt. Standardmäßig ist dies ***%windir%\ccmcache***.

- Clients können nur Inhalte von Peercacheclients übertragen, die sich in ihrer aktuellen Begrenzungsgruppe befinden.

-   Da die aktuelle Begrenzung einer Inhaltsquelle des Peercaches durch die letzte Hardwareinventurübermittlung des Clients bestimmt wird, gilt ein Client, der zu einem Netzwerkort in einer anderen Begrenzungsgruppe wechselt, für den Peercache weiterhin als Mitglied seiner früheren Begrenzungsgruppe. Dadurch kann ein Client als Inhaltsquelle des Peercaches angeboten werden, der sich nicht an seinem unmittelbaren Netzwerkort befindet. Es wird empfohlen, Clients, die für diese Konfiguration anfällig sind, von der Teilnahme als Peercachequelle auszuschließen.

## <a name="to-configure-client-peer-cache-client-settings"></a>So konfigurieren Sie Clienteinstellungen für Clientpeercache
1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clienteinstellungen**, und öffnen Sie dann das Objekt mit Geräteclienteinstellungen, das Sie verwenden möchten. Außerdem können Sie das Objekt „Clientstandardeinstellungen“ ändern.
2.  Wählen Sie in der Liste der verfügbaren Einstellungen **Clientcacheeinstellungen** aus.
3.  Legen Sie **Configuration Manager-Client in vollständigem Betriebssystem zur Freigabe von Inhalten aktivieren** auf **Ja** fest.
4.  Konfigurieren Sie die folgenden Einstellungen, um die Ports zu definieren, die für den Peercache verwendet werden sollen:  
  -  **Port für erste Netzwerkübertragung**
  -  **HTTPS für Client-Peer-Kommunikation aktivieren**
  -  **Port für Download der Inhalte vom Peer (HTTP/HTTPS)**

Wenn die Windows-Firewall verwendet wird, wird sie auf jedem für den Peercache aktivierten Computer von Configuration Manager so konfiguriert, dass die Verwendung der konfigurierten Ports zulässig ist.



<!--HONumber=Jan17_HO2-->


