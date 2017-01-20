---
title: Verwalten von Clients | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Clients in System Center Configuration Manager verwalten.
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: 17
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: dfdb5a95b672d3858d094750625cb5f6ef50700d


---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>Verwalten von Clients in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn ein System Center Configuration Manager-Client installiert und erfolgreich einem Configuration Manager-Standort zugewiesen wurde, wird Ihnen das Gerät im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Geräte** sowie in mindestens einer Sammlung im Knoten **Gerätesammlungen** angezeigt. Wenn Sie das Gerät oder die Sammlung, die das Gerät enthält, auswählen, können Sie verschiedene Verwaltungsvorgänge auswählen. Sie haben jedoch auch andere Möglichkeiten, den Client zu verwalten. Hierbei können andere Arbeitsbereiche der Konsole oder Tasks, von denen die Configuration Manager-Konsole nicht verwendet wird, relevant sein.  

 In diesem Thema finden Sie allgemeine Informationen dazu, mit welchen Tasks des Arbeitsbereichs ** Bestand und Kompatibilität** Sie einen Configuration Manager-Client verwalten können. Sie finden außerdem detailliertere Informationen zu den zusätzlichen Tasks zur Verwaltung des Configuration Manager-Clients. Informationen zum Konfigurieren des Clients finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Ein Configuration Manager-Client ist möglicherweise installiert, wird jedoch nicht in der Configuration Manager-Konsole angezeigt. Dies ist möglich, wenn der Client noch nicht erfolgreich einem Standort zugeordnet wurde, wenn die Konsole aktualisiert werden muss oder wenn ein Update auf eine Sammlungsmitgliedschaft angewendet werden muss.  
>   
>  Es ist außerdem möglich, dass ein Gerät in der Konsole angezeigt wird, wenn der Configuration Manager-Client nicht installiert ist. Dies ist möglich, wenn das Gerät zwar ermittelt wurde, der Configuration Manager-Client jedoch nicht installiert und zugewiesen wurde. Von mobilen Geräten, die mithilfe des Exchange Server-Connectors verwaltet werden, wird der Configuration Manager-Client nicht installiert. Darüber hinaus dürfen Geräte, die in Microsoft Intune registriert sind, den Configuration Manager-Client nicht installieren.  
>   
>  Verwenden Sie die Spalte **Client** in der Configuration Manager-Konsole, um zu bestimmen, ob der Configuration Manager-Client installiert ist, und um ihn mithilfe der Configuration Manager-Konsole verwalten zu können.  

##  <a name="a-namebkmkmanagingclientsdevicesnodea-manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> Verwalten von Clients mithilfe des Knotens „Geräte“  
 Verwenden Sie das folgende Verfahren und die folgende Tabelle, um ein oder mehrere Geräte im Arbeitsbereich **Bestand und Kompatibilität** mithilfe des Knotens **Geräte** zu verwalten.  

> [!IMPORTANT]  
>  Je nach Typ des Geräts sind einige dieser Optionen möglicherweise nicht verfügbar.  

#### <a name="to-manage-clients-from-the-devices-node"></a>So verwalten Sie Clients mithilfe des Knotens „Geräte“  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Geräte**.  

3.  Wählen Sie mindestens ein Gerät aus, und wählen Sie anschließend einen der folgenden Clientverwaltungstasks aus dem Menüband, oder indem Sie einen Rechtsklick auf das Gerät ausführen.  

    -   **Verwalten von Informationen zur Affinität zwischen Benutzer und Gerät**  

         Hiermit können Sie die Zuordnungen zwischen Benutzern und Geräten konfigurieren und in der Folge den Benutzern Software effizient bereitstellen.  

         Informationen hierzu finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

    -   **Hinzufügen des Geräts zu einer neuen oder vorhandenen Sammlung**  

         Verwenden Sie die sammlungsbezogenen Aktionen, um das ausgewählte Gerät mithilfe einer direkten Regel rasch einer Sammlung hinzuzufügen.  

         [Betriebs- und Wartungsaufgaben für Sammlungen in System Center Configuration Manager](../../../core/clients/manage/collections/operations-and-maintenance-for-collections.md)  

    -   **Installieren und erneutes Installieren des Clients mithilfe von Clientpushinstallation**  

         Mithilfe des Assistenten für die Clientpushinstallation ist ein effizientes Installieren und erneutes Installieren des Configuration Manager-Clients möglich. Auf diese Art lässt sich der Client reparieren oder auf Windows-Computern mit Standortkonfigurationsoptionen und zusätzlichen Eigenschaften für client.msi neu konfigurieren, die Sie für die Clientpushinstallation angegeben haben.  

        > [!TIP]  
        >  Es gibt viele verschiedene Möglichkeiten, den Configuration Manager-Client zu installieren (und erneut zu installieren). Die Clientpushinstallation ist eine praktische Methode zur Clientinstallation, da Sie sie mithilfe der Konsole ausführen können. Allerdings hat diese Installationsmethode zahlreiche Abhängigkeiten und ist nicht für alle Umgebungen geeignet. Wenn eine Installation mithilfe von Clientpush nicht erfolgreich ist, gibt es mehrere andere Installationsmethoden, die Sie verwenden können. Weitere Informationen zu den Abhängigkeiten finden Sie unter [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) (Voraussetzungen für die Bereitstellung von Clients auf Windows-PCs in System Center Configuration Manager). Weitere Informationen zu den anderen Clientinstallationsmethoden finden Sie unter [Clientinstallationsmethoden in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

         Informationen finden Sie auch unter [Installieren von Configuration Manager-Clients mittels Clientpush](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Neuzuweisen des Standorts**  

         Weisen Sie bei Bedarf einen oder mehrere Clients, einschließlich verwalteter mobiler Geräte, einem anderen primären Standort in der Hierarchie neu zu. Clients können einzeln neu zugewiesen werden. Sie können aber auch mehrere Clients auswählen und sie gleichzeitig einem neuen Standort neu zuweisen.  

    -   **Remotes Verwalten des Clients**  

         Sie können den Ressourcen-Explorer ausführen, um Informationen zu Hard- und Softwareinventar eines Windows-Clients anzuzeigen, und Sie können den Client per Remotesteuerung, Remoteunterstützung oder Remotedesktop remote verwalten.  

         Informationen hierzu finden Sie unter [Anzeigen des Hardwareinventars mit dem Ressourcen-Explorer in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) und [Anzeigen des Softwareinventars mit dem Ressourcen-Explorer in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

         Informationen hierzu finden Sie unter [Remoteverwaltung eines Windows-Clientcomputers mithilfe von System Center Configuration Manager](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

    -   **Genehmigen eines Clients**  

         Wenn die Kommunikation zwischen Client und Standortsystemen über HTTP erfolgt und ein selbstsigniertes Zertifikat verwendet wird, müssen Sie die Clients genehmigen, um sie als vertrauenswürdige Computer zu identifizieren. Standardmäßig werden Clients aus dem gleichen Active Directory-Gesamtverzeichnis sowie aus vertrauenswürdigen Gesamtverzeichnissen von der Standortkonfiguration automatisch genehmigt, sodass Sie nicht jeden Client manuell genehmigen müssen. Sie müssen jedoch Arbeitsgruppencomputer und andere Computer, die Sie als vertrauenswürdig einstufen, die jedoch nicht genehmigt sind, manuell genehmigen.  

        > [!WARNING]  
        >  Bei nicht genehmigten Clients sind einige Verwaltungsfunktionen möglicherweise nicht ausführbar. Dieses Szenario wird jedoch für Configuration Manager nicht unterstützt.  

         Sie müssen keine Clients genehmigen, deren Kommunikation mit Standortsystemen immer über HTTPS statt über HTTP erfolgt, und auch keine Clients, von denen zur Kommunikation mit Standortsystemen über HTTP ein PKI-Zertifikat verwendet wird. Von diesen Clients wird mithilfe der PKI-Zertifikate eine Vertrauensstellung mit Configuration Manager hergestellt.  

    -   **Blockieren und Zulassen eines Clients**  

         Blockieren Sie Clients, die Sie nicht mehr als vertrauenswürdig einstufen, um ein Übermitteln der Clientrichtlinie an die Clients und eine Kommunikation zwischen Configuration Manager-Standortsystemen und den Clients zu verhindern.  

        > [!WARNING]  
        >  Durch das Blockieren eines Clients wird nur die Kommunikation vom Client an die Configuration Manager-Standortsysteme verhindert. Die Kommunikation mit anderen Geräten wird nicht verhindert. Zusätzlich gibt es aus Sicherheitsgründen einige Einschränkungen, wenn die Kommunikation vom Client mit den Standortsystemen über HTTP anstatt HTTPS erfolgt.  

         Wenn Sie Ihre Einstufung später revidieren, können Sie blockierte Clients wieder zulassen. Wenn Sie jedoch einen blockierten Intel AMT-basierten Client zulassen, der für AMT bereitgestellt wurde, während er blockiert war, müssen Sie zusätzliche Schritte ausführen, bevor bei diesem Computer wieder eine Out-of-Band-Verwaltung möglich ist.  

         Informationen hierzu finden Sie unter [Bestimmen, ob Clients blockiert werden sollen, in System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

    -   **Löschen erforderlicher PXE-Bereitstellungen**  

         Verwenden Sie diese Option, um alle erforderlichen PXE-Bereitstellungen für den ausgewählten Computer erneut bereitzustellen.  

         Informationen hierzu finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   **Verwalten der Clienteigenschaften**  

         Sie können die Ermittlungsdaten und Bereitstellungen für den Client anzeigen. Sie können außerdem alle Variablen konfigurieren, die von Tasksequenzen zum Bereitstellen eines Betriebssystems für das Gerät verwendet werden.  

    -   **Löschen des Clients**  

        > [!WARNING]  
        >  Löschen Sie einen Client nicht, wenn Sie den Configuration Manager-Client deinstallieren oder aus einer Sammlung entfernen möchten.  

         Mit der Aktion **Löschen** wird der Clientdatensatz manuell aus der Configuration Manager-Datenbank gelöscht. Normalerweise sollten Sie diese Aktion nicht ausführen, sofern dies nicht zur Problembehandlung erforderlich ist. Wenn Sie den Clientdatensatz löschen, während der Configuration Manager-Client weiterhin installiert ist und Kommunikation zwischen ihm und Configuration Manager erfolgt, wird der Clientdatensatz von der Frequenzermittlung neu erstellt und wieder in der Configuration Manager-Konsole angezeigt, obwohl der Clientverlauf sowie alle bisherigen Zuordnungen verloren gehen.  

        > [!NOTE]  
        >  Wenn Sie ein mobiles Gerät löschen, das von Configuration Manager angemeldet wurde, wird dadurch auch das ausgestellte PKI-Zertifikat gesperrt, und dieses Zertifikat wird auch dann vom Verwaltungspunkt zurückgewiesen, wenn die Zertifikatsperrliste nicht von IIS geprüft wird. Zertifikate auf Legacyclients bei mobilen Geräten werden nicht gesperrt, wenn Sie diese Clients löschen.  

         Informationen zum Deinstallieren des Clients finden Sie unter [Deinstallieren des Configuration Manager-Clients](#BKMK_UninstalClient).  

         Informationen dazu, wie Sie den Client einem neuen primären Standort zuweisen, finden Sie unter [Zuweisen von Clients zu einem Standort in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

         Konfigurieren Sie die Sammlungseigenschaften neu, um den Client aus einer Sammlung zu entfernen. Informationen hierzu finden Sie unter [Verwalten von Sammlungen in System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md).  

    -   **Zurücksetzen eines mobilen Geräts**  

         Sie können mobile Geräte zurücksetzen, die den betreffenden Befehl unterstützen.  

         Durch diese Aktion werden alle Daten auf den mobilen Geräten endgültig gelöscht. Hiervon sind auch die persönlichen Einstellungen und Daten betroffen. Normalerweise wird das mobile Gerät durch diese Aktion auf die Werkseinstellungen zurückgesetzt. Setzen Sie ein mobiles Gerät zurück, wenn Sie es nicht mehr als vertrauenswürdig einstufen, beispielsweise nach Verlust oder Diebstahl.  

        > [!TIP]  
        >  Lesen Sie die Dokumentation des Herstellers, um sich darüber zu informieren, wie ein Befehl zum Remotezurücksetzen vom Gerät verarbeitet wird.  

         Wenn Sie eine Anforderung zum Zurücksetzen senden, wird der Zurücksetzbefehl oft erst nach einer zeitlichen Verzögerung vom mobilen Gerät empfangen:  

        -   Wenn das mobile Gerät von Configuration Manager oder Windows Intune angemeldet wurde, empfängt der Client den Zurücksetzbefehl, sobald die Clientrichtlinie das nächste Mal heruntergeladen wird.  

        -   Wenn das mobile Gerät vom Exchange Server-Connector verwaltet wird, wird der Zurücksetzbefehl empfangen, wenn die nächste Synchronisierung mit Exchange erfolgt.  

         Sie können anhand der Spalte **Zurücksetzstatus** überwachen, wann der Zurücksetzbefehl vom mobilen Gerät empfangen wird. Sie können den Zurücksetzbefehl abbrechen, bis vom mobilen Gerät eine Zurücksetzbestätigung an Configuration Manager gesendet wird.  

    -   **Außerkraftsetzen eines mobilen Geräts**  

         Die Option **Außerkraftsetzen** wird nur von mobilen Geräten unterstützt, die mit Intune oder lokaler Verwaltung mobiler Geräte angemeldet werden.  

         Weitere Informationen finden Sie unter [Schützen Ihrer Daten mit Remotezurücksetzen, Remotesperre und Kennungszurücksetzung mit System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

    -   **Ändern des Besitzers eines Geräts**  

         Sie können den Besitz von Geräten in **Firma** oder **Persönlich** ändern, wenn ein Gerät in keine Domäne eingebunden ist und der Configuration Manager-Client nicht darauf installiert ist.  

         Sie können diesen Wert in Anwendungsanforderungen zum Steuern von Bereitstellungen verwenden und mit dieser Konfiguration auch die Menge der Inventurinformationen steuern, die von Geräten von Benutzern gesammelt werden.  

        Sie müssen zum Anzeigen des Besitz-Werts in der Geräteliste möglicherweise der Ansicht die Spalte hinzufügen, indem Sie mit der rechten Maustaste auf eine beliebige Spaltenüberschrift klicken und **Gerätebesitzer**auswählen.

         Weitere Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

##  <a name="a-namebkmkmanagingclientsdevicecollectionsnodea-manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Verwalten von Clients mithilfe des Knotens „Gerätesammlungen“  
 Verwenden Sie das folgende Verfahren und die folgende Tabelle, um Geräte in einer Sammlung im Arbeitsbereich **Bestand und Kompatibilität** mithilfe des Knotens **Gerätesammlungen** zu verwalten.  

 Viele der Clientverwaltungstasks, die Sie ausführen können, wenn Sie ein einzelnes Gerät oder mehrere Geräte aus dem Knoten **Geräte** ausgewählt haben, können auch auf der Sammlungsebene ausgeführt werden. Dies hat den Vorteil, dass die Verwaltungstasks automatisch bei allen qualifizierten Geräten in der Sammlung ausgeführt werden. Dies kann eine praktische Methode zum gleichzeitigen Verwalten mehrerer Clients sein. Allerdings können dabei zahlreiche Netzwerkpakete erstellt und die Prozessorauslastung des Standortservers erhöht werden.  

 Es gibt auch einige Clientverwaltungstasks, die nur auf der Sammlungsebene ausgeführt werden können. Sie finden diese Tasks in der folgenden Tabelle aufgelistet.  

 Bevor Sie Clientverwaltungstasks auf Sammlungsebene ausführen, berücksichtigen Sie, wie viele Geräte in der Sammlung enthalten sind, ob die Geräte nur über Netzwerkverbindungen mit niedriger Bandbreite verbunden sind, und wie lange es dauern wird, bis der Task für alle Geräte ausgeführt ist. Wenn Sie einen Clientverwaltungstask ausführen, können Sie ihn nicht mithilfe der Konsole beenden.  

#### <a name="to-manage-clients-from-the-device-collections-node"></a>So verwalten Sie Clients mithilfe des Knotens „Gerätesammlungen“  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**.  

3.  Wählen Sie eine Sammlung aus, und wählen Sie anschließend einen der folgenden Clientverwaltungstasks über das Menüband aus, oder indem Sie einen Rechtsklick auf der Sammlung ausführen:  

    -   **Überprüfen von Computern auf Schadsoftware und Herunterladen von Antischadsoftware-Definitionsdateien**  

         Informationen hierzu finden Sie unter [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md)  

    -   **Bereitstellen von Software, Konfigurationsbasislinien und Tasksequenzen**  

         Weitere Informationen zum Bereitstellen von Software und Konfigurationsbasislinien finden Sie unter:  

        -   [Deploy software updates in System Center Configuration Manager (Bereitstellen von Softwareupdates in System Center Configuration Manager)](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [Planen und Konfigurieren von Kompatibilitätseinstellungen in System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **Konfigurieren der Energieverwaltungseinstellungen**  

         Informationen hierzu finden Sie unter [Erstellen und Anwenden von Energiesparplänen in System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md). Energiesparpläne können nur mit Computern verwendet werden, auf denen Windows ausgeführt wird.  

    -   **Auffordern von Computern zum schnellstmöglichen Herunterladen der Richtlinie**  

         Verwenden Sie die Clientbenachrichtigung, um die ausgewählten Windows-Clients zum schnellstmöglichen Herunterladen der Computerrichtlinie außerhalb des konfigurierten Clientrichtlinien-Abrufintervalls aufzufordern.  

         Die Clientbenachrichtigungstasks werden im Arbeitsbereich **Überwachung** unter dem Knoten **Clientvorgänge** angezeigt.  

##  <a name="a-namebkmkclientcachea-configure-the-client-cache-for-configuration-manager-clients"></a><a name="BKMK_ClientCache"></a> Konfigurieren des Clientcaches für Configuration Manager-Clients  
 Sie können den Speicherort sowie die Größe des Speicherplatzes konfigurieren, die von Windows-Configuration Manager-Clients zum Speichern temporärer Dateien und zum Installieren von Anwendungen und Programmen verwendet werden. Der Clientcache kann auch von Softwareupdates verwendet werden. Softwareupdates werden jedoch nicht von der konfigurierten Cache-Größe eingeschränkt, und es wird stets ein Herunterladen in den Cache versucht. Die Einstellungen des Clientcaches können beim manuellen Installieren des Configuration Manager-Clients, bei Verwendung der Clientpushinstallation oder nach der Installation des Clients konfiguriert werden.

In Configuration Manager Version 1606 können Sie die Größe des Cacheordners mithilfe von Clienteinstellungen in der Configuration Manager-Konsole angeben.   

 Der Standardspeicherort für den Configuration Manager-Clientcache ist %*windir*%\ccmcache, und der Standardspeicherplatz auf dem Datenträger beträgt 5120 MB.  

> [!IMPORTANT]  
>  Verschlüsseln Sie den Ordner für den Clientcache nicht. Das Herunterladen von Inhalt in einen verschlüsselten Ordner ist nicht möglich.  

### <a name="about-client-cache"></a>Informationen zum Clientcache  

Der Configuration Manager-Client lädt den Inhalt für erforderliche Software unmittelbar nach Erhalt der Bereitstellung herunter, führt ihn jedoch erst zum geplanten Bereitstellungszeitpunkt aus. Zum geplanten Zeitpunkt überprüft der Configuration Manager-Client, ob der Inhalt im Cache verfügbar ist. Wenn Inhalte im Cache verfügbar sind und in der richtigen Version vorliegen, werden grundsätzlich diese Cacheinhalte verwendet. Wenn allerdings die erforderliche Version der Inhalte geändert wurde oder die Inhalte gelöscht wurden, um das Einstellen eines anderen Pakets zu ermöglichen, werden die Inhalte erneut in den Cache heruntergeladen.  

Wenn der Client versucht, Inhalt für ein Programm oder eine Anwendung herunterzuladen, dessen Größe die Cachegröße überschreitet, tritt bei der Bereitstellung wegen unzureichender Cachegröße ein Fehler auf, und Configuration Manager generiert die Statusmeldungs-ID 10050. Wird die Cachegröße später erhöht, unterscheidet sich das Verhalten zum erneuten Herunterladen bei erforderlichen Programmen und erforderlichen Anwendungen:  

-   Erforderliches Programm: Es wird nicht automatisch erneut versucht, die Inhalte herunterzuladen. Sie müssen das Paket und das Programm erneut auf dem Client bereitstellen.  
-   Erforderliche Anwendung: Da die Bereitstellung von Anwendungen zustandsbasiert ist, wird beim nächsten Herunterladen der Clientrichtlinie durch den Client automatisch erneut versucht, die Inhalte herunterzuladen.  

Wenn versucht wird, ein Paket herunterzuladen, dessen Größe die Cachegröße unterschreitet, der Cache jedoch derzeit voll ist, werden Bereitstellungsversuche für alle erforderlichen Bereitstellungen so lange wiederholt, bis ausreichend Cachespeicher verfügbar ist oder bis das Zeitlimit bzw. die maximale Anzahl von Wiederholungen erreicht ist. Wird die Cachegröße später erweitert, wird vom Configuration Manager-Client im nächsten Wiederholungsintervall erneut versucht, das Paket herunterzuladen. Der Client startet alle vier Stunden einen neuen Versuch, um die Inhalte herunterzuladen. Maximal werden 18 Wiederholungen ausgeführt.  

Cacheinhalte werden nicht automatisch gelöscht. Sie verbleiben nach der Verwendung der Inhalte durch den Client mindestens einen Tag lang im Cache. Wenn Sie die Paketeigenschaften so konfigurieren, dass Inhalte dauerhaft im Clientcache gespeichert werden, werden die Paketinhalte nicht automatisch aus dem Cache gelöscht. Wenn der Speicherplatz des Clientcaches mit Paketen belegt ist, die in den letzten 24 Stunden heruntergeladen wurden, und weitere Pakete heruntergeladen werden müssen, können Sie entweder die Cachegröße erweitern oder die Option zum Löschen von persistent im Cache gespeicherten Inhalten auswählen.  

 Gehen Sie wie folgt vor, um den Clientcache während der manuellen Clientinstallation oder nach der Installation des Clients zu konfigurieren.  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>So konfigurieren Sie den Clientcache während der manuellen Clientinstallation  

Führen Sie den Befehl CCMSetup.exe vom Installationsquellspeicherort aus. Geben Sie dabei nach Bedarf die folgenden Eigenschaften durch Leerzeichen getrennt an:  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Verwenden Sie für Version 1606 die Einstellungen für die Cachegröße, die in den **Clienteinstellungen** in der Configuration Manager-Konsole statt in SMSCACHESIZE verfügbar sind. Weitere Informationen finden Sie unter [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md#client-cache-settings)

Weitere Informationen zur Verwendungsweise dieser Befehlszeileneigenschaften für „CCMSetup.exe“ finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>So konfigurieren Sie den Clientcacheordner während der Installation von Clients mithilfe der Clientpushinstallation  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.  

3.  Wählen Sie in der Liste **Standorte** den Standort aus, für den Sie die automatische standortweite Clientpushinstallation konfigurieren möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Clientinstallationseinstellungen**, und klicken Sie dann auf die Registerkarte **Installationseigenschaften**.  

5.  Geben Sie auf der Registerkarte **Installationseigenschaften** nach Bedarf die folgenden Eigenschaften durch Leerzeichen getrennt an:  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Verwenden Sie für Version 1606 die Einstellungen für die Cachegröße, die in den **Clienteinstellungen** in der Configuration Manager-Konsole statt in SMSCACHESIZE verfügbar sind. Weitere Informationen finden Sie unter [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md#client-cache-settings)

       Weitere Informationen zur Verwendungsweise dieser Befehlszeileneigenschaften für „CCMSetup.exe“ finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

6.  Klicken Sie auf **OK** um die angegebenen Eigenschaften zu speichern.  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>So konfigurieren Sie den Clientcacheordner auf dem Clientcomputer  

1.  Doppelklicken Sie in der Systemsteuerung des Clientcomputers auf **Configuration Manager** , um die Eigenschaften anzuzeigen.  

2.  Klicken Sie auf die Registerkarte **Cache** .  

3.  Geben Sie an, wie viel Speicherplatz für den Clientcache reserviert werden soll.  

4.  Zum Ändern des Speicherorts des Clientcacheordners klicken Sie auf **Ort ändern**, und geben Sie dann den neuen Speicherort an. Der Standardspeicherort lautet *%windir%*\ccmcache.  

5.  Wenn Sie alle derzeit im Clientcacheordner gespeicherten Dateien löschen möchten, klicken Sie auf **Dateien löschen**.  

6.  Klicken Sie auf **OK** , um die **Configuration Manager-Eigenschaften**zu schließen.  

### <a name="to-configure-client-cache-size-in-client-settings"></a>So konfigurieren Sie die Cachegröße des Clients in den Clienteinstellungen

Ab Version 1606 können Sie die Größe des Clientcacheordners anpassen, ohne den Client neu installieren zu müssen. Konfigurieren Sie dazu die Cachegröße des Clients in der Configuration Manager-Konsole über die Clienteinstellungen.  

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung**  >  **Clienteinstellungen**.

2. Führen Sie auf **Clientstandardeinstellungen** einen Doppelklick aus.
  Sie können auch benutzerdefinierte Einstellungen erstellen, um die Cachegröße gezielter anzuwenden. Weitere Informationen zu standardmäßigen und benutzerdefinierten Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

 3. Klicken Sie auf **Einstellungen für Clientcache** , und wählen Sie **Ja** für **Clientcachegröße konfigurieren**aus.

 4. Passen Sie die maximale Cachegröße entweder über die Einstellung **MB** oder die Einstellung **Prozentsatz des Datenträgers**an. Der Cache wird immer an die kleinere Größe angepasst.

 5. Klicken Sie auf **OK**.

    Der Configuration Manager-Client wird die Größe des Caches beim nächsten Download der Clientrichtlinie mit diesen Einstellungen konfigurieren.

##  <a name="a-namebkmkuninstalclienta-uninstall-the-configuration-manager-client"></a><a name="BKMK_UninstalClient"></a> Deinstallieren des Configuration Manager-Clients  
 Sie können die Windows-Configuration Manager-Clientsoftware mithilfe von **CCMSetup.exe** mit der Eigenschaft **/Uninstall** von einem Computer deinstallieren. Führen Sie CCMSetup.exe auf einem einzelnen Computer über die Eingabeaufforderung aus, oder stellen Sie ein Paket und ein Programm bereit, um den Client von einer Sammlung von Computern zu deinstallieren.  

> [!WARNING]  
>  Sie können den Configuration Manager-Client nicht von einem mobilen Gerät aus deinstallieren. Wenn die Deinstallation des Configuration Manager-Clients von einem mobilen Gerät aus erforderlich ist, müssen Sie das Gerät zurücksetzen. Dadurch werden alle Daten auf dem mobilen Gerät gelöscht.  

 Mithilfe des folgenden Verfahrens können Sie den Configuration Manager-Client von Macintosh-Computern deinstallieren.  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>So deinstallieren Sie den Configuration Manager-Client mithilfe der Eingabeaufforderung  

1.  Öffnen Sie eine Windows-Eingabeaufforderung, und ändern Sie den Ordner in den Speicherort von „CCMSetup.exe“.  

2.  Geben Sie **Ccmsetup.exe /uninstall**ein, und drücken Sie die **Eingabetaste.**  

> [!NOTE]  
>  Die Deinstallation erfolgt im Hintergrund. Es werden keine Ergebnisse auf dem Bildschirm angezeigt. Zur Überprüfung des Erfolgs der Clientdeinstallation untersuchen Sie die Protokolldatei **CCMSetup.log** im Ordner *%windir%\ccmsetup* auf dem Clientcomputer.  

##  <a name="a-namebkmkconflictingrecordsa-manage-conflicting-records-for-configuration-manager-clients"></a><a name="BKMK_ConflictingRecords"></a> Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients  
 Configuration Manager identifiziert mithilfe der Hardware-ID Clients, bei denen es sich um Duplikate handeln könnte. Sie werden über in Konflikt stehende Datensätze informiert. Wenn Sie z.B. einen Computer erneut installieren, bleibt die Hardware-ID unverändert, während die von Configuration Manager verwendete GUID sich ändern kann.  

 Wenn ein Konflikt von Configuration Manager mithilfe der Windows-Authentifizierung des Computerkontos oder mithilfe eines PKI-Zertifikats aus einer vertrauenswürdigen Quelle aufgelöst werden kann, geschieht dies automatisch. Wenn Configuration Manager den Konflikt dagegen nicht auflösen kann, wird eine Hierarchieeinstellung verwendet, um entweder beim Erkennen doppelter Hardware-IDs automatisch neue Datensätze zu erstellen (dies ist die Standardeinstellung) oder die Entscheidung über eine Zusammenführung, Sperrung oder Erstellung neuer Clientdatensätze Ihnen zu überlassen. Wenn Sie sich für das manuelle Verwalten duplizierter Datensätze entscheiden, müssen Sie die in Konflikt stehenden Datensätze mithilfe der Configuration Manager-Konsole manuell bearbeiten, um den Konflikt aufzulösen.  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>So ändern Sie die Hierarchieeinstellung zum Verwalten von in Konflikt stehenden Datensätzen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.  

3.  Klicken Sie in der Gruppe **Standorte** auf **Hierarchieeinstellungen**, und klicken Sie dann auf die Registerkarte **Clientgenehmigung und in Konflikt stehende Datensätze** .  

4.  Klicken Sie entweder auf **In Konflikt stehende Datensätze automatisch auflösen** , um in Konflikt stehende Datensätze automatisch zusammenzuführen, oder klicken Sie auf **In Konflikt stehende Datensätze manuell bearbeiten**. Klicken Sie dann auf **OK**.  

    > [!NOTE]  
    >  Wenn ein Konflikt von Configuration Manager mithilfe des Computerkontos oder eines PKI-Zertifikats aufgelöst werden kann, wird diese Einstellung ignoriert, und der Konflikt wird automatisch aufgelöst.  

#### <a name="to-manually-resolve-conflicting-records"></a>So bearbeiten Sie in Konflikt stehende Datensätze manuell  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Systemstatus**, und klicken Sie dann auf **In Konflikt stehende Datensätze**.  

3.  Wählen Sie im Ergebnisbereich mindestens einen in Konflikt stehenden Datensatz aus, und klicken Sie dann auf **In Konflikt stehende Datensätze**.  

4.  Wählen Sie im Dialogfeld **In Konflikt stehende Datensätze** eine der folgenden Optionen aus, und klicken Sie dann auf **OK**:  

    -   **Zusammenführen** : Hiermit kombinieren Sie den neu erkannten Datensatz mit dem vorhandenen Datensatz, und erstellen einen einheitlichen Datensatz.  

    -   **Neu** : Hiermit erstellen Sie einen neuen Datensatz für den in Konflikt stehenden Clientdatensatz.  

    -   **Sperren** : Hiermit erstellen Sie einen neuen Datensatz für den in Konflikt stehenden Clientdatensatz, markieren ihn jedoch als gesperrt.  

## <a name="manage-duplicate-hardware-identifiers"></a>Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients
Ab Configuration Manager Version 1610 können Sie eine Liste der Hardware-IDs angeben, die Configuration Manager für den PXE-Start und die Clientregistrierung ignoriert. Es gibt zwei häufige Probleme, die dadurch behandelt werden können.

1. Viele neue Geräte wie Surface Pro 3 haben keinen integrierten Ethernet-Anschluss. Ein USB-zu-Ethernet-Adapter wird im Allgemeinen verwendet, um eine Kabelverbindung für die Bereitstellung des Betriebssystems einzurichten. Allerdings handelt es sich hierbei aus Kostengründen und Gründen der allgemeinen Nutzbarkeit oft um gemeinsame Adapter. Nachdem die MAC-Adresse des Adapters zur Identifizierung des Geräts verwendet wird, ist es problematisch, den Adapter ohne zusätzliche Aktionen eines Administrators zwischen den Bereitstellungen wiederzuverwenden. Sie können nun in Configuration Manager mit Version 1610 von Current Branch die MAC-Adresse dieses Adapters ausschließen, damit er in diesem Szenario einfach wiederverwendet werden kann.
2. Während es sich bei SMBIOS-ID um eine eindeutige Hardware-ID handeln sollte, werden einige spezielle Hardwaregeräte mit doppelten IDs gebaut. Obwohl es nicht so häufig ist wie das oben beschriebene USB-zu-Ethernet-Adapter-Szenario, kann die Liste von Hardware-IDs ebenfalls dazu verwendet werden, das Problem zu behandeln.

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>So fügen Sie von Hardware-IDs hinzu, die Configuration Manager ignorieren soll  
1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Standorte**.
2. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.
3. Klicken Sie auf die Registerkarte **Clientgenehmigung und in Konflikt stehende Datensätze**.
4. Klicken Sie im Abschnitt **Doppelte Hardware-IDs** auf **Hinzufügen**, um neue Hardware-IDs hinzuzufügen.

##  <a name="a-namebkmkpolicyretrievala-initiate-policy-retrieval-for-a-configuration-manager-client"></a><a name="BKMK_PolicyRetrieval"></a> Initiieren des Richtlinienabrufs für einen Configuration Manager-Client  
 Clientrichtlinien werden von Windows-Configuration Manager-Clients nach einem als Clienteinstellung konfigurierten Zeitplan heruntergeladen. Es kann jedoch vorkommen, dass Sie Richtlinien ad hoc vom Client abrufen möchten, z.B. zur Problembehandlung oder während eines Tests.  

 Gehen Sie wie folgt vor, um Richtlinien außerhalb des geplanten Abrufintervalls ad hoc vom Client abzurufen, indem Sie entweder im Configuration Manager-Client die Registerkarte **Aktionen** verwenden oder ein Skript auf dem Computer ausführen. Sie müssen auf dem Clientcomputer mit lokalen Administratorrechten angemeldet sein, um diese Prozeduren ausführen zu können.  

> [!NOTE]  
>  Sie können die Clientbenachrichtigung verwenden, um den Clientrichtlinienabruf außerhalb des geplanten Clientrichtlinien-Abrufintervalls zu initiieren.  
>   
>  Sie können Clients verwalten, auf denen Linux und UNIX ausgeführt wird. Weitere Informationen zum Richtlinienabruf für Clients, auf denen Linux und UNIX ausgeführt wird, finden Sie unter [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU).  

#### <a name="to-initiate-client-policy-retrieval-by-using-client-notification"></a>So lösen Sie den Clientrichtlinienabruf mithilfe der Clientbenachrichtigung aus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**.  

3.  Wählen Sie die Gerätesammlung mit den Computern aus, von denen die Richtlinie heruntergeladen werden soll, und klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Sammlungen** auf **Clientbenachrichtigung** und dann auf **Computerrichtlinie herunterladen**.  

    > [!NOTE]  
    >  Sie können die Clientbenachrichtigung auch verwenden, um den Richtlinienabruf für ein oder mehrere ausgewählte Geräte zu initiieren, die in einem Knoten für eine temporäre Sammlung unter dem Knoten **Geräte** angezeigt werden.  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-the-actions-tab-on-the-configuration-manager-client"></a>So initiieren Sie den Clientrichtlinienabruf manuell im Configuration Manager-Client auf der Registerkarte „Aktionen“  

1.  Wählen Sie in der Systemsteuerung des Computers **Configuration Manager** aus.  

2.  Klicken Sie auf die Registerkarte **Aktionen** .  

3.  Klicken Sie auf **Computerrichtlinienabruf und Auswertungszyklus**, um die Computerrichtlinie zu initiieren, und klicken Sie anschließend auf **Jetzt ausführen**.  

4.  Klicken Sie zum Bestätigen der Eingabeaufforderung auf **OK** .  

5.  Wiederholen Sie die Schritte 3 und 4 für alle weiteren erforderlichen Aktionen, wie z.B. den **Benutzerrichtlinienabruf und Auswertungszyklus** für Benutzerclienteinstellungen.  

6.  Klicken Sie auf **OK** , um die **Configuration Manager-Eigenschaften**zu schließen.  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-a-script"></a>So initiieren Sie den Clientrichtlinienabruf manuell mithilfe eines Skripts  

1.  Öffnen Sie einen Text-Editor, z. B. Notepad.  

2.  Kopieren Sie Folgendes, und fügen Sie es in die Datei ein:  

    ```  
    on error resume next  

    dim oCPAppletMgr 'Control Applet manager object.  
    dim oClientAction 'Individual client action.  
    dim oClientActions 'A collection of client actions.  

    'Get the Control Panel manager object.  
    set  oCPAppletMgr=CreateObject("CPApplet.CPAppletMgr")  
    if err.number <> 0 then  
        Wscript.echo "Couldn't create control panel application manager"  
        WScript.Quit  
    end if  

    'Get a collection of actions.  
    set oClientActions=oCPAppletMgr.GetClientActions  
    if err.number<>0 then  
        wscript.echo "Couldn't get the client actions"  
        set oCPAppletMgr=nothing  
        WScript.Quit  
    end if  

    'Display each client action name and perform it.  
    For Each oClientAction In oClientActions  

        if oClientAction.Name = "Request & Evaluate Machine Policy" then  
            wscript.echo "Performing action " + oClientAction.Name   
            oClientAction.PerformAction  
        end if  
    next  

    set oClientActions=nothing  
    set oCPAppletMgr=nothing  
    ```  

3.  Speichern Sie die Datei mit der Erweiterung „.vbs“.  

4.  Führen Sie die Datei mithilfe einer der folgenden Methoden auf dem Clientcomputer aus:  

    -   Wechseln Sie mithilfe von Windows Explorer zu der Datei, und doppelklicken Sie auf die Skriptdatei.  

    -   Öffnen Sie eine Eingabeaufforderung, und geben Sie Folgendes ein: **cscript &lt;Pfad\Dateiname.vbs>**.  

5.  Klicken Sie im Dialogfeld **Windows Script Host** auf **OK** .  



<!--HONumber=Dec16_HO3-->


