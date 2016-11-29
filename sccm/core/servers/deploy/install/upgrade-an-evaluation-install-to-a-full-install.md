---
title: Upgrade von Evaluierungsinstallationen | System Center Configuration Manager
description: "Erfahren Sie, wie Sie ein Upgrade einer Evaluierungsinstallation auf eine vollständige Installation von System Center Configuration Manager durchführen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0ad15c0caddeb3c200b8c663631d2993a338c7c8

---
# <a name="upgrade-an-evaluation-install-of-system-center-configuration-manager-to-a-full-install"></a>Upgrade von Evaluierungsinstallationen von System Center Configuration Manager auf eine vollständige Installation

*Gilt für: System Center Configuration Manager (Current Branch)*



 Wenn Sie eine Evaluierungsversion von System Center Configuration Manager installiert haben, wird die Configuration Manager-Konsole nach 180 Tagen für Schreibvorgänge gesperrt, bis Sie in Setup auf der Seite **Standortwartung** das Produkt aktivieren. Sie haben jederzeit vor oder nach Ablauf des 180-tägigen Zeitraums die Möglichkeit, ein Upgrade der Evaluierungsinstallation auf eine Vollversion durchzuführen.  

> [!NOTE]  
>  Wenn Sie von einer Configuration Manager-Konsole aus eine Verbindung mit einer Evaluierungsinstallation von Configuration Manager herstellen, wird in der Titelleiste der Konsole die Anzahl der verbleibende Tage für die Gültigkeit der Evaluierungsinstallation angegeben. Die Tagesangabe wird nicht automatisch aktualisiert und ändert sich nur, wenn Sie eine neue Verbindung mit einem Standort herstellen.  

 **Sie können ein Upgrade der folgenden Standorte durchführen, an denen eine Evaluierungsinstallation ausgeführt wird:**  

-   Standort der zentralen Verwaltung  

-   Primärer Standort  

Da sekundäre Standorte nicht als Evaluierungsinstallationen behandelt werden, müssen Sie einen sekundären Standort nicht ändern, nachdem für den entsprechenden primären übergeordneten Standort ein Upgrade auf eine Vollversion durchgeführt wurde.  

**Voraussetzungen für ein Upgrade einer Evaluierungsversion auf eine Vollversion:**  

-   Sie müssen während des Upgrades ein gültiges Produkt verwenden.  

-   Ihr Konto benötigt **Administratorberechtigungen** auf dem Computer, auf dem der Standort installiert wird.  

### <a name="to-upgrade-an-evaluation-edition-of-configuration-manager-to-a-licensed-edition"></a>So führen Sie ein Upgrade einer Evaluierungsversion von Configuration Manager auf eine lizenzierte Version aus  

1.  Suchen Sie auf dem Standortserver **SETUP.exe** (Configuration Manager-Setup) im Configuration Manager-Installationsordner (**%path%\BIN\X64**), und führen Sie die Datei aus.  Sie müssen die Kopie von Setup ausführen, die sich auf dem Standortserver im Ordner „Configuration Manager“ befindet, da keine Standortwartungsoptionen verfügbar sind, wenn Sie Setup auf dem Installationsmedium ausführen.  

2.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  

3.  Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen**aus, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie auf der Seite **Standortwartung** die Option **Upgrade von der Evaluation Edition auf eine lizenzierte Edition ausführen**aus. Geben Sie einen gültigen Product Key ein, und klicken Sie dann auf **Weiter**.  

5.  Lesen und akzeptieren Sie auf der Seite **Microsoft Software-Lizenzbedingungen** die Lizenzbedingungen, und klicken Sie anschließend auf **Weiter**.  

6.  Klicken Sie auf der Seite **Konfiguration** auf **Schließen** , um den Assistenten abzuschließen.  

    > [!NOTE]  
    >  Die Titelleiste von Configuration Manager-Konsolen, die mit dem Standort verbunden bleiben, für den Sie ein Upgrade vornehmen, gibt ggf. an, dass der Standort weiter eine Evaluierungsversion ist, bis Sie die Konsole erneut mit dem Standort verbinden.  



<!--HONumber=Nov16_HO1-->


