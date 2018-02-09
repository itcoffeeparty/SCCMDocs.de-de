---
title: "Unterstützung für Windows 10"
titleSuffix: Configuration Manager
description: "Informationen Sie zu den Windows-10-Versionen, die als Clients oder für OSD mit System Center Configuration Manager unterstützt werden."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2dfe9b63e9e7c41a4f8457dc5622f386c7cceec2
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>Unterstützung von Windows 10 für System Center Configuration Manager  

*Gilt für: System Center Configuration Manager (Current Branch)*


 In diesem Thema werden die Releases von Windows 10 behandelt, die Sie mit verschiedenen Versionen von Current Branch in System Center Configuration Manager verwenden können. Diese Unterstützung umfasst Folgendes:
 -  Windows 10 als Configuration Manager-Client
 -  Windows-Assessment and Deployment Kit (ADK) für Windows 10

## <a name="windows-10-as-a-client"></a>Windows 10 als Client
Configuration Manager versucht, jedes neue Release von Windows 10 so bald wie möglich nach der Veröffentlichung als Client zu unterstützen. Da die Produkte über getrennte Zeitpläne für Entwicklung und Freigabe verfügen, hängt die Unterstützung von Configuration Manager davon ab, wann sie jeweils verfügbar sind.

Beispielsweise wird eine Version von Configuration Manager, deren [Support für diese Version](/sccm/core/servers/manage/current-branch-versions-supported) eingestellt wurde, aus der Kompatibilitätsmatrix gelöscht. Ebenso wird der Support für Windows 10-Versionen wie Enterprise 2015 LTSB oder 1511 aus der Kompatibilitätsmatrix entfernt, sobald diese nicht mehr unterstützt werden. Weitere Informationen finden Sie unter [Veraltete Betriebssysteme](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).


-   Die folgenden Informationen ergänzen die [unterstützten Betriebssysteme für Clients und Geräte](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Wenn Sie Long-Term Servicing Branch von Configuration Manager verwenden, finden Sie weitere Informationen unter [Unterstützte Konfigurationen für LTSB (Long-Term Servicing Branch) von System Center Configuration Manager](/sccm/core/understand/supported-configurations-for-ltsb).

|Windows 10-Version                    |  Configuration Manager 1702          |    Configuration Manager 1706 |Configuration Manager 1710          |  
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB                   |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
|Enterprise 2016 LTSB                   |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
|1607   <br />(Auch Anniversary Update genannt)<br />(*siehe Editionen*)   |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png)            |![Unterstützt](media/green_check.png) |
|1703   <br />(Auch Creators Update genannt)<br />(*siehe Editionen*)      |![Abwärtskompatibel](media/blue_compat.png) |![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
|1709   <br />(Auch Fall Creators Update genannt)<br />(*siehe Editionen*) |![Nicht unterstützt](media/Red_X.png)   |![Abwärtskompatibel](media/blue_compat.png) | ![Unterstützt](media/green_check.png) |



**Editionen:** Enterprise, Pro, Education, Pro Education   

|Schlüssel|
|--|
|![Unterstützt](media/green_check.png) = **Unterstützt**  |
|![Nicht unterstützt](media/blue_compat.png)  = **Abwärtskompatibel**: Vorhandene Clientverwaltungsfeatures (Hardwareinventur, Softwareinventur, Softwareupdates usw.) müssen mit dem neuen Release von Windows 10 ausgeführt werden können. Wir werden alle bekannten Probleme und Einschränkungen dokumentieren. <br><br>Dieser Ansatz bietet Ihnen die Möglichkeit zur Bereitstellung und Verwaltung der neuen Windows-Builds am ersten Tag mit Unterstützung der Anwendungskompatibilität, ohne dass eine neue Updateversion von Configuration Manager erforderlich ist. |
|![Unterstützt](media/Red_X.png) = **Nicht unterstützt**|


## <a name="windows-10-adk"></a>Windows 10 ADK
Beim Bereitstellen von Betriebssystemen mit Configuration Manager ist das [Windows ADK eine externe Abhängigkeit](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment), die erforderlich ist.

Die folgende Tabelle listet die Versionen des Windows 10 ADK auf, die Sie mit verschiedenen Versionen von Configuration Manager verwenden können.

|Windows 10 ADK-Version  |Configuration Manager 1702   |Configuration Manager 1706 |Configuration Manager 1710 |
|--------------------|-----|-----|-----|
|1607  |![Abwärtskompatibel](media/blue_compat.png) |![Nicht unterstützt](media/Red_X.png)| ![Nicht unterstützt](media/Red_X.png) |
|1703  |![Unterstützt](media/green_check.png)            |![Unterstützt](media/green_check.png) | ![Abwärtskompatibel](media/blue_compat.png)|
|1709  |![Nicht unterstützt](media/Red_X.png)              |![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png)|

|Schlüssel|
|--|
|![Unterstützt](media/green_check.png) = **Unterstützt**: Windows empfiehlt das Verwenden des Windows ADK, das der Windows-Version entspricht, die Sie bereitstellen. Verwenden Sie z. B. das Windows ADK für Windows 10, Version 1703, bei Bereitstellung der Windows 10-Version 1703. Weitere Informationen zur Unterstützung für die Windows ADK-Komponente finden Sie unter [Unterstützte DISM-Plattformen](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) und [USMT-Anforderungen](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
|![Abwärtskompatibel](media/blue_compat.png)  = **Abwärtskompatibel**: Diese Kombination wurde nicht getestet, sollte jedoch funktionieren. Wir werden alle bekannten Probleme und Einschränkungen dokumentieren. |
|![Unterstützt](media/Red_X.png) = **Nicht unterstützt**|
