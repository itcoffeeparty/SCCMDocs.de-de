---
title: 'Überwachen von Linux/UNIX-Clients '
titleSuffix: Configuration Manager
description: Clients auf Linux- und UNIX-Servern können in System Center Configuration Manager überwacht werden.
ms.date: 08/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 68370a09dda49e16edd05fb545922f2e182f79a5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Überwachen von Clients für Linux- und UNIX-Server in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können in der System Center Configuration Manager-Konsole Informationen von Linux- und UNIX-Servern mithilfe derselben Methoden anzeigen, die Sie auch zum Anzeigen von Informationen von Windows-basierten Clients verwenden.  

 Die Informationen, die Sie anzeigen können, umfassen Folgendes:  

-   Statusdetails von Clients in den Dashboards der Configuration Manager-Konsole  

-   Details zu Clients in den Configuration Manager-Standardberichten  

-   Inventurdetails im Ressourcen-Explorer  

 In den folgenden Abschnitten wird beschrieben, wie Sie diese Details aus dem Ressourcen-Explorer und den Berichten erhalten.  

##  <a name="BKMK_UseResourceExpforLnU"></a> Verwenden des Ressourcen-Explorers zur Anzeige von Inventuren für Linux- und UNIX-Server  

 Nachdem ein Configuration Manager-Client die Hardwareinventur an den Configuration Manager-Standort gesendet hat, können Sie Ressourcen-Explorer zum Anzeigen dieser Informationen verwenden. Der Configuration Manager-Client für Linux und UNIX fügt keine neuen Klassen oder Ansichten für die Inventur zu Ressourcen-Explorer hinzu. Die Linux- und UNIX-Inventurdaten werden vorhandenen WMI-Klassen zugeordnet. Mit dem Ressourcen-Explorer können Sie die Inventurdetails für Ihre Linux- und UNIX-Server in den Windows-basierten Klassifikationen anzeigen.  

 Beispielsweise können Sie die Liste aller systemeigen installierten Programme zusammenstellen, die auf den Linux- und UNIX-Servern gefunden werden. Beispiele für systemeigen installierte Programme umfassen **RPMS** in Linux oder **PKGS** in Solaris. Nachdem die Inventur von einem Linux- oder UNIX-Client gesendet wurde, können Sie die Liste aller nativ installierten Linux- oder UNIX-Programme im Ressourcen-Explorer in der Configuration Manager-Konsole anzeigen.  

 Informationen zur Verwendung von Ressourcen-Explorer finden Sie unter [How to use Resource Explorer to view hardware inventory in System Center Configuration Manager (Verwenden von Ressourcen-Explorer zum Anzeigen des Hardwarebestands in System Center Configuration Manager)](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="BKMK_UseReportsforLnU"></a> Verwenden von Berichten zur Anzeige von Informationen für Linux- und UNIX-Server  
 Berichte für Configuration Manager enthalten Informationen von Linux- und UNIX-Servern zusammen mit Informationen von Windows-basierten Computern. Es sind keine zusätzlichen Konfigurationen erforderlich, um die Linux- und UNIX-Daten in die Berichte zu integrieren.  

 Wenn Sie beispielsweise den Bericht zur Anzahl der Betriebssystemversionen ausführen, wird die Liste der verschiedenen Betriebssysteme und die Anzahl der Clients, auf denen das jeweilige Betriebssystem ausgeführt wird, angezeigt. Der Bericht basiert auf den Hardwareinventurinformationen, die von den verschiedenen Configuration Manager-Clients, auf denen die unterschiedlichen Betriebssysteme ausgeführt werden, gesendet wurden.  

 Es können auch benutzerdefinierte Berichte erstellt werden, die für Linux- und UNIX-Serverdaten spezifisch sind. Die Eigenschaft **Caption** der Hardwareinventurklasse **Operating System** ist ein nützliches Attribut, mit dem Sie bestimmte Betriebssysteme in der Berichtsabfrage ermitteln können.  

 Informationen zu Berichten in Configuration Manager finden Sie unter [Reporting in System Center Configuration Manager (Berichterstellung in System Center Configuration Manager)](../../../core/servers/manage/reporting.md).  
