---
title: "Abschließen der Migration | System Center Configuration Manager"
description: "Erfahren Sie, wie Sie die Migration zu einer System Center Configuration Manager-Zielhierarchie abschließen, nachdem eine Quellhierarchie keine Daten mehr enthält."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 862a039ada302c9432fc86d68f5ba9aad360f69b


---
# <a name="planning-to-complete-migration-in-system-center-configuration-manager"></a>Planen des Abschließens der Migration in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn in System Center Configuration Manager eine Quellhierarchie keine Daten mehr enthält, die Sie zur Zielhierarchie migrieren möchten, können Sie den Migrationsprozess abschließen. Der Abschluss der Migration umfasst die folgenden allgemeinen Schritte:  

-   Stellen Sie sicher, dass alle benötigten Daten migriert wurden. Vergewissern Sie sich vor dem Abschließen der Migration aus einer Quellhierarchie, dass Sie alle Ressourcen aus der Quellhierarchie migriert haben, die Sie in der Zielhierarchie benötigen. Bei diesen Ressourcen kann es sich um Daten und Clients handeln.  

-   Beenden Sie das Sammeln von Daten an Quellstandorten. Zum Abschließen der Migration aus einer Quellhierarchie müssen Sie zuerst das Sammeln von Daten an den Quellstandorten beenden.  

-   Bereinigen Sie die Migrationsdaten. Nachdem Sie die Datensammlung für alle Quellstandorte einer Quellhierarchie beendet haben, können Sie die Daten zum Migrationsprozess und zur Quellhierarchie aus der Datenbank der Zielhierarchie entfernen.  

-   Nehmen Sie die Quellhierarchie außer Betrieb. Wenn die Migration aus einer Quellhierarchie abgeschlossen ist und in dieser Hierarchie keine Ressourcen mehr enthalten sind, die von Ihnen verwaltet werden, können Sie die Standorte der Quellhierarchie außer Betrieb nehmen und die entsprechende Infrastruktur aus der Umgebung entfernen. Informationen zur Außerbetriebnahme von Standorten und Quellhierarchien finden Sie in der Dokumentation zur entsprechenden Version von Configuration Manager.  

Verwenden Sie die Informationen in den folgenden Abschnitten, um die Migration aus einer Quellhierarchie zu planen, indem Sie die Datensammlung beenden und anschließend die Migrationsdaten bereinigen:  

-   [Planen des Beendens der Datensammlung](#Plan_to_Stop_Data_Gath)  

-   [Planen der Bereinigung der Migrationsdaten](#Plan_to_clean_up)  

##  <a name="a-nameplantostopdatagatha-plan-to-stop-gathering-data"></a><a name="Plan_to_Stop_Data_Gath"></a> Planen des Beendens der Datensammlung  
 Bevor Sie die Migration abschließen und die Migrationsdaten bereinigen, müssen Sie die Datensammlung von den Quellstandorten in der Quellhierarchie beenden. Wenn keine Daten mehr von einem Quellstandort gesammelt werden sollen, führen Sie den Befehl **Sammeln von Daten beenden** bei den Quellstandorten der untersten Ebene aus und wiederholen den Vorgang dann bei jedem übergeordneten Standort. Der Standort der obersten Ebene der Quellhierarchie muss der letzte Standort sein, an dem Sie die Datensammlung beenden. Beenden Sie die Datensammlung bei jedem untergeordneten Standort, ehe Sie sie bei einem übergeordneten Standort beenden. Üblicherweise wird die Datensammlung erst dann beendet, wenn der Migrationsprozess abgeschlossen werden kann.  

 Nachdem die Datensammlung für einen Quellstandort beendet wurde, sind freigegebene Verteilungspunkte dieses Standorts nicht mehr als Inhaltsorte für Clients in der Zielhierarchie verfügbar. Sorgen Sie deshalb dafür, dass von den Clients in der Zielhierarchie benötigte migrierte Inhalte verfügbar bleiben, indem Sie eine der folgenden Optionen verwenden:  

-   Verteilen Sie Inhalte in der Zielhierarchie an mindestens einen Verteilungspunkt.  

-   Bevor Sie die Datensammlung an einem Quellstandort beenden, sollten Sie freigegebene Verteilungspunkte, auf denen erforderliche Inhalte vorliegen, aktualisieren oder neu zuweisen. Informationen zum Aktualisieren oder erneuten Zuweisen freigegebener Verteilungspunkte finden Sie in den betreffenden Abschnitten im Thema [Planen einer Migrationsstrategie für die Inhaltsbereitstellung in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

Wenn keine Daten mehr von den Quellstandorten in der Quellhierarchie gesammelt werden, können die Migrationsdaten bereinigt werden. Bis die Migrationsdaten bereinigt wurden, sind alle geplanten und ausgeführten Migrationsaufträge in der Configuration Manager-Konsole verfügbar.  

Weitere Informationen zu Quellstandorten und der Datensammlung finden Sie unter [Planen einer Strategie für Quellhierarchien in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="a-nameplantocleanupa-plan-to-clean-up-migration-data"></a><a name="Plan_to_clean_up"></a> Planen der Bereinigung der Migrationsdaten  
 Der letzte Schritt zum Abschließen der Migration besteht in der Bereinigung der Migrationsdaten. Sie können den Befehl **Migrationsdaten bereinigen** verwenden, nachdem Sie die Datensammlung für die einzelnen Quellstandorte in der Quellhierarchie beendet haben. Mit diesem optionalen Vorgang werden Daten zur aktuellen Quellhierarchie aus der Datenbank der Zielhierarchie entfernt.  

 Beim Bereinigen der Migrationsdaten werden die meisten Daten zur Migration aus der Datenbank der Zielhierarchie entfernt. Informationen zu migrierten Objekten werden jedoch beibehalten. Mit diesen Informationen können Sie den Arbeitsbereich **Migration** verwenden, um die Quellhierarchie, in der die migrierten Daten enthalten sind, neu zu konfigurieren. Sie können entweder die Migration von der betreffenden Quellhierarchie fortsetzen oder die Objekte und den Standortbesitz von zuvor migrierten Objekten prüfen.  



<!--HONumber=Nov16_HO1-->

