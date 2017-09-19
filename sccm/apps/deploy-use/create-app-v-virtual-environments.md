---
title: Erstellen virtueller App-V-Umgebungen | Microsoft-Dokumentation
description: "Erstellen Sie virtuelle Umgebungen mit Microsoft Application Virtualization, damit Apps Daten untereinander austauschen können."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: "6"
caps.handback.revision: "0"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: f672bb5bdea0878bfc38575840f0c8f8c7f065b6
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2017
---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Erstellen virtueller App-V-Umgebungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In einer virtuellen App-V-Umgebung (Microsoft Application Virtualization) in System Center Configuration Manager (Configuration Manager) können bereitgestellte virtuelle Anwendungen auf Windows-Clientcomputern ein Dateisystem und die Registrierung gemeinsam nutzen. Im Gegensatz zu virtuellen Standardanwendungen können diese Anwendungen Daten gemeinsam verwenden. Virtuelle Umgebungen werden bei der Installation der Anwendung bzw. bei der nächsten Auswertung der auf den Client-PCs installierten Anwendungen auf Clientcomputern erstellt oder geändert. Sie können diese Anwendungen mit Prioritäten versehen. Falls dann mehrere Anwendungen versuchen, ein Dateisystem oder einen Registrierungswert zu ändern, hat die Anwendung mit der höchsten Priorität Vorrang.  

> [!IMPORTANT]  
>  Verlassen Sie sich bei der Sicherheit, z.B. beim Schutz vor Antischadsoftware, nicht auf virtuelle App-V-Umgebungen.  

 Gehen Sie wie folgt vor, um in Configuration Manager eine virtuelle App-V-Umgebung zu erstellen.  

## <a name="create-an-app-v-virtual-environment"></a>So erstellen Sie eine virtuelle App-V-Umgebung  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **Virtuelle App-V-Umgebungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Virtuelle Umgebung erstellen** aus.  

4.  Geben Sie im Dialogfeld **Virtuelle Umgebung erstellen** die folgenden Informationen ein:  

    -   **Name**.  Geben Sie für die virtuelle Umgebung einen eindeutigen Namen (maximal 128 Zeichen) ein.  

    -   **Beschreibung**. (Optional) Geben Sie eine Beschreibung für die virtuelle Umgebung ein.  

5.  Wählen Sie **Hinzufügen** aus, um der virtuellen Umgebung einen neuen Bereitstellungstyp hinzuzufügen. Sie müssen mindestens einen Bereitstellungstyp hinzufügen.  

6.  Geben Sie im Dialogfeld **Anwendungen hinzufügen** einen **Gruppennamen** an (maximal 128 Zeichen). Sie können diesen Namen verwenden, um auf die Gruppe von Anwendungen zu verweisen, die Sie zur virtuellen Umgebung hinzufügen.  

7.  Wählen Sie **Hinzufügen** und die App-V 5-Anwendungen und Bereitstellungstypen aus, die Sie der Gruppe hinzufügen möchten, und wählen Sie anschließend **OK** aus.  

8.  Im Dialogfeld **Anwendungen hinzufügen** können Sie **Priorität erhöhen** oder **Priorität verringern** auswählen, um die Anwendung festzulegen, die Vorrang hat, falls mehrere Anwendungen versuchen, Dateisystem- oder Registrierungseinstellungen in derselben virtuellen Umgebung zu ändern.  

9. Wählen Sie **OK** aus, um zum Dialogfeld **Virtuelle Umgebung erstellen** zurückzukehren.  

10. Wählen Sie nach dem Hinzufügen der Gruppen **OK** aus, um die virtuelle Umgebung zu erstellen. Die neue virtuelle Umgebung wird in der Configuration Manager-Konsole unter dem Knoten **Virtuelle App-V-Umgebungen** angezeigt. Sie können den Status der virtuellen Umgebungen überwachen, indem Sie den Bericht zum Status der virtuellen App-V-Umgebung verwenden.  

    > [!NOTE]  
    >  Die virtuelle Umgebung wird auf Client-PCs hinzugefügt oder geändert, wenn die Anwendung installiert ist, oder wenn ein Client die nächste Auswertung seiner installierten Anwendungen durchführt.  
