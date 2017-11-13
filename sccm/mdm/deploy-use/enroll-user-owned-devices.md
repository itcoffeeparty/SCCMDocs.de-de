---
title: "Registrieren von Benutzergeräten für Hybridbereitstellungen"
titleSuffix: Configuration Manager
description: "Erfahren Sie mehr über verschiedene Methoden für die Registrierung von Benutzergeräten für Hybridbereitstellungen mit Configuration Manager."
ms.custom: na
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
caps.latest.revision: "13"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9bc0e23680ff2c7a5099938e546e50e03f998f5e
ms.sourcegitcommit: 1132886e07d0c0a87dcc7eeef4577dd8d8840023
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2017
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Registrieren von Benutzergeräten für Hybridbereitstellungen mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Benutzereigene Geräte können durch Registrierung in die Verwaltung aufgenommen werden. Dieser Prozess wird oft als „Bring Your Own Devices“ oder einfach als „BYOD“ bezeichnet. Benutzer können dazu die Unternehmensportal-App installieren und auf dem Gerät anmelden (iOS, macOS und Android) oder ein Geschäfts- oder Schulkonto zum Gerät hinzufügen und mit einer Domäne verknüpfen (Windows). Durch diesen Prozess wird das Gerät bei Intune registriert, wodurch der Benutzer Zugriff auf die von Intune verwalteten Ressourcen erhält. Außerdem kann Intune dadurch bestimmte Geräteeinstellungen verwalten, zum Beispiel das Anfordern einer PIN.

Sie müssen zunächst als Administrator die [mobile Geräteverwaltung einrichten](setup-hybrid-mdm.md) und die [Registrierung aktivieren](enable-platform-enrollment.md), um Geräte in die Verwaltung aufzunehmen. Sobald die Registrierung aktiviert ist, kann der Benutzer eigene Geräte registrieren. Weitere Überlegungen und Schritte, die Sie für Ihre Benutzer freigeben können, finden Sie unter [How to educate your end users about Microsoft Intune (Informieren der Endbenutzer über Microsoft Intune)](https://docs.microsoft.com/intune/end-user-educate).

Unternehmen oder Schulen, die Geräte erwerben, können von Programmen profitieren, mit denen Sie [unternehmenseigene Geräte verwalten](enroll-company-owned-devices.md) können.
