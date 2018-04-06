---
title: CMG-Zertifikate
description: Lernen Sie die unterschiedlichen digitalen Zertifikate kennen, die Sie mit dem Cloudverwaltungsgateway verwenden können.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 1c7adec8f8919736c61859791802a96766af31bb
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Zertifikate für das Cloudverwaltungsgateway

*Gilt für: System Center Configuration Manager (Current Branch)*

Zur Verwaltung von Clients im Internet mit dem Cloudverwaltungsgateway (cloud management gateway, CMG) benötigen Sie je nach Szenario mindestens ein digitales Zertifikat. Weitere Informationen zu unterschiedlichen Szenarios finden Sie unter [Vorbereiten des Cloudverwaltungsgateways](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="cmg-server-authentication-certificate"></a>CMG-Serverauthentifizierungszertifikat

*Dieses Zertifikat ist für alle Szenarios erforderlich.*

Dieses Zertifikat stellen Sie beim Erstellen des CMG in der Configuration Manager-Konsole bereit.

Das CMG erstellt einen HTTPS-Dienst, mit dem internetbasierte Clients eine Verbindung herstellen. Der Server benötigt ein Serverauthentifizierungszertifikat, um einen sicheren Kanal aufbauen zu können. Sie müssen daher von einem öffentlichen Anbieter ein Zertifikat erwerben oder dieses über Ihre Public Key-Infrastruktur (PKI) ausstellen. Weitere Informationen finden Sie im Abschnitt [Vertrauenswürdige CMG-Stammzertifikate für Clients](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > Zur Identifizierung eines Diensts in Azure ist für dieses Zertifikat ein auf globaler Ebene eindeutiger Name erforderlich. Bevor Sie ein Zertifikat anfordern, müssen Sie daher bestätigen, dass der gewünschte Azure-Domänenname noch nicht verwendet wird. Diesen Vorgang führen Sie im Folgenden beispielhaft für *GraniteFalls.CloudApp.Net* aus. Melden Sie sich zuerst beim [Microsoft Azure-Portal](https://portal.azure.com) an. Rufen Sie anschließend **Ressource erstellen** > **Compute** > **Clouddienst** auf. Geben Sie im Feld **DNS-Name** das gewünschte Präfix ein, z.B. *GraniteFalls*. Auf der Benutzeroberfläche wird angezeigt, ob der Domänenname verfügbar ist oder bereits von einem anderen Dienst verwendet wird. Verwenden Sie diesen Vorgang nicht, um den Dienst im Portal zu erstellen, sondern nur, um die Verfügbarkeit des Namens zu überprüfen. 
  
 > [!NOTE]
 > Das CMG-Serverauthentifizierungszertifikat unterstützt ab Version 1802 auch Platzhalter. Diese werden von einigen Zertifizierungsstellen bei der Ausstellung eines Zertifikat für den Hostnamen verwendet. Ein Beispiel dafür ist **\*contoso.com**. Manche Organisationen verwenden Platzhalterzertifikate, um ihre PKI zu vereinfachen und Wartungskosten zu senken.
 <!--491233-->


### <a name="cmg-trusted-root-certificate-to-clients"></a>Vertrauenswürdige CMG-Stammzertifikate für Clients

Clients sind auf vertrauenswürdige CMG-Stammzertifikate angewiesen. Dieses Vertrauen kann auf zwei Wegen sichergestellt werden:
- Verwenden Sie ein Zertifikat eines öffentlichen und global vertrauenswürdigen Zertifikatanbieters. Hierbei kann es sich beispielsweise um VeriSign oder Thawte handeln. Windows-Clients schließen vertrauenswürdige Stammzertifizierungsstellen von diesen Anbietern ein. Wenn Sie ein Serverauthentifizierungszertifikat von einem dieser Anbieter verwenden, vertrauen Ihre Clients automatisch dem Zertifikat. 
- Verwenden Sie ein Zertifikat, das von einer Unternehmenszertifizierungsstelle über Ihre PKI ausgestellt wird. Die meisten Unternehmens-PKI-Implementierungen integrieren vertrauenswürdige Stammzertifizierungsstellen in Windows-Clients. Ein Beispiel ist die Verwendung von Active Directory-Zertifikatdienste mit einer Gruppenrichtlinie. Wenn Sie das CMG-Serverauthentifizierungszertifikat über eine Zertifizierungsstelle ausstellen, der Ihre Clients nicht automatisch vertrauen, müssen Sie internetbasierten Clients ein vertrauenswürdiges Stammzertifikat der Zertifizierungsstelle hinzufügen.
    - Sie können auch Configuration Manager-Zertifikatprofile verwenden, um Zertifikate für Clients bereitzustellen. Weitere Informationen finden Sie unter [Einführung in Zertifikatprofile](/sccm/protect/deploy-use/introduction-to-certificate-profiles).

### <a name="server-authentication-certificate-issued-by-public-provider"></a>Von einem öffentlichen Anbieter ausgestellte Serverauthentifizierungszertifikate

Wenn Sie diese Methode verwenden, vertrauen Clients automatisch dem Zertifikat, und Sie müssen benutzerdefinierte Zertifikate nicht selbst erstellen. Configuration Manager erstellt den Dienst in Azure mit der Domäne cloudapp.net. Ein öffentlicher Zertifikatanbieter kann für Sie kein Zertifikat mit diesem Namen ausstellen. Erstellen Sie mit den folgenden Schritten einen DNS-Alias:

1. Erstellen Sie einen CNAME-Eintrag für den öffentlichen DNS-Server Ihrer Organisation. Hierdurch wird für das CMG ein Alias erstellt, den Sie als Anzeigename im öffentlichen Zertifikat verwenden können.
Wenn Contoso beispielsweise für das CMG den Namen **GraniteFalls** festlegt, wird in Azure der Name **GraniteFalls.CloudApp.Net** angezeigt. Im öffentlichen DNS-Namespace von Contoso, „contoso.com“, erstellt der DNS-Administrator einen neuen CNAME-Eintrag für **GraniteFalls.Contoso.com** für den echten Hostnamen **GraniteFalls.CloudApp.net**.
2. Fordern Sie mithilfe des allgemeinen Namens (Common Name, CN) des CNAME-Alias ein Serverauthentifizierungszertifikat von einem öffentlichen Anbieter an.
Contoso verwendet als allgemeinen Namen des Zertifikats z.B. **GraniteFalls.Contoso.com**.
3. Erstellen Sie mit diesem Zertifikat das CMG in der Configuration Manager-Konsole. Auf der Seite **Einstellungen** des Assistenten zum Erstellen von Cloudverwaltungsgateways werden folgende Aktionen ausgeführt: 
    - Der Assistent extrahiert als Dienstnamen den Hostnamen aus dem allgemeinen Namen des Zertifikats, sobald Sie das Serverzertifikat für diesen Clouddienst mit der Option **Zertifikatdatei** hinzufügen. 
    - Anschließend fügt der Assistent zur Erstellung des Diensts in Azure den Hostnamen als Dienst-FQDN an **cloudapp.net** oder **usgovcloudapp.net** für die Azure US Government Cloud an.
    - Wenn Contoso beispielsweise das CMG erstellt, extrahiert Configuration Manager den Hostnamen **GraniteFalls** aus dem allgemeinen Namen des Zertifikats. Den eigentlichen Dienst erstellt Azure mit dem Namen **GraniteFalls.CloudApp.net**.

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a>Über eine Unternehmens-PKI ausgestellte Serverauthentifizierungszertifikate

Erstellen Sie ein benutzerdefiniertes SSL-Zertifikat für das CMG, und gehen Sie dabei wie bei der Zertifikaterstellung für einen Cloudverteilungspunkt vor. Führen Sie die Anweisungen zum [Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) durch, aber beachten Sie folgenden Unterschied:

- Geben Sie beim Anfordern des benutzerdefinierten Webserverzertifikats einen FQDN für den allgemeinen Namen des Zertifikats an. Wenn Sie das CMG in einer öffentlichen Azure-Cloud verwenden möchten, müssen Sie für die Azure US Government Cloud einen Namen verwenden, der mit **cloudapp.net** oder **usgovcloudapp.net** endet.



## <a name="azure-management-certificate"></a>Azure-Verwaltungszertifikat

*Dieses Zertifikat ist für klassische Dienstbereitstellungen erforderlich. Für Azure Resource Manager-Bereitstellungen wird es nicht benötigt.*

Dieses Zertifikat stellen Sie im Azure-Portal und beim Erstellen des CMG in der Configuration Manager-Konsole bereit.

Zur Erstellung des CMG in Azure muss sich der Configuration Manager-Dienstverbindungspunkt zuerst bei Ihrem Azure-Abonnement authentifizieren. Bei Nutzung der klassischen Dienstbereitstellung wird von diesem das Azure-Verwaltungszertifikat für die Authentifizierung verwendet. Dieses Zertifikat wird von einem Azure-Administrator für Ihr Abonnement hochgeladen. Stellen Sie das Zertifikat beim Erstellen des CMG in der Configuration Manager-Konsole bereit.

Weitere Informationen und Anweisungen zum Hochladen eines Verwaltungszertifikats finden Sie unter den folgenden Artikeln in der Azure-Dokumentation:

- [Cloud services and management certificates (Clouddienste und Verwaltungszertifikate)](/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)

- [Upload an Azure Service Management Certificate (Hochladen eines Verwaltungszertifikats für Azure-Dienste)](/azure/azure-api-management-certs)

> [!IMPORTANT]
> Stellen Sie sicher, dass Sie die Abonnement-ID kopieren, die dem Verwaltungszertifikat zugeordnet ist. Diese verwenden Sie zur Erstellung des CMG in der Configuration Manager-Konsole.



## <a name="client-authentication-certificate"></a>Clientauthentifizierungszertifikat

*Dieses Zertifikat ist für internetbasierte Clients erforderlich, auf denen Windows 7, Windows 8.1 und Windows 10 ausgeführt wird und die nicht in Azure Active Directory (Azure AD) eingebunden sind. Außerdem wird es für den CMG-Verbindungspunkt benötigt. Nicht erforderlich ist es hingegen für Windows 10-Clients, die in Azure AD eingebunden sind.*

Clients verwenden dieses Zertifikat, um sich bei dem CMG zu authentifizieren. Windows 10-Geräte, die in Hybrid-Azure AD oder in eine Clouddomäne eingebunden sind, benötigen dieses Zertifikat nicht, da sie Azure AD zur Authentifizierung verwenden.

Stellen Sie dieses Zertifikat außerhalb des Configuration Manager-Kontexts bereit. Beispielsweise können Sie mit Active Directory-Zertifikatdienste und einer Gruppenrichtlinie Clientauthentifizierungszertifikate ausstellen. Weitere Informationen finden Sie unter [Bereitstellen des Clientzertifikats für Windows-Computer](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).


### <a name="client-trusted-root-certificate-to-cmg"></a>Vertrauenswürdige Clientstammzertifikate für CMG

*Dieses Zertifikat ist bei der Verwendung von Clientauthentifizierungszertifikaten erforderlich. Wenn alle Clients Azure AD für die Authentifizierung nutzen, wird dieses Zertifikat nicht benötigt.* 

Dieses Zertifikat stellen Sie beim Erstellen des CMG in der Configuration Manager-Konsole bereit.

Das CMG ist auf vertrauenswürdige Clientauthentifizierungszertifikate angewiesen. Dieses Vertrauen kann durch die Bereitstellung einer Vertrauenskette für Stammzertifikate sichergestellt werden. Sie können zwei vertrauenswürdige Stammzertifizierungsstellen und vier Zwischenzertifizierungsstellen (untergeordnete Zertifizierungsstellen) angeben. 


#### <a name="export-the-client-certificates-trusted-root"></a>Exportieren der vertrauenswürdigen Stammzertifizierungsstellen eines Clientauthentifizierungszertifikats

Nachdem Sie ein Clientauthentifizierungszertifikat für einen Computer ausgestellt haben, können Sie mit den folgenden Schritten auf diesem Computer die vertrauenswürdigen Stammzertifizierungsstellen exportieren:

1.  Öffnen Sie das Startmenü. Geben Sie „Ausführen“ ein, um das gleichnamige Fenster zu öffnen. Öffnen Sie **mmc**. 

2.  Klicken Sie im Menü „Datei“ auf **Snap-In hinzufügen/entfernen**.

3.  Klicken Sie im Dialogfeld „Snap-Ins hinzufügen bzw. entfernen“ auf **Zertifikate** und anschließend auf **Hinzufügen>**. 
    a. Klicken Sie im Dialogfeld für das Zertifikat-Snap-In zuerst auf **Computerkonto** und anschließend auf **Weiter**. 
    b. Klicken Sie im Dialogfeld „Computer auswählen“ zuerst auf **Lokaler Computer** und anschließend auf **Fertig stellen**. 
    c. Klicken Sie im Dialogfeld „Snap-Ins hinzufügen bzw. entfernen“ auf **OK**.

4.  Erweitern Sie die Knoten **Zertifikate** und **Eigene Zertifikate**, und klicken Sie anschließend auf **Zertifikate**.

5.  Wählen Sie ein Zertifikat aus, für das als „Beabsichtigter Zweck“ **Clientauthentifizierung** festgelegt ist. 
    a. Klicken Sie im Menü „Aktion“ auf **Öffnen**. 
    b. Wechseln Sie zur Registerkarte **Zertifizierungspfad**. c. Klicken Sie in der Zertifikatskette zuerst auf das übergeordnete Zertifikat und anschließend auf **Zertifikat anzeigen**.

6.  Wechseln im neuen Dialogfeld „Zertifikat“ zur Registerkarte **Details**. Klicken Sie auf **In Datei kopieren...**.

7.  Schließen Sie den Zertifikatexportassistenten ab, indem Sie das Standardzertifikatformat **DER-codiert-binär X.509 (.CER)** verwenden. Notieren Sie sich den Namen und den Speicherort des exportierten Zertifikats.

8. Exportieren Sie alle Zertifikate aus dem Zertifizierungspfad des ursprünglichen Clientauthentifizierungszertifikats. Notieren Sie sich, welche exportierten Zertifikate zu Zwischenzertifizierungsstellen und welche zu vertrauenswürdigen Stammzertifizierungsstellen gehören.



## <a name="enable-management-point-for-https"></a>Aktivieren des Verwaltungspunkts für HTTPS

*Zertifikatanforderungen*
- Beim Verwalten von herkömmlichen Clients mit einer lokalen Identität und einem Clientauthentifizierungszertifikat wird in den Versionen 1706 und 1710 dieses Zertifikat empfohlen, auch wenn es nicht erforderlich ist.
- Beim Verwalten von Windows 10-Clients, die in Azure AD eingebunden sind, wird in der Version 1710 dieses Zertifikat für Verwaltungspunkte benötigt. 
- Ab Version 1802 ist dieses Zertifikat für alle Szenarios erforderlich. 

Stellen Sie dieses Zertifikat außerhalb des Configuration Manager-Kontexts bereit. Beispielsweise können Sie mit Active Directory-Zertifikatdiensten und einer Gruppenrichtlinie ein Webserverzertifikat ausstellen. Weitere Informationen finden Sie unter [PKI-Zertifikatanforderungen](/sccm/core/plan-design/network/pki-certificate-requirements) und [Deploy the web server certificate for site systems that run IIS (Bereitstellen des Webserverzertifikats für Standortsysteme, auf denen IIS ausgeführt wird)](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).



## <a name="next-steps"></a>Nächste Schritte

- [Einrichten des Cloudverwaltungsgateways](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Häufig gestellte Fragen zum Cloudverwaltungsgateway](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Sicherheit und Datenschutz für Cloud Management Gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
