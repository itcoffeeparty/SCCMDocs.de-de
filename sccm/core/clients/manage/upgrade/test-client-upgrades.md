---
title: "Testen von Clientupgrades in einer Präproduktionssammlung | Microsoft-Dokumentation"
description: "Testen Sie Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager."
ms.custom: na
ms.date: 12/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
caps.latest.revision: 10
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 52d2e088b8db3c2e9a0af640ca3db72b9fd7af60
ms.openlocfilehash: 250c9312b932670c408554f3968ae43ae4f3dbaa


---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-system-center-configuration-manager"></a>Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können eine neue Configuration Manager-Clientversion in einer Präproduktionssammlung testen, bevor Sie die neue Version mit einem Upgrade auf den restlichen Standort anwenden.  Dabei werden nur Geräte aktualisiert, die Teil der Testsammlung sind. Nachdem Sie den Client testen konnten, können Sie ihn höherstufen. Auf diese Weise machen Sie die neue Version der Clientsoftware für den übrigen Standort verfügbar.

> [!NOTE]
> Um einen Testclient auf die Produktionsphase höherzustufen, müssen Sie als Benutzer mit der Sicherheitsrolle **Hauptadministrator** und dem Sicherheitsbereich **Alle** angemeldet sein. Weitere Informationen finden Sie unter [Grundlagen der rollenbasierten Verwaltung](/sccm/core/understand/fundamentals-of-role-based-administration). Sie müssen zudem an einem Server angemeldet sein, der mit dem Standort der zentralen Verwaltung oder einem eigenständigen primären Standort auf oberster Ebene verbunden ist.

 Es gibt 3 grundlegende Schritte zum Testen von Clients in der Präproduktionsphase.  

1.  Konfigurieren Sie automatische Clientupgrades für die Verwendung einer Präproduktionssammlung.  

2.  Installieren Sie ein Configuration Manager-Update, das eine neue Version des Clients enthält.  

3.  Stufen Sie den neuen Client auf die Produktionsphase höher.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>So konfigurieren Sie automatische Clientupgrades für die Verwendung einer Präproduktionssammlung  

1. [Richten Sie eine Sammlung mit den Computern ein](..\collections\create-collections.md), für die der Präproduktionsclient bereitgestellt werden soll. Schließen Sie Arbeitsgruppencomputer nicht in Präproduktionssammlungen ein. Arbeitsgruppencomputer können die für den Verteilungspunkt zum Zugreifen auf das Präproduktionsclientpaket erforderliche Authentifizierung nicht verwenden.   

1.  Öffnen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie **Hierarchieeinstellungen** aus.  

     Führen Sie auf der Registerkarte **Clientupgrade** der Seite **Eigenschaften von Hierarchie-Einstellungen**folgende Aktionen aus:  

    -   Aktivieren Sie **Alle Clients in der Präproduktionssammlung automatisch mithilfe des Präproduktionsclients aktualisieren**  

    -   Geben Sie den Namen einer Sammlung ein, die als Präproduktionssammlung verwendet werden soll  

![Testen von Clientupgrades](media/test-client-upgrades.png)


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>So installieren Sie ein Configuration Manager-Update, das eine neue Version des Clients enthält  

1.  Öffnen Sie in der Configuration Manager-Konsole **Verwaltung** > **Clouddienste** > **Updates und Wartung**, wählen Sie ein Update mit dem Status **Verfügbar** aus, und wählen Sie dann **Updatepaket installieren** aus.  

     Weitere Informationen zum Installieren von Updates finden Sie unter [Updates für System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

2.  Wählen Sie während der Installation des Updates auf der Seite **Clientoptionen** des Assistenten die Option **In der Präproduktionssammlung testen** aus.  

3.  Schließen Sie den Assistenten ab, und installieren Sie das Updatepaket.  

     Nachdem der Assistent abgeschlossen wurde, beginnen die Clients in der Präproduktionssammlung mit der Bereitstellung des aktualisierten Clients. Sie können die Bereitstellung der aktualisierten Clients überwachen, indem Sie auf **Überwachung** > **Clientstatus** > **Präproduktionsclientbereitstellung**gehen. Weitere Informationen finden Sie unter [Überwachen des Status der Clientbereitstellung in System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > Der Bereitstellungsstatus auf den Computern, auf denen Standortsystemrollen in einer Präproduktionssammlung gehostet werden, kann eventuell als **Nicht kompatibel** gemeldet werden, selbst wenn der Client erfolgreich bereitgestellt wurde. Wenn Sie den Client in den Produktivbetrieb versetzen, wird der Bereitstellungsstatus ordnungsgemäß gemeldet.

##  <a name="to-promote-the-new-client-to-production"></a>So stufen Sie den neuen Client auf die Produktionsphase höher  

1.  Öffnen Sie in der Configuration Manager-Konsole **Verwaltung** > **Clouddienste** > **Updates und Wartung**, und wählen Sie **Präproduktionsclient höher stufen** aus.

    > [!TIP]
    > Die Schaltfläche **Präproduktionsclient** ist ebenso bei der Überwachung von Clientbereitstellungen in der Konsole unter **Überwachung** > **Clientstatus** > **Präproduktionsclientbereitstellung**verfügbar.

2.  Überprüfen Sie die Clientversionen in Produktion und Präproduktion, und stellen Sie sicher, dass die richtige Präproduktionssammlung angegeben ist. Klicken Sie anschließend erst auf **Höher stufen** und dann auf **Ja**.  

3.  Nach Schließen des Dialogfelds wird die Clientversion in Ihrer Hierarchie durch die aktualisierte Clientversion ersetzt. Anschließend können Sie die Clients für den gesamten Standort aktualisieren. Informationen finden Sie unter [Aktualisieren von Clients für Windows-Computer in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  



<!--HONumber=Jan17_HO1-->

