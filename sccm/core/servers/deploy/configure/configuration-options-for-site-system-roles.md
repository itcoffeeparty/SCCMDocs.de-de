---
title: "Optionen für Standortsystemrollen | Microsoft-Dokumentation"
description: "In diesem Artikel finden Sie Informationen über Configuration Manager-Standortsystemrollen, die nicht unbedingt selbsterklärend sind."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: 2ff7c8b35538cf475aad665b29a95304d794c4ff

---
# <a name="configuration-options-for-site-system-roles-for-system-center-configuration-manager"></a>Konfigurationsoptionen für Standortsystemrollen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die meisten Konfigurationsoptionen für System Center Configuration Manager-Standortsystemrollen sind selbsterklärend oder werden im Assistenten oder den Dialogfeldern erklärt, wenn Sie sie konfigurieren.  Die folgenden Abschnitte enthalten ausführliche Informationen zu Standortsystemrollen, die über Einstellungen verfügen, die zusätzliche Informationen erfordern.  

##  <a name="a-namebkmkapplicationcatalogwebsitea-application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a> Anwendungskatalog-Websitepunkt  
 Informationen zum Konfigurieren des Anwendungskatalog-Websitepunkts für den Anwendungskatalog finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung in System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **Clientverbindungen**  

 Wählen Sie für die Verbindungen **HTTPS** aus, indem Sie die Einstellung mit höherer Sicherheit verwenden, um zu bestimmen, ob von Clients eine Verbindung über das Internet hergestellt wird. Für diese Option ist ein PKI-Zertifikat auf dem Server zur Serverauthentifizierung bei den Clients und zur Datenverschlüsselung mithilfe von SSL (Secure Sockets Layer) erforderlich. Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Eine Beispielbereitstellung des Serverzertifikats sowie Informationen zum Konfigurieren des Zertifikats in Internet Information Services (IIS) finden Sie im Abschnitt *Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden* des Themas [Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für System Center Configuration Manager: Windows Server 2008-Zertifizierungsstelle](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

 **Anwendungskatalog-Website der Zone vertrauenswürdiger Sites hinzufügen**  

 Von dieser Nachricht wird angezeigt, ob der Wert in der Clienteinstellung **Standardanwendungskatalog-Website zur Internet Explorer-Zone der vertrauenswürdigen Sites hinzufügen** aktuell **Wahr** oder **Falsch**lautet. Wenn Sie diese Einstellung mit benutzerdefinierten Clienteinstellungen konfiguriert haben, müssen Sie diesen Wert selbst prüfen.  

 Wenn dieses Standortsystem für einen FQDN konfiguriert ist und die Website sich nicht in der Internet Explorer-Zone der vertrauenswürdigen Sites befindet, werden Benutzer zur Eingabe von Anmeldeinformationen aufgefordert, wenn sie eine Verbindung mit dem Anwendungskatalog herstellen.  

 **Organisationsname**  

 Geben Sie den Namen ein, den die Benutzer im Anwendungskatalog sehen werden. Diese Branding-Informationen helfen den Benutzern, die Website als vertrauenswürdige Quelle zu identifizieren.  

##  <a name="a-namebkmkapplicationcatalogwebservicea-application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a> Anwendungskatalog-Webdienstpunkt  
 Informationen zum Konfigurieren des Anwendungskatalog-Webdienstpunkts für den Anwendungskatalog finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung in System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **HTTPS**  

 Wählen Sie **HTTPS** zur Authentifizierung der Anwendungskatalog-Websitepunkte bei diesem Anwendungskatalog-Webdienstpunkt aus.  Für diese Option ist ein PKI-Zertifikat auf den Servern, die den Anwendungskatalog-Websitepunkt ausführen, zur Serverauthentifizierung und zur Datenverschlüsselung mithilfe von SSL erforderlich. Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Eine Beispielbereitstellung des Serverzertifikats sowie Informationen zum Konfigurieren des Zertifikats in IIS finden Sie im Abschnitt *Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden* des Themas [Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für System Center Configuration Manager: Windows Server 2008-Zertifizierungsstelle](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="a-namebkmkcertificateregistrationpointa-certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a> Zertifikatregistrierungspunkt  
 Informationen zum Konfigurieren des Zertifikatregistrierungspunkts finden Sie unter [Introduction to certificate profiles in System Center Configuration Manager (Einführung in Zertifikatprofile in System Center Configuration Manager)](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

##  <a name="a-namebkmkdistributionpointa-distribution-point"></a><a name="BKMK_Distribution_Point"></a> Verteilungspunkt  
 Informationen zum Konfigurieren der Verteilungspunkte und zur Bereitstellung des Inhalts finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Informationen zum Konfigurieren der Verteilungspunkte für PXE-Bereitstellungen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Informationen zum Konfigurieren der Verteilungspunkte für Multicast-Bereitstellungen finden Sie unter [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 **IIS installieren und konfigurieren, sofern dies für Configuration Manager erforderlich ist**  
 Aktivieren Sie diese Option, damit IIS von Configuration Manager auf dem Server installiert und konfiguriert werden, sofern sie noch nicht installiert sind. IIS müssen auf allen Verteilungspunkten installiert sein, und Sie müssen diese Einstellung auswählen, um mit dem Assistenten fortzufahren.  

 **Standortsystem-Installationskonto**  
 Bei Verteilungspunkten, die auf einem Standortserver installiert sind, wird nur die Verwendung des Computerkontos des Standortservers als Standortsystem-Installationskonto unterstützt.  

 **Erstellen Sie ein selbstsigniertes Zertifikat, oder importieren Sie ein PKI-Clientzertifikat.**  
 Von diesem Zertifikat werden zwei Zwecke erfüllt:  

1.  Durch das Zertifikat wird der Verteilungspunkt gegenüber einem Verwaltungspunkt authentifiziert, bevor vom Verteilungspunkt Statusmeldungen gesendet werden.  

2.  Wenn das Kontrollkästchen **PXE-Unterstützung für Clients aktivieren** aktiviert ist, wird das Zertifikat an Computer gesendet, von denen ein PXE-Start ausgeführt wird, um während der Bereitstellung des Betriebssystems eine Verbindung mit dem Verwaltungspunkt zu ermöglichen.  

Wenn alle Verwaltungspunkte am Standort für HTTP konfiguriert sind, erstellen Sie ein selbstsigniertes Zertifikat. Wenn die Verwaltungspunkte für HTTPS konfiguriert sind, importieren Sie ein PKI-Clientzertifikat.  

Suchen Sie eine Public Key Cryptography Standard #12-Datei (PKCS 12), die ein PKI-Zertifikat mit den folgenden Anforderungen für Configuration Manager enthält, um das Zertifikat zu importieren:  

-   Die Clientauthentifizierung muss zur Verwendung vorgesehen sein.  

-   Der private Schlüssel muss für den Export konfiguriert sein.  

Es bestehen keine speziellen Anforderungen für den Zertifikatantragsteller oder den alternativen Antragstellernamen (Subject Alternative Name, SAN). Sie können ein Zertifikat für mehrere Verteilungspunkte verwenden.  

Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Eine Beispielbereitstellung dieses Zertifikats finden Sie im Abschnitt *Bereitstellen des Clientzertifikats für Verteilungspunkte* des Themas [Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für System Center Configuration Manager: Windows Server 2008-Zertifizierungsstelle](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

**Diesen Verteilungspunkt für vorab bereitgestellten Inhalt aktivieren**  
Aktivieren Sie dieses Kontrollkästchen, um den Verteilungspunkt für vorab bereitgestellten Inhalt zu aktivieren. Ist diese Einstellung ausgewählt, können Sie das Verteilungsverhalten bei der Inhaltsverteilung konfigurieren. Sie können zwischen den folgenden Möglichkeiten wählen: Inhalt wird vorab am Verteilungspunkt bereitgestellt, nur der Anfangsinhalt des Pakets wird vorab bereitgestellt und Updates erfolgen mithilfe des regulären Inhaltsverteilungsvorgangs, oder für Inhalt des Pakets wird stets der reguläre Inhaltsverteilungsvorgang verwendet.  

**Begrenzungsgruppen**  
 Sie können einem Verteilungspunkt Begrenzungsgruppen zuordnen. Bei der Inhaltsbereitstellung müssen sich die Clients in einer dem Verteilungspunkt zugeordneten Begrenzungsgruppe befinden, damit der Verteilungspunkt als Quellort für Inhalt verwendet werden kann.
 - **Vor Version 1610** können Sie das Kontrollkästchen **Fallbackquellpfad für Inhalt zulassen** aktivieren, um für Clients außerhalb solcher Begrenzungsgruppen ein Ausweichen auf den Verteilungspunkt als Quellort für Inhalt zu ermöglichen, wenn keine anderen Verteilungspunkte verfügbar sind.
 - **Ab Version 1610** können Sie **Fallbackquellpfad für Inhalt zulassen** nicht mehr konfigurieren.  Stattdessen können Sie Beziehungen zwischen Begrenzungsgruppen konfigurieren, die bestimmen, ab wann ein Client mit der Suche nach zusätzlichen Begrenzungsgruppen für einen gültigen Quellspeicherort für den Inhalt suchen kann.

##  <a name="a-namebkmkenrollmentpointa-enrollment-point"></a><a name="BKMK_Enrollment_Point"></a> Anmeldungspunkt  
Anmeldungspunkte werden zur Installation von Macintosh-Computern und Anmeldung mobiler Geräte  verwendet, die Sie mithilfe der lokalen Geräteverwaltung verwalten. Weitere Informationen finden Sie unter:  

-   [Bereitstellen von Clients auf Macintosh-Computern in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

-   [Informationen zur Registrierung von Geräten mit der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

**Zulässige Verbindungen**  
 Die HTTPS-Einstellung wird automatisch verwendet. Für diese ist ein PKI-Zertifikat für den Server zur Serverauthentifizierung beim Anmeldungsproxypunkt und beim Out-of-Band-Dienstpunkt sowie zur SSL-Datenverschlüsselung erforderlich. Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Eine Beispielbereitstellung des Serverzertifikats sowie Informationen zum Konfigurieren des Zertifikats in IIS finden Sie im Abschnitt *Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden* des Themas [Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für System Center Configuration Manager: Windows Server 2008-Zertifizierungsstelle](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="a-namebkmkenrollmentproxypointa-enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a> Anmeldungsproxypunkt  
Weitere Informationen zum Konfigurieren eines Anmeldungsproxypunkts für mobile Geräte finden Sie unter [Informationen zur Registrierung von Geräten mit der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

**Clientverbindungen**  
 Die HTTPS-Einstellung wird automatisch verwendet. Für diese ist ein PKI-Zertifikat für den Server zur Serverauthentifizierung bei mobilen Geräten und Macintosh-Computern, die mithilfe von Configuration Management angemeldet wurden, sowie zur SSL-Datenverschlüsselung (Secure Sockets Layer) erforderlich. Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Eine Beispielbereitstellung des Serverzertifikats sowie Informationen zum Konfigurieren des Zertifikats in IIS finden Sie im Abschnitt *Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden* des Themas [Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für System Center Configuration Manager: Windows Server 2008-Zertifizierungsstelle](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="a-namebkmkfallbackstatuspointa-fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a> Fallbackstatuspunkt  
**Anzahl der Zustandsmeldungen** und **Einschränkungsintervall (in Sekunden)**  
Die Standardeinstellungen dieser beiden Optionen (10.000 Zustandsmeldungen und 3.600 Sekunden beim Einschränkungsintervall) sind unter den meisten Umständen ausreichend. Dennoch kann es erforderlich sein, dass Sie diese Einstellungen ändern, wenn die beiden folgenden Bedingungen erfüllt sind:  

-   Vom Fallbackstatuspunkt werden Verbindungen nur aus dem Intranet akzeptiert.  

-   Sie verwenden den Fallbackstatuspunkt während der Einführung einer Clientbereitstellung für zahlreiche Computer.  

In diesem Szenario kann es durch einen kontinuierlichen Strom von Zustandsmeldungen zu einem Rückstand kommen, durch den dauerhaft eine hohe CPU-Auslastung auf dem Standortserver verursacht wird. Außerdem sehen Sie in der Configuration Manager-Konsole und in den Clientbereitstellungsberichten möglicherweise keine aktuellen Informationen über die Clientbereitstellung.  

Diese Einstellungen für Fallbackstatuspunkte sollen für Zustandsmeldungen konfiguriert werden, die während der Clientbereitstellung generiert werden. Sie sind nicht für Probleme bei der Kommunikation mit Clients gedacht, beispielsweise wenn von Clients im Internet keine Verbindung mit dem internetbasierten Verwaltungspunkt hergestellt werden kann. Da diese Einstellungen von dem Fallbackstatuspunkt nicht nur auf die Zustandsmeldungen angewendet werden können, die während der Clientbereitstellung generiert werden, sollten Sie die Einstellungen nicht konfigurieren, wenn vom Fallbackstatuspunkt Verbindungen aus dem Internet akzeptiert werden.  

Jeder Computer, auf dem der System Center 2012 Configuration Manager-Client installiert wurde, sendet die folgenden vier Zustandsmeldungen an den Fallbackstatuspunkt:  

-   Clientbereitstellung wurde gestartet  

-   Clientbereitstellung war erfolgreich  

-   Clientzuweisung wurde gestartet  

-   Clientzuweisung war erfolgreich  

Von Computern, die nicht installiert werden können bzw. von denen der Configuration Manager-Client nicht zugewiesen werden kann, werden zusätzliche Zustandsmeldungen gesendet.  

Wenn Sie den Configuration Manager-Client beispielsweise für 20.000 Computer bereitstellen, werden möglicherweise 80.000 Zustandsmeldungen von der Bereitstellung erstellt und an den Fallbackstatuspunkt gesendet. Da in der Standardkonfiguration der Einschränkung alle 3.600 Sekunden (1 Stunde) 10.000 Zustandsmeldungen an den Fallbackstatuspunkt gesendet werden können, kann beim Fallbackstatuspunkt ein Rückstand bei der Verarbeitung der Zustandsmeldungen entstehen. Bei der Verarbeitung zahlreicher Zustandsmeldungen müssen auch die verfügbare Netzwerkbandbreite zwischen dem Fallbackstatuspunkt und dem Standortserver sowie die Verarbeitungsgeschwindigkeit des Standortservers berücksichtigt werden.  

Um solche Probleme zu vermeiden, sollten Sie erwägen, die Anzahl von Zustandsmeldungen zu erhöhen und das Einschränkungsintervall zu verkürzen.  

Setzen Sie die Einschränkungswerte für den Fallbackstatuspunkt zurück, wenn eine der folgenden Bedingungen zutrifft:  

-   Ihren Berechnungen nach sind die aktuellen Einschränkungswerte höher, als dies für die Verarbeitung von Zustandsmeldungen vom Fallbackstatuspunkt erforderlich ist.  

-   Mit den aktuellen Einschränkungswerten stellen Sie eine hohe Prozessorauslastung des Standortservers fest.  

Ändern Sie die Einschränkungseinstellungen für den Fallbackstatuspunkt nur dann, wenn Sie sich über die Konsequenzen im Klaren sind. Wenn Sie beispielsweise die Einschränkungseinstellungen zu stark erhöhen, kann dadurch die Prozessorauslastung des Standortservers so erhöht werden, dass dadurch alle Standortvorgänge verlangsamt werden.  



<!--HONumber=Dec16_HO3-->


