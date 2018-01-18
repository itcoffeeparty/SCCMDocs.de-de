---
title: "Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem"
titleSuffix: Configuration Manager
description: "Mit den Tasksequenzen in System Center Configuration Manager kann für ein Betriebssystem automatisch ein Upgrade von Windows 7 oder höher auf Windows 10 durchgeführt werden."
ms.custom: na
ms.date: 12/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: "12"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 058b0710484a0452ddf19655bf2cabbb43f624ad
ms.sourcegitcommit: 92c3f916e6bbd35b6208463ff406e0247664543a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie Tasksequenzen in Configuration Manager, um automatisch ein Upgrade eines Betriebssystems auf einem Zielcomputer auszuführen. Sie können dieses Upgrade von Windows 7 oder höher auf Windows 10 oder von Windows Server 2012 oder höher auf Windows Server 2016 durchführen. Sie erstellen eine Tasksequenz, die auf das Upgradepaket für das Betriebssystem oder jegliche anderen Inhalte verweist, die installiert werden sollen, z.B. Anwendungen oder Softwareupdates. Die Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem ist Teil des Szenarios [Upgrade von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md).  

##  <a name="BKMK_UpgradeOS"></a> Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem  
 Um ein Upgrade des Betriebssystems auf Computern durchzuführen, können Sie eine Tasksequenz erstellen und im Assistenten zum Erstellen von Tasksequenzen die Option zum **Durchführen eines Upgrades für ein Betriebssystem mit einem Upgradepaket** auswählen. Der Assistent fügt die Schritte zum Durchführen des Upgrades für das Betriebssystem, zum Anwenden von Softwareupdates und zum Installieren von Anwendungen hinzu. Bevor Sie die Tasksequenz erstellen, müssen folgende Anforderungen erfüllt sein:    

-   **Erforderlich**  

     - Das [Upgradepaket für das Betriebssystem](../get-started/manage-operating-system-upgrade-packages.md) muss in der Configuration Manager-Konsole verfügbar sein.
     - Wenn Sie ein Upgrade auf Windows Server 2016 durchführen, müssen Sie im Tasksequenzschritt „Betriebssystem aktualisieren“ die Einstellung **Ignore any dismissable compatibility messages** (Alle verwerfbaren Konformitätsmeldungen ignorieren) auswählen. Andernfalls tritt beim Upgrade ein Fehler auf.

-   **Erforderlich (sofern verwendet)**  

    -   [Softwareupdates](../../sum/get-started/synchronize-software-updates.md) müssen in der Configuration Manager-Konsole synchronisiert werden.  

    -   [Anwendungen](../../apps/deploy-use/create-applications.md) müssen zur Configuration Manager-Konsole hinzugefügt werden.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>So erstellen Sie eine Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenz erstellen** , um den Tasksequenzerstellungs-Assistenten zu starten.  

4.  Klicken Sie auf der Seite **Neue Tasksequenz erstellen** auf die Option zum **Durchführen eines Upgrades für ein Betriebssystem mit einem Upgradepaket**, und klicken Sie dann auf **Weiter**.  

5.  Geben Sie auf der Seite **Informationen zur Tasksequenz** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Tasksequenzname**: Geben Sie einen Namen zur Identifikation der Tasksequenz an.  

    -   **Beschreibung**: Geben Sie eine Beschreibung der Aufgabe an, die von der Tasksequenz ausgeführt wird.  

6.  Geben Sie auf der Seite zum **Durchführen eines Upgrades für das Windows-Betriebssystem** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Upgradepaket**: Geben Sie die Upgradepaket, das die Quelldateien für das Upgrade des Betriebssystems enthält. Sie können überprüfen, ob Sie das richtige Paket ausgewählt haben, indem Sie die Informationen im **Eigenschaften** -Bereich betrachten. Weitere Informationen finden Sie unter [Manage operating system upgrade packages (Verwalten von Betriebssystem-Upgradepaketen)](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Editionsindex**: Wenn mehrere Editionsindizes für das Betriebssystem im Paket verfügbar sind, wählen Sie den gewünschten Editionsindex aus. Standardmäßig wird das erste Element ausgewählt.  

    -   **Product key**: Geben Sie den Product Key für das zu installierende Windows-Betriebssystem an. Sie können codierte Volumenlizenzschlüssel und standardmäßige Product Keys angeben. Wenn Sie einen nicht codierten Product Key verwenden, muss jede Gruppe aus fünf Zeichen durch einen Bindestrich (-) getrennt werden. Beispiel: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Wenn das Upgrade für eine Volumenlizenzedition vorgesehen ist, ist der Product Key nicht erforderlich. Sie benötigen nur einen Product Key, wenn das Upgrade für eine Verkaufsversion von Windows vorgesehen ist.  

    -   **Alle verwerfbaren Konformitätsmeldungen ignorieren**: Wählen Sie diese Einstellung aus, wenn Sie ein Upgrade auf Windows Server 2016 durchführen. Wenn Sie diese Einstellung nicht auswählen, kann die Tasksequenz nicht abgeschlossen werden, weil Windows Setup darauf wartet, dass der Benutzer in einem Bestätigungsdialogfeld in einer Windows-App auf **Bestätigen** klickt.   

7.  Geben Sie auf der Seite **Updates einschließen** an, ob erforderliche Softwareupdates, alle Softwareupdates oder keine Softwareupdates installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie angeben, dass Softwareupdates installiert werden sollen, werden von Configuration Manager nur die Softwareupdates installiert, die für Sammlungen bestimmt sind, von denen der Zielcomputer ein Mitglied ist.  

8.  Geben Sie auf der Seite **Anwendungen installieren** die Anwendungen an, die auf dem Zielcomputer installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie mehrere Anwendungen angeben, können Sie auch angeben, dass die Tasksequenz fortgesetzt werden soll, wenn bei der Installation einer bestimmten Anwendung ein Fehler auftritt.  

9. Schließen Sie den Assistenten ab.  



## <a name="configure-pre-cache-content"></a>Konfigurieren des zwischengespeicherten Inhalts
Ab Version 1702 können Clients mithilfe von Zwischenspeicherungsfunktionen für verfügbare Bereitstellungen von Tasksequenzen nur relevanten Inhalt herunterladen, bevor der Benutzer die Tasksequenz installiert.
> [!TIP]  
> Dieses Feature wurde erstmals in Version 1702 als [Vorabfeature](/sccm/core/servers/manage/pre-release-features) eingeführt. Ab Version 1706 können ist diese Funktion kein vorab veröffentlichtes Feature mehr.

Ein Beispiel: Es soll eine Tasksequenz für ein direktes Upgrade von Windows 10 bereitgestellt werden, es soll nur eine einzige Tasksequenz für alle Benutzer verwendet werden und es sollen mehrere Architekturen und/oder Sprachen verfügbar sein. In Vorgängerversionen startet der Download von Inhalten, wenn der Benutzer eine bereitgestellte Tasksequenz im Softwarecenter herunterlädt. Durch diese Verzögerung verzögert sich auch der Installationsstart. Alle Inhalte, auf die in der Tasksequenz verwiesen wird, werden heruntergeladen. Dieser Inhalt schließt das Ugradepaket für das Betriebssystem für alle Sprachen und Architekturen mit ein. Wenn jedes Upgradepaket in etwa eine Größe von 3 GB hat, ist der Gesamtinhalt sehr groß.

Mit dem Zwischenspeichern von Inhalten können Sie den Client dahingehend einschränken, dass er nur zutreffenden Inhalt herunterladen darf, wenn er die Bereitstellung empfängt. Wenn der Benutzer dann im Softwarecenter auf **Installieren** klickt, steht der Inhalt bereit, und die Installation startet sofort, da der Inhalt bereits auf der lokalen Festplatte gespeichert ist.

### <a name="to-configure-the-pre-cache-feature"></a>So konfigurieren Sie die Zwischenspeicherungsfunktion

1. Erstellen Sie Betriebssystem-Aktualisierungspakete für bestimmte Architekturen und Sprachen. Geben Sie die Architektur und die Sprache auf der Registerkarte **Datenquelle** des Pakets an. Verwenden Sie für die Sprache die Dezimalkonvertierung (1033 ist beispielsweise der Dezimalwert für Englisch, 0x0409 seine hexadezimale Entsprechung). Weitere Informationen finden Sie unter [Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Die Werte der Architektur und der Sprache stimmen mit den Bedingungen der einzelnen Schritte der Tasksequenz überein, damit bestimmt werden kann, ob das Upgradepaket für das Betriebssystem zwischengespeichert wird.
1. Erstellen Sie eine Tasksequenz mit bedingten Schritten für die verschiedenen Sprachen und Architekturen. Beispielsweise wird im folgenden Schritt die englische Version verwendet:

    ![Zwischenspeicherungseigenschaften](../media/precacheproperties2.png)

    ![Zwischenspeicherungsoptionen](../media/precacheoptions2.png)  

3. Bereitstellen der Tasksequenz Konfigurieren Sie für die Zwischenspeicherungsfunktion die folgenden Einstellungen:
    - Wählen Sie auf der Registerkarte **Allgemein** die Option **Inhalt für diese Tasksequenz vorab herunterladen** aus.
    - Konfigurieren Sie auf der Registerkarte **Bereitstellungseinstellungen** die Tasksequenz mit der Einstellung **Verfügbar** für **Zweck**.
    - Wählen Sie auf der Registerkarte **Zeitplanung** für die Einstellung **Verfügbarkeitsdatum der Bereitstellung festlegen** die derzeit ausgewählte Zeit aus. Der Client beginnt mit dem Zwischenspeichern des Inhalts zur verfügbaren Zeit der Bereitstellung. Wenn ein Zielclient diese Richtlinie empfängt, liegt der verfügbare Zeitpunkt in der Vergangenheit. Das bedeutet, dass der Download des Zwischenspeichers direkt startet. Wenn der Client diese Richtlinie empfängt, aber der verfügbare Zeitpunkt in der Zukunft liegt, beginnt der Client erst mit dem Zwischenspeichern des Inhalts, wenn dieser Zeitpunkt erreicht wurde. 
    - Konfigurieren Sie auf der Registerkarte **Verteilungspunkte** die Einstellungen der **Bereitstellungsoptionen**. Wenn der Inhalt noch nicht auf einem Client zwischengespeichert ist, wenn ein Benutzer die Installation startet, werden diese Einstellungen verwendet.


### <a name="user-experience"></a>Benutzerfreundlichkeit
- Wenn der Client die Bereitstellungsrichtlinie empfängt, startet er nach Ablauf des verfügbaren Zeitpunkts der Bereitstellung mit dem Zwischenspeichern des Inhalts. Dieser Inhalt umfasst alle referenzierten Pakete und nur das Upgradepaket für das Betriebssystem, das dem Client entspricht, und zwar basierend auf den in der Tasksequenz festgelegten Bedingungen.
- Wenn die Bereitstellung Benutzern verfügbar gemacht wird, wird eine Benachrichtigung angezeigt, um Benutzer über die neue Bereitstellung zu informieren. Die Tasksequenz wird außerdem im Softwarecenter angezeigt. Der Benutzer kann zum Softwarecenter navigieren und auf **Installieren** klicken, um die Installation zu starten.
- Wenn der Inhalt nicht vollständig zwischengespeichert wurde und der Benutzer die Tasksequenz installiert, verwendet der Client die Einstellungen, die Sie in der Registerkarte **Bereitstellungsoption** der Bereitstellung angegeben haben. 



## <a name="download-package-content-task-sequence-step"></a>Paketinhalt herunterladen – Tasksequenzschritt  
 Der Schritt [Paketinhalt herunterladen](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) kann in den folgenden Szenarios vor dem Schritt **Betriebssystem aktualisieren** ausgeführt werden:  

-   Sie verwenden eine einzelne Upgradetasksequenz, die sowohl für x86- als auch für x64-Plattformen verwendet werden kann. Fügen Sie der Gruppe **Vorbereitung auf das Upgrade** zwei **Paketinhalt herunterladen**-Schritte hinzu. Legen Sie für jeden Schritt Bedingungen fest, um die Clientarchitektur zu ermitteln. Diese Bedingung hat zur Folge, dass in diesem Schritt nur das passende Upgradepaket für das Betriebssystem heruntergeladen wird. Konfigurieren Sie jeden **Paketinhalt herunterladen** -Schritt zur Verwendung derselben Variablen, und verwenden Sie die Variable für den Medienpfad im Schritt **Betriebssystem aktualisieren** .  

-   Um dynamisch ein passendes Treiberpaket herunterzuladen, verwenden Sie zwei **Paketinhalt herunterladen** -Schritte mit Bedingungen zum Ermitteln des geeigneten Hardwaretyps für jedes Treiberpaket. Konfigurieren Sie jeden **Paketinhalt herunterladen**-Schritt, sodass dieselbe Variable verwendet wird. Verwenden Sie anschließend diese Variable für den Wert **Bereitgestellter Inhalt** im Abschnitt „Treiber“ des Schritts **Betriebssystem aktualisieren**.  

   > [!NOTE]
   > Wenn es mehrere Pakete gibt, fügt Configuration Manager dem Variablennamen ein numerisches Suffix hinzu. Wenn Sie z.B. eine Variable von %mycontent% als benutzerdefinierte Variable festlegen, speichert der Client an diesem Speicherort sämtlichen Inhalt, auf den verwiesen wird. Wenn Sie in einem späteren Schritt auf die Variable verweisen, z.B. **Betriebssystem aktualisieren**, verwenden Sie die Variable mit einem numerischen Suffix. In diesem Beispiel wird %mycontent01% oder %mycontent02% verwendet, wobei die Nummer der Reihenfolge entspricht, in der diese Inhalte im Schritt **Vorbereitung auf das Upgrade** aufgelistet sind.

## <a name="optional-post-processing-task-sequence-steps"></a>Optionale Nachbearbeitung – Tasksequenzschritte  
 Nach dem Erstellen der Tasksequenz können Sie nach Bedarf zusätzliche Schritte hinzufügen. So z.B. das Deinstallieren von Anwendungen mit bekannten Kompatibilitätsproblemen oder Maßnahmen zur Nachbearbeitung hinzufügen, die nach einem Neustart des Computers und der erfolgreichen Durchführung des Upgrades auf Windows 10 ausgeführt werden. Fügen Sie diese zusätzlichen Schritte in der Nachbearbeitungsgruppe der Tasksequenz hinzu.  

> [!NOTE]  
>  Da diese Tasksequenz nicht linear verläuft, gibt es Situationen bei den einzelnen Schritten, die sich auf die Ergebnisse der Tasksequenz auswirken können, je nachdem, ob der Clientcomputer erfolgreich aktualisiert wurde oder ob ein Rollback des Clientcomputers auf die ursprüngliche Betriebssystemversion durchgeführt werden muss.  

## <a name="optional-rollback-task-sequence-steps"></a>Optionales Rollback – Tasksequenzschritte  
 Wenn nach dem Neustart des Computers ein Fehler beim Upgradevorgang auftreten sollte, führt Windows Setup ein Rollback für das Upgrade auf das vorherige Betriebssystem aus. Die Tasksequenz fährt dann mit einem beliebigen Schritt in der Rollback-Gruppe fort. Nach dem Erstellen der Tasksequenz können Sie optionale Schritte zur Rollbackgruppe hinzufügen.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Nach Computerneustart entfernte Ordner und Dateien  
 Wenn die Tasksequenz abgeschlossen wurde, entfernt der Client die Skripts zur Nachbearbeitung und für Rollbacks erst, nachdem der Computer neugestartet wurde. Diese Skriptdateien enthalten keine vertraulichen Informationen.  
