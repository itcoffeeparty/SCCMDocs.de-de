---
title: "System Center Configuration Manager-Datenschutzbestimmungen – Configuration Manager-Cmdlet-Bibliothek"
description: "Erfahren Sie mehr darüber, wie Microsoft Daten zur System Center Configuration Manager-Cmdlet-Bibliothek sammelt und verwendet."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 88d11aaed4a0e6575cb859f5dfc3ac425bd2bf38


---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>System Center Configuration Manager-Datenschutzbestimmungen – Configuration Manager-Cmdlet-Bibliothek

*Gilt für: System Center Configuration Manager (Current Branch)*

Diese Datenschutzbestimmungen gelten für die Features der System Center Configuration Manager-Cmdlet-Bibliothek.  

## <a name="usage-data"></a>Nutzungsdaten  
 **Funktion dieses Features:**   
Mit der System Center Configuration Manager-Cmdlet-Bibliothek können Sie eine Configuration Manager-Hierarchie mithilfe von Windows PowerShell-Cmdlets und -Skripts verwalten. Die Cmdlet-Bibliothek sammelt Informationen darüber, wie Sie die in der Bibliothek enthaltenen Cmdlets verwenden, um Trends und Verwendungsmuster zu ermitteln.  Die Cmdlet-Bibliothek erfasst auch die Art und die Anzahl der Fehler, die beim Verwenden der Cmdlets auftreten.  

 **Erfasste, verarbeitete oder übertragene Informationen:**   
Zu den gesammelten Nutzungsdaten gehören das Starten, Anhalten und Beenden von Cmdlets und das Ausführen von veralteten Cmdlets und Aktivitätsmetriken für Vorgänge im Zusammenhang mit Cmdlets, die mit SMS-Anbietern verknüpft sind. Diese Informationen sind nicht personenbezogen.  Zu den gesammelten Informationen gehören u. a. die von Cmdlets zurückgegebenen Fehler sowie Details zu Ausnahmefehlern. Einige Detailberichte zu Fehlern enthalten möglicherweise unbeabsichtigt personenbezogene Daten, z. B. Seriennummern von Geräten, die mit dem Computer verbunden sind. Die Cmdlet-Bibliothek filtert und anonymisiert diese Informationen in den Fehlerberichten, um etwaige persönliche Informationen vor der Übertragung an Microsoft zu entfernen.  

 **Verwendung der Informationen:**   
Wir verwenden diese Informationen zur Verbesserung der Qualität, der Sicherheit und der Integrität der von uns angebotenen Produkte und Dienste.  

 **Auswahl/Kontrolle:**   
Das Feature zur Erfassung von Nutzungsdaten ist standardmäßig aktiviert. Die System Center Configuration Manager-Cmdlet-Bibliothek umfasst zwei Registrierungsschlüssel zur Steuerung dieser Funktionalität.  

 Zur vollständigen Deaktivierung müssen Sie die Werte dieser beiden Registrierungsschlüssel festlegen – jeweils einen für jeden der Anbieter zur Ereignisnachverfolgung für Windows (Event Tracing for Windows, ETW):  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (beendet die Erfassung von Nutzungsdaten für den Laufwerksanbieter)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (beendet die Erfassung von Nutzungsdaten für die Cmdlets)  

 Die Einstellungen für Nutzungsdaten gelten nur für den betreffenden Computer, auf dem sie festgelegt wurden.  

 Weitere Informationen zum Konfigurieren von Nutzungsdaten (Sammlung) finden Sie in der [Dokumentation für die System Center Configuration Manager-Cmdlets-Bibliothek](https://technet.microsoft.com/en-us/library/dn958404.aspx).  

## <a name="update-check"></a>Überprüfung auf Updates  
 **Funktion dieses Features:**   
Die System Center Configuration Manager-Cmdlet-Bibliothek überprüft automatisch täglich, ob Updates für die Bibliothek vorliegen, und fordert Sie ggf. auf, die aktualisierte Bibliothek herunterzuladen.  

 **Erfasste, verarbeitete oder übertragene Informationen:**   
Bei der Überprüfung auf Updates für die Cmdlet-Bibliothek wird eine kleine Textdatei aus dem Microsoft Download Center heruntergeladen, um eine Versionsprüfung vorzunehmen.   Diese Datei wird nicht lokal gespeichert.  Die Cmdlet-Bibliothek führt kein automatisches Upgrade der Software durch.  

 **Verwendung der Informationen:**   
Wir verwenden diese Informationen zur Verbesserung der Qualität, der Sicherheit und der Integrität der von uns angebotenen Produkte und Dienste.  

 **Auswahl/Kontrolle:**   
Die Überprüfung auf Updates ist standardmäßig aktiviert.  Die System Center Configuration Manager-Cmdlet-Bibliothek umfasst die folgenden Cmdlets zur Steuerung der Updatebenachrichtigungsfunktion:  

-   `Get-CMCmdletUpdateCheck` ruft die Konfiguration des Update-Features auf und gibt an, ob Benutzerrichtlinien durch Systemrichtlinien außer Kraft gesetzt werden.  

-   `Send-CMCmdletUpdateCheck` ermöglicht Ihnen die Durchführung einer nicht geplanten Überprüfung auf Updates. Bei einer außerplanmäßigen Überprüfung werden die Richtlinieneinstellungen nicht berücksichtigt.  

-   `Set-CMCmdletUpdateCheck` konfiguriert die Einstellungen für die Überprüfung auf Updates auf Benutzer- oder Systembasis. Für das Festlegen von Systemeinstellungen müssen Sie das Cmdlet als Administrator ausführen.  

 Weitere Informationen zum Konfigurieren der Überprüfung auf Updates finden Sie in der [Dokumentation zur System Center Configuration Manager-Cmdlet-Bibliothek](https://technet.microsoft.com/en-us/library/dn958404.aspx).  



<!--HONumber=Nov16_HO1-->


