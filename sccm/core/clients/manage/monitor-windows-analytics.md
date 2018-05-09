---
title: Überwachen von Clients mit Windows Analytics
titleSuffix: Configuration Manager
description: Windows Analytics umfasst Lösungen, die Teil der Operations Management Suite sind und Ihnen wertvolle Einblicke in den aktuellen Status Ihrer Umgebung geben. Dies geschieht durch die Nutzung von Windows-Telemetriedaten, die von Geräten in Ihrer Umgebung gesendet werden.
ms.date: 01/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e792f421520798a0e000384aafcb99f31dc8eb14
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Verwenden von Windows Analytics mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) umfasst Lösungen, die Teil der [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview) (OMS) sind. Mit diesen Lösungen erhalten Sie wertvolle Einblicke in den aktuellen Status Ihrer Umgebung. Geräte in Ihrer Umgebung melden Telemetriedaten, auf die mit Lösungen des [Operations Management Suite-Webportals](https://mms.microsoft.com) zugegriffen werden kann. Auch eine Analyse der Daten ist möglich. Durch das Verbinden der [Upgradebereitschaft](/sccm/core/clients/manage/upgrade/upgrade-analytics) mit Configuration Manager können Sie direkt auf die Daten im Knoten **Überwachung** der Configuration Manager-Konsole zugreifen.

Die von Windows Analytics analysierten Windows-Telemetriedaten werden nicht direkt an den Configuration Manager-Standortserver weitergeleitet. Stattdessen senden Clientcomputer Windows-Telemetriedaten an den Windows-Telemetriedienst. Dieser Dienst sendet dann die relevanten Daten an Windows Analytics-Lösungen, die in einem OMS-Arbeitsbereich Ihrer Organisation gehostet sind. Mit Configuration Manager können Sie entweder über kontextbezogene Links auf relevante Daten im Webportal zugreifen, oder sich direkt Daten der Lösungen anzeigen lassen, die Sie mit Configuration Manager verbunden haben. Über das Operation Management Suite-Webportal können Sie außerdem die Daten direkt abfragen.

>[!Important]
>[Diagnose- und Nutzungsdaten von Configuration Manager](../../plan-design/diagnostics/diagnostics-and-usage-data.md), die der Configuration Manager-Standortserver an Microsoft sendet, sind nicht Bestandteil der Datensammlung von Windows Analytics oder der Windows-Telemetriedaten.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Konfigurieren von Clients zum Senden von Daten an Windows Analytics

Damit Clientgeräte Daten an Windows Analytics senden, müssen Sie Geräte mit einem kommerziellen ID-Schlüssel konfigurieren, der dem OMS-Arbeitsbereich zugeordnet ist, der Ihre Windows Analytics-Daten hostet. Außerdem müssen Sie die Geräte so konfigurieren, dass sie Telemetriedaten auf einer Telemetriestufe senden, die für Ihre spezifischen Lösungen geeignet sind, die Sie verwenden. 

### <a name="configure-windows-analytics-client-settings"></a>Konfigurieren von Clienteinstellungen für Windows Analytics
Wählen Sie zum Konfigurieren von Windows Analytics in der Configuration Manager-Konsole **Verwaltung** > **Clienteinstellungen** aus, doppelklicken Sie auf **Benutzerdefinierte Clienteinstellungen für Geräte erstellen**, und aktivieren Sie dann **Windows Analytics**.  

Wechseln Sie zur Registerkarte mit den Einstellungen für **Windows Analytics**, und konfigurieren Sie folgende Einstellungen:
  -  **Kommerzieller ID-Schlüssel**  
Der Schlüssel „Kommerzielle ID“ ordnet Informationen der von Ihnen verwalteten Geräte zu dem OMS-Arbeitsbereich zu, der die Windows Analytics-Daten Ihrer Organisation hostet. Wenn Sie bereits einen kommerziellen ID-Schlüssel für die Verwendung mit der Upgradebereitschaft konfiguriert haben, verwenden Sie diese ID. Wenn Sie noch nicht über einen kommerziellen ID-Schlüssel verfügen, finden Sie weitere Informationen unter [Generieren des kommerziellen ID-Schlüssels]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Telemetriestufe für Windows 10-Geräte**   
Weitere Informationen zu jeder Telemetriestufe von Windows 10 finden Sie unter [Konfigurieren der Windows-Telemetrie in Ihrem Unternehmen](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

   > [!Note]
   > Ab dem Update 1710 können Sie die Stufe der Windows 10-Telemetriedatensammlung auf **Enhanced (Limited)** (Erweitert [Begrenzt]) festlegen. Mit dieser Einstellung können Sie wertvolle Einblicke zu Geräten in Ihrer Umgebung gewinnen, ohne dass alle Daten in der Telemetriestufe **Enhanced** an Windows 10-Version 1709 oder höher berichtet werden. Die Telemetriestufe „Enhanced (Limited)“ enthält grundlegende Metriken und eine Teilmenge von Daten, die auf der erweiterten Stufe in Windows Analytics gesammelt werden.


  -  **Abonnieren Sie die Sammlung kommerzieller Daten auf Geräten unter Windows 7, 8 und 8.1**   
Weitere Informationen finden Sie unter [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields (Appraiser-Telemetrieereignisse und -felder unter Windows 7, Windows 8, und Windows 8.1)](https://go.microsoft.com/fwlink/?LinkID=822965).

  -  **Konfigurieren der Datensammlung von Internet Explorer**  
Auf Geräten unter Windows 8.1 oder früher kann die Internet Explorer-Datensammlung es der Upgradebereitschaft ermöglichen, Inkompatibilitäten von Webanwendungen zu erkennen, die ein reibungsloses Upgrade auf Windows 10 verhindern könnten. Die Internet Explorer-Datensammlung kann für einzelne Internetzonen aktiviert werden. Weitere Informationen zu Internetzonen finden Sie unter [About URL Security Zones](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx) (Informationen zu URL-Sicherheitszonen).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Verwenden von Upgradebereitschaft zum Identifizieren von Windows 10-Kompatibilitätsproblemen

Mit Upgradebereitschaft (ehemals Upgrade Analytics) können Sie die Gerätebereitschaft und Kompatibilität unter Windows 10 analysieren. Durch diese Bewertung werden reibungslose Upgrades ermöglicht. Greifen Sie, nachdem Sie Upgradebereitschaft mit Configuration Manager verbunden haben, direkt auf Daten zur Konformität von Clientupgrades in der Configuration Manager-Konsole zu. Wählen Sie dann Geräte aus der Geräteliste für ein Upgrade oder Wartungsaufgaben aus.

Weitere Informationen und Details zum Konfigurieren und Verbinden mit Upgradebereitschaft finden Sie unter [Upgradebereitschaft](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Verwenden von Windows Analytics zur Identifizierung von Lücken in Windows Information Protection-Richtlinien

Geräte unter Windows 10 Version 1703 und höher, die mit den [Windows Information Protection-Richtlinien](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) konfiguriert sind, senden Telemetriedaten über Anwendungen, die zwar Zugriff auf Unternehmensdaten in Ihrer Umgebung haben, jedoch nicht in den Anwendungsregeln der WIP-Richtlinien berücksichtigt werden. WIP blockiert diese Anwendungen, die Benutzer möglicherweise benötigen, um produktiv zu bleiben. Das Wissen, dass Benutzer auf Unternehmensdaten zugreifen, ist bei der Wartung ihrer Windows Information Protection-Richtlinien in Configuration Manager nützlich. 

Greifen Sie über die [Operations Management Suite-Abfrage](https://go.microsoft.com/fwlink/?linkid=849952) auf die Windows Information Protection-Daten zu.