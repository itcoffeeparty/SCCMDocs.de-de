---
title: Importieren von Daten in Microsoft Intune
titleSuffix: Configuration Manager
description: 
keywords: 
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: d42a5fd64b5baead8ef87d8c08a99ec659f94633
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2017
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importieren von Configuration Manager-Daten in Microsoft Intune 

*Gilt für: System Center Configuration Manager (Current Branch)*    

Die empfohlene erste Phase im Prozess zum [Migrieren von hybriden MDM-Benutzern und -Geräten zu eigenständigem Intune](migrate-hybridmdm-to-intunesa.md) in der reinen Cloudkonfiguration ist der Einsatz des Intune-Tools zum Importieren von Daten. Nach Wunsch können Sie diese Phase überspringen und zur Phase [Vorbereiten von Intune auf Benutzermigration](migrate-prepare-intune.md) übergehen. Dieses Tool führt jedoch die folgenden Aufgaben aus, die Ihnen in der nächsten Phase viel Zeit sparen können: 
1.  Sammeln von Daten zu den Objekten, die Sie in Ihrer Configuration Manager-Hierarchie auswählen 
2.  Bereitstellen von Details zu den Objekten, die Sie für den Import auswählen können, und Informationen zu den Gründen, warum Objekte nicht importiert werden können
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
- Es gibt einige Profile, die von anderen Objekten abhängen. Wenn Sie ein Profil importieren möchten, das von einem anderen Objekt abhängt, z.B. ein E-Mail-Profil, das von einem Zertifikat abhängt, müssen Sie beide Objekte gleichzeitig importieren. Dies gilt nicht, wenn Sie das andere Objekt zuvor von demselben Computer mit demselben Benutzer importiert haben.  
- Nachdem Sie das Tool ausgeführt haben, müssen Sie möglicherweise zusätzliche manuelle Schritte ausführen. Sie müssen beispielsweise Apps und Richtlinien zu AAD-Gruppen zuordnen. 

## <a name="prerequisites"></a>Voraussetzungen
- Configuration Manager, Version 1610 oder höher. Wir empfehlen, den Standort auf oberster Ebene anzugeben und das Tool mit einem Benutzer zu starten, der Zugriff auf alle Objekte in der Standorthierarchie hat. Das Tool erkennt nur Objekte, auf die der Benutzer Zugriff hat, der das Tool ausführt. 
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

1. Navigieren Sie zur Seite mit den [GitHub-Releases für den Intune-Datenimporter](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases).
2. Um das neueste Release zu erhalten, klicken Sie auf **Microsoft.Intune.Data.Importer.exe**.
3. Speichern Sie die EXE-Datei, und führen Sie sie aus (oder führen Sie sie lediglich aus). Wählen Sie dann einen Zielordner aus, in den das Intune-Datenimportertool extrahiert werden soll.

## <a name="run-the-data-importer-tool"></a>Ausführen des Datenimport-Tools
Der Assistent für das Datenimport-Tool kann in drei Hauptschritte unterteilt werden. Dieser Abschnitt enthält Informationen, die Ihnen helfen, jeden Abschnitt des Assistenten zu vervollständigen und Configuration Manager-Daten erfolgreich in Intune zu importieren. Jeder Schritt wird dort fortgesetzt, wo der vorhergehende Schritt beendet wurde.

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Erteilen von Berechtigungen für das Datenimport-Tool für den Zugriff auf Ressourcen
Bevor Sie das Datenimport-Tool ausführen können, müssen Sie ein Konto eines globalen Administrators verwenden, um dem Datenimport-Tool in Azure die Berechtigung für den Zugriff auf Ressourcen zu erteilen. Anschließend können Sie das Tool mit dem Konto eines globalen Administrators oder Intune-Administrators ausführen.   

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

### <a name="manually-map-collections-to-azure-ad-groups"></a>Manuelles Zuordnen von Sammlungen zu Azure AD-Gruppen
Wenn Sie das Datenimportertool ausführen, wird mit einer einzigen Regel, die für eine einzelne AD-Gruppe gilt, der AD-Gruppenname aus Sammlungen extrahiert. Wenn die Arbeitsaufträge in Intune erstellt werden, sucht der Datenimporter nach einer Azure AD-Gruppe mit dem gleichen Namen wie den der AD-Gruppe. Bei einer Übereinstimmung ordnet der Datenimporter das importierte Objekt dieser Azure AD-Gruppe zu. Sie können den AD-Gruppennamen, den der Datenimporter für eine Sammlung sucht, überschreiben und eine oder mehrere Azure AD-Gruppen für diese Sammlung angeben. Die Verwendung der Sammlungszuordnungsdatei bietet Ihnen die Möglichkeit, Azure AD-Gruppen Sammlungen zuzuordnen, die normalerweise nicht mit dem Datenimporter importiert werden können.
#### <a name="find-the-collections-that-cannot-be-imported"></a>Suchen nach den nicht importierbaren Sammlungen
Sie können eine Liste aller nicht importierbarer Sammlungen abrufen, um sie Ihrer CSV-Sammlungszuordnungsdatei hinzufügen zu können. 
1. Führen Sie das Datenimportertool aus, und wählen Sie die zu importierenden Objekte aus. Um die Objekte zu ermitteln und auszuwählen, verwenden Sie die Prozeduren unter [Phase 1: Ermitteln von Configuration Manager-Objekten und Sammeln von Daten](#phase-1:-discover-configuration-manager-objects-and-collect-data) und [Phase 2: Beheben von Problemen und Auswählen der zu importierenden Objekte](#phase-2:-resolve-issues-and-select-the-objects-to-import). Wählen Sie dann auf der Seite **Summary** (Zusammenfassung) die Option **Export Details** (Details exportieren), um eine CSV-Datei mit sämtlichen für den Import ausgewählten Objekten zu erstellen, einschließlich der nicht importierbaren Objekte und Bereitstellungen. 
2. Öffnen Sie die CSV-Datei in Microsoft Excel, und filtern Sie die Daten nach **Deployment** (Bereitstellung) für die Spalte **Type** (Typ) und **No** (Nein) für die Spalte **Importable** (Importierbar). Die Spalte „collection name“ (Sammlungsname) enthält alle Sammlungen, die einer Sammlungszuordnungsdatei hinzugefügt werden müssen, damit diese Bereitstellungen importiert werden können.

#### <a name="create-the-collection-mapping-file"></a>Erstellen der Sammlungszuordnungsdatei
Bei der Sammlungszuordnungsdatei handelt es sich um eine durch Trennzeichen getrennte Datei (CSV), wobei die erste Spalte den Namen der Configuration Manager-Sammlung und die zweite Spalte den für diese Sammlung zu verwendenden Namen der Azure AD-Gruppe angibt. Um mehr als eine Azure AD-Gruppe für eine einzelne Configuration Manager-Sammlung anzugeben, erstellen Sie mehrere Zeilen in der CSV-Datei mit diesem Sammlungsnamen. Im folgenden Beispiel wird eine CSV-Datei mit zwei Sammlungen gezeigt. Die erste Sammlung wird einer einzelnen Azure AD-Gruppe zugeordnet, während die zweite Sammlung zwei Azure AD-Gruppen zugeordnet wird.

![Beispiel für eine CSV-Sammlungszuordnungsdatei](..\media\migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>Starten des Datenimportertools mithilfe der Sammlungszuordnung
Um eine Sammlungszuordnungsdatei zu verwenden, müssen Sie das Datenimportertool mit dem Befehlszeilenparameter *-CollectionMappingFile* und dem vollständigen Pfad zur erstellten CSV-Sammlungszuordnungsdatei starten. Beispiel:

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]
> Der Datenimporter zeigt keine Assistentenseiten an, die darauf hinweisen, dass die Sammlungszuordnungsdatei geladen wurde. Das Tool zeigt jedoch die beim Lesen der CSV-Datei gefundenen Fehler an. Darüber hinaus können Sie auf der Seite **Summary** (Zusammenfassung) des Assistenten die **Deployment types** (Bereitstellungstypen) überprüfen. Das Tool zeigt **Yes** (Ja) in der Spalte „Importable“ (Importierbar) an und listet die Azure AD-Gruppen auf, die es Objekten in der Spalte **Notes** (Hinweise) zuweist.

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Phase 1: Ermitteln von Configuration Manager-Objekten und Sammeln von Daten
In Phase 1 wählen Sie die zu ermittelnden Objekte aus und lassen das Tool Informationen zu den ausgewählten Objekten sammeln. 
1. Öffnen Sie das Tool, und klicken Sie auf **Start** (Starten).  
2. Lesen Sie die Informationen, und klicken Sie dann auf **Next** (Weiter). 
3. Wählen Sie aus, ob ein zuvor exportiertes Dataset importiert werden soll, oder wählen Sie die zu importierenden Objekttypen aus:
   - **Import previously exported data set** (Zuvor exportiertes Dataset importieren): Wählen Sie **Import data set exported from a previous run of Intune Data Importer** (Aus einer vorherigen Ausführung des Intune-Datenimporters exportiertes Dataset importieren), und klicken Sie unter **Exported data folder** (Exportierter Datenordner) auf **Browse** (Durchsuchen), um ein mit dem Datenimportertool zuvor exportiertes Dataset auszuwählen. Der Benutzer, der das Dataset importiert, muss derselbe Benutzer sein, der die Daten exportiert hat. Nach dem Import der Daten wird auf der Seite **Summary** (Zusammenfassung) des Assistenten eine Zusammenfassung der Objekte aufgelistet. Wenn die Zusammenfassung korrekt aussieht, springen Sie zu [Phase 3: Importieren ausgewählter Objekte in Intune](phase-3:-import-selected-object-to-intune).
 
      > [!Note]
      > Nachdem Sie die zu importierenden Objekte auf Ihrer Website ermittelt und ausgewählt haben, können Sie die Objekte in ein Dataset auf der Seite **Sign-in to Intune** (Bei Intune anmelden) des Assistenten exportieren. Anschließend können Sie das Dataset auf dieser Seite importieren. Da das Dataset mit den Windows-Benutzeranmeldeinformationen des angemeldeten Benutzers verschlüsselt ist, kann nur der Benutzer, der das Dataset exportiert hat, das Dataset in das Tool importieren. 
   - **Select object types to import** (Zu importierende Objekttypen auswählen): Wählen Sie **Select object types to import** (Zu importierende Objekttypen auswählen), um die zu importierenden Objekttypen auszuwählen und Objekte in Ihrer Umgebung zu ermitteln. Geben Sie die folgenden Informationen über Ihren Website und die Objekte an, die Sie importieren möchten.
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
 <!--   > [!Tip]     
    > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
    > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
    > - Objects are always grouped under their parent item even when you sort or filter the objects.
-->
6.  Sortieren Sie auf jeder Seite zur Elementauswahl die Objekte nach der Spalte „Importable“ (Importierbar), und überprüfen Sie die Objekte, die nicht importierbar sind. Die Informationen in der Spalte „Notes“ (Hinweise) geben Auskunft darüber, warum das Tool das Objekt nicht importieren kann. 
7.  Nun müssen Sie entscheiden, ob Sie die Probleme für nicht importierbare Objekte beheben möchten. Nachdem Sie ein oder mehrere Probleme behoben haben, klicken Sie auf „Previous“ (Zurück), bis Sie zur Seite „Select data from Configuration Manager“ (Daten aus Configuration auswählen) gelangen. Sammeln Sie dann die Daten erneut, um zu prüfen, ob das Problem behoben wurde. Sie können die Fehlerbehebung so lange fortsetzen, bis Sie mit den importierbaren Objekten zufrieden sind. 
8.  Wählen Sie auf jeder Elementauswahlseite die Objekte aus, die Sie importieren möchten. Die folgenden Spalten werden aufgeführt:
    - **Name**: Name des Configuration Manager-Objekts. 
    - **Importable** (Importierbar): Gibt an, ob ein Objekt importiert werden kann. Sie können nur Objekte auswählen, bei denen „Yes“ (Ja) in der Spalte „Importable“ (Importierbar) enthalten ist. 
    - **Platform** (Plattform): Gibt die vom Objekt unterstützte Plattform an.
    - **Already imported** (Bereits importiert): Gibt an, ob das Objekt bereits mit dem Tool auf diesem Computer importiert wurde. 
    - **Is superseded** (Ist abgelöst, für Apps): Gibt an, ob die App durch eine andere App abgelöst wird. Sie müssen oben auf der Seite das Kontrollkästchen **Show superseded apps** (Abgelöste Apps anzeigen) aktivieren, damit die abgelösten Apps angezeigt werden.
    - **Notes** (Hinweise): Bietet Informationen, warum ein Objekt nicht importiert werden kann. Die Spalte **Notes** (Hinweise) enthält auch Informationen über Einstellungen, die (bei einigen Objekttypen) ignoriert wurden, wobei das Objekt nach wie vor ohne diese Einstellungen importiert werden kann.
    - **Configuration baselines** (Konfigurationsbaselines) (für Konfigurationselemente): Gibt die Konfigurationsbaselines an, die einem Konfigurationselement zugeordnet sind.
    - **Required certificate** (Erforderliches Zertifikat) (für Profile und Richtlinien): Gibt an, ob dem Objekt ein Zertifikat zugeordnet ist. Wenn dem Objekt ein Zertifikat zugeordnet ist, müssen Sie auch das Zertifikat importieren.
9.  Nachdem Sie die zu importierenden Objekte ausgewählt haben, werden sie auf der Seite „Summary“ (Zusammenfassung) aufgelistet. Die folgenden Aktionen sind verfügbar: 
    - **Export details** (Details exportieren): Erstellt eine CSV-Datei, die die auf dem Bildschirm angezeigten Informationen enthält. Zudem werden nicht importierbare Objekte sowie die Gründe hierfür angegeben. Sie können diese Datei zur Bezugnahme aufbewahren. 
    - **Export error data** (Fehlerdaten exportieren): Exportiert eine komprimierte Datei, die Informationen zu den Daten enthält, die das Tool nicht konvertieren oder importieren konnte. 

### <a name="phase-3-import-selected-objects-to-intune"></a>Phase 3: Importieren ausgewählter Objekte in Intune
In Phase 3 melden Sie sich bei Intune an und importieren die ausgewählten Objekte. 
10. Klicken Sie auf **Next** (Weiter) und dann auf **Sign in to Intune** (Bei Intune anmelden), um sich für den Datenimport beim Intune-Mandanten anzumelden, oder wählen Sie die zu exportierenden Daten aus.

    - **Export** (Exportieren): Nachdem Sie die zu importierenden Objekte auf Ihrer Website ermittelt und ausgewählt haben, können Sie die Objekte in ein Dataset exportieren. Dadurch können Sie Objekte über einen Computer ohne Internetzugriff ermitteln, die Daten exportieren und diese dann auf einen Computer mit Internetzugriff importieren. Da das Dataset mit den Windows-Benutzeranmeldeinformationen des angemeldeten Benutzers verschlüsselt ist, kann nur der Benutzer, der das Dataset exportiert hat, das Dataset in das Tool importieren. Wenn Sie diese Option wählen, wählen Sie den Pfad zu den exportierten Daten aus. 
      1. Klicken Sie auf der Seite **Sign in to Intune** (Bei Intune anmelden) auf **Export** (Exportieren). 
      2. Klicken Sie auf **Browse** (Durchsuchen), um den Zielordner für den Export auswählen. Der Ordner muss leer sein. 
      3. Klicken Sie auf **Start** (Starten), um die Daten zu exportieren. Klicken Sie bei Abschluss des Exportvorgangs auf **Close** (Schließen), um den Assistenten abzuschließen und den Datenimporter zu schließen.
      4. Starten Sie den Datenimporter auf einem anderen Computer mit Internetzugriff unter Verwendung der gleichen Anmeldeinformationen, und wählen Sie auf der zweiten Seite des Assistenten **Import previously exported data set** (Zuvor exportiertes Dataset importieren) aus. Nachdem die Daten importiert wurden, leitet Sie der Assistent zur Seite **Sign in to Intune** (Bei Intune anmelden) weiter. 
    - **Sign in to Intune** (Bei Intune anmelden): Sie müssen sich mit dem Konto eines globalen Administrators oder Intune-Administrators anmelden. Nachdem Sie sich angemeldet haben, wird der Importvorgang gestartet.
    
      > [!Important]
      > Wir empfehlen, den Datenimportprozess zunächst mit einem Testmandanten zu testen. Nachdem Sie bestätigt haben, dass die von Ihnen erwarteten Daten importiert wurden, können Sie den gleichen Prozess mit Ihrem Intune-Mandanten in der Produktionsumgebung durchlaufen.
12. Die Seite „Status“ zeigt den Status an, während die Objekte importiert werden. Klicken Sie auf **Next** (Weiter), wenn der Import abgeschlossen ist. 
13. Auf der Seite „Completion“ (Abschluss) sind die importierten Objekte aufgeführt. Überprüfen Sie den Status aller Objekte, bei denen während des Importvorgangs ein Fehler aufgetreten ist. Die folgenden Aktionen sind verfügbar: 
    - **Export details** (Details exportieren): Erstellt eine CSV-Datei, die die auf dem Bildschirm angezeigten Informationen enthält. Sie können diese Datei zur Bezugnahme aufbewahren. 
    - **Export error data** (Fehlerdaten exportieren): Exportiert eine komprimierte Datei, die Informationen zu den Daten enthält, die das Tool nicht konvertieren oder importieren konnte.

## <a name="next-steps"></a>Nächste Schritte
Nachdem Sie die Daten in Intune importiert haben, müssen Sie Schritte unternehmen, um [ Intune für die Benutzermigration vorzubereiten](migrate-prepare-intune.md). 