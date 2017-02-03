---
title: Diagnose- und Nutzungsdaten | Microsoft-Dokumentation
description: "Erfahren Sie mehr zu Diagnose- und Nutzungsdaten, die System Center Configuration Manager über sich selbst sammelt."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 24a233516058e645df2a43623855665b97b041b0
ms.openlocfilehash: 54ec4886eaad6999cdf3ffff7411942859f1a5b2


---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Diagnose- und Nutzungsdaten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager sammelt Diagnose- und Nutzungsdaten über sich selbst, die von Microsoft zur Verbesserung der Anwendungsinstallation, der Qualität und der Sicherheit künftiger Releases verwendet werden.  

 Diagnose- und Nutzungsdaten sind für jede System Center Configuration Manager-Hierarchie aktiviert. Sie bestehen aus SQL Server-Abfragen, die wöchentlich an jedem primären Standort und am Standort der zentralen Verwaltung ausgeführt werden. Wenn die Hierarchie einen Standort der zentralen Verwaltung verwendet, werden die Daten von primären Standorten dann an diesen Standort repliziert. Am obersten Standort Ihrer Hierarchie sendet der Dienstverbindungspunkt diese Informationen, wenn er prüft, ob Updates vorhanden sind. Wenn sich der Dienstverbindungspunkt im Offlinemodus befindet, werden die Informationen mithilfe des Dienstverbindungstools übertragen.  

> [!NOTE]  
>  Configuration Manager sammelt Daten nur von der SQL Server-Datenbank des Standorts und nicht direkt von Clients oder Standortservern.  

 Weitere Informationen finden Sie in der [Datenschutzerklärung für System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527).  

 In den folgenden Artikeln erfahren Sie mehr über Diagnose- und Nutzungsdaten für System Center Configuration Manager:  

-   [Verwenden von Diagnose- und Nutzungsdaten für System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   Sammlungsebenen von Nutzungsdaten zu Diagnosezwecken:
    - [Diagnosedaten für 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
    - [Diagnosedaten für 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnosedaten für 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)  
    - [Diagnosedaten für 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  

-   [Sammeln von Diagnose- und Nutzungsdaten mit System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [Anzeigen von Diagnose- und Nutzungsdaten für System Center Configuration Manager](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [Programm zur Verbesserung der Benutzerfreundlichkeit (Customer Experience Improvement Program, CEIP) für System Center Configuration Manager](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

-   [Häufig gestellte Fragen zu Diagnose- und Nutzungsdaten für System Center Configuration Manager](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>Siehe auch  
 [Informationen zum Dienstverbindungspunkt in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md)



<!--HONumber=Dec16_HO5-->


