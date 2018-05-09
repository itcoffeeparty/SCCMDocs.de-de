---
title: CMG-Sicherheit und -Datenschutz
description: In diesem Artikel finden Sie Informationen und Empfehlungen zur Sicherheit und Datenschutz für Cloud Management Gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.openlocfilehash: d07c30d6a1e4fd1314b6e69ac157577ae0163696
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Sicherheit und Datenschutz für Cloud Management Gateway

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieser Artikel enthält Sicherheits- und Datenschutzinformationen für Configuration Manager Cloud Management Gateway (CMG). Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

## <a name="cmg-security-details"></a>Sicherheitsdetails zu CMG
- CMG akzeptiert und verwaltet Verbindungen von CMG-Verbindungspunkten. Es verwendet gegenseitige SSL-Authentifizierung mithilfe von Zertifikaten und Verbindungs-IDs.
- CMG akzeptiert Clientanforderungen und leitet diese weiter. Dies geschieht mithilfe der folgenden Methoden:
    - Vorabauthentifizierung von Verbindungen über gegenseitiges SSL mithilfe des PKI-basierten Clientauthentifizierungszertifikats oder Azure AD 
      - Überprüfung des Zertifikatpfads auf Grundlage der vertrauenswürdigen Stammzertifizierungsstellen-Zertifikate, die zu CMG hochgeladen wurden, mithilfe von Internetinformationsdiensten auf den CMG-VM-Instanzen
      - Überprüfung der Clientzertifikatsperrung, falls aktiviert, mithilfe von Internetinformationsdiensten auf der VM-Instanz Weitere Informationen finden Sie unter [Veröffentlichen der Zertifikatsperrungsliste](#bkmk_crl).
    - Über die Zertifikatsvertrauensliste wird der Stamm des Clientauthentifizierungszertifikats überprüft. Es werden auch die gleichen Überprüfungen ausgeführt wie durch den Verwaltungspunkt für den Client. Weitere Informationen finden Sie unter [Prüfen der Einträge in der Zertifikatsvertrauensliste des Standorts](#bkmk_ctl).
    - Überprüft und filtert Clientanforderungen (URLs), um zu überprüfen, ob alle CMG-Verbindungspunkte die Anforderung erfüllen können  
    - Die Inhaltslänge wird für jeden veröffentlichenden Endpunkt überprüft.
    - Mithilfe eines Roundrobinverfahrens wird für Lastenausgleich zwischen CMG-Verbindungspunkten des gleichen Standorts gesorgt.
- Der CMG-Verbindungspunkt verwendet die folgenden Methoden:
    - Es werden konsistente HTTP/TCP-Verbindungen mit allen VM-Instanzen von CMG erstellt. Diese Verbindungen werden minütlich überprüft und verwaltet.
    - Es verwendet gegenseitige SSL-Authentifizierung für CMG mithilfe von Zertifikaten.
    - Clientanforderungen werden basierend auf URL-Zuordnungen weitergeleitet.
    - Der Verbindungsstatus wird gemeldet, um den Dienstintegritätsstatus in der Konsole anzuzeigen.
    - Der Datenverkehr auf Endpunkten wird alle fünf Minuten gemeldet.

### <a name="configuration-manager-client-facing-roles"></a>Clientseitige Configuration Manager-Rollen
Der Verwaltungspunkt und der Softwareupdatepunkt hosten in IIS Endpunkte, um Clientanforderungen zu bedienen. CMG macht nicht alle internen Endpunkte verfügbar. Jeder in Cloud Management Gateway veröffentlichte Endpunkt verfügt über eine URL-Zuordnung.
  - Die externe URL ist die URL, über die der Client mit Cloud Management Gateway kommuniziert.
  - Die interne URL ist der CMG-Verbindungspunkt, der zum Weiterleiten von Anforderungen an den internen Server verwendet wird.

#### <a name="url-mapping-example"></a>Beispiel einer URL-Zuordnung
Wenn Sie CMG-Datenverkehr auf einem Verwaltungspunkt aktivieren, erstellt Configuration Manager interne URL-Zuordnungen für jeden Verwaltungspunktserver, zum Beispiel: ccm_system, ccm_incoming und sms_mp. Die externe URL für den ccm_system-Endpunkt des Verwaltungspunkts könnte beispielsweise folgendermaßen aussehen:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
Die URL ist eindeutig für jede Verwaltungspunkt. Der Configuration Manager-Client setzt den Namen des für CMG aktivierten Verwaltungspunkts auf die Liste der Internetverwaltungspunkte. Dieser Name sieht folgendermaßen aus:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
Der Standort lädt automatisch alle veröffentlichten externe URLs in CMG hoch. Dieses Verhalten ermöglicht es CMG, URLs zu filtern. Alle URL-Zuordnungen werden zum Verbindungspunkt von CMG repliziert. Anschließend wird die Kommunikation an die internen Server weitergeleitet, entsprechend der externen URL aus der Clientanforderung.



## <a name="security-guidance-for-cmg"></a>Sicherheitshinweise für CMG


<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>Veröffentlichen der Zertifikatsperrungsliste

Veröffentlichen Sie die Zertifikatsperrliste (Certificate Revocation List, CRL) Ihrer PKI, damit internetbasierte Clients darauf zugreifen können. Wenn Sie CMG mithilfe einer PKI bereitstellen, konfigurieren Sie den Dienst auf der Registerkarte „Einstellungen“ so, dass er die **Clientzertifikatsperrung überprüft**. Diese Einstellung konfiguriert den Dienst, sodass er eine veröffentlichte Zertifikatsperrliste (CRL) verwendet. Weitere Informationen finden Sie unter [Planen der PKI-Zertifikatsperrung](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).



<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Prüfen der Einträge in der Zertifikatsvertrauensliste des Standorts
<!--503739-->
Jeder Configuration Manager-Standort enthält eine Liste der vertrauenswürdigen Stammzertifizierungsstellen, die Zertifikatsvertrauensliste (Certificate Trust List, CTL). Sie können die Liste anzeigen und anpassen, indem Sie zum Arbeitsbereich „Verwaltung“ navigieren, den Bereich „Standortkonfiguration“ erweitern und „Standorte“ auswählen. Wählen Sie einen Standort aus, und klicken Sie im Menüband auf „Eigenschaften“. Wechseln Sie zur Registerkarte „Kommunikation mit Clientcomputern“, und klicken Sie unter „Vertrauenswürdige Stammzertifizierungsstellen“ auf **Festlegen**.
 
Verwenden Sie für einen Standort mit CMG und PKI-Clientauthentifizierung eine restriktivere CTL. Andernfalls werden Clients mit Clientauthentifizierungszertifikaten, die von einem vertrauenswürdigen Stamm ausgestellt werden, der bereits auf dem Verwaltungspunkt vorhanden ist, für die Clientregistrierung automatisch akzeptiert.

Mithilfe dieser Teilmenge können Administratoren die Sicherheit besser kontrollieren. Die CTL schränkt den Server ein, sodass dieser nur Clientzertifikate annimmt, die von den Zertifizierungsstellen in der CTL ausgegeben werden. Beispiel: Windows wird mit einigen Zertifikaten von bekannten Drittanbieter-Zertifizierungsstellen (Certification Authority, CA) geliefert, z.B. VeriSign und Thawte. Standardmäßig stufen Computer mit ISS Zertifikate dieser bekannten CAs als vertrauenswürdig ein. Wenn Sie ISS nicht mit einer CTL konfigurieren, werden alle Computer mit Clientzertifikaten, die von diesen CAs ausgestellt wurden, als gültige Configuration Manager-Clients zugelassen. Wenn Sie IIS mit einer CTL konfigurieren, die diese CAs nicht enthält, werden Clientverbindungen mit Zertifikaten dieser CAs abgelehnt. 


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>Nächste Schritte

- [Planen des Cloudverwaltungsgateways](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Einrichten des Cloudverwaltungsgateways](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Frequently asked questions about the cloud management gateway (Häufig gestellte Fragen zu Cloud Management Gateway)](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Zertifikate für Cloud Management Gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
