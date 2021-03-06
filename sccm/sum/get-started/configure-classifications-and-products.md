---
title: Konfigurieren von Klassifizierungen und Produkten
titleSuffix: Configuration Manager
description: Führen Sie diese Schritte zum Konfigurieren von Softwareupdateklassifizierungen und Produkten in der Configuration Manager-Konsole durch.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: a9af39cd5f57e8b2741facde269ea81bc1b10728
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
#  <a name="configure-classifications-and-products-to-synchronize"></a>Konfigurieren der zu synchronisierenden Klassifizierungen und Produkte  

*Gilt für: System Center Configuration Manager (Current Branch)*


> [!NOTE]  
>  Führen Sie das in diesem Abschnitt beschriebene Verfahren nur am Standort der obersten Ebene aus.  

 Die Metadaten von Softwareupdates werden während des Synchronisierungsprozesses in Configuration Manager abgerufen. Diese basieren auf den Einstellungen, die Sie in den Komponenteneigenschaften des Softwareupdatepunkts angeben. Nachdem Sie Softwareupdates zum ersten Mal synchronisiert haben oder neue Produkte und Klassifikationen freigegeben werden, müssen Sie in den Eigenschaften die neuen Elemente auswählen. Gehen Sie wie folgt vor, um die zu synchronisierenden Klassifizierungen und Produkte zu konfigurieren.  

#### <a name="to-configure-classifications-and-products-to-synchronize"></a>So konfigurieren Sie die zu synchronisierenden Klassifizierungen und Produkte  

1.  Wechseln Sie in der **Configuration Manager**-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**.

2. Wählen Sie entweder den Standort der zentralen Verwaltung oder den eigenständigen primären Standort aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren**, und klicken Sie dann auf **Softwareupdatepunkt**.

4.  Geben Sie auf der Registerkarte **Klassifizierungen** die Softwareupdateklassifizierungen an, für die Sie Softwareupdates synchronisieren möchten.  

    > [!NOTE]  
    >  Jedes Softwareupdate ist mit einer Updateklassifizierung definiert, die bei der Einteilung in verschiedene Updatearten behilflich ist. Bei der Synchronisierung werden die Metadaten für Softwareupdates für die angegebenen Klassifizierungen synchronisiert. Configuration Manager kann Softwareupdates mit folgenden Updateklassifizierungen synchronisieren:  
    >   
    > - **Wichtige Updates**: Hierbei handelt es sich um ein im großen Umfang freigegebenes Update für ein bestimmtes Problem, mit dem ein wichtiger, nicht sicherheitsrelevanter Fehler behoben wird.  
    > - **Definitionsupdates**: Hierbei handelt es sich um ein Update für Virus- oder andere Definitionsdateien.  
    > - **Feature Packs**: Hierbei handelt es sich um neue Produktfeatures, die außerhalb einer Produktveröffentlichung verteilt werden und in der Regel in der nächsten vollständigen Produktveröffentlichung enthalten sind.  
    > - **Sicherheitsupdates**: Hierbei handelt es sich um ein im großen Umfang freigegebenes Update für ein produktspezifisches, sicherheitsrelevantes Problem.  
    > - **Service Packs**: Hierbei handelt es sich um einen kumulativen Satz von Hotfixes, die auf eine Anwendung angewendet werden. Diese Hotfixes können Sicherheitsupdates, wichtige Updates, Softwareupdates usw. umfassen.  
    > - **Tools**: Hierbei handelt es sich um ein Dienstprogramm oder Feature, mit dem mindestens ein Task einfacher ausgeführt werden kann.  
    > - **Updaterollups**: Hierbei handelt es sich um einen kumulativen Satz von Hotfixes, die für eine einfache Bereitstellung gebündelt sind. Diese Hotfixes können Sicherheitsupdates, wichtige Updates, Updates usw. umfassen. Ein Aktualisierungsrollup betrifft in der Regel einen bestimmten Bereich, z. B. Sicherheit oder eine Produktkomponente.  
    > - **Updates**: Hierbei handelt es sich um ein Update für eine gegenwärtig installierte Anwendung oder Datei.  
    > - **Upgrade**: Hierbei handelt es sich um ein Upgrade für Windows 10-Features und -Funktionalität. Ihre Softwareupdatepunkte und Standorte müssen mindestens WSUS 4.0 mit dem [Hotfix 3095113](https://support.microsoft.com/kb/3095113) ausführen, um die Klassifizierung **Upgrade** zu erhalten.    
    >       

    > [!NOTE]    
    > Ab Version 1706 von Configuration Manager steht Ihnen die Option **Microsoft Surface-Treiber und Firmwareupdates einbeziehen** für die Synchronisierung von Microsoft Surface-Treibern zur Verfügung.<!--1098490--> Voraussetzung hierfür ist die Installation von Windows Server 2016 auf allen Softwareupdatepunkten. Wenn Sie einen Softwareupdatepunkt auf einem Computer mit Windows Server 2012 aktivieren, nachdem Sie Surface-Treiber aktiviert haben, sind die Suchergebnisse für die Treiberupdates ungenau. Dies führt zu fehlerhaften Konformitätsdaten, die in der Configuration Manager-Konsole und in Configuration Manager-Berichten angezeigt werden.  
    >  
    > Dieses Feature wurde erstmals in Version 1706 als [Vorabfeature](/sccm/core/servers/manage/pre-release-features) eingeführt. Ab Version 1710 können ist diese Funktion keine Vorabfunktion mehr.  
    >  
    > Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

5.  Geben Sie auf der Seite **Produkte** die Produkte an, für die Sie Softwareupdates synchronisieren möchten. Klicken Sie dann auf **Schließen**.  

    > [!NOTE]  
    >  Die Produkte, für die ein Update gilt, werden anhand der Metadaten für die einzelnen Softwareupdates definiert. Ein Produkt ist eine bestimmte Edition eines Betriebssystems oder einer Anwendung, z. B. Microsoft Windows Server 2012. Eine Produktfamilie ist das Basisbetriebssystem bzw. die Basisanwendung, von dem bzw. der die einzelnen Produkte abgeleitet sind. Ein Beispiel für eine Produktfamilie ist Windows. Windows Server 2012 ist ein Mitglied dieser Produktfamilie. Sie können eine Produktfamilie oder einzelne Produkte innerhalb einer Produktfamilie angeben. Je mehr Produkte Sie auswählen, desto länger dauert die Synchronisierung von Softwareupdates.  
    >   
    >  Wenn Softwareupdates auf mehrere Produkte anwendbar sind und mindestens eines der Produkte für die Synchronisierung ausgewählt wurde, werden sämtliche Produkte in der Configuration Manager-Konsole angezeigt, auch wenn einige Produkte nicht ausgewählt wurden. Wenn z. B. Windows Server 2012 das einzige Betriebssystem ist, das Sie ausgewählt haben, und ein Softwareupdate auf Windows 8 und auf Windows Server 2012 anwendbar ist, werden beide Produkte in der Configuration Manager-Konsole angezeigt.  

    > [!IMPORTANT]  
    >  Configuration Manager speichert eine Liste der Produkte und Produktfamilien, aus denen Sie bei der Erstinstallation des Softwareupdatepunkts auswählen können. Produkte und Produktfamilien, die nach der Veröffentlichung von Configuration Manager freigegeben werden, können möglicherweise erst ausgewählt werden, nachdem Sie die Softwareupdatesynchronisierung abgeschlossen haben. Dabei wird die Liste der verfügbaren Produkte und Produktfamilien, aus denen Sie auswählen können, aktualisiert.  

## <a name="next-steps"></a>Nächste Schritte
Starten Sie die Synchronisierung von Softwareupdates, um Softwareupdates auf der Grundlage der neuen Kriterien abzurufen. Mehr Informationen finden Sie unter [Synchronisieren von Softwareupdates](synchronize-software-updates.md).
