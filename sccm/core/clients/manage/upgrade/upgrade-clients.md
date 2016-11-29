---
title: Aktualisieren von Clients | System Center Configuration Manager
description: "Enthält Informationen über das Aktualisieren von Clients in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
caps.latest.revision: 8
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1571d31af1e2697c5ecbdc709a3eea9d6e28dbf0


---
# <a name="upgrade-clients-in-system-center-configuration-manager"></a>Aktualisieren von Clients in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Es gibt verschiedene Methoden zur Aktualisierung der Clientsoftware von System Center Configuration Manager auf Windows-Computern, UNIX- und Linux-Servern sowie Macintosh-Computern in Ihrem Unternehmen. In den folgenden Abschnitten sind die Vor- und Nachteile der einzelnen Clientaktualisierungsmethoden aufgeführt, um Ihnen die Auswahl der für Ihre Organisation am besten geeigneten Methode zu erleichtern.  

> [!TIP]  
>  Wenn Sie ein Upgrade Ihrer Serverinfrastruktur von einer früheren Version von Configuration Manager durchführen \(z.B. Configuration Manager 2007 oder System Center 2012 Configuration Manager\), empfiehlt es sich, das Serverupgrade einschließlich der Installation sämtlicher Branchupdates vollständig abzuschließen, bevor Sie ein Upgrade der Configuration Manager-Clients durchführen.   Das neueste Branchupdate enthält die neueste Version des Clients, Sie sollten das Clientupgrade also durchführen, nachdem Sie alle Configuration Manager-Updates installiert haben, die Sie verwenden möchten.  

## <a name="group-policy-installation"></a>Gruppenrichtlinieninstallation  
 **Unterstützte Clientplattformen:** Windows  

 **Vorteile**  

-   Erfordert keine Ermittlung von Computern als Voraussetzung für die Aktualisierung des Clients.  

-   Kann für neue Clientinstallationen oder für Aktualisierungen verwendet werden.  

-   Clientinstallationseigenschaften, die in Active Directory-Domänendienste veröffentlicht wurden, können von Computern gelesen werden.  

-   Erfordert keine Konfiguration oder Wartung eines Installationskontos für den betreffenden Clientcomputer.  

 **Nachteile**  

-   Kann beträchtlichen Netzwerkverkehr verursachen, wenn eine große Anzahl an Clients aktualisiert wird.  

-   Wenn das Active Directory-Schema nicht für Configuration Manager erweitert wurde, müssen Sie die Clientinstallationseigenschaften mithilfe von Gruppenrichtlinieneinstellungen den Computern des Standorts hinzufügen.  

 Weitere Informationen finden Sie unter [Installieren von Configuration Manager-Clients mithilfe von Gruppenrichtlinien](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP).  

## <a name="logon-script-installation"></a>Anmeldeskriptinstallation  
 **Unterstützte Clientplattformen:** Windows  

 **Vorteile**  

-   Erfordert keine Ermittlung von Computern als Voraussetzung für die Installation des Clients.  

-   Kann für neue Clientinstallationen oder für Aktualisierungen verwendet werden.  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

 **Nachteile**  

-   Kann beträchtlichen Netzwerkverkehr verursachen, wenn in kurzer Zeit eine große Anzahl von Clients aktualisiert wird.  

-   Die Aktualisierung auf allen Clientcomputern kann sehr lange dauern, wenn Benutzer sich nicht regelmäßig beim Netzwerk anmelden.  

 Weitere Informationen finden Sie unter [Installieren von Configuration Manager-Clients mithilfe von Anmeldeskripts](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>Manuelle Installation  
 **Unterstützte Clientplattformen:** Windows, UNIX/Linux, Mac OS X  

 **Vorteile**  

-   Erfordert keine Ermittlung von Computern als Voraussetzung für die Aktualisierung des Clients.  

-   Kann zu Testzwecken verwendet werden.  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

 **Nachteile**  

-   Keine Automatisierung, daher zeitaufwändig.  

 Weitere Informationen finden Sie unter den folgenden Themen:  

-   [How to Install Configuration Manager Clients Manually (Manuelles Installieren von Configuration Manager-Clients)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [How to upgrade clients for Linux and UNIX servers in System Center Configuration Manager (Aktualisieren von Clients für Linux- und UNIX-Server in System Center Configuration Manager)](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

-   [How to upgrade clients on Mac computers in System Center Configuration Manager (Aktualisieren von Clients auf Macintosh-Computern in System Center Configuration Manager)](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Upgrade-Installation (Anwendungsverwaltung)  
 **Unterstützte Clientplattformen:** Windows  

> [!NOTE]  
>  Mit dieser Methode können keine Upgrades von Configuration Manager 2007-Clients durchgeführt werden. In diesem Szenario können Sie den Configuration Manager-Client als Paket vom Configuration Manager 2007-Standort bereitstellen, oder Sie können das automatische Clientupgrade verwenden, wobei automatisch ein Paket erstellt und bereitgestellt wird, das die aktuellste Clientversion enthält.  

 **Vorteile**  

-   Unterstützt die Verwendung von Befehlszeileneigenschaften für CCMSetup.  

 **Nachteile**  

-   Kann beträchtlichen Netzwerkverkehr verursachen, wenn der Client auf große Sammlungen verteilt wird.  

-   Kann nur verwendet werden, um Clientsoftware auf Computern zu aktualisieren, die ermittelt und dem Standort zugewiesen wurden.  

 Weitere Informationen finden Sie unter [Installieren von Configuration Manager-Clients mithilfe eines Pakets und Programms](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Automatisches Clientupgrade  

> [!NOTE]  
>  Kann verwendet werden, um ein Upgrade von Configuration Manager 2007-Clients auf System Center Configuration Manager-Clients auszuführen. Ein Configuration Manager 2007-Client kann einem Configuration Manager-Standort zugewiesen werden, allerdings können keine anderen Aktionen außer dem automatischen Clientupgrade durchgeführt werden.  

 **Unterstützte Clientplattformen:** Windows  

 **Vorteile**  

-   Kann verwendet werden, um Clients eines Standorts automatisch auf die neueste Version zu aktualisieren.  

-   Erfordert minimalen Verwaltungsaufwand durch den Administrator.  

 **Nachteile**  

-   Kann nur für ein Upgrade der Clientsoftware verwendet werden, nicht für die Installation eines neuen Clients.  

-   Nicht geeignet für das gleichzeitige Upgrade zahlreicher Clients.  

-   Gilt für alle Clients in der Hierarchie, die einem Standort zugewiesen sind. Kann nicht auf Sammlungen begrenzt werden.  

-   Begrenzte Planungsoptionen  

 Weitere Informationen finden Sie unter [Aktualisieren von Clients für Windows-Computer in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>Testen von Clients  
 **Unterstützte Clientplattformen:** Windows  

 **Vorteile**  

-   Dient zum Testen neuer Clientversionen in einer kleineren Präproduktionssammlung.  

-   Nach Abschluss der Tests werden Clients in der Präproduktionsphase auf die Produktionsebene heraufgestuft, und automatisch am gesamten Configuration Manager-Standort aktualisiert.  

 **Nachteile**  

-   Kann nur für ein Upgrade der Clientsoftware verwendet werden, nicht für die Installation eines neuen Clients.  

 [Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  



<!--HONumber=Nov16_HO1-->

