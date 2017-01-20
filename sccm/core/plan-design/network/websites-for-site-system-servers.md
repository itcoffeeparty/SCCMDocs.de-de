---
title: "Websites für Standortsysteme | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über Standard- und Benutzerdefinierte Websites für Standortsystemserver in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 005c9f33367f173993d9626f10a72dd5b0141fbc


---
# <a name="websites-for-site-system-servers-in-system-center-configuration-manager"></a>Websites für Standortsystemserver in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mehrere Configuration Manager-Standortsystemrollen erfordern die Verwendung von Microsoft-Internetinformationsdiensten (IIS) und die Verwendung der IIS-Standardwebsite zum Hosten von Standortsystemdiensten. Wenn Sie andere Webanwendungen auf demselben Server ausführen müssen, und Einstellungen nicht mit Configuration Manager kompatibel sind, erwägen Sie die Nutzung einer benutzerdefinierten Website für Configuration Manager.  

> [!TIP]  
>  Aus Sicherheitsgründen wird empfohlen, für Configuration Manager-Standortsysteme, für die IIS erforderlich ist, einen eigenen Server zu verwenden. Wenn Sie in einem Configuration Manager-Standortsystem andere Anwendungen ausführen, vergrößern Sie die Angriffsfläche dieses Computers.  




##  <a name="a-namebkmkwhat2knowa-what-to-know-before-choosing-to-use-custom-websites"></a><a name="BKMK_What2Know"></a> Wissenswertes vor der Entscheidung für den Einsatz benutzerdefinierter Websites  
 Standortsystemrollen verwenden standardmäßig die **Standardwebsite** in IIS. Diese wird automatisch konfiguriert, wenn die Standortsystemrolle installiert wird. An primären Standorten können Sie jedoch stattdessen benutzerdefinierte Websites verwenden. Wenn Sie benutzerdefinierte Websites verwenden:  

-   Benutzerdefinierte Websites sind für den gesamten Standort, nicht für einzelne Standortsystemserver oder Rollen aktiviert.  

-   An primären Standorten muss jeder Computer, der eine anwendbare Standortsystemrolle hosten wird, mit einer benutzerdefinierten Website namens **SMSWEB** konfiguriert werden. Bis diese Website erstellt wird und die Standortsystemrollen auf diesem Computer so konfiguriert werden, dass sie die benutzerdefinierte Website verwenden, können Clients möglicherweise nicht mit Standortsystemrollen auf diesem Computer kommunizieren.  

-   Da sekundäre Standorte automatisch für die Verwendung einer benutzerdefinierten Website konfiguriert sind, wenn Sie diese Option für den übergeordneten primären Standort aktiviert haben, müssen Sie auch benutzerdefinierte Websites in IIS auf jedem sekundären Standortsystemserver erstellen, der IIS benötigt.  


  **Voraussetzungen für die Verwendung benutzerdefinierter Websites:**  

 Vor der Aktivierung der Option zur Verwendung benutzerdefinierter Websites an einem Standort müssen Sie  

-   eine benutzerdefinierte Website mit dem Namen **SMSWEB** in IIS auf jedem Standortsystemserver erstellen, der IIS erfordert. Führen Sie dies am primären Standort und an allen untergeordneten sekundären Standorten durch.  

-   die benutzerdefinierte Website so konfigurieren, dass sie auf den gleichen Port reagiert, den Sie für die Configuration Manager-Clientkommunikation (Portnummer für Clientanfragen) konfigurieren.  

-   für jede benutzerdefinierte Website oder Standardwebsite, die einen benutzerdefinierten Ordner verwendet, eine Kopie des verwendeten Standarddokumenttyps im Stammordner platzieren, der die Website hostet. Auf einem Windows Server 2008 R2-Computer beispielsweise mit Standardkonfigurationen ist **iisstart.htm** eins der verfügbaren Standarddokumenttypen. Suchen Sie im Stammverzeichnis der Standardwebsite nach dieser Datei, und legen Sie eine Kopie dieser Datei (oder eine Kopie des verwendeten Standarddokumenttyps) in den Stammordner, der die benutzerdefinierte SMSWEB-Website hostet. Weitere Informationen zu Standarddokumenttypen finden Sie unter [Standarddokument&lt; defaultDocument\> für IIS](http://www.iis.net/configreference/system.webserver/defaultdocument).  

**Informationen zu IIS-Anforderungen:**
**Für die folgenden Standortsystemrollen sind IIS und eine Website zum Hosten der Standortsystemdienste erforderlich:**  

-   Anwendungskatalog-Webdienstpunkt  

-   Anwendungskatalog-Websitepunkt  

-   Verteilungspunkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

-   Fallbackstatuspunkt  

-   Verwaltungspunkt  

-   Softwareupdatepunkt  

-   Zustandsmigrationspunkt  

Weitere Aspekte:  

-   Wenn für einen primärer Standort benutzerdefinierte Websites aktiviert sind, werden diesem Standort zugewiesene Clients so weitergeleitet, dass sie mit den benutzerdefinierten Websites anstatt mit den Standardwebsites auf den betreffenden Standortsystemservern kommunizieren.  

-   Wenn Sie benutzerdefinierte Websites für einen primären Standort verwenden, erwägen Sie, benutzerdefinierte Websites für alle primären Standorte in Ihrer Hierarchie zu verwenden, damit ein erfolgreiches Roaming von Clients innerhalb der Hierarchie möglich ist. (Roaming heißt der Vorgang, bei dem ein Clientcomputer zu einem neuen Netzwerksegment wechselt, das von einem anderen Standort verwaltet wird. Roaming kann Einfluss darauf haben, auf welche Ressourcen der Client lokal anstatt über eine WAN-Verbindung zugreifen kann.)  

-   Standortsystemrollen wie der Reporting Services-Punkt, die IIS verwenden, aber keine Clientverbindungen akzeptieren, verwenden ebenfalls die Website SMSWEB anstelle der Standardwebsite.  

-   Benutzerdefinierte Websites erfordern das Zuweisen von Portnummern, die sich von denjenigen unterscheiden, die von der Standardwebsite der Computer verwendet werden. Eine Standardwebsite und benutzerdefinierte Website können nicht gleichzeitig ausgeführt werden, wenn beide Websites versuchen, dieselben TCP/IP-Ports zu verwenden.  

-   Die TCP/IP-Ports, die Sie in IIS für die benutzerdefinierte Website konfigurieren, müssen mit den Clientanforderungsports des Standorts übereinstimmen.  

## <a name="switching-between-default-and-custom-websites"></a>Wechseln zwischen Standard- und benutzerdefinierten Websites  
Obwohl Sie das Kontrollkästchen zur Verwendung benutzerdefinierter Websites bei einem primären Standort jederzeit aktivieren bzw. deaktivieren können (Sie finden es auf der Seite „Eigenschaften“ auf der Registerkarte „Allgemein“), sollten Sie sorgfältig planen, bevor Sie diese Änderung vornehmen. Wenn diese Konfiguration geändert wird, müssen alle betreffenden Standortsystemrollen am primären Standort und untergeordneten sekundären Standorten deinstalliert und erneut installiert werden:  

Die folgenden Rollen werden **automatisch neu installiert**:  

-   Verwaltungspunkt  

-   Verteilungspunkt  

-   Softwareupdatepunkt  

-   Fallbackstatuspunkt  

-   Zustandsmigrationspunkt  

Die folgenden Rollen müssen **manuell neu installiert werden**:  

-   Anwendungskatalog-Webdienstpunkt  

-   Anwendungskatalog-Websitepunkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

Darüber hinaus gilt:  

-   Wenn Sie von der Standardwebsite zu einer benutzerdefinierten Website wechseln, werden die alten virtuellen Verzeichnisse nicht von Configuration Manager entfernt. Wenn Sie von Configuration Manager verwendete Dateien entfernen möchten, müssen Sie die virtuellen Verzeichnisse, die unter der Standardwebsite erstellt wurden, manuell löschen.  

-   Wenn Sie am Standort zu benutzerdefinierten Websites wechseln, müssen Clients, die bereits dem Standort zugewiesen sind, so neu konfiguriert werden, dass die neuen Clientanforderungsports für die benutzerdefinierten Websites verwendet werden. Weitere Informationen finden Sie unter [Konfigurieren von Clientkommunikationsports in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

## <a name="configure-custom-websites"></a>Konfigurieren benutzerdefinierter Websites  
Da die Schritte zum Erstellen einer benutzerdefinierten Website bei verschiedenen Betriebssystemversionen variieren, konsultieren Sie die Dokumentation Ihrer Betriebssystemversion hinsichtlich der genauen Schritte, doch befolgen Sie, sofern zutreffend, die folgenden Vorgaben:  

-   Der Websitename muss **SMSWEB**lauten.  

-   Beim Konfigurieren von HTTPS müssen Sie ein SSL-Zertifikat angeben, bevor Sie die Konfiguration speichern können.  

-   Nachdem Sie die benutzerdefinierte Website erstellt haben, entfernen Sie die benutzerdefinierten Websiteports, die von anderen Websites in IIS genutzt werden:  

    1.  Bearbeiten Sie die **Bindungen** der anderen Websites so, dass Ports entfernt werden, die denjenigen entsprechen, die der Website **SMSWEB** zugewiesen sind.  

    2.  Starten Sie die Website **SMSWEB** .  

    3.  Starten Sie den Dienst **SMS_SITE_COMPONENT_MANAGER** auf dem Standortserver des Standorts neu.  



<!--HONumber=Dec16_HO3-->


