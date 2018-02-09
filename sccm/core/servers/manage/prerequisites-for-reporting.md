---
title: "Voraussetzungen für die Berichterstattung"
titleSuffix: Configuration Manager
description: "Hier finden Sie Informationen zu verschiedenen Abhängigkeiten, die sich auf die Nutzung der Berichterstellung in System Center Configuration Manager auswirken."
ms.custom: na
ms.date: 01/29/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: 
caps.handback.revision: 
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 3feafa8a20bedfba381c29a5d7fe80a47517b6ab
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>Voraussetzungen für die Berichterstattung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Berichterstellung in System Center Configuration Manager hat externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts.  

## <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  
 In der folgenden Tabelle werden die externen Abhängigkeiten der Berichterstattung aufgelistet.  

|Voraussetzung|Weitere Informationen|  
|------------------|----------------------|  
|SQL Server Reporting Services|SQL Server Reporting Services muss zunächst installiert und konfiguriert werden, damit die Berichterstellung in Configuration Manager verwendet werden kann.<br /><br /> Informationen zum Planen und Bereitstellen von Reporting Services in Ihrer Umgebung finden Sie im Abschnitt [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) in der SQL Server 2008-Onlinedokumentation.|  
|Abhängigkeiten der Standortsystemrollen bei Computern, auf denen der Reporting Services-Punkt ausgeführt wird|[Unterstützte Konfigurationen für System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Interne Abhängigkeiten von Configuration Manager  
 In der folgenden Tabelle werden die Abhängigkeiten der Berichterstellung in Configuration Manager aufgelistet.  

|Voraussetzung|Weitere Informationen|  
|------------------|----------------------|  
|Reporting Services-Punkt|Die Standortsystemrolle des Reporting Services-Punkts muss konfiguriert werden, damit die Berichterstellung in Configuration Manager verwendet werden kann. Weitere Informationen zum Installieren und Konfigurieren eines Reporting Services-Punkts finden Sie unter [Configuring reporting in System Center Configuration Manager (Konfigurieren der Berichterstellung in System Center Configuration Manager)](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Unterstützte SQL Server-Versionen für den Reporting Services-Punkt  
 Die Reporting Services-Datenbank kann entweder auf der Standardinstanz oder auf einer benannten Instanz einer 64-Bit-SQL Server-Installation installiert werden. Die SQL Server-Instanz kann sich auf dem gleichen Computer wie der Standortsystemserver oder auf einem Remotecomputer befinden.  

 Die folgende Tabelle enthält eine Aufstellung der SQL Server-Versionen, die vom Reporting Services-Punkt unterstützt werden.  

|SQL Server-Version|Reporting Services-Punkt|  
|------------------------|------------------------------|
|SQL Server 2017 (mindestens mit kumulativem Update 2)<br /><br /> - Standard<br />- Enterprise|Ja, ab Configuration Manager-Version 1710|  
|SQL Server 2016 mit SP1<br /><br /> - Standard<br />- Enterprise|Ja| 
|SQL Server 2016<br /><br /> - Standard<br />- Enterprise|Ja|
|SQL Server 2014 mit SP2<br /><br /> - Standard<br />- Enterprise|Ja|
|SQL Server 2014 mit SP1<br /><br /> - Standard<br />- Enterprise|Ja|
|SQL Server 2012 mit SP4 <br /><br /> - Standard<br />- Enterprise|Ja|  
|SQL Server 2012 mit SP3 <br /><br /> - Standard<br />- Enterprise|Ja|  
|SQL Server 2008 R2 mit SP3<br /><br /> - Standard<br />- Enterprise<br />- Datacenter|Ja, für unterstützte Vorgängerversionen von Configuration Manager 1702.|  
|SQL Server Express 2008 R2 mit SP3|Nicht unterstützt| 




## <a name="next-steps"></a>Nächste Schritte
[Vorgänge und Wartungstasks für die Berichterstellung](operations-and-maintenance-for-reporting.md)
