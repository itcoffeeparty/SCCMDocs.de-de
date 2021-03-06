---
title: Konformitätsrichtlinien für Geräte
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Konformitätsrichtlinien in System Center Configuration Manager verwalten, damit Geräte als konform mit Richtlinien für bedingten Zugriff eingestuft werden können.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 776af7499c576f21d47dafec8a668f3c4051ad88
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

**Kompatibilitätsrichtlinien** in System Center Configuration Manager definieren die Regeln und Einstellungen, die ein Gerät erfüllen muss, damit es als kompatibel mit Richtlinien für bedingten Zugriff eingestuft wird. Konformitätsrichtlinien ermöglichen Ihnen auch, Konformitätsprobleme bei Geräten unabhängig von bedingten Zugriffsrechten zu überwachen und zu beheben.  


> [!IMPORTANT]  
>  In diesem Artikel werden die Kompatibilitätsrichtlinien für Geräte beschrieben, die von Microsoft Intune verwaltet werden.    Die Kompatibilitätsrichtlinien für PCs, die von System Center Configuration Manager verwaltet werden, sind unter [Verwalten des Zugriffs auf Office 365-Dienste für PCs, die von System Center Configuration Manager verwaltet werden](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md) beschrieben.  

 Diese Richtlinien schließen Anforderungen wie die folgenden ein:  

-   PIN und Kennwörter, um auf ein Gerät zuzugreifen

-   Verschlüsselung von auf dem Gerät gespeicherten Daten

-   Ob das Gerät per Jailbreak oder Rooting manipuliert wurde  

-   Ob der E-Mail-Dienst auf dem Gerät über eine Intune-Richtlinie verwaltet wird, oder ob das Gerät vom Windows-Integritätsnachweisdienst als fehlerhaft gemeldet wird.
-   Apps, die auf dem Gerät nicht installiert werden können.


 Sie stellen Konformitätsrichtlinien für Benutzer- und Gerätegruppen bereit. Wenn Sie eine Konformitätsrichtlinie für einen Benutzer bereitstellen, wird die Konformität aller Geräte des Benutzers überprüft.  

 Die folgende Tabelle enthält die von Konformitätsrichtlinien unterstützten Gerätetypen. Zudem ist darin angegeben, wie nicht konforme Einstellungen gehandhabt werden, wenn die Richtlinie mit einer bedingten Zugriffsrichtlinie verwendet wird.  

|Regel|Windows 8.1 und höher|Windows Phone 8.1 und höher|iOS 6.0 und höher|Android 4.0 und höher, Samsung KNOX Standard 4.0 und höher, Android for Work|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**PIN- oder Kennwortkonfiguration**|Wiederhergestellt|Wiederhergestellt|Wiederhergestellt|Isoliert|  
|**Geräteverschlüsselung**|N/V|Wiederhergestellt|Wiederhergestellt (durch Festlegen der PIN)|Isoliert<br>(Android for Work, immer verschlüsselt)|  
|**Gerät mit entfernten Nutzungsbeschränkungen**|N/V|N/V|Unter Quarantäne gestellt (keine Einstellung)|Unter Quarantäne gestellt (keine Einstellung)|  
|**E-Mail-Profil**|N/V|N/V|Isoliert|N/V|  
|**Minimales Release des Betriebssystems**|Isoliert|Isoliert|Isoliert|Isoliert|  
|**Maximales Release des Betriebssystems**|Isoliert|Isoliert|Isoliert|Isoliert|  
|**Integritätsnachweis des Geräts (Update 1602)**|Einstellung gilt nicht für Windows 8.1.<br /><br /> Windows 10 und Windows 10 Mobile werden isoliert.|N/V|N/V|N/V|  
|**Apps, die nicht installiert werden können**|N/V|N/V|Isoliert|Isoliert|

 **Wiederhergestellt** = Konformität wird vom Betriebssystem des Geräts erzwungen (z. B. wird der Benutzer gezwungen, eine PIN festzulegen).  Es gibt keinen Fall, in dem die Einstellung nicht konform ist.  

 **Unter Quarantäne** = Das Betriebssystem des Geräts erzwingt keine Konformität (z. B. zwingen Android-Geräte den Benutzer nicht dazu, das Gerät zu verschlüsseln).  Dies bedeutet:  

-   Das Gerät wird blockiert, wenn dem Benutzer eine bedingte Zugriffsrichtlinie zugewiesen wird.  

-   Das Unternehmensportal oder Webportal benachrichtigt den Benutzer bezüglich aller Konformitätsprobleme.  


### <a name="next-steps"></a>Nächste Schritte  
[Erstellen und Bereitstellen einer Gerätekompatibilitätsrichtlinie](create-compliance-policy.md)
### <a name="see-also"></a>Weitere Informationen:  
 [Verwalten des Zugriffs auf Dienste in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
