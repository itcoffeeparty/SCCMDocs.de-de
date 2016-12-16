---
title: "Einführung in Long-Term Servicing Branch | System Center Configuration Manager"
description: "Erfahren Sie mehr über Long-Term Servicing Branch von System Center Configuration Manager."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2a45cfb3e00d8078fbf45bdc8a2668b7dd0a62c6
ms.openlocfilehash: 926d1b1299e7851bd1d9168237859c5cd7a65abe


---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Einführung in Long-Term Servicing Branch von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Long-Term Servicing Branch)*

Verwenden Sie dieses Thema, um mehr über Long-Term Servicing Branch (LTSB) von Configuration Manager zu erfahren und die Dokumentation für diesen Branch zu verstehen.


LTSB ist ein einzelner Configuration Manager-Branch, der auf der Version 1606 von Current Branch basiert. Im Vergleich zu Current Branch verfügt LTSB über [eingeschränkte Funktionalität](#features-that-are-not-available-in-the-ltsb-of-configuration-manager). Es dient den Kunden, die [ihre Software Assurance-Rechte oder entsprechende Abonnementrechte auslaufen lassen](/sccm/core/understand/learn-more-editions#software-assurance-and-the-ltsb).

**Übersicht über die Lizenz:**   
Kunden mit aktiver Software Assurance für System Center Configuration Manager-Lizenzen oder mit entsprechenden Abonnementrechten ab 1. Oktober 2016, verfügen über Benutzungsrechte des System Center Configuration Manager-Release 1606 vom Oktober 2016. Kunden, die ab dem 1. Oktober 2016 oder danach über Rechte für System Center Configuration Manager verfügen, erhalten während der Installation zwei lizenzierte Optionen: Current Branch und Long-Term Servicing Branch (LTSB).

**Besonderheiten bei der Lizenzierung:**  
[Vollständige Geschäftsbedingungen für die Produkte, die Sie über Microsoft-Volumenlizenzierungsprogramme erwerben, finden Sie hier](http://go.microsoft.com/fwlink/?LinkId=800052).

Kunden, die über unbefristete Rechte für System Center Configuration Manager verfügen, oder die die Software Assurance oder das Abonnement nach dem 1. Oktober auslaufen lassen, können die LTSB-Version von System Center Configuration Manager installieren, die zu dem Zeitpunkt vorhanden ist, an dem die Software Assurance oder das Abonnement ausläuft.
- Informationen zur Software Assurance und zu Lizenzanforderungen für System Center Configuration Manager finden Sie unter [Licensing and branches for System Center Configuration Manager (Lizenzierung und Branches für System Center Configuration Manager)](learn-more-editions.md).
-   Informationen zu den Unterschieden zwischen den verschiedenen Branches finden Sie unter [Which branch of Configuration Manager should I use (Welchen Configuration Manager-Branch soll ich verwenden?)](which-branch-should-i-use.md).

Verwenden Sie das Baselinemedium von Version 1606, um einen neuen Standort zu installieren oder um ein Upgrade von einem unterstützten System Center 2012 Configuration Manager-Standort auf LTSB durchzuführen. Dieses Baselinemedium ist als Teil des Microsoft System Center 2016- oder des System Center Configuration Manager-Release (Current Branch und Long-Term Servicing Branch 1606) verfügbar. Das Baselinemedium, das LTSB installieren kann, kann auch verwendet werden, um die Current Branch-Version 1606 von Configuration Manager zu installieren. Weitere Informationen zum Baselinemedium finden Sie auf der Seite zu den [Baseline- und Updateversionen](/sccm/core/servers/manage/updates#baseline-and-update-versions).

Informationen zum Installieren eines LTSB-Standorts finden Sie unter [Install and Upgrade for the Long-Term Servicing Branch (Installieren und Upgraden für Long Term Servicing Branch)](install-the-ltsb.md). Informationen zum Erhalt von System Center 2016 finden Sie in der [Dokumentation für System Center 2016](https:\technet.microsoft.com\system-center-docs\System-Center-2016).

> [!IMPORTANT]
> Alle Standorte in einer Hierarchie müssen den gleichen Branch ausführen. Eine Hierarchie mit einer Mischung aus LTSB und Current Branch an unterschiedlichen Standorten wird nicht unterstützt.
>
> Entsprechend müssen Sie den Standort oder die Standortdatenbank auf den ursprünglichen Branch wiederherstellen, wenn Sie die Wiederherstellung verwenden. Sie können keine Current Branch-Standortdatenbank auf einer LTSB-Installation wiederherstellen oder umgekehrt.


## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Funktionen, die nicht in LTSB von Configuration Manager verfügbar sind
Im Vergleich zu Current Branch hat LTSB die folgenden Unterstützungseinschränkungen:

- Erhält keine Updates für neue Funktionen.
- Unterstützt nicht das Hinzufügen eines Microsoft Intune-Abonnements, das den Gebrauch von Folgendem verhindert:
  - Intune in einer Konfiguration mit hybrider Verwaltung mobiler Geräte
  - Lokale Verwaltung mobiler Geräte
-   Unterstützt nicht die Verwendung des Windows 10-Wartungsdashboards sowie Wartungspläne und unterstützt nicht Current Branch (CB) von Windows 10 und Current Branch for Business (CBB)
- Zukünftige Releases von LTSB für Windows 10 und Windows Server werden nicht unterstützt.
-   Keine Unterstützung für Asset Intelligence
-   Keine Unterstützung für cloudbasierte Verteilungspunkte
-   Keine Unterstützung für den Support für Exchange Online als Exchange-Connector
-   Unterstützt keine Features der Vorabversion


Obwohl die Unterstützung für diese Funktionen nicht in LTSB enthalten sind, bleiben einige davon in der Configuration Manager-Konsole sichtbar, können jedoch nicht ausgewählt oder verwendet werden.

Darüber hinaus werden neue Betriebssysteme, die als von Current Branch unterstützt hinzugefügt werden, nicht von LTSB unterstützt.

## <a name="documentation-for-the-ltsb"></a>Dokumentation für LTSB
Da LTSB auf Version 1606 Current Branch basiert, ist die von Ihnen verwendete Dokumentation für LTSB die [Onlinedokumentation, die für Current Branch gilt](https://docs.microsoft.com/sccm/), zusammen mit den Vorbehalten und Einschränkungen, die für LTSB spezifisch sind, so wie in folgendem Thema identifiziert:  

-   [Introduction to the Long-Term Servicing Branch (Einführung in Long Term Servicing Branch)](introduction-to-the-ltsb.md) – (dieses Thema)

-   [Which branch of Configuration Manager should I use (Welchen Configuration Manager-Branch soll ich verwenden)](which-branch-should-i-use.md) – Informationen über die unterschiedlichen System Center Configuration Manager-Branches, damit Sie sicher sein können, dass Sie den besten Branch für Ihre Bedürfnisse installieren.

-   [Install and upgrade with the version 1606 baseline media for System Center Configuration Manager (Installieren und Upgraden mit dem Baselinemedium der Version 1606 für System Center Configuration Manager)](install-the-ltsb.md) – So installieren Sie einen neuen LTSB-Standort oder upgraden einen System Center 2012 Configuration Manager-Standort auf LTSB.

-   [Upgrade the Long-Term Servicing Branch to the Current Branch (Upgraden von Long-Term Servicing Branch auf Current Branch)](convert-to-current-branch.md) – So konvertieren Sie Ihre LTSB-Installation in eine Current Branch-Installation.

-   [Licensing and branches for System Center Configuration Manager (Lizenzierung und Branches für System Center Configuration Manager)](learn-more-editions.md) – Informationen zur Software Assurance und zu Lizenzanforderungen für System Center Configuration Manager.
-   [Supported Configurations for the Long-Term Servicing Branch of System Center Configuration Manager (Unterstützte Konfigurationen für Long-Term Servicing Branch von System Center Configuration Manager)](supported-configurations-for-ltsb.md) – Die Versionen und Anforderungen für das Betriebssystem und für abhängige Produkte wie z.B. SQL Server, die Sie mit LTSB verwenden können.


Sie können den folgenden Leitfaden verwenden, der Ihnen dabei hilft, zu unterscheiden, für welchen Branch die bestimmte Dokumentation gilt:  
-   Themen mit dem Header *Gilt für: Current Branch* gelten jeweils für Current Branch und Long-Term Servicing Branch (obwohl Teile des Themas womöglich nur für eine neuere Version von Current Branch gelten).

-   Um die Teile eines Themas zu identifizieren, die nicht für LTSB gelten, werden Funktionen und Änderungen, die nach Version 1606 von Current Branch eingeführt wurden, mit dem Wortlaut wie etwa „Ab Version 1610“ identifiziert. Da diese nach Version 1606 von Current Branch eingeführt wurden, sind sie für LTSB nicht verfügbar.

### <a name="similarities-between-the-current-branch-and-the-ltsb"></a>Ähnlichkeiten zwischen Current Branch und LTSB
Da LTSB auf Version 1606 von Current Branch basiert (mit einigen Ausnahmen wie z.B. Intune-Integration und cloudbezogenen Funktionen), sind die meisten Tasks für die Planung der Bereitstellung sowie das Konfigurieren und Verwalten der beiden Branches identisch.

LTSB unterstützt z.B. die gleiche Anzahl von Standorten, Standorttypen, Clients und allgemeine Infrastruktur wie Current Branch. Sie verwenden daher den Leitfaden, den Sie in der Standort- und Hierarchieplanung sowie in den Entwurfsthemen für Current Branch finden. Ähnlich ist es bei Funktionen, die von beiden Branches unterstützt werden, wie z.B. Softwareupdates oder Betriebssystembereitstellung: Verwenden Sie den Leitfaden, den sie in den Abschnitten der Dokumentation von Current Branch finden, die den Vorbehalt enthält, dass Sie über keinen Zugriff auf die neuen Änderungen verfügen, die nach Version 1606 von Current Branch eingeführt wurden.


## <a name="how-to-identify-your-branch-and-version"></a>So identifizieren Sie Ihren Branch und die Version
In den Versionsinformationen für einen Configuration Manager-Standort können Sie auch den Branch ermitteln.

Um die Version Ihres Standorts zu überprüfen, wechseln Sie oben links in der Konsole, wo die **Standortversion** als **5.0.8412.1000** angezeigt wird, zu **Info zu System Center Configuration Manager**.

Um den Branch Ihres Standorts zu ermitteln (als LTSB oder Current Branch), gehen Sie in der Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, und öffnen Sie **Hierarchieeinstellungen**.  Wenn die Möglichkeit besteht, in Current Branch zu konvertieren, und diese Option aktiviert ist, führt der Standort die LTSB-Version aus. Wenn der Standort Current Branch ausführt, ist diese Option ausgegraut.

Informationen zu den verschiedenen Versionen von Configuration Manager finden Sie unter **Baseline- und Updateversionen** im Thema [Updates für System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="exceptions-for-using-the-ltsb"></a>Ausnahmen für die Verwendung von LTSB
### <a name="updates-and-servicing-of-the-ltsb"></a>Updates und Wartung von LTSB
Nur wichtige Sicherheitsupdates werden in LTSB als konsoleninterne Updates verfügbar gemacht.

Informationen zu herkömmlichen Updates für die nachfolgenden Releases von Current Branch sind jedoch in der Konsole sichtbar. Da diese Updates nicht für LTSB verfügbar gemacht wurden, werden sie nicht heruntergeladen und können nicht installiert werden.

Um konsoleninterne Updates für wichtige Sicherheitskorrekturen zu unterstützen, erfordert ein LTSB-Standort die Verwendung des [Dienstverbindungspunkts](/sccm/core/servers/deploy/configure/about-the-service-connection-point). Sie können diese Standortsystemrolle im Offline- oder Onlinemodus konfigurieren, wie für Current Branch. LTSB sammelt und sendet die gleichen Telemetrie- und Nutzungsdaten wie Current Branch.

LTSB unterstützt die Verwendung des Hotfixinstallationsprogramms und des Tools zur Updateregistrierung, so wie für Current Branch dokumentiert.

Allgemeine Informationen zu Updates und zur Wartung finden Sie unter [Updates für System Center Configuration Manager](/sccm/core/servers/manage/updates).

### <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Änderungen für die Standorterweiterung und den Ordner „CD.Latest“
Wenn Sie LTSB ausführen und einen eigenständigen primären Standort durch die Installation eines neuen Standorts der zentralen Verwaltung erweitern, müssen Sie das Setup und die Quelldateien des Baselinemediums von Version 1606 verwenden.  (Für Current Branch führen Sie das Setup aus und verwenden die Quelldatei aus dem Ordner „CD.Latest“.)

Obwohl Sie das Setup für die Standorterweiterung aus dem Ordner „CD.Latest“ nicht ausführen, verwenden Sie den Ordner „CD.Latest“ weiterhin für die Standortwiederherstellung und zum Installieren eines neuen untergeordneten primären Standorts, wenn Ihr erster LTSB-Standort ein Standort der zentralen Verwaltung war.

Weitere Informationen zur Standorterweiterung finden Sie unter [Expand a stand-alone primary site (Erweitern eines eigenständigen primären Standorts)](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site) im Thema [Use the Setup Wizard to install sites (Verwenden des Setup-Assistenten zum Installieren von Standorten)](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).
Weitere Informationen über den Ordner „CD.Latest“ finden Sie unter [Der Ordner „CD.Latest“ für System Center Configuration Manager](/sccm/core/servers/manage/the-cd.latest-folder).



<!--HONumber=Nov16_HO1-->


