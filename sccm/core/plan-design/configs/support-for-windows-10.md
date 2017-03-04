---
title: "Unterstützung für Windows 10 | Microsoft-Dokumentation"
description: "Erfahren Sie, welche Windows 10-Versionen unterstützt werden, um den System Center Configuration Manager-Client auszuführen."
ms.custom: na
ms.date: 2/10/2017
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
ms.sourcegitcommit: 3702993d6cf9644d5aebaadd168749668fbcb62c
ms.openlocfilehash: 4b90384621dd20475ab9ea33ea062c24f5ecf5fa
ms.lasthandoff: 02/22/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>Unterstützung für Windows 10 als ein Client von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 In diesem Thema werden die Versionen von Windows 10 identifiziert, die Sie als Client für die verschiedenen Versionen von Current Branch in System Center Configuration Manager verwenden können.

- Diese ergänzen [Unterstützte Betriebssysteme für Clients und Geräte](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
- Wenn Sie Long-Term Servicing Branch von Configuration Manager verwenden, finden Sie weitere Informationen unter [Unterstützte Konfigurationen für LTSB (Long-Term Servicing Branch) von System Center Configuration Manager](/sccm/core/understand/supported-configurations-for-ltsb).

Configuration Manager versucht jede neue Version von Windows 10 so bald wie möglich zu unterstützen, nachdem die Version freigegeben wurde. Da die Produkte über getrennte Zeitpläne für Entwicklung und Freigabe verfügen, hängt die Unterstützung von Configuration Manager davon ab, wann die Versionen und Verzweigungen jedes Produkts freigegeben werden.  



|Windows 10-Versionen |Configuration Manager 1602|Configuration Manager 1606|Configuration Manager 1610|
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|1507 <br />Enterprise, Pro | ![Unterstützt](media/green_check.png)| ![Unterstützt](media/green_check.png)|![Unterstützt](media/green_check.png) |
|1511 <br />Enterprise, Pro <br />(CB), (CBB) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |![Unterstützt](media/green_check.png) |
|Enterprise 2016 LTSB    |![Nicht unterstützt](media/Red_X.png) |![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png)|
|1607 <br />Enterprise, Pro<br /> (CB)    |![Nicht unterstützt](media/Red_X.png) |![Abwärtskompatibel](media/blue_compat.png) |![Unterstützt](media/green_check.png) |
|1607 <br />Enterprise, Pro <br />(CBB)    |![Nicht unterstützt](media/Red_X.png) |![Abwärtskompatibel](media/Red_X.png) |![Unterstützt](media/green_check.png) |


|Schlüssel|
|--|
|![Unterstützt](media/green_check.png) = **Unterstützt**  |
|![Nicht unterstützt](media/blue_compat.png)  = **Abwärtskompatibel**: Dies bedeutet, dass vorhandene Clientverwaltungsfunktionen (Hardwareinventur, Softwareinventur, Softwareupdates usw.) mit dem neuen Build von Windows 10 Current Branch arbeiten sollten. Bekannte Probleme oder Vorbehalte werden dokumentiert werden. <br><br>Dieser Ansatz bietet Ihnen die Möglichkeit zur Bereitstellung und Verwaltung der neuen Windows 10 CB Builds am ersten Tag mit Unterstützung der Anwendungskompatibilität, ohne dass eine neue Updateversion von Configuration Manager erforderlich ist. |
|![Unterstützt](media/Red_X.png) = **Nicht unterstützt**|
