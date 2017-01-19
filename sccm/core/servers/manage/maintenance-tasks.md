---
title: Wartungstasks | Microsoft-Dokumentation
description: "Hier finden Sie Informationen dazu, welche Wartungstasks für Configuration Manager-Standorte und -Hierarchien zu welchem Zeitpunkt durchgeführt werden müssen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 46a24145d28111d7611f393f5806d0d7cc47ed71


---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>Wartungstasks für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager-Standorte und -Hierarchien müssen regelmäßig gewartet und überwacht werden, damit Dienste effektiv und ohne Unterbrechungen bereitgestellt werden können. Durch regelmäßige Wartung wird die ordnungsgemäße, effiziente Funktionsfähigkeit von Hardware, Software und Configuration Manager-Standortdatenbank dauerhaft sichergestellt. Durch optimale Leistung wird das Risiko eines Ausfalls erheblich reduziert.  

 Informationen zum Konfigurieren von Benachrichtigungen sowie zum Überwachen der Integrität von Configuration Manager mit dem Statussystem finden Sie unter [Use alerts and the status system for System Center Configuration Manager (Verwenden von Benachrichtigungen und Statussystem für System Center Configuration Manager)](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   [Wartungstasks](#bkmk_MTs)  

##  <a name="a-namebkmkmtsa-maintenance-tasks"></a><a name="bkmk_MTs"></a> Wartungstasks  
 Eine regelmäßige Ausführung der Wartung ist wichtig, um den ordnungsgemäßen Standortbetrieb zu gewährleisten. Führen Sie ein tägliches Wartungsprotokoll, um zu dokumentieren, wann die Wartung von wem vorgenommen wurde, und um alle wartungsrelevanten Kommentare zum ausgeführten Task aufzuzeichnen.  

### <a name="when-to-perform-common-maintenance-tasks"></a>Wahl des Zeitpunkts für die Ausführung allgemeiner Wartungstasks  
 Erwägen Sie die Ausführung regelmäßiger Wartungstasks auf täglicher oder wöchentlicher Basis, in einigen Fällen sogar häufiger, um Ihren Standort zu warten. Zur allgemeinen Wartung können sowohl die integrierten Wartungstasks gezählt werden als auch andere Tasks wie die Kontowartung, die Sie zur Einhaltung Ihrer Unternehmensrichtlinien verwenden.  

 Orientieren Sie sich an den folgenden Informationen, wenn Sie den Ausführungszeitpunkt verschiedener Wartungstasks planen. Verwenden Sie diese Listen als Ausgangspunkt, und fügen Sie gegebenenfalls zusätzliche Tasks hinzu, die Sie benötigen.  

**Tägliche Aufgaben**   
Sie sollten erwägen, die folgenden Wartungstasks täglich auszuführen:  

-   Überprüfen, ob die vordefinierten Wartungstasks, die für die tägliche Ausführung geplant sind, erfolgreich ausgeführt werden  

-   Überprüfen des Configuration Manager-Datenbankstatus  

-   Überprüfen des Status des Standortservers  

-   Überprüfen der Posteingänge des Configuration Manager-Standortsystems auf Dateirückstände  

-   Überprüfen des Status der Standortsysteme  

-   Überprüfen der Betriebssystemereignisprotokolle auf den Standortsystemen  

-   Überprüfen des SQL Server-Fehlerprotokolls auf dem Standortdatenbankcomputer  

-   Überprüfen der Systemleistung  

-   Überprüfen von Configuration Manager-Benachrichtigungen  

**Wöchentliche Aufgaben**   
Sie sollten erwägen, die folgenden Wartungstasks wöchentlich auszuführen:  

-   Überprüfen Sie, ob die vordefinierten Wartungsaufgaben, die für die wöchentliche Ausführung geplant sind, erfolgreich ausgeführt werden.  

-   Löschen von nicht erforderlichen Dateien aus Standortsystemen  

-   Erstellen und Verteilen von Endbenutzerberichten (sofern erforderlich)  

-   Sichern von Anwendungs-, Sicherheits- und Systemereignisprotokollen sowie Löschen von deren Inhalten  

-   Überprüfen der Größe der Standortdatenbank und Sicherstellen, dass ausreichend Speicherplatz auf dem Standortdatenbankserver verfügbar ist, um dem Wachstum der Standortdatenbank gerecht zu werden  

-   Ausführen einer SQL Server-Datenbankwartung für die Standortdatenbank entsprechend Ihrem SQL Server-Wartungsplan  

-   Überprüfen des verfügbaren Speicherplatzes auf allen Standortsystemen  

-   Ausführen der Festplattendefragmentierungstools auf allen Standortsystemen  

**Regelmäßige Tasks**   
Einige Wartungstasks müssen nicht täglich oder wöchentlich ausgeführt werden, sind aber wichtig, um sicherzustellen, dass die gesamte Standortintegrität und -sicherheit sowie die Wiederherstellungspläne auf dem neuesten Stand sind. Bei den folgenden Wartungstasks empfiehlt sich unter Umständen eine häufigere Ausführung als täglich oder wöchentlich:  

-   Ggf. Ändern von Konten und Kennwörtern gemäß Ihrem Sicherheitsplan  

-   Überprüfen des Wartungsplans zur Sicherstellung, dass geplante Wartungstasks in Abhängigkeit von den konfigurierten Standorteinstellungen ordnungsgemäß und effektiv geplant sind  

-   Überprüfen des Configuration Manager-Hierarchieentwurfs auf erforderliche Änderungen  

-   Prüfen der Netzwerkleistung zur Sicherstellung, dass keine Änderungen vorgenommen wurden, die Standortvorgänge beeinträchtigen  

-   Sicherstellen, dass Active Directory-Einstellungen, die sich auf Standortvorgänge auswirken, nicht geändert wurden. Stellen Sie beispielsweise sicher, dass Subnetze, die als Grenzen für einen Configuration Manager-Standort verwendeten Active Directory-Standorten zugewiesen sind, nicht geändert wurden.  

-   Überprüfen des Wiederherstellungsplans auf erforderliche Änderungen  

-   Durchführen einer Standortwiederherstellung gemäß dem Wiederherstellungsplan in einem Testlabor mithilfe einer Sicherungskopie der aktuellen Sicherung, die über den Wartungstask „Standortserver sichern“ erstellt wurde  

-   Überprüfen der Hardware auf Fehler oder verfügbare Hardwareupdates  

-   Überprüfen der Gesamtintegrität des Standorts  

###  <a name="a-namebkmkusemtsa-maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a> Aufrechterhalten der funktionalen Integrität Ihrer Standortdatenbank  
 Während die von Ihnen geplanten und konfigurierten Tasks von Configuration Manager-Standort und -Hierarchie ausgeführt werden, werden der Configuration Manager-Datenbank durch Standortkomponenten ständig neue Daten hinzugefügt. Durch zunehmende Datenmengen werden die Datenbankleistung und der Datenbankspeicherplatz zunehmend beansprucht. Sie können Standortwartungstasks so konfigurieren, dass veraltete Daten, die Sie nicht mehr benötigen, entfernt werden.  

 In Configuration Manager sind vordefinierte Wartungstasks verfügbar, die Sie zur Aufrechterhaltung der Integrität der Configuration Manager-Datenbank verwenden können. Es sind nicht alle Wartungstasks an jedem Standort verfügbar. Standardmäßig sind mehrere Wartungstasks aktiviert, andere sind deaktiviert. Von allen Wartungstasks wird ein Zeitplan unterstützt, mithilfe dessen Sie konfigurieren können, wann die Wartungstasks ausgeführt werden sollen.  

 Von den meisten Wartungstasks werden veraltete Daten in regelmäßigen Abständen aus der Configuration Manager-Datenbank entfernt. Durch das Entfernen nicht erforderlicher Daten wird die Größe der Datenbank reduziert. Hierdurch werden Leistung und Integrität der Datenbank sowie in der Folge die Effizienz von Standort und Hierarchie erhöht. Mit anderen Tasks, beispielsweise mit **Indizes neu erstellen**, können Sie die Effizienz der Datenbank aufrechterhalten, und mit wieder anderen Tasks wie beispielsweise **Standortserver sichern** können Sie eine Notfallwiederherstellung vorbereiten.  

> [!IMPORTANT]  
>  Wenn Sie die Ausführung von Tasks planen, von denen Daten gelöscht werden, berücksichtigen Sie die hierarchieweite Verwendung dieser Daten. Wenn von einem Task, durch den Daten gelöscht werden, an einem Standort ausgeführt wird, werden die Informationen aus der Configuration Manager-Datenbank gelöscht, und diese Änderung wird an alle Standorte in der Hierarchie repliziert. Hiervon können andere Tasks, die von diesen Daten abhängig sind, beeinträchtigt werden. Beispielsweise könnten Sie am Standort der zentralen Verwaltung die Ermittlung zur Ausführung einmal monatlich konfigurieren, um Nicht-Clientcomputer zu identifizieren, und eine Installation des Configuration Manager-Clients auf diesen Computern innerhalb von zwei Wochen nach der Ermittlung planen. Jedoch konfiguriert ein Administrator an einem Standort in der Hierarchie den Task „Veraltete Ermittlungsdaten löschen“ für die Ausführung alle 7 Tage. Hierdurch werden die Nicht-Clientcomputer 7 Tage, nachdem sie ermittelt wurden, aus der Configuration Manager-Datenbank gelöscht. Sie wiederum bereiten am Standort der zentralen Verwaltung eine Pushinstallation des Configuration Manager-Clients auf den neuen Computern für Tag 10 vor. Doch da der Task „Veraltete Ermittlungsdaten löschen“ kürzlich ausgeführt wurde und dadurch Daten, die älter als 7 Tage waren, gelöscht wurden, sind die kürzlich ermittelten Computer in der Datenbank nicht mehr verfügbar.  

Überprüfen Sie nach der Installation eines Configuration Manager-Standorts die verfügbaren Wartungstasks, und aktivieren Sie diejenigen, die für Ihre Vorgänge erforderlich sind. Überprüfen Sie den Standardzeitplan jedes Tasks, und ändern Sie die Zeitpläne nach Bedarf, um eine Feinabstimmung des Tasks auf Ihre Hierarchie und Umgebung auszuführen. Der Standardzeitplan jedes Tasks ist für die meisten Umgebungen passend. Überwachen Sie dennoch die Leistung Ihrer Standorte und der Datenbank, und gehen Sie davon aus, dass eine Feinabstimmung der Tasks erforderlich ist, um die Effizienz Ihrer Bereitstellung zu steigern. Planen Sie regelmäßige Überprüfungen der Leistung von Standort und Datenbank ein, und konfigurieren Sie Wartungstasks sowie deren Zeitpläne neu, um die Effizienz aufrechtzuerhalten.  

#### <a name="configure-maintenance-tasks"></a>Konfigurieren von Wartungstasks  
 Von jedem Configuration Manager-Standort werden Wartungstasks unterstützt, mit denen die Betriebseffizienz der Standortdatenbank aufrechterhalten werden kann. Standardmäßig sind an jedem Standort mehrere Wartungstasks aktiviert. Von allen Tasks werden unabhängige Zeitpläne unterstützt. Wartungstasks werden für jeden Standort einzeln konfiguriert und gelten für die Datenbank an dem Standort; manche Tasks (z. B. **Veraltete Ermittlungsdaten löschen**) betreffen jedoch Informationen, die an allen Standorten der Hierarchie verfügbar sind.  

 In der Configuration Manager-Konsole werden nur die Wartungstasks angezeigt, die Sie an einem Standort konfigurieren können. Eine umfassende Liste mit Wartungstasks nach Standorttyp finden Sie unter [Referenz für Wartungstasks für System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Anhand des folgenden Verfahrens können Sie die allgemeinen Einstellungen von Wartungstasks konfigurieren.  

###### <a name="to-configure-maintenance-tasks-for-configuration-manager"></a>So konfigurieren Sie Wartungstasks für Configuration Manager  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** >**Standorte**.  

2.  Wählen Sie den Standort mit dem zu konfigurierenden Wartungstask aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Standortwartung**, und wählen Sie dann den Wartungstask aus, den Sie konfigurieren möchten.  

    > [!TIP]  
    >  Es werden nur die Tasks angezeigt, die am ausgewählten Standort verfügbar sind.  

4.  Klicken Sie zum Konfigurieren des Tasks auf **Bearbeiten**, vergewissern Sie sich, dass das Kontrollkästchen **Diese Aufgabe aktivieren** aktiviert ist, und konfigurieren Sie einen Zeitplan zum Ausführen des Tasks. Wenn mithilfe des Tasks auch veraltete Daten gelöscht werden, legen Sie fest, in welchem Alter Daten bei der Taskausführung aus der Datenbank gelöscht werden sollen. Klicken Sie auf **OK** , um die **Eigenschaften**des Tasks zu schließen.  

    > [!NOTE]  
    >  Legen Sie für **Veraltete Statusmeldungen löschen**fest, in welchem Alter Daten beim Konfigurieren von Statusfilterregeln gelöscht werden sollen.  

5.  Klicken Sie auf die Schaltflächen **Aktivieren** oder **Deaktivieren** , um den Task zu aktivieren bzw. zu deaktivieren, ohne die Taskeigenschaften zu ändern. Die Bezeichnung der Schaltfläche ändert sich je nach aktueller Konfiguration des Tasks.  

6.  Wen Sie die Wartungstasks konfiguriert haben, klicken Sie auf **OK** , um den Vorgang abzuschließen.



<!--HONumber=Dec16_HO3-->


