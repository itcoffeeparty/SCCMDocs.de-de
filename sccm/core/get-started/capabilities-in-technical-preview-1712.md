---
title: Technical Preview 1712 | Microsoft-Dokumentation
titleSuffix: Configuration Manager
description: "Erfahren Sie mehr über die Funktionen, die mit der Technical Preview-Version 1712 für System Center Configuration Manager zur Verfügung stehen."
ms.custom: na
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 85f0b22b3dc067f6f07816ad36d23a090885f355
ms.sourcegitcommit: ed8b2438ef85c9160741ef61f9171be41dd1ae0a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/17/2017
---
# <a name="capabilities-in-technical-preview-1712-for-system-center-configuration-manager"></a>Funktionen in Technical Preview 1712 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*

In diesem Artikel werden die Funktionen vorgestellt, die in Technical Preview Version 1712 für System Center Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. 

Lesen Sie sich die Informationen unter [Technical Preview für System Center Configuration Manager](/sccm/core/get-started/technical-preview) durch, bevor Sie diese Technical Preview-Version installieren. In diesem Artikel erhalten Sie Informationen zu den allgemeinen Anforderungen und Einschränkungen, die für die Verwendung von Technical Preview gelten. Außerdem erfahren Sie, wie Sie Updates zwischen den Versionen ausführen und Feedback zu den Funktionen von Technical Preview bereitstellen.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Bekannte Probleme in dieser Technical Preview:**
-   **Beim Update auf die Vorschauversion tritt ein Fehler auf, wenn Sie einen Standortserver im passiven Modus haben**. Wenn Sie über einen [primären Standortserver im Modus „Passiv“](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability) verfügen, müssen Sie den Standortserver im Modus „Passiv“ deinstallieren, bevor Sie ein Update auf diese neue Preview-Version durchführen. Sie können den Standortserver im passiven Modus erneut installieren, wenn das Update an Ihrem Standort abgeschlossen wurde.

  So deinstallieren Sie den Standortserver im passiven Modus:
  1. Navigieren Sie in der Configuration Manager-Konsole zu **Administration** > **Übersicht** > **Standortkonfiguration** > **Server und Standortsystemrollen**, und wählen Sie den Standortserver im Modus „Passiv“ aus.
  2. Klicken Sie im Bereich **Standortsystemrollen** mit der rechten Maustaste auf die Rolle **Standortserver**, und wählen Sie dann **Rolle entfernen** aus.
  3. Klicken Sie mit der rechten Maustaste auf den Standortserver im passiven Modus, und wählen Sie dann **Löschen**.
  4. Starten Sie nach dem Deinstallieren des Standortservers auf dem aktiven primären Standortserver den Dienst **CONFIGURATION_MANAGER_UPDATE** neu.
<!--sms489412-->


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>Führen Sie kein automatisches Upgrade für abgelöste Anwendungen aus
<!-- 1351266 -->
Basierend auf dem [Feedback von Benutzern](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior) haben Sie mit diesem Release die Möglichkeit, eine Anwendungsbereitstellung so zu konfigurieren, dass sie kein automatisches Upgrade für abgelöste Anwendungen ausführt. Wenn Sie dann die Bereitstellung erstellen, können Sie auf der Seite **Bereitstellungseinstellungen** des **Assistenten zum Bereitstellen von Software** die Option **Automatisch ein Upgrade aller abgelösten Versionen dieser Anwendung ausführen** für **verfügbare** oder **erforderliche** Installationen aktivieren oder deaktivieren.


## <a name="install-multiple-applications-in-software-center"></a>Installieren mehrerer Anwendungen im Softwarecenter
<!-- 1357126 -->
Falls ein Benutzer oder Techniker mehrere Anwendungen auf einem Gerät installieren muss, unterstützt das Softwarecenter jetzt die Installation mehrerer ausgewählter Anwendungen. Dadurch kann der Benutzer effizienter Arbeiten und muss nicht mehr darauf warten, dass eine Installation abgeschlossen wird, bevor er mit der nächsten beginnen kann.

Wenn Sie in der Registerkarte **Anwendungen** den Mehrfachauswahlmodus verwenden, bestimmen die folgenden Faktoren, welche Apps im Softwarecenter für die Mehrfachauswahl freigegeben sind:
 - Die App wird dem Benutzer angezeigt
 - Die App ist noch nicht installiert
 - Es wird keine Genehmigung durch den Administrator verlangt bzw. die Genehmigung wurde bereits erteilt
 - Der App-Status ist verfügbar (d.h. es wird zu diesem Zeitpunkt noch kein Inhalt heruntergeladen)

### <a name="try-it-out"></a>Probieren Sie es aus!
**In der Configuration Manager-Konsole:** Stellen Sie einem Benutzer oder Gerät mehrere Anwendungen entweder als „verfügbar“ oder „erforderlich“ zur Installation bereit, und legen Sie eine Frist für ein Datum in der Zukunft fest. Erfordern Sie keine Genehmigung des Administrators. Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](/sccm/apps/deploy-use/deploy-applications).

**Im Softwarecenter:**
 1. Die Registerkarte **Anwendungen** sollte sich standardmäßig öffnen. 
 2. Klicken Sie auf das Symbol „Neu“, um den Mehrfachauswahlmodus in die Listenansicht einzugeben. ![Mehrfachauswahlsymbol im Softwarecenter](media/software-center-multi-select-apps.png) in der oberen rechten Ecke.
 3. Wählen Sie mindestens zwei Apps aus, die installiert werden müssen, indem Sie das Feld links neben den Apps in der Liste aktivieren.
 4. Klicken Sie auf die Schaltfläche **Install Selected** (Auswahl installieren).

Die Apps werden wie gewöhnlich installiert, allerdings nacheinander.


## <a name="client-based-pxe-responder-service"></a>Clientbasierter PXE-Antwortdienst
<!-- 1357148 -->
Für Kunden ist es häufig schwierig, PXE-Dienste für Remotebüros oder Zweigstellen bereitzustellen, die nur über wenig bzw. gar keine Serverinfrastruktur verfügen. Die Rolle „Verteilungspunkt“ unterstützt Clientbetriebssysteme, ist aber aufgrund der Abhängigkeit von Windows-Bereitstellungsdiensten nicht PXE-fähig.

Es sind jetzt neue Clienteinstellungen verfügbar, um den PXE-Antwortdienst auf den Konfigurations-Manager-Clients zu aktivieren. Ein PXE-fähiges Startimage muss sich im Clientcache des PXE-Antwortdiensts befinden.

### <a name="try-it-out"></a>Probieren Sie es aus!
Vergewissern Sie sich, dass keine PXE-fähigen Verteilungspunkte oder andere PXE-Server in der Testumgebung vorhanden sind, die einen Konflikt mit dem PXE-Clientantwortdienst auslösen können.

In der Configuration Manager-Konsole:
 1. Im Arbeitsbereich **Softwarebibliothek** unter **Betriebssysteme**>**Tasksequenzen**: Erstellen Sie mithilfe der benutzerdefinierten Vorlage eine Tasksequenz.
    1. Klicken Sie erst auf **Hinzufügen**, dann auf **Allgemein**, und wählen Sie anschließen den Schritt **Tasksequenzvariable festlegen** aus. Geben Sie erst **SMSTSPersistContent** als Tasksequenzvariable ein und dann den Wert **TRUE**.
    1. Klicken Sie auf **Hinzufügen**, und wählen Sie erst **Software** und anschließend den Schritt **Paketinhalt herunterladen** aus. Klicken Sie auf das goldene Sternchen, und wählen Sie dann ein PXE-fähiges Startimage aus. Fügen Sie sowohl x86- als auch x64-Startimages ein. Konfigurieren Sie den Schritt, sodass er im **Configuration Manager-Clientcache** gespeichert wird.
    1. Klicken Sie erst auf **Hinzufügen**, dann auf **Allgemein**, und wählen Sie anschließen den Schritt **Tasksequenzvariable festlegen** aus. Geben Sie erst **SMSTSPreserveContent** als Tasksequenzvariable ein und dann den Wert **TRUE**.
 2. Im Arbeitsbereich **Administration** unter **Clienteinstellungen**: Erstellen Sie eine benutzerdefinierte Einstellungsrichtlinie für das Clientgerät.
    1. Wählen Sie die Gruppe **Einstellungen für Clientcache** aus.
  1. Legen Sie die Einstellung **Configuration Manager-Client in vollständigem Betriebssystem zur Freigabe von Inhalten aktivieren** auf **Ja** fest.
    1. Legen Sie die Einstellung **PXE-Antwortdienst aktivieren** auf **Ja** fest.
  1. Klicken Sie in der Einstellung **Erstellen Sie ein selbstsigniertes Zertifikat, oder importieren Sie ein PKI-Clientzertifikat** auf **Zertifikat bereitstellen**. Wenn Ihre Testumgebung über eine Public Key-Infrastruktur verfügt, wählen Sie **Zertifikat importieren** aus. Klicken Sie ansonsten auf **OK**. 
    1. Konfigurieren Sie die restlichen Einstellungen entsprechend Ihrer Testumgebung. (Die Standardeinstellungen sollten ausreichen, solange es keine bestimmten Anforderungen im Hinblick auf das Netzwerk oder die Sicherheit gibt.)
 3. Stellen Sie die Tasksequenz und die benutzerdefinierten Clienteinstellungen für eine Sammlung von Zielclients bereit, die in PXE-Antwortdienste umgewandelt werden sollen. Warten Sie, bis die Richtlinien angewendet werden und die Tasksequenz ausgeführt wird.
 4. Starten Sie einen anderen Client auf demselben Subnetz, um die PXE bzw. das Netzwerk wie gewöhnlich zu starten.

### <a name="known-issues"></a>Bekannte Probleme
 - Im Tasksequenz-Editor wird für den Schritt **Paketinhalt herunterladen** ein Fehlersymbol in rot angezeigt, wenn Sie ein Startimage hinzufügen. Die Tasksequenz wird aber trotzdem erfolgreich gespeichert. Wenn Sie die Tasksequenz erneut im Editor öffnen, wird eine Warnung angezeigt, weil keine Objekte gefunden werden können, auf die verwiesen wird. <!-- sms427542 -->
 - Im Startimage des Schritts „Paketinhalt herunterladen“ wird nicht die benutzerdefinierte Verweisliste der Tasksequenz angezeigt. Außerdem ist die Aktion **Inhalt verteilen** nicht verfügbar. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Ändern im Configuration Manager Client Install  
Basierend auf dem Feedback von Benutzern wird [Silverlight nicht mehr automatisch auf Clients installiert](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v). <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Ändern des Surface-Gerätedashboards
Im Surface-Gerätedashboard werden jetzt Firmwareversionen für Surface-Geräte anstelle von Betriebssystemversionen angezeigt. Navigieren Sie in der Konsole zu **Überwachung** > **Surface Devices** (Surface-Geräte). Sie können die folgenden Elemente anzeigen:
- Prozent von Surfaces
- Prozent von Surface-Modellen
- Die fünf beliebtesten Firmwareversion
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Verbesserungen des Office 365 Client Management-Dashboards 
Im Office 365 Client Management-Dashboard wird jetzt eine Liste von relevanten Geräten angezeigt, wenn die Diagrammabschnitte ausgewählt werden. Wechseln Sie in der Konsole zu **Softwarebibliothek** >**Übersicht** >**Office 365-Clientverwaltung**. Das Dashboard wird auf der rechten Seite angezeigt. Wenn Sie aus dem Diagramm einzelne Kriterien auswählen, wird eine Liste von Geräten angezeigt.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Verbesserungen der Configuration Manager-Konsole 
Basierend auf dem Feedback von Benutzern haben wir die folgenden Verbesserungen an der Configuration Manager-Konsole vorgenommen.

- [In der Geräteliste wird der primäre Benutzer angezeigt:](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user) Die Geräteliste unter „Bestand und Kompatibilität“ > „Geräte“ zeigt jetzt standardmäßig den primären Benutzer an. Der Benutzer, der als letztes angemeldet war, kann als optionale Spalte hinzugefügt werden. <!-- 1357280 -->
- [Umbenannte Sammlungen werden in bestehenden Sammlungsmitgliedschaftsregeln angezeigt:](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections) Wenn es sich bei einer Sammlung um ein Mitglied einer anderen Sammlung handelt, das umbenannt wird, wird der neue Name unter den Mitgliedschaftsregeln aktualisiert.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>Verbesserungen bei der Betriebssystembereitstellung
Teilweise basierend auf dem Feedback von Benutzern haben wir die folgenden Verbesserungen an der Betriebssystembereitstellung vorgenommen.
 - [Standardprotokollanzeige im Startimage:](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a) In Windows PE werden Sie beim Starten der cmtrace.exe-Datei nicht mehr aufgefordert, zu entscheiden, ob dieses Programm die Standardanzeige für Protokolldateien sein soll. <!-- SMS 500897 -->
 - Schritt „Paketinhalt herunterladen“: Sie können jetzt dem Schritt „Tasksequenz“ Startimages hinzufügen.


## <a name="windows-10-feedback-hub-app-integration"></a>Integration der Feedback Hub-App für Windows 10

Wir schätzen Ihr Feedback sehr. Daher können Sie ihr Feedback jetzt über die in Windows 10 integrierte [Feedback Hub-App](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) übermitteln. Wenn Sie **neues Feedback übermitteln**, achten Sie darauf, die Kategorie **Enterprise Management** auszuwählen und dann eine der folgenden Unterkategorien auszuwählen:
 - Configuration Manager-Client
 - Configuration Manager-Konsole
 - Betriebssystembereitstellung von Configuration Manager
 - Configuration Manager-Server

Nutzen Sie weiterhin unsere [Seite für Benutzerfeedback](http://configurationmanager.uservoice.com/), um über Ideen für neue Funktionen von Configuration Manager abzustimmen.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Installation oder dem Update der Technical Preview finden Sie unter [Technical Preview für System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
