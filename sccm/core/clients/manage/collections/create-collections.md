---
title: Erstellen von Sammlungen | System Center Configuration Manager
description: "Erstellen Sie Sammlungen in System Center Configuration Manager, um Benutzergruppen und Geräte leichter zu verwalten."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f73f0e58b82d1aab1f64f3695dd5c3a61e933d2a


---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>Erstellen von Sammlungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Erstellen Sie Sammlungen in System Center Configuration Manager, um logische Gruppierungen von Benutzern oder Geräten darzustellen. Mithilfe von Sammlungen lassen sich zahlreiche Aufgaben ausführen, einschließlich der Verwaltung von Anwendungen, der Bereitstellung von Kompatibilitätseinstellungen und der Installation von Softwareupdates. Außerdem können Sammlungen zur Verwaltung von Clienteinstellungsgruppen verwendet werden. Möglich ist auch eine Verwendung von Sammlungen mit rollenbasierter Verwaltung zum Angeben der Ressourcen, auf die ein Administrator zugreifen kann. In Configuration Manager sind einige Sammlungen bereits integriert. Weitere Informationen finden Sie unter [Einführung in Sammlungen in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).  

> [!NOTE]  
>  Eine einzelne Sammlung kann entweder Benutzer oder Geräte enthalten, aber nicht beides.  

 In der folgenden Tabelle werden Regeln aufgeführt, mit denen Sie die Mitglieder einer Sammlung in Configuration Manager konfigurieren können.  

|Typ der Mitgliedschaftsregel|Weitere Informationen|  
|--------------------------|----------------------|  
|Direktregel|Mit Direktregeln können Sie die Benutzer oder Computer wählen, die Sie als Mitglieder einer Sammlung hinzufügen möchten. Mit einer solchen Regel können Sie direkt steuern, welche Ressourcen Mitglieder der Sammlung sind. Diese Mitgliedschaft ändert sich nicht, es sei denn, eine Ressource wird aus Configuration Manager entfernt. Die Ressourcen müssen von Configuration Manager ermittelt oder von Ihnen importiert worden sein, bevor Sie sie einer Direktregelsammlung hinzufügen können. Direktregelsammlungen bedeuten einen höheren Verwaltungsaufwand als Abfrageregelsammlungen, weil dieser Sammlungstyp manuell geändert werden muss.|  
|Abfrageregel|Durch Abfrageregeln wird die Mitgliedschaft einer Sammlung dynamisch auf Basis einer Abfrage aktualisiert, die von Configuration Manager nach einem Zeitplan ausgeführt werden. Sie können beispielsweise eine Sammlung von Benutzern erstellen, die Mitglieder der Organisationseinheit "Personal" in den Active Directory-Domänendiensten sind. Im Gegensatz zu Direktregelsammlungen wird diese Sammlungsmitgliedschaft automatisch aktualisiert, wenn neue Benutzer der Organisationseinheit "Personal" hinzugefügt bzw. daraus entfernt werden.<br /><br /> Weitere Informationen zu Abfragen, die Sie zum Erstellen von Sammlungen verwenden können, finden Sie unter [Erstellen von Abfragen in System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).|  
|Regel "Sammlungen einschließen"|Mit der Regel „Sammlungen einschließen“ können Sie die Mitglieder einer anderen Sammlung in eine Configuration Manager-Sammlung einschließen. Die Mitgliedschaft der aktuellen Sammlung wird nach einem Zeitplan aktualisiert, wenn sich die Mitgliedschaft der eingeschlossenen Sammlung ändert.<br /><br /> Sie können einer Sammlung mehrere Regeln "Sammlungen einschließen" hinzufügen.<br />              **Beispiel:** Sie erstellen eine Sammlung, die zwei Regeln "Sammlungen einschließen" enthält. Die erste Regel "Sammlungen einschließen" bezieht sich auf eine Sammlung von Laptops und die zweite auf eine Sammlung von Desktops. Die neue Sammlung enthält alle Mitglieder der Laptopsammlung und der Desktopsammlung.|  
|Regel "Sammlungen ausschließen"|Mit der Regel „Sammlungen ausschließen“ können Sie die Mitglieder einer anderen Sammlung aus einer Configuration Manager-Sammlung ausschließen. Die Mitgliedschaft der aktuellen Sammlung wird nach einem Zeitplan aktualisiert, wenn sich die Mitgliedschaft der ausgeschlossenen Sammlung ändert.<br /><br /> Sie können einer Sammlung mehrere Regeln "Sammlungen ausschließen" hinzufügen. Wenn eine Sammlung sowohl Regeln zum Einschließen als auch zum Ausschließen von Sammlungen enthält und diese in Konflikt stehen, hat die Regel "Sammlungen ausschließen" Priorität vor der Regel "Sammlungen einschließen".<br />              **Beispiel:** Sie erstellen eine Sammlung, die eine Regel "Sammlungen einschließen" und eine Regel "Sammlungen ausschließen" enthält. Die Regel "Sammlungen einschließen" bezieht sich auf eine Sammlung von Dell-Desktops. Die Regel "Sammlungen ausschließen" bezieht sich auf eine Sammlung von Computern mit weniger als 4 GB RAM. Die neue Sammlung enthält Dell-Desktops, die über mindestens 4 GB RAM verfügen.|  

 Die folgenden Prozeduren helfen Ihnen beim Erstellen von Sammlungen in Configuration Manager. Sie können auch Sammlungen importieren, die an diesem oder einem anderen Configuration Manager-Standort erstellt wurden. Informationen zum Exportieren von Sammlungen finden Sie unter [Verwalten von Sammlungen in Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

 Informationen zum Erstellen von Sammlungen für Computer unter Linux und UNIX finden Sie unter [Verwalten von Clients für Linux- und UNIX-Server in System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md).  

##  <a name="a-namebkmk1a-to-create-a-device-collection"></a><a name="BKMK_1"></a> So erstellen Sie eine Gerätesammlung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Gerätesammlung erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Gerätesammlungen**die folgenden Informationen an:  

    -   **Name**: Geben Sie einen eindeutigen Namen für die Sammlung an.  

    -   **Kommentar**: Geben Sie eine Beschreibung für die Sammlung an.  

    -   **Begrenzende Sammlung**: Klicken Sie zum Auswählen einer begrenzenden Sammlung auf **Durchsuchen** . In der Sammlung, die Sie erstellen, sind nur Mitglieder aus der begrenzenden Sammlung enthalten.  

5.  Geben Sie auf der Seite **Mitgliedschaftsregeln** des **Assistenten zum Erstellen von Gerätesammlungen**die folgenden Informationen an:  

    -   Wählen Sie in der Liste **Regel hinzufügen** den Typ der Mitgliedschaftsregel aus, den Sie für diese Sammlung verwenden möchten. Sie können für jede Sammlung mehrere Regeln konfigurieren.  

         Gehen Sie wie folgt vor, um jeden Typ der Mitgliedschaftsregel zu konfigurieren.  

        ##### <a name="to-configure-a-direct-rule"></a>So konfigurieren Sie eine Direktregel  

        1.  Geben Sie im **Assistenten für die Erstellung von Regeln der direkten Mitgliedschaft** auf der Seite **Ressourcen suchen**die folgenden Informationen an:  

            -   **Ressourcenklasse**: Wählen Sie in der Liste den Typ der Ressource aus, die Sie suchen und der Sammlung hinzufügen möchten. Wählen Sie aus den Werten unter **Systemressource** Werte zur Suche nach Inventurdaten aus, die von Clientcomputern zurückgegeben wurden, oder wählen Sie **Unbekannter Computer** aus, um Werte auszuwählen, die von unbekannten Computern zurückgegeben wurden.  

            -   **Attributname**: Wählen Sie in der Liste das Attribut aus, das der ausgewählten Ressourcenklasse zugeordnet ist, die suchen möchten. Wenn Sie Computer beispielsweise nach NetBIOS-Namen auswählen möchten, wählen Sie in der Liste **Ressourcenklasse** die Option **Systemressource** und in der Liste **Attributname** die Option **NetBIOS-Name** aus.  

            -   **Als veraltet markierte Ressourcen ausschließen:** Wenn ein Clientcomputer als veraltet markiert wird, schließen Sie diesen Wert nicht in die Suchergebnisse ein.  

            -   **Ressourcen ausschließen, für die der Configuration Manager-Client nicht installiert wurde:** Wenn in den Suchergebnissen eine Ressource enthalten ist, auf der kein Configuration Manager-Client installiert ist, wird diese Ressource nicht in den Suchergebnissen angezeigt.  

            -   **Wert** : Geben Sie einen Wert ein, für den Sie den ausgewählten Attributnamen suchen möchten. Sie können das Prozentzeichen **%** als Platzhalter verwenden. Wenn Sie beispielsweise nach Computern suchen möchten, deren NetBIOS-Name mit einem „M“ beginnt, geben Sie in dieses Feld **M%** ein.  

        2.  Wählen Sie im **Assistenten für die Erstellung von Regeln der direkten Mitgliedschaft** auf der Seite **Ressourcen auswählen**die Ressourcen aus, die Sie der Sammlung in der Liste **Ressourcen** hinzufügen möchten, und klicken Sie dann auf **Weiter**.  

        3.  Schließen Sie den **Assistenten für die Erstellung von Regeln der direkten Mitgliedschaft**ab.  

        ##### <a name="to-configure-a-query-rule"></a>So konfigurieren Sie eine Abfrageregel  

        1.  Geben Sie im Dialogfeld **Eigenschaften für Abfrageregel** die folgenden Informationen an:  

            -   **Name**: Geben Sie einen eindeutigen Namen für die Abfrageregel an.  

            -   **Abfrageanweisung importieren:** Öffnet das Dialogfeld **Abfrage durchsuchen**, in dem Sie eine Configuration Manager-Abfrage auswählen können, die als Abfrageregel für die Sammlung verwendet werden soll. Weitere Informationen zum Erstellen dieser Abfragen und einige Beispiele finden Sie unter [Erstellen von Abfragen in System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).  

            -   **Ressourcenklasse** : Wählen Sie in der Liste den Typ der Ressource aus, die Sie suchen und der Sammlung hinzufügen möchten. Wählen Sie aus den Werten unter **Systemressource** einen Wert zur Suche von Inventurdaten aus, die von Clientcomputern zurückgegeben wurden, oder wählen Sie **Unbekannter Computer** aus, um Werte auszuwählen, die von unbekannten Computern zurückgegeben wurden.  

            -   **Abfrageanweisung bearbeiten:** Öffnet das Dialogfeld **Eigenschaften der Abfrageanweisung**, in dem Sie eine Abfrage erstellen können, die als Regel für die Sammlung verwendet werden soll. Weitere Informationen zu Abfragen finden Sie unter [Abfragen – Technische Referenz für System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

        2.  Klicken Sie auf **OK** , um das Dialogfeld **Eigenschaften für Abfrageregel** zu schließen und die Abfrageregel zu speichern.  

        ##### <a name="to-configure-an-include-collection-rule"></a>So konfigurieren Sie eine Regel "Sammlungen einschließen"  

        1.  Wählen Sie im Dialogfeld **Sammlungen auswählen** die Sammlungen aus, die Sie in die neue Sammlung einschließen möchten.  

        2.  Klicken Sie auf **OK** , um das Dialogfeld **Sammlungen auswählen** zu schließen und die Mitgliedschaftsregel "Sammlungen einschließen" zu speichern.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>So konfigurieren Sie eine Regel "Sammlungen ausschließen"  

        1.  Wählen Sie im Dialogfeld **Sammlungen auswählen** die Sammlungen aus, die Sie aus der neuen Sammlung ausschließen möchten.  

        2.  Klicken Sie auf **OK** , um das Dialogfeld **Sammlungen auswählen** zu schließen und die Mitgliedschaftsregel "Sammlungen ausschließen" zu speichern.  

    -   **Inkrementelle Updates für diese Sammlung verwenden:** Wählen Sie diese Option aus, um regelmäßig eine Überprüfung auf nur neue oder geänderte Ressourcen aus der vorherigen Sammlungsauswertung auszuführen und die Sammlungsmitgliedschaft nur mit diesen Ressourcen zu aktualisieren, unabhängig von einer vollständigen Sammlungsauswertung. Inkrementelle Updates erfolgen in Abständen von 10 Minuten.  

        > [!IMPORTANT]  
        >  Von Sammlungen, die mit Abfrageregeln erstellt wurden, in denen folgende Klassen verwendet werden, werden inkrementelle Updates nicht unterstützt:  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (nur für Benutzersammlungen)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (nur für Benutzersammlungen)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Vollständiges Update für diese Sammlung planen:** Wählen Sie diese Option aus, um eine normale, vollständige Auswertung der Sammlungsmitgliedschaft zu planen.  

6.  Schließen Sie den Assistenten ab, um die neue Sammlung zu erstellen. Die neue Sammlung wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Gerätesammlungen** angezeigt.  

> [!NOTE]  
>  Sie müssen die Configuration Manager-Konsole aktualisieren oder erneut laden, um die Sammlungsmitglieder anzuzeigen. Allerdings werden die Mitglieder erst nach dem ersten geplanten Update oder nachdem Sie manuell **Mitgliedschaft aktualisieren** für die Sammlung ausgewählt haben in der Sammlung angezeigt. Je nach Komplexität der Sammlungsregel und der Anzahl von Einträgen in der Configuration Manager-Datenbank kann das Aktualisieren einer Sammlung einige Minuten dauern.  

##  <a name="a-namebkmk2a-to-create-a-user-collection"></a><a name="BKMK_2"></a> So erstellen Sie eine Benutzersammlung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Benutzersammlungen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Benutzersammlung erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Benutzersammlungen**die folgenden Informationen an:  

    -   **Name**: Geben Sie einen eindeutigen Namen für die Sammlung an.  

    -   **Kommentar**: Geben Sie eine Beschreibung für die Sammlung an.  

    -   **Begrenzende Sammlung**: Klicken Sie zum Auswählen einer begrenzenden Sammlung auf **Durchsuchen** . In der Sammlung, die Sie erstellen, sind nur Mitglieder aus der begrenzenden Sammlung enthalten.  

5.  Geben Sie auf der Seite **Mitgliedschaftsregeln** des **Assistenten zum Erstellen von Benutzersammlungen**die folgenden Informationen an:  

    -   Wählen Sie in der Liste **Regel hinzufügen** den Typ der Mitgliedschaftsregel aus, den Sie für diese Sammlung verwenden möchten. Sie können für jede Sammlung mehrere Regeln konfigurieren.  

         Gehen Sie wie folgt vor, um jeden Typ der Mitgliedschaftsregel zu konfigurieren.  

        ##### <a name="to-configure-a-direct-rule"></a>So konfigurieren Sie eine Direktregel  

        1.  Geben Sie im **Assistenten für die Erstellung von Regeln der direkten Mitgliedschaft** auf der Seite **Ressourcen suchen**die folgenden Informationen an:  

            -   **Ressourcenklasse**: Wählen Sie in der Liste den Typ der Ressource aus, die Sie suchen und der Sammlung hinzufügen möchten. Wählen Sie Werte unter **Benutzerressource** aus, um Benutzerinformationen zu suchen, die von Configuration Manager gesammelt wurden, oder unter **Benutzergruppenressource**, um Benutzergruppeninformationen zu suchen, die von Configuration Manager gesammelt wurden.  

            -   **Attributname**: Wählen Sie in der Liste das Attribut aus, das der ausgewählten Ressourcenklasse zugeordnet ist, die suchen möchten. Wenn Sie Benutzer beispielsweise nach dem Namen der Organisationseinheit auswählen möchten, wählen Sie in der Liste **Ressourcenklasse** die Option **Benutzerressource** und in der Liste **Attributname** die Option **Benutzer-Organisationseinheitsname** aus.  

            -   **Wert** : Geben Sie einen Wert ein, für den Sie den ausgewählten Attributnamen suchen möchten. Sie können das Prozentzeichen **%** als Platzhalter verwenden. Wenn Sie Benutzer in der Organisationseinheit "Contoso" suchen möchten, geben Sie beispielsweise **Contoso** in dieses Feld ein.  

        2.  Wählen Sie im **Assistenten für die Erstellung von Regeln der direkten Mitgliedschaft** auf der Seite **Ressourcen auswählen**die Ressourcen aus, die Sie der Sammlung in der Liste **Ressourcen** hinzufügen möchten, und klicken Sie dann auf **Weiter**.  

        3.  Schließen Sie den **Assistenten für die Erstellung von Regeln der direkten Mitgliedschaft**ab.  

        ##### <a name="to-configure-a-query-rule"></a>So konfigurieren Sie eine Abfrageregel  

        1.  Geben Sie im Dialogfeld **Eigenschaften für Abfrageregel** die folgenden Informationen an:  

            -   **Name**: Geben Sie einen eindeutigen Namen für die Abfrageregel an.  

            -   **Abfrageanweisung importieren:** Öffnet das Dialogfeld **Abfrage durchsuchen**, in dem Sie eine Configuration Manager-Abfrage auswählen können, die als Abfrageregel für die Sammlung verwendet werden soll. Weitere Informationen zu Abfragen finden Sie unter [Abfragen – Technische Referenz für System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

            -   **Ressourcenklasse**: Wählen Sie in der Liste den Typ der Ressource aus, die Sie suchen und der Sammlung hinzufügen möchten. Wählen Sie Werte unter **Benutzerressource** aus, um Benutzerinformationen zu suchen, die von Configuration Manager gesammelt wurden, oder unter **Benutzergruppenressource**, um Benutzergruppeninformationen zu suchen, die von Configuration Manager gesammelt wurden.  

            -   **Abfrageanweisung bearbeiten:** Öffnet das Dialogfeld **Eigenschaften der Abfrageanweisung**, in dem Sie eine Abfrage erstellen können, die als Regel für die Sammlung verwendet werden soll. Weitere Informationen zu Abfragen finden Sie unter [Abfragen – Technische Referenz für System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

        2.  Klicken Sie auf **OK** , um das Dialogfeld **Eigenschaften für Abfrageregel** zu schließen und die Abfrageregel zu speichern.  

        ##### <a name="to-configure-an-include-collection-rule"></a>So konfigurieren Sie eine Regel "Sammlungen einschließen"  

        1.  Wählen Sie im Dialogfeld **Sammlungen auswählen** die Sammlungen aus, die Sie in die neue Sammlung einschließen möchten.  

        2.  Klicken Sie auf **OK** , um das Dialogfeld **Sammlungen auswählen** zu schließen und die Mitgliedschaftsregel "Sammlungen einschließen" zu speichern.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>So konfigurieren Sie eine Regel "Sammlungen ausschließen"  

        1.  Wählen Sie im Dialogfeld **Sammlungen auswählen** die Sammlungen aus, die Sie aus der neuen Sammlung ausschließen möchten.  

        2.  Klicken Sie auf **OK** , um das Dialogfeld **Sammlungen auswählen** zu schließen und die Mitgliedschaftsregel "Sammlungen ausschließen" zu speichern.  

    -   **Inkrementelle Updates für diese Sammlung verwenden:** Wählen Sie diese Option aus, um regelmäßig eine Überprüfung auf nur neue oder geänderte Ressourcen aus der vorherigen Sammlungsauswertung auszuführen und die Sammlungsmitgliedschaft nur mit diesen Ressourcen zu aktualisieren, unabhängig von einer vollständigen Sammlungsauswertung. Inkrementelle Updates erfolgen in Abständen von 10 Minuten.  

        > [!IMPORTANT]  
        >  Von Sammlungen, die mit Abfrageregeln erstellt wurden, in denen folgende Klassen verwendet werden, werden inkrementelle Updates nicht unterstützt:  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (nur für Benutzersammlungen)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (nur für Benutzersammlungen)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Vollständiges Update für diese Sammlung planen:** Wählen Sie diese Option aus, um eine normale, vollständige Auswertung der Sammlungsmitgliedschaft zu planen.  

6.  Schließen Sie den Assistenten ab, um die neue Sammlung zu erstellen. Die neue Sammlung wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Benutzersammlungen** angezeigt.  

> [!NOTE]  
>  Sie müssen die Configuration Manager-Konsole aktualisieren oder erneut laden, um die Sammlungsmitglieder anzuzeigen. Allerdings werden die Mitglieder erst nach dem ersten geplanten Update oder nachdem Sie manuell **Mitgliedschaft aktualisieren** für die Sammlung ausgewählt haben in der Sammlung angezeigt. Je nach Komplexität der Sammlungsregel und der Anzahl von Einträgen in der Configuration Manager-Datenbank kann das Aktualisieren einer Sammlung einige Minuten dauern.  

##  <a name="a-namebkmk3a-to-import-a-collection"></a><a name="BKMK_3"></a> So importieren Sie eine Sammlung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Benutzersammlungen** oder **Gerätesammlungen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Sammlungen importieren**.  

4.  Klicken Sie im **Assistenten zum Importieren von Sammlungen** auf der Seite **Allgemein**auf **Weiter**.  

5.  Klicken Sie auf der Seite **MOF-Dateiname** auf **Durchsuchen** , und suchen Sie dann die MOF-Datei, die die zu importierenden Sammlungsinformationen enthält.  

    > [!NOTE]  
    >  Die zu importierende Datei muss von einem Standort exportiert worden sein, an dem dieselbe Configuration Manager-Version wie am Zielstandort ausgeführt wird. Weitere Informationen zum Exportieren von Sammlungen finden Sie unter [Verwalten von Sammlungen in Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

6.  Schließen Sie den Assistenten ab, um die Sammlung zu importieren. Die neue Sammlung wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Benutzersammlungen** oder **Gerätesammlungen** angezeigt.  

> [!NOTE]  
>  Sie müssen die Configuration Manager-Konsole aktualisieren oder erneut laden, um die Sammlungsmitglieder für die neu importierte Sammlung anzuzeigen.  



<!--HONumber=Nov16_HO1-->


