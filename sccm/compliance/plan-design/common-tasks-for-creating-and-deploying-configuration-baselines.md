---
title: Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines mit System Center Configuration Manager | System Center Configuration Manager
description: Erfahren Sie, wie Sie System Center Configuration Manager-Konfigurationsbaselines erstellen und bereitstellen.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0d66240408dcd65576954ffb27395d3f05f5a41e


---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-system-center-configuration-manager"></a>Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbasislinien mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält häufige Szenarios, mit deren Hilfe Sie mehr über das Erstellen und Bereitstellen von System Center Configuration Manager-Konfigurationsbaselines erfahren.  

 Wenn Sie bereits mit Kompatibilitätseinstellungen vertraut sind, finden Sie eine ausführliche Dokumentation zu allen verwendbaren Funktionen in den Themen [Create configuration baselines in System Center Configuration Manager (Erstellen von Konfigurationsbaselines in System Center Configuration Manager)](../../compliance/deploy-use/create-configuration-baselines.md) und [How to deploy configuration baselines in System Center Configuration Manager (Bereitstellen von Konfigurationsbaselines in System Center Configuration Manager)](../../compliance/deploy-use/deploy-configuration-baselines.md).  

 Bevor Sie beginnen, lesen Sie [Get started with compliance settings in System Center Configuration Manager (Erste Schritte mit Kompatibilitätseinstellungen in System Center Configuration Manager)](../../compliance/get-started/get-started-with-compliance-settings.md), um einige Grundlagen der Kompatibilitätseinstellungen zu erfahren, und lesen Sie zudem [Plan for and configure compliance settings in System Center Configuration Manager (Planen und Konfigurieren von Kompatibilitätseinstellungen in System Center Configuration Manager)](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

## <a name="create-a-configuration-baseline"></a>Erstellen einer Konfigurationsbasislinie  
 In diesem Beispiel haben Sie ein Konfigurationselement ausschließlich für Windows 10-PCs erstellt, auf denen der Configuration Manager-Client ausgeführt wird.  

 Dieses Konfigurationselement erzwingt ein erforderliches Kennwort mit mindestens 6 Zeichen auf Windows 10-PCs. Das Konfigurationselement hat den Namen **Windows 10 Password Enforcement**.  

Im folgenden Verfahren erfahren Sie, wie dieses Konfigurationselement einer Konfigurationsbasislinie hinzugefügt wird, um es für die Bereitstellung vorzubereiten.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationsbaselines**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationsbasislinie erstellen**.  

4.  Konfigurieren Sie im Dialogfeld **Konfigurationsbasislinie erstellen** Folgendes:  

    -   **Name** : Geben Sie **Windows 10 Passwords** (oder einen anderen Namen Ihrer Wahl) ein.  

5.  Klicken Sie auf **Hinzufügen** > **Konfigurationselemente**.  

6.  Wählen Sie im Dialogfeld **Konfigurationselemente hinzufügen** das zuvor erstellte Konfigurationselement **Windows 10 Password Enforcement** aus, und klicken Sie dann auf **Hinzufügen**.  

7.  Klicken Sie auf "OK", um das Dialogfeld **Konfigurationselemente hinzufügen** zu schließen und zum Dialogfeld **Konfigurationsbasislinie erstellen** zurückzukehren, das ähnlich wie in diesem Screenshot aussehen sollte:  

     ![Dialogfeld „Konfigurationsbaseline erstellen“](/sccm/compliance/plan-design/media/Create-Configuration-Baseline.png)  

8.  Klicken Sie auf **OK** , um das Dialogfeld **Konfigurationsbasislinie erstellen** zu schließen.  

 Sie sehen nun die gerade erstellte Konfigurationsbaseline im Knoten **Konfigurationsbaselines** der Configuration Manager-Konsole.  

## <a name="deploy-the-configuration-baseline"></a>Bereitstellen der Konfigurationsbaseline  
 In diesem Beispiel stellen Sie die im vorherigen Verfahren erstellte Konfigurationsbasislinie für eine Sammlung von Computern bereit.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationsbaselines**.  

3.  Wählen Sie aus der Liste der Konfigurationsbasislinien **Windows 10 Passwords**aus.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

5.  Konfigurieren Sie im Dialogfeld **Konfigurationsbasislinien bereitstellen** Folgendes:  

    -   **Ausgewählte Konfigurationsbasislinien** : Stellen Sie sicher, dass die Konfigurationsbasislinie **Windows 10 Passwords** automatisch dieser Liste hinzugefügt wurde.  

    -   **Nicht kompatible Regeln wiederherstellen, falls dies unterstützt wird**: Wenn auf Zielgeräten nicht die richtigen Einstellungen vorhanden sind, können Sie mithilfe dieses Kontrollkästchens sicherstellen, dass die Einstellungen von Configuration Manager wiederhergestellt werden.  

    -   **Sammlung** : Klicken Sie auf **Durchsuchen** , um die Sammlung von Computern auszuwählen, auf denen die Konfigurationsbasislinie ausgewertet und die Kompatibilität wiederhergestellt wird. In diesem Beispiel wurde die Konfigurationsbasislinie für die integrierte Sammlung **Alle Desktop- und Serverclients** bereitgestellt.  

        > [!TIP]  
        >  Es ist unerheblich, ob die ausgewählte Sammlung Computer oder Geräte enthält, auf denen nicht Windows 10 ausgeführt wird. Solange Sie im erstellten Konfigurationselement unterstützte Plattformen konfiguriert haben, wird nur die Kompatibilität von Windows 10-PCs ausgewertet.  

    -   Konfigurieren Sie ggf. den Zeitplan, nach dem die Konfigurationsbasislinie ausgewertet wird. Andernfalls behalten Sie die Standardeinstellung **7 Tage**bei.  

6.  Das Dialogfeld sieht jetzt etwa wie folgt aus:  

     ![Dialogfeld „Bereitstellen von Konfigurationsbaselines“](/sccm/compliance/plan-design/media/Deploy-configuration-baselines.png)  

7.  Klicken Sie auf **OK** , um das Dialogfeld **Konfigurationsbasislinien bereitstellen** zu schließen und die Bereitstellung zu erstellen.  

 Um einen kurzen Blick auf die Kompatibilitätsstatistik für diese Bereitstellung zu werfen, klicken Sie im Arbeitsbereich **Überwachung** auf **Bereitstellungen**. Am unteren Bildschirmrand wird ein Diagramm **Kompatibilitätsstatistik** angezeigt.  

 Ausführlichere Informationen zum Überwachen von Konfigurationsbaselines finden Sie unter [Monitor compliance settings in System Center Configuration Manager (Verwalten von Kompatibilitätseinstellungen in System Center Configuration Manager)](../../compliance/deploy-use/monitor-compliance-settings.md).  



<!--HONumber=Nov16_HO1-->


