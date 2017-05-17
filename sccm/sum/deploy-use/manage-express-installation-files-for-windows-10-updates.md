---
title: "Verwalten von Express-Installationsdateien für Windows 10-Updates | Microsoft-Dokumentation"
description: "Configuration Manager unterstützt Express-Installationsdateien für Windows 10, die kleinere Downloads und kürzere Installationszeiten für Clients bieten."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.translationtype: Human Translation
ms.sourcegitcommit: d7b13f3dea5a3ae413ca6b8150ec24e1632a4d4d
ms.openlocfilehash: fcdcbcde61402b47871d51deba32d23867a78370
ms.contentlocale: de-de
ms.lasthandoff: 05/17/2017

---

## <a name="manage-express-installation-files-for-windows-10-updates"></a>Verwalten von Express-Installationsdateien für Windows 10-Updates
Configuration Manager unterstützt ab Version 1702 Express-Installationsdateien für Windows 10-Updates. Wenn Sie eine unterstützte Version von Windows 10 verwenden, können Sie die Configuration Manager-Einstellungen nutzen, um nur die Änderungen zwischen dem kumulativen Update von Windows 10 des laufenden Monats und dem Updates des Vormonats herunterzuladen. Ohne Express-Installationsdateien lädt Configuration Manager die kompletten kumulativen Updates für Windows 10 (einschließlich aller Updates aus den letzten Monaten) jeden Monat herunter. Mit Expressinstallationsdateien erhalten Sie kleinere Downloads und kürzere Installationszeiten.

> [!IMPORTANT]
> Während die Einstellungen zur Unterstützung der Verwendung von Express-Installationsdateien in der Version 1702 des Configuration Manager zur Verfügung stehen, ist die Clientunterstützung des Betriebssystems in Windows 10 Version 1607 mit einem Update des Windows Update-Agent verfügbar. Dieses Update ist in den Updates vom 11. April 2017 (Patch-Dienstag) enthalten. Weitere Informationen zu diesen Updates finden Sie im [Supportartikel 4015217](http://support.microsoft.com/kb/4015217). Zukünftige Updates werden Express für kleinere Downloads nutzen. Die Expressinstallationsdateien werden von älteren Versionen von Windows und von Windows 10 Version 1607 ohne Update nicht unterstützt.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>So aktivieren Sie den Download von Expressinstallationsdateien für Windows 10-Updates auf dem Server
Um mit der Synchronisierung der Metadaten für Windows 10-Expressinstallationsdatein zu beginnen, müssen Sie dies in den Punkteigenschaften des Software Updates aktivieren.
1.    Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**.
2.    Wählen Sie entweder den Standort der zentralen Verwaltung oder den eigenständigen primären Standort aus.
3.    Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren**, und klicken Sie dann auf **Softwareupdatepunkt**. Wählen Sie in der Registerkarte **Updatedateien** **Download full files for all approved updates and express installation files for Windows 10** (Vollständige Dateien für alle genehmigten Windows 10-Expressinstallationsdateien herunterladen) aus.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>So aktivieren Sie die Clientunterstützung für das Herunterladen und Installieren von Expressinstallationsdateien
Um die Unterstützung der Expressinstallationsdatein auf Clients zu aktivieren, müssen Sie die Expressinstallationsdateien auf Clients im Bereich Software Updates der Clienteinstellungen aktivieren. Dadurch wird ein neuer HTTP-Listener erstellt, der Anfragen zum Herunterladen von Expressinstallationsdateien auf den Port, den Sie angeben, abruft. Sobald Sie die Clienteinstellungen zur Aktivierung dieser Funktionalität auf dem Client bereitstellen, wird diese versuchen, das Delta zwischen dem kumulativen Update von Windows 10 des aktuellen Monat und dem Update des Vormonats herunterzuladen (Clients müssen eine Version von Windows 10 ausführen, die Espressinstallationsdateien unterstützt).
1.    Aktivieren Sie „Expressinstallationsdateien unterstützten“ in den Komponenteneigenschaften des Softwareupdatepunks (vorheriger Vorgang).
2.    Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clienteinstellungen**.
3.    Wählen Sie die entsprechenden Clienteinstellungen aus, und klicken Sie dann in der Registerkarte **Home** auf **Eigenschaften**.
4.    Wählen Sie die Seite **Softwareupdates** aus, konfigurieren Sie **Ja** für die Einstellung **Enable installation of Express Updates on clients** (Installation von Express-Updates auf Clients aktivieren), und konfigurieren Sie den Port, der für den HTTP-Listener auf dem Client für die Einstellung **Port used to download content for Express Updates** (Zum Herunterladen von Inhalt für Express-Updates verwendeter Port) verwendet wird.

