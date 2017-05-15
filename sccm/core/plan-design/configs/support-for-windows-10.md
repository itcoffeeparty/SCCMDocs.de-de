---
title: "Unterstützung für Windows 10 | Microsoft-Dokumentation"
description: "Informationen Sie zu den Windows-10-Versionen, die als Clients oder für OSD mit System Center Configuration Manager unterstützt werden."
ms.custom: na
ms.date: 05/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 065b1fcb25d7c7845b6f26e757b36e7fb97ce013
ms.openlocfilehash: 2ec25e9b093d9451d8880ba36f4d022ec4bad001
ms.contentlocale: de-de
ms.lasthandoff: 05/10/2017

---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>Unterstützung von Windows 10 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 In diesem Thema werden die Versionen von Windows 10 behandelt, die Sie mit verschiedenen Versionen von Current Branch in System Center Configuration Manager verwenden können. Dies umfasst u. a.:
 -  Windows 10 als Configuration Manager-Client.
 -  Das Windows Assessment and Deployment Kit (ADK) von Windows 10.

## <a name="windows-10-as-a-client"></a>Windows 10 als Client
Configuration Manager versucht, jede neue Version von Windows 10 so bald wie möglich, nachdem die Version veröffentlicht wurde, als Client zu unterstützen. Da die Produkte über getrennte Zeitpläne für Entwicklung und Freigabe verfügen, hängt die Unterstützung von Configuration Manager davon ab, wann die Versionen und Verzweigungen jedes Produkts freigegeben werden.

Eine Version von Configuration Manager, deren [Support für diese Version](/sccm/core/servers/manage/current-branch-versions-supported) eingestellt wurde, wird aus der Kompatibilitätsmatrix. Ebenso wird der Support für Windows 10 Versionen wie Enterprise 2015 LTSB oder 1607 (CBB) aus der Kompatibilitätsmatrix entfernt, wenn sie von der Liste der unterstützten Konfigurationen von Configuration Manager entfernt werden. Weitere Informationen finden Sie unter [Veraltete Betriebssysteme](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems).

-   Die folgenden Informationen ergänzen die [unterstützten Betriebssysteme für Clients und Geräte](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Wenn Sie Long-Term Servicing Branch von Configuration Manager verwenden, finden Sie weitere Informationen unter [Unterstützte Konfigurationen für LTSB (Long-Term Servicing Branch) von System Center Configuration Manager](/sccm/core/understand/supported-configurations-for-ltsb).

|Windows 10-Versionen                    |Configuration Manager 1606          |Configuration Manager 1610          |    Configuration Manager 1702 |
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB                   |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|1507 <br />(*siehe Editionen*)            |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|1511 (CB), (CBB)<br />(*siehe Editionen*) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|Enterprise 2016 LTSB                   |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|1607 (CB)    <br />Anniversary Update<br />(*siehe Editionen*)      |![Abwärtskompatibel](media/blue_compat.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|1607 (CBB)    <br />Anniversary Update<br />(*siehe Editionen*)      |![Nicht unterstützt](media/Red_X.png)   |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|1703 (CB)    <br />Creators Update<br />(*siehe Editionen*)      |![Nicht unterstützt](media/Red_X.png)   |![Nicht unterstützt](media/Red_X.png) |![Abwärtskompatibel](media/blue_compat.png) |


**Editionen:** Enterprise, Pro, Education, Pro Education   

|Schlüssel|
|--|
|![Unterstützt](media/green_check.png) = **Unterstützt**  |
|![Nicht unterstützt](media/blue_compat.png)  = **Abwärtskompatibel**: Dies bedeutet, dass vorhandene Clientverwaltungsfunktionen (Hardwareinventur, Softwareinventur, Softwareupdates usw.) mit dem neuen Build von Windows 10 Current Branch arbeiten sollten. Bekannte Probleme oder Vorbehalte werden dokumentiert werden. <br><br>Dieser Ansatz bietet Ihnen die Möglichkeit zur Bereitstellung und Verwaltung der neuen Windows 10 CB Builds am ersten Tag mit Unterstützung der Anwendungskompatibilität, ohne dass eine neue Updateversion von Configuration Manager erforderlich ist. |
|![Unterstützt](media/Red_X.png) = **Nicht unterstützt**|


## <a name="windows-10-adk"></a>Windows 10 ADK
Beim Bereitstellen von Betriebssystemen mit Configuration Manager ist das [Windows ADK eine externe Abhängigkeit](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment), die erforderlich ist.

Die folgende Tabelle listet die Versionen des Windows 10 ADK auf, die Sie mit verschiedenen Versionen von Configuration Manager verwenden können.

|Windows 10-Versionen |Configuration Manager 1606 |Configuration Manager 1610  |Configuration Manager 1702 |
|--------------------|-----|-----|-----|
|1507  |![Nicht unterstützt](media/Red_X.png)         |![Nicht unterstützt](media/Red_X.png)  |![Nicht unterstützt](media/Red_X.png)|
|1511  |![Abwärtskompatibel](media/blue_compat.png)|![Nicht unterstützt](media/Red_X.png)  |![Nicht unterstützt](media/Red_X.png)|
|1607  |![Unterstützt](media/green_check.png)       |![Unterstützt](media/green_check.png)|![Abwärtskompatibel](media/blue_compat.png) |
|1703  |![Nicht unterstützt](media/Red_X.png)         |![Nicht unterstützt](media/Red_X.png)  |![Unterstützt](media/green_check.png) |  

|Schlüssel|
|--|
|![Unterstützt](media/green_check.png) = **Unterstützt**: Windows empfiehlt das Verwenden des Windows ADK, das der Windows-Version entspricht, die Sie bereitstellen. Verwenden Sie z. B. das Windows ADK für Windows 10, Version 1703, bei Bereitstellung der Windows 10-Version 1703.  |
|![Abwärtskompatibel](media/blue_compat.png)  = **Abwärtskompatibel**: Diese Kombination wurde nicht getestet, sollte jedoch funktionieren. Bekannte Probleme oder Vorbehalte werden dokumentiert werden. |
|![Unterstützt](media/Red_X.png) = **Nicht unterstützt**|

