---
title: Sprachpakete | Microsoft-Dokumentation
description: "Erfahren Sie mehr über die Sprachunterstützung, die Ihnen in System Center Configuration Manager zur Verfügung steht."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 35d1008752a3275febef46b8817e97afdb91d580


---
# <a name="language-packs-in-system-center-configuration-manager"></a>Sprachpakete in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält technische Details zur Sprachunterstützung in System Center Configuration Manager.  

##  <a name="a-namebkmksuplanguagepacksa-supported-operating-system-languages"></a><a name="BKMK_SupLanguagePacks"></a> Unterstützte Betriebssystemsprachen  
 Sie können Unterstützung für die folgenden Anzeigesprachen installieren, indem Sie **Serversprachpakete** oder **Clientsprachpakete** an einem Standort der zentralen Verwaltung und an primären Standorten installieren. Sprachpaketdateien werden beim Ausführen von Setup im Rahmen des Downloads der erforderlichen Komponenten und Redistributable-Datei heruntergeladen. Sie können auch das [Setup-Downloadprogramm](setup-downloader.md) verwenden, um diese Dateien herunterzuladen, bevor Sie Setup ausführen. Während der Installation eines Standorts wählen Sie an diesem Standort zu unterstützenden Server- und Clientsprachen aus den verfügbaren verfügbaren Sprachpaketdateien aus.  

 Verwenden Sie die folgende Tabelle, um eine Gebietsschema-ID einer Sprache zuzuordnen, die auf Servern oder Clients unterstützt werden soll. Weitere Informationen zu Gebietsschema-IDs finden Sie unter [Von Microsoft zugewiesene Gebietsschema-IDs](http://go.microsoft.com/fwlink/p/?LinkId=252609) in der MSDN-Onlinebibliothek.  

### <a name="server-languages"></a>Serversprachen  

|Serversprache|Gebietsschema-ID (LCID)|Code mit drei Buchstaben|  
|---------------------|------------------------|-----------------------|  
|Englisch (Standard)|0409|ENU|  
|Chinesisch (traditionell, Hongkong SAR)|0c04|ZHH|  
|Chinesisch (vereinfacht)|0804|CHS|  
|Chinesisch (traditionell, Taiwan)|0404|CHT|  
|Tschechisch|0405|CSY|  
|Niederländisch – Niederlande|0413|NLD|  
|Französisch|040c|FRA|  
|Deutsch|0407|DEU|  
|Ungarisch|040e|HUN|  
|Italienisch – Italien|0410|ITA|  
|Japanisch|0411|JPN|  
|Koreanisch|0412|KOR|  
|Polnisch|0415|PLK|  
|Portugiesisch – Brasilien|0416|PTB|  
|Portugiesisch – Portugal|0816|PTG|  
|Russisch|0419|RUS|  
|Spanisch – Spanien|0c0a|ESN|  
|Schwedisch|041d|SVE|  
|Türkisch|041f|TRK|  

### <a name="client-languages"></a>Clientsprachen  

|Clientsprache|Gebietsschema-ID (LCID)|Code mit drei Buchstaben|  
|---------------------|------------------------|-----------------------|  
|Englisch (Standard)|0409|ENG|  
|Chinesisch (traditionell, Hongkong SAR)|0c04|ZHH|  
|Chinesisch (vereinfacht)|0804|CHS|  
|Chinesisch (traditionell, Taiwan)|0404|CHT|  
|Tschechisch|0405|CSY|  
|Dänisch|0406|DAN|  
|Niederländisch – Niederlande|0413|NLD|  
|Finnisch|040b|FIN|  
|Französisch|040c|FRA|  
|Deutsch|0407|DEU|  
|Griechisch|0408|ELL|  
|Ungarisch|040e|HUN|  
|Italienisch – Italien|0410|ITA|  
|Japanisch|0411|JPN|  
|Koreanisch|0412|KOR|  
|Norwegisch|0414|NOR|  
|Polnisch|0415|PLK|  
|Portugiesisch (Brasilien)|0416|PTB|  
|Portugiesisch (Portugal)|0816|PTG|  
|Russisch|0419|RUS|  
|Spanisch – Spanien|0c0a|ESN|  
|Schwedisch|041d|SVE|  
|Türkisch|041f|TRK|  

### <a name="mobile-device-client-languages"></a>Clientsprachen für mobile Geräte  
 Wenn Sie die Unterstützung für Sprachen mobiler Geräte hinzufügen, werden alle Clientsprachen für mobile Geräte einbezogen. Sie können keine einzelnen Sprachpakete für die Unterstützung mobiler Geräte auswählen.  

### <a name="how-to-identify-installed-language-packs"></a>Ermitteln installierter Sprachpakete  
Auf einem Computer, auf dem der Configuration Manager-Client ausgeführt wird, können Sie die installierten Language Packs ermitteln, indem Sie die Gebietsschema-ID (LCID) der installierten Language Packs in der Registrierung des Computers anzeigen. Diese Informationen sind unter folgendem Speicherort verfügbar:  

-   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs**  

Sie können diese Informationen mithilfe der Hardwareinventur sammeln und dann einen benutzerdefinierten Bericht erstellen, um die Sprachdetails anzuzeigen. Informationen zum Sammeln einer benutzerdefinierten Hardwareinventur finden Sie unter [Konfigurieren der Hardwareinventur in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md). Informationen zum Erstellen von Berichten finden Sie im Abschnitt [ (Verwalten von Configuration Manager-Berichten)](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md#BKMK_ManageReports) des Themas [Operations and maintenance for reporting in System Center Configuration Manager (Vorgänge und Wartungstasks für die Berichterstattung in Configuration Manager)](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md).  



<!--HONumber=Dec16_HO3-->


