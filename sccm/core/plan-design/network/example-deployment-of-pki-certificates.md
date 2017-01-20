---
title: Bereitstellung von PKI-Zertifikaten | Microsoft-Dokumentation
description: "Befolgen Sie ein Schritt-für-Schritt-Beispiel, um den Prozess des Erstellens und Bereitstellens von PKI-Zertifikaten zu erlernen, die System Center Configuration Manager verwendet."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: 11
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 2db82f0572df9519b3119d4dca4f4626ae09d936


---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für System Center Configuration Manager: Windows Server 2008-Zertifizierungsstelle

*Gilt für: System Center Configuration Manager (Current Branch)*

In dieser Schritt-für-Schritt-Beispielbereitstellung mit einer Windows Server 2008-Zertifizierungsstelle (CA) finden Sie Verfahren zum Erstellen und Bereitstellen von PKI-Zertifikaten (Public Key-Infrastruktur), die von System Center Configuration Manager verwendet werden. In diesem Verfahren werden eine Unternehmenszertifizierungsstelle (CA) und Zertifikatvorlagen verwendet. Die Schritte sollten nur in einem Testnetzwerk zur Konzeptüberprüfung angewendet werden.  

 Da die erforderlichen Zertifikate auf unterschiedliche Weise bereitgestellt werden, entnehmen Sie die Informationen zu den erforderlichen Vorgehensweisen und bewährten Methoden der entsprechenden Dokumentation für die PKI-Bereitstellung, um die erforderlichen Zertifikate für eine Produktionsumgebung bereitzustellen. Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

> [!TIP]  
>  Die Anweisungen in diesem Thema lassen sich leicht für andere als die im Abschnitt „Voraussetzungen für ein Testnetzwerk“ erwähnten Betriebssysteme anpassen. Wenn bei Ihnen allerdings die ausstellende Zertifizierungsstelle unter Windows Server 2012 ausgeführt wird, werden Sie nicht zur Eingabe der Zertifikatvorlagenversion aufgefordert. Geben Sie stattdessen auf der Registerkarte **Kompatibilität** die Vorlageneigenschaften wie folgt ein:  
>   
>  -   **Zertifizierungsstelle**: **Windows Server 2003**  
> -   **Zertifikatempfänger**: **Windows XP/Server 2003**  

## <a name="in-this-section"></a>Themen in diesem Abschnitt  
 In den folgenden Abschnitten finden Sie beispielhafte Schritt-für-Schritt-Anleitungen zum Erstellen und Bereitstellen der folgenden Zertifikate, die mit System Center Configuration Manager verwendet werden können:  

 [Voraussetzungen für ein Testnetzwerk](#BKMK_testnetworkenvironment)  

 [Übersicht über die Zertifikate](#BKMK_overview2008)  

 [Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden](#BKMK_webserver2008_cm2012)  

 [Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte](#BKMK_clouddp2008_cm2012)  

 [Bereitstellen des Clientzertifikats für Windows-Computer](#BKMK_client2008_cm2012)  

 [Bereitstellen des Clientzertifikats für Verteilungspunkte](#BKMK_clientdistributionpoint2008_cm2012)  

 [Bereitstellen des Anmeldungszertifikats für mobile Geräte](#BKMK_mobiledevices2008_cm2012)  

 [Bereitstellen der Zertifikate für AMT](#BKMK_AMT2008_cm2012)  

 [Bereitstellen des Clientzertifikats für Macintosh-Computer](#BKMK_MacClient_SP1)  

##  <a name="a-namebkmktestnetworkenvironmenta-test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> Voraussetzungen für ein Testnetzwerk  
 Für die schrittweisen Anleitungen gelten die folgenden Anforderungen:  

-   Im Testnetzwerk werden die Active Directory-Domänendienste mit Windows Server 2008 ausgeführt. Zudem ist das Netzwerk als eine einzelne Domäne bzw. Gesamtstruktur installiert.  

-   Sie verfügen über einen Mitgliedsserver, auf dem Windows Server 2008 Enterprise Edition ausgeführt wird und die Rolle „Active Directory-Zertifikatdienste“ installiert ist. Der Mitgliedsserver ist außerdem als Unternehmens-Stammzertifizierungsstelle konfiguriert.  

-   Sie verfügen über einen Computer mit Windows Server 2008 (Standard Edition oder Enterprise Edition, R2 oder höher), der als Mitgliedsserver festgelegt wurde und auf dem Internetinformationsdienste (IIS) installiert sind. Dieser Computer übernimmt die Funktion des System Center Configuration Manager-Standortsystemservers, den Sie mit einem Intranet-FQDN (zur Unterstützung von Clientverbindungen im Intranet) sowie einem Internet-FQDN konfigurieren, falls Sie mobile Geräte, die von System Center Configuration Manager angemeldet wurden sowie Clients im Internet unterstützen müssen.  

-   Sie verfügen über einen Windows Vista-Client, auf dem das aktuelle Service Pack installiert ist. Dieser Computer ist mit einem aus ASCII-Zeichen bestehenden Computernamen konfiguriert und gehört der Domäne an. Bei diesem Computer wird es sich um einen System Center Configuration Manager-Clientcomputer handeln.  

-   Sie können sich mit einem Administratorkonto der Stammdomäne oder der Unternehmensdomäne anmelden und dieses Konto für alle in dieser Beispielbereitstellung aufgeführten Prozeduren verwenden.  

##  <a name="a-namebkmkoverview2008a-overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> Übersicht über die Zertifikate  
 In der folgenden Tabelle werden die PKI-Zertifikattypen aufgelistet, die möglicherweise für System Center Configuration Manager erforderlich sind, und ihre Verwendung wird beschrieben.  

|Zertifikatanforderung|Zertifikatbeschreibung|  
|-----------------------------|-----------------------------|  
|Webserverzertifikat für Standortsysteme, an denen IIS ausgeführt werden|Dieses Zertifikat wird zum Verschlüsseln von Daten und zum Authentifizieren des Servers bei Clients verwendet. Es muss extern von System Center Configuration Manager auf Standortsystemservern installiert werden, auf denen IIS ausgeführt wird und die zur Verwendung von HTTPS in System Center Configuration Manager konfiguriert sind.<br /><br /> Die Schritte zum Konfigurieren und Installieren dieses Zertifikats finden Sie unter [Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden](#BKMK_webserver2008_cm2012) in diesem Thema.|  
|Servicezertifikat für Clients für die Verbindung mit cloudbasierten Verteilungspunkten|Die Schritte zum Konfigurieren und Installieren dieses Zertifikats finden Sie unter [Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte](#BKMK_clouddp2008_cm2012) in diesem Thema.<br /><br /> **Wichtig:** Dieses Zertifikat wird in Verbindung mit dem Microsoft Azure-Verwaltungszertifikat verwendet. Weitere Informationen zu diesem Verwaltungszertifikat finden Sie unter [Erstellen eines Verwaltungszertifikats](http://go.microsoft.com/fwlink/p/?LinkId=220281) und [Gewusst wie: Hinzufügen eines Verwaltungszertifikats zu einem Windows Azure-Abonnement](http://go.microsoft.com/fwlink/?LinkId=241722) im Abschnitt zur Windows Azure-Plattform in der MSDN Library.|  
|Clientzertifikat für Windows-Computer|Dieses Zertifikat wird zum Authentifizieren von System Center Configuration Manager-Clientcomputern auf Standortsystemen verwendet, die zum Verwenden von HTTPS konfiguriert sind. Es kann auch für Verwaltungspunkte und Zustandsmigrationspunkte verwendet werden, um deren Betriebsstatus zu überwachen, wenn sie zum Verwenden von HTTPS konfiguriert sind. Es muss extern von System Center Configuration Manager auf Computern installiert werden.<br /><br /> Die Schritte zum Konfigurieren und Installieren dieses Zertifikats finden Sie unter [Bereitstellen des Clientzertifikats für Windows-Computer](#BKMK_client2008_cm2012) in diesem Thema.|  
|Clientzertifikat für Verteilungspunkte|Von diesem Zertifikat werden zwei Zwecke erfüllt:<br /><br /> Das Zertifikat wird zum Authentifizieren des Verteilungspunkts bei einem für HTTPS aktivierten Verwaltungspunkt verwendet, bevor Statusmeldungen vom Verteilungspunkt gesendet werden.<br /><br /> Wenn die Verteilungspunktoption **PXE-Unterstützung für Clients aktivieren** ausgewählt ist, wird das Zertifikat an Computer gesendet, von denen ein PXE-Start ausgeführt wird, um während der Bereitstellung des Betriebssystems eine Verbindung mit dem für HTTPS aktivierten Verwaltungspunkt zu ermöglichen.<br /><br /> Die Schritte zum Konfigurieren und Installieren dieses Zertifikats finden Sie unter [Bereitstellen des Clientzertifikats für Verteilungspunkte](#BKMK_clientdistributionpoint2008_cm2012) in diesem Thema.|  
|Anmeldungszertifikat für mobile Geräte|Dieses Zertifikat wird zum Authentifizieren von System Center Configuration Manager-Clients für mobile Geräte bei Standortsystemen verwendet, die zum Verwenden von HTTPS konfiguriert sind. Das Zertifikat muss im Rahmen der Registrierung mobiler Geräte in System Center Configuration Manager installiert werden, und Sie wählen die konfigurierte Zertifikatvorlage als Clienteinstellung von mobilen Geräten aus.<br /><br /> Die Schritte zum Konfigurieren dieses Zertifikats finden Sie unter [Deploying the Enrollment Certificate for Mobile Devices](#BKMK_mobiledevices2008_cm2012) in diesem Thema.|  
|Zertifikate für Intel AMT|Es gibt drei Zertifikate im Zusammenhang mit der Out-of-Band-Verwaltung von Intel AMT-basierten Computern: Ein AMT-Bereitstellungszertifikat, ein AMT-Webserverzertifikat und optional ein Clientauthentifizierungszertifikat für 802.1X-Kabel- und Funknetzwerke.<br /><br /> Das AMT-Bereitstellungszertifikat muss von System Center Configuration Manager extern auf dem Computer mit dem Out-of-Band-Dienstpunkt installiert werden. Dann wählen Sie das installierte Zertifikat in den Eigenschaften des Out-of-Band-Dienstpunkts aus. Das AMT-Webserverzertifikat und das Clientauthentifizierungszertifikat werden im Rahmen der AMT-Bereitstellung und -Verwaltung installiert. Dann wählen Sie die konfigurierten Zertifikatvorlagen in den Eigenschaften der Out-of-Band-Verwaltungskomponente aus.<br /><br /> Die Schritte zum Konfigurieren dieser Zertifikate finden Sie unter [Bereitstellen der Zertifikate für AMT](#BKMK_AMT2008_cm2012) in diesem Thema.|  
|Clientzertifikat für Macintosh-Computer|Sie können dieses Zertifikat von einem Macintosh-Computer anfordern und installieren, wenn Sie die System Center Configuration Manager-Registrierung verwenden und die konfigurierte Zertifikatvorlage als Clienteinstellung für mobile Geräte auswählen.<br /><br /> Die Schritte zum Konfigurieren dieses Zertifikats finden Sie unter [Deploying the Client Certificate for Mac Computers](#BKMK_MacClient_SP1) in diesem Thema.|  

##  <a name="a-namebkmkwebserver2008cm2012a-deploying-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden  
 Diese Zertifikatbereitstellung besteht aus den folgenden Prozeduren:  

-   Erstellen und Ausstellen der Webserver-Zertifikatvorlage bei der Zertifizierungsstelle  

-   Anfordern des Webserverzertifikats  

-   Konfigurieren von IIS für die Verwendung des Webserverzertifikats  

###  <a name="a-namebkmkwebserver22008a-creating-and-issuing-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> Erstellen und Ausstellen der Webserver-Zertifikatvorlage bei der Zertifizierungsstelle  
 Dieses Verfahren erstellt eine Zertifikatvorlage für System Center Configuration Manager-Standortsysteme und fügt sie der Zertifizierungsstelle hinzu.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>So können Sie die Webserver-Zertifikatvorlage bei der Zertifizierungsstelle generieren und ausstellen  

1.  Erstellen Sie eine Sicherheitsgruppe mit der Bezeichnung **ConfigMgr IIS Servers**, die die Mitgliedsserver für die Installation der System Center Configuration Manager-Standortsysteme, die IIS ausführen, enthält.  

2.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifikatdienste installiert sind, in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen** , und klicken Sie dann auf **Verwalten** , um die Konsole **Zertifikatvorlagen** zu laden.  

3.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Webserver**angezeigt wird, und klicken Sie auf **Doppelte Vorlage**.  

4.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

5.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen zum Generieren der Webzertifikate ein, die auf Configuration Manager-Standortsystemen verwendet werden, beispielsweise **ConfigMgr-Webserverzertifikat**.  

6.  Klicken Sie auf die Registerkarte **Antragstellername** , und vergewissern Sie sich, dass **Informationen werden in der Anforderung angegeben** ausgewählt ist.  

7.  Klicken Sie auf die Registerkarte **Sicherheit** , und entfernen Sie aus den Sicherheitsgruppen **Domänen-Admins** und **Organisations-Admins** die Berechtigung **Anmelden**.  

8.  Klicken Sie auf **Hinzufügen**, geben Sie in das Textfeld **ConfigMgr-IIS-Server** ein, und klicken Sie dann auf **OK**.  

9. Wählen Sie für diese Gruppe die Berechtigung **Anmelden** aus, und lassen Sie die Berechtigung **Lesen** aktiviert.  

10. Klicken Sie auf **OK**, und schließen Sie die **Zertifikatvorlagenkonsole**.  

11. Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, klicken Sie auf **Neu**und dann auf **Auszustellende Zertifikatvorlage**.  

12. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr-Webserverzertifikat**aus, und klicken Sie dann auf **OK**.  

13. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

###  <a name="a-namebkmkwebserver32008a-requesting-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> Anfordern des Webserverzertifikats  
 Bei dieser Prozedur können Sie Werte für Intranet- und Internet-FQDN angeben, die in den Eigenschaften des Standortsystemservers konfiguriert werden, bevor das Webserverzertifikat auf dem Mitgliedsserver installiert wird, auf dem IIS ausgeführt werden.  

##### <a name="to-request-the-web-server-certificate"></a>So fordern Sie das Webserverzertifikat an  

1.  Starten Sie den Mitgliedsserver neu, auf dem IIS ausgeführt werden. Dadurch stellen Sie sicher, dass mithilfe der Berechtigungen **Lesen** und **Anmelden** , die Sie konfiguriert haben, für den Computer ein Zugriff auf die Zertifikatvorlage, die Sie erstellt haben, möglich ist.  

2.  Klicken Sie auf **Start**, klicken Sie auf **Ausführen**, und geben Sie **mmc.exe** ein. Klicken Sie in der leeren Konsole auf **Datei**angezeigt wird, und klicken Sie auf **Snap-In hinzufügen/entfernen**.  

3.  Wählen Sie im Dialogfeld **Snap-In hinzufügen/entfernen** aus der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**.  

4.  Wählen Sie im Dialogfeld **Zertifikat-Snap-In** die Option **Computerkonto**aus, und klicken Sie auf **Weiter**.  

5.  Vergewissern Sie sich, dass im Dialogfeld **Computer auswählen** die Option **Lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist. Klicken Sie anschließend auf **Fertig stellen**.  

6.  Klicken Sie im Dialogfeld **Snap-Ins hinzufügen/entfernen** auf **OK**.  

7.  Erweitern Sie in der Konsole **Zertifikate (Lokaler Computer)**, und klicken Sie dann auf **Persönlich**.  

8.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, klicken Sie auf **Alle Tasks**und dann auf **Neues Zertifikat anfordern**.  

9. Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  

10. Wenn die Seite **Zertifikatregistrierungsrichtlinie auswählen** angezeigt wird, klicken Sie auf **Weiter**.  

11. Wählen Sie auf der Seite **Zertifikate anfordern** in der Liste der angezeigten Zertifikate das **ConfigMgr-Webserverzertifikat** aus, und klicken Sie anschließend auf **Es werden zusätzliche Informationen für diese Zertifikatsregistrierung benötigt. Klicken Sie hier, um die Einstellungen zu konfigurieren**.  

12. Im Dialogfeld **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** muss der **Antragstellername**unverändert bleiben. Dies bedeutet, dass das Feld **Wert** für den Abschnitt **Antragstellername** leer bleibt. Klicken Sie stattdessen im Abschnitt **Alternativer Antragstellername** auf die Dropdownliste **Typ** , und wählen Sie dann **DNS**aus.  

13. Geben Sie im Feld **Wert** die FQDN-Werte an, die Sie in den Standortsystemeigenschaften von System Center Configuration Manager angeben werden, und klicken Sie dann auf **OK**, um das Dialogfeld **Zertifikateigenschaften** zu schließen.  

     Beispiele:  

    -   Wenn vom Standortsystem nur Clientverbindungen aus dem Intranet akzeptiert werden und der Intranet-FQDN des Standortsystemservers **server1.internal.contoso.com**lautet: Geben Sie **server1.internal.contoso.com**ein, und klicken Sie dann auf **Hinzufügen**.  

    -   Wenn vom Standortsystem Clientverbindungen aus dem Intranet und dem Internet akzeptiert werden, der Intranet-FQDN des Standortsystemservers **server1.internal.contoso.com** und der Internet-FQDN des Standortsystemservers **server.contoso.com**lauten:  

        1.  Geben Sie **server1.internal.contoso.com**ein, und klicken Sie dann auf **Hinzufügen**.  

        2.  Geben Sie **server.contoso.com**ein, und klicken Sie dann auf **Hinzufügen**.  

        > [!NOTE]  
        >  Es spielt keine Rolle, in welcher Reihenfolge Sie die FQDNs für System Center Configuration Manager angeben. Vergewissern Sie sich jedoch, dass von allen Geräten, von denen das Zertifikat verwendet wird (beispielsweise mobile Geräte und Proxywebserver), ein alternativer Antragstellername (SAN) für das Zertifikat sowie mehrere Werte für den SAN verwendet werden können. Wenn die Unterstützung der Geräte von SAN-Werten in den Zertifikaten begrenzt ist, müssen Sie möglicherweise die Reihenfolge der FQDNs ändern oder stattdessen den Antragsteller-Wert verwenden.  

14. Wählen Sie auf der Seite **Zertifikate anfordern** in der Liste der angezeigten Zertifikate die Vorlage **ConfigMgr-Webserverzertifikat** aus, und klicken Sie dann auf **Anmelden**.  

15. Warten Sie, bis auf der Seite mit den **Ergebnissen der Zertifikatinstallation** angezeigt wird, dass das Zertifikat installiert wurde. Klicken Sie dann auf **Fertig stellen**.  

16. Schließen Sie das Dialogfeld **Zertifikate (Lokaler Computer)**.  

###  <a name="a-namebkmkwebserver42008a-configuring-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> Konfigurieren von IIS für die Verwendung des Webserverzertifikats  
 Durch diese Prozedur wird das installierte Zertifikat an die IIS- **Standardwebsite**gebunden.  

##### <a name="to-configure-iis-to-use-the-web-server-certificate"></a>So konfigurieren Sie IIS für die Verwendung des Webserverzertifikats  

1.  Klicken Sie auf dem Mitgliedsserver mit IIS auf **Start**, auf **Programme**, auf **Verwaltung**und dann auf **Internetinformationsdienste-Manager**.  

2.  Erweitern Sie **Sites**, klicken Sie mit der rechten Maustaste auf **Standardwebsite**, und wählen Sie dann **Bindungen bearbeiten**aus.  

3.  Klicken Sie auf den Eintrag **HTTPS** und dann auf **Bearbeiten**.  

4.  Wählen Sie im Dialogfeld **Websitebindung bearbeiten** das Zertifikat aus, das Sie mithilfe der Vorlage „ConfigMgr-Webserverzertifikat“ angefordert haben, und klicken Sie dann auf **OK**.  

    > [!NOTE]  
    >  Wenn Sie sich nicht sicher sind, welches das richtige Zertifikat ist, wählen Sie ein Zertifikat aus, und klicken dann auf **Ansicht**. So können Sie die ausgewählten Zertifikatdetails mit den Zertifikaten vergleichen, die mit dem Zertifikat-Snap-In angezeigt werden. Beispielsweise wird mit dem Zertifikat-Snap-In die Zertifikatvorlage angezeigt, die für die Zertifikatanforderung verwendet wurde. Anschließend können Sie den Fingerabdruck des Zertifikats, das mit der Vorlage „ConfigMgr-Webserverzertifikat“ angefordert wurde, mit dem Fingerabdruck des Zertifikats vergleichen, das aktuell im Dialogfeld **Websitebindung bearbeiten** ausgewählt ist.  

5.  Klicken Sie im Dialogfeld **Websitebindung bearbeiten** auf **OK** , und klicken Sie dann auf **Schließen**.  

6.  Schließen Sie das Dialogfeld **Internetinformationsdienste-Manager**.  

 Der Mitgliedsserver ist nun mit einem Webserverzertifikat für System Center Configuration Manager ausgestattet.  

> [!IMPORTANT]  
>  Wenn Sie den System Center Configuration Manager-Standortsystemserver auf diesem Computer installieren, vergewissern Sie sich, dass Sie in den Standortsystemeigenschaften die gleichen FQDNs angeben wie bei der Anforderung des Zertifikats.  

##  <a name="a-namebkmkclouddp2008cm2012a-deploying-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte  

> [!NOTE]  
>  Das Dienstzertifikat für cloudbasierte Verteilungspunkte gilt für System Center Configuration Manager SP1 und höher.  

 Diese Zertifikatbereitstellung besteht aus den folgenden Prozeduren:  

-   [Erstellen und Ausstellen der benutzerdefinierten Webserver-Zertifikatvorlage bei der Zertifizierungsstelle](#BKMK_clouddpcreating2008)  

-   [Anfordern des benutzerdefinierten Webserverzertifikats](#BKMK_clouddprequesting2008)  

-   [Exportieren des benutzerdefinierten Webserverzertifikats für cloudbasierte Verteilungspunkte](#BKMK_clouddpexporting2008)  

###  <a name="a-namebkmkclouddpcreating2008a-creating-and-issuing-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> Erstellen und Ausstellen der benutzerdefinierten Webserver-Zertifikatvorlage bei der Zertifizierungsstelle  
 Mit dieser Prozedur wird eine benutzerdefinierte Zertifikatvorlage erstellt, die auf der Zertifikatvorlage für Webserver basiert. Das Zertifikat gilt für cloudbasierte Verteilungspunkte in System Center Configuration Manager, und der private Schlüssel muss exportierbar sein. Nachdem die Vorlage erstellt wurde, wird sie zur Zertifizierungsstelle hinzugefügt.  

> [!NOTE]  
>  In dieser Prozedur wird eine andere Zertifikatvorlage als die Zertifikatvorlage für Webserver verwendet, die Sie für IIS ausführende Standortsysteme erstellt haben, denn obwohl beide Zertifikate eine Serverauthentifizierungsfunktion erfordern, erfordert das Zertifikat für cloudbasierte Verteilungspunkte, dass Sie einen benutzerdefinierten Wert als Antragstellernamen eingeben. Des Weiteren muss der private Schlüssel exportiert werden. Aus Sicherheitsgründen wird empfohlen, Zertifikatvorlagen nur dann zum Zulassen des Exports des privaten Schlüssels zu konfigurieren, wenn dies erforderlich ist. Diese Konfiguration ist für den cloudbasierten Verteilungspunkt erforderlich, da Sie das Zertifikat als Datei importieren müssen, anstatt es aus dem Zertifikatspeicher auszuwählen.  
>   
>  Wenn Sie für dieses Zertifikat eine neue Zertifikatvorlage erstellen, können Sie beschränken, von welchen Computern Zertifikate, von denen der Export des privaten Schlüssels zugelassen wird, angefordert werden. In einem Produktionsnetzwerk sollten Sie außerdem die folgenden Änderungen für dieses Zertifikat erwägen:  
>   
>  -   Verlangen Sie eine Genehmigung zum Installieren des Zertifikats, um die Sicherheit zu erhöhen.  
> -   Verlängern Sie die Gültigkeitsdauer des Zertifikats. Sie müssen das Zertifikat jedes Mal vor Ablauf exportieren und importieren; diese Prozedur müssen Sie seltener wiederholen, wenn Sie die Gültigkeitsdauer verlängern. Wenn Sie jedoch die Gültigkeitsdauer verlängern, reduzieren Sie damit die Sicherheit des Zertifikats, da Angreifern mehr Zeit zum Entschlüsseln des privaten Schlüssels und zum Stehlen des Zertifikats zur Verfügung steht.  
> -   Verwenden Sie im Zertifikat Alternativer Antragstellername einen benutzerdefinierten Wert, um dieses Zertifikat unter den standardmäßigen Webserverzertifikaten zu identifizieren, die Sie mit IIS verwenden.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>So können Sie die benutzerdefinierte Zertifikatvorlage für Webserver bei der Zertifizierungsstelle generieren und ausstellen  

1.  Erstellen Sie eine Sicherheitsgruppe mit der Bezeichnung **ConfigMgr-Standortserver**, in der die Mitgliedsserver für die Installation der primären Standortserver von System Center Configuration Manager enthalten sind, von denen die cloudbasierten Verteilungspunkte verwaltet werden.  

2.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifizierungsstellenkonsole ausgeführt wird, mit der rechten Maustaste auf **Zertifikatvorlagen**, und klicken Sie dann auf **Verwalten** , um die Verwaltungskonsole für Zertifikatvorlagen zu laden.  

3.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Webserver**angezeigt wird, und klicken Sie auf **Doppelte Vorlage**.  

4.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

5.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen ein, beispielsweise **ConfigMgr – cloudbasiertes Verteilungspunktzertifikat**, um das Webserverzertifikat für cloudbasierte Verteilungspunkte zu erstellen.  

6.  Klicken Sie auf die Registerkarte **Anforderungsverarbeitung** , und wählen Sie **Exportieren von privatem Schlüssel zulassen**aus.  

7.  Klicken Sie auf die Registerkarte **Sicherheit** , und entfernen Sie aus der Sicherheitsgruppe **Enterprise Admins** die Berechtigung **Anmelden** .  

8.  Klicken Sie auf **Hinzufügen**, geben Sie in das Textfeld **ConfigMgr – Standortserver** ein, und klicken Sie dann auf **OK**.  

9. Wählen Sie für diese Gruppe die Berechtigung **Anmelden** aus, und lassen Sie die Berechtigung **Lesen** aktiviert.  

10. Klicken Sie auf **OK** , und schließen Sie die **Zertifikatvorlagenkonsole**.  

11. Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, klicken Sie auf **Neu**und dann auf **Auszustellende Zertifikatvorlage**.  

12. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr – cloudbasiertes Verteilungspunktzertifikat**aus, und klicken Sie auf **OK**.  

13. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

###  <a name="a-namebkmkclouddprequesting2008a-requesting-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> Anfordern des benutzerdefinierten Webserverzertifikats  
 Mit dieser Prozedur können Sie das benutzerdefinierte Webserverzertifikat anfordern und auf dem Mitgliedsserver installieren, auf dem der Standortserver ausgeführt wird.  

##### <a name="to-request-the-custom-web-server-certificate"></a>So fordern Sie das benutzerdefinierte Webserverzertifikat an  

1.  Führen Sie einen Neustart des Mitgliedsservers aus, nachdem Sie die Sicherheitsgruppe **ConfigMgr – Standortserver** erstellt und konfiguriert haben, um sicherzustellen, dass der Computer auf die von Ihnen erstellte Zertifikatvorlage zugreifen kann; verwenden Sie die von Ihnen konfigurierten Berechtigungen **Lesen** und **Anmelden** .  

2.  Klicken Sie auf **Start**, klicken Sie auf **Ausführen**, und geben Sie **mmc.exe** ein. Klicken Sie in der leeren Konsole auf **Datei**angezeigt wird, und klicken Sie auf **Snap-In hinzufügen/entfernen**.  

3.  Wählen Sie im Dialogfeld **Snap-In hinzufügen/entfernen** aus der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**.  

4.  Wählen Sie im Dialogfeld **Zertifikat-Snap-In** die Option **Computerkonto**aus, und klicken Sie auf **Weiter**.  

5.  Vergewissern Sie sich, dass im Dialogfeld **Computer auswählen** die Option **Lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist. Klicken Sie anschließend auf **Fertig stellen**.  

6.  Klicken Sie im Dialogfeld **Snap-Ins hinzufügen/entfernen** auf **OK**.  

7.  Erweitern Sie in der Konsole **Zertifikate (Lokaler Computer)**, und klicken Sie dann auf **Persönlich**.  

8.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, klicken Sie auf **Alle Tasks**und dann auf **Neues Zertifikat anfordern**.  

9. Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  

10. Wenn die Seite **Zertifikatregistrierungsrichtlinie auswählen** angezeigt wird, klicken Sie auf **Weiter**.  

11. Wählen Sie auf der Seite **Zertifikate anfordern** in der Liste der angezeigten Zertifikate das **ConfigMgr – cloudbasiertes Verteilungspunktzertifikat** aus, und klicken Sie dann auf **Es werden zusätzliche Informationen für diese Zertifikatsregistrierung benötigt. Klicken Sie hier, um die Einstellungen zu konfigurieren**.  

12. Wählen Sie im Dialogfenster **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** für den **Antragstellernamen**als **Typ** die Option **Allgemeiner Name**.  

13. Geben Sie im Feld **Wert** Ihre Auswahl für den Dienstnamen sowie Ihren Domänennamen ein, indem Sie das Format FQDN verwenden. Beispiel: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Welchen Dienstnamen Sie hier angeben, bleibt Ihnen überlassen, solange er in Ihrem Namespace einmalig ist. Mit DNS legen Sie einen Alias (CNAME-Datensatz) an, um diesen Dienstnamen zu einer automatisch generierten ID (GUID) und einer IP-Adresse von Windows Azure zuzuordnen.  

14. Klicken Sie auf **Hinzufügen**, und dann auf **OK** , um das Dialogfenster **Zertifikateigenschaften** zu schließen.  

15. Wählen Sie auf der Seite **Zertifikate anfordern** in der Liste der angezeigten Zertifikate das **ConfigMgr – cloudbasierte Verteilungspunktzertifikat** aus, und klicken Sie dann auf **Anmelden**.  

16. Warten Sie, bis auf der Seite mit den **Ergebnissen der Zertifikatinstallation** angezeigt wird, dass das Zertifikat installiert wurde. Klicken Sie dann auf **Fertig stellen**.  

17. Schließen Sie das Dialogfeld **Zertifikate (Lokaler Computer)**.  

###  <a name="a-namebkmkclouddpexporting2008a-exporting-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> Exportieren des benutzerdefinierten Webserverzertifikats für cloudbasierte Verteilungspunkte  
 Mithilfe dieser Prozedur können Sie das benutzerdefinierte Webserverzertifikat in eine Datei exportieren, damit sie beim Erstellen eines cloudbasierten Verteilungspunktes importiert werden kann.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>So exportieren Sie das benutzerdefinierten Webserverzertifikat für cloudbasierte Verteilungspunkte  

1.  Klicken Sie in der Konsole **Zertifikate (Lokaler Computer)** mit der rechten Maustaste auf das soeben installierte Zertifikat, wählen Sie **Alle Tasks**aus, und klicken Sie dann auf **Exportieren**.  

2.  Klicken Sie im Assistenten zum Exportieren von Zertifikaten auf **Weiter**.  

3.  Wählen Sie auf der Seite **Privaten Schlüssel exportieren** die Option **Ja, privaten Schlüssel exportieren**aus, und klicken Sie auf **Weiter**.  

    > [!NOTE]  
    >  Ist diese Option nicht verfügbar, wurde das Zertifikat ohne Option zum Exportieren des privaten Schlüssels erstellt. In diesem Szenario können Sie das Zertifikat nicht im erforderlichen Format exportieren. Sie müssen die Konfiguration der Zertifikatvorlage so anpassen, dass der private Schlüssel exportiert werden kann, und dann das Zertifikat erneut anfordern.  

4.  Auf der Seite **Format der zu exportierenden Datei** muss die Option **Privater Informationsaustausch - PKCS #12 (.PFX)** ausgewählt sein.  

5.  Geben Sie auf der Seite **Kennwort** ein sicheres Kennwort zum Schutz des exportierten Zertifikats mit seinem privaten Schlüssel an, und klicken Sie auf **Weiter**.  

6.  Geben Sie auf der Seite **Zu exportierende Datei** den Namen der Datei an, die exportiert werden soll, und klicken Sie auf **Weiter**.  

7.  Klicken Sie auf **Fertig stellen** , um den ** ** Assistenten zum Exportieren von Zertifikaten zu schließen, und klicken Sie dann im Bestätigungsdialogfeld auf **OK** .  

8.  Schließen Sie das Dialogfeld **Zertifikate (Lokaler Computer)**.  

9. Speichern Sie die Datei an einem sicheren Ort, und gewährleisten Sie, dass Sie von der System Center Configuration Manager-Konsole darauf zugreifen können.  

 Das Zertifikat kann nun importiert werden, wenn Sie einen cloudbasierten Verteilungspunkt erstellen.  

##  <a name="a-namebkmkclient2008cm2012a-deploying-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> Bereitstellen des Clientzertifikats für Windows-Computer  
 Diese Zertifikatbereitstellung besteht aus den folgenden Prozeduren:  

-   Erstellen und Ausstellen der Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle  

-   Konfigurieren der automatischen Anmeldung der Vorlage zur Arbeitsstationsauthentifizierung mithilfe einer Gruppenrichtlinie  

-   Automatisches Registrieren des Zertifikats zur Arbeitsstationsauthentifizierung und Überprüfen der Installation auf Computern  

###  <a name="a-namebkmkclient02008a-creating-and-issuing-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> Erstellen und Ausstellen der Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle  
 Dieses Verfahren erstellt eine Zertifikatvorlage für System Center Configuration Manager-Clientcomputer und fügt sie der Zertifizierungsstelle hinzu.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>So können Sie die Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle generieren und ausstellen  

1.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifizierungsstellenkonsole ausgeführt wird, mit der rechten Maustaste auf **Zertifikatvorlagen**, und klicken Sie dann auf **Verwalten** , um die Verwaltungskonsole für Zertifikatvorlagen zu laden.  

2.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Arbeitsstationsauthentifizierung**angezeigt wird, und klicken Sie auf **Doppelte Vorlage**.  

3.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

4.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen zum Generieren der Clientzertifikate ein, die auf Configuration Manager-Clientcomputern verwendet werden, z. B. **ConfigMgr-Clientzertifikat**.  

5.  Klicken Sie auf die Registerkarte **Sicherheit** , und wählen Sie die Gruppe **Domänencomputers** aus. Wählen Sie die zusätzlichen Berechtigungen **Lesen** und **Automatisch registrieren**aus. Lassen Sie **Anmelden**aktiviert.  

6.  Klicken Sie auf **OK** , und schließen Sie die **Zertifikatvorlagenkonsole**.  

7.  Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, klicken Sie auf **Neu**und dann auf **Auszustellende Zertifikatvorlage**.  

8.  Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr-Clientzertifikat**aus, und klicken Sie auf **OK**.  

9. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

###  <a name="a-namebkmkclient12008a-configuring-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> Konfigurieren der automatischen Anmeldung der Vorlage zur Arbeitsstationsauthentifizierung mithilfe einer Gruppenrichtlinie  
 Mit dieser Prozedur konfigurieren Sie die Gruppenrichtlinie zum automatischen Anmelden des Clientzertifikats auf Computern.  

##### <a name="to-configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>So konfigurieren Sie die automatische Anmeldung der Vorlage zur Arbeitsstationsauthentifizierung mithilfe einer Gruppenrichtlinie  

1.  Klicken Sie auf dem Domänencontroller auf **Start**&amp;gt; **Programme**&amp;gt; **Gruppenrichtlinienverwaltung**.  

2.  Wechseln Sie zu Ihrer Domäne. Klicken Sie mit der rechten Maustaste auf die Domäne, und wählen Sie dann **Gruppenrichtlinienobjekt hier erstellen und verknüpfen**aus.  

    > [!NOTE]  
    >  Für diesen Schritt hat es sich bewährt, eine neue Gruppenrichtlinie für benutzerdefinierte Einstellungen zu erstellen, statt die mit den Active Directory-Domänendiensten installierte Standarddomänenrichtlinie zu bearbeiten. Wenn Sie diese Gruppenrichtlinie auf Domänenebene zuweisen, wird sie auf alle Computer in der Domäne angewendet. In einer Produktionsumgebung können Sie die automatische Registrierung jedoch auf ausgewählte Computer einschränken. Weisen Sie die Gruppenrichtlinie zu diesem Zweck auf einer Organisationseinheitsebene zu, oder filtern Sie die Gruppenrichtlinie der Domäne mit einer Sicherheitsgruppe, sodass sie nur für die Computer in der Gruppe gilt. Wenn Sie die automatische Registrierung einschränken, müssen Sie den als Verwaltungspunkt konfigurierten Server einschließen.  

3.  Geben Sie im Dialogfeld **Neues Gruppenrichtlinienobjekt** einen Namen für die neue Gruppenrichtlinie ein, z. B. **Zertifikate automatisch registrieren**, und klicken Sie auf **OK**.  

4.  Klicken Sie im Ergebnisbereich auf der Registerkarte **Verknüpfte Gruppenrichtlinienobjekte** mit der rechten Maustaste auf die neue Gruppenrichtlinie, und klicken Sie dann auf **Bearbeiten**.  

5.  Vergewissern Sie sich, dass im Dialogfeld **Gruppenrichtlinienverwaltungs-Editor**unter **Computerkonfiguration** den Knoten **Richtlinien**, und wechseln Sie dann zu **Windows-Einstellungen** / **Sicherheitseinstellungen** / **Public Key Computerkonfiguration**.  

6.  Klicken Sie mit der rechten Maustaste auf den Objekttyp mit dem Namen **Zertifikatdiensteclient – Automatische Registrierung**, und klicken Sie anschließend auf **Eigenschaften**.  

7.  Klicken Sie in der Dropdown-Liste **Konfigurationsmodell** auf **Aktiviert**, klicken Sie auf **Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen**, klicken Sie auf **Zertifikate aktualisieren, die Zertifikatvorlagen verwenden**, und klicken Sie dann auf **OK**.  

8.  Schließen Sie die **Gruppenrichtlinienverwaltung**.  

###  <a name="a-namebkmkclient22008a-automatically-enrolling-the-workstation-authentication-certificate-and-verifying-its-installation-on-computers"></a><a name="BKMK_client22008"></a> Automatisches Registrieren des Zertifikats zur Arbeitsstationsauthentifizierung und Überprüfen der Installation auf Computern  
 Mit dieser Prozedur wird das Clientzertifikat auf Computern installiert, und die Installation wird überprüft.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>So registrieren Sie das Zertifikat zur Arbeitsstationsauthentifizierung automatisch und überprüfen die Installation auf dem Clientcomputer  

1.  Starten Sie die Arbeitsstation neu, und warten Sie einige Minuten, bevor Sie sich anmelden.  

    > [!NOTE]  
    >  Das Neustarten eines Computers ist die zuverlässigste Methode, eine erfolgreiche automatische Registrierung von Zertifikaten sicherzustellen.  

2.  Melden Sie sich mit einem Konto an, das über Administratorrechte verfügt.  

3.  Geben Sie in das Suchfeld **mmc.exe.**ein, und drücken Sie dann die ** **EINGABETASTE.  

4.  Klicken Sie in der leeren Verwaltungskonsole auf **Datei**und anschließend auf **Snap-In hinzufügen/entfernen**.  

5.  Wählen Sie im Dialogfeld **Snap-In hinzufügen/entfernen** aus der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**.  

6.  Wählen Sie im Dialogfeld **Zertifikat-Snap-In** die Option **Computerkonto**aus, und klicken Sie auf **Weiter**.  

7.  Vergewissern Sie sich, dass im Dialogfeld **Computer auswählen** die Option **Lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist. Klicken Sie anschließend auf **Fertig stellen**.  

8.  Klicken Sie im Dialogfeld **Snap-Ins hinzufügen/entfernen** auf **OK**.  

9. Erweitern Sie in der Konsole **Zertifikate (Lokaler Computer)**, erweitern Sie **Persönlich**, und klicken Sie dann auf **Zertifikate**.  

10. Überprüfen Sie, ob im Ergebnisbereich ein Zertifikat angezeigt wird, für das in der Spalte **Beabsichtigter Zweck** der Wert **Clientauthentifizierung** und in der Spalte **Zertifikatvorlage** der Wert **ConfigMgr-Clientzertifikat** angezeigt wird.  

11. Schließen Sie das Dialogfeld **Zertifikate (Lokaler Computer)**.  

12. Wiederholen Sie die Schritte 1 bis 11 für den Mitgliedsserver, um sicherzustellen, dass der als Verwaltungspunkt konfigurierte Server ebenfalls über ein Clientzertifikat verfügt.  

 Der Computer ist nun mit einem System Center Configuration Manager-Clientzertifikat ausgestattet.  

##  <a name="a-namebkmkclientdistributionpoint2008cm2012a-deploying-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> Bereitstellen des Clientzertifikats für Verteilungspunkte  

> [!NOTE]  
>  Dieses Zertifikat kann auch für Medienabbilder verwendet werden, die keinen PXE-Start verwenden, da die gleichen Zertifikatanforderungen bestehen.  

 Diese Zertifikatbereitstellung besteht aus den folgenden Prozeduren:  

-   Erstellen und Ausstellen einer benutzerdefinierten Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle  

-   Anfordern des benutzerdefinierten Zertifikats zur Arbeitsstationsauthentifizierung  

-   Exportieren des Clientzertifikats für Verteilungspunkte  

###  <a name="a-namebkmkclientdistributionpoint02008a-creating-and-issuing-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> Erstellen und Ausstellen einer benutzerdefinierten Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle  
 Mit diesem Verfahren wird eine benutzerdefinierte Zertifikatvorlage für System Center Configuration Manager-Verteilungspunkte erstellt, mit der der private Schlüssel exportiert werden kann, und die Zertifikatvorlage wird der Zertifizierungsstelle hinzugefügt.  

> [!NOTE]  
>  Von dieser Prozedur wird eine andere Zertifikatvorlage als die verwendet, die Sie für Clientcomputer erstellt haben, denn obgleich für beide Zertifikate Clientauthentifizierungsfunktionen erforderlich sind, ist für das Verteilungspunktzertifikat erforderlich, dass der private Schlüssel exportiert wird. Aus Sicherheitsgründen wird empfohlen, Zertifikatvorlagen nur dann zum Zulassen des Exports des privaten Schlüssels zu konfigurieren, wenn dies erforderlich ist. Diese Konfiguration ist für den Verteilungspunkt erforderlich, da Sie das Zertifikat als Datei importieren müssen, anstatt es aus dem Zertifikatspeicher auszuwählen.  
>   
>  Wenn Sie für dieses Zertifikat eine neue Zertifikatvorlage erstellen, können Sie beschränken, von welchen Computern Zertifikate, von denen der Export des privaten Schlüssels zugelassen wird, angefordert werden. In unserer Beispielbereitstellung ist dies die Sicherheitsgruppe, die Sie zuvor für System Center Configuration Manager-Standortsysteme, auf denen IIS ausgeführt werden, erstellt haben. Erwägen Sie in einem Produktionsnetzwerk, von dem die IIS-Standortsystemrollen verteilt werden, die Erstellung einer neuen Sicherheitsgruppe für die Server, auf denen Verteilungspunkte ausgeführt werden, sodass Sie das Zertifikat nur auf diese Standortsystemserver beschränken können. Außerdem sollten Sie die folgenden Änderungen für dieses Zertifikat erwägen:  
>   
>  -   Verlangen Sie eine Genehmigung zum Installieren des Zertifikats, um die Sicherheit zu erhöhen.  
> -   Verlängern Sie die Gültigkeitsdauer des Zertifikats. Sie müssen das Zertifikat jedes Mal vor Ablauf exportieren und importieren; diese Prozedur müssen Sie seltener wiederholen, wenn Sie die Gültigkeitsdauer verlängern. Wenn Sie jedoch die Gültigkeitsdauer verlängern, reduzieren Sie damit die Sicherheit des Zertifikats, da Angreifern mehr Zeit zum Entschlüsseln des privaten Schlüssels und zum Stehlen des Zertifikats zur Verfügung steht.  
> -   Verwenden Sie für das Zertifikat einen benutzerdefinierten Wert im Feld Antragsteller oder als alternativen Antragstellernamen (SAN), um die Unterscheidung dieses Zertifikats von den Standardclientzertifikaten zu vereinfachen. Dies ist vor allem dann nützlich, wenn Sie das gleiche Zertifikat für mehrere Verteilungspunkte verwenden möchten.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>So können Sie die benutzerdefinierte Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle generieren und ausstellen  

1.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifizierungsstellenkonsole ausgeführt wird, mit der rechten Maustaste auf **Zertifikatvorlagen**, und klicken Sie dann auf **Verwalten** , um die Verwaltungskonsole für Zertifikatvorlagen zu laden.  

2.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Arbeitsstationsauthentifizierung**angezeigt wird, und klicken Sie auf **Doppelte Vorlage**.  

3.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

4.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Namen ein, beispielsweise **ConfigMgr-Clientverteilungspunktzertifikat**, um das Clientauthentifizierungszertifikat für Verteilungspunkte zu erstellen.  

5.  Klicken Sie auf die Registerkarte **Anforderungsverarbeitung** , und wählen Sie **Exportieren von privatem Schlüssel zulassen**aus.  

6.  Klicken Sie auf die Registerkarte **Sicherheit** , und entfernen Sie aus der Sicherheitsgruppe **Enterprise Admins** die Berechtigung **Anmelden** .  

7.  Klicken Sie auf **Hinzufügen**, geben Sie in das Textfeld **ConfigMgr-IIS-Server** ein, und klicken Sie dann auf **OK**.  

8.  Wählen Sie für diese Gruppe die Berechtigung **Anmelden** aus, und lassen Sie die Berechtigung **Lesen** aktiviert.  

9. Klicken Sie auf **OK** , und schließen Sie die **Zertifikatvorlagenkonsole**.  

10. Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, klicken Sie auf **Neu**und dann auf **Auszustellende Zertifikatvorlage**.  

11. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr-Clientverteilungspunktzertifikat**aus, und klicken Sie auf **OK**.  

12. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

###  <a name="a-namebkmkclientdistributionpoint12008a-requesting-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> Anfordern des benutzerdefinierten Zertifikats zur Arbeitsstationsauthentifizierung  
 Mit dieser Prozedur fordern Sie das benutzerdefinierte Clientzertifikat an und installieren es auf dem Mitgliedsserver, auf dem IIS ausgeführt werden und der als Verteilungspunkt konfiguriert werden soll.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>So fordern Sie das benutzerdefinierte Zertifikat zur Arbeitsstationsauthentifizierung an  

1.  Klicken Sie auf **Start**, klicken Sie auf **Ausführen**, und geben Sie **mmc.exe** ein. Klicken Sie in der leeren Konsole auf **Datei**angezeigt wird, und klicken Sie auf **Snap-In hinzufügen/entfernen**.  

2.  Wählen Sie im Dialogfeld **Snap-In hinzufügen/entfernen** aus der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**.  

3.  Wählen Sie im Dialogfeld **Zertifikat-Snap-In** die Option **Computerkonto**aus, und klicken Sie auf **Weiter**.  

4.  Vergewissern Sie sich, dass im Dialogfeld **Computer auswählen** die Option **Lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist. Klicken Sie anschließend auf **Fertig stellen**.  

5.  Klicken Sie im Dialogfeld **Snap-Ins hinzufügen/entfernen** auf **OK**.  

6.  Erweitern Sie in der Konsole **Zertifikate (Lokaler Computer)**, und klicken Sie dann auf **Persönlich**.  

7.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, klicken Sie auf **Alle Tasks**und dann auf **Neues Zertifikat anfordern**.  

8.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  

9. Wenn die Seite **Zertifikatregistrierungsrichtlinie auswählen** angezeigt wird, klicken Sie auf **Weiter**.  

10. Wählen Sie auf der Seite **Zertifikate anfordern** in der Liste der angezeigten Zertifikate das **ConfigMgr-Clientverteilungspunktzertifikat** aus, und klicken Sie dann auf **Anmelden**.  

11. Warten Sie, bis auf der Seite mit den **Ergebnissen der Zertifikatinstallation** angezeigt wird, dass das Zertifikat installiert wurde. Klicken Sie dann auf **Fertig stellen**.  

12. Vergewissern Sie sich, dass im Ergebnisbereich ein Zertifikat angezeigt wird, für das in der Spalte **Beabsichtigter Zweck** der Wert **Clientauthentifizierung** und in der Spalte **Zertifikatvorlage** der Wert **ConfigMgr-Clientverteilungspunktzertifikat** angezeigt wird.  

13. Lassen Sie das Dialogfeld **Zertifikate (Lokaler Computer)**geöffnet.  

###  <a name="a-namebkmkexportclientdistributionpoint22008a-exporting-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> Exportieren des Clientzertifikats für Verteilungspunkte  
 Mithilfe dieser Prozedur können Sie das benutzerdefinierte Zertifikat zur Arbeitsstationsauthentifizierung in eine Datei exportieren, um diese in die Eigenschaften des Verteilungspunkts zu importieren.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>So exportieren Sie das Clientzertifikat für Verteilungspunkte  

1.  Klicken Sie in der Konsole **Zertifikate (Lokaler Computer)** mit der rechten Maustaste auf das soeben installierte Zertifikat, wählen Sie **Alle Tasks**aus, und klicken Sie dann auf **Exportieren**.  

2.  Klicken Sie im Assistenten zum Exportieren von Zertifikaten auf **Weiter**.  

3.  Wählen Sie auf der Seite **Privaten Schlüssel exportieren** die Option **Ja, privaten Schlüssel exportieren**aus, und klicken Sie auf **Weiter**.  

    > [!NOTE]  
    >  Ist diese Option nicht verfügbar, wurde das Zertifikat ohne Option zum Exportieren des privaten Schlüssels erstellt. In diesem Szenario können Sie das Zertifikat nicht im erforderlichen Format exportieren. Sie müssen die Konfiguration der Zertifikatvorlage so anpassen, dass der private Schlüssel exportiert werden kann, und dann das Zertifikat erneut anfordern.  

4.  Auf der Seite **Format der zu exportierenden Datei** muss die Option **Privater Informationsaustausch - PKCS #12 (.PFX)** ausgewählt sein.  

5.  Geben Sie auf der Seite **Kennwort** ein sicheres Kennwort zum Schutz des exportierten Zertifikats mit seinem privaten Schlüssel an, und klicken Sie auf **Weiter**.  

6.  Geben Sie auf der Seite **Zu exportierende Datei** den Namen der Datei an, die exportiert werden soll, und klicken Sie auf **Weiter**.  

7.  Klicken Sie auf **Fertig stellen** , um den ** ** Assistenten zum Exportieren von Zertifikaten zu schließen, und klicken Sie dann im Bestätigungsdialogfeld auf **OK** .  

8.  Schließen Sie das Dialogfeld **Zertifikate (Lokaler Computer)**.  

9. Speichern Sie die Datei an einem sicheren Ort, und gewährleisten Sie, dass Sie von der System Center Configuration Manager-Konsole darauf zugreifen können.  

 Das Zertifikat kann nun im Rahmen der Konfiguration des Verteilungspunkts importiert werden.  

> [!TIP]  
>  Dieselbe Zertifikatdatei können Sie verwenden, wenn Sie Medienabbilder für eine Betriebssystembereitstellung konfigurieren, bei der kein PXE-Start verwendet wird; die Tasksequenz zur Installation des Abbilds muss einen Verwaltungspunkt kontaktieren, der HTTPS-Clientverbindungen erfordert.  

##  <a name="a-namebkmkmobiledevices2008cm2012a-deploying-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> Bereitstellen des Anmeldungszertifikats für mobile Geräte  
 Diese Zertifikatbereitstellung besteht aus einer einzigen Prozedur zum Erstellen und Ausstellen der Anmeldungszertifikatvorlage bei der Zertifizierungsstelle.  

### <a name="creating-and-issuing-the-enrollment-certificate-template-on-the-certification-authority"></a>Erstellen und Ausstellen der Anmeldungszertifikatvorlage bei der Zertifizierungsstelle  
 Dieses Verfahren erstellt eine Registrierungszertifikatvorlage für mobile Geräte für System Center Configuration Manager und fügt sie der Zertifizierungsstelle hinzu.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>So erstellen Sie die Anmeldungszertifikatvorlage und stellen sie bei der Zertifizierungsstelle aus  

1.  Erstellen Sie eine Sicherheitsgruppe mit Benutzern, die mobile Geräte in System Center Configuration Manager registrieren werden.  

2.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifikatdienste installiert sind, in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, und klicken Sie dann auf **Verwalten** , um die Verwaltungskonsole für Zertifikatvorlagen zu laden.  

3.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Text **Authentifizierte Sitzung**angezeigt wird, und klicken Sie dann auf **Doppelte Vorlage**.  

4.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

5.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen zum Generieren der Registrierungszertifikate für die mobilen Geräte ein, die von System Center Configuration Manager verwaltet werden sollen, z.B. **ConfigMgr-Registrierungszertifikat für mobile Geräte**.  

6.  Klicken Sie auf die Registerkarte **Antragsteller** , überprüfen Sie, ob **Aus diesen Informationen in Active Directory erstellen** ausgewählt ist, wählen Sie für **Format des Antragstellernamens** die Option **Allgemeiner Name** aus, und löschen Sie unter **Informationen im alternativen Antragstellernamen einbeziehen** den Eintrag **Benutzerprinzipalname (UPN)**.  

7.  Klicken Sie auf die Registerkarte **Sicherheit** , wählen Sie die Sicherheitsgruppe mit Benutzern aus, die mobile Geräte anmelden müssen, und wählen Sie die zusätzliche Berechtigung **Anmelden**aus. Lassen Sie **Lesen**aktiviert.  

8.  Klicken Sie auf **OK** , und schließen Sie die **Zertifikatvorlagenkonsole**.  

9. Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, klicken Sie auf **Neu**und dann auf **Auszustellende Zertifikatvorlage**.  

10. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr-Anmeldungszertifikat für mobile Geräte**aus, und klicken Sie dann auf **OK**.  

11. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole Zertifizierungsstelle.  

 Sie können die Anmeldungszertifikatvorlage für mobile Geräte jetzt in den Clienteinstellungen beim Konfigurieren eines Anmeldungsprofils für mobile Geräte auswählen.  

##  <a name="a-namebkmkamt2008cm2012a-deploying-the-certificates-for-amt"></a><a name="BKMK_AMT2008_cm2012"></a> Bereitstellen der Zertifikate für AMT  
 Diese Zertifikatbereitstellung besteht aus den folgenden Prozeduren:  

-   Erstellen, Ausstellen und Installieren des AMT-Bereitstellungszertifikats  

-   Erstellen und Ausstellen des Webserverzertifikats für AMT-basierte Computer  

-   Erstellen und Ausstellen der Clientauthentifizierungszertifikate für AMT-basierte Computer mit 802.1X-Authentifizierung  

###  <a name="a-namebkmkamtprovisioning2008a-creating-issuing-and-installing-the-amt-provisioning-certificate"></a><a name="BKMK_AMTprovisioning2008"></a> Creating, Issuing, and Installing the AMT Provisioning Certificate  
 Erstellen Sie das Bereitstellungszertifikat mit Ihrer internen Zertifizierungsstelle, wenn die AMT-basierten Computer mit dem Zertifikatfingerabdruck Ihrer internen Stammzertifizierungsstelle konfiguriert sind. Wenn dies nicht der Fall ist und Sie eine externe Zertifizierungsstelle verwenden müssen, folgen Sie den Anweisungen des Unternehmens, von dem das AMT-Bereitstellungszertifikat ausgestellt wurde. Dies umfasst in der Regel das Anfordern des Zertifikats auf der öffentlichen Unternehmenswebsite. Im Intel vPro Expert Center finden Sie auf den Seiten zur Microsoft vPro-Verwaltbarkeit zudem ausführliche Anweisungen für externe Zertifizierungsstellen:[http://go.microsoft.com/fwlink/?LinkId=132001](http://go.microsoft.com/fwlink/?LinkId=132001).  

> [!IMPORTANT]  
>  Nicht alle externen Zertifizierungsstellen bieten eine Unterstützung der Objekt-ID für die Intel AMT-Bereitstellung. In diesem Fall können Sie das OU-Attribut **Intel(R) Client Setup Certificate**verwenden.  

 Wenn Sie ein AMT-Bereitstellungszertifikat von einer externen Zertifizierungsstelle anfordern, installieren Sie das Zertifikat im persönlichen Zertifikatspeicher des Mitgliedsservers, der als Host für den Out-of-Band-Dienstpunkt dienen soll.  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>So fordern Sie das AMT-Bereitstellungszertifikat an und stellen es aus  

1.  Erstellen Sie eine Sicherheitsgruppe mit den Computerkonten der Standortsystemserver, auf denen der Out-of-Band-Dienstpunkt ausgeführt werden soll.  

2.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifikatdienste installiert sind, in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, und klicken Sie dann auf **Verwalten** , um die Konsole **Zertifikatvorlagen** zu laden.  

3.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Webserver** angezeigt wird, und klicken Sie dann auf **Doppelte Vorlage**.  

4.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

5.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Namen für die Vorlage des AMT-Bereitstellungszertifikats an, zum Beispiel **ConfigMgr-AMT-Bereitstellung**.  

6.  Wählen Sie auf der Registerkarte **Antragstellername** die Option **Aus diesen Informationen in Active Directory erstellen**aus, und wählen Sie **Allgemeiner Name**.  

7.  Wählen Sie auf der Registerkarte **Erweiterungen** die Option **Anwendungsrichtlinien** aus, und klicken sie dann auf **Bearbeiten**.  

8.  Klicken Sie im Dialogfeld **Anwendungsrichtlinienerweiterung bearbeiten** auf **Hinzufügen**.  

9. Klicken Sie im Dialogfeld **Anwendungsrichtlinie hinzufügen** auf **Neu**.  

10. Geben Sie im Dialogfeld **Neue Anwendungsrichtlinie** im Feld **Name** die Bezeichnung **AMT-Bereitstellung** ein, und geben Sie anschließend folgende Zahl als **Objekt-ID**ein: **2.16.840.1.113741.1.2.3**.  

11. Klicken Sie auf **OK**, und klicken Sie anschließend im Dialogfeld **Anwendungsrichtlinie hinzufügen** auf **OK** .  

12. Klicken Sie im Dialogfeld **Anwendungsrichtlinienerweiterung bearbeiten** auf **OK** .  

13. Im Dialogfeld **Eigenschaften der neuen Vorlage** sollte nun folgende Beschreibung unter **Anwendungsrichtlinien** angezeigt werden: **Serverauthentifizierung** und **AMT-Bereitstellung**.  

14. Klicken Sie auf die Registerkarte **Sicherheit** , und entfernen Sie aus den Sicherheitsgruppen **Domänen-Admins** und **Organisations-Admins** die Berechtigung **Anmelden**.  

15. Klicken Sie auf **Hinzufügen**, geben Sie den Namen einer Sicherheitsgruppe ein, die das Computerkonto für die Standortsystemrolle „Out-of-Band-Dienstpunkt“ enthält, und klicken Sie dann auf **OK**.  

16. Wählen Sie für diese Gruppe die Berechtigung **Anmelden** aus, und lassen Sie die Berechtigung **Lesen** aktiviert.  

17. Klicken Sie auf **OK**, und schließen Sie die Konsole **Zertifikatvorlagen** .  

18. Klicken Sie in der Konsole **Zertifizierungsstelle**mit der rechten Maustaste auf **Zertifikatvorlagen**, klicken Sie auf **Neu**und dann auf **Auszustellende Zertifikatvorlage**.  

19. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr-AMT-Bereitstellung**aus, und klicken Sie dann auf **OK**.  

    > [!NOTE]  
    >  Wenn Sie die Schritte 18 oder 19 nicht ausführen können, prüfen Sie, ob die Enterprise Edition von Windows Server 2008 verwendet wird. Mit Windows Server Standard Edition und Zertifikatdiensten können Sie zwar Vorlagen konfigurieren, aber das Bereitstellen von Zertifikaten mit geänderten Zertifikatsvorlagen ist nur mit Windows Server 2008 Enterprise möglich.  

20. Lassen Sie die Konsole **Zertifizierungsstelle**geöffnet.  

 Das AMT-Bereitstellungszertifikat von Ihrer internen Zertifizierungsstelle kann jetzt auf dem Out-of-Band-Dienstpunktcomputer installiert werden.  

##### <a name="to-install-the-amt-provisioning-certificate"></a>So installieren Sie das AMT-Bereitstellungszertifikat  

1.  Starten Sie den Mitgliedsserver, auf dem IIS ausgeführt wird, neu, um sicherzustellen, dass der Zugriff auf die Zertifikatvorlage mit der konfigurierten Berechtigung möglich ist.  

2.  Klicken Sie auf **Start**, klicken Sie auf **Ausführen**, und geben Sie **mmc.exe** ein. Klicken Sie in der leeren Konsole auf **Datei**angezeigt wird, und klicken Sie auf **Snap-In hinzufügen/entfernen**.  

3.  Wählen Sie im Dialogfeld **Snap-In hinzufügen/entfernen** aus der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**.  

4.  Wählen Sie im Dialogfeld **Zertifikat-Snap-In** die Option **Computerkonto**aus, und klicken Sie auf **Weiter**.  

5.  Vergewissern Sie sich, dass im Dialogfeld **Computer auswählen** die Option **Lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist. Klicken Sie anschließend auf **Fertig stellen**.  

6.  Klicken Sie im Dialogfeld **Snap-Ins hinzufügen/entfernen** auf **OK**.  

7.  Erweitern Sie in der Konsole **Zertifikate (Lokaler Computer)**, und klicken Sie dann auf **Persönlich**.  

8.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, klicken Sie auf **Alle Tasks**und dann auf **Neues Zertifikat anfordern**.  

9. Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  

10. Wenn die Seite **Zertifikatregistrierungsrichtlinie auswählen** angezeigt wird, klicken Sie auf **Weiter**.  

11. Wählen Sie auf der Seite **Zertifikate anfordern** in der Liste der angezeigten Zertifikate **AMT-Bereitstellung** aus, und klicken Sie dann auf **Anmelden**.  

12. Warten Sie, bis auf der Seite mit den **Ergebnissen der Zertifikatinstallation** angezeigt wird, dass das Zertifikat installiert wurde. Klicken Sie dann auf **Fertig stellen**.  

13. Schließen Sie das Dialogfeld **Zertifikate (Lokaler Computer)**.  

 Das AMT-Bereitstellungszertifikat von Ihrer internen Zertifizierungsstelle ist jetzt installiert und kann in den Eigenschaften des Out-of-Band-Dienstpunkts ausgewählt werden.  

### <a name="creating-and-issuing-the-web-server-certificate-for-amt-based-computers"></a>Erstellen und Ausstellen des Webserverzertifikats für AMT-basierte Computer  
 Gehen Sie folgendermaßen vor, um die Webserverzertifikate für AMT-basierte Computer vorzubereiten.  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>So erstellen Sie die Webserverzertifikatvorlage und stellen sie aus  

1.  Erstellen Sie eine leere Sicherheitsgruppe für die AMT-Benutzerkonten, die während der AMT-Bereitstellung von System Center Configuration Manager erstellt werden.  

2.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifikatdienste installiert sind, in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, und klicken Sie dann auf **Verwalten** , um die Konsole **Zertifikatvorlagen** zu laden.  

3.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Webserver**angezeigt wird, und klicken Sie auf **Doppelte Vorlage**.  

4.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition.**  

5.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen für die zu generierenden Webzertifikate ein, die für die Out-of-Band-Verwaltung auf AMT-Computern verwendet werden sollen, z. B. **ConfigMgr-AMT-Webserverzertifikat**.  

6.  Klicken Sie auf die Registerkarte **Antragsteller** , klicken Sie auf **Aus diesen Informationen in Active Directory erstellen**, wählen Sie für **Format des Antragstellernamens** die Option **Allgemeiner Name**aus, und löschen Sie dann für den alternativen Antragstellernamen den Eintrag **Benutzerprinzipalname (UPN)** .  

7.  Klicken Sie auf die Registerkarte **Sicherheit** , und entfernen Sie aus den Sicherheitsgruppen **Domänen-Admins** und **Organisations-Admins** die Berechtigung **Anmelden**.  

8.  Klicken Sie auf **Hinzufügen** , und geben Sie den Namen der für die AMT-Bereitstellung erstellten Sicherheitsgruppe ein. Klicken Sie anschließend auf **OK**.  

9. Wählen Sie für diese Sicherheitsgruppe die folgenden Berechtigungen vom Typ **Zulassen** aus: **Lesen** und **Einschreiben**.  

10. Klicken Sie auf **OK**, und schließen Sie die Konsole **Zertifikatvorlagen** .  

11. Klicken Sie in der Konsole **Zertifizierungsstelle** mit der rechten Maustaste auf **Zertifikatvorlagen**, klicken Sie auf **Neu**und dann auf **Auszustellende Zertifikatvorlage**.  

12. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage mit der Bezeichnung **ConfigMgr-AMT-Webserverzertifikat**aus, und klicken Sie auf **OK**.  

13. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

 Die AMT-Webservervorlage kann jetzt zur Bereitstellung von AMT-basierten Computern mit Webserverzertifikaten verwendet werden. Wählen Sie diese Zertifikatvorlage in den Eigenschaften der Out-of-Band-Verwaltungskomponente aus.  

### <a name="creating-and-issuing-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>Erstellen und Ausstellen der Clientauthentifizierungszertifikate für AMT-basierte Computer mit 802.1X-Authentifizierung  
 Gehen Sie wie folgt vor, wenn für AMT-basierte Computer Clientzertifikate in 802.1X-authentifizierten Kabel- und Drahtlosnetzwerken verwendet werden sollen.  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>So können Sie die Zertifikatvorlage für die Clientauthentifizierung bei der Zertifizierungsstelle generieren und ausstellen  

1.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifikatdienste installiert sind, in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, und klicken Sie dann auf **Verwalten** , um die Konsole **Zertifikatvorlagen** zu laden.  

2.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Arbeitsstationsauthentifizierung**angezeigt wird, und klicken Sie auf **Doppelte Vorlage**.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition.**  

3.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen für die zu generierenden Clientzertifikate ein, die für die Out-of-Band-Verwaltung auf AMT-Computern verwendet werden sollen, z. B. **ConfigMgr-AMT-Clientauthentifizierungszertifikat_802.1X**.  

4.  Klicken Sie auf der Registerkarte **Antragstellername** auf **Aus diesen Informationen in Active Directory erstellen** , und wählen Sie dann für **Format des Antragstellernamens** die Option **Allgemeiner Name**aus. Deaktivieren Sie für den alternativen Antragstellernamen das Kontrollkästchen **DNS-Name** , und wählen Sie dann **Benutzerprinzipalname (UPN)**aus.  

5.  Klicken Sie auf die Registerkarte **Sicherheit** , und entfernen Sie aus den Sicherheitsgruppen **Domänen-Admins** und **Organisations-Admins** die Berechtigung **Anmelden**.  

6.  Klicken Sie auf **Hinzufügen** , und geben Sie den Namen der Sicherheitsgruppe ein, die Sie in den Eigenschaften der Out-of-Band-Verwaltungskomponente für die Benutzerkonten der AMT-basierten Computer angeben werden. Klicken Sie anschließend auf **OK**.  

7.  Wählen Sie für diese Sicherheitsgruppe die folgenden Berechtigungen vom Typ **Zulassen** aus: **Lesen** und **Einschreiben**.  

8.  Klicken Sie auf **OK**, und schließen Sie die Verwaltungskonsole **Zertifikatvorlagen**, **certtmpl – [Zertifikatvorlagen]**.  

9. Klicken Sie in der Verwaltungskonsole der ** ** Zertifizierungsstelle mit der rechten Maustaste auf **Zertifikatvorlagen**, klicken Sie auf **Neu**und dann auf **Auszustellende Zertifikatvorlage**.  

10. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage mit der Bezeichnung **ConfigMgr-AMT-Clientauthentifizierungszertifikat_802.1X**aus, und klicken Sie auf **OK**.  

11. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

 Die Zertifikatvorlage für die Clientauthentifizierung kann jetzt zum Ausstellen von Zertifikaten auf AMT-basierten Computern für die 802.1X-Clientauthentifizierung verwendet werden. Wählen Sie diese Zertifikatvorlage in den Eigenschaften der Out-of-Band-Verwaltungskomponente aus.  

##  <a name="a-namebkmkmacclientsp1a-deploying-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> Bereitstellen des Clientzertifikats für Macintosh-Computer  

> [!NOTE]  
>  Das Clientzertifikat für Macintosh-Computer gilt für System Center Configuration Manager SP1 und höher.  

 Diese Zertifikatbereitstellung besteht aus einer einzigen Prozedur zum Erstellen und Ausstellen der Anmeldungszertifikatvorlage bei der Zertifizierungsstelle.  

###  <a name="a-namebkmkmacclientcreatingissuinga-creating-and-issuing-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> Erstellen und Ausstellen einer Clientzertifikatvorlage für Macintosh bei der Zertifizierungsstelle  
 Dieses Verfahren erstellt eine benutzerdefinierte Zertifikatvorlage für Macintosh-Computer für System Center Configuration Manager und fügt das Zertifikat der Zertifizierungsstelle hinzu.  

> [!NOTE]  
>  In dieser Prozedur wird eine andere Zertifikatvorlage verwendet als die Zertifikatvorlage, die Sie möglicherweise für Windows-Clientcomputer oder für Verteilungspunkte erstellt haben.  
>   
>  Durch das Erstellen einer neuen Zertifikatvorlage für dieses Zertifikat können Sie die Zertifikatanforderung auf berechtigte Benutzer beschränken.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>So erstellen Sie die Clientzertifikatvorlage für Macintosh bei der Zertifizierungsstelle  

1.  Erstellen Sie eine Sicherheitsgruppe, die Benutzerkonten für Administratoren enthält, die das Zertifikat auf dem Macintosh-Computer über System Center Configuration Manager registrieren.  

2.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifizierungsstellenkonsole ausgeführt wird, mit der rechten Maustaste auf **Zertifikatvorlagen**, und klicken Sie dann auf **Verwalten** , um die Verwaltungskonsole für Zertifikatvorlagen zu laden.  

3.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Text **Authentifizierte Sitzung**angezeigt wird, und klicken Sie dann auf **Doppelte Vorlage**.  

4.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

5.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen zur Erstellung des Macintosh-Clientzertifikats ein, beispielsweise **ConfigMgr – Macintosh-Clientzertifikat**.  

6.  Klicken Sie auf die Registerkarte **Antragsteller** , überprüfen Sie, ob **Aus diesen Informationen in Active Directory erstellen** ausgewählt ist, wählen Sie für **Format des Antragstellernamens** die Option **Allgemeiner Name** aus, und löschen Sie unter **Informationen im alternativen Antragstellernamen einbeziehen** den Eintrag **Benutzerprinzipalname (UPN)**.  

7.  Klicken Sie auf die Registerkarte **Sicherheit** , und entfernen Sie aus den Sicherheitsgruppen **Domänen-Admins** und **Organisations-Admins** die Berechtigung **Anmelden** .  

8.  Klicken Sie auf **Hinzufügen**, geben Sie die Sicherheitsgruppe an, die Sie im ersten Schritt erstellt haben, und klicken Sie dann auf **OK**.  

9. Wählen Sie für diese Gruppe die Berechtigung **Anmelden** aus, und lassen Sie die Berechtigung **Lesen** aktiviert.  

10. Klicken Sie auf **OK** , und schließen Sie die **Zertifikatvorlagenkonsole**.  

11. Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, klicken Sie auf **Neu**und dann auf **Auszustellende Zertifikatvorlage**.  

12. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr – Macintosh-Clientzertifikat**aus, und klicken Sie auf **OK**.  

13. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

 Die Clientzertifikatvorlage für Macintosh kann jetzt ausgewählt werden, wenn Sie Clienteinstellungen für die Anmeldung konfigurieren.



<!--HONumber=Dec16_HO3-->


