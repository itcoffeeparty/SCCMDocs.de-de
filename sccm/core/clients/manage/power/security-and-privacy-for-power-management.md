---
title: "Sicherheit und Datenschutz für die Energieverwaltung | Microsoft-Dokumentation"
description: "Hier finden Sie Informationen zu Sicherheit und Datenschutz für die Energieverwaltung in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
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
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: f72059973057e707f58cb6b7aa495226b6c1962c
ms.lasthandoff: 12/16/2016


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

