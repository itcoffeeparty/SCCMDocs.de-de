---
title: Upgraden von Clients | Windows |System Center Configuration Manager
description: "Upgraden von Clients für Windows-Computer in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
caps.latest.revision: 11
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2b1600e6f04095506f18f4c2cd0988a320fbb951


---
# <a name="how-to-upgrade-clients-for-windows-computers-in-system-center-configuration-manager"></a>Aktualisieren von Clients für Windows-Computer in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können den Client auf Windows-Computern mithilfe von Clientinstallationsmethoden oder den Features für automatisches Clientupgrade in Configuration Manager aktualisieren. Die folgenden Clientinstallationsmethoden eignen sich für ein Upgrade der Clientsoftware auf Windows-Computern:  

-   Gruppenrichtlinieninstallation  

-   Anmeldeskriptinstallation  

-   Manuelle Installation  

-   Upgradeinstallation  

 Wenn Sie an einem Upgrade des Clients mithilfe einer Clientinstallationsmethode interessiert sind, finden Sie mehr dazu unter [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

> [!TIP]  
>  Wenn Sie ein Upgrade Ihrer Serverinfrastruktur von einer früheren Version von Configuration Manager durchführen \(z.B. Configuration Manager 2007 oder System Center 2012 Configuration Manager\), empfiehlt es sich, das Serverupgrade einschließlich der Installation sämtlicher Branchupdates vollständig abzuschließen, bevor Sie ein Upgrade der Configuration Manager-Clients durchführen.   Das neueste Branchupdate enthält die neueste Version des Clients, Sie sollten das Clientupgrade also durchführen, nachdem Sie alle Configuration Manager-Updates installiert haben, die Sie verwenden möchten.  

## <a name="use-automatic-client-upgrade"></a>Verwenden des automatischen Clientupgrades  
 Sie können Configuration Manager auch so konfigurieren, dass die Clientsoftware automatisch auf die aktuelle Configuration Manager-Clientversion aktualisiert wird, wenn in Configuration Manager festgestellt wird, dass ein der Configuration Manager-Hierarchie zugewiesener Client in einer niedrigeren als der in der Hierarchie verwendeten Version vorhanden ist. Dieses Szenario umfasst das Upgrade des Clients auf die neueste Version, wenn versucht wird, den Client einem Configuration Manager-Standort zuzuweisen.  

 Ein Client kann in den folgenden Szenarien automatisch aktualisiert werden:  

-   Die Clientversion ist niedriger als die in der Hierarchie verwendete Version.  

-   Auf dem Client am Standort der zentralen Verwaltung ist ein Sprachpaket installiert, und auf dem vorhandenen Client ist kein Sprachpaket installiert.  

-   Eine erforderliche Clientkomponente in der Hierarchie weist eine andere als die auf dem Client installierte Version auf.  

-   Mindestens eine Clientinstallationsdatei liegt in einer anderen Version vor.  

> [!NOTE]  
>  Sie können im Berichtsordner **Standort – Clientinformationen** den Bericht **Anzahl von Configuration Manager-Clients nach Clientversionen** ausführen, um die verschiedenen in Ihrer Hierarchie vorhandenen Versionen des Configuration Manager-Clients zu ermitteln.  

 Configuration Manager erstellt standardmäßig ein Upgradepaket, das automatisch an alle Verteilungspunkte in der Hierarchie gesendet wird. Wenn Sie Änderungen an dem am Standort der zentralen Verwaltung gespeicherten Clientpaket vornehmen, beispielsweise ein Clientsprachpaket hinzufügen, wird das Paket von Configuration Manager automatisch aktualisiert und an alle Verteilungspunkte in der Hierarchie verteilt. Wenn das automatische Clientupgrade aktiviert ist, wird das neue Clientsprachpaket auf allen Clients automatisch installiert.  

> [!NOTE]  
>  Configuration Manager sendet das Clientupgradepaket nicht automatisch an cloudbasierte Verteilungspunkte von Configuration Manager.  

 Automatische Clientupgrades sind nützlich bei einer geringen Anzahl von Clientcomputern, die von Ihrer Hauptmethode für die Clientinstallation nicht erfasst wurden. Dies kann beispielsweise der Fall sein, wenn einige Clients während der Bereitstellung des Clientupgrades offline waren. Daraufhin führen Sie das Clientupgrade für diese Computer mithilfe dieser Methode aus, sobald die Computer wieder aktiv sind.  

 Gehen Sie wie folgt vor, um das automatische Clientupgrade zu konfigurieren. Das automatische Clientupgrade muss an einem Standort der zentralen Verwaltung konfiguriert werden, und diese Konfiguration gilt für alle Clients in der Hierarchie.  

#### <a name="to-configure-automatic-client-upgrades"></a>So konfigurieren Sie automatische Clientupgrades  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.  

4.  Überprüfen Sie im Dialogfeld **Eigenschaften von Hierarchieeinstellungen** auf der Registerkarte **Clientupgrade** die Version und das Datum des Produktionsclient, und vergewissern Sie sich, dass es die Version ist, die Sie für ein Upgrade von Windows-Computern verwenden möchten.  Wenn es sich nicht um die erwartete Clientversion handelt, müssen Sie den Präproduktionsclient ggf. auf eine Produktionsversion heraufstufen. Weitere Informationen finden Sie unter [Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md).  

5.  Klicken Sie auf **Alle Clients in der Hierarchie mithilfe des Produktionsclients aktualisieren** und dann im Bestätigungsdialogfeld auf **OK** .  

6.  Wenn Sie keine Clientupgrades auf Server anwenden möchten, klicken Sie auf **Server nicht aktualisieren**.  

7.  Geben Sie hier die Anzahl der Tage an, innerhalb derer Computer den Client nach Erhalten der Clientrichtlinie aktualisieren müssen. Das Clientupgrade wird zu einem zufällig gewählten Zeitpunkt innerhalb dieses Zeitraums ausgeführt. Dadurch wird verhindert, dass für eine große Anzahl von Clientcomputern gleichzeitig ein Upgrade ausgeführt wird.

    > [!NOTE]
    > Ein Computer muss ausgeführt werden, um den Client upzugraden. Falls ein Computer nicht ausgeführt wird, wenn er wie geplant das Upgrade erhalten soll, wird das Upgrade nicht ausgeführt. Stattdessen wird beim Neustart des Computers ein anderes Upgrade für einen zufälligen Zeitpunkt innerhalb der zulässigen Anzahl von Tagen geplant. Tritt dieser Fall nach Ablauf der Anzahl von Tagen ein, wird das Upgrade so geplant, dass es zu einem zufälligen Zeitpunkt innerhalb von 24 Stunden nach dem Neustart des Computers durchgeführt wird.
    >     
    > Aufgrund dieses Verhaltens dauert das Upgrade von Computern, die regelmäßig am Ende des Arbeitstags heruntergefahren werden, möglicherweise länger als erwartet, wenn die zufällig geplante Upgradezeit nicht in die normale Arbeitszeit fällt.

8.  Klicken Sie auf **Installationspakete des Clients automatisch an Verteilungspunkte verteilen, die für vorab bereitgestellten Inhalt aktiviert wurden**, wenn das Clientinstallationspaket auf Verteilungspunkte kopiert werden soll, die für vorab bereitgestellten Inhalt aktiviert wurden.  

9. Klicken Sie auf **OK** , um die Einstellungen zu speichern und das Dialogfeld **Eigenschaften von Hierarchieeinstellungen** zu schließen. Diese Einstellungen werden beim nächsten Herunterladen einer Richtlinie auf Clients übertragen.  



<!--HONumber=Nov16_HO1-->


