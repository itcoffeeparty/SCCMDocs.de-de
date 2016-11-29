---
title: "Veröffentlichen von Standortdaten | System Center Configuration Manager"
description: "Hier erfahren Sie, wie Configuration Manager-Standorte in Active Directory Domain Services veröffentlicht werden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cda87a3bdcbba342f111b68af75369ca14744441


---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>Veröffentlichen von Standortdaten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Nachdem Sie das Active Directory-Schema für System Center Configuration Manager erweitert haben, können Sie Configuration Manager-Standorte in den Active Directory Domain Services (AD DS) veröffentlichen und so ermöglichen, dass Standortdaten durch Active Directory-Computer gesichert aus einer vertrauenswürdigen Quelle abgerufen werden. Das Veröffentlichen von Standortinformationen in AD DS ist für die Basisfunktionen von Configuration Manager zwar nicht erforderlich, doch Sie können hierdurch den Verwaltungsaufwand reduzieren.  

-   **Wenn ein Standort für das Veröffentlichen in AD DS konfiguriert ist**, können Configuration Manager-Clients über die Active Directory-Veröffentlichung gefunden werden. Hierzu wird eine LDAP-Abfrage an einen globalen Katalogserver gestellt.  

-   **Wenn ein Standort keine Daten in AD DS veröffentlicht**, benötigen Clients einen alternativen Mechanismus zum Auffinden ihres Standardverwaltungspunkts.  

Weitere Informationen dazu, wie Clients nach einem Verwaltungspunkt suchen, finden Sie unter [Understand how clients find site resources and services for System Center Configuration Manager (Informationen dazu, wie Clients nach Standortressourcen und -diensten für System Center Configuration Manager suchen)](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Konfigurieren von Standorten für die Veröffentlichung in AD DS  
 Es folgen die allgemeinen Schritte:  

-   Sie müssen [das Active Directory-Schema für System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) in allen Gesamtstrukturen erweitern, in denen Sie Standortdaten veröffentlichen möchten. Zudem müssen Sie sicherstellen, dass der Container **Systemverwaltung** vorhanden ist.  

-   Sie müssen dem Computerkonto aller primären Standorte, das Daten veröffentlicht, die Berechtigung   **Vollzugriff** für den Container **System Management** und alle seine untergeordneten Objekte erteilen.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>So aktivieren Sie einen Configuration Manager-Standort für das Veröffentlichen von Standortinformationen in Active Directory-Gesamtstrukturen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration** , und klicken Sie auf **Standorte**. Wählen Sie den Standort aus, den Sie für die Veröffentlichung seiner Standortdaten konfigurieren möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

3.  Wählen Sie auf der Registerkarte **Veröffentlichen** der Standorteigenschaften die Gesamtstrukturen aus, in denen dieser Standort Standortdaten veröffentlichen wird.  

4.  Klicken Sie auf **OK** , um die Konfiguration zu speichern.  

 Verwenden Sie das folgende Verfahren zum Konfigurieren einer Active Directory-Gesamtstruktur für die Veröffentlichung:  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>So konfigurieren Sie Active Directory-Gesamtstrukturen für die Veröffentlichung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Active Directory-Gesamtstrukturen**. Wenn eine Active Directory-Gesamtstrukturermittlung bereits ausgeführt wurde, werden die ermittelten Gesamtstrukturen im Ergebnisbereich angezeigt. Bei der Ausführung der Active Directory-Gesamtstrukturermittlung werden die lokale Gesamtstruktur und alle vertrauenswürdigen Gesamtstrukturen ermittelt. Nur nicht vertrauenswürdige Gesamtstrukturen müssen manuell hinzugefügt werden.  

    -   Wählen Sie zum Konfigurieren einer bereits ermittelten Gesamtstruktur die gewünschte Gesamtstruktur im Ergebnisbereich aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften** , um die Eigenschaften der Gesamtstruktur anzuzeigen. Fahren Sie mit Schritt 3 fort.  

    -   Klicken Sie zum Konfigurieren einer nicht aufgelisteten Gesamtstruktur auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Gesamtstruktur hinzufügen** , um das Dialogfeld **Gesamtstruktur hinzufügen** zu öffnen. Fahren Sie mit Schritt 3 fort.  

3.  Schließen Sie auf der Registerkarte **Allgemein** die Konfiguration für die zu ermittelnde Gesamtstruktur ab, und geben Sie das **Konto für die Active Directory-Gesamtstruktur**an.  

    > [!NOTE]  
    >  Für die Active Directory-Gesamtstrukturermittlung ist ein globales Konto erforderlich, damit Ermittlung und Veröffentlichung in nicht vertrauenswürdigen Gesamtstrukturen möglich sind. Wenn Sie nicht das Computerkonto des Standortservers verwenden, können Sie nur ein globales Konto auswählen.  

4.  Wenn Sie planen, eine Veröffentlichung von Standortdaten in dieser Gesamtstruktur zu ermöglichen, konfigurieren Sie auf der Registerkarte **Veröffentlichen** das Veröffentlichen in dieser Gesamtstruktur.  

    > [!NOTE]  
    >  Wenn Sie Standorte für die Veröffentlichung in einer Gesamtstruktur aktivieren, müssen Sie das Active Directory-Schema dieser Gesamtstruktur für Configuration Manager erweitern. Außerdem muss das Konto für die Active Directory-Gesamtstruktur über Vollzugriff auf den Systemcontainer in dieser Gesamtstruktur verfügen.  

5.  Wenn Sie die Konfiguration dieser Gesamtstruktur zur Verwendung mit der Active Directory-Gesamtstrukturermittlung abgeschlossen haben, klicken Sie auf **OK** , um die Konfiguration zu speichern.  



<!--HONumber=Nov16_HO1-->


