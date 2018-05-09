---
title: Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk
titleSuffix: Configuration Manager
description: Sie können ein Betriebssystem im Softwarecenter bereitstellen, um einen vorhandenen Computer mit einer neuen Version von Windows zu aktualisieren oder ein Upgrade von Windows auf die neueste Version durchzuführen.
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fd4853a35c4bfa1112e61286add1e1f458e8b6f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können die Tasksequenz zum Installieren eines Betriebssystems in System Center Configuration Manager im Softwarecenter zur Verfügung stellen. Sie können in den folgenden Szenarien für die Betriebssystembereitstellung ein Betriebssystem im Softwarecenter bereitstellen:

-   [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Upgrade von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md)

Führen Sie die Schritte in einem der Szenarien für die Betriebssystembereitstellung aus. Befolgen Sie dann die Anweisungen in den folgenden Abschnitten, um die Bereitstellungen vorzubereiten, die im Softwarecenter verfügbar sind.

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen  
Konfigurieren Sie die Bereitstellung, um die Betriebssystembereitstellung im Softwarecenter verfügbar zu machen. Sie können die Bereitstellung auf der Seite **Bereitstellungseinstellungen** im Assistenten zum Bereitstellen von Software oder auf der Registerkarte **Bereitstellungseinstellungen** in den Eigenschaften der Bereitstellung konfigurieren. Konfigurieren Sie für die Einstellung **Verfügbar machen für** entweder die Option **Nur Configuration Manager-Clients** oder **Configuration Manager-Clients, Medien und PXE**. Das Betriebssystem wird nach seiner Bereitstellung durch das System im Softwarecenter für Mitglieder der Zielsammlung angezeigt.

##  <a name="BKMK_Deploy"></a> Bereitstellen der Tasksequenz für Computer  
Stellen Sie das Betriebssystem für eine Zielsammlung bereit. Weitere Informationen finden Sie unter [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Beim Bereitstellen von Betriebssystemen für das Softwarecenter können Sie konfigurieren, ob die Bereitstellung erforderlich oder verfügbar ist.

-   **Erforderliche Bereitstellung**: Bei erforderlichen Bereitstellungen wird das Betriebssystem im Softwarecenter zur Verfügung gestellt, aber es wird gemäß dem konfigurierten Zuweisungszeitplan automatisch gestartet.

-   **Verfügbare Bereitstellung**: Das Betriebssystem ist im Softwarecenter verfügbar und kann vom Benutzer bei Bedarf installiert werden.
