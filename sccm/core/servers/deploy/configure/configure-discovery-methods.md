---
title: Konfigurieren von Ermittlungsmethoden | Microsoft-Dokumentation
description: "Konfigurieren Sie Ermittlungsmethoden zur Ausführung auf einem Configuration Manager-Standort, um Ressourcen zu suchen, die Sie von der Netzwerkinfrastruktur und Active Directory verwalten können."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 2fcc392ba700f871349200166fac715b73788c16

---
# <a name="configure-discovery-methods-for-system-center-configuration-manager"></a>Konfigurieren von Ermittlungsmethoden für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Sie konfigurieren Ermittlungsmethoden zur Ausführung auf einem System Center Configuration Manager-Standort, um Ressourcen zu suchen, die Sie von der Netzwerkinfrastruktur und Active Directory verwalten können. Dazu müssen Sie jede Methode aktivieren und anschließend konfigurieren, die Sie zum Suchen in Ihrer Umgebung verwenden möchten. (Sie können außerdem jede Methode mit den gleichen Schritten deaktivieren, mit denen sie aktiviert wird.)  Die einzigen Ausnahmen hiervon sind Frequenzermittlung und Serverermittlung:  

-   In der Standardeinstellung ist die Frequenzermittlung bereits aktiviert, wenn Sie einen primären Standort von Configuration Manager installieren, und für die Ausführung nach einem einfachen Zeitplan konfiguriert. Lassen Sie die Frequenzermittlung aktiviert, da durch diese Methode sichergestellt wird, dass die Discovery Data Records (DDRs) für Geräte aktuell sind. Weitere Informationen zur Frequenzermittlung finden Sie unter [Informationen zur Frequenzermittlung](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).  

-   Die Serverermittlung ist eine automatische Erkennungsmethode, die Computer findet, die Sie als Standortsystem verwenden. Es ist keine Methode, die Sie konfigurieren oder deaktivieren können.  

**So aktivieren Sie jede konfigurierbare Ermittlungsmethode:**  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** und dann auf **Ermittlungsmethoden**.  

2.  Wählen Sie die Ermittlungsmethode für den Standort aus, an dem die Ermittlung aktiviert werden soll.  

3.  Klicken Sie in der Gruppe **Eigenschaften** auf der Registerkarte **Startseite** auf **Eigenschaften**, und aktivieren Sie dann auf der Registerkarte **Allgemein** das Kontrollkästchen **Ermittlungsmethode&lt;aktivieren\>**.  

     Wenn dieses Kontrollkästchen bereits aktiviert ist, können Sie die Ermittlungsmethode deaktivieren, indem Sie das Kontrollkästchen deaktivieren.  

4.  Klicken Sie auf **OK** , um die Konfiguration zu speichern.  


##  <a name="a-namebkmkconfigadforestdisca-configure-active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a> Konfigurieren der Active Directory-Gesamtstrukturermittlung  
 Sie müssen an zwei Orten Einstellungen konfigurieren, um die Konfiguration der Active Directory-Gesamtstrukturermittlung abzuschließen:  

-   Im Knoten **Ermittlungsmethoden** können Sie diese Ermittlungsmethode aktivieren. Sie können einen Abfragezeitplan festlegen und auswählen, ob von der Ermittlung automatisch Grenzen für die ermittelten Active Directory-Standorte und -Subnetze erstellt werden sollen.  

-   Im Knoten **Active Directory-Gesamtstruktur** können Sie zu ermittelnde Gesamtstrukturen hinzufügen und die Ermittlung von Active Directory-Standorten und -Subnetzen in der jeweiligen Gesamtstruktur aktivieren. Außerdem können Sie Einstellungen konfigurieren, mit denen ein Veröffentlichen der Standortinformationen von Configuration Manager-Standorten in der Gesamtstruktur ermöglicht wird, und Sie können jeder Gesamtstruktur ein Konto für die Verwendung als Active Directory-Gesamtstrukturkonto zuweisen.  

 Wenden Sie die folgenden Verfahren an, um die Active Directory-Gesamtstrukturermittlung zu aktivieren und individuelle Gesamtstrukturen für die Verwendung mit der Active Directory-Gesamtstrukturermittlung zu konfigurieren.  

#### <a name="to-enable-active-directory-forest-discovery"></a>So aktivieren Sie die Active Directory-Gesamtstrukturermittlung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** und anschließend auf **Ermittlungsmethoden**.  

2.  Wählen Sie die Methode Active Directory-Gesamtstrukturermittlung für den Standort, an dem die Ermittlung konfiguriert werden soll, aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen zum Aktivieren der Ermittlung. Sie können die Ermittlung auch sofort konfigurieren und später aktivieren.  

5.  Geben Sie Optionen zum Erstellen von Standortgrenzen für ermittelte Orte an.  

6.  Geben Sie einen Zeitplan für die Ausführung der Ermittlung an.  

7.  Wenn Sie mit der Konfiguration der Active Directory-Gesamtstrukturermittlung für diesen Standort fertig sind, klicken Sie auf **OK** , um die Konfiguration zu speichern.  

#### <a name="to-configure-a-forest-for-active-directory-forest-discovery"></a>So konfigurieren Sie eine Gesamtstruktur für die Active Directory-Gesamtstrukturermittlung  

1.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Active Directory-Gesamtstrukturen**. Wenn eine Active Directory-Gesamtstrukturermittlung bereits ausgeführt wurde, werden die ermittelten Gesamtstrukturen im Ergebnisbereich angezeigt. Bei der Ausführung der Active Directory-Gesamtstrukturermittlung werden die lokale Gesamtstruktur und alle vertrauenswürdigen Gesamtstrukturen ermittelt. Nur nicht vertrauenswürdige Gesamtstrukturen müssen manuell hinzugefügt werden.  

    -   Wählen Sie zum Konfigurieren einer bereits ermittelten Gesamtstruktur die gewünschte Gesamtstruktur im Ergebnisbereich aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften** , um die Eigenschaften der Gesamtstruktur anzuzeigen. Fahren Sie mit Schritt 3 fort.  

    -   Klicken Sie zum Konfigurieren einer nicht aufgelisteten Gesamtstruktur auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Gesamtstruktur hinzufügen** , um das Dialogfeld **Gesamtstruktur hinzufügen** zu öffnen. Fahren Sie mit Schritt 3 fort.  

2.  Schließen Sie auf der Registerkarte **Allgemein** die Konfiguration für die zu ermittelnde Gesamtstruktur ab, und geben Sie das **Konto für die Active Directory-Gesamtstruktur**an.  

    > [!NOTE]  
    >  Für die Active Directory-Gesamtstrukturermittlung ist ein globales Konto erforderlich, damit Ermittlung und Veröffentlichung in nicht vertrauenswürdigen Gesamtstrukturen möglich sind. Wenn Sie nicht das Computerkonto des Standortservers verwenden, können Sie nur ein globales Konto auswählen.  

3.  Wenn Sie planen, eine Veröffentlichung von Standortdaten in dieser Gesamtstruktur zu ermöglichen, konfigurieren Sie auf der Registerkarte **Veröffentlichen** das Veröffentlichen in dieser Gesamtstruktur.  

    > [!NOTE]  
    >  Wenn Sie Standorte für die Veröffentlichung in einer Gesamtstruktur aktivieren, müssen Sie das Active Directory-Schema dieser Gesamtstruktur für Configuration Manager erweitern. Außerdem muss das Konto für die Active Directory-Gesamtstruktur über Vollzugriff auf den Systemcontainer in dieser Gesamtstruktur verfügen.  

4.  Wenn Sie die Konfiguration dieser Gesamtstruktur zur Verwendung mit der Active Directory-Gesamtstrukturermittlung abgeschlossen haben, klicken Sie auf **OK** , um die Konfiguration zu speichern.  

##  <a name="a-namebkmkconfigaddiscgenerala-configure-active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a> Konfigurieren der Active Directory-Ermittlung für Computer, Benutzer oder Gruppen  
 Verwenden Sie die Informationen in den folgenden Abschnitten, um für Computer, Benutzer oder Gruppen eine der folgenden Ermittlungsmethoden zu konfigurieren:  

-   Active Directory-Gruppenermittlung  

-   Active Directory-Systemermittlung  

-   Active Directory-Benutzerermittlung  

> [!NOTE]  
>  Die Informationen in diesem Abschnitt gelten nicht für die Active Directory-Gesamtstrukturermittlung.  

 Jede dieser Ermittlungsmethoden kann unabhängig von den anderen angewendet werden; ihre Optionen sind jedoch vergleichbar. Weitere Informationen zu diesen Konfigurationsoptionen finden Sie unter [Shared options for Group, System, and User discovery (Gemeinsam genutzte Optionen für die Gruppen-, System- und Benutzererkennung)](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
>  Durch die Active Directory-Abfragen im Rahmen jeder dieser Ermittlungsmethoden kann eine erhebliche Netzwerkauslastung verursacht werden. Erwägen Sie, die Ermittlungsmethoden für Zeiten zu planen, wenn die geschäftliche Nutzung des Netzwerks durch eine solche Netzwerkauslastung nicht beeinträchtigt wird.  

#### <a name="to-configure-active-directory-group-discovery"></a>Konfigurieren der Active Directory-Gruppenermittlung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** und anschließend auf **Ermittlungsmethoden**.  

2.  Wählen Sie die Methode **Active Directory-Gruppenermittlung** für den Standort aus, an dem die Ermittlung konfiguriert werden soll.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen zum Aktivieren der Ermittlung. Sie können die Ermittlung auch sofort konfigurieren und später aktivieren.  

5.  Klicken Sie auf **Hinzufügen** , um einen Ermittlungsbereich zu konfigurieren. Wählen Sie entweder **Gruppen** oder **Ort**aus, und führen Sie im Dialogfeld **Gruppen hinzufügen**bzw. im Dialogfeld **Active Directory-Ort hinzufügen** die folgenden Konfigurationen aus:  

    1.  Geben Sie einen Namen ** ** für diesen Ermittlungsbereich an.  

    2.  Geben Sie eine **Active Directory-Domäne** oder einen **Ort** zum Durchsuchen an:  

        -   Wenn Sie **Gruppen**ausgewählt haben, geben Sie mindestens eine Active Directory-Gruppe an, die ermittelt werden soll.  

        -   Wenn Sie **Ort**ausgewählt haben, geben Sie einen Active Directory-Container als Ort, der ermittelt werden soll, an. Sie können auch eine rekursive Suche in den untergeordneten Active Directory-Containern dieses Orts aktivieren.  

    3.  Geben Sie das **Konto für die Active Directory-Sicherheitsgruppenermittlung** an, das zum Durchsuchen dieses Ermittlungsbereichs verwendet werden soll.  

    4.  Klicken Sie auf **OK** , um die Konfiguration des Ermittlungsbereichs zu speichern.  

6.  Wiederholen Sie Schritt 6 für jeden zusätzlichen Ermittlungsbereich, den Sie definieren möchten.  

7.  Konfigurieren Sie auf der Registerkarte **Abfragezeitplan** den Zeitplan für die vollständige Ermittlungsabfrage sowie die Deltaermittlung.  

8.  Optional können Sie auf der Registerkarte **Option** Optionen zum Herausfiltern oder Ausschließen veralteter Computerdatensätze von der Ermittlung sowie zum Ermitteln der Mitgliedschaft von Verteilergruppen konfigurieren.  

    > [!NOTE]  
    >  Von der Active Directory-Gruppenermittlung wird standardmäßig nur die Mitgliedschaft von Sicherheitsgruppen ermittelt.  

9. Wenn Sie mit dem Konfigurieren der Active Directory-Gruppenermittlung fertig sind, klicken Sie auf **OK** , um die Konfiguration zu speichern.  

#### <a name="to-configure-active-directory-system-discovery"></a>So konfigurieren Sie die Active Directory-Systemermittlung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** und anschließend auf **Ermittlungsmethoden**.  

2.  Wählen Sie die Ermittlungsmethode für den Standort aus, an dem die Ermittlung konfiguriert werden soll.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen zum Aktivieren der Ermittlung. Sie können die Ermittlung auch sofort konfigurieren und später aktivieren.  

5.  Klicken Sie auf das Symbol **Neu** ![New icon](media/Disc_new_Icon.gif), um einen neuen Active Directory-Container anzugeben. Führen Sie dann im Dialogfeld **Active Directory-Container** die folgenden Konfigurationsschritte aus:  

    1.  Geben Sie mindestens einen Speicherort an, der durchsucht werden soll.  

    2.  Geben Sie für jeden Speicherort Optionen an, von denen das Suchverhalten geändert wird.  

    3.  Geben Sie für jeden Speicherort ein Konto an, das als **Active Directory-Ermittlungskonto**verwendet werden soll.  

        > [!TIP]  
        >  Sie können für jeden Speicherort, den Sie angeben, einen Satz von Ermittlungsoptionen und ein eindeutiges Active Directory-Ermittlungskonto konfigurieren.  

    4.  Klicken Sie auf **OK** , um die Konfiguration des Active Directory-Containers zu speichern.  

6.  Konfigurieren Sie auf der Registerkarte Abfragezeitplan den Zeitplan für die vollständige Ermittlungsabfrage sowie die Deltaermittlung.  

7.  Optional können Sie auf der Registerkarte **Active Directory-Attribute** zusätzliche Active Directory-Attribute für Computer, die ermittelt werden sollen, konfigurieren. Es werden auch die Standardobjektattribute aufgelistet.  

8.  Optional können Sie auf der Registerkarte **Option** Optionen zum Herausfiltern oder Ausschließen veralteter Computerdatensätze von der Ermittlung konfigurieren.  

9. Wenn Sie mit dem Konfigurieren der Active Directory-Systemermittlung fertig sind, klicken Sie auf **OK**, um die Konfiguration zu speichern.  

#### <a name="to-configure-active-directory-user-discovery"></a>So konfigurieren Sie die Active Directory-Benutzerermittlung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** und anschließend auf **Ermittlungsmethoden**.  

2.  Wählen Sie die Methode **Active Directory-Benutzerermittlung** für den Standort aus, an dem die Ermittlung konfiguriert werden soll.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen zum Aktivieren der Ermittlung. Sie können die Ermittlung auch sofort konfigurieren und später aktivieren.  

5.  Klicken Sie auf das Symbol **Neu** ![Symbol Neu](media/Disc_new_Icon.gif), um einen neuen Active Directory-Container anzugeben. Führen Sie dann im Dialogfeld **Active Directory-Container** die folgenden Konfigurationsschritte aus:  

    1.  Geben Sie mindestens einen Speicherort an, der durchsucht werden soll.  

    2.  Geben Sie für jeden Speicherort Optionen an, von denen das Suchverhalten geändert wird.  

    3.  Geben Sie für jeden Speicherort ein Konto an, das als **Active Directory-Ermittlungskonto**verwendet werden soll.  

        > [!NOTE]  
        >  Sie können für jeden Speicherort, den Sie angeben, einen eindeutigen Satz von Ermittlungsoptionen und ein eindeutiges Active Directory-Ermittlungskonto konfigurieren.  

    4.  Klicken Sie auf **OK** , um die Konfiguration des Active Directory-Containers zu speichern.  

6.  Konfigurieren Sie auf der Registerkarte **Abfragezeitplan** den Zeitplan für die vollständige Ermittlungsabfrage sowie die Deltaermittlung.  

7.  Optional können Sie auf der Registerkarte **Active Directory-Attribute** zusätzliche Active Directory-Attribute für Computer, die ermittelt werden sollen, konfigurieren. Es werden auch die Standardobjektattribute aufgelistet.  

8.  Wenn Sie mit dem Konfigurieren der Active Directory-Systemermittlung fertig sind, klicken Sie auf **OK**, um die Konfiguration zu speichern.  

##  <a name="a-namebkmkconfighbdisca-configure-heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a> Konfigurieren einer Frequenzermittlung  
 Die Frequenzermittlung ist standardmäßig aktiviert, wenn Sie einen primären Configuration Manager-Standort installieren. Daher müssen Sie nur mithilfe eines Zeitplans festlegen, wie oft die Discovery Data Records (DDRs) der Frequenzermittlung von den Clients an einen Verwaltungspunkt gesendet werden sollen, wenn Sie nicht die Standardeinstellung „alle 7 Tage“ verwenden möchten.  

> [!NOTE]  
>  Wenn an einem Standort die Clientpushinstallation und der Standortwartungstask **Installationsflag löschen** zugleich aktiviert sind, legen Sie den Zeitplan für die Frequenzermittlung mit einem kürzeren Zeitraum als dem **Clientneuermittlungs-Zeitraum** des Standortwartungstasks **Installationsflag löschen** fest. Weitere Informationen zu Standortwartungstasks finden Sie unter [Wartungstasks für System Center Configuration Manager](../../../../core/servers/manage/maintenance-tasks.md).  

#### <a name="to-configure-the-heartbeat-discovery-schedule"></a>So konfigurieren Sie den Zeitplan für die Frequenzermittlung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration**, und anschließend auf **Ermittlungsmethoden**.  

2.  Wählen Sie **Frequenzermittlung** für den Standort, an dem die Frequenzermittlung konfiguriert werden soll, aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Konfigurieren Sie die Häufigkeit, mit der Discovery Data Records (DDRs) der Frequenzermittlung von den Clients übermittelt werden sollen, und klicken Sie auf **OK** , um die Konfiguration zu speichern.  

##  <a name="a-namebkmkconfignetworkdisca-configure-network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a> Konfigurieren einer Netzwerkermittlung  
 Verwenden Sie die Informationen in den folgenden Abschnitten zum Konfigurieren der Netzwerkermittlung.  

###  <a name="a-namebkmkaboutconfignetworkdisca-about-configuring-network-discovery"></a><a name="BKMK_AboutConfigNetworkDisc"></a> Informationen zum Konfigurieren der Netzwerkermittlung  
 Zum Konfigurieren der Netzwerkermittlung benötigen Sie die folgenden Informationen:  

-   Verfügbare Ebenen der Netzwerkermittlung  

-   Verfügbare Optionen der Netzwerkermittlung  

-   Begrenzen der Netzwerkermittlung im Netzwerk  

Weitere Informationen finden Sie im Abschnitt [Informationen zur Netzwerkermittlung](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutNetwork).  

 In den folgenden Abschnitten finden Sie Informationen zu häufig verwendeten Konfigurationen für die Netzwerkermittlung. Sie können eine oder mehrere dieser Konfigurationen innerhalb einer Ermittlungsausführung verwenden. Wenn Sie mehrere Konfigurationen verwenden, müssen Sie die Interaktionen berücksichtigen, durch die die Ermittlungsergebnisse beeinflusst werden können.  

 Beispielsweise möchten Sie möglicherweise alle SNMP-Geräte mit einem bestimmten öffentlichen SNMP-Namen ermitteln. Zusätzlich möchten Sie für diese Ermittlungsausführung möglicherweise die Ermittlung in einem bestimmten Subnetz deaktivieren. Wenn die Ermittlung ausgeführt wird, werden die SNMP-Geräte mit dem angegebenen öffentlichen Namen im deaktivierten Subnetz nicht ermittelt.  

####  <a name="a-namebkmkdeterminenettopologya-determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a> Bestimmen der Netzwerktopologie  
 Sie können eine topologiebezogene Ermittlung verwenden, um Ihr Netzwerk zuzuordnen. Von dieser Art der Ermittlung werden keine potenziellen Clients erkannt. Die topologiebezogene Netzwerkermittlung beruht auf SNMP.  

 Wenn Sie Ihre Netzwerktopologie zuordnen, müssen Sie im Dialogfeld **Netzwerkermittlung Eigenschaften** auf der Registerkarte **SNMP** die **Maximale Hopanzahl** konfigurieren. Bei einer geringen Hopanzahl ist es einfacher, die Netzwerkauslastung beim Ausführen der Ermittlung zu kontrollieren. Mit zunehmender Ermittlung des Netzwerks können Sie die Hopanzahl steigern, um sich ein besseres Bild von Ihrer Netzwerktopologie zu verschaffen.  

 Wenn Ihnen die Netzwerktopologie bekannt ist, können Sie zusätzliche Eigenschaften für die Netzwerkerkennung konfigurieren, um potenzielle Clients sowie deren Betriebssysteme zu ermitteln, während Sie verfügbare Konfigurationen zur Begrenzung der durchsuchbaren Netzwerksegmente verwenden.  

####  <a name="a-namebkmklimitbysubneta-limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a> Begrenzen von Suchvorgängen mithilfe von Subnetzen  
 Sie können die Netzwerkermittlung so konfigurieren, dass bestimmte Subnetze durchsucht werden, wenn eine Ermittlung ausgeführt wird. Standardmäßig wird von der Netzwerkermittlung das Subnetz des Servers, auf dem die Ermittlung ausgeführt wird, durchsucht. Für alle zusätzlichen Subnetze, die Sie konfigurieren und aktivieren, gelten nur die Suchoptionen von Simple Network Management Protocol (SNMP) und Dynamic Host Configuration Protocol (DHCP). Wenn von der Netzwerkermittlung Domänen durchsucht werden, gilt dabei keine konfigurierte Begrenzung auf Subnetze.  

 Wenn Sie im Dialogfeld **Netzwerkermittlung Eigenschaften** auf der Registerkarte **Subnetze** ein oder mehrere Subnetze angeben, werden nur die Subnetze durchsucht, die als **Aktiviert** gekennzeichnet sind.  

 Wenn Sie ein Subnetz deaktivieren, ist es von der Ermittlung ausgeschlossen, und es treffen die folgenden Bedingungen zu:  

-   SNMP-basierte Abfragen werden nicht auf dem Subnetz ausgeführt.  

-   Von DHCP-Servern wird keine Listen mit Ressourcen, die sich im Subnetz befinden, zurückgegeben.  

-   Von domänenbasierten Abfragen können Ressourcen im Subnetz ermittelt werden.  

####  <a name="a-namebkmksearchbydomaina-search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a> Durchsuchen einer bestimmten Domäne  
 Sie können die Netzwerkermittlung so konfigurieren, dass bei einer Ermittlungsausführung eine bestimmte Domäne oder ein bestimmter Domänensatz durchsucht wird. Standardmäßig wird von der Netzwerkermittlung die lokale Domäne des Servers, auf dem die Ermittlung ausgeführt wird, durchsucht.  

 Wenn Sie im Dialogfeld **Netzwerkermittlung Eigenschaften** auf der Registerkarte **Domänen** eine oder mehrere Domänen angeben, werden nur die Domänen durchsucht, die als **Aktiviert** gekennzeichnet sind.  

 Wenn Sie eine Domäne deaktivieren, ist sie von der Ermittlung ausgeschlossen, und es treffen die folgenden Bedingungen zu:  

-   Von der Netzwerkermittlung werden keine Domänencontroller in dieser Domäne abgefragt.  

-   SNMP-basierte Abfragen können auf Subnetzen in der Domäne weiterhin ausgeführt werden.  

-   Von DHCP-Servern werden weiterhin Listen mit Ressourcen in der Domäne zurückgegeben.  

####  <a name="a-namebkmklimitbysnmpnamea-limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a> Begrenzen von Suchvorgängen mithilfe von SNMP-Communitynamen  
 Sie können die Netzwerkermittlung so konfigurieren, dass eine bestimmte SNMP-Community oder ein bestimmter Communitysatz durchsucht wird, wenn eine Ermittlung ausgeführt wird. Standardmäßig ist der Communityname **Öffentlich** für die Verwendung konfiguriert.  

 Die Netzwerkermittlung verwendet Communitynamen für den Zugriff auf Router, bei denen es sich um SNMP-Geräte handelt. Von einem Router können Informationen zu verknüpften Routern und Subnetzen für die Netzwerkermittlung bereitgestellt werden.  

> [!NOTE]  
>  SNMP-Communitynamen sind mit Kennwörtern vergleichbar. Die Netzwerkermittlung kann nur Informationen von einem SNMP-Medium beziehen, für das Sie einen Communitynamen angegeben haben. Jedes SNMP-Gerät kann einen eigenen Communitynamen besitzen, oft verwenden jedoch mehrere Medien denselben Communitynamen. Zusätzlich haben die meisten SNMP-Geräte den Standardcommunitynamen **Öffentlich**. Von einigen Unternehmen wird der Communityname **Öffentlich** jedoch als Sicherheitsmaßnahme von den Geräten gelöscht.  

 Wenn im Dialogfeld **Netzwerkermittlung Eigenschaften** auf der Registerkarte **SNMP** mehrere SNMP-Communitys angezeigt werden, werden sie von der Netzwerkermittlung in der angezeigten Reihenfolge durchsucht. Sorgen Sie dafür, dass die meistverwendeten Namen sich oben auf der Liste befinden, um die Netzwerkauslastung durch Versuche, den Kontakt zu einem Gerät mithilfe verschiedener Namen herzustellen, möglichst gering zu halten.  

> [!NOTE]  
>  Zusätzlich zum SNMP-Communitynamen können Sie auch die IP-Adresse oder den auflösbaren Namen eines bestimmten SNMP-Geräts verwenden. Sie können die IP-Adresse oder den auflösbaren Namen eines bestimmten Geräts im Dialogfeld **Netzwerkermittlung Eigenschaften** auf der Registerkarte **SNMP-Geräte** konfigurieren.  

####  <a name="a-namebkmksearchbydhcpa-search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a> Durchsuchen eines bestimmten DHCP-Servers  
 Sie können die Netzwerkermittlung zur Verwendung eines oder mehrerer bestimmter DHCP-Server zum Ermitteln der DHCP-Clients konfigurieren.  

 Jeder DHCP-Server, den Sie im Dialogfeld **Netzwerkermittlung Eigenschaften** auf der Registerkarte **DHCP** angeben, wird von der Netzwerkermittlung durchsucht. Wenn die IP-Adresse durch den Server, von dem die Ermittlung ausgeführt wird, von einem DHCP-Server geleast wird, können Sie die Ermittlung für das Durchsuchen dieses DHCP-Servers konfigurieren, indem Sie das Kontrollkästchen **Den vom Standortserver verwendeten DHCP-Server einschließen** aktivieren.  

> [!NOTE]  
>  Zum erfolgreichen Konfigurieren eines DHCP-Servers für die Netzwerkermittlung ist es erforderlich, dass IPv4 von der Umgebung unterstützt wird. Sie können die Netzwerkermittlung nicht für die Verwendung eines DHCP-Servers in einer nativen IPv6-Umgebung konfigurieren.  

###  <a name="a-namebkmkhowtoconfignetdisca-how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a> Konfigurieren der Netzwerkermittlung  
 Wenden Sie die folgenden Verfahren an, um zunächst nur Ihre Netzwerktopologie zu ermitteln und die Netzwerkermittlung danach für das Ermitteln potenzieller Clients mithilfe einer oder mehrerer verfügbarer Netzwerkermittlungsoptionen zu konfigurieren.  

##### <a name="to-determine-your-network-topology"></a>So bestimmen Sie die Netzwerktopologie  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration**, und anschließend auf **Ermittlungsmethoden**.  

2.  Wählen Sie für den Standort, an dem die Netzwerkermittlung ausgeführt werden soll, **Netzwerkermittlung** aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

    -   Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen **Netzwerkermittlung aktivieren** , und wählen Sie dann aus den Optionen **Art der Ermittlung** die Option **Topologie** aus.  

    -   Aktivieren Sie auf der Registerkarte **Subnetze** das Kontrollkästchen **Lokale Subnetze durchsuchen** .  

        > [!TIP]  
        >  Wenn Ihnen die speziellen Subnetze des Netzwerks bekannt sind, können Sie das Kontrollkästchen **Lokale Subnetze durchsuchen** deaktivieren und über das Symbol **Neu** ![Symbol neu](media/Disc_new_Icon.gif) die Subnetze hinzufügen, die durchsucht werden sollen. Bei großen Netzwerken ist es oft sinnvoll, nur ein oder zwei Subnetze auf einmal zu durchsuchen, um die Netzwerkauslastung zu minimieren.  

    -   Aktivieren Sie auf der Registerkarte **Domänen** das Kontrollkästchen **Lokale Domäne durchsuchen** .  

    -   Verwenden Sie auf der Registerkarte **SNMP** die Dropdownliste **Maximale Hopanzahl** , um die Anzahl der Routerhops zu begrenzen, die von der Netzwerkermittlung bei der Zuordnung der Topologie ausgeführt werden können.  

        > [!TIP]  
        >  Für die erste Zuordnung Ihrer Netzwerktopologie konfigurieren Sie nur wenige Routerhops, um die Netzwerkauslastung zu minimieren.  

4.  Klicken Sie auf der Registerkarte **Zeitplan** auf das Symbol **Neu** ![Symbol Neu](media/Disc_new_Icon.gif), um einen Zeitplan für die Ausführung der Netzwerkermittlung festzulegen.  

    > [!NOTE]  
    >  Es ist nicht möglich, einzelnen Zeitplänen für die Netzwerkermittlung verschiedene Ermittlungskonfigurationen zuzuweisen. Bei jedem Ausführen der Netzwerkermittlung wird die aktuelle Ermittlungskonfiguration verwendet.  

5.  Klicken Sie auf **OK** , um die Konfigurationen zu übernehmen. Die Netzwerkermittlung wird zum geplanten Zeitpunkt ausgeführt.  

##### <a name="to-configure-network-discovery"></a>So konfigurieren Sie die Netzwerkermittlung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration**, und anschließend auf **Ermittlungsmethoden**.  

2.  Wählen Sie für den Standort, an dem die Netzwerkermittlung ausgeführt werden soll, **Netzwerkermittlung** aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen **Netzwerkermittlung aktivieren** , und wählen Sie dann aus den Optionen **Art der Ermittlung** die Art der auszuführenden Ermittlung aus.  

5.  Klicken Sie zum Konfigurieren der Ermittlung für das Durchsuchen von Subnetzen auf die Registerkarte **Subnetze** , und konfigurieren Sie ** ** dort eine oder mehrere der folgenden Optionen:  

    -   Aktivieren Sie das Kontrollkästchen **Lokale Subnetze durchsuchen** , um die Ermittlung in Subnetzen auszuführen, die sich lokal auf dem Computer befinden, von dem die Ermittlung ausgeführt wird.  

    -   Wenn ein bestimmtes Subnetz durchsucht werden soll, muss es unter **Zu durchsuchende Subnetze**aufgeführt sein, und der Wert **Suchen** muss **Aktiviert**lauten.  

        1.  Ist das Subnetz nicht aufgeführt, klicken Sie auf das Symbol **Neu** ![Symbol Neu](media/Disc_new_Icon.gif). Geben Sie im Dialogfeld **Neue Subnetzzuweisung** die Informationen zu **Subnetz** und **Maske** ein, und klicken Sie dann auf **OK**. Es wird standardmäßig ein neues Subnetz für die Suche aktiviert.  

        2.  Zum Ändern des Werts **Suchen** für ein aufgeführtes Subnetz wählen Sie das Subnetz aus und klicken dann auf das Symbol **Ein-/Ausschalten** , um zwischen **Deaktiviert** und **Aktiviert**zu wechseln.  

6.  Zum Konfigurieren der Ermittlung für das Durchsuchen von Domänen klicken Sie auf die Registerkarte **Domänen** und konfigurieren ** ** dort eine oder mehrere der folgenden Optionen:  

    -   Aktivieren Sie das Kontrollkästchen **Lokale Domäne durchsuchen** , um die Ermittlung in der Domäne des Computers auszuführen, von dem die Ermittlung ausgeführt wird.  

    -   Wenn eine bestimmte Domäne durchsucht werden soll, muss sie unter **Domänen** aufgeführt sein, und der Wert **Suchen** muss **Aktiviert**lauten.  

        1.  Ist die Domäne nicht aufgeführt, klicken Sie auf das Symbol **Neu** ![Symbol Neu](media/Disc_new_Icon.gif). Geben Sie im Dialogfeld **Domäneneigenschaften** Informationen zur **Domäne** ein, und klicken Sie anschließend auf **OK**. Es wird standardmäßig eine neue Domäne für die Suche aktiviert.  

        2.  Zum Ändern des Werts **Suchen** für eine aufgeführte Domäne wählen Sie die Domäne aus und klicken dann auf das Symbol **Ein-/Ausschalten** , um zwischen **Deaktiviert** und **Aktiviert**zu wechseln.  

7.  Zum Konfigurieren der Ermittlung für das Durchsuchen bestimmter SNMP-Communitynamen für SNMP-Geräte klicken Sie auf die Registerkarte **SNMP** und konfigurieren ** ** dort eine oder mehrere der folgenden Optionen:  

    -   Wenn Sie der Liste **SNMP-Communitynamen** einen SNMP-Communitynamen hinzufügen möchten, klicken Sie auf das Symbol **Neu** ![Symbol Neu](media/Disc_new_Icon.gif), geben im Dialogfeld **Neuer öffentlicher SNMP-Name** den **Namen** der SNMP-Community an, und klicken anschließend auf **OK**.  

    -   Wenn Sie einen SNMP-Communitynamen entfernen möchten, wählen Sie den Namen aus und klicken anschließend auf das Symbol **Löschen** ![Symbol Löschen](media/Disc_delete_Icon.gif).  

    -   Wenn Sie die Suchreihenfolge der SNMP-Communitynamen ändern möchten, wählen Sie einen Namen aus und klicken auf das Symbol **Nach oben** ![Symbol Nach oben](media/Disc_moveUp_Icon.gif) bzw. auf das Symbol **Nach unten** ![Symbol Nach unten](media/Disc_moveDown_Icon.gif). Beim Ausführen der Ermittlung werden die Communitynamen von oben nach unten durchsucht.  

        > [!NOTE]  
        >  Die Netzwerkermittlung greift anhand von SMS-Communitynamen auf Router zu, bei denen es sich um SNMP-Geräte handelt. Die Netzwerkermittlung kann von einem Router über mit diesem verknüpfte Router und Subnetze informiert werden.  

        -   SNMP-Communitynamen sind mit Kennwörtern vergleichbar.  

        -   Die Netzwerkermittlung kann nur Informationen von einem SNMP-Medium beziehen, für das Sie einen Communitynamen angegeben haben.  

        -   Jedes SNMP-Gerät kann einen eigenen Communitynamen haben. Oft wird jedoch derselbe Communityname von mehreren Geräten verwendet.  

        -   Die meisten SNMP-Geräte haben den Standardcommunitynamen **Öffentlich** . Dieser Name kann verwendet werden, wenn Ihnen keine anderen Communitynamen bekannt sind. Von einigen Unternehmen wird der Communityname **Öffentlich** jedoch als Sicherheitsmaßnahme von den Geräten gelöscht.  

8.  Zum Konfigurieren der maximalen Anzahl von Routerhops bei SNMP-Suchen klicken Sie auf die Registerkarte **SNMP** und wählen ** ** dort die gewünschte Anzahl aus der Dropdownliste **Maximale Hopanzahl** aus.  

9. Zum Konfigurieren von **SNMP-Geräten** klicken Sie auf die Registerkarte **SNMP-Geräte**, und anschließend auf die Registerkarte **SNMP**. Wenn das Gerät dort nicht aufgeführt ist, klicken Sie auf das Symbol **Neu** ![Symbol Neu](media/Disc_new_Icon.gif). Geben Sie im Dialogfeld **Neues SNMP-Gerät** die IP-Adresse oder den Gerätenamen des SNMP-Geräts ein, und klicken Sie dann auf **OK**.  

    > [!NOTE]  
    >  Wenn Sie einen Gerätenamen angeben, muss der NetBIOS-Name von Configuration Manager in eine IP-Adresse aufgelöst werden können.  

10. Zum Konfigurieren der Ermittlung für die Abfrage bestimmter DHCP-Server für DHCP-Clients klicken Sie auf die Registerkarte **DHCP** und konfigurieren ** ** dort eine oder mehrere der folgenden Optionen:  

    -   Wenn der DHCP-Server auf dem Computer, auf dem die Ermittlung ausgeführt wird, abgefragt werden soll, aktivieren Sie das Kontrollkästchen **Immer den DHCP-Server des Standortservers verwenden** .  

        > [!NOTE]  
        >  Dabei ist es erforderlich, dass die IP-Adresse durch den Server von einem DHCP-Server geleast wird. Es kann keine statische IP-Adresse verwendet werden.  

    -   Wenn ein bestimmter DHCP-Server abgefragt werden soll, klicken Sie auf das Symbol **Neu** ![Symbol Neu](media/Disc_new_Icon.gif), geben im Dialogfeld **Neuer DHCP-Server** die IP-Adresse bzw. den Servernamen des DHCP-Servers an, und klicken anschließend auf **OK**.  

        > [!NOTE]  
        >  Wenn Sie einen Servernamen angeben, muss der NetBIOS-Name von Configuration Manager in eine IP-Adresse aufgelöst werden können.  

11. Konfigurieren Sie, wann die Ermittlung ausgeführt werden soll, indem Sie auf die Registerkarte **Zeitplan** klicken. Klicken Sie auf der Registerkarte **Zeitplan** dann auf das Symbol **Neu** ![Symbol Neu](media/Disc_new_Icon.gif) klicken, um einen Zeitplan für die Ausführung der Netzwerkermittlung festzulegen.  

     Sie können mehrere Zeitpläne für die Netzwerkermittlung konfigurieren, darunter wiederkehrende und nicht wiederkehrende Zeitpläne.  

    > [!NOTE]  
    >  Wenn auf der Registerkarte **Zeitplan** mehrere Zeitpläne zugleich angezeigt werden, werden die Netzwerkermittlungen zu den darin angegebenen Zeiten entsprechend den Konfigurationen ausgeführt. Dies gilt auch für Zeitpläne mit Wiederholung.  

12. Klicken Sie auf **OK** , um die Konfigurationen zu speichern.  

###  <a name="a-namebkmkhowtoverifynetdisca-how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a> Überprüfen, ob die Netzwerkermittlung abgeschlossen ist  
 Die Zeit, die für die Netzwerkermittlung erforderlich ist, wird von zahlreichen Faktoren beeinflusst. Folgende Faktoren können die Dauer beeinflussen:  

-   Die Größe des Netzwerks  

-   Die Topologie des Netzwerks  

-   Die maximale Anzahl von Hops, die zum Suchen von Routern im Netzwerk konfiguriert ist  

-   Die Art der Ermittlung, die ausgeführt wird  

Von der Netzwerkermittlung werden keine Meldungen über den Abschluss der Ermittlung erstellt. Sie können mithilfe des folgenden Verfahrens überprüfen, ob die Ermittlung abgeschlossen ist.  

##### <a name="to-verify-that-network-discovery-has-finished"></a>So überprüfen Sie, ob die Netzwerkermittlung abgeschlossen ist  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** die Option **Systemstatus**, und klicken Sie dann auf **Statusmeldungsabfragen**.  

3.  Wählen Sie **Alle Statusmeldungen**aus.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Statusmeldungsabfragen** auf **Meldungen anzeigen**.  

5.  Wählen Sie in der Dropdownliste **Datum und Uhrzeit auswählen** einen Wert aus, der berücksichtigt, wie viel Zeit seit dem Start der Ermittlung vergangen ist. Klicken Sie dann auf **OK** , um die **Configuration Manager-Statusmeldungsanzeige**zu öffnen.  

    > [!TIP]  
    >  Mithilfe der Option **Datum und Uhrzeit angeben** können Sie auch den Zeitpunkt (Datum und Uhrzeit) auswählen, zu dem die Ermittlung ausgeführt wurde. Diese Option ist nützlich, wenn Sie die Netzwerkermittlung an einem bestimmten Termin ausgeführt haben und nur Meldungen von diesem Datum abrufen möchten.  

6.  Suchen Sie nach einer Statusmeldung mit den folgenden Details, um zu überprüfen, ob die Netzwerkermittlung abgeschlossen ist:  

    -   Meldungs-ID: **502**  

    -   Komponente: **SMS_NETWORK_DISCOVERY**  

    -   Beschreibung: **Diese Komponente wurde beendet.**  

    Wenn diese Statusmeldung nicht vorhanden ist, ist die Netzwerkermittlung nicht abgeschlossen.  

7.  Suchen Sie nach einer Statusmeldung mit den folgenden Details, um zu überprüfen, wann die Netzwerkermittlung gestartet wurde:  

    -   Meldungs-ID: **500**  

    -   Komponente: **SMS_NETWORK_DISCOVERY**  

    -   Beschreibung: **Diese Komponente wurde gestartet.**  

    Dadurch wird bestätigt, dass die Netzwerkermittlung gestartet wurde. Wenn diese Informationen fehlen, planen Sie die Netzwerkermittlung neu.  



<!--HONumber=Dec16_HO3-->


