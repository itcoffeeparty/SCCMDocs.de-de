---
title: Grundlagen der Clientverwaltung | Microsoft-Dokumentation
description: "Erfahren Sie mehr über Tasks, die Sie für die Verwaltung von System Center Configuration Manager-Clients ausführen können."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 9648fc831e21f8a5ee6e12cfe7754933ba9f6239


---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Grundlagen der Clientverwaltungsaufgaben für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Nach der Installation von System Center Configuration Manager-Clients können Sie verschiedene Aufgaben zur Verwaltung der Clients ausführen.  Manche starten Sie von der Configuration Manager-Konsole aus, während andere von der Configuration Manager-App des Clients in der Windows-Systemsteuerung aus auf einem Client gestartet oder angezeigt werden können.  

## <a name="the-console"></a>Die Konsole  
 Aus der Configuration Manager-Konsole heraus können Sie verschiedene Clientverwaltungstasks ausführen. Dazu gehören unter anderem:  

-   Bereitstellen von Anwendungen, Softwareupdates, Wartungsskripts und Betriebssystemen. Diese können so konfiguriert werden, dass sie zu einem bestimmten Termin installiert werden oder dass sie den Benutzern zur Verfügung gestellt und auf Anforderung installiert werden. Anwendungen können zudem deinstalliert werden.  

-   Schutz der Computer vor Schadsoftware und Sicherheitsrisiken sowie Ausgeben einer Warnung, wenn Probleme erkannt werden  

-   Definieren von Clientkonfigurationseinstellungen, die Sie überwachen und bei fehlender Kompatibilität wiederherstellen möchten  

-   Sammeln von Hardware- und Softwareinventurinformationen, darunter die Überwachung und Abstimmung von Lizenzinformationen von Microsoft  

-   Problembehandlung auf Computern mit der Remotesteuerung.  

-   Implementieren von Energieverwaltungseinstellungen zum Verwalten und Überwachen des Stromverbrauchs von Computern  

Mithilfe von Warnungen und Statusinformationen können Sie diese Vorgänge über die Configuration Manager-Konsole nahezu in Echtzeit überwachen. Zum Erfassen von Daten und Auswerten historischer Trends können Sie die integrierten Berichterstattungsfunktionen von SQL Reporting Services verwenden.  Clients senden Informationen als Clientstatus an den Standort.  Clientstatusinformationen liefern Daten über die Integrität des Clients sowie die Clientaktivität und können in der Konsole oder mithilfe integrierter Berichte für Configuration Manager angezeigt werden. Mithilfe dieser Daten können Sie Computer identifizieren, die nicht reagieren, und in einigen Fällen Probleme automatisch beheben.  

 Weitere Informationen zu den Verwaltungsaufgaben für Clients finden Sie unter [Verwalten von Clients in System Center Configuration Manager](../../core/clients/manage/manage-clients.md) und [Verwalten von Clients für Linux- und UNIX-Server in System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Informationen zur Verwendung von Berichten finden Sie unter   
            [Einführung in die Berichterstellung in System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="the-windows-control-panel-app"></a>Die Windows-Systemsteuerung-App.  
 Wenn Sie die Configuration Manager-Clientsoftware installieren, wird die Clientanwendung **Configuration Manager** in der Systemsteuerung installiert. Im Gegensatz zum Softwarecenter ist diese Anwendung nicht für Endbenutzer bestimmt, sondern für den Helpdesk. Einige Konfigurationsoptionen erfordern lokale Administratorberechtigungen, und für die meisten Optionen sind technische Kenntnisse der Funktionsweise von Configuration Manager erforderlich. Sie können diese Anwendung verwenden, um auf einem Client die folgenden Aufgaben auszuführen:  

-   Anzeigen von Eigenschaften des Clients, z. B. Buildnummer, zugewiesener Standort, mit welchem Verwaltungspunkt der Client kommuniziert und ob ein PKI-Zertifikat oder ein selbstsigniertes Zertifikat verwendet wird  

-   Bestätigen, dass nach der Erstinstallation des Clients erfolgreich eine Clientrichtlinie heruntergeladen wurde und dass Clienteinstellungen erwartungsgemäß aktiviert oder deaktiviert sind, also gemäß den in der Configuration Manager-Konsole konfigurierten Clienteinstellungen.  

-   Starten von Clientaktionen, z.B. Herunterladen der Clientrichtlinie, wenn eine Änderung der Konfiguration in der Configuration Manager-Konsole vorgenommen wurde und Sie nicht auf den nächsten geplanten Download warten möchten.  

-   Manuelles Zuweisen eines Clients zu einem Configuration Manager-Standort oder Suchen nach einem Standort und Angeben des DNS-Suffixes für Verwaltungspunkte, die auf DNS veröffentlichen.  

-   Konfigurieren des Clientcaches, in dem Dateien vorübergehend gespeichert werden, und Löschen von Dateien im Cache, wenn zusätzlicher Speicherplatz zum Installieren von Software erforderlich ist  

-   Konfigurieren von Einstellungen für die internetbasierte Clientverwaltung  

-   Anzeigen von Konfigurationsbasislinien, die auf dem Client bereitgestellt wurden, Initiieren der Kompatibilitätsauswertung und Anzeigen von Kompatibilitätsberichten  



<!--HONumber=Dec16_HO3-->


