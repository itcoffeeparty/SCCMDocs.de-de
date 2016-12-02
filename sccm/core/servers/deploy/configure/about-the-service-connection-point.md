---
title: Dienstverbindungspunkt| System Center Configuration Manager
description: "Erfahren Sie mehr über diese Standortsystemrolle von Configuration Manager, und verstehen und planen Sie den Verwendungsbereich."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: 18
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e30c3d4bbf42e008a3f570c843b2f63251bce158


---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>Informationen zum Dienstverbindungspunkt in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Der System Center Configuration Manager-Dienstverbindungspunkt ist eine Standortsystemrolle, die mehrere wichtige Funktionen für die Hierarchie übernimmt. Bevor Sie den Dienstverbindungspunkt konfigurieren, sollten Sie seinen Verwendungsbereich verstehen und planen, da dies Auswirkungen auf die Konfiguration dieser Standortsystemrolle haben kann:  

-   **Verwalten mobiler Geräte mit Microsoft Intune** – Diese Rolle ersetzt den Windows Intune-Connector, der von früheren Configuration Manager-Versionen verwendet wurde, und kann mit Ihren Intune-Abonnementdetails konfiguriert werden. Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune](../../../../mdm/plan-design/hybrid-mobile-device-management.md).  

-   **Verwalten mobiler Geräte mit lokaler Verwaltung mobiler Geräte** – Diese Rolle bietet Unterstützung für lokale Geräte, die Sie verwalten, und die keine Verbindung mit dem Internet herstellen. Informationen finden Sie unter [Verwalten mobiler Geräte mithilfe lokaler Infrastruktur in System Center Configuration Manager](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

-   **Hochladen von Nutzungsdaten aus Ihrer Configuration Manager-Infrastruktur** – Sie können die Ebene, oder die Menge der hochgeladenen Details steuern. Hochgeladene Daten geben uns folgende Möglichkeiten:  

    -   Proaktives Erkennen und Beheben von Problemen  

    -   Verbesserung unserer Produkte und Dienste  

    -   Ermitteln von Updates für Configuration Manager, die für die von Ihnen verwendete Configuration Manager-Version gelten  

     Siehe [Usage data levels and settings](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

-   **Herunterladen von Updates, die auf Ihre Configuration Manager-Infrastruktur zutreffen** – Auf Grundlage der von Ihnen hochgeladenen Nutzungsdaten werden nur Updates verfügbar gemacht, die für Ihre Infrastruktur relevant sind.  

 **Jede Hierarchie unterstützt eine einzelne Instanz dieser Rolle:**  

-   Die Standortsystemrolle kann nur am Standort der obersten Ebene Ihrer Hierarchie (einem Standort der zentralen Verwaltung oder dem eigenständigen primären Standort) installiert werden.  

-   Wenn Sie einen eigenständigen primären Standort in eine größere Hierarchie erweitern, müssen Sie diese Rolle am primären Standort deinstallieren und können sie dann am Standort der zentralen Verwaltung installieren.  

##  <a name="a-namebkmkmodesa-modes-of-operation"></a><a name="bkmk_modes"></a> Betriebsmodi  
 Der Dienstverbindungspunkt unterstützt zwei Betriebsmodi:  

-   Im **Onlinemodus**sucht der Dienstverbindungspunkt automatisch alle 24 Stunden nach Updates und lädt dann neue Updates herunter, die für Ihre aktuelle Infrastruktur und Produktversion verfügbar sind, und stellt sie in der Configuration Manager-Konsole bereit.  

-   Im **Offlinemodus** stellt der Dienstverbindungspunkt keine Verbindung mit dem Microsoft-Clouddienst her, und Sie müssen das [Dienstverbindungstool für System Center Configuration Manager](../../../../core/servers/manage/use-the-service-connection-tool.md) manuell ausführen, um verfügbare Updates zu importieren.  

Wenn Sie den Modus zwischen online oder offline wechseln möchten, nachdem Sie den Dienstverbindungspunkt installiert haben, müssen Sie anschließend den SMS_DMP_DOWNLOADER-Thread des SMS_Executive-Diensts von Configuration Manager neu starten, damit diese Änderung wirksam wird.  Verwenden Sie hierzu den Dienst-Manager von Configuration Manager, um nur den SMS_DMP_DOWNLOADER-Thread des SMS_Executive-Diensts neu zu starten.  Sie können auch den SMS_Executive-Dienst für Configuration Manager neu starten (wodurch die meisten Standortkomponenten neu gestartet werden) oder auf einen Zeitplantask wie z.B. eine Standortsicherung warten, der beendet wird und später SMS_Executive für Sie neu startet.  

Wechseln Sie zum Verwenden des Dienst-Managers von Configuration Manager in der Konsole zu **Überwachung** > **Systemstatus** > **Komponentenstatus**, klicken Sie auf **Starten**, und wählen Sie anschließend **Configuration Manager Service Manager** (Service Manager von Configuration Manager) aus.  Gehen Sie in Service Manager folgendermaßen vor:  

-   Erweitern Sie im Navigationsbereich den Standort und dann **Komponenten**, und wählen Sie anschließend die Komponente aus, die neu gestartet werden soll.  

-   Klicken Sie im Detailbereich mit der rechten Maustaste auf die Komponente, und wählen Sie **Abfrage** aus.  

-   Wenn der Status der Komponente bestätigt wurde, klicken Sie erneut mit der rechten Maustaste auf die Komponente, und wählen Sie **Beenden**.  

-   Führen Sie die **Abfrage** für die Komponente erneut aus, um sicherzustellen, dass sie beendet wurde, und klicken Sie anschließend mit der rechten Maustaste noch einmal auf die Komponente, und wählen Sie **Starten**.  

> [!IMPORTANT]  
>  Beim Hinzufügen eines Microsoft Intune-Abonnements für den Dienstverbindungspunkt wird die Standortsystemrolle automatisch auf „Online“ festgelegt. Bei einer Konfiguration mit einem Intune-Abonnement unterstützt der Dienstverbindungspunkt den Offlinemodus nicht.  

**Wenn die Rolle auf einem Computer installiert wird, der sich an einem vom Standortserver entfernten Ort befindet:**  

-   Sie müssen den Standortsystemserver, der die Rolle hostet, mit einem Standortsystem-Installationskonto konfigurieren.  

-   Das Standortsystem-Installationskonto wird vom Verteilungs-Manager auf dem Standortserver zum Übertragen von Updates vom Dienstverbindungspunkt verwendet.  

##  <a name="a-namebkmkurlsa-internet-access-requirements"></a><a name="bkmk_urls"></a> Erforderliche Berechtigungen für den Internetzugriff  
Der Computer, der den Dienstverbindungspunkt und alle Firewalls zwischen dem Computer und dem Internet hostet, muss die Kommunikation über den **Port TCP 443** an die folgenden Internet-URLs übergeben, um den Vorgang zu aktivieren. Der Dienstverbindungspunkt unterstützt auch Webproxys (mit oder ohne Authentifizierung) für den Zugriff auf diese URLs.  

**Updates und Wartung**  

-   *.akamaiedge.net  

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *manage.microsoft.com  
-   https://bspmts.mp.microsoft.com/V
-   https://login.microsoftonline.com/{TenantID}


**Windows 10-Wartung**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  



<!--HONumber=Nov16_HO1-->


