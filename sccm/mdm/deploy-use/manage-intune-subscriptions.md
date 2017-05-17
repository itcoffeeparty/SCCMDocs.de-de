---
title: Verwalten Ihres Intune-Abonnements, das System Center Configuration Manager zugeordnet ist | Microsoft-Dokumentation
description: Verwalten Ihres Intune-Abonnements, das System Center Configuration Manager zugeordnet ist.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 2e0b3cd1070d0f8adb1219acd33c3126d2758a49
ms.contentlocale: de-de
ms.lasthandoff: 05/17/2017

---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>Verwalten Ihres Intune-Abonnements, das System Center Configuration Manager zugeordnet ist

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn Sie Configuration Manager ein Microsoft Intune-Abonnement (Testabonnement oder kostenpflichtiges Abonnement) hinzufügen und dann zu einem anderen Intune-Abonnement wechseln müssen, müssen Sie sowohl das **Microsoft Intune-Abonnement** als auch den **Dienstverbindungspunkt** aus der Configuration Manager-Konsole löschen, bevor Sie ein neues Abonnement hinzufügen können.

> [!NOTE]
> Sie können jeweils nur ein Intune-Abonnement in der hybriden Verwaltung mobiler Geräte konfigurieren.

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Löschen eines Intune-Abonnements aus Configuration Manager

> [!IMPORTANT]
>  Alle Inhalte, einschließlich Benutzerregistrierungen, Richtlinien und App-Bereitstellungen, die für Geräte konfiguriert sind, die vom Intune-Abonnement verwaltet werden, werden beim Löschen des Abonnements entfernt.

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Übersicht** > **Clouddienste** > **Microsoft Intune-Abonnements** aus.

2.  Klicken Sie mit der rechten Maustaste auf das aufgeführte **Microsoft Intune-Abonnement**, und klicken Sie anschließend auf **Löschen**.

3.   Klicken Sie im Assistenten auf **Microsoft Intune-Abonnement aus Configuration Manager entfernen**, klicken Sie auf **Weiter**, und klicken Sie anschließend erneut auf **Weiter**, um das Abonnement zu entfernen.


## <a name="how-to-remove-the-service-connection-point-role"></a>So entfernen Sie die Rolle „Dienstverbindungspunkt“

1.  Wechseln Sie zu **Verwaltung** > **Übersicht** > **-Standortkonfiguration** > **Server und Standortsystemrollen**.

2.  Wählen Sie den Server aus, auf dem die Rolle **Dienstverbindungspunkt** gehostet wird.

3.  Wählen Sie in der Liste **Standortsystemrollen** die Option **Dienstverbindungspunkt** aus, und klicken Sie anschließend im Menüband auf **Rolle entfernen**. Bestätigen Sie, dass Sie die Rolle entfernen möchten. Der Dienstverbindungspunkt wird gelöscht.

Sie können jetzt einen neuen Dienstverbindungspunkt erstellen, Configuration Manager ein neues Intune-Abonnement hinzufügen und Configuration Manager als MDM-Autorität festlegen.

## <a name="how-to-change-mdm-authority-to-intune"></a>So stellen Sie die MDM-Autorität auf Intune um

Ab Version 1610 können Sie die MDM-Autorität von Configuration Manager auf Intune ändern. Informationen zu dieser Funktion sind in Kürze verfügbar.

