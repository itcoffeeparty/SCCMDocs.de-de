---
title: Verwalten von Clients
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Clients in System Center Configuration Manager verwalten.
ms.date: 12/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 623d7b6a048b7728e40adb3655dc1017408fb1d7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>Verwalten von Clients in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn der Konfigurations-Manager-Client auf einem Gerät installiert und erfolgreich einem Standort zugewiesen wurde, wird Ihnen das Gerät im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Geräte** angezeigt sowie in mindestens einer Sammlung im Knoten **Gerätesammlungen**. Wenn Sie das Gerät oder eine Sammlung auswählen, können Sie verschiedene Verwaltungsvorgänge durchführen. Es gibt jedoch andere Möglichkeiten, um den Client zu verwalten. Hierfür können andere Arbeitsbereiche in der Konsole oder Aufgaben außerhalb der Konsole verwendet werden.  

> [!NOTE]  
>  Wenn der Konfigurations-Manager-Client installiert wurde, aber noch nicht erfolgreich einem Standort zugewiesen wurde, wird dieser möglicherweise nicht in der Konsole angezeigt. Nachdem der Client einem Standort zugewiesen wurde, aktualisieren Sie die Sammlungsmitgliedschaft und die Konsolenansicht.  
>   
>  Es ist außerdem möglich, dass ein Gerät in der Konsole angezeigt wird, wenn der Configuration Manager-Client nicht installiert ist. Dieses Verhalten kann auftreten, wenn das Gerät ermittelt, aber der Client nicht installiert und zugewiesen wurde. 
>
> Bei mobilen Geräten, die mithilfe des Exchange Server-Connectors verwaltet werden sowie bei Geräten, die in Microsoft Intune registriert wurden, wird der Konfigurations-Manager-Client nicht installiert.  
>   
>  Verwenden Sie die Spalte **Client** in der Configuration Manager-Konsole, um zu bestimmten, ob der Client installiert ist, damit Sie diesen über die Konsole verwalten können.  

##  <a name="BKMK_ManagingClients_DevicesNode"></a> Verwalten von Clients mithilfe des Knotens „Geräte“  

Je nach Typ des Geräts sind einige dieser Optionen möglicherweise nicht verfügbar.  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Konformität** >  **Geräte** aus.  

3.  Wählen Sie ein oder mehrere Geräte aus, und wählen Sie dann einen dieser Clientverwaltungstasks aus dem Menüband oder per Rechtsklick auf das Gerät aus:  

    -   **Verwalten von Informationen zur Affinität zwischen Benutzer und Gerät**  

         Konfigurieren Sie die Zuordnungen zwischen Benutzern und Geräten, sodass Sie Benutzern Software effizient bereitstellen können.  

         Informationen hierzu finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

    -   **Hinzufügen des Geräts zu einer neuen oder vorhandenen Sammlung**  

         Fügen Sie das Gerät einer Sammlung mit einer direkten Regel hinzu.  

    -   **Installieren und erneutes Installieren des Clients mithilfe von Clientpushinstallation**  

         Installieren Sie den Konfigurations-Manager-Client, und installieren Sie ihn dann erneut, um ihn zu reparieren oder zu konfigurieren. Diese Option enthält Konfigurationseinstellungen und client.msi-Eigenschaften für den Standort. Diese Einstellungen legen Sie für die Clientpushinstallation fest.  

        > [!TIP]  
        >  Es gibt viele verschiedene Möglichkeiten, den Configuration Manager-Client zu installieren (und erneut zu installieren). Die Clientpushinstallation ist eine praktische Methode zur Clientinstallation, da sie mithilfe der Konsole ausgeführt werden kann. Allerdings hat diese Installationsmethode zahlreiche Abhängigkeiten und ist nicht für alle Umgebungen geeignet. Weitere Informationen zu den Abhängigkeiten finden Sie unter [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) (Voraussetzungen für die Bereitstellung von Clients auf Windows-PCs in System Center Configuration Manager). Weitere Informationen zu den anderen Clientinstallationsmethoden finden Sie unter [Clientinstallationsmethoden in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

         Informationen finden Sie auch unter [Installieren von Configuration Manager-Clients mittels Clientpush](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Neuzuweisen des Standorts**  

         Weisen Sie bei Bedarf einen oder mehrere Clients, einschließlich verwalteter mobiler Geräte, einem anderen primären Standort in der Hierarchie neu zu. Clients können einzeln neu zugewiesen werden. Sie können aber auch mehrere Clients auswählen und sie gleichzeitig einem neuen Standort neu zuweisen.  

    -   **Remotes Verwalten des Clients**  

         Führen Sie Ressourcen-Explorer aus, um die Informationen zur Hardware- und Softwareinventur eines Windows-Clients anzuzeigen. Verwalten Sie das Gerät remote, indem Sie die Remotesteuerung, die Remoteunterstützung oder Remotedesktop verwenden.  

         Weitere Informationen finden Sie unter [Anzeigen des Hardwareinventars mit Ressourcen-Explorer](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) und [Anzeigen des Softwareinventars mit Ressourcen-Explorer](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

         Weitere Informationen finden Sie unter [Remoteverwaltung eines Windows-Clientcomputers](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

    -   **Genehmigen eines Clients**  

         Wenn die Kommunikation zwischen Client und Standortsystemen über HTTP erfolgt und ein selbstsigniertes Zertifikat verwendet wird, müssen Sie die Clients genehmigen, um sie als vertrauenswürdige Computer zu identifizieren. Standardmäßig werden Clients aus dem gleichen Active Directory-Gesamtverzeichnis sowie aus vertrauenswürdigen Gesamtverzeichnissen von der Standortkonfiguration automatisch genehmigt, sodass Sie nicht jeden Client manuell genehmigen müssen. Sie müssen jedoch Arbeitsgruppencomputer und andere Computer, die Sie als vertrauenswürdig einstufen, die jedoch nicht genehmigt sind, manuell genehmigen.  

        > [!WARNING]  
        >  Bei nicht genehmigten Clients sind einige Verwaltungsfunktionen möglicherweise nicht ausführbar. Dieses Szenario wird jedoch für Configuration Manager nicht unterstützt.  

         Sie müssen keine Clients genehmigen, deren Kommunikation mit Standortsystemen immer über HTTPS erfolgt, und auch keine Clients, von denen zur Kommunikation mit Standortsystemen über HTTP ein PKI-Zertifikat verwendet wird. Von diesen Clients wird mithilfe der PKI-Zertifikate eine Vertrauensstellung hergestellt.  

    -   **Blockieren und Zulassen eines Clients**  

         Blockieren Sie einen Client, den Sie nicht mehr als vertrauenswürdig einstufen. Durch das Blockieren wird verhindert, dass der Client Richtlinien empfängt und dass die Standortsysteme mit diesem kommunizieren.  

        > [!WARNING]  
        >  Durch das Blockieren eines Clients wird nur die Kommunikation vom Client an die Configuration Manager-Standortsysteme verhindert. Die Kommunikation mit anderen Geräten wird nicht verhindert. Zusätzlich gibt es aus Sicherheitsgründen einige Einschränkungen, wenn die Kommunikation vom Client mit den Standortsystemen über HTTP anstatt HTTPS erfolgt.  

         Sie können die Blockierung blockierter Clients wieder aufheben. 

         Informationen hierzu finden Sie unter [Bestimmen, ob Clients blockiert werden sollen, in System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

    -   **Löschen erforderlicher PXE-Bereitstellungen**  

         Stellen Sie die erforderlichen PXE-Bereitstellungen für den Computer erneut bereit.  

         Informationen hierzu finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   **Verwalten der Clienteigenschaften**  

         Überprüfen Sie die Ermittlungsdaten und Bereitstellungen für den Client. Sie können außerdem Variablen konfigurieren, die von Tasksequenzen zum Bereitstellen eines Betriebssystems für das Gerät verwendet werden.  

    -   **Löschen des Clients**  

        > [!WARNING]  
        >  Löschen Sie einen Client nicht, wenn Sie den Configuration Manager-Client deinstallieren oder aus einer Sammlung entfernen möchten.  

         Mit der Aktion **Löschen** wird der Clientdatensatz manuell aus der Configuration Manager-Datenbank gelöscht. Normalerweise sollten Sie diese Aktion nicht ausführen, sofern dies nicht zur Problembehandlung erforderlich ist. Wenn Sie den Clientdatensatz löschen, der Client aber weiterhin installiert ist und mit dem Standort kommuniziert, erstellt die Frequenzermittlung den Clientdatensatz erneut. Der Clientdatensatz wird erneut in der Configuration Manager-Konsole angezeigt, obwohl der Clientverlauf und bisherige Zuordnungen nicht mehr vorhanden sind.  

        > [!NOTE]  
        >  Wenn Sie ein mobiles Gerät löschen, das von Configuration Manager angemeldet wurde, wird dadurch auch das ausgestellte PKI-Zertifikat gesperrt, und dieses Zertifikat wird auch dann vom Verwaltungspunkt zurückgewiesen, wenn die Zertifikatsperrliste nicht von IIS geprüft wird. Zertifikate auf Legacyclients bei mobilen Geräten werden nicht gesperrt, wenn Sie diese Clients löschen.  

         Informationen zum Deinstallieren des Clients finden Sie unter [Deinstallieren des Configuration Manager-Clients](#BKMK_UninstalClient).  

         Informationen dazu, wie Sie den Client einem neuen primären Standort zuweisen, finden Sie unter [Zuweisen von Clients zu einem Standort in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

         Konfigurieren Sie die Sammlungseigenschaften neu, um den Client aus einer Sammlung zu entfernen. Informationen hierzu finden Sie unter [Verwalten von Sammlungen in System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md).  

    -   **Zurücksetzen eines mobilen Geräts**  

         Sie können mobile Geräte zurücksetzen, die den betreffenden Befehl unterstützen.  

         Durch diese Aktion werden alle Daten auf den mobilen Geräten endgültig gelöscht. Hiervon sind auch die persönlichen Einstellungen und Daten betroffen. Normalerweise wird das mobile Gerät durch diese Aktion auf die Werkseinstellungen zurückgesetzt. Setzen Sie ein mobiles Gerät zurück, wenn dieses nicht mehr als vertrauenswürdig eingestuft wird. Dies wird beispielsweise empfohlen, wenn das Gerät verloren geht oder gestohlen wird.  

        > [!TIP]  
        >  Lesen Sie die Dokumentation des Herstellers, um sich darüber zu informieren, wie ein Befehl zum Remotezurücksetzen vom Gerät verarbeitet wird.  

         Der Zurücksetzungsbefehl wird oft erst nach einer zeitlichen Verzögerung vom mobilen Gerät empfangen:  

        -   Wenn das mobile Gerät von Configuration Manager oder Windows Intune registriert wurde, empfängt der Client den Befehl, sobald die Clientrichtlinie das nächste Mal heruntergeladen wird.  

        -   Wenn das mobile Gerät vom Exchange Server-Connector verwaltet wird, wird der Befehl empfangen, wenn die nächste Synchronisierung mit Exchange erfolgt.  

         Sie können anhand der Spalte **Zurücksetzungsstatus** überwachen, wann der Zurücksetzungsbefehl vom Gerät empfangen wird. Sie können den Zurücksetzungsbefehl abbrechen, bis vom Gerät eine Zurücksetzungsbestätigung an Configuration Manager gesendet wird.  

    -   **Außerkraftsetzen eines mobilen Geräts**  

         Die Option **Außerkraftsetzen** wird nur von mobilen Geräten unterstützt, die mit Microsoft Intune oder mit der lokalen Verwaltung mobiler Geräte angemeldet werden.  

         Weitere Informationen finden Sie unter [Schützen Ihrer Daten mit Remotezurücksetzen, Remotesperre und Kennungszurücksetzung mit System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

    -   **Ändern des Besitzers eines Geräts**  

         Wenn ein Gerät nicht mit einer Domäne verknüpft ist oder über eine Installation des Konfigurations-Manager-Clients verfügt, verwenden Sie diese Option, um den Besitz von **Unternehmen** in **Persönlich** zu ändern.  

         Sie können diesen Wert in Anwendungsanforderungen zum Steuern von Bereitstellungen verwenden und auch die Menge der Inventurinformationen steuern, die von Geräten von Benutzern gesammelt werden.  

        Möglicherweise müssen Sie der Ansicht die Spalte **Gerätebesitzer** hinzufügen, indem Sie mit der rechten Maustaste auf eine beliebige Spaltenüberschrift klicken und sie auswählen.

         Weitere Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

##  <a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Verwalten von Clients mithilfe des Knotens „Gerätesammlungen“  
  Viele der Aufgaben, die im Knoten **Geräte** für Geräte verfügbar sind, sind ebenfalls für Sammlungen verfügbar. Die Konsole führt den Vorgang automatisch für alle qualifizierten Geräte in der Sammlung aus. Wenn eine Aktion für eine gesamte Sammlung ausgeführt wird, werden zusätzliche Netzwerkpakete generiert und die CPU-Nutzung auf dem Standortserver steigt.  

  Beachten Sie Folgendes, bevor Sie Aufgaben auf Sammlungsebene ausführen. Nach dem Start kann der Task nicht mehr in der Konsole beendet werden. 
 - Wie viele Geräte befinden sich in der Sammlung?
 - Sind die Geräte über Netzwerkverbindungen mit geringer Bandbreite verbunden?
 - Wie viel Zeit muss aufgewendet werde, um diese Aufgabe für alle Geräte auszuführen?

#### <a name="to-manage-clients-from-the-device-collections-node"></a>So verwalten Sie Clients mithilfe des Knotens „Gerätesammlungen“  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Konformität** > **Gerätesammlungen**.  

3.  Wählen Sie eine Sammlung aus, und wählen Sie anschließend einen der folgenden Clientverwaltungstasks über das Menüband oder per Rechtsklick auf die Sammlung aus. Diese Tasks zur Clientverwaltung können *nur* auf Sammlungsebene ausgeführt werden.  

    -   **Überprüfen von Computern auf Schadsoftware und Herunterladen von Antischadsoftware-Definitionsdateien**  

         Informationen hierzu finden Sie unter [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md)  

    -   **Bereitstellen von Software, Konfigurationsbasislinien und Tasksequenzen**  

         Siehe:  

        -   [Deploy software updates in System Center Configuration Manager (Bereitstellen von Softwareupdates in System Center Configuration Manager)](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [Planen und Konfigurieren von Kompatibilitätseinstellungen in System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **Konfigurieren der Energieverwaltungseinstellungen**  

         Informationen hierzu finden Sie unter [Erstellen und Anwenden von Energiesparplänen in System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md). Energiesparpläne können nur mit Computern verwendet werden, auf denen Windows ausgeführt wird.  

    -   **Auffordern von Computern zum schnellstmöglichen Herunterladen der Richtlinie**  

         Verwenden Sie die Clientbenachrichtigung, um die ausgewählten Windows-Clients zum schnellstmöglichen Herunterladen der Computerrichtlinie außerhalb des Clientrichtlinien-Abrufintervalls aufzufordern.  

         Die Clientbenachrichtigungstasks werden im Arbeitsbereich **Überwachung** unter dem Knoten **Clientvorgänge** angezeigt.  


## <a name="restart-clients"></a>Neustarten von Clients
Ab Version 1710 können Sie die Configuration Manager-Konsole verwenden, um Clients zu identifizieren, für die ein Neustart erforderlich ist. Verwenden Sie eine Aktion zur Clientbenachrichtigung, um diese neu zu starten.

> [!Tip]
> Sie müssen die Clients ebenfalls auf Version 1710 upgraden, damit diese Funktion verwendet werden kann. Es wird empfohlen, automatische Clientupgrades zu aktivieren, damit Ihre Clients mit minimalem Verwaltungsaufwand auf dem neuesten Stand bleiben. Weitere Informationen finden Sie unter [Verwenden des automatischen Clientupgrades](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).

Wechseln Sie zum Arbeitsbereich **Bestand und Kompatibilität** in der Configuration Manager-Konsole, und klicken Sie auf den Knoten **Geräte**, um Geräte zu identifizieren, für die ein Neustart aussteht. Zeigen Sie dann im Bereich „Details“ den Status für jedes Gerät in einer neuen Spalte namens **Neustart ausstehend** an. Jedes Gerät besitzt mindestens einen der folgenden Werte: 
 - **Nein:** Es steht kein Neustart aus.
 - **Configuration Manager:** Dieser Wert stammt aus der Koordinierungskomponente für den Neustart des Clients (RebootCoordinator.log).
 - **Datei umbenennen:** Dieser Wert stammt aus einem Bericht von Windows für einen ausstehenden Umbenennungsvorgang für eine Datei (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations).
 - **Windows Update:** Dieser Wert stammt vom Windows Update-Agent, der meldet, dass ein ausstehender Neustart für mindestens ein Update erforderlich ist (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired).
 - **Feature hinzufügen oder entfernen:** Dieser Wert stammt von einem komponentenbasierten Windows-Dienst und gibt an, dass das Hinzufügen oder Entfernen eines Windows-Features einen Neustart erfordert (HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pending).

**So erstellen Sie die Clientbenachrichtigung zum Neustarten eines Geräts**
1.  Suchen Sie das Gerät, das Sie neu starten möchten, in der Sammlung im Knoten **Gerätesammlungen** der Konsole.
2.  Klicken Sie mit der rechten Maustaste auf das Gerät, und wählen Sie **Clientbenachrichtigung** und danach **Neustart** aus. Dadurch wird ein Fenster mit Informationen zum Neustart geöffnet. Klicken Sie zum Bestätigen der Anforderung des Neustarts auf **OK** .

Wenn ein Client diese Benachrichtigung empfängt, wird dort ein **Softwarecenter**-Benachrichtigungsfenster geöffnet, um den Benutzer über den Neustart zu informieren. Standardmäßig erfolgt der Neustart nach 90 Minuten. Sie können den Zeitpunkt des Neustarts durch Konfigurieren der [Clienteinstellungen](/sccm/core/clients/deploy/configure-client-settings) ändern. Sie finden die Einstellungen für das Neustartverhalten in den Standardeinstellungen auf der Registerkarte [Computerneustart](/sccm/core/clients/deploy/about-client-settings#computer-restart).


##  <a name="BKMK_ClientCache"></a> Konfigurieren des Clientcaches für Configuration Manager-Clients  
Der Clientcache speichert temporäre Dateien, die beim Installieren von Anwendungen und Programmen durch Clients verwendet werden. Softwareupdates verwenden ebenfalls den Clientcache. Diese versuchen jedoch unabhängig von der Größeneinstellung stets, Downloads in den Cache durchzuführen. Konfigurieren Sie die Cacheeinstellungen (z.B. Größe und Speicherort), wenn Sie den Client installieren, die Clientpushinstallation verwenden oder die Installation abgeschlossen haben.

Ab Configuration Manager Version 1606 können Sie die Größe des Cacheordners mithilfe von Clienteinstellungen in der Configuration Manager-Konsole angeben.   

 Der Standardspeicherort für den Configuration Manager-Clientcache ist %*windir*%\ccmcache, und der Standardspeicherplatz auf dem Datenträger beträgt 5120 MB.  

> [!IMPORTANT]  
>  Verschlüsseln Sie den Ordner für den Clientcache nicht. Das Herunterladen von Inhalt in einen verschlüsselten Ordner ist nicht möglich.  

### <a name="about-client-cache"></a>Informationen zum Clientcache  

Der Configuration Manager-Client lädt den Inhalt für erforderliche Software unmittelbar nach Erhalt der Bereitstellung herunter, führt ihn jedoch erst zum geplanten Bereitstellungszeitpunkt aus. Zum geplanten Zeitpunkt überprüft der Configuration Manager-Client, ob der Inhalt im Cache verfügbar ist. Wenn Inhalte im Cache verfügbar sind und in der richtigen Version vorliegen, werden diese Cacheinhalte verwendet. Wenn die erforderliche Version des Inhalts geändert wird oder der Client den Inhalt löscht, um Speicherplatz für ein anderes Paket freizugeben, lädt der Client den Inhalt erneut in den Cache herunter.  

Wenn versucht wird, Inhalte für ein Programm oder eine Anwendung herunterzuladen, deren Größe die Cachegröße überschreitet, tritt bei der Bereitstellung wegen unzureichender Cachegröße ein Fehler auf. Der Client generiert die Statusmeldung 10050 für unzureichende Cachegröße. Das spätere Erhöhen der Cachegröße führt zu folgendem Ergebnis:  

-   Erforderliches Programm: Es wird nicht automatisch erneut versucht, die Inhalte herunterzuladen. Stellen Sie das Paket und das Programm erneut für den Client bereit.  
-   Erforderliche Anwendung: Der Client versucht beim Herunterladen der Clientrichtlinie erneut automatisch, die Inhalte herunterzuladen.  

Wenn der Client versucht, ein Paket herunterzuladen, das die Cachegröße unterschreitet, der Cache jedoch voll ist, werden alle erforderlichen Bereitstellungsversuche so lange wiederholt, bis ausreichend Cachespeicher verfügbar ist, bis das Zeitlimit für den Download erreicht ist, oder die Grenze für die Anzahl von Wiederholungen erreicht ist. Wird die Cachegröße später erweitert, wird vom Configuration Manager-Client im nächsten Wiederholungsintervall erneut versucht, das Paket herunterzuladen. Der Client startet alle vier Stunden einen neuen Versuch, um die Inhalte herunterzuladen. Maximal werden 18 Wiederholungen ausgeführt.  

Cacheinhalte werden nicht automatisch gelöscht. Sie verbleiben nach der Verwendung der Inhalte durch den Client mindestens einen Tag lang im Cache. Wenn Sie die Paketeigenschaften so konfigurieren, dass Inhalte dauerhaft im Clientcache gespeichert werden, werden die Paketinhalte nicht automatisch aus dem Cache gelöscht. Wenn der Cachespeicher von Paketen verwendet wird, die innerhalb der letzten 24 Stunden heruntergeladen wurden, und der Client neue Pakete herunterladen muss, können Sie entweder den Cachespeicher erhöhen oder die Option zum Löschen von gespeicherten Cacheinhalten auswählen.  

 Gehen Sie wie folgt vor, um den Clientcache während der manuellen Clientinstallation oder nach der Installation des Clients zu konfigurieren.  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>So konfigurieren Sie den Clientcache während der manuellen Clientinstallation  

Führen Sie den Befehl CCMSetup.exe vom Installationsquellspeicherort aus. Geben Sie dabei nach Bedarf die folgenden Eigenschaften durch Leerzeichen getrennt an:  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Verwenden Sie für Version 1606 die Einstellungen für die Cachegröße, die in den **Clienteinstellungen** in der Configuration Manager-Konsole statt in SMSCACHESIZE verfügbar sind. Weitere Informationen finden Sie unter [Einstellungen des Clientcaches](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

Weitere Informationen zum Verwenden dieser Befehlszeileneigenschaften für „CCMSetup.exe“ finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>So konfigurieren Sie den Clientcacheordner während der Installation von Clients mithilfe der Clientpushinstallation  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** > **Standorte** aus.  

3.  Wählen Sie den entsprechenden Standort aus, und klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Clientinstallationseinstellungen** > **Installationseigenschaften**.  

5.  Geben Sie die folgenden Eigenschaften getrennt durch Leerzeichen an:  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Verwenden Sie für Version 1606 die Einstellungen für die Cachegröße, die in den **Clienteinstellungen** in der Configuration Manager-Konsole statt in SMSCACHESIZE verfügbar sind. Weitere Informationen finden Sie unter [Einstellungen des Clientcaches](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

       Weitere Informationen zum Verwenden dieser Befehlszeileneigenschaften für „CCMSetup.exe“ finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>So konfigurieren Sie den Clientcacheordner auf dem Clientcomputer  

1.  Doppelklicken Sie in der Systemsteuerung des Clientcomputers auf **Configuration Manager**, um die Eigenschaften anzuzeigen.  

2.  Legen Sie auf der Registerkarte **Cache** die Eigenschaften für Speicherplatz und Speicherort fest. Der Standardspeicherort lautet *%windir%* \ccmcache.  

3.  Wählen Sie zum Löschen der Dateien im Cacheordner **Dateien löschen** aus.  

### <a name="to-configure-client-cache-size-in-client-settings"></a>So konfigurieren Sie die Cachegröße des Clients in den Clienteinstellungen

Passen Sie die Größe des Clientcaches an, ohne den Client neu installieren zu müssen, indem Sie die Cachegröße in der Configuration Manager-Konsole mithilfe der Cacheeinstellungen konfigurieren.  

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung**  >  **Clienteinstellungen**.

2. Führen Sie auf **Clientstandardeinstellungen** einen Doppelklick aus.
  Sie können auch benutzerdefinierte Einstellungen erstellen, um die Cachegröße gezielter anzuwenden. Weitere Informationen zu standardmäßigen und benutzerdefinierten Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

 3. Klicken Sie auf **Einstellung des Clientcaches**, und wählen Sie **Ja** für **Configure client cache size** (Konfigurieren der Cachegröße des Clients) aus. Verwenden Sie dann entweder **MB** oder die Einstellung **Prozentsatz des Datenträgers**. Der Cache wird immer an die kleinere Größe angepasst.

     Der Configuration Manager-Client wird die Größe des Caches beim nächsten Download der Clientrichtlinie mit diesen Einstellungen konfigurieren.



##  <a name="BKMK_UninstalClient"></a> Deinstallieren des Configuration Manager-Clients  
 Sie können die Windows-Configuration Manager-Clientsoftware mithilfe von **CCMSetup.exe** mit der Eigenschaft **/Uninstall** von einem Computer deinstallieren. Führen Sie CCMSetup.exe auf einem einzelnen Computer über die Eingabeaufforderung aus, oder stellen Sie ein Paket und ein Programm bereit, um den Client von einer Sammlung von Computern zu deinstallieren.  

> [!WARNING]  
>  Sie können den Configuration Manager-Client nicht von einem mobilen Gerät aus deinstallieren. Wenn die Deinstallation des Configuration Manager-Clients von einem mobilen Gerät aus erforderlich ist, müssen Sie das Gerät zurücksetzen. Dadurch werden alle Daten auf dem mobilen Gerät gelöscht.  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>So deinstallieren Sie den Configuration Manager-Client mithilfe der Eingabeaufforderung  

1.  Öffnen Sie eine Windows-Eingabeaufforderung, und ändern Sie den Ordner in den Speicherort von „CCMSetup.exe“.  

2.  Geben Sie **Ccmsetup.exe /uninstall**ein, und drücken Sie die **Eingabetaste.**  

> [!NOTE]  
>  Bei der Deinstallation werden keine Ergebnisse auf dem Bildschirm angezeigt. Zur Sicherstellung, dass die Clientdeinstallation erfolgreich war, überprüfen Sie die Protokolldatei **CCMSetup.log** im Ordner *%windir%\ccmsetup* auf dem Clientcomputer.  

##  <a name="BKMK_ConflictingRecords"></a> Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients  
 Configuration Manager verwendet Hardware-IDs, um Clients zu identifizieren, bei denen es sich um Duplikate handeln könnte, und informiert Sie über in Konflikt stehende Datensätze. Wenn Sie z.B. einen Computer erneut installieren, bleibt die Hardware-ID unverändert, während die von Configuration Manager verwendete GUID sich ändern kann.  

 Configuration Manager löst Konflikte automatisch mithilfe der Windows-Authentifizierung des Computerkontos oder eines PKI-Zertifikats aus einer vertrauenswürdigen Quelle. Wenn Configuration Manager Konflikte durch doppelte Hardware-IDs jedoch nicht lösen kann, bestimmt eine Hierarchieeinstellung, ob die Datensätze automatisch zusammengeführt werden oder ob Sie das Verhalten bestimmen können. Wenn Sie sich für das manuelle Verwalten duplizierter Datensätze entscheiden, müssen Sie die in Konflikt stehenden Datensätze in der Configuration Manager-Konsole manuell bearbeiten, um den Konflikt aufzulösen.  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>So ändern Sie die Hierarchieeinstellung zum Verwalten von in Konflikt stehenden Datensätzen  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** > **Standorte** > **Hierarchieeinstellungen** aus.
2.  Klicken Sie auf der Registerkarte **Clientgenehmigung und in Konflikt stehende Datensätze** entweder auf **In Konflikt stehende Datensätze automatisch auflösen** oder **In Konflikt stehende Datensätze manuell bearbeiten**.  

#### <a name="to-manually-resolve-conflicting-records"></a>So bearbeiten Sie in Konflikt stehende Datensätze manuell  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Überwachung** > **Systemstatus** > **In Konflikt stehende Datensätze** aus.  

3.  Wählen Sie mindestens einen in Konflikt stehenden Datensatz aus, und klicken Sie dann auf **In Konflikt stehende Datensätze**.  

4.  Wählen Sie eine der folgenden Optionen aus:  

    -   **Zusammenführen**: Hiermit kombinieren Sie den neu erkannten Datensatz mit dem vorhandenen Clientdatensatz.  

    -   **Neu** : Hiermit erstellen Sie einen neuen Datensatz für den in Konflikt stehenden Clientdatensatz.  

    -   **Sperren** : Hiermit erstellen Sie einen neuen Datensatz für den in Konflikt stehenden Clientdatensatz, markieren ihn jedoch als gesperrt.  

## <a name="manage-duplicate-hardware-identifiers"></a>Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients
Das Bereitstellen einer Liste von Hardware-IDs, die Configuration Manager für den PXE-Start und die Clientregistrierung ignoriert, ist für das Beheben von zwei häufigen Problemen hilfreich.

1. Viele neue Geräte wie Surface Pro 3 haben keinen integrierten Ethernet-Anschluss. Techniker verwenden einen USB-zu-Ethernet-Adapter zum Einrichten einer Kabelverbindung für die Bereitstellung eines Betriebssystems. Diese Adapter werden aus Kostengründen und wegen der allgemeinen Nutzbarkeit häufig gemeinsam genutzt. Nachdem die MAC-Adresse des Adapters zur Identifizierung des Geräts verwendet wird, ist es problematisch, den Adapter ohne zusätzliche Aktionen eines Administrators zwischen den Bereitstellungen wiederzuverwenden. Schließen Sie die MAC-Adresse des Adapters aus, um diesen für ein solches Szenario wiederzuverwenden.
2. Während das SMBIOS-Attribut eindeutig sein sollte, verfügen einige spezielle Hardwaregeräte über doppelte IDs. Schließen Sie diese doppelten ID aus, und verwenden Sie die eindeutige MAC-Adresse jedes Geräts.

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>So fügen Sie von Hardware-IDs hinzu, die Configuration Manager ignorieren soll  
1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Standorte**.
2. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.
3. Wählen Sie auf der Registerkarte **Clientgenehmigung und in Konflikt stehende Datensätze** im Abschnitt **Doppelte Hardware-IDs** die Option **Hinzufügen** aus, um neue Hardware-IDs hinzuzufügen.

##  <a name="BKMK_PolicyRetrieval"></a> Initiieren des Richtlinienabrufs für einen Configuration Manager-Client  
 Clientrichtlinien werden von Windows-Configuration Manager-Clients nach einem als Clienteinstellung konfigurierten Zeitplan heruntergeladen. Es kann jedoch vorkommen, dass Sie Richtlinien lokal vom Client abrufen möchten, z.B. zur Problembehandlung oder während eines Tests.  

Sie können den Richtlinienabruf auslösen:


- [Clientbenachrichtigung](#initiate-client-policy-retrieval-using-client-notification)
- [Registerkarte **Aktionen** auf dem Client](#manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client)
- [Skript](#manually-initiate-client-policy-retrieval-by-script)

> [!NOTE]  
>   
>  Weitere Informationen zum Richtlinienabruf für Clients, auf denen Linux und UNIX ausgeführt wird, finden Sie unter [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU).  

#### <a name="initiate-client-policy-retrieval-using-client-notification"></a>So lösen Sie den Clientrichtlinienabruf mithilfe der Clientbenachrichtigung aus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Konformität** > **Gerätesammlungen**.  

3.  Wählen Sie die Gerätesammlung mit den Computern aus, deren Richtlinie heruntergeladen werden soll. Wählen Sie auf der Registerkarte **Start** in der Gruppe **Sammlungen** **Clientbenachrichtigung** > **Computerrichtlinie herunterladen** aus.  

    > [!NOTE]  
    >  Sie können die Clientbenachrichtigung auch verwenden, um den Richtlinienabruf für ein oder mehrere ausgewählte Geräte zu initiieren, die in einem Knoten für eine temporäre Sammlung unter dem Knoten **Geräte** angezeigt werden.  

#### <a name="manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client"></a>So lösen Sie den Computerrichtlinienabruf manuell im Configuration Manager-Client auf der Registerkarte „Aktionen“ aus  

1.  Wählen Sie in der Systemsteuerung des Computers **Configuration Manager** aus.  

2.  Klicken Sie auf der Registerkarte **Aktionen** auf **Computerrichtlinienabruf und Auswertungszyklus**, um die Computerrichtlinie zu initiieren, und klicken Sie anschließend auf **Jetzt ausführen**.  

4.  Klicken Sie zum Bestätigen der Eingabeaufforderung auf **OK**.  

5.  Wiederholen Sie die Schritte 3 und 4 für alle weiteren erforderlichen Aktionen, wie z.B. den **Benutzerrichtlinienabruf und Auswertungszyklus** für Benutzerclienteinstellungen.  

#### <a name="manually-initiate-client-policy-retrieval-by-script"></a>So lösen Sie den Clientrichtlinienabruf manuell mithilfe eines Skripts aus  

1.  Öffnen Sie einen Text-Editor, z. B. Notepad.  

2.  Kopieren Sie folgendes Beispiel für Visual Basic Scripting Edition-Code, und fügen Sie dieses in die Datei ein:  

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

5.  Klicken Sie im Dialogfeld **Windows Script Host** auf **OK**.  
