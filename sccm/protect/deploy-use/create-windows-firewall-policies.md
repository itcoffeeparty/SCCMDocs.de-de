---
title: "Windows-Firewall-Richtlinien für Endpoint Protection | System Center Configuration Manager"
description: "Hier erfahren Sie, wie Firewallrichtlinien für Endpoint Protection in System Center 2012 Configuration Manager erstellt und bereitgestellt werden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 98e4c49a19da396389acdd0aa56aee9113ce58c9


---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-system-center-configuration-manager"></a>Erstellen und Bereitstellen von Windows-Firewall-Richtlinien für Endpoint Protection in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mithilfe von Firewallrichtlinien für Endpoint Protection in System Center 2012 Configuration Manager können Sie grundlegende Konfigurations- und Wartungstasks an der Windows-Firewall auf Clientcomputern in der Hierarchie ausführen. Über die Windows-Firewall-Richtlinien können Sie die folgenden Tasks ausführen:  

-   Steuern, ob die Windows-Firewall aktiviert oder deaktiviert ist  

-   Steuern, ob eingehende Verbindungen auf Clientcomputern zulässig sind  

-   Steuern, ob Benutzer benachrichtigt werden, wenn von der Windows-Firewall ein neues Programm blockiert wird  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie anschließend auf **Windows-Firewall-Richtlinien**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Windows-Firewall-Richtlinie erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** unter **Assistent zum Erstellen von Windows-Firewall-Richtlinien**einen Namen und optional eine Beschreibung für diese Firewallrichtlinie ein, und klicken Sie dann auf **Weiter**.  

5.  Konfigurieren Sie auf der Seite **Profileinstellungen** des Assistenten die folgenden Einstellungen für jedes Netzwerkprofil:  

    > [!IMPORTANT]  
    >  Wenn Sie Windows-Firewall-Richtlinien auf Computern bereitstellen möchten, auf denen Windows Server 2008 und Windows Vista Service Pack 1 ausgeführt werden, müssen Sie auf diesen Computern zuvor den [Hotfix KB971800](http://go.microsoft.com/fwlink/p/?LinkId=231239) installieren.  

    > [!NOTE]  
    >  Weitere Informationen zu Netzwerkprofilen finden Sie in der Windows-Dokumentation.  

    -   **Windows-Firewall aktivieren**  

        > [!NOTE]  
        >  Wenn **Windows-Firewall aktivieren** nicht aktiviert ist, sind die weiteren Einstellungen auf dieser Seite des Assistenten nicht verfügbar.  

    -   **Alle eingehenden Verbindungen blockieren, einschließlich der in der Liste der zugelassenen Programme**  

    -   **Benutzer benachrichtigen, wenn ein neues Programm von der Windows-Firewall blockiert wird**  

6.  Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die durchzuführenden Aktionen, und schließen Sie dann den Assistenten ab.  

7.  Überprüfen Sie, ob die neue Windows-Firewall-Richtlinie in der Liste **Windows-Firewall-Richtlinien** angezeigt wird.  

##  <a name="a-namebkmkassigna-to-deploy-a-windows-firewall-policy"></a><a name="BKMK_Assign"></a> So stellen Sie eine Windows-Firewall-Richtlinie bereit  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie anschließend auf **Windows-Firewall-Richtlinien**.  

3.  Wählen Sie aus der Liste **Windows-Firewall-Richtlinien** die Windows-Firewall-Richtlinie aus, die Sie bereitstellen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

5.  Geben Sie im Dialogfeld **Windows-Firewall-Richtlinie bereitstellen** die Sammlung an, der Sie diese Windows-Firewall-Richtlinie zuweisen möchten, und legen Sie einen Zuweisungszeitplan fest. Die Windows-Firewall-Richtlinie wird mithilfe dieses Zeitplans auf Kompatibilität bewertet, und die Windows-Firewall-Einstellungen auf den Clients werden neu konfiguriert, damit sie mit der Windows-Firewall-Richtlinie übereinstimmen.  

6.  Klicken Sie auf **OK** , um das Dialogfeld **Windows-Firewall-Richtlinie bereitstellen** zu schließen und die Windows-Firewall-Richtlinie bereitzustellen.  

    > [!IMPORTANT]  
    >  Wenn Sie eine Windows-Firewall-Richtlinie auf einer Sammlung bereitstellen, wird diese Richtlinie auf den Computern in zufälliger Reihenfolge über einen Zeitraum von 2 Stunden angewendet, um ein Überfluten des Netzwerks zu verhindern.



<!--HONumber=Nov16_HO1-->

