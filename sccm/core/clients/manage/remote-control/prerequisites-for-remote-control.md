---
title: "Voraussetzungen für die Remotesteuerung | Microsoft-Dokumentation"
description: "Hier erhalten Sie Informationen über die Voraussetzungen für die Remotesteuerung in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: 6
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: eafa0d85935c2009cc63d17b06ed83a4666d7fac
ms.lasthandoff: 12/16/2016


---
# <a name="prerequisites-for-remote-control-in-system-center-configuration-manager"></a>Voraussetzungen für die Remotesteuerung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Remotesteuerung in System Center Configuration Manager hat externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts.  

## <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Computer-Grafikkartentreiber|Vergewissern Sie sich, dass auf den Clientcomputern der aktuelle Grafikkartentreiber installiert ist, um bei der Remotesteuerung optimale Ergebnisse zu erzielen.|  

 Computer, auf denen Windows Embedded, Windows Embedded for Point of Service (POS) oder Windows Fundamentals for Legacy PCs ausgeführt wird, unterstützen den Remotesteuerungsviewer nicht, doch sie unterstützen den Remotesteuerungsclient.  

 Die Configuration Manager-Remotesteuerung kann nicht zur Remotesteuerung von Clientcomputern verwendet werden, auf denen Systems Management Server 2003 oder Configuration Manager 2007 ausgeführt wird.  

> [!NOTE]  
>  Es sind keine Windows-Dienste als externe Abhängigkeit für die Remotesteuerung erforderlich.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Unterstützte Betriebssysteme für den Remotesteuerungsviewer  
 In der folgenden Tabelle finden Sie Informationen zu den unterstützten Betriebssystemen für den Remotesteuerungsviewer. Informationen zu unterstützten Clientbetriebssystemen finden Sie unter [Unterstützte Konfigurationen für System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

|Betriebssystem|Unterstützung des Viewers|Weitere Informationen|  
|----------------------|--------------------|----------------------|  
|Windows XP (32-Bit)|Ja|Zum Ausführen des Remotesteuerungsviewers unter diesem Betriebssystem muss zunächst das [Clientupdate für Remotedesktopverbindung 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) aus dem Microsoft Download Center heruntergeladen und installiert werden.|  
|Windows XP (64-Bit)|Nein|keine zusätzlichen Informationen|  
|Windows Vista (32-Bit)|Ja|Zum Ausführen des Remotesteuerungsviewers unter diesem Betriebssystem muss zunächst das [Clientupdate für Remotedesktopverbindung 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) aus dem Microsoft Download Center heruntergeladen und installiert werden.|  
|Windows Vista (64-Bit)|Ja|Zum Ausführen des Remotesteuerungsviewers unter diesem Betriebssystem muss zunächst das [Clientupdate für Remotedesktopverbindung 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) aus dem Microsoft Download Center heruntergeladen und installiert werden.|  
|Windows 7 (32-Bit)|Ja|keine zusätzlichen Informationen|  
|Windows 7 (64-Bit)|Ja|keine zusätzlichen Informationen|  
|Windows Server 2003 (32-Bit)|Nein|keine zusätzlichen Informationen|  
|Windows Server 2003 (64-Bit)|Nein|keine zusätzlichen Informationen|  
|Windows Server 2008 (32-Bit)|Nein|keine zusätzlichen Informationen|  
|Windows Server 2008 (64-Bit)|Nein|keine zusätzlichen Informationen|  
|Windows Server 2008 R2 (64-Bit)|Ja|keine zusätzlichen Informationen|  

## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Remotesteuerung muss für Clients aktiviert werden|Die Remotesteuerung ist in der Standardeinstellung nicht aktiviert, wenn Configuration Manager installiert wird. Informationen zum Aktivieren und Konfigurieren der Remotesteuerung finden Sie unter [Configuring remote control in System Center Configuration Manager (Konfigurieren der Remotesteuerung in System Center Configuration Manager)](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Reporting Services-Punkt|Die Standortsystemrolle des Reporting Services-Punkts muss installiert werden, bevor Berichte für die Remotesteuerung ausgeführt werden können. Weitere Informationen finden Sie unter [Berichterstellung in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Sicherheitsberechtigungen zum Verwalten der Remotesteuerung|Für den Zugriff auf Sammlungsressourcen sowie zum Initiieren einer Remotesteuerungssitzung über die Configuration Manager-Konsole: Berechtigung **AMT steuern**, **Lesen**, **Ressource lesen** und **Remotesteuerung** für das Objekt **Sammlung**.<br /><br /> Die Sicherheitsrolle **Remotetoolsverantwortlicher** umfasst diese Berechtigungen, die zum Verwalten der Remotesteuerung in Configuration Manager erforderlich sind.<br /><br /> Weitere Informationen finden Sie unter [Configure role-based administration for System Center Configuration Manager (Konfigurieren der rollenbasierten Verwaltung)](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Außerdem müssen die Benutzer, denen Berechtigungen zum Verwenden der Remotesteuerung und Remoteunterstützung gewährt werden soll, zur Liste der zugelassenen Remotesteuerungsviewer hinzugefügt werden, indem die Option **Zugelassene Viewer für Remotesteuerung und Remoteunterstützung** in den **Remotetools** -Clienteinstellungen verwendet wird.|  

