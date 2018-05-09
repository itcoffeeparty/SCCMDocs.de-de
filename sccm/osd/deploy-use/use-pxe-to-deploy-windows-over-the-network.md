---
title: Verwenden von PXE für die Betriebssystembereitstellung über das Netzwerk
titleSuffix: Configuration Manager
description: Verwenden Sie mit PXE initiierte Betriebssystembereitstellungen, um das Betriebssystem eines Computers zu aktualisieren oder eine neue Version von Windows auf einem neuen Computer zu installieren.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: deb8321400eac4085cefca8686f2703cea5f659a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei einer mithilfe von PXE (Pre-Boot eXecution Environment) ausgelösten Betriebssystembereitstellung in Configuration Manager werden Betriebssysteme von Clients über das Netzwerk angefordert und bereitgestellt. In diesem Bereitstellungsszenario senden Sie das Betriebssystemimage und die Startimages an einen PXE-fähigen Verteilungspunkt.

> [!NOTE]  
>  Wenn Sie eine Betriebssystembereitstellung nur für x64-BIOS-Computer erstellen, müssen das x64-Startimage und das x86-Startimage auf dem Verteilungspunkt verfügbar sein.

Sie können über PXE initiierte Bereitstellungen in den folgenden Szenarios verwenden:

-   [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

Führen Sie die Schritte in einem der Szenarios für die Betriebssystembereitstellung aus, und bereiten Sie dann die von PXE ausgelösten Bereitstellungen anhand der Abschnitte in diesem Artikel vor.



##  <a name="BKMK_Configure"></a> Konfigurieren mindestens eines Verteilungspunkts zum Akzeptieren von PXE-Anforderungen
Zum Bereitstellen von Betriebssystemen für Configuration Manager-Clients, die PXE-Startanforderungen ausführen, müssen Sie mindestens einen Verteilungspunkt so konfigurieren, dass er PXE-Anforderungen akzeptiert. Sobald der Verteilungspunkt konfiguriert ist, reagiert er auf PXE-Startanforderungen und ermittelt die geeigneten Bereitstellungsaktionen. Weitere Informationen finden Sie unter [Installieren oder Modifizieren eines Verteilungspunkts](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#pxe).  



## <a name="prepare-a-pxe-enabled-boot-image"></a>Vorbereiten eines PXE-fähigen Startabbilds
Um PXE zum Bereitstellen eines Betriebssystems zu verwenden, muss sowohl ein PXE-fähiges x86-Startimage als auch ein PXE-fähiges x64-Startimage an mindestens einen PXE-fähigen Verteilungspunkt verteilt sein. Verwenden Sie die Informationen zum Aktivieren von PXE in einem Startimage, verteilen Sie das Startimage an Verteilungspunkte:

-   Um PXE für ein Startabbild zu aktivieren, wählen Sie in den Startabbildeinstellungen auf der Registerkarte **Datenquelle** die Option **Dieses Startabbild über den PXE-fähigen Verteilungspunkt bereitstellen** aus.

-   Wenn Sie die Eigenschaften für das Startabbild ändern, verteilen Sie das Startabbild erneut an Verteilungspunkte. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).



##  <a name="BKMK_PXEExclusionList"></a> Erstellen einer Ausschlussliste für PXE-Bereitstellungen
Wenn Sie Betriebssysteme mit PXE bereitstellen, können Sie für jeden Verteilungspunkt eine Ausschlussliste erstellen. Fügen Sie der Ausschlussliste die MAC-Adressen der Computer hinzu, die vom Verteilungspunkt ignoriert werden sollen. Aufgeführte Computer empfangen nicht die Bereitstellungstasksequenzen, die Configuration Manager für die PXE-Bereitstellung verwendet.

#### <a name="to-create-the-exclusion-list"></a>So erstellen Sie die Ausschlussliste

1.  Erstellen Sie eine Textdatei auf dem Verteilungspunkt, der für PXE aktiviert ist. Geben Sie dieser Textdatei beispielsweise den Namen **pxeExceptions.txt**.

2.  Verwenden Sie einen Standardtexteditor wie Editor, und fügen Sie die MAC-Adressen der Computer hinzu, die vom PXE-fähigen Verteilungspunkt ignoriert werden sollen. Trennen Sie die MAC-Adresswerte mit Kommas, und geben Sie jede Adresse in einer eigenen Zeile ein. Beispiel: `01:23:45:67:89:ab`

3.  Speichern Sie die Textdatei auf dem PXE-fähigen Verteilungspunkt-Standortsystemserver. Die Textdatei kann auf dem Server an einem beliebigen Speicherort gespeichert werden.

4.  Bearbeiten Sie die Registrierung des PXE-fähigen Verteilungspunkts so, dass der Registrierungsschlüssel **MACIgnoreListFile** erstellt wird. Fügen Sie den Zeichenfolgenwert des vollständigen Pfads der Textdatei dem PXE-fähigen Standortsystemserver mit dem Verteilungspunkt hinzu. Verwenden Sie den folgenden Registrierungspfad:

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  Durch eine unsachgemäße Verwendung des Registrierungs-Editors können schwerwiegende Fehler auftreten, die möglicherweise eine Neuinstallation des Betriebssystems erforderlich machen. Microsoft kann nicht garantieren, dass Probleme, die aufgrund einer unsachgemäßen Verwendung des Registrierungs-Editors entstehen, behoben werden können. Die Verwendung des Registrierungs-Editors erfolgt auf eigene Gefahr.

     Nach dieser Registrierungsänderung ist kein Neustart des Servers erforderlich.



## <a name="manage-duplicate-hardware-identifiers"></a>Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients
Configuration Manager erkennt möglicherweise mehrere Computer als ein einziges Gerät, wenn sie über doppelte SMBIOS-Attribute verfügen oder Sie einen gemeinsam genutzten Netzwerkadapter verwenden. Sie können diese Probleme lösen, indem Sie doppelte Hardware-IDs in den Hierarchieeinstellungen verwalten. Weitere Informationen finden Sie unter [Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).



##  <a name="BKMK_RamDiskTFTP"></a>RamDisk-TFTP-Blockgröße und Fenstergröße
Sie können die Größe des RamDisk-TFTP-Blocks und des Fensters für PXE-fähige Verteilungspunkte anpassen. Wenn Sie Ihr Netzwerk angepasst haben, kann eine übermäßige Block- oder Fenstergröße zu einem Timeout beim Herunterladen des Startimages führen. Durch Anpassen der Größe des RamDisk-TFTP-Blocks und des Fensters können Sie den TFTP-Datenverkehr bei Verwendung von PXE für Ihre spezifischen Netzwerkanforderungen optimieren. Um die effizienteste Einstellung zu ermitteln, müssen Sie die benutzerdefinierten Einstellungen in Ihrer Umgebung testen. Weitere Informationen finden Sie unter [Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points (Anpassen der RamDisk-TFTP-Blockgröße und der Fenstergröße auf PXE-fähigen Verteilungspunkten)](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).



## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen
Um eine PXE-initiierte Betriebssystembereitstellung zu verwenden, müssen Sie die Bereitstellung konfigurieren, um das Betriebssystem für PXE-Startanforderungen verfügbar zu machen. Konfigurieren Sie die verfügbaren Betriebssysteme in den Bereitstellungseigenschaften auf der Registerkarte **Bereitstellungseinstellungen**. Wählen Sie für die Einstellung **Verfügbar machen für** eine der folgenden Optionen aus:

-   Configuration Manager-Clients, Medien und PXE

-   Nur Medien und PXE

-   Nur Medien und PXE (ausgeblendet)



##  <a name="BKMK_Deploy"></a> Bereitstellen der Tasksequenz
Stellen Sie das Betriebssystem in einer Zielauflistung bereit. Weitere Informationen finden Sie unter [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Beim Bereitstellen von Betriebssystemen unter Verwendung von PXE können Sie konfigurieren, ob die Bereitstellung erforderlich oder verfügbar ist.

-   **Erforderliche Bereitstellung**: Bei erforderlichen Bereitstellungen wird PXE ohne jegliches Eingreifen des Benutzers verwendet. Der Benutzer kann den PXE-Start nicht umgehen. Wenn ein Benutzer den PXE-Startvorgang jedoch abbricht, bevor der PXE-Verteilungspunkt antwortet, wird das Betriebssystem nicht bereitgestellt.

-   **Available deployment** (Verfügbare Bereitstellung): Für verfügbare Bereitstellungen muss der Benutzer am Zielcomputer anwesend sein. Ein Benutzer muss die Taste F12 drücken, um den PXE-Startvorgang fortzusetzen Wenn der Benutzer nicht anwesend ist und die Taste F12 nicht drücken kann, startet der Computer mit dem aktuellen Betriebssystem oder vom nächsten verfügbaren Startgerät.

Sie können eine erforderliche PXE-Bereitstellung erneut bereitstellen, indem Sie den Status der letzten PXE-Bereitstellung löschen, die einer Configuration Manager-Sammlung oder einem Computer zugewiesen ist. Weitere Informationen zur Aktion **Erforderliche PXE-Bereitstellungen löschen** finden Sie unter [Verwalten von Clients](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode) oder [Verwalten von Sammlungen](/sccm/core/clients/manage/collections/manage-collections#how-to-manage-device-collections). Mit dieser Aktion wird der Status der Bereitstellung zurückgesetzt, und die letzten erforderlichen Bereitstellungen werden erneut installiert.

> [!IMPORTANT]
> Das PXE-Protokoll ist nicht sicher. Stellen Sie sicher, dass der PXE-Server und der PXE-Client sich in einem physisch sicheren Netzwerk (z. B. in einem Rechenzentrum) befinden, um unbefugten Zugriff auf den Standort zu verhindern.



##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Wie wird das Startimage für Clients ausgewählt, die mit PXE gestartet werden?
Wenn ein Client mit PXE gestartet wird, stellt Configuration Manager ein Startimage für den Client bereit. Configuration Manager verwendet ein Startimage mit einer exakten architektonischen Übereinstimmung. Ist dies nicht der Fall, verwendet Configuration Manager ein Startabbild mit einer kompatiblen Architektur. In der folgenden Liste finden Sie Informationen dazu, wie ein Startimage für Clients ausgewählt wird, die mit PXE gestartet werden.
1. Configuration Manager sucht in der Standortdatenbank nach dem Systemdatensatz, bei dem die MAC-Adresse oder das SMBIOS mit der MAC-Adresse oder dem SMBIOS des Clients übereinstimmt, der gestartet werden soll.  

    > [!NOTE]
    > Wenn ein Computer, der einem Standort zugewiesen ist, für einen anderen Standort mit PXE gestartet wird, werden die Richtlinien für den Computer nicht angezeigt. Wenn z.B. ein Client bereits Standort A zugewiesen ist, können ein Verwaltungspunkt und ein Verteilungspunkt an Standort B nicht auf die Richtlinien von Standort A zugreifen. Der Client wird deshalb nicht erfolgreich mit PXE gestartet.

2. Configuration Manager sucht nach Tasksequenzen, die für den Systemdatensatz in Schritt 1 bereitgestellt werden.

3. In der Liste mit Tasksequenzen in Schritt 2 sucht Configuration Manager nach einem Startimage mit einer Architektur, die mit der des Clients übereinstimmt, der gestartet werden soll. Wenn ein Startimage mit derselben Architektur gefunden wird, wird dieses Startimage verwendet.

4. Wenn kein Startabbild mit derselben Architektur gefunden wird, sucht Configuration Manager nach einem Startabbild, das mit der Architektur des Clients kompatibel ist. Hierfür wird die Liste der Tasksequenzen in Schritt 2 verwendet. Ein 64-Bit-Client ist beispielsweise mit 32-Bit- und 64-Bit-Startimages kompatibel. Ein 32-Bit-Client ist nur mit 32-Bit-Startimages kompatibel. Ein UEFI-Client ist nur mit 64-Bit-Startabbildern kompatibel.
