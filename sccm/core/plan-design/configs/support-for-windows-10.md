---
title: "Unterstützung für Windows 10 | Microsoft-Dokumentation"
description: "Erfahren Sie, welche Windows 10-Versionen unterstützt werden, um den System Center Configuration Manager-Client auszuführen."
ms.custom: na
ms.date: 3/28/2017
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
translationtype: Human Translation
ms.sourcegitcommit: 2cdd25343cf68a79067a317b820572491a3633a2
ms.openlocfilehash: 84d6fdcec2c539f0fd3043f01d18e165da8c52c9
ms.lasthandoff: 04/12/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>Unterstützung für Windows 10 als ein Client von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 In diesem Thema werden die Versionen von Windows 10 identifiziert, die Sie als Client für die verschiedenen Versionen von Current Branch in System Center Configuration Manager verwenden können.

- Diese ergänzen [Unterstützte Betriebssysteme für Clients und Geräte](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
- Wenn Sie Long-Term Servicing Branch von Configuration Manager verwenden, finden Sie weitere Informationen unter [Unterstützte Konfigurationen für LTSB (Long-Term Servicing Branch) von System Center Configuration Manager](/sccm/core/understand/supported-configurations-for-ltsb).

Configuration Manager versucht jede neue Version von Windows 10 so bald wie möglich zu unterstützen, nachdem die Version freigegeben wurde. Da die Produkte über getrennte Zeitpläne für Entwicklung und Freigabe verfügen, hängt die Unterstützung von Configuration Manager davon ab, wann die Versionen und Verzweigungen jedes Produkts freigegeben werden.

Eine Version von Configuration Manager, deren [Support für diese Version](/sccm/core/servers/manage/current-branch-versions-supported) eingestellt wurde, wird aus der Kompatibilitätsmatrix. Ebenso wird der Support für Windows 10 Versionen wie Enterprise 2015 LTSB oder 1607 (CBB) aus der Kompatibilitätsmatrix entfernt, wenn sie von der Liste der unterstützten Konfigurationen von Configuration Manager entfernt werden. Weitere Informationen finden Sie unter [Veraltete Betriebssysteme](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems).



|Windows 10-Versionen                    |Configuration Manager 1606          |Configuration Manager 1610          |    Configuration Manager 1702 |
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB                   |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|1507 <br />(*siehe Editionen*)            |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|1511 (CB), (CBB)<br />(*siehe Editionen*) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|Enterprise 2016 LTSB                   |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|1607 (CB)    <br />Anniversary Update<br />(*siehe Editionen*)      |![Abwärtskompatibel](media/blue_compat.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|1607 (CBB)    <br />Anniversary Update<br />(*siehe Editionen*)      |![Nicht unterstützt](media/Red_X.png)   |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|1703 (CBB)    <br />Creators Update<br />(*siehe Editionen*)      |![Nicht unterstützt](media/Red_X.png)   |![Nicht unterstützt](media/Red_X.png) |![Abwärtskompatibel](media/blue_compat.png) |



**Editionen:** Enterprise, Pro, Education, Pro Education   

|Schlüssel|
|--|
|![Unterstützt](media/green_check.png) = **Unterstützt**  |
|![Nicht unterstützt](media/blue_compat.png)  = **Abwärtskompatibel**: Dies bedeutet, dass vorhandene Clientverwaltungsfunktionen (Hardwareinventur, Softwareinventur, Softwareupdates usw.) mit dem neuen Build von Windows 10 Current Branch arbeiten sollten. Bekannte Probleme oder Vorbehalte werden dokumentiert werden. <br><br>Dieser Ansatz bietet Ihnen die Möglichkeit zur Bereitstellung und Verwaltung der neuen Windows 10 CB Builds am ersten Tag mit Unterstützung der Anwendungskompatibilität, ohne dass eine neue Updateversion von Configuration Manager erforderlich ist. |
|![Unterstützt](media/Red_X.png) = **Nicht unterstützt**|

