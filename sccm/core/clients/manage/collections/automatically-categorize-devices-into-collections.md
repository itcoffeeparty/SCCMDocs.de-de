---
title: "Automatisches Kategorisieren von Geräten in Sammlungen | Microsoft-Dokumentation"
description: "Geräte mit System Center Configuration Manager automatisch in Sammlungen kategorisieren."
ms.custom: na
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: "5"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 0de7a3d4183fb00f444a27c45d178141dc4e9375
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2017
---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>Geräte mit System Center Configuration Manager automatisch in Sammlungen kategorisieren

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können Gerätekategorien erstellen, mit denen Geräte automatisch in Gerätesammlungen platziert werden, wenn Sie Configuration Manager mit Microsoft Intune verwenden. Benutzer müssen eine Gerätekategorie auswählen, wenn sie ein Gerät in Intune registrieren. Sie können außerdem eine Gerätekategorie in der Configuration Manager-Konsole ändern.

> [!IMPORTANT]  
    >  Diese Funktion wird vom Microsoft Intune-Release vom **Juni 2016** und später unterstützt. Stellen Sie sicher, dass Sie über dieses Release verfügen, bevor Sie dieses Verfahren ausprobieren.

## <a name="create-device-categories"></a>Gerätekategorien erstellen

1.  Wechseln Sie zu **Bestand und Konformität** > **Übersicht** >  **Gerätesammlungen**.
2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Gerätesammlungen** die Option **Gerätekategorien verwalten** aus.
3.  Erstellen, bearbeiten oder entfernen Sie Kategorien.

## <a name="associate-a-collection-with-a-device-category"></a>Ordnen Sie eine Sammlung einer Gerätekategorie zu

Wenn Sie eine Sammlung einer Gerätekategorie zuordnen, werden alle Geräte in der Kategorie der Sammlung hinzugefügt. Sie können keine Gerätekategorieregel zu einer integrierten Sammlung wie **Alle Systeme** hinzufügen.

1.  Wählen Sie auf der Registerkarte **Mitgliedschaftsregeln** des Dialogfelds **Eigenschaften** einer Gerätesammlung **Regel hinzufügen** > **Device Category Rule** (Gerätekategorieregel) aus.
2.  Wählen Sie im Dialogfeld **Gerätekategorien auswählen** eine oder mehrere Gerätekategorien aus, die auf allen Geräte in der Sammlung angewendet werden.

## <a name="change-the-category-of-a-device"></a>Ändern der Gerätekategorie

1.  Wählen Sie unter **Bestand und Konformität** > **Übersicht** > **Geräte** ein Gerät in der Liste **Geräte** aus.
2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Gerät** dann **Kategorie ändern** aus.
3.  Wählen Sie eine Kategorie und anschließend **OK** aus.

## <a name="view-which-category-a-device-belongs-to"></a>Anzeigen der Kategorie eines Geräts

Unter **Bestand und Konformität** > **Übersicht** > **Geräte** wird in der Liste **Geräte** die Kategorie in der Spalte **Gerätekategorie** angezeigt.

Klicken Sie mit der rechten Maustaste auf die Überschrift einer der Spalten in der Liste **Geräte** (wie **Name**), und wählen Sie dann **Gerätekategorie** aus, wenn die Spalte **Gerätekategorie** nicht angezeigt wird.

Wenn Sie ein Gerät zu einer Kategorie zuweisen, und die Kategorie anschließend löschen, zeigt der Bericht **Liste der pro Benutzer in Microsoft Intune registrierten Geräte** eine GUID in der Spalte **Gerätekategorie** statt eines Kategorienamens an.
