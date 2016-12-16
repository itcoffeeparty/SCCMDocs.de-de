---
title: "Sicherheit und Datenschutz für die Energieverwaltung | System Center Configuration Manager"
description: "Hier finden Sie Informationen zu Sicherheit und Datenschutz für die Energieverwaltung in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 26880f6682e2bdf61cb7f29416e5dfded3559e8e


---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz für die Energieverwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieser Abschnitt enthält Informationen zu Sicherheit und Datenschutz für die Energieverwaltung in System Center Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Bewährte Sicherheitsmethoden für die Energieverwaltung  
 Für die Energieverwaltung sind keine bewährten Sicherheitsmethoden vorhanden.  

## <a name="privacy-information-for-power-management"></a>Informationen zum Datenschutz für die Energieverwaltung  
 Zur Überwachung des Energieverbrauchs und zum Anwenden von Energieeinstellungen auf Computer während und außerhalb der Geschäftszeiten nutzt die Energieverwaltung in Windows integrierte Funktionen. Configuration Manager sammelt Informationen zum Energieverbrauch von Computern, beispielsweise auch zu den Computernutzungszeiten von Benutzern. Obwohl von Configuration Manager nur der Energieverbrauch einer Sammlung und nicht jedes Computers überwacht wird, ist es möglich, eine Sammlung mit nur einem Computer zu überwachen. Die Energieverwaltung ist standardmäßig nicht aktiviert und muss von einem Administrator konfiguriert werden.  

 Die Informationen zum Energieverbrauch werden in der Configuration Manager-Datenbank gespeichert und nicht an Microsoft gesendet. Ausführliche Informationen werden 31 Tage in der Datenbank gespeichert, zusammengefasste Informationen 13 Monate. Das Löschintervall kann nicht konfiguriert werden.  

 Berücksichtigen Sie beim Konfigurieren der Energieverwaltung Ihre Datenschutzanforderungen.  



<!--HONumber=Nov16_HO1-->


