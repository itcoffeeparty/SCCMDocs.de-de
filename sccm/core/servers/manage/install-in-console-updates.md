---
title: Konsoleninterne Updates
titleSuffix: Configuration Manager
description: Installieren von Configuration Manager-Updates über die Microsoft-Cloud
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: 36
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5d364e35c8777c782499da978f0d1a31694278cc
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Installieren konsoleninterner Updates für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Configuration Manager ruft Updates durch die Synchronisierung mit dem Microsoft-Clouddienst ab. Danach können Sie Updates aus der Configuration Manager-Konsole installieren.

## <a name="get-available-updates"></a>Abrufen aller verfügbaren Updates
Nur Updates, die für Ihre Infrastruktur und Version relevant sind, werden heruntergeladen und Ihrer Hierarchie zur Verfügung gestellt. Diese Synchronisierung kann automatisch oder manuell erfolgen, je nachdem, wie Sie den Dienstverbindungspunkt für Ihre Hierarchie konfigurieren:

-   Im **Onlinemodus**stellt der Dienstverbindungspunkt automatisch eine Verbindung mit dem Microsoft-Clouddienst her und lädt relevante Updates herunter.  

     Configuration Manager sucht standardmäßig alle 24 Stunden nach neuen Updates. Sie können auch sofort nach Updates suchen, indem Sie in der Configuration Manager-Konsole im Knoten **Verwaltung** > **Updates und Wartung** die Option **Auf Updates prüfen** auswählen. 

-   Im **Offlinemodus** stellt der Dienstverbindungspunkt keine Verbindung mit dem Microsoft-Clouddienst her. Verwenden Sie zum Herunterladen und anschließenden Importieren verfügbarer Updates [das Dienstverbindungstool](../../../core/servers/manage/use-the-service-connection-tool.md).  

> [!NOTE]  
>   Sie können Out-of-band-Fixes in Ihre Konsole importieren. Verwenden Sie hierzu das [Tool zur Updateregistrierung](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Diese Out-of-band-Fixes ergänzen die Updates, die Sie beim Synchronisieren mit dem Microsoft-Clouddienst erhalten.


Nach der Synchronisierung der Updates können Sie sie in der Configuration Manager-Konsole anzeigen, indem Sie zum Knoten **Verwaltung** > **Updates und Wartung** navigieren:  

-   Nicht installierte Updates werden als **Verfügbar**angezeigt.

-   Installierte Updates werden als **Installiert**angezeigt. Nur die aktuellsten Updates werden angezeigt. Um sich bereits installierte Updates anzeigen zu lassen, wählen Sie die Schaltfläche **Verlauf** im Menüband aus.



Bevor Sie den Dienstverbindungspunkt konfigurieren, sollten Sie die zusätzlichen Anwendungsbereiche verstehen und entsprechend planen. Folgende Verwendungen können Auswirkungen auf Ihre Konfiguration dieser Standortsystemrolle haben:  

-   Der Dienstverbindungspunkt wird verwendet, um Nutzungsinformationen zu Ihrem Standort hochzuladen. Diese Informationen helfen dem Microsoft-Clouddienst bei der Identifizierung von Updates, die für die aktuelle Version Ihrer Infrastruktur verfügbar sind. Weitere Informationen finden Sie unter [Diagnose- und Nutzungsdaten](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   Der Dienstverbindungspunkt wird verwendet, um Geräte mithilfe von Microsoft Intune und der lokalen Verwaltung mobiler Geräte (Mobile Device Management; MDM) in Configuration Manager zu verwalten. Weitere Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

Wenn Sie sich ausführlicher über die Vorgänge bei einem Update informieren möchten, können Sie sich Folgendes anschauen:  

-   [Flussdiagramm – Herunterladen von Updates für System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Flowchart - Update replication for System Center Configuration Manager (Flussdiagramm: Updatereplikation für System Center Configuration Manager)](../../../core/servers/manage/update-replication-flowchart.md)  



## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Zuweisen von Berechtigungen zum Anzeigen und Verwalten von Updates und Funktionen
Um Updates in der Konsole anzuzeigen, muss einem Benutzer eine rollenbasierte Administratorsicherheitsrolle zugewiesen sein, die die Sicherheitsklasse **Updatepakete** enthält. Diese Klasse gewährt Zugriff auf das Anzeigen und Verwalten von Updates in der Configuration Manager-Konsole.    

#### <a name="about-the-update-packages-class"></a>Die Updatepakete-Klasse   
In der Standardeinstellung ist die Klasse **Updatepakete** (SMS_CM_Updatepackages) Teil der folgenden integrierten Sicherheitsrollen mit den aufgeführten Berechtigungen:
 -  **Hauptadministrator** mit den Berechtigungen **Ändern** und **Lesen** .
    -   Ein Benutzer mit dieser Sicherheitsrolle und Zugriff auf den Sicherheitsbereich **Alle** kann Updates anzeigen und installieren. Der Benutzer kann auch während der Installation Funktionen aktivieren, und er kann einzelne Funktionen aktivieren, nachdem das Update installiert wurde.
    - Ein Benutzer mit dieser Sicherheitsrolle und Zugriff auf den Sicherheitsbereich **Standard** kann Updates anzeigen und installieren. Der Benutzer kann auch während der Installation Funktionen aktivieren, und er kann Funktionen anzeigen, nachdem ein Update installiert wurde. Dieser Benutzer kann jedoch keine Funktionen nach Abschluss des Updates aktivieren.

- **Analyst mit Leseberechtigung** mit der Berechtigung **Lesen** :
  -  Ein Benutzer mit dieser Sicherheitsrolle und Zugriff auf den **Standard**bereich kann sich Updates anzeigen lassen, diese aber nicht installieren. Dieser Benutzer kann sich ebenfalls Funktionen nach Abschluss eines Updates anzeigen lassen, diese jedoch nicht aktivieren.

#### <a name="permissions-required-for-updates-and-servicing"></a>Erforderliche Berechtigungen für Updates und Wartung   
  - Verwenden Sie ein Konto, das einer Sicherheitsrolle zugewiesen ist, die über die Klasse **Updatepakete** mit den Berechtigungen **Ändern** und **Lesen** verfügt.
  - Das Konto muss dem Bereich **Standard** zugewiesen sein.

#### <a name="permissions-to-only-view-updates"></a>Berechtigungen, mit denen sich Updates ausschließlich anzeigen lassen   
  - Verwenden Sie ein Konto, das einer Sicherheitsrolle zugewiesen ist, die über die Klasse **Updatepakete** mit ausschließlich der Berechtigung **Lesen** verfügt.
  - Das Konto muss dem Bereich **Standard** zugewiesen sein.

#### <a name="permissions-required-to-enable-features-after-updates-are-installed"></a>Erforderliche Berechtigungen zum Aktivieren dieser Features nach der Installation von Updates   
  -  Verwenden Sie ein Konto, das einer Sicherheitsrolle zugewiesen ist, die über die Klasse **Updatepakete** mit den Berechtigungen **Ändern** und **Lesen** verfügt.
  -  Das Konto muss dem Bereich **Alle** zugewiesen sein.



##  <a name="bkmk_beforeinstall"></a> Vor der Installation eines konsoleninternen Updates  
 Sehen Sie sich die folgenden Schritte an, bevor Sie ein Update in der Configuration Manager-Konsole installieren.  

###  <a name="bkmk_step1"></a> Schritt 1: Überprüfen der Updatecheckliste  
Überprüfen Sie die zutreffende Updatecheckliste mit vor dem Update durchzuführenden Schritten:

- [Prüfliste für die Installation von Update 1706](../../../core/servers/manage/checklist-for-installing-update-1706.md)  

- [Prüfliste für die Installation von Update 1710](../../../core/servers/manage/checklist-for-installing-update-1710.md)  

- [Prüfliste für die Installation von Update 1802](../../../core/servers/manage/checklist-for-installing-update-1802.md)


###  <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a>Schritt 2: Ausführen der Voraussetzungsprüfung vor der Installation eines Updates  
Bevor Sie ein Update installieren, sollten Sie die Voraussetzungsprüfung für das Update ausführen. Wenn Sie vor der Installation eines Updates die Voraussetzungsprüfung ausführen, geschieht Folgendes:  

-   Die Updatedateien werden an andere Standorte repliziert, bevor das Update installiert wird.  

-   Die Voraussetzungsprüfung wird automatisch erneut ausgeführt, wenn Sie sich für die Installation des Updates entscheiden.  

> [!NOTE]   
> Wenn Sie eine Voraussetzungsprüfung starten und dann den Status anzeigen, wird die Phase **Installation** als aktiv angezeigt. Das Update wird jedoch tatsächlich nicht installiert. Um die Voraussetzungsprüfung auszuführen, extrahiert der Updatevorgang das Paket aus der Inhaltsbibliothek und schreibt es in einen Stagingordner, in dem auf die aktuellen Voraussetzungsprüfungen zugegriffen werden kann. Der gleiche Vorgang wird ausgeführt, wenn Sie ein Update installieren. Aus diesem Grund wird für die Installation der Status „In Bearbeitung“ angezeigt. Nur der Schritt *Updatepaket extrahieren* wird in der Kategorie „Installation“ angezeigt.  

Wenn Sie später das Update installieren, können Sie das Update so konfigurieren, das Warnungen der Voraussetzungsprüfung ignoriert werden.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>So führen Sie vor der Installation eines Updates die Voraussetzungsprüfung aus  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Updates und Wartung**.   

2.  Klicken Sie mit der rechten Maustaste auf das Updatepaket, für das die Voraussetzungsprüfung ausgeführt werden soll.  

3.  Wählen Sie **Voraussetzungsprüfung ausführen**aus.  

     Beim Ausführen der Voraussetzungsprüfung wird der Inhalt für das Update auf untergeordnete Standorte repliziert. Sie können die Datei distmgr.log auf dem Standortserver anzeigen, um sicherzustellen, dass der Inhalt erfolgreich repliziert wird.  

4.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Update- und Wartungsstatus**, und suchen Sie nach dem Voraussetzungsstatus, um die Ergebnisse der Überprüfung anzuzeigen. Sie können auch die Datei „ConfigMgrPrereq.log“ auf dem Standortserver anzeigen, um weitere Details zu erhalten.  



##  <a name="bkmk_install"></a> Installieren konsoleninterner Updates  
 Wenn Sie zur Installation von Updates in der Configuration Manager-Konsole bereit sind, beginnen Sie mit dem Standort der obersten Ebene der Hierarchie. Dieser Standort ist entweder der Standort der zentralen Verwaltung oder ein eigenständiger primärer Standort.  

 Es wird empfohlen, die Installation des Updates für jeden Standort außerhalb der normalen Geschäftszeiten durchzuführen, um die Auswirkungen auf den Geschäftsbetrieb zu minimieren. Der Grund hierfür ist, dass die Updateinstallation Aktionen wie das Neuinstallieren von Standortkomponenten und Standortsystemrollen umfassen kann.  

-   An untergeordneten primären Standorten wird das Update automatisch gestartet, sobald die Installation des Updates am Standort der zentralen Verwaltung abgeschlossen ist. Hierbei handelt es sich um den empfohlenen Standardprozess. Mithilfe von [Dienstfenstern für Standortserver](/sccm/core/servers/manage/service-windows) können Sie jedoch steuern, wann Updates an einem primären Standort installiert werden.  

-   Aktualisieren Sie sekundäre Standorte über die Configuration Manager-Konsole manuell, nachdem das Update des primären, übergeordneten Standorts abgeschlossen wurde. Die automatische Aktualisierung sekundärer Standortserver wird nicht unterstützt.  

-   Wenn Sie nach dem Standortupdate eine Configuration Manager-Konsole verwenden, werden Sie aufgefordert, die Konsole zu aktualisieren.  

-  Nachdem der Standortserver die Installation eines Updates erfolgreich abschließt, werden automatisch alle relevanten Standortsystemrollen aktualisiert. Die einzige Einschränkung gilt für Verteilungspunkte. Beim Installieren eines Updates werden nicht alle Verteilungspunkte erneut installiert und gehen offline, um gleichzeitig aktualisiert zu werden. Stattdessen verwendet der Standortserver die Einstellungen des Standorts zur Inhaltsverteilung, um das Update nacheinander auf eine Teilmenge von Verteilungspunkten zu verteilen. Das bedeutet, dass nur manche Verteilungspunkte offline geschaltet werden, um das Update zu installieren. Verteilungspunkte, die noch nicht aktualisiert wurden oder bei denen das Update schon abgeschlossen ist, bleiben online und können Clients Inhalte bereitstellen.


###  <a name="bkmk_overview"></a> Übersicht über die konsoleninterne Updateinstallation  
#### <a name="1-when-the-update-installation-starts"></a>1. Zu Beginn der Updateinstallation  
Der Updates-Assistent zeigt eine Liste der vom Update betroffenen Produktbereiche an.  

-   Auf der Seite **Allgemein** des Assistenten können Sie **Voraussetzungswarnungen**konfigurieren.  
    -   Bei Voraussetzungsfehlern wird Updateinstallation immer beendet. Beheben Sie die Fehler, bevor die Installation des Updates erfolgreich wiederholt werden kann. Weitere Informationen finden Sie unter [Wiederholen der Installation eines fehlerhaften Updates](#bkmk_retry).  

    -   Bei Voraussetzungswarnungen kann die Updateinstallation ebenfalls beendet werden. Beheben Sie die Warnungen, bevor Sie die Installation des Updates wiederholen. Weitere Informationen finden Sie unter [Wiederholen der Installation eines fehlerhaften Updates](#bkmk_retry).  
    -   **Ignore any prerequisite check warnings and install this update regardless of missing requirements** (Alle Warnungen der Voraussetzungsprüfung ignorieren und das Update unabhängig von fehlenden Voraussetzungen installieren): Eine Bedingung für die Updateinstallation wird festgelegt, durch die Voraussetzungswarnungen ignoriert werden. Mit dieser Option kann die Installation des Updates fortgesetzt werden. Wenn Sie diese Option nicht auswählen, wird die Updateinstallation beendet, wenn eine Warnung auftritt. Von der Verwendung dieser Option wird abgeraten, wenn Sie vorher keine Voraussetzungsprüfung durchgeführt und Voraussetzungswarnungen für einen Standort nicht behoben haben.  

      In den Arbeitsbereichen **Verwaltung** und **Überwachung** enthält der Knoten Updates und Wartung eine Schaltfläche auf dem Menüband **Warnungen der erforderlichen Komponente ignorieren**. Diese Schaltfläche wird verfügbar, wenn ein Updatepaket die Installation aufgrund von Warnungen der Voraussetzungsprüfung nicht erfolgreich abschließen kann. Beispiel: Sie installieren ein Update, ohne die Option zum Ignorieren von Voraussetzungswarnungen (im Update-Assistenten) zu verwenden. Die Updateinstallation wird mit einem Status beendet, dass Voraussetzungswarnungen vorliegen, jedoch keine Fehler. Sie können später im Menüband **Warnungen zu erforderlichen Komponenten ignorieren** auswählen, um eine automatische Fortsetzung dieser Updateinstallation auszulösen, die dann Voraussetzungswarnungen ignoriert. Wenn Sie diese Option verwenden, wird die Installation der Updates automatisch nach einigen Minuten fortgesetzt.



-   Wenn ein Update für den Configuration Manager-Client relevant ist, wird Ihnen die Option angeboten, das Clientupdate mit einer begrenzten Clientanzahl zu testen. Weitere Informationen finden Sie unter [Testen von Clientupgrades in einer Präproduktionssammlung](../../../core/clients/manage/upgrade/test-client-upgrades.md).  


#### <a name="2-during-the-update-installation"></a>2. Während der Updateinstallation  
Im Rahmen der Updateinstallation führt Configuration Manager folgende Aktionen aus:  

-   Neuinstallation aller betroffenen Komponenten wie der Standortsystemrollen oder der Configuration Manager-Konsole.  

-   Updates für Clients werden auf der Grundlage Ihrer Auswahl für Pilottests für Clients und für [automatische Clientupgrades](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade) verwaltet.  

-   Standortsystemserver werden im Zuge des Updates nicht neu gestartet (es sei denn, .NET wird als Teil einer Voraussetzung für die Standortsystemrollen installiert).  

> [!TIP]  
>  Bei der Installation von Updates aktualisiert Configuration Manager auch den Ordner „CD.Latest“. Dieser Ordner wird bei der Standortwiederherstellung verwendet.  


#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Überwachen des Status von Updates während der Installation  
Gehen Sie folgendermaßen vor, um den Fortschritt zu überwachen:  

-   In der Configuration Manager-Konsole: Der Knoten **Verwaltung** > **Updates und Wartung**. Dieser Knoten zeigt den Installationsstatus aller Updatepakete an.


-   Navigieren Sie in der Configuration Manager-Konsole zum Knoten **Überwachung** > **Übersicht** > **Update- und Wartungsstatus**. Dieser Knoten zeigt nur den Installationsstatus des Updatepakets, das gerade installiert wird.  

    Die Updatepaketinstallation zur Erleichterung der Überwachung ist in folgende Phasen aufgeteilt. Für jede Phase sind jetzt zusätzliche Details verfügbar, einschließlich der für weitere Informationen anzeigbaren Protokolldateien:  
    -   **Herunterladen** (Diese Phase gilt nur für den Standort der obersten Ebene, auf dem der Dienstverbindungspunkt-Standort installiert ist.)   

    -   **Replikation**   

    -   **Prüfung der erforderlichen Komponenten**   

    -   **Installation**    

    -   **Nach der Installation**: Weitere Informationen finden Sie unter [Tasks nach der Installation](#post-installation-tasks).  

-   Sie können die Datei **CMUpdate.log** unter **&lt;ConfigMgr_Installationsverzeichnis>\Protokolle** anzeigen.  


#### <a name="4-when-the-update-installation-completes"></a>4. Zum Abschluss der Updateinstallation  
Nach dem Abschluss der Installation des ersten Standortupdates:  

-   An untergeordneten primären Standorten wird das Update automatisch installiert. Es ist keine weitere Aktion erforderlich.  

-   Sekundäre Standorte müssen manuell in der Configuration Manager-Konsole aktualisiert werden.
> [!TIP]
> Obwohl die Version eines sekundären Standorts nicht in der Konsole angezeigt wird, können Sie die Standortversion mit dem Configuration Manager SDK ermitteln. Informationen hierzu finden Sie unter [SMS_Site Server WMI Class (SMS_Site Server WMI-Klasse)](/sccm/develop/reference/core/servers/configure/sms_site-server-wmi-class).


-   Bis für alle Standorte in der Hierarchie das Update auf die neue Version durchgeführt wurde, erfolgt der Betrieb der Hierarchie im gemischten Versionsmodus. Weitere Informationen finden Sie unter [Interoperabilität zwischen verschiedenen Versionen von Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


#### <a name="5-update-configuration-manager-consoles"></a>5. Aktualisieren von Configuration Manager-Konsolen  
Nach dem Update eines Standorts der zentralen Verwaltung oder eines primären Standorts muss jede Configuration Manager-Konsole, die mit diesem Standort eine Verbindung herstellt, ebenfalls aktualisiert werden. In folgenden Fällen werden Sie zum Aktualisieren einer Konsole aufgefordert:  

-   Sie öffnen die Konsole.

-   Sie navigieren in einer geöffneten Konsole zu einem neuen Knoten.

Es wird empfohlen, das Update sofort und ohne Verzögerung zu installieren.  

Nach Abschluss des Konsolenupdates können Sie überprüfen, ob die Version von Konsole und Standort korrekt ist. Gehen Sie oben links in der Konsole zu **Info zu System Center Configuration Manager**.  


###  <a name="bkmk_toptier"></a> So starten Sie die Updateinstallation am Standort der obersten Ebene  
Wechseln Sie am Standort der obersten Ebene Ihrer Hierarchie in der Configuration Manager-Konsole zu **Verwaltung** > **Updates und Wartung**, wählen Sie ein Update mit dem Status **Verfügbar** aus, und klicken Sie anschließend auf **Updatepaket installieren**.  


###  <a name="bkmk_secondary"></a> So starten Sie die Updateinstallation an einem sekundären Standort  
Nachdem der übergeordnete primäre Standort eines sekundären Standorts aktualisiert wurde, können Sie den sekundären Standort über die Configuration Manager-Konsole aktualisieren. Verwenden Sie dafür den **Assistenten für das Update von sekundären Standorten**.  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, wählen Sie den zu aktualisierenden Standort aus, und klicken Sie auf der Registerkarte „Start“ in der Gruppe **Standort** auf **Upgrade**.  

2.  Klicken Sie auf **Ja** , um das Update des sekundären Standorts zu starten.  

Um die Updateinstallation an einem sekundären Standort zu überwachen, wählen Sie den sekundären Server aus. Wählen Sie danach auf der Registerkarte **Startseite** in der Gruppe **Standort** **Installationsstatus anzeigen** aus. Sie können der Konsolenanzeige auch die Spalte **Version** hinzufügen, sodass Sie die Version jedes sekundären Standorts anzeigen können.  

Wenn der Status in der Konsole nicht aktualisiert wird oder darauf hinweist, dass beim Update ein Fehler aufgetreten ist, können Sie nach dem erfolgreichen Update eines sekundären Standorts die Option **Installation noch mal versuchen** verwenden. Diese Option installiert das Update für einen sekundären Standort, an dem das Update erfolgreich installiert wurde, nicht erneut, zwingt jedoch die Konsole dazu, den Status zu aktualisieren.


### <a name="post-installation-tasks"></a>Tasks nach der Installation
Wenn ein Standort ein Update installiert, gibt es mehrere Tasks, die erst gestartet werden können, nachdem die Installation des Updates auf dem Standortserver abgeschlossen wurde. Die folgende Liste enthält Tasks nach der Installation, die für Standort- und Hierarchievorgänge von entscheidender Bedeutung sind. Da sie von entscheidender Bedeutung sind, werden sie aktiv überwacht. Zu den zusätzlichen Tasks, die nicht direkt überwacht werden, gehört die erneute Installation von Standortsystemrollen. Wählen Sie zum Anzeigen des Status von kritischen Tasks nach der Installation den Task **Nach der Installation** während der Überwachung der Updateinstallation für einen Standort aus.

Nicht alle Tasks werden sofort abgeschlossen. Einige Tasks werden erst gestartet, wenn für jeden Standort die Installation des Updates abgeschlossen ist. Aus diesem Grund kann sich die Bereitstellung der erwarteten neuen Funktionen verzögern, bis diese Tasks abgeschlossen sind. Da neue Features erst aktiviert werden, wenn für alle Standorte die Updateinstallation abgeschlossen ist, werden neue Features möglicherweise einige Zeit nicht angezeigt.

Tasks nach der Installation:

-   **Der SMS_EXECUTIVE-Dienst wird installiert**
  -   Kritischer Dienst, der auf dem Standortserver ausgeführt wird.
  -   Die Neuinstallation dieses Diensts sollte schnell abgeschlossen werden.


-   **Die SMS_DATABASE_NOTIFICATION_MONITOR-Komponente wird installiert**
  -   Kritischer Standortkomponententhread des SMS_EXECUTIVE-Diensts.
  -   Die Neuinstallation dieses Diensts sollte schnell abgeschlossen werden.


-   **Die SMS_HIERARCHY_MANAGER-Komponente wird installiert**
  -   Kritische Standortkomponente, die auf dem Standortserver ausgeführt wird.
  -   Verantwortlich für die erneute Installation von Standortsystemrollen auf Servern des Standortsystems. Der Status für die Neuinstallation einzelner Standortsystemrollen wird nicht angezeigt.
  -   Die Neuinstallation dieses Diensts sollte schnell abgeschlossen werden.


-   **Die SMS_REPLICATION_CONFIGURATION_MONITOR-Komponente wird installiert**
  -   Kritische Standortkomponente, die auf dem Standortserver ausgeführt wird.
  -   Die Neuinstallation dieses Diensts sollte schnell abgeschlossen werden.


-   **Die SMS_POLICY_PROVIDER-Komponente wird installiert**
  -   Kritische Standortkomponente, die nur in primären Standorten ausgeführt wird.
  -   Die Neuinstallation dieses Diensts sollte schnell abgeschlossen werden.


-   **Replikationsinitialisierung wird überwacht**   
  -   Dieser Task wird nur am Standort der zentralen Verwaltung und an untergeordneten primären Standorten angezeigt.
  -   Hängt von SMS_REPLICATION_CONFIGURATION_MONITOR ab.
  -   Sollte schnell abgeschlossen sein.


-   **Das Configuration Manager-Clientpaket für die Präproduktion wird aktualisiert**    
  -   Dieser Task wird selbst dann angezeigt, wenn die Verwendung von Clientpaketen für die Präproduktion (sogenannte Clientpilottests) nicht aktiviert ist.
  -   Wird erst gestartet, wenn für alle Standorte in der Hierarchie die Installation des Updates abgeschlossen ist.


-   **Der Clientordner auf dem Standortserver wird aktualisiert**
  -   Dieser Task wird nicht angezeigt, wenn Sie den Client in der Präproduktion verwenden.  
  -   Sollte schnell abgeschlossen sein.


-   **Das Configuration Manager-Clientpaket wird aktualisiert**
  -   Dieser Task wird nicht angezeigt, wenn Sie den Client in der Präproduktion verwenden.  
  -   Wird erst beendet, wenn für alle Standorte das Update installiert wurde.  


-   **Features werden aktiviert**
  -   Dieser Task wird nur am Standort der obersten Ebene in der Hierarchie angezeigt.
  -   Wird erst gestartet, wenn für alle Standorte in der Hierarchie die Installation des Updates abgeschlossen ist.
  -   Einzelne Features werden nicht angezeigt.



##  <a name="bkmk_retry"></a> Wiederholen der Installation eines fehlerhaften Updates  
Wenn ein Update nicht installiert werden kann, überprüfen Sie das Feedback in der Konsole, um Lösungen für Warnungen und Fehler zu finden. Sie können auch die Datei „ConfigMgrPrereq.log“ auf dem Standortserver anzeigen, um weitere Details zu erhalten. Bevor Sie die Installation eines Updates wiederholen, müssen Sie die Fehler und sollten Sie die Warnungen beheben.  

> [!TIP]  
> Wenn beim Herunterladen oder Replizieren eines Updates Probleme auftreten, können Sie das [Tool für das Zurücksetzen von Updates](/sccm/core/servers/manage/update-reset-tool) verwenden. 

Wenn Sie die Installation eines Updates wiederholen möchten, wählen Sie das fehlerhafte Update aus, und wählen Sie anschließend eine zutreffende Option aus. Das Verhalten der Wiederholung der Updateinstallation hängt vom Knoten ab, von dem aus Sie die Wiederholung starten und von der Wiederholungsoption, die Sie verwenden.  

#### <a name="retry-installation-for-the-hierarchy"></a>Wiederholen der Installation für die Hierarchie
Sie können die Installation eines Updates für die gesamte Hierarchie wiederholen, wenn sich das Update in einem der folgenden Zustände befindet:  

  -   Voraussetzungsprüfung mit mindestens einer Warnung bestanden, und die Option zum Ignorieren von Voraussetzungswarnungen wurde im Update-Assistenten nicht festgelegt. (Der Updatewert für **Voraussetzungswarnung ignorieren** im Knoten **Updates und Wartung** ist auf **Nein** festgelegt.)   
  -   Fehler bei der Voraussetzung.    
  -   Fehler bei der Installation.
  -   Fehler bei der Replikation des Inhalts auf den Standort.   

Wechseln Sie zu **Verwaltung** > **Updates und Wartung**, wählen Sie das Update aus, und wählen Sie anschließend eine der folgenden Optionen aus:  

  -   **Wiederholen**: Wenn Sie **Wiederholen** von diesem Knoten ausführen, startet die Installation des Updates erneut und ignoriert automatisch Voraussetzungswarnungen. Auch Inhalt für das Update wird erneut repliziert, wenn die Replikation zuvor fehlgeschlagen ist.
  - **Warnungen zu erforderlichen Komponenten ignorieren:** Wenn die Installation des Updates aufgrund einer Warnung angehalten wird, können Sie auf **Warnungen zu erforderlichen Komponenten ignorieren** klicken. Dadurch kann die Installation des Updates (nach wenigen Minuten) fortgesetzt werden, und die Option zum Ignorieren von Voraussetzungswarnungen wird angewendet.   

#### <a name="retry-installation-for-the-site"></a>Wiederholen der Installation für den Standort  
 Sie können die Installation eines Updates an einem bestimmten Standort wiederholen, wenn sich das Update in einem der folgenden Zustände befindet:  

  -   Voraussetzungsprüfung mit mindestens einer Warnung bestanden, und die Option zum Ignorieren von Warnungen der Voraussetzungsprüfung wurde im Update-Assistenten nicht festgelegt. (Der Updatewert für **Voraussetzungswarnung ignorieren** im Knoten „Updates und Wartung“ ist auf **Nein** festgelegt.)  
  -   Fehler bei der Voraussetzung.    
  -   Fehler bei der Installation.    

Wechseln Sie zu **Überwachung** > **Übersicht** > **Wartungsstatus des Standorts**, wählen Sie das Update aus, und klicken Sie anschließend auf eine der folgenden Optionen:

  - **Wiederholen:** Wenn Sie **Wiederholen** von diesem Knoten ausführen, starten Sie die Installation des Updates nur an diesem Standort erneut. Im Gegensatz zur Ausführung von **Wiederholen** vom Knoten **Updates und Wartung** ignoriert diese Wiederholung Voraussetzungswarnungen nicht.
  - **Warnungen zu erforderlichen Komponenten ignorieren:** Wenn die Installation des Updates aufgrund einer Warnung angehalten wird, können Sie auf **Warnungen zu erforderlichen Komponenten ignorieren** klicken. Dadurch kann die Installation des Updates (nach wenigen Minuten) fortgesetzt werden, und die Option zum Ignorieren von Voraussetzungswarnungen wird angewendet.



##  <a name="bkmk_after"></a> Nach der Installation eines Updates an einem Standort  
Verwenden Sie die folgende Checkliste, um allgemeine Aufgaben und Konfigurationen durchzuführen, die nach dem Aktualisieren eines Standorts vorgenommen werden.   

**Bestätigen, dass die Standort-zu-Standort-Replikation aktiv ist:** Wechseln Sie in der Configuration Manager-Konsole zu den folgenden Orten, um den Status anzuzeigen und sicherzustellen, dass die Replikation aktiv ist:  

-   **Überwachung** > **Übersicht** > **Standorthierarchie**  

-   **Überwachung** > **Übersicht** > **Datenbankreplikation**  

Weitere Informationen finden Sie unter [Überwachen der Hierarchie- und Replikationsinfrastruktur](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) und [Informationen zur Replikationslinkanalyse](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Bestätigen, dass Standortserver und Remote-Standortsystemserver neu gestartet wurden (falls erforderlich):** Überprüfen Sie Ihre Standortinfrastruktur, und stellen Sie sicher, dass die relevanten Standortserver und Standortsystemserver erfolgreich neu gestartet wurden. In der Regel werden Standortserver nur neu gestartet, wenn Configuration Manager .NET als Voraussetzung für eine Standortsystemrolle installiert.  

 **Aktualisieren eigenständiger Configuration Manager-Konsolen:** Stellen Sie sicher, dass alle Configuration Manager-Remotekonsolen auf die gleiche Version aktualisiert werden. In folgenden Fällen werden Sie zum Aktualisieren der Konsole aufgefordert:  

-   Wenn Sie in der Konsole zu einem neuen Knoten navigieren.  

-   Sie öffnen die Konsole.

**Neukonfigurieren von Datenbankreplikaten für Verwaltungspunkte an primären Standorten:** Wenn Sie Datenbankreplikate für Verwaltungspunkte an primären Standorten verwenden, müssen Sie die Datenbankreplikate deinstallieren, bevor Sie den Standort aktualisieren. Konfigurieren Sie das Datenbankreplikat für Verwaltungspunkte nach dem Update eines primären Standorts neu. Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Neukonfigurieren von Datenbankwartungstasks, die Sie vor dem Update deaktiviert haben:** Wenn Sie die [Datenbankwartungstasks](../../../core/servers/manage/maintenance-tasks.md) vor der Installation des Updates an einem Standort deaktiviert haben, konfigurieren Sie diese Tasks an dem Standort neu. Verwenden Sie dazu die Einstellungen, die schon vor dem Update verwendet wurden.  

**Upgrade für Clients durchführen:** Weitere Informationen finden Sie unter [How to upgrade clients for Windows computers (Upgraden von Clients für Windows-Computer)](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Zusätzliche Konfigurationen:** Überprüfen Sie die Änderungen, die Sie vor Beginn des Updates vorgenommen haben, und stellen Sie diese Konfigurationen für Ihre Standorte und Hierarchie wieder her.  



##  <a name="bkmk_options"></a> Aktivieren optionaler Features von Updates  
Wenn ein Update ein oder mehrere optionale Features enthält, haben Sie die Möglichkeit, diese Features in Ihrer Hierarchie zu aktivieren. Sie können Features zum Zeitpunkt der Updateinstallation aktivieren, oder Sie können zu einem späteren Zeitpunkt zur Konsole zurückkehren, um die optionalen Features zu aktivieren.

Wechseln Sie in der Konsole zu **Verwaltung** > **Updates und Wartung** > **Features**, um verfügbare Funktionen und deren Status anzuzeigen.

Wenn ein Feature nicht optional ist, wird es automatisch installiert und nicht im Knoten **Features** aufgeführt.  


Wenn Sie ein neues Features oder ein Feature der Vorabversion aktivieren, muss der Hierarchie-Manager von Configuration Manager (HMAN) die Änderung verarbeiten, bevor Sie das Feature nutzen können. Das Verarbeiten der Änderung wird oftmals direkt abgeschlossen; es kann aber bis zu 30 Minuten in Anspruch nehmen, abhängig vom Verarbeitungszyklus des HMAN. Nachdem die Änderung verarbeitet wurde, müssen Sie Ihre Konsole neu starten, bevor die zu diesem Feature gehörige UI angezeigt wird.



##  <a name="bkmk_prerelease"></a> Verwenden von vorab veröffentlichten Features von Updates
Features des Vorabrelease sind in Current Branch enthalten, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen. Sie können diese Features in Ihrer Produktionsumgebung verwenden, aber sie gelten als nicht bereit für die Produktion. Erfahren Sie mehr über [Features der Vorabversion](/sccm/core/servers/manage/pre-release-features), z.B. wie Sie sie in Ihrer Umgebung aktivieren.             



## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

###  <a name="bkmk_faq"></a> Warum werden bestimmte Updates nicht in der Konsole angezeigt?  
 Wenn Sie nach einer erfolgreichen Synchronisierung mit dem Microsoft-Clouddienst ein bestimmtes Update in der Konsole nicht finden, kann dieses Verhalten folgende Ursachen haben:  

-   Für das Update ist eine Konfiguration erforderlich, die von Ihrer Infrastruktur nicht verwendet wird, oder eine Voraussetzung für den Empfang des Updates wird von der aktuellen Produktversion nicht erfüllt.  

     Wenn Sie Ihrer Meinung nach über alle erforderlichen Konfigurationen und Voraussetzungen für ein fehlendes Update verfügen, überprüfen Sie, ob sich Ihr Dienstverbindungspunkt im Onlinemodus befindet. Verwenden Sie anschließend unter dem Knoten **Updates und Wartung** die Option **Suchen nach Updates**, um die Prüfung zu erzwingen. Wenn Sie sich im Offlinemodus befinden, müssen Sie das Dienstverbindungstool verwenden, um eine manuelle Synchronisierung mit dem Clouddienst auszuführen.  

-   Ihr Konto verfügt nicht über die richtigen rollenbasierten Administratorberechtigungen zum Anzeigen von Updates in der Configuration Manager-Konsole.

    Unter [Berechtigungen zum Verwalten von Updates](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) in diesem Thema finden Sie Informationen zu erforderlichen Berechtigungen zum Anzeigen von Updates und Aktivieren von Features in der Konsole.

