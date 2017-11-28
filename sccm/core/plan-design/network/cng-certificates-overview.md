---
title: "CNG-Zertifikate: Übersicht"
titleSuffix: Configuration Manager
description: "Eine Übersicht über CNG-Zertifikate in Configuration Manager"
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 
author: vhorne
ms.author: victorh
manager: angrobe
ms.openlocfilehash: f5f5138270d4f14b76b2c41e41ec034a0c12a932
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="cng-certificates-overview"></a>CNG-Zertifikate: Übersicht
<!-- 1356191 --> 

Configuration Manager bietet eingeschränkte Unterstützung für CNG-Zertifikate (Cryptography: Next Generation). Configuration Manager-Clients können das PKI-Clientauthentifizierungszertifikat mit dem privaten Schlüssel im CNG-Schlüsselspeicheranbieter (KSP) verwenden. Dank der KSP-Unterstützung unterstützen Configuration Manager-Clients hardwarebasierte private Schlüssel, wie z. B. TPM KSP für PKI-Clientauthentifizierungszertifikate.

## <a name="supported-scenarios"></a>Unterstützte Szenarien
Sie können Zertifikatvorlagen des Typs [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) für die folgenden Szenarien verwenden:

- Clientregistrierung und Kommunikation mit einem HTTPS-Verwaltungspunkt   
- Softwareverteilung und Anwendungsbereitstellung mit einem HTTPS-Verteilungspunkt   
- Betriebssystembereitstellung  
- Client messaging SDK (mit dem aktuellen Update) und ISV-Proxy   
- Cloud Management Gateway-Konfiguration  

> [!NOTE]
> CNG ist mit Crypto API (CAPI) abwärtskompatibel. CAPI-Zertifikate werden weiterhin unterstützt, auch wenn die CNG-Unterstützung auf dem Client aktiviert ist.

## <a name="unsupported-scenarios"></a>Nicht unterstützte Szenarien

Die folgenden Szenarien werden derzeit nicht unterstützt:

- Die Rollen „Anwendungskatalog-Webdienst“, „Anwendungskatalog-Website“, „Anmeldungspunkt“ und „Anmeldungsproxypunkt“ funktionieren nicht bei Installation im HTTPS-Modus, wenn ein CNG-Zertifikat in Internetinformationsdienste (IIS) an die Website gebunden ist. Softwarecenter zeigt keine Anwendungen und Pakete als verfügbar an, die für Benutzer- oder Benutzergruppensammlungen bereitgestellt werden.

- Wenn bei Installation im HTTPS-Modus ein CNG-Zertifikat an die Website in IIS gebunden ist, ist der Zustandsmigrationspunkt nicht betriebsbereit.

- Mithilfe von CNG-Zertifikaten kann kein Cloudverteilungspunkt erstellt werden.

- Die Kommunikation zwischen dem Richtlinienmodul des Registrierungsdiensts für Netzwerkgeräte (NDES) und dem Zertifikatregistrierungspunkt misslingt, wenn das NDES-Richtlinienmodul als Zertifikat für die Clientauthentifizierung ein CNG-Zertifikat nutzt.

- Bei Angabe eines CNG-Zertifikats kann mithilfe der Tasksequenz zur Medienerstellung kein startfähiges Medium erstellt werden.

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