---
title: 'Verwalten von Clients in einer virtuellen Desktopinfrastruktur (VDI) '
titleSuffix: Configuration Manager
description: Verwalten Sie System Center Configuration Manager-Clients in einer virtuellen Desktopinfrastruktur (VDI).
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
caps.latest.revision: "7"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 1d35865895a8837d4c30a4f43967f777e61d7cbf
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2017
---
# <a name="considerations-for-managing-system-center-configuration-manager-clients--in-a-virtual-desktop-infrastructure-vdi"></a>Überlegungen zum Verwalten von System Center Configuration Manager-Clients in einer virtuellen Desktopinfrastruktur (VDI)

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager unterstützt die Installation des Configuration Manager-Clients auf den folgenden Szenarios einer virtuellen Desktopinfrastruktur (VDI):  

-   **Persönliche virtuelle Computer**: Persönliche virtuelle Computer werden normalerweise verwendet, wenn Sie sicherstellen möchten, dass Benutzerdaten und Benutzereinstellungen auf dem virtuellen Computer zwischen den Sitzungen beibehalten werden.  

-   **Remotedesktopdienste-Sitzungen**: Mit Remotedesktopdiensten können mehrere Clientsitzungen zugleich auf einem Server gehostet werden. Benutzer können eine Verbindung zu einer Sitzung herstellen und dann Anwendungen auf diesem Server ausführen.  

-   **Zusammengefasste virtuelle Computer**: Virtuelle Computer, die in einem Pool zusammengefasst sind, werden zwischen den Sitzungen nicht beibehalten. Wenn eine Sitzung geschlossen wird, werden alle Daten und Einstellungen verworfen. Zusammengefasste virtuelle Computer sind nützlich, wenn die Remotedesktopdienste nicht verwendet werden können, weil eine erforderliche Geschäftsanwendung nicht auf dem Windows-Server, auf dem die Clientsitzung gehostet wird, ausgeführt werden kann.  

 In der folgenden Tabelle sind Überlegungen zur Verwaltung des Configuration Manager-Clients in einer virtuellen Desktopinfrastruktur aufgelistet.  

|Virtueller Computertyp|Überlegungen|  
|--------------------------|--------------------|  
|Persönliche virtuelle Computer|Persönliche virtuelle Computer und physische Computer werden von Configuration Manager identisch behandelt. Der Configuration Manager-Client kann auf dem Image eines virtuellen Computers vorinstalliert oder nach der Bereitstellung des virtuellen Computers bereitgestellt werden.|  
|Remotedesktopdienste|Der Configuration Manager-Client wird nicht für einzelne Remotedesktopsitzungen installiert. Er wird nur einmal auf dem Remotedesktopdienste-Server installiert. Alle Configuration Manager-Funktionen können auf dem Remotedesktopdienste-Server verwendet werden.|  
|Zusammengefasste virtuelle Computer|Wenn ein in einem Pool zusammengefasster, virtueller Computer außer Betrieb genommen wird, gehen Änderungen, die Sie mithilfe von Configuration Manager vorgenommen haben, verloren.<br /><br /> Daten, die von Configuration Manager-Funktionen wie Hardwareinventur, Softwareinventur und Softwaremessung zurückgegeben werden, sind für Ihren Bedarf möglicherweise nicht relevant, da der virtuelle Computer möglicherweise nur für eine kurze Dauer funktionsfähig ist. Erwägen Sie, zusammengefasste virtuelle Computer von Inventurtasks auszuschließen.|  

 Bei der Virtualisierung ist die Ausführung mehrerer Configuration Manager-Clients auf dem gleichen physischen Computer möglich. Aus diesem Grund haben viele Clientvorgänge eine integrierte zufällige Verzögerung für geplante Aktionen wie Hardware- und Softwareinventur, Antischadsoftwareüberprüfungen, Softwareinstallationen und Softwareupdateüberprüfungen. Hierdurch lassen sich die Prozessorauslastung und die Datenübertragung für einen Computer, der mehrere virtuelle Computer mit dem Configuration Manager-Client hat, leichter verteilen.  

> [!NOTE]  
>  Diese zufällige Verzögerung wird auch von Configuration Manager-Clients verwendet, die nicht in virtualisierten Umgebungen ausgeführt werden, wobei Windows Embedded-Clients, die sich im Wartungsmodus befinden, die Ausnahme bilden. Wenn es viele bereitgestellte Clients gibt, lassen sich mit diesem Verhalten Spitzen bei der Netzwerkbandbreite vermeiden und die Prozessoranforderungen in den Configuration Manager-Standortsystemen verringern, beispielsweise auf dem Verwaltungspunkt und Standortserver. Das Verzögerungsintervall hängt von der Configuration Manager-Funktionalität ab.  
>   
>  Die zufällige Verzögerung wird für erforderliche Softwareupdates und Anwendungsbereitstellungen mithilfe der Clienteinstellung **Zufällige Stichtaganordnung deaktivieren**unter **Computer-Agent**standardmäßig deaktiviert.
