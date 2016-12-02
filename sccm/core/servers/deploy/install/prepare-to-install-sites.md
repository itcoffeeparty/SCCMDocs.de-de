---
title: Vorbereiten auf die Installation von Standorten | System Center Configuration Manager
description: Lesen Sie diese Angaben, um Zeit bei der Installation mehrerer Standorte zu sparen und Fehler zu vermeiden.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6f240f1da4561c05bee974b78f43bfcdba591df6

---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>Vorbereiten auf die Installation von System Center Configuration Manager-Standorten

*Gilt für: System Center Configuration Manager (Current Branch)*

Zur Vorbereitung auf eine erfolgreiche Bereitstellung von System Center Configuration Manager-Standorten machen Sie sich mit den Details in diesem Artikel vertraut. Durch diese Schritte können Sie während der Installation von mehreren Standorten Zeit sparen und Fehler vermeiden, nach denen möglicherweise einer oder mehrere Standorte neu installiert werden müssen.
 > [!TIP]
 >  Die folgenden Szenarios sind ähnlich, aber anders als die Installation eines Standorts von System Center Configuration Manager (Current Branch):
 > -  **Upgrade**: Installieren von System Center Configuration Manager zum **Upgraden** von System Center 2012 Configuration Manager finden Sie unter [Upgraden auf System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)
 > -  **Aktualisieren**: Verwenden von konsoleninternen Updates zum Installieren einer neuen **Updateversion** für einen vorhandenen System Center Configuration Manager-Standort finden Sie unter [Updates für System Center Configuration Manager](../../../../core/servers/manage/updates.md)
 > -  **Migrieren**: Informationen zur **Datenmigration** aus einer anderen Configuration Manager-Hierarchie zu Ihrer aktuellen System Center Configuration Manager-Hierarchie finden Sie unter [Planen der Migration zu System Center Configuration Manager](../../../../core/migration/planning-for-migration.md)



## <a name="a-namebkmkoptionsa-options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a> Optionen für die Installation verschiedener Standorttypen
Wenn Sie einen neuen Configuration Manager installieren, hängt die Version der Quelldateien, die Sie verwenden können, von der Version der Standorte ab, die sich bereits in der Hierarchie befinden (falls vorhanden), und die verfügbaren Installationsmethoden hängen vom jeweiligen Standorttyp ab, den Sie installieren möchten.  

Stellen Sie vor der Installation von Standorten sicher, dass Sie Ihre Hierarchie geplant haben und den Standorttyp, den Sie installieren möchten, kennen. Weitere Informationen finden Sie unter [Entwerfen einer Hierarchie von Standorten](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### <a name="first-site"></a>Erster Standort
Der erste Standort, den Sie für eine Hierarchie installieren, ist entweder ein eigenständiger primärer Standort oder ein Standort der zentralen Verwaltung.

**Installieren von Medien**: Zur Installation eines Standorts der zentralen Verwaltung oder eines eigenständigen primären Standorts als ersten Standort in einer neuen Hierarchie benötigen Sie eine [Baselineversion](../../../../core/servers/manage/updates.md#bkmk_Baselines) von Configuration Manager. Installieren Sie den ersten Standort einer neuen Hierarchie nicht mit aktualisierten Quelldateien aus dem [Ordner CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) eines beliebigen Standorts.

**Installationsmethode**: Sie können entweder beide Standorttypen mithilfe des [Configuration Manager-Setup-Assistenten](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) installieren, oder Sie können ein Skript für eine [Installation über die Befehlszeile mithilfe von Skripts](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md) konfigurieren.


### <a name="additional-sites"></a>Zusätzliche Standorte
Nachdem der erste Standort installiert ist, können Sie zusätzliche Standorte zu einem beliebigen Zeitpunkt hinzufügen. Die folgenden Optionen sind vorhanden, um zusätzliche Standorte hinzuzufügen (bis zu den [unterstützten Höchstgrenzen](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

Vorhandener Standort          |Zusätzliche Standorte, die Sie installieren können  
---------                   |---------
Standort der zentralen Verwaltung |   Installieren eines untergeordneten primären Standorts            
Untergeordneter primärer Standort          |   Installieren eines sekundären Standorts        
Eigenständiger primärer Standort    |   Installieren eines sekundären Standorts<br />Erweitern des primären Standorts, wodurch der eigenständige primäre Standort in einen untergeordneten primären Standort konvertiert wird

**Installieren von Medien**: Wenn Sie einen Standort der zentralen Verwaltung installieren, um auf einem eigenständigen primären Standort zu erweitern, oder einen neuen untergeordneten primären Standort in einer vorhandenen Hierarchie installieren, benötigen Sie Installationsmedien (Quelldateien), die mit der Version des oder der vorhandenen Standorte übereinstimmen.
> [!IMPORTANT]
> Wenn Sie konsoleninterne Aktualisierungen installiert haben, die die Versionen der zuvor installierten Standorte geändert haben, verwenden Sie anstelle der Originalinstallationsmedien die neusten Quelldateien aus dem [Ordner CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) eines aktualisierten Standorts.  Configuration Manager erfordert die Verwendung von Quelldateien, die mit der Version des bestehenden Standorts übereinstimmen, mit dem der neue Standort eine Verbindung herstellt.


Ein sekundärer Standort muss in der Configuration Manager-Konsole installiert werden und wird daher immer mithilfe von Quelldateien aus dem übergeordneten primären Standort installiert.

**Installationsmethode**: Die Methode, die Sie zum Installieren zusätzlicher Standorte verwenden, hängt vom Typ des Standorts ab, den Sie installieren möchten.
-   **Hinzufügen eines Standorts der zentralen Verwaltung**:  
Sie können den Configuration Manager-Setup-Assistenten oder eine skriptgesteuerte Befehlszeile verwenden, um den neuen Standort der zentralen Verwaltung als übergeordneten Standort für Ihren vorhandenen eigenständigen primären Standort zu installieren.  Weitere Informationen finden Sie unter [Erweitern eines eigenständigen primären Standorts](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
-   **Hinzufügen eines untergeordneten primären Standorts**:  
Sie können den Configuration Manager-Setup-Assistenten oder eine Befehlszeileninstallation verwenden, um einen untergeordneten primären Standort unterhalb eines Standorts der zentralen Verwaltung hinzuzufügen.
-   **Hinzufügen eines sekundären Standortes**:   
Sie verwenden die Configuration Manager-Konsole zur Installation eines sekundären Standorts als untergeordneten Standort unter einem primären Standort. Andere Methoden werden für sekundäre Standorte nicht unterstützt.



## <a name="a-namebkmktasksa-common-tasks-to-complete-before-starting-an-install"></a><a name="bkmk_tasks"></a> Gängige vor dem Starten einer Installation auszuführende Tasks
-   Vertrautmachen mit der Topologie der Hierarchie, die Sie für Ihre Bereitstellung verwenden    
     (siehe [Entwerfen einer Hierarchie von Standorten für System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md))  

-   Vorbereiten und Konfigurieren von einzelnen Servern zum Erfüllen der Voraussetzungen und unterstützte Konfigurationen für die Verwendung mit Configuration Manager (siehe [Voraussetzungen für Standorte und Standortsysteme](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md))  

-   Installation und Konfiguration von SQL Server zum Hosten der Standortdatenbank (siehe    
    [Unterstützung für SQL Server-Versionen für System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md))  

-   Vorbereiten der Netzwerkumgebung zur Unterstützung von Configuration Manager (siehe [Configure firewalls, ports, and domains to prepare for Configuration Manager (Konfigurieren von Firewalls, Ports und Domänen als Vorbereitung für Configuration Manager)](/sccm/core/plan-design/network/configure-firewalls-ports-domains))  

-   Wenn Sie eine PKI verwenden, bereiten Sie Ihre Infrastruktur und Zertifikate vor (siehe [PKI-Zertifikatanforderungen für Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md))

-   Installieren Sie die neuesten Sicherheitsupdates auf Computern, die Sie als Standortserver oder Standortsystemserver verwenden, und starten Sie diese wenn nötig neu.



## <a name="a-namebkmksitecodesa-about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a> Informationen zu Standortnamen und Standortcodes
Mithilfe von Standortcodes und Standortnamen werden die Standorte einer Configuration Manager-Hierarchie identifiziert und verwaltet. In der Configuration Manager-Konsole werden Standortcode und Standortname im Format &lt;Standortcode\> - &lt;Standortname\> angezeigt. Jeder in Ihrer Hierarchie verwendete Standortcode muss eindeutig sein. Wenn Active Directory für Configuration Manager erweitert wurde und Daten an Standorten veröffentlicht werden, müssen die Standortcodes innerhalb der Active Directory-Gesamtstruktur eindeutig sein. Dies gilt auch dann, wenn sie in verschiedenen Configuration Manager-Hierarchien verwendet werden oder in früheren Configuration Manager-Installationen verwendet wurden. Planen Sie die Standortcodes und Standortnamen sorgfältig, bevor Sie die Hierarchie bereitstellen.

### <a name="specify-a-site-code-and-site-name"></a>Angeben eines Standortcodes und Standortnamens
Während des Configuration Manager-Setups werden Sie dazu aufgefordert, einen Standortcode und einen Standortnamen für den Standort der zentralen Verwaltung sowie für jede primäre und sekundäre Standortinstallation anzugeben. Der Standortcode muss jeden Standort der Hierarchie eindeutig identifizieren. Da der Standortcode in Ordnernamen verwendet wird, dürfen keine der folgenden Namen für den Standortcode verwendet werden. Dazu zählen für Configuration Manager und Windows reservierte Namen wie:
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> Das Setup von Configuration Manager überprüft nicht, ob der eingegebene Standortcode bereits verwendet wird.



Zum Eingeben des Standortcodes für einen Standort während des Configuration Manager-Setups müssen Sie drei alphanumerische Zeichen eingeben. Es sind nur Buchstaben von A bis Z und Ziffern von 0 bis 9 oder Kombinationen aus Buchstaben und Ziffern als Standortcodes zulässig. Die Reihenfolge der Buchstaben oder Ziffern hat keine Auswirkungen auf die Kommunikation zwischen Standorten. Es ist beispielsweise nicht notwendig, den primären Standort mit ABC und den sekundären Standort mit DEF zu benennen.

Der Standortname dient als Anzeigename für den Standort. Verwenden Sie in Standortnamen nur die Standardzeichen A bis Z, a bis z, 0 bis 9 und den Bindestrich (-).
> [!IMPORTANT]
> Das Ändern von Standortcodes oder Standortnamen nach der Installation wird nicht unterstützt.

### <a name="reuse-a-site-code"></a>Wiederverwenden eines Standortcodes
Standortcodes können nicht mehr als einmal in einer Configuration Manager-Hierarchie für einen zentralen Verwaltungsstandort oder primäre Standorte verwendet werden, auch wenn der ursprüngliche Standort und Standortcode deinstalliert wurde. Wenn Sie einen bereits vorhandenen Standortcode verwenden, besteht die Gefahr, dass es in Ihrer Hierarchie zu Konflikten zwischen Objekt-IDs kommt. Sie können den Standortcode für einen sekundären Standort wiederverwenden, wenn dieser in Ihrer Configuration Manager-Hierarchie oder in der Active Directory-Gesamtstruktur nicht mehr verwendet wird.


## <a name="limits-and-restrictions-for-installed-sites"></a>Limits und Einschränkungen für installierte Standorte
Beachten Sie vor der Installation von Standorten die für Standorte und Hierarchien geltenden folgenden Einschränkungen:
-   Nachdem Setup abgeschlossen ist, können Sie die folgenden Standorteigenschaften nicht ändern, ohne den Standort zu deinstallieren und anschließend mit den neuen Werten erneut zu installieren:  
    -   Das Installationsverzeichnis für Programmdateien  
    -   Standortcode  
    -   Standortbeschreibung  
-   Falls Ihre Hierarchie einen Standort der zentralen Verwaltung aufweist:  
    -   Configuration Manager unterstützt nicht das Verschieben eines untergeordneten primären Standorts aus einer Hierarchie zum Erstellen eines eigenständigen primären Standorts oder zum Hinzufügen des Standorts zu einer anderen Hierarchie. Stattdessen müssen Sie den untergeordneten primären Standort deinstallieren und dann erneut als neuen eigenständigen primären Standort oder untergeordneten Standort der zentralen Verwaltung von einer anderen Hierarchie installieren.  


## <a name="a-namebkmkoptionalstepsa-optional-steps-to-run-before-starting-setup"></a><a name="bkmk_optionalsteps"></a> Optionale Schritte vor Beginn der Installation
**Sie können das [Setup-Downloadprogramm](../../../../core/servers/deploy/install/setup-downloader.md) manuell ausführen**, um die aktualisierten Setupdateien für Configuration Manager herunterzuladen.

Wenn der Computer, auf dem Sie Setup ausführen möchten, nicht mit dem Internet verbunden ist oder Sie die Installation mehrerer Standortserver erwarten, erwägen Sie den Einsatz des Setup-Downloadprogramms zum Herunterladen der erforderlichen Updates in Setupdateien:

-  Standardmäßig verbindet sich Setup mit dem Internet, um aktualisierte Setupdateien herunterzuladen.
-  Standardmäßig werden die Dateien in einem Ordner namens „Redist“ gespeichert.
-  Sie können Setup an einen Speicherort im Netzwerk verweisen, an dem Sie zuvor eine Kopie dieser Dateien gespeichert haben.


**Sie können die [Voraussetzungsprüfung](../../../../core/servers/deploy/install/prerequisite-checker.md) manuell ausführen**, um vor der Ausführung von Setup Probleme zu bestimmen und zu beheben. Vor dem Start des Setups zum Installieren eines Standorts und vor dem Installieren einer Standortsystemrolle auf einem Server können Sie die Voraussetzungsprüfung ausführen. Damit lässt sich sicherstellen, dass der Computer die Anforderungen zum Hosten des Standorts oder der Standortsystemrolle erfüllt.
 -  Setup führt die Voraussetzungsprüfung standardmäßig aus.
 -  Bei etwaigen Fehlern wird das Setup angehalten, bis das Problem behoben ist.


**Bestimmen Sie optionale Ports** , die von Standortsystemen und Clients verwendet werden können.
 -  Standardmäßig verwenden Standortsysteme und Clients vordefinierte Ports zur Kommunikation.
 -  Während der Installation können Sie alternative Ports konfigurieren.
 -  Weitere Informationen finden Sie unter [In System Center Configuration Manager verwendete Ports](../../../../core/plan-design/hierarchy/ports.md).



<!--HONumber=Nov16_HO1-->


