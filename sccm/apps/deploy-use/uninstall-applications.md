---
title: Deinstallieren von Anwendungen | System Center Configuration Manager
description: Deinstallieren von Anwendungen mithilfe von System Center Configuration Manager
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9f654d899a1e3e1603eccb3943ffc4d4c178e143


---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>Deinstallieren von Anwendungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


## <a name="introduction"></a>Einführung  
  
-   Geben Sie im ** ** Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Inhalt**die Befehlszeile zum Deinstallieren des Bereitstellungstypinhalts an.  

-   Stellen Sie die Anwendung mit der Bereitstellungsaktion **Deinstallieren**bereit.  

> [!IMPORTANT]  
>  Einige Anwendungstypen unterstützen keine Deinstallation.  

 In der folgenden Liste finden Sie weitere Informationen zum Deinstallationsverhalten von Anwendungen:  

-   Wenn Sie eine Configuration Manager-Anwendung deinstallieren, werden abhängige Anwendungen nicht automatisch deinstalliert.  

-   Wenn Sie eine Anwendung mit der Aktion **Deinstallieren** für einen Benutzer bereitstellen und die Anwendung für alle Benutzer des Computers installiert wurde, kann bei der Deinstallation ein Fehler auftreten, falls die Berechtigungen des entsprechenden Benutzerkontos für die Deinstallation unzureichend sind.  

-   Wenn Sie einen Benutzer oder ein Gerät aus einer Sammlung entfernen, für die eine Anwendung bereitgestellt wurde, wird die Anwendung nicht automatisch vom Gerät entfernt.  

-   Bei einer Bereitstellung mit dem Bereitstellungszweck **Deinstallieren** werden keine Anforderungsregeln überprüft. Wenn die Anwendung auf dem Computer installiert ist, auf dem die Bereitstellung ausgeführt wird, wird sie deinstalliert.  

> [!IMPORTANT]  
>  Sie müssen alle vorhandenen Bereitstellungen oder simulierten Bereitstellungen einer Anwendung für eine Sammlung löschen, bevor Sie die Anwendung mithilfe der Bereitstellungsaktion **Deinstallieren**bereitstellen können.  
  
 Weitere Informationen zum Erstellen von Bereitstellungstypen finden Sie unter [Anwendungen erstellen](../../apps/deploy-use/create-applications.md).  
  
 Weitere Informationen zum Bereitstellen von Anwendungen finden Sie unter [Anwendungen bereitstellen](../../apps/deploy-use/deploy-applications.md).  
  
## <a name="uninstall-an-application"></a>Deinstallieren einer Anwendung  

1.  Konfigurieren Sie den Bereitstellungstyp für die Anwendung mit der Deinstallationsbefehlszeile mithilfe einer der folgenden Methoden:  

    -   Wählen Sie im ** ** Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemein**die Option **Informationen zu diesem Bereitstellungstyp automatisch den Installationsdateien entnehmen**aus. Wenn die Informationen in den Installationsdateien verfügbar sind, wird den Eigenschaften des Bereitstellungstyps automatisch die Deinstallationsbefehlszeile hinzugefügt.  

    -   Geben Sie im ** ** Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Inhalt**im Feld **Deinstallationsprogramm** die Befehlszeile zum Deinstallieren der Anwendung an.  

        > [!NOTE]  
        >  Die Seite **Inhalt** wird nur angezeigt, wenn Sie im ** ** Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemein** die Option **Informationen zum Bereitstellungstyp manuell angeben**auswählen.  

    -   Geben Sie im Dialogfeld **Eigenschaften** von *<Name des Bereitstellungstyps\>* auf der Registerkarte **Programme** im Feld **Deinstallationsprogramm** die Befehlszeile zum Deinstallieren der Anwendung an.  

2.  Stellen Sie die Anwendung bereit, und wählen Sie im ** ** Assistenten zum Bereitstellen von Software auf der Seite **Bereitstellungseinstellungen** die Bereitstellungsaktion **Deinstallieren**aus.  

    > [!NOTE]  
    >  Wenn Sie die Bereitstellungsaktion **Deinstallieren**auswählen, wird der Bereitstellungszweck automatisch als **Erforderlich**konfiguriert.  



<!--HONumber=Nov16_HO1-->


