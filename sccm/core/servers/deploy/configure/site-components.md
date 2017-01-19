---
title: Standortkomponenten | Microsoft-Dokumentation
description: "Erfahren Sie, wie Standortkomponenten so konfiguriert werden, dass sich das Verhalten von Standortsystemrollen und die Statusberichterstellung des Standorts ändert."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e22ffc898dc93f702f13417878aa6050d4cdd4ec


---
# <a name="site-components-for-system-center-configuration-manager"></a>Standortkomponenten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

An jedem System Center Configuration Manager-Standort können Sie Standortkomponenten konfigurieren, um das Verhalten von Standortsystemrollen und die Statusberichterstellung des Standorts zu ändern. Konfigurationen von Standortkomponenten gelten für einen Standort sowie für jede Instanz einer anwendbaren Standortsystemrolle am Standort.  

## <a name="about-site-components"></a>Informationen zu Standortkomponenten  
 Die meisten Optionen für die verschiedenen Standortkomponenten sind bei Anzeige in der Configuration Manager-Konsole selbsterklärend. Allerdings können die folgenden Details Ihnen bei der Erläuterung einiger komplexerer Konfigurationen helfen oder Sie auf zusätzliche Inhalte mit Erklärungen verweisen:  

**Softwareverteilung:**  

-   **Inhaltsverteilungseinstellungen:**  Sie können Einstellungen konfigurieren, die ändern, wie der Standortserver Inhalte an seine Verteilungspunkte überträgt. Wenn Sie die Werte der Einstellungen für die gleichzeitige Verteilung erhöhen, kann die Inhaltsverteilung mehr Netzwerkbandbreite nutzen.  

-   **Netzwerkzugriffskonto:** Informationen zum Konfigurieren und Verwenden des Netzwerkzugriffskontos finden Sie unter [Network Access Account (Netzwerkzugriffskonto)](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

**Softwareupdatepunkt:**  

-   Informationen zu den Konfigurationsoptionen für die Softwareupdatepunkt-Komponente finden Sie unter [Install a software update point (Installieren eines Softwareupdatepunkts)](../../../../sum/get-started/install-a-software-update-point.md).  

**Verwaltungspunkt:**  

-   **Verwaltungspunkte:** Sie können den Standort so konfigurieren, dass Informationen zu seinen Verwaltungspunkten in Active Directory-Domänendiensten veröffentlicht werden.  

     Configuration Manager-Clients werden Verwaltungspunkte für die Dienstidentifizierung verwenden, um Standortinformationen zu suchen, wie Zugehörigkeit zu Begrenzungsgruppen und PKI-Zertifikatauswahloptionen sowie andere Verwaltungspunkte auf dem Standort und Verteilungspunkte, von denen Software heruntergeladen werden kann. Bei Clients werden Verwaltungspunkte darüber hinaus verwendet, um Standortzuweisungen abzuschließen, Clientrichtlinien herunterzuladen und ihre Clientinformationen hochzuladen.  

     Die sicherste Methode zum Suchen von Verwaltungspunkten besteht für Clients darin, sie in den Active Directory-Domänendiensten zu veröffentlichen. Daher wählen Sie in der Regel alle funktionsfähigen Verwaltungspunkte für die Veröffentlichung in den Active Directory-Domänendiensten aus. Allerdings ist es für diese Methode der Dienstidentifizierung erforderlich, dass das Schema für Configuration Manager erweitert wird, dass ein **System Management**-Container mit entsprechenden Sicherheitsberechtigungen für den Standortserver zur Veröffentlichung in diesem Container vorhanden ist, dass der Configuration Manager-Standort für die Veröffentlichung in Active Directory Domain Services konfiguriert ist, und dass Clients der gleichen Active Directory-Gesamtstruktur zugewiesen sind wie die Gesamtstruktur des Standortservers.  

     Wenn es für Clients im Intranet nicht möglich ist, Verwaltungspunkte mithilfe von Active Directory Domain Services zu suchen, verwenden Sie die [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns)-Veröffentlichung.  

     Allgemeine Informationen zur Dienstidentifizierung durch Clients finden Sie unter [Understand how clients find site resources and services for System Center Configuration Manager (Informationen dazu, wie Clients nach Standortressourcen und -diensten für System Center Configuration Manager suchen)](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   **Ausgewählte Intranetverwaltungspunkte in DNS veröffentlichen:** Geben Sie diese Option an, wenn es für Clients im Intranet nicht möglich ist, Verwaltungspunkte mithilfe von Active Directory-Domänendiensten zu suchen, jedoch die Verwendung eines DNS-Ressourceneintrags zur Dienstidentifizierung (SRV RR) eine Option ist, um einen Verwaltungspunkt in ihrem zugewiesenen Standort zu suchen.  

    Damit in Configuration Manager Intranetverwaltungspunkte in DNS veröffentlicht werden können, müssen die beiden folgenden Bedingungen erfüllt sein:  

    -   Ihre DNS-Server verfügen mindestens über die BIND-Version 8.1.2.  

    -   Ihre DNS-Server sind für automatische Updates konfiguriert und unterstützen Ressourceneinträge zur Dienstidentifizierung.  

    -   Zu den angegebenen FQDNs für die Verwaltungspunkte in Configuration Manager müssen Hosteinträge (A- oder AAA-Datensätze) in DNS vorhanden sein.  

    > [!WARNING]  
    >  Damit in DNS veröffentlichte Verwaltungspunkte von Clients gefunden werden können, müssen Sie die Clients einem bestimmten Standort zuweisen (statt die automatische Standortzuweisung zu verwenden) und diese Clients für die Verwendung des Standortcodes mit dem Domänensuffix ihres Verwaltungspunkts konfigurieren. Weitere Informationen finden Sie im Abschnitt [Locating Management Points (Zuordnen von Verwaltungspunkten)](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_LocatingMPs) unter [How to assign clients to a site in System Center Configuration Manager (Zuweisen von Clients zu einem Standort in System Center Configuration Manager)](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

     Wenn es für Configuration Manager-Clients nicht möglich ist, Verwaltungspunkte mithilfe von Active Directory Domain Services oder DNS zu suchen, wird als Alternative [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins) verwendet. Der erste für einen Standort installierte Verwaltungspunkt wird automatisch in WINS veröffentlicht, wenn er für das Zulassen von HTTP-Clientverbindungen im Intranet konfiguriert wird.  

**Statusberichterstattung:**  

-   Diese Einstellungen dienen zum direkten Konfigurieren der Detailebene, die in Statusberichte von Standorten und Clients einbezogen wird.  

**E-Mail-Benachrichtigung:**  

-   Geben Sie Konto- und E-Mail-Serverdetails an, um Configuration Manager das Senden von E-Mail-Benachrichtigungen zu Warnungen zu ermöglichen.  

**Auswertung der Sammlungsmitgliedschaft:**  

-   Verwenden Sie diesen Task, um die Häufigkeit der inkrementellen Auswertung der Sammlungsmitgliedschaft festzulegen. Bei der inkrementellen Auswertung wird eine Sammlungsmitgliedschaft nur mit neuen oder geänderten Ressourcen aktualisiert.  

#### <a name="to-edit-the-site-components-at-a-site"></a>So bearbeiten Sie die Standortkomponenten auf einem Standort  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie den Standort mit den Standortkomponenten aus, die Sie konfigurieren möchten.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren** , und wählen Sie dann die Standortkomponente aus, die Sie konfigurieren möchten.  

##  <a name="a-namebkmkservicemgra-use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Verwalten von Standortkomponenten mit dem Dienst-Manager für Configuration Manager  
Mit dem Dienst-Manager für Configuration Manager können Sie Configuration Manager-Dienste steuern und den Status von Configuration Manager-Diensten oder -Arbeitsthreads (zusammen als Configuration Manager-Komponenten bezeichnet) anzeigen:  

-   Configuration Manager-Komponenten können auf beliebigen Standortsystemen ausgeführt werden.  

-   Die Verwaltung von Komponenten entspricht der Verwaltung von Diensten in Windows. Sie können Configuration Manager-Komponenten starten, beenden, anhalten, fortsetzen und abfragen.  

Ein Configuration Manager-Dienst wird bei von ihm angeforderten Aktionen ausgeführt (üblicherweise, wenn eine Konfigurationsdatei in die Eingangsbox einer Komponente geschrieben wird). Wenn Sie die an einem Vorgang beteiligten Komponenten identifizieren müssen, können Sie mithilfe des **Dienst-Managers für Configuration Manager** verschiedene Configuration Manager-Dienste und -Threads bearbeiten und die sich daraus ergebende Änderung im Verhalten von Configuration Manager anzeigen. Sie können beispielsweise Configuration Manager-Dienste einzeln beenden, bis eine bestimmte Reaktion beseitigt ist. So können Sie bestimmen, welcher Dienst das Verhalten verursacht.  

> [!TIP]  
>  Mithilfe des folgenden Verfahrens können Sie das Verhalten von Configuration Manager-Komponenten bearbeiten.  

#### <a name="to-use-the-configuration-manager-service-manager"></a>So verwenden Sie den Dienst-Manager für Configuration Manager  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung** >  **Systemstatus** und anschließend auf **Komponentenstatus**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Komponente** auf **Starten**, und wählen Sie dann **Dienst-Manager für Configuration Manager**aus.  

3.  Wenn der Dienst-Manager für Configuration Manager geöffnet wird, stellen Sie eine Verbindung mit dem zu verwaltenden Standort her.  

     Wenn der zu verwaltende Standort nicht angezeigt wird, klicken Sie auf **Standort**, klicken Sie auf **Verbinden**, und geben Sie dann den Namen des Standortservers für den gewünschten Standort ein.  

4.  Erweitern Sie den Standort, und wechseln Sie zu **Komponenten** oder **Server** , je nachdem, wo die zu verwaltenden Komponenten sich befinden.  

5.  Wählen Sie im rechten Bereich mindestens eine Komponente aus, und klicken Sie dann im Menü **Komponente** auf **Abfrage** , um den Status Ihrer Auswahl zu aktualisieren.  

6.  Nachdem der Status der Komponente aktualisiert wurde, verwenden Sie eine der vier aktionsbasierten Optionen im Menü **Komponente** , um das Verhalten der Komponente zu ändern. Nachdem eine Aktion angefordert wurde, müssen Sie die Komponente abfragen, um den neuen Status der Komponente anzuzeigen.  

7.  Schließen Sie den Dienst-Manager für Configuration Manager, wenn Sie das Bearbeiten des Betriebsstatus der Komponenten abgeschlossen haben.  



<!--HONumber=Dec16_HO3-->


