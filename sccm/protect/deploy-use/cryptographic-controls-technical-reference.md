---
title: "Technische Referenz für kryptografische Steuerelemente"
titleSuffix: Configuration Manager
description: "Erfahren Sie mehr darüber, wie die Signierung und Verschlüsselung Sie vor Angriffen schützen kann, die Daten in System Center Configuration Manager lesen."
ms.custom: na
ms.date: 12/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: ebaff93d346b53afea8770fbe0634112bcecf82d
ms.sourcegitcommit: 372171a5cd8d143d6d47b651018cda0c91cad67c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/09/2017
---
# <a name="cryptographic-controls-technical-reference"></a>Technische Referenz für kryptografische Steuerelemente

*Gilt für: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager verwendet die Signierung und Verschlüsselung zum Schutz der Geräteverwaltung in der Configuration Manager-Hierarchie. Wenn Daten bei der Übertragung verändert wurden, werden sie mit der Signierung verworfen. Bei der Verschlüsselung wird mithilfe einer Netzwerkprotokollanalyse verhindert, dass ein Angreifer die Daten lesen kann.  

 Beim von Configuration Manager primär verwendeten Hashalgorithmus wird SHA-256 zur Signierung verwendet. Wenn zwei Configuration Manager-Standorte miteinander kommunizieren, signieren sie ihre Kommunikation mithilfe von SHA-256. Der in Configuration Manager primär implementierte Verschlüsselungsalgorithmus ist 3DES. Er wird zur Datenspeicherung in der Configuration Manager-Datenbank und für die-HTTP-Clientkommunikation verwendet. Wenn Sie die Clientkommunikation über HTTPS verwenden, können Sie Ihre Public Key-Infrastruktur (PKI) für die Verwendung von RSA-Zertifikaten mit den maximalen Hashalgorithmen und Schlüssellängen konfigurieren, die in [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md) beschrieben sind.  

 Für die meisten kryptografischen Vorgänge auf Windows-basierten Betriebssystemen verwendet Configuration Manager die SHA-2-, 3DES-, AES- und RSA-Algorithmen aus der Windows CryptoAPI-Bibliothek „rsaenh.dll“.  

> [!IMPORTANT]  
>  Sehen Sie sich die Informationen zu empfohlenen Änderungen als Reaktion auf SSL-Sicherheitsrisiken unter [Über SSL-Sicherheitsrisiken](#about-ssl-vulnerabilities)an.  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Kryptografische Steuerelemente für Configuration Manager-Vorgänge  
 Informationen in Configuration Manager können signiert und verschlüsselt werden, unabhängig davon, ob Sie die PKI-Zertifikate mit Configuration Manager verwenden oder nicht.  

### <a name="policy-signing-and-encryption"></a>Signieren und Verschlüsseln von Richtlinien  
 Clientrichtlinienzuweisungen werden mit dem selbstsignierten Signaturzertifikat des Standortservers signiert, um das Sicherheitsrisiko zu verhindern, dass von einem gefährdeten Verwaltungspunkt manipulierte Richtlinien versendet werden. Dies ist insbesondere dann wichtig, wenn Sie eine internetbasierte Clientverwaltung verwenden, da diese Umgebung einen Verwaltungspunkt erfordert, der der Internetkommunikation ausgesetzt ist.  

 Richtlinien werden mit 3DES verschlüsselt, wenn sie sensible Daten enthalten. Richtlinien, die sensible Daten enthalten, werden ausschließlich an autorisierte Clients gesendet. Richtlinien, die keine sensiblen Daten enthalten, werden nicht verschlüsselt.  

 Wenn eine Richtlinie auf Clients gespeichert wird, wird sie mithilfe der Anwendungsprogrammierschnittstelle für Datenschutz (Data Protection application programming interface, DPAPI) verschlüsselt.  

### <a name="policy-hashing"></a>Hashwert von Richtlinien  
 Wenn Configuration Manager-Clients eine Richtlinie anfordern, erhalten sie zunächst eine Richtlinienzuordnung, sodass sie wissen, welche Richtlinien auf sie zutreffen, und fordern dann nur diese Richtlinientexte an. Jede Richtlinienzuordnung enthält den errechneten Hashwert für den entsprechenden Richtlinientext. Der Client ruft die entsprechenden Richtlinientexte ab und berechnet aufgrund dieses Texts dann den Hashwert. Stimmt der Hashwert des heruntergeladenen Richtlinientexts nicht mit dem Hashwert der Richtlinienzuordnung überein, wird der Richtlinientext vom Client verworfen.  

 Hashalgorithmen für Richtlinien sind SHA-1 und SHA-256.  

### <a name="content-hashing"></a>Inhaltshashing  
 Der Verteilungs-Manager-Dienst des Standortservers erstellt einen Hashwert für die Inhaltsdateien aller Pakete. Der Richtlinienanbieter bindet den Hashwert in die Softwareverteilungsrichtlinie ein. Wenn der Inhalt vom Configuration Manager-Client heruntergeladen wird, wird der Hashwert vom Client lokal erneut generiert und mit dem Hashwert der Richtlinie verglichen. Stimmen die Hashwerte überein, wurde der Inhalt nicht geändert. Der Inhalt wird vom Client installiert. Wurde auch nur ein Byte des Inhalts geändert, stimmen die Hashwerte nicht überein, und die Software wird nicht installiert. Mit dieser Überprüfung wird sichergestellt, dass die richtige Software installiert wird, da der tatsächliche Inhalt mit der Richtlinie verglichen wird.  

 Der Hashalgorithmus für Richtlinien ist standardmäßig SHA-256. Informationen zum Ändern dieser Standardeinstellung finden Sie in der Dokumentation für das Configuration Manager Software Development Kit (SDK).  

 Die Verwendung von Inhaltshashs wird nicht von allen Geräten unterstützt. Ausnahmen sind:  

-   Windows-Clients beim Streamen von App-V-Inhalten  

-   Windows Phone-Clients, da diese Clients die Signatur einer Anwendung, die von einer vertrauenswürdigen Quelle signiert wird, überprüfen.  

-   Windows RT-Clients, da diese Clients die Signatur einer Anwendung, die von einer vertrauenswürdigen Quelle signiert wird, überprüfen, und außerdem die Überprüfung des vollständigen Paketnamens (PFN) verwenden.  

-   iOS, da diese Geräte die Signatur einer Anwendung, die von einem Entwicklerzertifikat einer vertrauenswürdigen Quelle signiert wird, überprüfen.  

-   Nokia-Clients, da diese Clients die Signatur einer Anwendung, die ein selbstsigniertes Zertifikat verwendet, überprüfen. Alternativ dazu kann die Signatur eines Zertifikats aus einer vertrauenswürdigen Quelle verwendet werden, und mit dem Zertifikat können Nokia Symbian Installation Source-Anwendungen (SIS) signiert werden.  

-   Android: Darüber hinaus wird die Signaturüberprüfung für die Anwendungsinstallation von diesen Geräten nicht verwendet.  

-   Clients, auf denen Linux- und UNIX-Versionen ausgeführt werden, die SHA-256 nicht unterstützen. Weitere Informationen finden Sie unter [Planen der Clientbereitstellung für Linux- und UNIX-Computer in System Center Configuration Manager](../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

### <a name="inventory-signing-and-encryption"></a>Signieren und Verschlüsseln der Inventur  
 Inventurdaten, die von Clients an Verwaltungspunkte gesendet werden, werden stets von Geräten signiert. Dies gilt unabhängig davon, ob die Kommunikation mit Verwaltungspunkten über HTTP oder HTTPS erfolgt. Wenn HTTP verwendet wird, wird aus Sicherheitsgründen empfohlen, diese Daten zu verschlüsseln.  

### <a name="state-migration-encryption"></a>Zustandsmigrationsverschlüsselung  
 Auf Zustandsmigrationspunkten für die Betriebssystembereitstellung gespeicherte Daten werden vom User State Migration Tool (USMT) immer unter Verwendung von 3DES verschlüsselt.  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>Verschlüsselung für Multicastpakete zum Bereitstellen von Betriebssystemen  
 Sie können für jedes Paket der Betriebssystembereitstellung die Verschlüsselung aktivieren, wenn das Paket über Multicast an Computer übertragen wird. Bei der Verschlüsselung wird der erweiterte Verschlüsselungsstandard (Advanced Encryption Standard, AES) verwendet. Wenn Sie die Verschlüsselung aktivieren, ist keine zusätzliche Konfiguration für das Zertifikat erforderlich. Der multicastfähige Verteilungspunkt generiert automatisch symmetrische Schlüssel zur Paketverschlüsselung. Jedes Paket erhält einen anderen Verschlüsselungsschlüssel. Der Schlüssel wird mithilfe von Windows-Standard-APIs auf dem multicastfähigen Verteilungspunkt gespeichert. Wenn vom Client eine Verbindung mit der Multicastsitzung hergestellt wird, erfolgt der Schlüsselaustausch über einen Kanal, der entweder mit dem Clientauthentifizierungszertifikat der PKI (wenn vom Client HTTPS verwendet wird) oder mit dem selbstsignierten Zertifikat (wenn vom Client HTTP verwendet wird) verschlüsselt ist. Der Client speichert den Schlüssel nur für die Dauer der Multicastsitzung im Arbeitsspeicher.  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>Verschlüsselung von Medien zum Bereitstellen von Betriebssystemen  
 Wenn Sie Betriebssysteme über Medien bereitstellen und zum Schutz der Medien ein Kennwort angeben, werden die Umgebungsvariablen mithilfe des erweiterten Verschlüsselungsstandards (Advanced Encryption Standard, AES) verschlüsselt. Andere Daten auf den Medien, wie beispielsweise Pakete und Inhalt für Anwendungen, werden nicht verschlüsselt.  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>Verschlüsselung für Inhalte, die auf cloudbasierten Verteilungspunkten gehostet werden  
 Ab System Center 2012 Configuration Manager SP1 werden bei Verwendung cloudbasierter Verschlüsselungspunkte die Inhalte, die Sie auf diese Verteilungspunkte hochladen, mithilfe des erweiterten Verschlüsselungsstandards (Advanced Encryption Standard, AES) unter Verwendung eines 256-Bit-Schlüssels verschlüsselt. Der Inhalt wird jeweils neu verschlüsselt, wenn Sie ihn aktualisieren. Wenn der Inhalt von Clients heruntergeladen wird, wird er verschlüsselt und ist per HTTPS-Verbindung geschützt.  

### <a name="signing-in-software-updates"></a>Signieren von Softwareupdates  
 Alle Softwareupdates müssen zum Schutz vor Manipulation von einem vertrauenswürdigen Herausgeber signiert werden. Clientcomputer werden von Windows Update Agent (WUA) auf die Updates aus dem Katalog überprüft. Ein Update wird jedoch nur installiert, wenn das digitale Zertifikat im Speicher des vertrauenswürdigen Herausgebers auf dem lokalen Computer vorhanden ist. Wenn bei der Veröffentlichung des Updatekatalogs ein selbstsigniertes Zertifikat wie „WSUS Publishers Self-signed“ verwendet wurde, muss sich das Zertifikat auch im Zertifikatspeicher der vertrauenswürdigen Stammzertifizierungsstellen auf dem lokalen Computer befinden, damit die Gültigkeit des Zertifikats überprüft werden kann. WUA überprüft auch, ob auf dem lokalen Computer die Gruppenrichtlinieneinstellung **Signierten Inhalt von Intranet-Speicherort für Microsoft-Updatedienst zulassen** aktiviert ist. Diese Richtlinieneinstellung muss für WUA aktiviert sein, damit Updates überprüft werden können, die mithilfe von Update Publisher erstellt und veröffentlicht wurden.  

 Wenn Softwareupdates in System Center Updates Publisher veröffentlicht werden, werden die Softwareupdates bei Veröffentlichung auf einem Updateserver durch ein digitales Zertifikat signiert. Sie können entweder ein PKI-Zertifikat angeben oder festlegen, dass Updates Publisher ein selbstsigniertes Zertifikat zum Signieren des Softwareupdates generieren soll.  

### <a name="signed-configuration-data-for-compliance-settings"></a>Signierte Konfigurationsdaten für Kompatibilitätseinstellungen  
 Beim Importieren von Konfigurationsdaten überprüft Configuration Manager die digitale Signatur der Datei. Falls die Dateien nicht signiert wurden oder bei der Überprüfung der digitalen Signatur ein Fehler auftritt, wird eine Warnung ausgegeben. Sie werden dann aufgefordert, anzugeben, ob der Importvorgang fortgesetzt werden soll. Sie sollten mit dem Import der Konfigurationsdaten nur fortfahren, wenn Sie dem Herausgeber und der Integrität der Daten wirklich vertrauen.  

### <a name="encryption-and-hashing-for-client-notification"></a>Verschlüsselung und Hashing für die Clientbenachrichtigung  
 Wenn Sie die Clientbenachrichtigung nutzen, werden bei der gesamten Kommunikation TLS und die höchste Verschlüsselungsstufe verwendet, die von den Betriebssystemen des Servers und Clients ausgehandelt werden kann. Bei einem Clientcomputer mit Windows 7 und einem Verwaltungspunkt mit Windows Server 2008 R2 kann z. B. die 128-Bit-AES-Verschlüsselung unterstützt werden, während für einen Clientcomputer mit Vista für denselben Verwaltungspunkt nur die 3DES-Verschlüsselung ausgehandelt werden kann. Diese Aushandlung wird auch für das Hashing der Pakete ausgeführt, die im Laufe der Clientbenachrichtigung übertragen werden. Dabei wird SHA-1 oder SHA-2 verwendet.  

##  <a name="certificates-used-by-configuration-manager"></a>Von Configuration Manager verwendete Zertifikate  
 Eine Liste der PKI-Zertifikate, die von Configuration Manager verwendet werden können, eine Übersicht über spezielle Anforderungen oder Einschränkungen sowie Informationen zur Verwendung der Zertifikate finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md). Diese Liste enthält die unterstützten Hashalgorithmen und Schlüssellängen. Von den meisten Zertifikaten werden SHA-256 und eine Schlüssellänge von 2048 Bit unterstützt.  

> [!NOTE]  
>  Alle von Configuration Manager verwendeten Zertifikate dürfen im Antragstellernamen oder alternativen Antragstellernamen nur Einzelbyte-Zeichen enthalten.  

 PKI-Zertifikate sind in den folgenden Fällen erforderlich:  

-   Verwalten von Configuration Manager-Clients im Internet.  

-   Verwalten von Configuration Manager-Clients auf mobilen Geräten.  

-   Bei der Verwaltung von Macintosh-Computern.  

-   Bei der Verwendung von cloudbasierten Verteilungspunkten.  

-   Bei der Out-of-Band-Verwaltung Intel AMT-basierter Computer.  

 Für die übrige Configuration Manager-Kommunikation, bei der Zertifikate zur Authentifizierung, zum Signieren oder Verschlüsseln erforderlich sind, verwendet Configuration Manager automatisch PKI-Zertifikate, sofern diese verfügbar sind. Wenn sie nicht verfügbar sind, generiert Configuration Manager selbstsignierte Zertifikate.  

 Bei der Verwaltung mobiler Geräte über den Exchange Server-Connector verwendet Configuration Manager keine PKI-Zertifikate.  

### <a name="mobile-device-management-and-pki-certificates"></a>Verwaltung mobiler Geräte und PKI-Zertifikate  
 Wenn das mobile Gerät nicht durch den mobilen Betreiber gesperrt wurde, können Sie mithilfe von Configuration Manager oder Microsoft Intune ein Clientzertifikat anfordern und installieren. Dieses Zertifikat dient zur gegenseitigen Authentifizierung des Clients auf dem mobilen Gerät und den Configuration Manager-Standortsystemen oder Microsoft Intune-Diensten. Wenn Ihr mobiles Gerät gesperrt ist, können Sie Configuration Manager oder Intune nicht zur Bereitstellung von Zertifikaten verwenden.  

 Wenn Sie die Hardwareinventur für mobile Geräte aktivieren, inventarisieren Configuration Manager oder Intune auch die Zertifikate, die auf dem mobilen Gerät installiert sind.  

### <a name="out-of-band-management-and-pki-certificates"></a>Out-of-Band-Verwaltung und PKI-Zertifikate  
 Bei der Out-of-Band-Verwaltung für Intel AMT-basierte Computer werden mindestens zwei PKI-Zertifikattypen verwendet: ein AMT-Bereitstellungszertifikat und ein Webserverzertifikat.  

 Der Out-of-Band-Dienstpunkt verwendet ein AMT-Bereitstellungszertifikat, um Computer auf die Out-of-Band-Verwaltung vorzubereiten. Die bereitzustellenden AMT-basierten Computer müssen dem vom Out-of-Band-Verwaltungspunkt vorgelegten Zertifikat vertrauen. Standardmäßig werden AMT-basierte Computer vom Computerhersteller für die Verwendung externer Zertifizierungsstellen (Certification Authorities, CAs) wie VeriSign, Go Daddy, Comodo und Starfield konfiguriert. Wenn Sie ein Bereitstellungszertifikat von einer externen Zertifizierungsstelle erwerben und Configuration Manager für die Verwendung dieses Bereitstellungszertifikats konfigurieren, vertrauen AMT-basierte Computer der Zertifizierungsstelle für das Bereitstellungszertifikat, und die Bereitstellung kann erfolgreich durchgeführt werden. Aus Sicherheitsgründen sollten Sie jedoch eine eigene interne Zertifizierungsstelle zum Ausstellen des AMT-Bereitstellungszertifikats verwenden.  

 In der Firmware der AMT-basierten Computer wird eine Webserverkomponente ausgeführt, von der der Kommunikationskanal mit dem Out-of-Band-Dienstpunkt mithilfe von Transport Layer Security (TLS) verschlüsselt wird. Es gibt keine Benutzeroberfläche, über die ein Zertifikat manuell für das AMT-BIOS konfiguriert werden könnte. Sie müssen daher über eine Microsoft-Unternehmenszertifizierungsstelle verfügen, von der Zertifikatanforderungen von AMT-basierten Computern automatisch genehmigt werden. Als Format für die Anforderung wird „PKCS#10“ verwendet, was wiederum die Verwendung von „PKCS#7“ für die Übertragung der Zertifikatinformationen an den AMT-basierten Computer nach sich zieht.  

 Der AMT-basierte Computer ist zwar für den jeweiligen Verwaltungscomputer authentifiziert, es gibt aber kein entsprechendes PKI-Zertifikat für den Clientcomputer, der diesen verwaltet. Für diese Kommunikationen wird stattdessen Kerberos oder HTTP Digest-Authentifizierung verwendet. Wen HTTP Digest verwendet wird, erfolgt die Verschlüsselung über TLS.  

 Für die Out-of-Band-Verwaltung AMT-basierter Computer ist möglicherweise ein weiterer Zertifikattyp erforderlich: ein optionales Clientzertifikat für 802.1X-authentifizierte Kabel- und Drahtlosnetzwerke. Der AMT-basierte Computer benötigt möglicherweise ein Clientzertifikat zur Authentifizierung beim RADIUS-Server. Wurde der RADIUS-Server für die EAP-TLS-Authentifizierung konfiguriert, ist ein Clientzertifikat immer erforderlich. Wurde der RADIUS-Server für EAP-TTLS/MSCHAPv2 oder PEAPv0/EAP-MSCHAPv2 konfiguriert, hängt es von der RADIUS-Konfiguration ab, ob ein Clientzertifikat erforderlich ist oder nicht. Dieses Zertifikat wird von den AMT-basierten Computern mithilfe derselben Prozesse angefordert, die auch zur Anforderung des Webserverzertifikats verwendet werden.  

### <a name="operating-system-deployment-and-pki-certificates"></a>Betriebssystembereitstellung und PKI-Zertifikate  
 Wenn Sie Configuration Manager zur Bereitstellung von Betriebssystemen verwenden und für einen Verwaltungspunkt HTTPS-Clientverbindungen erforderlich sind, muss der Clientcomputer ebenfalls über ein Zertifikat für die Kommunikation mit dem Verwaltungspunkt verfügen. Dies gilt auch, wenn der Computer sich in einer Übergangsphase befindet, wie beim Starten von einem Tasksequenzmedium oder einem PXE-fähigen Verteilungspunkt. Um dieses Szenario zu unterstützen, müssen Sie ein PKI-Clientauthentifizierungszertifikat erstellen, es mit dem privaten Schlüssel exportieren, dann in den Eigenschaften des Standortservers importieren und auch das vertrauenswürdige Stammzertifizierungsstellen-Zertifikat des Verwaltungspunkts hinzufügen.  

 Wenn Sie startbare Medien erstellen, importieren Sie das Clientauthentifizierungszertifikat bei der Erstellung des startbaren Mediums. Konfigurieren Sie zum Schutz des privaten Schlüssels und anderer sensibler Daten, die in der Tasksequenz konfiguriert werden, ein Kennwort für das startbare Medium. Dem Verwaltungspunkt wird von jedem Computer, der von dem startbaren Medium aus gestartet wird, das gleiche Zertifikat wie für Clientfunktionen (z. B. zum Anfordern einer Clientrichtlinie) vorgelegt.  

 Wenn Sie PXE-Start verwenden, importieren Sie das Clientauthentifizierungszertifikat in den PXE-fähigen Verteilungspunkt. Für jeden Client, der von diesem PXE-fähigen Verteilungspunkt gestartet wird, wird das gleiche Zertifikat verwendet. Aus Sicherheitsgründen wird empfohlen, Benutzer, die ihren Computer mit einem PXE-Dienst verbinden, zur Eingabe eines Kennworts aufzufordern. Dadurch schützen Sie den privaten Schlüssel und andere sensible Daten in den Tasksequenzen.  

 Sollte eines dieser Clientauthentifizierungszertifikate gefährdet sein, sperren Sie die Zertifikate im Arbeitsbereich **Verwaltung** über die Knoten **Zertifikate** und **Sicherheit** . Sie benötigen das Recht zur **Verwaltung des Zertifikats zur Betriebssystembereitstellung**, um diese Zertifikate verwalten zu können.  

 Nach der Bereitstellung des Betriebssystems und der Installation von Configuration Manager fordert der Client sein eigenes PKI-Clientauthentifizierungszertifikat für die HTTPS-Clientkommunikation.  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>ISV-Proxylösungen und PKI-Zertifikate  
 Unabhängige Softwarehersteller (Independent Software Vendors, ISVs) können Anwendungen zum Erweitern von Configuration Manager erstellen. Ein ISV kann beispielsweise Erweiterungen erstellen, um Nicht-Windows-Plattformen, wie Macintosh- oder UNIX-Computer, zu unterstützen. Wenn für die Standortsysteme jedoch HTTPS-Clientverbindungen erforderlich sind, müssen von diesen Clients ebenfalls PKI-Zertifikate für die Kommunikation mit dem Standort verwendet werden. Configuration Manager bietet die Möglichkeit, dem ISV-Proxy ein Zertifikat zuzuweisen, über das die Kommunikation zwischen den ISV-Proxyclients und dem Verwaltungspunkt ermöglicht wird. Wenn Sie Erweiterungen verwenden, die ISV-Proxyzertifikate erfordern, sollten Sie die Dokumentation des Produkts zu Hilfe nehmen. Weitere Informationen zum Erstellen von ISV-Proxyzertifikaten finden Sie im Configuration Manager Software Developer Kit (SDK).  

 Sollte das ISV-Zertifikat gefährdet sein, sperren Sie das Zertifikat im Arbeitsbereich **Verwaltung** über die Knoten **Zertifikate** und **Sicherheit** .  

### <a name="asset-intelligence-and-certificates"></a>Asset Intelligence und Zertifikate  
 Configuration Manager wird mit einem X.509-Zertifikat installiert, über das vom Asset Intelligence-Synchronisierungspunkt eine Verbindung mit Microsoft hergestellt wird. Configuration Manager verwendet dieses Zertifikat, um ein Clientauthentifizierungszertifikat vom Microsoft-Zertifikatdienst anzufordern. Das Clientauthentifizierungszertifikat wird auf dem Standortsystemserver des Asset Intelligence-Synchronisierungspunkts installiert und dient zur Authentifizierung des Servers gegenüber Microsoft. In Configuration Manager dient das Clientauthentifizierungszertifikat zum Herunterladen des Asset Intelligence-Katalogs und zum Hochladen von Softwaretiteln.  

 Dieses Zertifikat hat eine Schlüssellänge von 1024 Bit.  

### <a name="cloud-based-distribution-points-and-certificates"></a>Cloudbasierte Verteilungspunkte und Zertifikate  
 Ab System Center 2012 Configuration Manager SP1 erfordern cloudbasierte Verteilungspunkte ein Verwaltungszertifikat (selbstsigniert oder PKI), das Sie in Microsoft Azure hochladen. Für dieses Verwaltungszertifikat ist eine Funktion zur Serverauthentifizierung und eine Zertifikatschlüssellänge von 2048 Bit erforderlich. Außerdem müssen Sie ein Dienstzertifikat für jeden cloudbasierten Verteilungspunkt konfigurieren, bei dem es sich nicht um ein selbstsigniertes Zertifikat handeln darf. Die Funktion zur Serverauthentifizierung und eine Zertifikatschlüssellänge von 2048 Bit ist hierfür jedoch ebenfalls erforderlich.  

> [!NOTE]  
>  Das selbstsignierte Verwaltungszertifikat dient nur zu Testzwecken und ist nicht für Produktionsnetzwerke geeignet.  

 Für Clients ist es nicht erforderlich, dass für ein PKI-Clientzertifikat cloudbasierte Verteilungspunkte verwendet werden. Die Authentifizierung für die Verwaltung erfolgt entweder über ein selbstsigniertes Zertifikat oder ein PKI-Clientzertifikat. Der Verwaltungspunkt stellt dann ein Configuration Manager-Zugriffstoken für den Client aus, das der Client dem cloudbasierten Verteilungspunkt präsentieren kann. Das Token ist acht Stunden lang gültig.  

### <a name="the-microsoft-intune-connector-and-certificates"></a>Der Microsoft Intune-Connector und Zertifikate  
 Wenn Windows Intune mobile Geräte registriert, können Sie diese mobilen Geräte in Configuration Manager verwalten, indem Sie einen Microsoft Intune-Connector erstellen. Der Connector verwendet ein PKI-Zertifikat mit Clientauthentifizierungsfunktion, um Configuration Manager gegenüber Microsoft Intune zu authentifizieren, und alle Informationen per SSL-Verbindung zu übertragen. Die Zertifikatschlüsselgröße beträgt 2048 Bit, und es wird der SHA-1-Hashalgorithmus verwendet.  

 Wenn Sie den Connector installieren, wird ein Signaturzertifikat für Sideload-Schlüssel erstellt und auf dem Standortserver gespeichert. Ferner wird ein Verschlüsselungszertifikat erstellt und auf dem Zertifikatregistrierungspunkt gespeichert, um die SCEP-Abfrage (Simple Certificate Enrollment Protocol) zu verschlüsseln. Die Zertifikatschlüsselgröße beträgt 2048 Bit, und es wird der SHA-1-Hashalgorithmus verwendet.  

 Wenn Intune mobile Geräte registriert, installiert es ein PKI-Zertifikat auf dem mobilen Gerät. Dieses Zertifikat verfügt über eine Funktion zur Clientauthentifizierung, und es werden eine Schlüsselgröße von 2048 Bit und der SHA-1-Hashalgorithmus verwendet.  

 Diese PKI-Zertifikate werden von Microsoft Intune automatisch angefordert, generiert und installiert.  

### <a name="crl-checking-for-pki-certificates"></a>Überprüfen der Zertifikatsperrlisten für PKI-Zertifikate  
 Durch eine PKI-Zertifikatsperrliste wird zwar der Verwaltungs- und Verarbeitungsaufwand erhöht, aber auch mehr Sicherheit gewährleistet. Wenn die Überprüfung der Zertifikatsperrlisten aktiviert ist, aber die Zertifikatsperrliste nicht abgerufen werden kann, kann keine PKI-Verbindung hergestellt werden. Weitere Informationen finden Sie unter [Sicherheit und Datenschutz für System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

 Die Überprüfung der Zertifikatsperrlisten ist in IIS standardmäßig aktiviert. Wenn Sie also eine Zertifikatsperrliste bei einer PKI-Bereitstellung verwenden, müssen die Configuration Manager-Standortsysteme, auf denen IIS ausgeführt werden, in der Regel nicht weiter konfiguriert werden. Eine Ausnahme sind Softwareupdates, die einen manuellen Schritt zum Aktivieren der CRL-Prüfung erfordern, damit die Signaturen in Softwareupdatedateien überprüft werden können.  

 Die Überprüfung der Zertifikatsperrlisten ist für Clientcomputer, von denen HTTPS-Clientverbindungen verwendet werden, standardmäßig aktiviert. Die Überprüfung der Zertifikatsperrlisten ist nicht standardmäßig aktiviert, wenn Sie die Out-of-Band-Verwaltungskonsole ausführen, um eine Verbindung mit einem AMT-basierten Computer herzustellen. Sie können diese Option aktivieren. Sie können die Überprüfung der Zertifikatsperrlisten für Clients auf Macintosh-Computern in Configuration Manager SP1 oder höher nicht deaktivieren.  

 Die Überprüfung der Zertifikatsperrlisten wird nicht für die folgenden Verbindungen in Configuration Manager unterstützt:  

-   Server-zu-Server-Verbindungen  

-   Von Configuration Manager registrierte mobile Geräte.  

-   Von Microsoft Intune registrierte mobile Geräte.  

##  <a name="cryptographic-controls-for-server-communication"></a>Kryptografische Steuerelemente für die Serverkommunikation  
 Configuration Manager verwendet die folgenden kryptografischen Steuerelemente für die Serverkommunikation.  

### <a name="server-communication-within-a-site"></a>Serverkommunikation innerhalb eines Standorts  
 Jeder Standortsystemserver verwendet ein Zertifikat zur Datenübertragung auf andere Standortsysteme innerhalb des gleichen Configuration Manager-Standorts. Von einigen Standortsystemrollen werden auch Zertifikate für die Authentifizierung verwendet. Wenn Sie beispielsweise den Anmeldungsproxypunkt auf einem Server und den Anmeldungspunkt auf einem anderen Server installieren, erfolgt die gegenseitige Authentifizierung über dieses Identitätszertifikat. Wenn Configuration Manager für diese Kommunikation ein Zertifikat verwendet, und ein PKI-Zertifikat mit Serverauthentifizierungsfunktion verfügbar ist, wird dieses Zertifikat automatisch von Configuration Manager verwendet. Andernfalls generiert Configuration Manager ein selbstsigniertes Zertifikat. Von diesem selbstsignierten Zertifikat, das Serverauthentifizierungsfunktionen hat, wird SHA-256 verwendet und eine Schlüssellänge von 2048 Bit unterstützt. Configuration Manager kopiert das Zertifikat in den Speicher für vertrauenswürdige Personen auf anderen Standortsystemservern, von denen das Standortsystem möglicherweise als vertrauenswürdig eingestuft werden muss. Mithilfe dieser Zertifikate und PeerTrust wird eine bidirektionale Vertrauensstellung zwischen Standortsystemen ermöglicht.  

 Zusätzlich zu diesem Zertifikat für jeden Standortsystemserver generiert Configuration Manager für die meisten Standortsystemrollen ein selbstsigniertes Zertifikat. Wenn es von einer Standortsystemrolle mehrere Instanzen am gleichen Standort gibt, gilt für alle Instanzen das gleiche Zertifikat. Beispielsweise können sich an einem Standort mehrere Verwaltungspunkte oder Anmeldungspunkte befinden. Von diesem selbstsignierten Zertifikat wird ebenfalls SHA-256 verwendet, und es hat eine Schlüssellänge von 2048 Bit. Es wird ebenfalls in den Speicher für vertrauenswürdige Personen auf Standortsystemservern kopiert, von denen es möglicherweise als vertrauenswürdig eingestuft werden muss. Dieses Zertifikat wird von den folgenden Standortsystemrollen generiert:  

-   Anwendungskatalog-Webdienstpunkt  

-   Anwendungskatalog-Websitepunkt  

-   Asset Intelligence-Synchronisierungspunkt  

-   Zertifikatregistrierungspunkt  

-   Endpoint Protection-Punkt  

-   Anmeldungspunkt  

-   Fallbackstatuspunkt  

-   Verwaltungspunkt  

-   Multicast-fähiger Verteilungspunkt  

-   Out-of-Band-Dienstpunkt  

-   Reporting Services-Punkt  

-   Softwareupdatepunkt  

-   Zustandsmigrationspunkt  

-   Systemintegritätsprüfungspunkt  

-   Microsoft Intune-Connector  

 Diese Zertifikate werden automatisch von Configuration Manager verwaltet und bei Bedarf automatisch generiert.  

 Configuration Manager verwendet außerdem ein Clientauthentifizierungszertifikat, um Statusmeldungen vom Verteilungspunkt an den Verwaltungspunkt zu senden. Wenn der Verwaltungspunkt nur für HTTPS-Clientverbindungen konfiguriert ist, müssen Sie ein PKI-Zertifikat verwenden. Wenn vom Verwaltungspunkt HTTP-Verbindungen akzeptiert werden, können Sie ein PKI-Zertifikat verwenden oder die Option zur Verwendung eines selbstsignierten Zertifikats mit Clientauthentifizierungsfunktion auswählen. Von diesem Zertifikat wird SHA-256 verwendet, und es hat eine Schlüssellänge von 2048 Bit.  

### <a name="server-communication-between-sites"></a>Serverkommunikation zwischen Standorten  
 Configuration Manager überträgt Daten zwischen den Standorten mithilfe von Datenbankreplikation und dateibasierter Replikation. Weitere Informationen finden Sie unter [Kommunikation zwischen Endpunkten in System Center Configuration Manager](../../core/plan-design/hierarchy/communications-between-endpoints.md).  

 Configuration Manager konfiguriert die Datenbankreplikation zwischen Standorten automatisch, und verwendet PKI-Zertifikate mit Serverauthentifizierungsfunktion, falls diese verfügbar sind. Wenn nicht, erstellt Configuration Manager selbstsignierte Zertifikate für die Serverauthentifizierung. In beiden Fällen erfolgt die Authentifizierung zwischen Standorten mithilfe von Zertifikaten im Speicher für vertrauenswürdige Personen, von dem PeerTrust verwendet wird. Mit diesem Zertifikatspeicher wird sichergestellt, dass nur die SQL Server-Computer, die von der Configuration Manager-Hierarchie verwendet werden, an der Replikation zwischen Standorten teilnehmen. Konfigurationsänderungen können von primären Standorten und dem Standort der zentralen Verwaltung an allen Standorten in der Hierarchie repliziert werden; bei sekundären Standorten hingegen ist die Replikation von Konfigurationsänderungen nur am jeweiligen übergeordneten Standort möglich.  

 Die Kommunikation zwischen Standorten wird von Standortservern mithilfe eines sicheren, automatisch ablaufenden Schlüsselaustausches eingerichtet. Vom sendenden Standortserver wird ein Hashwert generiert und mit seinem privaten Schlüssel signiert. Der empfangende Standortserver prüft die Signatur mithilfe des öffentlichen Schlüssels und vergleicht den Hashwert mit einem lokal erstellten Wert. Stimmen die Werte überein, werden die replizierten Daten vom empfangenden Standort akzeptiert. Wenn die Werte nicht übereinstimmen, lehnt Configuration Manager die Replikationsdaten ab.  

 Bei der Datenbankreplikation in Configuration Manager werden Daten mit dem SQL Server Service Broker anhand der folgenden Mechanismen zwischen Standorten übertragen:  

-   Verbindung von SQL Server mit SQL Server: Hierbei werden Windows-Anmeldeinformationen für die Serverauthentifizierung sowie selbstsignierte Zertifikate mit 1024 Bit zum Signieren und Verschlüsseln der Daten mithilfe des erweiterten Verschlüsselungsstandards (Advanced Encryption Standard, AES) verwendet. Falls PKI-Zertifikate mit Serverauthentifizierungsfunktionen verfügbar sind, werden diese verwendet. Das Zertifikat muss sich im persönlichen Speicher des Computerzertifikatspeichers befinden.  

-   SQL Service Broker: Hierbei werden selbstsignierte Zertifikate mit 2048 Bit zur Authentifizierung sowie zum Signieren und Verschlüsseln der Daten mithilfe des erweiterten Verschlüsselungsstandards (Advanced Encryption Standard, AES) verwendet. Das Zertifikat muss sich in der SQL Server-Masterdatenbank befinden.  

 Bei der dateibasierten Replikation wird das SMB-Protokoll (Server Message Block) verwendet. Diese Daten werden mit SHA-256 signiert, aber nicht verschlüsselt, da sie keine sensiblen Daten enthalten. Wenn Sie diese Daten verschlüsseln möchten, können Sie IPsec verwenden. In diesem Fall müssen Sie IPsec unabhängig von Configuration Manager implementieren.  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>Kryptografische Steuerelemente für Clients, bei denen die Kommunikation mit Standortsystemen über HTTPS erfolgt  
 Wenn von Standortsystemrollen Clientverbindungen akzeptiert werden, können Sie sie für Verbindungen über HTTPS und HTTPS bzw. nur über HTTPS konfigurieren. Von Standortsystemrollen, bei denen nur Verbindungen über das Internet möglich sind, werden nur Clientverbindungen über HTTPS akzeptiert.  

 Bei Clientverbindungen über HTTPS ist ein höheres Maß an Sicherheit gegeben, da sie in eine Public Key-Infrastruktur (PKI) integriert werden, um die Kommunikation zwischen Clients und Servern zu schützen. Wenn Sie HTTPS-Clientverbindungen konfigurieren, ohne sich zuvor umfassend mit der PKI-Planung, -Bereitstellung und den PKI-Operationen vertraut gemacht zu haben, können jedoch immer noch Sicherheitslücken bestehen. Wenn Sie Ihre Stammzertifizierungsstelle beispielsweise nicht sichern, können Angreifer die Vertrauensstellung Ihrer gesamten PKI-Infrastruktur gefährden. Wenn die PKI-Zertifikate nicht im Rahmen kontrollierter und sicherer Prozesse bereitgestellt und verwaltet werden, werden einige Clients möglicherweise nicht verwaltet, und ihnen werden daher keine kritischen Softwareupdates oder Pakete bereitgestellt.  

> [!IMPORTANT]  
>  Die für die Clientkommunikation verwendeten PKI-Zertifikate dienen lediglich zum Schutz der Kommunikation zwischen dem Client und einigen Standortsystemen. Der Kommunikationskanal zwischen dem Standortserver und den Standortsystemen oder zwischen Standortservern wird nicht von ihnen geschützt.  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>Kommunikation, die unverschlüsselt ist, wenn Clients die HTTPS-Kommunikation verwenden  
 Die Kommunikation zwischen Clients und Standortsystemen über HTTPS wird in der Regel über SSL verschlüsselt. In den folgenden Situationen findet die Kommunikation der Clients mit Standortsystemen jedoch ohne Verschlüsselung statt:  

-   Von Clients kann keine HTTPS-Verbindung im Intranet hergestellt werden, und es wird auf HTTP ausgewichen, sofern diese Konfiguration von Standortsystemen zugelassen wird.  

-   Kommunikation mit den folgenden Standortsystemrollen:  

    -   Vom Client werden Zustandsmeldungen an den Fallbackstatuspunkt gesendet.  

    -   Vom Client werden PXE-Anforderungen an einen PXE-fähigen Verteilungspunkt gesendet.  

    -   Vom Client werden Benachrichtigungsdaten an einen Verwaltungspunkt gesendet.  

 Reporting Services-Punkte sind dazu konfiguriert, HTTP oder HTTPS unabhängig vom Clientkommunikationsmodus zu verwenden.  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>Kryptografische Steuerelemente für Clientchats, bei denen die Kommunikation mit Standortsystemen über HTTP erfolgt  
 Wenn die Kommunikation zwischen Client und Standortsystemrollen über HTTP erfolgt, können für die Clientauthentifizierung PKI-Zertifikate oder von Configuration Manager generierte, selbstsignierte Zertifikate verwendet werden. Wenn Configuration Manager selbstsignierte Zertifikate generiert, verfügen sie über einen benutzerdefinierten Objektbezeichner zum Signieren und Verschlüsseln, und diese Zertifikate werden verwendet, um den Client eindeutig zu identifizieren. Bei allen unterstützten Betriebssystemen mit Ausnahme von Windows Server 2003 verwenden diese selbstsignierten Zertifikate SHA-256 und weisen eine Schlüssellänge von 2048 Bit auf. Bei Windows Server 2003 wird SHA1 mit einer Schlüssellänge von 1024 Bit verwendet.  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>Betriebssystembereitstellung und selbstsignierte Zertifikate  
 Wenn Sie Configuration Manager zur Bereitstellung von Betriebssystemen mithilfe von selbstsignierten Zertifikaten verwenden, muss ein Clientcomputer ebenfalls über ein Zertifikat verfügen, um mit dem Verwaltungspunkt kommunizieren zu können, auch wenn der Computer sich in einer Übergangsphase befindet, wie z.B. beim Starten von Tasksequenzmedien oder PXE-fähigen Verteilungspunkten. Zur Unterstützung dieses Szenarios für HTTP-Clientverbindungen generiert Configuration Manager selbstsignierte Zertifikate, die einen benutzerdefinierten Objektbezeichner für die Signierung und Verschlüsselung haben. Diese Zertifikate werden verwendet, um den Client eindeutig zu identifizieren. Bei allen unterstützten Betriebssystemen mit Ausnahme von Windows Server 2003 verwenden diese selbstsignierten Zertifikate SHA-256 und weisen eine Schlüssellänge von 2048 Bit auf. Bei Windows Server 2003 wird SHA1 mit einer Schlüssellänge von 1024 Bit verwendet. Wenn diese Clientauthentifizierungszertifikate gefährdet sind, sperren Sie die Zertifikate im Arbeitsbereich **Verwaltung** über die Knoten **Zertifikate** und **Sicherheit** , um zu verhindern, dass sie von Angreifern verwendet werden, um die Identität vertrauenswürdiger Clients anzunehmen.  

### <a name="client-and-server-authentication"></a>Client- und Severauthentifizierung  
 Bei HTTP-Clientverbindungen werden Verwaltungspunkte entweder mithilfe der Active Directory Domain Services oder mithilfe des vertrauenswürdigen Configuration Manager-Stammschlüssels authentifiziert. Von Clients werden keine anderen Standortsystemrollen, wie z. B. Zustandsmigrationspunkte oder Softwareupdatepunkte, authentifiziert.  

 Bei der ersten Authentifizierung eines Clients von einem Verwaltungspunkt mithilfe des selbstsignierten Clientzertifikats bietet dieses Verfahren nur minimale Sicherheit, da selbstsignierte Zertifikate von jedem beliebigen Computer generiert werden können. In diesem Szenario muss die Identifizierung des Clients durch eine Genehmigung ergänzt werden. Die Genehmigung darf nur für vertrauenswürdige Computer und entweder automatisch durch Configuration Manager oder manuell durch einen Administrator erfolgen. Weitere Informationen finden Sie im Genehmigungsabschnitt unter [Datenübertragungen zwischen Endpunkten in System Center Configuration Manager](../../core/plan-design/hierarchy/communications-between-endpoints.md).  

## <a name="to-make-configuration-manager-servers-more-secure"></a>So wird der Schutz von Configuration Manager-Servern erhöht  
Um den Schutz von Configuration Manager-Servern zu erhöhen, gehen Sie wie folgt vor:

-   Aktivieren von TLS 1.2

    Informationen zum Aktivieren von TLS 1.2 für Configuration Manager finden Sie im folgenden Wissensdatenbankartikel: [Aktivieren von TLS 1.2 für Configuration Manager]( https://support.microsoft.com/en-us/help/4040243/how-to-enable-tls-1-2-for-configuration-manager).
-   Deaktivieren von SSL 3.0, TLS 1.0 und TLS 1.1 
-   Neuanordnen der TLS-bezogenen Verschlüsselungssammlungen 

Weitere Informationen finden Sie im folgenden Wissensdatenbankartikel: [Beschränken der Verwendung bestimmter kryptografischer Algorithmen und Protokolle in „Schannel.dll“](https://support.microsoft.com/en-us/kb/245030/). Diese Verfahren haben keine Auswirkungen auf die Configuration Manager-Funktionalität.

