---
title: "Automatisches Kategorisieren von Geräten in Sammlungen | Microsoft-Dokumentation"
description: "Geräte mit System Center Configuration Manager automatisch in Sammlungen kategorisieren."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: d5ef7260bcc2ab9cc56d8fed530a406aa1045c5a

---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>Geräte mit System Center Configuration Manager automatisch in Sammlungen kategorisieren

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können Gerätekategorien erstellen, mit denen Geräte automatisch in Gerätesammlungen platziert werden, wenn Sie Configuration Manager mit Microsoft Intune verwenden. Benutzer müssen eine Gerätekategorie auswählen, wenn sie ein Gerät in Intune registrieren. Sie können außerdem die Kategorie eines Geräts in der Configuration Manager-Konsole ändern.

> [!IMPORTANT]  
    >  Diese Funktion arbeitet mit dem **Juni 2016**-Release von Microsoft Intune. Stellen Sie sicher, dass Sie auf diesen Release aktualisiert haben, bevor Sie diese Verfahren ausprobieren.

## <a name="create-device-categories"></a>Gerätekategorien erstellen

1.  Erweitern Sie **Überblick** im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole, und klicken Sie dann auf **Gerätesammlungen**.
2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Gerätesammlungen** auf **Gerätekategorien verwalten**.
3.  Im Dialogfeld **Gerätekategorien verwalten** können Sie Kategorien erstellen, bearbeiten oder entfernen.

## <a name="associate-a-collection-with-a-device-category"></a>Zuordnen einer Sammlung zu einer Gerätekategorie

Wenn Sie eine Sammlung zu einer Gerätekategorie zuordnen, werden alle Geräte in der von Ihnen angegebenen Kategorie zu dieser Sammlung hinzugefügt.

> [!IMPORTANT]  
    >  Sie können keine Gerätekategorieregel zu einer integrierten Sammlung wie **Alle Systeme** hinzufügen.

1.  Klicken Sie auf der Registerkarte **Mitgliedschaftsregeln** des Dialogfelds **Eigenschaften** einer Gerätesammlung auf **Regel hinzufügen** > **Gerätekategorieregel**.
2.  Wählen Sie im Dialogfeld **Gerätekategorien auswählen** eine oder mehrere Gerätekategorien aus, die auf allen Geräte in der Sammlung angewendet werden.
3.  Schließen Sie das Dialogfeld **Gerätekategorie auswählen** sowie das Dialogfeld „Sammlungseigenschaften“.


## <a name="change-the-category-of-a-device"></a>Ändern der Kategorie eines Geräts

1.  Erweitern Sie den **Überblick** im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole, und klicken Sie dann auf **Geräte**.
2.  Wählen Sie ein Gerät in der Liste **Geräte** aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Gerät** auf **Kategorie ändern**.
3.  Wählen Sie im Dialogfeld **Gerätekategorie bearbeiten** die Kategorie aus, die auf dieses Gerät angewendet werden soll, und klicken Sie dann auf **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Anzeigen der Kategorie eines Geräts

1.  Erweitern Sie **Überblick** im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole, und klicken Sie dann auf **Geräte**.
2.  Die Kategorie wird in der Spalte **Gerätekategorie** in der Liste **Geräte** angezeigt.
> [!TIP]  
    >  Klicken Sie mit der rechten Maustaste auf die Überschrift einer der Spalten in der Liste **Geräte** (wie **Name**), und wählen Sie dann **Gerätekategorie** aus, wenn die Spalte **Gerätekategorie** nicht angezeigt wird.

Wenn Sie ein Gerät zu einer Kategorie zuweisen, und die Kategorie anschließend löschen, zeigt der Bericht **Liste der pro Benutzer in Microsoft Intune registrierten Geräte** eine GUID in der Spalte **Gerätekategorie** statt eines Kategorienamens an.



<!--HONumber=Dec16_HO3-->


