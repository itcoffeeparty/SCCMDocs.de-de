---
title: Unterstützung für Windows 10
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu Windows 10-Versionen, die bei Verwendung von System Center Configuration Manager als Clients oder für Betriebssystembereitstellungen unterstützt werden.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 877732c4095438b19a863335a4a0026b7b088b24
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="support-for-windows-10-in-system-center-configuration-manager"></a>Unterstützung von Windows 10 in System Center Configuration Manager  

*Gilt für: System Center Configuration Manager (Current Branch)*


In diesem Artikel erhalten Sie Informationen zu Windows 10-Versionen, die von Configuration Manager unterstützt werden. Hierzu zählen:
 -  Windows 10 als Configuration Manager-Client
 -  Windows-Assessment and Deployment Kit (ADK) für Windows 10

## <a name="windows-10-as-a-client"></a>Windows 10 als Client
Configuration Manager versucht, neue Windows 10-Versionen nach der Veröffentlichung möglichst schnell als Client zu unterstützen. Da die Produkte über getrennte Zeitpläne für Entwicklung und Freigabe verfügen, hängt die Unterstützung von Configuration Manager davon ab, wann sie jeweils verfügbar sind.

Beispielsweise wird eine Version von Configuration Manager, deren [Support für diese Version](/sccm/core/servers/manage/current-branch-versions-supported) eingestellt wurde, aus der Kompatibilitätsmatrix gelöscht. Ebenso wird der Support für Windows 10-Versionen wie Enterprise 2015 LTSB oder 1511 aus der Kompatibilitätsmatrix entfernt, sobald diese nicht mehr unterstützt werden. Weitere Informationen finden Sie unter [Veraltete Betriebssysteme](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).


-   Die folgenden Informationen ergänzen die [unterstützten Betriebssysteme für Clients und Geräte](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Wenn Sie Long-Term Servicing Branch von Configuration Manager verwenden, finden Sie weitere Informationen unter [Unterstützte Konfigurationen für LTSB (Long-Term Servicing Branch) von System Center Configuration Manager](/sccm/core/understand/supported-configurations-for-ltsb).

| Windows 10-Version | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 |
|---------------------|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
| Enterprise 2016 LTSB            <!--10/13/2026-->   | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
| 1607   <br />(*siehe Editionen*)   <!--04/10/2018-->   | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
| 1703   <br />(*siehe Editionen*)   <!--10/09/2018-->   | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |
| 1709   <br />(*siehe Editionen*)   <!--04/09/2019-->   | ![Abwärtskompatibel](media/blue_compat.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**Editionen:** Enterprise, Pro, Education, Pro Education   

|Schlüssel|
|--|
|![Unterstützt](media/green_check.png) = **Unterstützt**  |
|![Abwärtskompatibel](media/blue_compat.png)  = **Backwards compatible:** Vorhandene Clientverwaltungsfeatures sollten mit der neuen Version von Windows 10 verwendet werden können. Dazu zählen beispielsweise Hardware- und Softwareinventur sowie Softwareupdates. Wir werden alle bekannten Probleme und Einschränkungen dokumentieren. <br><br>Dieser Ansatz bietet Ihnen die Möglichkeit zur Bereitstellung und Verwaltung der neuen Windows-Versionen mit sofortiger Unterstützung der Anwendungskompatibilität, ohne dass eine neue Updateversion von Configuration Manager erforderlich ist. |
|![Nicht unterstützt](media/Red_X.png) = **Not supported**|

 > [!NOTE]
 > Ab Version 1802 unterstützt Configuration Manager den Client auf ARM64-Geräten mit Windows 10. Vorhandene Clientverwaltungsfeatures sollten jetzt mit diesen neuen Geräten funktionieren. Beispiele: Hardware- und Softwareinventur, Softwareupdates und Anwendungsverwaltung. Die Betriebssystembereitstellung wird zurzeit nicht unterstützt. <!-- 1353704 --> 



## <a name="windows-10-adk"></a>Windows 10 ADK
Beim Bereitstellen von Betriebssystemen mit Configuration Manager ist das [Windows ADK eine externe Abhängigkeit](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment), die erforderlich ist.

Die folgende Tabelle listet die Versionen des Windows 10 ADK auf, die Sie mit verschiedenen Versionen von Configuration Manager verwenden können.

| Windows 10 ADK-Version  | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802   |
|--------------------|-----|-----|-----|
| 1607  | ![Nicht unterstützt](media/Red_X.png)   | ![Nicht unterstützt](media/Red_X.png) | ![Nicht unterstützt](media/Red_X.png) |
| 1703  | ![Unterstützt](media/green_check.png) | ![Abwärtskompatibel](media/blue_compat.png) | ![Abwärtskompatibel](media/blue_compat.png) |
| 1709  | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) |

|Schlüssel|
|--|
|![Unterstützt](media/green_check.png) = **Unterstützt**: Windows empfiehlt das Verwenden des Windows ADK, das der Windows-Version entspricht, die Sie bereitstellen. Verwenden Sie z. B. das Windows ADK für Windows 10, Version 1703, bei Bereitstellung der Windows 10-Version 1703. Weitere Informationen zur Unterstützung für die Windows ADK-Komponente finden Sie unter [Unterstützte DISM-Plattformen](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) und [USMT-Anforderungen](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
|![Abwärtskompatibel](media/blue_compat.png)  = **Abwärtskompatibel**: Diese Kombination wurde nicht getestet, sollte jedoch funktionieren. Wir werden alle bekannten Probleme und Einschränkungen dokumentieren. |
|![Nicht unterstützt](media/Red_X.png) = **Not supported**|

 > [!Note]
 > Configuration Manager unterstützt nur x86- und AMD64-Komponenten des Windows 10 ADK. ARM- oder ARM64-Komponenten werden derzeit nicht unterstützt. 