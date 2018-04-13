---
title: Automatisches Bereitstellen von Softwareupdates
titleSuffix: Configuration Manager
description: Stellen Sie automatisch Softwareupdates durch Hinzufügen neuer Updates zu einer Updategruppe bereit, die mit einer aktiven Bereitstellung verknüpft ist, oder mithilfe von ADRs.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: afa0bd21d23dc0be50d90452ad5dd5d909542279
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
#  <a name="BKMK_AutoDeploy"></a> Automatisches Bereitstellen von Softwareupdates  

*Gilt für: System Center Configuration Manager (Current Branch)*

 Anstatt neue Updates zu einer vorhandenen Updategruppe hinzuzufügen, können Sie eine Regel zur automatischen Bereitstellung (Automatic Deployment Rule, ADR) verwenden. Die Bereitstellung per ADR eignet sich insbesondere für monatliche Softwareupdates („Patch-Dienstag“) und für die Verwaltung von Definitionsupdates. Wenn Sie Hilfe bei der Ermittlung der für Sie geeigneten Bereitstellungsmethode benötigen, lesen Sie [Bereitstellen von Softwareupdates](deploy-software-updates.md).

<!--##  <a name="BKMK_AddUpdatesToExistingGroup"></a> Add software updates to a deployed update group  
After you create and deploy a software update group, you can add software updates to the update group and they will be automatically deployed.  

> [!IMPORTANT]  
>  When you add software updates to an existing software update group that has already been deployed, it might take several minutes before the additional software updates are added to the deployment.  

Use the following procedure to add software updates to an existing update group.  

#### To add software updates to an existing software update group  

1.  In the Configuration Manager console, navigate to **Software Library** > **Overview** > **Software Updates**.  

2.  Select the software updates that are to be added to the new software update group.  

3.  On the **Home** tab, in the **Update** group, click **Edit Membership**.  

4.  Select the software update group to which you want to add the software updates as members.  

5.  Click the **Software Update Groups** node to display the software update group.  

6.  Click the software update group, and in the **Home** tab, in the **Update** group, click **Show Members** to display a list of the software updates in the group.  --mstewart this is already doc'd on the SUG page. -->

##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Erstellen einer automatischen Bereitstellungsregel  
Sie können Softwareupdates mithilfe einer automatischen Bereitstellungsregel automatisch genehmigen und bereitstellen. Sie können festlegen, dass die Regel bei jeder Ausführung Softwareupdates zu einer neuen Softwareupdategruppe hinzufügt oder Softwareupdates zu einer vorhandenen Gruppe hinzufügt. Wenn eine Regel ausgeführt wird und Softwareupdates zu einer vorhandenen Gruppe hinzufügt, entfernt die Regel alle Updates aus der Gruppe und fügt dann die Updates, die die definierten Kriterien erfüllen, zur Gruppe hinzu. 

> [!WARNING]  
>  Überprüfen Sie, ob die Softwareupdatesynchronisierung am Standort abgeschlossen ist, und erstellen Sie erst dann die erste automatische Bereitstellungsregel. Dies ist wichtig, wenn Sie Configuration Manager in einer anderen Sprache als Englisch ausführen. Die Softwareupdateklassifizierungen werden vor der ersten Synchronisierung in Englisch angezeigt und nach dem Abschluss der Softwareupdatesynchronisierung in der lokalisierten Sprache. Regeln, die Sie vor der Synchronisierung der Softwareupdates erstellen, können nach der Synchronisierung möglicherweise nicht verwendet werden, da die Textzeichenfolgen eventuell nicht übereinstimmen.  

 Gehen Sie wie nachfolgend beschrieben vor, um eine automatische Bereitstellungsregel zu erstellen.  

#### <a name="to-create-an-adr"></a>So erstellen Sie eine automatische Bereitstellungsregel  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** **Übersicht** > **Softwareupdates** > **Automatische Bereitstellungsregeln**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Automatische Bereitstellungsregel erstellen**. Der Assistent zum Erstellen automatischer Bereitstellungsregeln wird geöffnet.  

3.  Konfigurieren Sie auf der Seite **Allgemein** die folgenden Einstellungen:  

    -   **Name**: Geben Sie den Namen der automatischen Bereitstellungsregel an. Der Name muss eindeutig sein, das Ziel der Regel angeben und sich am Configuration Manager-Standort leicht von anderen Namen unterscheiden lassen.  

    -   **Beschreibung**: Geben Sie eine Beschreibung der automatischen Bereitstellungsregel an. Die Beschreibung muss einen Überblick über die Bereitstellungsregel und alle anderen relevanten Informationen umfassen, die die Unterscheidung der Regel von anderen Regeln erleichtern. Das Feld „Beschreibung“ ist optional, hat eine Begrenzung auf 256 Zeichen und ist standardmäßig leer.  

    -   **Bereitstellungsvorlage auswählen**: Geben Sie an, ob eine zuvor gespeicherte Bereitstellungsvorlage angewendet werden soll. Sie können eine Bereitstellungsvorlage konfigurieren, die mehrere allgemeine Updates umfasst und bei der Erstellung automatischer Bereitstellungsregeln eingesetzt werden kann. Mit diesen Vorlagen sorgen Sie nicht nur für Konsistenz mit ähnlichen Bereitstellungen, sondern verringern auch Ihren Zeitaufwand.  

         - Im Assistenten zum Erstellen automatischer Bereitstellungsregeln stehen zwei integrierte Vorlagen für die Softwareupdatebereitstellung zur Auswahl. Die Vorlage **Definitionsupdates** enthält allgemeine Einstellungen für die Bereitstellung von Softwaredefinitionsupdates. Die Vorlage **Patch-Dienstag** enthält allgemeine Einstellungen für die monatliche Bereitstellung von Softwaredefinitionsupdates.  

    -   **Sammlung**: Gibt die für die Bereitstellung zu verwendende Zielsammlung an. Mitglieder dieser Sammlung erhalten die in der Bereitstellung definierten Softwareupdates.  

    -   Entscheiden Sie, ob Softwareupdates einer neuen oder bereits vorhandenen Softwareupdategruppe hinzugefügt werden sollen. In den meisten Fällen dürften Sie sich dafür entscheiden, beim Ausführen der automatischen Bereitstellungsregel eine neue Softwareupdategruppe zu erstellen. Falls für die Regel ein aggressiverer Zeitplan gilt, bietet es sich jedoch an, eine vorhandene Gruppe auszuwählen. Wenn Sie die Regel beispielsweise täglich für Definitionsupdates ausführen, können Sie die Softwareupdates einer vorhandenen Softwareupdategruppe hinzufügen.  

    -   **Bereitstellung nach Ausführung dieser Regel aktivieren**: Geben Sie an, ob die Softwareupdatebereitstellung nach der Ausführung der automatischen Bereitstellungsregel aktiviert werden soll. Hinsichtlich dieser Spezifikation ist Folgendes zu beachten:  

        -   Wenn Sie die Bereitstellung aktivieren, werden die Updates, die die Kriterien der Regel erfüllen, einer Softwareupdategruppe hinzugefügt. Der Softwareupdateinhalt wird bei Bedarf heruntergeladen. Der Inhalt wird zu den angegebenen Verteilungspunkten kopiert, und die Updates werden für die Clients in der Zielsammlung bereitgestellt.  

        -   Wenn Sie die Bereitstellung nicht aktivieren, werden die Updates, die die Kriterien der Regel erfüllen, einer Softwareupdategruppe hinzugefügt. Die Bereitstellungsrichtlinie für Softwareupdates ist konfiguriert. Die Updates werden jedoch weder heruntergeladen noch für Clients bereitgestellt. Sie haben somit Zeit, die Bereitstellung der Updates vorzubereiten, zu prüfen, ob die den Kriterien entsprechenden Updates geeignet sind, sowie die Bereitstellung zu einem späteren Zeitpunkt zu aktivieren.  

4.  Konfigurieren Sie auf der Seite Bereitstellungseinstellungen die folgenden Einstellungen:  

    -   **Wake-on-LAN verwenden, um Clients für erforderliche Bereitstellungen zu aktivieren**: Gibt an, ob Wake-On-LAN am Stichtag aktiviert werden soll, damit Aktivierungspakete an Computer gesendet werden, für die mindestens eines der in der Bereitstellung enthaltenen Softwareupdates erforderlich ist. Alle Computer, die sich am Installationsstichtag im Energiesparmodus befinden, werden aktiviert, damit die Installation initiiert werden kann. Clients, die sich im Energiesparmodus befinden und für die keine der in der Bereitstellung enthaltenen Softwareupdates erforderlich sind, werden nicht gestartet. Diese Einstellung ist standardmäßig deaktiviert. Sie können diese Option nur verwenden, wenn Computer und Netzwerke für Wake-On-LAN konfiguriert sind. 

    -   **Detailstufe**: Geben Sie die Detailstufe für die von den Clientcomputern zurückgegebenen Zustandsmeldungen an.  

        > [!IMPORTANT]  
        >  Stellen Sie die Detailstufe beim Bereitstellen von Definitionsupdates auf **Nur Fehler** ein, damit vom Client nur dann eine Zustandsmeldung zurückgegeben wird, wenn ein Definitionsupdate fehlschlägt. Andernfalls gehen vom Client zahlreiche Zustandsmeldungen ein, die sich auf die Leistung des Standortservers auswirken können.  

    -   **Lizenzbedingungen**: Geben Sie an, ob Softwareupdates mit zugehörigen Lizenzbedingungen automatisch bereitgestellt werden sollen. Einige Softwareupdates enthalten Lizenzbedingungen, z. B. Service Packs. Bei der automatischen Bereitstellung von Softwareupdates werden die Lizenzbedingungen nicht angezeigt, und es gibt keine Option zum Annehmen der Lizenzbedingungen. Nach Wunsch können Sie alle Softwareupdates unabhängig von den zugehörigen Lizenzbedingungen automatisch bereitstellen. Sie können aber auch nur Updates bereitstellen, für die es keine zugehörigen Lizenzbedingungen gibt.  
        - Zum Überprüfen der Lizenzbedingungen eines Softwareupdates wählen Sie das Softwareupdate im Arbeitsbereich **Softwarebibliothek** im Knoten **Alle Softwareupdates** aus. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Update** auf **Lizenz lesen**.    
        - Zum Identifizieren der Softwareupdates mit zugehörigen Lizenzbedingungen fügen Sie dem Ergebnisbereich im Knoten **Alle Softwareupdates** die Spalte **Lizenzbedingungen** hinzu. Klicken Sie dann auf die Spaltenüberschrift, um die Spalte nach Softwareupdates mit Lizenzbedingungen zu sortieren.  

5.  Konfigurieren Sie auf der Seite „Softwareupdates“ die Kriterien für die Softwareupdates, die von der automatischen Bereitstellungsregel abgerufen und der Softwareupdategruppe hinzugefügt werden. Das Limit für Softwareupdates in einer automatischen Bereitstellungsregel ist 1.000. Sie können ggf. nach Inhaltsgrößen für Softwareupdates in automatischen Bereitstellungsregeln filtern. Details finden Sie unter [Configuration Manager und vereinfachte Windows-Wartung auf vorherigen Betriebssystemebene](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).


6.  Geben Sie auf der Seite „Auswertungszeitplan“ an, ob die Ausführung der automatischen Bereitstellungsregel nach einem Zeitplan aktiviert werden soll. Ist dies der Fall, klicken Sie auf **Anpassen** , und legen Sie den Wiederholungszeitplan fest. Die für den Zeitplan konfigurierte Startzeit basiert auf der lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird.
    - Die für den Zeitplan konfigurierte Startzeit basiert auf der lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird.
    - Die Auswertung der automatischen Bereitstellungsregel kann dreimal täglich ausgeführt werden.
    - Legen Sie für den Auswertungszeitplan niemals eine Häufigkeit fest, die über den Zeitplan der Softwareupdatesynchronisierung hinausgeht. Der Zeitplan für die Synchronisierung des Softwareupdatepunkts wird angezeigt, damit Sie die Häufigkeit des Auswertungszeitplans leichter festlegen können. 
    - Sie können die automatische Bereitstellungsregel manuell ausführen. Wählen Sie dazu die Regel aus, und klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Automatische Bereitstellungsregel** auf **Jetzt ausführen** .
    
       > [!NOTE]  
       >Ab Configuration Manager Version 1802 können ADRs so geplant werden, dass Sie den Offset eines festgelegten Tags überprüfen können. Wenn der Patchvorgang, der am Dienstag ausgeführt werden soll, bei Ihnen auf einen Mittwoch fällt, kann der Zeitplan für die Auswertung für den zweiten Dienstag des Monats versetzt um einen Tag festgelegt werden. <!--1357133-->
       > - Wenn Sie die Auswertung so planen, dass sie mit einem Offset während der letzten Woche des Monats durchgeführt werden soll, wird sie für den letzten Tag des Monats geplant, wenn der ausgeführte Offset zu einem Überlauf in den nächsten Monat führt. <!--506731-->

       > ![Offset der ADR des benutzerdefinierten Auswertungszeitplans von einem Basistag](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Konfigurieren Sie auf der Seite Bereitstellungszeitplan die folgenden Einstellungen:  

    -   **Auswertung planen**: Geben Sie an, ob die verfügbare Zeit und die Installationsstichtage von Configuration Manager mit UTC oder der lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird, ausgewertet werden sollen.  
         - Wenn Sie die Ortszeit auswählen und dann **So bald wie möglich** für **Zeitpunkt der Verfügbarkeit der Software** oder **Installationsstichtag** auswählen, wird die aktuelle Uhrzeit auf dem Computer mit der Configuration Manager-Konsole verwendet, um zu bestimmen, wann Updates verfügbar sind, oder auf einem Client installiert werden. Wenn sich der Client in einer anderen Zeitzone befindet, erfolgen diese Aktionen, sobald die Evaluierungszeit des Clients erreicht ist.  

    -   **Zeitpunkt der Verfügbarkeit der Software**: Wählen Sie eine der folgenden Einstellungen aus, um anzugeben, wann die Softwareupdates den Clients zur Verfügung stehen:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung den Clientcomputern so bald wie möglich zur Verfügung gestellt werden. Wenn diese Einstellung beim Erstellen der Bereitstellung ausgewählt ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Die zur Installation verfügbaren Updates können dann abgerufen werden.  

        -   **Bestimmte Zeit**: Dadurch werden die Softwareupdates, die in der für Clientcomputer verfügbaren Bereitstellung enthalten sind, zu einem bestimmten Termin (Datum und Uhrzeit) zur Verfügung gestellt. Wenn diese Einstellung beim Erstellen der Bereitstellung aktiviert ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Allerdings stehen die Softwareupdates in der Bereitstellung erst nach dem konfigurierten Termin (Datum und Uhrzeit) für die Installation zur Verfügung.  

    -   **Installationsstichtag**: Wählen Sie eine der folgenden Einstellungen aus, um den Installationsstichtag für die Softwareupdates in der Bereitstellung anzugeben:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung so bald wie möglich automatisch installiert werden.  

        -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung zu einem bestimmten Termin (Datum und Uhrzeit) automatisch installiert werden. Configuration Manager bestimmt den Stichtag zum Installieren von Softwareupdates durch Hinzufügen der konfigurierten Intervalle **Bestimmte Zeit** zu **Zeitpunkt der Verfügbarkeit der Software**.  

            - Der tatsächliche Installationsstichtag ergibt sich aus der Addition des angezeigten Stichtags und eines zufälligen Zeitraums von bis zu zwei Stunden. Durch die zufällige Stichtaganordnung werden die potenziellen Auswirkungen reduziert, die mit der gleichzeitigen Installation der Updates in der Bereitstellung durch alle Clientcomputer in der Sammlung einhergehen.  
          
             - Sie können die Clienteinstellung **Zufällige Stichtaganordnung deaktivieren** für den **Computer-Agent** konfigurieren, um die zufällige Verzögerung der Installation für die erforderlichen Softwareupdates zu deaktivieren. Weitere Informationen finden Sie unter [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8. Konfigurieren Sie auf der Seite Benutzerfreundlichkeit die folgenden Einstellungen:  

    -   **Benutzerbenachrichtigungen**: Geben Sie an, ob zum vorgegebenen **Zeitpunkt der Verfügbarkeit der Software** auf dem Clientcomputer eine Benachrichtigung zu den Softwareupdates im Softwarecenter angezeigt werden soll. Geben Sie auch an, ob auf den Clientcomputern Benutzerbenachrichtigungen angezeigt werden sollen.  

    -   **Verhalten am Stichtag**: Geben Sie das gewünschte Verhalten am Stichtag der Softwareupdatebereitstellung an. Geben Sie an, ob die Softwareupdates in der Bereitstellung installiert werden sollen. Geben Sie auch, ob nach einer Softwareupdateinstallation unabhängig von einem konfigurierten Wartungsfenster ein Systemneustart ausgeführt werden soll. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Verhalten beim Geräteneustart**: Geben Sie an, ob ein Systemneustart auf den Servern und Arbeitsstationen unterdrückt werden soll, wenn ein Systemneustart zum Abschließen der Updateinstallation erforderlich ist.  

        > [!WARNING]  
        >  Das Unterdrücken von Systemneustarts kann in Serverumgebungen oder in Fällen hilfreich sein, in denen Computer nach der Installation von Softwareupdates nicht standardmäßig neu gestartet werden sollen. Allerdings kann dies zu einem unsicheren Computerzustand führen. Durch Erzwingen eines Neustarts hingegen wird gewährleistet, dass die Softwareupdateinstallation umgehend abgeschlossen wird.  

    -   **Schreibfilterverarbeitung für Windows Embedded-Geräte**: Beim Bereitstellen von Softwareupdates für Windows Embedded-Geräte mit Schreibfilteraktivierung können Sie angeben, dass das Softwareupdate auf dem temporären Overlay installiert wird und die Änderungen entweder später, am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden sollen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.  

           -  Stellen Sie beim Bereitstellen eines Softwareupdates auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist.  

    - **Neubewertungsverhalten bei Softwareupdatebereitstellungen nach einem Neustart:** Wählen Sie diese Einstellung aus, um die Bereitstellung von Softwareupdates so zu konfigurieren, dass Clients direkt nach dem Neustart im Anschluss an die Installation von Softwareupdates eine Complianceüberprüfung durchführen. Mithilfe dieser Einstellung kann der Client nach zusätzlichen Updates suchen, die nach dem Neustart des Clients relevant werden, und diese im gleichen Wartungsfenster installieren.

9. Geben Sie auf der Seite „Warnungen“ an, wie Configuration Manager und System Center Operations Manager Warnungen für diese Bereitstellung generieren sollen. Sie können die letzten Warnungen zu Softwareupdates im Arbeitsbereich **Softwarebibliothek** im Knoten **Softwareupdates** prüfen.  

10. Konfigurieren Sie auf der Seite Downloadeinstellungen die folgenden Einstellungen:  

    - Geben Sie an, ob die Updates vom Client heruntergeladen und installiert werden sollen, wenn dieser mit einer langsamen Netzwerkverbindung verbunden ist oder eine Fallbackinhaltsquelle verwendet.  

    - Geben Sie an, ob die Softwareupdates von Clients von einem Fallbackverteilungspunkt heruntergeladen und installiert werden sollen, wenn der Inhalt für die Softwareupdates an einem bevorzugten Verteilungspunkt nicht verfügbar ist.  

    - **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Geben Sie an, ob BranchCache beim Herunterladen von Inhalten verwendet werden soll. Weitere Informationen zu BranchCache finden Sie unter [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Inhalt von Microsoft Updates herunterladen, falls Softwareupdates in aktuellen oder benachbarten Begrenzungsgruppen oder in Standortbegrenzungsgruppen am Verteilungspunkt nicht verfügbar sind**: Wählen Sie diese Einstellung aus, damit die mit dem Intranet verbundenen Clients Softwareupdates von Microsoft Update herunterladen, wenn keine Updates auf Verteilungspunkten verfügbar sind. Internetbasierte Clients können Softwareupdates immer von Microsoft Update herunterladen.

    - Geben Sie an, ob es Clients mit einer getakteten Internetverbindung möglich sein soll, Inhalt nach dem Installationsstichtag herunterzuladen. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.  

    > [!NOTE]  
    >  Der Inhaltsort für die Softwareupdates in einer Bereitstellung wird von den Clients von einem Verwaltungspunkt angefordert. Das Downloadverhalten richtet sich danach, wie Sie den Verteilungspunkt, das Bereitstellungspaket und die Einstellungen auf dieser Seite konfiguriert haben. Weitere Informationen finden Sie unter [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Wählen Sie auf der Seite Bereitstellungspaket ein vorhandenes Bereitstellungspaket aus, oder erstellen Sie anhand der nachfolgenden Einstellungen ein neues Bereitstellungspaket:  

    1.  **Name**: Geben Sie den Namen des Bereitstellungspakets an. Verwenden Sie einen eindeutigen Namen sein, der den Paketinhalt beschreibt. Er ist auf 50 Zeichen begrenzt.  

    2.  **Beschreibung**: Geben Sie eine Beschreibung mit Informationen zum Bereitstellungspaket an. Die Beschreibung ist auf 127 Zeichen begrenzt.  

    3.  **Paketquelle**: Gibt den Speicherort der Quelldateien der Softwareupdates an.  Geben Sie für den Quellspeicherort einen Netzwerkpfad wie **\\\Server\Freigabename\Pfad**ein. Alternativ können Sie auf **Durchsuchen** klicken, um den Netzwerkpfad zu suchen. Erstellen Sie den freigegebenen Ordner für die Quelldateien des Bereitstellungspakets, bevor Sie mit der nächsten Seite fortfahren.  

        - Der von Ihnen angegebene Quellspeicherort des Bereitstellungspakets kann von keinem anderen Softwarebereitstellungspaket verwendet werden.
        - Sie können den Paketquellspeicherort in den Eigenschaften des Bereitstellungspakets ändern, nachdem das Bereitstellungspaket von Configuration Manager erstellt wurde. In diesem Fall müssen Sie jedoch zuerst den Inhalt von der ursprünglichen Paketquelle an den neuen Paketquellspeicherort kopieren.  
        -  Das Computerkonto für den SMS-Anbieter und der Benutzer, der den Assistenten zum Herunterladen der Softwareupdates ausführt, müssen über die NTFS-Berechtigung **Schreiben** für den Downloadort verfügen. Sie müssen den Zugriff auf den Downloadort beschränken, um das Risiko zu verringern, dass Angreifer die Quelldateien der Softwareupdates manipulieren.  
       

    4.  **Sendepriorität**: Geben Sie die Sendepriorität für das Bereitstellungspaket an. Configuration Manager verwendet Sendepriorität für das Bereitstellungspaket beim Senden des Pakets an Verteilungspunkte. Bereitstellungspakete werden in der Reihenfolge ihrer Priorität gesendet: „Hoch“, „Mittel“ oder „Niedrig“. Pakete mit identischer Priorität werden in der Reihenfolge ihrer Erstellung gesendet. Wenn es keinen Rückstand gibt, wird das Paket unabhängig von seiner Priorität sofort verarbeitet.  

12. Geben Sie auf der Seite Verteilungspunkte die Verteilungspunkte oder Verteilungspunktgruppen an, auf denen die Softwareupdatedateien gehostet werden sollen. Weitere Informationen zu Verteilungspunkten finden Sie unter [Konfigurationen für Verteilungspunkte](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Diese Seite ist nur verfügbar, wenn Sie ein neues Softwareupdate-Bereitstellungspaket erstellen.
  

13. Geben Sie auf der Seite Downloadort an, ob die Softwareupdatedateien vom Internet oder aus dem lokalen Netzwerk heruntergeladen werden sollen. Konfigurieren Sie die folgenden Einstellungen:  

    -   **Softwareupdates aus dem Internet herunterladen**: Wählen Sie diese Einstellung aus, um die Softwareupdates von einem bestimmten Speicherort im Internet herunterzuladen. Diese Einstellung ist standardmäßig aktiviert.  

    -   **Softwareupdates von einem Pfad im lokalen Netzwerk herunterladen**: Wählen Sie diese Einstellung aus, um die Softwareupdates aus einem lokalen Verzeichnis oder aus einem freigegebenen Ordner herunterzuladen. Diese Einstellung ist nützlich, wenn der Computer, auf dem der Assistent ausgeführt wird, keine Internetverbindung aufweist. Die Softwareupdates können von jedem Computer mit Internetzugriff vorläufig heruntergeladen und im lokalen Netzwerk an einem Speicherort abgelegt werden, der von dem Computer aus zugänglich ist, auf dem der Assistent ausgeführt wird.  

14. Wählen Sie auf der Seite Sprachauswahl die Sprachen aus, für die die ausgewählten Softwareupdates heruntergeladen werden. Die Softwareupdates werden nur dann heruntergeladen, wenn sie in den ausgewählten Sprachen verfügbar sind. Softwareupdates, die nicht sprachspezifisch sind, werden immer heruntergeladen. Standardmäßig werden vom Assistenten die Sprachen ausgewählt, die Sie in den Eigenschaften des Softwareupdatepunkts konfiguriert haben. Es muss mindestens eine Sprache ausgewählt werden, bevor die nächste Seite angezeigt werden kann. Wenn Sie nur Sprachen auswählen, die von einem Softwareupdate nicht unterstützt werden, kann das Update nicht heruntergeladen werden.  

15. Überprüfen Sie die Einstellungen auf der Seite Zusammenfassung. Klicken Sie auf **Als Vorlage speichern**, um die Einstellungen für eine Bereitstellungsvorlage zu speichern. Geben Sie einen Namen ein, und wählen Sie die Einstellungen aus, die Sie in der Vorlage einschließen möchten. Klicken Sie anschließend auf **Speichern**. Zum Ändern einer konfigurierten Einstellung klicken Sie auf die entsprechende Assistentenseite, und nehmen Sie die Änderung vor.  
    -  Der Vorlagenname kann alphanumerische ASCII-Zeichen sowie die Zeichen **\\** (umgekehrter Schrägstrich) oder **‘** (einfaches Anführungszeichen) enthalten.  

16. Klicken Sie auf **Weiter** , um die automatische Bereitstellungsregel zu erstellen.  

 Nachdem Sie den Assistenten abgeschlossen haben, wird die automatische Bereitstellungsregel ausgeführt. Dadurch werden die Softwareupdates, die den angegebenen Kriterien entsprechen, einer Softwareupdategruppe hinzugefügt. Die ADR lädt daraufhin die Updates in eine Inhaltsbibliothek auf den Standortserver herunter und verteilt sie an die konfigurierten Verteilungspunkte. Die ADR stellt anschließend die Softwareupdategruppe für Clients in der Zielsammlung bereit.  

##  <a name="BKMK_AddDeploymentToADR"></a> Hinzufügen einer neuen Bereitstellung zu einer vorhandenen automatischen Bereitstellungsregel  
 Nach der Erstellung einer automatischen Bereitstellungsregel können Sie zusätzliche Bereitstellungen zur Regel hinzufügen. Dies hilft Ihnen dabei, die Komplexität der Bereitstellung verschiedener Updates für verschiedene Sammlungen zu verwalten. Jede neue Bereitstellung verfügt über sämtliche Funktionen und die Bereitstellungsüberwachungsumgebung.  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>So fügen Sie einer vorhandenen automatischen Bereitstellungsregel eine neue Bereitstellung hinzu  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Softwareupdates** > **Automatische Bereitstellungsregeln**, und wählen Sie dann die gewünschte Regel.  

2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Automatische Bereitstellungsregel** auf **Bereitstellung hinzufügen**. Der Assistent zum Hinzufügen einer Bereitstellung wird geöffnet.  

3.  Konfigurieren Sie auf der Seite **Sammlung** die folgenden Einstellungen:  

    -   **Sammlung**: Gibt die für die Bereitstellung zu verwendende Zielsammlung an. Mitglieder dieser Sammlung erhalten die in der Bereitstellung definierten Softwareupdates.  

    -   **Bereitstellung nach Ausführung dieser Regel aktivieren**: Geben Sie an, ob die Softwareupdatebereitstellung nach der Ausführung der automatischen Bereitstellungsregel aktiviert werden soll. Hinsichtlich dieser Spezifikation ist Folgendes zu beachten:  

        -   Wenn Sie die Bereitstellung aktivieren, werden die Updates, die die Kriterien der Regel erfüllen, einer Softwareupdategruppe hinzugefügt. Der Softwareupdateinhalt wird bei Bedarf heruntergeladen. Der Inhalt wird zu den angegebenen Verteilungspunkten kopiert, und die Updates werden für die Clients in der Zielsammlung bereitgestellt.  

        -  Wenn Sie die Bereitstellung nicht aktivieren, werden die Updates, die die Kriterien der Regel erfüllen, einer Softwareupdategruppe hinzugefügt. Die Bereitstellungsrichtlinie für Softwareupdates ist konfiguriert. Die Updates werden jedoch weder heruntergeladen noch für Clients bereitgestellt. Sie haben somit Zeit, die Bereitstellung der Updates vorzubereiten, zu prüfen, ob die den Kriterien entsprechenden Updates geeignet sind, sowie die Bereitstellung zu einem späteren Zeitpunkt zu aktivieren.  

4.  Konfigurieren Sie auf der Seite Bereitstellungseinstellungen die folgenden Einstellungen:  

    -   **Wake-on-LAN verwenden, um Clients für erforderliche Bereitstellungen zu aktivieren**: Gibt an, ob Wake-On-LAN am Stichtag aktiviert werden soll, damit Aktivierungspakete an Computer gesendet werden, für die mindestens eines der in der Bereitstellung enthaltenen Softwareupdates erforderlich ist. Alle Computer, die sich am Installationsstichtag im Energiesparmodus befinden, werden aktiviert, damit die Installation initiiert werden kann. Clients, die sich im Energiesparmodus befinden und für die keine der in der Bereitstellung enthaltenen Softwareupdates erforderlich sind, werden nicht gestartet. Diese Einstellung ist standardmäßig deaktiviert. Sie können diese Option nur verwenden, wenn Computer und Netzwerke für Wake-On-LAN konfiguriert sind.  

    -   **Detailstufe**: Geben Sie die Detailstufe für die von den Clientcomputern zurückgegebenen Zustandsmeldungen an.  

        > [!IMPORTANT]  
        >  Stellen Sie die Detailstufe beim Bereitstellen von Definitionsupdates auf **Nur Fehler** ein, damit vom Client nur dann eine Zustandsmeldung zurückgegeben wird, wenn ein Definitionsupdate nicht an den Client geliefert werden kann. Andernfalls gehen vom Client zahlreiche Zustandsmeldungen ein, die sich auf die Leistung des Standortservers auswirken können.  

5.  Konfigurieren Sie auf der Seite Bereitstellungszeitplan die folgenden Einstellungen:  

    -   **Auswertung planen**: Geben Sie an, ob die verfügbare Zeit und die Installationsstichtage von Configuration Manager mit UTC oder der lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird, ausgewertet werden sollen.  

           -  Wenn Sie die Ortszeit auswählen und dann **So bald wie möglich** für **Zeitpunkt der Verfügbarkeit der Software** oder **Installationsstichtag** auswählen, wird die aktuelle Uhrzeit auf dem Computer mit der Configuration Manager-Konsole verwendet, um zu bestimmen, wann Updates verfügbar sind, oder auf einem Client installiert werden. Wenn sich der Client in einer anderen Zeitzone befindet, erfolgen diese Aktionen, sobald die Evaluierungszeit des Clients erreicht ist.  

    -   **Zeitpunkt der Verfügbarkeit der Software**: Wählen Sie eine der folgenden Einstellungen aus, um anzugeben, wann die Softwareupdates den Clients zur Verfügung stehen:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung den Clientcomputern so bald wie möglich zur Verfügung gestellt werden. Wenn diese Einstellung beim Erstellen der Bereitstellung ausgewählt ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Die zur Installation verfügbaren Updates können dann abgerufen werden.  

        -   **Bestimmte Zeit**: Dadurch werden die Softwareupdates, die in der für Clientcomputer verfügbaren Bereitstellung enthalten sind, zu einem bestimmten Termin (Datum und Uhrzeit) zur Verfügung gestellt. Wenn diese Einstellung beim Erstellen der Bereitstellung aktiviert ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Allerdings stehen die Softwareupdates in der Bereitstellung erst nach dem konfigurierten Termin (Datum und Uhrzeit) für die Installation zur Verfügung. 

    -   **Installationsstichtag**: Wählen Sie eine der folgenden Einstellungen aus, um den Installationsstichtag für die Softwareupdates in der Bereitstellung anzugeben:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung so bald wie möglich automatisch installiert werden.  

        -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung zu einem bestimmten Termin (Datum und Uhrzeit) automatisch installiert werden. Configuration Manager bestimmt den Stichtag zum Installieren von Softwareupdates durch Hinzufügen der konfigurierten Intervalle **Bestimmte Zeit** zu **Zeitpunkt der Verfügbarkeit der Software**.  

               - Der tatsächliche Installationsstichtag ergibt sich aus der Addition des angezeigten Stichtags und eines zufälligen Zeitraums von bis zu zwei Stunden. Dadurch werden die potenziellen Auswirkungen reduziert, die mit der gleichzeitigen Installation der Updates in der Bereitstellung durch alle Clientcomputer in der Zielsammlung einhergehen.  
              - Sie können die Clienteinstellung **Zufällige Stichtaganordnung deaktivieren** für den **Computer-Agent** konfigurieren, um die zufällige Verzögerung der Installation für die erforderlichen Softwareupdates zu deaktivieren. Weitere Informationen finden Sie unter [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

6.  Konfigurieren Sie auf der Seite Benutzerfreundlichkeit die folgenden Einstellungen:  

    -   **Benutzerbenachrichtigungen**: Geben Sie an, ob zum vorgegebenen **Zeitpunkt der Verfügbarkeit der Software** auf dem Clientcomputer eine Benachrichtigung zu den Softwareupdates im Softwarecenter angezeigt werden soll. Geben Sie auch an, ob auf den Clientcomputern Benutzerbenachrichtigungen angezeigt werden sollen.  

    -   **Verhalten am Stichtag**: Geben Sie das gewünschte Verhalten am Stichtag der Softwareupdatebereitstellung an. Geben Sie an, ob die Softwareupdates in der Bereitstellung installiert werden sollen. Geben Sie auch, ob nach einer Softwareupdateinstallation unabhängig von einem konfigurierten Wartungsfenster ein Systemneustart ausgeführt werden soll. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Verhalten beim Geräteneustart**: Geben Sie an, ob ein Systemneustart auf den Servern und Arbeitsstationen unterdrückt werden soll, wenn ein Systemneustart zum Abschließen der Updateinstallation erforderlich ist.  
 
           > [!WARNING]  
           >  Das Unterdrücken von Systemneustarts kann in Serverumgebungen oder in Fällen hilfreich sein, in denen Computer nach der Installation von Softwareupdates nicht standardmäßig neu gestartet werden sollen. Allerdings kann dies zu einem unsicheren Computerzustand führen. Durch Erzwingen eines Neustarts hingegen wird gewährleistet, dass die Softwareupdateinstallation umgehend abgeschlossen wird.  

    - **Schreibfilterverarbeitung für Windows Embedded-Geräte**: Beim Bereitstellen von Softwareupdates für Windows Embedded-Geräte mit Schreibfilteraktivierung können Sie angeben, dass das Softwareupdate auf dem temporären Overlay installiert wird und die Änderungen entweder später, am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden sollen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.  

        - Stellen Sie beim Bereitstellen eines Softwareupdates auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist.  

7.  Geben Sie auf der Seite „Warnungen“ an, wie Configuration Manager und System Center Operations Manager Warnungen für diese Bereitstellung generieren sollen. Sie können die letzten Warnungen zu Softwareupdates im Arbeitsbereich **Softwarebibliothek** im Knoten **Softwareupdates** prüfen.  

8. Konfigurieren Sie auf der Seite Downloadeinstellungen die folgenden Einstellungen:  

    - Geben Sie an, ob die Softwareupdates vom Client heruntergeladen und installiert werden sollen, wenn dieser mit einer langsamen Netzwerkverbindung oder einer Fallbackinhaltsquelle vorliegt.  

    - Geben Sie an, ob die Softwareupdates vom Client von einem Fallbackverteilungspunkt heruntergeladen und installiert werden sollen, wenn der Inhalt für die Softwareupdates an einem bevorzugten Verteilungspunkt nicht verfügbar ist.  

    - **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Geben Sie an, ob BranchCache beim Herunterladen von Inhalten verwendet werden soll. Weitere Informationen zu BranchCache finden Sie unter [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Inhalt von Microsoft Updates herunterladen, falls Softwareupdates in aktuellen oder benachbarten Begrenzungsgruppen oder in Standortbegrenzungsgruppen am Verteilungspunkt nicht verfügbar sind**: Wählen Sie diese Einstellung aus, damit die mit dem Intranet verbundenen Clients Softwareupdates von Microsoft Update herunterladen, wenn keine Updates auf Verteilungspunkten verfügbar sind. Internetbasierte Clients können Softwareupdates immer von Microsoft Update herunterladen.

    - Geben Sie an, ob es Clients mit einer getakteten Internetverbindung möglich sein soll, Inhalt nach dem Installationsstichtag herunterzuladen. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.  

    > [!NOTE]  
    > Der Inhaltsort für die Softwareupdates in einer Bereitstellung wird von den Clients von einem Verwaltungspunkt angefordert. Das Downloadverhalten richtet sich danach, wie Sie den Verteilungspunkt, das Bereitstellungspaket und die Einstellungen auf dieser Seite konfiguriert haben. Weitere Informationen finden Sie unter [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

Weitere Informationen zum Bereitstellungsprozess finden Sie unter [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Nächste Schritte
[Überwachen von Softwareupdates](monitor-software-updates.md)
