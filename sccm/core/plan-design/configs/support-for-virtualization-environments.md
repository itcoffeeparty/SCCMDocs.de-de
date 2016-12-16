---
title: "Unterstützung für die Virtualisierung | System Center Configuration Manager"
description: "Rufen Sie die Anforderungen für die Installation der System Center Configuration Manager-Client- und Standortsystemrollen in einer Virtualisierungsumgebung ab."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: be32ccee17bc4829888d42dfff3f2818f4fc2810


---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>Unterstützung für Virtualisierungsumgebungen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Configuration Manager unterstützt die Installation von Client- und Standortsystemrollen auf unterstützten Betriebssystemen, die als virtueller Computer in den folgenden Virtualisierungsumgebungen ausgeführt werden. Dies gilt auch, wenn der Host für virtuelle Computer (Virtualisierungsumgebung) nicht als Client oder Standortserver unterstützt wird.  

 **Beispiel:**Wenn Sie Microsoft Hyper-V Server 2012 beispielsweise zum Hosten eines virtuellen Computers verwenden, auf dem Windows Server 2012 ausgeführt wird, können Sie die Client- oder Standortsystemrollen auf dem virtuellen Computer (Windows Server 2012), aber nicht auf dem Host (Microsoft Hyper-V Server 2012) installieren.  

|Virtualisierungsumgebung|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|  

 Für jeden von Ihnen verwendeten virtuellen Computer gelten die gleichen Mindestanforderungen für Hardware und Software wie für einen physischen Configuration Manager-Computer.  

 Sie können mithilfe des Programms zur Validierung der Servervirtualisierung und des Online-Richtlinienassistenten für die Virtualisierungsunterstützung überprüfen, ob Ihre Virtualisierungsumgebung für Configuration Manager unterstützt wird. Weitere Informationen zum Programm zur Validierung der Servervirtualisierung finden Sie unter [Windows Server Virtualization Validation Program (Programm zur Validierung der Windows-Servervirtualisierung)](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
>  Configuration Manager unterstützt keine auf Macintosh ausgeführten Virtual PC- oder Virtual Server-Gastbetriebssysteme.  

Mit Configuration Manager ist die Verwaltung virtueller Computer nur möglich, wenn diese online sind. Ein virtueller Computer im Offlinemodus kann weder aktualisiert noch können Inventurdaten mithilfe des Configuration Manager-Clients auf dem Hostcomputer gesammelt werden.  

Für virtuelle Computer werden keine speziellen Vorkehrungen getroffen. Beispielsweise erkennt Configuration Manager möglicherweise nicht, ob auf das Image eines virtuellen Computers, auf den ein Update angewendet wurde, das Update erneut angewendet werden muss, wenn der virtuelle Computer ohne vorheriges Speichern seines Status heruntergefahren und neu gestartet wird.  

##  <a name="a-namebkmkazurea-microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Virtuelle Microsoft Azure-Computer  
 Configuration Manager kann auf virtuellen Computern in Microsoft Azure genau wie auf lokalen Computern innerhalb des physischen Unternehmensnetzwerks ausgeführt werden. Sie können Configuration Manager mit virtuellen Computern in Microsoft Azure in den folgenden Szenarios nutzen:  

-   **Szenario 1:** Sie können Configuration Manager auf einem virtuellen Microsoft Azure-Computer ausführen und zum Verwalten von auf anderen virtuellen Microsoft Azure-Computern installierten Clients verwenden.  

-   **Szenario 2:** Sie können Configuration Manager auf einem virtuellen Microsoft Azure-Computer ausführen und zum Verwalten von Clients verwenden, die nicht in Microsoft Azure ausgeführt werden.  

-   **Szenario 3:** Sie können verschiedene Configuration Manager-Standortsystemrollen auf virtuellen Microsoft Azure-Computern ausführen, während Sie andere Rollen im physischen Unternehmensnetzwerk (mit der entsprechenden Netzwerkkonnektivität für die Kommunikation) ausführen.  

Für die Installation in Microsoft Azure gelten die gleichen System Center Configuration Manager-Anforderungen für Netzwerke, unterstützte Konfigurationen und Hardwareanforderungen wie für die lokale Installation von Configuration Manager in Ihrem physischen Unternehmensnetzwerk.  

> [!IMPORTANT]  
>  Für Configuration Manager-Standorte und -Clients, die auf virtuellen Azure-Computern ausgeführt werden, gelten die gleichen Lizenzanforderungen wie für lokale Installationen.  



<!--HONumber=Nov16_HO1-->


