---
title: Anzeigen von Diagnosedaten
titleSuffix: Configuration Manager
description: Zeigen Sie Diagnose- und Nutzungsdaten an, um zu bestätigen, dass die System Center Configuration Manager-Hierarchie keine vertraulichen Informationen enthält.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15e6f84be22d90e937c33ebd3a24520e6832a751
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Informationen zum Anzeigen von Diagnose- und Verwendungsdaten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können in Ihrer System Center Configuration Manager-Hierarchie Diagnose- und Nutzungsdaten anzeigen und überprüfen, um sicherzustellen, dass keine sensiblen oder identifizierbaren Informationen enthalten sind. Telemetriedaten werden zusammengefasst, in der Tabelle **TEL_TelemetryResults** der Standortdatenbank gespeichert und so formatiert, dass sie programmgesteuert und effizient zu verwenden sind. Obwohl Ihnen die folgenden Optionen einen Überblick über die genauen Daten verschaffen, die an Microsoft gesendet werden, sollen diese nicht für andere Zwecke (z.B. zur Datenanalyse) verwendet werden.  

Verwenden Sie den folgenden SQL-Befehl, um den Inhalt dieser Tabelle und die Daten anzuzeigen, die gesendet werden. (Sie können diese Daten auch in eine Textdatei exportieren):  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  Bevor Sie Version 1602 installieren, sind die Telemetriedaten in der Tabelle **TelemetryResults** gespeichert.  

Wenn sich der Dienstverbindungspunkt im Offlinemodus befindet, können Sie die aktuellen Diagnose- und Verwendungsdaten mit dem Dienstverbindungstool in eine Datei mit kommagetrennten Werten (CSV) exportieren. Führen Sie das Dienstverbindungstool auf dem Dienstverbindungspunkt mithilfe des Parameters **-Export** aus.  

##  <a name="bkmk_hashes"></a> Unidirektionale Hashes  
Einige Daten bestehen aus Zeichenfolgen aus zufälligen alphanumerischen Zeichen. Configuration Manager verwendet den SHA-256-Algorithmus, der mit unidirektionalen Hashes sicherstellt, dass keine potentiell sensiblen Daten gesammelt werden. Der Algorithmus belässt Daten in einem Zustand, in dem sie dennoch für Korrelations- und Vergleichszwecke verwendet werden können. Anstatt z. B. die Namen von Tabellen in der Standortdatenbank zu erfassen, wird für jeden Tabellennamen ein unidirektionaler Hash erfasst. Dadurch wird sichergestellt, dass benutzerdefinierte Tabellennamen, die Sie erstellt haben, oder Produkt-Add-Ons von Dritten nicht sichtbar sind. Anschließend können Sie denselben unidirektionalen Hash der standardmäßig im Produkt enthaltenen SQL-Tabellennamen ausführen und die Ergebnisse der beiden Abfragen vergleichen, um die Abweichung Ihres Datenbankschemas von der Standardeinstellung des Produkts zu bestimmen. Das Ergebnis wird anschließend verwendet, um Updates zu verbessern, die Änderungen des SQL-Schemas erforderlich machen.  

Beim Anzeigen der Rohdaten enthält jede Datenzeile einen allgemeinen Hashwert. Dies ist die Hierarchie-ID. Mit diesem Hashwert wird dann sichergestellt, dass die Daten mit der gleichen Hierarchie korreliert werden, ohne den Kunden oder die Quelle zu identifizieren.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Funktionsweise eines unidirektionale Hashs  

1.  Sie rufen Ihre Hierarchie-ID ab, indem Sie die folgende SQL-Anweisung in SQL Management Studio auf die Configuration Manager-Datenbank anwenden: **select [dbo].[fnGetHierarchyID]\(\)**  

2.  Verwenden Sie das folgende Windows PowerShell-Skript zum Anwenden des unidirektionalen Hashs auf die GUID, die aus der Datenbank abgerufen wurde. Sie können dann diesen Wert mit der Hierarchie-ID in den Rohdaten vergleichen, um zu prüfen, wie wir diese Daten maskiert haben.  

    ```  
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)   
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)   
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()    
    # Hash the input   
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)              
    # Base64 encode the result for transport   
    $result = [Convert]::ToBase64String($hashedBytes)    
    return $result   
    ```  
