---
title: Softwareinventur für mobile Geräte, die bei Microsoft Intune registriert sind
titleSuffix: Configuration Manager
description: Softwareinventur für mobile Geräte, die bei Microsoft Intune registriert sind.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1aa0bb03b2e27aebbbf1c080b32445bc7c58c47
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Softwareinventur für mobile Geräte, die bei Microsoft Intune registriert sind

*Gilt für: System Center Configuration Manager (Current Branch)*

 Sie können Inventurdaten zu Apps sammeln, die auf mobilen Geräten installiert sind. Welche Apps inventarisiert werden, hängt davon ab, ob es sich um ein firmeneigenes Gerät handelt, oder ob das Gerät dem Benutzer gehört. Für persönliche Geräte werden nur von Microsoft Intune verwaltete Apps inventarisiert.  

> [!NOTE]  
>  Inventurdaten zu auf mobilen Geräten installierten Apps werden bei der [Hardwareinventur](mobile-device-hardware-inventory-hybrid.md) gesammelt.  

 Die folgende Liste umfasst die inventarisierten Apps für Geräte, die einem Benutzer gehören, und für Geräte, die dem Unternehmen gehören.  

|Plattform|Geräte, die einem Benutzer gehören|Geräte, die dem Unternehmen gehören|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (ohne Configuration Manager-Client)|Nur verwaltete Apps|Nur verwaltete Apps|
|Windows 8.1 (ohne Configuration Manager-Client)|Nur verwaltete Apps|Nur verwaltete Apps|  
|Windows Phone 8|Nur verwaltete Apps|Nur verwaltete Apps|  
|Windows RT|Nur verwaltete Apps|Nur verwaltete Apps|  
|iOS|Nur verwaltete Apps|Alle auf dem Gerät installierten Apps|  
|Android|Nur verwaltete Apps|Alle auf dem Gerät installierten Apps|  

Finden Sie unter [Einführung in die Softwareinventur](../../core/clients/manage/inventory/introduction-to-software-inventory.md) und [Konfigurieren der Softwareinventur ](../../core/clients/manage/inventory/configure-software-inventory.md) ausführliche Informationen zur Verwendung der Softwareinventur, um Dateiinformationen auf Clientgeräten zu sammeln.
