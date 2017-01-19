---
title: Anzeigen von Diagnosedaten | Microsoft-Dokumentation
description: "Zeigen Sie Diagnose- und Nutzungsdaten an, um zu bestätigen, dass die System Center Configuration Manager-Hierarchie keine vertraulichen Informationen enthält."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 5b5d6b6c176de8acbc1161f6820aa1cc3e9fca49


---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Informationen zum Anzeigen von Diagnose- und Verwendungsdaten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können in Ihrer System Center Configuration Manager-Hierarchie Diagnose- und Nutzungsdaten anzeigen und überprüfen, um sicherzustellen, dass keine sensiblen oder identifizierbaren Informationen enthalten sind. Telemetriedaten werden zusammengefasst, in der Tabelle **TEL_TelemetryResults** der Standortdatenbank gespeichert und so formatiert, dass sie programmgesteuert und effizient zu verwenden sind. Die folgenden Optionen geben Ihnen einen Überblick über die genauen Daten, die an Microsoft gesendet werden. Diese werden nicht für andere Zwecke (z. B. zur Datenanalyse) verwendet.  

Mit dem folgenden SQL-Befehl können Sie den Inhalt dieser Tabelle und die genauen Daten anzeigen, die gesendet werden (Sie können diese Daten auch in eine Textdatei exportieren):  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  Vor der Installation der Version 1602 lautet die Tabelle, in der Telemetriedaten gespeichert werden, **TelemetryResults**.  

Wenn sich der Dienstverbindungspunkt im Offlinemodus befindet, können Sie die aktuellen Diagnose- und Verwendungsdaten mit dem Dienstverbindungstool in eine Datei mit kommagetrennten Werten (CSV) exportieren. Führen Sie das Dienstverbindungstool auf dem Dienstverbindungspunkt mit dem Parameter **-Export** aus.  

##  <a name="a-namebkmkhashesa-one-way-hashes"></a><a name="bkmk_hashes"></a> Unidirektionale Hashes  
Einige der Daten bestehen aus Zeichenfolgen aus zufälligen alphanumerischen Zeichen. Configuration Manager verwendet unidirektionale Hashs unter Verwendung des SHA-256-Algorithmus zum Sicherstellen, dass wir möglicherweise sensible Daten nicht sammeln. Dabei bleiben die Daten in einem Zustand, der ihre Nutzung zu Korrelations- und Vergleichszwecken erlaubt. Anstatt z. B. die Namen von Tabellen in der Standortdatenbank zu erfassen, wird für jeden Tabellennamen ein unidirektionaler Hash erfasst. Dadurch wird sichergestellt, dass keine benutzerdefinierten Tabellennamen sichtbar sind, die von Ihnen oder durch Produkt-Add-Ons von Drittanbietern erstellt wurden. Anschließend kann derselbe unidirektionale Hash der standardmäßig im Produkt enthaltenen SQL-Tabellennamen erstellt und verglichen werden, um die Abweichung Ihres Datenbankschemas gegenüber der Standardeinstellung des Produkts zu bestimmen. Das Ergebnis wird anschließend verwendet, um Updates zu verbessern, die Änderungen des SQL-Schemas erforderlich machen.  

Beim Anzeigen der Rohdaten enthält jede Datenzeile einen allgemeinen Hashwert. Dies ist die Hierarchie-ID. Dieser Hashwert dient zum Sicherstellen, dass die Daten mit der gleichen Hierarchie korreliert werden, ohne den Kunden oder die Quelle zu identifizieren.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Funktionsweise eines unidirektionale Hashs  

1.  Sie rufen Ihre Hierarchie-ID ab, indem Sie die folgende SQL-Anweisung in SQL Management Studio auf die Configuration Manager-Datenbank anwenden: **select [dbo].[fnGetHierarchyID](\)**  

2.  Als Nächstes verwenden Sie das folgende Windows PowerShell-Skript zum Anwenden des unidirektionalen Hashs auf die GUID, die aus der Datenbank abgerufen wurde. Sie können dann diesen Wert mit der Hierarchie-ID in den Rohdaten vergleichen, um zu prüfen, wie wir diese Daten maskiert haben.  

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



<!--HONumber=Dec16_HO3-->


