---
title: Softwareinventur | Microsoft-Dokumentation
description: "Erhalten Sie eine Einführung in die Softwareinventur in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a468ce93e9536fe3f6bf0fc191ff9764dd1c3343
ms.openlocfilehash: 401ba6e37d740310d49ab9e96112ce576d7130e4


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Einführung in die Softwareinventur in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sammeln Sie mit der Softwareinventur in System Center Configuration Manager Informationen zu Dateien, die auf Clientgeräten in Ihrer Organisation vorliegen. Zusätzlich können bei der Softwareinventur Dateien von Clientgeräten gesammelt und auf dem Standortserver gespeichert werden. Das Softwareinventar wird gesammelt, wenn in den Clienteinstellungen die Einstellung **Softwareinventur auf Clients aktivieren** aktiviert ist.  

 Nachdem die Softwareinventur aktiviert und ein Softwareinventurzyklus vom Client ausgeführt wurde, werden die vom Client gesammelten Inventurinformationen an einen Verwaltungspunkt am Standort des Clients gesendet. Der Verwaltungspunkt leitet diese Inventurinformationen an den Configuration Manager-Standortserver weiter, auf dem die Inventurinformationen in der Standortdatenbank gespeichert werden. Die Softwareinventur wird auf Clients gemäß dem Zeitplan ausgeführt, den Sie in den Clienteinstellungen festlegen.  

 Sie können die von Configuration Manager gesammelten Softwareinventurdaten unter Zuhilfenahme mehrerer Methoden anzeigen. Dazu gehören die folgenden:  

-   Erstellen von Abfragen, von denen Geräte basierend auf den von Ihnen angegebenen, auf den Geräten befindlichen Dateien zurückgegeben werden. Weitere Informationen finden Sie unter [Abfragen – Technische Referenz für System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

-   Erstellen von abfragebasierten Sammlungen basierend auf von Ihnen angegebenen, auf den Geräten befindlichen Dateien. Mitgliedschaften abfragebasierter Sammlungen werden automatisch nach einem Zeitplan aktualisiert. Sie können für eine Reihe von Tasks, wie z. B. die Softwarebereitstellung, Sammlungen verwenden. Weitere Informationen finden Sie unter [Einführung in Sammlungen in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).  

-   Ausführen von Berichten, in denen spezifische Details zu Geräten in Ihrer Organisation angezeigt werden. Weitere Informationen finden Sie unter [Berichterstellung in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

-   Anzeigen von detaillierten Informationen zu Dateien im Ressourcen-Explorer, die inventarisiert und von Clientgeräten gesammelt wurden. Weitere Informationen finden Sie unter [Anzeigen des Softwareinventars mit dem Ressourcen-Explorer in System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

 Beim Ausführen der Softwareinventur auf einem Clientgerät enthält der erste zurückgegebene Inventurbericht immer ein vollständiges Inventar. Alle nachfolgenden Inventurberichte enthalten lediglich Deltainventurinformationen. Vom Standortserver werden die Deltainventurinformationen in der Reihenfolge verarbeitet, in der sie empfangen wurden. Falls Deltainventurinformationen für einen Client fehlen, werden weitere Deltainventurinformationen vom Standortserver zurückgewiesen, und der Client erhält die Anweisung für einen vollständigen Inventurzyklus.  

 Configuration Manager bietet eingeschränkte Unterstützung für Dual-Boot-Computer. Eine Ermittlung von Dual-Boot-Computern ist in Configuration Manager zwar möglich, es werden jedoch nur die Inventurinformationen von dem Betriebssystem zurückgegeben, das zum Zeitpunkt der Inventur aktiv war.  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Softwareinventur für mobile Geräte, die bei Microsoft Intune registriert sind  
 Sie können Inventurdaten zu Apps sammeln, die auf mobilen Geräten installiert sind. Welche Apps inventarisiert werden, hängt davon ab, ob es sich um ein firmeneigenes Gerät handelt, oder ob das Gerät dem Benutzer gehört. Für persönliche Geräte werden nur von Microsoft Intune verwaltete Apps inventarisiert.  

> [!NOTE]  
>  Die Inventurdaten der auf mobilen Geräten installierten Apps werden als Teil der Hardwareinventur in Configuration Manager gesammelt. Weitere Informationen finden Sie unter [Konfigurieren von Hardwareinventur für mobile Geräte, die von Microsoft Intune und System Center Configuration Manager registriert werden](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md).  

 Die folgende Tabelle enthält eine Liste der inventarisierten Apps für Geräte, die einem Benutzer gehören, und für Geräte, die dem Unternehmen gehören.  

|Plattform|Geräte, die einem Benutzer gehören|Geräte, die dem Unternehmen gehören|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (ohne Configuration Manager-Client)|Nur verwaltete Apps|Nur verwaltete Apps| 
|Windows 8.1 (ohne Configuration Manager-Client)|Nur verwaltete Apps|Nur verwaltete Apps|  
|Windows Phone 8|Nur verwaltete Apps|Nur verwaltete Apps|  
|Windows RT|Nur verwaltete Apps|Nur verwaltete Apps|  
|iOS|Nur verwaltete Apps|Alle auf dem Gerät installierten Apps|  
|Android|Nur verwaltete Apps|Alle auf dem Gerät installierten Apps|  



<!--HONumber=Dec16_HO3-->


