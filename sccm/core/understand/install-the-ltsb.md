---
title: "Installieren eines Standorts mit dem 1606-Baselinemedium | für System Center Configuration Manager"
description: "Erfahren Sie mehr über das 1606-Baselinemedium zum Installieren oder Upgraden von Standorten für System Center Configuration Manager."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e97fbcdc21022e98b4cbdb198273dfe544a561f
ms.openlocfilehash: 3df46a00f2208ffa687c8c99ce610266e206eef0


---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media-for-system-center-configuration-manager"></a>Installieren und Upgraden mit dem Baselinemedium von Version 1606 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*

In diesem Thema erfahren Sie, wie Sie das Configuration Manager-Setup ausführen, wenn Sie das Baselinemedium des Releases 1606 des Microsoft System Center 2016- oder des System Center Configuration Manager-Release (Current Branch und Long-Term Servicing Branch 1606) verwenden. Sie können das Installationsmedium zur Installation eines neuen Standorts verwenden oder ein Upgrade von System Center 2012 Configuration Manager mit Service Pack 2 oder auf System Center 2012 R2 Configuration Manager mit Service Pack 1 ausführen. Während des Setups können Sie auswählen, ob Sie Current Branch oder Long-Term Servicing Branch (LTSB) installieren möchten.

Wenn Sie das Baselinemedium von Version 1606 verwenden, ist der Standort, den Sie installieren (oder auf den Sie aktualisieren):
- **Ein Current Branch-Standort**, der einem Standort entspricht, der anfänglich mit dem 1511-Baselinemedium installiert wurde und später auf Version 1606 und das entsprechende 1606-Hotfixrollup „KB3186654“ aktualisiert wurde.
-   **Ein LTSB-Standort**, der dem Current Branch-Standort entspricht, der die Version 1606 und das entsprechende 1606-Hotfixrollup „KB3186654“ ausführt (das Baselinemedium enthält bereits das Hotfixrollup).  Allerdings unterstützt LTSB nicht alle Features oder Funktionen, die in Current Branch verfügbar sind, wie im Artikel [Introduction to the Long-Term Servicing Branch of System Center Configuration Manager (Einführung in Long-Term Servicing Branch von System Center Configuration Manager)](introduction-to-the-ltsb.md) beschrieben.

Wenn Sie nicht mit den verschiedenen Branches von System Center Configuration Manager vertraut sind, finden Sie weitere Informationen unter [Which branch of Configuration Manager should I use (Welchen Configuration Manager-Branch sollte ich verwenden?)](which-branch-should-i-use.md).


## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Änderungen an dem Setup mit dem 1606-Baselinemedium
Das 1606-Baselinemedium führt die folgenden Neuerungen für das Configuration Manager-Setup ein.

### <a name="branch-and-edition"></a>Branch und Edition
Wenn Sie das Setup ausführen, wird Ihnen jetzt eine Lizenzierungsseite angezeigt, in dem Sie den Branch von Configuration Manager auswählen können, den Sie installieren möchten. Sie können Current Branch oder LTSB als lizenzierte Installation auswählen. Alternativ können Sie sich für eine Evaluierungsversion von Current Branch als nicht lizenzierte Installation entscheiden.

Weitere Informationen finden Sie unter [Licensing and branches for System Center Configuration Manager (Lizenzierung und Branches für System Center Configuration Manager)](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Ablauf der Software Assurance
Während der Installation haben Sie die Option, das **Software Assurance-Ablaufdatum** einzugeben. Dies ist ein optionaler Wert, den Sie als praktische Erinnerung angeben können.

> [!NOTE]
> Das angegebene Ablaufdatum wird von Microsoft nicht überprüft. Microsoft verwendet das von Ihnen angegebene Datum ebenso wenig, um die Lizenz zu überprüfen.  Stattdessen können Sie das Ablaufdatum angeben, um daran erinnert zu werden. Dies ist hilfreich, da Configuration Manager regelmäßig überprüft, ob neue Softwareupdates online angeboten werden, und Ihr Software Assurance-Lizenzstatus sollte aktuell sein, damit Sie von diesen zusätzlichen Updates profitieren können.    

- Geben Sie den Wert auf der Seite **Product Key** des Setup-Assistenten an, wenn Sie das Setup vom Baselinemedium von System Center Configuration Manager-Version 1606 ausführen
- Sie können das Datum auch auf Registerkarte **Lizenzierung** der **Eigenschaften von Hierarchieeinstellungen** in der Configuration Manager-Konsole angeben.

Weitere Informationen finden Sie unter *Software Assurance agreements (Software Assurance-Verträge)* in [Licensing and branches for System Center Configuration Manager (Lizenzierung und Branches für System Center Configuration Manager)](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Zusätzliche Konfigurationen vor dem Upgrade
Vor dem Starten eines Upgrades von System Center 2012 Configuration Manager auf LTSB, müssen Sie für die Prüfliste die folgenden zusätzlichen Schritte ausführen.  
Deinstallieren Sie die nicht von LTSB unterstützten Standortsystemrollen:
- Asset Intelligence-Synchronisierungspunkt
- Microsoft Intune-Connector
- Cloudbasierte Verteilungspunkte

Weitere Informationen finden Sie unter [Upgrade auf System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).


### <a name="new-scripted-install-options"></a>Neue Skriptinstallationsoptionen
Das Baselinemedium von Version 1606 unterstützt einen neuen, unbeaufsichtigten Skriptdateischlüssel für skriptgesteuerte Installationen eines neuen Standorts der obersten Ebene. Dies gilt sowohl für die Installation eines neuen, eigenständigen primären Standorts als auch eines Standorts der zentralen Verwaltung im Rahmen eines Standorterweiterungsszenarios.

Bei Verwendung eines unbeaufsichtigten Skripts für die Installation eines Lizenzbranches müssen Sie den folgenden Abschnitt, Schlüsselnamen und die Werte für den Abschnitt „Optionen“ Ihres Skripts hinzufügen (Sie müssen diese Werte nicht verwenden, um die Installation einer Evaluierungsedition von Current Branch):  

 **SABranchOptions**
-   **Schlüsselname: SSActive**
  - Werte: 0 oder 1  
  - Details: 0 installiert eine nicht lizenzierte Evaluierungsversion von Current Branch, und 1 installiert die lizenzierte Version.   

- **CurrentBranch**
  - Werte: 0 oder 1  
  - Details: 0 installiert Long-Term Servicing Branch, und 1 installiert Current Branch.  

Um eine lizenzierte Current Branch-Edition zu erstellen, würden Sie z.B. Folgendes verwenden:

  **Schlüsselname: SABranchOptions**
   -    **SSActive = 1**
   - **CurrentBranch = 1**
 

> [!IMPORTANT]  
> **SABranchOptions** funktioniert nur mit dem Setup vom Baselinemedium. Es funktioniert nicht, wenn Sie das Setup aus dem Ordner „CD.Latest“ ausführen, den Sie zuvor mithilfe des Baselinemediums von Version 1606 installiert haben.
>
> **SABranchOptions** funktioniert nicht für skriptgesteuerte Upgrades von System Center 2012 Configuration Manager und installiert immer Current Branch.

Weitere Informationen finden Sie unter [Install System Center Configuration Manager consoles (Installieren von System Center Configuration Manager-Konsolen)](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites).


## <a name="install-a-new-site"></a>Installieren eines neuen Standorts
Wenn Sie das 1606-Baselinemedium verwenden, um einen neuen Standort für jeden Branch zu installieren, verwenden Sie die Standortplanung, die Vorbereitung und die Installationsprozedur, die im Thema [Installieren von System Center Configuration Manager-Standorten](/sccm/core/servers/deploy/install/installing-sites) dokumentiert sind, zusätzlich zu den folgenden Überlegungen zum Setup:

- Während des Setups müssen Sie den Configuration Manager-Branch auswählen, den Sie installieren möchten, und Sie können Details zu Ihrem Software Assurance-Vertrag angeben.
-   Neue Skriptinstallationsoptionen

## <a name="expand-a-stand-alone-primary-site"></a>Erweitern eines eigenständigen primären Standorts
Sie können einen eigenständigen primären Standort erweitern, auf dem LTSB ausgeführt wird.  Der Prozess unterscheidet sich nicht von dem, der für einen Current Branch-Standort verwendet wird, jedoch mit einer Einschränkung:

- Bei der Installation des neuen Standorts der zentralen Verwaltung müssen Sie das Setup vom ursprünglichen Quellmedium verwenden, das Sie zum Installieren des LTSB-Standorts verwendet haben. (Die Ausführung des Setups aus dem Ordner „CD.Latest“ wird für dieses Szenario nicht unterstützt).

Weitere Informationen zur Standorterweiterung finden Sie unter *Expand a stand-alone primary site (Erweitern eines eigenständigen primären Standorts)* im Thema [Use the Setup Wizard to install System Center Configuration Manager sites (Verwenden des Setup-Assistenten zum Installieren von System Center Configuration Manager-Standorten)](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Upgrade von System Center 2012 Configuration Manager
Bei einem Upgrade von System Center 2012 Configuration Manager sollten Sie die Standortplanung, die Vorbereitung und die Prozeduren wie im Thema [Upgrade auf System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) beschrieben verwenden, jedoch mit den folgenden Änderungen:

**Upgrade auf Current Branch:**
- Während des Setups müssen Sie Current Branch auswählen, den Sie installieren möchten, und Sie können Details zu Ihrem Software Assurance-Vertrag angeben.
-   Neue Skriptinstallationsoptionen

**Upgrade auf LTSB:**  
- Zusätzliche Schritte zu der vor dem Upgrade durchzugehenden Prüfliste
- Während des Setups müssen Sie LTSB auswählen, den Sie installieren möchten, und Sie können Details zu Ihrem Software Assurance-Vertrag angeben.
- Sie können ausschließlich Standorte upgraden, an denen System Center 2012 Configuration Manager mit Service Pack 2 oder System Center 2012 R2 Configuration Manager mit Service Pack 1 ausgeführt wird.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Pfade für direkte Upgrades für das 1606-Baselinemedium
Sie können das 1606-Baselinemedium verwenden, um folgende Versionen auf eine lizenzierte Version von System Center Configuration Manager upzugraden:
- System Center 2012 Configuration Manager mit Service Pack 2
- System Center 2012 R2 Configuration Manager mit Service Pack 1

Sie können diese Medien auch dazu verwenden, um eine nicht lizenzierte Evaluierungsversion von Current Branch auf eine vollständig lizenzierte Version von Current Branch upzugraden.

Das Medium unterstützt kein Upgrade von:
- Andere Versionen von System Center 2012 Configuration Manager
- Configuration Manager 2007 oder früher
- Eine Release Candidate-Install von System Center Configuration Manager

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Informationen zu dem Ordner „CD.Latest“ und LTSB
Die sind die Einschränkungen der Verwendung des Mediums, das Configuration Manager im Ordner „CD.Latest“ auf dem Standortserver erstellt. Diese gelten für Websites, auf denen LTSB ausgeführt wird: Medien im Ordner „CD.Latest“ werden unterstützt für:
- Standortwiederherstellung
- Standortwartung
- Installieren zusätzlicher, untergeordneter primärer Standorte

Medien werden im Ordner „CD.Latest“ nicht unterstützt für:  
- Die Installation eines Standorts der zentralen Verwaltung im Rahmen eines Szenarios zur Standorterweiterung.

Weitere Informationen finden Sie unter [Der Ordner „CD.Latest“ für System Center Configuration Manager](/sccm/core/servers/manage/the-cd.latest-folder).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Sicherung, Wiederherstellung und Standartwartung für LTSB
Verwenden Sie zum Sichern, Wiederherstellen oder Ausführen der Wartung eines LTSB-Standorts den Leitfaden und die Prozeduren in [Sicherung und Wiederherstellung für System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  

Verwenden Sie das Configuration Manager-Setup im Ordner „CD.Latest“ der Sicherung Ihres LTSB-Standorts.



<!--HONumber=Nov16_HO1-->

