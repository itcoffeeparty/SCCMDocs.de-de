---
title: Verwalten von Sammlungen | Microsoft-Dokumentation
description: "Hier erhalten Sie Informationen zum Ausführen von allgemeinen Verwaltungstasks für Sammlungen in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
caps.latest.revision: 8
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: b41b50c75f1b89c8fc712b53988bd8e24813106d


---
# <a name="how-to-manage-collections-in-system-center-configuration-manager"></a>Verwalten von Sammlungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mithilfe der Übersichtsinformationen in diesem Thema können Sie Verwaltungstasks für Sammlungen in System Center Configuration Manager ausführen.  

> [!NOTE]  
>  Informationen zum Erstellen von Configuration Manager-Sammlungen finden Sie unter [How to create collections in System Center Configuration Manager (Erstellen von Sammlungen in System Center Configuration Manager)](../../../../core/clients/manage/collections/create-collections.md).  

## <a name="how-to-manage-device-collections"></a>Verwalten von Gerätesammlungen  
 Wählen Sie im Arbeitsbereich **Bestand und Kompatibilität** die Option **Gerätesammlungen**und dann die zu verwaltende Sammlung aus. Wählen Sie anschließend einen Verwaltungstask aus.  

 In der nachfolgenden Tabelle finden Sie weitere Informationen zu den Verwaltungstasks, für die möglicherweise einige Informationen benötigt werden, bevor Sie sie auswählen.  

|Verwaltungstask|Details|Weitere Informationen|  
|---------------------|-------------|----------------------|  
|**Mitglieder anzeigen**|Zeigt alle Ressourcen an, die Mitglieder der ausgewählten Sammlung in einem temporären Knoten unter dem Knoten **Geräte** sind.|keine zusätzlichen Informationen|  
|**Ausgewählte Elemente hinzufügen**|Bietet die folgenden Optionen, um eine der folgenden Aktionen auszuführen:<br /><br /> - <br />                    **Ausgewählte Elemente der vorhandenen Gerätesammlung hinzufügen** – öffnet das Dialogfeld **Sammlung auswählen**, in dem Sie die Sammlung auswählen können, der Sie die Mitglieder der ausgewählten Sammlung hinzufügen möchten. Die ausgewählte Sammlung wird durch die Mitgliedschaftsregel **Sammlungen einschließen** in diese Sammlung eingeschlossen.<br /><br /> - **Ausgewählte Elemente der neuen Gerätesammlung hinzufügen** – öffnet den **Assistenten zum Erstellen von Gerätesammlungen**, mit dem Sie eine neue Sammlung erstellen können. Die ausgewählte Sammlung wird durch die Mitgliedschaftsregel **Sammlungen einschließen** in diese Sammlung eingeschlossen.|[How to create collections in System Center Configuration Manager (Erstellen von Sammlungen in System Center Configuration Manager)](../../../../core/clients/manage/collections/create-collections.md)|  
|**Client installieren**|Öffnet den **Assistenten zum Installieren von Configuration Manager-Clients**, von dem mithilfe der Clientpushinstallation auf allen Computern in der ausgewählten Gruppe ein Configuration Manager-Client installiert wird.|[Clientbereitstellungstasks für System Center Configuration Manager](../../../../core/clients/deploy/client-deployment-tasks.md)|  
|**Affinitätsanforderungen verwalten**|Öffnet das Dialogfeld **Affinitätsanforderungen zwischen Benutzer und Gerät verwalten** , in dem Sie ausstehende Anforderungen genehmigen oder ablehnen können, um Affinitäten zwischen Benutzern und Geräten für Geräte in der ausgewählten Sammlung festzulegen.|[Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Erforderliche PXE-Bereitstellungen löschen**|Löscht alle erforderlichen PXE-Startbereitstellungen von allen Mitgliedern der ausgewählten Sammlung.|[Einführung in die Betriebssystembereitstellung](../../../../osd/understand/introduction-to-operating-system-deployment.md)|  
|**Mitgliedschaft aktualisieren**|Wertet die Mitgliedschaft für die ausgewählte Sammlung aus. Bei Sammlungen mit vielen Mitgliedern kann dieser Vorgang einige Zeit in Anspruch nehmen. Mit der Aktion **Aktualisieren** können Sie die Anzeige mit den neuen Sammlungsmitgliedern nach Abschluss des Vorgangs aktualisieren.|keine zusätzlichen Informationen|  
|**Ressourcen hinzufügen**|Öffnet das Dialogfeld **Ressourcen zur Sammlung hinzufügen** , in dem Sie nach neuen Ressourcen zum Hinzufügen zur ausgewählten Sammlung suchen können.<br /><br /> Während des Vorgangs wird für die ausgewählte Sammlung ein Sanduhrsymbol angezeigt.|keine zusätzlichen Informationen|  
|**Clientbenachrichtigung**|Weist alle Clients in der ausgewählten Gerätesammlung an, die Computer- oder Benutzerrichtlinie herunterzuladen.|keine zusätzlichen Informationen|  
|**Endpoint Protection**|Führt eine vollständige oder schnelle Antischadsoftware-Überprüfung aus oder lädt die aktuellen Antischadsoftware-Definitionen auf Computer in der ausgewählten Sammlung herunter.|[Endpoint Protection in System Center Configuration Manager](../../../../protect/deploy-use/endpoint-protection.md)|  
|**Exportierenieren**|Öffnet den **Assistenten zum Exportieren von Sammlungen**, mit dem Sie diese Sammlung in eine MOF-Datei (Managed Object Format) exportieren können, die dann an einem anderen Configuration Manager-Standort archiviert oder verwendet werden kann.<br /><br /> Wenn Sie eine Sammlung exportieren, werden Sammlungen, auf die durch Anwenden einer Regel ( **Einschließen** oder **Ausschließen** ) in der ausgewählten Sammlung verwiesen wird, nicht exportiert.|keine zusätzlichen Informationen|  
|**Kopieren**|Erstellt eine Kopie der ausgewählten Sammlung. Von der neuen Sammlung wird die ausgewählte Sammlung als begrenzende Sammlung verwendet.|keine zusätzlichen Informationen|  
|**Löschen**|Löscht die ausgewählte Sammlung. Sie können auch alle Ressourcen in der Sammlung aus der Standortdatenbank löschen.<br /><br /> In Configuration Manager integrierte Sammlungen können nicht gelöscht werden.|Eine Liste der integrierten Sammlungen finden Sie unter [Introduction to collections in System Center Configuration Manager (Einführung in Sammlungen in System Center Configuration Manager)](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Bereitstellung simulieren**|Öffnet den **Assistenten zum Simulieren der Anwendungsbereitstellung** , mit dem Sie die Ergebnisse einer Anwendungsbereitstellung ohne Installieren oder Deinstallieren einer Anwendung überprüfen können.|[Simulieren von Anwendungsbereitstellungen mit System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Bereitstellen**|Zeigt folgende Optionen an:<br /><br /> - <br />                    **Anwendung** – öffnet den **Assistenten zum Bereitstellen von Software**, mit dem Sie eine Anwendungsbereitstellung für die ausgewählte Sammlung auswählen und konfigurieren können.<br /><br /> - <br />                    **Programm** – öffnet den **Assistenten zum Bereitstellen von Software** , mit dem Sie eine Paket- und Programmbereitstellung für die ausgewählte Sammlung auswählen und konfigurieren können.<br /><br /> - **Konfigurationsbaseline** – öffnet das Dialogfeld **Konfigurationsbaselines bereitstellen**, mit dem Sie die Bereitstellung von einer oder mehreren Konfigurationsbaselines für die ausgewählte Sammlung konfigurieren können.<br /><br /> - <br />                    **Tasksequenz** – öffnet den **Assistenten zum Bereitstellen von Software** , mit dem Sie eine Tasksequenzbereitstellung für die ausgewählte Sammlung auswählen und konfigurieren können.<br /><br /> - <br />                    **Softwareupdates** – öffnet den **Assistenten zum Bereitstellen von Softwareupdates**, mit dem Sie die Bereitstellung von Softwareupdates für Ressourcen in der ausgewählten Sammlung konfigurieren können.|[Bereitstellen von Anwendungen mit System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Pakete und Programme in System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [Bereitstellen von Konfigurationsbaselines in System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)<br /><br /> [Verwalten von Tasksequenzen zum Automatisieren von Aufgaben in System Center Configuration Manager](../../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)<br /><br /> [Verwalten von Softwareupdates in System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction)|  

## <a name="how-to-manage-user-collections"></a>Verwalten von Benutzersammlungen  
 Wählen Sie im Arbeitsbereich **Bestand und Kompatibilität** die Option **Benutzersammlungen**und dann die zu verwaltende Sammlung aus. Wählen Sie anschließend einen Verwaltungstask aus.  

 In der nachfolgenden Tabelle finden Sie weitere Informationen zu den Verwaltungstasks, für die möglicherweise einige Informationen benötigt werden, bevor Sie sie auswählen.  

|Verwaltungstask|Details|Weitere Informationen|  
|---------------------|-------------|----------------------|  
|**Mitglieder anzeigen**|Zeigt alle Ressourcen an, die Mitglieder der ausgewählten Sammlung in einem temporären Knoten unter dem Knoten **Benutzer** sind.|keine zusätzlichen Informationen|  
|**Ausgewählte Elemente hinzufügen**|Mit dieser Option können Sie eine der folgenden Aktionen ausführen:<br /><br /> - <br />                    **Ausgewählte Elemente der vorhandenen Benutzersammlung hinzufügen** – öffnet das Dialogfeld **Sammlung auswählen**, in dem Sie die Sammlung auswählen können, der Sie die Mitglieder der ausgewählten Sammlung hinzufügen möchten. Die ausgewählte Sammlung wird durch die Mitgliedschaftsregel **Sammlungen einschließen** in diese Sammlung eingeschlossen.<br /><br /> - **Ausgewählte Elemente der neuen Benutzersammlung hinzufügen** – öffnet den **Assistenten zum Erstellen von Benutzersammlungen**, mit dem Sie eine neue Sammlung erstellen können. Die ausgewählte Sammlung wird durch die Mitgliedschaftsregel **Sammlungen einschließen** in diese Sammlung eingeschlossen.|[How to create collections in System Center Configuration Manager (Erstellen von Sammlungen in System Center Configuration Manager)](../../../../core/clients/manage/collections/create-collections.md)|  
|**Affinitätsanforderungen verwalten**|Öffnet das Dialogfeld **Affinitätsanforderungen zwischen Benutzer und Gerät verwalten** , in dem Sie ausstehende Anforderungen genehmigen oder ablehnen können, um Affinitäten zwischen Benutzern und Geräten für Benutzer in der ausgewählten Sammlung festzulegen.|[Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Mitgliedschaft aktualisieren**|Wertet die Mitgliedschaft für die ausgewählte Sammlung aus. Bei Sammlungen mit vielen Mitgliedern kann dieser Vorgang einige Zeit in Anspruch nehmen. Mit der Aktion **Aktualisieren** können Sie die Anzeige mit den neuen Sammlungsmitgliedern nach Abschluss des Vorgangs aktualisieren.<br /><br /> Während des Vorgangs wird für die ausgewählte Sammlung ein Sanduhrsymbol angezeigt.|keine zusätzlichen Informationen|  
|**Ressourcen hinzufügen**|Öffnet das Dialogfeld **Ressourcen zur Sammlung hinzufügen** , in dem Sie nach neuen Ressourcen zum Hinzufügen zur ausgewählten Sammlung suchen können.|keine zusätzlichen Informationen|  
|**Exportierenieren**|Öffnet den **Assistenten zum Exportieren von Sammlungen**, mit dem Sie diese Sammlung in eine MOF-Datei (Managed Object Format) exportieren können, die dann an einem anderen Configuration Manager-Standort archiviert oder verwendet werden kann.<br /><br /> Wenn Sie eine Sammlung exportieren, werden Sammlungen, auf die durch Anwenden einer Regel ( **Einschließen** oder **Ausschließen** ) in der ausgewählten Sammlung verwiesen wird, nicht exportiert.|keine zusätzlichen Informationen|  
|**Kopieren**|Erstellt eine Kopie der ausgewählten Sammlung. Von der neuen Sammlung wird die ausgewählte Sammlung als begrenzende Sammlung verwendet.|keine zusätzlichen Informationen|  
|**Löschen**|Löscht die ausgewählte Sammlung. Sie können auch alle Ressourcen in der Sammlung aus der Standortdatenbank löschen.<br /><br /> In Configuration Manager integrierte Sammlungen können nicht gelöscht werden.|Eine Liste der integrierten Sammlungen finden Sie unter [Introduction to collections in System Center Configuration Manager (Einführung in Sammlungen in System Center Configuration Manager)](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Bereitstellung simulieren**|Öffnet den **Assistenten zum Simulieren der Anwendungsbereitstellung** , mit dem Sie die Ergebnisse einer Anwendungsbereitstellung ohne Installieren oder Deinstallieren einer Anwendung überprüfen können.|[Simulieren von Anwendungsbereitstellungen mit System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Bereitstellen**|Zeigt folgende Optionen an:<br /><br /> - **Anwendung** – öffnet den **Assistenten zum Bereitstellen von Software**, mit dem Sie eine Anwendungsbereitstellung für die ausgewählte Sammlung auswählen und konfigurieren können.<br /><br /> - <br />                    **Programm** – öffnet den **Assistenten zum Bereitstellen von Software** , mit dem Sie eine Paket- und Programmbereitstellung für die ausgewählte Sammlung auswählen und konfigurieren können.<br /><br /> - **Konfigurationsbaseline** – öffnet das Dialogfeld **Konfigurationsbaselines bereitstellen**, mit dem Sie die Bereitstellung von einer oder mehreren Konfigurationsbaselines für die ausgewählte Sammlung konfigurieren können.|[Bereitstellen von Anwendungen mit System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Pakete und Programme in System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [Bereitstellen von Konfigurationsbaselines in System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)|  

##  <a name="a-namebkmkcollpropa-collection-properties"></a><a name="BKMK_CollProp"></a> Sammlungseigenschaften  
 Wenn Sie das Dialogfeld **Eigenschaften** einer Sammlung öffnen, können Sie die folgenden Eigenschaften einer Sammlung anzeigen und konfigurieren.  

|Name der Registerkarte|Weitere Informationen|  
|--------------|----------------------|  
|**Allgemein**|Auf dieser Registerkarte können Sie allgemeine Informationen zur ausgewählten Sammlung anzeigen und konfigurieren, einschließlich des Sammlungsnamens und der begrenzenden Sammlung.|  
|**Mitgliedschaftsregeln**|Auf dieser Registerkarte können Sie die Mitgliedschaftsregeln konfigurieren, in denen die Mitgliedschaft dieser Sammlung definiert wird. Weitere Informationen finden Sie unter [How to create collections in System Center Configuration Manager (Erstellen von Sammlungen in System Center Configuration Manager)](../../../../core/clients/manage/collections/create-collections.md).|  
|**Energieverwaltung**|Auf dieser Registerkarte können Sie Energieverwaltungspläne konfigurieren, die Computern in der ausgewählten Gruppe zugewiesen sind. Weitere Informationen finden Sie unter [Einführung in die Energieverwaltung](../../../../core/clients/manage/power/introduction-to-power-management.md).|  
|**Bereitstellungen**|Auf dieser Registerkarte wird jede Software angezeigt, die für Mitglieder der ausgewählten Sammlung bereitgestellt wurde.|  
|**Wartungsfenster**|Auf dieser Registerkarte können Sie Wartungsfenster anzeigen und konfigurieren, die auf Mitglieder der ausgewählten Sammlung angewendet werden. Weitere Informationen finden Sie unter [How to use maintenance windows in System Center Configuration Manager (Verwenden von Wartungsfenstern in System Center Configuration Manager)](../../../../core/clients/manage/collections/use-maintenance-windows.md).|  
|**Sammlungsvariablen**|Auf dieser Registerkarte können Sie Variablen konfigurieren, die für diese Sammlung gelten und die von Tasksequenzen verwendet werden können. Weitere Informationen finden Sie unter [Task sequence built-in variables (Integrierte Tasksequenzvariablen)](../../../../osd/understand/task-sequence-built-in-variables.md).|  
|**Verteilungspunktgruppen**|Auf dieser Registerkarte können Sie eine oder mehrere Verteilungspunktgruppen zu Mitgliedern der ausgewählten Sammlung zuordnen. Weitere Informationen finden Sie unter [Manage content and content infrastructure for System Center Configuration Manager (Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager)](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Sicherheit**|Auf dieser Registerkarte können Sie die Administratoren anzeigen, die dank zugeordneter Rollen und Sicherheitsbereiche über Berechtigungen für die ausgewählte Sammlung verfügen|  
|**Monitor**|Auf dieser Registerkarte können Sie konfigurieren, wann Warnungen zu Clientstatus und Endpoint Protection generiert werden. Weitere Informationen finden Sie unter [How to configure client status in System Center Configuration Manager (Konfigurieren des Clientstatus in System Center Configuration Manager)](../../../../core/clients/deploy/configure-client-status.md) und unter [How to monitor Endpoint Protection in System Center Configuration Manager (Überwachen von Endpoint Protection in System Center Configuration Manager)](../../../../protect/deploy-use/monitor-endpoint-protection.md).|  



<!--HONumber=Dec16_HO3-->


