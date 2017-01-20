---
title: Clientinstallationsmethoden | System Center Configuration Manager
description: "Erfahren Sie mehr über Clientinstallationsmethoden für System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 169e7871bc1fbc83964ecb17e277d64ce4fd472c


---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>Clientinstallationsmethoden in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Es gibt verschiedene Methoden zur Installation der Clientsoftware von System Center Configuration Manager auf Windows-Geräten, UNIX- und Linux-Servern sowie Macintosh-Computern in Ihrem Unternehmen. Sie können je nach Anforderungen eine Methode oder eine beliebige Kombination dieser Methoden verwenden.  

 In den folgenden Abschnitten werden die Vor- und Nachteile der einzelnen Clientinstallationsmethoden aufgeführt, um Ihnen die Auswahl der für Ihre Organisation am besten geeigneten Methode zu erleichtern.  

## <a name="client-push-installation"></a>Clientpushinstallation  

 **Unterstützte Clientplattformen:** Windows  

 **Vorteile**  

-   Kann für die Installation des Clients auf einem einzelnen Computer, einer Sammlung von Computern oder den Ergebnissen einer Abfrage verwendet werden.  

-   Kann zum automatischen Installieren des Clients auf allen ermittelten Computern verwendet werden.  

-   Verwendet automatisch die Clientinstallationseigenschaften, die im Dialogfeld **Eigenschaften von Clientpushinstallation** auf der Registerkarte **Client** definiert sind.  

 **Nachteile**  

-   Kann beträchtlichen Netzwerkverkehr verursachen, wenn mithilfe von Push auf große Sammlungen übertragen wird.  

-   Kann nur auf Computern verwendet werden, die von Configuration Manager ermittelt wurden.  

-   Kann nicht verwendet werden, um Clients in einer Arbeitsgruppe zu installieren.  

-   Es muss ein Clientpushinstallationskonto angegeben werden, das über Administratorrechte für den betreffenden Clientcomputer verfügt.  

-   Die Windows-Firewall muss auf Clientcomputern mit Ausnahmeregeln konfiguriert sein, damit die Clientpushinstallation abgeschlossen werden kann.  

-   Sie können die Clientpushinstallation nicht abbrechen. Wenn Sie diese Clientinstallationsmethode für einen Standort verwenden, wird die Ausführung der Installation des Clients von Configuration Manager auf allen ermittelten Ressourcen versucht und beim Auftreten von Fehlern bis zu sieben Tage lang wiederholt.  

 Weitere Informationen zu dieser Installationsmethode finden Sie unter [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="software-update-point-based-installation"></a>Auf einem Softwareupdatepunkt basierende Installation  
 **Unterstützte Clientplattformen:** Windows  

 **Vorteile:**  

-   Kann die vorhandene Softwareupdateinfrastruktur für die Verwaltung der Clientsoftware verwenden.  

-   Kann automatisch die Clientsoftware auf neuen Computern installieren, wenn WSUS (Windows Server Update Services) und Gruppenrichtlinieneinstellungen in Active Directory-Domänendienste ordnungsgemäß konfiguriert sind.  

-   Erfordert keine Ermittlung von Computern als Voraussetzung für die Installation des Clients.  

-   Clientinstallationseigenschaften, die in Active Directory-Domänendienste veröffentlicht wurden, können von Computern gelesen werden.  

-   Installiert die Clientsoftware erneut, wenn sie entfernt wurde.  

-   Erfordert keine Konfiguration oder Wartung eines Installationskontos für den betreffenden Clientcomputer.  

 **Nachteile:**  

-   Erfordert eine funktionsfähige Softwareupdateinfrastruktur als Voraussetzung.  

-   Muss denselben Server für die Clientinstallation und für die Softwareupdates verwenden, und dieser Server muss sich innerhalb eines primären Standorts befinden.  

-   Sie müssen ein Gruppenrichtlinienobjekt (Group Policy Object, GPO) in Active Directory-Domänendienste mit dem aktiven Softwareupdatepunkt des Clients und dem Port konfigurieren, um neue Clients zu installieren.  

-   Wenn das Active Directory-Schema nicht für Configuration Manager erweitert wurde, müssen Sie Gruppenrichtlinieneinstellungen zur Bereitstellung von Computern mit Clientinstallationseigenschaften verwenden.  

 Weitere Informationen zu dieser Installationsmethode finden Sie unter [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="group-policy-installation"></a>Gruppenrichtlinieninstallation  
 **Unterstützte Clientplattformen:** Windows  

 **Vorteile:**  

-   Erfordert keine Ermittlung von Computern als Voraussetzung für die Installation des Clients.  

-   Kann für neue Clientinstallationen oder für Aktualisierungen verwendet werden.  

-   Clientinstallationseigenschaften, die in Active Directory-Domänendienste veröffentlicht wurden, können von Computern gelesen werden.  

-   Erfordert keine Konfiguration oder Wartung eines Installationskontos für den betreffenden Clientcomputer.  

 **Nachteile:**  

-   Kann beträchtlichen Netzwerkverkehr verursachen, wenn eine große Anzahl an Clients installiert wird.  

-   Wenn das Active Directory-Schema nicht für Configuration Manager erweitert wurde, müssen Sie die Clientinstallationseigenschaften mithilfe von Gruppenrichtlinieneinstellungen den Computern des Standorts hinzufügen.  

 Weitere Informationen zu dieser Installationsmethode finden Sie unter [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="logon-script-installation"></a>Anmeldeskriptinstallation  
 **Unterstützte Clientplattformen:** Windows  

 **Vorteile:**  

-   Erfordert keine Ermittlung von Computern als Voraussetzung für die Installation des Clients.  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

 **Nachteile:**  

-   Kann beträchtlichen Netzwerkverkehr verursachen, wenn in kurzer Zeit eine große Anzahl von Clients installiert wird.  

-   Die Installation auf allen Clientcomputern kann sehr lange dauern, wenn Benutzer sich nicht regelmäßig beim Netzwerk anmelden.  

 Weitere Informationen zu dieser Installationsmethode finden Sie unter [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="manual-installation"></a>Manuelle Installation  
 **Unterstützte Clientplattformen:** Windows, UNIX/Linux, Mac OS X  

 **Vorteile:**  

-   Erfordert keine Ermittlung von Computern als Voraussetzung für die Installation des Clients.  

-   Kann zu Testzwecken verwendet werden.  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

 **Nachteile:**  

-   Keine Automatisierung, daher zeitaufwändig.  

 Weitere Informationen zum manuellen Installieren des Clients auf jeder Plattform finden hier:  

-   [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

-   [Bereitstellen von Clients auf UNIX- und Linux-Servern in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)  

-   [Bereitstellen von Clients auf Macintosh-Computern in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  



<!--HONumber=Nov16_HO1-->


