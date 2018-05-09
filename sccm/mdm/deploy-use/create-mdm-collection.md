---
title: Erstellen einer MDM-Sammlung
titleSuffix: Configuration Manager
description: Erstellen einer MDM-Sammlung unter Verwendung von System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d271499baf48364fe24a8961cae767c46d05a332
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Erstellen einer MDM-Sammlung mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Zum Angeben der Benutzer, die Geräte in der Verwaltung registrieren können, ist eine Configuration Manager-Benutzersammlung erforderlich. Es können nur Benutzersammlungen (keine Gerätesammlungen) verwendet werden, da Intune-Lizenzen nach Benutzer zugewiesen werden.

> [!NOTE]
> Zum Registrieren von Geräten mit Intune ist es nicht erforderlich, im Office 365-Portal oder im Azure Active Directory-Portal Benutzern Lizenzen zuzuweisen. Sie müssen lediglich die Benutzer in eine Sammlung einbinden, die (in einem [späteren Schritt](configure-intune-subscription.md)) dem Intune-Abonnement zugeordnet wird.

Sie können zu Testzwecken eine **Direktregel** einrichten und bestimmte Benutzer hinzufügen, die Geräte registrieren können. Wählen Sie in der Configuration Manager-Konsole die Option **Assets und Konformität** > **Benutzersammlungen** aus, klicken Sie auf der Registerkarte **Startseite** auf die Gruppe **Erstellen**, und klicken Sie dann auf **Benutzersammlung erstellen**. Verwenden Sie für eine größer angelegte Verteilung **Abfrageregeln**, um Benutzer zu definieren. Weitere Informationen zu Sammlungen finden Sie unter [Erstellen von Sammlungen](https://technet.microsoft.com/library/mt629371.aspx).

![Erstellen einer Benutzersammlung für MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
[Nächster Schritt >](confirm-dns.md)
