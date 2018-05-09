---
title: Wartung für Softwareupdates
titleSuffix: Configuration Manager
description: Um die Softwareupdates in Configuration Manager zu gewährleisten, können Sie den WSUS-Bereinigungstask planen oder manuell ausführen.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 03eabbfcd070bb61b2930fac89a551bbeb111eb4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="software-updates-maintenance"></a>Wartung für Softwareupdates

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können den WSUS-Bereinigungstask von der Configuration Manager-Konsole aus planen und ausführen, oder Sie können den WSUS-Bereinigungstask von den Eigenschaften der Softwareupdatepunktkomponente aus manuell ausführen. Wenn Sie die Ausführung der WSUS-Bereinigungsaufgabe auswählen, wird sie bei der nächsten Softwareupdatesynchronisierung ausgeführt. Die abgelaufenen Softwareupdates werden auf dem WSUS-Server auf den Status „Abgelehnt“ festgelegt, und der Windows Update-Agent auf Computern durchsucht diese Softwareupdates daraufhin nicht mehr. Standardmäßig wird der WSUS-Bereinigungsauftrag alle 30 Tage ausgeführt.  

#### <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>So wird die WSUS-Bereinigungsaufgabe geplant und ausgeführt  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Standorte**.  

2.  Klicken Sie in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren** , und klicken Sie dann auf **Softwareupdatepunkt** , um die Eigenschaften der Softwareupdatepunkt-Komponente zu öffnen.  

3.  Klicken Sie auf die Registerkarte **Ablösungsregeln** , wählen Sie **Assistent für die WSUS-Serverbereinigung ausführen**, und klicken Sie dann auf **OK**.
