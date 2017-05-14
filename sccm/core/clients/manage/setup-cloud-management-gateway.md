---
title: Einrichten des Cloudverwaltungsgateways | Microsoft Docs
description: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 05/01/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.translationtype: Human Translation
ms.sourcegitcommit: d5a6fdc9a526c4fc3a9027dcedf1dd66a6fff5a7
ms.openlocfilehash: 97e1bc6585cee0ff433da0ec0b60b9604cb7348f
ms.contentlocale: de-de
ms.lasthandoff: 05/01/2017

---

# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Einrichten des Cloudverwaltungsgateways für Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1610 umfasst der Prozess zum Einrichten des Cloudverwaltungsgateways in Configuration Manager die folgenden Schritte:

## <a name="step-1-configure-required-certificates"></a>Schritt 1: Konfigurieren der erforderlichen Zertifikate

## <a name="option-1-preferred---use-the-server-authentication-certificate-from-a-public-and-globally-trusted-certificate-provider-like-verisign"></a>Option 1 (bevorzugt) – Verwenden Sie das Serverauthentifizierungszertifikat von einem öffentlichen und global vertrauenswürdigen Zertifikatanbieter (z.B. VeriSign).

Wenn Sie diese Methode verwenden, vertrauen Clients automatisch dem Zertifikat, und Sie müssen benutzerdefinierte SSL-Zertifikate nicht selbst erstellen.

1. Erstellen Sie einen kanonischen Namenseintrag (CNAME) im öffentlichen Domain Name Service (DNS) Ihrer Organisation, um einen Alias für den Cloud Management Gateway-Dienst als Anzeigenamen zu erstellen, der im öffentlichen Zertifikat verwendet wird.
Contoso nennt seinen Cloud Management Gateway-Dienst beispielsweise **GraniteFalls**, der in Azure als **GraniteFalls.CloudApp.Net** angezeigt wird. Im öffentlichen DNS-Namespace von Contoso, „contoso.com“, erstellt der DNS-Administrator einen neuen CNAME-Eintrag für **GraniteFalls.Contoso.com** für den echten Hostnamen **GraniteFalls.CloudApp.net**.
2. Fordern Sie als Nächstes mithilfe des allgemeinen Namens (Common Name, CN) des CNAME-Alias ein Serverauthentifizierungszertifikat von einem öffentlichen Anbieter an.
Contoso verwendet als allgemeinen Namen des Zertifikats z.B. **GraniteFalls.Contoso.com**.
3. Erstellen Sie mithilfe dieses Zertifikats den Cloud Management Gateway-Dienst in der Configuration Manager-Konsole.
    - Wenn Sie auf der Seite **Einstellungen** des Assistenten zum Erstellen von Cloudverwaltungsgateways das Serverzertifikat für diesen Clouddienst (aus der **Zertifikatdatei**) hinzufügen, extrahiert der Assistent als Dienstnamen den Hostnamen aus dem allgemeinen Namen des Zertifikats. Dieser wird dann zur Erstellung des Diensts in Azure als Dienst-FQDN an **cloudapp.net** (oder **usgovcloudapp.net** für die Azure US Government Cloud) angefügt.
Wenn das Cloudverwaltungsgateway z.B. bei Contoso erstellt wird, wird der Hostname **GraniteFalls** aus dem allgemeinen Namen des Zertifikats extrahiert, sodass der eigentliche Dienst in Azure als **GraniteFalls.CloudApp.net** erstellt wird.

### <a name="option-2---create-a-custom-ssl-certificate-for-cloud-management-gateway-in-the-same-way-as-for-a-cloud-based-distribution-point"></a>Option 2 – Erstellen Sie ein benutzerdefiniertes SSL-Zertifikat für das Cloudverwaltungsgateway auf dieselbe Weise wie bei einem cloudbasierten Verteilungspunkt.

Sie können ein benutzerdefiniertes SSL-Zertifikat für das Cloudverwaltungsgateway auf die gleiche Weise erstellen, wie Sie bei einem cloudbasierten Verteilungspunkt vorgehen würden. Führen Sie die Anweisungen zum [Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) durch, tun Sie jedoch folgende Dinge anders:

- Erteilen Sie beim Einrichten der neuen Zertifikatvorlage die Berechtigungen „Lesen“ und **Registrieren** für die Sicherheitsgruppe, die Sie für Configuration Manager-Server einrichten.
- Geben Sie beim Anfordern des benutzerdefinierten Webserverzertifikats für den allgemeinen Namen des Zertifikats einen FQDN an, der auf **cloudapp.net** endet, wenn Sie das Cloudverwaltungsgateway in der öffentlichen Azure-Cloud verwenden möchten, bzw. der auf **usgovcloudapp.net** endet, wenn Sie Azure Government Cloud verwenden möchten.


## <a name="step-2-export-the-client-certificates-root"></a>Schritt 2: Exportieren des Clientstammzertifikats

Die einfachste Möglichkeit zum Export der Clientstammzertifikate im Netzwerk ist, ein Clientzertifikat auf einem Computer zu öffnen und zu kopieren, der einer Domäne angehört, und der über eines verfügt.

> [!NOTE] 
>
> Clientzertifikate sind auf jedem Computer erforderlich, den Sie mit dem Cloudverwaltungsgateway verwalten möchten, und auf jedem Standortsystemserver, der den Cloudverwaltungsgateway-Connectorpunkt hostet. Wenn Sie jedem dieser Computer ein Clientzertifikat hinzufügen müssen, finden Sie mehr Informationen unter [Bereitstellen des Clientzertifikats für Windows-Computer](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

1.  Geben Sie im Ausführungsfenster **Mmc** ein, und drücken Sie die Eingabetaste.

2.  Klicken Sie im Menü „Datei“ auf **Snap-In hinzufügen/entfernen**.

3.  Wählen Sie im Dialogfeld „Snap-In hinzufügen/entfernen“ **Zertifikate** > **Hinzufügen &gt;** > **Computerkonto** > **Weiter** > **Lokaler Computer** > **Fertig stellen** aus. 

4.  Wechseln Sie zu **Zertifikate**&gt;**Privat**&gt;**Zertifikate**.

5.  Doppelklicken Sie auf das Zertifikat zur Clientauthentifizierung auf dem Computer, wählen Sie die Registerkarte „Zertifizierungspfad“ aus, und doppelklicken Sie auf die Stammzertifizierungsstelle (am Anfang des Pfades).

6.  Wählen Sie auf der Registerkarte „Details“ die Option **In Datei kopieren** aus.

7.  Schließen Sie den Zertifikatexportassistenten ab, indem Sie das Standardzertifikatformat verwenden. Notieren Sie sich den Namen und den Speicherort des Stammzertifikats, das Sie erstellen. Sie benötigen es in einem [späteren Schritt](#step-4-set-up-cloud-management-gateway) zum Konfigurieren des Cloudverwaltungsgateways.

## <a name="step-3-upload-the-management-certificate-to-azure"></a>Schritt 3: Hochladen des Verwaltungszertifikats in Azure

Ein Azure-Verwaltungszertifikat ist für Configuration Manager erforderlich, um auf die Azure-API zuzugreifen und das Cloudverwaltungsgateway zu konfigurieren. Weitere Informationen und Anweisungen zum Hochladen eines Verwaltungszertifikats finden Sie unter den folgenden Artikeln in der Azure-Dokumentation:

- [Übersicht über Zertifikate für Azure Cloud Services](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [Hochladen eines Verwaltungszertifikats für die Azure-Verwaltung-API](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>Stellen Sie sicher, dass Sie die Abonnement-ID kopieren, die dem Verwaltungszertifikat zugeordnet ist. Sie benötigen sie im [nächsten Schritt](#step-4-set-up-cloud-management-gateway) zum Konfigurieren des Cloudverwaltungsgateways in der Configuration Manager-Konsole.

### <a name="subordinate-ca-certificates-and-azure"></a>Zertifikate untergeordneter Zertifizierungsstellen und Azure

Wenn das Zertifikat von einer untergeordneten Zertifizierungsstelle (subCA) ausgestellt wird und die PKI-Infrastruktur Ihres Unternehmens sich nicht im Internet befindet, verwenden Sie dieses Verfahren, um das Zertifikat in Azure hochzuladen. 

1. Suchen Sie nach dem Einrichten eines Cloudverwaltungsgateways in Ihrem Azure-Portal nach dem Cloudverwaltungsgateway-Dienst, und wechseln Sie zur Registerkarte **Zertifikat**. Laden Sie Ihr(e) subCA-Zertifikat(e) dort hoch. Wenn Sie über mehrere subCA-Zertifikate verfügen, müssen Sie sie alle hochladen. 
2. Sobald das Zertifikat hochgeladen wurde, notieren Sie seinen Fingerabdruck. 
3. Fügen Sie den Fingerabdruck mithilfe dieses Skripts zur Standortdatenbank hinzu:
    
```

    DIM serviceCName
    DIM subCAThumbprints

    ' Verify arguments
    IF WScript.Arguments.Count <> 2 THEN
    WScript.StdOut.WriteLine "Usage: CScript UpdateSubCAThumbprints.vbs <ServiceCName> <SubCA cert thumbprints, separated by ;>"
    WScript.Quit 1
    END IF

    'Get arguments
    serviceCName = WScript.Arguments.Item(0)
    subCAThumbprints = WScript.Arguments.Item(1)

    'Find SMS Provider
    WScript.StdOut.WriteLine "Searching for SMS Provider for local site..."
    SET objSMSNamespace = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms")
    SET results = objSMSNamespace.ExecQuery("SELECT * From SMS_ProviderLocation WHERE ProviderForLocalSite = true")

    'Process the results
    FOR EACH var in results
    siteCode = var.SiteCode
    NEXT

    IF siteCode = "" THEN
    WScript.StdOut.WriteLine "Failed to locate SMS provider."
    WScript.Quit 1
    END IF

    WScript.StdOut.WriteLine "SiteCode = " & siteCode 

    ' Connect to the SMS namespace
    SET objWMIService = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms\site_" & siteCode)

    'Get instance of SMS_AzureService
    DIM query
    query = "SELECT * From SMS_AzureService WHERE ServiceType = 'CloudProxyService' AND ServiceCName = '" & serviceCName & "'"
    WScript.StdOut.WriteLine "Run WQL query: " &  query
    SET objInstances = objWMIService.ExecQuery(query)

    IF IsNull(objInstances) OR (objInstances.Count = 0) THEN
    WScript.StdOut.WriteLine "Failed to get Azure_Service instance."
    WScript.Quit 1
    END IF

    FOR EACH var IN objInstances
    SET azService = var
    NEXT

    WScript.StdOut.WriteLine "Update [SubCACertThumbprint] to " & subCAThumbprints

    'Update SubCA cert thumbprints
    azService.Properties_.item("SubCACertThumbprint") = subCAThumbprints

    'Save data back to provider
    azService.Put_

    WScript.StdOut.WriteLine "[SubCACertThumbprint] is updated successfully."
```


## <a name="step-4-set-up-cloud-management-gateway"></a>Schritt 4: Einrichten des Cloudverwaltungsgateways

>[!NOTE]
>In Version 1610 ist das Cloudverwaltungsgateway ein Vorabfeature. Wie Sie es aktivieren, erfahren Sie unter [Use pre-release features from updates (Verwenden von vorab veröffentlichten Features von Updates)](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clouddienste** > **Cloudverwaltungsgateway**.
2. Wählen Sie **Cloudverwaltungsgateway erstellen** aus.

3. Geben Sie im Assistenten zur Erstellung des Cloudverwaltungsgateways Ihre Azure-Abonnement-ID (aus dem Azure-Verwaltungsportal kopiert) ein, klicken Sie auf „Durchsuchen“, und wählen Sie die Zertifikatdatei aus, die Sie als Azure-Verwaltungszertifikat hochgeladen haben. Klicken Sie auf **Weiter**, und warten Sie einige Augenblicke, bis sich die Konsole mit Azure verbindet.

4. Füllen Sie die zusätzlichen Details im Assistenten aus:

    - Geben Sie den Namen für den Dienst ein, der in Azure ausgeführt wird. Der Dienstname darf nur alphanumerische Zeichen enthalten und muss aus 3-24 Zeichen bestehen.

    - Wählen Sie die Azure-Region aus, in der der Dienst ausgeführt werden soll.

    - Geben Sie die Anzahl der virtuellen Maschinen an, die Sie für den Dienst verwenden möchten. Der Standardwert ist 1, aber Sie können bis zu 16 virtuelle Computer für den Dienst ausführen.

    >[!NOTE]
    >Wenn Sie für den Cloudverwaltungsgateway-Verbindungspunkt einen Internetproxy verwenden, müssen Sie die Anzahl der Ports auf dem Proxy um die Anzahl der verwendeten virtuellen Maschinen erhöhen, beginnend bei Port 10124.

    - Geben Sie den privaten Schlüssel (PFX-Datei) an, den Sie aus dem benutzerdefinierten SSL-Zertifikat exportiert haben.

    - Geben Sie das aus dem Clientzertifikat exportierte Stammzertifikat an.

    -   Geben Sie den gleichen FQDN-Dienstnamen an, den Sie bei der Erstellung der neuen Zertifikatvorlage verwendet haben. Basierend auf der verwendeten Azure-Cloud müssen Sie eines der folgenden Suffixe für den FQDN-Dienstnamen angeben:

    Azure-Cloud | FQDN-Suffix
    --------------|-------------
    Öffentliche (kommerzielle) Cloud | .cloudapp.net    
    Government-Cloud | .usgovcloudapp.net

  - Deaktivieren Sie das Kontrollkästchen **Clientzertifikatsperre überprüfen** (es sei denn, Sie veröffentlichen Ihre CRL-Informationen).

  - Klicken Sie auf **Weiter**, wenn Sie fertig sind.

5. Wenn Sie den Cloudverwaltungsgateway-Datenverkehr mit einem Schwellenwert von 14 Tagen überwachen möchten, aktivieren Sie Kontrollkästchen für Schwellenwertwarnungen. Legen Sie dann die Schwellenwerte und Prozentsätze für die verschiedenen Warnungsebenen fest. Klicken Sie auf **Weiter**, wenn Sie fertig sind.

6. Überprüfen Sie die Einstellungen, und klicken Sie auf **Weiter**. Configuration Manager beginnt mit der Einrichtung des Diensts. Nach dem Schließen des Assistenten dauert es 5 bis 15 Minuten, bis der Dienst vollständig in Azure bereitgestellt wird. Überprüfen Sie die Spalte **Status** für das neu eingerichtete Cloudverwaltungsgateway, um zu bestimmen, wann der Dienst bereit ist.

## <a name="step-5-configure-primary-site-for-client-certification-authentication"></a>Schritt 5: Konfigurieren des primären Standorts für die Clientzertifikatauthentifizierung

1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**.

2. Wählen Sie den primären Standort für die Clients aus, die Sie über das Cloudverwaltungsgateway verwalten möchten, und klicken Sie auf **Eigenschaften**.

3. Aktivieren Sie auf der Registerkarte „Clientcomputerkommunikation“ im Eigenschaftenblatt für den primären Standort das Kontrollkästchen **PKI-Clientzertifikat (Clientauthentifizierungsfunktion) verwenden, sofern dieses verfügbar ist**.

4. Stellen Sie sicher, dass das Kontrollkästchen **Die Zertifikatsperrliste für Standortsysteme wird von Clients überprüft** deaktiviert ist. Diese Option wäre nur erforderlich, wenn Sie Ihre CRL veröffentlichen würden.


## <a name="step-6-add-the-cloud-management-gateway-connector-point"></a>Schritt 6: Hinzufügen des Cloudverwaltungsgateway-Connectorpunkts

Der Cloudverwaltungsgateway-Connectorpunkt ist eine neue Standortsystemrolle für die Kommunikation mit dem Cloudverwaltungsgateway. Wenn Sie den Cloudverwaltungsgateway-Connectorpunkt hinzufügen möchten, führen Sie die Anweisungen unter [Hinzufügen von Standortsystemrollen für System Center Configuration Manager](/sccm/core/servers/deploy/configure/add-site-system-roles) aus.

## <a name="step-7-configure-roles-for-cloud-management-gateway-traffic"></a>Schritt 7: Konfigurieren von Rollen für Cloudverwaltungsgateway-Datenverkehr

Der letzte Schritt bei der Einrichtung des Cloudverwaltungsgateways ist das Konfigurieren der Standortsystemrollen zum Akzeptieren des Cloudverwaltungsgateway-Datenverkehrs. Für Tech Preview 1606 werden nur die Rollen „Verwaltungspunkt“, „Verteilungspunkt“ und „Softwareupdatepunkt“ für das Cloudverwaltungsgateway unterstützt. Sie müssen jede Rolle einzeln konfigurieren.

1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Server und Standortsystemrollen**.

2. Wählen Sie den Standortsystemserver für die Rolle aus, die Sie für den Cloudverwaltungsgateway-Datenverkehr konfigurieren möchten.

3. Wählen Sie die Rolle aus, und klicken Sie danach auf **Eigenschaften**.

4. Wählen Sie auf dem Eigenschaftenblatt der Rolle unter „Clientverbindungen“ die Option **HTTPS** aus, aktivieren Sie das Kontrollkästchen neben **Datenverkehr über Configuration Manager-Cloudverwaltungsgateway zulassen**, und klicken Sie dann auf **OK**. Wiederholen Sie diese Schritte für die übrigen Rollen.

## <a name="step-8-configure-clients-for-cloud-management-gateway"></a>Schritt 8: Konfigurieren von Clients für das Cloudverwaltungsgateway

Nachdem das Cloudverwaltungsgateway und die Standortsystemrollen vollständig konfiguriert sind und ausgeführt werden, erhalten Clients den Speicherort des Cloudverwaltungsgateway-Diensts automatisch bei der nächsten Anforderung des Speicherorts. Clients müssen sich im Unternehmensnetzwerk befinden, um den Speicherort des Cloudverwaltungsgateway-Diensts zu erhalten. Der Abfragezyklus für Standortanfragen beträgt 24 Stunden. Wenn Sie nicht auf die normal geplante Standortanfragen warten möchten, können Sie sie erzwingen, indem Sie den SMS-Agent-Hostdienst (ccmexec.exe) auf dem Computer neustarten.

Ist der Speicherort des Cloudverwaltungsgateway-Diensts auf dem Client konfiguriert, kann dieser automatisch bestimmen, ob er sich im Intranet oder im Internet befindet. Wenn der Client den Domänencontroller oder den lokalen Verwaltungspunkt kontaktieren kann, verwendet er diesen für die Kommunikation mit Configuration Manager. Andernfalls geht er davon aus, dass er sich im Internet befindet, und verwendet den Speicherort des Cloudverwaltungsgateway-Diensts für die Kommunikation.

>[!NOTE]
> Sie können erzwingen, dass der Client immer das Cloudverwaltungsgateway verwendet, und zwar unabhängig davon, ob er sich im Intranet oder im Internet befindet. Dazu legen Sie den folgenden Registrierungsschlüssel auf dem Clientcomputer fest:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`

Um sicherzustellen, dass Clients Configuration Manager kontaktieren können, führen Sie den folgenden PowerShell-Befehl auf dem Clientcomputer aus:

`gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate`

Dieser Befehl zeigt die Verwaltungspunkte an, die der Client kontaktieren kann, z.B. den Cloudverwaltungsgateway-Dienst.

## <a name="next-steps"></a>Nächste Schritte

[Überwachen von Clients für das Cloudverwaltungsgateway](monitor-clients-cloud-management-gateway.md)

