---
title: Aktualisieren von Windows auf die neueste Version | Microsoft-Dokumentation
description: "Erfahren Sie mehr über das Verwenden von Configuration Manager, um ein Upgrade eines Betriebssystems von Windows 7 oder höher auf Windows 10 durchzuführen."
ms.custom: na
ms.date: 02/06/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: 13
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 288a4c649f371d9701fe7249449356aa222bf372
ms.openlocfilehash: 35f04e237efffbdb12893f658950a99dc0b98b85
ms.contentlocale: de-de
ms.lasthandoff: 05/17/2017


---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Aktualisieren von Windows auf die neueste Version mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält die Schritte in System Center Configuration Manager zum Durchführen eines Upgrades eines Betriebssystems auf einem Computer von Windows 7 oder höher auf Windows 10. Sie können aus unterschiedlichen Bereitstellungsmethoden auswählen, z. B. eigenständige Medien oder Softwarecenter. Szenario für das direkte Windows 10-Upgrade:  

-   Aktualisiert das Betriebssystem auf Computern, auf denen derzeit Windows 7, Windows 8 oder Windows 8.1 durchgeführt wird. Sie können auch Upgrades von Windows 10-Build zu Windows 10-Build durchführen. Beispielsweise können Sie Windows 10 RTM auf Windows 10, Version 1511, aktualisieren.  

-   Behält die Anwendungen, Einstellungen und Benutzerdaten auf dem Computer bei.  

-   Weist keine externen Abhängigkeiten auf, wie z. B. das Windows ADK.  

-   Ist im Allgemeinen schneller und stabiler als herkömmliche Betriebssystembereitstellungen.  

 Nutzen Sie die folgenden Abschnitte, um mithilfe einer Tasksequenz Betriebssysteme über das Netzwerk bereitzustellen.  

##  <a name="BKMK_Plan"></a> Plan  

-   **Überprüfen Sie die für die Tasksequenz zum Durchführen eines Betriebssystemupgrades geltenden Einschränkungen.**  

     Überprüfen Sie die folgenden, für die Tasksequenz zum Durchführen eines Betriebssystemupgrades geltenden Anforderungen und Einschränkungen, und stellen Sie sicher, dass die Tasksequenz Ihren Anforderungen entspricht:  

    -   Fügen Sie nur Tasksequenzschritte hinzu, die sich auf die Kernaufgaben der Betriebssystembereitstellung und der Konfiguration der Computer nach der Installation des Images beziehen. Dazu zählen Schritte, die Pakete, Anwendungen oder Updates installieren, und Schritte, die Befehlszeilen oder PowerShell ausführen bzw. dynamische Variablen festlegen.  

    -   Überprüfen Sie vor dem Bereitstellen der Upgradetasksequenz die auf den Computern installierten Treiber und Anwendungen, um sicherzustellen, dass sie mit Windows 10 kompatibel sind.  

    -   Die folgenden Tasks sind mit dem direkten Upgrade nicht kompatibel und erfordern herkömmliche Betriebssystembereitstellungen:  

        -   Ändern der Domänenmitgliedschaft der Computer oder Aktualisieren lokaler Administratoren.  

        -   Implementieren einer grundlegenden Änderung auf dem Computer, z. B. die Datenträgerpartitionierung, einen Architekturwechsel von x86 zu x64, die Implementierung von UEFI oder das Ändern der Sprache des zugrunde liegenden Betriebssystems.  

        -   Sie haben benutzerdefinierte Anforderungen, z.B. die Verwendung eines benutzerdefinierten Basisimages mit Festplattenverschlüsselung eines <sup>Drittanbieters</sup>, oder müssen WinPE-Offlinevorgänge durchführen.  

-   **Planen und Implementieren von Anforderungen an die Infrastruktur**  

     Die einzige Voraussetzung für das Upgradeszenario ist, dass ein Verteilungspunkt für das Betriebssystem-Upgradepaket und alle anderen in der Tasksequenz enthaltenen Pakete verfügbar ist. Weitere Informationen finden Sie unter [Install or modify a distribution point (Installieren oder Modifizieren eines Verwaltungspunkts)](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

##  <a name="BKMK_Configure"></a> Konfigurieren  

1.  **Vorbereiten des Betriebssystem-Upgradepakets**  

     Das Windows 10-Upgradepaket enthält die erforderlichen Quelldateien zum Aktualisieren des Betriebssystems auf dem Zielcomputer. Das Upgradepaket muss die gleiche Edition, Architektur und Sprache wie die Clients aufweisen, die aktualisiert werden sollen.  Weitere Informationen finden Sie unter [Manage operating system upgrade packages (Verwalten von Betriebssystem-Upgradepaketen)](../get-started/manage-operating-system-upgrade-packages.md).  

2.  **Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades**  

     Verwenden Sie die Schritte unter [Create a task sequence to upgrade an operating system (Erstellen einer Tasksequenz zum Aktualisieren eines Betriebssystems)](create-a-task-sequence-to-upgrade-an-operating-system.md), um das Durchführen eines Upgrades des Betriebssystems zu automatisieren.  

    > [WICHTIG] Wenn Sie eigenständige Medien verwenden, müssen Sie ein Startimage in die Tasksequenz einschließen, damit sie im Tasksequenzmedien-Assistenten zur Verfügung stehen.


    > [!NOTE]  
    >  In der Regel verwenden Sie die Schritte unter [Create a task sequence to upgrade an operating system (Erstellen einer Tasksequenz zum Aktualisieren eines Betriebssystems)](create-a-task-sequence-to-upgrade-an-operating-system.md), um eine Tasksequenz zu erstellen, um ein Upgrade eines Betriebssystems auf Windows 10 durchzuführen. Die Tasksequenz enthält den Schritt „Betriebssystem aktualisieren“ sowie weitere empfohlene Schritte und Gruppen für den End-to-End-Aktualisierungsprozess. Sie können jedoch eine benutzerdefinierte Tasksequenz erstellen und den Tasksequenzschritt [Betriebssystem aktualisieren](../understand/task-sequence-steps.md#BKMK_UpgradeOS) zum Aktualisieren des Betriebssystems hinzufügen. Dies ist der einzige Schritt, der zum Aktualisieren des Betriebssystems auf Windows 10 erforderlich ist. Wenn Sie diese Methode auswählen, fügen Sie nach dem Schritt „Betriebssystem aktualisieren“ außerdem den Schritt [Computer neu starten](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer) hinzu, um das Upgrade abzuschließen. Stellen Sie sicher, dass die Einstellung **Aktuell installiertes Standardbetriebssystem** aktiviert ist, um den Computer mit dem installierten Betriebssystem und nicht mit Windows PE neu zu starten.  

##  <a name="BKMK_Deploy"></a> Bereitstellen  

-   Verwenden Sie eine der folgenden Bereitstellungsmethoden, um das Betriebssystem bereitzustellen:  

    -   [Use Software Center to deploy Windows over the network (Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk)](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Use stand-alone media to deploy Windows without using the network (Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks)](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Überwachen der Tasksequenzbereitstellung**  

     Weitere Informationen zum Überwachen der Tasksequenzbereitstellung zum Durchführen eines Upgrade des Betriebssystems finden Sie unter [Monitor operating system deployments (Überwachen von Betriebssystembereitstellungen)](monitor-operating-system-deployments.md).  

