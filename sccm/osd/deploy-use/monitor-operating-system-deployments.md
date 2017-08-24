---
title: "Überwachen von Betriebssystembereitstellungen | Microsoft-Dokumentation"
description: "Um Betriebssystembereitstellungsobjekte zu überwachen, bietet die Configuration Manager-Konsole Warnungen, Berichte und verschiedene Statusanzeigen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 154c0a286e6b9ccedc7545eb010967ac00d35407
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-operating-system-deployments-in-system-center-configuration-manager"></a>Überwachen von Betriebssystembereitstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Configuration Manager-Konsole bietet die folgenden Möglichkeiten zum Überwachen von Objekten bei der Betriebssystembereitstellung.  


##  <a name="BKMK_OSDAlerts"></a> Benachrichtigungen zu Betriebssystembereitstellungen  
 Sie können eine Benachrichtigung in den Bereitstellungseinstellungen der Tasksequenz konfigurieren, um Administratoren zu informieren, dass die Kompatibilitätsstufen für die Bereitstellung unter dem konfigurierten Prozentsatz liegen.  

 Nachdem Sie die Warnungseinstellungen konfiguriert haben, wird von Configuration Manager eine Warnung ausgegeben, wenn die angegebenen Bedingungen erfüllt sind. Sie können Bereitstellungsbenachrichtigungen für die Tasksequenz an den folgenden Stellen überprüfen:  

1.  Überprüfen Sie die neuesten Benachrichtigungen im Arbeitsbereich **Softwarebibliothek** im Knoten **Betriebssysteme** .  

2.  Verwalten Sie die konfigurierten Warnungen im Arbeitsbereich **Überwachung** im Knoten **Warnungen** .  

##  <a name="BKMK_TSDeployStatus"></a> Tasksequenz – Bereitstellungsstatus  
 Nachdem Sie eine Tasksequenz bereitgestellt haben, können Sie den Bereitstellungsstatus überwachen. Gehen Sie wie folgt vor, um den Bereitstellungsstatus einer Tasksequenz zu überwachen.  

#### <a name="to-monitor-deployment-status"></a>So überwachen Sie den Bereitstellungsstatus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Klicken Sie im Arbeitsbereich „Überwachung“ auf **Bereitstellungen**.  

3.  Klicken Sie auf die Tasksequenz, deren Bereitstellungsstatus Sie überwachen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen**.  

##  <a name="BKMK_TSReports"></a> Betriebssystembereitstellung – Berichte  
 Es stehen viele vordefinierte Berichte zur Betriebssystembereitstellung zur Verfügung. Diese sind in verschiedene Kategorien unterteilt und dienen dazu, spezifische Informationen zur Zustandsmigration und Bereitstellungen von Tasksequenzen zu liefern. Zusätzlich zu den vorkonfigurierten Berichten können Sie auch benutzerdefinierte Softwareupdateberichte erstellen, die auf die Anforderungen Ihres Unternehmens zugeschnitten sind. Weitere Informationen finden Sie unter [Vorgänge und Wartungstasks für die Berichterstellung](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_MonitorContent"></a> Überwachen von Inhalt  
 Sie können den Inhalt in der Configuration Manager-Konsole überwachen, und so den Status aller Pakettypen im Zusammenhang mit den zugeordneten Verteilungspunkten prüfen. Dies kann den Inhaltsprüfungsstatus des Paketinhalts, den Status von Inhalt, der einer bestimmten Verteilungspunktgruppe zugeordnet ist, den Zustand von Inhalt, der einem Verteilungspunkt zugeordnet ist, und den Status optionaler Funktionen jedes Verteilungspunkts (Inhaltsprüfung, PXE und Multicast) umfassen.  

###  <a name="BKMK_ContentStatus"></a> Überwachung des Inhaltsstatus  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Inhaltsstatus** Informationen zu Inhaltspaketen. Sie können allgemeine Informationen zum Paket, den Verteilungsstatus des Pakets sowie detaillierte Statusinformationen zum Paket prüfen. Gehen Sie wie folgt vor, um den Inhaltsstatus anzuzeigen.  

#### <a name="to-monitor-content-status"></a>So überwachen Sie den Inhaltsstatus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich „Überwachung“ den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Inhaltsstatus**. Die Pakete werden angezeigt.  

3.  Wählen Sie das Paket aus, für das Sie detaillierte Statusinformationen anzeigen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** auf **Status anzeigen**. Detaillierte Statusinformationen zum Paket werden angezeigt.  

###  <a name="BKMK_DPGroupStatus"></a> Status der Verteilungspunktgruppe  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktgruppe** Informationen zu Verteilungspunktgruppen. Sie können allgemeine Informationen zur Verteilungspunktgruppe, wie beispielsweise den Status der Verteilungspunktgruppe und die Kompatibilitätsstufe, sowie detaillierte Informationen zur Verteilungspunktgruppe anzeigen. Gehen Sie wie folgt vor, um den Status einer Verteilungspunktgruppe anzuzeigen.  

#### <a name="to-monitor-distribution-point-group-status"></a>So überwachen Sie den Status einer Verteilungspunktgruppe  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich „Überwachung“ den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Status der Verteilungspunktgruppe**. Die Verteilungspunktgruppen werden angezeigt.  

3.  Wählen Sie die Verteilungspunktgruppe aus, für die detaillierte Statusinformationen angezeigt werden sollen.  

4.  Klicken Sie auf der Registerkarte **Startseite** auf **Status anzeigen**. Detaillierte Statusinformationen zur Verteilungspunktgruppe werden angezeigt.  

###  <a name="BKMK_DPConfigStatus"></a> Status der Verteilungspunktkonfiguration  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktkonfiguration** Informationen zum Verteilungspunkt. Sie können prüfen, welche Attribute für den Verteilungspunkt aktiviert sind, wie z. B. PXE, Multicast und Inhaltsprüfung. Außerdem können Sie detaillierte Statusinformationen zum Verteilungspunkt anzeigen. Gehen Sie wie folgt vor, um den Status einer Verteilungspunktkonfiguration anzuzeigen.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>So überwachen Sie den Status einer Verteilungspunktkonfiguration  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich „Überwachung“ den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Status der Verteilungspunktkonfiguration**. Die Verteilungspunkte werden angezeigt.  

3.  Wählen Sie den Verteilungspunkt aus, für den Statusinformationen angezeigt werden sollen.  

4.  Klicken Sie im Ergebnisbereich auf die Registerkarte **Details** . Statusinformationen zum Verteilungspunkt werden angezeigt.  
