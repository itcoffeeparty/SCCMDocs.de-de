---
title: "Funktionen in Technical Preview 1603 für System Center Configuration Manager"
description: "Erfahren Sie mehr zu Funktionen, die in System Center Configuration Manager Technical Preview 1603 zur Verfügung stehen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 39a9cde3bd955c84f301d25258b413fecaa4393b
ms.openlocfilehash: ab9f71700ff80414f7cb8e79f54fba3262f810ff

---
# <a name="capabilities-in-technical-preview-1603-for-system-center-configuration-manager"></a>Funktionen in Technical Preview 1603 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*

In diesem Artikel werden die Funktionen erläutert, die in der Technical Preview für System Center Configuration Manager 1603 verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bei Verwendung von System Center Technical Preview 5 wird diese Version auch als eine Baselineversion von System Center Configuration Manager Technical Preview installiert. Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen, und zu erfahren, wie Sie Updates zwischen Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.  

 **Bekannte Probleme für diese Technical Preview:**  

-   Diese Version enthält Updates für zuvor veröffentlichte Features, umfasst jedoch keine neuen Features. Aus diesem Grund ist die Seite „Features“ des Update-Assistenten leer, wenn Sie zuvor ein Upgrade auf 1602 durchgeführt und alle in 1602 enthaltenen Features aktiviert haben.  

-   Nach dem Update Ihres Standortservers auf Technical Preview 1603 können Sie auf Clients erst dann wieder Remotesteuerungsfunktionen verwenden, wenn diese ebenfalls auf Version 1603 aktualisiert werden.  

 **Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

##  <a name="a-namebkmksc1603a-improvements-to-software-center"></a><a name="BKMK_SC1603"></a> Verbesserungen für Software Center  

### <a name="new-tiled-view-for-apps"></a>Neue Kachelansicht für Apps  
 Endbenutzer können jetzt in Software Center auf der Registerkarte **Anwendungen** zwischen einer Liste von Apps oder einer Kachelansicht von Apps auswählen.  

### <a name="select-multiple-updates-in-software-center"></a>Auswählen mehrerer Updates in Software Center  
 Auf der Registerkarte **Updates** in Software Center können Sie jetzt mehrere Updates oder **Alle aktualisieren** auswählen, um mehrere Updates gleichzeitig zu installieren.  

##  <a name="a-namebkmkrc1603a-improvements-to-remote-control"></a><a name="BKMK_RC1603"></a> Verbesserungen an der Remotesteuerung  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Beschränken des Zugriffs auf die freigegebene Zwischenablage in einer Remotesteuerungssitzung  
 Sie können in den Remotetools jetzt die neue Clienteinstellung **Benutzer zum Erteilen der Berechtigung zur Freigabe der Zwischenablage für Dateiübertragungen auffordern** aktivieren, um den Zugriff auf die freigegebene Zwischenablage in einer Remotesteuerungssitzung zu beschränken.  

 Wenn diese Option aktiviert ist, muss der Endbenutzer, der eine Remotesitzung freigibt, dem Remotebetrachter dieser Sitzung die entsprechenden Berechtigungen erteilen, damit der Remotebetrachter Dateien aus der Sitzung über die freigegebene Zwischenablage auf seinen lokalen Computer übertragen kann.  

 Dadurch wird für den Endbenutzer eine weitere Sicherheitsebene hinzugefügt. Wenn dem Remotebetrachter zuvor Vollzugriff auf den Computer des Endbenutzers erteilt wurde, hatte er über die freigegebene Zwischenablage die Möglichkeit, Dateien unbemerkt vom Endbenutzer aus der Sitzung auf den lokalen Computer zu übertragen.  

##  <a name="a-namebkmkramdisktftpa-customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> Anpassen der RamDisk-TFTP-Blockgröße und der Fenstergröße auf PXE-fähigen Verteilungspunkten  
 In Technical Preview 1603 können Sie die RamDisk-TFTP-Blockgröße und die Fenstergröße für PXE-fähige Verteilungspunkte anpassen. Wenn Sie Ihr Netzwerk angepasst haben, kann dies wegen übermäßiger Block- oder Fenstergröße zu einem Timeout beim Herunterladen des Startimages führen. Durch Anpassen der RamDisk-TFTP-Blockgröße und der Fenstergröße können Sie den TFTP-Datenverkehr bei Verwendung von PXE für Ihre spezifischen Netzwerkanforderungen optimieren.   
Sie müssen die benutzerdefinierten Einstellungen in Ihrer Umgebung testen, um die effizienteste Einstellung zu ermitteln.  

-   **TFTP-Blockgröße:**Die Blockgröße ist die Größe der Datenpakete, die vom Server an den Client gesendet werden, der die Datei herunterlädt (wie in RFC 2347 erörtert). Mit einer größeren Blockgröße kann der Server weniger Pakete senden, sodass weniger Roundtripverzögerungen zwischen dem Server und dem Client auftreten. Große Blöcke führen jedoch zu fragmentierten Paketen, die von den meisten PXE-Clientimplementierungen nicht unterstützt werden.  

-   **TFTP-Fenstergröße:**TFTP erfordert ein Bestätigungspaket (acknowledgment packet; ACK) für jeden gesendeten Datenblock. Der Server sendet den nächsten Block in der Sequenz erst, wenn er das ACK-Paket für den vorherigen Block empfangen hat. TFTP-Fenster sind ein Feature in den Windows-Bereitstellungsdiensten, mit dem Sie definieren können, wie viele Datenblöcke ein Fenster füllen. Der Server sendet die Datenblöcke nach dem Back-to-Back-Prinzip, bis das Fenster gefüllt ist. Anschließend sendet der Client ein ACK-Paket. Durch Erhöhen diese Fenstergröße reduzieren Sie die Anzahl von Roundtripverzögerungen zwischen Client und Server und verringern die Gesamtzeit, die zum Herunterladen eines Startimages erforderlich ist.  

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die folgenden Aufgaben durchzuführen, und verwenden Sie dann die Feedbackinformationen oben in diesem Thema, um uns Ihre Erfahrungen mitzuteilen:  

-   Ich kann die RamDisk-TFTP-Fenstergröße auf dem PXE-fähigen Verteilungspunkt anpassen.  

-   Ich kann die RamDisk-TFTP-Blockgröße auf dem PXE-fähigen Verteilungspunkt anpassen.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>So ändern Sie die RamDisk-TFTP-Fenstergröße  

-   Fügen Sie auf PXE-fähigen Verteilungspunkten den folgenden Registrierungsschlüssel hinzu, um die RamDisk-TFTP-Fenstergröße anzupassen:  

     **Speicherort:**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Name: RamDiskTFTPWindowSize  

     **Typ:**REG_DWORD  

     **Wert**: &lt;angepasste Fenstergröße\>  

 Der Standardwert ist 1 (1 Datenblock füllt das Fenster aus)  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>So ändern Sie die RamDisk-TFTP-Blockgröße  

-   Fügen Sie auf PXE-fähigen Verteilungspunkten den folgenden Registrierungsschlüssel hinzu, um die RamDisk-TFTP-Fenstergröße anzupassen:  

     **Speicherort:**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Name: RamDiskTFTPBlockSize  

     **Typ:**REG_DWORD  

     **Wert**: &lt;angepasste Blockgröße\>  

 Der Standardwert ist 4096 (4 KB).  



<!--HONumber=Nov16_HO1-->


