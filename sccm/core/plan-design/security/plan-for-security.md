---
title: Planen der Sicherheit in System Center Configuration Manager | Microsoft-Dokumentation
description: "Bewährte Sicherheitsmethoden und Datenschutzinformationen für System Center Configuration Manager."
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
caps.latest.revision: 6
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: af06fb10d905e3fe447c6cd6ed35dac10488161f
ms.openlocfilehash: 1bf519ad4593f6a08d7dc393f9fab91c70b51b25
ms.lasthandoff: 01/05/2017


---
# <a name="plan-for-security-in-system-center-configuration-manager"></a>Planen der Sicherheit in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

##  <a name="a-namebkmkplanningforcertificatesa-plan-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> Planen von Zertifikaten (selbstsigniert und PKI)  
 Von Configuration Manager wird eine Kombination von selbstsignierten Zertifikaten und PKI-Zertifikaten (Public Key-Infrastruktur) verwendet.  

 Verwenden Sie als bewährte Sicherheitsmethode nach Möglichkeit PKI-Zertifikate. Weitere Informationen zu den PKI-Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md). Wenn die PKI-Zertifikate von Configuration Manager angefordert werden, beispielsweise bei der Registrierung mobiler Geräte und bei der AMT-Bereitstellung (Intel Active Management Technology), müssen Sie Active Directory Domain Services verwenden und eine Unternehmenszertifizierungsstelle in Anspruch nehmen. Alle anderen PKI-Zertifikate müssen Sie unabhängig von Configuration Manager bereitstellen und verwalten.  

 PKI-Zertifikate sind auch dann erforderlich, wenn von Clientcomputern eine Verbindung mit internetbasierten Standortsystemen hergestellt wird. Zudem wird empfohlen, PKI-Zertifikate zu verwenden, wenn von Clients eine Verbindung mit Standortsystemen hergestellt wird, auf welchen Internetinformationsdienste (IIS) ausgeführt werden. Weitere Informationen zur Clientkommunikation finden Sie unter [Konfigurieren von Clientkommunikationsports in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

 Wenn Sie eine PKI verwenden, können Sie auch IPsec verwenden, um die Kommunikation zwischen den Servern der Standortsysteme innerhalb eines Standorts, zwischen Standorten sowie beim Übertragen anderer Daten zwischen Computern zu sichern. Die Implementierung von IPsec erfolgt unabhängig von Configuration Manager.  

 Von Configuration Manager können automatisch selbstsignierte Zertifikate erstellt werden, wenn keine PKI-Zertifikate verfügbar sind, und einige Zertifikate in Configuration Manager sind immer selbstsigniert. In den meisten Fällen werden die selbstsignierten Zertifikate von Configuration Manager automatisch verwaltet, sodass Sie keine zusätzlichen Aktionen ausführen müssen. Eine mögliche Ausnahme gilt für das Signaturzertifikat des Standortservers. Das Signaturzertifikat des Standortservers ist immer selbstsigniert. Mit seiner Hilfe wird gewährleistet, dass die Clientrichtlinien, die durch die Clients vom Verwaltungspunkt heruntergeladen werden, vom Standortserver gesendet wurden und nicht manipuliert sind.  

### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a>Planen des Signaturzertifikats des Standortservers (selbstsigniert)  
 Kopien des Signaturzertifikat des Standortservers können auf sichere Art von den Active Directory-Domänendiensten und einer Clientpushinstallation an die Clients übermittelt werden. Wenn eine solche Kopie nicht mithilfe der genannten Mechanismen an die Clients übermittelt werden kann, installieren Sie aus Sicherheitsgründen eine Kopie des Signaturzertifikats des Standortservers, wenn Sie den Client installieren. Dies ist vor allem wichtig, wenn die erste Kommunikation des Clients mit dem Standort über das Internet erfolgt. Hierbei wird eine Verbindung des Verwaltungspunkts mit einem nicht vertrauenswürdigen Netzwerk hergestellt, und entsprechende Angriffsrisiken werden eröffnet. Wenn Sie diesen zusätzlichen Schritt nicht ausführen, wird von den Clients automatisch eine Kopie des Signaturzertifikats des Standortservers vom Verwaltungspunkt heruntergeladen.  

 Es kann Szenarios geben, in denen ein sicheres Herunterladen einer Kopie des Signaturzertifikats des Standortservers durch die Clients nicht möglich ist. Dazu gehören folgende Szenarios:  

-   Sie installieren den Client nicht mithilfe von Clientpush, und eine der folgenden Bedingungen ist erfüllt:  

    -   Das Active Directory-Schema ist nicht für Configuration Manager erweitert.  

    -   Der Clientstandort ist nicht in Active Directory Domain Services veröffentlicht.  

    -   Der Client befindet sich in einer nicht vertrauenswürdigen Gesamtstruktur oder einer Arbeitsgruppe.  

-   Sie installieren den Client, während dieser mit dem Internet verbunden ist.  

##### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>So installieren Sie Clients mit einer Kopie des Signaturzertifikats des Standortservers  

1.  Suchen Sie das Signaturzertifikat des Standortservers auf dem primären Standortserver des Clients. Das Zertifikat ist im **SMS**-Zertifikatspeicher unter dem Antragstellernamen **Standortserver** und dem Anzeigenamen **Signaturzertifikat des Standortservers** gespeichert.  

2.  Exportieren Sie das Zertifikat ohne den privaten Schlüssel, speichern Sie es an einem sicheren Ort, und greifen Sie nur über gesicherte Kanäle, beispielsweise mithilfe von SMB-Signaturen (Server Message Block) oder IPsec darauf zu.  

3.  Installieren Sie den Client, indem Sie die „Client.msi“-Eigenschaft **SMSSIGNCERT=***&lt;Vollständiger Pfad und Dateiname\>* mit der Datei „CCMSetup.exe“ verwenden.  

###  <a name="a-namebkmkplanningforcrlsa-plan-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> Planen der PKI-Zertifikatsperrung  
Wenn Sie PKI-Zertifikate mit Configuration Manager verwenden, planen Sie, ob und wie von Clients und Servern zur Überprüfung des Zertifikats des Computers, der die Verbindung herstellt, eine Zertifikatssperrliste verwendet werden soll. Bei der Zertifikatssperrliste handelt es sich um eine Datei, die von einer Zertifizierungsstelle erstellt und signiert wird und die eine Liste mit Zertifikaten enthält, die von der Zertifizierungsstelle zwar ausgestellt, aber gesperrt wurden. Ein Zertifizierungsstellenadministrator kann Zertifikate sperren, wenn beispielsweise bekannt ist oder vermutet wird, dass ein ausgestelltes Zertifikat gefährdet ist.  

> [!IMPORTANT]  
>  Der Speicherort der Zertifikatssperrliste wird einem Zertifikat bei dessen Ausstellung durch die Zertifizierungsstelle hinzugefügt. Daher müssen Sie Ihre Sperrliste planen, bevor Sie PKI-Zertifikate zur Verwendung durch Configuration Manager bereitstellen.  

Die Zertifikatsperrliste wird standardmäßig von IIS stets auf Clientzertifikate hin überprüft. Diese Konfiguration können Sie in Configuration Manager nicht ändern. Die Zertifikatssperrliste für Standortsysteme wird von Configuration Manager-Clients standardmäßig geprüft. Diese Einstellung können Sie jedoch ändern, indem Sie eine Standorteigenschaft und eine CCMSetup-Eigenschaft angeben. Bei einer Out-of-Band-Verwaltung von Intel AMT-basierten Computern können Sie die Überprüfung der Zertifikatssperrlisten auch für den Out-of-Band-Dienstpunkt und für Computer, auf denen die Out-of-Band-Verwaltungskonsole ausgeführt wird, aktivieren.  

Wenn die Zertifikatsperrprüfung von Computern verwendet wird, aber keine Zertifikatssperrliste gefunden wird, wird von den Clients reagiert wie bei einer Sperrung aller Zertifikate in der Zertifikatkette, da nicht überprüft werden kann, ob Zertifikate in der Liste fehlen. In diesem Szenario können Verbindungen, für die Zertifikate erforderlich sind und Zertifikatsperrlisten verwendet werden, nicht aufgebaut werden.  

Durch das Überprüfen der Zertifikatsperrliste bei jeder Verwendung eines Zertifikats lässt sich der Schutz vor gesperrten Zertifikaten erhöhen. Es kommt jedoch auch zu einer Verbindungsverzögerung und zu zusätzlichen Verarbeitungsvorgängen auf dem Client. Diese zusätzliche Sicherheitsprüfung ist eher dann erforderlich, wenn Verbindungen zwischen Clients und dem Internet oder einem nicht vertrauenswürdigen Netzwerk hergestellt werden.  

Wenden Sie sich an Ihre PKI-Administratoren, bevor Sie entscheiden, ob stets eine Überprüfung der Zertifikatssperrlisten durch die Configuration Manager-Clients erfolgen soll, und erwägen Sie dann, diese Option in Configuration Manager aktiviert zu lassen, wenn die beiden folgenden Bedingungen erfüllt sind:  

-   Von Ihrer PKI-Infrastruktur wird eine Sperrliste unterstützt, und die Sperrliste ist an einem Speicherort veröffentlicht, der für alle Configuration Manager-Clients zugänglich ist. Bedenken Sie, dass hierzu auch Clients mit Internetverbindung, wenn Sie eine internetbasierte Clientverwaltung verwenden, sowie Clients in nicht vertrauenswürdigen Gesamtstrukturen gehören können.  

-   Die Anforderung, die Zertifikatssperrliste für jede Verbindung mit einem Standortsystem, das für die Verwendung eines PKI-Zertifikats konfiguriert ist, zu überprüfen, wird schwerer gewichtet als die Anforderung an schnelle Verbindungen und eine effiziente Verarbeitung auf dem Client. Sie wird auch schwerer gewichtet als das Risiko, dass ein Zugriff von Clients auf Server nicht möglich ist, weil die Zertifikatssperrliste nicht verfügbar ist.  

###  <a name="a-namebkmkplanningforrootcasa-plan-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> Planen von vertrauenswürdigen PKI-Stammzertifikaten und der Liste der Zertifikataussteller  
Wenn von Ihren IIS-Standortsystemen PKI-Clientzertifikate zur Clientauthentifizierung über HTTP oder zur Clientauthentifizierung und Verschlüsselung über HTTPS verwendet werden, müssen Sie möglicherweise Stamm-Zertifizierungsstellenzertifikate als Standorteigenschaft importieren. Die folgenden beiden Szenarios sind möglich:  

-   Sie stellen Betriebssysteme mithilfe von Configuration Manager bereit, und von den Verwaltungspunkten werden nur HTTPS-Clientverbindungen akzeptiert.  

-   Sie verwenden PKI-Clientzertifikate, die mit keinem für die Verwaltungspunkte vertrauenswürdigen Stamm-Zertifizierungsstellenzertifikat verkettet sind.  

    > [!NOTE]  
    >  Wenn Sie Client-PKI-Zertifikate aus der gleichen Zertifizierungsstellenhierarchie ausstellen, von der auch die Serverzertifikate ausgestellt werden, die Sie für Verwaltungspunkte verwenden, müssen Sie dieses Stamm-Zertifizierungsstellenzertifikat nicht angeben. Wenn Sie jedoch mehrere Zertifizierungsstellenhierarchien verwenden und nicht sicher sind, ob diese voneinander als vertrauenswürdig eingestuft werden, importieren Sie das Stammzertifikat der Zertifizierungsstellenhierarchie des Clients.  

Wenn Sie Stamm-Zertifizierungsstellenzertifikate für Configuration Manager importieren müssen, exportieren Sie sie von der ausstellenden Zertifizierungsstelle oder vom Clientcomputer. Wenn Sie das Zertifikat von der ausstellenden Zertifizierungsstelle exportieren, die auch die Stammzertifizierungsstelle ist, dann achten Sie darauf, dass der private Schlüssel nicht exportiert wird. Speichern Sie die exportierte Zertifikatsdatei an einem sicheren Ort, um Manipulationen zu verhindern. Beim Einrichten des Standorts benötigen Sie Zugriff auf diese Datei. Wenn Sie über das Netzwerk auf die Datei zugreifen, vergewissern Sie sich, dass die Kommunikation durch SMB-Signaturen oder IPsec vor Manipulationen geschützt ist.  

Wenn ein importiertes Stamm-Zertifizierungsstellenzertifikat erneuert wird, müssen Sie das erneuerte Zertifikat importieren.  

Aus diesen importierten Stamm-Zertifizierungsstellenzertifikaten sowie aus den Stamm-Zertifizierungsstellenzertifikaten jedes Verwaltungspunkts wird die Liste der Zertifikataussteller erstellt, die von Configuration Manager-Computern auf folgende Arten verwendet wird:  

-   Wenn von Clients Verbindungen zu Verwaltungspunkten hergestellt werden, wird durch die Verwaltungspunkte überprüft, ob das Clientzertifikat mit einem vertrauenswürdigen Stammzertifikat auf der Standortliste der Zertifikataussteller verkettet ist. Wenn dies nicht der Fall ist, wird das Zertifikat abgelehnt, und die PKI-Verbindung kann nicht hergestellt werden.  

-   Wenn von Clients ein PKI-Zertifikat ausgewählt wird und für die Clients eine Liste der Zertifikataussteller verfügbar ist, wird ein Zertifikat ausgewählt, das mit einem vertrauenswürdigen Stammzertifikat in dieser Liste verkettet ist. Wenn keine Übereinstimmung vorhanden ist, wird von den Clients kein PKI-Zertifikat ausgewählt. Weitere Informationen zum Clientzertifikatvorgang finden Sie im Abschnitt [Planen der Auswahl des PKI-Clientzertifikats](#BKMK_PlanningForClientCertificateSelection) in diesem Artikel.  

Unabhängig von der Standortkonfiguration kann der Import eines Stamm-Zertifizierungsstellenzertifikats auch bei der Anmeldung von mobilen Geräten oder Macintosh-Computern und beim Einrichten von Intel AMT-basierten Computern für Funknetzwerke erforderlich sein.  

###  <a name="a-namebkmkplanningforclientcertificateselectiona-plan-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> Planen der Auswahl des PKI-Clientzertifikats  
 Wenn von Ihren IIS-Standortsystemen PKI-Clientzertifikate zur Clientauthentifizierung über HTTP oder zur Clientauthentifizierung und Verschlüsselung über HTTPS verwendet werden sollen, planen Sie, auf welche Art das Zertifikat zur Verwendung in Configuration Manager von den Windows-Clients ausgewählt werden soll.  

> [!NOTE]  
>  Nicht auf allen Geräten wird eine Zertifikatauswahlmethode unterstützt. Stattdessen wird das erste Zertifikat ausgewählt, das die Zertifikatanforderungen erfüllt. Beispiel: Von Clients auf Macintosh-Computern und mobilen Geräten wird keine Zertifikatauswahlmethode unterstützt.  

In vielen Fällen sind Standardkonfiguration und Standardverhalten ausreichend. Vom Configuration Manager-Client auf Windows-Computern werden mehrere Zertifikate anhand der folgenden Kriterien in der angegebenen Reihenfolge gefiltert:  

1.  Liste der Zertifikataussteller: Das Zertifikat ist mit einem Stamm-Zertifizierungsstellenzertifikat verkettet, das vom Verwaltungspunkt als vertrauenswürdig eingestuft wird.  

2.  Das Zertifikat befindet sich im Standardzertifikatspeicher **Persönlich**.  

3.  Das Zertifikat ist gültig. Es ist nicht gesperrt und nicht abgelaufen. Bei der Gültigkeitsprüfung wird sichergestellt, dass der private Schlüssel zugänglich ist und dass das Zertifikat nicht mit einer Zertifikatvorlage der Version 3 erstellt wird, da diese mit Configuration Manager nicht kompatibel ist.  

4.  Zum Zertifikat gehört eine Clientauthentifizierungsfunktion, oder das Zertifikat wurde auf den Computernamen ausgestellt.  

5.  Das Zertifikat weist die längste Gültigkeitsdauer auf.  

Clients können mithilfe der folgenden Mechanismen für die Verwendung der Liste der Zertifikataussteller konfiguriert werden:  

-   Sie werden als Configuration Manager-Standortinformationen zu Active Directory Domain Services veröffentlicht.  

-   Clients werden mithilfe von Clientpush installiert.  

-   Die Liste wird durch Clients, die ihrem Standort erfolgreich zugewiesen wurden, vom Verwaltungspunkt heruntergeladen.  

-   Die Liste wird während der Clientinstallation als „CCMSetup client.msi“-Eigenschaft von CCMCERTISSUERS angegeben.  

Von Clients, deren Erstinstallation ohne die Liste der Zertifikataussteller erfolgt und die dem Standort noch nicht zugewiesen sind, wird dieser Schritt übersprungen. Wenn die Liste der Zertifikataussteller für die Clients verfügbar ist, jedoch kein PKI-Zertifikat, das mit einem vertrauenswürdigen Stammzertifikat mit dieser Liste verkettet ist, ist keine Zertifikatauswahl möglich. In diesem Fall wird von den Clients nicht mit den anderen Zertifikatauswahlkriterien fortgefahren.  

In den meisten Fällen wird vom Configuration Manager-Client ein eindeutiges und angemessenes PKI-Zertifikat korrekt identifiziert. Wenn dies nicht der Fall ist, können Sie die folgenden beiden alternativen Auswahlmethoden einrichten, anstatt das Zertifikat anhand der Clientauthentifizierungsfunktion auszuwählen:  

-   Suche nach teilweise übereinstimmenden Zeichenfolgen im Antragstellernamen des Clientzertifikats. Dies ist ein Abgleich ohne Beachtung der Groß- und Kleinschreibung, der nützlich sein kann, wenn Sie den vollständig qualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) eines Computers im Feld für den Antragstellernamen verwenden und eine Zertifikatauswahl auf Basis des Domänensuffixes wünschen, beispielsweise **contoso.com**. Sie können diese Auswahlmethode jedoch auch verwenden, um nach einer beliebigen Zeichenfolge im Antragstellernamen des Zertifikats zu suchen, mit der Sie das gewünschte Zertifikat von den anderen Zertifikaten im Clientzertifikatspeicher unterscheiden können.  

    > [!NOTE]  
    >  Sie können die teilweise übereinstimmenden Zeichenfolgen nicht mit dem alternativen Antragstellernamen (Subject Alternative Name, SAN) als Standorteinstellung verwenden. Sie können zwar mithilfe von CCMSetup eine teilweise übereinstimmende Zeichenfolge für den SAN angeben, doch diese wird in den folgenden Szenarien von den Standorteigenschaften überschrieben:  
    >   
    >  -   Von Clients werden Standortinformationen abgerufen, welche in den Active Directory-Domänendiensten veröffentlicht sind.  
    > -   Clients werden mithilfe einer Clientpushinstallation installiert.  
    >   
    >  Verwenden Sie teilweise Übereinstimmungen beim SAN nur dann, wenn Sie Clients manuell installieren und von den Clients keine Standortinformationen aus den Active Directory-Domänendiensten abgerufen werden. Beispielsweise gelten diese Bedingungen für Clients, die mit der Einstellung „Nur Internetverbindungen zulassen“ konfiguriert sind.  

-   Eine Suche nach Übereinstimmungen bei den Attributwerten für „Antragstellername“ oder „Alternativer Antragstellername“ im Clientzertifikat. Bei dieser Suche wird die Groß-/Kleinschreibung beachtet. Sie bietet sich an, wenn Sie einen X500 DN (Distinguished Name) oder entsprechende Objektkennung (OID) gemäß RFC 3280 verwenden und die Zertifikatauswahl auf den Attributwerten basieren soll. Sie können nur die Attribute und deren Werte angeben, die zur eindeutigen Identifizierung oder Überprüfung der Gültigkeit des Zertifikats erforderlich sind und das Zertifikat von den anderen Zertifikaten im Zertifikatspeicher unterscheiden.  

In der folgenden Tabelle sind die Attributwerte aufgeführt, die von Configuration Manager bei den Auswahlkriterien für Clientzertifikate unterstützt werden.  

|OID-Attribut|DN-Attribut (Distinguished Name)|Attributdefinition|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Domänenkomponente|  
|1.2.840.113549.1.9.1|E oder E-mail|E-Mail-Adresse|  
|2.5.4.3|CN|Allgemeiner Name|  
|2.5.4.4|SN|Antragstellername|  
|2.5.4.5|SERIALNUMBER|Seriennummer|  
|2.5.4.6|C|Ländercode|  
|2.5.4.7|L|Ort|  
|2.5.4.8|S oder ST|Name des Bundeslands bzw. des Kantons|  
|2.5.4.9|STREET|Straße|  
|2.5.4.10|O|Organisationsname|  
|2.5.4.11|OU|Organisationseinheit|  
|2.5.4.12|T oder Title|Titel|  
|2.5.4.42|G oder GN oder GivenName|Vorname|  
|2.5.4.43|I oder Initials|Initialen|  
|2.5.29.17|(kein Wert)|Alternativer Antragstellername|  

Falls nach der Anwendung der Auswahlkriterien mehrere geeignete Zertifikate gefunden werden, können Sie die Standardkonfiguration außer Kraft setzen, laut der das Zertifikat mit der längsten Gültigkeitsdauer ausgewählt wird, und stattdessen festlegen, dass kein Zertifikat ausgewählt werden soll. In diesem Fall kann die Kommunikation des Clients mit IIS-Standortsystemen nicht über ein PKI-Zertifikat erfolgen. Vom Client wird eine Fehlermeldung an den ihm zugewiesenen Fallbackstatuspunkt gesendet, um Sie über den Fehler bei der Zertifikatauswahl zu informieren und Ihnen die Gelegenheit zu geben, die Zertifikatauswahlkriterien zu ändern oder zu optimieren. Das Verhalten des Clients richtet sich dann danach, ob die fehlerhafte Verbindung über HTTPS oder HTTP hergestellt wurde:  

-   Falls die fehlerhafte Verbindung über HTTPS erfolgte, wird vom Client versucht, eine Verbindung über HTTP herzustellen. Dabei wird das selbstsignierte Zertifikat verwendet.  

-   Falls die fehlerhafte Verbindung über HTTP erfolgte, wird vom Client versucht, erneut eine Verbindung über HTTP herzustellen. Dabei wird das selbstsignierte Clientzertifikat verwendet.  

Sie können die Identifizierung eines eindeutigen PKI-Clientzertifikats erleichtern, indem Sie für den **Computerspeicher** anstelle der Standardeinstellung **Persönlich** einen benutzerdefinierten Speicher angeben. Sie müssen diesen Speicher jedoch unabhängig von Configuration Manager erstellen und in der Lage sein, Zertifikate für diesen benutzerdefinierten Speicher bereitzustellen und zu erneuern, bevor deren Gültigkeit abläuft.  

Weitere Informationen zum Konfigurieren der Einstellungen für Clientzertifikate finden Sie im Abschnitt [Konfigurieren von Einstellungen für Client-PKI-Zertifikate](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) im Artikel [Konfigurieren der Sicherheit in System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

###  <a name="a-namebkmkplanningforpkitransitiona-plan-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> Planen einer Übergangsstrategie für PKI-Zertifikate und internetbasierte Clientverwaltung  
Mithilfe der flexiblen Konfigurationsoptionen in Configuration Manager können Sie Clients und den Standort allmählich auf PKI-Zertifikate umstellen und so für sichere Clientendpunkte sorgen. PKI-Zertifikate bieten nicht nur eine größere Sicherheit, sondern ermöglichen auch die Verwaltung von Clients im Internet.  

Dank der zahlreichen Konfigurationsoptionen und -möglichkeiten in Configuration Manager gibt es mehrere Methoden, sämtliche Clients eines Standorts auf HTTPS-Verbindungen umzustellen. Unabhängig von der ausgewählten Methode können Sie die folgenden Schritte als Richtlinie verwenden:  

1.  Installieren Sie den Configuration Manager-Standort, und konfigurieren Sie ihn so, dass von den Standortsystemen Clientverbindungen über HTTPS und HTTP akzeptiert werden.  

2.  Wählen Sie in den Standorteigenschaften auf der Registerkarte **Kommunikation mit Clientcomputern** unter **Einstellungen des Standortsystems** die Option **HTTP oder HTTPS** aus, und aktivieren Sie das Kontrollkästchen **PKI-Clientzertifikat (Clientauthentifizierungsfunktion) verwenden, sofern dieses verfügbar ist**.  Weitere Informationen finden Sie im Abschnitt [Konfigurieren von Einstellungen für Client-PKI-Zertifikate](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) des Artikels [Konfigurieren der Sicherheit in System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

3.  Führen Sie PKI im Rahmen eines Pilotversuchs für Clientzertifikate ein. Eine Beispielbereitstellung hierfür finden Sie im Abschnitt *Bereitstellen des Clientzertifikats für Windows-Computer* im Artikel [Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für System Center Configuration Manager: Windows Server 2008-Zertifizierungsstelle](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

4.  Installieren Sie Clients mithilfe der Clientpushinstallation. Weitere Informationen finden Sie im Abschnitt [Installieren von Configuration Manager-Clients mittels Clientpush](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush) im Artikel [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

5.  Überwachen Sie Clientbereitstellung und -status mithilfe der Berichte und Informationen in der Configuration Manager-Konsole.  

6.  Verfolgen Sie über die Spalte **Clientzertifikat** im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Geräte** , von wie vielen Clients ein Client-PKI-Zertifikat verwendet wird.  

     Sie können Computern auch das Configuration Manager-Tool zur Überprüfung der HTTPS-Bereitschaft (**cmHttpsReadiness.exe**) bereitstellen und mithilfe der Berichte feststellen, von wie vielen Computern ein Client-PKI-Zertifikat mit Configuration Manager.  

    > [!NOTE]  
    >  Bei der Installation des Configuration Manager-Clients wird das Tool **cmHttpsReadiness.exe** im Ordner *%windir%***\CCM** installiert. Bei der Ausführung dieses Tools auf Clients können Sie die folgenden Optionen angeben:  
    >   
    >  -   /Store:&lt;Name\>  
    > -   /Issuers:&lt;Liste\>  
    > -   /Criteria:&lt;Kriterium\>  
    > -   /SelectFirstCert  
    >   
    >  Diese Optionen sind den folgenden Client.msi-Eigenschaften zugeordnet: **CCMCERTSTORE**, **CCMCERTISSUERS**, **CCMCERTSEL**und **CCMFIRSTCERT** . Weitere Informationen zu diesen Optionen finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

7.  Wenn Sie sicher sind, dass von genügend Clients das eigene Client-PKI-Zertifikat erfolgreich für die Authentifizierung über HTTP verwendet wird, gehen Sie wie folgt vor:  

    1.  Stellen Sie ein PKI-Webserverzertifikat auf einem Mitgliedsserver bereit, von dem ein zusätzlicher Verwaltungspunkt für den Standort ausgeführt wird. Konfigurieren Sie dieses Zertifikat in den IIS. Weitere Informationen finden Sie im Abschnitt *Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden* des Artikels [Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für System Center Configuration Manager: Windows Server 2008-Zertifizierungsstelle](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

    2.  Installieren Sie die Verwaltungspunktrolle auf diesem Server, und konfigurieren Sie in den Verwaltungspunkteigenschaften unter **HTTPS** die Option **Clientverbindungen**.  

8.  Überwachen und überprüfen Sie, ob der neue Verwaltungspunkt von Clients mit einem PKI-Zertifikat mithilfe von HTTPS verwendet wird. Verwenden Sie hierzu die IIS-Protokollierung oder Leistungsindikatoren.  

9. Konfigurieren Sie andere Standortsystemrollen so neu, dass von ihnen HTTPS-Client-Verbindungen verwendet werden. Falls Sie Clients im Internet verwalten möchten, achten Sie darauf, dass Standortsysteme über einen Internet-FQDN verfügen. Konfigurieren Sie einzelne Verwaltungspunkte und Verteilungspunkte so, dass von ihnen Clientverbindungen aus dem Internet akzeptiert werden.  

    > [!IMPORTANT]  
    >  Prüfen Sie die Planungsinformationen und Voraussetzungen für die internetbasierte Clientverwaltung, bevor Sie die Standortsystemrollen so einrichten, dass von ihnen Verbindungen aus dem Internet akzeptiert werden. Weitere Informationen finden Sie unter [Kommunikation zwischen Endpunkten in System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

10. Dehnen Sie die Einführung von PKI-Zertifikaten für Clients und Standortsysteme mit IIS aus, und richten Sie gegebenenfalls die Standortsystemrollen für HTTPS-Clientverbindungen und Internet-Verbindungen ein.  

11. Zur Gewährleistung der maximalen Sicherheit legen Sie in den Standorteigenschaften die ausschließliche Verwendung von HTTPS fest, wenn Sie sicher sind, dass von allen Clients für die Authentifizierung und Verschlüsselung ein Client-PKI-Zertifikat verwendet wird.  

 Wenn Sie PKI-Zertifikate anhand dieses Plans nach und nach einführen – zunächst nur Authentifizierung über HTTP, dann Authentifizierung und Verschlüsselung über HTTPS –, verringern Sie das Risiko, dass Clients nicht mehr verwaltet werden. Darüber hinaus profitieren Sie von der höchsten Sicherheit, die Configuration Manager unterstützt.  

##  <a name="a-namebkmkplanningforrtka-plan-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> Planen des vertrauenswürdigen Stammschlüssels  
Mit dem vertrauenswürdigen Stammschlüssel von Configuration Manager kann von Configuration Manager-Clients überprüft werden, ob Standortsysteme ihrer Hierarchie angehören. Von jedem Standortserver wird ein Standortaustauschschlüssel für die Kommunikation mit anderen Standorten generiert. Der Standortaustauschschlüssel des Standorts auf der obersten Ebene einer Hierarchie wird als vertrauenswürdiger Stammschlüssel bezeichnet.  

Die Funktion des vertrauenswürdigen Stammschlüssels in Configuration Manager ähnelt der eines Stammzertifikats in einer Public Key-Infrastruktur, in der alle vom privaten Schlüssel des vertrauenswürdigen Stammschlüssels signierten Elemente weiter unten in der Hierarchie als vertrauenswürdig angesehen werden. Wenn beispielsweise das Verwaltungspunktzertifikat mit dem privaten Schlüssel des vertrauenswürdigen Stammschlüsselpaars signiert und eine Kopie des öffentlichen Schlüssels des vertrauenswürdigen Stammschlüsselpaars den Clients zur Verfügung gestellt wird, können Verwaltungspunkte, die sich innerhalb oder außerhalb ihrer Hierarchie befinden, leichter von Clients unterschieden werden. Von Clients wird Windows Management Instrumentation (WMI) zum Speichern einer Kopie des vertrauenswürdigen Stammschlüssels im Namespace **root\ccm\locationservices** verwendet.  

Die öffentliche Kopie des vertrauenswürdigen Stammschlüssels kann von Clients anhand zweier Methoden automatisch abgerufen werden:  

-   Das Active Directory-Schema wird für Configuration Manager erweitert, der Standort wird auf Active Directory Domain Services veröffentlicht, und diese Standortinformationen können von Clients aus einem globalen Katalogserver abgerufen werden.  

-   Clients werden mithilfe von Clientpush installiert.  

Falls der vertrauenswürdige Stammschlüssel nicht anhand einer dieser Methoden von Clients abgerufen werden kann, wird der vertrauenswürdige Stammschlüssel des ersten Verwaltungspunkts, mit dem eine Kommunikation hergestellt werden kann, von den Clients als vertrauenswürdig eingestuft. In diesem Fall könnte ein Client an den Verwaltungspunkt eines Angreifers fehlgeleitet werden und Richtlinien von diesem nicht autorisierten Verwaltungspunkt erhalten. Ein solcher Angriff trägt die Handschrift eines technisch versierten Angreifers und tritt möglicherweise nur kurze Zeit auf, bevor der Client den vertrauenswürdigen Stammschlüssel eines gültigen Verwaltungspunkts erhält. Sie können für Clients bereits vorab einen vertrauenswürdigen Stammschlüssel bereitstellen, um das Risiko zu reduzieren, dass Clients von einem Angreifer an einen nicht autorisierten Verwaltungspunkt fehlgeleitet werden.  

Anhand der folgenden Methoden können Sie einem Configuration Manager-Client den vertrauenswürdigen Stammschlüssel vorab bereitstellen und diesen Schlüssel prüfen:  

-   Vorabbereitstellung des vertrauenswürdigen Stammschlüssels an einen Client mithilfe einer Datei  

-   Vorabbereitstellung des vertrauenswürdigen Stammschlüssels an einen Client ohne eine Datei  

-   Überprüfung des vertrauenswürdigen Stammschlüssels auf einem Client  

> [!NOTE]  
>  Es ist nicht notwendig, einem Client den vertrauenswürdigen Stammschlüssel vorab bereitzustellen, wenn er diesen Schlüssel von den Active Directory-Domänendiensten abrufen kann oder wenn er durch Clientpush installiert wird. Die Vorabbereitstellung ist zudem nicht notwendig, wenn die Kommunikation der Clients mit Verwaltungspunkten über HTTPS erfolgt, da die Vertrauenswürdigkeit über die PKI-Zertifikate bestätigt wird.  

Sie können den vertrauenswürdigen Hauptschlüssel aus einem Client entfernen, indem Sie die „Client.msi“-Eigenschaft **RESETKEYINFORMATION = TRUE** mit „CCMSetup.exe“ verwenden. Installieren Sie den Client zusammen mit dem neuen vertrauenswürdigen Hauptschlüssel neu, um den vertrauenswürdigen Hauptschlüssel zu ersetzen. Verwenden Sie hierzu Clientpush, oder legen Sie die Client.msi-Eigenschaft **SMSPublicRootKey** mit CCMSetup.exe fest.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a>So stellen Sie einem Client den vertrauenswürdigen Stammschlüssel mithilfe einer Datei vorab bereit  

1.  Öffnen Sie in einem Text-Editor die Datei *&lt;Configuration Manager-Verzeichnis\>***\bin\mobileclient.tcf**.  

2.  Suchen Sie den Eintrag **SMSPublicRootKey=**, kopieren Sie den in dieser Zeile stehenden Schlüssel, und schließen Sie die Datei, ohne Änderungen zu speichern.  

3.  Erstellen Sie eine neue Textdatei, und fügen Sie den in der Datei „mobileclient.tcf“ kopierten Schlüssel ein.  

4.  Speichern Sie die Datei an einem Speicherort, auf den alle Computer Zugriff haben, an dem die Datei aber vor Manipulationen geschützt ist.  

5.  Installieren Sie den Client mit einer beliebigen Methode, von der „Client.msi“-Eigenschaften akzeptiert werden. Legen Sie die „Client.msi“-Eigenschaft **SMSROOTKEYPATH=***&lt;Vollständiger Pfad und Dateiname\>* fest.  

    > [!IMPORTANT]  
    >  Wenn Sie den vertrauenswürdigen Stammschlüssel bei der Clientinstallation als zusätzliche Sicherheitsmaßnahme angeben, müssen Sie auch den Standortcode angeben, indem Sie die „Client.msi“-Eigenschaft **SMSSITECODE=&lt;Standortcode\>** verwenden.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a>So stellen Sie einem Client den vertrauenswürdigen Stammschlüssel ohne eine Datei vorab bereit  

1.  Öffnen Sie in einem Text-Editor die Datei *&lt;Configuration Manager-Verzeichnis\>***\bin\mobileclient.tcf**.  

2.  Suchen Sie den Eintrag „SMSPublicRootKey=“, notieren Sie sich den in dieser Zeile stehenden Schlüssel bzw. kopieren Sie ihn in die Zwischenablage, und schließen Sie die Datei, ohne Änderungen zu speichern.  

3.  Installieren Sie den Client mit einer beliebigen Methode, von der „Client.msi“-Eigenschaften akzeptiert werden. Legen Sie die „Client.msi“-Eigenschaft **SMSPublicRootKey=***&lt;Schlüssel\>* fest, wobei *&lt;Schlüssel\>* die Zeichenfolge ist, die Sie in „mobileclient.tcf“ kopiert haben.  

    > [!IMPORTANT]  
    >  Wenn Sie den vertrauenswürdigen Stammschlüssel bei der Clientinstallation als zusätzliche Sicherheitsmaßnahme angeben, müssen Sie auch den Standortcode angeben, indem Sie die „Client.msi“-Eigenschaft **SMSSITECODE=&lt;Standortcode\>** verwenden.  

#### <a name="to-verify-the-trusted-root-key-on-a-client"></a>So überprüfen Sie den vertrauenswürdigen Stammschlüssel auf einem Client  

1.  Wählen Sie im Menü **Start** die Option **Ausführen** aus, und geben Sie **Wbemtest** ein.  

2.  Wählen Sie im Dialogfeld **Testprogramm für Windows-Verwaltungsinstrumentation** die Option **Verbinden** aus.  

3.  Geben Sie im Dialogfeld **Verbinden** in das Feld **Namespace** die Zeichenfolge **root\ccm\locationservices** ein, und wählen Sie die Option **Verbinden** aus.  

4.  Wählen Sie im Dialogfeld **Testprogramm für Windows-Verwaltungsinstrumentation** unter **IWbemServices** die Option **Klassen aufzählen** aus.  

5.  Wählen Sie im Dialogfeld **Informationen zur übergeordneten Klasse** die Option **Rekursiv für alle Klassen** und anschließend **OK** aus.  

6.  Führen Sie im Fenster **Abfrageergebnis** einen Bildlauf an das Ende der Liste aus, und doppelklicken Sie auf **TrustedRootKey ()**.  

7.  Wählen Sie im Dialogfeld **Objekt-Editor für TrustedRootKey** die Option **Instanzen** aus.  

8.  Doppelklicken Sie im neuen Fenster **Abfrageergebnis**, in dem die Instanzen von **TrustedRootKey** aufgeführt werden, auf **TrustedRootKey=@**.  

9. Führen Sie im Dialogfeld **Objekt-Editor für TrustedRootKey=@** im Bereich **Eigenschaften** einen Bildlauf aus zu **TrustedRootKey CIM_STRING**. Die Zeichenfolge in der rechten Spalte ist der vertrauenswürdige Stammschlüssel. Sie sollte mit dem Wert von **SMSPublicRootKey** in der Datei *&lt;Configuration Manager-Verzeichnis\>***\bin\mobileclient.tcf** übereinstimmen.  

##  <a name="a-namebkmkplanningforsigningencryptiona-plan-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> Planen von Signierung und Verschlüsselung  
 Wenn für die gesamte Clientkommunikation PKI-Zertifikate verwendet werden, ist es nicht notwendig, zum Schutz der übermittelten Daten deren Signierung und Verschlüsselung zu planen. Wenn Sie aber festgelegt haben, dass bei Standortsystemen, von denen IIS ausgeführt werden, HTTP-Clientverbindungen zulässig sind, müssen Sie zum Schutz der Clientkommunikation an diesem Standort entsprechende Maßnahmen ergreifen.  

 Beispielsweise können Sie verlangen, dass die Daten, die von Clients an Verwaltungspunkte gesendet werden, signiert sein müssen. Zusätzlich können Sie verlangen, dass Daten von Clients, von denen HTTP verwendet wird, mit dem SHA-256-Algorithmus signiert werden müssen. Diese Einstellung bietet zwar ein höheres Maß an Sicherheit, aber Sie sollten sie dennoch nur aktivieren, wenn SHA-256 von allen Clients unterstützt wird. Viele Betriebssysteme bieten zwar eine systemeigene Unterstützung für SHA-256, aber für ältere Betriebssysteme ist möglicherweise ein Update oder Hotfix erforderlich. Beispielsweise muss auf Computern mit Windows Server 2003 SP2 das im [KB-Artikel 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666)genannte Hotfix installiert werden.  

 Durch die Signierung werden Daten vor Manipulationen geschützt. Durch die Verschlüsselung hingegen wird die Veröffentlichung von Informationen verhindert. Sie können für die Inventurdaten und Zustandsmeldungen, die von Clients an Verwaltungspunkte des Standorts gesendet werden, die 3DES-Verschlüsselung aktivieren. Die Verwendung dieser Option setzt nicht voraus, dass Sie auf den Clients Updates installieren. Sie sollten aber die zusätzliche CPU-Auslastung erwägen, die mit der Verschlüsselung und Entschlüsselung auf Clients und am Verwaltungspunkt einhergeht.  

 Weitere Informationen zum Konfigurieren der Einstellungen für die Signierung und Verschlüsselung finden Sie im Abschnitt [Konfigurieren von Signierung und Verschlüsselung](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) im Artikel [Konfigurieren der Sicherheit in System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

##  <a name="a-namebkmkplanningforrbaa-plan-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> Planen der rollenbasierten Verwaltung  
 Weitere Informationen finden Sie unter [Grundlagen der rollenbasierten Verwaltung für System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="see-also"></a>Weitere Informationen:
[Technische Referenz für kryptografische Steuerelemente](../../../protect/deploy-use/cryptographic-controls-technical-reference.md)  

