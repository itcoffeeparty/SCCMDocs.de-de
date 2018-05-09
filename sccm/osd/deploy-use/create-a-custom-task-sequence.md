---
title: Erstellen einer benutzerdefinierten Tasksequenz
titleSuffix: Configuration Manager
description: Bearbeiten einer benutzerdefinierten Tasksequenz in System Center Configuration Manager, um Schritte zur Tasksequenz hinzuzufügen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e5a0e6d8066fc52bf64dd4e53eba4c4dc1c84aa6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-custom-task-sequence-with-system-center-configuration-manager"></a>Erstellen einer benutzerdefinierten Tasksequenz mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn Sie eine benutzerdefinierte Tasksequenz in System Center Configuration Manager erstellen, enthält diese keine Tasksequenzschritte. Nach der Erstellung der Tasksequenz müssen Sie diese bearbeiten und die benötigten Tasksequenzschritte hinzufügen.  

##  <a name="BKMK_CustomTS"></a> Erstellen einer benutzerdefinierten Tasksequenz  
 Gehen Sie folgendermaßen vor, um eine benutzerdefinierte Tasksequenz zu erstellen.  

#### <a name="to-create-a-custom-task-sequence"></a>So erstellen Sie eine benutzerdefinierte Tasksequenz  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenz erstellen** , um den Tasksequenzerstellungs-Assistenten zu starten.  

4.  Wählen Sie auf der Seite **Neue Tasksequenz erstellen** die Option **Neue benutzerdefinierte Tasksequenz erstellen**aus.  

5.  Geben Sie auf der Seite **Informationen zur Tasksequenz** für die Tasksequenz einen Namen, eine Beschreibung und ein optionales von der Tasksequenz zu verwendendes Startabbild an, und schließen Sie dann den Assistenten ab.  

 Nachdem Sie den Tasksequenzerstellungs-Assistenten abgeschlossen haben, fügt Configuration Manager dem Knoten **Tasksequenzen** eine benutzerdefinierte Tasksequenz hinzu. Sie können diese Tasksequenz dann bearbeiten, um ihr Schritte hinzuzufügen.  

 Eine Liste verfügbarer Tasksequenzschritte finden Sie unter [Tasksequenzschritte](../understand/task-sequence-steps.md).  

 Weitere Informationen zum Bearbeiten einer Tasksequenz finden Sie unter [Edit a task sequence (Bearbeiten einer Tasksequenz)](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Am häufigsten werden Sie Tasksequenzen zum Automatisieren von Betriebssystem-Bereitstellungstasks verwenden, aber Sie können auch benutzerdefinierte Tasksequenzen erstellen, um zahlreiche andere Tasks zu automatisieren. Weitere Informationen finden Sie unter [Create a task sequence for non-operating system deployments (Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen)](create-a-task-sequence-for-non-operating-system-deployments.md).  

 ## <a name="next-steps"></a>Nächste Schritte
 [Deploy the task sequence (Bereitstellen der Tasksequenz)](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
