---
title: "Voraussetzungen für Asset Intelligence | Microsoft-Dokumentation"
description: "Hier erhalten Sie Informationen über die Voraussetzungen für Asset Intelligence in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
caps.latest.revision: 10
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 156d6679817b81ca27fbd2b8836431396e1e6b23


---
# <a name="prerequisites-for-asset-intelligence-in-system-center-configuration-manager"></a>Voraussetzungen für Asset Intelligence in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Asset Intelligence in System Center Configuration Manager weist externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts auf.  

## <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  
 Die folgende Tabelle enthält die Configuration Manager-externen Abhängigkeiten für Asset Intelligence.  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Überwachung der Voraussetzungen für erfolgreiche Anmeldeereignisse|In vier Asset Intelligence-Berichten werden Informationen angezeigt, die aus den Windows-Sicherheitsereignisprotokollen auf den Clientcomputern zusammengestellt werden. Wenn die Einstellungen des Sicherheitsereignisprotokolls nicht so konfiguriert sind, dass alle erfolgreichen Anmeldeereignisse protokolliert werden, enthalten diese Berichte selbst dann keine Daten, wenn die entsprechende Hardwareinventur-Berichterstattungsklasse aktiviert ist.<br /><br /> Die folgenden Asset Intelligence-Berichte hängen von gesammelten Informationen in den Windows-Sicherheitsereignisprotokollen ab:<br /><br /> - Hardware 03A – Primäre Computerbenutzer<br />- Hardware 03B – Computer für einen bestimmten primären Konsolenbenutzer<br />- Hardware 04A – Freigegebene (Mehrbenutzer-)Computer<br />- Hardware 05A – Konsolenbenutzer auf einem bestimmten Computer<br /><br /> Damit der Hardwareinventurclient-Agent die zur Unterstützung dieser Berichte erforderlichen Informationen inventarisieren kann, müssen Sie zunächst die Einstellungen für das Windows-Sicherheitsereignisprotokoll auf Clients so ändern, dass alle erfolgreichen Anmeldeereignisse protokolliert werden, und Sie müssen die Hardwareinventur-Berichterstattungsklasse **SMS_SystemConsoleUser** aktivieren. Weitere Informationen zum Ändern der Einstellungen des Sicherheitsereignisprotokolls zum Protokollieren aller erfolgreichen Anmeldeereignisse finden Sie unter [Enable Auditing of Success Logon Events (Aktivieren der Überwachung von erfolgreichen Anmeldeereignissen)](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents).|  

> [!NOTE]  
>  In der Hardwareinventur-Berichterstattungsklasse **SMS_SystemConsoleUser** werden, unabhängig von der Länge des Protokolls, erfolgreiche Anmeldedaten lediglich für die vorhergehenden 90 Tage des Sicherheitsereignisprotokolls aufbewahrt. Wenn das Sicherheitsereignisprotokoll Daten für weniger als 90 Tage enthält, wird das gesamte Protokoll gelesen.  

## <a name="dependencies-internal-to-configuration-manager"></a>Interne Abhängigkeiten von Configuration Manager  
 Die folgende Tabelle enthält die Configuration Manager-internen Abhängigkeiten für Asset Intelligence.  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Client-Agent-Voraussetzungen|Die Asset Intelligence-Berichte hängen von den Clientinformationen ab, die bei den Hardware- und Softwareinventurberichten auf dem Client abgerufen werden. Wenn Sie die notwendigen Informationen für alle Asset Intelligence-Berichte abrufen möchten, müssen die folgenden Client-Agents aktiviert werden:<br /><br /> - Hardwareinventurclient-Agent<br />- Softwaremessungsclient-Agent|  
|Abhängigkeiten des Hardwareinventurclient-Agents|Wenn Sie die Inventurdaten sammeln möchten, die für einige Asset Intelligence-Berichte benötigt werden, muss der Hardwareinventurclient-Agent aktiviert werden. Außerdem müssen auf den primären Standortservercomputern einige Hardwareinventur-Berichtsklassen aktiviert werden, zu denen die Asset Intelligence-Berichte Abhängigkeiten aufweisen.<br /><br /> Informationen zum Aktivieren des Hardwareinventurclient-Agents finden Sie unter [How to extend hardware inventory in System Center Configuration Manager (Erweitern der Hardwareinventur in System Center Configuration Manager)](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).|  
|Abhängigkeiten des Softwaremessungsclient-Agents|Eine Reihe von Asset Intelligence-Softwareberichten erhält ihre Daten vom Softwaremessungsclient-Agent. Informationen zum Aktivieren des Softwaremessungsclient-Agents finden Sie unter [Überwachen der App-Nutzung mittels Softwaremessung in System Center Configuration Manager](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).<br /><br /> Die folgenden Asset Intelligence-Berichte erhalten ihre Daten vom Softwaremessungsclient-Agent:<br /><br /> - Software 07A – Zuletzt verwendete ausführbare Dateien, geordnet nach Anzahl der Computer<br />- Software 07B – Computer, auf denen eine angegebene ausführbare Datei zuletzt verwendet wurde<br />- Software 07C – Zuletzt verwendete ausführbare Dateien auf einem bestimmten Computer<br />- Software 08A – Zuletzt verwendete ausführbare Dateien, geordnet nach Anzahl der Computer<br />- Software 08B – Benutzer, die eine angegebene ausführbare Datei zuletzt verwendet haben<br />- Software 08C – Zuletzt verwendete ausführbare Dateien, geordnet nach angegebenem Benutzer|  
|Voraussetzungen für Asset Intelligence-Hardwareinventur-Berichtsklassen|Asset Intelligence-Berichte in Configuration Manager hängen von bestimmten Hardwareinventur-Berichtsklassen ab. Solange die Hardwareinventur-Berichtsklassen noch nicht aktiviert sind und von Clients keine Hardwareinventuren basierend auf diesen Klassen gemeldet wurden, enthalten die verknüpften Asset Intelligence-Berichte keine Daten. Sie können die folgenden Hardwareinventur-Berichtsklassen aktivieren, um Asset Intelligence-Berichterstattungsanforderungen zu unterstützen:<br /><br /> - SMS_SystemConsoleUsage<sup>1</sup><br />- SMS_SystemConsoleUser<sup>1</sup><br />- SMS_InstalledSoftware<br />- SMS_AutoStartSoftware<br />- SMS_BrowserHelperObject<br />- Win32_USBDevice<br />- SMS_InstalledExecutable<br />- SMS_SoftwareShortcut<br />- SoftwareLicensingService<br />- SoftwareLicensingProduct<br />- SMS_SoftwareTag<br /><br /> <sup>1</sup> Die Asset Intelligence-Hardwareinventur-Berichtsklassen **SMS_SystemConsoleUsage** und **SMS_SystemConsoleUser** sind standardmäßig aktiviert.<br /><br /> Sie können die Asset Intelligence-Hardwareinventur-Berichtsklassen in der Configuration Manager-Konsole bearbeiten, indem Sie im Arbeitsbereich **Bestand und Kompatibilität** auf den Knoten **Asset Intelligence** klicken. Weitere Informationen finden Sie im Abschnitt [Enable Asset Intelligence hardware inventory reporting classes (Aktivieren von Asset Intelligence-Hardwareinventur-Berichtsklassen)](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) im Thema [Configuring Asset Intelligence in System Center Configuration Manager (Konfigurieren von Asset Intelligence in System Center Configuration Manager)](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).|  
|Reporting Services-Punkt|Die Standortsystemrolle des Reporting Services-Punkts muss installiert werden, damit Berichte zu Softwareupdates angezeigt werden können. Weitere Informationen über die Erstellung eines Reporting Services-Punkts finden Sie unter [Configuring Reporting in Configuration Manager (Konfigurieren der Berichterstattung in Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkId=232661).|  



<!--HONumber=Dec16_HO3-->


