---
title: Dienstfenster
titleSuffix: Configuration Manager
description: Verwenden Sie Dienstfenster, um den Zeitpunkt von Updateinstallationen für System Center Configuration Manager-Standorte zu steuern.
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 8b81efc7f31339bd7b19530ef603855f0ee8fad6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
#  <a name="service-windows-for-site-servers"></a>Dienstfenster für Standortserver

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können Dienstfenster an Standorten der zentralen Verwaltung und primären Standorten konfigurieren, um den Installationszeitpunkt von konsoleninternen Updates zu steuern.  Sie können mehrere Fenster konfigurieren. Dabei wird das für die Installation zugelassene Fenster von einer Kombination aller Dienstfenster für diesen Standortserver bestimmt.

Wenn kein Dienstfenster konfiguriert ist:
- **Für den Standort der obersten Ebene** (ein Standort der zentralen Verwaltung oder ein eigenständiger primärer Standort) entscheiden Sie, wann die Updateinstallation gestartet werden soll.
- **An untergeordneten primären Standorten** wird das Update automatisch installiert, sobald die Installation des Updates am Standort der zentralen Verwaltung abgeschlossen ist.
- **An einem sekundären Standort** werden Updates nicht automatisch gestartet. Dort müssen Sie die Updateinstallation manuell aus der Konsole starten, nachdem das Update am übergeordneten primären Standort installiert wurde.

Wenn ein Dienstfenster konfiguriert ist:
- **An Ihrem Standort der obersten Ebene** können Sie die Installation von neuen Updates nicht von der Configuration Manager-Konsole aus starten. Selbst bei konfigurierten Dienstfenstern werden am Standort automatisch Updates heruntergeladen, damit sie bereit für die Installation sind.  
- **An einem untergeordneten primären Standort** werden Updates, die am Standort der zentralen Verwaltung installiert wurden, zwar am primären Standort herunterladen, aber nicht automatisch gestartet. Sie können die Installation eines Updates nicht während eines Zeitraums manuell starten, der durch ein Dienstfenster blockiert ist. Wenn die Updateinstallation nicht mehr von einem Dienstfenster blockiert wird, wird die Installation des Updates automatisch gestartet.
- **An sekundären Standorten** werden Dienstfenster und die automatische Installation von Updates nicht unterstützt. Nachdem am übergeordneten primären Standort eines sekundären Standorts ein Update installiert wurde, können Sie das Update des sekundären Standorts aus der Konsole starten.

## <a name="to-configure-a-service-window"></a>Konfigurieren eines Dienstfensters

1.  Öffnen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie anschließend den Standort aus, für den Sie ein Dienstfenster konfigurieren möchten.  

2.  Als Nächstes bearbeiten Sie die **Eigenschaften** der Standortserver und wählen die Registerkarte **Dienstfenster** aus, auf der Sie mindestens ein Dienstfenster für den jeweiligen Standortserver festlegen können.  
