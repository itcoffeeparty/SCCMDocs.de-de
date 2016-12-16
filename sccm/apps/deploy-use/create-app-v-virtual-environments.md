---
title: Erstellen virtueller App-V-Umgebungen | System Center Configuration Manager
description: "Erstellen Sie virtuelle Umgebungen mit Microsoft Application Virtualization, damit Apps Daten untereinander austauschen können."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 625ea93d855089f6dbbdcc8368032e61b8a1ba0b


---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Erstellen virtueller App-V-Umgebungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mithilfe von virtuellen App-V-Umgebungen (Microsoft Application Virtualization) in System Center Configuration Manager können bereitgestellte virtuelle Anwendungen auf Windows-Clientcomputern ein Dateisystem und die Registrierung gemeinsam nutzen. Dies bedeutet, dass diese Anwendungen im Gegensatz zu virtuellen Standardanwendungen Daten freigeben können. Virtuelle Umgebungen werden bei der Installation der Anwendung bzw. bei der nächsten Auswertung der auf den Client-PCs installierten Anwendungen auf Clientcomputern erstellt oder geändert. Sie können diese Anwendungen mit Prioritäten versehen. Falls dann mehrere Anwendungen versuchen, ein Dateisystem oder einen Registrierungswert zu ändern, hat die Anwendung mit der höchsten Priorität Vorrang.  

> [!IMPORTANT]  
>  Verlassen Sie sich bei der Sicherheit, z. B. beim Schutz vor Antischadsoftware, nicht auf virtuelle App-V-Umgebungen.  

 Gehen Sie wie folgt vor, um in Configuration Manager virtuelle App-V-Umgebungen zu erstellen.  

## <a name="create-an-app-v-virtual-environment"></a>So erstellen Sie eine virtuelle App-V-Umgebung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Anwendungsverwaltung** > **Virtuelle App-V-Umgebungen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Virtuelle Umgebung erstellen**.  

4.  Geben Sie im Dialogfeld **Virtuelle Umgebung erstellen** die folgenden Informationen an:  

    -   **Name:** Geben Sie für die virtuelle Umgebung einen eindeutigen Namen mit maximal 128 Zeichen an.  

    -   **Beschreibung:** Geben Sie optional eine Beschreibung für die virtuelle Umgebung an.  

5.  Klicken Sie auf **Hinzufügen** , um der virtuellen Umgebung einen neuen Bereitstellungstyp hinzuzufügen. Sie müssen mindestens einen Bereitstellungstyp hinzufügen.  

6.  Geben Sie im Dialogfeld **Anwendungen hinzufügen** unter **Gruppenname** einen Namen mit maximal 128 Zeichen für diese Gruppe von Anwendungen an, die Sie der virtuellen Umgebung hinzufügen.  

7.  Klicken Sie auf **Hinzufügen**, wählen Sie die App-V 5-Anwendungen und Bereitstellungstypen aus, die Sie der Gruppe hinzufügen möchten, und klicken Sie dann auf **OK**.  

8.  Im Dialogfeld **Anwendungen hinzufügen** können Sie auf **Priorität erhöhen** oder **Priorität verringern** klicken, um anzugeben, welche Anwendung Vorrang hat, falls mehrere Anwendungen versuchen, Dateisystem- oder Registrierungseinstellungen in derselben virtuellen Umgebung zu ändern.  

9. Klicken Sie auf **OK** , um zum Dialogfeld **Virtuelle Umgebung erstellen** zurückzukehren.  

10. Klicken Sie nach dem Hinzufügen der Gruppen auf **OK** , um die virtuelle Umgebung zu erstellen. Die neue virtuelle Umgebung wird in der Configuration Manager-Konsole unter dem Knoten **Virtuelle App-V-Umgebungen** angezeigt. Sie können den Status der virtuellen Umgebungen überwachen, indem Sie den Bericht **Status der virtuellen App-V-Umgebung**verwenden.  

    > [!NOTE]  
    >  Die virtuelle Umgebung wird auf Client-PCs hinzugefügt oder geändert, wenn die Anwendung installiert wird oder wenn ein Client die nächste Auswertung seiner installierten Anwendungen durchführt.  



<!--HONumber=Nov16_HO1-->


