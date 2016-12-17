---
title: Ermittlungsmethoden | System Center Configuration Manager
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8bb71e477bb9a265b3485bd3ef8232f6e9933a37

---
# <a name="about-discovery-methods-for-system-center-configuration-manager"></a>About discovery methods for System Center Configuration Manager (Informationen zu Ermittlungsmethoden in System Center Configuration Manager)

*Gilt für: System Center Configuration Manager (Current Branch)*

Jede System Center Configuration Manager-Ermittlungsmethode kann andere Geräte im Netzwerk oder Geräte und Benutzer aus Active Directory suchen. Um effizient eine Ermittlungsmethode zu verwenden, sollten Sie die verfügbaren Konfigurationen und Einschränkungen verstehen.  

##  <a name="a-namebkmkaboutforesta-active-directory-forest-discovery"></a><a name="bkmk_aboutForest"></a> Active Directory-Gesamtstrukturermittlung  
 **Konfigurierbar:** Ja  

 **Standardmäßig aktiviert:** Nein  

 **Konten** zum Ausführen dieser Methode:  

-   **Active Directory-Gesamtstruktur-Ermittlungskonto** (Benutzerdefiniert)  

-   **Computerkonto** des Standortservers  

Im Unterschied zu anderen Active Directory-Ermittlungsmethoden werden von der Active Directory-Gesamtstrukturermittlung keine Ressourcen, die Sie verwalten können, erkannt. Stattdessen erkennt diese Methode Netzwerkorte, die in Active Directory konfiguriert sind, und kann diese Orte zur hierarchieweiten Verwendung in Grenzen konvertieren.  

Wenn diese Methode ausgeführt wird, sucht sie in der lokalen Active Directory-Gesamtstruktur, allen vertrauenswürdigen Gesamtstrukturen und alle weiteren von Ihnen im Knoten **Active Directory-Gesamtstrukturen** der Configuration Manager-Konsole konfigurierten Gesamtstrukturen.  

Verwenden Sie die Active Directory-Gesamtstrukturermittlung für:  

-   Die Ermittlung von Active Directory-Standorten und Subnetzen, und das anschließende Erstellen von Configuration Manager-Grenzen basierend auf diesen Netzwerkorten  

-   Das Identifizieren von Supernetzen, die einem Active Directory-Standort zugewiesen sind, und das Konvertieren des Supernetzes in eine IP-Adressbereichsgrenze  

-   Veröffentlichen in den Active Directory-Domänendiensten einer Gesamtstruktur, sofern die Veröffentlichung in dieser Gesamtstruktur aktiviert ist und dem angegebenen Active Directory-Gesamtstrukturkonto entsprechende Berechtigungen für diese Gesamtstruktur erteilt wurden  

Sie können die Active Directory-Gesamtstrukturermittlung in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** unter **Hierarchiekonfiguration** in den folgenden Knoten verwalten:  

-   **Ermittlungsmethoden**: Hier können Sie die Ausführung der Active Directory-Gesamtstrukturermittlung am Standort der obersten Ebene Ihrer Hierarchie aktivieren. Sie können außerdem einen einfachen Zeitplan für die Ausführung der Ermittlung angeben, und Sie können die automatische Erstellung von Grenzen aus den ermittelten IP-Subnetzen und Active Directory-Standorten konfigurieren. Die Active Directory-Gesamtstrukturermittlung kann weder an untergeordneten primären Standorten noch an sekundären Standorten ausgeführt werden.  

-   **Active Directory-Gesamtstrukturen**: Hier konfigurieren Sie die zusätzlichen Active Directory-Gesamtstrukturen, die ermittelt werden sollen, geben das Konto zur Verwendung als Active Directory-Gesamtstrukturkonto für jede Gesamtstruktur an und konfigurieren das Veröffentlichen in jeder Gesamtstruktur. Zusätzlich können Sie den Ermittlungsvorgang überwachen und Configuration Manager IP-Subnetze sowie Active Directory-Standorte als Grenzen und Mitglieder von Begrenzungsgruppen hinzufügen.  

Zum Konfigurieren aller Standorte in einer Hierarchie für die Veröffentlichung in Active Directory-Gesamtstrukturen verbinden Sie die Configuration Manager-Konsole mit dem Standort auf der obersten Ebene der Hierarchie. Im Dialogfeld **Eigenschaften** eines Active Directory-Standorts werden auf der Registerkarte **Veröffentlichen** nur der aktuelle Standort und dessen untergeordnete Standorte angezeigt. Wenn die Veröffentlichung für eine Gesamtstruktur aktiviert ist und das Gesamtstrukturschema für Configuration Manager erweitert wurde, werden für jeden Standort, bei dem die Veröffentlichung in dieser Active Directory-Gesamtstruktur aktiviert ist, die folgenden Informationen veröffentlicht:  

-    **SMS-Standort-&lt;Standortcode>**

-   **SMS-MP-&lt;Standortcode>-&lt;System-Standortservername>**  

-   **SMS-SLP-&lt;Standortcode>-&lt;System-Standortservername>**  

-   **SMS-&lt;Standortcode>-&lt;Active Directory-Standortname oder Subnetz>**  

> [!NOTE]  
>  Die Veröffentlichung in Active Directory durch sekundäre Standorte erfolgt immer über das Computerkonto des sekundären Standortservers. Wenn Sie die Veröffentlichung durch sekundäre Standorte in Active Directory wünschen, stellen Sie sicher, dass das Computerkonto des sekundären Standortservers zur Veröffentlichung in Active Directory berechtigt ist. In einer nicht vertrauenswürdigen Gesamtstruktur können von einem sekundären Standort keine Daten veröffentlicht werden.  

> [!CAUTION]  
>  Wenn Sie die Option zum Veröffentlichen eines Standorts in einer Active Directory-Gesamtstruktur deaktivieren, werden alle bereits veröffentlichten Informationen dieses Standorts, einschließlich der verfügbaren Standortsystemrollen, aus dieser Active Directory-Gesamtstruktur entfernt.  

Aktionen im Rahmen der Active Directory-Gesamtstrukturermittlung werden in den folgenden Protokollen aufgezeichnet:  

-   Alle Aktionen, mit Ausnahme von Aktionen im Zusammenhang mit der Veröffentlichung, werden auf dem Standortserver in der Datei **ADForestDisc.Log** im Ordner **&lt;InstallationPath>\Logs** aufgezeichnet.  

-   Veröffentlichungsaktionen im Zusammenhang mit der Active Directory-Gesamtstrukturermittlung werden auf dem Standortserver in den Dateien **hman.log** und **sitecomp.log** im Ordner **&lt;InstallationPath>\Logs** aufgezeichnet.  

Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Configure discovery methods for System Center Configuration Manager (Konfigurieren der Active Directory-Ermittlung in Configuration Manager)](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="a-namebkmkaboutgroupa-active-directory-group-discovery"></a><a name="bkmk_aboutGroup"></a> Active Directory-Gruppenermittlung  
**Konfigurierbar:** Ja  

**Standardmäßig aktiviert:** Nein  

**Konten** zum Ausführen dieser Methode:  

-   **Active Directory-Gesamtstruktur-Ermittlungskonto** (Benutzerdefiniert)  

-   **Computerkonto** des Standortservers  

> [!TIP]  
>  Neben den Informationen in diesem Abschnitt finden Sie weitere unter [Allgemeine Features von Active Directory-Gruppe, System und Ermittlung](#bkmk_shared).  

Verwenden Sie diese Methode, um Active Directory Domain Services (AD DS) zur Identifizierung zu suchen:  

-   Lokale, globale und universelle Sicherheitsgruppen  

-   Mitgliedschaft in Gruppen  

-   Eingeschränkte Informationen über die Mitgliedscomputer und Benutzer einer Gruppe, auch wenn diese Computer und Benutzer zuvor nicht von einer anderen Ermittlungsmethode ermittelt wurden  

Mithilfe dieser Ermittlungsmethode lassen sich Gruppen sowie Gruppenbeziehungen der Mitglieder von Gruppen identifizieren. Standardmäßig werden nur Sicherheitsgruppen ermittelt. Sie können auch die Mitgliedschaften in Verteilergruppen ermitteln, indem Sie im Dialogfeld Eigenschaften der Active Directory-Gruppenermittlung auf der Registerkarte **Option** das Kontrollkästchen für die Option **Mitgliedschaft von Verteilergruppen ermitteln** aktivieren.  

Die Active Directory-Gruppenermittlung unterstützt nicht die erweiterten Active Directory-Attribute, die mithilfe der Active Directory-Systemermittlung oder der Active Directory-Benutzerermittlung identifiziert werden können. Da diese Ermittlungsmethode nicht für die Ermittlung von Computer- und Benutzerressourcen optimiert ist, sollten Sie sie ausführen, nachdem Sie die Active Directory-Systemermittlung und die Active Directory-Benutzerermittlung ausgeführt haben. Dies liegt daran, dass von dieser Methode ein vollständiger DDR für Gruppen erstellt wird, während für Computer, die Mitglieder von Gruppen sind, nur ein eingeschränkter DDR erstellt wird.  

Sie können die folgenden Ermittlungsbereiche konfigurieren; von diesen wird gesteuert, auf welche Art von dieser Methode nach Informationen gesucht wird:  

-   **Speicherort**: Verwenden Sie einen Speicherort, wenn Sie einen oder mehrere Active Directory-Container durchsuchen möchten. Von dieser Bereichsoption wird ein rekursives Durchsuchen der angegebenen Active Directory-Container unterstützt, wobei auch die untergeordneten Container des angegebenen Containers durchsucht werden. Dieser Prozess wird fortgesetzt, bis keine untergeordneten Container mehr gefunden werden.  

-   **Gruppen**: Verwenden Sie Gruppen, wenn Sie eine oder mehrere bestimmte Active Directory-Gruppen durchsuchen möchten. Sie können die **Active Directory-Domäne** zum Verwenden von Standarddomäne und Standardgesamtstruktur konfigurieren, oder Sie können die Suche auf einen einzelnen Domänencontroller beschränken. Zusätzlich können Sie eine oder mehrere zu durchsuchende Gruppen angeben. Wenn Sie nicht mindestens eine Gruppe angeben, werden alle Gruppen, die am angegebenen ** ** Active Directory-Domänenspeicherort gefunden werden, durchsucht.  

> [!CAUTION]  
>  Wenn Sie einen Ermittlungsbereich konfigurieren, wählen Sie nur die Gruppen aus, die ermittelt werden müssen. Dies ist notwendig, weil von der Active Directory-Gruppenermittlung versucht wird, jedes Mitglied in allen Gruppen innerhalb des Ermittlungsbereichs zu ermitteln. Bei der Ermittlung großer Gruppen kann es zu einer übermäßigen Beanspruchung von Bandbreite und Active Directory-Ressourcen kommen.  

> [!NOTE]  
>  Je nachdem, was Sie ermitteln möchten, müssen Sie entweder die Active Directory-Systemerkennung oder die Active Directory-Benutzererkennung ausführen, um Sammlungen auf Basis von erweiterten Active Directory-Attributen zu erstellen und um zu gewährleisten, dass die Ermittlungsergebnisse für Computer und Benutzer korrekt sind.  

Die Aktionen der Active Directory-Gruppenermittlung werden in der Datei **adsgdis.log** im Ordner **&lt;InstallationPath\>\LOGS** auf dem Standortserver aufgezeichnet.  

Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Configure discovery methods for System Center Configuration Manager (Konfigurieren der Active Directory-Ermittlung in Configuration Manager)](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="a-namebkmkaboutsystema-active-directory-system-discovery"></a><a name="bkmk_aboutSystem"></a> Active Directory-Systemermittlung  
**Konfigurierbar:** Ja  

**Standardmäßig aktiviert:** Nein  

**Konten** zum Ausführen dieser Methode:  

-   **Konto für Active Directory-Systemermittlung** (Benutzerdefiniert)  

-   **Computerkonto** des Standortservers  

> [!TIP]  
>  Neben den Informationen in diesem Abschnitt finden Sie weitere unter [Allgemeine Features von Active Directory-Gruppe, System und Ermittlung](#bkmk_shared).  

Verwenden Sie diese Ermittlungsmethode, um nach den angegebenen Active Directory Domain Services.Speicherorten (AD DS) für Computerressourcen zu suchen, die zum Erstellen von Sammlungen und Abfragen verwendet werden können. Sie können auch Configuration Manager-Client für ein ermitteltes Gerät mithilfe der Clientpushinstallation installieren.  

Von dieser Methode werden standardmäßig Basisinformationen über den Computer einschließlich der folgenden Informationen ermittelt:  

-   Computername  

-   Betriebssystem und Version  

-   Active Directory-Containername  

-   IP-Adresse  

-   Active Directory-Standort  

-   Zeitstempel der letzten Anmeldung  

Damit erfolgreich ein Discovery Data Record (DDR) für einen Computer erstellt werden kann, muss das Computerkonto von der Active Directory-Systemermittlung identifiziert werden, und der Computername muss erfolgreich in eine IP-Adresse aufgelöst werden.  

Sie können im Dialogfeld **Eigenschaften der Active Directory-Systemermittlung** auf der Registerkarte **Active Directory-Attribute** die Standardliste von Objektattributen anzeigen, welche von der Active Directory-Systemermittlung zurückgegeben werden, und Sie können zusätzliche Attribute konfigurieren, die ermittelt werden sollen.  

Die Aktionen der Active Directory-Systemermittlung werden in der Datei **adsysdis.log** im Ordner **&lt;InstallationPath\>\LOGS** auf dem Standortserver aufgezeichnet.  

Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Configure discovery methods for System Center Configuration Manager (Konfigurieren der Active Directory-Ermittlung in Configuration Manager)](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="a-namebkmkaboutusera-active-directory-user-discovery"></a><a name="bkmk_aboutUser"></a> Active Directory-Benutzerermittlung  
**Konfigurierbar:** Ja  

**Standardmäßig aktiviert:** Nein  

**Konten** zum Ausführen dieser Methode:  

-   **Konto für Active Directory-Benutzerermittlung** (Benutzerdefiniert)  

-   **Computerkonto** des Standortservers  

> [!TIP]  
>  Neben den Informationen in diesem Abschnitt finden Sie weitere unter [Allgemeine Features von Active Directory-Gruppe, System und Ermittlung](#bkmk_shared).  

Verwenden Sie diese Ermittlungsmethode zum Suchen von Active Directory Domain Services (AD DS) zum Identifizieren von Benutzerkonten und zugeordneter Attribute.  Standardmäßig ermittelt diese Methode grundlegende Informationen über das Benutzerkonto, einschließlich der folgenden:  

-   Benutzername  

-   Eindeutiger Benutzername (einschließlich Domänenname)  

-   Domain  

-   Active Directory-Containernamen  

Sie können im Dialogfeld **Eigenschaften der Active Directory-Benutzerermittlung** auf der Registerkarte **Active Directory-Attribute** die Standardliste von Objektattributen anzeigen, welche von der Active Directory-Benutzerermittlung zurückgegeben werden, und Sie können zusätzliche Attribute konfigurieren, die ermittelt werden sollen.  

Die Aktionen der Active Directory-Benutzerermittlung werden in der Datei **adusrdis.log** im Ordner **&lt;InstallationPath\>\LOGS** auf dem Standortserver aufgezeichnet.  

Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Configure discovery methods for System Center Configuration Manager (Konfigurieren der Active Directory-Ermittlung in Configuration Manager)](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="a-namebkmkaboutheartbeata-heartbeat-discovery"></a><a name="bkmk_aboutHeartbeat"></a> Frequenzermittlung  
**Konfigurierbar:** Ja  

**Standardmäßig aktiviert:** Ja  

**Konten** zum Ausführen dieser Methode:  

-   **Computerkonto** des Standortservers  

Die Frequenzermittlung unterscheidet sich von anderen Configuration Manager-Ermittlungsmethoden. Sie ist standardmäßig aktiviert und wird auf jedem Computerclient (statt auf einem Standortserver) ausgeführt, um einen Discovery Data Record (DDR) zu erstellen. Für mobile Geräteclients wird dieser DDR von dem Verwaltungspunkt erstellt, der vom mobilen Geräteclient verwendet wird.  Es wird empfohlen, die Frequenzermittlung nicht zu deaktivieren, um den Datenbankdatensatz von Configuration Manager-Clients aufrechtzuerhalten.  Zusätzlich zum Erhalt des Datenbankdatensatzes kann bei dieser Methode die Ermittlung eines Computers als neuer Ressourceneintrag erzwungen oder der Datenbankdatensatz eines aus der Datenbank gelöschten Computers neu aufgefüllt werden.  

Die Frequenzermittlung wird entweder nach einem für alle Clients in der Hierarchie festgelegten Zeitplan ausgeführt oder manuell für einen bestimmten Client aufgerufen. Zur manuellen Ausführung muss im Configuration Manager-Programm des betreffenden Clients auf der Registerkarte **Aktion** der **Ermittlungsdaten-Sammlungszyklus** ausgeführt werden. Laut Standardzeitplan wird die Frequenzermittlung alle 7 Tage ausgeführt. Achten Sie bei einer Änderung des Frequenzermittlungsintervalls darauf, dass die Frequenzermittlung häufiger als der Standortwartungstask **Veraltete Ermittlungsdaten löschen**ausgeführt wird. Von diesem Task werden inaktive Clientdatensätze aus der Standortdatenbank gelöscht. Sie können den Task **Veraltete Ermittlungsdaten löschen** nur für primäre Standorte konfigurieren.  

Bei der Frequenzermittlung wird ein DDR erstellt, der die aktuellen Informationen des Clients enthält. Der Client kopiert anschließend diese kleine Datei (ca. 1 kB Größe) an einen Verwaltungspunkt, damit sie von einem primären Standort verarbeitet werden kann.  Die Datei enthält die folgenden Informationen:  

-   Netzwerkadresse  

-   NetBIOS-Name  

-   Version des Client-Agents  

-   Betriebsstatusdetails  

Die Frequenzermittlung ist die einzige Ermittlungsmethode, von der Details zum Clientinstallationsstatus bereitgestellt werden. Dabei wird das Clientattribut der Systemressource auf den Wert **Ja** aktualisiert.  

> [!NOTE]  
>  Selbst wenn die Frequenzermittlung deaktiviert ist, werden dennoch DDRs für aktive mobile Geräteclients erstellt und übermittelt. Auf diese Weise wird sichergestellt, dass aktive mobile Geräte vom Task **Veraltete Ermittlungsdaten löschen** nicht beeinträchtigt werden. Denn wenn ein Datenbankeintrag für ein mobiles Gerät vom Task **Veraltete Ermittlungsdaten löschen** gelöscht wird, wird auch das Gerätezertifikat aufgehoben, und die Verbindung des mobilen Geräts mit Verwaltungspunkten wird blockiert.  

Frequenzermittlungsaktionen werden an den folgenden Speicherorten protokolliert:  

-   Für Computerclients werden Frequenzermittlungsaktionen auf dem Client in der Datei **InventoryAgent.log** im Ordner *%Windir%\CCM\Logs* aufgezeichnet.  

-   Für mobile Clients werden Frequenzermittlungsaktionen in der Datei **DMPRP.log** im Ordner *%Program Files%\CCM\Logs* des vom mobilen Geräteclient verwendeten Verwaltungspunkts aufgezeichnet.  

Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Configure discovery methods for System Center Configuration Manager (Konfigurieren der Active Directory-Ermittlung in Configuration Manager)](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="a-namebkmkaboutnetworka-network-discovery"></a><a name="bkmk_aboutNetwork"></a> Netzwerkermittlung  
**Konfigurierbar:** Ja  

**Standardmäßig aktiviert:** Nein  

**Konten** zum Ausführen dieser Methode:  

-   **Computerkonto** des Standortservers  

Verwenden Sie diese Methode zum Ermitteln der Topologie Ihres Netzwerks und von Geräten in Ihrem Netzwerk, die über eine IP-Adresse verfügen. Bei der Netzwerkermittlung wird ein Netzwerk nach IP-fähigen Ressourcen durchsucht. Dazu werden Server abgefragt, auf denen eine Microsoft-Implementierung von DHCP, ARP-Caches (Address Resolution Protocol) in Routern, SNMP-fähige Geräte und Active Directory-Domänen ausgeführt werden.  

Falls Sie die Netzwerkermittlung verwenden möchten, müssen Sie die auszuführende **Ermittlungsebene** festlegen. Sie müssen außerdem mindestens einen Ermittlungsmechanismus konfigurieren, mit dessen Hilfe von der Netzwerkermittlung eine Abfrage nach Netzwerksegmenten oder -geräten ausgeführt werden kann. Außerdem können Sie Einstellungen festlegen, die die Steuerung von Ermittlungsaktionen im Netzwerk erleichtern. Abschließend definieren Sie mindestens einen Zeitplan für die Ausführung der Netzwerkermittlung.  

Die erfolgreiche Ermittlung einer Ressource mit dieser Methode setzt voraus, dass die IP-Adresse und die Subnetzmaske der Ressource von der Netzwerkermittlung identifiziert werden. Die folgenden Methoden werden verwendet, um die Subnetzmaske eines Objekts zu identifizieren:  

-   **Router-ARP-Cache:** Bei der Netzwerkermittlung wird der ARP-Cache eines Routers abgefragt, um Subnetzinformationen zu identifizieren. Daten in einem Router-ARP-Cache sind in der Regel nicht lange gültig. Wenn der ARP-Cache im Rahmen der Netzwerkermittlung abgefragt wird, sind Informationen zum angeforderten Objekt möglicherweise nicht mehr im ARP-Cache vorhanden.  

-   **DHCP:** Bei der Netzwerkermittlung wird jeder angegebene DHCP-Server abgefragt, um die Geräte zu ermitteln, für die eine Lease des DHCP-Servers verfügbar ist. Bei der Netzwerkermittlung werden nur DHCP-Server unterstützt, auf denen die Microsoft-Implementierung von DHCP ausgeführt wird.  

-   **SNMP-Gerät:** Bei der Netzwerkermittlung kann ein SNMP-Gerät direkt abgefragt werden. Damit ein Gerät bei der Netzwerkermittlung abgefragt werden kann, muss auf dem Gerät ein lokaler SNMP-Agent installiert sein. Sie müssen die Netzwerkermittlung zur Verwendung des Communitynamens konfigurieren, der vom SNMP-Agent verwendet wird.  

Wenn bei der Ermittlung ein IP-fähiges Objekt identifiziert wird und die Subnetzmaske des Objekts bestimmt werden kann, wird für dieses Objekt ein Discovery Data Record (DDR) erstellt. Da unterschiedliche Gerätetypen eine Verbindung mit dem Netzwerk herstellen können, werden bei der Netzwerkermittlung gegebenenfalls Ressourcen ermittelt, von denen die Configuration Manager-Clientsoftware nicht unterstützt werden kann. Zu den Geräten, die ermittelt, aber nicht verwaltet werden können, gehören beispielsweise Drucker und Router.  

Von der Netzwerkermittlung können mehrere Attribute als Teil des von ihr erstellten Ermittlungsdatensatzes zurückgegeben werden. Dazu gehören:  

-   NetBIOS-Name  

-   IP-Adressen  

-   Domäne der Ressource  

-   Systemrollen  

-   SNMP-Communityname  

-   MAC-Adressen  

Die Netzwerkermittlungsaktivität wird in der Datei **Netdisc.log** im Ordner **&lt;InstallationPath\>\Logs** auf dem Standortserver, auf dem die Ermittlung ausgeführt wird, aufgezeichnet.  

 Weitere Informationen zum Konfigurieren dieser Ermittlungsmethode finden Sie unter [Konfigurieren der Active Directory-Ermittlung in Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

> [!NOTE]  
>  Durch komplexe Netzwerke und Verbindungen mit geringer Bandbreite kann die Ausführung der Netzwerkermittlung beeinträchtigt werden und ein starker Netzwerkdatenverkehr entstehen. Es wird empfohlen, die Netzwerkermittlung nur auszuführen, wenn die zu ermittelnden Ressourcen von den anderen Ermittlungsmethoden nicht gefunden werden. Die Netzwerkermittlung bietet sich beispielsweise an, wenn Sie Arbeitsgruppencomputer ermitteln müssen. Arbeitsgruppencomputer werden von anderen Ermittlungsmethoden nicht erkannt.  

###  <a name="a-namebkmknetdisclevelsa-levels-of-network-discovery"></a><a name="BKMK_NetDiscLevels"></a> Ebenen der Netzwerkermittlung  
Beim Konfigurieren der Netzwerkermittlung stehen drei Ermittlungsebenen zur Auswahl:  

|Ermittlungsebene|Details|  
|------------------------|-------------|  
|Topologie|Auf dieser Ebene werden Router und Subnetze ermittelt. Es werden keine Subnetzmasken für Objekte identifiziert.|  
|Topologie und Client|Auf dieser Ebene werden zusätzlich zur Topologie auch potenzielle Clients wie Computer sowie Ressourcen wie Drucker und Router ermittelt. Es wird versucht, die Subnetzmaske der gefundenen Objekte zu identifizieren.|  
|Topologie, Client und Clientbetriebssystem|Auf dieser Ebene wird versucht, zusätzlich zur Topologie und zu potenziellen Clients den Namen und die Version des Computerbetriebssystems zu ermitteln. Dabei werden Windows-Browser- und Windows-Netzwerkaufrufe verwendet.|  

 Je höher die Stufe, desto stärker die Aktivität der Netzwerkermittlung und die Auslastung der Netzwerkbandbreite. Es empfiehlt sich, die Folgen für den Netzwerkdatenverkehr sorgfältig zu erwägen, bevor Sie alle Optionen der Netzwerkermittlung aktivieren.  

 Beispielsweise wäre es sinnvoll, sich beim ersten Einsatz der Netzwerkermittlung mit der Topologieebene zu begnügen und nur die Netzwerkinfrastruktur zu ermitteln. Anschließend könnten Sie die Netzwerkermittlung neu konfigurieren, damit auch Objekte und deren Gerätebetriebssysteme ermittelt werden. Sie könnten auch Einstellungen festlegen, durch die die Netzwerkermittlung auf bestimmte Netzwerksegmente beschränkt wird und nur Objekte an den erforderlichen Netzwerkorten ermittelt werden. Auf diese Weise können Sie unnötigen Netzwerkdatenverkehr und die Ermittlung von Objekten vermeiden, die sich auf Edgeroutern oder außerhalb des Netzwerks befinden.  

###  <a name="a-namebkmknetdiscoptionsa-network-discovery-options"></a><a name="BKMK_NetDiscOptions"></a> Optionen für die Netzwerkermittlung  
Damit bei der Netzwerkermittlung IP-fähige Geräte gesucht werden können, müssen Sie durch Konfigurieren mindestens einer der folgenden Optionen angeben, wie Geräte abgefragt werden sollen.  

> [!NOTE]  
>  Die Netzwerkermittlung wird im Kontext des Computerkontos auf dem Standortserver, auf dem die Ermittlung ausgeführt wird, ausgeführt. Falls das Computerkonto keine Berechtigungen für eine nicht vertrauenswürdige Domäne hat, kann es vorkommen, dass weder von der Serverkonfiguration „Domäne“, noch von der Konfiguration „DHCP“ Ressourcen ermittelt werden können.  

**DHCP:**  

Geben Sie alle DHCP-Server an, die bei der Netzwerkermittlung abgefragt werden sollen. (Bei der Netzwerkermittlung werden nur DHCP-Server unterstützt, auf denen die Microsoft-Implementierung von DHCP ausgeführt wird.)  

-   Bei der Netzwerkermittlung werden Informationen mithilfe von Remoteprozeduraufrufen an die Datenbank auf dem DHCP-Server abgerufen.  

-   Bei der Netzwerkermittlung können sowohl 32-Bit- als auch 64-Bit-DHCP-Server nach einer Liste der Geräte abgefragt werden, die bei den einzelnen Servern registriert sind.  

-   Ein DHCP-Server kann bei der Netzwerkermittlung nur erfolgreich abgefragt werden, wenn das Computerkonto des Servers, auf dem die Ermittlung ausgeführt wird, ein Mitglied der DHCP-Benutzergruppe auf dem DHCP-Server ist. Beispielsweise ist diese Zugriffsebene gegeben, wenn eine der folgenden Aussagen zutrifft:  

    -   Der angegebene DHCP-Server ist der DHCP-Server des Servers, auf dem die Ermittlung ausgeführt wird.  

    -   Der Computer, auf dem die Ermittlung ausgeführt wird, und der DHCP-Server befinden sich in der gleichen Domäne.  

    -   Zwischen dem Computer, auf dem die Ermittlung ausgeführt wird, und dem DHCP-Server ist eine bidirektionale Vertrauensstellung vorhanden.  

    -   Der Standortserver ist ein Mitglied der DHCP-Benutzergruppe.  

-   Wenn bei der Netzwerkermittlung ein DHCP-Server aufgezählt wird, können statische IP-Adressen nicht immer ermittelt werden. Bei der Netzwerkermittlung werden keine IP-Adressen gefunden, die einem ausgeschlossenen IP-Adressbereich auf dem DHCP-Server angehören. IP-Adressen, die für die manuelle Zuweisung reserviert sind, werden ebenfalls nicht ermittelt.  

**Domänen:**  

Geben Sie alle Domänen an, die bei der Netzwerkermittlung abgefragt werden sollen.  

-   Das Computerkonto des Standortservers, auf dem die Ermittlung ausgeführt wird, muss für die Domänencontroller in allen angegebenen Domänen über eine Leseberechtigung verfügen.  

-   Zum Ermitteln von Computern in der lokalen Domäne müssen Sie auf mindestens einem Computer den Computersuchdienst aktivieren. Der Computer muss sich dabei im gleichen Subnetz wie der Standortserver befinden, auf dem die Netzwerkermittlung ausgeführt wird.  

-   Bei der Netzwerkermittlung kann jeder Computer ermittelt werden, den Sie beim Durchsuchen des Netzwerks auf dem Standortserver anzeigen können.  

-   Zuerst wird die IP-Adresse abgerufen, und dann wird jedes gefundene Gerät mit einer ICMP-Echoanforderung (Internet Control Message-Protokoll) gepingt. Mit dem Befehl **ping** können Sie feststellen, welche Computer zurzeit aktiv sind.  

**SNMP-Geräte:**  

Geben Sie alle SNMP-Geräte an, die bei der Netzwerkermittlung abgefragt werden sollen.  

-   Bei der Netzwerkermittlung wird von jedem SNMP-Gerät, von dem keine Antwort auf die Abfrage eingeht, der Wert „ipNetToMediaTable“ abgerufen. Von diesem Wert werden Arrays von IP-Adressen zurückgegeben, bei denen es sich um Clientcomputer oder andere Ressourcen wie Drucker, Router oder sonstige IP-fähige Geräte handelt.  

-   Zum Abfragen eines Geräts müssen Sie die IP-Adresse oder den NetBIOS-Namen dieses Geräts angeben.  

-   Sie müssen die Netzwerkermittlung für die Verwendung des Communitynamens des Geräts konfigurieren. Andernfalls wird die SNMP-basierte Abfrage vom Gerät abgelehnt.  

###  <a name="a-namebkmklimitnetdisca-limiting-network-discovery"></a><a name="BKMK_LimitNetDisc"></a> Beschränken der Netzwerkermittlung  
Beim Abfragen eines SNMP-Geräts am Rand des Netzwerks können von der Netzwerkermittlung Informationen über Subnetze und SNMP-Geräte identifiziert werden, die sich außerhalb des unmittelbaren Netzwerks befinden. Sie können mithilfe der folgenden Informationen die Netzwerkermittlung beschränken. Dazu konfigurieren Sie die SNMP-Geräte, bei denen die Kommunikation mit der Ermittlung möglich ist, und geben die abzufragenden Netzwerksegmente an.  

**Subnetze:**  

Konfigurieren Sie die Subnetze, die bei der Netzwerkermittlung abgefragt werden, sofern die Ermittlungsoptionen SNMP-Geräte und DHCP ausgewählt wurden. Von diesen beiden Optionen werden nur die aktivierten Subnetze durchsucht.  

Beispielsweise können von einer DHCP-Anforderung Geräte von Orten im gesamten Netzwerk zurückgegeben werden. Falls Sie nur Geräte in einem bestimmten Subnetz ermitteln möchten, müssen Sie im Dialogfeld **Eigenschaften von Netzwerkermittlung** auf der Registerkarte **Subnetze** dieses Subnetz angeben und aktivieren. Wenn Sie Subnetze angeben und aktivieren, beschränken Sie künftige DHCP- und SNMP-Ermittlungsvorgänge auf diese Subnetze.  

> [!NOTE]  
>  Die Objekte, die von der Ermittlungsoption Domänen ermittelt werden, werden durch die Subnetzkonfigurationen nicht beschränkt.  

**SNMP-Community-Namen:**  

Damit ein SNMP-Gerät erfolgreich abgefragt werden kann, müssen Sie beim Konfigurieren der Netzwerkermittlung den Communitynamen des Geräts angeben. Wird die Netzwerkermittlung nicht anhand des Communitynamens des SNMP-Geräts konfiguriert, wird die Abfrage vom Gerät abgelehnt.  

**Maximale Hopanzahl:**  

Wenn Sie die maximale Anzahl der Routerhops festlegen, schränken Sie die Anzahl der Netzwerksegmente und Router ein, die von der Netzwerkermittlung mithilfe von SNMP abgefragt werden kann.  

-   Durch die konfigurierte Hopanzahl wird die Anzahl der zusätzlichen Geräte und Netzwerksegmente eingeschränkt, die bei der Netzwerkermittlung abgefragt werden können.  

 Beispielsweise wird bei einer auf die Topologie beschränkten Ermittlung mit **0** (null) Routerhops das Subnetz ermittelt, in dem sich der ursprüngliche Server befindet, und alle Router in diesem Subnetz werden mit eingeschlossen.  

Im folgenden Diagramm ist dargestellt, was bei einer auf die Topologie beschränkten Netzwerkermittlung gefunden wird, wenn sie auf Server 1 ausgeführt wird und 0 Routerhops angegeben sind: Subnetz D und Router 1.  

 ![Bild der Ermittlung mit 0 (null) Routerjumps](media/Disc-0.gif)  

 Im folgenden Diagramm ist dargestellt, was bei einer Topologie- und Clientnetzwerkermittlung gefunden wird, wenn sie auf Server 1 ausgeführt wird und 0 Routerhops angegeben sind: Subnetz D, Router 1 und alle potenziellen Clients in Subnetz D.  

 ![Bild der Ermittlung mit 1 (einem) Routerjump](media/Disc-1.gif)  

 Damit Sie besser verstehen, wie Routerhops die Anzahl der ermittelten Netzwerkressourcen erhöhen können, stellen Sie sich folgendes Netzwerk vor:  

 ![Bild der Ermittlung mit 2 (zwei) Routerjumps](media/Disc-2.gif)  

 Beim Ausführen einer nur auf die Topologie bezogenen Netzwerkermittlung auf Server 1 mit einem einzigen Routerhop wird Folgendes ermittelt:  

-   Router 1 und Subnetz 10.1.10.0 (nach 0 Hops gefunden).  

-   Subnetze 10.1.20.0 und 10.1.30.0, Subnetz A und Router 2 (auf dem ersten Hop gefunden).  

> [!WARNING]  
>  Durch jede Erhöhung der Anzahl von Routerhops kann die Anzahl der ermittelten Ressourcen deutlich erhöht und die von der Netzwerkermittlung verwendete Netzwerkbandbreite gesteigert werden.  

##  <a name="a-namebkmkaboutservera-server-discovery"></a><a name="bkmk_aboutServer"></a> Serverermittlung  
**Konfigurierbar:** Nein  

Zusätzlich zu den benutzerkonfigurierbaren Ermittlungsmethoden wird von Configuration Manager auch ein als **Serverermittlung** (SMS_WINNT_SERVER_DISCOVERY_AGENT) bezeichneter Prozess verwendet. Bei dieser Ermittlungsmethode werden Ressourceneinträge für Computer, bei denen es sich um Standortsysteme handelt, erstellt. Dazu gehören beispielsweise Computer, die als Verwaltungspunkte konfiguriert sind.  

##  <a name="a-namebkmkshareda-common-features-of-active-directory-group-system-and-user-discovery"></a><a name="bkmk_shared"></a> Allgemeine Funktionen der Active Directory-Gruppen-, System- und Benutzerermittlung  
Dieser Abschnitt enthält Informationen zu den Funktionen, die folgende Ermittlungsmethoden gemeinsam haben:  

-   Active Directory-Gruppenermittlung  

-   Active Directory-Systemermittlung  

-   Active Directory-Benutzerermittlung  

> [!NOTE]  
>  Die Informationen in diesem Abschnitt gelten nicht für die Active Directory-Gesamtstrukturermittlung.  

Diese drei Ermittlungsmethoden weisen Ähnlichkeiten in Bezug auf die Konfiguration und die Vorgänge auf. Mit ihnen können Computer, Benutzer und Informationen über die Gruppenmitgliedschaften von Ressourcen, die in den Active Directory-Domänendiensten gespeichert sind, ermittelt werden. Der Ermittlungsprozess wird von einem Ermittlungs-Agent verwaltet. Dieser wird an jedem Standort, an dem die Ermittlung konfigurationsgemäß ausgeführt werden soll, auf dem Standortserver ausgeführt. Sie können für jede dieser Ermittlungsmethoden festlegen, dass mindestens ein Active Directory-Ort als Ortsinstanz in der lokalen Gesamtstruktur oder in Remotegesamtstrukturen durchsucht werden soll.  

Beim Durchsuchen einer als nicht vertrauenswürdig eingestuften Gesamtstruktur nach Ressourcen muss vom Ermittlungs-Agent Folgendes aufgelöst werden können:  

-   Der FQDN der Ressource muss vom Ermittlungs-Agent aufgelöst werden können, um eine Computerressource mit der Active Directory-Systemermittlung zu ermitteln. Ist dies nicht möglich, wird versucht, die Ressource anhand ihres NetBIOS-Namens aufzulösen.  

-   Der FQDN des von Ihnen für den Active Directory-Ort angegebenen Domänencontrollernamens muss vom Ermittlungs-Agent aufgelöst werden können, um einen Benutzer oder eine Benutzergruppe mit der Active Directory-Benutzerermittlung oder der Active Directory-Gruppenermittlung zu ermitteln.  

Sie können für jeden von Ihnen angegebenen Ort individuelle Suchoptionen konfigurieren. Beispielsweise können Sie das rekursive Durchsuchen der untergeordneten Active Directory-Container an diesen Orten aktivieren. Außerdem können Sie ein eindeutiges Konto konfigurieren, das beim Durchsuchen dieses Orts verwendet werden soll. Sie haben somit die flexible Möglichkeit, eine Ermittlungsmethode an einem Standort zu konfigurieren und zum Durchsuchen mehrerer Active Directory-Orte in vielen Gesamtstrukturen anzuweisen, ohne ein einzelnes Konto mit Berechtigungen für sämtliche Orte konfigurieren zu müssen.  

Bei der Ausführung dieser drei Ermittlungsmethoden an einem bestimmten Standort wird vom Configuration Manager-Standortserver an diesem Standort eine Verbindung mit dem nächstgelegenen Domänencontroller in der angegebenen Active Directory-Gesamtstruktur hergestellt, um Active Directory-Ressourcen zu suchen. Die Domäne und die Gesamtstruktur können sich in einem beliebigen unterstützten Active Directory-Modus befinden. Das Konto, das Sie jeder Ortsinstanz zuweisen, muss über die Berechtigung **Lesen** für die angegebenen Active Directory-Orte verfügen. Bei der Ermittlung werden zunächst die angegebenen Orte nach Objekten durchsucht. Anschließend wird versucht, Informationen über diese Objekte zu sammeln. Falls genügend Informationen zu einer Ressource identifiziert werden können, wird ein DDR erstellt. Welche Informationen erforderlich sind, hängt jeweils von der verwendeten Ermittlungsmethode ab.  

Sie können die gleiche Ermittlungsmethode für die Ausführung an mehreren Configuration Manager-Standorten konfigurieren, um den Vorteil von Abfragen an die lokalen Active Directory-Server zu nutzen. In diesem Fall können Sie jeden Standort mit einem eindeutigen Satz von Ermittlungsoptionen konfigurieren. Da die Ermittlungsdaten für alle Standorte in der Hierarchie freigegeben werden, sollten Sie ein Überlappen zwischen diesen Konfigurationen vermeiden, um jede Ressource effektiv ein Mal ermitteln zu können. In kleineren Umgebungen können Sie erwägen, jede Ermittlungsmethode nur an einem einzigen Standort in der Hierarchie auszuführen. So können Sie den Verwaltungsaufwand gering halten und die Wahrscheinlichkeit, dass die gleichen Ressourcen von mehreren Ermittlungsaktionen ermittelt werden, senken. Wenn Sie die Anzahl von Standorten, an denen die Ermittlung ausgeführt wird, so gering wie möglich halten, können Sie dadurch die gesamte Netzwerkbandbreite, die von der Ermittlung verwendet wird, sowie die Gesamtzahl von DDRs, die von den Standortservern erstellt und verarbeitet werden müssen, senken.  

Viele Konfigurationen von Ermittlungsmethoden sind selbsterklärend. In den nachfolgenden Abschnitten finden Sie weitere Informationen, die Sie möglicherweise benötigen, bevor Sie sie die entsprechenden Ermittlungsoptionen konfigurieren.  

Die folgenden Optionen stehen für die Verwendung mit mehreren Active Directory-Ermittlungsmethoden zur Verfügung:  

-   [Deltaermittlung](#bkmk_delta)  

-   [Filtern veralteter Computerdatensätze bei der Domänenanmeldung](#bkmk_stalelogon)  

-   [Filtern veralteter Datensätze nach Computerkennwort](#bkmk_stalepassword)  

-   [Suchen nach benutzerdefinierten Attributen von Active Directory](#bkmk_customAD)  

###  <a name="a-namebkmkdeltaa-delta-discovery"></a><a name="bkmk_delta"></a> Deltaermittlung  
Verfügbar für:  

-   Active Directory-Gruppenermittlung  

-   Active Directory-Systemermittlung  

-   Active Directory-Benutzerermittlung  

Deltaermittlung ist eine unabhängige Ermittlungsmethode, jedoch als Option für die entsprechenden Methoden verfügbar. Deltaermittlung sucht bestimmte Active Directory-Attribute für die Änderungen, die seit dem letzten vollständigen Ermittlungszyklus der entsprechenden Ermittlungsmethode vorgenommen wurden.  Diese Suche benötigt weniger Ressourcen als bei einem vollständigen Ermittlungszyklus, und die Attributänderungen werden an die Configuration Manager-Datenbank zur Aktualisierung des Ermittlungsdatensatzes der Ressource gesendet.  

Die Deltaermittlung wird standardmäßig in einem Fünfminutenzyklus ausgeführt. Dies ist sehr viel häufiger als der normale Zeitplan für einen vollständigen Ermittlungszyklus.  Dieser häufige Zyklus ist möglich, da Deltaermittlung weniger Standortserver- und Netzwerkressourcen verwendet als ein vollständiger Ermittlungszyklus. Bei der Verwendung der Deltaermittlung können Sie die Häufigkeit des vollständigen Ermittlungszyklus der betreffenden Ermittlungsmethode reduzieren.  

Die gängigsten Änderungen, die von der Deltaermittlung erkannt werden, sind:  

-   Neue Computer oder Benutzer, die Active Directory hinzugefügt wurden  

-   Änderungen an grundlegenden Computer- und Benutzerinformationen  

-   Neue Computer oder Benutzer, die einer Gruppe hinzugefügt wurden  

-   Computer oder Benutzer, die aus einer Gruppe entfernt wurden  

-   Änderungen an Systemgruppenobjekten  

Bei der Deltaermittlung können zwar neue Ressourcen und Änderungen an der Gruppenmitgliedschaft erkannt werden, jedoch nicht, ob eine Ressource aus dem Active Directory gelöscht wurde. DDRs, die von der Deltaermittlung erstellt werden, werden wie von einem vollständigen Ermittlungszyklus erstellte DDRs verarbeitet.  

Die Deltaermittlung wird in den Eigenschaften einer Ermittlungsmethode auf der Registerkarte **Abfragezeitplan** konfiguriert.  

###  <a name="a-namebkmkstalelogona-filter-stale-computer-records-by-domain-logon"></a><a name="bkmk_stalelogon"></a> Filtern veralteter Computerdatensätze bei der Domänenanmeldung  
Verfügbar für:  

-   Active Directory-Gruppenermittlung  

-   Active Directory-Systemermittlung  

Sie können die Ermittlung so konfigurieren, dass veraltete Computerdatensätze auf Basis der letzten Domänenanmeldung des Computers von der Ermittlung ausgeschlossen werden. Wenn diese Option aktiviert ist, wird jeder identifizierte Computer von der Active Directory-Systemermittlung ausgewertet. Von der Active Directory-Gruppenermittlung wird jeder Computer ausgewertet, der Mitglied in einer ermittelten Gruppe ist.  

Verwendungszweck der Option:  

-   Computer müssen so konfiguriert werden, dass das Attribut **LastLogonTimeStamp** in Active Directory Domain Services aktualisiert wird.  

-   Die Active Directory-Domänenfunktionsebene muss auf Windows Server 2003 oder höher festgelegt sein.  

Berücksichtigen Sie das Intervall der Replikation zwischen Domänencontrollern, wenn Sie die Zeit nach der letzten Anmeldung konfigurieren, die Sie verwenden möchten.  

Konfigurieren Sie das Filtern auf der Registerkarte **Option** sowohl im Dialogfeld **Eigenschaften der Active Directory-Systemermittlung** als auch im Dialogfeld **Eigenschaften der Active Directory-Gruppenermittlung** , indem Sie die Option **Nur Computer ermitteln, die in einem bestimmten Zeitraum bei einer Domäne angemeldet waren**auswählen.  

> [!WARNING]  
>  Wenn Sie diesen Filter konfigurieren und **Filtern veralteter Datensätze nach Computerkennwort** verwenden, werden Computer, die die Kriterien mindestens eines Filters erfüllen, von der Ermittlung ausgeschlossen.  

###  <a name="a-namebkmkstalepassworda-filter-stale-records-by-computer-password"></a><a name="bkmk_stalepassword"></a> Filtern veralteter Datensätze nach Computerkennwort  
Verfügbar für:  

-   Active Directory-Gruppenermittlung  

-   Active Directory-Systemermittlung  

Sie können die Ermittlung so konfigurieren, dass Computer mit veralteten Computerdatensätzen auf Basis der letzten Aktualisierung des Computerkontokennworts von der Ermittlung ausgeschlossen werden. Wenn diese Option aktiviert ist, wird jeder identifizierte Computer von der Active Directory-Systemermittlung ausgewertet. Von der Active Directory-Gruppenermittlung wird jeder Computer ausgewertet, der Mitglied in einer ermittelten Gruppe ist.  

Verwendungszweck der Option:  

-   Computer müssen so konfiguriert werden, dass das Attribut **pwdLastSet** in Active Directory Domain Services aktualisiert wird.  

Berücksichtigen Sie das Updateintervall des Attributs sowie das Intervall der Replikation zwischen Domänencontrollern, wenn Sie diese Option konfigurieren.  

Konfigurieren Sie das Filtern auf der Registerkarte **Option** sowohl im Dialogfeld **Eigenschaften der Active Directory-Systemermittlung** als auch im Dialogfeld **Eigenschaften der Active Directory-Gruppenermittlung** , indem Sie die Option **Nur Computer ermitteln, von denen in einem bestimmten Zeitraum das Kennwort für das Computerkonto aktualisiert wurde**auswählen.  

> [!WARNING]  
>  Wenn Sie diesen Filter konfigurieren und **Filtern veralteter Datensätze nach Anmeldung an der Domäne** verwenden, werden Computer, die die Kriterien mindestens eines Filters erfüllen, von der Ermittlung ausgeschlossen.  

###  <a name="a-namebkmkcustomada-search-customized-active-directory-attributes"></a><a name="bkmk_customAD"></a> Suchen nach benutzerdefinierten Attributen von Active Directory  
 Verfügbar für:  

-   Active Directory-Systemermittlung  

-   Active Directory-Benutzerermittlung  

Von jeder Ermittlungsmethode wird eine eindeutige Liste von Active Directory Attributen, die ermittelt werden können, unterstützt.  

Prüfen und konfigurieren Sie die Liste benutzerdefinierter Attribute auf der Registerkarte **Active Directory-Attribute** sowohl im Dialogfeld **Eigenschaften der Active Directory-Systemermittlung** als auch im Dialogfeld **Eigenschaften der Active Directory-Benutzerermittlung**.  



<!--HONumber=Nov16_HO1-->

