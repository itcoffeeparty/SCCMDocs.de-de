---
title: Erstellen einer MDM-Sammlung unter Verwendung von System Center Configuration Manager | Microsoft-Dokumentation
description: Erstellen einer MDM-Sammlung unter Verwendung von System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 43316e4915b27aaeca563eaf52b51f053a839222
ms.sourcegitcommit: 974fbc4408028c8be28911e5cd646efcf47c7f15
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
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
