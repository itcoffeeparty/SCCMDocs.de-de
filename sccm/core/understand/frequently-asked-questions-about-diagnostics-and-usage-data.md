---
title: "Häufig gestellte Fragen zu Diagnosedaten | Microsoft-Dokumentation"
description: "In diesem Artikel finden Sie häufig gestellte Fragen zu Diagnose- und Verwendungsdaten für System Center Configuration Manager."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6cf291d79c1c5d9540f809fcb00e7ab48e0c3d3b
ms.openlocfilehash: 177a30a30f6b8579fa1956d28581d4f9d3a11838


---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Häufig gestellte Fragen zu Diagnose- und Verwendungsdaten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Nachstehend finden Sie häufig gestellte Fragen zu Diagnose- und Verwendungsdaten für System Center Configuration Manager:  

###  <a name="a-namebkmkoffa-how-do-i-turn-off-telemetry"></a><a name="bkmk_off"></a> Wie schalte ich Telemetrie aus?  
Telemetriedaten können nicht deaktiviert werden. Sie können jedoch die Ebene der erfassten Telemetriedaten wählen. Sie können auch einen Dienstverbindungspunkt im Offlinemodus verwenden, um den Zeitpunkt der Übermittlung von Telemetriedaten zu verwalten.

Der aktuelle Branch von Configuration Manager muss in regelmäßigen Abständen aktualisiert werden, um neue Versionen von Windows 10 und Microsoft Intune zu unterstützen. Microsoft erfordert mindestens die Basisebene der Diagnose- und Verwendungsdaten, um das Produkt auf dem neuesten Stand zu halten, den Updateprozess zu optimieren sowie die Qualität und Sicherheit des Produkts zu verbessern.

###  <a name="a-namebkmkretentiona-what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> Wie lange ist der Datenaufbewahrungszeitraum?  
 Diagnose- und Nutzungsdaten werden ein Jahr aufbewahrt.  

###  <a name="a-namebkmkupdatea-is-diagnostics-and-usage-data-sent-when-installing-or-updating-the-product"></a><a name="bkmk_update"></a> Werden Diagnose- und Verwendungsdaten beim Installieren oder Aktualisieren des Produkts gesendet?  
 Nein. Diagnose- und Verwendungsdaten erst nur gesendet, sobald der Standort installiert wurde und betriebsbereit ist.  

###  <a name="a-namebkmkfrequencya-how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> Wie oft werden die Daten gesendet?  
 Die gespeicherten SQL-Prozeduren werden alle sieben Tage (ab dem Datum der Installation des Standorts) ausgeführt. Im Onlinemodus ist der Dienstverbindungspunkt so konfiguriert, dass die Daten nach Ausführen der Abfragen hochgeladen werden. Im Offlinemodus verwendet der Administrator das Dienstverbindungstool zum Hochladen der Daten. (Beachten Sie, dass die Daten erst sieben Tage nach der Installation des Standorts für die Offlineverwendung verfügbar sind.)  

###  <a name="a-namebkmknetworka-can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> Können die Daten zum Erstellen einer Netzwerkübersicht verwendet werden?  
 So wie in der Beschreibung der Ebenen bei der Sammlung von Nutzungsdaten zu Diagnosezwecken für System Center Configuration Manager gezeigt, enthalten Standortdetails Zeitzoneninformationen jedes Standorts. So erhalten Sie Einblicke in die allgemeine geografische und globale Verteilung von Standorten in einer Hierarchie. Es werden allerdings keine Netzwerkdetails wie IP-Adressen oder detaillierte geografische Informationen erfasst.
 - [Diagnosedaten für 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [Diagnosedaten für 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [Diagnosedaten für 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [Diagnosedaten für 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="a-namebkmktablesa-can-you-see-data-in-custom-tables"></a><a name="bkmk_tables"></a> Können Daten in benutzerdefinierten Tabellen angezeigt werden?  
 Nein. Diagnose- und Verwendungsdaten werden mithilfe gespeicherter SQL-Prozeduren gesammelt, die auf Standardprodukttabellen in der Datenbank angewendet werden, die alle das Präfix **TEL_** haben. Als Teil der SQL-Abfrage zur Erkennung des Schemas werden alle Tabellennamen für den Vergleich mit bekannten Standardwerten hashcodiert. Dies dient zum Bestimmen, ob benutzerdefinierte Tabellen in den Daten vorhanden sind (d. h., ob das Datenbankschema abweichend vom Standard erweitert wurde), aber nicht der Daten, die in diesen Tabellen vorhanden waren.  

###  <a name="a-namebkmkdatabasesa-can-you-see-names-of-other-databases-or-can-you-see-data-in-other-databases"></a><a name="bkmk_databases"></a> Können die Namen anderer Datenbanken oder Daten in anderen Datenbanken angezeigt werden?  
 Nein. Die gespeicherten Prozeduren zum Sammeln von Daten sind auf die Standortdatenbank beschränkt.  

## <a name="see-also"></a>Weitere Informationen:  
 [Diagnose- und Nutzungsdaten für System Center Configuration Manager](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)



<!--HONumber=Feb17_HO2-->


