---
title: Informationen zu Security Content Automation Protocol-Erweiterungen (SCAP)
titleSuffix: System Center Configuration Manager
description: Informationen zu Security Content Automation Protocol-Erweiterungen (SCAP)
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: fc986e2175583124377ccb7c080df4b219ea8df0
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>Informationen zu Security Content Automation Protocol-Erweiterungen (SCAP)

*Gilt für: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Dieses Feature wurde erstmals in Technical Preview Version 1803 als [Vorabfeature](/sccm/core/servers/manage/pre-release-features) eingeführt. Diese Vorabversion der SCAP-Erweiterungen kann unter allen derzeit unterstützten Versionen von Configuration Manager Current Branch und LTSB 1606 installiert werden. Die Installationsdatei befindet sich unter cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi ab Technical Preview Version 1803. 

Mithilfe der SCAP-Erweiterungen für Microsoft System Center Configuration Manager können Sie Ihre Netzwerkumgebung in Hinsicht auf Konformität mit SCAP (Security Content Automation Protocol) analysieren und bewerten. SCAP wird vom US-amerikanischen National Institute of Standards and Technology (NIST) definiert und verwaltet.

Die SCAP-Erweiterungen für Microsoft System Center Configuration Manager verwenden das Feature für Konformitätseinstellungen in Microsoft System Center Configuration Manager, um die Computer in Ihrer Umgebung zu überprüfen und anschließend den Grad der Konformität mit dem USGCB-Standard (United States Government Configuration Baseline) zu dokumentieren.

Durch die Erweiterungen kann Configuration Manager SCAP-Datenströme nutzen, Systeme in Hinsicht auf ihre Konformität bewerten und Berichtsergebnisse im SCAP-Format generieren. Nun kann Ihre Organisation auf Grundlage der vorhandenen Configuration Manager-Infrastruktur sicherstellen, dass die von Ihnen verwalteten Computer diesen Kompatibilitätsanforderungen entsprechen und die für NIST (National Institute of Standards und Technology) und das US-amerikanische Office of Management and Budget (OMB) erforderlichen USGCB-Berichte generieren.

Dieser Leitfaden enthält Informationen zum Installieren, Konfigurieren und Ausführen der SCAP-Erweiterungen in der System Center Configuration Manager-Infrastruktur.



# <a name="what39s-new-in-scap-extensions-prerelease-for-microsoft-system-center-configuration-manager"></a>Neuerungen in der Vorabversion der SCAP-Erweiterungen für Microsoft System Center Configuration Manager

In diesem Abschnitt lernen Sie die Neuerungen der aktuellen Version kennen.

Vorabversion der SCAP-Erweiterungen für System Center Configuration Manager:

- Enthält eine Erweiterung der Configuration Manager-Konsole, die die Konvertierung von SCAP-Inhalten in Baselines für die Konformitätseinstellungen für System Center Configuration Manager Current Branch vollständig unterstützt
- Unterstützt SCAP, Version 1.2, und ist abwärtskompatibel mit SCAP, Version 1.1 und 1.0.


  - Unterstützt das XCCDF-Format (Extensible Configuration Checklist Description), Version 1.2.
  - Unterstützt OVAL-Versionen (Open Vulnerability and Assessment Language) bis 5.10.
  - Unterstützt das Generieren von ARF-Berichten (Asset Reporting Format), Version 1.1.
  - Unterstützt CPE 2.3 (Common Platform Enumeration)
  - Unterstützt CVE (Common Vulnerabilities and Exposures)
  - Unterstützt CCE Version 5 (Common Configuration Enumeration)
  - Unterstützt USGCB Internet Explorer 8, USGCB Windows 7 und USGCB Windows 7-Firewall.

- Enthält einen UI-Assistenten, um SCAP 1.2/1.1/1.0 und OVAL-Inhalte für die Konvertierung zu Konfigurationsbaselines zu importieren.


  - Ermöglicht die Auswahl von SCAP-Quelldatenströme und XCCDF-Benchmarks und -Profile für die Konvertierung.

- Enthält einen UI-Assistenten, um das Konfigurationsauswertungsergebnis in XML-Berichte im SCAP-Format zu exportieren.


  - Zeigt Quelldatei, SCAP-Datenstrom, XCCDF-Benchmark und XCCDF-Profil an, das verwendet wird, um die Baseline zu generieren.
  - Unterstützt das Generieren des Cyberscope LASR-Berichts (Lightweight Asset Summary Results).

- Unterstützt das Generieren von SCAP-Berichten basierend auf der Bereitstellung der Konfigurationsbaseline. Enthält ein neues Dashboard, mit dem die Clientkompatibilität und die Kompatibilität der XCCDF-Regel visualisiert werden. Das Dashboard unterstützt Drillthroughs für ausführlichere Berichte, in denen Sie suchen und filtern können.
- Verbessert die Leistung von mehreren Arten von Konfigurationselementen, die aus OVAL-Tests konvertiert wurden. Dies ermögliche eine schnellere Auswertung.

- Behebt mehrere Probleme, die in Inhalten von Windows 10 DISA v1r3 gefunden wurden.

# <a name="scap-extensions-for-microsoft-system-center-configuration-manager-deployment-process"></a>SCAP-Erweiterungen für den Bereitstellungsprozess von Microsoft System Center Configuration Manager

In dieser Anleitung wird beschrieben, wie Sie mithilfe der SCAP-Erweiterungen für Microsoft System Center Configuration Manager die SCAP-Konformität analysieren, bewerten und Berichte dazu erstellen. Es folgt eine kurze Zusammenfassung der auszuführenden Schritte:

- Vorbereiten der erforderlichen Infrastruktur zur Nutzung der Erweiterungen
- Installieren und Konfigurieren der SCAP-Erweiterungen für Microsoft System Center Configuration Manager
- Herunterladen, Installieren und Konfigurieren der SCAP-Datenstromdateien aus der [National Vulnerability Database](http://nvd.nist.gov) (NVD).
- Konvertieren und Importieren Sie die SCAP-Datenstromdateien direkt in eine Baseline der Kompatibilitätseinstellungen in System Center Configuration Manager. Verwenden Sie dazu den Importassistenten **oder** eine CAB-Datei mit dem Befehlszeilentool „Microsoft.Sces.ScapToDcm.exe“.
- Exportieren Sie die Kompatibilitätsergebnisse im SCAP-Format. Verwenden Sie dazu den Exportassistenten oder das Befehlszeilentool „Microsoft.Sces.DcmToScap.exe“.

# <a name="terms"></a>Bestimmungen

**OVAL-ID:** Ein Bezeichner für eine bestimmte OVAL-Definition, die dem Format für OVAL-IDs entspricht.

**SCAP-Datenstromdateiergebnis:** Eine Zusammenstellung von SCAP-Komponenten, die zusammen mit den Zuordnungen von Verweisen zwischen SCAP-Komponenten die Ausgabeinhalte (Ergebnis) enthalten.

**SCAP-Quelldatenstrom:** Eine Zusammenstellung von SCAP-Komponenten, die zusammen mit den Zuordnungen von Verweisen zwischen SCAP-Komponenten die Eingabeinhalte (Quelle) enthalten.

# <a name="prepare-the-prerequisite-infrastructure"></a>Vorbereiten der erforderlichen Infrastruktur

Stellen Sie sicher, dass die folgenden Software- und Hardwareanforderungen erfüllt sind, um die SCAP-Erweiterungen für Microsoft System Center Configuration Manager nutzen zu können.

## <a name="software-requirements"></a>Softwareanforderungen

Zum Installieren, Konfigurieren und Ausführen der SCAP-Erweiterungen für Microsoft System Center Configuration Manager benötigen Sie einen Computer mit folgender Software:

- Eine [unterstützte Version](/sccm/core/servers/manage/current-branch-versions-supported) der Konsole von System Center Configuration Manager (Current Branch).
- Ein Betriebssystem, das mit der System Center Configuration Manager-Konsole kompatibel ist. Eine Liste kompatibler Betriebssysteme finden Sie unter [Supported operating systems for System Center Configuration Manager consoles (Unterstützte Betriebssysteme für System Center Configuration Manager-Konsolen)](/sccm/core/plan-design/configs/supported-operating-systems-consoles).

Zusätzlich zum Computer, der SCAP-Erweiterungen ausführt, benötigen Sie außerdem die folgenden Elemente:

- Eine System Center Configuration Manager Current Branch-Infrastruktur. Weitere Informationen zu den Anforderungen einer Bereitstellung von Configuration Manager finden Sie im Artikel [Supported Configurations for Configuration Manager (Unterstützte Konfigurationen für Configuration Manager)](/sccm/core/plan-design/configs/supported-configurations).

Die Computer, die Sie auf SCAP-Konformität untersuchen möchten, benötigen die folgende Software und Konfiguration:

- Die Komponente "Kompatibilitäts- und Einstellungsverwaltung" muss auf dem Configuration Manager-Client aktiviert sein.
- Windows PowerShell 2.0 oder höher.
- Die Ausführungsrichtlinie für Configuration Manager-PowerShell muss auf **Umgehen** festgelegt sein. Weitere Informationen finden Sie im Artikel [PowerShell-Ausführungsrichtlinie](/sccm/core/clients/deploy/about-client-settings#computer-agent).
- Eines der folgenden Betriebssysteme
  - Release-Version von Windows 7 oder SP 1, 32 Bit oder 64 Bit
  - Windows 10 32-Bit oder 64-Bit
  - Windows Server 2012 R2

## <a name="hardware-requirements"></a>Hardwareanforderungen

Die Mindestsystemanforderungen finden Sie hier:

[Planen der Hardwarekonfigurationen für Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)



## <a name="accessibility-features"></a>Barrierefreiheitsfeatures

Zu den SCAP-Erweiterungen für System Center Configuration Manager gehören Windows-Befehlszeilentools, die die Barrierefreiheitsfeatures und Tools von Windows nutzen können.

- Befehlszeilenparameter sind in diesem Benutzerhandbuch für „Microsoft.Sces.ScapToDcm.exe“ und „Microsoft.Sces.DcmToScap.exe“ dokumentiert.
- -help und -? wird die Toolverwendung auf dem Bildschirm ausgegeben, wodurch sie für die Bildschirmsprachausgabe und andere Hilfstechnologien zur Verfügung steht.
- Windows [Barrierefreiheit](http://windows.microsoft.com/windows/help/accessibility)

Die SCAP-Erweiterungen verwenden auch Features in System Center Configuration Manager.  Configuration Manager enthält Features, durch die das Produkt für Menschen mit Behinderungen zugänglich gemacht wird.

- [Barrierefreiheitsfeatures in System Center Configuration Manager](/sccm/core/understand/accessibility-features)

Allgemeine Informationen zu Barrierefreiheitsprodukten und -diensten von Microsoft finden Sie auf der [Microsoft-Website zur Barrierefreiheit](http://go.microsoft.com/fwlink/p/?LinkId=9212).

## <a name="next-step"></a>Nächste Schritte
> [!div class="nextstepaction"]
> [Installieren und Konfigurieren der SCAP-Erweiterungen](/sccm/compliance/plan-design/scap/install-configure-scap)
