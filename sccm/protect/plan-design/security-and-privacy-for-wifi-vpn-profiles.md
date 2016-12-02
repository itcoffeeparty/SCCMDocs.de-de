---
title: "Sicherheit und Datenschutz für WLAN- und VPN-Profile | System Center Configuration Manager"
description: "Erfahren Sie mehr über bewährte Sicherheitsmethoden für die Verwaltung von WLAN- und VPN-Profilen für Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 10/19/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 32dff36aa8027b0563b999e7fe6ef41d0eb79020
ms.openlocfilehash: b9d70018708ab5932a3032134b03aef236ef9fda


---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz für WLAN- und VPN-Profile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Dieses Thema enthält Sicherheits- und Datenschutzinformationen für WLAN- und VPN-Profile in System Center Configuration Manager.  

##  <a name="a-namebkmksecurityremoteconnectionsa-security-best-practices-for-wi-fi-and-vpn-profiles"></a><a name="BKMK_Security_RemoteConnections"></a> Bewährte Sicherheitsmethoden für WLAN- und VPN-Profile  
 Verwenden Sie die folgenden bewährten Sicherheitsmethoden bei der Verwaltung von WLAN- und VPN-Profilen für Geräte.  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Wählen Sie nach Möglichkeit die sichersten Optionen aus, die von der WLAN- und VPN-Infrastruktur sowie den Clientbetriebssystemen unterstützt werden.|WLAN- und VPN-Profile stellen eine praktische Methode dar, um von Ihren Geräten bereits unterstützte WLAN- und VPN-Einstellungen zentral zu verteilen und zu verwalten. System Center Configuration Manager bietet keine zusätzlichen WLAN- oder VPN-Funktionen.<br /><br /> Bestimmen, implementieren und beachten Sie die bewährten Sicherheitsmethoden, die für Ihre Geräte und die Infrastruktur empfohlen wurden.|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Datenschutzinformationen für WLAN-Profile  
 Sie können WLAN- und VPN-Profile verwenden, um Clientgeräte für die Verbindung mit WLAN- und VPN-Servern zu konfigurieren, und dann auswerten, ob diese Geräte nach der Anwendung der Profile Kompatibilität erreichen. Vom Verwaltungspunkt werden Kompatibilitätsinformationen an den Standortserver gesendet, die dann in der Standortdatenbank gespeichert werden. Die Informationen werden verschlüsselt, wenn sie von Geräten an den Verwaltungspunkt gesendet werden, sie werden aber nicht in einem verschlüsselten Format in der Standortdatenbank gespeichert. Die Informationen verbleiben in der Datenbank, bis sie mit dem Standortwartungstask **Veraltete Konfigurationsverwaltungsdaten löschen** gelöscht werden. Das Löschintervall beträgt standardmäßig 90 Tage, kann aber geändert werden. Die Kompatibilitätsinformationen werden nicht an Microsoft gesendet.  

 Standardmäßig werden WLAN- und VPN-Profile nicht von Geräten ausgewertet. Darüber hinaus müssen Sie die Profile konfigurieren und sie dann für Benutzer bereitstellen.  

 Berücksichtigen Sie vor dem Konfigurieren der WLAN- und VPN-Profile Ihre Datenschutzanforderungen.  



<!--HONumber=Nov16_HO1-->


