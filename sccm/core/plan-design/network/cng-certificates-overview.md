---
title: 'CNG-Zertifikate: Übersicht'
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zur Unterstützung von CNG-Zertifikaten (Cryptography Next Generation) für Configuration Manager-Clients und -Server.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4a4f37330f94111bcc41b81d9127039056f69e2b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="cng-certificates-overview"></a>CNG-Zertifikate: Übersicht
<!-- 1356191 --> 

Configuration Manager bietet eingeschränkte Unterstützung für CNG-Zertifikate (Cryptography: Next Generation). Configuration Manager-Clients können das PKI-Clientauthentifizierungszertifikat mit dem privaten Schlüssel im CNG-Schlüsselspeicheranbieter (KSP) verwenden. Dank der KSP-Unterstützung unterstützen Configuration Manager-Clients hardwarebasierte private Schlüssel, wie z. B. TPM KSP für PKI-Clientauthentifizierungszertifikate.

## <a name="supported-scenarios"></a>Unterstützte Szenarien
Sie können Zertifikatvorlagen des Typs [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) für die folgenden Szenarien verwenden:

- Clientregistrierung und Kommunikation mit einem HTTPS-Verwaltungspunkt   
- Softwareverteilung und Anwendungsbereitstellung mit einem HTTPS-Verteilungspunkt   
- Betriebssystembereitstellung  
- Client Messaging SDK (mit dem aktuellen Update) und ISV-Proxy   
- Cloud Management Gateway-Konfiguration  

Ab Version 1802 können Sie CNG-Zertifikate für die folgenden HTTPS-fähigen Serverrollen verwenden: <!-- 1357314 -->   
- Verwaltungspunkt
- Verteilungspunkt
- Softwareupdatepunkt
- Zustandsmigrationspunkt     

> [!NOTE]
> CNG ist mit Crypto API (CAPI) abwärtskompatibel. CAPI-Zertifikate werden weiterhin unterstützt, auch wenn die CNG-Unterstützung auf dem Client aktiviert ist.

## <a name="unsupported-scenarios"></a>Nicht unterstützte Szenarien

Die folgenden Szenarios werden derzeit nicht unterstützt:

- Die folgenden Serverrollen sind nicht betriebsbereit, wenn sie im HTTPS-Modus installiert werden und ein CNG-Zertifikat an die Website auf IIS (Internetinformationsdienste) gebunden ist: 
    - Anwendungskatalog-Webdienst
    - Anwendungskatalog-Website
    - Anmeldungspunkt  
    - Anmeldungsproxypunkt  

- Softwarecenter zeigt keine Anwendungen und Pakete als verfügbar an, die für Benutzer- oder Benutzergruppensammlungen bereitgestellt werden.

- Mithilfe von CNG-Zertifikaten kann kein Cloudverteilungspunkt erstellt werden.

- Wenn das NDES-Richtlinienmodul ein CNG-Zertifikat für die Clientauthentifizierung nutzt, schlägt die Kommunikation mit dem Zertifikatregistrierungspunkt fehl.

- Wenn Sie beim Erstellen von Tasksequenzmedien ein CNG-Zertifikat angeben, schlägt der Assistent beim Erstellen startbarer Medien fehl.

## <a name="to-use-cng-certificates"></a>So verwenden Sie CNG-Zertifikate

Um CNG-Zertifikate zu verwenden, muss die Zertifizierungsstelle (Certification Authority, CA) CNG-Zertifikatvorlagen für Zielcomputer bereitstellen. Vorlagendetails variieren je nach Szenario. Allerdings sind die folgenden Eigenschaften erforderlich:

- Registerkarte **Kompatibilität**

    - Die **Zertifizierungsstelle** muss Windows Server 2008 oder höher sein. Empfohlen wird Windows Server 2012.

    - Der **Zertifikatempfänger** muss Windows Vista/Server 2008 oder höher sein. Empfohlen wird Windows 8/Windows Server 2012.

- Registerkarte **Kryptografie**

    - Die **Anbieterkategorie** muss der **Schlüsselspeicheranbieter** sein. (erforderlich)

> [!NOTE]
> Die Anforderungen an Ihre Umgebung oder Organisation können unterschiedlich sein. Wenden Sie sich an Ihren PKI-Experten. Beachten Sie unbedingt, dass eine Zertifikatsvorlage einen Schlüsselspeicheranbieter verwenden muss, um CNG nutzen zu können.

Für optimale Ergebnisse wird empfohlen, einen Antragstellernamen aus Active Directory-Informationen zu erstellen. Verwenden Sie den DNS-Namen für das **Format des Antragstellernamens**, und verwenden Sie den DNS-Namen im alternativen Antragstellernamen. Andernfalls müssen Sie diese Informationen bereitstellen, wenn das Gerät beim Zertifikatprofil registriert wird.