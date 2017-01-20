---
title: Anzeigen des Hardwareinventars | Microsoft-Dokumentation | Resource Explorer
description: Verwenden Sie den Ressourcen-Explorer zum Anzeigen des Hardwareinventars in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 2cd138b3bbb437d84f0ff7c2aeef869518bd817d


---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Anzeigen des Hardwareinventars mit dem Ressourcen-Explorer in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zeigen Sie mithilfe des Ressourcen-Explorers in System Center Configuration Manager Hardwareinventarinformationen an, die von Clients in Ihrer Hierarchie gesammelt wurden.  

> [!NOTE]  
>  Im Ressourcen-Explorer werden keine Inventurdaten angezeigt, bis auf dem Client, mit dem eine Verbindung hergestellt wird, ein Hardwareinventurzyklus ausgeführt wurde.  

 Der Ressourcen-Explorer in Configuration Manager enthält die folgenden Bereiche im Zusammenhang mit Hardwareinventar:  

-   **Hardware** - enthält das neueste Hardwareinventar von dem angegebenen Configuration Manager Client-Gerät. Sie können das Inventarelement **Status der Arbeitsstation** zum Ermitteln von Uhrzeit und Datum, wenn das Gerät eine Hardwareinventur zuletzt ausgeführt.  

-   **Hardwareverlauf** – enthält einen Verlauf inventarisierter Elemente, die sich seit der letzten Hardwareinventur geändert haben. Jedes Listenelement verfügt über einen **Current**-Knoten (Aktuell) und mindestens einen *<date\>*-Knoten (Datum). Sie können die Daten im aktuellen Knoten mit denen eines Verlaufsknotens vergleichen, um Elemente zu ermitteln, die sich im Hardwareinventar des Clientcomputers geändert haben.  

    > [!NOTE]  
    >  Der Hardwareinventurverlauf wird von Configuration Manager für die Anzahl von Tagen beibehalten, die Sie im Standortwartungstask **Veralteten Inventurverlauf löschen** festlegen.  

> [!NOTE]  
>  Informationen zum Anzeigen der Hardwareinventur von Clients, auf denen Linux und UNIX ausgeführt werden, finden Sie unter [How to monitor clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Ausführen des Ressourcen-Explorers über die Configuration Manager-Konsole  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Geräte** , oder öffnen Sie eine beliebige Sammlung, in der Geräte angezeigt werden.  

3.  Klicken Sie auf den Computer, der die anzuzeigende Inventur enthält. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Geräte** auf **Start** und dann auf **Ressourcen-Explorer**. Das Fenster **Ressourcen-Explorer** wird geöffnet.  

4.  Sie können auf allen Elementen im rechten Bereich des **Ressourcen-Explorer**-Fensters einen Rechtsklick ausführen und anschließend auf **Eigenschaften** klicken, um das Dialogfeld *<Elementname\>***Eigenschaften** zu öffnen. Dies kann nützlich sein, um die gesammelten Inventurinformationen in einem besser lesbaren Format anzuzeigen.  

5.  Wenn Sie fertig sind, schließen Sie das Fenster **Ressourcen-Explorer** .  



<!--HONumber=Dec16_HO3-->


