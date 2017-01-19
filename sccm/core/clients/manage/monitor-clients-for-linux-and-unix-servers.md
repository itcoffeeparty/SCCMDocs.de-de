---
title: "Überwachen von Clients | System Center Configuration Manager | Linux UNIX "
description: "Clients auf Linux- und UNIX-Servern können in System Center Configuration Manager überwacht werden."
ms.custom: na
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
caps.latest.revision: 6
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 620c1caf50b4859afc8f32490ab7945df810aefd
ms.openlocfilehash: b2b7c88784eed6fbee6ac1f6348d7d6991df1fbb


---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Überwachen von Clients für Linux- und UNIX-Server in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können in der System Center Configuration Manager-Konsole Informationen von Linux- und UNIX-Servern mithilfe derselben Methoden anzeigen, die Sie auch zum Anzeigen von Informationen von Windows-basierten Clients verwenden.  

 Die Informationen, die Sie anzeigen können, umfassen Folgendes:  

-   Statusdetails von Clients in den Dashboards der Configuration Manager-Konsole  

-   Details zu Clients in den Configuration Manager-Standardberichten  

-   Inventurdetails im Ressourcen-Explorer  

 In den folgenden Abschnitten wird beschrieben, wie man diese Details vom Ressourcen-Explorer und von den Berichten erhält.  

##  <a name="a-namebkmkuseresourceexpforlnua-use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a> Verwenden des Ressourcen-Explorers zur Anzeige von Inventuren für Linux- und UNIX-Server  
 
 Nachdem ein Configuration Manager-Client die Hardwareinventur an den Configuration Manager-Standort gesendet hat, können Sie Ressourcen-Explorer zum Anzeigen dieser Informationen verwenden. Der Configuration Manager-Client für Linux und UNIX fügt keine neuen Klassen oder Ansichten für die Inventur zu Ressourcen-Explorer hinzu. Die Linux- und UNIX-Inventurdaten werden vorhandenen WMI-Klassen zugeordnet. Mit dem Ressourcen-Explorer können Sie die Inventurdetails für Ihre Linux- und UNIX-Server in den Windows-basierten Klassifikationen anzeigen.  

 Beispielsweise können Sie die Liste aller systemeigen installierten Programme zusammenstellen, die auf den Linux- und UNIX-Servern gefunden werden. Beispiele für systemeigen installierte Programme umfassen **RPMS** in Linux oder **PKGS** in Solaris. Nachdem die Inventur von einem Linux- oder UNIX-Client gesendet wurde, können Sie die Liste aller nativ installierten Linux- oder UNIX-Programme im Ressourcen-Explorer in der Configuration Manager-Konsole anzeigen.  

 Informationen zur Verwendung von Ressourcen-Explorer finden Sie unter [How to use Resource Explorer to view hardware inventory in System Center Configuration Manager (Verwenden von Ressourcen-Explorer zum Anzeigen des Hardwarebestands in System Center Configuration Manager)](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="a-namebkmkusereportsforlnua-how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> Verwenden von Berichten zur Anzeige von Informationen für Linux- und UNIX-Server  
 Berichte für Configuration Manager enthalten Informationen von Linux- und UNIX-Servern zusammen mit Informationen von Windows-basierten Computern. Es sind keine zusätzlichen Konfigurationen erforderlich, um die Linux- und UNIX-Daten in die Berichte zu integrieren.  

 Wenn Sie beispielsweise den Bericht zur Anzahl der Betriebssystemversionen ausführen, wird die Liste der verschiedenen Betriebssysteme und die Anzahl der Clients, auf denen das jeweilige Betriebssystem ausgeführt wird, angezeigt. Der Bericht basiert auf den Hardwareinventurinformationen, die von den verschiedenen Configuration Manager-Clients, auf denen die unterschiedlichen Betriebssysteme ausgeführt werden, gesendet wurden.  

 Es können auch benutzerdefinierte Berichte erstellt werden, die für Linux- und UNIX-Serverdaten spezifisch sind. Die Eigenschaft **Caption** der Hardwareinventurklasse **Operating System** ist ein nützliches Attribut, mit dem Sie bestimmte Betriebssysteme in der Berichtsabfrage ermitteln können.  

 Informationen zu Berichten in Configuration Manager finden Sie unter [Reporting in System Center Configuration Manager (Berichterstellung in System Center Configuration Manager)](../../../core/servers/manage/reporting.md).  



<!--HONumber=Dec16_HO3-->


