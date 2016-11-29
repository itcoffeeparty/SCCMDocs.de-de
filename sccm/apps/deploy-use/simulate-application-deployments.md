---
title: Simulieren von Anwendungsbereitstellungen | System Center Configuration Manager
description: "Bewerten Sie die Erkennungsmethode, Anforderungen und Abhängigkeiten für einen Bereitstellungstyp, ohne die Anwendung zu installieren."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a7d9267d35b58fdc6a01b869eb739e9c721db4a4


---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simulieren von Anwendungsbereitstellungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie simulierte Bereitstellungen, um die Anwendbarkeit einer Anwendungsbereitstellung auf Computern zu testen, ohne die Anwendung zu installieren oder zu deinstallieren. Bei einer simulierten Bereitstellung werden Erkennungsmethode, Anforderungen und Abhängigkeiten für einen Bereitstellungstyp ausgewertet. Anschließend wird ein Bericht mit den Ergebnissen im Arbeitsbereich **Überwachung** unter dem Knoten **Bereitstellungen** ausgegeben. Gehen Sie zum Simulieren einer Anwendungsbereitstellung in System Center Configuration Manager wie in diesem Thema beschrieben vor.  

> [!NOTE]  
>  Die Verwendung von simulierten Bereitstellungen für Sammlungen von mobilen Geräten ist nicht möglich.  
>   
>  Sie können eine Anwendung mit dem Bereitstellungszweck **Deinstallieren** nicht bereitstellen, wenn bereits eine simulierte Bereitstellung der gleichen Anwendung aktiv ist.  
  
Konfigurieren Sie eine simulierte Anwendungsbereitstellung anhand des folgenden Verfahrens:
  
1.  Wählen Sie in der Configuration Manager-Konsole eines der folgenden Elemente aus:  

    -   Eine Sammlung von Benutzern  

    -   Eine Sammlung von Geräten  

    -   Eine Configuration Manager-Anwendung  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellung simulieren**.  

3.  Geben Sie im **Assistenten zum Simulieren der Anwendungsbereitstellung**die folgenden Informationen an:  

    -   **Anwendung** : Klicken Sie auf **Durchsuchen** , und wählen Sie dann die Anwendung aus, für die Sie eine simulierte Bereitstellung erstellen möchten.  

    -   **Sammlung** : Klicken Sie auf **Durchsuchen** , und wählen Sie dann die Sammlung aus, die Sie für die simulierte Bereitstellung verwenden möchten.  

    -   **Aktion** : Wählen Sie in der Dropdownliste aus, ob Sie das Installieren oder Deinstallieren der ausgewählten Anwendung simulieren möchten.  

    -   **Automatisch mit oder ohne Benutzeranmeldung bereitstellen** : Wenn diese Option aktiviert ist, wird die simulierte Bereitstellung von den Clients unabhängig davon ausgewertet, ob diese angemeldet sind.  

4.  Klicken Sie auf **Weiter**, überprüfen Sie die Informationen auf der Seite **Zusammenfassung** , und schließen Sie den Assistenten zum Simulieren der Anwendungsbereitstellung ab.  

5.  Simulierte Anwendungen werden im Arbeitsbereich **Überwachung** im Knoten **Bereitstellungen** mit dem Bereitstellungszweck **Simulieren**angezeigt. Weitere Informationen zum Überwachen von Anwendungsbereitstellungen finden Sie unter [Überwachen von Anwendungen in der System Center Configuration Manager-Konsole](../../apps/deploy-use/monitor-applications-from-the-console.md).  



<!--HONumber=Nov16_HO1-->


