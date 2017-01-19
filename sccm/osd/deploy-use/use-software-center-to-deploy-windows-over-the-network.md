---
title: "Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk | Microsoft-Dokumentation"
description: "Sie können ein Betriebssystem im Softwarecenter bereitstellen, um einen vorhandenen Computer mit einer neuen Version von Windows zu aktualisieren oder ein Upgrade von Windows auf die neueste Version durchzuführen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 4c3ec20396da37d36f908af527f445a7a736e0ac


---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Tasksequenz zum Installieren eines Betriebssystems in System Center Configuration Manager kann über das Softwarecenter zur Verfügung gestellt werden. Sie können in den folgenden Betriebssystembereitstellungsszenarien ein Betriebssystem im Softwarecenter bereitstellen:  

-   [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Upgrade von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md)  

 Führen Sie die Schritte in einem der Betriebssystembereitstellungsszenarien aus, und verwenden Sie dann die folgenden Abschnitte, um die Bereitstellungen vorzubereiten, die im Softwarecenter verfügbar sind.  

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen  
 Wenn die Betriebssystembereitstellung im Softwarecenter verfügbar sein soll, müssen Sie die Bereitstellung konfigurieren, um das Betriebssystem Configuration Manager-Clients zur Verfügung zu stellen. Sie können dies auf der Seite der **Bereitstellungseinstellungen** des Assistenten oder der Registerkarte für die **Bereitstellungseinstellungen** in den Eigenschaften für die Bereitstellung konfigurieren.  Konfigurieren Sie für die Einstellung **Verfügbar machen für** entweder die Option **Nur Configuration Manager-Clients** oder **Configuration Manager-Clients, Medien und PXE**. Das Betriebssystem wird nach seiner Bereitstellung im Softwarecenter für Mitglieder der Zielsammlung angezeigt.  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> Bereitstellen der Tasksequenz für Computer  
 Stellen Sie das Betriebssystem für eine Zielsammlung bereit. Weitere Informationen finden Sie unter [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Beim Bereitstellen von Betriebssystemen für das Softwarecenter können Sie konfigurieren, ob die Bereitstellung erforderlich oder verfügbar ist.  

-   **Erforderliche Bereitstellung**: Bei erforderlichen Bereitstellungen wird das Betriebssystem im Softwarecenter zur Verfügung gestellt, aber es wird gemäß dem konfigurierten Zuweisungszeitplan automatisch gestartet.  

-   **Verfügbare Bereitstellung**: Das Betriebssystem ist im Softwarecenter verfügbar und kann vom Benutzer bei Bedarf installiert werden.  



<!--HONumber=Dec16_HO3-->


