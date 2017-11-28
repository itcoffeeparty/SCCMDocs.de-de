---
title: Importieren von Daten in Microsoft Intune
titleSuffix: Configuration Manager
description: 
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: 4b5f788a611b9df7c12f788099d82fadbf1e4af9
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importieren von Configuration Manager-Daten in Microsoft Intune 

*Gilt für: System Center Configuration Manager (Current Branch)*    

Die empfohlene erste Phase im Prozess zum [Migrieren von hybriden MDM-Benutzern und -Geräten zu eigenständigem Intune](migrate-hybridmdm-to-intunesa.md) in der reinen Cloudkonfiguration ist der Einsatz des Intune-Tools zum Importieren von Daten. Nach Wunsch können Sie diese Phase überspringen und zur Phase [Vorbereiten von Intune auf Benutzermigration](migrate-prepare-intune.md) übergehen. Dieses Tool führt jedoch die folgenden Aufgaben aus, die Ihnen in der nächsten Phase viel Zeit sparen können: 
1.  Sammeln von Daten zu den Objekten, die Sie in Ihrer Configuration Manager-Hierarchie auswählen 
2.  Bereitstellen von Details zu den Objekten, die Sie für den Import auswählen können, und Informationen zu den Gründen, warum ein Objekt nicht importiert werden kann
3.  Importieren ausgewählter Objekte in Ihren Microsoft Intune-Mandanten 

Das Datenimport-Tool ändert Ihre Configuration Manager-Umgebung in keiner Weise. Daher können Sie Objekte in Intune importieren und prüfen, ob alles wie erwartet funktioniert, ohne das Risiko einzugehen, Ihre hybriden MDM-Geräte in einem nicht verwalteten Zustand zu hinterlassen. 

## <a name="what-objects-can-this-tool-import"></a>Welche Objekte können mit diesem Tool importiert werden?
Das Import-Tool kann Informationen zu den folgenden Objekttypen im Configuration Manager sammeln und gibt Auskunft darüber, ob die gesammelten Objekte importiert werden können: 
- Konfigurationselemente
- Zertifikatprofile
- E-Mail-Profile
- VPN-Profile
- WLAN-Profile
- Kompatibilitätsrichtlinien
- Apps
- Bereitstellungen

> [!Note]    
> Das Importieren von Bereitstellungen ist nur für andere Objekttypen sinnvoll, die Sie importieren. Wenn Sie beispielsweise VPN-Profile und Bereitstellungen importieren, können Sie nur die Bereitstellungen für die von Ihnen ausgewählten VPN-Profile importieren. Bereitstellungen werden in Intune als „Zuweisungen“ bezeichnet. Wenn Sie eine Bereitstellung für ein zuvor importiertes Objekt importieren möchten, müssen Sie dieses Objekt erneut importieren oder die Zuweisung in Intune in Azure manuell erstellen. Wenn Sie beispielsweise VPN-Profile und keine Bereitstellungen importieren, müssen Sie das Tool erneut ausführen und VPN-Profile und Bereitstellungen auswählen oder die Zuweisung in Intune in Azure manuell erstellen.  Wenn Sie das Tool erneut ausführen, können duplizierte Objekte erstellt werden, die Sie später in Intune in Azure löschen können.  

> [!Important]    
> Wenn die Sammlung für eine Bereitstellung auf einer Active Directory-Gruppe basiert, die in Azure Active Directory (AAD) repliziert wurde, zielt das Tool automatisch auf migrierte Objekte in den Gruppen ab, sofern Sie beim Ausführen des Tools die entsprechende Bereitstellung auswählen. Wenn Sie komplexere Sammlungen oder Sammlungen direkter Mitgliedschaften haben, müssen Sie diese in AAD manuell neu anlegen und für diese in Intune in Azure manuelle Objektzuweisungen vornehmen.


## <a name="things-to-know-before-you-run-the-tool"></a>Was Sie vor dem Ausführen des Tools wissen sollten
- Durch Ausführen des Tools wird Ihre Configuration Manager-Umgebung in keiner Weise geändert.
- Wir empfehlen, den Datenimportprozess zunächst mit einem Testmandanten zu testen. Nachdem Sie bestätigt haben, dass die von Ihnen erwarteten Daten importiert wurden, können Sie den gleichen Prozess mit Ihrem Intune-Mandanten in der Produktionsumgebung durchlaufen.
- Das Datenimport-Tool ist darauf ausgelegt, Configuration Manager-Daten nur einmal zu importieren. Es dient nicht zum Nachverfolgen von Objekten in Configuration Manager oder Intune. Wenn Sie das Import-Tool jedoch erneut auf demselben Computer wie zuvor ausführen, erfahren Sie, welche Objekte Sie zuvor importiert haben. Das Tool weiß nicht, ob das Objekt noch in Intune vorhanden ist oder ob sich ein Objekt geändert hat. Wenn Sie Daten mehrmals in Intune importieren, kann es zu duplizierten Objekten kommen.
- Nicht alle Profileinstellungen können importiert werden. Kioskmodus- oder PFX-Einstellungen können z. B. nicht importiert werden. 
- Wenn Sie eine Configuration Manager-Richtlinie mit Einstellungen haben, die für die ausgewählten Plattformen nicht gelten, ignoriert das Tool diese Einstellungen möglicherweise während des Imports. Das Ignorieren der Einstellungen hilft sicherzustellen, dass die Richtlinie importiert und von Intune unterstützt werden kann. 
- Das Tool versucht, Ihnen einen Grund zu nennen, warum ein Objekt nicht importiert werden kann. In einigen Fällen können Sie vor dem Importieren von Objekten in Intune zur Configuration Manager-Konsole zurückkehren, das Problem beheben, die Objekterkennung in Configuration Manager erneut starten und anschließend die Objekte importieren. Mitunter ist es notwendig oder wünschenswert, diese Objekte manuell in Intune neu zu erstellen.
- Es gibt einige Profile, die von anderen Objekten abhängen. Wenn Sie ein Profil importieren möchten, das von einem anderen Objekt abhängt, z. B. ein E-Mail-Profil, das von einem Zertifikat abhängt, müssen Sie beide Objekte gleichzeitig importieren.
- Nachdem Sie das Tool ausgeführt haben, müssen Sie möglicherweise zusätzliche manuelle Schritte ausführen. Sie müssen beispielsweise Apps und Richtlinien zu AAD-Gruppen zuordnen. 

## <a name="prerequisites"></a>Voraussetzungen
- Configuration Manager, Version 1610 oder höher. Wir empfehlen, den Standort auf oberster Ebene anzugeben und das Tool mit einem Benutzer zu starten, der Zugriff auf alle Objekte in der Standorthierarchie hat. Das Tool erkennt nur Objekte, auf die der Benutzer Zugriff hat, der das Tool ausführt. 
- Sie müssen das Tool auf einem Computer ausführen, der Zugriff auf den SMS-Anbieter (zum Sammeln von Configuration Manager-Daten) und das Internet (zum Importieren von Objekten in Intune) hat.
- Ein globaler Administrator muss das Datenimport-Tool beim ersten Mal mit dem Parameter ***intunedataimporter.exe -GlobalConsent*** ausführen. Anschließend kann das Tool von einem globalen Administrator oder Intune-Administrator ausgeführt werden.  


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->

## <a name="download-the-data-importer-tool"></a>Herunterladen des Datenimport-Tools
Das Datenimport-Tool kann von GitHub aus dem Repository „ConfigMgrTools/Intune-Data-Importer“ heruntergeladen werden. Gehen Sie zum Herunterladen des Tools wie folgt vor.

1. Wechseln Sie zur GitHub-Seite [Intune-Data-Importer](https://go.microsoft.com/fwlink/?linkid=858194).
2. Klicken Sie auf **Clone or download**, dann auf **Download ZIP**, und speichern die komprimierte ZIP-Datei. 
3. Extrahieren Sie den Inhalt der ZIP-Datei.

## <a name="run-the-data-importer-tool"></a>Ausführen des Datenimport-Tools
Bevor Sie das Datenimport-Tool ausführen können, müssen Sie ein Konto eines globalen Administrators verwenden, um dem Datenimport-Tool in Azure die Berechtigung für den Zugriff auf Ressourcen zu erteilen. Anschließend können Sie das Tool mit dem Konto eines globalen Administrators oder Intune-Administrators ausführen.     

Der Assistent für das Datenimport-Tool kann in drei Hauptschritte unterteilt werden. Dieser Abschnitt enthält Informationen, die Ihnen helfen, jeden Abschnitt des Assistenten zu vervollständigen und Configuration Manager-Daten erfolgreich in Intune zu importieren. Jeder Schritt wird dort fortgesetzt, wo der vorhergehende Schritt beendet wurde.

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Erteilen von Berechtigungen für das Datenimport-Tool für den Zugriff auf Ressourcen
1.  Ein globaler Administrator muss das Tool beim ersten Mal mit dem Parameter ***intunedataimporter.exe -GlobalConsent*** ausführen. 
2. Beim Start des Tools wird ein Anmeldebildschirm angezeigt, auf dem Sie sich mit einem Konto der Rolle „Globaler Administrator“ bei Azure anmelden müssen. 
3. Klicken Sie zum Erstellen einer Anwendung in Azure mit ausreichenden Berechtigungen in Microsoft Graph auf **Accept** (Annehmen). Das Datenimport-Tool benötigt diese Rechte zum Importieren von Objekten in Microsoft Intune.   

   > [!Important]
   > Beim Klicken auf **Accept** (Annehmen) erteilen Sie dem Tool die Berechtigung für die folgenden Aktionen:
   > - Alle Gruppen lesen
   > - Anmelden und das Benutzerprofil lesen
   > - Intune-Gerätekonfiguration und -Richtlinien lesen und schreiben
   > - Intune-Apps lesen und schreiben
   > - Intune-Steuerungsrichtlinien für die rollenbasierte Verwaltung lesen und schreiben
   > - Intune-Geräte lesen und schreiben
   > - Intune-Konfiguration lesen und schreiben
1. Nachdem Sie die Zustimmung gegeben haben, kann jeder andere globale Administrator oder Intune-Administrator das Tool ausführen, um Daten aus Configuration Manager in Intune in Azure zu importieren.    
        
    > [!Note]
    > Wenn die Zustimmung nicht zuerst von einem globalen Administrator gegeben wurde, zeigt das Tool möglicherweise **You can't access this application** (Sie können nicht auf diese Anwendung zugreifen) an, nachdem ein Intune-Administrator das Datenimport-Tool ausgeführt und sich beim Intune-Abonnement angemeldet hat.

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Phase 1: Ermitteln von Configuration Manager-Objekten und Sammeln von Daten
In Phase 1 wählen Sie die zu ermittelnden Objekte aus und lassen das Tool Informationen zu den ausgewählten Objekten sammeln. 
1. Öffnen Sie das Tool, und klicken Sie auf **Start** (Starten).  
2. Lesen Sie die Informationen, und klicken Sie dann auf **Next** (Weiter). 
3. Geben Sie die folgenden Informationen über Ihren Standort und die Objekte am Standort an, die Sie importieren möchten. 
    - **Site server name** (Standortservername): Geben Sie zum Importieren von Objekten den vollqualifizierten Domänennamen des Standortservers an. Das Tool erkennt nur Objekte, auf die der Benutzer Zugriff hat, der das Tool ausführt. In der Regel geben Sie den Standort auf oberster Ebene an und starten das Tool mit einem Benutzer, der Zugriff auf alle Objekte in der Standorthierarchie hat.
    - **Site code** (Standortcode): Geben Sie den Standortcode für den Standortserver an. Sie finden den aus drei Buchstaben bestehenden Code oben in der Configuration Manager-Konsole.
    - **Object types to import** (Zu importierende Objekttypen): Wählen Sie die Objekte aus, die das Tool sammeln soll. Sie können **Select all** (Alle auswählen) wählen, um alle Objekte oder einzelne Objekttypen auszuwählen. 
4.  Klicken Sie auf **Next** (Weiter), um mit dem Erkennen der Objekte am Standort zu beginnen. Das Tool zeigt den Status für jeden Objekttyp an. 
    - Wenn das Tool keine Daten für einen ausgewählten Objekttyp findet, zeigt der Statusbalken für diesen Objekttyp „Completed“ (Abgeschlossen) an.
    - Objekte, die Sie nicht ausgewählt haben, werden nicht auf der Seite **Collect data** (Daten sammeln) angezeigt. 
    - Für Objekte, die nicht gesammelt wurden oder bei denen Sie den Sammelvorgang abgebrochen haben, können Sie das Tool erneut ausführen.

### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>Phase 2: Lösen von Problemen und Auswählen der zu importierenden Objekte  
In Phase 2 überprüfen Sie die vom Tool gefundenen Objekte, beheben Probleme, die verhindern, dass das Objekt in Intune importiert wird, und wählen die zu importierenden Objekte aus. Wenn Sie Probleme beheben, kehren Sie zur Seite **Discover environment** (Umgebung erfassen) des Assistenten zurück, um die Objekte erneut zu ermitteln. 
5.  Klicken Sie auf **Next** (Weiter), um die gesammelten Objekte zu überprüfen. Für jeden gesammelten Objekttyp steht eine Elementauswahlseite zur Verfügung. 

    > [!Tip]     
    > Auf jeder Seite zur Auswahl von Elementen können Sie einen Filter erstellen, der Ihnen hilft, die Objekte zu finden, die Sie importieren möchten. Allerdings sollten Sie Folgendes beachten:
    > - Wenn Sie sich auf einer Elementauswahlseite befinden und die Ansicht gefiltert ist, gelten die Kontrollkästchen des Typs „Select all“ (Alle auswählen) nur für die angezeigten Elemente. Alle aufgrund eines Filters ausgeblendeten Objekte werden bei Verwendung der Kontrollkästchen nicht berücksichtigt.
    > - Objekte werden stets unter ihrem übergeordneten Element gruppiert, auch wenn Sie die Objekte sortieren oder filtern.


6.  Sortieren Sie auf jeder Seite zur Elementauswahl die Objekte nach der Spalte „Importable“ (Importierbar), und überprüfen Sie die Objekte, die nicht importierbar sind. Die Informationen in der Spalte „Notes“ (Hinweise) geben Auskunft darüber, warum das Tool das Objekt nicht importieren kann. 
7.  Nun müssen Sie entscheiden, ob Sie die Probleme für nicht importierbare Objekte beheben möchten. Nachdem Sie ein oder mehrere Probleme behoben haben, klicken Sie auf „Previous“ (Zurück), bis Sie zur Seite „Select data from Configuration Manager“ (Daten aus Configuration auswählen) gelangen. Sammeln Sie dann die Daten erneut, um zu prüfen, ob das Problem behoben wurde. Sie können die Fehlerbehebung so lange fortsetzen, bis Sie mit den importierbaren Objekten zufrieden sind. 
8.  Wählen Sie auf jeder Elementauswahlseite die Objekte aus, die Sie importieren möchten. Die folgenden Spalten werden aufgeführt:
    - **Name**: Name des Configuration Manager-Objekts. 
    - **Importable** (Importierbar): Gibt an, ob ein Objekt importiert werden kann. Sie können nur Objekte auswählen, bei denen „Yes“ (Ja) in der Spalte „Importable“ (Importierbar) enthalten ist. 
    - **Platform** (Plattform): Gibt die vom Objekt unterstützte Plattform an.
    - **Already imported** (Bereits importiert): Gibt an, ob das Objekt bereits mit dem Tool auf diesem Computer importiert wurde. 
    - **Notes** (Hinweise): Bietet Informationen, warum ein Objekt nicht importiert werden kann.
    - **Configuration baselines** (Konfigurationsbaselines) (für Konfigurationselemente): Gibt die Konfigurationsbaselines an, die einem Konfigurationselement zugeordnet sind.
    - **Required certificate** (Erforderliches Zertifikat) (für Profile und Richtlinien): Gibt an, ob dem Objekt ein Zertifikat zugeordnet ist. Wenn dem Objekt ein Zertifikat zugeordnet ist, müssen Sie auch das Zertifikat importieren.
9.  Nachdem Sie die zu importierenden Objekte ausgewählt haben, werden sie auf der Seite „Summary“ (Zusammenfassung) aufgelistet. Die folgenden Aktionen sind verfügbar: 
    - **Export details** (Details exportieren): Erstellt eine CSV-Datei, die die auf dem Bildschirm angezeigten Informationen enthält. Sie können diese Datei zur Bezugnahme aufbewahren. 
    - **Export error data** (Fehlerdaten exportieren): Exportiert eine komprimierte Datei, die Informationen zu den Daten enthält, die das Tool nicht konvertieren oder importieren konnte. 

### <a name="phase-3-import-selected-object-to-intune"></a>Phase 3: Importieren ausgewählter Objekte in Intune
In Phase 3 melden Sie sich bei Intune an und importieren die ausgewählten Objekte. 
10. Klicken Sie auf **Next** (Weiter) und dann auf **Sign in to Intune** (Bei Intune anmelden), um sich für den Datenimport beim Intune-Mandanten anzumelden. Sie müssen sich mit dem Konto eines globalen Administrators oder Intune-Administrators anmelden. Nachdem Sie sich angemeldet haben, wird der Importvorgang gestartet.

    > [!Important]
    > Wir empfehlen, den Datenimportprozess zunächst mit einem Testmandanten zu testen. Nachdem Sie bestätigt haben, dass die von Ihnen erwarteten Daten importiert wurden, können Sie den gleichen Prozess mit Ihrem Intune-Mandanten in der Produktionsumgebung durchlaufen.

12. Die Seite „Status“ zeigt den Status an, während die Objekte importiert werden. Klicken Sie auf **Next** (Weiter), wenn der Import abgeschlossen ist. 
13. Auf der Seite „Completion“ (Abschluss) sind die importierten Objekte aufgeführt. Überprüfen Sie den Status aller Objekte, bei denen während des Importvorgangs ein Fehler aufgetreten ist. Die folgenden Aktionen sind verfügbar: 
    - **Export details** (Details exportieren): Erstellt eine CSV-Datei, die die auf dem Bildschirm angezeigten Informationen enthält. Sie können diese Datei zur Bezugnahme aufbewahren. 
    - **Export error data** (Fehlerdaten exportieren): Exportiert eine komprimierte Datei, die Informationen zu den Daten enthält, die das Tool nicht konvertieren oder importieren konnte.

## <a name="next-steps"></a>Nächste Schritte
Nachdem Sie die Daten in Intune importiert haben, müssen Sie Schritte unternehmen, um [ Intune für die Benutzermigration vorzubereiten](migrate-prepare-intune.md). 