---
title: Diagnosedatensammlung
titleSuffix: Configuration Manager
description: "Erfahren Sie mehr darüber, wie System Center Configuration Manager Diagnose- und Nutzungsdaten über sich selbst sammelt."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: "5"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: a879bd0eba04ffef1f3c6c6ce8426c380aefc1d3
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Sammeln von Diagnose- und Verwendungsdaten mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

An jedem primären Standort werden wöchentlich SQL Server-Abfragen ausgeführt, um Diagnose- und Nutzungsdaten für System Center Configuration Manager zu sammeln. In einer Hierarchie mit mehreren Standorten werden die Daten an den zentralen Verwaltungsstandort repliziert.  

Am obersten Standort einer Hierarchie sendet die Standortsystemrolle „Dienstverbindungspunkt“ diese Informationen, wenn sie prüft, ob Updates vorhanden sind. Wie die Daten übermittelt werden, hängt vom Modus des Dienstverbindungspunkts ab:  

-   **Im Onlinemodus:** Diagnose- und Nutzungsdaten werden automatisch einmal pro Woche vom Dienstverbindungspunkt an den Clouddienst gesendet.  

-   **Im Offlinemodus:** Diagnose- und Nutzungsdaten werden manuell mithilfe des Dienstverbindungstools übertragen. Weitere Informationen finden Sie unter [Verwenden des Dienstverbindungstools für System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Weitere Informationen finden Sie unter [Informationen zum Dienstverbindungspunkt in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  
