---
title: Diagnosedatensammlung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr darüber, wie System Center Configuration Manager Diagnose- und Nutzungsdaten über sich selbst sammelt.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7eb4becd24ac143ce17c476cda0535ac6bedd039
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Sammeln von Diagnose- und Verwendungsdaten mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

An jedem primären Standort werden wöchentlich SQL Server-Abfragen ausgeführt, um Diagnose- und Nutzungsdaten für System Center Configuration Manager zu sammeln. In einer Hierarchie mit mehreren Standorten werden die Daten an den zentralen Verwaltungsstandort repliziert.  

Am obersten Standort einer Hierarchie sendet die Standortsystemrolle „Dienstverbindungspunkt“ diese Informationen, wenn sie prüft, ob Updates vorhanden sind. Wie die Daten übermittelt werden, hängt vom Modus des Dienstverbindungspunkts ab:  

-   **Im Onlinemodus:** Diagnose- und Nutzungsdaten werden automatisch einmal pro Woche vom Dienstverbindungspunkt an den Clouddienst gesendet.  

-   **Im Offlinemodus:** Diagnose- und Nutzungsdaten werden manuell mithilfe des Dienstverbindungstools übertragen. Weitere Informationen finden Sie unter [Verwenden des Dienstverbindungstools für System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Weitere Informationen finden Sie unter [Informationen zum Dienstverbindungspunkt in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  
