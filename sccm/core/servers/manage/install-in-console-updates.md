---
title: Konsoleninterne Updates | System Center Configuration Manager
description: "System Center Configuration Manager wird mit dem Microsoft-Clouddienst synchronisiert, um Updates abzurufen, die in der Konsole installieren werden können."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: b9721737b4181d8f5e41224c3e2c32ae41647554


---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Installieren konsoleninterner Updates für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager wird mit dem Microsoft-Clouddienst synchronisiert, um Updates abzurufen, die in der Configuration Manager-Konsole installieren werden können.

## <a name="get-available-updates"></a>Abrufen aller verfügbaren Updates
Nur Updates, die für Ihre Infrastruktur und Version relevant sind, werden heruntergeladen und Ihrer Hierarchie zur Verfügung gestellt. Diese Synchronisierung kann automatisch oder manuell erfolgen, je nachdem, wie Sie den Dienstverbindungspunkt für Ihre Hierarchie konfigurieren:

-   Im **Onlinemodus**stellt der Dienstverbindungspunkt automatisch eine Verbindung mit dem Microsoft-Clouddienst her und lädt relevante Updates herunter.  

     Configuration Manager sucht standardmäßig alle 24 Stunden nach neuen Updates. Ab Version 1602 oder höher können Sie auch sofort nach Updates suchen, indem Sie in der Configuration Manager-Konsole im Knoten **Verwaltung** > **Clouddienste** > **Updates und Wartung** auf die Option **Auf Updates prüfen** klicken.  

-   Im **Offlinemodus** stellt der Dienstverbindungspunkt keine Verbindung mit dem Microsoft-Clouddienst her, und Sie müssen [Verwenden des Dienstverbindungstools für System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md) manuell ausführen, um verfügbare Updates herunterzuladen und anschließend zu importieren.  

> [!NOTE]  
>  Zusätzlich zu den Updates, die Sie bei der Synchronisierung mit dem Microsoft Clouddienst erhalten, werden auch Out-of-band-Korrekturen in Ihre Konsole importiert, wo Sie sie für die Installation auswählen können. Diese werden über das [Update-Registrierungstool](http://technet.microsoft.com/library/mt691544.aspx) installiert.  

Nach der Synchronisierung der Updates können Sie sie in der Configuration Manager-Konsole anzeigen, indem Sie zum Knoten **Verwaltung** > **Clouddienste** > **Updates und Wartung** wechseln:  

-   Nicht installierte Updates werden als **Verfügbar**angezeigt.

-   Installierte Updates werden als **Installiert**angezeigt.  Ab Version 1606 wird nur das neueste installierte Update angezeigt, und Sie können auf dem Menüband auf die Schaltfläche **Verlauf** klicken, um die vorher installierten Updates anzuzeigen.



Bevor Sie den Dienstverbindungspunkt konfigurieren, sollten Sie die zusätzlichen Anwendungsbereiche verstehen und planen, da dies Auswirkungen auf die Konfiguration dieser Standortsystemrolle haben kann:  

-   Der Dienstverbindungspunkt wird verwendet, um Nutzungsinformationen zu Ihrem Standort hochzuladen. Diese Informationen helfen dem Microsoft-Clouddienst bei der Identifizierung von Updates, die für die aktuelle Version Ihrer Infrastruktur verfügbar sind. Weitere Informationen finden Sie unter [Diagnose- und Nutzungsdaten für System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   Der Dienstverbindungspunkt wird verwendet, um Geräte mithilfe von Microsoft Intune und der lokalen Verwaltung mobiler Geräte (Mobile Device Management; MDM) in Configuration Manager zu verwalten. Weitere Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md).  

Informationen zum besseren Verständnis darüber, was passiert, wenn Updates heruntergeladen werden, finden Sie unter:  

-   [Flussdiagramm: Herunterladen von Updates für System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md).  

-   [Flowchart - Update replication for System Center Configuration Manager (Flussdiagramm: Updatereplikation für System Center Configuration Manager)](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="permissions-to-view-and-manage-updates-and-features"></a>Berechtigungen zum Anzeigen und Verwalten von Updates und Funktionen
Vor der Installation von Update 1606 musste ein Benutzer einer Sicherheitsrolle, die die Berechtigung **Lesen** in der Berechtigungsgruppe **Standort**umfasst, sowie dem Sicherheitsbereich **Alle**zugewiesen werden, um Updates in der Konsole anzeigen zu können. Ab dem Update 1606 wird eine neue rollenbasierte Verwaltungssicherheitsklasse namens **Updatepakete** eingeführt, die Zugriff auf die Ansicht und Verwaltung von Updates in der Configuration Manager-Konsole erteilt.    

**Über die Updatepakete-Klasse:**  
In der Standardeinstellung ist die Klasse **Updatepakete** (SMS_CM_Updatepackages) Teil der folgenden integrierten Sicherheitsrolle mit den erforderlichen Berechtigungen:
 -  **Hauptadministrator** mit den Berechtigungen **Ändern** und **Lesen** .
    -   Ein Benutzer mit dieser Sicherheitsrolle und Zugriff auf den Sicherheitsbereich **Alle** kann Updates anzeigen, Updates installieren und Funktionen während der Installation aktivieren sowie einzelne Funktionen aktivieren, nachdem das Update bereits installiert wurde.
    - Ein Benutzer mit dieser Sicherheitsrolle und Zugriff auf den Sicherheitsbereich **Standard** kann sich Updates anzeigen lassen, Updates installieren und währenddessen Features aktivieren. Zusätzlich kann er sich nach der Updateinstallation Features anzeigen lassen. Eine nachträgliche Aktivierung von Features ist jedoch nicht möglich.

- **Analyst mit Leseberechtigung** mit der Berechtigung **Lesen** :
  -  Ein Benutzer mit dieser Sicherheitsrolle und Zugriff auf den Bereich **Standard** kann Updates anzeigen, aber nicht installieren, und kann Funktionen anzeigen, nachdem ein Update installiert wurde, kann diese jedoch nicht selbst aktivieren.

**Übersicht über die erforderlichen Berechtigungen für Updates und Wartung:**   
  - Verwenden Sie ein Konto, das einer Sicherheitsrolle zugewiesen ist, die über die Klasse **Updatepakete** mit den Berechtigungen **Ändern** und **Lesen** verfügt.
  - Das Konto muss dem Bereich **Standard** zugewiesen sein.

**Nur Aktualisierungen anzeigen**:
  - Verwenden Sie ein Konto, das einer Sicherheitsrolle zugewiesen ist, die über die Klasse **Updatepakete** mit ausschließlich der Berechtigung **Lesen** verfügt.
  - Das Konto muss dem Bereich **Standard** zugewiesen sein.

**So aktivieren Sie Funktionen nach der Installation von Updates:**
  -   Verwenden Sie ein Konto, das einer Sicherheitsrolle zugewiesen ist, die über die Klasse **Updatepakete** mit den Berechtigungen **Ändern** und **Lesen** verfügt.
  -  Das Konto muss dem Bereich **Alle** zugewiesen sein.






##  <a name="a-namebkmkbeforeinstalla-before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Vor der Installation eines konsoleninternen Updates  
 Sehen Sie sich die folgenden Schritte an, bevor Sie Updates in der Configuration Manager-Konsole installieren:  

###  <a name="a-namebkmkstep1a-step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> Schritt 1: Überprüfen der Updatecheckliste  
Bevor Sie ein neues Update in der Configuration Manager-Konsole installieren, prüfen Sie die relevante Updatecheckliste auf Aktionen, die vor dem Starten des Updates durchgeführt werden müssen:  

-   Upgrade auf 1511 von [Upgrade to System Center Configuration Manager](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Upgrade auf System Center Configuration Manager).    

-   Update auf 1602 von 1511: Informationen finden Sie unter [Checklist for installing update 1602 for System Center Configuration Manager](../../../core/servers/manage/checklist-for-installing-update-1602.md) (Checkliste für die Installation von Update 1602 für System Center Configuration Manager).

- Update auf 1606 von 1511 oder 1602: Informationen finden Sie unter [Checklist for installing update 1606 for System Center Configuration Manager](../../../core/servers/manage/checklist-for-installing-update-1606.md) (Checkliste für die Installation von Update 1606 für System Center Configuration Manager).  


###  <a name="a-namebkmkstep2a-step-2-test-the-database-upgrade-before-installing-an-update"></a><a name="bkmk_step2"></a> Schritt 2: Testen des Datenbankupgrades vor der Installation eines Updates  
Vor der Installation eines neuen Updates in Ihrer Hierarchie, beispielsweise 1602, sollten Sie das Upgrade der Standortdatenbank testen. Der Name der Befehlszeilenoption, mit der Sie die Installation eines Updates an einer Sicherungskopie Ihrer Standortdatenbank testen, lautet **testdbupgrade**.  

Im Gegensatz zu früheren Versionen von Configuration Manager müssen Sie hier keine Standortwiederherstellung durchführen, wenn bei einem Update ein Fehler auftritt, sondern können stattdessen die Updateinstallation wiederholen. Auch wenn das Testupgrade der Datenbank weniger kritisch ist als in früheren Produktversionen, wird dieser Schritt daher nach wie vor empfohlen.  

##### <a name="to-run-testdbupgrade-before-installing-an-update"></a>So führen Sie vor dem Installieren eines Updates „testdbupgrade“ aus  

1.  Rufen Sie einen Satz von Quelldateien aus dem Ordner **CD.Latest** eines Standorts ab, an dem die Version ausgeführt wird, auf die Sie aktualisieren möchten. Dazu müssen Sie möglicherweise zuerst einen Standort in einer Labor- oder Testumgebung installieren, an dem diese Version von System Center Configuration Manager ausgeführt wird.  

     Der Ordner **CD.Latest** für einen Standort enthält die Quelldateien für diese Version. Sie müssen diese Quelldateien verwenden, um das Testupgrade für Ihre Standortdatenbank auszuführen. Weitere Informationen zu diesen Dateien finden Sie unter [Der Ordner „CD.Latest“ für System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md).  

     Wenn an Ihrem Standort beispielsweise Version 1501 ausgeführt wird und Sie auf 1602 aktualisieren möchten, müssen Sie einen Ordner „CD.Latest“ von einem Standort abrufen, der bereits auf Version 1602 aktualisiert wurde. Normalerweise können Sie einen neuen und temporären Standort in einer Laborumgebung installieren und ein Upgrade auf Version 1602 durchführen, um den Ordner „CD.Latest“ mit den erforderlichen Dateien zu erstellen.  

2.  Kopieren Sie den Ordner „CD.Latest“ in einen Speicherort auf dem SQL Server-Computer, den Sie zum Ausführen des Testupgrades für die Datenbank verwenden möchten. (Informationen hierzu finden Sie im nächsten Schritt.)  

3.  Erstellen Sie eine Sicherungskopie der Standortdatenbank, für die Sie das Testupgrade durchführen möchten, und stellen Sie eine Kopie dieser Datenbank auf einer Instanz von SQL Server wieder her, in der kein Configuration Manager-Standort gehostet wird. Die SQL Server-Instanz muss derselben Edition von SQL Server entsprechen wie die Standortdatenbank.  

4.  Führen Sie nach der Wiederherstellung der Datenbankkopie die Datei **Setup** in dem Ordner „CD.Latest“ aus, den Sie aus Ihrer Labor- oder Testumgebung kopiert haben. Verwenden Sie beim Ausführen von Setup die Befehlszeilenoption **/TESTDBUPGRADE** . Handelt es sich bei der SQL Server-Instanz, von der die Datenbankkopie gehostet wird, nicht um die Standardinstanz, müssen Sie auch die Befehlszeilenargumente angeben. Damit können Sie ermitteln, von welcher Instanz die Kopie der Standortdatenbank gehostet wird.  

     Angenommen, Sie planen das Upgrade einer Standortdatenbank namens „SMS_ABC“. Sie stellen eine Kopie dieser Standortdatenbank auf einer unterstützten Instanz von SQL Server wieder her, die Sie „DBTest“ genannt haben. Verwenden Sie folgende Befehlszeile, um ein Upgrade dieser Kopie der Standortdatenbank zu testen: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Die Datei „Setup.exe“ befindet sich auf dem Quellmedium für System Center Configuration Manager an folgendem Speicherort: **SMSSETUP\BIN\X64**.  

5.  Überprüfen Sie den Fortschritt und den Erfolg des Upgrades in der Instanz von SQL Server, in der Sie den Test ausführen. Die nötigen Angaben dazu finden Sie in der Datei „ConfigMgrSetup.log“ im Stammverzeichnis des Systemlaufwerks:  

     Wenn beim Testen des Upgrades Fehler auftreten, beheben Sie die Probleme, die mit dem Upgrade der Standortdatenbank in Verbindung stehen. Erstellen Sie eine neue Sicherung der Standortdatenbank, und testen Sie anschließend das Upgrade der neuen Kopie der Standortdatenbank.  

     Wenn der Prozess erfolgreich abgeschlossen ist, können Sie die Datenbankkopie löschen.  

    > [!NOTE]  
    >  Es wird nicht unterstützt, die für den Upgradetest verwendete Kopie der Datenbank mit dem Ziel der Verwendung als Standortdatenbank wiederherzustellen.  

###  <a name="a-namebkmkstep3a-step-3-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step3"></a> Schritt 3: Ausführen der Voraussetzungsprüfung vor der Installation eines Updates  
Bevor Sie ein Update installieren, sollten Sie die Voraussetzungsprüfung für das Update ausführen. Wenn Sie vor der Installation eines Updates die Voraussetzungsprüfung ausführen, geschieht Folgendes:  

-   Die Updatedateien werden an andere Standorte repliziert, bevor das Update tatsächlich installiert wird.  

-   Die Voraussetzungsprüfung wird automatisch erneut ausgeführt, wenn Sie sich für die Installation des Updates entscheiden.  

Wenn Sie später ein Update installieren, können Sie das Update so konfigurieren, das Warnungen der Voraussetzungsprüfung ignoriert werden.  

##### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>So führen Sie vor der Installation eines Updates die Voraussetzungsprüfung aus  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clouddienste** > **Updates und Wartung**.  

2.  Klicken Sie mit der rechten Maustaste auf das Updatepaket, für das die Voraussetzungsprüfung ausgeführt werden soll.  

3.  Wählen Sie **Voraussetzungsprüfung ausführen**aus.  Sie können anzeigen, die  

     Beim Ausführen der Voraussetzungsprüfung wird der Inhalt für das Update auf untergeordnete Standorte repliziert.  Sie können die Datei **distmgr.log** auf dem Standortserver anzeigen, um sicherzustellen, dass der Inhalt erfolgreich repliziert wird.  

4.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Update- und Wartungsstatus**, und suchen Sie nach dem Voraussetzungsstatus, um die Ergebnisse der Überprüfung anzuzeigen. Sie können auch die Datei „ConfigMgrPrereq.log“ auf dem Standortserver anzeigen, um weitere Details zu erhalten.  



##  <a name="a-namebkmkinstalla-install-in-console-updates"></a><a name="bkmk_install"></a> Installieren konsoleninterner Updates  
 Wenn Sie zur Installation von Updates in der Configuration Manager-Konsole bereit sind, beginnen Sie mit dem Standort der obersten Ebene der Hierarchie. Dies ist entweder der Standort der zentralen Verwaltung oder ein eigenständiger primärer Standort.  

 Es wird empfohlen, die Installation des Updates für jeden Standort außerhalb der normalen Geschäftszeiten zu planen, wenn die Installation des Updates und die zugehörigen Aktionen zum Neuinstallieren von Standortkomponenten und Standortsystemrollen die geringsten Auswirkungen auf die Geschäftsvorgänge haben.  

-   An untergeordneten primären Standorten wird das Update automatisch gestartet, sobald die Installation des Updates am Standort der zentralen Verwaltung abgeschlossen ist. Dies ist der standardmäßige und empfohlene Prozess. Mithilfe von [Dienstfenstern für Standortserver](#bkmk_ServiceWindow) können Sie jedoch steuern, wann Updates an einem primären Standort installiert werden.  

-   Sekundäre Standorte müssen Sie von der Configuration Manager-Konsole aus manuell aktualisieren, nachdem das Update des primären, übergeordneten Standorts abgeschlossen wurde. Die automatische Aktualisierung sekundärer Standortserver wird nicht unterstützt.  

-   Wenn Sie nach dem Standortupdate eine Configuration Manager-Konsole verwenden, werden Sie aufgefordert, die Konsole zu aktualisieren.  

-  Nachdem der Standortserver die Installation eines Updates erfolgreich abschließt, werden automatisch alle relevanten Standortsystemrollen aktualisiert.  Nur bei Verteilungspunkten müssen Sie auf Folgendes achten:
  - Aufgrund von Änderungen, die mit Update 1606 eingeführt wurden, werden nicht mehr alle Verteilungspunkte bei der Installation eines Updates an einem Standort mit Version 1606 oder höher offline geschaltet, um gleichzeitig ein Update durchzuführen. Stattdessen verwendet der Standortserver die Einstellungen des Standorts zur Inhaltsverteilung, um das Update nacheinander auf eine Teilmenge von Verteilungspunkten zu verteilen. Das bedeutet, dass nur manche Verteilungspunkte offline geschaltet werden, um das Update zu installieren. Dadurch können Verteilungspunkte, die noch nicht aktualisiert wurden oder bei denen das Update schon abgeschlossen ist, online bleiben und Inhalt an Clients bereitstellen.


###  <a name="a-namebkmkoverviewa-overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Übersicht über die konsoleninterne Updateinstallation  
**1. Zu Beginn der Updateinstallation**  
Der Updates-Assistent zeigt eine Liste der vom Update betroffenen Produktbereiche an.  

-   Auf der Seite **Allgemein** des Assistenten können Sie **Voraussetzungswarnungen**konfigurieren.  
      -   Bei Voraussetzungsfehlern wird Updateinstallation immer beendet. Sie müssen die Fehler beheben, bevor die Installation des Updates erfolgreich wiederholt werden kann. Weitere Informationen finden Sie unter [Wiederholen der Installation eines fehlerhaften Updates](#bkmk_retry) .  

    -   Bei Voraussetzungswarnungen kann die Updateinstallation ebenfalls beendet werden. Sie sollten Warnungen auflösen, bevor Sie die Installation des Updates wiederholen.   Weitere Informationen finden Sie unter [Wiederholen der Installation eines fehlerhaften Updates](#bkmk_retry) .  
    -   Durch Auswahl der Option **Alle Warnungen der Voraussetzungsprüfung ignorieren und das Update unabhängig von fehlenden Voraussetzungen installieren**wird eine Bedingung für die Updateinstallation festgelegt, durch die Voraussetzungswarnungen ignoriert werden und die Updateinstallation fortgesetzt wird. Wenn Sie diese Option nicht auswählen, wird die Updateinstallation beendet, wenn eine Warnung auftritt. Von der Verwendung dieser Option wird abgeraten, wenn Sie nicht vorher die Voraussetzungsprüfung ausgeführt und Voraussetzungswarnungen für einen Standort aufgelöst haben.  

      Ab Version 1606 enthalten sowohl die Arbeitsbereiche **Verwaltung** und **Überwachung** als auch der Knoten „Updates und Wartung“ eine Schaltfläche auf dem Menüband mit der Bezeichnung **Warnungen zu erforderlichen Komponenten ignorieren**. Diese Schaltfläche wird verfügbar, wenn ein Updatepaket die Installation aufgrund von Warnungen der Voraussetzungsüberprüfung nicht erfolgreich abschließen kann.  Wenn Sie z.B. ein Update installieren, ohne die Option „Warnungen zu erforderlichen Komponenten ignorieren“ (innerhalb des Update-Assistenten) zu verwenden und diese Updateinstallation im Status der Voraussetzungswarnung aber ohne Fehler stoppt, können Sie später **Warnungen zu erforderlichen Komponenten ignorieren** aus dem Menüband auswählen, um eine automatische Fortsetzung der Updateinstallation auszulösen, bei der die Voraussetzungswarnungen ignoriert werden.  Wenn diese Option verwendet wird, wird die Installation der Updates automatisch nach einigen Minuten fortgesetzt.



-   Wenn ein Update für den Configuration Manager-Client relevant ist, wird Ihnen die Option angeboten, das Clientupdate mit einer begrenzten Clientanzahl zu testen. Weitere Informationen finden Sie unter [Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Während der Updateinstallation**  
Im Rahmen der Updateinstallation führt Configuration Manager folgende Aktionen aus:  

-   Neuinstallation aller betroffenen Komponenten wie der Standortsystemrollen oder der Configuration Manager-Konsole.  

-   Updates für Clients werden auf der Grundlage Ihrer Auswahl für Clientpilottests und für [automatische Clientupgrades](https://technet.microsoft.com/library/mt627885.aspx)verwaltet.  

-   Ein Neustart von Standortsystemservern ist im Zuge des Updates nicht erforderlich (es sei denn, .NET wird als Teil einer Voraussetzung für die Standortsystemrollen installiert).  

> [!TIP]  
>  Bei der Installation von Updates aktualisiert Configuration Manager auch den Ordner „CD.Latest“, der während der Wiederherstellung eines Standorts verwendet wird.  

**3. Überwachen des Status von Updates während der Installation**  
Gehen Sie folgendermaßen vor, um den Fortschritt zu überwachen:  

-   Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clouddienste** > **Updates und Wartung**. Dieser Knoten zeigt den Installationsstatus aller Updatepakete an.


-   Navigieren Sie in der Configuration Manager-Konsole zum Knoten **Überwachung** > **Übersicht** > **Update- und Wartungsstatus**. Dieser Knoten zeigt nur den Installationsstatus des Updatepakets, das gerade installiert wird.  

    Ab Version 1606 ist die Updatepaketinstallation zur Erleichterung der Überwachung in folgende Phasen aufgeteilt. Für jede Phase sind jetzt zusätzliche Details verfügbar, einschließlich welche Protokolldatei Sie für weitere Informationen anzeigen können:  
    -   **Herunterladen** (Dies gilt nur für den Standort der obersten Ebene, auf dem die Standortsystemrolle des Dienstverbindungspunkts installiert ist)
    -   **Replikation**
    - **Prüfung der erforderlichen Komponenten**
    - **Installation**

-   Sie können die Datei **CMUpdate.log** unter **&lt;Configuration Manager-Installationsverzeichnis>\Logs\\** anzeigen.  

**4. Beim Abschluss der Updateinstallation**  
Nach dem Abschluss der Installation des ersten Standortupdates:  

-   An untergeordneten primären Standorten wird das Update automatisch installiert. Es ist keine weitere Aktion erforderlich.  

-   Sekundäre Standorte müssen manuell in der Configuration Manager-Konsole aktualisiert werden.
> [!TIP]
> Obwohl die Version eines sekundären Standorts nicht in der Konsole angezeigt wird, können Sie die Standortversion mit dem Configuration Manager SDK ermitteln. Informationen hierzu finden Sie unter [SMS_Site Server WMI Class (SMS_Site Server WMI-Klasse)](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx).


-   Bis für alle Standorte in der Hierarchie das Update auf die neue Version durchgeführt wurde, erfolgt der Betrieb der Hierarchie im gemischten Versionsmodus. Weitere Informationen finden Sie unter [Interoperability between different versions of System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Aktualisieren von Configuration Manager-Konsolen**  
Nach dem Update eines Standorts der zentralen Verwaltung oder eines primären Standorts muss jede Configuration Manager-Konsole, die mit diesem Standort eine Verbindung herstellt, ebenfalls aktualisiert werden. In folgenden Fällen werden Sie zum Aktualisieren einer Konsole aufgefordert:  

-   Wenn Sie die Konsole öffnen.  

-   Wenn Sie in einer geöffneten Konsole zu einem neuen Knoten wechseln.  

Es wird empfohlen, das Update sofort und ohne Verzögerung zu installieren.  

Nach Abschluss des Konsolenupdates können Sie überprüfen, ob die Version von Konsole und Standort korrekt ist. Wechseln Sie oben links in der Konsole, wo die neue Version des Standorts und der Konsole angezeigt wird, zu **Info zu System Center Configuration Manager** .  

###  <a name="a-namebkmktoptiera-to-start-the-update-installation-at-the-top-tier-site"></a><a name="bkmk_toptier"></a> So starten Sie die Updateinstallation am Standort der obersten Ebene  
Wechseln Sie am Standort der obersten Ebene Ihrer Hierarchie in der Configuration Manager-Konsole zu **Verwaltung** > **Clouddienste** > **Updates und Wartung**, wählen Sie ein Update mit dem Status **Verfügbar** aus, und klicken Sie anschließend auf **Updatepaket installieren**.  

###  <a name="a-namebkmksecondarya-to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> So starten Sie die Updateinstallation an einem sekundären Standort  
Nachdem der übergeordnete primäre Standort eines sekundären Standorts aktualisiert wurde, können Sie den sekundären Standort von der Configuration Manager-Konsole aus aktualisieren.  Verwenden Sie dafür den **Assistenten für das Update von sekundären Standorten**.  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, wählen Sie den zu aktualisierenden Standort aus, und klicken Sie auf der Registerkarte „Start“ in der Gruppe „Standort“ auf **Upgrade**.  

2.  Klicken Sie auf **Ja** , um das Update des sekundären Standorts zu starten.  

Um die Updateinstallation an einem sekundären Standort zu überwachen, wählen Sie den Server des sekundären Standorts aus, und klicken Sie auf der Registerkarte „Start“ in der Gruppe „Standort“ auf **Installationsstatus anzeigen**. Sie können der Konsolenanzeige auch die Spalte **Version** hinzufügen, sodass Sie die Version jedes sekundären Standorts anzeigen können.  

Wenn der Status in der Konsole nicht aktualisiert wird oder darauf hinweist, dass beim Update ein Fehler aufgetreten ist, können Sie nach dem erfolgreichen Update eines sekundären Standorts, die Option **Installation noch mal versuchen** verwenden. Diese Option installiert das Update für einen sekundären Standort, an dem das Update erfolgreich installiert wurde, nicht erneut, zwingt jedoch die Konsole dazu, den Status zu aktualisieren.


##  <a name="a-namebkmkretrya-retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Wiederholen der Installation eines fehlerhaften Updates  
Wenn ein Update nicht installiert werden kann, überprüfen Sie das Feedback in der Konsole, um Lösungen für Warnungen und Fehler zu finden.  Sie können auch die Datei „ConfigMgrPrereq.log“ auf dem Standortserver anzeigen, um weitere Details zu erhalten. Bevor Sie die Installation eines Updates wiederholen, müssen Sie die Fehler und sollten Sie die Warnungen beheben.  

Wenn Sie die Installation eines Updates wiederholen möchten, wählen Sie das fehlerhafte Update aus, und wählen Sie anschließend eine zutreffende Option aus. Das Verhalten der Wiederholung der Updateinstallation hängt vom Knoten ab, von dem aus Sie die Wiederholung starten und von der Wiederholungsoption, die Sie verwenden.  

1.  **Wiederholen der Installation für die Hierarchie:**  
Sie können die Installation eines Updates für die gesamte Hierarchie wiederholen, wenn sich das Update in einem der folgenden Zustände befindet:  

    -   Voraussetzungsprüfung mit mindestens einer Warnung bestanden, und die Option zum Ignorieren von Voraussetzungswarnungen wurde im Update-Assistenten nicht festgelegt. (Der Updatewert **Voraussetzungswarnung ignorieren** im Knoten „Updates und Wartung“ ist auf **Nein**festgelegt.)   
    -   Fehler bei der Voraussetzung.    
    -   Fehler bei der Installation.
    -   Fehler bei der Replikation des Inhalts auf den Standort.   

    Wechseln Sie zu **Verwaltung** > **Clouddienste** > **Updates und Wartung**, wählen Sie das Update aus, und klicken Sie anschließend auf eine der folgenden Optionen:  

    -   **Wiederholen** – Wenn Sie „Wiederholen“ von diesem Knoten ausführen, startet die Installation des Updates erneut und ignoriert automatisch Voraussetzungswarnungen. Die Installation repliziert erneut den Inhalt für das Update, wenn die Replikation zuvor fehlgeschlagen ist.
    - **Warnungen zu erforderlichen Komponenten ignorieren** – Ab Version 1606 können Sie auf „Warnungen zu erforderlichen Komponenten ignorieren“ klicken, wenn die Installation des Updates aufgrund einer Warnung stoppt. Dadurch kann die Installation des Updates (nach wenigen Minuten) fortgesetzt werden, und die Option zum Ignorieren von Voraussetzungswarnungen wird angewendet.   

2.  **Wiederholen der Installation für den Standort:**  
 Sie können die Installation eines Updates an einem bestimmten Standort wiederholen, wenn sich das Update in einem der folgenden Zustände befindet:  

    -   Voraussetzungsprüfung mit mindestens einer Warnung bestanden, und die Option zum Ignorieren von Voraussetzungswarnungen wurde im Update-Assistenten nicht festgelegt. (Der Updatewert **Voraussetzungswarnung ignorieren** im Knoten „Updates und Wartung“ ist auf **Nein**festgelegt.)  
    -   Fehler bei der Voraussetzung.    
    -   Fehler bei der Installation.    

    Wechseln Sie zu **Überwachung** > **Übersicht** > **Wartungsstatus des Standorts**, wählen Sie das Update, und klicken Sie anschließend auf eine der folgenden Optionen.

       - **Wiederholen** – Wenn Sie „Wiederholen“ von diesem Knoten ausführen, starten Sie die Installation des Updates nur in diesem Standort erneut. Im Gegensatz zur Ausführung von „Wiederholen“ vom Knoten „Updates und Wartung“ ignoriert diese Wiederholung Voraussetzungswarnungen nicht.
       -    **Warnungen zu erforderlichen Komponenten ignorieren** – Ab Version 1606 können Sie auf „Warnungen zu erforderlichen Komponenten ignorieren“ klicken, wenn die Installation des Updates aufgrund einer Warnung stoppt. Dadurch kann die Installation des Updates (nach wenigen Minuten) fortgesetzt werden, und die Option zum Ignorieren von Voraussetzungswarnungen wird angewendet.

##  <a name="a-namebkmkaftera-after-a-site-installs-an-update"></a><a name="bkmk_after"></a> Nach der Installation eines Updates an einem Standort  
Verwenden Sie die folgende Checkliste, um allgemeine Aufgaben und Konfigurationen durchzuführen, die nach dem Aktualisieren eines Standorts vorgenommen werden:  

**Bestätigen, dass die Standort-zu-Standort-Replikation aktiv ist:** Wechseln Sie in der Configuration Manager-Konsole zu den folgenden Orten, um den Status anzuzeigen und sicherzustellen, dass die Replikation aktiv ist:  

-   **Überwachung** > **Übersicht** > **Standorthierarchie**  

-   **Überwachung** > **Übersicht** > **Datenbankreplikation**  

Weitere Informationen finden Sie unter [Überwachen der Hierarchie- und Replikationsinfrastruktur in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) und [Informationen zur Replikationslinkanalyse](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Bestätigen, dass Standortserver und Remote-Standortsystemserver neu gestartet wurden (falls erforderlich):** Überprüfen Sie Ihre Standortinfrastruktur, und stellen Sie sicher, dass die relevanten Standortserver und Standortsystemserver (remote vom Standortserver) erfolgreich neu gestartet wurden.  Dies wird in der Regel nur erwartet, wenn Configuration Manager .NET als Voraussetzung für eine Standortsystemrolle installiert.  

 **Aktualisieren eigenständiger Configuration Manager-Konsolen:** Stellen Sie sicher, dass alle Configuration Manager-Remotekonsolen auf die gleiche Version aktualisiert werden. In folgenden Fällen werden Sie zum Aktualisieren der Konsole aufgefordert:  

-   Wenn Sie in der Konsole zu einem neuen Knoten wechseln.  

-   Wenn Sie die Konsole öffnen.  

**Neukonfigurieren von Datenbankreplikaten für Verwaltungspunkte an primären Standorten:** Wenn Sie Datenbankreplikate für Verwaltungspunkte an primären Standorten verwenden, müssen Sie die Datenbankreplikate deinstallieren, bevor Sie den Standort aktualisieren. Konfigurieren Sie das Datenbankreplikat für Verwaltungspunkte nach dem Update eines primären Standorts neu. Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte für System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Neukonfigurieren von Datenbankwartungstasks, die Sie vor dem Update deaktiviert haben:** Wenn Sie Datenbank-[Wartungstasks für System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) vor dem Update an einem Standort deaktiviert haben, konfigurieren Sie diese Tasks an dem Standort mithilfe derselben Einstellungen neu, die auch vor dem Update verwendet wurden.  

**Upgrade von Clients:** Informationen zum Ausführen eines Upgrades für vorhandene Clients und zum Installieren neuer Clients finden Sie unter [Aktualisieren von Clients für Windows-Computer in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Zusätzliche Konfigurationen:** Überprüfen Sie die Änderungen, die Sie vor Beginn des Updates vorgenommen haben, und stellen Sie diese Konfigurationen für Ihre Standorte und Hierarchie wieder her.  

##  <a name="a-namebkmkoptionsa-enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Aktivieren optionaler Features von Updates  
Wenn Sie ein Update installieren, das ein oder mehrere optionale Features enthält, haben Sie die Möglichkeit, diese Features in Ihrer Hierarchie zu aktivieren.  Dies können Sie zum Zeitpunkt der Updateinstallation durchführen, oder Sie können zu einem späteren Zeitpunkt zur Konsole zurückkehren und die optionalen Features aktivieren.

Wechseln Sie in der Konsole zu **Verwaltung** > **Clouddienste** > **Updates und Wartung** > **Features**, um verfügbare Funktionen und deren Status anzuzeigen.

Wenn ein Feature nicht optional ist, wird es automatisch installiert und nicht im Knoten **Features** aufgeführt.  

##  <a name="a-namebkmkprereleasea-use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Verwenden von vorab veröffentlichten Features von Updates
Ab Version 1606 müssen Sie für die Verwendung von Featurevorabversionen in System Center Configuration Manager Ihre Zustimmung geben, bevor Sie diese auswählen und verwenden können.  

Vorab veröffentlichte Features werden in das Produkt aufgenommen, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen. Sie sollten nicht als für den Produktivbetrieb geeignet betrachtet werden.

Sie geben Ihre Zustimmung, indem Sie in der Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**navigieren, und anschließend **Hierarchieeinstellungen**auswählen. Wählen Sie auf der Registerkarte **Allgemein** **Verwendung von Featurevorabversionen zustimmen**aus.
 -  Die Zustimmung ist eine einmalige Aktion pro Hierarchie, die nicht rückgängig gemacht werden kann.  
 -  Sie können bis zu Ihrer Zustimmung keine Featurevorabversionen aktivieren, die im Update 1606 oder höheren Updateversionen enthalten sind.

 > [!NOTE]
 > Wenn Sie die Featurevorabversionen von Update 1602 vor der Installation von Update 1606 aktiviert haben, bleiben diese Features nach der Installation von Version 1606 für die Verwendung aktiviert,auch wenn Sie keine Zustimmung zur Verwendung von Featurevorabversionen gegeben haben.

Wenn Ihre Hierarchie Version 1606 oder höher ausführt, und Sie ein Update installieren, das Featurevorabversionen enthält, sind diese Features im Assistenten für Updates und Wartung zusammen mit den regulären Funktionen sichtbar, die im Update enthalten sind.
  - **Wenn Sie Ihre Zustimmung gegeben haben:** Sie können Featurevorabversionen innerhalb des Assistenten für Updates und Wartung aktivieren, wenn Sie das Update installieren. Wählen Sie dazu die Featurevorabversionen aus, so wie Sie jede andere Funktion auswählen würden.     

    Optional können Sie die Featurevorabversionen auch später vom **Verwaltung** > **Clouddienste** > **Updates und Wartung** > **Features** -Knoten der Konsole aktivieren. Wählen Sie dazu im Knoten „Features“ das Feature aus, und klicken Sie anschließend auf **Aktivieren**. (Diese Option ist ausgegraut und nicht verfügbar, bis Sie Ihre Zustimmung geben.)  
  -   **Wenn Sie nicht Ihre Zustimmung gegeben haben:** Beim Installieren eines Updates sind Featurevorabversionen im Assistenten für Updates und Wartung sichtbar, sie sind jedoch ausgegraut und können nicht aktiviert werden. Nach der Installation des Updates können Sie diese Features auf dem Knoten „Features“ anzeigen, diese jedoch nicht aktivieren, bis sie Ihre Zustimmung in den Hierarchieeinstellungen gegeben haben.

 > [!TIP]
 > Wenn Sie Update 1606 installieren, sind Featurevorabversionen, die in Update 1606 enthalten sind, nicht im Assistenten für Updates und Wartung sichtbar und können zu diesem Zeitpunkt nicht aktiviert werden. Nach der Installation des Updates 1606 können Sie sich im Knoten „Features“ die noch nicht veröffentlichen Features anzeigen lassen.

Wenn Sie an einem eigenständigen primären Standort Ihre Zustimmung erteilt haben, und die Hierarchie durch die Installation eines neuen Standorts der zentralen Verwaltung erweitern, müssen Sie am Standort zentralen Verwaltung erneut Ihre Zustimmung geben.

**Die folgenden, vorab veröffentlichten Features sind verfügbar:**

 |Komponente                    |Als Vorabversion hinzugefügt |Als vollständiges Feature hinzugefügt |  
|----------------------------|---------------------|------------------------|
| Microsoft OMS-Connector (Operations Management Suite)  | [Version 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Warten einer clusterfähigen Sammlung (Warten einer Servergruppe)| [Version 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#bkmk_servergroups)|![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Bedingter Zugriff für PCs, die von System Center Configuration Manager verwaltet werden | [Version 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     |![Noch nicht](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)                        |




##  <a name="a-namebkmkservicewindowa-service-windows-for-site-servers"></a><a name="bkmk_ServiceWindow"></a> Dienstfenster für Standortserver  
Sie können Dienstfenster auf einem Standortserver konfigurieren, um zu steuern, wann Infrastruktur-Updates für Configuration Manager auf diesem Standortserver angewendet werden können.  Jeder Standortserver unterstützt mehrere Fenster. Dabei wird das zulässige Fenster für die Installation von Infrastruktur-Updates von einer Kombination aller für den jeweiligen Server konfigurierten Fenster bestimmt.  

**So konfigurieren Sie ein Dienstfenster**  

1.  Öffnen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie anschließend den Standort aus, für den Sie ein Dienstfenster konfigurieren möchten.  

2.  Als Nächstes bearbeiten Sie die **Eigenschaften** der Standortserver und wählen die Registerkarte **Dienstfenster** aus, auf der Sie mindestens ein Dienstfenster für den jeweiligen Standortserver festlegen können.  

##  <a name="a-namebkmkfaqa-why-dont-i-see-certain-updates-in-my-console"></a><a name="bkmk_faq"></a> Warum werden bestimmte Updates nicht in der Konsole angezeigt?  
 Wenn Sie nach einer erfolgreichen Synchronisierung mit dem Microsoft-Clouddienst ein bestimmtes Update nicht finden oder gar keine Updates in der Konsole angezeigt werden, kann dies folgende Ursachen haben:  

-   Für das Update ist eine Konfiguration erforderlich, die von Ihrer Infrastruktur nicht verwendet wird, oder eine Voraussetzung für den Empfang des Updates wird von der aktuellen Produktversion nicht erfüllt.  

     Wenn Sie der Ansicht sind, dass die erforderlichen Konfigurationen vorliegen und die anderen Voraussetzungen für ein fehlendes Update erfüllt werden, stellen Sie sicher, dass Ihr Dienstverbindungspunkt sich im Onlinemodus befindet, und verwenden Sie anschließend die Option **Auf Updates prüfen** im Knoten „Updates und Wartung“, um eine Überprüfung zu erzwingen.  Wenn Sie sich im Offlinemodus befinden, müssen Sie das Dienstverbindungstool verwenden, um eine manuelle Synchronisierung mit dem Clouddienst auszuführen.  

-   Ihr Konto verfügt nicht über die richtigen rollenbasierten Administratorberechtigungen zum Anzeigen von Updates in der Configuration Manager-Konsole.

    Unter [Berechtigungen zum Verwalten von Updates](../../../core/servers/manage/install-in-console-updates.md#Permissions-to-view-and-manage-updates-and-features) in diesem Thema finden Sie Informationen zu erforderlichen Berechtigungen zum Anzeigen von Updates und Aktivieren von Features in der Konsole.



<!--HONumber=Nov16_HO1-->


