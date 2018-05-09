---
title: Einführung in Abfragen
titleSuffix: Configuration Manager
description: Erstellen Sie Abfragen erstellen, und führen Sie sie aus, um Objekte in einer Configuration Manager-Hierarchie zu suchen, die mit den Abfragekriterien übereinstimmen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ebc5c1b7f7efb1ba9c3f1fc7b36f82b6be59858f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Einführung in Abfragen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können Abfragen erstellen und ausführen, um Objekte in einer Configuration Manager-Hierarchie zu suchen, die mit den Abfragekriterien übereinstimmen. Zu diesen Objekten gehören Elemente wie beispielsweise bestimmte Typen von Computern oder Benutzergruppen. In Abfragen können die meisten Configuration Manager-Objekttypen zurückgegeben werden, darunter Standorte, Sammlungen, Anwendungen und Inventurdaten.  

 Wenn Sie eine Abfrage erstellen, müssen Sie mindestens zwei Parameter angeben: wo Sie suchen möchten und was Sie suchen möchten. Wenn Sie beispielsweise den verfügbaren Festplattenspeicherplatz auf allen Computern eines Configuration Manager-Standorts ermitteln möchten, können Sie mit einer Abfrage über das Attribut **Free Space (MB)** der Attributklasse **Logical Disk** den verfügbaren freien Speicherplatz ermitteln.  

 Nachdem Sie eine Ausgangsabfrage erstellt haben, können Sie zusätzliche Abfragekriterien angeben. Sie können z. B. festlegen, dass in den Abfrageergebnissen nur Computer eingeschlossen werden sollen, die einem bestimmten Standort zugewiesen sind. Sie können darüber hinaus die Darstellungsweise von Ergebnissen ändern, so dass Sie die Ergebnisse in einer für Sie sinnvollen Reihenfolge angezeigt werden. So können Sie beispielsweise angeben, dass die Ergebnisse in aufsteigender oder absteigender Reihenfolge nach Umfang des freien Festplattenspeicherplatzes sortiert werden sollen.  

 Wenn Sie eine Abfrage erstellen, wird diese von Configuration Manager gespeichert und im Knoten **Abfragen** im Arbeitsbereich **Überwachung** angezeigt. In diesem Bereich können Sie eine neue Abfrage erstellen und dann eine vorhandene Abfrage ausführen, aktualisieren oder verwalten.  

 Sie können eine Abfrage auch in eine Abfrageregel einer Configuration Manager-Sammlung importieren. Weitere Informationen finden Sie unter [Erstellen von Sammlungen in System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

## <a name="see-also"></a>Siehe auch  
 [Abfragen – Technische Referenz für System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
