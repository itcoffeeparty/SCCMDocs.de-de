---
title: Vorbereiten der Softwareupdateverwaltung
titleSuffix: Configuration Manager
description: Um die Updateverwaltung vorzubereiten, müssen Sie diese Tasks durchführen, um Daten zur Bewertung der Konformität in der System Center Configuration Manager-Konsole anzuzeigen.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f2608d8cd46572a0fbcbafc6bc8c0f5e013356a2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-for-software-updates-management"></a>Vorbereiten der Softwareupdateverwaltung

*Gilt für: System Center Configuration Manager (Current Branch)*

Bevor Daten zur Bewertung der Kompatibilität von Softwareupdates in der System Center Configuration Manager-Konsole angezeigt werden, und bevor Sie Softwareupdates auf Clientcomputern bereitstellen können, müssen Sie die Schritte in den folgenden Abschnitten ausführen.

## <a name="step-1-install-a-software-update-point"></a>Schritt 1: Installieren eines Softwareupdatepunkts  
Der Softwareupdatepunkt ist am Standort der zentralen Verwaltung oder am eigenständigen primären Standort und an primären Standorten erforderlich, um die Bewertung der Kompatibilität von Softwareupdates und die Bereitstellung von Softwareupdates an Clients zu ermöglichen. An sekundären Standorten ist der Softwareupdatepunkt optional. Weitere Informationen finden Sie unter [Installieren eines Softwareupdatepunkts](install-a-software-update-point.md)  

## <a name="step-2-synchronize-software-updates"></a>Schritt 2: Synchronisieren von Softwareupdates
Bei der Softwareupdatesynchronisierung werden die Metadaten für Softwareupdates abgerufen, die die von Ihnen konfigurierten Kriterien erfüllen. Softwareupdates werden nicht in der Configuration Manager-Konsole angezeigt, bis Sie Softwareupdates synchronisieren. Mehr Informationen finden Sie unter [Synchronisieren von Softwareupdates](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Schritt 3: Konfigurieren zu synchronisierender Klassifizierungen und Produkte
Führen Sie diese Konfiguration am Standort der zentralen Verwaltung oder an einem eigenständigen primären Standort aus. Nachdem Sie zum ersten Mal Softwareupdates synchronisiert haben, ruft Configuration Manager eine aktualisierte Liste der Klassifizierungen und Produkte ab. Nun können Sie aus den neuen Optionen in den Komponenteneigenschaften von Softwareupdatepunkt auswählen. Nachdem Sie die neue Klassifizierungen und Produkte konfiguriert haben, wiederholen Sie Schritt 2, um die Synchronisierung von Softwareupdates zum Abrufen von Metadaten für Softwareupdates für die neuen Kriterien zu starten. Mehr Informationen finden Sie unter [Konfigurieren der zu synchronisierenden Klassifizierungen und Produkte](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Schritt 4: Verwalten von Einstellungen für Softwareupdates
Nach der Synchronisierung von Softwareupdates überprüfen Sie Configuration Manager-Clienteinstellungen, Konfigurationen für Gruppenrichtlinien und Softwareupdateeinstellungen, bevor Sie Softwareupdates bereitstellen. Weitere Informationen finden Sie unter [Verwalten von Einstellungen für Softwareupdates](manage-settings-for-software-updates.md).
