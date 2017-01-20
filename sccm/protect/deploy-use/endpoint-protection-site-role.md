---
title: Konfigurieren von Endpoint Protection | Microsoft-Dokumentation
description: "Informationen über das Konfigurieren von Endpoint Protection zum Verwalten von Sicherheit und Schadsoftware auf Configuration Manager-Clientcomputern."
defintion: 
definition: 
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 4639203bf5e90486ce4b97abc2fc4f54eae3afe9


---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Erstellen einer Endpoint Protection-Standortsystemrolle

*Gilt für: System Center Configuration Manager (Current Branch)*

 Die Standortsystemrolle für den Endpoint Protection-Punkt muss installiert sein, bevor Sie Endpoint Protection verwenden können. Sie darf nur auf einem einzigen Standortsystemserver installiert sein, und sie muss auf der obersten Hierarchieebene eines zentralen Verwaltungsstandorts oder eines eigenständigen primären Standorts installiert sein.

 Verwenden Sie eins der folgenden Verfahren, je nachdem, ob Sie einen neuen Standortsystemserver für Endpoint Protection installieren oder einen bestehenden Standortsystemserver verwenden möchten:
 - [Installieren auf einem neuen Standortsystemserver](#new-site-system-server)
 - [Installieren auf einem bestehenden Standortsystemserver](#existing-site-system-server)

> [!IMPORTANT]
>  Bei der Installation eines Endpoint Protection-Punkts ist ein Endpoint Protection-Client auf dem Server installiert, der den Endpoint Protection-Punkt hostet. Dienste und Überprüfungen sind auf diesem Client deaktiviert, damit er gemeinsam mit einer bestehenden Antischadsoftwarelösung auf dem Server installiert sein kann. Wenn Sie diesen Server später für die Verwaltung mit Endpoint Protection aktivieren und die Option auswählen, alle Antischadsoftware-Lösungen von Drittanbietern zu entfernen, werden Produkte von Drittanbietern nicht entfernt. Solche Produkte müssen manuell deinstalliert werden.

## <a name="new-site-system-server"></a>neuer Standortsystemserver

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Server und Standortsystemrollen**.

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Standortsystemserver erstellen**.

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an, und klicken Sie dann auf **Weiter**.

5.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Endpoint Protection-Punkt** aus, und klicken Sie dann auf **Weiter**.

6.  Aktivieren Sie auf der Seite **Endpoint Protection** das Kontrollkästchen **Ich stimme den Endpoint Protection-Lizenzbedingungen zu** , und klicken Sie dann auf **Weiter**.

    > [!IMPORTANT]
    >  Sie können Endpoint Protection nur in Configuration Manager nutzen, wenn Sie dem Lizenzvertrag zustimmen.

7.  Wählen Sie die Informationsebene aus, die Sie an Microsoft senden wollen, um die Entwicklung neuer Definitionen zu unterstützen auf der Seite **Cloud Protection Service** aus, und klicken Sie dann auf **Weiter**.

    > [!NOTE]
    >  Mit dieser Option werden die Einstellungen des Cloud Protection Service (ehem. Microsoft Active Protection Service oder MAPS) konfiguriert, die als Standard verwendet werden. Anschließend können Sie benutzerdefinierte Einstellungen für jede Richtlinie für Antischadsoftware konfigurieren, die Sie erstellen. Treten Sie Cloud Protection Service bei, um Ihre Computer besser sichern zu können, indem Sie Microsoft Schadsoftwarebeispiele zur Aktualisierung der Antischadsoftwaredefinitionen zur Verfügung stellen. Wenn Sie Cloud Protection Service beitreten, kann der Endpoint Protection-Client außerdem den Dienst für dynamische Signaturen verwenden, um neue Definitionen herunterzuladen, bevor diese in Windows Update veröffentlicht werden. Weitere Informationen finden Sie unter [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).

8.  Schließen Sie den Assistenten ab.

> [!div class="button"]
[Nächster Schritt >](endpoint-configure-alerts.md)

> [!div class="button"]
[Zurück >](endpoint-protection-configure.md)

## <a name="existing-site-system-server"></a>bestehender Standortsystemserver

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, klicken Sie auf **Server und Standortsystemrollen**, und wählen Sie den Server aus, den Sie für Endpoint Protection verwenden möchten.

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Server** auf **Standortsystemrollen hinzufügen**.

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an, und klicken Sie dann auf **Weiter**.

5.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Endpoint Protection-Punkt** aus, und klicken Sie dann auf **Weiter**.

6.  Aktivieren Sie auf der Seite **Endpoint Protection** das Kontrollkästchen **Ich stimme den Endpoint Protection-Lizenzbedingungen zu** , und klicken Sie dann auf **Weiter**.

    > [!IMPORTANT]
    >  Sie können Endpoint Protection nur in Configuration Manager nutzen, wenn Sie dem Lizenzvertrag zustimmen.

7.  Wählen Sie die Informationsebene aus, die Sie an Microsoft senden wollen, um die Entwicklung neuer Definitionen zu unterstützen auf der Seite **Cloud Protection Service** aus, und klicken Sie dann auf **Weiter**.

    > [!NOTE]
    >  Mit dieser Option werden die Einstellungen des Cloud Protection Service (ehem. Microsoft Active Protection Service oder MAPS) konfiguriert, die als Standard verwendet werden. Anschließend können Sie benutzerdefinierte Einstellungen für jede Richtlinie für Antischadsoftware konfigurieren, die Sie erstellen. Weitere Informationen finden Sie unter [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).

8.  Schließen Sie den Assistenten ab.

> [!div class="button"]
[Nächster Schritt >](endpoint-configure-alerts.md)

> [!div class="button"]
[Zurück >](endpoint-protection-configure.md)



<!--HONumber=Dec16_HO3-->


