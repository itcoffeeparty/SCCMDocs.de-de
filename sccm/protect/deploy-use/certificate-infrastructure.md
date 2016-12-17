---
title: Konfigurieren der Zertifikatinfrastruktur | System Center Configuration Manager
description: Erfahren Sie mehr zum Konfigurieren der Zertifikatregistrierung in System Center Configuration Manager.
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
caps.latest.revision: 7
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: 9af69a813a1fe2a07e3b7b289e258b2d0b51a6f7

---
# <a name="certificate-infrastructure"></a>Zertifikatinfrastruktur

*Gilt für: System Center Configuration Manager (Current Branch)*


 Hier finden Sie die Schritte, Details und weitere Informationen zum Konfigurieren der Zertifikatregistrierung in System Center Configuration Manager. Überprüfen Sie, bevor Sie beginnen, die in [Voraussetzungen für Zertifikatprofile in System Center Configuration Manager](../../protect/plan-design/prerequisites-for-certificate-profiles.md) aufgeführten Voraussetzungen.  

 Nachdem Sie diese Schritte abgeschlossen und die Installation überprüft haben, können Sie Zertifikatprofile konfigurieren und bereitstellen. Weitere Informationen finden Sie unter [Erstellen von Zertifikatprofilen in System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  


**Schritt 1:** Installieren und Konfigurieren des Registrierungsdiensts für Netzwerkgeräte und der Abhängigkeiten Der Rollendienst „Registrierungsdienst für Netzwerkgeräte“ für Active Directory-Zertifikatdienste (AD CS) muss unter dem Betriebssystem Windows Server 2012 R2 ausgeführt werden.
     **Wichtig:** Sie müssen weitere Konfigurationsschritte ausführen, bevor Sie den Registrierungsdienst für Netzwerkgeräte mit System Center Configuration Manager verwenden können.
**Schritt 2:** Installieren und Konfigurieren des Zertifikatregistrierungspunkts Sie müssen mindestens einen Zertifikatregistrierungspunkt installieren. Dieser Registrierungspunkt kann sich wahlweise an einem Standort der zentralen Verwaltung oder an einem primären Standort befinden.
**Schritt 3:** Installieren des System Center Configuration Manager-Richtlinienmoduls Installieren Sie das Richtlinienmodul auf dem Server mit dem Registrierungsdienst für Netzwerkgeräte.

## <a name="supplemental-procedures-to-configure-certificate-enrollment-in-configuration-manager"></a>Zusätzliche Verfahren zum Konfigurieren der Zertifikatregistrierung in Configuration Manager  
 Verwenden Sie die folgenden Informationen, wenn die Schritte in der vorstehenden Tabelle zusätzliche Verfahren erfordern.  

###  <a name="step-1-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Schritt 1: Installieren und Konfigurieren des Registrierungsdiensts für Netzwerkgeräte und der Abhängigkeiten  
 Sie müssen den Rollendienst „Registrierungsdienst für Netzwerkgeräte“ für Active Directory-Zertifikatdienste (AD CS) installieren und konfigurieren, die Sicherheitsberechtigungen für die Zertifikatvorlagen ändern, ein PKI-Zertifikat (Public Key Infrastructure) zur Clientauthentifizierung bereitstellen und die Registrierung bearbeiten, um das standardmäßige URL-Größenlimit für IIS anzuheben. Bei Bedarf müssen Sie zudem die ausstellende Zertifizierungsstelle so konfigurieren, dass ein benutzerdefinierter Gültigkeitszeitraum zulässig ist.  

> [!IMPORTANT]  
>  Überprüfen Sie die Installation und Konfiguration des Registrierungsdiensts für Netzwerkgeräte, bevor Sie System Center Configuration Manager für den Registrierungsdienst für Netzwerkgeräte konfigurieren. Wenn diese Abhängigkeiten nicht ordnungsgemäß funktionieren, wird die Problembehandlung der Zertifikatregistrierung mit System Center Configuration Manager erschwert.  

##### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>So installieren und konfigurieren Sie den Registrierungsdienst für Netzwerkgeräte und die Abhängigkeiten  

1.  Installieren und konfigurieren Sie auf einem Server unter Windows Server 2012 R2 den Rollendienst „Registrierungsdienst für Netzwerkgeräte“ für die Serverrolle „Active Directory-Zertifikatdienste“. Weitere Informationen finden Sie im [Leitfaden für den Registrierungsdienst für Netzwerkgeräte](http://go.microsoft.com/fwlink/p/?LinkId=309016) in der Bibliothek zu Active Directory-Zertifikatdiensten in TechNet.  

2.  Überprüfen Sie die Sicherheitsberechtigungen für die Zertifikatvorlagen, die vom Registrierungsdienst für Netzwerkgeräte verwendet werden, und ändern Sie sie bei Bedarf:  

    -   Für das Konto, das die System Center Configuration Manager-Konsole ausführt: die Berechtigung **Lesen**.  

         Diese Berechtigung ist erforderlich, damit Sie während der Ausführung des Assistenten zum Erstellen von Zertifikatprofilen die Zertifikatvorlage suchen und auswählen können, die Sie bei der Erstellung eines SCEP-Einstellungsprofils verwenden möchten. Durch die Auswahl einer Zertifikatvorlage werden einige Einstellungen im Assistenten automatisch festgelegt. Sie müssen also weniger Einstellungen konfigurieren, und die Gefahr, dass Sie Einstellungen auswählen, die mit den vom Registrierungsdienst für Netzwerkgeräte verwendeten Zertifikatvorlagen nicht kompatibel sind, wird verringert.  

    -   Für das SCEP-Dienstkonto, das vom Anwendungspool des Registrierungsdiensts für Netzwerkgeräte verwendet wird: Berechtigungen **Lesen** und **Anmelden** .  

         Diese Anforderung gilt nicht nur für System Center Configuration Manager, sondern ist Bestandteil der Konfiguration des Registrierungsdiensts für Netzwerkgeräte. Weitere Informationen finden Sie im [Leitfaden für den Registrierungsdienst für Netzwerkgeräte](http://go.microsoft.com/fwlink/p/?LinkId=309016) in der Bibliothek zu Active Directory-Zertifikatdiensten in TechNet.  

    > [!TIP]  
    >  Zeigen Sie auf dem Server, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird, den folgenden Registrierungsschlüssel an, um die vom Registrierungsdienst für Netzwerkgeräte verwendeten Zertifikatvorlagen zu ermitteln: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

    > [!NOTE]  
    >  Dies sind die standardmäßigen Sicherheitsberechtigungen, die für die meisten Umgebungen geeignet sind. Sie können auch eine alternative Sicherheitskonfiguration verwenden. Weitere Informationen finden Sie unter [Planen der Berechtigungen von Zertifikatvorlagen für Zertifikatprofile in System Center Configuration Manager](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3.  Stellen Sie auf diesem Server ein PKI-Zertifikat bereit, das die Clientauthentifizierung unterstützt. Es ist möglich, dass bereits ein geeignetes Zertifikat auf dem Computer installiert ist, das Sie verwenden können. Möglicherweise müssen (oder möchten) Sie aber auch ein Zertifikat speziell für diesen Zweck bereitstellen. Weitere Informationen zu den Anforderungen für dieses Zertifikat finden Sie in den Details für Server, auf denen das System Center Configuration Manager-Richtlinienmodul mit dem Rollendienst „Registrierungsdienst für Netzwerkgeräte“ ausgeführt wird. Diese finden Sie im Abschnitt **PKI-Zertifikate für Server** des Themas [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  

    > [!TIP]  
    >  Falls Sie Hilfe bei der Bereitstellung dieses Zertifikats benötigen, können Sie die Anweisungen unter [Bereitstellen des Clientzertifikats für Verteilungspunkte](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012) verwenden, da die Zertifikatanforderungen mit einer einzigen Ausnahme identisch sind:  
    >   
    >  -   Aktivieren Sie nicht das Kontrollkästchen **Exportieren von privatem Schlüssel zulassen** auf der Registerkarte **Anforderungsverarbeitung** der Eigenschaften der Zertifikatvorlage.  
    >   
    >  Sie müssen dieses Zertifikat nicht mit dem privaten Schlüssel exportieren, da Sie danach im lokalen Computerspeicher suchen und es auswählen können, wenn Sie das System Center Configuration Manager-Richtlinienmodul konfigurieren.  

4.  Suchen Sie das Stammzertifikat, mit dem das Clientauthentifizierungszertifikat verkettet ist. Exportieren Sie dann dieses Zertifikat der Stammzertifizierungsstelle in eine CER-Zertifikatdatei. Speichern Sie diese Datei an einem sicheren Speicherort, auf den Sie sicher zugreifen können, wenn Sie zu einem späteren Zeitpunkt den Standortsystemserver für den Zertifikatregistrierungspunkt installieren und konfigurieren.  

5.  Verwenden Sie auf dem gleichen Server den Registrierungs-Editor, um das standardmäßige URL-Größenlimit für IIS anzuheben. Hierzu legen Sie die DWORD-Werte des folgenden Registrierungsschlüssels unter HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters fest:  

    -   Legen Sie den Schlüssel **MaxFieldLength** auf **65534**fest.  

    -   Legen Sie den Schlüssel **MaxRequestBytes** auf **16777216**fest.  

     Weitere Informationen finden Sie im Artikel [820129: Http.sys-Registrierungseinstellungen für IIS](http://go.microsoft.com/fwlink/?LinkId=309013) in der Microsoft Knowledge Base.  

6.  Ändern Sie auf dem gleichen Server im IIS-Manager (Internet Information Services, Internetinformationsdienste) die Einstellungen für die Anforderungsfilterung für die Anwendung /certsrv/mscep. Starten Sie dann den Server neu. Im Dialogfeld **Einstellungen für die Anforderungsfilterung bearbeiten** sollten die Einstellungen unter **Anforderungslimits** wie folgt lauten:  

    -   **Maximal zulässige Inhaltslänge (Bytes)**: **30000000**  

    -   **Maximale URL-Länge (Bytes)**: **65534**  

    -   **Maximale Länge einer Abfragezeichenfolge (Bytes)**: **65534**  

     Weitere Informationen zu diesen Einstellungen und deren Konfiguration finden Sie im Thema [Requests Limits (Anforderungslimits)](http://go.microsoft.com/fwlink/?LinkId=309014) der Bibliothek mit IIS-Referenzen.  

7.  Wenn Sie ein Zertifikat mit einem kürzeren Gültigkeitszeitraum als dem der verwendeten Zertifikatvorlage anfordern möchten: Diese Konfiguration ist für eine Unternehmenszertifizierungsstelle standardmäßig deaktiviert. Sie können diese Option für eine Unternehmenszertifizierungsstelle mit dem Befehlszeilentool „Certutil“ aktivieren. Verwenden Sie dann die folgenden Befehle, um den Zertifikatdienst zu beenden und neu zu starten:  

    1.  **certutil ‒ setreg Richtlinie\EditFlags +EDITF_ATTRIBUTEENDDATE**  

    2.  **net stop certsvc**  

    3.  **net start certsvc**  

     Weitere Informationen finden Sie unter [Certificate Services Tools and Settings (Tools und Einstellungen für Zertifikatdienste)](http://go.microsoft.com/fwlink/p/?LinkId=309015) in der PKI-Technologiebibliothek auf TechNet.  

8.  Verwenden Sie den folgenden Link als Beispiel, um zu überprüfen, ob der Registrierungsdienst für Netzwerkgeräte funktioniert: **https://server.contoso.com/certsrv/mscep/mscep.dll**. Es sollte die integrierte Webseite „Registrierungsdienst für Netzwerkgeräte“ angezeigt werden. Auf dieser Webseite wird der Dienst erläutert, und Sie erfahren, dass Netzwerkdienste die URL zum Übermitteln von Zertifikatanforderungen verwenden.  

 Nachdem Sie den Registrierungsdienst für Netzwerkgeräte und die Abhängigkeiten konfiguriert haben, können Sie den Zertifikatregistrierungspunkt installieren und konfigurieren.  

###  <a name="step-2-install-and-configure-the-certificate-registration-point"></a>Schritt 2: Installieren und Konfigurieren des Zertifikatregistrierungspunkts  
 Sie müssen mindestens einen Zertifikatregistrierungspunkt in der System Center Configuration Manager-Hierarchie installieren und konfigurieren. Dann können Sie diese Standortsystemrolle wahlweise am Standort der zentralen Verwaltung oder an einem primären Standort installieren.  

> [!IMPORTANT]  
>  Lesen Sie vor der Installation des Zertifikatregistrierungspunkts die Informationen zu Betriebssystemanforderungen und -abhängigkeiten für den Zertifikatregistrierungspunkt im Abschnitt **Anforderungen für Standortsysteme** im Thema [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) .  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>So installieren und konfigurieren Sie den Zertifikatregistrierungspunkt  

1.  Klicken Sie in der System Center Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, klicken Sie auf **Server und Standortsystemrollen**, und wählen Sie dann den Server aus, den Sie als Zertifikatregistrierungspunkt verwenden möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Server** auf **Standortsystemrollen hinzufügen**.  

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an, und klicken Sie dann auf **Weiter**.  

5.  Klicken Sie auf der Seite **Proxy** auf **Weiter**. Für den Zertifikatregistrierungspunkt werden keine Internetproxyeinstellungen verwendet.  

6.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Zertifikatregistrierungspunkt** aus, und klicken Sie dann auf **Weiter**.  

7.  Übernehmen oder ändern Sie auf der Seite **Zertifikatregistrierungspunkt** die Standardeinstellungen, und klicken Sie dann auf **Hinzufügen**.  

8.  Geben Sie im Dialogfeld **URL und Zertifikat der Stammzertifizierungsstelle hinzufügen** Folgendes an, und klicken Sie dann auf **OK**:  

    1.  **URL für den Registrierungsdienst für Netzwerkgeräte:** Geben Sie die URL im folgenden Format an: https://*<FQDN des Servers>*/certsrv/mscep/mscep.dll. Beispiel: Wenn der FQDN des Servers mit dem Registrierungsdienst für Netzwerkgeräte server1.contoso.com ist, geben Sie **https://server1.contoso.com/certsrv/mscep/mscep.dll**ein.  

    2.  **Zertifikat der Stammzertifizierungsstelle**: Navigieren Sie zur CER-Zertifikatdatei, die Sie in **Schritt 1: Installieren und Konfigurieren des Registrierungsdiensts für Netzwerkgeräte und der Abhängigkeiten**erstellt und gespeichert haben, und wählen Sie sie aus. Mit diesem Zertifikat der Stammzertifizierungsstelle kann das Clientauthentifizierungszertifikat, das vom System Center Configuration Manager-Richtlinienmodul verwendet wird, durch den Zertifikatregistrierungspunkt überprüft werden.  

    > [!NOTE]  
    >  Wenn Sie mehrere Server mit dem Registrierungsdienst für Netzwerkgeräte verwenden, klicken Sie auf **Hinzufügen** , um die Details für die weiteren Server anzugeben.  

9. Klicken Sie auf **Weiter** , und schließen Sie den Assistenten ab.  

10. Warten Sie einige Minuten, bis die Installation abgeschlossen ist. Überprüfen Sie dann mit einer der folgenden Methoden, ob der Zertifikatregistrierungspunkt erfolgreich installiert wurde:  

    -   Erweitern Sie im Arbeitsbereich **Überwachung** die Option **Systemstatus**, klicken Sie auf **Komponentenstatus**, und suchen Sie nach Statusmeldungen der Komponente **SMS_CERTIFICATE_REGISTRATION_POINT** .  

    -   Verwenden Sie auf dem Standortsystemserver die Datei „*<Configuration Manager-Installationspfad\>*\Logs\crpsetup.log“ und die Datei „*<Configuration Manager-Installationspfad\>*\Logs\crpmsi.log“. Bei einer erfolgreichen Installation wird der Exitcode 0 zurückgegeben.  

    -   Überprüfen Sie mit einem Browser, ob Sie eine Verbindung mit der URL des Zertifikatregistrierungspunkts herstellen können. Beispiel: https://server1.contoso.com/CMCertificateRegistration. Es sollte eine Seite mit einem **Serverfehler** für den Anwendungsnamen mit einer HTTP 404-Beschreibung angezeigt werden.  

11. Suchen Sie nach der exportierten Zertifikatdatei für die Stammzertifizierungsstelle, die vom Zertifikatregistrierungspunkt automatisch im folgenden Ordner auf dem primären Standortservercomputer erstellt wurde: *<Configuration Manager-Installationspfad\>*\inboxes\certmgr.box. Speichern Sie diese Datei an einem sicheren Speicherort, auf den Sie zu einem späteren Zeitpunkt während der Installation des System Center Configuration Manager-Richtlinienmoduls auf dem Server mit dem Registrierungsdienst für Netzwerkgeräte sicher zugreifen können.  

    > [!TIP]  
    >  Dieses Zertifikat steht nicht sofort in diesem Ordner zur Verfügung. Möglicherweise müssen Sie eine Weile warten (beispielsweise eine halbe Stunde), bis System Center Configuration Manager die Datei in diesen Speicherort kopiert.  

 Nachdem Sie den Zertifikatregistrierungspunkt installiert und konfiguriert haben, können Sie das System Center Configuration Manager-Richtlinienmodul für den Registrierungsdienst für Netzwerkgeräte installieren.  

###  <a name="step-3-install-the-configuration-manager-policy-module"></a>Schritt 3: Installieren des Configuration Manager-Richtlinienmoduls  
 Sie müssen das System Center Configuration Manager-Richtlinienmodul auf jedem Server installieren und konfigurieren, den Sie unter **Schritt 2: Installieren und Konfigurieren des Zertifikatregistrierungspunkts** in den Eigenschaften des Zertifikatregistrierungspunkts als **URL für den Registrierungsdienst für Netzwerkgeräte** angegeben haben.  

##### <a name="to-install-the-policy-module"></a>So installieren Sie das Richtlinienmodul  

1.  Melden Sie sich auf dem Server mit dem Registrierungsdienst für Netzwerkgeräte als Domänenadministrator an, und kopieren Sie die folgenden Dateien aus dem Ordner „<Configuration Manager-Installationsmedium\>\SMSSETUP\POLICYMODULE\X64“ auf dem System Center Configuration Manager-Installationsmedium in einen temporären Ordner:  

    -   PolicyModule.msi  

    -   PolicyModuleSetup.exe  

     Wenn das Installationsmedium den Ordner LanguagePack enthält, kopieren Sie auch diesen Ordner und seinen Inhalt.  

2.  Führen Sie über den temporären Ordner „PolicyModuleSetup.exe“ aus, um den Setup-Assistenten für das System Center Configuration Manager-Richtlinienmodul zu starten.  

3.  Klicken Sie auf der ersten Seite des Assistenten auf **Weiter**, nehmen Sie die Lizenzbedingungen an, und klicken Sie dann auf **Weiter**.  

4.  Übernehmen Sie auf der Seite **Installationsordner** den standardmäßigen Installationsordner für das Richtlinienmodul, oder geben Sie einen anderen Ordner an, und klicken Sie dann auf **Weiter**.  

5.  Geben Sie auf der Seite **Zertifikatregistrierungspunkt** die URL des Zertifikatregistrierungspunkts an, indem Sie den FQDN des Standortsystemservers und den Namen der virtuellen Anwendung verwenden, der in den Eigenschaften des Zertifikatregistrierungspunkts aufgeführt ist. Der Standardname der virtuellen Anwendung lautet „CMCertificateRegistration“. Beispiel: Wenn der Standortsystemserver den FQDN server1.contoso.com aufweist und Sie den Standardnamen der virtuellen Anwendung verwendet haben, geben Sie **https://server1.contoso.com/CMCertificateRegistration**an.  

6.  Übernehmen Sie den Standardport **443** , oder geben Sie die alternative Portnummer an, die vom Zertifikatregistrierungspunkt verwendet wird. Klicken Sie dann auf **Weiter**.  

7.  Navigieren Sie auf der Seite **Clientzertifikat für das Richtlinienmodul**zum Clientauthentifizierungszertifikat, das Sie in **Schritt 1: Installieren und Konfigurieren des Registrierungsdiensts für Netzwerkgeräte und der Abhängigkeiten**bereitgestellt haben, und geben Sie es an. Klicken Sie dann auf **Weiter**.  

8.  Klicken Sie auf der Seite **Zertifikat für Zertifikatregistrierungspunkt** auf **Durchsuchen** , um die exportierte Zertifikatdatei für die Stammzertifizierungsstelle auszuwählen, die Sie am Ende von **Schritt 2: Installieren und Konfigurieren des Zertifikatregistrierungspunkts**gesucht und gespeichert haben.  

    > [!NOTE]  
    >  Wenn Sie diese Zertifikatdatei zuvor nicht gespeichert haben, befindet sie sich im Ordner „<Configuration Manager-Installationspfad\>\inboxes\certmgr.box“ auf dem Standortservercomputer.  

9. Klicken Sie auf **Weiter** , und schließen Sie den Assistenten ab.  

 Nachdem Sie die Konfigurationsschritte für die Installation des Registrierungsdiensts für Netzwerkgeräte und der Abhängigkeiten, des Zertifikatregistrierungspunkts und des System Center Configuration Manager-Richtlinienmoduls abgeschlossen haben, können Sie Zertifikate für Benutzer und Geräte bereitstellen, indem Sie Zertifikatprofile erstellen und bereitstellen. Weitere Informationen zum Erstellen von Zertifikatprofilen finden Sie unter [Erstellen von Zertifikatprofilen in System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  

 Wenn Sie das System Center Configuration Manager-Richtlinienmodul deinstallieren möchten, verwenden Sie hierzu die Option **Programme und Features** in der Systemsteuerung.  



<!--HONumber=Nov16_HO1-->

