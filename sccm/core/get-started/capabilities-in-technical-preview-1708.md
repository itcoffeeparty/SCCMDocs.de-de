---
title: Technical Preview 1708
titleSuffix: Configuration Manager
description: "Erfahren Sie mehr über die Funktionen, die mit der Technical Preview-Version 1708 für System Center Configuration Manager zur Verfügung stehen."
ms.custom: na
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: 84d3b10bf5eede1ce7557adb74a1b11a38fad777
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1708-for-system-center-configuration-manager"></a>Funktionen in der Technical Preview 1708 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*

In diesem Artikel werden die Features erläutert, die in der Technical Preview für System Center Configuration Manager 1708 verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Technical Preview-Version installieren, lesen Sie [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview-Version vertraut zu machen und zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Funktionen in einer Technical Preview-Version geben können.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bekannte Probleme in dieser Technical Preview:**
-   **Beim Update auf Vorschauversion 1708 tritt ein Fehler auf, wenn Sie über einen Standortserver im passiven Modus verfügen**. Wenn Sie die Vorschauversion 1706 oder 1707 ausführen und über einen [primären Standortserver im passiven Modus](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability) verfügen, müssen Sie den Standortserver im passiven Modus deinstallieren, bevor Sie Ihren Vorschaustandort erfolgreich auf Version 1708 aktualisieren können. Sie können den Standortserver im passiven Modus erneut installieren, wenn an Ihrem Standort Version 1708 ausgeführt wird.

  So deinstallieren Sie den Standortserver im passiven Modus:
  1. Navigieren Sie in der Konsole zu **Administration** > **Übersicht** > **Standortkonfiguration** > **Server und Standortsystemrollen**, und wählen Sie den Standortserver im passiven Modus aus.
  2. Klicken Sie im Bereich **Standortsystemrollen** mit der rechten Maustaste auf die Rolle **Standortserver**, und wählen Sie dann **Rolle entfernen**.
  3. Klicken Sie mit der rechten Maustaste auf den Standortserver im passiven Modus, und wählen Sie dann **Löschen**.
  4. Starten Sie nach dem Deinstallieren des Standortservers auf dem aktiven primären Standortserver den Dienst **CONFIGURATION_MANAGER_UPDATE** neu.




**Im Folgenden werden neue Funktionen aufgelistet, die Sie mit dieser Version ausprobieren können.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Verbesserungen beim Angeben von Skriptparametern während der Bereitstellung von PowerShell-Skripts aus Configuration Manager
<!-- 1236459 -->

Ab Configuration Manager 1706 können Sie [PowerShell-Skripts über die Configuration Manager-Konsole erstellen und ausführen](/sccm/apps/deploy-use/create-deploy-scripts).

In der [Technical Preview 1707](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) wurde diese Funktionalität erweitert, sodass Configuration Manager jetzt Parameter aus dem Skript lesen kann.

In dieser Technical Preview haben wir die Funktionalität für Skriptparameter erweitert: Configuration Manager kann jetzt ermitteln, welche Parameter obligatorisch und welche optional sind, und Sie auffordern, diese Parameter einzugeben.

### <a name="try-it-out"></a>Probieren Sie es aus!

1. Folgen Sie zum [Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole](/sccm/apps/deploy-use/create-deploy-scripts) diesen Anweisungen.
2. Wählen Sie auf der neuen Seite **Skriptparameter** des **Assistenten zum Erstellen von Skripts** einen Parameter aus, und bearbeiten Sie die Parameterwerte.
Der Assistent zeigt an, welche Parameter obligatorisch und welche optional sind.
4. Wenn Sie mit dem Bearbeiten der Parameter fertig sind, schließen Sie den Assistenten ab.

Wenn das Skript ausgeführt wird, werden alle Parameterwerte verwendet, die Sie konfiguriert haben. Wenn Sie einen obligatorischen Parameter nicht konfiguriert haben, werden Endbenutzer beim Ausführen des Skripts aufgefordert, diesen Parameter anzugeben.

## <a name="management-insights"></a>Einblicke für die Verwaltung
<!-- 1353967 -->
Sie können jetzt anhand der Analyse von Daten in der Standortdatenbank Einblicke in den aktuellen Zustand Ihrer Umgebung erhalten. Diese Einblicke vermitteln Ihnen ein genaueres Verständnis Ihrer Umgebung, sodass Sie entsprechende Maßnahmen ergreifen können. Sie können die Einblicke für die Verwaltung in der Configuration Manager-Konsole unter **Verwaltung** > **Einblicke für die Verwaltung** > **Alle Einblicke** anzeigen. In diesem Release sind jetzt folgende Einblicke verfügbar:

- **Anwendungen ohne Bereitstellungen**: Führt diejenigen Anwendungen in Ihrer Umgebung auf, für die keine aktiven Bereitstellungen vorhanden sind. So können Sie nicht verwendete Anwendungen finden und löschen, um die in der Konsole angezeigte Anwendungsliste zu vereinfachen.
- **Leere Sammlungen**: Führt die Sammlungen in Ihrer Umgebung auf, die keine Elemente enthalten. Sie können diese Sammlungen löschen, um die Liste der Sammlungen zu vereinfachen, die z.B. beim Bereitstellen von Objekten angezeigt wird.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Neustarten von Computern über die Configuration Manager-Konsole   
<!-- 1356283 -->
Ab diesem Release können Sie die Configuration Manager-Konsole verwenden, um Clientgeräte zu identifizieren, die einen Neustart erfordern, und diese Geräte dann mit einer Clientbenachrichtungsaktion neu starten.

Um Geräte zu identifizieren, für die ein Neustart aussteht, wechseln Sie zu **Assets und Konformität** > **Geräte**, und wählen Sie eine Sammlung mit Geräten aus, die möglicherweise neu gestartet werden müssen. Nach Auswahl der Sammlung können Sie den Status für jedes Gerät im Detailbereich in einer neuen Spalte namens **Neustart steht aus** auswählen. Jedes Gerät weist entweder den Wert **Ja** oder den Wert **Nein** auf.

So erstellen Sie die Clientbenachrichtigung zum Neustarten eines Geräts:
1.  Ermitteln Sie im Knoten „Geräte“ der Konsole das Gerät, das Sie neu starten möchten.
2.  Klicken Sie mit der rechten Maustaste auf das Gerät, und wählen Sie **Clientbenachrichtigung** und danach **Neustart** aus. Dadurch wird ein Fenster mit Informationen zum Neustart geöffnet. Klicken Sie zum Bestätigen der Anforderung des Neustarts auf **OK** .

Wenn ein Client diese Benachrichtigung empfängt, wird dort ein **Softwarecenter**-Benachrichtigungsfenster geöffnet, um den Benutzer über den Neustart zu informieren. Standardmäßig erfolgt der Neustart nach 90 Minuten. Sie können den Zeitpunkt des Neustarts durch Konfigurieren der [Clienteinstellungen](/sccm/core/clients/deploy/configure-client-settings) ändern. Sie finden die Einstellungen für das Neustartverhalten in den Standardeinstellungen auf der Registerkarte [Computerneustart](/sccm/core/clients/deploy/about-client-settings#computer-restart).


### <a name="try-it-out"></a>Probieren Sie es aus!
Versuchen Sie, die folgenden Aufgaben auszuführen, und senden Sie uns dann **Feedback** über die Registerkarte **Start** des Menübands, um uns zu wissen zu lassen, wie es funktioniert hat:
1.  Stellen Sie eine App oder eine Aktualisierung auf einem Gerät bereit, die zum Abschließen der Installation einen Geräteneustart erfordert.
2.  Suchen Sie das Gerät im Konsolenknoten **Assets und Konformität** > **Geräte**, und vergewissern Sie sich, dass in der Spalte **Neustart steht aus** der Wert **Ja** angezeigt wird. Es kann bis zu 20 Minuten dauern, bis der Status „Neustart steht aus“ in der Konsole berücksichtigt und angezeigt wird.
3.  Überwachen Sie das Gerät, um sicherzustellen, dass die Softwarecenter-Benachrichtigung geöffnet und das Gerät erfolgreich neu gestartet wird.


## <a name="software-center-customization"></a>Anpassen des Softwarecenters
<!-- 1351224 -->
Im Softwarecenter können Sie Brandingelemente Ihres Unternehmens hinzufügen und die Sichtbarkeit von Registerkarten festlegen. Sie können den im Softwarecenter verwendeten Namen Ihres Unternehmens hinzufügen sowie ein Farbschema für die Softwarecenter-Konfiguration, ein Unternehmenslogo und die sichtbaren Registerkarten für Clientgeräte festlegen.

### <a name="customize-software-center"></a>Anpassen des Softwarecenters

So ändern Sie das Softwarecenter:

1. Wählen Sie in der **Configuration Manager**-Konsole **Verwaltung** > **Clienteinstellungen** aus. Klicken Sie auf die gewünschte Clienteinstellungsinstanz.
2. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.
3. Wählen Sie im Dialogfeld **Standardeinstellungen** die Option **Softwarecenter** aus.
4. Klicken Sie bei **Neue Einstellungen zum Angeben von Unternehmensinformationen auswählen** die Option **Ja** aus, um die Einstellungen für die Softwarecenter-Anpassung zu aktivieren.
5. Geben Sie den **Namen Ihres Unternehmens** ein.
6. Wählen Sie das gewünschte **Farbschema für Softwarecenter** aus.
7. Klicken Sie auf **Durchsuchen**, um zu Ihrem Logo für Softwarecenter zu navigieren. Das Logo muss eine JPEG- oder PNG-Datei mit 400 × 100 Pixeln und einer Größe von maximal 750 KB sein.
8. Wählen Sie **Ja**, damit die Registerkarten im Softwarecenter für Clientgeräte sichtbar werden. Mindestens eine Registerkarte muss sichtbar sein:

    -  Registerkarte „Anwendungen“ aktivieren
    -  Registerkarte „Updates“ aktivieren
    -  Registerkarte „Betriebssysteme“ aktivieren
    -  Registerkarte „Installationsstatus“ aktivieren
    -  Registerkarte Gerätekonformität“ aktivieren
    -  Registerkarte „Optionen“ aktivieren

### <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Anwendungsverwaltung in Configuration Manager finden Sie unter [Einführung in die Anwendungsverwaltung in System Center Configuration Manager](\sccm\apps\understand\introduction-to-application-management).
