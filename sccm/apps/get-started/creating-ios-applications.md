---
title: Erstellen von iOS-Anwendungen | Microsoft Docs
description: "Was Sie beim Erstellen und Bereitstellen von Apps für iOS-Geräte berücksichtigen müssen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5420109-6538-4430-9ca6-db352ee84c2e
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: e9e34359f4412ba07b9fb49f871a1eb2d36cecf8
ms.openlocfilehash: eb2d1245932d71bd10fd63d95a155eae7d128836


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Erstellen von iOS-Apps mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Berücksichtigen Sie beim Erstellen und Bereitstellen von Apps für iOS-Geräte Folgendes.  

## <a name="general-considerations"></a>Allgemeine Aspekte  
 Configuration Manager unterstützt die Bereitstellung folgender App-Typen:  

|Gerätetyp|Unterstützte Dateien|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> In System Center Configuration Manager müssen Sie beim Importieren einer iOS-App keine Eigenschaftenliste (.plist) angeben.|  

 Die folgenden Bereitstellungsaktionen werden unterstützt:  

|Gerätetyp|Unterstützte Aktionen|  
|-----------------|-----------------------|  
|iOS|**Verfügbar**, **Erforderlich** Der Benutzer muss der Installation und Deinstallation zustimmen.

> [!IMPORTANT]  
>  Derzeit können Endbenutzer Unternehmens-Apps nicht über die Microsoft Intune-Unternehmensportal-App für iOS installieren. Der Grund sind für Apps geltende Einschränkungen, die im iOS App Store veröffentlicht werden (siehe App Store-Rezensionsrichtlinien, Abschnitt 2). Benutzer können Unternehmens-Apps (einschließlich verwalteter App Store-Apps und Branchenanwendungspakete) durch Navigieren zum Webportal von Intune auf ihrem Gerät installieren (portal.manage.microsoft.com). Weitere Informationen über die mobilen Verwaltungsfunktionen, die von der Intune-Unternehmensportal-App aktiviert werden, finden Sie unter [Verwaltungsfunktionen für registrierte Geräte in Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx).  



<!--HONumber=Dec16_HO3-->


