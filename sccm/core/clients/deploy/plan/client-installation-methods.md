---
title: Clientinstallationsmethoden
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu unterschiedlichen Installationsmethoden für den Configuration Manager-Client.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
caps.latest.revision: 9
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38f7d428149f4a4ac2b0bcb604031eca60a0fae5
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>Clientinstallationsmethoden in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können unterschiedliche Methoden verwenden, um Configuration Manager-Clientsoftware zu installieren. Dabei ist sowohl eine einzelne Methode als auch eine Kombination mehrerer Methoden denkbar. In diesem Artikel werden alle Methoden beschrieben, damit Sie die für Ihre Organstation geeignete auswählen können.  

## <a name="client-push-installation"></a>Clientpushinstallation  

**Unterstützte Clientplattform:** Windows  

#### <a name="advantages"></a>Vorteile  

-   Kann für die Installation des Clients auf einem einzelnen Computer, einer Sammlung von Computern oder den Ergebnissen einer Abfrage verwendet werden.  

-   Kann zum automatischen Installieren des Clients auf allen ermittelten Computern verwendet werden.  

-   Verwendet automatisch die Clientinstallationseigenschaften, die im Dialogfeld **Eigenschaften von Clientpushinstallation** auf der Registerkarte **Client** definiert sind.  

#### <a name="disadvantages"></a>Nachteile  

-   Kann beträchtlichen Netzwerkverkehr verursachen, wenn mithilfe von Push auf große Sammlungen übertragen wird.  

-   Kann nur auf Computern verwendet werden, die von Configuration Manager ermittelt wurden.  

-   Kann nicht verwendet werden, um Clients in einer Arbeitsgruppe zu installieren.  

-   Es muss ein Clientpushinstallationskonto angegeben werden, das über Administratorrechte für den betreffenden Clientcomputer verfügt.  

-   Für die Windows-Firewall müssen Ausnahmen auf den Clientcomputern konfiguriert werden.   

-   Sie können die Clientpushinstallation nicht abbrechen. Configuration Manager versucht, den Client auf allen ermittelten Ressourcen zu installieren. Bei Fehlern wird bis zu sieben Tage lang versucht, die Installation durchzuführen.  

Weitere Informationen finden Sie unter [Installieren von Clients mittels Clientpush](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).  



## <a name="software-update-point-based-installation"></a>Auf einem Softwareupdatepunkt basierende Installation  

**Unterstützte Clientplattform:** Windows  

#### <a name="advantages"></a>Vorteile  

-   Kann die vorhandene Softwareupdateinfrastruktur für die Verwaltung der Clientsoftware verwenden.  

-   Wenn WSUS (Windows Server Update Services) und Gruppenrichtlinieneinstellungen in Active Directory Domain Services ordnungsgemäß konfiguriert sind, kann die Clientsoftware automatisch auf neuen Computern installiert werden.  

-   Keine Ermittlung von Computern für die Installation des Clients erforderlich.  

-   Clientinstallationseigenschaften, die in Active Directory-Domänendienste veröffentlicht wurden, können von Computern gelesen werden.  

-   Wenn der Client entfernt wird, wird er durch diese Methode erneut installiert.  

-   Keine Konfiguration oder Wartung eines Installationskontos für den betreffenden Clientcomputer erforderlich.  

#### <a name="disadvantages"></a>Nachteile  

-   Erfordert eine funktionsfähige Softwareupdateinfrastruktur als Voraussetzung.  

-   Für die Clientinstallation und für Softwareupdates muss derselbe Server verwendet werden. Dieser Server muss sich an einem primären Standort befinden.  

-   Sie müssen ein Gruppenrichtlinienobjekt in Active Directory Domain Services mit dem aktiven Softwareupdatepunkt des Clients und dem Port konfigurieren, um neue Clients zu installieren.  

-   Wenn das Active Directory-Schema nicht für Configuration Manager erweitert wurde, müssen Sie Gruppenrichtlinieneinstellungen zur Bereitstellung von Computern mit Clientinstallationseigenschaften verwenden.  

Weitere Informationen finden Sie unter [How to install clients with software update-based installation (Installieren von Clients mithilfe einer auf einem Softwareupdate basierenden Installation)](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP).  



## <a name="group-policy-installation"></a>Gruppenrichtlinieninstallation  

**Unterstützte Clientplattform:** Windows  

#### <a name="advantages"></a>Vorteile  

-   Keine Ermittlung von Computern für die Installation des Clients erforderlich.  

-   Kann für neue Clientinstallationen oder für Aktualisierungen verwendet werden.  

-   Clientinstallationseigenschaften, die in Active Directory-Domänendienste veröffentlicht wurden, können von Computern gelesen werden.  

-   Keine Konfiguration oder Wartung eines Installationskontos für den betreffenden Clientcomputer erforderlich.  

#### <a name="disadvantages"></a>Nachteile  

-   Wenn eine große Anzahl von Clients installiert wird, kann dies beträchtlichen Netzwerkdatenverkehr verursachen.  

-   Wenn das Active Directory-Schema nicht für Configuration Manager erweitert wurde, müssen Sie die Clientinstallationseigenschaften mithilfe von Gruppenrichtlinieneinstellungen den Computern des Standorts hinzufügen.  

Weitere Informationen finden Sie unter [Installieren von Clients mit einer Gruppenrichtlinie](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientGP).  



## <a name="logon-script-installation"></a>Anmeldeskriptinstallation  

**Unterstützte Clientplattform:** Windows  

#### <a name="advantages"></a>Vorteile  

-   Keine Ermittlung von Computern für die Installation des Clients erforderlich.  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

#### <a name="disadvantages"></a>Nachteile  

-   Wenn in kurzer Zeit eine große Anzahl von Clients installiert wird, kann dies beträchtlichen Netzwerkdatenverkehr verursachen.  

-   Wenn Benutzer sich nicht regelmäßig beim Netzwerk anmelden, kann die Installation auf allen Clientcomputern sehr lange dauern.  

Weitere Informationen finden Sie unter [Installieren von Clients mithilfe von Anmeldeskripts](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientLogonScript).  



## <a name="manual-installation"></a>Manuelle Installation  

**Unterstützte Clientplattformen:** Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Vorteile  

-   Keine Ermittlung von Computern für die Installation des Clients erforderlich.  

-   Kann zu Testzwecken verwendet werden.  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

#### <a name="disadvantages"></a>Nachteile  

-   Keine Automatisierung, daher zeitaufwändig.  

Weitere Informationen zum manuellen Installieren des Clients auf unterschiedlichen Plattformen finden in den folgenden Artikeln:  

-   [Bereitstellen von Clients auf Windows-Computern](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)  

-   [Bereitstellen von Clients auf UNIX- und Linux-Servern](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)  

-   [Bereitstellen von Clients auf Macintosh-Computern](/sccm/core/clients/deploy/deploy-clients-to-macs)  



## <a name="microsoft-intune-mdm-installation"></a>Installation von Microsoft Intune-MDM

**Unterstützte Clientplattform:** Windows 10

#### <a name="advantages"></a>Vorteile  

-   Keine Ermittlung von Computern für die Installation des Clients erforderlich.  

-   Keine Konfiguration oder Wartung eines Installationskontos für den betreffenden Clientcomputer erforderlich.  

-   Authentifizierung mit Azure Active Directory ist möglich.  

-   Computer im Internet können installiert und zugewiesen werden.  

-   Automatische Verwendung mit Windows Autopilot und Microsoft Intune für die Co-Verwaltung möglich.  

#### <a name="disadvantages"></a>Nachteile  

-   Zusätzliche Technologien, die nicht in Configuration Manager verfügbar sind, sind erforderlich.  

-   Ein Gerät muss auch dann auf das Internet zugreifen können, wenn es nicht internetbasiert ist.  

Weitere Informationen finden Sie in den folgenden Artikeln:  

-   [Installieren von Clients für mit Intune MDM verwaltete Windows-Geräte](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#bkmk_mdm)  

-   [Installieren und Zuweisen von Windows 10-Clients in Configuration Manager mit Authentifizierung über Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

