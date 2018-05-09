---
title: Tasksequenzschritte
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Schritte, die Sie einer Configuration Manager-Tasksequenz hinzufügen können.
ms.date: 03/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a678cbbd8500070e2d4056d6e424818e7000ef83
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Tasksequenzschritte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die folgenden Tasksequenzschritte können einer Configuration Manager-Tasksequenz hinzugefügt werden. Weitere Informationen zum Bearbeiten einer Tasksequenz finden Sie unter [Edit a task sequence](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

Folgende Einstellungen gelten für alle Tasksequenzschritte:

Auf der Registerkarte **Eigenschaften**:
 - **Name:** Der Tasksequenz-Editor erfordert, dass Sie einen kurzen Namen zur Beschreibung dieses Schritts angeben. Wenn Sie einen neuen Schritt hinzufügen, legt der Tasksequenz-Editor den Namen standardmäßig auf den Typ fest. Der **Name** darf nicht länger als 50 Zeichen sein.
 - **Beschreibung:** Geben Sie optional ausführlichere Informationen zu diesem Schritt an. Die **Beschreibung** darf nicht länger als 256 Zeichen sein.
Im weiteren Verlauf dieses Artikels werden andere Einstellungen der Registerkarte **Eigenschaften** für jeden Tasksequenzschritt beschrieben.

Auf der Registerkarte **Optionen**:  
-   **Diesen Schritt deaktivieren:** Die Tasksequenz überspringt diesen Schritt, wenn sie auf einem Computer ausgeführt wird. Das Symbol für diesen Schritt wird im Tasksequenz-Editor abgeblendet. 
-   **Bei Fehler fortsetzen:** Die Tasksequenz wird fortgeführt, wenn bei der Ausführung dieses Schritts ein Fehler auftritt.  
-   **Bedingung hinzufügen:** Die Tasksequenz wertet diese bedingten Anweisungen aus, um zu bestimmen, ob der Schritt ausgeführt wird.   
In den folgenden Abschnitten werden andere mögliche Einstellungen für bestimmte Tasksequenzschritte auf der Registerkarte **Optionen** beschrieben.



##  <a name="BKMK_ApplyDataImage"></a> Anwenden von Datenimages   
 Mithilfe dieses Schritts können Sie das Datenimage auf die angegebene Zielpartition kopieren.  

 Dieser Schritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen finden Sie unter [Tasksequenz-Aktionsvariablen](task-sequence-action-variables.md).  

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Images** > **Apply Data Image** (Datenimage anwenden), um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Imagepaket**  
 Klicken Sie auf **Durchsuchen**, um das **Imagepaket** festzulegen, das von dieser Tasksequenz verwendet wird. Wählen Sie das zu installierende Paket im Dialogfeld **Paket auswählen** aus. Die zugeordneten Eigenschaftsinformationen für jedes vorhandene Abbildpaket werden unten im Dialogfeld **Paket auswählen** angezeigt. Wählen Sie mithilfe der Dropdownliste das zu installierende **Abbild** aus dem ausgewählten **Abbildpaket**aus.  

> [!NOTE]  
>  In dieser Tasksequenzaktion wird das Image als Datendatei behandelt. Diese Aktion führt kein Setup aus, um das Image als Betriebssystem zu starten.  

 **Ziel**  
 Konfigurieren Sie eine der folgenden Optionen:

-   **Nächste verfügbare Partition:** Verwendet die nächste verfügbare Partition, die in dieser Tasksequenz nicht bereits für eine Aktion **Betriebssystem anwenden** oder **Datenimage anwenden** verwendet wurde.  

-   **Bestimmter Datenträger und Partition:** Wählen Sie die Nummer des **Datenträgers** (beginnend mit 0) und die Nummer der **Partition** (beginnend mit 1) aus.  

-   **Bestimmter Buchstabe für logisches Laufwerk:** Geben Sie den **Laufwerkbuchstaben** ein, der der Partition von Windows PE zugewiesen wurde. Dieser Laufwerkbuchstabe kann sich von dem Laufwerkbuchstaben unterscheiden, der von dem neu bereitgestellten Betriebssystem zugewiesen wird.  

-   **In Variable gespeicherter Buchstabe für logisches Laufwerk:** Geben Sie die Tasksequenzvariable an, die den der Partition von Windows PE zugewiesenen Laufwerksbuchstaben enthält. Diese Variable wird in der Regel im Bereich „Erweitert“ des Dialogfelds **Partitionseigenschaften** für die Tasksequenzaktion **Datenträger formatieren und partitionieren** festgelegt.  

**Vor dem Anwenden des Images den gesamten Inhalt der Partition löschen**  
 Legt fest, dass die Tasksequenz alle Dateien auf der Zielpartition löscht, bevor das Image installiert wird. Indem der Inhalt dieser Partition nicht gelöscht wird, kann mit diesem Schritt einer zuvor eingerichteten Partition weiterer Inhalt zugewiesen werden.  



##  <a name="BKMK_ApplyDriverPackage"></a> Treiberpaket anwenden  
 Mithilfe dieses Schritts können Sie alle Treiber im Treiberpaket herunterladen und auf dem Windows-Betriebssystem installieren.

 Mit dem Tasksequenzschritt **Treiberpaket anwenden** können Sie alle Gerätetreiber eines Treiberpakets zur Verwendung in Windows bereitstellen. Fügen Sie diesen Schritt zwischen den Schritten **Betriebssystem anwenden** und **Windows und ConfigMgr einrichten** hinzu, um die Treiber in diesem Paket für Windows zur Verfügung zu stellen. Der Schritt **Treiberpaket anwenden** wird in der Regel hinter dem Schritt **Treiber automatisch anwenden** eingefügt. Der Tasksequenzschritt **Treiberpaket anwenden** ist auch für die Bereitstellung mithilfe eigenständiger Medien nützlich.  

 Stellen Sie sicher, dass ähnliche Gerätetreiber in einem Treiberpaket zusammengestellt werden, und verteilen Sie diese auf die entsprechenden Verteilungspunkte. Nachdem die Treiber verteilt sind, können sie von Configuration Manager-Clientcomputern installiert werden. Packen Sie beispielsweise alle Treiber eines Herstellers in ein Treiberpaket. Verteilen Sie das Paket anschließend an Verteilungspunkte, auf die die entsprechenden Computer zugreifen können.

 Der Schritt **Treiberpaket anwenden** ist für eigenständige Medien nützlich. Dieser Schritt ist ebenfalls nützlich, wenn Sie eine bestimmte Gruppe von Treibern installieren möchten. Hierzu zählen die Treiber für Geräte, die nicht durch eine Plug & Play-Überprüfung erkannt werden, z.B. Netzwerkdrucker.  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Apply Driver Package Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Treiber** > **Treiberpaket anwenden**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Treiberpaket**  
 Klicken Sie auf **Durchsuchen** , und öffnen Sie das Dialogfeld **Paket auswählen** , um das Treiberpaket anzugeben, das die erforderlichen Gerätetreiber enthält. Geben Sie ein vorhandenes Paket an, das verfügbar gemacht werden soll. Die zugehörigen Paketeigenschaften werden unten im Dialogfeld angezeigt.  

 **Wählen Sie den Massenspeichertreiber im Paket aus, der bei allen Betriebssystemen vor Vista vor dem Setup installiert werden muss**  
 Geben Sie alle Massenspeichertreiber an, die für die Installation eines klassischen Betriebssystems erforderlich sind.  

 **Treiber**  
 Wählen Sie die Datei für die Installation der Massenspeichertreiber aus, bevor Sie ein klassisches Betriebssystem einrichten. Die Dropdownliste wird mit den Treibern aus dem angegebenen Paket aufgefüllt.  

 **Modell**  
 Geben Sie das für den Systemstart erforderliche Gerät an, das für Bereitstellungen von Betriebssystemen vor Windows Vista erforderlich ist.  

 **Unbeaufsichtigte Installation von nicht signierten Treibern bei Windows-Versionen ausführen, wenn zulässig**  
 Durch diese Option können Sie unter Windows Treiber ohne digitale Signatur installieren.  



##  <a name="BKMK_ApplyNetworkSettings"></a> Anwenden von Netzwerkeinstellungen   
 Mithilfe dieses Schritts können Sie die Konfigurationsinformationen für das Netzwerk oder die Arbeitsgruppe des Zielcomputers angeben. Die Tasksequenz speichert diese Werte in der entsprechenden Antwortdatei. Windows Setup verwendet diese Antwortdatei während der Aktion **Windows und ConfigMgr einrichten**.  

 Dieser Tasksequenzschritt wird entweder in einem Standardbetriebssystem oder in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Apply Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Einstellungen** > **Netzwerkeinstellungen anwenden**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Einer Arbeitsgruppe beitreten**  
 Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Arbeitsgruppe hinzuzufügen. Geben Sie den Namen der Arbeitsgruppen in die Zeile **Arbeitsgruppe** ein. Dieser Wert kann durch den Wert überschrieben werden, der mit dem Tasksequenzschritt **Netzwerkeinstellungen erfassen** erfasst wird.  

 **Einer Domäne beitreten**  
 Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Domäne hinzuzufügen. Geben Sie die Domäne an, oder klicken Sie auf "Durchsuchen", um die Domäne auszuwählen, z. B. *fabricam.com*. Geben Sie einen LDAP-Pfad (Lightweight Directory Access Protocol) für eine Organisationseinheit an, oder suchen Sie nach einem LDAP-Pfad. Beispiel: *LDAP//OU=computers, DC=Fabricam.com, C=com*  

 **Konto**  
 Klicken Sie auf **Festlegen** , um ein Konto anzugeben, das die für den Beitritt zur Domäne erforderlichen Berechtigungen aufweist. Im Dialogfeld **Windows-Benutzerkonto** können Sie den Benutzernamen in folgendem Format eingeben: **Domäne\Benutzer**.  

 **Netzwerkkarteneinstellungen**  
 Geben Sie die Netzwerkkonfigurationen für alle Netzwerkadapter auf dem Computer an. Klicken Sie auf **Neu** , um das Dialogfeld **Netzwerkeinstellungen** zu öffnen, und geben Sie dann die Netzwerkeinstellungen an. Wenn Sie ebenfalls den Schritt **Netzwerkeinstellungen erfassen** verwenden, wendet die Tasksequenz die zuvor erfassten Einstellungen auf den Netzwerkadapter an. Die Tasksequenz wendet nicht die Einstellungen an, die Sie in diesem Schritt festlegen. Wenn die Tasksequenz zuvor keine Netzwerkeinstellungen erfasst hat, werden die im Schritt **Netzwerkeinstellungen anwenden** festgelegten Einstellungen angewendet. Die Tasksequenz wendet diese Einstellungen in der Reihenfolge der Windows-Gerätenummern auf Netzwerkadapter an.  



##  <a name="BKMK_ApplyOperatingSystemImage"></a> Betriebssystemimage anwenden  

> [!TIP]  
> Ab Windows 10 (Version 1709) enthalten Medien mehrere Editionen. Wenn Sie eine Tasksequenz konfigurieren, um ein Betriebssystemupgradepaket oder ein Betriebssystemimage zu verwenden, achten Sie darauf, eine [unterstützte Edition](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client) auszuwählen.

 Verwenden Sie diesen Schritt, um ein Betriebssystem auf dem Zielcomputer zu installieren. Die Aktionen dieses Schritts hängen davon ob, ein Betriebssystemimage oder ein Betriebssystemupgradepaket verwendet wird.  

 Wenn ein Betriebssystemimage verwendet wird, werden mit dem Schritt **Betriebssystemimage anwenden** folgende Aktionen ausgeführt:  

1.  Alle Inhalte auf dem Zielvolume werden gelöscht, außer die Dateien in dem Ordner, der von der Variable „_SMSTSUserStatePath“ angegeben wird.

2.  Alle Inhalte der angegebenen WIM-Datei werden in die angegebene Zielpartition extrahiert.  

3.  Die Antwortdatei wird vorbereitet:  

    1.  Eine neue Standardantwortdatei für Windows Setup („sysprep.inf“ oder „unattend.xml“) wird für das bereitzustellende Betriebssystem erstellt.  

    2.  Alle Werte aus der vom Benutzer bereitgestellten Antwortdatei werden zusammengeführt.  

4.  Windows-Startladeprogramme werden in die aktive Partition kopiert.  

5.  Legen Sie die Datei „boot.ini“ bzw. die Startkonfigurationsdaten (Boot Configuration Data, BCD) so fest, dass sie auf das neu installierte Betriebssystem verweist.  

 Wenn ein Betriebssystemupgradepaket verwendet wird, werden mit dem Schritt **Betriebssystemimage anwenden** folgende Aktionen ausgeführt:  

1.  Alle Inhalte auf dem Zielvolume werden gelöscht, außer die Dateien in dem Ordner, der von der Variable „_SMSTSUserStatePath“ angegeben wird.  

2.  Die Antwortdatei wird vorbereitet:  

    1.  Eine neue Antwortdatei mit von Configuration Manager erstellten Standardwerten wird erstellt.  

    2.  Alle Werte aus der vom Benutzer bereitgestellten Antwortdatei werden zusammengeführt.  

> [!NOTE]  
>  Der Schritt **Windows und ConfigMgr einrichten** startet die Installation von Windows. 

 Nach Ausführung der Aktion **Betriebssystem anwenden** wird die Variable „OSDTargetSystemDrive“ auf den Laufwerksbuchstaben der Partition festgelegt, in der sich die Betriebssystemdateien befinden.  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Apply Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Images** > **Apply Operating System Image** (Betriebssystemimage anwenden), um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Betriebssystem von einem erfassten Image übernehmen**  
 Installiert ein zuvor erfasstes Betriebssystemabbild. Klicken Sie auf **Durchsuchen** , um das Dialogfeld **Paket auswählen** zu öffnen, und wählen Sie dann das vorhandene Abbildpaket aus, das Sie installieren möchten. Wenn mehrere Images mit dem angegebenen **Imagepaket**verknüpft sind, geben Sie das zugehörige Image für diese Bereitstellung mithilfe der Dropdownliste an. Sie können zu jedem vorhandenen Abbild grundlegende Informationen anzeigen, indem Sie auf das Abbild klicken.  

 **Betriebssystem von einer ursprünglichen Installationsquelle übernehmen**  
 Installiert ein Betriebssystem mithilfe einer ursprünglichen Installationsquelle. Klicken Sie auf **Durchsuchen**, um das Dialogfeld **Betriebssysteminstallationspaket auswählen** zu öffnen. Wählen Sie dann das vorhandene Betriebssystemupgradepaket aus, das Sie verwenden möchten. Sie können zu jeder vorhandenen Abbildquelle grundlegende Informationen anzeigen, indem Sie auf die Abbildquelle klicken. Die zugeordneten Eigenschaften der Abbildquelle werden unten im Dialogfeld im Ergebnisbereich angezeigt. Falls dem angegebenen Paket mehrere Editionen zugeordnet sind, geben Sie die verwendete zugeordnete **Edition** in der Dropdownliste an.  

 **Datei für unbeaufsichtigte Installation oder Antwortdatei für Systemvorbereitung bei benutzerdefinierter Installation verwenden**  
 Stellen Sie mit dieser Option je nach Betriebssystemversion und Installationsmethode eine Windows Setup-Antwortdatei (**unattend.xml**, **unattend.txt**oder **sysprep.inf**) bereit. Die von Ihnen angegebene Datei kann alle Standardkonfigurationsoptionen enthalten, die von Windows-Antwortdateien unterstützt werden. Sie können damit beispielsweise die Standardstartseite im Internet Explorer angeben. Geben Sie das Paket mit der Antwortdatei sowie den entsprechenden Pfad zu der Datei im Paket an.  

> [!NOTE]  
>  Die angegebene Windows Setup-Antwortdatei kann eingebettete Tasksequenzvariablen im Format %*varname*% enthalten, wobei *varname* den Namen der Variable darstellt. Der Schritt **Windows und ConfigMgr einrichten** ersetzt die Zeichenfolge %*varname*% durch die richtigen Variablenwerte. Diese eingebetteten Tasksequenzvariablen können nicht in den rein numerischen Feldern in der Antwortdatei „unattend.xml“ verwendet werden.  

 Wenn Sie keine Windows Setup-Antwortdatei angeben, generiert diese Tasksequenzaktion automatisch eine Antwortdatei.  

 **Ziel**  
 Konfigurieren Sie eine der folgenden Optionen:  

-   **Nächste verfügbare Partition:** Verwendet die nächste verfügbare Partition, die in dieser Tasksequenz nicht bereits für eine Aktion **Betriebssystem anwenden** oder **Datenimage anwenden** verwendet wurde. 

-   **Bestimmter Datenträger und Partition:** Wählen Sie die Nummer des **Datenträgers** (beginnend mit 0) und die Nummer der **Partition** (beginnend mit 1) aus.  

-   **Bestimmter Buchstabe für logisches Laufwerk:** Geben Sie den **Laufwerkbuchstaben** ein, der der Partition von Windows PE zugewiesen wurde. Dieser Laufwerkbuchstabe kann sich von dem Laufwerkbuchstaben unterscheiden, der von dem neu bereitgestellten Betriebssystem zugewiesen wird.  

-   **In Variable gespeicherter Buchstabe für logisches Laufwerk:** Geben Sie die Tasksequenzvariable an, die den der Partition von Windows PE zugewiesenen Laufwerksbuchstaben enthält. Diese Variable wird in der Regel im Bereich „Erweitert“ des Dialogfelds **Partitionseigenschaften** für die Tasksequenzaktion **Datenträger formatieren und partitionieren** festgelegt.  

### <a name="options"></a>Optionen  
 Konfigurieren Sie neben den Standardoptionen auch folgende zusätzliche Einstellungen auf der Registerkarte **Optionen** dieses Tasksequenzschritts:  

-   **Auf Inhalt direkt vom Verteilungspunkt aus zugreifen**  
     Konfigurieren Sie die Tasksequenz so, dass sie direkt vom Verteilungspunkt aus auf das Betriebssystemimage zugreift. Verwenden Sie diese Option, wenn Sie beispielsweise Betriebssysteme für eingebettete Geräte mit begrenzter Speicherkapazität bereitstellen. Wenn Sie diese Option aktivieren, müssen Sie auch die Einstellungen für die Paketfreigabe auf der Registerkarte **Datenzugriff** der Paketeigenschaften konfigurieren.  

    > [!NOTE]  
    >  Diese Einstellung setzt die Bereitstellungsoption außer Kraft, die Sie auf der Seite **Verteilungspunkte** des **Assistenten zum Bereitstellen von Software** konfigurieren. Diese Außerkraftsetzung gilt nur für das von diesem Schritt angegebene Betriebssystemimage, nicht für alle Inhalte der Tasksequenz.  



##  <a name="BKMK_ApplyWindowsSettings"></a> Windows-Einstellungen anwenden  
 Mithilfe dieses Schritts können Sie die Windows-Einstellungen für den Zielcomputer konfigurieren. Die Tasksequenz speichert diese Werte in der entsprechenden Antwortdatei. Windows Setup verwendet diese Antwortdatei während der Aktion **Windows und ConfigMgr einrichten**.  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Apply Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Einstellungen** > **Windows-Einstellungen anwenden**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Benutzername**  
 Geben Sie den registrierten Benutzernamen an, der dem Zielcomputer zugeordnet ist. Dieser Wert kann durch den Wert überschrieben werden, der mit der Tasksequenzaktion **Windows-Einstellungen erfassen** erfasst wird.  

 **Name der Organisation**  
 Geben Sie den registrierten Organisationsnamen an, der dem Zielcomputer zugeordnet ist. Dieser Wert kann durch den Wert überschrieben werden, der mit der Tasksequenzaktion **Windows-Einstellungen erfassen** erfasst wird.  

 **Product Key**  
 Geben Sie den Product Key an, der für die Windows-Installation auf dem Bereitstellungszielcomputer verwendet wird.  

 **Serverlizenzierung**  
 Geben Sie den Serverlizenzierungsmodus an. Sie können als Lizenzierungsmodus **Pro Server** oder **Pro Benutzer** auswählen. Wenn Sie **Pro Server** auswählen, geben Sie ebenfalls die maximale Anzahl von Verbindungen an, die gemäß Ihrem Lizenzvertrag zulässig ist. Falls der Bereitstellungszielcomputer kein Server ist oder Sie den Lizenzierungsmodus nicht angeben möchten, wählen Sie **Nicht angeben** aus.  

 **Maximale Verbindungen**  
 Geben Sie die maximale Anzahl der Verbindungen an, die für diesen Computer gemäß Ihrem Lizenzvertrag zulässig sind.  

 **Lokales Administratorkennwort zufällig erstellen und das Konto auf allen unterstützten Plattformen deaktivieren (empfohlen)**  
 Wählen Sie diese Option aus, um das lokale Administratorkennwort auf eine zufällig generierte Zeichenfolge festzulegen. Diese Option deaktiviert das lokale Administratorkonto auf allen Plattformen, die diese Funktion unterstützen.  

 **Konto aktivieren und lokales Administratorkennwort angeben**  
 Wählen Sie diese Option aus, um das lokale Administratorkonto mithilfe des angegebenen Kennworts zu aktivieren. Geben Sie das Kennwort in der Zeile **Kennwort** ein, und bestätigen Sie es in der Zeile **Kennwort bestätigen** .  

 **Zeitzone**  
 Geben Sie die zu konfigurierende Zeitzone auf dem Zielcomputer an. Dieser Wert kann durch den Wert überschrieben werden, der mit dem Tasksequenzschritt **Windows-Einstellungen erfassen** erfasst wird.  



##  <a name="BKMK_AutoApplyDrivers"></a> Treiber automatisch anwenden  
 Verwenden Sie diesen Schritt, um Gerätetreiber anzupassen und als Teil der Betriebssystembereitstellung zu installieren.  

 Mit dem Tasksequenzschritt **Treiber automatisch anwenden** werden folgende Aktionen ausgeführt:  

1.  Überprüft die Hardware und ermittelt die Plug & Play-IDs für alle auf dem System vorhandenen Geräte.  

2.  Sendet die Liste mit den Geräten und den ihnen zugeordneten Plug & Play-IDs an den Verwaltungspunkt. Der Verwaltungspunkt gibt für jedes Hardwaregerät eine Liste mit kompatiblen Treibern aus dem Treiberkatalog zurück. Die Liste enthält alle Treiber, unabhängig von dem Treiberpaket, in dem sie sich befinden, sowie Treiber, die mit der angegebenen Treiberkategorie markiert sind, und nicht deaktivierte Treiber.  

3.  Die Tasksequenz wählt für jedes Hardwaregerät den besten Treiber aus. Dieser Treiber ist für das bereitgestellte Betriebssystem geeignet und befindet sich auf einem verfügbaren Verteilungspunkt.  

4.  Die Tasksequenz lädt die ausgewählten Treiber von einem Verteilungspunkt herunter und stellt diese auf dem Zielbetriebssystem bereit.  

    1.  Bei imagebasierten Installationen legt die Tasksequenz die Treiber im Treiberspeicher des Betriebssystems ab.  

    2.  Bei setupbasierten Installation konfiguriert die Tasksequenz Windows Setup mit dem Speicherort des Treibers.  

5.  Während der Schritt **Windows und ConfigMgr einrichten** in der Tasksequenz ausgeführt wird, sucht Windows Setup nach den von dieser Aktion bereitgestellten Treibern.  

> [!IMPORTANT]
>  Eigenständige Medien können den Schritt **Treiber automatisch anwenden** nicht verwenden. Windows Setup besitzt in diesem Szenario keine Verbindung zum Configuration Manager-Standort.

Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Auto Apply Drivers Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Treiber** > **Treiber automatisch anwenden**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Nur Treiber mit der höchsten Kompatibilität installieren**  
 Hiermit wird angegeben, dass vom Tasksequenzschritt nur der am besten geeignete Treiber für das jeweilige erkannte Hardwaregerät installiert wird.  

 **Alle kompatiblen Treiber installieren**  
 Die Tasksequenz installiert alle Treiber, die mit dem jeweiligen ermittelten Hardwaregerät kompatibel sind. Windows Setup wählt anschließend den besten Treiber aus. Diese Option beansprucht mehr Netzwerkbandbreite und Festplattenspeicher. Die Tasksequenz lädt mehr Treiber herunter, wodurch Windows jedoch einen besseren Treiber auswählen kann.  

 **Treiber aller Kategorien berücksichtigen**  
 Die Tasksequenz durchsucht alle verfügbaren Treiberkategorien nach den geeigneten Gerätetreibern.  

 **Nur Treiber in bestimmten Kategorien berücksichtigen**  
 Die Tasksequenz durchsucht die angegebenen Treiberkategorien nach den geeigneten Gerätetreibern.  

 **Unbeaufsichtigte Installation von nicht signierten Treibern bei Windows-Versionen ausführen, wenn zulässig**  
 Durch diese Option können Sie unter Windows Treiber ohne digitale Signatur installieren.   

  > [!IMPORTANT]  
  >  Diese Option gilt nicht für Betriebssysteme, deren Richtlinie für Treibersignierung nicht konfiguriert werden kann.  



##  <a name="BKMK_CaptureNetworkSettings"></a> Netzwerkeinstellungen erfassen  
 Verwenden Sie diesen Schritt zum Erfassen der Microsoft-Netzwerkeinstellungen des Computers, auf dem die Tasksequenz ausgeführt wird. Die Tasksequenz speichert diese Einstellungen in Tasksequenzvariablen. Diese Einstellungen setzen die Standardeinstellungen außer Kraft, die Sie im Schritt **Netzwerkeinstellungen anwenden** konfigurieren.  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Capture Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Einstellungen** > **Netzwerkeinstellungen erfassen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Domänen- und Arbeitsgruppenmitgliedschaft migrieren**  
 Hiermit werden Informationen zur Domänen- und Arbeitsgruppenmitgliedschaft des Zielcomputers erfasst.  

 **Netzwerkkartenkonfiguration migrieren**  
 Hiermit wird die Netzwerkadapterkonfiguration des Zielcomputers erfasst. Diese Informationen umfassen die globalen Netzwerkeinstellungen, die Anzahl der Netzwerkkarten und die den Karten zugeordneten Netzwerkeinstellungen. Diese Einstellungen umfassen auch DNS-, WINS-, IP- und Portfiltereinstellungen.  



##  <a name="BKMK_CaptureOperatingSystemImage"></a> Betriebssystemabbild erfassen  
 Dieser Schritt erfasst mindestens ein Image von einem Referenzcomputer. Diese Tasksequenz erstellt eine Windows-Imagedatei (WIM) auf der angegebenen Netzwerkfreigabe. Verwenden Sie anschließend den Assistenten **Add Operating System Image Package** (Betriebssystemimagepaket hinzufügen), um dieses Image in Configuration Manager zu importieren, damit imagebasierte Betriebssystembereitstellungen verwendet werden können.  

 Configuration Manager erfasst jedes Volume (Laufwerk) des Referenzcomputers in einem separaten Image innerhalb der WIM-Datei. Wenn der Referenzcomputer über mehrere Volumes verfügt, enthält die erstellte WIM-Datei für jedes Volume ein separates Image. Es werden nur als NTFS oder FAT32 formatierte Volumes erfasst. Volumes in anderen Formaten sowie USB-Volumes werden nicht berücksichtigt.  

 Das auf dem Referenzcomputer installierte Betriebssystem muss in einer von Configuration Manager unterstützten Windows-Version vorliegen. Verwenden Sie das SysPrep-Tool, um das Betriebssystem des Referenzcomputers vorzubereiten. Bei dem Volume mit dem installierten Betriebssystem und dem Startvolume muss es sich um dasselbe Volume handeln.  

 Geben Sie ein Konto mit Schreibberechtigungen für die ausgewählte Netzwerkfreigabe an.  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Capture Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Images** > **Capture Operating System Image** (Betriebssystemimage erfassen), um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Ziel**  
 Dies ist der Name des Dateisystempfads, der von Configuration Manager zum Speichern des erfassten Betriebssystemimages verwendet wird.  

 **Beschreibung**  
 Eine optionale benutzerdefinierte Beschreibung des erfassten Betriebssystemabbilds, die in der WIM-Datei gespeichert wird.  

 **Version**  
 Eine optionale benutzerdefinierte Versionsnummer, die dem erfassten Betriebssystemabbild zugewiesen wird. Dieser Wert kann aus einer beliebigen Kombination aus Buchstaben und Ziffern bestehen und wird in der WIM-Datei gespeichert.  

 **Erstellt von**  
 Der optionale Name des Benutzers, der das Betriebssystemabbild erstellt hat. Dieser Name wird in der WIM-Datei gespeichert.  

 **Konto für die Erfassung des Betriebssystemimages**  
 Sie müssen das Windows-Konto eingeben, das über Berechtigungen für den Zugriff auf die von Ihnen ausgewählte Netzwerkfreigabe verfügt. Klicken Sie auf **Festlegen** , um den Namen dieses Windows-Kontos anzugeben.  



##  <a name="BKMK_CaptureUserState"></a> Benutzerzustand erfassen  
 Verwenden Sie diesen Schritt, um das Migrationstool für den Benutzerstatus (User State Migration Tool, USMT) zum Erfassen des Benutzerzustands und der Benutzereinstellungen des Computers zu verwenden, der die Tasksequenz ausführt. Dieser Tasksequenzschritt wird in Verbindung mit dem Tasksequenzschritt **Benutzerzustand wiederherstellen** verwendet. In USMT 3.0.1 und höher wird der USMT-Zustandsspeicher mit dieser Option stets mit einem von Configuration Manager generierten und verwalteten Verschlüsselungsschlüssel verschlüsselt.  

 Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

 Wenn Sie die Einstellungen für den Benutzerstatus von einem Zustandsmigrationspunkt aus speichern und wiederherstellen möchten, verwenden Sie den Schritt **Benutzerzustand erfassen** mit den Schritten **Zustandsspeicher anfordern** und **Zustandsspeicher freigeben**.  

 Mit dem Tasksequenzschritt **Benutzerzustand erfassen** kann eine begrenzte Teilmenge der am häufigsten verwendeten USMT-Optionen gesteuert werden. Zusätzliche Befehlszeilenoptionen können mithilfe der Tasksequenzvariablen „OSDMigrateAdditionalCaptureOptions“ angegeben werden.  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Capture User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureUserState).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Benutzerzustand** > **Benutzerzustand erfassen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **USMT-Paket (Migrationsprogramm für den Benutzerzustand)**  
 Geben Sie das Paket an, das das Migrationstool für den Benutzerstatus (USMT) enthält. Die Tasksequenz verwendet diese Version von USMT, um den Benutzerzustand und die Benutzereinstellungen zu erfassen. Für dieses Paket ist kein Programm erforderlich. Geben Sie ein Paket an, das die 32-Bit- oder 64-Bit-Version von USMT enthält. Die Architektur von USMT richtet sich nach der Architektur des Betriebssystems, dessen Zustand die Tasksequenz erfasst.  

 **Alle Benutzerprofile mit Standardoptionen erfassen**  
 Migrieren Sie alle Benutzerprofilinformationen. Dies ist die Standardoption.  

 Wenn Sie diese Option auswählen, jedoch im Schritt **Benutzerzustand wiederherstellen** nicht **Lokale Computerbenutzerprofile wiederherstellen** ausgewählt haben, schlägt die Tasksequenz fehl. Configuration Manager kann neue Konten nicht migrieren, ohne diesen Kennwörter zuzuweisen. 

 Wenn Sie die Option **Install an existing image package** (Bestehendes Imagepaket installieren) des Assistenten **Neue Tasksequenz** verwenden, wird die resultierende Tasksequenz standardmäßig auf **Alle Benutzerprofile mit Standardoptionen erfassen** festgelegt. Diese Standardtasksequenz legt die Option nicht auf **Lokale Computerbenutzerprofile wiederherstellen** (d.h. Benutzerkonten außerhalb der Domäne) fest.  

 Wählen Sie **Lokale Computerbenutzerprofile wiederherstellen** aus, und geben Sie für das zu migrierende Konto ein Kennwort ein. In einer manuell erstellten Tasksequenz finden Sie diese Einstellung im Schritt „Benutzerzustand wiederherstellen“. Wird die Tasksequenz vom **Tasksequenzerstellungs-Assistenten** erstellt, befindet sich diese Einstellung auf der Seite **Benutzerdateien und -einstellungen wiederherstellen** des Assistenten.  

 Wenn Sie nicht über lokale Benutzerkonten verfügen, ist diese Einstellung nicht relevant.  

 **Erfassung der Benutzerprofile anpassen**  
 Wählen Sie diese Option aus, um eine benutzerdefinierte Profildateimigration anzugeben. Klicken Sie auf **Dateien** , um die von USMT bei diesem Schritt zu verwendenden Konfigurationsdateien auszuwählen. Geben Sie eine benutzerdefinierte XML-Datei an, die Regeln zur Definition der zu migrierenden Benutzerzustandsdateien enthält.  

 **Klicken Sie zum Auswählen der Konfigurationsdateien auf diese Schaltfläche:**  
 Wählen Sie diese Option aus, um im USMT-Paket die Konfigurationsdateien auszuwählen, die Sie zum Erfassen von Benutzerprofilen verwenden möchten. Klicken Sie auf die Schaltfläche **Dateien** , um das Dialogfeld **Konfigurationsdateien** zu öffnen. Zum Angeben einer Konfigurationsdatei geben Sie in die Zeile **Dateiname** den Dateinamen ein und klicken auf die Schaltfläche **Hinzufügen** .  

 **Ausführliche Protokollierung aktivieren**  
 Aktivieren Sie diese Option, um ausführlichere Protokolldateiinformationen zu generieren. Wenn der Zustand erfasst wird, generiert die Tasksequenz standardmäßig die Datei „ScanState.log“ im Protokollordner der Tasksequenz (\windows\system32\ccm\logs).   

 **Dateien mit EFS (Encrypted File System) überspringen**  
 Aktivieren Sie diese Option, um das Erfassen von Dateien zu überspringen, die mit EFS (Encrypted File System, verschlüsselndes Dateisystem) verschlüsselt wurden. Diese Dateien enthalten Benutzerprofildateien. Je nach Betriebssystem und USMT-Version sind verschlüsselte Dateien nach der Wiederherstellung möglicherweise nicht lesbar. Weitere Informationen finden Sie in der USMT-Dokumentation.  

 **Mithilfe des normalen Dateisystemzugriffs kopieren**  
 Aktivieren Sie diese Option, um alle oder einige der folgenden Einstellungen anzugeben:  

-   **Fortsetzen, wenn einige Dateien nicht erfasst werden können**: Aktivieren Sie diese Einstellung, um den Migrationsprozess auch dann fortzusetzen, wenn einige Dateien nicht erfasst werden können. Wenn Sie diese Option deaktivieren und eine Datei nicht erfasst werden kann, kann dieser Schritt nicht ausgeführt werden. Diese Option ist standardmäßig aktiviert.  

-   **Lokal erfassen mithilfe von Links statt durch Kopieren von Dateien**: Aktivieren Sie diese Einstellung, um feste NTFS-Links zum Erfassen von Dateien zu verwenden.  

     Weitere Informationen zum Migrieren von Daten mithilfe von festen Links finden Sie unter [Migrationsspeicher mit festem Link](http://go.microsoft.com/fwlink/p/?LinkId=240222).  

-   **Im Offlinemodus erfassen (nur Windows PE)**: Aktivieren Sie diese Einstellung, um den Benutzerzustand nicht im vollständigen Betriebssystem, sondern in Windows PE zu erfassen.  
    
**Mithilfe des Volumeschattenkopie-Diensts (VSS) erfassen**  
 Mithilfe dieser Option können Sie Dateien sogar dann erfassen, wenn sie durch eine andere Anwendung für die Bearbeitung gesperrt sind.  



##  <a name="BKMK_CaptureWindowsSettings"></a> Windows-Einstellungen erfassen  
 Verwenden Sie diesen Schritt zum Erfassen der Windows-Einstellungen des Computers, auf dem die Tasksequenz ausgeführt wird. Die Tasksequenz speichert diese Einstellungen in Tasksequenzvariablen. Diese erfassten Einstellungen setzen die Standardeinstellungen außer Kraft, die Sie im Schritt **Windows-Einstellungen anwenden** konfigurieren.  

 Dieser Tasksequenzschritt wird entweder in Windows PE oder in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Capture Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Einstellungen** > **Windows-Einstellungen erfassen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Computernamen migrieren**  
 Erfassen Sie den NetBIOS-Computernamen des Computers.  

 **Registrierte Benutzer- und Organisationsnamen migrieren**  
 Erfassen Sie auf dem Computer die Namen registrierter Benutzer und Organisationen.  

 **Zeitzone migrieren**  
 Erfassen Sie die Zeitzoneneinstellungen auf dem Computer.  



##  <a name="BKMK_CheckReadiness"></a> Bereitschaft überprüfen  
 Verwenden Sie diesen Schritt, um zu überprüfen, ob der Zielcomputer die Voraussetzungen für die Bereitstellung erfüllt.  

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Allgemein** > **Bereitschaft überprüfen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Mindestens erforderlicher Arbeitsspeicher (MB)**  
 Stellen Sie sicher, dass die Größe des Arbeitsspeichers (in Megabyte bzw. MB) der angegebenen Größe entspricht oder diese übersteigt. Der Schritt aktiviert diese Einstellung standardmäßig.  

 **Mindestens erforderliche Prozessorgeschwindigkeit (MHz)**  
 Überprüfen Sie, dass die Geschwindigkeit des Prozessors (in Megahertz bzw. MHz) der angegebenen Geschwindigkeit entspricht oder diese übersteigt. Der Schritt aktiviert diese Einstellung standardmäßig.  

 **Mindestens erforderlicher freier Speicherplatz (MB)**  
 Stellen Sie sicher, dass die Größe des freien Speicherplatzes auf dem Datenträger (in Megabyte bzw. MB) der angegebenen Größe entspricht oder diese übersteigt.  

 **Aktuelles Betriebssystem, das aktualisiert wird**  
 Stellen Sie sicher, dass das auf dem Zielcomputer installierte Betriebssystem die angegebene Anforderung erfüllt. Der Schritt legt dies standardmäßig auf **CLIENT** fest.  

### <a name="options"></a>Optionen
 > [!NOTE]  
 > Wenn Sie die Einstellung **Bei Fehler fortsetzen** auf der Registerkarte **Optionen** dieses Schritts aktivieren, werden nur die Ergebnisse der Überprüfung auf Bereitschaft protokolliert. Wenn eine Überprüfung fehlschlägt, wird die Tasksequenz nicht beendet.



##  <a name="BKMK_ConnectToNetworkFolder"></a> Verbindung mit Netzwerkordner herstellen  
 Verwenden Sie diesen Schritt, um eine Verbindung mit einem freigegebenen Netzwerkordner herzustellen.  

 Dieser Tasksequenzschritt wird in einem Standardbetriebssystem oder in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Connect to Network Folder Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Allgemein** > **Verbindung mit Netzwerkordner herstellen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Pfad**  
 Klicken Sie auf **Durchsuchen**, um den Netzwerkordnerpfad anzugeben. Verwenden Sie das Format *\\\server\share*.

 **Laufwerk**  
 Wählen Sie den Buchstaben des lokalen Laufwerks aus, das Sie dieser Verbindung zuweisen möchten. 

 **Konto**  
 Klicken Sie auf **Festlegen**, um das Benutzerkonto mit den Berechtigungen zum Herstellen einer Verbindung mit diesem Netzwerkordner anzugeben.



##  <a name="BKMK_DisableBitLocker"></a> BitLocker deaktivieren  
 Verwenden Sie diesen Schritt, um die BitLocker-Verschlüsselung auf dem aktuellen Betriebssystemlaufwerk oder auf einem bestimmten Laufwerk zu deaktivieren. Nach dieser Aktion sind die Schlüsselschutzkomponenten im Klartext auf der Festplatte sichtbar, die Inhalte des Laufwerks werden jedoch nicht entschlüsselt. Dieser Vorgang ist daher praktisch sofort beendet.  

> [!NOTE]  
>  BitLocker-Laufwerkverschlüsselung bietet eine niedrige Verschlüsselungsstufe der Inhalte eines Datenträgervolumes.  

 Wenn Sie über mehrere verschlüsselte Laufwerke verfügen, müssen Sie „BitLocker deaktivieren“ zuerst für alle Datenlaufwerke anwenden, bevor Sie die BitLocker-Verschlüsselung des Betriebssystemlaufwerks deaktivieren können.  

 Dieser Schritt wird nur in Standardbetriebssystemen ausgeführt. Er wird nicht in Windows PE ausgeführt.  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Datenträger** > **BitLocker deaktivieren**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Aktuelles Betriebssystemlaufwerk**  
 Deaktiviert BitLocker auf dem aktuellen Betriebssystemlaufwerk.  

 **Bestimmtes Laufwerk**  
 Deaktiviert BitLocker auf einem bestimmten Laufwerk. Geben Sie in der Dropdownliste das Laufwerk an, auf dem BitLocker deaktiviert ist.  



##  <a name="BKMK_DownloadPackageContent"></a> Paketinhalt herunterladen  
 Verwenden Sie diesen Schritt, um einen der folgenden Pakettypen herunterzuladen:  

-   Betriebssystemabbilder  

-   Betriebssystem-Upgradepakete  

-   Treiberpakete  

-   Pakete  

-   Startabbilder
    
Dieser Schritt funktioniert gut in einer Tasksequenz zum Aktualisieren eines Betriebssystems in den folgenden Szenarien:  

-   Zum Verwenden einer einzigen Upgradetasksequenz für x86- und x64-Plattformen. Fügen Sie der Gruppe **Vorbereitung auf das Upgrade** zwei **Paketinhalt herunterladen**-Schritte hinzu. Legen Sie auf der Registerkarte **Optionen** Bedingungen fest, um die Clientarchitektur zu ermitteln und nur das entsprechende Betriebssystemupgradepaket herunterzuladen. Konfigurieren Sie jeden **Paketinhalt herunterladen**-Schritt, sodass dieselbe Variable verwendet wird. Verwenden Sie die Variable für den Medienpfad im Schritt **Betriebssystem aktualisieren**.  

-   Um dynamisch ein passendes Treiberpaket herunterzuladen, verwenden Sie zwei **Paketinhalt herunterladen** -Schritte mit Bedingungen zum Ermitteln des geeigneten Hardwaretyps für jedes Treiberpaket. Konfigurieren Sie jeden **Paketinhalt herunterladen**-Schritt, sodass dieselbe Variable verwendet wird. Verwenden Sie die Variable für den Wert **Bereitgestellter Inhalt** im Abschnitt „Treiber“ des Schritts **Betriebssystem aktualisieren**.  

> [!NOTE]    
> Wenn Sie eine Tasksequenz bereitstellen, die den Schritt „Paketinhalt herunterladen“ enthält, aktivieren Sie im Assistenten zum Bereitstellen von Software auf der Seite **Verteilungspunkte** für **Bereitstellungsoptionen** nicht **Alle Inhalte vor dem Start der Tasksequenz lokal herunterladen** oder **Auf Inhalt direkt vom Verteilungspunkt aus zugreifen**.  

Dieser Schritt wird entweder in einem Standardbetriebssystem oder in Windows PE ausgeführt. WinPE unterstützt die Option, die Pakete im Clientcache des Configuration Manager zu speichern, jedoch nicht.

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Software** > **Paketinhalt herunterladen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Paket auswählen** -Symbol  
 Klicken Sie auf das Symbol, um das Paket zum Herunterladen auszuwählen. Nachdem Sie ein Paket ausgewählt haben, können Sie erneut auf das Symbol klicken, um ein anderes Paket auszuwählen.  

 **In folgendem Verzeichnis speichern**  
 Sie können das Paket in einem der folgenden Verzeichnisse speichern:  

 -   **Tasksequenz-Arbeitsverzeichnis**  

 -   **Configuration Manager-Clientcache**: Verwenden Sie diese Option, um den Inhalt im Clientcache zu speichern. Der Client fungiert als Peercachequelle für andere Peercacheclients. Weitere Informationen finden Sie unter [Vorbereiten des Windows PE-Peercache zum Reduzieren des WAN-Datenverkehrs](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

 -    **Benutzerdefinierter Pfad:** Mit dieser Option lädt die Tasksequenzengine zunächst das Paket in das Tasksequenzarbeitsverzeichnis herunter und verschiebt dieses anschließend an diesen von Ihnen angegebenen Pfad. Die Tasksequenzengine hängt den Pfad mit der Paket-ID an. 
   
**Pfad als Variable speichern**  
 Sie können den Pfad als Variable speichern, die in einem anderen Tasksequenzschritt verwendet werden kann. Configuration Manager fügt dem Variablennamen ein numerisches Suffix hinzu. Wenn Sie z.B. eine Variable von %*mycontent*% als benutzerdefinierte Variable festlegen, stellt diese das Stammverzeichnis dar, in dem die Tasksequenz alle Inhalte speichert, auf die verwiesen wird. Diese Inhalte können mehrere Pakete enthalten. Wenn Sie dann auf die Variable verweisen, fügen Sie ein numerisches Suffix hinzu. Beispielsweise verweisen Sie für das erste Paket auf %*mycontent01*%. Wenn Sie auf die Variable in einem Untersequenzschritt verweisen, z.B. **Betriebssystem aktualisieren**, verwenden Sie %*mycontent02*% oder %*mycontent03*%, wobei die Anzahl der Reihenfolge entspricht, in der der Schritt **Paketinhalt herunterladen** die Pakete auflistet.  

**Wenn ein Fehler bei einem Paketdownload auftritt, mit anderen Paketen in der Liste fortfahren**  
 Wenn die Tasksequenz ein Paket nicht herunterladen kann, startet es den Download des nächsten Pakets in der Liste.  



##  <a name="BKMK_EnableBitLocker"></a> BitLocker aktivieren  
Verwenden Sie diesen Schritt, um die BitLocker-Verschlüsselung auf mindestens zwei Partitionen auf der Festplatte zu aktivieren. Die erste aktive Partition enthält den Windows-Bootstrap-Code. Eine weitere Partition beinhaltet das Betriebssystem. Die Bootstrap-Partition muss unverschlüsselt bleiben.  

Verwenden Sie den Tasksequenzschritt **BitLocker vorab bereitstellen** zum Aktivieren von BitLocker auf einem Laufwerk in Windows PE. Weitere Informationen finden Sie im Abschnitt [BitLocker vorab bereitstellen](#BKMK_PreProvisionBitLocker).  

> [!NOTE]  
>  BitLocker-Laufwerkverschlüsselung bietet eine niedrige Verschlüsselungsstufe der Inhalte eines Datenträgervolumes.  

Der Schritt **BitLocker aktivieren** wird nur in Standardbetriebssystemen ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

Wenn Sie **Nur TPM**, **TPM und Schlüssel zum Systemstart auf USB** oder **TPM-und-PIN** angeben, muss das Trusted Platform Module (TPM) sich in folgendem Zustand befinden, bevor Sie den Schritt **BitLocker aktivieren** ausführen können:  

-   Aktiviert  
-   Aktiviert  
-   Besitz zulässig  
   
Dieser Schritt schließt alle verbleibenden TPM-Initialisierungen ab. Die verbleibenden Schritte erfordern keine physische Präsenz und keine Neustarts. Der Schritt **BitLocker aktivieren** schließt die verbleibenden Schritte für die TPM-Initialisierung bei Bedarf transparent ab:  

-   Endorsement Key-Paar erstellen  
-   Besitzerauthentifizierungswert erstellen und in Active Directory hinterlegen, welches zur Unterstützung dieses Werts erweitert worden sein muss  
-   Besitz übernehmen  
-   Storage Root Key (SRK, Speicherstammschlüssel) erstellen bzw. zurücksetzen, falls bereits einer vorhanden ist, der jedoch inkompatibel ist  
   
Wenn die Tasksequenz auf den Schritt **BitLocker aktivieren** warten soll, bevor der Vorgang der Laufwerkverschlüsselung abgeschlossen wird, aktivieren Sie die Option **Warten**. Wenn Sie die Option **Warten** nicht aktivieren, wird der Vorgang der Laufwerkverschlüsselung im Hintergrund ausgeführt. Die Tasksequenz fährt sofort mit dem nächsten Schritt fort.  

Mithilfe von BitLocker können mehrere Laufwerke in einem Computersystem (sowohl Betriebssystem- als auch Datenlaufwerke) verschlüsselt werden. Verschlüsseln Sie zum Verschlüsseln eines Datenlaufwerks zunächst das Betriebssystemlaufwerk, und schließen Sie den Verschlüsselungsvorgang ab. Diese Anforderung besteht, da das Betriebssystemlaufwerk die Schlüsselschutzvorrichtungen für die Datenlaufwerke speichert. Wenn Sie das Betriebssystem und die Datenlaufwerke in derselben Tasksequenz verschlüsseln, aktivieren Sie die Option **Warten** des Schritts **BitLocker aktivieren** für das Betriebssystemlaufwerk.  

Wenn die Festplatte bereits verschlüsselt, aber BitLocker deaktiviert ist, aktiviert der Schritt **BitLocker aktivieren** die Schlüsselschutzvorrichtungen erneut und wird schnell abgeschlossen. Eine erneute Verschlüsselung des Laufwerks ist in diesem Fall nicht notwendig.  

Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Datenträger** > **BitLocker aktivieren**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Wählen Sie das zu verschlüsselnde Laufwerk aus**  
 Gibt das zu verschlüsselnde Laufwerk an. Um das aktuelle Betriebssystemlaufwerk zu verschlüsseln, wählen Sie **Aktuelles Betriebssystemlaufwerk** aus und konfigurieren anschließend eine der folgenden Optionen für die Schlüsselverwaltung.  

-   **Nur TPM**: Wählen Sie diese Option, um nur Trusted Platform Module (TPM) zu verwenden.  

-   **Nur Schlüssel zum Systemstart auf USB**: Wählen Sie diese Option, um einen auf einem USB-Flashlaufwerk gespeicherten Systemstartschlüssel zu verwenden. Wenn Sie diese Option auswählen, sperrt BitLocker den normalen Startvorgang, bis ein USB-Gerät mit einem BitLocker-Systemstartschlüssel an den Computer angeschlossen wird.  

-   **TPM &amp; Schlüssel zum Systemstart auf USB**: Wählen Sie diese Option, um TPM und einen auf einem USB-Flashlaufwerk gespeicherten Systemstartschlüssel zu verwenden. Wenn Sie diese Option auswählen, sperrt BitLocker den normalen Startvorgang, bis ein USB-Gerät mit einem BitLocker-Systemstartschlüssel an den Computer angeschlossen wird.  

-   **TPM-und-PIN**: Wählen Sie diese Option, um TPM und eine persönliche Identifikationsnummer (PIN) zu verwenden. Wenn Sie diese Option auswählen, sperrt BitLocker den normalen Startvorgang, bis der Benutzer die PIN eingibt.  
   
Um ein bestimmtes Datenlaufwerk (kein Betriebssystemlaufwerk) zu verschlüsseln, wählen Sie **Bestimmtes Laufwerk**, und wählen Sie dann das Laufwerk in der Liste aus.  

**Wählen Sie aus, wo der Wiederherstellungsschlüssel erstellt werden soll**  
 Wählen Sie **In Active Directory** aus, um festzulegen, wo BitLocker das Wiederherstellungskennwort erstellt und um dieses in Active Directory zu hinterlegen. Wenn Sie diese Option auswählen, müssen Sie Active Directory für den Standort erweitern. BitLocker kann die zugehörigen Wiederherstellungsinformationen dann in Active Directory speichern. Wählen Sie **Do not create recovery key** (Keinen Wiederherstellungsschlüssel erstellen) aus, um kein Kennwort zu erstellen. Das Erstellen eines Kennworts ist jedoch eine bewährte Methode.  

**Vor dem Fortsetzen der Tasksequenzausführung warten, bis BitLocker den Laufwerkverschlüsselungsvorgang auf allen Laufwerken abgeschlossen hat**  
 Wählen Sie diese Option aus, damit die BitLocker-Laufwerkverschlüsselung abgeschlossen wird, bevor der nächste Schritt in der Tasksequenz ausgeführt wird. Wenn Sie diese Option auswählen, verschlüsselt BitLocker das gesamte Datenträgervolume, bevor der Benutzer sich beim Computer anmelden kann.  

Beim Verschlüsseln einer großen Festplatte kann der Verschlüsselungsvorgang mehrere Stunden andauern. Wenn diese Option nicht ausgewählt wird, kann die Tasksequenz sofort fortgesetzt werden.  



##  <a name="BKMK_FormatandPartitionDisk"></a> Datenträger formatieren und partitionieren  
 Mit diesem Schritt können Sie einen angegebenen Datenträger auf einem Zielcomputer formatieren und partitionieren.  

> [!IMPORTANT]  
>  Jede von Ihnen für diesen Tasksequenzschritt angegebene Einstellung gilt nur für einen angegebenen Datenträger. Wenn Sie einen anderen Datenträger auf dem Zielcomputer formatieren und partitionieren möchten, fügen Sie der Tasksequenz den zusätzlichen Schritt **Datenträger formatieren und partitionieren** hinzu.  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Format and Partition Disk Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Datenträger** > **Datenträger formatieren und partitionieren**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Datenträgernummer**  
 Die Nummer des physischen Datenträgers, der formatiert werden soll Die Nummer basiert auf der Reihenfolge der Datenträgerenumeration in Windows.  

 **Datenträgertyp**  
 Typ des Datenträgers, der formatiert wird In der Dropdownliste stehen zwei Optionen zur Auswahl zur Verfügung: 

-   Standard (MBR) – Master Boot Record
-   GPT – GUID-Partitionstabelle  

> [!NOTE]  
>  Wenn Sie den Datenträgertyp von **Standard (MBR)** in **GPT** ändern und das Partitionslayout eine erweiterte Partition enthält, entfernt die Tasksequenz alle erweiterten und logischen Partitionen aus dem Layout. Der Tasksequenz-Editor fordert Sie dazu auf, diese Aktion vor dem Ändern des Datenträgertyps zu bestätigen.  
   
**Volume**  
 Weitere Informationen zu der Partition oder dem Volume, die bzw. das von der Tasksequenz erstellt wird, einschließlich folgender Attribute:  

-   Name  
-   Verbleibender Speicherplatz  
   
Zum Erstellen einer neuen Partition klicken Sie auf **Neu** , um das Dialogfeld **Partitionseigenschaften** aufzurufen. Geben Sie die Größe und den Typ der Partition an und ob es sich um eine Startpartition handelt. Zum Ändern einer vorhandenen Partition klicken Sie auf die zu ändernde Partition und dann auf die Schaltfläche „Eigenschaften“. Weitere Informationen zum Konfigurieren von Festplattenpartitionen finden Sie in einem der folgenden Artikel:  

-   [Konfigurieren von UEFI-/GPT-basierten Festplattenpartitionen](http://go.microsoft.com/fwlink/?LinkID=272104)  
-   [Konfigurieren von BIOS-/MBR-basierten Festplattenpartitionen](http://go.microsoft.com/fwlink/?LinkId=272105)  

Wählen Sie zum Löschen einer Partition die zu löschende Partition aus, und klicken Sie dann auf **Löschen**.  



##  <a name="BKMK_InstallApplication"></a> Anwendung installieren  
Dieser Schritt installiert die angegebenen Anwendungen oder eine von einer dynamischen Liste mit Tasksequenzvariablen definierte Anwendungsgruppe. Wenn dieser Schritt ausgeführt wird, beginnt die Anwendungsinstallation sofort; das nächste Richtlinienabfrageintervall wird nicht abgewartet.  

Von Anwendungen, die installiert werden, müssen die folgenden Kriterien erfüllt werden:  

-   Die Anwendung muss ein Bereitstellungstyp von Windows Installer oder des Skriptinstallationsprogramms sein. Bereitstellungstypen des Windows-App-Pakets (APPX-Datei) werden nicht unterstützt.  

-   Es muss unter dem lokalen Systemkonto ausgeführt werden und nicht unter dem Benutzerkonto.  

-   Es darf keine Interaktion mit dem Desktop erfolgen. Das Programm muss im Hintergrund oder in einem unbeaufsichtigten Modus ausgeführt werden.  

-   Es darf durch die Anwendung kein eigenständiger Computerneustart initiiert werden. Ein Computerneustart muss über den Standardneustartcode (Exitcode 3010) angefordert werden. Durch dieses Verhalten wird sichergestellt, dass der Tasksequenzschritt den Neustart ordnungsgemäß ausführt. Wenn ein Exitcode 3010 von der Anwendung zurückgegeben wird, so wird der Neustart vom zugrundeliegenden Tasksequenzmodul ausgeführt. Nach dem Neustart wird die Tasksequenz automatisch fortgesetzt.  

Bei Ausführung des Schritts **Anwendung installieren** wird die Anwendbarkeit der Anforderungsregeln und der Ermittlungsmethode für die Bereitstellungstypen geprüft. Auf Basis der Ergebnisse dieser Überprüfung wird der anwendbare Bereitstellungstyp installiert. Wenn ein Bereitstellungstyp Abhängigkeiten enthält, wird der abhängige Bereitstellungstyp im Rahmen des Anwendungsinstallationsschritts ausgewertet und installiert. Abhängigkeiten von Anwendungen werden für eigenständige Medien nicht unterstützt.  

> [!NOTE]  
>  Zum Installieren einer Anwendung, die eine andere Anwendung ablöst, müssen die Inhaltsdateien für die abgelöste Anwendung verfügbar sein. Andernfalls tritt beim Tasksequenzschritt ein Fehler auf. Beispiel: Microsoft Visio 2010 ist auf einem Client oder in einem erfassten Abbild installiert. Wenn der Schritt **Anwendung installieren** Microsoft Visio 2013 installiert, müssen die Inhaltsdateien für Microsoft Visio 2010 (die abgelöste Anwendung) an einem Verteilungspunkt verfügbar sein. Wenn Microsoft Visio auf einem Client oder einem erfassten Image nicht installiert ist, installiert die Tasksequenz Microsoft Visio 2013, ohne nach den Inhaltsdateien von Microsoft Visio 2010 zu suchen.  

> [!NOTE]
> Wenn der Client die Liste der Verwaltungspunkte nicht von den Standortdiensten abrufen kann, verwenden Sie die integrierten Variablen „SMSTSMPListRequestTimeoutEnabled“ und „SMSTSMPListRequestTimeout“, um anzugeben, für wie viele Millisekunden eine Tasksequenz wartet, bevor die Installation einer Anwendung oder eines Softwareupdates erneut versucht wird. Weitere Informationen finden Sie unter [Task sequence built-in variables (Integrierte Tasksequenzvariablen)](task-sequence-built-in-variables.md).

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt.  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Software** > **Anwendung installieren**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Folgende Anwendungen installieren**  
 Die Tasksequenz installiert diese Anwendungen in der angegebenen Reihenfolge.  

 Deaktivierte Anwendungen und Anwendungen mit den folgenden Einstellungen werden von Configuration Manager herausgefiltert:  

-   Nur wenn ein Benutzer angemeldet ist  
-   Mit Benutzerrechten ausführen  

Diese Anwendungen erscheinen nicht im Dialogfeld **Zu installierende Anwendung auswählen**.
  
**Anwendungen entsprechend der dynamischen Variablenliste installieren**  
Die Tasksequenz installiert Anwendungen mithilfe dieses Basisvariablennamens. Der Basisvariablenname gilt für eine Gruppe von Tasksequenzvariablen, die für eine Sammlung oder für einen Computer definiert wurden. Von diesen Variablen werden die Anwendungen angegeben, die von der Tasksequenz für die Sammlung bzw. für den Computer installiert werden. Jeder Variablenname besteht aus einem allgemeinen Basisnamen sowie einem numerischen bei 01 beginnenden Suffix Der Wert jeder Variable darf nur den Namen der Anwendung und nichts anderes enthalten.  

Damit die Tasksequenz Anwendungen mithilfe einer dynamischen Variablenliste installiert, müssen Sie folgende Einstellung auf der Registerkarte **Allgemein** der Anwendung **Eigenschaften** aktivieren: **Allow this application to be installed from the Install Application task sequence action instead of deploying manually** (Installation dieser Anwendung durch die Tasksequenzaktion „Anwendung installieren“ statt durch manuelle Bereitstellung zulassen)  

> [!NOTE]  
>  Bei Bereitstellungen mit eigenständigen Medien können Sie Anwendungen nicht mithilfe einer dynamischen Variablenliste installieren.  

Beispiel: Geben Sie folgende Variable an, um eine einzelne Anwendung mithilfe einer Tasksequenzvariablen namens AA01 zu installieren:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Bei der Installation von zwei Anwendungen sind folgende zusätzliche Variablen anzugeben:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

Folgende Bedingungen wirken sich auf die Anwendungen aus, die von der Tasksequenz installiert wurden:  

-   Der Variablenwert enthält noch andere bzw. keine anderen Informationen als den Namen der Anwendung. Die Tasksequenz installiert die Anwendung nicht und wird fortgesetzt.  

-   Wenn die Tasksequenz keine Variable mit dem angegebenen Basisnamen und dem Suffix „01“ findet, installiert diese keine Anwendungen. 
    
> [!Important]  
> Bei diesen Werten ist die Groß-/Kleinschreibung relevant. Beispielsweise unterscheidet sich „install“ von „Install“. Wenn Sie den Wert ändern müssen, wird eine Änderung der Groß-/Kleinschreibung vom Tasksequenz-Editor nicht erkannt. Sie müssen gleichzeitig eine weitere Bearbeitung vornehmen, z. B. die Schrittbeschreibung ändern.<!--509714-->   

   
**Wenn ein Fehler bei einer Anwendungsinstallation auftritt, mit anderen Anwendungen in der Liste fortfahren**  
 Mit dieser Einstellung geben Sie an, dass der Schritt fortgesetzt werden soll, wenn bei einer einzelnen Anwendungsinstallation ein Fehler auftritt. Wenn Sie diese Einstellungen angeben, wird die Tasksequenz unabhängig von Installationsfehlern fortgesetzt. Wenn Sie diese Einstellung nicht angeben und die Installation fehlschlägt, wird der Schritt sofort beendet.  

### <a name="options"></a>Optionen
 > [!NOTE] 
 > Wenn Sie auf der Registerkarte **Optionen** dieses Schritts die Option **Bei Fehler fortsetzen** auswählen, wird die Tasksequenz bei einem Fehler der Anwendungsinstallation fortgesetzt. Wenn Sie diese Option nicht aktivieren, tritt bei der Tasksequenz ein Fehler auf und verbleibende Anwendungen werden nicht installiert.  
 
Konfigurieren Sie neben den Standardoptionen auch folgende zusätzliche Einstellungen auf der Registerkarte **Optionen** dieses Tasksequenzschritts:  

-   **Führen Sie diesen Schritt erneut aus, wenn der Computer unerwartet neu gestartet wird**  
    Wenn eine der Anwendungsinstallationen den Computer unerwartet neu startet, wiederholen Sie diesen Schritt. Der Schritt aktiviert diese Einstellung standardmäßig mit zwei Wiederholungen. Sie können eine bis fünf Wiederholungen angeben.  



##  <a name="BKMK_InstallPackage"></a> Paket installieren
Verwenden Sie diesen Schritt, um ein Softwarepaket als Teil der Tasksequenz zu installieren. Wenn dieser Schritt ausgeführt wird, beginnt die Installation sofort, und das nächste Richtlinienabfrageintervall wird nicht abgewartet.  

Das Paket muss folgende Kriterien erfüllen:  

-   Es muss unter dem lokalen Systemkonto ausgeführt werden und nicht unter einem Benutzerkonto.  

-   Es sollte nicht mit dem Desktop interagieren. Das Programm muss im Hintergrund oder in einem unbeaufsichtigten Modus ausgeführt werden.  

-   Es darf durch die Anwendung kein eigenständiger Computerneustart initiiert werden. Ein Computerneustart muss über den Standardneustartcode (Exitcode 3010) angefordert werden. Durch dieses Verhalten wird sichergestellt, dass der Tasksequenzschritt den Neustart ordnungsgemäß ausführt. Wenn die Software einen Exitcode 3010 zurückgibt, startet die Engine der zugrunde liegenden Tasksequenz den Computer neu. Nach dem Neustart wird die Tasksequenz automatisch fortgesetzt.  

Programme, von denen die Option **Ein anderes Programm zuerst ausführen** zur Installation eines abhängigen Programms verwendet wird, werden bei der Bereitstellung eines Betriebssystems nicht unterstützt. Wenn Sie die Paketoption **Ein anderes Programm zuerst ausführen** aktivieren und das abhängige Programm bereits auf dem Zielcomputer ausgeführt wurde, wird dieses ausgeführt und die Tasksequenz wird fortgesetzt. Wurde das abhängige Programm jedoch noch nicht auf dem Zielcomputer ausgeführt, tritt bei diesem Tasksequenzschritt ein Fehler auf.  

> [!NOTE]  
>  Der Standort der zentralen Verwaltung verfügt nicht über die erforderlichen Clientkonfigurationsrichtlinien, die während der Tasksequenz zum Aktivieren des Softwareverteilungs-Agents erforderlich sind. Wenn Sie am Standort der zentralen Verwaltung eigenständige Medien für eine Tasksequenz erstellen und die Tasksequenz den Schritt **Paket installieren** enthält, kann in der Datei "CreateTsMedia.log" der folgende Fehler enthalten sein:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  Bei eigenständigen Medien, die den Schritt **Paket installieren** enthalten, erstellen Sie das eigenständige Medium an einem primären Standort, bei dem der Softwareverteilungs-Agent aktiviert ist. Fügen Sie alternativ den Schritt **Befehlszeile ausführen** nach dem Schritt **Windows und ConfigMgr einrichten** und vor dem ersten **Paket installieren**-Schritt hinzu. Im Schritt **Befehlszeile ausführen** wird ein WMIC-Befehl ausgeführt, um den Softwareverteilungs-Agent vor dem ersten Schritt **Paket installieren** zu aktivieren. Verwenden Sie im Schritt **Befehlszeile ausführen** folgenden Befehl:  
>   
>  **Befehlszeile**: `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>   
>  Weitere Informationen zum Erstellen eigenständiger Medien finden Sie unter [Erstellen eigenständiger Medien](../deploy-use/create-stand-alone-media.md).  

Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt.  

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Software** > **Paket installieren**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Einzelnes Softwarepaket installieren**  
 Diese Einstellung gibt ein Configuration Manager-Softwarepaket an. Bei diesem Schritt wird gewartet, bis die Installation abgeschlossen ist.  

 **Softwarepakete entsprechend der dynamischen Variablenliste installieren**  
 Die Tasksequenz installiert Pakete mithilfe dieses Basisvariablennamens. Der Basisvariablenname gilt für eine Gruppe von Tasksequenzvariablen, die für eine Sammlung oder für einen Computer definiert wurden. Von diesen Variablen werden die Pakete angegeben, die von der Tasksequenz für die Sammlung bzw. für den Computer installiert werden. Jeder Variablenname besteht aus einem allgemeinen Basisnamen sowie einem numerischen bei 001 beginnenden Suffix. Der Wert jeder Variablen muss eine Paket-ID und den Namen der Software (durch einen Doppelpunkt getrennt) enthalten.  

 Damit die Tasksequenz Software mithilfe einer dynamischen Variablenliste installieren kann, aktivieren Sie folgende Einstellung auf der Registerkarte **Erweitert** des Pakets **Eigenschaften**: **Installation dieses Programms aus der Tasksequenz „Paket installieren“ ohne Bereitstellung zulassen**  

> [!NOTE]  
>  Bei Bereitstellungen mit eigenständigen Medien können Sie Softwarepakete nicht mithilfe einer dynamischen Variablenliste installieren.  

 Beispiel: Geben Sie folgende Variable an, um ein einzelnes Softwarepaket mithilfe einer Tasksequenzvariablen namens AA001 zu installieren:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

 Bei der Installation von drei Softwarepaketen sind folgende zusätzliche Variablen anzugeben:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

 Folgende Bedingungen wirken sich auf die Pakete aus, die von der Tasksequenz installiert wurden:  

-   Wenn Sie den Wert einer Variablen nicht im richtigen Format erstellen oder dieser keine gültige Paket-ID und keinen gültigen Namen angibt, schlägt die Installation der Software fehl.  

-   Wenn die Paket-ID Kleinbuchstaben enthält, schlägt die Installation der Software fehl.  

-   Wenn die Tasksequenz keine Variable mit dem angegebenen Basisnamen und dem Suffix „001“ findet, installiert diese keine Pakete. Die Tasksequenz wird fortgesetzt.  
    
> [!Important]  
> Bei diesen Werten ist die Groß-/Kleinschreibung relevant. Beispielsweise unterscheidet sich „install“ von „Install“. Wenn Sie den Wert ändern müssen, wird eine Änderung der Groß-/Kleinschreibung vom Tasksequenz-Editor nicht erkannt. Sie müssen gleichzeitig eine weitere Bearbeitung vornehmen, z. B. die Schrittbeschreibung ändern.<!--509714-->   

   
**Wenn ein Fehler bei einer Softwarepaketinstallation auftritt, mit anderen Paketen in der Liste fortfahren**  
 Mit dieser Einstellung geben Sie an, dass der Schritt fortgesetzt werden soll, wenn bei einer einzelnen Softwarepaketinstallation ein Fehler auftritt. Wenn Sie diese Einstellungen angeben, wird die Tasksequenz unabhängig von Installationsfehlern fortgesetzt. Wenn Sie diese Einstellung nicht angeben und die Installation fehlschlägt, wird der Schritt sofort beendet.  



##  <a name="BKMK_InstallSoftwareUpdates"></a> Softwareupdates installieren  
Verwenden Sie diesen Schritt, um Softwareupdates auf dem Zielcomputer zu installieren. Der Zielcomputer wird erst beim Ausführen dieses Tasksequenzschritts hinsichtlich anwendbarer Softwareupdates ausgewertet. An diesem Punkt wird der Zielcomputer wie jeder andere Configuration Manager-Client hinsichtlich Softwareupdates ausgewertet. Damit dieser Schritt Softwareupdates installiert, müssen Sie die Updates zunächst für eine Sammlung bereitstellen, der der Zielcomputer angehört.  
>  [!IMPORTANT]
> Eine bewährte Methode für optimale Leistung besteht darin, die aktuelle Version des Windows Update-Agents zu installieren. 
>* Für Windows 7 siehe [Knowledge Base-Artikel 3161647](https://support.microsoft.com/kb/3161647).
>* Für Windows 8 siehe [Knowledge Base-Artikel 3163023](https://support.microsoft.com/kb/3163023).

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Install Software Updates Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > Wenn der Client die Liste der Verwaltungspunkte nicht von den Standortdiensten abrufen kann, verwenden Sie die integrierten Variablen „SMSTSMPListRequestTimeoutEnabled“ und „SMSTSMPListRequestTimeout“, um anzugeben, für wie viele Millisekunden eine Tasksequenz wartet, bevor die Installation einer Anwendung oder eines Softwareupdates erneut versucht wird. Weitere Informationen finden Sie unter [Task sequence built-in variables (Integrierte Tasksequenzvariablen)](task-sequence-built-in-variables.md).

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Software** > **Softwareupdates installieren**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Installation erforderlich – Nur obligatorische Softwareupdates**  
 Wählen Sie diese Option aus, um alle erforderlichen Softwareupdates mit einem vom Administrator definierten Installationsstichtag zu installieren.  

 **Bereit zur Installation – Alle Softwareupdates**  
 Wählen Sie diese Option aus, um alle verfügbaren Softwareupdates zu installieren. Sie müssen diese Updates zunächst für eine Sammlung bereitstellen, der dieser Computer angehört. Die Tasksequenz installiert alle verfügbaren Softwareupdates auf den Zielcomputern.  

 **Softwareupdates anhand von zwischengespeicherten Überprüfungsergebnissen auswerten**  
 Standardmäßig verwendet die Tasksequenz zwischengespeicherte Überprüfungsergebnisse des Windows Update-Agents. Deaktivieren Sie das Kontrollkästchen, damit der Windows Update-Agent den aktuellen Katalog vom Softwareupdatepunkt herunterlädt. Wählen Sie diese Option aus, wenn Sie eine Tasksequenz dafür verwenden, [ein Betriebssystemimage zu erfassen und zu erstellen](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). In diesem Szenario muss wahrscheinlich eine große Anzahl von Softwareupdates durchgeführt werden. Viele dieser Updates verfügen über Abhängigkeiten, beispielsweise müssen Sie ggf. X installieren, bevor Y angezeigt wird. Wenn Sie diese Einstellung deaktivieren und die Tasksequenz für viele Clients bereitstellen, werden alle zur selben Zeit eine Verbindung mit dem Softwareupdatepunkt herstellen. Dieses Verhalten kann während des Prozesses und des Downloads des Katalogs zu Leistungsproblemen führen. Eine bewährte Methode besteht im Verwenden der Standardeinstellungen, damit zwischengespeicherte Überprüfungsergebnisse verwendet werden. 

Die Tasksequenzvariable „SMSTSSoftwareUpdateScanTimeout“ steuert während dieses Schritts die Überprüfung von Zeitüberschreitungen bei Softwareupdates. Der Standardwert beträgt 30 Minuten. Weitere Informationen finden Sie unter [Task sequence built-in variables (Integrierte Tasksequenzvariablen)](task-sequence-built-in-variables.md).

### <a name="options"></a>Optionen   
 Konfigurieren Sie neben den Standardoptionen auch folgende zusätzliche Einstellungen auf der Registerkarte **Optionen** dieses Tasksequenzschritts:  

-   **Führen Sie diesen Schritt erneut aus, wenn der Computer unerwartet neu gestartet wird**  
    Wenn eines der Updates den Computer unerwartet neu startet, wiederholen Sie diesen Schritt. Der Schritt aktiviert diese Einstellung standardmäßig mit zwei Wiederholungen. Sie können eine bis fünf Wiederholungen angeben.  

    > [!NOTE]
    > Konfigurieren Sie die Variable „SMSTSWaitForSecondReboot“, um anzugeben, für wie viele Sekunden die Tasksequenz in diesem Szenario angehalten wird, nachdem der Computer neu gestartet wurde. Weitere Informationen finden Sie unter [Task sequence built-in variables (Integrierte Tasksequenzvariablen)](task-sequence-built-in-variables.md).



##  <a name="BKMK_JoinDomainorWorkgroup"></a> Einer Domäne oder Arbeitsgruppe beitreten  
 Verwenden Sie diesen Schritt, um den Zielcomputer einer Arbeitsgruppe oder einer Domäne hinzuzufügen.  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Join Domain or Workgroup Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Allgemein** > **Einer Domäne oder Arbeitsgruppe beitreten**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Einer Arbeitsgruppe beitreten**  
 Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Arbeitsgruppe hinzuzufügen. Wenn der Computer derzeit Mitglied einer Domäne ist, wird er durch Auswählen dieser Option neu gestartet.  

 **Einer Domäne beitreten**  
 Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Domäne hinzuzufügen.  

 Sie können optional eine Organisationseinheit (OU), der der Computer beitreten soll, eingeben oder in der angegebenen Domäne danach suchen. Wenn der Computer derzeit Mitglied einer anderen Domäne oder Arbeitsgruppe ist, wird er durch diese Option neu gestartet. Wenn der Computer bereits Mitglied einer anderen Organisationseinheit ist, ignoriert Windows Setup diese Einstellung, da Active Directory Domain Services das Ändern der Organisationseinheit über diese Methode nicht zulässt.  

 **Geben Sie das Konto ein, das zum Beitreten zur Domäne berechtigt ist**  
 Klicken Sie auf **Festlegen**, um den Benutzernamen und das Kennwort für ein Konto mit der Berechtigung für den Domänenbeitritt einzugeben. Geben Sie das Konto im Format *Domain\account* ein.  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> ConfigMgr-Client für Erfassung vorbereiten  
Verwenden Sie diesen Schritt, um den Configuration Manager-Client auf dem Referenzcomputer zu konfigurieren oder um ihn von diesem zu entfernen. Diese Aktion bereitet den Computer auf die Erfassung im Rahmen des Imageerstellungsprozesses vor.

Ab Version 1610 von Configuration Manager wird der Configuration Manager-Client im Schritt **ConfigMgr-Client vorbereiten** vollständig entfernt, statt nur wichtige Informationen zu entfernen. Wenn die Tasksequenz das erfasste Betriebssystemimage bereitstellt, wird jedes Mal ein neuer Configuration Manager-Client installiert.  

> [!Note]  
>  Die Tasksequenz-Engine entfernt während der Tasksequenz **Referenz-Betriebssystemabbild erstellen und erfassen** nur den Client. Die Tasksequenz-Engine entfernt den Client nicht während anderer Erfassungsmethoden, z.B. Erfassungsmedien oder benutzerdefinierte Tasksequenzen.

Vor der Configuration Manager-Version 1610 werden bei diesem Schritt folgende Aufgaben ausgeführt:  

-   Entfernt den Abschnitt mit den Clientkonfigurationseigenschaften aus der Datei „smscfg.ini“ im Windows-Verzeichnis. Diese Eigenschaften umfassen clientspezifische Informationen, darunter die Configuration Manager-GUID und andere Clientbezeichner.  

-   Löscht alle SMS- oder Configuration Manager-Computerzertifikate  

-   Löscht den Configuration Manager-Clientcache  

-   Löscht die zugewiesene Standortvariable für den Configuration Manager-Client  

-   Löscht alle lokalen Configuration Manager-Richtlinien  

-   Entfernt den vertrauenswürdigen Stammschlüssel für den Configuration Manager-Client  

Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt.  

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Images** > **ConfigMgr-Client für Erfassung vorbereiten**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Dieser Schritt erfordert keine Einstellungen auf der Registerkarte **Eigenschaften**.



##  <a name="BKMK_PrepareWindowsforCapture"></a> Windows für die Erfassung vorbereiten  
 Verwenden Sie diesen Schritt, um die Sysprep-Optionen beim Erfassen eines Betriebssystemimages auf dem Referenzcomputer anzugeben. Diese Tasksequenzaktion führt Sysprep aus und startet dann den Computer über das für die Tasksequenz angegebene Windows PE-Startimage neu. Diese Aktion schlägt fehl, wenn der Referenzcomputer einer Domäne angehört.  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Prepare Windows for Capture Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Images** > **Windows für die Erfassung vorbereiten**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Automatisch Liste der Massenspeichertreiber erstellen**  
 Wählen Sie diese Option aus, damit Sysprep automatisch eine Liste der Massenspeichertreiber vom Referenzcomputer erstellt. Mit dieser Option wird die Option „Build Mass Storage Drivers“ (Massenspeichertreiber erstellen) in der Datei Sysprep.inf auf dem Referenzcomputer aktiviert. Weitere Informationen zu dieser Option finden Sie in der Sysprep-Dokumentation.  

 **Aktivierungskennzeichnung nicht zurücksetzen**  
 Wählen Sie diese Option aus, damit Sysprep das Produktaktivierungsflag nicht zurücksetzt.  



##  <a name="BKMK_PreProvisionBitLocker"></a> BitLocker vorab bereitstellen  
 Verwenden Sie diesen Schritt, um BitLocker auf einem Laufwerk in Windows PE zu aktivieren. Es wird nur der auf dem Laufwerk verwendete Speicherplatz verschlüsselt, sodass die Verschlüsselungszeit erheblich verkürzt wird. Sie wenden die Schlüsselverwaltungsoptionen an, indem Sie den Tasksequenzschritt [Aktivieren von BitLocker](#BKMK_EnableBitLocker) nach der Betriebssysteminstallation ausführen. Dieser Schritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt.  

> [!IMPORTANT]  
>  Für das Bereitstellen von BitLocker im Voraus ist mindestens Windows 7 erforderlich. Der Computer muss ebenfalls ein unterstütztes und aktiviertes Trusted Platform Module (TPM) enthalten.  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Datenträger** > **BitLocker vorab bereitstellen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **BitLocker auf das angegebene Laufwerk anwenden**  
 Geben Sie das Laufwerk aus, für das Sie BitLocker aktivieren möchten. Nur der verwendete Speicherplatz auf dem Laufwerk wird verschlüsselt.  

 **Diesen Schritt bei Computern überspringen, die nicht über ein TPM verfügen oder bei denen das TPM nicht aktiviert ist**  
 Wählen Sie diese Option aus, um die Laufwerkverschlüsselung auf einem Computer zu überspringen, der kein unterstütztes oder aktiviertes TPM enthält. Sie können diese Option beispielsweise verwenden, wenn Sie ein Betriebssystem für einen virtuellen Computer bereitstellen.  



##  <a name="BKMK_ReleaseStateStore"></a> Zustandsspeicher freigeben  
 Verwenden Sie diesen Schritt, um den Zustandsmigrationspunkt darüber zu benachrichtigen, dass die Erfassungs- oder Wiederherstellungsaktion abgeschlossen ist. Verwenden Sie diesen Schritt zusammen mit den Schritten **Zustandsspeicher anfordern**, **Benutzerzustand erfassen** und **Benutzerzustand wiederherstellen**. Verwenden Sie diese Schritte, um Benutzerzustanddaten mithilfe eines Zustandsmigrationspunkts und des Migrationstools für den Benutzerstatus zu migrieren.  

 Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

 Wenn Sie den Schritt **Zustandsspeicher anfordern** verwenden, um Zugriff auf einen Zustandsmigrationspunkt für die *Erfassung* des Benutzerzustands anzufordern, meldet dieser Schritt dem Zustandsmigrationspunkt, dass der Erfassungsvorgang abgeschlossen ist. Der Zustandsmigrationspunkt markiert die Benutzerzustandsdaten dann als für die Wiederherstellung verfügbar. Der Zustandsmigrationspunkt legt die Zugriffssteuerungsberechtigungen für die Benutzerzustandsdaten so fest, dass nur der wiederherstellende Computer über Lesezugriff verfügt.  

 Wenn Sie den Schritt **Zustandsspeicher anfordern** verwenden, um Zugriff auf einen Zustandsmigrationspunkt für die *Wiederherstellung* des Benutzerzustands anzufordern, meldet dieser Schritt dem Zustandsmigrationspunkt, dass der Wiederherstellungsvorgang abgeschlossen ist. Der Zustandsmigrationspunkt aktiviert anschließend die konfigurierten Einstellungen für die Datenaufbewahrung.  

> [!IMPORTANT]  
>  Eine bewährte Methode besteht darin, die Option **Bei Fehler fortsetzen** für alle Schritte zwischen **Zustandsspeicher anfordern** und **Zustandsspeicher freigeben** festzulegen. Für jeden **Zustandsspeicher anfordern**-Schritt muss ein übereinstimmender **Zustandsspeicher freigeben**-Schritt vorhanden sein.  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Release State Store Sequence Action Variables](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Benutzerzustand** > **Zustandsspeicher freigeben**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Dieser Schritt erfordert keine Einstellungen auf der Registerkarte **Eigenschaften**.



##  <a name="BKMK_RequestStateStore"></a> Zustandsspeicher anfordern  
 Mit diesem Schritt können Sie beim Erfassen oder Wiederherstellen eines Zustands Zugriff auf einen Zustandsmigrationspunkt anfordern.  

 Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

 Verwenden Sie diesen Schritt zusammen mit den Schritten **Zustandsspeicher freigeben**, **Benutzerzustand erfassen** und **Benutzerzustand wiederherstellen**. Verwenden Sie diese Schritte, um den Computerzustand mithilfe eines Zustandsmigrationspunkts und des Migrationstools für den Benutzerstatus zu migrieren.  

> [!NOTE]  
>  Wenn Sie einen neuen Zustandsmigrationspunkt erstellen, kann es bis zu einer Stunde dauern, bis der Benutzerzustandsspeicher verfügbar ist. Für eine beschleunigte Verfügbarkeit können Sie alle Eigenschaftseinstellungen des Zustandsmigrationspunkts so einstellen, dass das Update einer Standortsteuerungsdatei ausgelöst wird.  

 Dieser Tasksequenzschritt wird in einem Standardbetriebssystem und in Windows PE für Offline-USMT ausgeführt. Weitere Informationen zu den Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Request State Store Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RequestState).  

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Benutzerzustand** > **Zustandsspeicher anfordern**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Zustand des Computers erfassen**  
 Suchen Sie einen Zustandsmigrationspunkt, der die in den Einstellungen für Zustandsmigrationspunkte konfigurierten Mindestanforderungen erfüllt. Zum Beispiel **Maximale Anzahl von Clients** und **Minimum amount of free disk space** (Mindestens erforderliche Menge an freiem Speicherplatz). Diese Option garantiert nicht, dass zum Zeitpunkt der Zustandsmigration genügend freier Speicherplatz verfügbar ist. Durch diese Option wird Zugriff auf den Zustandsmigrationspunkt angefordert, um den Benutzerzustand und die Einstellungen eines Computers zu erfassen.  

 Wenn der Configuration Manager-Standort über mehrere aktive Zustandsmigrationspunkte verfügt, sucht dieser Schritt einen Zustandsmigrationspunkt mit verfügbarem Speicherplatz. Die Tasksequenz fragt den Verwaltungspunkt nach einer Liste der Zustandsmigrationspunkte ab und wertet diese dann aus, bis einer davon die Mindestanforderungen erfüllt.  

 **Zustand von anderem Computer wiederherstellen**  
 Fordern Sie Zugriff auf einen Zustandsmigrationspunkt an, um einen zuvor erfassten Benutzerzustand sowie Einstellungen auf einem Zielcomputer wiederherzustellen.  

 Wenn es mehrere Zustandsmigrationspunkte gibt, sucht dieser Schritt den Zustandsmigrationspunkt, dessen Zustand dem des Zielcomputers entspricht.  

 **Anzahl von Wiederholungen**  
 Die Anzahl der Versuche, die von diesem Schritt unternommen werden, um einen entsprechenden Zustandsmigrationspunkt zu suchen, bevor ein Fehler auftritt  

 **Wiederholungsverzögerung (in Sekunden)**  
 Hiermit wird die Anzahl der Sekunden angegeben, die vom Tasksequenzschritt zwischen Wiederholversuchen gewartet wird.  

 **Das Netzwerkzugriffskonto verwenden, falls das Computerkonto keine Verbindung mit dem Zustandsspeicher herstellen kann.**  
 Wenn die Tasksequenz mithilfe des Computerkontos nicht auf den Zustandsmigrationspunkt zugreifen kann, werden die Anmeldeinformationen für das Netzwerkzugriffskonto verwendet, um eine Verbindung herzustellen. Diese Option ist nicht so sicher wie andere, da andere Computer das Netzwerkzugriffskonto verwenden könnten, um auf den gespeicherten Zustand zuzugreifen. Diese Option ist möglicherweise erforderlich, wenn der Zielcomputer nicht in eine Domäne eingebunden ist.  



##  <a name="BKMK_RestartComputer"></a> Computer neu starten  
 Verwenden Sie diesen Schritt, um den Computer neu zu starten, der die Tasksequenz ausführt. Nach dem Neustart führt der Computer automatisch den nächsten Schritt der Tasksequenz aus.  

 Dieser Schritt kann entweder in einem Standardbetriebssystem oder in Windows PE ausgeführt werden. Weitere Informationen zu den Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Variablen der Tasksequenzaktion „Computer neu starten“](task-sequence-action-variables.md#BKMK_RestartComputer).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Allgemein** > **Computer neu starten**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Der Tasksequenz zugewiesenes Startimage**  
 Wenn Sie diese Option auswählen, wird das der Tasksequenz zugewiesene Startimage vom Zielcomputer verwendet. Die Tasksequenz verwendet das Startimage, um nachfolgende Schritte in Windows PE auszuführen.  

 **Aktuell installiertes Standardbetriebssystem**  
 Wenn Sie diese Option auswählen, wird der Zielcomputer mit dem installierten Betriebssystem neu gestartet.  

 **Benutzer vor dem Neustart benachrichtigen**  
 Wenn Sie diese Option auswählen, wird dem Benutzer vor dem Neustart des Zielcomputers eine Benachrichtigung angezeigt. Der Schritt wählt diese Option standardmäßig aus.  

 **Benachrichtigungsmeldung**  
 Geben Sie eine Benachrichtigungsmeldung ein, die dem Benutzer vor dem Neustart des Zielcomputers angezeigt werden soll.  

 **Timeout der Meldungsanzeige**  
 Geben Sie den Zeitraum in Sekunden an, der bis zum Neustart des Zielcomputers verbleibt. Der Standardwert ist 60 Sekunden.  



##  <a name="BKMK_RestoreUserState"></a> Benutzerzustand wiederherstellen  
 Mithilfe dieses Schritts können Sie das Migrationstool für den Benutzerstatus dazu initiieren, den Benutzerzustand und die Benutzereinstellungen auf einem Zielcomputer wiederherzustellen. Verwenden Sie diesen Schritt zusammen mit dem Schritt **Benutzerzustand erfassen**.  

 Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

 Verwenden Sie diesen Schritt zusammen mit den Schritten **Zustandsspeicher anfordern** und **Zustandsspeicher freigeben**, um die Zustandseinstellungen mit einem Zustandsmigrationspunkt zu speichern oder wiederherzustellen. In USMT 3.0 und höher wird der USMT-Zustandsspeicher mit dieser Option stets mit einem von Configuration Manager generierten und verwalteten Verschlüsselungsschlüssel entschlüsselt.  

 Mit dem Schritt **Benutzerzustand wiederherstellen** kann eine begrenzte Teilmenge der am häufigsten verwendeten USMT-Optionen gesteuert werden. Geben Sie zusätzliche Befehlszeilenoptionen mit der Tasksequenzvariable „OSDMigrateAdditionalRestoreOptions“ an.  

> [!IMPORTANT]  
>  Wenn Sie diesen Schritt für eine Aufgabe verwenden, die nicht im Zusammenhang mit einem Szenario der Betriebssystembereitstellung steht, fügen Sie den Schritt [Computer neu starten](#BKMK_RestartComputer) unmittelbar nach dem Schritt **Benutzerzustand wiederherstellen** hinzu.  

 Dieser Schritt wird nur in Standardbetriebssystemen ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu den Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Restore User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RestoreUserState).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Benutzerzustand** > **Benutzerzustand wiederherstellen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **USMT-Paket (Migrationsprogramm für den Benutzerzustand)**  
 Geben Sie das Paket an, das die Version von USMT enthält, die für diesen Schritt verwendet werden soll. Für dieses Paket ist kein Programm erforderlich. Wenn der Schritt ausgeführt wird, verwendet die Tasksequenz die Version von USMT, die sich im angegebenen Paket befindet. Geben Sie ein Paket an, das die 32-Bit- oder 64-Bit-Version von USMT enthält. Die Architektur von USMT richtet sich nach der Architektur des Betriebssystems, dessen Zustand die Tasksequenz wiederherstellt. 

 **Alle erfassten Benutzerprofile mit Standardoptionen wiederherstellen**  
 Stellt die erfassten Benutzerprofile mit den Standardoptionen wieder her. Wählen Sie zum Anpassen der von USMT wiederherzustellenden Optionen **Erfassung der Benutzerprofile anpassen** aus.  

 **Wiederherstellung von Benutzerprofilen anpassen**  
 Ermöglicht Ihnen die Anpassung der Dateien, die Sie auf dem Zielcomputer wiederherstellen möchten. Klicken Sie auf **Dateien** , um im USMT-Paket die Konfigurationsdateien anzugeben, die Sie für die Wiederherstellung der Benutzerprofile verwenden möchten. Zum Hinzufügen einer Konfigurationsdatei geben Sie einen Namen im Feld **Dateiname** an, und klicken Sie dann auf **Hinzufügen**. Der Bereich „Dateien“ listet die Konfigurationsdateien auf, die USMT verwendet. Die von Ihnen angegebene XML-Datei legt fest, welche Benutzerdatei von USMT wiederhergestellt wird.  

 **Lokale Computerbenutzerprofile wiederherstellen**  
 Stellt die lokalen Computerbenutzerprofile wieder her. Diese Profile sind nicht für Domänenbenutzer vorgesehen. Sie müssen den wiederhergestellten lokalen Benutzerkonten neue Kennwörter zuweisen. USMT kann die ursprünglichen Kennwörter nicht migrieren. Geben Sie das Kennwort im Feld **Kennwort** ein, und bestätigen Sie es im Feld **Kennwort bestätigen** .  

 **Fortsetzen, wenn einige Dateien nicht wiederhergestellt werden können**  
 Setzt die Wiederherstellung des Benutzerzustands und der Benutzereinstellungen auch dann fort, wenn USMT einige Dateien nicht wiederherstellen kann. Der Schritt aktiviert diese Option standardmäßig. Wenn Sie diese Option deaktivieren und beim Wiederherstellen von Dateien durch USMT Fehler auftreten, schlägt dieser Schritt sofort fehl. USMT stellt nicht alle Dateien wieder her.   

 **Ausführliche Protokollierung aktivieren**  
 Aktivieren Sie diese Option, um ausführlichere Protokolldateiinformationen zu generieren. Wenn der Zustand wiederhergestellt wird, generiert die Tasksequenz standardmäßig die Datei „Loadstate.log“ im Protokollordner der Tasksequenz (\windows\system32\ccm\logs).  



##  <a name="BKMK_RunCommandLine"></a> Befehlszeile ausführen  
 Verwenden Sie diesen Schritt, um die angegebene Befehlszeile auszuführen.  

 Dieser Schritt kann in einem Standardbetriebssystem oder in Windows PE ausgeführt werden. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Run Command Line Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RunCommand).  

 Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Allgemein** > **Befehlszeile ausführen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Befehlszeile**  
 Gibt die ausgeführte Befehlszeile an. Dieses Feld ist erforderlich. Die Verwendung von Dateinamenerweiterungen, wie .vbs und .exe, ist eine bewährte Methode. Sie sollten alle erforderlichen Einstellungsdateien, Befehlszeilenoptionen oder -parameter einschließen.  

 Wenn der Dateiname ohne Dateinamenerweiterung angegeben ist, versucht Configuration Manager, die Erweiterung .com, .exe oder .bat zu verwenden. Enthält der Dateiname eine Erweiterung, die keiner ausführbaren Datei zugeordnet ist, versucht Configuration Manager eine lokale Zuordnung anzuwenden. Lautet die Befehlszeile z.B. „readme.gif“, startet Configuration Manager die Anwendung, die auf dem Zielcomputer zum Öffnen von GIF-Dateien angegeben ist.  

 Beispiele:  

 `setup.exe /a`  

 `cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
>  Für eine erfolgreiche Ausführung sollte Befehlszeilenoptionen der Befehl **cmd.exe /c** vorausgehen. Zu den Beispielen für diese Aktionen zählen die Umleitung der Ausgabe, das Piping und das Kopieren von Befehlen.  

 **64-Bit-Dateisystemumleitung deaktivieren**  
 64-Bit-Betriebssysteme verwenden standardmäßig den Dateisystem-Redirector von WOW64, um Befehlszeilen auszuführen. Durch dieses Verhalten können 32-Bit-Versionen von ausführbaren Betriebssystemdateien und Bibliotheken ordnungsgemäß gesucht werden. Wählen Sie diese Option aus, um die Verwendung des Dateisystem-Redirectors von WOW64 zu deaktivieren. Windows führt den Befehl mithilfe nativer 64-Bit-Versionen von ausführbaren Betriebssystemdateien und Bibliotheken aus. Unter einem 32-Bit-Betriebssystem hat diese Option keine Auswirkungen.  

 **Starten in**  
 Gibt den ausführbaren Ordner für das Programm mit bis zu 127 Zeichen an. Für diesen Ordner kann ein absoluter Pfad auf dem Zielcomputer oder ein relativer Pfad zum Verteilungspunktordner mit dem Paket angegeben werden. Dieses Feld ist optional.  

 Beispiele:  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  Die Schaltfläche **Durchsuchen** durchsucht den lokalen Computer nach Dateien und Ordnern. Jede Auswahl muss ebenfalls auf dem Zielcomputer am selben Speicherort und mit denselben Datei- und Ordnernamen vorhanden sein.  

 **Paket**  
 Wenn Sie Dateien oder Programme in der Befehlszeile angeben, die sich nicht bereits auf dem Zielcomputer befinden, wählen Sie diese Option aus, um das Configuration Manager-Paket anzugeben, das die entsprechenden Dateien enthält. Für das Paket ist kein Programm erforderlich. Diese Option ist nicht erforderlich, wenn die angegebenen Dateien auf dem Zielcomputer vorhanden sind.  

 **Timeout**  
 Legt einen Wert fest, der angibt, wie lange Configuration Manager das Ausführen der Befehlszeile zulässt. Dieser Wert kann aus dem Bereich von 1 bis 999 Minuten stammen. Der Standardwert beträgt 15 Minuten.  

 Diese Option ist standardmäßig deaktiviert.  

> [!IMPORTANT]  
>  Wenn Sie einen Wert eingeben, der nicht genügend Zeit zum erfolgreichen Abschließen des angegebenen Befehls zur Verfügung stellt, schlägt dieser Schritt fehl. In Abhängigkeit von anderen Steuerelementeinstellungen kann die gesamte Tasksequenz fehlschlagen. Wenn das Timeout abläuft, beendet Configuration Manager den Befehlszeilenprozess.  

 **Diesen Schritt mit folgendem Konto ausführen**  
 Hiermit wird angegeben, dass die Befehlszeile unter einem anderen Windows-Benutzerkonto als dem lokalen Systemkonto ausgeführt wird.  

> [!NOTE]  
>  Wenn Sie einfache Skripts oder Befehle nach der Installation des Betriebssystems mit einem anderen Konto ausführen möchten, müssen Sie dieses Konto zunächst auf dem Computer hinzufügen. Zudem müssen Sie das Profil des Windows-Benutzerkontos wiederherstellen, damit komplexere Programme wie Windows Installer ausgeführt werden können.  

 **Konto**  
 Gibt das Windows-Benutzerkonto an, das dieser Schritt zum Ausführen der Befehlszeile verwendet. Die Befehlszeile wird mit den Berechtigungen des angegebenen Kontos ausgeführt. Klicken Sie auf **Festlegen** , um das lokale Benutzer- oder Domänenkonto anzugeben.  

> [!IMPORTANT]  
>  Wenn dieser Schritt ein Benutzerkonto angibt und unter Windows PE ausgeführt wird, schlägt die Aktion fehl. Sie können Windows PE nicht mit einer Domäne verknüpfen. Die Datei „smsts.log“ zeichnet diesen Fehler auf.  



##  <a name="BKMK_RunPowerShellScript"></a> PowerShell-Skript ausführen  
 Verwenden Sie diesen Schritt, um das angegebene PowerShell-Skript auszuführen.  

 Dieser Schritt kann in einem Standardbetriebssystem oder in Windows PE ausgeführt werden. Um diesen Schritt in Windows PE auszuführen, muss PowerShell im Startabbild aktiviert sein. Sie können Windows PowerShell (WinPE-PowerShell) auf der Registerkarte **Optionale Komponenten** in den Eigenschaften des Startabbilds aktivieren. Weitere Informationen dazu, wie ein Startimage geändert wird, finden Sie unter [Verwalten von Startimages](../get-started/manage-boot-images.md).  

> [!NOTE]  
>  PowerShell ist unter Windows Embedded-Betriebssystemen nicht standardmäßig aktiviert.  

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Allgemein** > **PowerShell-Skript ausführen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Paket**  
 Gibt das Configuration Manager-Paket mit dem PowerShell-Skript an. Ein Paket kann mehrere PowerShell-Skripts enthalten.  

 **Skriptname**  
 Gibt den Namen des auszuführenden PowerShell-Skripts an. Dieses Feld ist erforderlich.  

 **Parameter**  
 Gibt die Parameter an, die an das Windows PowerShell-Skript übergeben werden. Diese Parameter sind identisch mit den Windows PowerShell-Skriptparametern in der Befehlszeile.  

> [!IMPORTANT]  
>  Geben Sie die Parameter an, die vom Skript verwendet werden, nicht die für die Windows PowerShell-Befehlszeile.  
>   
>  Das folgende Beispiel enthält gültige Parameter:  
>   
>  `-MyParameter1 MyValue1 -MyParameter2 MyValue2`  
>   
>  Das folgende Beispiel enthält ungültige Parameter. Bei den ersten beiden Elementen handelt es sich um Windows PowerShell-Befehlszeilenparameter (**-NoLogo** und **-ExecutionPolicy Unrestricted**). Das Skript verarbeitet diese Parameter nicht.  
>   
>  `-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`  

 **PowerShell-Ausführungsrichtlinie**  
 Bestimmen Sie, welche Windows PowerShell-Skripts auf dem Computer ausgeführt werden können. Wählen Sie eine der folgenden Ausführungsrichtlinien aus:  

-   **Alle signiert:** Nur Skripts, die von einem vertrauenswürdigen Herausgeber signiert wurden, werden ausgeführt.  

-   **Nicht definiert:** Keine Ausführungsrichtlinie wird definiert.  

-   **Umgehung**: Alle Konfigurationsdateien werden geladen und alle Skripts ausgeführt. Wenn Sie ein nicht signiertes Skript aus dem Internet herunterladen, fordert Windows PowerShell Sie vor der Ausführung des Skripts nicht zum Erteilen der Berechtigung auf.  

> [!IMPORTANT]  
>  Die Ausführungsrichtlinien „Undefiniert“ und „Umgehung“ werden von PowerShell 1.0 nicht unterstützt.  



##  <a name="child-task-sequence"></a> Ausführen einer Tasksequenz

Ab Configuration Manager Version 1710 können Sie einen neuen Schritt hinzufügen, der eine andere Tasksequenz ausführt. Dieser Schritt erstellt eine Über-/Unterordnungsbeziehung zwischen den Tasksequenzen. Mithilfe einer untergeordneten Tasksequenz können Sie weitere modular aufgebaute, wiederverwendbare Tasksequenzen erstellen.

Berücksichtigen Sie folgende Anweisungen, wenn Sie eine untergeordnete Tasksequenz einer Tasksequenz hinzufügen:
 - Die über- und untergeordneten Tasksequenzen werden effektiv in einer einzigen Richtlinie kombiniert, die der Client ausführt.
 - Die Umgebung ist global. Wenn die übergeordnete Tasksequenz eine Variable festlegt und die untergeordnete Tasksequenz diese Variable ändert, behält diese den aktuellen Wert bei. Wenn die untergeordnete Tasksequenz eine neue Variable erstellt, ist diese für den Rest der übergeordneten Tasksequenz verfügbar.
 - Statusmeldungen werden in der Regel für einen einzelnen Tasksequenzvorgang gesendet.
 - Die Tasksequenzen schreiben Einträge in die Datei „smsts.log“, mit neuen Protokolleinträgen, die den Start einer untergeordneten Tasksequenz deutlich machen.

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Allgemein** > **Tasksequenz ausführen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

**Auszuführende Tasksequenz auswählen**  
 Klicken Sie auf **Durchsuchen**, um die untergeordnete Tasksequenz auszuwählen. Das Dialogfeld **Tasksequenz auswählen** zeigt die übergeordnete Tasksequenz nicht an.



##  <a name="BKMK_SetDynamicVariables"></a> Dynamische Variablen festlegen  
 Verwenden Sie diesen Schritt, um folgende Aktionen durchzuführen:  

1.  Sammeln von Informationen vom Computer und aus der Umgebung, in der er sich befindet, und Festlegen angegebener Tasksequenzvariablen anhand dieser Informationen.  

2.  Auswerten definierter Regeln und Festlegen von Tasksequenzvariablen basierend auf den Variablen und Werten, die für als „Wahr“ ausgewertete Regeln konfiguriert wurden.  

Die Tasksequenz legt automatisch die folgenden schreibgeschützten Tasksequenzvariablen fest:  
 -   &#95;SMSTSMake  
 -   &#95;SMSTSModel  
 -   &#95;SMSTSMacAddresses  
 -   &#95;SMSTSIPAddresses  
 -   &#95;SMSTSSerialNumber  
 -   &#95;SMSTSAssetTag  
 -   &#95;SMSTSUUID  

Dieser Schritt kann entweder in einem Standardbetriebssystem oder in Windows PE ausgeführt werden. Weitere Informationen zu Tasksequenzvariablen finden Sie unter [Tasksequenz-Aktionsvariablen](task-sequence-action-variables.md).  

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Allgemein** > **Dynamische Variablen festlegen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

**Dynamische Regeln und Variablen**  
 Fügen Sie eine Regel hinzu, um eine dynamische Variable für die Verwenden in der Tasksequenz festzulegen. Legen Sie dann einen Wert für jede Variable fest, die in der Regel angegeben wurde. Fügen Sie zusätzlich mindestens eine Variable hinzu, ohne eine Regel hinzuzufügen. Wenn Sie eine Regel hinzufügen, können Sie aus den folgenden Kategorien auswählen:  

 -   **Computer:** Werte für das Hardwarebestandskennzeichen, die UUID, Seriennummer oder MAC-Adresse werden ausgewertet. Legen Sie bei Bedarf mehrere Werte fest. Wenn ein Wert TRUE ist, wird die Regel als TRUE gewertet. Folgende Regel wird beispielsweise aus TRUE ausgewertet, wenn die Seriennummer des Geräts „5892087“ und die MAC-Adresse „22-A4-5A-13-78-26“ ist.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Speicherort:** Werte für das Standardgateway des Netzwerks werden ausgewertet.  

-   **Typ und Modell:** Werte für den Typ und das Modell eines Computers werden ausgewertet. Sowohl Hersteller als auch Modell müssen als „Wahr“ ausgewertet werden, damit die Regel als „Wahr“ ausgewertet wird.   

    <!-- for future edits: an escape code must be used for the bolded asterisk character, but may be removed somewhere along the way. Instead of five asterisk, should be bold tags with &#42; in-between -->

    Ab Version 1610 von Configuration Manager können Sie ein Sternchen (*****) und ein Fragezeichen (**?**) als Platzhalter an der Stelle angeben, an der ***** mehreren Zeichen und **?** entspricht. entspricht einem einzelnen Zeichen. Zum Beispiel die Zeichenfolge „DELL*900?“ wird „DELL-ABC-9001“ und „DELL9009“ entsprechen. 

    Geben Sie ein Sternchen (**&#42;**) und ein Fragezeichen (**?**) als Platzhalter an der Stelle an, an der **&#42;** mehreren Zeichen und **?** entspricht. entspricht einem einzelnen Zeichen. Zum Beispiel die Zeichenfolge „DELL*900?“ ist identisch mit „DELL-ABC-9001“ and „DELL9009“.

-   **Tasksequenzvariable:** Fügt eine Tasksequenzvariable, eine Bedingung und einen Wert zum Auswerten hinzu. Die Regel wird als „Wahr“ ausgewertet, wenn der für die Variable festgelegte Wert die angegebene Bedingung erfüllt.  

    Geben Sie eine oder mehrere Variablen an, die für eine Regel festgelegt werden sollen, die als TRUE ausgewertet wird, oder legen Sie Variablen ohne Verwendung einer Regel fest. Wählen Sie eine vorhandene Variable aus, oder erstellen Sie eine benutzerdefinierte Variable.  

     -   **Vorhandene Tasksequenzvariablen**: Eine oder mehrere Variablen werden aus einer Liste vorhandener Tasksequenzvariablen ausgewählt. Arrayvariablen stehen nicht zur Auswahl.  

     -   **Benutzerdefinierte Tasksequenzvariablen**: Eine benutzerdefinierte Tasksequenzvariable wird definiert. Sie können auch eine vorhandene Tasksequenzvariable angeben. Diese Einstellung ist nützlich, um ein vorhandenes Variablenarray wie z. B. „OSDAdapter“ anzugeben, da Variablenarrays nicht in der Liste der vorhandenen Tasksequenzvariablen enthalten sind.  

Nachdem Sie die Variablen für eine Regel ausgewählt haben, müssen Sie einen Wert für jede Variable angeben. Die Variable wird auf den angegebenen Wert festgelegt, wenn die Regel als „Wahr“ ausgewertet wird. Sie können für jede Variable **Geheimer Wert** auswählen, um den Wert der Variablen auszublenden. Standardmäßig werden Werte für einige vorhandene Variablen ausgeblendet, z. B. für die Tasksequenzvariable OSDCaptureAccountPassword.  

> [!IMPORTANT]  
>  Configuration Manager entfernt alle Variablenwerte, die als **Geheimniswert** markiert sind, wenn Sie eine Tasksequenz mit dem Schritt **Dynamische Variablen festlegen** importieren. Geben Sie den Wert für die dynamische Variable nach dem Import der Tasksequenz erneut ein.  



##  <a name="BKMK_SetTaskSequenceVariable"></a> Tasksequenzvariable festlegen  
Verwenden Sie diesen Schritt, um den Wert einer Variablen festzulegen, die mit der Tasksequenz verwendet wird.  

Dieser Schritt kann entweder in einem Standardbetriebssystem oder in Windows PE ausgeführt werden. Tasksequenzvariablen werden von Tasksequenzaktionen gelesen und definieren das Verhalten dieser Aktionen. Weitere Informationen zu bestimmten Variablen für Tasksequenzaktionen finden Sie unter [Tasksequenz-Aktionsvariablen](task-sequence-action-variables.md). Weitere Informationen zu bestimmten integrierten Tasksequenzvariablen finden Sie unter [Integrierte Tasksequenzvariablen](/sccm/osd/understand/task-sequence-built-in-variables).

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Allgemein** > **Tasksequenzvariable festlegen**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Tasksequenzvariable**  
 Geben Sie den Namen einer integrierten Tasksequenzvariablen oder einer Tasksequenz-Aktionsvariablen an, oder geben Sie einen benutzerdefinierten Variablennamen an.  

 **Wert**  
 Die Tasksequenz legt die Variable auf diesen Wert fest. Legen Sie diese Tasksequenzvariable auf den Wert einer anderen Tasksequenzvariablen mit der Syntax „ %varname%“ fest.  



##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Windows und ConfigMgr einrichten  
 Verwenden Sie diesen Schritt, um den Übergang von Windows PE zum neuen Betriebssystem durchzuführen. Dieser Tasksequenzschritt muss bei jeder Betriebssystembereitstellung ausgeführt werden. Mit diesem Schritt wird der Configuration Manager-Client im neuen Betriebssystem installiert und die weitere Ausführung der Tasksequenz im neuen Betriebssystem ermöglicht.  

 Dieser Schritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Variablen der Tasksequenzaktion „Windows und ConfigMgr einrichten“](task-sequence-action-variables.md#BKMK_SetupWindows).  

 Mit diesem Schritt werden sysprep.inf- oder unattend.xml-Verzeichnisvariablen wie „%WINDIR%“ und „%ProgramFiles%“ durch das Windows PE-Installationsverzeichnis „X:\Windows“ ersetzt. Die Tasksequenz ignoriert Variablen, die mithilfe dieser Umgebungsvariablen angegeben wurden.  

 Verwenden Sie diesen Tasksequenzschritt zur Durchführung der nachstehend beschriebenen Aktionen:  

1.  Vorbereitende Maßnahmen: Windows°PE  

    1.  Ersetzt Tasksequenzvariablen in der Datei „unattend.xml“.  

    2.  Lädt das Paket herunter, das den Configuration Manager-Client enthält. Fügt das Paket zum bereitgestellten Image hinzu.  

2.  Einrichten von Windows  

    1.  Imagebasierte Installation  

        1.  Deaktivieren Sie den Configuration Manager-Client im Image, falls dieser vorhanden ist. Deaktivieren Sie also den automatischen Start für den Configuration Manager-Clientdienst.  

        2.  Aktualisieren Sie die Registrierung im bereitgestellten Image, um das bereitgestellte Betriebssystem zu starten, das den gleichen Laufwerkbuchstaben wie der Referenzcomputer besitzt.  

        3.  Führen Sie einen Neustart für das bereitgestellte Betriebssystem aus.  

        4.  Die Windows-Miniinstallation wird unter Verwendung der zuvor angegebenen Antwortdatei „sysprep.inf“ oder „unattend.xml“ ausgeführt. Bei diesem Vorgang werden alle Interaktionen mit Benutzern unterdrückt. Wenn Sie den Schritt **Netzwerkeinstellungen anwenden** verwenden, um eine Verknüpfung mit einer Domäne zu erstellen, befindet sich diese Information in der Antwortdatei. Die Windows-Miniinstallation verknüpft den Computer mit der Domäne.  

    2.  Setup.exe-basierte Installation.  Führt „Setup.exe“ aus. Dieser Vorgang entspricht dem normalen Windows-Installationsprozess:  

        1.  Kopieren Sie das Betriebssystemupgradepaket, das im Schritt **Betriebssystem anwenden** angegeben wurde, auf das Festplattenlaufwerk.  

        2.  Führen Sie einen Neustart für das neu bereitgestellte Betriebssystem aus.  

        3.  Die Windows-Miniinstallation wird unter Verwendung der zuvor angegebenen Antwortdatei „sysprep.inf“ oder „unattend.xml“ ausgeführt. Bei diesem Vorgang werden alle Einstellungen der Benutzeroberfläche unterdrückt. Wenn Sie den Schritt **Netzwerkeinstellungen anwenden** verwenden, um eine Verknüpfung mit einer Domäne zu erstellen, befindet sich diese Information in der Antwortdatei. Die Windows-Miniinstallation verknüpft den Computer mit der Domäne.  

3.  Einrichten des Configuration Manager-Clients  

    1.  Nachdem die Windows-Miniinstallation abgeschlossen ist, wird die Tasksequenz mithilfe von „setupcomplete.cmd“ fortgesetzt.  

    2.  Aktivieren oder deaktivieren Sie das lokale Administratorkonto, je nachdem, welche Option im Schritt **Windows-Einstellungen anwenden** ausgewählt wurde.  

    3.  Installieren Sie den Configuration Manager-Client mithilfe des zuvor heruntergeladenen Downloadpakets und der in diesem Schritt angegebenen Installationseigenschaften. Der Client wird im „Bereitstellungsmodus“ installiert, um zu verhindern, dass neue Richtlinienanfragen verarbeitet werden, bevor die Tasksequenz abgeschlossen ist.  

    4.  Warten Sie, bis der Client voll funktionstüchtig ist.  

4.  Die Tasksequenz fährt mit der Ausführung des nächsten Schritts fort.  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Images** > **Windows und ConfigMgr einrichten**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
 Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

 **Clientpaket**  
 Klicken Sie auf **Durchsuchen**, und wählen Sie dann das Installationspaket für den Konfigurations-Manager-Client aus, das in diesem Schritt verwendet werden soll.  

 **Clientpaket vor der Produktion verwenden, wenn verfügbar**  
 Wenn ein Präproduktions-Clientpaket verfügbar ist, und der Computer zur Pilotsammlung gehört, verwendet die Tasksequenz dieses Paket statt des Produktionsclientpakets. Bei einem Präproduktionsclient handelt es sich um eine neuere Version für das Testen in der Produktionsumgebung. Klicken Sie auf **Durchsuchen**, und wählen Sie dann das Präproduktions-Clientpaket aus, das in diesem Schritt verwendet werden soll.  

 **Installationseigenschaften**  
 Die Standortzuweisung und die Standardkonfiguration werden von der Tasksequenzaktion automatisch angegeben. Sie können in diesem Feld zusätzliche Installationseigenschaften angeben, die bei der Installation des Clients verwendet werden sollen. Wenn sie mehrere Installationseigenschaften eingeben möchten, müssen Sie sie durch ein Leerzeichen trennen.  

 Sie können Befehlszeilenoptionen angeben, die während der Clientinstallation verwendet werden sollen. Sie können beispielsweise **/skipprereq: silverlight.exe** eingeben, um „CCMSetup.exe“ anzuweisen, die erforderliche Komponente Microsoft Silverlight nicht zu installieren. Weitere Informationen zu diesen Befehlszeileneigenschaften für CCMSetup.exe finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="options"></a>Optionen
> [!NOTE]
> Aktivieren Sie auf der Registerkarte **Optionen** nicht **Bei Fehler fortsetzen**. Wenn während dieses Schritts ein Fehler auftritt, schlägt die Tasksequenz unabhängig davon fehl, ob diese Einstellung aktiviert ist.



##  <a name="BKMK_UpgradeOS"></a> Betriebssystem aktualisieren  
 > [!TIP]  
 > Ab Windows 10 (Version 1709) enthalten Medien mehrere Editionen. Wenn Sie eine Tasksequenz konfigurieren, um ein Betriebssystemupgradepaket oder ein Betriebssystemimage zu verwenden, achten Sie darauf, eine [unterstützte Edition](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client) auszuwählen.

 Verwenden Sie diesen Schritt, um ein Upgrade einer älteren Version von Windows auf eine neuere Version von Windows 10 durchzuführen.  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt.  

Klicken Sie im Tasksequenz-Editor auf **Hinzufügen** > **Images** > **Betriebssystem aktualisieren**, um diesen Schritt hinzuzufügen. 

### <a name="properties"></a>Eigenschaften  
Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

**Upgradepaket**  
 Wählen Sie diese Option aus, um das für das Upgrade zu verwendende Windows 10-Betriebssystemupgradepaket anzugeben.  

**Quellpfad**  
 Gibt einen lokalen Pfad oder einen Netzwerkpfad für die Windows 10-Medien an, die Windows Setup verwendet. Diese Einstellung entspricht der Windows Setup-Befehlszeilenoption **/InstallFrom**. Sie können auch eine Variable angeben, z. B. %mycontentpath% oder %DPC01%. Wenn Sie eine Variable als Quellpfad verwenden, muss diese zuvor in der Tasksequenz festgelegt werden. Wenn Sie beispielsweise den Schritt [Paketinhalt herunterladen](#BKMK_DownloadPackageContent) in der Tasksequenz verwenden, können Sie eine Variable für den Speicherort des Betriebssystemupgradepakets festlegen. Anschließend können Sie die Variable in diesem Schritt als Quellpfad verwenden.  

**Edition**  
 Geben Sie die für das Upgrade zu verwendende Edition in den Betriebssystemmedien an.  

**Product Key**  
 Geben Sie den auf den Upgradeprozess anzuwendenden Product Key an.  

**Folgenden Treiberinhalt während des Upgrades für Windows Setup bereitstellen**  
 Fügt während des Upgradevorgangs Treiber auf dem Zielcomputer hinzu. Diese Einstellung entspricht der Windows Setup-Befehlszeilenoption **/InstallDriver**. Die Treiber müssen mit Windows 10 kompatibel sein. Geben Sie eine der folgenden Optionen an:  

-   **Treiberpaket**: Klicken Sie auf **Durchsuchen** , und wählen Sie ein vorhandenes Treiberpaket aus der Liste aus.  

-   **Bereitgestellter Inhalt**: Wählen Sie diese Option, um den Speicherort für das Treiberpaket anzugeben. Sie können einen lokalen Ordner, einen Netzwerkpfad oder eine Tasksequenzvariable angeben. Wenn Sie eine Variable als Quellpfad verwenden, muss diese zuvor in der Tasksequenz festgelegt werden. Zum Beispiel mithilfe des Schritts [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) .  

**Timeout (Minuten)**  
 Gibt die Anzahl von Minuten an, bevor Configuration Manager diesen Schritt als fehlgeschlagen wertet. Diese Option ist nützlich, wenn Windows Setup die Verarbeitung nicht mehr fortsetzt, aber nicht beendet wird.  

**Kompatibilitätsprüfung für Windows Setup ausführen, ohne Upgrade zu starten**  
 Führt die Kompatibilitätsprüfung für Windows Setup durch, ohne den Upgradevorgang zu starten. Diese Einstellung entspricht der Windows Setup-Befehlszeilenoption **/Compat ScanOnly**. Wenn Sie diese Option verwenden, müssen Sie die gesamte Installationsquelle bereitstellen. Setup gibt als Ergebnis der Überprüfung einen Exitcode zurück. Die folgende Tabelle enthält einige der häufigeren Exitcodes.  

|Exitcode|Details|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Keine Kompatibilitätsprobleme (Erfolg).|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Kompatibilitätsprobleme mit Handlungsbedarf.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Ausgewählte Migrationsoption ist nicht verfügbar, z. B. Enterprise zu Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Nicht für Windows 10 geeignet.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Nicht genügend freier Speicherplatz.|  

Weitere Informationen zu diesem Parameter finden Sie unter [Windows Setup-Befehlszeilenoptionen](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).  

**Alle ablehnbaren Kompatibilitätsmeldungen ignorieren**  
 Gibt an, dass das Setup die Installation abschließt und dabei alle vernachlässigbaren Kompatibilitätsmeldungen ignoriert. Diese Einstellung entspricht der Windows Setup-Befehlszeilenoption **/Compat IgnoreWarning**.  

**Windows Setup dynamisch mit Windows Update aktualisieren**  
 Ermöglicht, dass das Setup dynamische Updatevorgänge durchführt, z.B. das Suchen, Herunterladen und Installieren von Updates. Diese Einstellung entspricht der Windows Setup-Befehlszeilenoption **/DynamicUpdate**. Diese Einstellung ist nicht kompatibel mit den Softwareupdates in Configuration Manager. Aktivieren Sie diese Option, wenn Sie Updates mit eigenständigen Versionen von Windows Server Update Services (WSUS) oder Windows Update for Business verwalten.  

**Richtlinie überschreiben und Standard-Microsoft Update verwenden:** Die lokale Richtlinie wird vorübergehend in Echtzeit außer Kraft gesetzt, um dynamische Updatevorgänge auszuführen und den Computer Updates von Windows Update abrufen zu lassen.
