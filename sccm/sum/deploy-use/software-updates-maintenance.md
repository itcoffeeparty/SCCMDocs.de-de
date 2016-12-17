---

title: "Wartung für Softwareupdates | Configuration Manager"
description: "Um die Softwareupdates in Configuration Manager zu gewährleisten, können Sie den WSUS-Bereinigungstask planen oder manuell ausführen."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1495aa474c39723767ec2d81bc60eb1582ac5504



---
# <a name="software-updates-maintenance"></a>Wartung für Softwareupdates

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können den WSUS-Bereinigungstask von der Configuration Manager-Konsole aus planen und ausführen, oder Sie können den WSUS-Bereinigungstask von den Eigenschaften der Softwareupdatepunktkomponente aus manuell ausführen. Wenn Sie die Ausführung der WSUS-Bereinigungsaufgabe auswählen, wird sie bei der nächsten Softwareupdatesynchronisierung ausgeführt. Die abgelaufenen Softwareupdates werden auf dem WSUS-Server auf den Status „Abgelehnt“ festgelegt, und der Windows Update-Agent auf Computern durchsucht diese Softwareupdates daraufhin nicht mehr. Standardmäßig wird der WSUS-Bereinigungsauftrag alle 30 Tage ausgeführt.  

#### <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>So wird die WSUS-Bereinigungsaufgabe geplant und ausgeführt  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Standorte**.  

2.  Klicken Sie in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren** , und klicken Sie dann auf **Softwareupdatepunkt** , um die Eigenschaften der Softwareupdatepunkt-Komponente zu öffnen.  

3.  Klicken Sie auf die Registerkarte **Ablösungsregeln** , wählen Sie **Assistent für die WSUS-Serverbereinigung ausführen**, und klicken Sie dann auf **OK**.



<!--HONumber=Nov16_HO1-->

