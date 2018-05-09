---
title: Diagnose- und Nutzungsdaten
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Diagnose- und Nutzungsdaten, die System Center Configuration Manager über sich selbst sammelt.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a70f632c04d7202ed1c41e5e138ed63dfdba1c6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Diagnose- und Nutzungsdaten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Configuration Manager sammelt Diagnose- und Nutzungsdaten über sich selbst, die von Microsoft zur Verbesserung der Anwendungsinstallation, der Qualität und der Sicherheit künftiger Releases verwendet werden.  

 Diagnose- und Nutzungsdaten sind für jede Configuration Manager-Hierarchie aktiviert. Sie bestehen aus SQL Server-Abfragen, die wöchentlich an jedem primären Standort und am Standort der zentralen Verwaltung ausgeführt werden. Wenn die Hierarchie einen Standort der zentralen Verwaltung verwendet, werden die Daten von primären Standorten dann an diesen Standort repliziert. Am obersten Standort Ihrer Hierarchie sendet der Dienstverbindungspunkt diese Informationen, wenn er prüft, ob Updates vorhanden sind. Wenn sich der Dienstverbindungspunkt im Offlinemodus befindet, werden die Informationen mithilfe des Dienstverbindungstools übertragen.  

> [!NOTE]  
>  Configuration Manager sammelt Daten nur von der SQL Server-Datenbank des Standorts und nicht direkt von Clients oder Standortservern.  

 Weitere Informationen finden Sie in der [Datenschutzerklärung von Microsoft](https://go.microsoft.com/fwlink/?LinkID=626527).  

## <a name="articles"></a>Artikel
 In den folgenden Artikeln erfahren Sie mehr über Diagnose- und Nutzungsdaten für Configuration Manager:  

-   [Nutzung von Diagnose- und Verwendungsdaten](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   Sammlungsebenen von Nutzungsdaten zu Diagnosezwecken:
    - [Diagnosedaten für Version 1802](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1802)  
    - [Diagnosedaten für Version 1710](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1710)  
    - [Diagnosedaten für 1706](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1706)    

<!--
    - [Diagnostic data for 1702](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702)      
    - [Diagnostic data for 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  
    - [Diagnostic data for  1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)    
    - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnostic data for  1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
-->

-   [Sammeln von Diagnose- und Verwendungsdaten](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [Anzeigen von Diagnose- und Verwendungsdaten](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP)](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

     > [!Note]  
     > Ab Configuration Manager Version 1802 ist das CEIP-Feature nicht mehr im Produkt enthalten.


-   [Häufig gestellte Fragen zu Diagnose- und Verwendungsdaten](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>Siehe auch  
 [Informationen zum Dienstverbindungspunkt](../../../core/servers/deploy/configure/about-the-service-connection-point.md)
