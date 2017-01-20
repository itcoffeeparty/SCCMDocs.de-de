---
title: "Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen | Microsoft-Dokumentation"
description: "Erstellen von Tasksequenzen, die nicht mit Systemen zur Betriebssystembereitstellung verknüpft sind, z.B. Verteilen von Software, Aktualisieren von Treibern, Bearbeiten von Benutzerzuständen, usw."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
caps.latest.revision: 6
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: ec146270ef39d48673ae6f3ca405b3f0bd7e8afa


---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Tasksequenzen in System Center Configuration Manager dienen zum Automatisieren einer Vielzahl von Aufgaben in Ihrer Umgebung. Diese Tasks wurden in erster Linie für die Bereitstellung von Betriebssystemen konzipiert und getestet.  Configuration Manager bietet viele weitere Features für den Einsatz als primäre Technologie in Szenarios wie [Anwendungsinstallation](../../apps/understand/introduction-to-application-management.md), [Installation von Softwareupdates](../../sum/understand/software-updates-introduction.md), [Konfiguration von Einstellungen](../../compliance/understand/ensure-device-compliance.md) oder benutzerdefinierte Automatisierung. Es gibt noch weitere Microsoft System Center-Automatisierungstechnologien wie [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) und [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) , die Sie auch in Erwägung ziehen sollten.  

 Die Stärke von Tasksequenzen liegt in ihrer Flexibilität. Sie können mit ihrer Hilfe Clienteinstellungen konfigurieren, Software verteilen, Treiber aktualisieren, Benutzerzustände bearbeiten und andere Tasks außerhalb der reinen Betriebssystembereitstellung ausführen. Sie können eine benutzerdefinierte Tasksequenz erstellen, der Sie beliebig viele Tasks hinzufügen können. Während die grundlegende Verwendung von benutzerdefinierten Tasksequenzen für die Bereitstellung von Betriebssystem unterstützt wird, besteht keine Möglichkeit zum Testen aller möglichen Konfigurationen. Je komplexer ihre Tasksequenzen werden, desto größer ist die Wahrscheinlichkeit, dass Probleme auftreten.  

 Die folgenden Schritte können in einer benutzerdefinierten Tasksequenz erfolgen, die nicht für die Betriebssystembereitstellung gedacht ist:  

-   [Bereitschaft überprüfen](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Verbindung mit Netzwerkordner herstellen](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Paketinhalt herunterladen](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Anwendung installieren](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Paket installieren](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Softwareupdates installieren](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Computer neu starten](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)  

-   [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [PowerShell-Skript ausführen](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Dynamische Variablen festlegen](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Tasksequenzvariable festlegen](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Nächste Schritte
[Deploy the task sequence (Bereitstellen der Tasksequenz)](manage-task-sequences-to-automate-tasks.md#a-namebkmkdeploytsa-deploy-a-task-sequence)



<!--HONumber=Dec16_HO3-->


