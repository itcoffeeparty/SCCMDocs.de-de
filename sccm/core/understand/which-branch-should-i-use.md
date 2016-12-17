---
title: Welcher Branch soll verwendet werden? | System Center Configuration Manager
description: "Hier finden Sie Informationen zu den Unterschieden zwischen den verfügbaren Branches von System Center Configuration Manager."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bbaaf9ed876f7693ea831be7c787dba904197a62
ms.openlocfilehash: 3957e854e980246c410f7de27caed9d66fc4829f


---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Welcher Branch von Configuration Manager soll verwendet werden?

*Gilt für: System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch), (Technical Preview)*


Seit Oktober 2016 ist System Center Configuration Manager in drei Branches verfügbar. Mithilfe dieses Themas können Sie den für sich geeigneten Branch wählen.

## <a name="current-branch-of-system-center-configuration-manager"></a>Current Branch von System Center Configuration Manager
Hierbei handelt es sich um einen lizenzierten Branch zur Verwendung in einer Produktionsumgebung mit der Möglichkeit, die neuesten Features und Funktionen zu erhalten. Diesen Branch sollten Sie verwenden, wenn Sie über eines der folgenden Abonnements verfügen: System Center Datacenter, System Center Standard, System Center Configuration Manager oder entsprechende Abonnementrechte.  Weitere Informationen zu Software Assurance und Lizenzierungsoptionen finden Sie unter [Licensing and branches for System Center Configuration Manager (Lizenzierung und Branches für System Center Configuration Manager)](learn-more-editions.md).


>  [!TIP]
> Current Branch kann auch als Evaluierungsversion installiert werden, für die keine Lizenz erforderlich ist. Die Evaluierungsversion kann 180 Tage verwendet und auf eine lizenzierte Version von Current Branch aktualisiert werden.

Current Branch wird mehrmals pro Jahr mit neuen Features aktualisiert. Jedes Updaterelease wird nach der Veröffentlichung ein (1) Jahr lang unterstützt. Bis zum Ablauf dieses einen Jahres müssen Sie Current Branch auf eine neuere Version aktualisieren. Die Updates auf neuere Versionen sind als konsoleninterne Updates verfügbar.

Um Current Branch als neuen Standort oder als Upgrade von *System Center 2012 Configuration Manager mit Service Pack 2* oder *System Center 2012 R2 Configuration Manager mit Service Pack 1* zu installieren, verwenden Sie die [Baselinemedien](/sccm/core/servers/manage/updates#baseline-and-update-versions) für System Center Configuration Manager, die mit System Center 2016 auf einer DVD ausgeliefert werden oder als Teil eines eigenständigen Releases von System Center Configuration Manager verfügbar sind. Der Zugriff auf diese Medien hängt von Ihrer Lizenzierung von System Center Configuration Manager ab.

Mithilfe der Baselinemedien können Sie auch einen neuen Standort mit einer Evaluierungsversion von Current Branch installieren. Wenn Sie nur eine Evaluierungsversion installieren möchten, erhalten Sie die Software auf der Website [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

>  [!NOTE]
> Baselinemedien werden nur zum Installieren von Standorten für eine neue Configuration Manager-Hierarchie verwendet. Wenn Sie bereits eine Baselineversion wie etwa 1511 installiert haben, aktualisieren Sie Ihre Standorte mithilfe von konsoleninternen Updates auf eine neue Version wie etwa 1606.
>
> Standorte, die mit konsoleninternen Updates aktualisiert werden, sind nach dem Update mit einem neuen Standort identisch, der mithilfe der Baselinemedien installiert wurde.
>
> Weitere Informationen finden Sie unter [Updates for System Center Configuration Manager (Updates für System Center Configuration Manager)](/sccm/core/servers/manage/updates).

**Features von Current Branch:**
- Empfängt [konsoleninterne Updates](/sccm/core/servers/manage/install-in-console-updates), mit denen neue Features zur Verwendung verfügbar gemacht werden.
- Empfängt konsoleninterne Updates, mit denen Sicherheits- und Qualitätsfixes für vorhandene Features bereitgestellt werden.
- Unterstützt bei Bedarf Out-of-Band-Updates. Weitere Informationen finden Sie unter [Use the Update Registration Tool (Verwenden des Tools zur Updateregistrierung)](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) oder unter [Use the Hotfix Installer (Verwenden des Hotfixinstallationsprogramms)](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Kann mit Microsoft Intune und anderen cloudbasierten Diensten und Infrastrukturen zusammenarbeiten.
- Unterstützt die [Migration von Daten](/sccm/core/migration/migrate-data-between-hierarchies) zu und von anderen Configuration Manager-Installationen.
- Unterstützt ein Upgrade von früheren Versionen von Configuration Manager.
- Unterstützt die Installation als Evaluierungsversion, für die später ein Upgrade auf eine vollständig lizenzierte Version durchgeführt werden kann.

Das erste Release von Current Branch war Version 1511. Danach folgen Updates mit den Versionen 1602, 1606 und so weiter. Jede Version wird ein Jahr lang unterstützt, und Microsoft empfiehlt möglichst rasch nach der Veröffentlichung ein Update auf die jeweils neueste Version durchzuführen. Sie können bis zu einem Jahr mit dem Update auf eine neuere Version warten. Sie können ein Update auch überspringen, um die neueste Version zu installieren. Wenn Sie ein Update überspringen und die neueste Version installieren, haben Sie dennoch Zugriff auf alle Features und Verbesserungen aus früheren Versionen, da alle Versionen kumulativ sind.

Weitere Informationen finden Sie unter [Support for Current Branch versions (Unterstützung für Current Branch-Versionen)](/sccm/core/servers/manage/current-branch-versions-supported).

**Update-Optionen:**
- Mit einer aktiven Software Assurance-Lizenz können Sie konsoleninterne Updates für Current Branch-Versionen installieren.  
- Es gibt keine Option zum Konvertieren von Current Branch- zu einer Technical Preview-Version. Technical Previews sind separate Installationen, für die keine Lizenz erforderlich ist.
- Es gibt keine Option zum Konvertieren von Current Branch zu LTSB (Long-Term Servicing Branch). Wenn Sie wechseln möchten, müssen Sie zuerst Current Branch deinstallieren und anschließend die LTSB-Version neu installieren.

##  <a name="long-term-servicing-branch-ltsb-of-system-center-configuration"></a>Long-Term Servicing Branch (LTSB) von System Center Configuration
Hierbei handelt es sich um einen lizenzierten Branch zur Verwendung in Produktionsumgebungen für Configuration Manager-Kunden, die Current Branch verwenden und bei denen die Configuration Manager Software Assurance-Lizenz oder entsprechende Abonnements nach dem 1. Oktober 2016 abgelaufen sind.  Weitere Informationen zu Software Assurance und Lizenzierungsoptionen finden Sie unter [Licensing and branches for System Center Configuration Manager (Lizenzierung und Branches für System Center Configuration Manager)](learn-more-editions.md).

Mit dem LTSB erhalten Sie keine konsoleninternen Updates, mit denen neue Features oder Updates für vorhandene Funktionen bereitgestellt werden. Wichtige Sicherheitsfixes werden jedoch bereitgestellt.

Zur Installation des LTSB als neuen Standort oder als Upgrade von einem unterstützten Configuration Manager 2012-Standort verwenden Sie die [Baselinemedien](/sccm/core/servers/manage/updates#baseline-and-update-versions) von Version 1606, die Sie mit System Center 2016 oder System Center Configuration Manager (Current Branch und Long-Term Servicing Branch 1606) als DVD erhalten. Mit den Baselinemedien können Sie einen neuen Standort, an dem Version 1606 von Current Branch ausgeführt wird, oder einen neuen Standort, an dem Long-Term Servicing Branch ausgeführt wird, installieren.

> [!TIP]  
> Weitere Informationen zu System Center 2016 finden Sie in der [Dokumentation zu System Center 2016](https://technet.microsoft.com/system-center-docs/System-Center-2016). In dieser Dokumentation wird auch beschrieben, wie Sie System Center 2016 erhalten, eine Lösung, für die Sie einen Microsoft-Lizenzvertrag oder entsprechende Rechte benötigen.  Sie können auch eine Evaluierungsversion von System Center 2016 erhalten, die Sie im [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview) herunterladen können.

**Features des LTSB:**
-   Empfängt konsoleninterne Updates, mit denen wichtige Sicherheitsfixes bereitgestellt werden.
- Stellt eine Installationsoption bereit, wenn der Software Assurance-Vertrag oder entsprechende Rechte für Configuration Manager abgelaufen sind.
- Unterstützt ein Upgrade (Konvertierung) auf Current Branch, wenn Sie über einen aktuellen Software Assurance-Vertrag oder entsprechende Rechte für Configuration Manager verfügen.

**Einschränkungen:**  
Der LTSB basiert auf der Current Branch-Version 1606 und weist die folgenden Einschränkungen auf:
- Der LTSB wird nach der allgemeinen Verfügbarkeit (Oktober 2016) 10 Jahre lang mit wichtigen Sicherheitsupdates unterstützt. Danach läuft die Unterstützung für diesen Branch ab.  Weitere Informationen zum Supportlebenszyklus finden Sie unter [Microsoft Lifecycle-Richtlinie](https://support.microsoft.com/en-us/lifecycle).
- Unterstützt eine eingeschränkte feste Liste mit Server- und Clientbetriebssystemen und entsprechenden Technologien wie SQL Server-Versionen.  Weitere Informationen dazu, was von diesem Branch unterstützt wird, finden Sie unter [Supported Configurations for the Long-Term Servicing Branch (Unterstützte Konfigurationen für Long-Term Servicing Branch)](supported-configurations-for-ltsb.md).
- Erhält keine Updates für neue Features.
- Unterstützt nicht das Hinzufügen eines Microsoft Intune-Abonnements, das den Gebrauch von Folgendem verhindert:
  - Intune in einer Konfiguration mit hybrider Verwaltung mobiler Geräte
 - Lokale Verwaltung mobiler Geräte
-   Unterstützt nicht die Verwendung des Windows 10-Wartungsdashboards sowie Wartungspläne und unterstützt nicht Current Branch (CB) von Windows 10 und Current Branch for Business (CBB)
- Zukünftige Releases von LTSB für Windows 10 und Windows Server werden nicht unterstützt.
-   Keine Unterstützung für Asset Intelligence
-   Keine Unterstützung für cloudbasierte Verteilungspunkte
-   Keine Unterstützung für den Support für Exchange Online als Exchange-Connector
-   Unterstützt keine Features der Vorabversion.



**Update-Optionen:**
- Es ist möglich, die LTSB-Installation in eine Current Branch-Installation zu konvertieren. Die Konvertierung zu Current Branch wird vor oder nach Ablauf der Unterstützung für LTSB unterstützt.

  Für die Konvertierung ist ein aktiver Software Assurance-Vertrag mit Microsoft erforderlich.  Weitere Informationen finden Sie unter den folgenden Links:
  - [Upgrade the Long-Term Servicing Branch to the Current Branch (Upgrade von Long-Term Servicing Branch auf Current Branch)](convert-to-current-branch.md)
  - [Lizenzierung und Branches für System Center Configuration Manager](learn-more-editions.md)
  - [Baseline and update versions (Baseline- und Updateversionen)](/sccm/core/servers/manage/updates#baseline-and-update-versions) in [Updates for Configuration Manager (Updates für Configuration Manager)](/sccm/core/servers/manage/updates)
- Es gibt keine Option zum Konvertieren von der LTSB- zu einer Technical Preview-Version. Technical Previews sind separate Installationen, für die keine Lizenz erforderlich ist.
-   Für eine Evaluierungsversion von Current Branch kann kein Upgrade auf eine LTSB-Installation durchgeführt werden.


## <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview für System Center Configuration Manager
Die Technical Preview-Version ist für die Verwendung in einer Laborumgebung vorgesehen, in der Sie die neuesten Features für Configuration Manager kennenlernen und ausprobieren können. In einer Produktionsumgebung wird die Technical Preview-Version nicht unterstützt. Für diese Version ist kein Software Assurance-Lizenzvertrag erforderlich.

Wenn Sie einen neuen Standort installieren möchten, an dem die Technical Preview ausgeführt wird, verwenden Sie die neuesten [Baselinemedien für die System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). Nach der Installation der Technical Preview sind jeden Monat neue Versionen als konsoleninterne Updates verfügbar.

**Features der Technical Preview:**
-  Basiert auf aktuellen Baselineversionen von Current Branch.
-  Empfängt konsoleninterne Updates, mit denen die Installation auf die neueste Technical Preview-Version aktualisiert wird.
-  Enthält neu entwickelte Features, für die sich unsere Entwickler ein Feedback wünschen.
-  Empfängt Updates, die nur für die Technical Preview gelten.

**Einschränkungen:**
-  [Eingeschränkte Unterstützung](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), die nur einen primären Standort mit bis zu 10 Clients umfasst.  
-  Ein Upgrade auf eine Current Branch- oder LTSB-Version ist nicht möglich.
-  Die Migration zum Importieren oder Exportieren von Daten in oder von einer anderen Configuration Manager-Installation wird nicht unterstützt.
-  Ein Upgrade von einer früheren Version von Configuration Manager wird nicht unterstützt.
-  Die Installation als Evaluierungsversion wird nicht unterstützt.

Features, die mit einer Technical Preview eingeführt werden, werden später häufig in Current Branch ebenfalls bereitgestellt.  Jede neue Technical Preview-Version beinhaltet die Features aus früheren Technical Preview-Versionen, auch wenn diese Features dann auch in Current Branch enthalten sind.

Weitere Informationen finden Sie unter [Technical Preview for System Center Configuration Manager (Technical Preview für System Center Configuration Manager)](/sccm/core/get-started/technical-preview).

**Update-Optionen:**
-   Für eine neue Technical Preview-Version kann jedes konsoleninterne Update installiert werden.
-   Es gibt keine Option zum Konvertieren von einer Technical Preview-Version zu Current Branch- oder LTSB-Version.



<!--HONumber=Nov16_HO1-->

