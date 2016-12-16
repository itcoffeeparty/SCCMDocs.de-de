---
title: Definieren von Standortgrenzen |System Center Configuration Manager
description: "Hier erfahren Sie, wie Sie Netzwerkadressen in Ihrem Internet festlegen können. Diese können Geräte umfassen, die Sie verwalten möchten"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9df8b5d5fd67a5ced5860771295d05dfb56a3982


---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Definieren von Standortgrenzen und Begrenzungsgruppen für Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mithilfe von Grenzen für System Center Configuration Manager werden Netzwerkadressen in Ihrem Intranet definiert, die Geräte enthalten können, die Sie verwalten möchten. Begrenzungsgruppen sind logische Gruppen von Grenzen, die Sie konfigurieren. Begrenzungsgruppen und Grenzen sind in der gesamten Hierarchie verfügbar und werden nicht für einzelne Standorte konfiguriert.  

 Eine Hierarchie kann eine beliebige Anzahl von Begrenzungsgruppen enthalten, und jede Begrenzungsgruppe kann eine beliebige Kombination der folgenden Grenztypen enthalten:  

-   IP-Subnetz,  

-   Active Directory-Standortname  

-   IPv6-Präfix  

-   IP-Adressbereich  

Clients im Intranet bewerten ihre aktuelle Adresse im Netzwerk und bestimmen anhand dieser Informationen Begrenzungsgruppen, zu denen sie gehören.  

 Clients nutzen Begrenzungsgruppen für folgende Zwecke:  

-   **Suchen eines zugewiesenen Standorts:** Mithilfe von Begrenzungsgruppen können Clients einen primären Standort für die Clientzuweisung finden (automatische Standortzuweisung).  

-   **Suchen bestimmter Standortsystemrollen, die Sie verwenden können:**  Wenn Sie eine Begrenzungsgruppe bestimmten Standortsystemrollen zuordnen, bietet die Begrenzungsgruppe Clients eine Liste mit Standortsystemen, die während der Inhaltssuche und als bevorzugte Verwaltungspunkte verwendet werden sollen.  

Von Clients, die sich im Internet befinden oder nur für Internetverbindungen konfiguriert sind, werden keine Begrenzungsinformationen verwendet. Die automatische Standortzuweisung kann von diesen Clients nicht verwendet werden. Wenn der Verteilungspunkt für das Zulassen von Clientverbindungen aus dem Internet konfiguriert ist, werden Inhalte stets von einem beliebigen Verteilungspunkt im Standort heruntergeladen, der dem Client zugeordnet ist.  


##  <a name="a-namebkmkboundariesa-boundaries"></a><a name="BKMK_Boundaries"></a> Standortgrenzen  
 Sie können einzelne Grenzen manuell erstellen. Darüber hinaus können Sie [Active Directory Forest Discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) für die automatische Erkennung und Erstellung von Grenzen für jeden erkannten IP-Subnetze und Active Directory-Standort konfigurieren.  

-   Jede Grenze stellt eine Netzwerkadresse dar und ist an jedem Standort der Hierarchie verfügbar.  

-   In Configuration Manager wird die direkte Eingabe eines Supernetzes als Grenze nicht unterstützt. Verwenden Sie stattdessen den Grenztyp IP-Adressbereich.  

-   Wenn von der Active Directory-Gesamtstrukturermittlung ein Supernetz identifiziert wird, das einem Active Directory-Standort zugewiesen ist, konvertiert Configuration Manager das Supernetz in eine Grenze vom Typ IP-Adressbereich.  

-   Die Grenze, auf der sich ein Client befindet, entspricht dem Active Directory-Standort oder der Netzwerk-IP-Adresse, die den Client identifiziert. (Es ist nicht ungewöhnlich, dass ein Client eine IP-Adresse verwendet, die dem Configuration Manager-Administrator unbekannt ist. Wenn die Netzwerkadresse des Clients zweifelhaft ist, prüfen Sie, was der Client als seine Adresse meldet, indem Sie den Befehl **IPCONFIG** auf dem Client aufrufen.)  

Wenn Sie eine Grenze erstellen, erhält sie automatisch einen Namen, der auf dem Typ und Bereich der Grenze basiert. Dieser Name kann nicht geändert werden. Geben Sie stattdessen beim Konfigurieren der Grenze eine Beschreibung an, anhand derer Sie die Grenze in der Configuration Manager-Konsole identifizieren können.  

 Sie können die Eigenschaften einer vorhandenen Grenze zu folgenden Zwecken ändern:  

-   Hinzufügen der Grenze zu einer oder mehreren Begrenzungsgruppen  

-   Ändern des Typs oder des Bereichs der Grenze  

-   Anzeigen der Registerkarte **Standortsysteme** für die Grenze, um festzustellen, welche Standortsystemserver (Verteilungspunkte, Zustandsmigrationspunkte und Verwaltungspunkte) der Grenze zugeordnet sind.  

#### <a name="to-create-a-boundary"></a>So erstellen Sie eine Grenze  

1.  Klicken Sie in der Configuration Manager-Konsole auf**Verwaltung** > **Hierarchiekonfiguration** > **Grenzen**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Erstellen Boundary.**.  

3.  Auf der Registerkarte **Allgemein** des Dialogfelds **Grenze erstellen** können Sie eine Beschreibung angeben, um die Grenze anhand eines Anzeigenamens oder einer Referenz zu identifizieren.  

4.  Wählen Sie einen **Typ** für diese Grenze aus:  

    -   Bei Auswahl von **IP-Subnetz**müssen Sie eine **Subnetz-ID** für diese Grenze angeben.  

        > [!TIP]  
        >  Sie können **Netzwerk** und **Subnetzmaske** angeben, um die **Subnetz-ID** automatisch zuordnen zu lassen. Wenn Sie die Grenze speichern, wird nur der Wert für die Subnetz-ID gespeichert.  

    -   Bei Auswahl von **Active Directory-Standort**müssen Sie in der lokalen Gesamtstruktur des Standortservers einen Active Directory-Standort angeben oder durch Klicken auf **Durchsuchen** auswählen.  

        > [!IMPORTANT]  
        >  Wenn Sie einen Active Directory-Standort für eine Grenze angeben, umfasst die Grenze alle IP-Subnetze, die Mitglieder dieses Active Directory-Standorts sind. Wenn die Konfiguration des Active Directory-Standorts in Active Directory geändert wird, werden auch die in dieser Grenze enthaltenen Netzwerkorte geändert.  

    -   Bei Auswahl von **IPv6-Präfix**müssen Sie ein **Präfix** im IPv6-Präfixformat angeben.  

    -   Bei Auswahl von **IP-Adressbereich**müssen Sie eine **IP-Startadresse** und eine **IP-Endadresse** angeben, die einen Teil eines IP-Subnetzes oder mehrere IP-Subnetze abdeckt.  

5.  Klicken Sie auf **OK** , um die neue Grenze zu speichern.  

#### <a name="to-configure-a-boundary"></a>So konfigurieren Sie eine Grenze  

1.  Klicken Sie in der Configuration Manager-Konsole auf**Verwaltung** > **Hierarchiekonfiguration** > **Grenzen**.  

2.  Wählen Sie die Grenze aus, die Sie ändern möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Wählen Sie im Dialogfeld **Eigenschaften** für die Grenze die Registerkarte **Allgemein** aus, um die **Beschreibung** oder den **Typ** der Grenze zu bearbeiten. Sie können darüber hinaus den Bereich einer Grenze ändern, indem Sie die Netzwerkorte für die Grenze bearbeiten. Sie können beispielsweise für eine Active Directory-Standortgrenze einen neuen Active Directory-Standortnamen angeben.  

5.  Wählen Sie die Registerkarte **Standortsysteme** aus, um die Standortsysteme anzuzeigen, die dieser Grenze zugeordnet sind. Diese Konfiguration kann nicht über die Eigenschaften einer Grenze geändert werden.  

    > [!TIP]  
    >  Ein Standortsystemserver wird nur dann als Standortsystem für eine Grenze aufgelistet, wenn der Standortsystemserver als solcher mindestens einer Begrenzungsgruppe zugeordnet ist, in der diese Grenze enthalten ist. Dies wird auf der Registerkarte **Referenzen** einer Begrenzungsgruppe konfiguriert.  

6.  Wählen Sie die Registerkarte **Begrenzungsgruppen** aus, um die Begrenzungsgruppenmitgliedschaft für diese Grenze zu ändern:  

    -   Wenn Sie Begrenzungsgruppen diese Grenze hinzufügen möchten, klicken Sie auf **Hinzufügen**, aktivieren Sie das Kontrollkästchen für die betreffende(n) Begrenzungsgruppe(n), und klicken Sie dann auf **OK**.  

    -   Wenn Sie diese Grenze aus einer Begrenzungsgruppe entfernen möchten, wählen Sie die Begrenzungsgruppe aus, und klicken Sie auf **Entfernen**.  

7.  Klicken Sie auf **OK** , um die Eigenschaften der Grenze zu schließen und die Konfiguration zu speichern.  

##  <a name="a-namebkmkboundarygroupsa-boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Boundary groups  
 Sie erstellen Begrenzungsgruppen zum logischen Gruppieren zusammenhängender Netzwerkadressen (Grenzen), um die Verwaltung Ihrer Infrastruktur zu erleichtern. Sie müssen einer Begrenzungsgruppe zunächst Grenzen hinzufügen, damit Sie die Begrenzungsgruppe verwenden können. Clients verwenden die Konfiguration der Begrenzungsgruppe für folgende Zwecke:  

-   Automatische Standortzuweisung  

-   Inhaltsort  

-   Bevorzugte Verwaltungspunkte (wenn Sie bevorzugte Verwaltungspunkte verwenden möchten, müssen Sie diese Option für die Hierarchie und nicht in der Konfiguration der Begrenzungsgruppe aktivieren. Weitere Informationen finden Sie im folgenden Verfahren: *So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte*).  

Beim Konfigurieren von Begrenzungsgruppen fügen Sie der Begrenzungsgruppe eine oder mehrere Grenzen hinzu und konfigurieren dann zusätzliche Einstellungen für Clients, die sich auf diesen Grenzen befinden.  

#### <a name="to-create-a-boundary-group"></a>So erstellen Sie eine Begrenzungsgruppe  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Begrenzungsgruppe erstellen**.  

3.  Wählen Sie im Dialogfeld **Begrenzungsgruppe erstellen** die Registerkarte **Allgemein** aus, und geben Sie unter **Name** einen Namen für diese Begrenzungsgruppe an.  

4.  Klicken Sie auf **OK** , um die neue Begrenzungsgruppe zu speichern.  

#### <a name="to-configure-a-boundary-group"></a>So konfigurieren Sie eine Begrenzungsgruppe  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

2.  Wählen Sie die Begrenzungsgruppe aus, die Sie ändern möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Wählen Sie im Dialogfeld **Eigenschaften** für die Begrenzungsgruppe die Registerkarte **Allgemein** aus, um die Grenzen zu ändern, die Mitglieder dieser Begrenzungsgruppe sind.  

    -   Wenn Sie Grenzen hinzufügen möchten, klicken Sie auf **Hinzufügen**, aktivieren Sie das Kontrollkästchen für eine oder mehrere Grenzen, und klicken Sie dann auf **OK**.  

    -   Wenn Sie Grenzen entfernen möchten, wählen Sie die Grenze aus, und klicken Sie auf **Entfernen**.  

5.  Wählen Sie die Registerkarte **Referenzen** aus, um die Konfiguration für Standortzuweisung und zugeordnete Standortsystemserver zu ändern:  

    -   Aktivieren Sie das Kontrollkästchen **Diese Begrenzungsgruppe für die Standortzuweisung verwenden**, und wählen Sie dann aus der Dropdownliste **Zugewiesener Standort** einen Standort aus, damit Clients diese Begrenzungsgruppe für die Standortzuweisung verwenden können.  

    -   Um zu konfigurieren, welche verfügbaren Standortsystemserver dieser Begrenzungsgruppe zugeordnet sind, gehen Sie wie folgt vor:  

    1.  Klicken Sie auf **Hinzufügen**, und aktivieren Sie dann das Kontrollkästchen für einen oder mehrere Server. Die Server werden als zugeordnete Standortsystemserver für diese Begrenzungsgruppe hinzugefügt. Nur Server, auf denen die unterstützte Standortsystemrolle installiert ist, sind verfügbar.  

        > [!NOTE]  
        >  Sie können eine beliebige Kombination verfügbarer Standortsysteme von einem beliebigen Standort in der Hierarchie auswählen. Ausgewählte Standortsysteme werden in den Eigenschaften jeder Grenze, die dieser Begrenzungsgruppe angehört, auf der Registerkarte **Standortsysteme** aufgelistet.  

    2.  Wenn Sie einen Server aus dieser Begrenzungsgruppe entfernen möchten, wählen Sie den Server aus, und klicken Sie dann auf **Entfernen**.  

        > [!NOTE]  
        >  Wenn diese Begrenzungsgruppe nicht mehr zum Zuordnen von Standortsystemen verwendet werden soll, müssen Sie alle Server entfernen, die als zugeordnete Standortsystemserver aufgelistet sind.  

    3.  Wenn Sie die Netzwerkverbindungsgeschwindigkeit eines Standortsystemservers für diese Begrenzungsgruppe ändern möchten, wählen Sie den Server aus, und klicken Sie dann auf **Verbindung ändern**.  

         Die Standardeinstellung für die Verbindungsgeschwindigkeit lautet für alle Standortsysteme **Schnell**, sie kann aber auch in **Langsam**geändert werden. Über die Netzwerkverbindungsgeschwindigkeit und die Konfiguration einer Bereitstellung wird festgelegt, ob ein Client Inhalte vom Server herunterladen kann.  

6.  Klicken Sie auf **OK** , um die Eigenschaften der Begrenzungsgruppe zu schließen und die Konfiguration zu speichern.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>So ordnen Sie einen Inhaltsbereitstellungsserver oder Verwaltungspunkt einer Begrenzungsgruppe zu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

2.  Wählen Sie die Begrenzungsgruppe aus, die Sie ändern möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Wählen Sie im Dialogfeld **Eigenschaften** für die Begrenzungsgruppe die Registerkarte **Referenzen** aus.  

5.  Klicken Sie unter **Standortsystemserver auswählen**auf **Hinzufügen**, aktivieren Sie das Kontrollkästchen für die Standortsystemserver, die dieser Begrenzungsgruppe zugeordnet werden sollen, und klicken Sie dann auf **OK**.  

6.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen und die Konfiguration der Begrenzungsgruppe zu speichern.  

#### <a name="to-enable-use-of-preferred-management-points"></a>So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie anschließend **Hierarchieeinstellungen**auf der Registerkarte **Start** aus.  

2.  Wählen Sie im Dialogfeld „Hierarchieeinstellungen“ auf der Registerkarte **Allgemein** die Option **Clients bevorzugen die in Begrenzungsgruppen angegebenen Verwaltungspunkte**.  

3.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen und die Konfiguration zu speichern.  

#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>So konfigurieren Sie einen Fallbackstandort für die automatische Standortzuweisung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** >  **Standorte**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.  

3.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen **Fallbackstandort verwenden**, und wählen Sie dann in der Dropdownliste **Fallbackstandort** einen Standort aus.  

4.  Klicken Sie auf **OK** , um die Konfiguration zu speichern.  

 In den folgenden Abschnitten finden Sie zusätzliche Informationen zu Konfigurationen von Begrenzungsgruppen.  

###  <a name="a-namebkmkboundarysiteassignmenta-about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Informationen zur Standortzuweisung  
 Sie können jede Begrenzungsgruppe mit einem zugewiesenen Standort für Clients konfigurieren.  

-   Ein neu installierter Client, der die automatische Standortzuweisung verwendet, tritt dem zugewiesenen Standort einer Begrenzungsgruppe bei, die die aktuelle Netzwerkadresse des Clients enthält.  

-   Nach Zuweisung zu einem Standort ändert sich die Standortzuweisung eines Clients nicht, wenn sich seine Netzwerkadresse ändert. Beim Wechseln des Clients zu einer neuen Netzwerkadresse, die von einer Grenze in einer Begrenzungsgruppe mit abweichender Standortzuweisung repräsentiert wird, bleibt der dem Client zugewiesene Standort unverändert.  

-   Wenn mithilfe von Active Directory-Systemermittlung eine neue Ressource ermittelt wird, werden die Netzwerkinformationen für diese Ressource anhand der Grenzen in Begrenzungsgruppen bewertet. Dabei wird die neue Ressource einem zugewiesenen Standort zur Verwendung bei einer Clientpushinstallation zugeordnet.  

-   Wenn eine Grenze zu mehreren Begrenzungsgruppen gehört, denen verschiedene Standorte zugewiesen sind, wählen die Clients einen dieser Standorte nach dem Zufallsprinzip aus.  

-   Änderungen an dem zugewiesenen Standort einer Begrenzungsgruppe betreffen nur neue Standortzuweisungsaktionen. Clients, die bereits einem Standort zugewiesen sind, bewerten ihre Standortzuweisung nicht basierend auf Änderungen an der Konfiguration einer Begrenzungsgruppe (oder ihrer eigenen Netzwerkadresse) neu.  

Weitere Informationen zur automatischen Standortzuweisung finden Sie unter [Verwenden von automatischen Standortzuweisungen für Computer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [Zuweisen von Clients zu einem Standort in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="a-namebkmkboundarycontentlocationa-about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Informationen zu Inhaltsorten  
 Sie können jede Begrenzungsgruppe mit einem oder mehreren Verteilungspunkten und Zustandsmigrationspunkten konfigurieren. Ferner können Sie dieselben Verteilungspunkte und Zustandsmigrationspunkte mehreren Begrenzungsgruppen zuordnen.  

-   **Während der Softwareverteilung**fordern Clients einen Speicherort für Bereitstellungsinhalte an. Configuration Manager sendet dem Client eine Liste der Verteilungspunkte, die den einzelnen Begrenzungsgruppen zugeordnet sind, die den aktuellen Netzwerkort des Clients einbeziehen.  

-   **Während der Bereitstellung des Betriebssystems** fordern Clients einen Speicherort zum Senden oder Empfangen ihrer Zustandsmigrationsinformationen an. Configuration Manager sendet dem Client eine Liste der Zustandsmigrationspunkte, die den einzelnen Begrenzungsgruppen zugeordnet sind, die den aktuellen Netzwerkort des Clients einbeziehen.  

So kann von den Clients der am nächsten liegende Server zur Übertragung der Inhalts- oder Zustandsmigrationsinformationen ausgewählt werden.  

###  <a name="a-namebkmkpreferredmpa-about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Informationen zu bevorzugten Verwaltungspunkten  
 Bevorzugte Verwaltungspunkte ermöglichen einem Client die Identifikation eines Verwaltungspunkts, der seiner aktuellen Netzwerkadresse (oder Begrenzung) zugeordnet ist.  

-   Ein Client versucht zunächst, einen bevorzugten Verwaltungspunkt seines zugewiesenen Standorts zu verwenden, bevor er einen Verwaltungspunkt seines zugewiesenen Standorts verwendet, der nicht als bevorzugt konfiguriert wurde.  

-   Um diese Option verwenden zu können, müssen Sie sie für die Hierarchie aktivieren und Begrenzungsgruppen an den einzelnen primären Standorten konfigurieren, die die Verwaltungspunkte enthalten, die den Grenzen dieser Begrenzungsgruppe zugeordnet sein sollen.  

-   Wenn bevorzugte Verwaltungspunkte konfiguriert werden und ein Client seine Liste der Verwaltungspunkte organisiert, platziert er die bevorzugten Verwaltungspunkte ganz oben in der Liste der zugewiesenen Verwaltungspunkte (die alle Verwaltungspunkte des zugewiesenen Standorts des Clients enthält)  

> [!NOTE]  
>  Wenn ein Client seinen Standort wechselt (d. h. sich seine Netzwerkadresse ändert, wenn beispielsweise ein Laptop an einem Remotestandort mit dem Netzwerk verbunden wird), kann er einen Verwaltungspunkt (bzw. Proxyverwaltungspunkt) des lokalen Standorts verwenden, bevor versucht wird, einen Verwaltungspunkt seines zugewiesenen Standorts zu verwenden (was die bevorzugten Verwaltungspunkte einschließt).  Weitere Informationen finden Sie unter [Understand how clients find site resources and services for System Center Configuration Manager (Verstehen, wie Clients Standortressourcen und -dienste für System Center Configuration Manager suchen)](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

###  <a name="a-namebkmkboundaryoverlapa-about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Informationen zu überlappenden Grenzen  
 Bei der Abfrage von Inhaltsorten werden überlappende Grenzkonfigurationen von Configuration Manager unterstützt:  

-   **Wenn ein Client Inhalt anfordert**und die Netzwerkadresse des Clients zu mehreren Begrenzungsgruppen gehört, erhält der Client von Configuration Manager eine Liste mit allen Verteilungspunkten, die über diesen Inhalt verfügen.  

-   **Wenn von einem Client Zustandsmigrationsinformationen bei einem Server angefordert bzw. an diesen gesendet werden**und das Netzwerk des Clients Mitglied mehrerer Begrenzungsgruppen ist, erhält der Client von Configuration Manager eine Liste mit allen Zustandsmigrationspunkten, die einer Begrenzungsgruppe mit der aktuellen Netzwerkadresse des Clients zugeordnet sind.  

So kann von den Clients der am nächsten liegende Server zur Übertragung der Inhalts- oder Zustandsmigrationsinformationen ausgewählt werden.  

###  <a name="a-namebkmkboudnarynetworkspeeda-about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> Informationen zur Netzwerkverbindungsgeschwindigkeit  
 Sie können die Netzwerkverbindungsgeschwindigkeit für jeden Standortsystemserver in einer Begrenzungsgruppe festlegen. Diese Einstellung gilt für Clients, die sich mit einem Standortsystem basierend auf dieser Konfiguration von Begrenzungsgruppen verbinden. Der gleiche Standortsystemserver kann in verschiedenen Begrenzungsgruppen unterschiedliche Verbindungsgeschwindigkeiten aufweisen.  

 Für die Netzwerkverbindungsgeschwindigkeit ist standardmäßig die Einstellung **Schnell**festgelegt, es kann aber auch **Langsam**festgelegt werden. Anhand der Netzwerkverbindungsgeschwindigkeit und der Bereitstellungskonfiguration wird festgelegt, ob Inhalt von Verteilungspunkten heruntergeladen werden kann, wenn der betreffende Client Mitglied in einer zugeordneten Begrenzungsgruppe ist.  

 Weitere Informationen zum Einfluss der Netzwerkverbindungsgeschwindigkeit auf den Inhaltsabruf durch Clients finden Sie unter [Quellspeicherortszenarios für Inhalte](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

##  <a name="a-namebkmkboundarybestpracticesa-best-practices-for-boundaries"></a><a name="BKMK_BoundaryBestPractices"></a> Bewährte Methoden für Grenzen  

-   **Ziehen Sie die Verwendung des Grenztyps „IP-Adressbereich“ nur dann in Betracht, wenn andere Grenztypen nicht verwendet werden können:**  

     Beim Entwerfen Ihrer Grenzstrategie ist es empfehlenswert, auf Active Directory-Standorten basierenden Grenzen den Vorzug vor anderen Grenztypen einzuräumen. Falls Grenzen auf Basis von Active Directory-Standorten nicht infrage kommen, verwenden Sie das IP-Subnetz oder IPv6 für die Definition von Grenzen. Steht keine dieser Optionen offen, nutzen Sie die Grenzen des Typs „IP-Adressbereich“. Grund hierfür ist die Tatsache, dass die Grenzmitglieder am Standort in regelmäßigen Abständen ausgewertet werden und für die Abfrage zur Auswertung der Mitglieder eines IP-Adressbereichs die SQL-Serverressourcen in deutlich höherem Ausmaß beansprucht werden als für Abfragen zu Mitgliedern anderer Grenztypen.  

-   **Vermeiden Sie überlappende Grenzen bei der automatischen Standortzuweisung:**  

     Obwohl jede Begrenzungsgruppe sowohl Konfigurationen der Standortzuweisung als auch für die Inhaltssuche unterstützt, ist es eine bewährte Methode, einen getrennten Satz von Begrenzungsgruppen nur für die Standortzuweisung zu nutzen. Achten Sie also darauf, dass in einer Begrenzungsgruppe enthaltene Grenzen nicht gleichzeitig einer anderen Begrenzungsgruppe mit abweichender Standortzuweisung angehören. Der Grund ist wie folgt:  

    -   Eine einzelne Grenze kann zu mehreren Begrenzungsgruppen gehören.  

    -   Jede Begrenzungsgruppe kann für die Standortzuweisung einem anderen primären Standort zugeordnet werden.  

    -   Ein Client auf einer Grenze, die zu zwei verschiedenen Begrenzungsgruppen mit unterschiedlichen Standortzuweisungen gehört, wählt für den Beitritt zu einem Standort das Zufallsprinzip, wobei dies ggf. nicht der Standort ist, dem der Client beitreten möchte.  Diese Konfiguration wird als überlappende Grenzen bezeichnet.  

     Überlappende Grenzen sind kein Problem für die Inhaltssuche und stattdessen häufig eine gewünschte Konfiguration, um Clients zusätzliche Ressourcen oder Inhaltsorte zu bieten, die sie verwenden können.  



<!--HONumber=Nov16_HO1-->


