---
title: Definieren von Standortgrenzen | Microsoft-Dokumentation
description: "Hier erfahren Sie, wie Sie Netzwerkadressen in Ihrem Internet festlegen können. Diese können Geräte umfassen, die Sie verwalten möchten"
ms.custom: na
ms.date: 12/15/2016
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
ms.sourcegitcommit: edc406adf1fdfab8e821b63dc02f37a30504ecd3
ms.openlocfilehash: 6135a94e30e8cce8ed4b8d08e5de26c15988b195


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

### <a name="to-create-a-boundary"></a>So erstellen Sie eine Grenze  

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

### <a name="to-configure-a-boundary"></a>So konfigurieren Sie eine Grenze  

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
> [!IMPORTANT]  
>  **Die Informationen in diesem Begrenzungsgruppen-Abschnitt und seinen untergeordneten Abschnitten gelten für die Version 1610 oder höher.** Dieser Inhalt wurde überarbeitet, um für die Entwurfsänderungen spezifisch zu sein, die für Begrenzungsgruppen mit dieser Updateversion eingeführt werden.
>
> **Wenn Sie die Versionen 1511, 1602 oder 1606 verwenden**, finden Sie unter [Boundary groups for System Center Configuration Manager versions 1511, 1602, and 1606 (Begrenzungsgruppen für die System Center Configuration Manager-Versionen 1511, 1602 und 1606)](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) Informationen zum Verwenden und Konfigurieren von Begrenzungsgruppen mit diesen Versionen.

Version 1610 umfasst wichtige Änderungen an Begrenzungsgruppen und deren Zusammenarbeit mit Verteilungspunkten. Diese Änderungen helfen bei der Vereinfachung des Entwurfs Ihrer Inhaltsinfrastruktur, wobei Sie mehr Kontrolle darüber erhalten, wie und wann ein Fallback der Clients erfolgt, um zusätzliche Verteilungspunkte als Quellspeicherorte für Inhalt zu suchen. Dies schließt sowohl lokale als auch cloudbasierte Verteilungspunkte ein.

**Informationen zu Begrenzungsgruppen:**  
 Sie erstellen Begrenzungsgruppen zum logischen Gruppieren zusammenhängender Netzwerkadressen (Grenzen), um die Verwaltung Ihrer Infrastruktur zu erleichtern. Sie müssen einer Begrenzungsgruppe zunächst Grenzen hinzufügen, damit Sie die Begrenzungsgruppe verwenden können. Clients verwenden die Konfiguration der Begrenzungsgruppe für folgende Zwecke:  

-   Automatische Standortzuweisung  
-   Inhaltsort  
-   Bevorzugte Verwaltungspunkte (wenn Sie bevorzugte Verwaltungspunkte verwenden möchten, müssen Sie diese Option für die Hierarchie und nicht in der Konfiguration der Begrenzungsgruppe aktivieren. Weitere Informationen finden Sie im folgenden Verfahren in diesem Thema: [So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte](#to-enable-use-of-preferred-management-points).)  

Beim Konfigurieren von Begrenzungsgruppen fügen Sie der Begrenzungsgruppe eine oder mehrere Grenzen hinzu und konfigurieren dann zusätzliche Einstellungen für Clients, die sich auf diesen Grenzen befinden.  

Sie finden die [Verfahren zum Verwalten von Begrenzungsgruppen](#procedures-for-boundary-groups) weiter unten in diesem Thema.


###  <a name="a-namebkmkboundarysiteassignmenta-about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Informationen zur Standortzuweisung  
 Sie können jede Begrenzungsgruppe mit einem zugewiesenen Standort für Clients konfigurieren.  

-   Ein neu installierter Client, der die automatische Standortzuweisung verwendet, tritt dem zugewiesenen Standort einer Begrenzungsgruppe bei, die die aktuelle Netzwerkadresse des Clients enthält.  
-   Nach Zuweisung zu einem Standort ändert sich die Standortzuweisung eines Clients nicht, wenn sich seine Netzwerkadresse ändert. Beim Wechseln des Clients zu einer neuen Netzwerkadresse, die von einer Grenze in einer Begrenzungsgruppe mit abweichender Standortzuweisung repräsentiert wird, bleibt der dem Client zugewiesene Standort unverändert.  
-   Wenn mithilfe von Active Directory-Systemermittlung eine neue Ressource ermittelt wird, werden die Netzwerkinformationen für diese Ressource anhand der Grenzen in Begrenzungsgruppen bewertet. Dabei wird die neue Ressource einem zugewiesenen Standort zur Verwendung bei einer Clientpushinstallation zugeordnet.  
-   Wenn eine Grenze zu mehreren Begrenzungsgruppen gehört, denen verschiedene Standorte zugewiesen sind, wählen die Clients einen dieser Standorte nach dem Zufallsprinzip aus.  
-   Änderungen an dem zugewiesenen Standort einer Begrenzungsgruppe betreffen nur neue Standortzuweisungsaktionen. Clients, die bereits einem Standort zugewiesen sind, bewerten ihre Standortzuweisung nicht basierend auf Änderungen an der Konfiguration einer Begrenzungsgruppe (oder ihrer eigenen Netzwerkadresse) neu.  

Weitere Informationen zur automatischen Standortzuweisung finden Sie unter [Verwenden von automatischen Standortzuweisungen für Computer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [Zuweisen von Clients zu einem Standort in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="a-namebkmkboundarycontentlocationa-about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Informationen zu Inhaltsorten  
Wenn Sie Begrenzungsgruppen konfigurieren, ordnen Sie der Begrenzungsgruppe Grenzen (Netzwerkspeicherorte) und Standortsystemrollen wie Verteilungspunkte zu. Dadurch können Clients mit Standortsystemservern wie Verteilungspunkten verknüpft werden, die sich in der Nähe der Clients auf dem Netzwerk befinden.

Sie können dieselbe Grenze zu mehreren Begrenzungsgruppen zuweisen, und Standortsystemserver, wie Verteilungspunkte, können mehreren Begrenzungsgruppen zugeordnet werden. Dadurch werden sie für eine größere Zahl von Netzwerkadressen verfügbar.

-   **Während der Softwareverteilung**fordern Clients einen Speicherort für Bereitstellungsinhalte an. Configuration Manager sendet dem Client eine Liste der Verteilungspunkte, die den einzelnen Begrenzungsgruppen zugeordnet sind, die den aktuellen Netzwerkort des Clients einbeziehen.  
-   **Während der Bereitstellung des Betriebssystems** fordern Clients einen Speicherort zum Senden oder Empfangen ihrer Zustandsmigrationsinformationen an. Configuration Manager sendet dem Client eine Liste der Zustandsmigrationspunkte, die den einzelnen Begrenzungsgruppen zugeordnet sind, die den aktuellen Netzwerkort des Clients einbeziehen.  

Sie definieren die Begrenzungsgruppenbeziehungen, um das Fallbackverhalten für die Quellspeicherorte für Inhalt zu konfigurieren. Ab Version 1610 konfigurieren Sie Beziehungen auf der neuen Registerkarte **Beziehungen** der Begrenzungsgruppeneigenschaften. „Beziehungen“ ersetzt die Notwendigkeit, die Standortsysteme als langsam oder schnell zu konfigurieren, oder per Konfiguration einer Begrenzungsgruppe einen Fallbackquellpfad für Inhalt zu ermöglichen.

Beim Konfigurieren einer Begrenzungsgruppe, die als **aktuelle** Begrenzungsgruppe bezeichnet wird, fügen Sie weitere Begrenzungsgruppen hinzu, um einen unidirektionalen Link aus der aktuellen Begrenzungsgruppe zu jeder hinzugefügten Begrenzungsgruppe zu erstellen. Begrenzungsgruppen, die Sie hinzufügen, heißen **Nachbar**begrenzungsgruppen. Für jeden Link zu einem Nachbarn, den Sie erstellen, können Sie anschließend Verteilungspunkte mit einer Fallbackzeit in Minuten konfigurieren. Dadurch wird bestimmt, nach welcher Zeit Clients in der aktuellen Begrenzungsgruppe beginnen können, Verteilungspunkte in der Nachbarbegrenzungsgruppe zu verwenden, wenn Clients in Ihrer aktuellen Begrenzungsgruppe keinen gültigen Quellspeicherort für Inhalt finden können.

Wenn ein Client keinen Inhalt finden kann und beginnt, Speicherorte in Nachbarbegrenzungsgruppen zu durchsuchen, wird der Pool verfügbarer Verteilungspunkte für diesen Client kontrolliert vergrößert.

-   Eine Begrenzungsgruppe kann mehr als eine Beziehung haben. Dadurch können Sie Fallbacks auf verschiedene Nachbarn konfigurieren, die nach Ablauf verschiedener Zeiten eintreten.
-   Der Fallback der Clients erfolgt nur auf eine Begrenzungsgruppe, die ein direkter Nachbar ihrer aktuellen Begrenzungsgruppe ist.
-   Wenn ein Client Mitglied mehrerer Begrenzungsgruppen ist, wird die aktuelle Begrenzungsgruppe als die Gesamtheit aller Begrenzungsgruppen dieses Clients definiert. Anschließend kann ein Fallback dieses Clients auf einen Nachbar einer beliebigen dieser ursprünglichen Begrenzungsgruppen erfolgen.

Zusätzlich zu den Links, die Sie definieren, wird zwischen den Begrenzungsgruppen, die Sie erstellen, und der Standardbegrenzungsgruppe, die automatisch für jeden Standort erstellt wird, automatisch ein implizierter Link erstellt. Dieser automatische Link:
-   Wird von Clients verwendet, die nicht an einer Grenze liegen, die einer Begrenzungsgruppe in der Hierarchie zugeordnet ist. Clients verwenden automatisch die Standardgruppe für die Grenze von ihrem zugewiesenen Standort, um gültige Quellspeicherorte für Inhalte zu ermitteln.
-   Ist eine Standardoption für ein Fallback von der aktuellen Begrenzungsgruppe auf die Standardbegrenzungsgruppe der Standorte, die nach 120 Minuten verwendet wird.

**Wenn Inhalt nicht aus einer aktuellen Begrenzungsgruppe verfügbar ist:**  
Wenn Inhalt, der von einem Client angefordert wird, nicht von einer gültigen Inhaltsquelle in einer aktuellen Begrenzungsgruppe verfügbar ist, verwendet der Client sofortigen Fallback, um den Inhalt von einem Verteilungspunkt in einer Nachbar-Begrenzungsgruppe zu suchen:   
- Sofortiger Fallback erfolgt an Nachbarbegrenzungsgruppen oder Gruppen, die mit der kleinsten Fallback-Zeitangabe konfiguriert sind. Dies kann die Standardbegrenzungsgruppe einschließen, wenn es keine Nachbarbegrenzungsgruppen mit einer kürzeren Fallbackzeit gibt.
- Nach dem sofortigen Fallback auf den ersten Satz von Nachbarbegrenzungsgruppen tritt ein Fallback auf zusätzliche Begrenzungsgruppen auf, basierend auf der konfigurierten Fallbackzeit für diese Gruppen.

Wenn der Inhalt bei Bedarf verteilt wird, jedoch nicht verfügbar ist, wenn er von einem Client angefordert wird, beginnt der Prozess zum Übertragen des Inhalts zu einem Verteilungspunkt in der aktuellen Grenze. Da der Inhalt zu diesem Zeitpunkt nicht verfügbar ist, verwendet der Client den sofortigen Fallback auf eine Nachbarbegrenzungsgruppe mit der kürzesten Fallbackzeit. Nachdem der Inhalt in der aktuellen Begrenzungsgruppe verfügbar wird, verwenden zusätzliche Clients nicht mehr den sofortigen Fallback auf Nachbargruppen.



**Beispiel für die Verwendung des neuen Modells:**   
Sie erstellen drei Begrenzungsgruppen, die keine Grenzen oder Standortsystemserver teilen:
-   Gruppe BG_A mit den Verteilungspunkten DP_A1 und DP_A2, die der Gruppe zugeordnet sind
-   Gruppe BG_B mit den Verteilungspunkten DP_B1 und DP_B2, die der Gruppe zugeordnet sind
-   Gruppe BG_C mit den Verteilungspunkten DP_C1 und DP_C2, die der Gruppe zugeordnet sind

Fügen Sie die Netzwerkspeicherorte Ihres Clients nur der Begrenzungsgruppe BG_A als Grenze hinzu, und konfigurieren Sie anschließend Beziehungen von dieser Begrenzungsgruppe zu den anderen beiden Begrenzungsgruppen:
-   Konfigurieren Sie Verteilungspunkte für die erste *Nachbargruppe* (BG_B), die nach 10 Minuten verwendet wird. Diese Gruppe enthält die Verteilungspunkte DP_B1 und DP_B2. Beide verfügen über eine gute Verbindung mit den Grenzspeicherorten der ersten Gruppe.
-   Konfigurieren Sie die zweite *Nachbargruppe* (BG_C), die nach 20 Minuten verwendet wird. Diese Gruppe enthält die Verteilungspunkte DP_C1 und DP_C2. Beide sind über ein WAN von den anderen Begrenzungsgruppen aus zugänglich.
-   Fügen Sie auch einen zusätzlichen Verteilungspunkt hinzu, der sich auf dem Standortserver der Standard-Standortbegrenzungsgruppe der Standorte befindet. Dies ist der am wenigsten bevorzugte Quellspeicherort für Inhalt, der sich jedoch zu all Ihren Begrenzungsgruppen zentral befindet.

    Beispiel für Begrenzungsgruppen und Fallbackzeiten:

     ![BG_Fallback](media/BG_Fallback.png)


Mit dieser Konfiguration:
-   Beginnt der Client die Suche nach Inhalt aus Verteilungspunkten in seiner *aktuellen* Begrenzungsgruppe (BG_A), wobei er jeden Verteilungspunkt 2 Minuten lang durchsucht, bevor er zum nächsten Verteilungspunkt in der Begrenzungsgruppe wechselt. Der Pool des Clients mit gültigen Quellspeicherorten für Inhalt umfasst DP_A1 und DP_A2.
-   Wenn der Client 10 Minuten lang keinen Inhalt aus der *aktuellen* Begrenzungsgruppe findet, fügt er die Verteilungspunkte aus der Begrenzungsgruppe BG_B zur Suche hinzu. Anschließend setzt er die Suche nach Inhalt von einem Verteilungspunkt in seinem kombinierten Pool von Verteilungspunkten fort, der nun die Verteilungspunkte der Begrenzungsgruppen BG_A und BG_B enthält. Der Client kontaktiert weiterhin jeden Verteilungspunkt zwei Minuten lang, bevor er zum nächsten Verteilungspunkt seines Pools wechselt. Der Pool des Clients mit gültigen Quellspeicherorten für Inhalt umfasst DP_A1, DP_A2, DP_B1 und DP_B2.
-   Nach weiteren 10 Minuten (insgesamt 20 Minuten), in denen der Client immer noch keinen Verteilungspunkt mit Inhalt gefunden hat, erweitert er seinen Pool mit verfügbaren Verteilungspunkten um die Verteilungspunkte der zweiten *Nachbargruppe*, also der Begrenzungsgruppe BG_C. Der Client verfügt nun über 6 Verteilungspunkte, die er durchsuchen kann (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 und DP_C2), und wechselt weiterhin alle zwei Minuten zu einem neuen Verteilungspunkt, bis er Inhalt gefunden hat.
-   Wenn der Client nach maximal 120 Minuten keinen Inhalt gefunden hat, greift er darauf zurück, die *Standard-Standortbegrenzungsgruppe* als Teil der kontinuierlichen Suche einzuschließen. In den Pool mit Verteilungspunkten werden nun alle Verteilungspunkte aus den drei konfigurierten Begrenzungsgruppen sowie der letzte Verteilungspunkt eingeschlossen, der sich auf dem Standortservercomputer befindet.  Der Client setzt die Suche nach Inhalt anschließend fort und wechselt alle zwei Minuten den Verteilungspunkt, bis er Inhalt gefunden hat.

Indem Sie die verschiedenen Nachbargruppen so konfigurieren, dass diese zu verschiedenen Zeiten verfügbar sind, steuern Sie, wann bestimmte Verteilungspunkte als Quellspeicherort für Inhalt hinzugefügt werden, sowie wann bzw. ob der Client ein Fallback auf die Standard-Standortbegrenzungsgruppe als Sicherheitsnetz für Inhalt verwendet, der von einem anderen Speicherort nicht verfügbar ist.




### <a name="update-existing-boundary-groups-to-the-new-model"></a>Aktualisieren vorhandener Begrenzungsgruppen auf das neue Modell
Wenn Sie auf die Version 1610 aktualisieren, werden die folgenden Konfigurationen automatisch vorgenommen. Diese sollen sicherstellen, dass Ihr aktuelles Fallbackverhalten verfügbar bleibt, bis Sie neue Begrenzungsgruppen und Beziehungen konfigurieren.
-   Eine standardmäßige Standort-Begrenzungsgruppe für jeden primären Standort wird erstellt, der Name ist ***Standard-Standort-Begrenzungsgruppe&lt;Standortcode>.***
-   Verteilungspunkte mit aktiviertem *Fallbackquellpfad für Inhalt zulassen* und Zustandsmigrationspunkten an primären Standorten werden der *Standard-Standort-Begrenzungsgruppe&lt;Standortcode>* Begrenzungsgruppe dieses Standorts hinzugefügt.
-   Von jeder vorhandenen Begrenzungsgruppe, die einen Standortserver umfasst, der mit einer langsamen Verbindung konfiguriert wurde, wird eine Kopie erstellt. Der Name der neuen Gruppe lautet ***&lt;ursprünglicher Name der Begrenzungsgruppe>-&lt;ursprüngliche ID der Begrenzungsgruppe>***:  
    -   Standortsysteme, die über eine schnelle Verbindung verfügen, bleiben in der ursprünglichen Begrenzungsgruppe.
    -   Eine Kopie der Standortsysteme (Verteilungspunkte, Verwaltungspunkte und Zustandsmigrationspunkte) mit einer langsamen Verbindung wird der Kopie der Begrenzungsgruppe hinzugefügt. Die ursprünglichen Standortsysteme, die als langsam konfiguriert wurden, bleiben zur Abwärtskompatibilität in den ursprünglichen Begrenzungsgruppen, werden von diesen Begrenzungsgruppen jedoch nicht verwendet.
    -   Dieser Begrenzungsgruppenkopie sind keine Grenzen zugeordnet. Jedoch wird ein Fallbacklink zwischen der ursprünglichen Gruppe und der neuen Begrenzungsgruppe erstellt, deren Fallbackzeit auf 0 festgelegt ist.  


- **Für sekundäre Standorte gilt:**
  - Eine Begrenzungsgruppe wird erstellt, wenn ein sekundärer Standort mindestens einen Verteilungspunkt mit aktiviertem *Fallbackquellpfad für Inhalt zulassen* oder Zustandsmigrationspunkt aufweist. Der Name der Begrenzungsgruppe ist ***Sekundärer-Standort-Nachbar--Tmp&lt;Standortcode>.***
  - Alle Verteilungspunkte mit aktiviertem *Fallbackquellpfad für Inhalt zulassen* und Zustandsmigrationspunkten werden dieser neu erstellten sekundären Standortbegrenzungsgruppe hinzugefügt.
  - Ein Fallbacklink wird zwischen der ursprünglichen Begrenzungsgruppe und der neu erstellten Nachbarbegrenzungsgruppe erstellt, deren Fallbackzeit auf 0 festgelegt ist.


 Die folgende Tabelle ermittelt das neue Fallbackverhalten, das Sie von der Kombination aus den ursprünglichen Bereitstellungseinstellungen und den Verteilungspunktkonfigurationen erwarten können:

Ursprüngliche Bereitstellungskonfiguration für „Programm nicht ausführen“ im langsamen Netzwerk  |Ursprüngliche Verteilungspunktkonfiguration für „Allow client to use a fallback source location for content“ (Zulassen, dass der Client einen Fallbackquellspeicherort für Inhalt verwendet)  |Neues Fallbackverhalten  
---------|---------|---------
Ausgewählt     |  Ausgewählt    |  **Kein Fallback** – Verwenden Sie nur die Verteilungspunkte in der aktuellen Begrenzungsgruppe.       
Ausgewählt     |  Nicht ausgewählt|  **Kein Fallback** – Verwenden Sie nur die Verteilungspunkte in der aktuellen Begrenzungsgruppe.       
Nicht ausgewählt |  Nicht ausgewählt|  **Fallback auf Nachbar** – Verwenden Sie die Verteilungspunkte in der aktuellen Begrenzungsgruppe, und fügen Sie anschließend die Verteilungspunkte aus der Nachbarbegrenzungsgruppe hinzu. Sofern kein expliziter Link zur Standard-Standortbegrenzungsgruppe konfiguriert wurde, erfolgt kein Fallback der Clients auf diese Gruppe.    
Nicht ausgewählt | Ausgewählt     |   **Normales Fallback** – Verwenden Sie die Verteilungspunkte in der aktuellen Begrenzungsgruppe und anschließend die der Nachbar- und der Standard-Standortbegrenzungsgruppen.

 Alle anderen Bereitstellungskonfigurationen führen zum **Normalen Fallback**.  



### <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Änderungen gegenüber früheren Versionen für Benutzeroberfläche und Verhalten für Speicherorte für Inhalt
Im Folgenden handelt es sich um mit Version 1610 eingeführte wichtige Änderungen an Begrenzungsgruppen und daran, wie Clients Inhalt suchen. Viele dieser Änderungen und Konzepte arbeiten zusammen.


-   **Konfigurationen für „schnell“ oder „langsam“ werden entfernt:** Sie konfigurieren einzelne Verteilungspunkte nicht mehr so, dass diese schnell oder langsam sind.  Stattdessen wird jedes Standortsystem, das einer Begrenzungsgruppe zugeordnet ist, auf die gleiche Weise behandelt. Aufgrund dieser Änderung unterstützt die Registerkarte **Referenz** der Begrenzungsgruppeneigenschaften die Konfiguration von „schnell“ und „langsam“ nicht mehr.
-   **Neue Standardbegrenzungsgruppen an jedem Standort:** Jeder primäre Standort verfügt über eine neue Standardbegrenzungsgruppe mit dem Namen ***Default-Site-Boundary-Group&lt;sitecode>***.  Wenn sich ein Client nicht an einem Netzwerkstandort befindet, der einer Begrenzungsgruppe zugewiesen ist, verwendet dieser Client die Standortsysteme, die der Standardgruppe seines zugewiesenen Standorts zugeordnet sind. Planen Sie, diese Begrenzungsgruppe als Ersatz für das Konzept der Fallbackinhaltsquelle zu verwenden.      
 -  **Allow fallback source locations for content** (Fallbackquellspeicherorte für Inhalt zulassen) wird entfernt: Sie konfigurieren nicht mehr explizit einen Verteilungspunkt, der für das Fallback verwendet wird, und die Optionen, um dies festzulegen, werden von der Benutzeroberfläche entfernt.

    Darüber hinaus hat sich das Ergebnis geändert, das auftritt, wenn die Einstellung **Die Verwendung eines Fallbackquellpfads für den Inhalt durch Clients zulassen** auf einem Bereitstellungstyp für Anwendungen festgelegt wird. Diese Einstellung auf einem Bereitstellungstyp ermöglicht es einem Client nun, die Standard-Standortbegrenzungsgruppe als Quellspeicherort für Inhalt zu verwenden.

 -  **Begrenzungsgruppenbeziehungen:** Jede Begrenzungsgruppe kann mit einer oder mehreren zusätzlichen Begrenzungsgruppen verknüpft werden. Diese Links bilden Beziehungen, die auf der neuen Registerkarte der Begrenzungsgruppeneigenschaften mit dem Namen **Beziehungen** konfiguriert sind:
    -   Jede Begrenzungsgruppe, der ein Client direkt zugewiesen ist, wird **aktuelle** Begrenzungsgruppe genannt.  
    -   Jede Begrenzungsgruppe, die ein Client aufgrund einer Zuweisung zwischen der *aktuellen* Begrenzungsgruppe des Clients und einer anderen Gruppe verwenden kann, wird **Nachbarbegrenzungsgruppe** genannt.
    -  Auf der Registerkarte **Beziehungen** können Sie Begrenzungsgruppen hinzufügen, die als *Nachbarbegrenzungsgruppe* verwendet werden können. Sie können auch eine Zeit in Minuten konfigurieren, die bestimmt, wann ein Client, der keinen Inhalt von einem Verteilungspunkt in der *aktuellen* Gruppe findet, beginnt, Speicherorte für Inhalt von diesen *Nachbarbegrenzungsgruppen* zu suchen.

        Beim Hinzufügen oder Ändern einer Begrenzungsgruppenkonfiguration verfügen Sie über die Option, das Fallback auf diese bestimmte Begrenzungsgruppe von der aktuellen Gruppe zu blockieren, die Sie konfigurieren.

    Um die neue Konfiguration zu verwenden, definieren Sie explizite Zuordnungen (Links) von einer Begrenzungsgruppe zu einer anderen, und konfigurieren Sie alle Verteilungspunkte in dieser zugeordneten Gruppe mit der gleichen Zeit in Minuten. Die Zeit, die Sie konfigurieren, bestimmt, wann ein Client, der keine Inhaltsquelle von seiner *aktuellen* Begrenzungsgruppe findet, beginnt, Inhaltsquellen von dieser Nachbarbegrenzungsgruppe zu suchen.

    Zusätzlich zu Begrenzungsgruppen, die Sie explizit konfigurieren, verfügt jede Begrenzungsgruppe über einen implizierten Link zur Standard-Standortbegrenzungsgruppe. Dieser Link wird nach 120 Minuten aktiv, wenn die Standard-Standortbegrenzungsgruppe zu einer Nachbarbegrenzungsgruppe wird, was den Clients ermöglicht, die Verteilungspunkte zu verwenden, die dieser Begrenzungsgruppe als Quellspeicherort für Inhalt zugeordnet sind.

    Dieses Verhalten ersetzt, was zuvor als Fallback für den Inhalt bezeichnet wurde.  Sie können dieses Standardverhalten von 120 Minuten außer Kraft setzen, indem Sie die Standardbegrenzungsgruppe einer *aktuellen* Gruppe zuordnen und eine bestimmte Zeit in Minuten festlegen oder das Fallback vollständig blockieren, um dessen Verwendung zu verhindern.


-   **Clients versuchen bis zu 2 Minuten lang, Inhalt aus jedem Verteilungspunkt zu erhalten:** Wenn ein Client nach einem Quellspeicherort für Inhalt sucht, versucht er 2 Minuten lang auf jeden Verteilungspunkt zuzugreifen, bevor er anschließend einen anderen Verteilungspunkt versucht. Dabei handelt es sich um eine Änderung gegenüber früheren Versionen, bei denen Clients bis zu 2 Stunden lang versucht haben, eine Verbindung zu einem Verteilungspunkt herzustellen.

    - Der erste Verteilungspunkt, den ein Client versucht zu verwenden, wird zufällig aus dem Pool verfügbarer Punkte in der *aktuellen* Begrenzungsgruppe (bzw. den aktuellen Begrenzungsgruppen) ausgewählt.

    - Wenn der Client den Inhalt nach zwei Minuten nicht gefunden hat, wechselt er zu einem neuen Verteilungspunkt und versucht, Inhalt von diesem Server zu erhalten. Dieser Vorgang wird alle zwei Minuten wiederholt, bis der Client den Inhalt findet oder den letzten Server im Pool erreicht.

    - Wenn ein Client in seinem *aktuellen* Pool keinen gültigen Quellspeicherort für Inhalt findet, bevor der Zeitraum für ein Fallback auf eine *Nachbarbegrenzungsgruppe* erreicht ist, fügt der Client die Verteilungspunkte aus dieser *Nachbarbegrenzungsgruppe* zum Ende seiner aktuellen Liste hinzu und durchsucht anschließend die erweiterte Gruppe von Quellspeicherorten, die die Verteilungspunkte aus beiden Begrenzungsgruppen umfasst.

        > [!TIP]  
        > Wenn Sie einen expliziten Link von der aktuellen Begrenzungsgruppe zu der Standard-Standortbegrenzungsgruppe erstellen und eine Fallbackzeit festlegen, die kürzer ist als die Fallbackzeit für einen Link zu einer Nachbarbegrenzungsgruppe, beginnen Clients, Quellspeicherorte aus der Standard-Standortbegrenzungsgruppe zu durchsuchen, bevor sie die Nachbargruppe einschließen.

    - Wenn der Client vom letzten Server im Pool keinen Inhalt abrufen kann, beginnt er den Prozess erneut.





###  <a name="a-namebkmkpreferredmpa-about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Informationen zu bevorzugten Verwaltungspunkten  
 Bevorzugte Verwaltungspunkte ermöglichen einem Client die Identifikation eines Verwaltungspunkts, der seiner aktuellen Netzwerkadresse (oder Begrenzung) zugeordnet ist.  

-   Ein Client versucht zunächst, einen bevorzugten Verwaltungspunkt seines zugewiesenen Standorts zu verwenden, bevor er einen Verwaltungspunkt seines zugewiesenen Standorts verwendet, der nicht als bevorzugt konfiguriert wurde.  
-   Um diese Option verwenden zu können, müssen Sie sie für die Hierarchie aktivieren und Begrenzungsgruppen an den einzelnen primären Standorten konfigurieren, die die Verwaltungspunkte enthalten, die den Grenzen dieser Begrenzungsgruppe zugeordnet sein sollen.  
-   Wenn bevorzugte Verwaltungspunkte konfiguriert werden und ein Client seine Liste der Verwaltungspunkte organisiert, platziert er die bevorzugten Verwaltungspunkte ganz oben in der Liste der zugewiesenen Verwaltungspunkte (die alle Verwaltungspunkte des zugewiesenen Standorts des Clients enthält)  

> [!NOTE]  
>  Wenn ein Client seinen Standort wechselt (d. h. sich seine Netzwerkadresse ändert, wenn beispielsweise ein Laptop an einem Remotestandort mit dem Netzwerk verbunden wird), kann er einen Verwaltungspunkt (bzw. Proxyverwaltungspunkt) des lokalen Standorts verwenden, bevor versucht wird, einen Verwaltungspunkt seines zugewiesenen Standorts zu verwenden (was die bevorzugten Verwaltungspunkte einschließt).  Weitere Informationen finden Sie unter [Understand how clients find site resources and services for System Center Configuration Manager (Verstehen, wie Clients Standortressourcen und -dienste für System Center Configuration Manager suchen)](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

###   <a name="a-namebkmkboundaryoverlapa-about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Informationen zu überlappenden Grenzen  
 Bei der Abfrage von Inhaltsorten werden überlappende Grenzkonfigurationen von Configuration Manager unterstützt:  

-   **Wenn ein Client Inhalt anfordert**und die Netzwerkadresse des Clients zu mehreren Begrenzungsgruppen gehört, erhält der Client von Configuration Manager eine Liste mit allen Verteilungspunkten, die über diesen Inhalt verfügen.  
-   **Wenn von einem Client Zustandsmigrationsinformationen bei einem Server angefordert bzw. an diesen gesendet werden**und das Netzwerk des Clients Mitglied mehrerer Begrenzungsgruppen ist, erhält der Client von Configuration Manager eine Liste mit allen Zustandsmigrationspunkten, die einer Begrenzungsgruppe mit der aktuellen Netzwerkadresse des Clients zugeordnet sind.  

So kann von den Clients der am nächsten liegende Server zur Übertragung der Inhalts- oder Zustandsmigrationsinformationen ausgewählt werden.  






## <a name="procedures-for-boundary-groups"></a>Prozeduren für Begrenzungsgruppen
Die folgenden Prozeduren gelten ab Version 1610. Wenn Sie Version 1511, 1602 oder 1606 verwenden, finden Sie die Prozeduren in [Boundary groups for System Center Configuration Manager version 1511, 1602, and 1606 (Begrenzungsgruppen für die System Center Configuration Manager-Versionen 1511, 1602 und 1606)](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).


### <a name="to-create-a-boundary-group"></a>So erstellen Sie eine Begrenzungsgruppe  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Begrenzungsgruppe erstellen**.  

3.  Wählen Sie im Dialogfeld **Begrenzungsgruppe erstellen** die Registerkarte **Allgemein** aus, und geben Sie unter **Name** einen Namen für diese Begrenzungsgruppe an.  

4.  Klicken Sie auf **OK** , um die neue Begrenzungsgruppe zu speichern.  


### <a name="to-configure-a-boundary-group"></a>So konfigurieren Sie eine Begrenzungsgruppe  
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

 6.  Wählen Sie die Registerkarte **Beziehungen** aus, um das Fallbackverhalten zu konfigurieren:  

     - Klicken Sie auf **Hinzufügen**, und wählen Sie anschließend die Begrenzungsgruppe aus, die Sie konfigurieren möchten.

     - Legen Sie eine Fallbackzeit für Verteilungspunkte fest. Nach dieser Zeitspanne können Clients in der Begrenzungsgruppe, für die Sie die Beziehungen konfigurieren, die Suche nach Inhalten aus den Verteilungspunkten der von Ihnen hinzugefügten Begrenzungsgruppe starten.

     - Zur Verhinderung von Fallback auf eine bestimmte Begrenzungsgruppe einschließlich der *Standard-Standortbegrenzungsgruppe*, die standardmäßig konfiguriert ist, wählen Sie die Begrenzungsgruppe aus, und aktivieren Sie das Kontrollkästchen **Never Fallback** (Kein Fallback).   

 7.  Klicken Sie auf **OK** , um die Eigenschaften der Begrenzungsgruppe zu schließen und die Konfiguration zu speichern.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>So ordnen Sie einen Inhaltsbereitstellungsserver oder Verwaltungspunkt einer Begrenzungsgruppe zu  
 1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

 2.  Wählen Sie die Begrenzungsgruppe aus, die Sie ändern möchten.  

 3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

 4.  Wählen Sie im Dialogfeld **Eigenschaften** für die Begrenzungsgruppe die Registerkarte **Referenzen** aus.  

 5.  Klicken Sie unter **Standortsystemserver auswählen**auf **Hinzufügen**, aktivieren Sie das Kontrollkästchen für die Standortsystemserver, die dieser Begrenzungsgruppe zugeordnet werden sollen, und klicken Sie dann auf **OK**.  

 6.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen und die Konfiguration der Begrenzungsgruppe zu speichern.  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>So konfigurieren Sie einen Fallbackstandort für die automatische Standortzuweisung  

  1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** >  **Standorte**.  

  2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.  

  3.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen **Fallbackstandort verwenden**, und wählen Sie dann in der Dropdownliste **Fallbackstandort** einen Standort aus.  

  4.  Klicken Sie auf **OK** , um die Konfiguration zu speichern.  

#### <a name="to-enable-use-of-preferred-management-points"></a>So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte  

 1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie anschließend **Hierarchieeinstellungen**auf der Registerkarte **Start** aus.  

 2.  Wählen Sie im Dialogfeld „Hierarchieeinstellungen“ auf der Registerkarte **Allgemein** die Option **Clients bevorzugen die in Begrenzungsgruppen angegebenen Verwaltungspunkte**.  

 3.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen und die Konfiguration zu speichern.  


### <a name="to-enable-use-of-pre-release-features"></a>Verwendung von Pre-Release-Funktionen aktivieren
1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie anschließend **Hierarchieeinstellungen**auf der Registerkarte **Start** aus.  

2.  Wählen Sie auf der Registerkarte **Allgemein** der Hierarchieeinstellungen **Verwendung von Featurevorabversionen zustimmen** aus.  

3.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen und die Konfiguration zu speichern.  



##  <a name="a-namebkmkboundarybestpracticesa-best-practices-for-boundaries"></a><a name="BKMK_BoundaryBestPractices"></a> Bewährte Methoden für Grenzen  

-   **Verwenden Sie eine Kombination aus den wenigsten Grenzen, die Ihren Anforderungen entsprechen:**  
   In der Vergangenheit empfahlen wir die Verwendung von einigen Typen von Grenzen gegenüber anderen. Mit Änderungen zur Verbesserung der Leistung empfehlen wir Ihnen, die von Ihnen gewählten Grenzen oder Typen für Ihre Umgebung zu verwenden, sodass Sie die wenigsten möglichen Grenzen verwenden können, um Ihre Verwaltungsaufgaben zu vereinfachen.      

-   **Vermeiden Sie überlappende Grenzen bei der automatischen Standortzuweisung:**  
     Obwohl jede Begrenzungsgruppe sowohl Konfigurationen der Standortzuweisung als auch für die Inhaltssuche unterstützt, ist es eine bewährte Methode, einen getrennten Satz von Begrenzungsgruppen nur für die Standortzuweisung zu nutzen. Achten Sie also darauf, dass in einer Begrenzungsgruppe enthaltene Grenzen nicht gleichzeitig einer anderen Begrenzungsgruppe mit abweichender Standortzuweisung angehören. Der Grund ist wie folgt:  

    -   Eine einzelne Grenze kann zu mehreren Begrenzungsgruppen gehören.  

    -   Jede Begrenzungsgruppe kann für die Standortzuweisung einem anderen primären Standort zugeordnet werden.  

    -   Ein Client auf einer Grenze, die zu zwei verschiedenen Begrenzungsgruppen mit unterschiedlichen Standortzuweisungen gehört, wählt für den Beitritt zu einem Standort das Zufallsprinzip, wobei dies ggf. nicht der Standort ist, dem der Client beitreten möchte.  Diese Konfiguration wird als überlappende Grenzen bezeichnet.  

     Überlappende Grenzen sind kein Problem für die Inhaltssuche und stattdessen häufig eine gewünschte Konfiguration, um Clients zusätzliche Ressourcen oder Inhaltsorte zu bieten, die sie verwenden können.  



<!--HONumber=Dec16_HO3-->


