---
title: Verwalten von Abfragen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Abfragen verwalten. Enthält eine Tabelle für detaillierte Referenzinformationen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9d538106f2cc30a9eca5be51c4174af531bbbda9
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>Verwalten von Abfragen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Informationen in diesem Thema helfen Ihnen bei der Abfragenverwaltung in Configuration Manager.  

 Informationen zum Erstellen von Abfragen finden Sie unter [Erstellen von Abfragen in System Center Configuration Manager](../../../core/servers/manage/create-queries.md).  

## <a name="how-to-manage-queries"></a>Verwalten von Abfragen  
 Wählen Sie im Arbeitsbereich **Überwachung** die Option **Abfragen**aus, markieren Sie die zu verwaltende Abfrage, und wählen Sie dann einen Verwaltungstask aus.  

 In der nachfolgenden Tabelle finden Sie weitere Informationen zu den Verwaltungstasks, für die möglicherweise einige Informationen benötigt werden, bevor Sie sie auswählen.  

|Verwaltungstask|Details|Weitere Informationen|  
|---------------------|-------------|----------------------|  
|**Ausführen**|Die ausgewählte Abfrage wird ausgeführt, und die Ergebnisse werden in der Configuration Manager-Konsole angezeigt.|Keine zusätzlichen Informationen|  
|**Client installieren**|Öffnet den **Assistenten zum Installieren von Clients**, mit dem Sie den Configuration Manager-Client auf Computern installieren können, die von der ausgewählten Abfrage zurückgegeben werden.<br /><br /> Diese Option ist nicht für Abfragen verfügbar, von denen mobile Geräte, Benutzer oder Benutzergruppen zurückgegeben werden.|Weitere Informationen zum Installieren von Configuration Manager-Clients per Clientpush finden Sie unter [Bereitstellen von Clients auf Windows-Computern](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).|  
|**Exportierenieren**|Öffnet den **Assistenten zum Exportieren von Objekten** , mit dem Sie diese Abfrage in eine MOF-Datei (Managed Object Format) exportieren können, die dann an einem anderen Standort importiert werden kann.|Keine zusätzlichen Informationen|  
|**Verschieben**|Öffnet das Dialogfeld **Ausgewählte Elemente verschieben** zum Verschieben der ausgewählten Abfrage in einen Ordner, den Sie zuvor unter dem Knoten **Abfragen** erstellt haben.|Keine zusätzlichen Informationen|  

## <a name="see-also"></a>Siehe auch  
 [Vorgänge und Wartungstasks für Abfragen in System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
