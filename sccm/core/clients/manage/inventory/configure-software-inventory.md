---
title: Konfigurieren einer Softwareinventur | Microsoft-Dokumentation
description: Richten Sie die Softwareinventur und einen Inventurausschlussordner in System Center Configuration Manager ein.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: cc226259-0e28-410a-94d3-223bdc948818
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 7ba943bee7faf417099cde0388649e4907525738


---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Konfigurieren der Softwareinventur in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können eine ausgeblendete Datei namens **Skpswi.dat** erstellen und im Stammverzeichnis einer Clientfestplatte speichern, um diese aus der System Center Configuration Manager-Softwareinventur auszuschließen. Sie können diese Datei auch im Stammordner einer Ordnerstruktur ablegen, die Sie von der Softwareinventur ausschließen möchten. Mit dieser Prozedur können Sie die Softwareinventur auf einer Arbeitsstation oder einem Serverclient, z. B. einem großen Dateiserver, deaktivieren.  

> [!NOTE]  
>  Die Softwareinventur inventarisiert das Clientlaufwerk nicht noch einmal, außer diese Datei wird vom Laufwerk auf dem Clientcomputer gelöscht.  

### <a name="to-exclude-folders-from-software-inventory"></a>So schließen Sie Ordner aus der Softwareinventur aus  

1.  Erstellen Sie mit "Notepad.exe" eine leere Datei namens **Skpswi.dat**.  

2.  Klicken Sie mit der rechten Maustaste auf die Datei **Skpswi.dat** , und klicken Sie dann auf **Eigenschaften**. Wählen Sie in den Dateieigenschaften für die Datei "Skpswi.dat" das Attribut **Ausgeblendet** aus.  

3.  Platzieren Sie die Datei **Skpswi.dat** im Stammverzeichnis jeder Clientfestplatte oder Ordnerstruktur, die von der Softwareinventur ausgeschlossen werden soll.  



<!--HONumber=Dec16_HO3-->


