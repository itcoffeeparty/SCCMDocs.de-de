---
title: Aktivieren von Lookout MTP in Intune
titleSuffix: Configuration Manager
description: Aktivieren von Lookout Mobile Threat Protection in der Intune-Verwaltungskonsole.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
caps.latest.revision: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2d4cdb20f66864ac9bf79b89189e97fab26b34f3
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/12/2017
---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>Aktivieren von Lookout MTP in der Intune-Verwaltungskonsole

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema zeigt Ihnen, wie Sie die Lookout MTP-Verbindung in Intune aktivieren können. Sie sollten den Intune Connector bereits in der Lookout-Konsole konfiguriert haben, bevor Sie diesen Schritt ausführen.  Wenn nicht bereits geschehen, führen Sie die Schritte unter [Set up your subscription with Lookout mobile threat protection (Einrichten Ihres Abonnements für den Lookout-Schutz vor Bedrohungen für mobile Geräte)](set-up-your-subscription-with-lookout.md) aus.

Zur Aktivierung der Lookout-MTP-Verbindung in Intune wählen Sie auf der Seite **Verwaltung** in der [Microsoft Intune-Administratorkonsole](https://manage.microsoft.com) **Drittanbieterintegration** aus. Wählen Sie **Lookout-Status** und **Synchronisierung mit MTP** mithilfe der Umschaltfläche aus.

![Screenshot der Lookout-Synchronisationsseite mit hervorgehobener Umschaltfläche](media/lookout-intune-synchronization.png)

Damit ist die Einrichtung der Lookout- und Intune-Integration in der Intune-Administratorkonsole abgeschlossen.  Die nächsten Schritte zur Implementierung dieser Lösung beinhalten die Bereitstellung der [Lookout for Work-Apps](configure-and-deploy-lookout-for-work-apps.md) und Einrichten der [Konformitätsrichtlinie](enable-device-threat-protection-rule-compliance-policy.md).

>[!IMPORTANT]
> Sie **müssen** die Lookout for Work-App konfigurieren, bevor Sie Konformitätsrichtlinienregeln erstellen und den bedingten Zugriff konfigurieren. Dadurch wird sichergestellt, dass die App für die Endbenutzer bereitsteht und verfügbar ist, bevor sie Zugriff auf E-Mails oder andere Unternehmensressourcen erhalten.

## <a name="next-steps"></a>Nächste Schritte
[Konfigurieren der Lookout for Work-App](configure-and-deploy-lookout-for-work-apps.md)
