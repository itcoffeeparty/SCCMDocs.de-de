---
title: Häufig gestellte Fragen zu Diagnose- und Nutzungsdaten
titleSuffix: Configuration Manager
description: In diesem Artikel finden Sie häufig gestellte Fragen zu Diagnose- und Verwendungsdaten für System Center Configuration Manager.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b4174c68d5a6ccd31355d976b7830b6d09f39d91
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Häufig gestellte Fragen zu Diagnose- und Verwendungsdaten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Artikel erhalten Sie Antworten zu häufig gestellten Fragen zu Diagnose- und Nutzungsdaten in Configuration Manager.

## <a name="faqs"></a>Häufig gestellte Fragen

###  <a name="bkmk_off"></a> Wie schalte ich Telemetrie aus?  
Telemetriedaten können nicht deaktiviert werden. Sie können jedoch die Ebene der erfassten Telemetriedaten wählen. Verwenden Sie einen Dienstverbindungspunkt im Offlinemodus, um den Zeitpunkt der Übermittlung von Telemetriedaten zu verwalten.

Der aktuelle Branch von Configuration Manager muss in regelmäßigen Abständen aktualisiert werden, um neue Versionen von Windows 10 und Microsoft Intune zu unterstützen. Für Microsoft ist zumindest ein grundlegendes Verständnis von Diagnose- und Nutzungsdaten erforderlich. Dieses Daten werden verwendet, um das Produkt auf dem neuesten Stand zu halten, den Updateprozess zu optimieren sowie die Qualität und Sicherheit des Produkts zu verbessern.

###  <a name="bkmk_retention"></a> Wie lange ist der Datenaufbewahrungszeitraum?  
 Diagnose- und Nutzungsdaten werden ein Jahr lang gespeichert.  

###  <a name="bkmk_update"></a> Werden Diagnose- und Verwendungsdaten beim Installieren oder Aktualisieren des Produkts gesendet?  
 Nein. Diagnose- und Verwendungsdaten erst nur gesendet, sobald der Standort installiert wurde und betriebsbereit ist.  

###  <a name="bkmk_frequency"></a> Wie oft werden die Daten gesendet?  
 Die gespeicherten SQL-Prozeduren werden alle sieben Tage (ab dem Datum der Installation des Standorts) ausgeführt. Im Onlinemodus ist der Dienstverbindungspunkt so konfiguriert, dass die Daten nach Ausführen der Abfragen hochgeladen werden. Im Offlinemodus verwendet der Administrator das Dienstverbindungstool zum Hochladen der Daten. (Die Daten sind erst sieben Tage nach der Installation des Standorts für die Offlineverwendung verfügbar.)  

###  <a name="bkmk_network"></a> Können die Daten zum Erstellen einer Netzwerkübersicht verwendet werden?  
 So wie in der Beschreibung der Ebenen von Diagnose- und Nutzungsdaten gezeigt, enthalten Standortdetails Zeitzoneninformationen jedes Standorts. So erhalten Sie Einblicke in die allgemeine geografische und globale Verteilung von Standorten in einer Hierarchie. In diesen Daten sind jedoch keine Netzwerkdetails wie IP-Adressen oder detaillierte geografische Informationen enthalten. Weitere Informationen finden Sie in den [Artikeln zu Diagnose- und Nutzungsdaten](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data#articles). Die Ebenen der Diagnose- und Nutzungsdatensammlung für die Version, die Sie verwenden, finden Sie ebenfalls in diesen Artikeln.


###  <a name="bkmk_tables"></a> Können Daten in benutzerdefinierten Tabellen angezeigt werden?  
 Nein. Configuration Manager erfasst Diagnose- und Nutzungsdaten über in SQL gespeicherte Prozeduren. Diese gespeicherten Prozeduren werden für die Standardprodukttabellen in der Datenbank ausgeführt. Diese gesamten SQL-Tabellen werden mit dem Präfix **TEL_** versehen. Als Teil der SQL-Abfrage zur Erkennung des Schemas werden alle Tabellennamen für den Vergleich mit bekannten Standardwerten hashcodiert. Durch dieses Verhalten wird festgelegt, dass benutzerdefinierte Tabellen in der Datenbank vorhanden sind. Benutzerdefinierte Tabellen informieren darüber, dass das Datenbankschema abweichend vom Standard erweitert wurde. Es enthält keine Daten, die in diesen Tabellen gespeichert sind.  

###  <a name="bkmk_databases"></a> Können die Namen anderer Datenbanken oder Daten in anderen Datenbanken angezeigt werden? 
 Nein. Die gespeicherten Prozeduren zum Sammeln von Daten sind auf die Standortdatenbank beschränkt.  

### <a name="bkmk_gdpr"></a> Unterliegt Configuration Manager der Datenschutz-Grundverordnung (DSGVO)?
 Nein. Configuration Manager unterliegt nicht der Kontrolle durch die GSGVO. Es handelt sich um ein lokales Produkt, das direkt von Ihnen bereitgestellt, verwaltet und ausgeführt wird. Die Diagnose- und Nutzungsdaten, die von Microsoft gesammelt werden, verbessern die Anwendungsinstallation, Qualität sowie die Sicherheit zukünftiger Releases. Diese Daten unterliegen der Kontrolle durch die GSGVO. Es werden keine Informationen zur Endbenutzeridentifizierung oder pseudonyme Identifizierungsmerkmale von Endbenutzern gesammelt und an Microsoft übermittelt. Weitere Informationen zur GSGVO erhalten Sie im [Microsoft Trust Center zur EU-Datenschutz-Grundverordnung](https://microsoft.com/gdpr). Weitere Informationen zu Configuration Manager-Daten finden Sie unter [Diagnose- und Nutzungsdaten für System Center Configuration Manager](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).


## <a name="see-also"></a>Weitere Informationen:  
 [Diagnose- und Verwendungsdaten](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)
