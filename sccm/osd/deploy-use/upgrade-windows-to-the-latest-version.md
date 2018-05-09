---
title: Upgrade auf Windows 10
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über das Verwenden von Configuration Manager, um ein Upgrade von Windows 7 oder höher auf Windows 10 durchzuführen.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbba0306cececebeb7a0e20757e7de3b0d4d0e70
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Aktualisieren von Windows auf die neueste Version mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Artikel erhalten Sie Informationen zu den Schritten, die Sie in Configuration Manager durchführen müssen, um das Betriebssystems Ihres Computers zu upgraden. Sie können aus unterschiedlichen Bereitstellungsmethoden auswählen, z. B. eigenständige Medien oder Softwarecenter. Durch das direkte Upgrade wird Folgendes durchgeführt:  

-   Das Betriebssystem wird auf Computern mit den folgenden Betriebssystemen aktualisiert:
    - Windows 7, Windows 8 oder Windows 8.1. Sie können auch Upgrades von Windows 10-Build zu Windows 10-Build durchführen. Beispielsweise können Sie Windows 10 Version 1607 auf Windows 10 Version 1709 aktualisieren.  
    
    - Windows Server 2012. Sie können auch Build-zu-Build-Upgrades von Windows 2016 durchführen. Weitere Informationen zu den unterstützten Upgradepfaden finden Sie unter [Unterstützte Upgradepfade](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016).    

-   Behält die Anwendungen, Einstellungen und Benutzerdaten auf dem Computer bei.  

-   Weist keine externen Abhängigkeiten auf, wie z. B. das Windows ADK.  

-   Das Upgrade ist schneller und stabiler als herkömmliche Betriebssystembereitstellungen.  


> [!Note]  
> Ab Version 1802 unterstützt die Tasksequenz für das direkte Upgrade von Windows 10 die Bereitstellung auf internetbasierten Clients über das [Cloud Management Gateway](/sccm/core/clients/manage/plan-cloud-management-gateway). Mit dieser Funktion können Remotebenutzer einfacher ein Upgrade auf Windows 10 durchführen, ohne eine Verbindung mit dem Intranet herstellen zu müssen. Weitere Informationen finden Sie unter [Bereitstellen eines direkten Upgrades für Windows 10 über das CMG](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->



##  <a name="BKMK_Plan"></a> Plan  

### <a name="task-sequence-requirements-and-limitations"></a>Anforderungen und Einschränkungen der Tasksequenz

Überprüfen Sie die folgenden, für die Tasksequenz zum Durchführen eines Betriebssystemupgrades geltenden Anforderungen und Einschränkungen, und stellen Sie sicher, dass die Tasksequenz Ihren Anforderungen entspricht:  

  -   Führen Sie nur zusätzliche Tasksequenzschritte aus, wenn diese für das Upgrade des Betriebssystems relevant sind. Zu derartigen Schritten gehört u.a. das Installieren von Paketen, Anwendung und Updates. Führen Sie außerdem Schritte durch, in denen die Befehlszeilen oder PowerShell ausgeführt oder dynamische Variablen festgelegt werden.  

  -   Überprüfen Sie vor dem Bereitstellen der Upgradetasksequenz die auf den Computern installierten Treiber und Anwendungen, um sicherzustellen, dass sie mit Windows 10 kompatibel sind.  

  -   Die folgenden Tasks sind mit einem direkten Upgrade nicht möglich. Dafür müssen Sie herkömmliche Betriebssystembereitstellungen verwenden:  

     -   Ändern der Domänenmitgliedschaft des Computers oder Aktualisieren der lokalen Administratorengruppe.  

     -   Implementieren einer grundlegenden Änderung auf Ihrem Computer. Das kann z.B. Folgendes sein: 
         - Ändern der Datenträgerpartitionen
         - Ändern der Systemarchitektur von x86 in x64
         - Implementieren von UEFI. (Weitere Informationen zu einer anderen Möglichkeit finden Sie unter [Convert from BIOS to UEFI during an in-place upgrade (Wechsel von BIOS zu UEFI während eines direkten Upgrades)](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).)
         - Anpassen der Standardbetriebssystemsprache  

     -   Es gibt benutzerdefinierte Anforderungen, z.B. die Verwendung eines benutzerdefinierten Basisimages mit Festplattenverschlüsselung eines Drittanbieters oder das Durchführen von WinPE-Offlinevorgängen.  

### <a name="infrastructure-requirements"></a>Anforderungen an die Infrastruktur  

Die einzige Voraussetzung für ein Upgrade ist die Verfügbarkeit eines Verteilungspunkts. Verteilen Sie das Betriebssystemupgradepaket und alle anderen Pakete, die in der Tasksequenz beinhaltet sind. Weitere Informationen finden Sie unter [Installieren oder Modifizieren eines Verteilungspunkts](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).



##  <a name="BKMK_Configure"></a> Konfigurieren  

### <a name="prepare-the-os-upgrade-package"></a>Vorbereiten des Betriebssystemupgradepakets  

  Das Windows 10-Upgradepaket enthält die erforderlichen Quelldateien zum Aktualisieren des Betriebssystems auf dem Zielcomputer. Das Upgradepaket muss die gleiche Edition, Architektur und Sprache wie die Clients aufweisen, die aktualisiert werden sollen. Weitere Informationen finden Sie unter [Manage operating system upgrade packages (Verwalten von Betriebssystem-Upgradepaketen)](../get-started/manage-operating-system-upgrade-packages.md).  


### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades  

  Verwenden Sie die Schritte unter [Create a task sequence to upgrade an operating system (Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades)](create-a-task-sequence-to-upgrade-an-operating-system.md), um das Upgrade des Betriebssystems zu automatisieren.  

   > [!NOTE]  
   > Durch die Schritte unter [Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades](create-a-task-sequence-to-upgrade-an-operating-system.md) wird eine Tasksequenz erstellt, mit der das Upgrade eines Betriebssystems auf Windows 10 durchgeführt wird. Die Tasksequenz enthält den Schritt „Betriebssystem aktualisieren“ sowie weitere empfohlene Schritte und Gruppen für den End-to-End-Aktualisierungsprozess. Sie können jedoch eine benutzerdefinierte Tasksequenz erstellen und den Tasksequenzschritt [Betriebssystem aktualisieren](../understand/task-sequence-steps.md#BKMK_UpgradeOS) zum Aktualisieren des Betriebssystems hinzufügen. Dieser Schritt ist der einzige erforderliche Schritt für das Betriebssystemupgrade auf Windows 10. Wenn Sie diese Methode auswählen, fügen Sie nach dem Schritt „Betriebssystem aktualisieren“ außerdem den Schritt [Computer neu starten](../understand/task-sequence-steps.md#BKMK_RestartComputer) hinzu, um das Upgrade abzuschließen. Stellen Sie sicher, dass die Einstellung **Aktuell installiertes Standardbetriebssystem** aktiviert ist, um den Computer mit dem installierten Betriebssystem und nicht mit Windows PE neu zu starten.  



##  <a name="BKMK_Deploy"></a> Bereitstellen  

Verwenden Sie eine der folgenden Bereitstellungsmethoden, um das Betriebssystem bereitzustellen:  

  -   [Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk](use-software-center-to-deploy-windows-over-the-network.md)  

  -   [Use stand-alone media to deploy Windows without using the network (Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks)](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

      > [!IMPORTANT]  
      > Wenn Sie eigenständige Medien verwenden, müssen Sie ein Startimage in die Tasksequenz einschließen, damit die Medien im Tasksequenzmedien-Assistenten zur Verfügung stehen.




## <a name="monitor"></a>Monitor  

Weitere Informationen zum Überwachen der Tasksequenzbereitstellung zum Durchführen eines Betriebssystemupgrades finden Sie unter [Überwachen von Betriebssystembereitstellungen](monitor-operating-system-deployments.md).  
