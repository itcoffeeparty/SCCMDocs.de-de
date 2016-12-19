---
title: "Testen von Clientupgrades in einer Präproduktionssammlung | Microsoft Docs"
description: "Testen Sie Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager."
ms.custom: na
ms.date: 12/04/2016
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
ms.sourcegitcommit: 17b36eae97272c408fce20e1f88812dafc984773
ms.openlocfilehash: bfc53760572e71814ebf0e38ea24c5c4684619ee


---
# <a name="how-to-test-client-upgrades-in-a-preproduction-collection-in-system-center-configuration-manager"></a>Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können eine neue Configuration Manager-Clientversion in einer Präproduktionssammlung testen, bevor Sie die neue Version mit einem Upgrade auf den restlichen Standort anwenden.  Dabei werden nur Geräte aktualisiert, die Teil der Testsammlung sind. Nachdem Sie den Client testen konnten, können Sie ihn höherstufen. Auf diese Weise machen Sie die neue Version der Clientsoftware für den übrigen Standort verfügbar.

> [!NOTE]
> Um einen Testclient auf die Produktionsphase höherzustufen, müssen Sie als Benutzer mit der Sicherheitsrolle **Hauptadministrator** und dem Sicherheitsbereich **Alle** angemeldet sein. Weitere Informationen finden Sie unter [Grundlagen der rollenbasierten Verwaltung](/sccm/core/understand/fundamentals-of-role-based-administration). Sie müssen zudem an einem Server angemeldet sein, der mit dem Standort der zentralen Verwaltung oder einem eigenständigen primären Standort auf oberster Ebene verbunden ist.

 Es gibt 3 grundlegende Schritte zum Testen von Clients in der Präproduktionsphase.  

1.  [So konfigurieren Sie automatische Clientupgrades für die Verwendung einer Präproduktionssammlung](#BKMK_config)  

2.  [So installieren Sie ein Configuration Manager-Update, das eine neue Version des Clients enthält](#BKMK_install) Während der Installation geben Sie eine Präproduktionssammlung für die neue Clientsoftware an.  

3.  [So stufen Sie den neuen Client nach erfolgreichem Test auf die Produktionsphase höher](#BKMK_promote)  

> [!TIP]  
>  Wenn Sie ein Upgrade Ihrer Serverinfrastruktur von einer früheren Version von Configuration Manager durchführen \(z.B. Configuration Manager 2007 oder System Center 2012 Configuration Manager\), empfiehlt es sich, die Serverupgrades einschließlich der Installation sämtlicher Branchupdates vollständig abzuschließen. Dadurch wird sichergestellt, dass die neueste Version der Clientsoftware installiert ist, bevor ein Upgrade der Configuration Manager-Clients durchgeführt wird.  

##  <a name="a-namebkmkconfiga-to-configure-automatic-client-upgrades-to-use-a-preproduction-collection"></a><a name="BKMK_config"></a> So konfigurieren Sie automatische Clientupgrades für die Verwendung einer Präproduktionssammlung  

1. Richten Sie eine Sammlung mit den Computern ein, für die der Präproduktionsclient bereitgestellt werden soll. Weitere Informationen zu diesem Schritt finden Sie unter [Erstellen von Sammlungen in Configuration Manager](..\collections\create-collections.md).

> [!NOTE]
> Schließen Sie Arbeitsgruppencomputer nicht in Präproduktionssammlungen ein. Arbeitsgruppencomputer können die für den Verteilungspunkt zum Zugreifen auf das Präproduktionsclientpaket erforderliche Authentifizierung nicht verwenden.   

1.  Öffnen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie **Hierarchieeinstellungen** aus.  

     Führen Sie auf der Registerkarte **Clientupgrade** der Seite **Eigenschaften von Hierarchie-Einstellungen**folgende Aktionen aus:  

    -   Aktivieren Sie **Alle Clients in der Präproduktionssammlung automatisch mithilfe des Präproduktionsclients aktualisieren**  

    -   Geben Sie den Namen einer Sammlung ein, die als Präproduktionssammlung verwendet werden soll  


##  <a name="a-namebkmkinstalla-to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a><a name="BKMK_install"></a> So installieren Sie ein Configuration Manager-Update, das eine neue Version des Clients enthält  

1.  Öffnen Sie in der Configuration Manager-Konsole **Verwaltung** > **Clouddienste** > **Updates und Wartung**, wählen Sie ein Update mit dem Status **Verfügbar** aus, und wählen Sie dann **Updatepaket installieren** aus.  

     Weitere Informationen zum Installieren von Updates finden Sie unter [Updates für System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

2.  Wählen Sie während der Installation des Updates auf der Seite **Clientoptionen** des Assistenten die Option **In der Präproduktionssammlung testen** aus.  

3.  Schließen Sie den Assistenten ab, und installieren Sie das Updatepaket.  

     Nachdem der Assistent abgeschlossen wurde, beginnen die Clients in der Präproduktionssammlung mit der Bereitstellung des aktualisierten Clients. Sie können die Bereitstellung der aktualisierten Clients überwachen, indem Sie auf **Überwachung** > **Clientstatus** > **Präproduktionsclientbereitstellung**gehen. Weitere Informationen finden Sie unter [Überwachen des Status der Clientbereitstellung in System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > Der Bereitstellungsstatus auf den Computern, auf denen Standortsystemrollen in einer Präproduktionssammlung gehostet werden, kann eventuell als **Nicht kompatibel** gemeldet werden, selbst wenn der Client erfolgreich bereitgestellt wurde. Wenn Sie den Client in den Produktivbetrieb versetzen, wird der Bereitstellungsstatus ordnungsgemäß gemeldet.

##  <a name="a-namebkmkpromotea-to-promote-the-new-client-to-production"></a><a name="BKMK_promote"></a> So stufen Sie den neuen Client auf die Produktionsphase höher  

1.  Öffnen Sie in der Configuration Manager-Konsole **Verwaltung** > **Clouddienste** > **Updates und Wartung**, und wählen Sie **Präproduktionsclient höher stufen** aus.

    > [!TIP]
    > Die Schaltfläche **Präproduktionsclient** ist ebenso bei der Überwachung von Clientbereitstellungen in der Konsole unter **Überwachung** > **Clientstatus** > **Präproduktionsclientbereitstellung**verfügbar.

2.  Überprüfen Sie im Dialogfeld die Clientversionen in Produktion und Präproduktion, und stellen Sie sicher, dass die richtige Präproduktionssammlung angegeben ist. Klicken Sie anschließend auf **Höher stufen** Klicken Sie im Bestätigungsdialogfeld auf **Ja**.  

3.  Nach dem Schließen des Dialogfelds wird die aktuelle Clientversion in Ihrer Benutzerhierarchie durch die aktualisierte Clientversion ersetzt. Anschließend können Sie die Clients für den gesamten Standort aktualisieren. Informationen finden Sie unter [Aktualisieren von Clients für Windows-Computer in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  



<!--HONumber=Dec16_HO3-->


