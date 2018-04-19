---
title: Importieren von SCAP-Kompatibilitätseinstellungen
titleSuffix: System Center Configuration Manager
description: Importieren von SCAP-Kompatibilitätseinstellungen als Konfigurationsbaselines und Exportieren der Ergebnisse
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 5863f8b9a79e8e22e215e9feac7744b4a6ce279d
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="import-the-compliance-settings-compliant-cab-files-into-system-center-configuration-manager"></a>Importieren der konformen CAB-Dateien für Konformitätseinstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Dieses Feature wurde erstmals in Technical Preview Version 1803 als [Vorabfeature](/sccm/core/servers/manage/pre-release-features) eingeführt. Diese Vorabversion der SCAP-Erweiterungen kann unter allen derzeit unterstützten Versionen von Configuration Manager Current Branch und LTSB 1606 installiert werden. Die Installationsdatei befindet sich unter cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi ab Technical Preview Version 1803. 

Im nächsten Schritt wird die Configuration Manager-Konsole verwendet, um die konformen CAB-Dateien für Konformitätseinstellungen in Configuration Manager zu importieren. Wenn Sie die zuvor erstellten CAB-Dateien importieren, werden ein oder mehrere Konfigurationselemente und Konfigurationsbasislinien in der Configuration Manager-Datenbank erstellt. Später können Sie die einzelnen Konfigurationsbasislinien einer Computersammlung in Configuration Manager zuweisen.

## <a name="to-import-the-compliance-settings-compliant-cab-files-into-configuration-manager"></a>So importieren Sie die konformen CAB-Dateien für Konformitätseinstellungen in Configuration Manager

1. Öffnen Sie die **Configuration Manager-Konsole**.
2. Wechseln Sie in der **Configuration Manager-Konsole im Navigationsbereich zu **Bestand und Kompatibilität**> **Konformitätseinstellungen** > **Konfigurationsbaselines**.

3. Klicken Sie im Aktionsbereich auf **Konfigurationsdaten importieren**, um den Assistenten zum Importieren von Konfigurationsdaten zu starten.

1. Führen Sie den **Assistenten zum Importieren von Konfigurationsdaten** anhand der Informationen in der folgenden Tabelle aus. Sofern nicht anders angegeben, übernehmen Sie die Standardwerte.



Vorgänge des Assistenten zum Importieren von Konfigurationsdaten

| Name der Assistentenseite | Benutzeraktion |
| --- | --- |
| **Dateien auswählen** |1. Klicken Sie auf **Hinzufügen**. </br>Das Dialogfeld "Öffnen" wird angezeigt.|
||2. Navigieren Sie im Dialogfeld **Öffnen** zum **&lt;Kompatible CAB-Ausgabe\_Ordner&gt;**. Klicken Sie auf die **&lt; kompatible\_CAB&gt;**.cab-Datei, wobei der _kompatible CAB **Ausgabe\_Ordner** der Ordner ist, der nach dem –output-Parameter angegeben wurde, wenn Sie das Tool „Sces.ScapToDcm.exe“ ausführen. **kompatible\_Datei** ist der Name einer CAB-Datei, die Sie zuvor in diesem Prozess erstellt haben. Klicken Sie dann auf **Öffnen**. </br> Das Dialogfeld "Configuration Manager-Konsole – Sicherheitswarnung" wird angezeigt.|
||3. Klicken Sie im Dialogfeld **Configuration Manager-Konsole – Sicherheitswarnung** auf **Ausführen**. Auf der Seite "Dateien auswählen" werden die Konfigurationsdaten in der Liste der zu importierenden Basislinien angezeigt.|
||3. Klicken Sie auf **Weiter**.|
| **Zusammenfassung** |5. Klicken Sie auf **Weiter**. |
| **Assistent zum Importieren von Konfigurationsdaten abschließen** |6. Klicken Sie auf **Schließen**. |

Die neue Konfigurationsbasislinie wird im Informationsbereich der Configuration Manager-Konsole angezeigt.

>[!IMPORTANT]
> Sie müssen diesen Vorgang für jede zuvor erstellte CAB-Datei wiederholen. Für jedes ausgewählte Profil in der XCCDF/DataStream-XML-Datei, die Sie von der NVD-Website heruntergeladen haben, ist eine CAB-Datei vorhanden, die Sie durch Ausführen des Tools „Microsoft.Sces.ScapToDcm.exe“ verarbeiten können.

Die importierte Konfigurationsbaseline ist schreibgeschützt und weist den Status &#39;Aktiviert&#39; sowie den anfänglichen Bereitstellungsstatus &#39;Nein&#39; auf.  Die Eigenschaft &#39;Änderungsdatum&#39; gibt den Zeitpunkt an, zu dem die Baseline importiert wurde.  Der Name der Konfigurationsbaseline stammt aus dem Anzeigenamenbereich der XCCDF/DataStream-XML-Datei. Der Name wird mithilfe der folgenden Konvention erstellt:

ABC[XYZ]. Dabei steht ABC für die XCCDF-Benchmark-ID und XYZ für die XCCDF-Profil-ID (wenn ein Profil ausgewählt ist).



## <a name="assign-configuration-baselines-to-the-computer-collections"></a>Zuweisen von Konfigurationsbaselines zu Computersammlungen

Nachdem Sie die entsprechenden Computersammlungen für die Computer erstellt haben, die hinsichtlich der SCAP-Konformität bewertet werden sollen, können Sie die Konfigurationsbaselines zuweisen, die Sie zum Verknüpfen mit den Computersammlungen importiert haben. Dieser Abschnitt enthält Informationen zum Zuweisen einer Konfigurationsbasislinie zu einer Computersammlung mithilfe der Configuration Manager-Konsole.

So weisen Sie einer Computersammlung eine Konfigurationsbaseline zu:

1. Öffnen Sie die **Configuration Manager**-**Konsole**.

2. Wechseln Sie in der **Configuration Manager-Konsole im Navigationsbereich zu **Bestand und Kompatibilität** > **Konformitätseinstellungen** >**Konfigurationsbaselines**.
3. Klicken Sie im Navigationsbereich auf &lt; **configuration\_baseline>. Dabei ist &lt;_configuration\_baseline&gt;_ der Name der Konfigurationsbaseline, die einer Computersammlung zugewiesen werden soll.

    Die Liste der Konfigurationselemente für die Konfigurationsbasislinie wird im Informationsbereich von Configuration Manager angezeigt.

4. Klicken Sie im Aktionsbereich auf **Bereitstellen**.

5. Füllen Sie das **Dialogfeld** **Bereitstellen** **Konfigurationsbaseline bereitstellen** anhand der Informationen in der folgenden Tabelle aus. Sofern nicht anders angegeben, übernehmen Sie die Standardwerte.

### <a name="deploy-configuration-baseline-dialog-process"></a>Dialogfeld „Konfigurationsbaseline bereitstellen“

| Name der Assistentenseite | Benutzeraktion |
| --- | --- |
| **Sammlung auswählen** | 1. Klicken Sie auf **Durchsuchen**.|
||2. Wählen Sie im Dialogfeld **Sammlung auswählen** **Gerätesammlungen** aus. Klicken Sie dann auf **&lt;computer\_collection&gt;**, wobei &lt;_computer\_collection&gt;_ der Name der Computersammlung ist, die Sie zuvor erstellt haben. Klicken Sie auf **OK**.|
| **Zeitplan festlegen** |3. Wählen Sie den für Ihre Organisation geeigneten Zeitplan aus.|
 
>[!IMPORTANT]
> Wiederholen Sie diesen Vorgang für jede Computersammlung, die Sie den einzelnen Konfigurationsbasislinien zuweisen möchten. Als Mindestvoraussetzung weisen Sie jede Konfigurationsbasislinie mindestens einer Computersammlung zu.

## <a name="verify-that-the-compliance-data-has-been-collected"></a>Sicherstellen, dass die Konformitätsdaten erfasst wurden

Bevor Sie die Konformitätsdaten wieder in das SCAP-Format exportieren, müssen Sie sicherstellen, dass die Daten erfasst wurden. Nachdem Sie einer Computersammlung eine Konfigurationsbasislinie zugewiesen haben, sammelt der Configuration Manager-Client auf jedem Computer in der Sammlung automatisch die Kompatibilitätsinformationen. Anschließend werden die Kompatibilitätsinformationen in der Configuration Manager-Datenbank gespeichert.

Sie zeigen den Bereitstellungsstatus der Konfigurationsbasislinie in Configuration Manager an, um sicherzustellen, dass die entsprechenden Daten von den Configuration Manager-Clients gesammelt wurden. Es muss sichergestellt werden, dass die jeweiligen Konformitätsdaten in Configuration Manager gesammelt wurden, da dies beim Überprüfen der später zu erstellenden XCCDF/DataStream-Ergebnisdateien hilfreich sein kann.



### <a name="verify-that-the-compliance-data-has-been-collected"></a>Sicherstellen, dass die Konformitätsdaten erfasst wurden

1. Öffnen Sie die Configuration Manager-Konsole.
2. Wechseln Sie in der Configuration Manager-Konsole im Navigationsbereich zu **Überwachung** > **Bereitstellungen**.
3. Klicken Sie auf den **Featuretyp**, um den Bereitstellungstyp zu sortieren und nach Elementen des Typs **Baseline** in der Liste zu suchen.
4. Klicken Sie in der Liste mit der rechten Maustaste auf die &lt;configuration\_baseline&gt;, die Sie gerade für die Sammlung bereitgestellt haben, und klicken Sie auf **Status anzeigen**.
5. Wechseln Sie dann zum Knoten &lt;configuration\_baseline&gt;, um den Konformitätsstatus anzuzeigen. Wenn ein Computer einen unbekannten Status aufweist, bedeutet das, dass die Kompatibilitätsdatensammlung für diesen Computer noch nicht abgeschlossen ist.

### <a name="validate-the-xccdfdatastream-results"></a>Überprüfen der XCCDF/Datastream-Ergebnisse

1. Öffnen Sie die Configuration Manager-Konsole.
2. Wechseln Sie in der Configuration Manager-Konsole im Navigationsbereich zu **Konformitätseinstellungen** > **SCAP-Dashboard**.
3. Wählen Sie die Konfigurationsbaseline, Zuweisung, SCAP-Datei, Datastream, Vergleichstest und das Profil (falls anwendbar) aus.
4. Klicken Sie auf **Bericht anzeigen**
 ![SCAP-Bericht](./media/scap-report.png)



## <a name="export-compliance-results-to-scap-format"></a>Exportieren der Konformitätsergebnisse im SCAP-Format

Als Nächstes exportieren Sie die Konformitätsdaten für Konformitätseinstellungen in das SCAP-Format. Dies ist eine ARF-Berichtsdatei in XML-/lesbarem Format. Mit dem Assistenten für den Export der SCAP-Erweiterungen und dem Tool „Microsoft.Sces.DcmToScap.exe“ wird eine separate XCCDF/DataStream-ARF-Ergebnisdatei für jede Konfigurationsbaseline für Konformitätseinstellungen exportiert. Diese Dateien entsprechen den einzelnen XCCDF/DataStream-Eingabedateien, die vom Tool „Microsoft.Sces.ScapToDcm.exe“ verwendet werden, um die einzelnen Konfigurationsbaselines für Konformitätseinstellungen zu erstellen.

### <a name="export-the-compliance-settings-compliance-data-using-the-export-scap-report-wizard"></a>Exportieren der Konformitätsdaten für Konformitätseinstellungen mit dem Assistenten zum Exportieren von SCAP-Berichten

1. Starten Sie den Assistenten zum Exportieren von SCAP-Berichten über einen Klick mit der rechten Maustaste auf dem SCAP-Dashboard.
![Aus dem SCAP-Dashboard importieren](./media/import-from-scap-dashboard.png)

2. Wählen Sie die Konfigurationsbaseline und die Zuweisung ![Baseline auswählen](./media/select-ci-baseline.png) aus

3. Wählen Sie den Speicherort der SCAP-Datenstromdateien, der XCCDF/CPE-Datei oder des Oval-Inhalts und der Variablendateien aus.
![Datastream auswählen](./media/export-scap-report-datastream.png)

4. Geben Sie den Organisationsnamen an, und wählen Sie den Speicherort des Ordners aus, um den SCAP-Bericht zu exportieren.
 ![Datastream auswählen](./media/specify-org-export.png)

5. Überprüfen Sie die Einstellungen.
 ![Datastream auswählen](./media/confirm-export.png)

6. Wählen Sie **Weiter aus, um den Bericht zu exportieren.  Es wird eine Statusanzeige und dann die „Abschluss“-Seite angezeigt.
 ![Export abschließen](./media/complete-report-export.png)



### <a name="alternate-method-export-the-compliance-settings-compliance-data-using-the-microsoftscesdcmtoscapexe-tool"></a>(Alternative Methode) Exportieren Sie die Kompatibilitätsdaten der Konformitätseinstellungen mithilfe des „Microsoft.Sces.DcmToScap.exe“-Tools

1. Wechseln Sie in der Eingabeaufforderung zum Ordner AdminConsole\Bin, geben Sie die Befehlszeilenparameter ein, die in der folgenden Tabelle aufgelistet sind, und drücken Sie dann die **EINGABETASTE:

    >[!NOTE] 
    >Ihr Konto muss über Leseberechtigungen für die Configuration Manager-Anbieter und über Schreibberechtigungen für den Ausgabeordner verfügen, der im Parameter „-out“ der Befehlszeile angegeben ist.

**Bei SCAP 1.0/1.1-Inhalt (z.B. USGCB- und DISA-Inhalt):**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt;  -select &lt;xccdfBenchmark/profile&gt; -out &lt;Ausgabeergebnisordner&gt;  [-log Protokolldateiname]

  >[!NOTE] 
    >Verwenden Sie den Parameter –select zum Angeben von Benchmark/Profil, das auf den Clients bewertet wurde, falls mehrere Angaben für Benchmark/Profil im Inhalt vorhanden sind.

**Bei SCAP 1.2-Inhalt (z.B. der neueste USGCB-Inhalt):**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID  -select &lt;datastream/xccdfBenchmark/profile&gt; -out &lt;Ausgabeergebnisordner&gt;  [-log Protokolldateiname]

   >[!NOTE] 
   >Verwenden Sie den Parameter –select zum Angeben von Datenstrom/Benchmark/Profil, das auf den Clients bewertet wurde, falls mehrere Angaben für Datenstrom/Benchmark/Profil im Inhalt vorhanden sind.

**Bei einzelner OVAL-Datei mit externen Variablen:**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;]  -out &lt;Ausgabeergebnisordner&gt;  [-log Protokolldateiname]

   >[!NOTE] 
    >„Microsoft.Sces.DcmToScap.exe“ generiert nur den Ergebnisbericht der OVAL-Definition für die einzelnen Zielcomputer, der ARF-Bericht wird nicht generiert.

#### <a name="how-to-get-baseline-ci-id-and-assignment-id"></a>Abrufen der ID des Baseline-Konfigurationselements und des Arbeitsauftrags

Klicken Sie in der Verwaltungskonsole auf **Bestand und Kompatibilität** > **Konformitätseinstellungen** > **Konfigurationsbaselines**. Die CI-ID ist die ID des Konfigurationselements der Konfigurationsbaseline.

![Abrufen der ID des Konfigurationselements und des Arbeitsauftrags](./media/get-to-baselines.png)

Wählen Sie die gewünschte Konfigurationsbaseline, klicken Sie auf die Registerkarte „Bereitstellungen“, wenn die Arbeitsauftrags-ID nicht angezeigt wird, klicken Sie mit der rechten Maustaste auf die Spaltenüberschrift, und klicken Sie auf die Arbeitsauftrags-ID, um sie zu aktivieren.
![Abrufen der ID des Konfigurationselements und des Arbeitsauftrags](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>„Microsoft.Sces.DcmToScap.exe“-Befehlszeilenparameter

| **Parameter** | **Verwendung** | **Erforderlich** |
| --- | --- | --- |
| -Baseline [Baseline-CI-ID] | Angeben der Konfigurationsbaseline | Ja |
| -Arbeitsauftrag [Arbeitsauftrags-ID] | Angeben der Bereitstellung der Konfigurationsbaseline | Ja |
| -organization [Organisationsname] | Angeben des Organisationsnamens, der im Bericht angezeigt werden soll. Zur Angabe eines mehrzeiligen Organisationsnamens kann &#39;;&#39; als Trennzeichen verwendet werden. | Nein |
| -type [thin/full/fullnosc] | Angeben des OVAL-Ergebnistyps: eingeschränktes Ergebnis, vollständiges Ergebnis oder vollständiges Ergebnis ohne Systemmerkmal. | Nein (wenn kein Wert angegeben wird, lautet der Standardwert „full“) |
| -scap [SCAP-Datenstromdatei] | Angeben der SCAP-Datenstromdatei | Ja (für SCAP 1.2-Datenstrom, schließt sich mit „-xccdf“ und „-oval“/„-variable“ gegenseitig aus) |
| -xccdf [XCCDF-Datei] | Angeben der XCCDF-Datei | Ja (für SCAP 1.0/1.1-XCCDF, schließt sich mit „-scap“ und „-oval“/„-variable“ gegenseitig aus) |
| -Cpe [Cpe-Datei] | Angeben der CPE-Datei | Ja (für SCAP 1.0/1.1-XCCDF, schließt sich mit „-scap“ und „-oval“/„-variable“ gegenseitig aus) |
| -oval [OVAL-Datei] | Angeben der OVAL-Datei | Ja (für eigenständige OVAL-Datei, schließt sich mit „-xccdf“ und „-scap“ gegenseitig aus) |
| -variable [externe OVAL-Variablendatei] | Angeben der externen OVAL-Variablendatei | Nein (optional für eigenständige OVAL-Datei, wenn eine externe OVAL-Variablendatei vorhanden ist, schließt sich mit „-xccdf“ und „-scap“ gegenseitig aus) |
| -select [XCCDF-Benchmark/Profil] | Auswählen von XCCDF-Benchmark/Profil aus der SCAP-Datenstromdatei oder XCCDF-Datei | Ja (es muss eine Auswahl getroffen werden, damit ein Bericht generiert wird, der mit der entsprechenden DCM-Baseline in der Configuration Manager-Datenbank verglichen werden kann) |
| -out [Ausgabeverzeichnis] | Angeben des Ausgabeorts der CAB-Datei für Konformitätseinstellungen | Nein (wenn kein Wert angegeben wird, listet das Tool nur den Inhalt ohne Konvertierung auf) |
| -log [Protokolldatei] | Angeben der Protokolldatei | Nein (wenn kein Wert angegeben wird, wird das Protokoll in die „Microsoft.Sces.DcmToScap.log“-Datei geschrieben) |
| -help / -? | Ausgeben der Toolverwendung | Nein |



 >[!TIP] 
 >Sie können den Parameter "-?", „-h“ oder „-help“ angeben, um die Syntax des Tools „Microsoft.Sces.DcmToScap.exe“ sowie eine Liste der Parameter anzuzeigen.

Standardmäßig greift das Tool „Microsoft.Sces.DcmToScap.exe“ mit Ihren Anmeldeinformationen auf die Configuration Manager-Datenbank zu. Das Tool „Microsoft.Sces.DcmToScap.exe“ erfordert mindestens Lesezugriff auf die Configuration Manager-Datenbank.

Nachdem Sie überprüft haben, ob der entsprechende **ARF**-Bericht: „_ARF\_xxxx.xml_“ und/oder **lesbare**  Bericht: „xxx.txt“, **Cyberscope**-Bericht: „LASR\_xxx.xml“, **ConsumedOval**-Bericht: „xx-oval-&lt;machineName&gt;.xml“, **XCCDF-Benchmark-Ergebnis**-Bericht: „xccdf\_xxx.xml“-Dateien bestehen, geben Sie in der Befehlszeile „Beenden“ ein, und drücken dann die **EINGABETASTE**, um das Aufgabefenster zu verlassen.

## <a name="next-step"></a>Nächste Schritte
> [!div class="nextstepaction"]
> [Problembehandlung](/sccm/compliance/plan-design/scap/troubleshooting-scap)
