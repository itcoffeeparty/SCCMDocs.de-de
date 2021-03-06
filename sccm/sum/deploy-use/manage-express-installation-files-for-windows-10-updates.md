---
title: Verwalten von Express-Installationsdateien für Windows 10-Updates
titleSuffix: Configuration Manager
description: Configuration Manager unterstützt Express-Installationsdateien für Windows 10, die kleinere Downloads und kürzere Installationszeiten für Clients bieten.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/24/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 4ca7a6c37137e266d719b76532b4131a6c43d4de
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Verwalten von Express-Installationsdateien für Windows 10-Updates
Configuration Manager unterstützt ab Version 1702 Express-Installationsdateien für Windows 10-Updates. Wenn Sie eine unterstützte Version von Windows 10 verwenden, können Sie die Configuration Manager-Clienteinstellungen nutzen, um den Client so zu konfigurieren, dass er nur die Änderungen zwischen dem kumulativen Update von Windows 10 des laufenden Monats und dem Update des Vormonats herunterlädt. Ohne Express-Installationsdateien laden Configuration Manager-Clients die kompletten kumulativen Updates für Windows 10 (einschließlich aller Updates aus den letzten Monaten) jeden Monat herunter. Mit Expressinstallationsdateien erhalten Sie kleinere Downloads und kürzere Installationszeiten.

> [!IMPORTANT]
> Während die Einstellungen zur Unterstützung der Verwendung von Express-Installationsdateien in der Version 1702 des Configuration Manager zur Verfügung stehen, ist die Clientunterstützung des Betriebssystems in Windows 10 Version 1607 mit einem Update des Windows Update-Agent verfügbar. Dieses Update ist in den Updates vom 11. April 2017 (Patch-Dienstag) enthalten. Weitere Informationen zu diesen Updates finden Sie im [Supportartikel 4015217](http://support.microsoft.com/kb/4015217). Zukünftige Updates werden Express für kleinere Downloads nutzen. Die Expressinstallationsdateien werden von älteren Versionen von Windows und von Windows 10 Version 1607 ohne Update nicht unterstützt.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates"></a>So aktivieren Sie den Download von Expressinstallationsdateien für Windows 10-Updates
Um mit der Synchronisierung der Metadaten für Windows 10-Expressinstallationsdatein zu beginnen, müssen Sie dies in den Punkteigenschaften des Software Updates aktivieren.
1.  Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**.
2.  Wählen Sie entweder den Standort der zentralen Verwaltung oder den eigenständigen primären Standort aus.
3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren**, und klicken Sie dann auf **Softwareupdatepunkt**. Wählen Sie auf der Registerkarte **Updatedateien** die Option **Download both full files for all approved updates and express installation files for Windows 10** (Die beiden vollständigen Dateien für alle genehmigten Windows 10-Expressinstallationsdateien herunterladen) aus.

> [!NOTE]    
> Sie können die Softwareupdatepunkt-Komponente nicht so konfigurieren, dass nur Express-Updates heruntergeladen werden.  Der Download der Express-Installationsdateien geschieht zusätzlich zum Download der vollständigen Dateien und erhöht somit die Menge an Inhalt, der an Verteilungspunkte verteilt und auf diesen gespeichert wird.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>So aktivieren Sie die Clientunterstützung für das Herunterladen und Installieren von Expressinstallationsdateien
Um die Unterstützung der Expressinstallationsdateien auf Clients zu aktivieren, müssen Sie die Expressinstallationsdateien im Abschnitt „Softwareupdates“ der Clienteinstellungen aktivieren. Dadurch wird ein neuer HTTP-Listener erstellt, der Anfragen zum Herunterladen von Expressinstallationsdateien auf den Port, den Sie angeben, abruft.

> [!NOTE]    
> Dies ist ein lokaler Port, auf dem Clients auf Anforderungen der Übermittlungsoptimierung (Delivery Optimization, DO) oder des Intelligenten Hintergrundübertragungsdiensts (Background Intelligent Transfer Service, BITS) lauschen, um Expressinhalte vom Verteilungspunkt herunterzuladen. Sie müssen diesen Port nicht in Firewalls öffnen, da sämtlicher Datenverkehr auf dem lokalen Computer erfolgt.

Sobald Sie die Clienteinstellungen zur Aktivierung dieser Funktionalität auf dem Client bereitstellen, wird diese versuchen, das Delta zwischen dem kumulativen Update von Windows 10 des aktuellen Monat und dem Update des Vormonats herunterzuladen (Clients müssen eine Version von Windows 10 ausführen, die Expressinstallationsdateien unterstützt).
1.  Aktivieren Sie „Expressinstallationsdateien unterstützten“ in den Komponenteneigenschaften des Softwareupdatepunks (vorheriger Vorgang).
2.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clienteinstellungen**.
3.  Wählen Sie die entsprechenden Clienteinstellungen aus, und klicken Sie dann in der Registerkarte **Home** auf **Eigenschaften**.
4.  Wählen Sie die Seite **Softwareupdates** aus, konfigurieren Sie **Ja** für die Einstellung **Installation von Express-Updates auf Clients aktivieren**, und konfigurieren Sie den Port, der für den HTTP-Listener auf dem Client für die Einstellung **Zum Herunterladen von Inhalt für Express-Updates verwendeter Port** verwendet wird.
