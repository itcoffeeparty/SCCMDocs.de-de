---
title: Migrieren von Inhalt | System Center Configuration Manager
description: "Verwenden Sie Verteilungspunkte für das Verwalten von Inhalten beim Migrieren von Daten zu einer Zielhierarchie in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aa88f18247b49995bff4a4a6f5fd1e1ed70ca214


---
# <a name="planning-a-content-deployment-migration-strategy-in-system-center-configuration-manager"></a>Planen einer Migrationsstrategie für die Inhaltsbereitstellung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Während Sie aktiv Daten zu einer System Center Configuration Manager-Zielhierarchie migrieren, verfügen die Configuration Manager-Clients sowohl in der Quell- als auch der Zielhierarchie über Zugriff auf Inhalte, die Sie in der Quellhierarchie bereitgestellt haben. Außerdem können Sie mithilfe der Migration Verteilungspunkte aus der Quellhierarchie aktualisieren oder neu zuweisen, sodass sie zu Verteilungspunkten in der Zielhierarchie werden. Wenn Sie Verteilungspunkte freigeben und aktualisieren neu zuweisen, müssen Sie dank dieser Strategie den Inhalt für die von Ihnen migrierten Clients nicht erneut für die neuen Server in der Zielhierarchie bereitstellen.  

Sie können dieselben Inhalte zwar in der Zielhierarchie erstellen und verteilen, es ist aber auch möglich, die Inhalte anhand der folgenden Optionen zu verwalten:  

-   Geben Sie Verteilungspunkte in der Quellhierarchie für Clients in der Zielhierarchie frei.  

-   Führen Sie für eigenständige Configuration Manager 2007-Verteilungspunkte oder sekundäre Configuration Manager 2007-Standorte ein Upgrade in der Quellhierarchie aus, damit sie in der Zielhierarchie zu Verteilungspunkten werden.  

-   Ordnen Sie Verteilungspunkte aus einer System Center Configuration Manager-Quellhierarchie einem Standort in der Zielhierarchie neu zu.  

Die folgenden Abschnitte helfen Ihnen beim Planen der Bereitstellung von Inhalten während der Migration:  

-   [Freigeben von Verteilungspunkten zwischen Quell- und Zielhierarchien](#About_Shared_DPs_in_Migration)  

-   [Planen von Upgrades freigegebener Configuration Manager 2007-Verteilungspunkte](#Planning_to_Upgrade_DPs)  

    -   [Upgradeprozess für Verteilungspunkte](#BKIMK_UpgradeProcess)  

    -   [Planning to upgrade Configuration Manager 2007 secondary sites](#BKMK_UpgradeSS)  

-   [Planen der Neuzuweisung von System Center Configuration Manager-Verteilungspunkten](#BKMK_ReassignDistPoint)  

    -   [Neuzuweisungsprozess für Verteilungspunkte](#BKMK_ReassignProcess)  

-   [Inhaltsbesitz beim Migrieren von Inhalten](#About_Migrating_Content)  

##  <a name="a-nameaboutshareddpsinmigrationa-share-distribution-points-between-source-and-destination-hierarchies"></a><a name="About_Shared_DPs_in_Migration"></a> Freigeben von Verteilungspunkten zwischen Quell- und Zielhierarchien  
Während der Migration können Sie Verteilungspunkte aus der Quellhierarchie für die Zielhierarchie freigeben. Sie können freigegebene Verteilungspunkte nutzen, um aus einer Quellhierarchie migrierte Inhalte unmittelbar für Clients in der Zielhierarchie verfügbar zu machen, ohne die Inhalte neu erstellen und an neue Verteilungspunkte in der Zielhierarchie verteilen zu müssen. Wenn in der Zielhierarchie Inhalte von Clients angefordert werden, die an von Ihnen freigegebenen Verteilungspunkten bereitgestellt werden, dann können die freigegebenen Verteilungspunkte den Clients als gültige Inhaltsorte angeboten werden.  

 Abgesehen davon, dass ein Verteilungspunkt ein gültiger Inhaltsort für Clients in der Zielhierarchie ist, solange die Migration von der Quellhierarchie aktiv ist, können Sie ein Upgrade für ihn durchführen oder ihn der Zielhierarchie zuweisen. Sie können für freigegebene Configuration Manager 2007-Verteilungspunkte ein Upgrade durchführen und freigegebene Verteilungspunkte für System Center 2012 Configuration Manager erneut zuweisen. Wenn Sie einen freigegebenen Verteilungspunkt aktualisieren oder erneut zuweisen, wird der Verteilungspunkt aus der Quellhierarchie entfernt und wird zu einem Verteilungspunkt in der Zielhierarchie. Nachdem Sie einen freigegebenen Verteilungspunkt aktualisiert oder erneut zugewiesen haben, können Sie den Verteilungspunkt weiterhin in der Zielhierarchie verwenden, nachdem die Migration aus der Quellhierarchie abgeschlossen ist. Weitere Informationen zum Upgrade freigegebener Verteilungspunkte finden Sie unter [Planning to upgrade Configuration Manager 2007 shared distribution points](#Planning_to_Upgrade_DPs). Informationen zur erneuten Zuweisung eines freigegebenen Verteilungspunktes finden Sie unter [Planen der Neuzuweisung von System Center Configuration Manager-Verteilungspunkten](#BKMK_ReassignDistPoint).  

 Sie können Verteilungspunkte von allen Quellstandorten in der Zielhierarchie freigeben. Wenn Sie Verteilungspunkte für einen Quellstandort freigeben, dann wird jeder qualifizierte Verteilungspunkt an diesem primären Standort und an allen untergeordneten sekundären Standorten dieses primären Standorts freigegeben. Damit ein Verteilungspunkt als freigegebener Verteilungspunkt infrage kommt, muss der Standortsystemserver, der den Verteilungspunkt hostet, mit einem vollqualifizierten Domänennamen (FQDN) konfiguriert sein. Verteilungspunkte, die mit einem NetBIOS-Namen konfiguriert sind, werden nicht berücksichtigt.  

> [!TIP]  
>  Bei Configuration Manager 2007 müssen Sie keinen FQDN für Standortsystemserver konfigurieren.  

Die folgenden Informationen helfen Ihnen beim Planen freigegebener Verteilungspunkte:  

-   Von Ihnen freigegebene Verteilungspunkte müssen die Voraussetzungen für freigegebene Verteilungspunkte erfüllen. Informationen zu diesen Voraussetzungen finden Sie im Abschnitt [Für die Migration erforderliche Konfigurationen](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) des Themas [Voraussetzungen für die Migration in System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

-   Die Aktion Verteilungspunkte freigeben ist eine standortweite Einstellung, mit der alle qualifizierten Verteilungspunkte an einem Quellstandort und an allen direkt untergeordneten sekundären Standorten freigegeben werden. Es ist nicht möglich, einzelne Verteilungspunkte freizugeben, wenn die Freigabe der Verteilungspunkte aktiviert wird.  

-   Von Clients in der Zielhierarchie können Informationen zum Inhaltsspeicherort für Pakete empfangen werden, die auf aus der Quellhierarchie freigegebenen Verteilungspunkten verteilt werden. Bei Verteilungspunkten aus einer Configuration Manager 2007-Zielhierarchie umfasst dies Zweigverteilungspunkte, Verteilungspunkte auf Serverfreigaben und Standardverteilungspunkte.  

    > [!WARNING]  
    >  Wenn Sie die Quellhierarchie ändern, sind die freigegebenen Verteilungspunkte der Originalquellhierarchie nicht mehr verfügbar und können den Clients in der Zielhierarchie nicht als Inhaltsorte angeboten werden. Wenn Sie die Migration zur Verwendung der Originalquellhierarchie umkonfigurieren, werden die zuvor freigegebenen Verteilungspunkte als gültige Inhaltsortserver wiederhergestellt.  

-   Wenn Sie ein Paket migrieren, das auf einem freigegebenen Verteilungspunkt gehostet wird, dann muss die Paketversion in den Quell- und Zielhierarchien identisch sein. Wenn die Paketversion in der Quell- und Zielhierarchie nicht identisch ist, dann können von Clients in der Zielhierarchie keine Inhalte vom freigegebenen Verteilungspunkt abgerufen werden. Wenn Sie ein Paket in der Quellhierarchie aktualisieren, müssen Sie die Paketdaten zunächst erneut migrieren, bevor der Inhalt von einem freigegebenen Verteilungspunkt von Clients in der Zielhierarchie abgerufen werden kann.  

    > [!NOTE]  
    >  Wenn Sie Details für ein Paket anzeigen, das auf einem freigegebenen Verteilungspunkt gehostet wird, wird die Anzahl von Paketen, welche auf der Registerkarte **Freigegebene Verteilungspunkte** der Quellstandorte als **Gehostete migrierte Pakete** angezeigt werden, erst dann aktualisiert, wenn der nächste Datensammlungszyklus abgeschlossen ist.  

-   Sie können freigegebene Verteilungspunkte und ihre Eigenschaften im Knoten **Quellhierarchie** im Arbeitsbereich **Verwaltung** der Configuration Manager-Konsole anzeigen, mit der eine Verbindung mit der Zielhierarchie hergestellt wird.  

-   Ein freigegebener Verteilungspunkt aus einer Configuration Manager 2007-Quellhierarchie kann nicht zum Hosten von Paketen für Microsoft Application Virtualization (App-V) verwendet werden. App-V-Pakete müssen für die Verwendung von Clients in der Zielhierarchie migriert und konvertiert werden. Sie können jedoch einen freigegebenen Verteilungspunkt aus einer System Center 2012 Configuration Manager- oder System Center Configuration Manager-Quellhierarchie verwenden, um App-V-Pakete für Clients in einer Zielhierarchie zu hosten.  

-   Wenn Sie einen geschützten Verteilungspunkt aus einer Configuration Manager 2007-Quellhierarchie freigeben, erstellt die Zielhierarchie eine Begrenzungsgruppe, in der die geschützten Netzwerkspeicherorte dieses Verteilungspunkts enthalten sind. Sie können diese Begrenzungsgruppe in der Zielhierarchie nicht ändern. Wenn Sie jedoch die Informationen der geschützten Begrenzungen für den Verteilungspunkt in der Configuration Manager 2007-Quellhierarchie ändern, werden diese Änderungen nach Abschluss des nächsten Datensammlungszyklus in der Zielhierarchie dargestellt.  

    > [!NOTE]  
    >  Da System Center 2012 Configuration Manager- und System Center Configuration Manager-Standorten das Konzept bevorzugter Verteilungspunkte anstelle geschützter Verteilungspunkte verwenden, gilt diese Bedingung nur für Verteilungspunkte, die von Configuration Manager 2007-Quellstandorten freigegeben werden.  

Die verfügbaren Verteilungspunkte sind erst in der Configuration Manager-Konsole sichtbar, wenn Sie Verteilungspunkte aus einem Quellstandort freigeben. Nach der Freigabe der Verteilungspunkte werden nur die erfolgreich freigegebenen Verteilungspunkte aufgeführt.  

Nach der Freigabe der Verteilungspunkte können Sie die Konfiguration jedes freigegebenen Verteilungspunkts in der Quellhierarchie ändern. Änderungen an der Konfiguration eines Verteilungspunkts werden nach dem nächsten Datensammlungszyklus in der Zielhierarchie dargestellt. Verteilungspunkte, die Sie aktualisiert haben, um sie für die Freigabe zu qualifizieren, werden automatisch freigegeben, während von den nicht mehr qualifizierten Verteilungspunkten, keine Verteilungspunkte mehr freigegeben werden. Sie könnten beispielsweise über einen Verteilungspunkt verfügen, der nicht mit einem Intranet-FQDN konfiguriert ist und zunächst nicht für die Zielhierarchie freigegeben war. Nach der Konfiguration des FQDN für diesen Verteilungspunkt wird diese Änderung durch den nächsten Datensammlungszyklus erkannt, und der Verteilungspunkt wird für die Zielhierarchie freigegeben.  

##  <a name="a-nameplanningtoupgradedpsa-planning-to-upgrade-configuration-manager-2007-shared-distribution-points"></a><a name="Planning_to_Upgrade_DPs"></a> Planen von Upgrades freigegebener Configuration Manager 2007-Verteilungspunkte  
Wenn Sie eine Migration aus einer Configuration Manager 2007-Quellhierarchie ausführen, können Sie einen freigegebenen Verteilungspunkt auf einen System Center Configuration Manager-Verteilungspunkt upgraden. Sie können Verteilungspunkte an primären und an sekundären Standorten aktualisieren. Beim Upgradeprozess wird der Verteilungspunkt aus der Configuration Manager 2007-Hierarchie entfernt und zu einem Standortsystemserver in der Zielhierarchie befördert. Bei diesem Prozess wird außerdem der vorhandene Inhalt auf dem Verteilungspunkt auf einen neuen Speicherort auf dem Verteilungspunktcomputer kopiert. Anschließend wird vom Upgradeprozess die Kopie der Inhalts geändert, um den SIS (Single Instance Store) zur Verwendung mit der Inhaltsbereitstellung in der Zielhierarchie zu erstellen. Wenn Sie ein Upgrade eines Verteilungspunkts durchführen, müssen Sie daher keine migrierten Inhalte neu verteilen, die auf dem Configuration Manager 2007-Verteilungspunkt gehostet waren.  

Nachdem Configuration Manager den Inhalt in einen Single Instance Store (SIS) umgewandelt hat, löscht Configuration Manager den ursprünglichen Quellinhalt auf dem Verteilungspunktcomputer, um Speicherplatz freizugeben. Dabei wird der Speicherort des ursprünglichen Quellinhalts nicht verwendet.  

Nicht alle Configuration Manager 2007-Verteilungspunkte, die Sie freigeben können, können auf System Center Configuration Manager upgegradet werden. Ein Configuration Manager 2007-Verteilungspunkt muss die Bedingungen für ein Upgrade erfüllen, um für ein Upgrade berechtigt zu sein. Zu diesen gehören der Standortsystemserver, auf dem der Verteilungspunkt installiert ist, und die Art des installierten Configuration Manager 2007-Verteilungspunkts. Sie können beispielsweise nicht für jede Art von Verteilungspunkten, die auf dem Standortservercomputer an einem primären Standort installiert sind, ein Upgrade durchführen, Sie können jedoch ein Upgrade für einen Standardverteilungspunkt durchführen, der auf dem Standortservercomputer an einem sekundären Standort installiert ist.  

> [!NOTE]  
>  Sie können nur für die freigegebenen Configuration Manager 2007-Verteilungspunkte ein Upgrade durchführen, die sich auf einem Computer mit einem Betriebssystem befinden, von dem Verteilungspunkte in der Zielhierarchie unterstützt werden. Beispiel: Obwohl Sie einen Configuration Manager 2007-Verteilungspunkt freigeben können, der sich auf einem Computer mit Windows Vista befindet, können Sie diesen freigegebenen Verteilungspunkt nicht upgraden, da das Betriebssystem nicht von System Center Configuration Manager zur Verwendung als Verteilungspunkt unterstützt wird.  

In der folgenden Tabelle werden die unterstützten Speicherorte für jede Art von Configuration Manager 2007-Verteilungspunkten aufgelistet, für die ein Upgrade durchgeführt werden kann.  

|Art des Verteilungspunkts|Verteilungspunkt auf einem Standortsystemcomputer, der nicht der Standortserver ist|Verteilungspunkt auf einen Standortsystemcomputer, der nicht der Standortserver ist und von dem andere Standortsystemrollen gehostet werden|Verteilungspunkt auf einem sekundären Standortserver|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|Standardverteilungspunkt|Ja|Nein|Ja|  
|Verteilungspunkt auf Serverfreigaben<sup>1</sup>|Ja|Nein|Nein|  
|Zweigverteilungspunkt|Ja|Nein|Nein|  

 <sup>1</sup> System Center Configuration Manager unterstützt keine Serverfreigaben für Standortsysteme, dafür jedoch Upgrades eines Configuration Manager 2007-Verteilungspunkts auf einer Serverfreigabe. Beim Upgrade eines Configuration Manager 2007-Verteilungspunkts, der sich auf einer Serverfreigabe befindet, wird die Verteilungspunktart automatisch in einen Server umgewandelt, und Sie müssen das Laufwerk auf dem Verteilungspunktcomputer auswählen, auf dem sich der Single Instance Content Store befinden soll.  

> [!WARNING]  
>  Bevor Sie ein Upgrade eines Zweigverteilungspunkts durchführen, müssen Sie die Configuration Manager 2007-Clientsoftware deinstallieren. Wenn Sie ein Upgrade eines Zweigverteilungspunkts durchführen, für den die Configuration Manager 2007-Clientsoftware installiert ist, wird der zuvor auf dem Computer bereitgestellte Inhalt vom Computer entfernt, und beim Upgrade des Verteilungspunkts tritt ein Fehler auf.  

Zur Identifizierung von Verteilungspunkten, die für ein Upgrade berechtigt sind, wählen Sie in der Configuration Manager-Konsole im Knoten **Quellhierarchie** einen Quellstandort aus, und rufen Sie dann die Registerkarte **Freigegebene Verteilungspunkte** auf. Bei den entsprechenden Verteilungspunkten wird in der Spalte **Zum Upgrade berechtigt** **Ja** angezeigt.  

Wenn Sie für einen Verteilungspunkt, der auf einem sekundären Standortserver von Configuration Manager 2007 installiert ist, ein Upgrade durchführen, wird der sekundäre Standort in der Quellhierarchie deinstalliert. Obwohl dieses Szenario als Upgrade eines sekundären Standorts bezeichnet wird, trifft es nur auf die Standortsystemrolle „Verteilungspunkt“ zu. Das führt dazu, dass der sekundäre Standort nicht aktualisiert, sondern deinstalliert wird. So verbleibt nur ein Verteilungspunkt aus der Zielhierarchie auf dem Computer, welcher der sekundäre Standortserver war. Da der sekundäre Standort aus der Quellhierarchie entfernt wurde, sollten Sie den Abschnitt [Planning to upgrade Configuration Manager 2007 secondary sites](#BKMK_UpgradeSS) dieses Themas beachten, wenn Sie ein Upgrade des Verteilungspunkts an einem sekundären Standort durchführen möchten.  

###  <a name="a-namebkimkupgradeprocessa-distribution-point-upgrade-process"></a><a name="BKIMK_UpgradeProcess"></a> Upgradeprozess für Verteilungspunkte  
Sie können die Configuration Manager-Konsole zum Durchführen von Upgrades von Configuration Manager 2007-Verteilungspunkten verwenden, die Sie für die Zielhierarchie freigegeben haben. Wird ein Upgrade eines freigegebenen Verteilungspunkts durchgeführt, wird dieser am Configuration Manager 2007-Standort deinstalliert und als Verteilungspunkt installiert, der mit einem in der Zielhierarchie angegebenen primären oder sekundären Standort verbunden ist. Beim Upgradeprozess werden die migrierten Inhalte kopiert, die auf dem Verteilungspunkt gespeichert sind. Diese Kopie wird dann in den Single Instance Content Store konvertiert. Wenn Configuration Manager ein Paket in den Single Instance Content Store konvertiert, dann wird dieses Paket aus der SMSPKG-Freigabe auf dem Verteilungspunktcomputer gelöscht, es sei denn, das Paket enthält eine oder mehrere Ankündigungen, für welche die Option **Programm vom Verteilungspunkt ausführen** konfiguriert ist.  

Zum Durchführen des Verteilungspunktupgrades verwendet Configuration Manager das **Zugriffskonto des Quellstandorts**, das für die Datensammlung vom SMS-Anbieter des Quellstandorts konfiguriert ist. Zur Datensammlung vom Quellstandort benötigen die Standortobjekte für dieses Konto zwar nur die Berechtigung **Lesen**, doch die Berechtigungen **Löschen** und **Ändern** für die Klasse **Standort** sind ebenfalls erforderlich, um den Verteilungspunkt beim Upgrade erfolgreich vom Configuration Manager 2007-Standort entfernen zu können.  

> [!NOTE]  
>  Configuration Manager kann nur an jeweils einem einzelnen Verteilungspunkt Inhalte in den Single Instance Store konvertieren. Wenn Sie Upgrades für mehrere Verteilungspunkte planen, werden die Verteilungspunkte in eine Upgradereihenfolge gebracht und nacheinander bearbeitet.  

Vergewissern Sie sich, dass alle auf dem Verteilungspunkt gehosteten Inhalte migriert wurden, bevor Sie das Upgrade des freigegebenen Verteilungspunkts durchführen. Inhalte, die vor dem Upgrade des Verteilungspunkts nicht migriert wurden, stehen nach dem Upgrade in der Zielhierarchie nicht mehr zur Verfügung. Wenn Sie ein Upgrade eines Verteilungspunkts durchführen, werden die Inhalte der migrierten Pakete in ein Format konvertiert, das mit dem SIS (Single Instance Store) der Zielhierarchie kompatibel ist.  

Damit das Upgrade des Verteilungspunkts von der Configuration Manager-Konsole aus durchgeführt werden kann, muss der Configuration Manager 2007-Standortsystemserver die folgenden Bedingungen erfüllen:  

-   Die Konfiguration und der Speicherort des Verteilungspunkts müssen für das Upgrade berechtigt sein.  

-   Auf dem Verteilungspunktcomputer muss ausreichend freier Speicherplatz für die Inhalte verfügbar sein, die vom Configuration Manager 2007-Inhaltsspeicherformat in das SIS-Format konvertiert werden. Für diese Konvertierung ist verfügbarer Speicherplatz in der Größe des größten Pakets erforderlich, das auf dem Verteilungspunkt gespeichert ist.  

-   Auf dem Verteilungspunktcomputer muss eine Betriebssystemversion ausgeführt werden, die als Verteilungspunkt in der Zielhierarchie unterstützt wird.  

    > [!NOTE]  
    >  Wenn Configuration Manager die Upgradeberechtigung eines Verteilungspunkts überprüft, wird dabei nicht die Betriebssystemversion des Verteilungspunktcomputers überprüft.  

Zur Durchführung eines Upgrades eines Verteilungspunkts erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**und dann den Knoten **Quellhierarchie** , und wählen Sie den Standort mit dem betreffenden Verteilungspunkt aus. Wählen Sie dann im Detailbereich der Registerkarte **Freigegebene Verteilungspunkte** den Verteilungspunkt aus, bei dem das Upgrade durchgeführt werden soll.  

Anhand der Statusangabe in der Spalte **Zur Neuzuweisung berechtigt** können Sie erkennen, ob der Verteilungspunkt für das Upgrade geeignet ist.  Wählen Sie dann im Menüband der Configuration Manager-Konsole auf der Registerkarte **Verteilungspunkte** in der Gruppe **Verteilungspunkt** die Option **Neu zuweisen** aus. Es wird ein Assistent geöffnet, mit dem Sie das Upgrade des Verteilungspunkts abschließen können.  

Wenn Sie ein Upgrade eines freigegebenen Verteilungspunkts durchführen, müssen Sie diesen anschließend einem primären oder sekundären Standort Ihrer Wahl in der Zielhierarchie zuweisen. Nachdem das Upgrade des Verteilungspunkts durchgeführt ist, können Sie ihn wie jeden anderen als Verteilungspunkt in der Zielhierarchie verwenden.  

Sie können den Fortschritt eines Verteilungspunktupgrades in der Configuration Manager-Konsole überwachen, indem Sie im Arbeitsbereich **Verwaltung** unter dem Knoten **Migration** den Knoten **Verteilungspunktmigration** auswählen. Informationen können auch der Datei **Migmctrl.log** auf dem Standortserver der zentralen Verwaltung der Zielhierarchie oder der Datei **distmgr.log** auf dem Standortserver in der Zielhierarchie, in welcher der aktualisierte Verteilungspunkt verwaltet wird, entnommen werden.  

> [!NOTE]  
>  Beim Upgrade eines Verteilungspunkts auf die Zielhierarchie wird die Standortsystemrolle „Verteilungspunkt“ vom Configuration Manager 2007-Quellstandort entfernt. Pakete, die zum Verteilungspunkt gesendet wurden, werden in der Configuration Manager 2007-Hierarchie allerdings nicht aktualisiert. In der Configuration Manager 2007-Konsole führen Pakete, die zum Verteilungspunkt gesendet wurden, den Standortsystemcomputer weiterhin als Verteilungspunkt mit dem **Typ** **Unbekannt** auf. Nachfolgende Updates des Pakets in Configuration Manager 2007 führen für diesen Standort in der Datei „distmgr.log“ zu Berichtfehlern des Verteilungs-Managers, wenn der Standort versucht, das Paket auf dem unbekannten Standortsystem zu aktualisieren.  

Auch wenn Sie für einen freigegebenen Verteilungspunkt kein Upgrade durchführen möchten, können Sie immer noch einen Verteilungspunkt aus der Zielhierarchie auf einem ehemaligen Configuration Manager 2007-Verteilungspunkt installieren. Vor der Installation des neuen Verteilungspunkts müssen Sie alle Configuration Manager 2007-Standortsystemrollen vom Verteilungspunktcomputer deinstallieren. Dazu gehört auch der Configuration Manager 2007-Standort, wenn es sich um den Standortservercomputer handelt. Wenn Sie einen Configuration Manager 2007-Verteilungspunkt deinstallieren, wird der auf dem Verteilungspunkt bereitgestellte Inhalt nicht vom Computer gelöscht.  

###  <a name="a-namebkmkupgradessa-planning-to-upgrade-configuration-manager-2007-secondary-sites"></a><a name="BKMK_UpgradeSS"></a> Planning to upgrade Configuration Manager 2007 secondary sites  
 Wenn Sie ein Upgrade eines freigegebenen Verteilungspunkts, der auf einem sekundären Configuration Manager 2007-Standortserver gehostet wird, über eine Migration durchführen, upgradet Configuration Manager nicht nur die Standortsystemrolle „Verteilungspunkt“ auf einen Verteilungspunkt in der Zielhierarchie, sondern deinstalliert auch den sekundäre Standort in der Quellhierarchie. Das Ergebnis ist ein System Center Configuration Manager-Verteilungspunkt, jedoch kein sekundärer Standort.  

 Damit ein Verteilungspunkt auf dem Standortservercomputer zum Upgrade berechtigt ist, muss Configuration Manager den sekundären Standort einschließlich aller Standortsystemrollen auf diesem Computer deinstallieren können. Typischerweise ist ein freigegebener Verteilungspunkt auf einer Configuration Manager 2007-Serverfreigabe zum Upgrade berechtigt. Wenn jedoch eine Serverfreigabe auf dem sekundären Standortserver besteht, sind der sekundäre Standort und freigegebene Verteilungspunkte auf diesem Computer nicht zum Upgrade berechtigt. Die Ursache ist der Versuch des Prozesses, den sekundären Standort zu deinstallieren, wobei die Serverfreigabe jedoch als zusätzliches Standortsystemobjekt behandelt wird, wodurch dieses Objekt nicht vom Prozess deinstalliert werden kann. In diesem Szenario können Sie einen Standard-Verteilungspunkt auf dem sekundären Standortserver aktivieren und den Inhalt anschließend erneut auf einem Standard-Verteilungspunkt verteilen. Für diesen Vorgang wird keine Netzwerkbandbreite verbraucht und nach Abschluss können Sie den Verteilungspunkt auf der Serverfreigabe deinstallieren, die Serverfreigabe entfernen und anschließend das Upgrade des Verteilungspunkts und des sekundären Standorts durchführen.  

 Überprüfen Sie vor dem Upgrade die Konfiguration des freigegebenen Verteilungspunkts in Configuration Manager 2007, damit Sie kein Upgrade eines Verteilungspunkts an einem sekundären Standort durchführen, den Sie weiterhin mit Configuration Manager 2007 verwenden möchten. Das liegt daran, dass nach dem Upgrade eines freigegebenen Verteilungspunkts auf einem Standortssystemserver der Standortsystemserver aus der Configuration Manager 2007-Hierarchie entfernt wird und dort nicht mehr zur Verfügung steht. Nach dem Entfernen des sekundären Standorts sind alle verbleibenden Verteilungspunkte an diesem sekundären Standort verwaist. Das bedeutet, dass sie von Configuration Manager 2007 nicht mehr verwaltet werden und nicht mehr zum Upgrade freigegeben werden oder berechtigt sind.  

> [! WARNUNG]  
>  Wenn Sie in der Configuration Manager-Konsole freigegebene Verteilungspunkte anzeigen, gibt es keinen sichtbaren Hinweis darauf, ob sich ein freigegebener Verteilungspunkt auf einem Remote-Standortsystemserver bzw. einem sekundären Standortserver befindet.  

 Es wird empfohlen, für sekundäre Standorte mit freigegebenem Verteilungspunkt ein Upgrade durchzuführen, wenn Sie über einen sekundären Standort an einem Remotenetzwerkort verfügen, der primär zur Steuerung der Bereitstellung von Inhalten für diesen Remotespeicherort verwendet wird. Da Sie bei der Verteilung von Inhalten auf einen System Center Configuration Manager-Verteilungspunkt die Bandbreitensteuerung konfigurieren können, können Sie einen sekundären Standort häufig auf einen Verteilungspunkt upgraden, den Verteilungspunkt zur Bandbreitensteuerung konfigurieren und das Installieren eines sekundären Standorts an diesem Netzwerkspeicherort in der Zielhierarchie vermeiden.  

 Der Upgradeprozess eines freigegebenen Verteilungspunkts auf einem sekundären Standortserver verläuft genauso wie jedes andere Verteilungspunktupgrade. Inhalte werden kopiert und in den von der Zielhierarchie verwendeten SIS (Single Instance Store) konvertiert. Wenn Sie jedoch für einen freigegebenen Verteilungspunkt, der sich auf einem sekundären Standortserver befindet, ein Upgrade durchführen, werden beim Upgradeprozess der Verwaltungspunkt (wenn vorhanden) sowie der sekundäre Standort deinstalliert. Als Ergebnis wird der sekundäre Standort aus der Configuration Manager 2007-Hierarchie entfernt. Für die Deinstallation des sekundären Standorts verwendet Configuration Manager das Konto, das zur Sammlung von Daten vom Quellstandort konfiguriert ist.  

 Zwischen der Deinstallation des sekundären Configuration Manager 2007-Standorts und dem Beginn der Installation des Verteilungspunkts in der Zielhierarchie gibt es beim Upgrade eine Verzögerung. Der Datensammlungszyklus beziffert diese Verzögerung auf bis zu vier Stunden. Die Verzögerung dient dazu, Zeit für die Deinstallation des sekundären Standorts zu schaffen, bevor die Installation des neuen Verteilungspunkts beginnt.  

 Weitere Informationen zum Upgrade freigegebener Verteilungspunkte finden Sie unter [Planning to upgrade Configuration Manager 2007 shared distribution points](#Planning_to_Upgrade_DPs).  

##  <a name="a-namebkmkreassigndistpointa-planning-to-reassign-system-center-configuration-manager-distribution-points"></a><a name="BKMK_ReassignDistPoint"></a> Planen der Neuzuweisung von System Center Configuration Manager-Verteilungspunkten  
 Bei der Migration von einer unterstützten Version von System Center 2012 Configuration Manager zu einer Hierarchie mit der gleichen Version, können Sie einen freigegebenen Verteilungspunkt aus der Quellhierarchie erneut einem Standort in der Zielhierarchie zuweisen. Dieser Vorgang ähnelt dem Konzept eines Upgrades eines Configuration Manager 2007-Verteilungspunkts auf einen Verteilungspunkt in der Zielhierarchie. Sie können Verteilungspunkte an primären und an sekundären Standorten neu zuweisen. Mit der Aktion zum Neuzuweisen eines Verteilungspunkts wird der Verteilungspunkt aus der Quellhierarchie entfernt, und der Computer sowie sein Verteilungspunkt werden zum Standortsystemserver für den Standort, den Sie in der Zielhierarchie auswählen können.  

 Wenn Sie einen Verteilungspunkt neu zuweisen, müssen Sie keine migrierten Inhalte neu verteilen, die auf dem Verteilungspunkt des Quellstandorts gehostet waren. Zudem ist anders als beim Upgrade eines Configuration Manager 2007-Verteilungspunkts bei der Neuzuweisung eines Verteilungspunkts kein zusätzlicher Speicherplatz auf dem Verteilungspunktcomputer erforderlich. Dies liegt daran, dass ab System Center 2012 Configuration Manager Verteilungspunkte das SIS-Format (Single Instance Store) für Inhalte verwenden, und der Inhalt auf dem Verteilungspunktcomputer nicht konvertiert werden muss, wenn der Verteilungspunkt zwischen Hierarchien neu zugewiesen wird.  

 Damit ein System Center 2012 Configuration Manager-Verteilungspunkt zur Neuzuweisung berechtigt ist, müssen folgende Kriterien erfüllt werden:  

-   Ein freigegebener Verteilungspunkt muss auf einem anderen Computer als dem Standortserver installiert werden.  

-   Ein freigegebener Verteilungspunkt darf sich nicht auf demselben Computer wie beliebige zusätzliche Standortsystemrollen befinden.  

Zur Identifizierung von Verteilungspunkten, die für eine Neuzuweisung berechtigt sind, wählen Sie in der Configuration Manager-Konsole im Knoten **Quellhierarchie** einen Quellstandort aus, und rufen Sie dann die Registerkarte **Freigegebene Verteilungspunkte** auf. Berechtigte Verteilungspunkte zeigen in der Spalte **Zur Neuzuweisung berechtigt** **Ja** an (vor System Center 2012 R2 Configuration Manager hatte diese Spalte den Namen **Zum Upgrade berechtigt**).  

###  <a name="a-namebkmkreassignprocessa-distribution-point-reassignment-process"></a><a name="BKMK_ReassignProcess"></a> Neuzuweisungsprozess für Verteilungspunkte  
 Sie können die Configuration Manager-Konsole zur Neuzuweisung von Verteilungspunkten verwenden, die Sie in einer aktiven Quellhierarchie freigegeben haben. Wird ein freigegebener Verteilungspunkt erneut zugewiesen, wird dieser am Quellstandort deinstalliert und als Verteilungspunkt installiert, der mit einem in der Zielhierarchie angegebenen primären oder sekundären Standort verbunden ist.  

 Zum Neuzuweisen des Verteilungspunkts wird von der Zielhierarchie das Zugriffskonto des Quellstandorts verwendet, das für die Sammlung von Daten des SMS-Anbieters des Quellstandorts konfiguriert ist. Informationen zu erforderlichen Berechtigungen und zusätzlichen Voraussetzungen finden Sie unter [Voraussetzungen für die Migration in System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

##  <a name="a-nameaboutmigratingcontenta-content-ownership-when-migrating-content"></a><a name="About_Migrating_Content"></a> Inhaltsbesitz beim Migrieren von Inhalten  
 Wenn Sie Inhalte für Bereitstellungen migrieren, müssen Sie das Inhaltsobjekt einem Standort in der Zielhierarchie zuweisen. Dieser Standort wird dann zum Besitzer dieses Inhalts in der Zielhierarchie. Vom Standort der obersten Ebene der Zielhierarchie werden die Metadaten der Inhalte zwar eigentlich migriert, doch es ist der zugewiesene Standort, durch den über das Netzwerk ein Zugriff auf die Originalquelle der Inhalte erfolgt.  

 Zum Minimieren der beim Migrieren von Inhalten verwendeten Netzwerkbandbreite übertragen Sie den Besitz des Inhalts auf einen Standort in der Zielhierarchie, der sich im Netzwerk in der Nähe des Inhaltsorts in der Quellhierarchie befindet. Die Inhaltsinformationen sind in der Zielhierarchie global freigegeben und daher an jedem Standort verfügbar.  

 Inhaltsinformationen werden zwar mithilfe der Datenbankreplikation für alle Standorte freigegeben, doch alle Inhalte, die einem primären Standort zugewiesen und dann für Verteilungspunkte an anderen primären Standorten bereitgestellt werden, werden mithilfe von dateibasierter Replikation übertragen. Diese Übertragung wird über den zentralen Verwaltungsstandort zum zusätzlichen primären Standort weitergeleitet. Bei geringer Netzwerkbandbreite können Sie Datentransfers reduzieren, indem Sie Pakete zentralisieren, die Sie vor oder während der Migration an mehrere primäre Standorte verteilen möchten, wenn Sie einen Standort als Besitzer des Inhalts zuweisen.  



<!--HONumber=Nov16_HO1-->

