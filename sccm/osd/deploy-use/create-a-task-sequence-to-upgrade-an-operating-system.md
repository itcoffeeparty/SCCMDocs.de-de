---
title: Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem
titleSuffix: Configuration Manager
description: Automatisches Upgrade von Windows 7 oder höher auf Windows 10 mithilfe einer Tasksequenz
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 91d3bf5b1488eb7eac52c7426e4bdeeb92ff43b8
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie Tasksequenzen in Configuration Manager, um automatisch ein Upgrade eines Betriebssystems auf einem Zielcomputer auszuführen. Sie können dieses Upgrade von Windows 7 oder höher auf Windows 10 oder von Windows Server 2012 oder höher auf Windows Server 2016 durchführen. Erstellen Sie eine Tasksequenz, die auf das Upgradepaket für das Betriebssystem oder jegliche anderen Inhalte verweist, die installiert werden sollen, z.B. Anwendungen oder Softwareupdates. Die Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem ist Teil des Szenarios [Upgrade von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md).  



##  <a name="BKMK_UpgradeOS"></a> Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem  
 Um ein Upgrade des Betriebssystems auf Computern durchzuführen, können Sie eine Tasksequenz erstellen und im Assistenten zum Erstellen von Tasksequenzen die Option zum **Durchführen eines Upgrades für ein Betriebssystem mit einem Upgradepaket** auswählen. Der Assistent fügt die Schritte der Tasksequenz zum Durchführen des Upgrades für das Betriebssystem, zum Anwenden von Softwareupdates und zum Installieren von Anwendungen hinzu. Bevor Sie die Tasksequenz erstellen, müssen folgende Anforderungen erfüllt sein:    

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

7.  Geben Sie auf der Seite **Updates einschließen** an, ob erforderliche, alle oder keine Softwareupdates installiert werden sollen. Klicken Sie anschließend auf **Weiter**. Wenn Sie angeben, dass Softwareupdates installiert werden sollen, werden von Configuration Manager nur die Softwareupdates installiert, die für Sammlungen bestimmt sind, von denen der Zielcomputer ein Mitglied ist.  

8.  Geben Sie auf der Seite **Anwendungen installieren** die Anwendungen an, die auf dem Zielcomputer installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie mehrere Anwendungen angeben, können Sie auch angeben, dass die Tasksequenz fortgesetzt werden soll, wenn bei der Installation einer bestimmten Anwendung ein Fehler auftritt.  

9. Schließen Sie den Assistenten ab.  


 > [!Important] 
 > Wenn die Tasksequenz abgeschlossen wurde, entfernt der Client die Skripts zur Nachbearbeitung und für Rollbacks erst, nachdem der Computer neugestartet wurde. Diese Skriptdateien enthalten keine vertraulichen Informationen.  


 > [!Note]
 > Ab Version 1802 enthält die Standardvorlage der Tasksequenz für das direkte Windows 10-Upgrade zusätzliche Gruppen mit empfohlenen Aktionen, die vor und nach dem Upgradevorgang hinzugefügt werden können. Diese Aktionen werden häufig von Kunden eingesetzt, die erfolgreiche Upgrades ihrer Geräte auf Windows 10 durchführen. Weitere Informationen finden Sie in den empfohlenen Tasksequenzschritten [zum Vorbereiten des Upgrades](#recommended-task-sequence-steps-to-prepare-for-upgrade) und [zur Nachbearbeitung](#recommended-task-sequence-steps-for-post-processing).



## <a name="configure-pre-cache-content"></a>Konfigurieren des zwischengespeicherten Inhalts
Clients können mithilfe des Features zum Vorabzwischenspeichern für verfügbare Bereitstellungen von Tasksequenzen relevante Betriebssystem-Upgradepakete herunterladen, bevor der Benutzer die Tasksequenz installiert.
> [!TIP]  
> Dieses Feature wurde erstmals in Version 1702 als [Vorabfeature](/sccm/core/servers/manage/pre-release-features) eingeführt. Ab Version 1706 können ist diese Funktion kein vorab veröffentlichtes Feature mehr.

Beispiel: Alle Benutzer sollen über eine einzige direkte Upgradetasksequenz verfügen, und es stehen viele verschiedene Architekturen und Sprachen zur Verfügung. In Vorgängerversionen startet der Download von Inhalten, wenn der Benutzer eine bereitgestellte Tasksequenz im Softwarecenter herunterlädt. Durch diese Verzögerung verzögert sich auch der Installationsstart. Alle Inhalte, auf die in der Tasksequenz verwiesen wird, werden heruntergeladen. Dieser Inhalt schließt das Ugradepaket für das Betriebssystem für alle Sprachen und Architekturen mit ein. Wenn jedes Upgradepaket in etwa eine Größe von 3 GB hat, ist der Gesamtinhalt sehr groß.

Mit dem Vorabzwischenspeichern von Inhalten können Sie den Client dahingehend einschränken, dass er nur das zutreffende Betriebssystem-Upgradepaket und alle anderen referenzierten Inhalte herunterladen darf, wenn er die Bereitstellung empfängt. Wenn der Benutzer dann im Softwarecenter auf **Installieren** klickt, steht der Inhalt bereit, und die Installation startet sofort, da der Inhalt bereits auf der lokalen Festplatte gespeichert ist.

 > [!NOTE]
 > Dieses Verhalten gilt derzeit nur für das Betriebssystem-Upgradepaket. Das Paket ist der Inhalt, für den Sie die entsprechende Architektur oder Sprache angeben. Wenn die Tasksequenz z.B. auch auf mehrere Treiberpakete verweist, lädt der Client sie derzeit alle herunter. Die Tasksequenz-Engine wertet die Bedingungen für die Schritte aus, während die Tasksequenz ausgeführt wird, nicht im Voraus. Der Client verwendet die Tags in den Paketeigenschaften, um zu bestimmen, welche Inhalte vorab zwischengespeichert werden sollen.

### <a name="to-configure-the-pre-cache-feature"></a>So konfigurieren Sie die Zwischenspeicherungsfunktion

1. Erstellen Sie Betriebssystem-Upgradepakete für bestimmte Architekturen und Sprachen. Geben Sie die Architektur und die Sprache auf der Registerkarte **Datenquelle** des Pakets an. Verwenden Sie für die Sprache die Konvertierung in das Dezimalsystem. 1033 ist beispielsweise der Dezimalwert für Englisch, 0x0409 seine hexadezimale Entsprechung.

    Der Client wertet die Architektur- und Sprachwerte aus, um zu bestimmen, welches Betriebssystem-Upgradepaket während dem Vorabzwischenspeichern heruntergeladen werden soll.

1. Erstellen Sie eine Tasksequenz mit bedingten Schritten für die verschiedenen Sprachen und Architekturen. Beispielsweise wird im folgenden Schritt die englische Version verwendet:

    ![Der Tasksequenz-Editor zeigt mehrere Upgrade OS-Schritte für ENU, DEU und JPN](../media/precacheproperties2.png)

    ![Tasksequenz-Editor, Registerkarte „Optionen“, Anzeige der WMI WQL-Abfrage für „Locale“ und „OSArchitecture“](../media/precacheoptions2.png)  

3. Bereitstellen der Tasksequenz Konfigurieren Sie für die Zwischenspeicherungsfunktion die folgenden Einstellungen:
    - Wählen Sie auf der Registerkarte **Allgemein** die Option **Inhalt für diese Tasksequenz vorab herunterladen** aus.
    - Konfigurieren Sie auf der Registerkarte **Bereitstellungseinstellungen** die Tasksequenz mit der Einstellung **Verfügbar** für **Zweck**.
    - Wählen Sie auf der Registerkarte **Zeitplanung** für die Einstellung **Verfügbarkeitsdatum der Bereitstellung festlegen** die derzeit ausgewählte Zeit aus. Der Client beginnt mit dem Zwischenspeichern des Inhalts zur verfügbaren Zeit der Bereitstellung. Wenn ein Zielclient diese Richtlinie empfängt, liegt der verfügbare Zeitpunkt in der Vergangenheit. Das bedeutet, dass der Download des Zwischenspeichers direkt startet. Wenn der Client diese Richtlinie empfängt, aber der verfügbare Zeitpunkt in der Zukunft liegt, beginnt der Client erst mit dem Zwischenspeichern des Inhalts, wenn dieser Zeitpunkt erreicht wurde. 
    - Konfigurieren Sie auf der Registerkarte **Verteilungspunkte** die Einstellungen der **Bereitstellungsoptionen**. Wenn der Inhalt nicht vorab zwischengespeichert wird, bevor ein Benutzer die Installation startet, verwendet der Client diese Einstellungen.
  

### <a name="user-experience"></a>Benutzerfreundlichkeit
- Wenn der Client die Bereitstellungsrichtlinie empfängt, startet er nach Ablauf des verfügbaren Zeitpunkts der Bereitstellung mit dem Vorabzwischenspeichern des Inhalts. Dieser Inhalt umfasst alle referenzierten Pakete, jedoch nur das Betriebssystem-Upgradepaket, das den Architektur- und Sprachattributen für das Paket entspricht.
- Wenn der Client die Bereitstellung für Benutzer verfügbar macht, wird eine Benachrichtigung angezeigt, um Benutzer über die neue Bereitstellung zu informieren. Die Tasksequenz ist jetzt im Softwarecenter sichtbar. Der Benutzer kann zum Softwarecenter navigieren und auf **Installieren** klicken, um die Installation zu starten.
- Wenn der Inhalt nicht vollständig zwischengespeichert wurde und der Benutzer die Tasksequenz installiert, verwendet der Client die Einstellungen, die Sie in der Registerkarte **Bereitstellungsoption** der Bereitstellung angegeben haben. 



## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Empfohlene Tasksequenzschritte zur Vorbereitung von Upgrades

Ab Version 1802 enthält die Standardvorlage der Tasksequenz für das direkte Windows 10-Upgrade zusätzliche Gruppen mit empfohlenen Aktionen, die vor dem Upgradevorgang hinzugefügt werden können. Diese Aktionen in der Gruppe **Vorbereitung auf das Upgrade	** werden häufig von Kunden eingesetzt, die erfolgreiche Upgrades ihrer Geräte auf Windows 10 durchführen. Fügen Sie diese Aktionen für Standorte mit früheren Versionen als 1802 manuell der Tasksequenz in der Gruppe **Vorbereitung auf das Upgrade** hinzu.
- **Akkuprüfung**: Fügen Sie in dieser Gruppe Schritte hinzu, mit denen überprüft wird, ob ein Computer mit einem Akku betrieben wird oder an das Stromnetz angeschlossen ist. Für diese Aktion ist ein benutzerdefiniertes Skript oder ein Hilfsprogramm erforderlich, um diese Prüfung auszuführen.
- **Überprüfung der Netzwerkverbindung**: Fügen Sie in dieser Gruppe Schritte hinzu, mit denen sichergestellt wird, dass der Computer mit einem Netzwerk verbunden ist und keine drahtlose Verbindung verwendet. Für diese Aktion ist ein benutzerdefiniertes Skript oder ein Hilfsprogramm erforderlich, um diese Prüfung auszuführen.
- **Inkompatible Anwendung entfernen**: Fügen Sie in dieser Gruppe Schritte hinzu, mit denen alle Anwendungen entfernt werden, die mit dieser Version von Windows 10 nicht kompatibel sind. Die Methoden zum Deinstallieren einer Anwendung variieren. Wenn die Anwendung den Windows Installer verwendet, kopieren Sie die Befehlszeile **Programm deinstallieren** von der Registerkarte **Programme** in den Eigenschaften des Windows Installer-Bereitstellungstyps der Anwendung. Fügen Sie dann in diese Gruppe mit der Befehlszeile zum Deinstallieren des Programms einen Schritt **Befehlszeile ausführen** ein. Zum Beispiel: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Inkompatible Treiber entfernen**: Fügen Sie in dieser Gruppe Schritte hinzu, mit denen alle Treiber entfernt werden, die mit dieser Version von Windows 10 nicht kompatibel sind.
- **Sicherheitsfunktionen von Drittanbietern entfernen/anhalten**: Fügen Sie in dieser Gruppe Schritte hinzu, mit denen Sicherheitsprogramme von Drittanbietern – z.B. Antivirenprogramme – entfernt oder angehalten werden.
   - Wenn Sie ein Drittanbieterprogramm zur Datenträgerverschlüsselung verwenden, geben Sie den Verschlüsselungstreiber in Windows Setup mit der [Befehlszeilenoption](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers** an. Fügen Sie der Tasksequenz in dieser Gruppe einen Schritt [Tasksequenzvariable festlegen](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) hinzu. Legen Sie die Tasksequenzvariable auf **OSDSetupAdditionalUpgradeOptions** fest. Legen Sie den Wert auf **/ReflectDriver** mit dem Pfad zum Treiber fest. Die [Tasksequenz-Aktionsvariable](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) fügt die von der Tasksequenz verwendete Windows Setup-Befehlszeile an. Wenden Sie sich an den Anbieter Ihrer Software, um weitere Informationen zu diesem Vorgang zu erhalten.

### <a name="download-package-content-task-sequence-step"></a>Paketinhalt herunterladen – Tasksequenzschritt  
 Der Schritt [Paketinhalt herunterladen](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) kann in den folgenden Szenarios vor dem Schritt **Betriebssystem aktualisieren** ausgeführt werden:  

-   Sie verwenden eine einzelne Upgradetasksequenz, die sowohl für x86- als auch für x64-Plattformen verwendet werden kann. Fügen Sie der Gruppe **Vorbereitung auf das Upgrade** zwei **Paketinhalt herunterladen**-Schritte hinzu. Legen Sie für jeden Schritt Bedingungen fest, um die Clientarchitektur zu ermitteln. Diese Bedingung hat zur Folge, dass in diesem Schritt nur das passende Upgradepaket für das Betriebssystem heruntergeladen wird. Konfigurieren Sie jeden **Paketinhalt herunterladen** -Schritt zur Verwendung derselben Variablen, und verwenden Sie die Variable für den Medienpfad im Schritt **Betriebssystem aktualisieren** .  

-   Um dynamisch ein passendes Treiberpaket herunterzuladen, verwenden Sie zwei **Paketinhalt herunterladen** -Schritte mit Bedingungen zum Ermitteln des geeigneten Hardwaretyps für jedes Treiberpaket. Konfigurieren Sie jeden **Paketinhalt herunterladen**-Schritt, sodass dieselbe Variable verwendet wird. Verwenden Sie anschließend diese Variable für den Wert **Bereitgestellter Inhalt** im Abschnitt „Treiber“ des Schritts **Betriebssystem aktualisieren**.  

   > [!NOTE]
   > Wenn es mehrere Pakete gibt, fügt Configuration Manager dem Variablennamen ein numerisches Suffix hinzu. Wenn Sie z.B. eine Variable von %mycontent% als benutzerdefinierte Variable festlegen, speichert der Client an diesem Speicherort sämtlichen Inhalt, auf den verwiesen wird. Wenn Sie in einem späteren Schritt auf die Variable verweisen, z.B. **Betriebssystem aktualisieren**, verwenden Sie die Variable mit einem numerischen Suffix. In diesem Beispiel wird %mycontent01% oder %mycontent02% verwendet, wobei die Nummer der Reihenfolge entspricht, in der diese Inhalte im Schritt **Vorbereitung auf das Upgrade** aufgelistet sind.



## <a name="recommended-task-sequence-steps-for-post-processing"></a>Empfohlene Tasksequenzschritte für die Nachbearbeitung   
 Nachdem Sie die Tasksequenz erstellt haben, fügen Sie diese zusätzlichen Schritte in der Gruppe **Nachbearbeitung** der Tasksequenz hinzu.  

> [!NOTE]  
>  Diese Tasksequenz ist nicht linear. Es gibt Bedingungen für die einzelnen Schritte, die sich auf die Ergebnisse der Tasksequenz auswirken können. Dieses Verhalten hängt davon ab, ob das Upgrade des Clientcomputers erfolgreich verläuft oder ob ein Rollback auf das ursprüngliche Betriebssystem ausgeführt werden muss.  

Ab Version 1802 enthält die Standardvorlage der Tasksequenz für das direkte Windows 10-Upgrade zusätzliche Gruppen mit empfohlenen Aktionen, die nach dem Upgradevorgang hinzugefügt werden können. Diese Aktionen in der Gruppe **Nachbearbeitung** werden häufig von Kunden eingesetzt, die erfolgreiche Upgrades ihrer Geräte auf Windows 10 durchführen. Fügen Sie diese Aktionen für Standorte mit früheren Versionen als 1802 manuell der Tasksequenz in der Gruppe **Nachbearbeitung** hinzu.
- **Setupbasierte Treiber anwenden**: Fügen Sie in dieser Gruppe Schritte hinzu, mit denen setupbasierte Treiber (EXE-Dateien) aus Paketen installiert werden.
- **Sicherheitsfunktionen von Drittanbietern installieren/aktivieren**: Fügen Sie in dieser Gruppe Schritte hinzu, mit denen Sicherheitsprogramme von Drittanbietern – z.B. Antivirenprogramme – installiert oder aktiviert werden. 
- **Windows-Standard-Apps und -Zuordnungen festlegen**: Fügen Sie in dieser Gruppe Schritte hinzu, mit denen standardmäßige Windows-Apps und -Dateizuordnungen festgelegt werden. Bereiten Sie zuerst einen Referenzcomputer mit den gewünschten App-Zuordnungen vor. Führen Sie dann die folgende Befehlszeile für den Export aus: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Fügen Sie die XML-Datei zu einem Paket hinzu. Fügen Sie dann in dieser Gruppe einen Schritt [Befehlszeile ausführen](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) hinzu. Geben Sie das Paket, das die XML-Datei enthält, sowie die folgende Befehlszeile an: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Weitere Informationen finden Sie unter [Exportieren oder Importieren von standardmäßigen Anwendungszuordnungen](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Anpassungen und Personalisierung anwenden**: Fügen Sie in dieser Gruppe Schritte hinzu, mit denen Anpassungen des Startmenüs angewendet werden, z.B. zum Organisieren von Programmgruppen. Weitere Informationen finden Sie unter [Anpassen des Startbildschirms](/windows-hardware/manufacture/desktop/customize-the-start-screen).



## <a name="optional-task-sequence-steps-for-rollback"></a>Optionale Tasksequenzschritte für ein Rollback  
 Wenn nach dem Neustart des Computers ein Fehler beim Upgradevorgang auftreten sollte, führt Windows Setup ein Rollback für das Upgrade auf das vorherige Betriebssystem aus. Die Tasksequenz fährt dann mit einem beliebigen Schritt in der **Rollback**-Gruppe fort. Nach dem Erstellen der Tasksequenz können Sie optionale Schritte zur Rollbackgruppe hinzufügen. Sie können z.B. alle Änderungen am System in der Gruppe „Prepare for Upgrade“ rückgängig machen, z.B. nicht kompatible Software deinstallieren.



## <a name="additional-recommendations"></a>Weitere Empfehlungen
- Lesen Sie die Windows-Dokumentation zum [Beheben von Windows 10-Upgradefehlern](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Dieser Artikel enthält auch detaillierte Informationen zum Upgradeprozess.
- Aktivieren Sie im Standardschritt **Bereitschaft überprüfen** die Option **Mindestens erforderlicher freier Speicherplatz (MB)**. Legen Sie den Wert für das Upgrade eines 32-Bit-Betriebssystems auf mindestens **16384** (16 GB) fest. Für ein 64-Bit-System beträgt der Wert **20480** (20 GB). 
- Verwenden Sie die [integrierte Tasksequenzvariable](/sccm/osd/understand/task-sequence-built-in-variables) **SMSTSDownloadRetryCount**, um erneut zu versuchen, die Richtlinie herunterzuladen. Derzeit ist die Variable standardmäßig auf „2“ festgelegt, der Client unternimmt also zwei Wiederholungsversuche. Wenn Ihre Clients keine kabelgebundene Verbindung zum Unternehmensnetzwerk verwenden, können weitere Wiederholungen dabei helfen, dass der Client die Richtlinie abrufen kann. Die Verwendung dieser Variablen hat keine negativen Auswirkungen, außer dass ein verzögerter Fehler auftritt, wenn die Richtlinie nicht heruntergeladen werden kann.<!-- 501016 --> Erhöhen Sie auch die Variable **SMSTSDownloadRetryDelay** vom Standardwert „15 Sekunden“.
- Führen Sie eine Inline-Kompatibilitätsbewertung durch. 
   - Fügen Sie an einem frühen Punkt in der Gruppe **Für Aktualisierung vorbereiten** einen zweiten Schritt **Betriebssystem aktualisieren** hinzu. Nennen Sie den Schritt *Upgradebewertung*. Geben Sie das gleiche Upgradepaket an, und aktivieren Sie die Option **Kompatibilitätsprüfung für Windows Setup ausführen, ohne Upgrade zu starten**. Aktivieren Sie **Bei Fehler fortsetzen** auf der Registerkarte „Optionen“. 
   - Fügen Sie unmittelbar nach dem Schritt *Upgradebewertung* einen Schritt **Befehlszeile ausführen** hinzu. Geben Sie die folgende Befehlszeile an:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Fügen Sie auf der Registerkarte **Optionen** die folgende Bedingung hinzu: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Dieser Rückgabecode ist die dezimale Entsprechung von MOSETUP_E_COMPAT_SCANONLY (0xC1900210), einer erfolgreichen Kompatibilitätsüberprüfung ohne Fehler. Wenn der Schritt *Upgradebewertung* erfolgreich ausgeführt wurde und diesen Code zurückgibt, wird dieser Schritt übersprungen. Wenn der Bewertungsschritt einen anderen Rückgabecode zurückgibt, führt dieser Schritt in der Tasksequenz mit dem Rückgabecode aus der Windows Setup-Kompatibilitätsüberprüfung zu einem Fehler.
   - Weitere Informationen finden Sie unter [Betriebssystem aktualisieren](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).
- Wenn Sie das Gerät während dieser Tasksequenz von BIOS zu UEFI konvertieren möchten, finden Sie weitere Informationen unter [Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).
