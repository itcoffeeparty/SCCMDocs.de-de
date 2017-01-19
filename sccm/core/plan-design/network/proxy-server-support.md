---
title: "Unterstützung von Proxyservern | Microsoft-Dokumentation"
description: "Erfahren Sie mehr zur Unterstützung der von Standortsystemservern und Clients verwendeten Proxyserver durch System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 97f9cc792d1fea20c32f38bc98cbdfb9ba90640d


---
# <a name="proxy-server-support-in-system-center-configuration-manager"></a>Unterstützung von Proxyservern in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sowohl System Center Configuration Manager-Standortsystemserver als auch Clients können einen Proxyserver verwenden.  

## <a name="site-system-servers"></a>Standortsystemserver  
Sind für Standortsystemrollen Verbindungen mit dem Internet erforderlich, können Sie die Rollen so konfigurieren, dass sie einen Proxyserver verwenden.  

-   Ein Computer, der einen Standortsystemserver hostet, unterstützt eine einzelne Proxyserverkonfiguration, die von allen Standortsystemrollen auf diesem Computer freigegeben wurde. Wenn Sie getrennte Proxyserver für verschiedene Rollen oder Instanzen einer Rolle benötigen, müssen Sie diese Rollen auf separaten Standortsystemservern platzieren.  

-   Wenn Sie neue Proxyservereinstellungen für einen Standortsystemserver konfigurieren, für den es bereits eine Proxyserverkonfiguration gibt, wird die ursprüngliche Konfiguration überschrieben.  

-   Verbindungen zum Proxy verwenden das Konto **System** des Computers, der die Standortsystemrolle hostet.  

Die folgenden Standortsystemrollen stellen eine Verbindung zum Internet her und benötigen möglicherweise einen Proxyserver.  Mit einer Ausnahme verwenden Standortsystemrollen, die dies können, einen Proxy ohne zusätzliche Konfiguration. Die Ausnahme ist der Softwareupdatepunkt. Die folgende Liste enthält Informationen zu den zusätzlichen Konfigurationen, die für einen Softwareupdatepunkt erforderlich sind:  

**Asset Intelligence-Synchronisierungspunkt** – diese Standortsystemrolle stellt eine Verbindung mit Microsoft her und verwendet eine Proxyserverkonfiguration auf dem Computer, auf dem der Asset Intelligence-Synchronisierungspunkt gehostet wird.  

**Cloudbasierter Verteilungspunkt** – Um einen Proxyserver für einen cloudbasierten Verteilungspunkt zu konfigurieren, konfigurieren Sie den Proxy auf dem primären Standort, der den cloudbasierten Verteilungspunkt verwaltet.  

Für diese Konfiguration gilt für den primären Standortserver Folgendes:  

-   Er muss in der Lage sein, eine Verbindung mit Microsoft Azure herzustellen, um Inhalte für den Verteilungspunkt bereitzustellen, zu überwachen und zu verteilen.  

-   Er verwendet das System-Konto dieses Computers, um die Verbindung herzustellen.  

-   Er verwendet den Standardwebbrowser dieses Computers.  

Sie können keinen Proxyserver auf dem cloudbasierten Verteilungspunkt in Microsoft Azure konfigurieren.  

**Cloudverbindungspunkt** – Diese Standortsystemrolle stellt eine Verbindung mit dem Configuration Manager-Clouddienst her, um Versionsupdates für Configuration Manager herunterzuladen, und verwendet einen Proxyserver, der auf dem Computer konfiguriert ist, der den Dienstverbindungspunkt hostet.  

**Der Exchange Server-Connector:** Diese Standortsystemrolle stellt eine Verbindung mit einem Exchange Server her und verwendet eine Proxyserverkonfiguration auf dem Computer, auf dem der Exchange Server-Connector gehostet wird.  

**Dienstverbindungspunkt** – Für diese Standortsystemrolle wird eine Verbindung mit Microsoft Intune hergestellt, und es wird eine Proxyserverkonfiguration auf dem Computer verwendet, auf dem der Dienstverbindungspunkt gehostet wird.  

**Softwareupdatepunkt** – Diese Standortsystemrolle kann den Proxy zur Verbindung mit Microsoft Update verwenden, um Patches herunterzuladen und Informationen zu Updates zu synchronisieren.   
Softwareupdatepunkte verwenden nur dann einen Proxy für die beiden folgenden Optionen, wenn Sie diese Option beim Konfigurieren des Softwareupdatepunkts aktivieren:  

-   **Verwenden von Proxyserver beim Synchronisieren von Softwareupdates**  

-   **Proxyserver beim Herunterladen von Inhalt mithilfe der Regeln zur automatischen Bereitstellung verwenden** (Obwohl sie zur Verwendung verfügbar ist, wird diese Einstellung von Softwareupdatepunkten in sekundären Standorten nicht verwendet.)  

Konfigurieren Sie die Proxyservereinstellungen im Assistent zum Hinzufügen von Standortsystemrollen auf der Seite „Aktiver Softwareupdatepunkt“ oder in „Eigenschaften der Softwareupdatepunktkomponente“ auf der Registerkarte „Allgemein“.  

-   Die Proxyservereinstellungen werden nur dem Softwareupdatepunkt am Standort zugeordnet.  

-   Proxyserveroptionen sind nur verfügbar, wenn bereits ein Proxyserver für den Standortsystemserver konfiguriert ist, der den Softwareupdatepunkt hostet.  

> [!NOTE]  
>  Das Konto **System** für den Server, auf dem die automatische Bereitstellungsregel erstellt wurde, wird bei der Ausführung der automatischen Bereitstellungsregeln standardmäßig zum Herstellen der Verbindung mit dem Internet und zum Herunterladen von Softwareupdates verwendet.  
>   
>  Wenn über dieses Konto keine Verbindung mit dem Internet hergestellt werden kann, können keine Softwareupdates heruntergeladen werden. In diesem Fall wird der Datei „ruleengine.log“ der folgende Eintrag hinzugefügt: **Fehler beim Herunterladen des Updates aus dem Internet. Fehler = 12007**.  

#### <a name="to-configure-the-proxy-server-for-a-site-system-server"></a>So konfigurieren Sie den Proxyserver für einen Standortsystemserver  

1.  Klicken Sie in der Configuration Manager-Konsole auf „Verwaltung“, erweitern Sie „Standortkonfiguration“, und klicken Sie dann auf „Server- und Standortsystemrollen“.  

2.  Wählen Sie den Standortsystemserver aus, den Sie bearbeiten möchten, und klicken Sie im Detailbereich mit der rechten Maustaste auf Standortsystem, und wählen Sie Eigenschaften.  

3.  Wählen Sie unter Eigenschaften des Standortsystems die Registerkarte Proxy aus, und konfigurieren Sie die Proxyeinstellungen für diesen primären Standortserver.  

4.  Klicken Sie auf OK, um die neue Proxyserverkonfiguration zu speichern.  



<!--HONumber=Dec16_HO3-->


