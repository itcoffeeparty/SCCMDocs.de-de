---
title: "Bewährte Methoden für die Berichterstellung | System Center Configuration Manager"
description: Hier finden Sie hilfreiche Tipps zur Berichterstattungsfunktion von System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: 4
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fae72b0455b53923aaf93b5b53afb562bedc2eca


---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>Bewährte Methoden für die Berichterstellung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die folgenden bewährten Methoden für die Berichterstattung in System Center Configuration Manager:  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>Installieren des Reporting Services-Punkts auf einem Remote-Standortsystemserver aus Leistungsgründen  
 Sie haben die Wahl, ob Sie den Reporting Services-Punkt auf dem Standortserver oder auf einem Remote-Standortsystem installieren. Durch eine Installation auf einem Remote-Standortsystem wird jedoch die Leistung verbessert.  

## <a name="optimize-sql-server-reporting-services-queries"></a>Optimieren von SQL Server Reporting Services-Abfragen  
 In der Regel sind Verzögerungen bei der Berichterstattung darauf zurückzuführen, dass das Ausführen von Abfragen und das Abrufen der Ergebnisse Zeit kosten. Wenn Sie Microsoft SQL Server verwenden, können Tools wie Query Analyzer und Profiler zur Optimierung der Abfragen beitragen.  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>Planen der Verarbeitung von Berichtsabonnements außerhalb der normalen Geschäftszeiten  
 Planen Sie die Verarbeitung von Berichtsabonnements nach Möglichkeit außerhalb der normalen Geschäftszeiten, um die Prozessorauslastung des Configuration Manager-Standortdatenbank zu minimieren. Durch dieses Vorgehen wird auch die Verfügbarkeit von unvorhergesehenen Berichtsanforderungen verbessert.  

## <a name="next-steps"></a>Nächste Schritte
[Konfigurieren der Berichterstellung](configuring-reporting.md)



<!--HONumber=Nov16_HO1-->

