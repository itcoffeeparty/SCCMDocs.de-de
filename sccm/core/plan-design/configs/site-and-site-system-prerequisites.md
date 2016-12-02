---
title: "Voraussetzungen für Standorte | System Center Configuration Manager"
description: Erfahren Sie, wie ein Windows-Computer als System Center Configuration Manager-Standortsystemserver konfiguriert wird.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f24fd912b3e65dc0c0074ef1c8f76cc128a716c

---
# <a name="site-and-site-system-prerequisites-for-system-center-configuration-manager"></a>Voraussetzungen für Standorte und Standortsysteme für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 Der Einsatz von Windows-Computern als System Center Configuration Manager-Standortsystemserver setzt bestimmte Konfigurationen voraus.  


 Bei einigen Produkten wie Windows Server Update Services (WSUS) für den Softwareupdatepunkt finden Sie Informationen zu weiteren Voraussetzungen und Einschränkungen zur Nutzung des Produkts in der Dokumentation zum jeweiligen Produkt. Hier werden nur Konfigurationen beschrieben, die sich direkt auf die Verwendung mit Configuration Manager beziehen.   

> [!NOTE]  
>  Unterstützung für .NET 4.0, 4.5 und 4.5.1 läuft ab am 12. Januar 2016. Weitere Informationen finden Sie im Artikel [FAQ zur Lifecycle Support-Richtlinie – Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) unter „support.microsoft.com“.  

## <a name="a-namebkmkgeneralprerewqa-general-site-server-requierments-and-limitations"></a><a name="bkmk_generalprerewq"></a> Allgemeine Anforderungen und Einschränkungen für den Standortserver:
**Folgendes gilt für alle Standortsystemserver:**

-   Jeder Standortsystemserver muss ein 64-Bit-Betriebssystem verwenden. Die einzige Ausnahme gilt für die Standortsystemrolle „Verteilungspunkt“, die unter manchen 32-Bit-Betriebssystemen installiert werden kann.  

-   Standortsysteme werden unter keinem Betriebssystem auf Server Core-Installationen unterstützt. Eine Ausnahme ist, dass Server Core-Installationen für Verteilungspunkt-Standortsystemrollen ohne PXE- oder Multicast-Unterstützung unterstützt werden.  

-   Nach der Installation eines Standortsystemservers können folgende Elemente nicht geändert werden:  

    -   Der Domänenname der Domäne, in der sich der Standortsystemcomputer befindet (wird auch als **Domänenumbenennung** bezeichnet)  

    -   Die Domänenmitgliedschaft des Computers  

    -   Name des Computers  

  Um eines dieser Elemente zu ändern, müssen Sie zuerst die Standortsystemrolle vom Computer entfernen und die Rolle nach der Änderung erneut installieren. Falls sich dies auf den Standortservercomputer auswirkt, müssen Sie den Standort deinstallieren und nach der Änderung erneut installieren.  

-   Standortsystemrollen werden auf Instanzen von Windows Server-Clustern nicht unterstützt. Die einzige Ausnahme gilt für den Standortdatenbankserver.  

-   Die Änderung der Einstellungen für Starttyp und „Anmelden als“ für beliebige Configuration Manager-Dienste wird nicht unterstützt. Wenn Sie die Einstellungen trotzdem ändern, werden wichtige Dienste möglicherweise nicht ordnungsgemäß ausgeführt.  

##  <a name="a-namebkmk2012prereqa-prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Voraussetzungen für Windows Server 2012 und höhere Betriebssysteme  
###  <a name="a-namebkmk2012sspreqa-site-server---central-administration-site-and-primary-site"></a><a name="bkmk_2012sspreq"></a> Standortserver – Standort der zentralen Verwaltung und primärer Standort  
  **Windows Server-Rollen und -Features:**  

-   .NET Framework 3.5 SP1 (oder höher)  

-   .NET Framework 4.5.2  

-   Remotedifferenzialkomprimierung  

**Windows ADK:**  

-   Bevor Sie einen Standort der zentralen Verwaltung oder einen primären Standort installieren oder aktualisieren, müssen Sie die Version von Windows ADK installieren, die die Version von Configuration Manager erfordert, die Sie installieren oder aktualisieren.  

    -   Die 1511-Version von Configuration Manager erfordert die Win10 RTM-Version (10.0.10240) von Windows ADK.  

-   Weitere Informationen zu dieser Anforderung finden Sie unter „Betriebssystembereitstellung“.  

**Visual C++ Redistributable:**  

-   Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable auf jedem Computer, auf dem ein Standortserver installiert wird.  

-   Standorte der zentralen Verwaltung und primäre Standorte erfordern sowohl die x86- als auch die x64-Version der betreffenden Redistributable-Datei.  

###  <a name="a-namebkmk2012secpreqa-site-server--secondary-site"></a><a name="bkmk_2012secpreq"></a> Standortserver – sekundärer Standort  
**Windows Server-Rollen und -Features:**  

-   .NET Framework 3.5 SP1 (oder höher)  

-   .NET Framework 4.5.2  

-   Remotedifferenzialkomprimierung  

**Visual C++ Redistributable:**  

-   Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable auf jedem Computer, auf dem ein Standortserver installiert wird.  

-   Sekundäre Standorte erfordern nur die x64-Version.  

**Standard-Standortsystemrollen:**  

-   Standardmäßig werden von einem sekundären Standort ein **Verwaltungspunkt** und ein **Verteilungspunkt** installiert.  

-   Stellen Sie sicher, dass der sekundäre Standortserver die Voraussetzungen für diese Standortsystemrollen erfüllt.  

###  <a name="a-namebkmk2012dbpreqa-database-server"></a><a name="bkmk_2012dbpreq"></a> Datenbankserver  
**Remoteregistrierungsdienst:**  

-   Während der Installation des Configuration Manager-Standorts muss der Remoteregistrierungsdienst auf dem Computer aktiviert sein, auf dem die Standortdatenbank gehostet wird.  

 **SQL Server**  

-   Bevor Sie einen Standort der zentralen Verwaltung oder einen primären Standort installieren, müssen Sie eine unterstützte Version von SQL Server zum Hosten der Standortdatenbank installieren.  

-   Bevor Sie einen sekundären Standort installieren, können Sie eine unterstützte Version von SQL Server installieren.  

-   Wenn Sie entscheiden, dass Configuration Manager im Rahmen der Installation des sekundären Standorts SQL Server Express installieren soll, stellen Sie sicher, dass der Computer die Voraussetzungen zur Ausführung von SQL Server Express erfüllt.  

###  <a name="a-namebkmk2012smsprovpreqa-sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> SMS-Anbieterserver  
**Windows ADK:**  

-   Auf dem Computer, auf dem Sie eine Instanz des SMS-Anbieters installieren, muss die Version von Windows ADK installiert sein, die für die von Ihnen installierte bzw. aktualisierte Version von Configuration Manager erforderlich ist.  

    -   Die 1511-Version von Configuration Manager erfordert die Win10 RTM-Version (10.0.10240) von Windows ADK.  

-   Weitere Informationen zu dieser Anforderung finden Sie unter „Betriebssystembereitstellung“.  

###  <a name="a-namebkmk2012acwspreqa-application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a> Anwendungskatalog-Websitepunkt  
**Windows Server-Rollen und -Features:**  

-   .NET Framework 3.5 SP1 (oder höher)  

-   .NET Framework 4.5.2  

    -   ASP.NET 4.5  

**IIS-Konfiguration:**  

-   Allgemeine HTTP-Features:  

    -   Standarddokument  

    -   Statischer Inhalt  

-   Anwendungsentwicklung:  

    -   ASP.NET 3.5 (und automatisch ausgewählte Optionen)  

    -   ASP.NET 4.5 (und automatisch ausgewählte Optionen)  

    -   .NET-Erweiterbarkeit 3.5  

    -   .NET-Erweiterbarkeit 4.5  

-   Sicherheit:  

    -   Windows-Authentifizierung  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

###  <a name="a-namebkmk2012acwsitepreqa-application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a> Anwendungskatalog-Webdienstpunkt  
**Windows Server-Rollen und -Features:**  

-   .NET Framework 3.5 SP1 (oder höher)  

-   .NET Framework 4.5.2  

    -   ASP.NET 4.5  

        -   HTTP-Aktivierung (und automatisch ausgewählte Optionen)  

**IIS-Konfiguration:**  

-   Allgemeine HTTP-Features:  

    -   Standarddokument  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

-   Anwendungsentwicklung:  

    -   ASP.NET 3.5 (und automatisch ausgewählte Optionen)  

    -   .NET-Erweiterbarkeit 3.5  

    -   ASP.NET 4.5 (und automatisch ausgewählte Optionen)  

    -   .NET-Erweiterbarkeit 4.5  

**Arbeitsspeicher:**  

-   Auf dem Computer, der diese Standortsystemrolle hostet, müssen mindestens 5 % Speicher frei sein, um die Verarbeitung von Anforderungen durch die Standortsystemrolle zu ermöglichen.  

-   Wenn diese Standortsystemrolle zusammen mit einer anderen Standortsystemrolle installiert wird, für die dieselbe Anforderung gilt, wird die Speicheranforderung für den Computer nicht erhöht, die Mindestanforderung von 5 % besteht jedoch weiter.  

###  <a name="a-namebkmk2012aipreqa-asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a> Asset Intelligence-Synchronisierungspunkt  
**Windows Server-Rollen und -Features:**  

-   .NET Framework 4.5.2  

###  <a name="a-namebkmk2012crppreqa-certificate-registration-point"></a><a name="bkmk_2012crppreq"></a> Zertifikatregistrierungspunkt  
**Windows Server-Rollen und -Features:**  

-   .NET Framework 4.5.2  

    -   HTTP-Aktivierung  

**IIS-Konfiguration:**  

-   Anwendungsentwicklung:  

    -   ASP.NET 3.5 (und automatisch ausgewählte Optionen)  

    -   ASP.NET 4.5 (und automatisch ausgewählte Optionen)  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

    -   IIS 6-WMI-Kompatibilität  

###  <a name="a-namebkmk2012dppreqa-distribution-point"></a><a name="bkmk_2012dppreq"></a> Verteilungspunkt  
**Windows Server-Rollen und -Features:**  

-   Remotedifferenzialkomprimierung  

**IIS-Konfiguration:**  

-   Anwendungsentwicklung:  

    -   ISAPI-Erweiterungen  

-   Sicherheit:  

    -   Windows-Authentifizierung  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

    -   IIS 6-WMI-Kompatibilität  

**PowerShell:**  

-   Unter Windows Server 2012 oder höher ist PowerShell 3.0 oder 4.0 vor der Installation des Verteilungspunkts erforderlich.  

**Visual C++ Redistributable:**  

-   Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable auf jedem Computer, auf dem ein Verteilungspunkt gehostet wird.  

-   Welche Version installiert wird, hängt von der Computerplattform (x86 oder x64) ab.  

**Microsoft Azure:**  

-   Sie können einen Clouddienst in Microsoft Azure verwenden, um einen Verteilungspunkt zu hosten.  

**So unterstützen Sie PXE oder Multicast:**  

-   Installieren und konfigurieren Sie die Windows-Rolle „Windows-Bereitstellungsdienste“ (Windows Deployment Services, WDS).  

    > [!NOTE]  
    >  WDS wird automatisch installiert und konfiguriert, wenn Sie einen Verteilungspunkt zur Unterstützung von PXE oder Multicast auf einem Server konfigurieren, der Windows Server 2012 oder höher ausführt.  

> [!NOTE]  
>  Die Standortsystemrolle „Verteilungspunkt“ erfordert keinen intelligenten Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS). Wenn BITS auf dem Verteilungspunktcomputer konfiguriert ist, wird BITS auf diesem Computer nicht verwendet, um BITS-Clients den Download von Inhalten zu erleichtern.  

###  <a name="a-namebkmk2012epppreqa-endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Endpoint Protection-Punkt  
**Windows Server-Rollen und -Features:**  

-   .NET Framework 3.5 SP1 (oder höher)  

###  <a name="a-namebkmk2012enrollpreqa-enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a> Anmeldungspunkt  
**Windows Server-Rollen und -Features:**  

-   Mindestens .NET Framework 3.5  

-   .NET Framework 4.5.2  

     Bei der Installation diese Standortsystemrolle installiert Configuration Manager automatisch .NET Framework 4.5.2. Diese Installation kann den Server in den Status „Ausstehender Neustart“ setzen. Wenn für .NET Framework ein Neustart aussteht, können .NET-Anwendungen möglicherweise erst nach dem Neustart des Servers und dem Abschluss der Installation ausgeführt werden.  

    -   HTTP-Aktivierung (und automatisch ausgewählte Optionen)  

    -   ASP.NET 4.5  


**IIS-Konfiguration:**  

-   Allgemeine HTTP-Features:  

    -   Standarddokument  

-   Anwendungsentwicklung:  

    -   ASP.NET 3.5 (und automatisch ausgewählte Optionen)  

    -   .NET-Erweiterbarkeit 3.5  

    -   ASP.NET 4.5 (und automatisch ausgewählte Optionen)  

    -   .NET-Erweiterbarkeit 4.5  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

**Arbeitsspeicher:**  

-   Auf dem Computer, der diese Standortsystemrolle hostet, müssen mindestens 5 % Speicher frei sein, um die Verarbeitung von Anforderungen durch die Standortsystemrolle zu ermöglichen.  

-   Wenn diese Standortsystemrolle zusammen mit einer anderen Standortsystemrolle installiert wird, für die dieselbe Anforderung gilt, wird die Speicheranforderung für den Computer nicht erhöht, die Mindestanforderung von 5 % besteht jedoch weiter.  

###  <a name="a-namebkmk2012enrollproxpreqa-enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a> Anmeldungsproxypunkt  
**Windows Server-Rollen und -Features:**  

-   Mindestens .NET Framework 3.5  

-   .NET Framework 4.5.2  

     Bei der Installation diese Standortsystemrolle installiert Configuration Manager automatisch .NET Framework 4.5.2. Diese Installation kann den Server in den Status „Ausstehender Neustart“ setzen. Wenn für .NET Framework ein Neustart aussteht, können .NET-Anwendungen möglicherweise erst nach dem Neustart des Servers und dem Abschluss der Installation ausgeführt werden.  

**IIS-Konfiguration:**  

-   Allgemeine HTTP-Features:  

    -   Standarddokument  

    -   Statischer Inhalt  

-   Anwendungsentwicklung:  

    -   ASP.NET 3.5 (und automatisch ausgewählte Optionen)  

    -   ASP.NET 4.5 (und automatisch ausgewählte Optionen)  

    -   .NET-Erweiterbarkeit 3.5  

    -   .NET-Erweiterbarkeit 4.5  

-   Sicherheit:  

    -   Windows-Authentifizierung  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

**Arbeitsspeicher:**  

-   Auf dem Computer, der diese Standortsystemrolle hostet, müssen mindestens 5 % Speicher frei sein, um die Verarbeitung von Anforderungen durch die Standortsystemrolle zu ermöglichen.  

-   Wenn diese Standortsystemrolle zusammen mit einer anderen Standortsystemrolle installiert wird, für die dieselbe Anforderung gilt, wird die Speicheranforderung für den Computer nicht erhöht, die Mindestanforderung von 5 % besteht jedoch weiter.  

###  <a name="a-namebkmk2012fsppreqa-fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a> Fallbackstatuspunkt  
**Die IIS-Standardkonfiguration mit den folgenden Ergänzungen ist erforderlich:**  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

###  <a name="a-namebkmk2012mppreqa-management-point"></a><a name="bkmk_2012MPpreq"></a> Verwaltungspunkt  
**Windows Server-Rollen und -Features:**  

-   .NET Framework 4.5.2  

-   BITS-Servererweiterungen (und automatisch ausgewählte Optionen) oder intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS) (und automatisch ausgewählte Optionen)  

**IIS-Konfiguration:**  

-   Anwendungsentwicklung:  

    -   ISAPI-Erweiterungen  

-   Sicherheit:  

    -   Windows-Authentifizierung  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

    -   IIS 6-WMI-Kompatibilität  

###  <a name="a-namebkmk2012rspointa-reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> Reporting Services-Punkt  
**Windows Server-Rollen und -Features:**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services:**  

-   Sie müssen zur Unterstützung von SQL Server Reporting Services vor dem Installieren des Reporting Services-Punkts mindestens eine SQL Server-Instanz installieren und konfigurieren.  

-   Sie können für SQL Server Reporting Services die gleiche Instanz wie für die Standortdatenbank verwenden.  

-   Darüber hinaus kann die verwendete Instanz für andere System Center-Produkte freigegeben werden, solange die anderen System Center-Produkte keiner Einschränkung für die Freigabe von SQL Server-Instanzen unterliegen.  

###  <a name="a-namebkmkscppreqa-service-connection-point"></a><a name="bkmk_SCPpreq"></a> Dienstverbindungspunkt  
**Windows Server-Rollen und -Features:**  

-   .NET Framework 4.5.2  

     Bei der Installation diese Standortsystemrolle installiert Configuration Manager automatisch .NET Framework 4.5.2. Diese Installation kann den Server in den Status „Ausstehender Neustart“ setzen. Wenn für .NET Framework ein Neustart aussteht, können .NET-Anwendungen möglicherweise erst nach dem Neustart des Servers und dem Abschluss der Installation ausgeführt werden.  

**Visual C++ Redistributable:**  

-   Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable auf jedem Computer, auf dem ein Verteilungspunkt gehostet wird.  

-   Die Standortsystemrolle erfordert die x64-Version.  

###  <a name="a-namebkmk2012suppreqa-software-update-point"></a><a name="bkmk_2012SUPpreq"></a> Softwareupdatepunkt  
**Windows Server-Rollen und -Features:**  

-   .NET Framework 3.5 SP1 (oder höher)  

-   .NET Framework 4.5.2  

**Die IIS-Standardkonfiguration ist erforderlich.**  

**Windows Server Update Services:**  

-   Sie müssen die Windows-Serverrolle Windows Server Update Services auf einem Computer installieren, bevor Sie einen Softwareupdatepunkt installieren.  

-   Weitere Informationen finden Sie unter [Planen von Softwareupdates in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Zustandsmigrationspunkt  
**Die IIS-Standardkonfiguration ist erforderlich.**  

##  <a name="a-namebkmk2008a-prerequisites-for-windows-server-2008-r2-and-windows-server-2008"></a><a name="bkmk_2008"></a> Voraussetzungen für Windows Server 2008 R2 und Windows Server 2008  
Windows Server 2008 und Windows Server 2008 R2 unterliegen nun dem erweiterten Support und nicht mehr dem grundlegenden Support, wie in [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) ausführlich erläutert. Weitere Informationen zur Featureunterstützung für diese Betriebssysteme als Standortsysteme mit Configuration Manager finden Sie unter [Entfernte und veraltete Features für System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**Folgendes gilt für alle .NET Framework-Anforderungen:**  

-   Installieren Sie die Vollversion von Microsoft .NET Framework, bevor Sie die Standortsystemrollen installieren. Sie können diese beispielsweise unter [Microsoft .NET Framework 4 (eigenständiger Installer)](http://go.microsoft.com/fwlink/p/?LinkId=193048) herunterladen. Microsoft.NET Framework 4 Client Profile ist für diese Anforderung unzureichend.  

**Folgendes gilt für alle Anforderungen zur Aktivierung von Windows Communication Foundation (WCF):**  

-   Sie können die WCF-Aktivierung als Bestandteil des Windows-Features .NET Framework auf dem Standortsystemserver konfigurieren. Führen Sie beispielsweise unter Windows Server 2008 R2 den **Assistenten zum Hinzufügen von Features** aus, um weitere Features auf dem Server zu installieren. Erweitern Sie auf der Seite **Features auswählen** den Knoten **.NET Framework 3.5.1-Features** und anschließend den Knoten **WCF-Aktivierung**, und aktivieren Sie anschließend die Kontrollkästchen für **HTTP-Aktivierung** und **Nicht-HTTP-Aktivierung**, um diese Optionen zu aktivieren.  

###  <a name="a-namebkmk2008sspreqa-site-server---central-administration-site-and-primary-site"></a><a name="bkmk_2008sspreq"></a> Standortserver – Standort der zentralen Verwaltung und primärer Standort  
**.NET Framework:**  

-   3.5 SP1 (oder höher)  

-   .NET Framework 4.5.2  

**Windows-Feature:**  

-   Remotedifferenzialkomprimierung  

**Windows ADK:**  

-   Bevor Sie einen Standort der zentralen Verwaltung oder einen primären Standort installieren oder aktualisieren, müssen Sie die Version von Windows ADK installieren, die die Version von Configuration Manager erfordert, die Sie installieren oder aktualisieren.  

    -   Die 1511-Version von Configuration Manager erfordert die Win10 RTM-Version (10.0.10240) von Windows ADK.  

-   Weitere Informationen zu dieser Anforderung finden Sie unter „Betriebssystembereitstellung“.  

**Visual C++ Redistributable:**  

-   Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable auf jedem Computer, auf dem ein Standortserver installiert wird.  

-   Standorte der zentralen Verwaltung und primäre Standorte erfordern sowohl die x86- als auch die x64-Version der betreffenden Redistributable-Datei.  

###  <a name="a-namebkmk2008secpreqa-site-server--secondary-site"></a><a name="bkmk_2008secpreq"></a> Standortserver – sekundärer Standort  
**.NET Framework:**  

-   3.5 SP1 (oder höher)  

-   .NET Framework 4.5.2  

**Visual C++ Redistributable:**  

-   Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable auf jedem Computer, auf dem ein Standortserver installiert wird.  

-   Sekundäre Standorte erfordern nur die x64-Version.  

**Standard-Standortsystemrollen:**  

-   Standardmäßig werden von einem sekundären Standort ein **Verwaltungspunkt** und ein **Verteilungspunkt** installiert.  

-   Stellen Sie sicher, dass der sekundäre Standortserver die Voraussetzungen für diese Standortsystemrollen erfüllt.  

###  <a name="a-namebkmk2008dbpreqa-database-server"></a><a name="bkmk_2008dbpreq"></a> Datenbankserver  
**Remoteregistrierungsdienst:**  

-   Während der Installation des Configuration Manager-Standorts muss der Remoteregistrierungsdienst auf dem Computer aktiviert sein, auf dem die Standortdatenbank gehostet wird.  

**SQL Server**  

-   Bevor Sie einen Standort der zentralen Verwaltung oder einen primären Standort installieren, müssen Sie eine unterstützte Version von SQL Server zum Hosten der Standortdatenbank installieren.  

-   Bevor Sie einen sekundären Standort installieren, können Sie eine unterstützte Version von SQL Server installieren.  

-   Wenn Sie entscheiden, dass Configuration Manager im Rahmen der Installation des sekundären Standorts SQL Server Express installieren soll, stellen Sie sicher, dass der Computer die Voraussetzungen zur Ausführung von SQL Server Express erfüllt.  

###  <a name="a-namebkmk2008smsprovpreqa-sms-provider-server"></a><a name="bkmk_2008smsprovpreq"></a> SMS-Anbieterserver  
**Windows ADK:**  

-   Auf dem Computer, auf dem Sie eine Instanz des SMS-Anbieters installieren, muss die Version von Windows ADK installiert sein, die für die von Ihnen installierte bzw. aktualisierte Version von Configuration Manager erforderlich ist.  

    -   Die 1511-Version von Configuration Manager erfordert die Win10 RTM-Version (10.0.10240) von Windows ADK.  

-   Weitere Informationen zu dieser Anforderung finden Sie unter „Betriebssystembereitstellung“.  

###  <a name="a-namebkmk2008acwspreqa-application-catalog-website-point"></a><a name="bkmk_2008acwspreq"></a> Anwendungskatalog-Websitepunkt  
**.NET Framework:**  

-   .NET Framework 4.5.2  

**IIS-Konfiguration**: Die IIS-Standardkonfiguration mit den folgenden Ergänzungen ist erforderlich:  

-   Allgemeine HTTP-Features:  

    -   Statischer Inhalt  

    -   Standarddokument  

-   Anwendungsentwicklung:  

    -   ASP.NET (und automatisch ausgewählte Optionen)  

         In einigen Szenarios, wenn z.B. IIS nach der Installation von .NET Framework 4.5.2 installiert oder umkonfiguriert wird, müssen Sie ASP.NET 4.5 ausdrücklich aktivieren. Führen Sie auf einem 64-Bit-Computer, auf dem .NET Framework 4.0.30319 ausgeführt wird, z.B. den folgenden Befehl aus: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**.  

-   Sicherheit:  

    -   Windows-Authentifizierung  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

###  <a name="a-namebkmk2008acwsitepreqa-application-catalog-web-service-point"></a><a name="bkmk_2008ACwsitepreq"></a> Anwendungskatalog-Webdienstpunkt  
**.NET Framework:**  

-   3.5 SP1 (oder höher)  

-   .NET Framework 4.5.2  

**Aktivierung von Windows Communication Foundation (WCF):**  

-   HTTP-Aktivierung  

-   Nicht-HTTP-Aktivierung  

**IIS-Konfiguration**: Die IIS-Standardkonfiguration mit den folgenden Ergänzungen ist erforderlich:  

-   Anwendungsentwicklung:  

    -   ASP.NET (und automatisch ausgewählte Optionen)  

         In einigen Szenarios, wenn z.B. IIS nach der Installation von .NET Framework 4.5.2 installiert oder umkonfiguriert wird, müssen Sie ASP.NET 4.5 ausdrücklich aktivieren. Führen Sie auf einem 64-Bit-Computer, auf dem .NET Framework 4.0.30319 ausgeführt wird, z.B. den folgenden Befehl aus: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**.  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

**Arbeitsspeicher:**  

-   Auf dem Computer, der diese Standortsystemrolle hostet, müssen mindestens 5 % Speicher frei sein, um die Verarbeitung von Anforderungen durch die Standortsystemrolle zu ermöglichen.  

-   Wenn diese Standortsystemrolle zusammen mit einer anderen Standortsystemrolle installiert wird, für die dieselbe Anforderung gilt, wird die Speicheranforderung für den Computer nicht erhöht, die Mindestanforderung von 5 % besteht jedoch weiter.  

###  <a name="a-namebkmk2008aipreqa-asset-intelligence-synchronization-point"></a><a name="bkmk_2008AIpreq"></a> Asset Intelligence-Synchronisierungspunkt  
**.NET Framework:**  

-   .NET Framework 4.5.2  

###  <a name="a-namebkmk2008crppreqa-certificate-registration-point"></a><a name="bkmk_2008crppreq"></a> Zertifikatregistrierungspunkt  
**.NET Framework:**  

-   .NET Framework 4.5.2  

-   HTTP-Aktivierung  

**IIS-Konfiguration**: Die IIS-Standardkonfiguration mit den folgenden Ergänzungen ist erforderlich:  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

    -   IIS 6-WMI-Kompatibilität  

###  <a name="a-namebkmk2008dppreqa-distribution-point"></a><a name="bkmk_2008dppreq"></a> Verteilungspunkt  
**IIS-Konfiguration:** Sie können die IIS-Standardkonfiguration oder eine benutzerdefinierte Konfiguration verwenden.  Sie müssen die folgenden Optionen für IIS aktivieren, um eine benutzerdefinierte IIS-Konfiguration verwenden zu können:  

-   Anwendungsentwicklung:  

    -   ISAPI-Erweiterungen  

-   Sicherheit:  

    -   Windows-Authentifizierung  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

    -   IIS 6-WMI-Kompatibilität  

Wenn Sie eine benutzerdefinierte IIS-Konfiguration verwenden, können Sie nicht benötigte Optionen entfernen, darunter die folgenden:  

-   Allgemeine HTTP-Features:  

    -   HTTP-Umleitung  

-   IIS-Verwaltungsskripts und -tools  

**Windows-Feature:**  

-   Remotedifferenzialkomprimierung  

**Visual C++ Redistributable:**  

-   Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable auf jedem Computer, auf dem ein Verteilungspunkt gehostet wird.  

-   Welche Version installiert wird, hängt von der Computerplattform (x86 oder x64) ab.  

**Microsoft Azure:**  

-   Sie können einen Clouddienst in Microsoft Azure verwenden, um einen Verteilungspunkt zu hosten.  

**So unterstützen Sie PXE oder Multicast:**  

-   Installieren und konfigurieren Sie die Windows-Rolle „Windows-Bereitstellungsdienste“ (Windows Deployment Services, WDS).  

    > [!NOTE]  
    >  WDS wird automatisch installiert und konfiguriert, wenn Sie einen Verteilungspunkt zur Unterstützung von PXE oder Multicast auf einem Server konfigurieren, der Windows Server 2012 oder höher ausführt.  

> [!NOTE]  
>  Die Standortsystemrolle „Verteilungspunkt“ erfordert keinen intelligenten Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS). Wenn BITS auf dem Verteilungspunktcomputer konfiguriert ist, wird BITS auf diesem Computer nicht verwendet, um BITS-Clients den Download von Inhalten zu erleichtern.  


###  <a name="a-namebkmk2008epppreqa-endpoint-protection-point"></a><a name="bkmk_2008EPPpreq"></a> Endpoint Protection-Punkt  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (oder höher)  

###  <a name="a-namebkmk2008enrollpreqa-enrollment-point"></a><a name="bkmk_2008Enrollpreq"></a> Anmeldungspunkt  
**.NET Framework:**  

-   4.5.2  

     Wenn diese Standortsystemrolle installiert wird, installiert der Configuration Manager automatisch .NET Framework 4.5.2, wenn auf dem Server nicht bereits eine unterstützte Version von .NET Framework installiert ist. Diese Installation kann den Server in den Status „Ausstehender Neustart“ setzen. Wenn für .NET Framework ein Neustart aussteht, können .NET-Anwendungen möglicherweise erst nach dem Neustart des Servers und dem Abschluss der Installation ausgeführt werden.  

**Aktivierung von Windows Communication Foundation (WCF):**  

-   HTTP-Aktivierung  

-   Nicht-HTTP-Aktivierung  

**IIS-Konfiguration**: Die IIS-Standardkonfiguration mit den folgenden Ergänzungen ist erforderlich:  

-   Anwendungsentwicklung:  

    -   ASP.NET (und automatisch ausgewählte Optionen)  

         In einigen Szenarios, wenn z.B. IIS nach der Installation von .NET Framework 4.5.2 installiert oder umkonfiguriert wird, müssen Sie ASP.NET 4.5 ausdrücklich aktivieren. Führen Sie auf einem 64-Bit-Computer, auf dem .NET Framework 4.0.30319 ausgeführt wird, z.B. den folgenden Befehl aus: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**.  

**Arbeitsspeicher:**  

-   Auf dem Computer, der diese Standortsystemrolle hostet, müssen mindestens 5 % Speicher frei sein, um die Verarbeitung von Anforderungen durch die Standortsystemrolle zu ermöglichen.  

-   Wenn diese Standortsystemrolle zusammen mit einer anderen Standortsystemrolle installiert wird, für die dieselbe Anforderung gilt, wird die Speicheranforderung für den Computer nicht erhöht, die Mindestanforderung von 5 % besteht jedoch weiter.  

###  <a name="a-namebkmk2008enrollproxpreqa-enrollment-proxy-point"></a><a name="bkmk_2008EnrollProxpreq"></a> Anmeldungsproxypunkt  
**.NET Framework:**  

-   4.5.2  

     Wenn diese Standortsystemrolle installiert wird, installiert der Configuration Manager automatisch .NET Framework 4.5.2, wenn auf dem Server nicht bereits eine unterstützte Version von .NET Framework installiert ist. Diese Installation kann den Server in den Status „Ausstehender Neustart“ setzen. Wenn für .NET Framework ein Neustart aussteht, können .NET-Anwendungen möglicherweise erst nach dem Neustart des Servers und dem Abschluss der Installation ausgeführt werden.  

**Aktivierung von Windows Communication Foundation (WCF):**  

-   HTTP-Aktivierung  

-   Nicht-HTTP-Aktivierung  

**IIS-Konfiguration**: Die IIS-Standardkonfiguration mit den folgenden Ergänzungen ist erforderlich:  

-   Anwendungsentwicklung:  

    -   ASP.NET (und automatisch ausgewählte Optionen)  

         In einigen Szenarios, wenn z.B. IIS nach der Installation von .NET Framework 4.5.2 installiert oder umkonfiguriert wird, müssen Sie ASP.NET 4.5 ausdrücklich aktivieren. Führen Sie auf einem 64-Bit-Computer, auf dem .NET Framework 4.0.30319 ausgeführt wird, z.B. den folgenden Befehl aus: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**.  

**Arbeitsspeicher:**  

-   Auf dem Computer, der diese Standortsystemrolle hostet, müssen mindestens 5 % Speicher frei sein, um die Verarbeitung von Anforderungen durch die Standortsystemrolle zu ermöglichen.  

-   Wenn diese Standortsystemrolle zusammen mit einer anderen Standortsystemrolle installiert wird, für die dieselbe Anforderung gilt, wird die Speicheranforderung für den Computer nicht erhöht, die Mindestanforderung von 5 % besteht jedoch weiter.  

###  <a name="a-namebkmk2008fsppreqa-fallback-status-point"></a><a name="bkmk_2008FSPpreq"></a> Fallbackstatuspunkt  
**IIS-Konfiguration**: Die IIS-Standardkonfiguration mit den folgenden Ergänzungen ist erforderlich:  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

###  <a name="a-namebkmk2008mppreqa-management-point"></a><a name="bkmk_2008MPpreq"></a> Verwaltungspunkt  
**.NET Framework:**  

-   4.5.2  

**IIS-Konfiguration:** Sie können die IIS-Standardkonfiguration oder eine benutzerdefinierte Konfiguration verwenden. Jeder Verwaltungspunkt, den Sie für die Unterstützung mobiler Geräte aktivieren, erfordert die zusätzliche IIS-Konfiguration für ASP.NET (und automatisch ausgewählte Optionen). In einigen Szenarios, wenn z.B. IIS nach der Installation von .NET Framework 4.5.2 installiert oder umkonfiguriert wird, müssen Sie ASP.NET 4.5 ausdrücklich aktivieren. Führen Sie auf einem 64-Bit-Computer, auf dem .NET Framework 4.0.30319 ausgeführt wird, z.B. den folgenden Befehl aus: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**.  


Sie müssen die folgenden Optionen für IIS aktivieren, um eine benutzerdefinierte IIS-Konfiguration verwenden zu können:  

-   Anwendungsentwicklung:  

    -   ISAPI-Erweiterungen  

-   Sicherheit:  

    -   Windows-Authentifizierung  

-   IIS 6-Verwaltungskompatibilität:  

    -   IIS 6-Metabasiskompatibilität  

    -   IIS 6-WMI-Kompatibilität  


Wenn Sie eine benutzerdefinierte IIS-Konfiguration verwenden, können Sie nicht benötigte Optionen entfernen, darunter die folgenden:  

-   Allgemeine HTTP-Features:  

    -   HTTP-Umleitung  

-   IIS-Verwaltungsskripts und -tools  

**Windows-Feature:**  

-   BITS-Servererweiterungen (und automatisch ausgewählte Optionen) oder intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS) (und automatisch ausgewählte Optionen)  

###  <a name="a-namebkmk2008rspointa-reporting-services-point"></a><a name="bkmk_2008RSpoint"></a> Reporting Services-Punkt  
**.NET Framework:**  

-   4.5.2  

**SQL Server Reporting Services:**  

-   Sie müssen zur Unterstützung von SQL Server Reporting Services vor dem Installieren des Reporting Services-Punkts mindestens eine SQL Server-Instanz installieren und konfigurieren.  

-   Sie können für SQL Server Reporting Services die gleiche Instanz wie für die Standortdatenbank verwenden.  

-   Darüber hinaus kann die verwendete Instanz für andere System Center-Produkte freigegeben werden, solange die anderen System Center-Produkte keiner Einschränkung für die Freigabe von SQL Server-Instanzen unterliegen.  

###  <a name="a-namebkmk2008scppreqa-service-connection-point"></a><a name="bkmk_2008SCPpreq"></a> Dienstverbindungspunkt  
**.NET Framework:**  

-   4.5.2  

     Wenn diese Standortsystemrolle installiert wird, installiert der Configuration Manager automatisch .NET Framework 4.5.2, wenn auf dem Server nicht bereits eine unterstützte Version von .NET Framework installiert ist. Diese Installation kann den Server in den Status „Ausstehender Neustart“ setzen. Wenn für .NET Framework ein Neustart aussteht, können .NET-Anwendungen möglicherweise erst nach dem Neustart des Servers und dem Abschluss der Installation ausgeführt werden.  

**Visual C++ Redistributable:**  

-   Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable auf jedem Computer, auf dem ein Verteilungspunkt gehostet wird.  

-   Die Standortsystemrolle erfordert die x64-Version.  

###  <a name="a-namebkmk2008suppreqa-software-update-point"></a><a name="bkmk_2008SUPpreq"></a> Softwareupdatepunkt  
**.NET Framework:**  

-   3.5 SP1 (oder höher)  

-   .NET Framework 4.5.2  

**IIS-Konfiguration:** Die IIS-Standardkonfiguration ist erforderlich.  

**Windows Server Update Services:**  

-   Sie müssen die Windows-Serverrolle Windows Server Update Services auf einem Computer installieren, bevor Sie einen Softwareupdatepunkt installieren.  

-   Weitere Informationen finden Sie unter [Plan for software updates in System Center Configuration Manager (Planen von Softwareupdates in System Center Configuration Manager)](../../../sum/plan-design/plan-for-software-updates.md).

###  <a name="a-namebkmk2008smppreqa-state-migration-point"></a><a name="bkmk_2008SMPpreq"></a> Zustandsmigrationspunkt  
**IIS-Konfiguration:** Die IIS-Standardkonfiguration ist erforderlich.  



<!--HONumber=Nov16_HO1-->


