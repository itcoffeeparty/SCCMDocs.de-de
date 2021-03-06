---
title: Entfernen eines Softwareupdatepunkts
titleSuffix: Configuration Manager
description: Gehen Sie wie folgt vor, um die Softwareupdatepunkt-Standortsystemrolle an einem Standort in der Configuration Manager-Konsole zu entfernen.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 585077c44b13d79da55e8ab140fd93998b8371c1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
#  <a name="BKMK_RemoveSUP"></a> Entfernen der Standortsystemrolle „Softwareupdatepunkt“  

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können die Softwareupdatepunkt-Standortsystemrolle an einem Standort in der Configuration Manager-Konsole entfernen. Die Clientrichtlinie wird aktualisiert, um den Softwareupdatepunkt aus der Liste zu entfernen. Wenn Sie den letzten Softwareupdatepunkt des Standorts entfernen, enthält die Softwareupdatepunkt-Liste keine Einträge mehr, und Softwareupdates sind für den Standort somit praktisch deaktiviert. Sie müssen einen anderen Softwareupdatepunkt des Standorts als neue Synchronisierungsquelle auswählen, wenn an einem primären Standort mehr als ein Softwareupdatepunkt vorhanden ist und Sie den Softwareupdatepunkt entfernen, der als Synchronisierungsquelle konfiguriert ist.  

> [!NOTE]  
>  Wenn Sie die Softwareupdatepunkt-Standortrolle aus einem Standortsystem entfernen, sollten Sie mindestens 15 Minuten warten, bevor Sie die Softwareupdatepunkt-Standortrolle wieder installieren.  

 Verwenden Sie das folgende Verfahren, um einen Softwareupdatepunkt zu entfernen.  

#### <a name="to-remove-the-software-update-point"></a>So entfernen Sie den Softwareupdatepunkt  

1.  Klicken Sie in der **Configuration Manager** -Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung**den Bereich **Standortkonfiguration**, und klicken Sie dann auf "Server und Standortsystemrollen".  

3.  Wählen Sie den Standortsystemserver mit dem zu entfernenden Softwareupdatepunkt aus, und wählen Sie unter **Standortsystemrollen**die Option **Softwareupdatepunkt**aus.  

4.  Klicken Sie auf der Registerkarte **Standortrolle** in der Gruppe **Standortrolle** auf **Rolle entfernen**. Bestätigen Sie, dass Sie den Softwareupdatepunkt entfernen möchten, oder wählen Sie eine neue Synchronisierungsquelle für die anderen Softwareupdatepunkte am Standort.  
