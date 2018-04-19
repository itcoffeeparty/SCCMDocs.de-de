---
title: Installieren und Konfigurieren der Security Content Automation Protocol-Erweiterungen (SCAP)
titleSuffix: System Center Configuration Manager
description: Installieren und Konfigurieren der Security Content Automation Protocol-Erweiterungen (SCAP)
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 03fc9fa9f82aeae8ab22d6b4c3fa7858e93401cc
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-configure-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Installieren und Konfigurieren der SCAP-Erweiterungen für Microsoft System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Dieses Feature wurde erstmals in Technical Preview Version 1803 als [Vorabfeature](/sccm/core/servers/manage/pre-release-features) eingeführt. Diese Vorabversion der SCAP-Erweiterungen kann unter allen derzeit unterstützten Versionen von Configuration Manager Current Branch und LTSB 1606 installiert werden. Die Installationsdatei befindet sich unter cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi ab Technical Preview Version 1803.   

Nachdem Sie die erforderliche Infrastruktur vorbereitet haben, können Sie die SCAP-Erweiterungen für Microsoft System Center Configuration Manager auf dem Computer installieren und konfigurieren, von dem aus Sie diesen Vorgang ausführen möchten.

## <a name="install-scap-extensions-configuration-manager"></a>Installieren der SCAP-Erweiterungen für Configuration Manager

1. Führen Sie ConfigMgr\_Extensions\_for\_SCAP.msi aus, um das Tool zu installieren.
2. Wechseln Sie in Windows Explorer zum Ordner, in den Sie die **ConfigMgr\_Extensions\_for\_SCAP.msi**-Datei heruntergeladen haben, und doppelklicken Sie dann auf die **ConfigMgr\_Extensions\_for\_SCAP.msi**-Datei. Somit wird der Assistent zum Installieren der SCAP-Erweiterungen für Microsoft System Center Configuration Manager gestartet.

Führen Sie den **Assistenten zum Installieren der SCAP-Erweiterungen für Microsoft System Center Configuration Manager** anhand der Informationen in der folgenden Tabelle aus. Übernehmen Sie dabei die Standardwerte im Assistenten, sofern Sie diese nicht angeben müssen.

**Tabelle 1.0** Der Assistent zum Installieren der SCAP-Erweiterungen für Microsoft System Center Configuration Manager

| Name der Assistentenseite | Benutzeraktion |
| --- | --- |
| Willkommen und Endbenutzer-Lizenzvertrag |1. Lesen Sie den Lizenzvertrag|
| Willkommen und Endbenutzer-Lizenzvertrag|2. Klicken Sie auf **Ich stimme den Bedingungen des Lizenzvertrags zu**.|
| Willkommen und Endbenutzer-Lizenzvertrag|3. Klicken Sie auf **Installieren**.|
| Assistent zum Installieren der SCAP-Erweiterungen für Microsoft System Center Configuration Manager ist abgeschlossen |4. Klicken Sie auf **Fertig stellen**.|
 



Der Assistent zum Installieren der SCAP-Erweiterungen für Microsoft System Center Configuration Manager installiert die Erweiterungen standardmäßig im Installationsordner der Configuration Manager-Konsole.



## <a name="download-and-install-the-scap-data-stream-files"></a>Herunterladen und Installieren der SCAP-Datenstromdateien

Bevor Sie die SCAP-Erweiterungen ausführen können, um SCAP-Datenstromdateien zu konvertieren und anschließend in das Feature für Konformitätseinstellungen zu importieren, müssen Sie die SCAP-Datenstromdateien von der [Downloadseite](http://nvd.nist.gov/fdcc/download_fdcc.cfm) der NVD-Website (National Vulnerability Database) herunterladen. Anschließend kopieren Sie die Dateien in den Ordner, in dem Sie die SCAP-Erweiterungen installiert haben.

Je nach Umgebung sind möglicherweise nicht alle SCAP-Datenstromdateien erforderlich, die auf der Downloadseite aufgelistet sind.

So installieren Sie die SCAP-Datenströme

1. Rufen Sie die [NVD-Website](http://nvd.nist.gov/) auf, um die SCAP-Datenströme zu ermitteln, die von Ihrer Organisation benötigt werden.
Die von NIST veröffentlichten SCAP-Datenströme sind in mehreren Paketen angeordnet, die auch _Checklisten_ genannt werden.

2. Laden Sie die SCAP-Datenströme von der [NVD-Website](http://nvd.nist.gov/home.cfm) herunter. Diese sind in komprimierten Dateien mit der Dateinamenerweiterung „.zip“ gespeichert oder als DataStream-XML-Datei gekennzeichnet.

    >[!IMPORTANT] 
    >Es gibt eine Vielzahl von SCAP-Datenstromdateien mit der Erweiterung ".xml", die Sie von NVD herunterladen können. Allerdings sind nur XML-Dateien mit Inhalten des Typs XCCDF (SCAP1.0 und 1.1)/DataStream (SCAP1.2) zur Verwendung mit den SCAP-Erweiterungen geeignet.

3. Extrahieren Sie die ZIP-Dateien/DataStream-XML-Dateien für SCAP-Datenströme, die Sie in denselben Ordner heruntergeladen haben, in dem die SCAP-Erweiterungen installiert sind.

## <a name="convert-and-import-the-scap-data-stream-files-using-the-import-scap-content-wizard"></a>Konvertieren und Importieren der SCAP-Datenstromdateien mithilfe des Installationsassistenten für SCAP-Inhalt

Nach Eingang der SCAP-Datenströme sind Sie zum Importieren und Konvertieren der Datenströme in Konfigurationsbaselines bereit. Die von NIST veröffentlichten SCAP-Datenströme sind in mehreren Paketen angeordnet. Folgen Sie den Anweisungen von NIST&#39;s, um zu prüfen, welche Pakete in Ihrer Umgebung zu verwenden sind. Es gibt z.B. ein separates Paket für jede Windows-Version, ein weiteres versionsspezifisches Paket für die Firewallkonfiguration und ein Paket für Internet Explorer 8.0. Führen Sie für diese Aufgabe die folgenden Verfahren aus.

### <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>So importieren Sie die SCAP-Datenströme in Configuration Manager

1. Starten Sie den Assistenten zum Import von SCAP-Inhalt aus dem Menüband der Konfigurationsbaseline.

     ![Starten Sie den Assistenten zum Import von SCAP-Inhalt aus dem CI-Baseline-Menüband](./media/import-scap-content.png)

2. Wählen Sie den Inhaltstyp aus.

      ![Wählen Sie den Inhaltstyp aus](./media/import-new-scap-content.png)

3. Wählen Sie die SCAP-Datenstromdatei, XCCDF und CPE-Wörterbuchdatei oder die Oval-Inhaltsdatei aus.

     ![Wählen Sie die SCAP-Datenstromdatei aus](./media/select-datastream-file.png)

4. Wenn SCAP 1.2 den Datenstrom auswählt. Wählen Sie dann den Vergleichstest und das Profil für SCAP 1.x aus.  Wählen Sie **Weiter** aus, um den Inhalt zu konvertieren. Daraufhin wird eine Statusanzeige angezeigt.

      ![Wählen Sie dann den Vergleichstest und das Profil für SCAP 1.2 aus.](./media/select-benchmark-and-profile.png)

5. Bestätigen Sie die zu importierenden Konfigurationsdaten.

      ![Bestätigen Sie den Screenshot der Konfiguration](./media/confirm-configuration.png)

6. Klicken Sie auf **Weiter**, um die Konfigurationsdaten zu importieren.

      ![Import abschließen](./media/complete-import.png)

## <a name="alternate-method-convert-and-import-the-scap-data-stream-files-using-the-cmd-line-tool"></a>(Alternative Methode) Konvertieren und Importieren der SCAP-Datenstromdateien mithilfe des cmd-Befehlszeilentools

Nach dem Erhalt der SCAP-Datenströme können Sie das „Microsoft.Sces.ScapToDcm.exe“-Tool verwenden, um die SCAP-Datenströme in konforme CAB-Dateien für Konformitätseinstellungen zu konvertieren. Importieren Sie dann die CAB-Datei in Configuration Manager. Mit dem Tool „Microsoft.Sces.ScapToDcm.exe“ werden die SCAP-Datenströme in Konfigurationselemente und Konfigurationsbaselines konvertiert, auf die Sie mithilfe des Features für Konformitätseinstellungen in Configuration Manager zugreifen können. Das „Microsoft.Sces.ScapToDcm.exe“-Tool konvertiert die SCAP-Datenströme in XML-Manifeste. Anschließend packt es die XML-Manifeste in eine CAB-Datei, die Sie in Configuration Manager importieren können.

Die von NIST veröffentlichten SCAP-Datenströme sind in mehreren Paketen angeordnet. Folgen Sie den Anweisungen von NIST&#39;s, um zu prüfen, welche Pakete in Ihrer Umgebung zu verwenden sind. Es gibt z.B. ein separates Paket für jede Windows-Version, ein weiteres versionsspezifisches Paket für die Firewallkonfiguration und ein Paket für Internet Explorer 8.0. Führen Sie für diese Aufgabe die folgenden Verfahren aus.





## <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>So importieren Sie die SCAP-Datenströme in Configuration Manager

1. Konvertieren Sie die SCAP-Datenströme in eine kompatible CAB-Datei für Kompatibilitätseinstellungen.
2. Importieren Sie die CAB-Datei in Configuration Manager.

### <a name="convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files"></a>Konvertieren der SCAP-Datenströme in konforme CAB-Dateien für Konformitätseinstellungen

Bevor Sie die Konformität Ihrer Systeme analysieren und bewerten können, müssen Sie die SCAP-Datenströme im XML-Format in XML-Manifeste konvertieren, die mit den Konfigurationselementen und Konfigurationsbasislinien für Konformitätseinstellungen konform sind. Das „Microsoft.Sces.ScapToDcm.exe“-Tool konvertiert die SCAP-Datenströme in XML-Manifeste. Anschließend packt es die XML-Manifeste in eine CAB-Datei, die Sie später in Configuration Manager importieren können.

#### <a name="to-convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files-using-the-microsoftscesscaptodcmexe-tool"></a>**So konvertieren Sie die SCAP-Datenströme mithilfe des Tools „Microsoft.Sces.ScapToDcm.exe“ in konforme CAB-Dateien für Konformitätseinstellungen**

Navigieren Sie in der Eingabeaufforderung zum Ordner AdminConsole\Bin, führen Sie „Microsoft.Sces.ScapToDcm.exe“ aus, um eine konforme CAB-Datei für Konformitätseinstellungen zu generieren und im Configuration Manager-Standort zu importieren.

   >[!NOTE] 
   > Ihr Konto muss über Lese-/Schreibberechtigungen für den Ausgabeordner verfügen.

**Bei SCAP 1.0/1.1-Inhalt (XCCDF-XML-Datei, z.B. USGCB- und DISA-Inhalt):**

 Microsoft.Sces.ScapToDcm.exe –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt; -out &lt;Ausgabeordner&gt; [-select benchmark/profile] [-log Protokolldateiname]

   >[!NOTE] 
   >Wenn Sie den Parameter „-select“ nicht zum Angeben von Benchmark/Profil verwenden, generiert das Tool eine DCM-CAB-Datei für jede Testversion in der Inhaltsdatei.

**Bei SCAP 1.2-Inhalt (DataStream-XML-Datei, z.B. der neueste USGCB-Inhalt):**

Microsoft.Sces.ScapToDcm.exe –scap &lt;scapdatastreamfile.xml&gt; -out &lt;Ausgabeordner&gt; [-select datastream/benchmark/profile] [-log Protokolldateiname]

   >[!NOTE] 
   > Wenn Sie den Parameter „-select“ nicht zum Angeben von Datenstrom/Benchmark/Profil verwenden, generiert das Tool eine DCM-CAB-Datei für jede Testversion in der Inhaltsdatei.

**Bei einzelner OVAL-Datei mit externen Variablen:**

Microsoft.Sces.ScapToDcm.exe –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;] -out &lt;Ausgabeordner&gt; [-log Protokolldateiname]

   >[!NOTE] 
   > Wenn mehrere Werte für eine Variable in der externen Variablendatei enthalten sind, behandelt das Tool „Microsoft.Sces.ScapToDcm.exe“ die Werte als ein Array für diese Variable.



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Microsoft.Sces.ScapToDcm.exe. Befehlszeilenparameter

| **Parameter** | **Verwendung** | **Erforderlich** |
| --- | --- | --- |
| -scap [SCAP-Datenstromdatei] | Angeben der SCAP-Datenstromdatei | Ja (für SCAP 1.2-Datenstrom, schließt sich mit „-xccdf“ und „-oval“/„-variable“ gegenseitig aus) |
| -xccdf [XCCDF-Datei] | Angeben der XCCDF-Datei | Ja (für SCAP 1.0/1.1-XCCDF, schließt sich mit „-scap“ und „-oval“/„-variable“ gegenseitig aus) |
| -Cpe [Cpe-Datei] | Angeben der CPE-Datei | Ja (für SCAP 1.0/1.1-XCCDF, schließt sich mit „-scap“ und „-oval“/„-variable“ gegenseitig aus) |
| -oval [OVAL-Datei] | Angeben der OVAL-Datei | Ja (für eigenständige OVAL-Datei, schließt sich mit „-xccdf“ und „-scap“ gegenseitig aus) |
| -variable [externe OVAL-Variablendatei] | Angeben der externen OVAL-Variablendatei | Nein (optional für eigenständige OVAL-Datei, wenn eine externe OVAL-Variablendatei vorhanden ist, schließt sich mit „-xccdf“ und „-scap“ gegenseitig aus) |
| -select [XCCDF-Benchmark/Profil] | Auswählen von XCCDF-Benchmark/Profil aus der SCAP-Datenstromdatei oder XCCDF-Datei | Nein (Es wird empfohlen, diese Option anzugeben. Ist das nicht der Fall, generiert das Tool eine CAB-Datei für alle Profile in allen eingebetteten DataStream/Benchmarks.) |
| -out [Ausgabeverzeichnis] | Angeben eines Speicherorts für die DCM-CAB-Dateiausgabe | Nein (Wenn kein Wert angegeben wird, listet das Tool nur den Inhalt ohne Konvertierung auf.) |
| -log [Protokolldatei] | Angeben der Protokolldatei | Nein (wenn kein Wert angegeben wird, wird das Protokoll in die „Microsoft.Sces.ScapToDcm.log“-Datei geschrieben) |
| -help / -? | Ausgeben der Toolverwendung | Nein |





#### <a name="the-following-command-lines-are-samples-for-the-microsoftscesscaptodcmexe-tool"></a>Die folgenden Befehlszeilen sind Beispiele für das „Microsoft.Sces.ScapToDcm.exe“-Tool:

**SCAP1.2-Inhalt:**

  Microsoft.Sces.ScapToDcm.exe –scap scap\_gov.nist\_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID

**SCAP1.0/1.1-Inhalt:**

   Microsoft.Sces.ScapToDcm.exe–xccdf scap\_gov.nist\_Test-WinXP\_xccdf.xml –cpe scap\_gov.nist\_Test-WinXP\_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID

**SCAP OVAL-Inhalt:**

  Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder

**Die folgende Ausgabe ist eine Stichprobe des „Microsoft.Sces.ScapToDcm.exe“-Tools:**

  Kompatible CAB-Datei für Konformitätseinstellungen erstellt:

  Überprüfen Sie das Schema der SCAP-Datenstromdatei C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Überprüfen Sie das Schema der SCAP-Datenstromdatei erfolgreich C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Process XCCDF Benchmark xccdf\_tst.bvt\_benchmark\_Windows-F

  Verarbeiten Sie das XCCDF-Profil: xccdf\_tst.bvt\_profile\_version\_1.0.0.0-BVT Profile #1

  Verarbeiten Sie OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  OVAL-Prozess erfolgreich abgeschlossen: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Verarbeiten Sie OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml

  OVAL-Prozess erfolgreich abgeschlossen: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml Process SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip SCAP Data Stream: [scap\_tst.bvt\_datastream\_Windows-F.zip]

  Version:        [1.2]

  Zeitstempel:      [2/24/2012]

  Anwendungsfall:       [CONFIGURATION]

  CPE-Wörterbuch:  [scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml] Produktname:    [National Institute of Standards and Technology]

  Produktversion: []

  Schemaversion:  [5.3]

  Zeitstempel:       [2/24/2012]

  XCCDF-Benchmark: [xccdf\_tst.bvt\_benchmark\_Windows-F]

  Version:       [v1.0.0.0] Update:        [http://usgcb.nist.gov]

  Zeitstempel:     [2/24/2012]

  Status:        [accepted]

  Stichtag:   [2/24/2012]

  Titel:         [Ohh New BVT for SCAP 1.2]

 Beschreibung:   [My description]

  XCCDF-Profil: [xccdf\_tst.bvt\_profile\_version\_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Produktname:    [scaptool]

   Produktversion: []

   Schemaversion:  [5.4]

   Zeitstempel:       [2/24/2012]

  Starten Sie die SCAP-DCM-Konvertierung...

  Verarbeiten Sie SCAP-Datenströme: „scap\_tst.bvt\_datastream\_Windows-F.zip“

  Verarbeiten Sie das CPE-Wörterbuch: „scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml“

  …

  Generieren von CI-Baseline-CAB-Dateien: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Erfolgreiches Generieren von CI-Baseline-CAB-Dateien: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Erfolgreiches Konvertieren von XCCDF-Profilen: xccdf\_tst.bvt\_profile\_version\_1.0.0.0 into DCM baseline xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

## <a name="next-step"></a>Nächste Schritte
> [!div class="nextstepaction"]
> [Import SCAP compliance settings and export compliance results (Importieren von SCAP-Kompatibilitätseinstellungen und Exportieren von Kompatibilitätsergebnissen)](/sccm/compliance/plan-design/scap/import-scap-compliance-settings)
