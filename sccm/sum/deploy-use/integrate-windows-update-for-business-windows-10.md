---

title: "Integration mit Windows Update für Unternehmen in Windows 10 | Microsoft-Dokumentation"
description: "Verwenden Sie Windows Update for Business, um Windows 10-basierte Geräte in Ihrer Organisation, die mit Windows Update verbunden sind, auf dem neuesten Stand zu halten."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
translationtype: Human Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 8bdbacd54632475ac69a0d0a9a34b2567c3daa13


---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Integration mit Windows Update für Unternehmen in Windows 10

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit Windows Update for Business (WUfB) können Sie Windows 10-basierte Geräte in Ihrem Unternehmen hinsichtlich der neuesten Schutzmaßnahmen und Windows-Features auf dem neuesten Stand halten, wenn diese Geräte eine direkte Verbindung mit dem Windows Update-Dienst herstellen. Configuration Manager kann zwischen Windows 10-Computern unterscheiden, die WUfB und WSUS zum Abrufen von Softwareupdates verwenden.  

 Einige Configuration Manager-Features sind nicht mehr verfügbar, wenn Configuration Manager-Clients so konfiguriert sind, dass sie Updates von Windows Update empfangen, was Windows Update for Business (WUfB) oder Windows Insider einbezieht:  

-   Windows Update-Berichterstellung zur Kompatibilität:  

    -   Configuration Manager wird nicht über die Updates informiert, die auf Windows Update veröffentlicht werden. Die Configuration Manager-Clients, die für den Empfang von Updates von WU konfiguriert sind, zeigen für diese Updates in der Configuration Manager-Konsole **Unbekannt** an.  

    -   Die Problembehandlung für den allgemeinen Kompatibilitätsstatus ist schwierig, da der Status **Unbekannt** nur für die Clients verwendet wird, die den Überprüfungsstatus nicht an WSUS zurückgemeldet haben.  Jetzt werden auch Configuration Manager-Clients einbezogen, die Updates von Windows Update erhalten.  

    -   Der bedingte Zugriff (auf Unternehmensressourcen) auf Basis des Status zur Kompatibilität funktioniert nicht erwartungsgemäß für Clients, die Updates von Windows Update empfangen, da sie nie die Kompatibilität von Configuration Manager erfüllen.  

    -   Die Kompatibilität der Definitionsupdates ist Teil der gesamten Berichterstellung zur Updatekompatibilität und funktioniert auch nicht wie erwartet.  Die Kompatibilität der Definitionsupdates zählt auch zur bedingten Zugriffsauswertung  

-   Die auf dem Status der Updatekompatibilität basierte allgemeine Endpoint Protection-Berichterstellung für Defender gibt aufgrund der fehlenden Überprüfungsdaten keine exakten Ergebnisse.  

-   Configuration Manager kann keine Microsoft-Updates wie Office, Internet Explorer und Visual Studio für Clients bereitstellen, die für den Empfang von Updates mit WUfB verbunden sind.  

-   Configuration Manager kann keine auf WSUS veröffentlichten und über Configuration Manager verwalteten Updates von Drittanbietern für Clients bereitstellen, die für den Empfang von Updates mit WUfB verbunden sind.  

-   Die vollständige Clientbereitstellung von Configuration Manager, die die Softwareupdateinfrastruktur verwendet, funktioniert nicht für Clients, die für den Empfang von Updates mit WUfB verbunden sind.  

## <a name="identify-clients-that-use--wufb-for-windows-10-updates"></a>Identifizieren von Clients, die WUfB für Windows 10-Updates verwenden  
 Verwenden Sie das folgende Verfahren, um Clients zu identifizieren, die WUfB zum Abrufen von Windows 10-Updates und -Upgrades verwenden. Konfigurieren Sie diese Clients derart, dass sie zum Abrufen von Updates kein WSUS verwenden, und stellen Sie eine Einstellung für den Client-Agent bereit, um den Workflow der Softwareupdates für diese Clients zu deaktivieren.  

 **Voraussetzungen**  

-   Clients, die Windows 10 Desktop Pro oder Windows 10 Enterprise Edition Version 1511 oder höher ausführen  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) wird bereitgestellt und die Clients verwenden WUfB zum Abrufen von Windows 10-Updates und -Upgrades.  

#### <a name="to-identify-clients-that-use-wufb"></a>So identifizieren Sie Clients, die WUfB verwenden  

1.  Deaktivieren Sie den Windows Update-Agent, damit er nicht auf WSUS sucht, wenn er zuvor aktiviert war.   
    Der Registrierungsschlüssel **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer** kann so festgelegt werden, dass er anzeigt, ob der Computer auf WSUS oder Windows Update sucht.  Wenn der Wert „2“ ist, sucht er nicht auf WSUS.  

2.  Es gibt ein neues Attribut, **UseWUServer**, unter dem Knoten **Windows Update** im Ressourcen-Explorer von Configuration Manager.  

3.  Erstellen Sie eine Sammlung auf Basis des **UseWUServer** -Attributs für alle Computer, die für Updates und Upgrades über WUfB verbunden sind.  

4.  Erstellen Sie eine Client-Agent-Einstellung, um den Softwareupdate-Workflow zu deaktivieren, und stellen Sie die Einstellung in der Sammlung von Computern bereit, die direkt mit WUfB verbunden sind.  

5.  Die Computer, die über WUfB verwaltet werden, zeigen als Kompatibilitätsstatus **Unbekannt** an und werden im Gesamtprozentsatz der Kompatibilität nicht berücksichtigt.  



<!--HONumber=Dec16_HO3-->


