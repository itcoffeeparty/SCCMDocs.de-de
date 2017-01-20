---
title: "Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk | Microsoft Docs"
description: Verwenden Sie PXE-initiierte Betriebssystembereitstellungen, um das Betriebssystem eines Computers zu aktualisieren oder eine neue Version von Windows auf einem neuen Computer zu installieren.
ms.custom: na
ms.date: 12/07/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
caps.latest.revision: 19
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3f44505c977b511223a083a960f871371c0ff133
ms.openlocfilehash: b22cdbd42693078caa47f41182ce73ea881c3515


---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei einer PXE-initiierten Betriebssystembereitstellung in System Center Configuration Manager werden Betriebssysteme von Clientcomputern über das Netzwerk angefordert und bereitgestellt. Bei diesem Szenario der Betriebssystembereitstellung werden das Betriebssystemimage und die x86- und x64-Versionen der Windows PE-Startimages an einen Verteilungspunkt gesendet, der so konfiguriert ist, dass PXE-Startanforderungen akzeptiert werden.  

> [!NOTE]  
>  Wenn Sie eine Betriebssystembereitstellung nur für x64-BIOS-Computer erstellen, müssen das x64-Startabbild und das x86-Startabbild auf dem Verteilungspunkt verfügbar sein.  

 Sie können PXE-initiierte Betriebssystembereitstellungen in den folgenden Betriebssystembereitstellungsszenarien verwenden:  

-   [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

 Führen Sie die Schritte in einem der Betriebssystembereitstellungsszenarien aus, und verwenden Sie dann die folgenden Abschnitte, um PXE-initiierte Bereitstellungen vorzubereiten.  

##  <a name="a-namebkmkconfigurea-configure-at-least-one-distribution-point-to-accept-pxe-requests"></a><a name="BKMK_Configure"></a> Konfigurieren mindestens eines Verteilungspunkts zum Akzeptieren von PXE-Anforderungen  
 Sie müssen mindestens einen zum Antworten auf PXE-Startanforderungen konfigurierten Verteilungspunkt verwenden, um Betriebssysteme auf Configuration Manager-Clients bereitzustellen, auf denen PXE-Startanforderungen gestellt werden.  Die Schritte zum Aktivieren von PXE auf einem Verteilungspunkt finden Sie unter [Configuring distribution points to accept PXE requests (Konfigurieren von Verteilungspunkten zum Akzeptieren von PXE-Anforderungen)](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

## <a name="prepare-a-pxe-enabled-boot-image"></a>Vorbereiten eines PXE-fähigen Startabbilds  
 Um PXE zum Bereitstellen eines Betriebssystems zu verwenden, muss sowohl ein PXE-fähiges x86-Startabbild als auch ein PXE-fähiges x64-Startabbild an mindestens einen PXE-fähigen Verteilungspunkt verteilt sein. Verwenden Sie die Informationen zum Aktivieren von PXE in einem Startimage, verteilen Sie das Startimage an Verteilungspunkte:  

-   Um PXE für ein Startimage zu aktivieren, wählen Sie die Option  **Dieses Startimage über den PXE-fähigen Verteilungspunkt bereitstellen** auf der Registerkarte **Datenquelle** in den Startimageeinstellungen aus.  

-   Wenn Sie die Eigenschaften für das Startimage ändern, verteilen Sie das Startimage erneut an Verteilungspunkte. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

##  <a name="a-namebkmkpxeexclusionlista-create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> Erstellen einer Ausschlussliste für PXE-Bereitstellungen  
 Wenn Sie PXE zur Bereitstellung von Betriebssystemen verwenden, können Sie eine Ausschlussliste für jeden Verteilungspunkt erstellen, sodass PXE-Startanforderungen von Computern, die in der Ausschlussliste enthalten sind, ignoriert werden. Diese Ausschlussliste enthält die MAC-Adressen der Computer, die vom Verteilungspunkt ignoriert werden sollen. Die von Configuration Manager für die PXE-Bereitstellung verwendeten Bereitstellungstasksequenzen werden nicht an diese Computer gesendet.  

 Führen Sie die folgenden Schritte aus, um die PXE-Ausschlussliste zu erstellen.  

#### <a name="to-create-the-exclusion-list"></a>So erstellen Sie die Ausschlussliste  

1.  Erstellen Sie eine Textdatei auf dem Verteilungspunkt, der für PXE aktiviert ist. Geben Sie dieser Textdatei beispielsweise den Namen **pxeExceptions.txt**.  

2.  Verwenden Sie einen Standardeditor wie Notepad, und fügen Sie die MAC-Adressen der Computer hinzu, die vom PXE-fähigen Verteilungspunkt ignoriert werden sollen. Trennen Sie die MAC-Adresswerte mit Kommas, und geben Sie jede Adresse in einer eigenen Zeile ein. Beispiel: `01:23:45:67:89:ab`  

3.  Speichern Sie die Textdatei auf dem PXE-fähigen Verteilungspunkt-Standortsystemserver. Die Textdatei kann auf dem Server an einem beliebigen Speicherort gespeichert werden.  

4.  Bearbeiten Sie die Registrierung des PXE-fähigen Verteilungspunkts, um einen **MACIgnoreListFile** -Registrierungsschlüssel zu erstellen, der den Zeichenfolgenwert des vollständigen Pfads zur Textdatei auf dem Systemserver des PXE-fähigen Verteilungspunkts enthält. Verwenden Sie den folgenden Registrierungspfad:  

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  Durch eine unsachgemäße Verwendung des Registrierungs-Editors können schwerwiegende Fehler auftreten, die möglicherweise eine Neuinstallation des Betriebssystems erforderlich machen. Microsoft kann nicht garantieren, dass Probleme, die aufgrund einer unsachgemäßen Verwendung des Registrierungs-Editors entstehen, behoben werden können. Die Verwendung des Registrierungs-Editors erfolgt auf eigene Gefahr.  

     Nach dieser Registrierungsänderung ist kein Neustart des Servers erforderlich.  

##  <a name="a-namebkmkramdisktftparamdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a>RamDisk-TFTP-Blockgröße und Fenstergröße  
Sie können die RamDisk-TFTP-Blockgröße und ab Configuration Manager Version 1606 die Fenstergröße für PXE-fähige Verteilungspunkte anpassen. Wenn Sie Ihr Netzwerk angepasst haben, kann dies wegen übermäßiger Block- oder Fenstergröße zu einem Timeout beim Herunterladen des Startimages führen. Durch Anpassen der RamDisk-TFTP-Blockgröße und der Fenstergröße können Sie den TFTP-Datenverkehr bei Verwendung von PXE für Ihre spezifischen Netzwerkanforderungen optimieren. Sie müssen die benutzerdefinierten Einstellungen in Ihrer Umgebung testen, um die effizienteste Einstellung zu ermitteln. Weitere Informationen finden Sie unter [Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points (Anpassen der RamDisk-TFTP-Blockgröße und der Fenstergröße auf PXE-fähigen Verteilungspunkten)](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen  
 Zum Verwenden einer PXE-initiierten Betriebssystembereitstellung müssen Sie die Bereitstellung konfigurieren, um das Betriebssystem für PXE-Startanforderungen zur Verfügung zu stellen. Sie können dies auf der Seite der **Bereitstellungseinstellungen** des Assistenten oder der Registerkarte für die **Bereitstellungseinstellungen** in den Eigenschaften für die Bereitstellung konfigurieren.  Konfigurieren Sie eine der folgenden Optionen für die Einstellung **Verfügbar machen für** :  

-   Configuration Manager-Clients, Medien und PXE  

-   Nur Medien und PXE  

-   Nur Medien und PXE (ausgeblendet)  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Bereitstellen der Tasksequenz  
 Stellen Sie das Betriebssystem in einer Zielsammlung bereit. Weitere Informationen finden Sie unter [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Beim Bereitstellen von Betriebssystemen unter Verwendung von PXE können Sie konfigurieren, ob die Bereitstellung erforderlich oder verfügbar ist.  

-   **Erforderliche Bereitstellung**: Bei erforderlichen Bereitstellungen wird PXE ohne jegliches Eingreifen des Benutzers verwendet. Der Benutzer ist nicht in der Lage, den PXE-Start zu umgehen. Wenn ein Benutzer den PXE-Startvorgang jedoch abbricht, bevor vom PXE-Verteilungspunkt geantwortet wird, wird das Betriebssystem nicht bereitgestellt.  

-   **Verfügbare Bereitstellung**: Für verfügbare Bereitstellungen muss der Benutzer am Zielcomputer anwesend sein, damit er die Taste F12 drücken kann, um den PXE-Startvorgang fortzusetzen. Wenn der Benutzer nicht anwesend ist und die Taste F12 nicht drücken kann, wird der Computer mit dem aktuellen Betriebssystem oder vom nächsten verfügbaren Startgerät neu gestartet.  

 Sie können eine erforderliche PXE-Bereitstellung erneut bereitstellen, indem Sie den Status der letzten PXE-Bereitstellung, die einer Configuration Manager-Sammlung oder einem Computer zugewiesen ist, löschen. Mit dieser Aktion wird der Status der Bereitstellung zurückgesetzt, und die letzten erforderlichen Bereitstellungen werden erneut bereitgestellt.  

> [!IMPORTANT]  
>  Das PXE-Protokoll ist nicht sicher. Stellen Sie sicher, dass der PXE-Server und der PXE-Client sich in einem physisch sicheren Netzwerk (z. B. in einem Rechenzentrum) befinden, um unbefugten Zugriff auf den Standort zu verhindern.  

##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Wie wird das Startimage für Clients ausgewählt, die mit PXE gestartet werden?
Wenn ein Client mit PXE gestartet wird, stellt Configuration Manager ein Startimage für den Client bereit. Configuration Manager verwendet ab Version 1606 ein Startimage mit einer exakten architektonischen Übereinstimmung, sofern ein entsprechendes Image verfügbar ist. Ist dies nicht der Fall, verwendet Configuration Manager ein Startimage mit einer kompatiblen Architektur. In der folgenden Liste finden Sie Informationen dazu, wie ein Startimage für Clients ausgewählt wird, die mit PXE gestartet werden.
1. Configuration Manager sucht in der Standortdatenbank nach dem Systemdatensatz, bei dem die MAC-Adresse oder das SMBIOS mit der MAC-Adresse oder dem SMBIOS des Clients übereinstimmt, der gestartet werden soll.
    > [!NOTE]
    > Wenn ein Computer, der einem Standort zugewiesen ist, für einen anderen Standort mit PXE gestartet wird, werden die Richtlinien für den Computer nicht angezeigt. Wenn z.B. ein Client bereits Standort A zugewiesen ist, können ein Verwaltungspunkt und ein Verteilungspunkt an Standort B nicht auf die Richtlinien von Standort A zugreifen, und der Client wird nicht erfolgreich mit PXE gestartet.
2. Configuration Manager sucht nach Tasksequenzen, die für den Systemdatensatz in Schritt 1 bereitgestellt werden.
3. In der Liste mit Tasksequenzen in Schritt 2 sucht Configuration Manager nach einem Startimage mit einer Architektur, die mit der des Clients übereinstimmt, der gestartet werden soll. Wenn ein Startimage mit derselben Architektur gefunden wird, wird dieses Startimage verwendet.

4. Wenn kein Startimage mit derselben Architektur gefunden wird, sucht Configuration Manager (in der Liste mit Tasksequenzen in Schritt 2) nach einem Startimage, das mit der Architektur des Clients kompatibel ist, der gestartet werden soll. Ein 64-Bit-Client ist beispielsweise mit 32-Bit- und 64-Bit-Startimages kompatibel. Ein 32-Bit-Client ist nur mit 32-Bit-Startimages kompatibel. Ein UEFI-Client ist nur mit 64-Bit-Startimages kompatibel.



<!--HONumber=Dec16_HO3-->


