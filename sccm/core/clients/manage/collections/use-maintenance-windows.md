---
title: Verwenden von Wartungsfenstern | Microsoft-Dokumentation
description: Verwenden Sie Sammlungen und Wartungsfenster in System Center Configuration Manager, um Clients effektiv zu verwalten.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: e59953f41422ee8f79ca054b5ccaccf41bb4e7af


---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Verwenden von Wartungsfenstern in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit Wartungsfenstern in System Center Configuration Manager können Administratoren einen Zeitraum definieren, innerhalb dessen verschiedene Configuration Manager-Vorgänge für Mitglieder einer Gerätesammlung ausgeführt werden können. Sie können die Wartungsfenster verwenden, um Konfigurationsänderungen bei den Clients dann vorzunehmen, wenn sie die Produktivität des Unternehmens nicht beeinträchtigen.  

 Wartungsfenster werden von folgenden Configuration Manager-Vorgängen unterstützt:  

-   Softwarebereitstellungen  

-   Softwareupdatebereitstellungen  

-   Bereitstellen und Bewerten von Kompatibilitätseinstellungen  

-   Betriebssystembereitstellungen  

-   Tasksequenzbereitstellungen  

 Wartungsfenster werden mit Startdatum, Start- und Endzeit sowie Wiederholungsmuster für eine Sammlung konfiguriert. Die Dauer von Wartungsfenstern muss weniger als 24 Stunden betragen. In der Standardeinstellung sind Computerneustarts durch Bereitstellungen außerhalb von Wartungsfenstern nicht zulässig. Sie können die Standardeinstellung in den Einstellungen für jede Bereitstellung jedoch außer Kraft setzen. Wartungsfenster beziehen sich nur auf den Zeitraum, in dem das Bereitstellungsprogramm ausgeführt wird. Von Anwendungen, die für den lokalen Download und die lokale Ausführung konfiguriert sind, können auch außerhalb des Wartungsfensters Inhalte heruntergeladen werden.  

 Wenn ein Clientcomputer Mitglied einer Gerätesammlung mit konfiguriertem Wartungsfenster ist, wird ein Bereitstellungsprogramm nur dann ausgeführt, wenn die maximal zulässige Laufzeit nicht die Dauer überschreitet, die für das Wartungsfenster konfiguriert ist. Kann das Programm nicht ausgeführt werden, wird eine Warnung ausgegeben, und die Bereitstellung wird während des nächsten geplanten Wartungsfensters ausgeführt, das Zeitkapazitäten hat.  

## <a name="using-multiple-maintenance-windows"></a>Verwenden mehrerer Wartungsfenster  
 Wenn ein Clientcomputer Mitglied mehrerer Gerätesammlungen mit konfigurierten Wartungsfenstern ist, gelten die folgenden Regeln:  

-   Wenn sich die Wartungsfenster nicht überschneiden, werden sie als zwei unabhängige Wartungsfenster behandelt.  

-   Wenn sich die Wartungsfenster überschneiden, werden sie als ein einziges Wartungsfenster behandelt, das den Zeitraum beider Wartungsfenster umfasst. Beispielsweise betrüge bei zwei Wartungsfenstern von jeweils einer Stunde Dauer, die sich um 30 Minuten überschneiden, die effektive Dauer des Wartungsfensters 90 Minuten.  

 Wenn ein Benutzer im Softwarecenter eine Anwendungsinstallation initiiert, wird die Anwendung unabhängig von konfigurierten Wartungsfenstern sofort installiert.  

 Wenn die Installationsfrist einer als **erforderlich** eingestuften Anwendungsbereitstellung außerhalb der Geschäftszeiten abläuft, die von einem Benutzer im Softwarecenter konfiguriert wurden, wird die Anwendung installiert.  

### <a name="how-to-configure-maintenance-windows"></a>Konfigurieren von Wartungsfenstern  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**.  

3.  Wählen Sie in der Liste **Gerätesammlungen** die Sammlung aus, für die Sie ein Wartungsfenster konfigurieren möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie auf der Registerkarte **Wartungsfenster** des Dialogfelds **&lt;Sammlungsname\> Eigenschaften** auf das Symbol **Neu**.  

    > [!NOTE]  
    >  Es können keine Wartungsfenster für die Sammlung **Alle Systeme** erstellt werden.  

6.  Geben Sie im Dialogfeld **&lt;Neu\> Zeitplan** einen Namen, einen Zeitplan, und ein Wiederholungsmuster für das Wartungsfenster an. Sie können auch die Option aktivieren, durch die der Zeitplan nur auf Tasksequenzen angewendet wird.  

7.  Wählen Sie in der Dropdownliste **Diesen Zeitplan anwenden auf** aus, ob dieses Wartungsfenster für alle Bereitstellungen, nur Softwareupdates oder nur Tasksequenzen gelten soll.  

8.  Klicken Sie auf **OK**, um das Dialogfeld **&lt;Neu\> Zeitplan** zu schließen, und das neue Wartungsfenster zu erstellen.  

9. Schließen Sie das Dialogfeld **&lt;Sammlungsname\> Eigenschaften**.  



<!--HONumber=Dec16_HO3-->


