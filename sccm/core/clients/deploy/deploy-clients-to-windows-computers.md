---
title: Bereitstellen von Windows-Clients | System Center Configuration Manager
description: Erfahren Sie, wie Sie Clients auf Windows-Computern in System Center Configuration Manager bereitstellen.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
caps.latest.revision: 13
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5a52386c6327ded3c5a400c7a046a6a12af96bae


---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können verschiedene Clientbereitstellungsmethoden verwenden, um die System Center Configuration Manager-Clientsoftware auf Computern zu installieren. Eine Hilfestellung bei der Entscheidung für eine Bereitstellungsmethode finden Sie unter [Clientinstallationsmethoden in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

 Vergewissern Sie sich, dass alle Voraussetzungen erfüllt sind und Sie alle erforderlichen Bereitstellungskonfigurationen abgeschlossen haben, bevor Sie Configuration Manager-Clients installieren. Weitere Informationen finden Sie unter [Voraussetzungen für die Bereitstellung von Clients auf Windows-Computern in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  


##  <a name="a-namebkmkclientpusha-how-to-install-configuration-manager-clients-by-using-client-push"></a><a name="BKMK_ClientPush"></a> Installieren von Configuration Manager-Clients mithilfe der Clientpushinstallation  

 Verwenden Sie die Clientpushinstallation, um die Configuration Manager-Clientsoftware auf von Configuration Manager ermittelten Computern zu installieren. Sie können die Clientpushinstallation für einen Standort konfigurieren, wird sie automatisch auf den Computern ausgeführt, die innerhalb der konfigurierten Standortgrenzen ermittelt wurden, sofern diese Grenzen als Begrenzungsgruppe konfiguriert wurden. Sie können die Clientpushinstallation auch initiieren, indem Sie den Clientpushinstallations-Assistenten für eine bestimmte Sammlung oder für eine bestimmte Ressource innerhalb einer Sammlung ausführen.  

 Sie können den Clientpushinstallations-Assistenten außerdem verwenden, um den Configuration Manager-Client auf Computern zu installieren, die als Ergebnisse einer Abfrage zurückgegeben werden. Zu den von der ausgewählten Abfrage zurückgegebenen Elementen muss das Attribut **Ressourcen-ID** der Attributklasse **Systemressource**gehören, damit die Installation in diesem Szenario erfolgreich ausgeführt werden kann. Weitere Informationen zu Abfragen finden Sie unter [Abfragen – Technische Referenz für System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md).  

 Wenn vom Standortserver kein Kontakt zum Clientcomputer hergestellt oder der Installationsvorgang nicht gestartet werden kann, wird bis zu 7 Tage lang stündlich ein weiterer Installationsversuch gestartet, bis die Installation erfolgreich abgeschlossen wird.  

 Installieren Sie das Standortsystem „Fallbackstatuspunkt“, bevor Sie die Clients installieren, um den Clientinstallationsprozess besser nachverfolgen zu können. Wenn ein Fallbackstatuspunkt installiert ist, wird er automatisch Clients zugewiesen, wenn diese mithilfe von Clientpushinstallation installiert werden. Verfolgen Sie den Clientinstallationsfortschritt anhand der Clientbereitstellungs- und -zuweisungsberichte nach. Zusätzlich finden Sie in den Clientprotokolldateien ausführlichere Informationen zur Problembehebung. Die Installation eines Fallbackstatuspunkts ist für Clientprotokolldateien nicht erforderlich. Beispielsweise werden alle Probleme, die beim Verbindungsversuch des Standortservers mit dem Computer auftreten, in der Datei CCM.log auf dem Standortserver aufgezeichnet, und der Installationsvorgang wird in der Datei CCMSetup.log auf dem Client aufgezeichnet.  

> [!IMPORTANT]  
>  Vergewissern Sie sich, dass alle Voraussetzungen erfüllt sind, damit die Clientpushinstallation erfolgreich abgeschlossen werden kann. Diese finden Sie im Abschnitt „Installationsmethodenabhängigkeiten“ des Artikels [Voraussetzungen für die Bereitstellung von Clients auf Windows-Computern in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  

#### <a name="to-configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>So konfigurieren Sie den Standort für die automatische Verwendung von Clientpush für ermittelte Computer  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.  

3.  Wählen Sie in der Liste **Standorte** den Standort aus, für den Sie die automatische standortweite Clientpushinstallation konfigurieren möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Clientinstallationseinstellungen**, und klicken Sie dann auf **Clientpushinstallation**.  

5.  Aktivieren Sie im Dialogfeld **Eigenschaften der Clientpushinstallation** auf der Registerkarte **Allgemein** das Kontrollkästchen **Automatische standortweite Clientpushinstallation aktivieren**. Wählen Sie aus **Server**, **Arbeitsstationen** oder **Configuration Manager-Standortsystemserver** die Systemtypen aus, auf denen die Clientsoftware von Configuration Manager mithilfe von Push installiert werden soll. In der Standardeinstellung sind **Server** und **Arbeitsstationen**ausgewählt.  

6.  Wählen Sie aus, ob die Configuration Manager-Clientsoftware von der automatischen, standortweiten Clientpushinstallation auf Domänencontrollern installiert werden soll.  

7.  Geben Sie auf der Registerkarte **Konten** mindestens ein Konto an, das von Configuration Manager verwendet werden soll, um eine Verbindung mit dem Computer zur Installation der Clientsoftware herzustellen. Klicken Sie auf das Symbol **Erstellen** , geben Sie den **Benutzernamen** und das **Kennwort**ein, bestätigen Sie das Kennwort, und klicken Sie dann auf **OK**. Sie müssen mindestens ein Konto für die Clientpushinstallation angeben, das über lokale Administratorrechte auf jedem Computer verfügen muss, auf dem der Client installiert werden soll. Wenn Sie kein Konto für die Clientpushinstallation angeben, versucht Configuration Manager, das Konto des Standortsystemcomputers zu verwenden, was zu einem Fehler bei der domänenübergreifenden Clientpushinstallation führt.  

    > [!IMPORTANT]  
    >  Das Kennwort für das Clientpushinstallationskonto darf maximal 38 Zeichen lang sein.  

    > [!NOTE]  
    >  Wenn Sie die Clientpushinstallation von einem sekundären Standort aus verwenden möchten, muss das Konto an dem sekundären Standort, an dem Clientpush initiiert werden soll, angegeben werden.  
    >   
    >  Weitere Informationen zum Clientpushinstallationskonto finden Sie im nächsten Abschnitt „So verwenden Sie den Clientpushinstallations-Assistenten“.  

8.  Geben Sie auf der Registerkarte **Installationseigenschaften** alle Installationseigenschaften an, die bei der Installation des Configuration Manager-Clients verwendet werden sollen. Sie können beliebige Installationseigenschaften für das Windows Installer-Paket („Client.msi“) sowie die folgenden Eigenschaften für „CCMSetup.exe“ angeben:  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     Die auf dieser Registerkarte angegebenen Clientinstallationseigenschaften werden in Active Directory Domain Services veröffentlicht, wenn das Schema für Configuration Manager erweitert wird, und sie werden von Clientinstallationen gelesen, bei denen CCMSetup ohne Installationseigenschaften ausgeführt wird. Weitere Informationen zu den Clientinstallationseigenschaften finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!NOTE]  
    >  Wenn Sie die Clientpushinstallation auf einem sekundären Standort aktivieren, achten Sie darauf, dass die SMSSITECODE-Eigenschaft auf den Configuration Manager-Standortnamen des übergeordneten primären Standorts festgelegt ist. Wenn das Active Directory-Schema für Configuration Manager erweitert wurde, können Sie auch auf den Wert „Automatisch“ festlegen, um die korrekte Standortzuweisung automatisch suchen zu lassen.  

#### <a name="to-use-the-client-push-installation-wizard"></a>So verwenden Sie den Clientpushinstallations-Assistenten  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.  

3.  Wählen Sie in der Liste **Standorte** den Standort aus, für den Sie die automatische standortweite Clientpushinstallation konfigurieren möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Clientinstallationseinstellungen**, und klicken Sie dann auf **Clientpushinstallation**.  

5.  Geben Sie auf der Registerkarte **Installationseigenschaften** alle Installationseigenschaften an, die bei der Installation des Configuration Manager-Clients verwendet werden sollen. Sie können beliebige Installationseigenschaften für das Windows Installer-Paket („Client.msi“) sowie die folgenden Eigenschaften für „CCMSetup.exe“ angeben:  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     Die auf dieser Registerkarte angegebenen Clientinstallationseigenschaften werden in Active Directory Domain Services veröffentlicht, wenn das Schema für Configuration Manager erweitert wird, und sie werden von Clientinstallationen gelesen, bei denen CCMSetup ohne Installationseigenschaften ausgeführt wird. Weitere Informationen zu den Clientinstallationseigenschaften finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

6.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

7.  Wählen Sie im Arbeitsbereich **Bestand und Kompatibilität** einen oder mehrere Computer oder eine Sammlung von Computern aus.  

8.  Wählen Sie auf der Registerkarte **Startseite** eine der folgenden Optionen aus:  

    -   Wenn Sie den Client auf einem oder mehreren Computern installieren möchten, klicken Sie in der Gruppe **Geräte** auf **Client installieren**.  

    -   Wenn Sie den Client auf einer Sammlung Computern installieren möchten, klicken Sie in der Gruppe **Sammlung** auf **Client installieren**.  

9. Überprüfen Sie im ** ** Assistenten zum Installieren von Configuration Manager-Clients auf der Seite **Vorbereitung**die Informationen, und klicken Sie dann auf **Weiter**.  

10. Konfigurieren Sie auf der Seite **Installationsoptionen** , ob der Client auf Domänencontrollern installiert werden kann und ob der Client bei Computern mit vorhandenem Client neu installiert oder repariert bzw. ob ein Upgrade des vorhandenen Clients ausgeführt werden soll. Konfigurieren Sie außerdem den Namen des Standorts, von dem aus die Installation der Clientsoftware ausgeführt wird. Klicken Sie auf **Weiter**.  

11. Überprüfen Sie die Installationseinstellungen, und schließen Sie dann den Assistenten.  

> [!NOTE]  
>  Sie können über den Assistenten Clients installieren, auch wenn der Standort gar nicht für Clientpush konfiguriert ist.  

##  <a name="a-namebkmkclientsupa-how-to-install-configuration-manager-clients-by-using-software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> So installieren Sie Configuration Manager-Clients mithilfe von auf Softwareupdate basierender Installation  
 Bei der auf Softwareupdate basierenden Clientinstallation wird der Configuration Manager-Client als zusätzliches Softwareupdate auf einem Softwareupdatepunkt veröffentlicht. Diese Clientinstallationsmethode kann zur Installation des Configuration Manager-Clients auf Computern, auf denen der Client noch nicht installiert ist, sowie zum Ausführen von Upgrades bei vorhandenen Configuration Manager-Clients verwendet werden.  

 Ist der Configuration Manager-Client auf einem Computer bereits installiert, stellt Configuration Manager den Servernamen und den Port für den Softwareupdatepunkt bereit, von dem Softwareupdates abgerufen werden sollen. Diese Informationen sind in der Clientrichtlinie enthalten.  

> [!IMPORTANT]  
>  Sie müssen zum Installieren des Clients und für Softwareupdates den gleichen WSUS-Server (Windows Server Update Services) verwenden, wenn Sie die auf Softwareupdate basierende Installation verwenden möchten. Dieser Server muss an einem primären Standort der aktive Softwareupdatepunkt sein. Weitere Informationen finden Sie unter [Install a software update point (Installieren eines Softwareupdatepunkts)](../../../sum/get-started/install-a-software-update-point.md).  

 Wenn der Configuration Manager-Client auf einem Computer nicht installiert ist, müssen Sie ein Gruppenrichtlinienobjekt (Group Policy Object, GPO) in Active Directory Domain Services konfigurieren und zuweisen, um den Servernamen des Softwareupdatepunkts anzugeben, von dem der Computer Softwareupdates abrufen sollen.  

 Sie können der auf Softwareupdate basierenden Clientinstallation keine Befehlszeileneigenschaften hinzufügen. Wenn Sie das Active Directory-Schema für Configuration Manager erweitert haben, werden die Active Directory Domain Services von den Clientcomputern bei deren Installation automatisch nach den Installationseigenschaften abgefragt.  

 Wenn Sie das Active Directory-Schema nicht erweitert haben, können Sie die Clientinstallationseinstellungen für Computer an Ihrem Standort mithilfe einer Gruppenrichtlinie bereitstellen. Diese Einstellungen werden bei allen auf Softwareupdate basierenden Clientinstallationen automatisch angewendet. Weitere Informationen finden Sie unter [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](#BKMK_Provision) (gruppenrichtlinien- und updatebasierte Clientinstallation) und [Zuweisen von Clients zu einem Standort in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

 Gehen Sie wie folgt vor, um Computer ohne Configuration Manager-Client so zu konfigurieren, dass sie den Softwareupdatepunkt für die Clientinstallation und Softwareupdates verwenden und die Configuration Manager-Clientsoftware auf dem Softwareupdatepunkt veröffentlichen.  

> [!NOTE]  
>  Wenn sich Computer im Anschluss an eine vorherige Softwareinstallation im Status „Neustart ausstehend“ befinden, dann kann eine auf dem Softwareupdate basierende Clientinstallation zum Neustart des Computers führen.  

#### <a name="to-configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>So konfigurieren Sie ein Gruppenrichtlinienobjekt in den Active Directory-Domänendiensten, um den Softwareupdatepunkt für die Clientinstallation und für Softwareupdates anzugeben  

1.  Verwenden Sie die Gruppenrichtlinien-Verwaltungskonsole, um ein neues oder vorhandenes Gruppenrichtlinienobjekt zu öffnen.  

2.  Erweitern Sie in der Konsole **Computerkonfiguration**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **Windows-Komponenten**, und klicken Sie dann auf **Windows Update**.  

3.  Öffnen Sie die Eigenschaften der Einstellung **Internen Pfad für den Microsoft Updatedienst angeben**, und klicken Sie dann auf **Aktiviert**.  

4.  Geben Sie im Feld **Interner Updatedienst zum Ermitteln von Updates**den Servernamen und den Port des Softwareupdatepunkts, den Sie verwenden möchten, an. Beide müssen exakt mit dem vom Softwareupdatepunkt verwendeten Servernamenformat und Port übereinstimmen:  

    -   Falls das Configuration Manager-Standortsystem für die Verwendung eines vollständig qualifizierten Domänennamens (Fully Qualified Domain Name, FQDN) konfiguriert ist, geben Sie den Servernamen im FQDN-Format an.  

    -   Falls das Configuration Manager-Standortsystem nicht für die Verwendung eines FQDN konfiguriert ist, geben Sie den Servernamen im Kurznamenformat an.  

    > [!NOTE]  
    >  Informationen zum Bestimmen der Portnummer, die vom Softwareupdatepunkt verwendet wird, finden Sie unter [Bestimmen der Porteinstellungen für WSUS in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

     Beispiel: **http://server1.contoso.com:8530**  

5.  Geben Sie im Feld **Intranetserver für die Statistik**den Namen des Intranetservers für die Statistik, den Sie verwenden möchten, an. Für die Angabe dieses Servers gelten keine speziellen Anforderungen. Es kann ein anderer Computer als der Softwareupdatepunkt-Server sein, und bei Verwendung desselben Servers darf das Format abweichen.  

6.  Weisen Sie das Gruppenrichtlinienobjekt den Computern zu, auf denen Sie den Configuration Manager-Client installieren und Softwareupdates erhalten möchten.  

#### <a name="to-publish-the-configuration-manager-client-to-the-software-update-point"></a>So veröffentlichen Sie den Configuration Manager-Client auf dem Softwareupdatepunkt  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.  

3.  Wählen Sie in der Liste **Standorte** den Standort aus, für den Sie die auf Softwareupdate basierende Clientinstallation konfigurieren möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Clientinstallationseinstellungen**, und klicken Sie dann auf **Auf Softwareupdate basierende Clientinstallation**.  

5.  Aktivieren Sie im Dialogfeld **Eigenschaften der auf Softwareupdate basierenden Clientinstallation** das Kontrollkästchen **Auf Softwareupdate basierende Clientinstallation aktivieren** , um diese Clientinstallationsmethode zu aktivieren.  

6.  Wenn auf dem Configuration Manager-Standortserver eine höhere Clientsoftwareversion als auf dem Softwareupdatepunkt gespeichert ist, wird das Dialogfeld **Höhere Version des Clientpakets erkannt** angezeigt. Klicken Sie auf **Ja** , um die aktuelle Version der Clientsoftware auf dem Softwareupdatepunkt zu veröffentlichen.  

    > [!NOTE]  
    >  Wenn die Clientsoftware noch nicht auf dem Softwareupdatepunkt veröffentlicht wurde, ist dieses Feld leer.  

7.  Klicken Sie auf **OK**, um die Konfiguration der Clientinstallation mithilfe des Softwareupdatepunkts abzuschließen.  

> [!NOTE]  
>  Das Softwareupdate für den Configuration Manager-Client wird nicht automatisch aktualisiert, wenn eine neue Version vorhanden ist. Wenn Sie ein Standortupgrade ausführen, das eine neue Clientversion enthält, müssen Sie dieses Verfahren wiederholen und bei Schritt 6 auf **Ja** klicken.  

##  <a name="a-namebkmkclientgpa-how-to-install-configuration-manager-clients-by-using-group-policy"></a><a name="BKMK_ClientGP"></a> So installieren Sie Configuration Manager-Clients mithilfe von Gruppenrichtlinien  
 Mithilfe von Gruppenrichtlinien in Active Directory Domain Services können Sie den Configuration Manager-Client veröffentlichen oder Computern in Ihrem Unternehmen für die Installation zuzuweisen. Wenn Sie den Configuration Manager-Client mithilfe einer Gruppenrichtlinie Computern zuweisen, wird der Client beim nächsten Computerstart installiert. Wenn Sie den Configuration Manager-Client mithilfe einer Gruppenrichtlinie für Benutzer veröffentlichen, wird der Client in der Systemsteuerung des Computers unter **Software** zur Installation durch den Benutzer angezeigt.  

 Verwenden Sie das Windows Installer-Paket (CCMSetup.msi) bei auf Gruppenrichtlinien basierenden Installationen. Diese Datei befindet sich im Ordner **&lt;ConfigMgr-Installationsverzeichnis\>\bin\i386** auf dem Configuration Manager-Standortserver. Sie können dieser Datei keine Eigenschaften hinzufügen, um das Installationsverhalten zu ändern:  

> [!IMPORTANT]  
>  Sie müssen über Administratorberechtigungen für den Ordner verfügen, um auf die Clientinstallationsdateien zugreifen zu können.  

-   Wenn das Active Directory-Schema für Configuration Manager erweitert wurde und im Dialogfeld **Standorteigenschaften** auf der Registerkarte **Erweitert** die Option **Diesen Standort in Active Directory Domain Services veröffentlichen** ausgewählt ist, werden Active Directory Domain Services automatisch von den Clientcomputern nach Installationseigenschaften durchsucht. Weitere Informationen zu den Installationseigenschaften, die veröffentlicht werden, finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager, die in Active Directory-Domänendiensten veröffentlicht wurden](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   Wenn das Active Directory-Schema nicht erweitert wurde, können Sie das folgende Verfahren in diesem Thema anwenden, um Installationseigenschaften in der Computerregistrierung zu speichern: [Bereitstellen der Clientinstallationseigenschaften (auf einer Gruppenrichtlinie oder auf einem Softwareupdate basierende Clientinstallation)](#BKMK_Provision). Diese Eigenschaften werden dann verwendet, wenn der Configuration Manager-Client installiert wird.  

 Weitere Informationen zum Verwenden von Gruppenrichtlinien in den Active Directory-Domänendiensten zur Softwareinstallation finden Sie in Ihrer Windows Server-Dokumentation.  

##  <a name="a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually"></a><a name="BKMK_Manual"></a> Manuelles Installieren von Configuration Manager-Clients  
 Mithilfe des Programms „CCMSetup.exe“ können Sie die Configuration Manager-Clientsoftware manuell auf Computern in Ihrem Unternehmen installieren. Sie finden dieses Programm und die unterstützenden Dateien im Ordner **Client** des Configuration Manager-Installationsordners auf dem Standortserver und an den Verwaltungspunkten an Ihrem Standort. Dieser Ordner ist im Netzwerk freigegeben unter  

 \\\\*&lt;Name des Standortservers\>*\SMS_*&lt;Standortcode\>*\Client\  

 wobei *&lt;Name des Standortservers\>* der Name eines der Server ist, die einen Verwaltungspunkt hosten, und *&lt;Standortcode\>* der Code des primären Standorts ist, zu dem der Client gehören soll.  Zum Ausführen von „CCMSetup.exe“ in der Befehlszeile auf dem Client müssen Sie diesem Speicherort ein Netzlaufwerk zuordnen und dann den Befehl ausführen.  

> [!IMPORTANT]  
>  Sie müssen über Administratorberechtigungen für den Ordner verfügen, um auf die Clientinstallationsdateien zugreifen zu können.  

 Von CCMSetup.exe werden alle notwendigen Installationsvoraussetzungen auf den Clientcomputer kopiert, und das Windows Installer-Paket (Client.msi) wird aufgerufen, um die Clientinstallation auszuführen.  

> [!IMPORTANT]  
>  Sie können Client.msi nicht direkt ausführen.  

 Sie können sowohl für CCMSetup.exe als auch für Client.msi Befehlszeileneigenschaften angeben, um das Verhalten der Clientinstallation zu ändern. Geben Sie unbedingt zuerst die CCMSetup-Eigenschaften an (die Eigenschaften, die mit „**/**“ beginnen), bevor Sie die Eigenschaften für „Client.msi“ angeben.  

 Sie können z. B. den folgenden Befehl angeben:  

```  
CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01  
```  

 Der Client wird mit den folgenden Eigenschaften installiert:  

|Eigenschaft|Beschreibung|  
|--------------|-----------------|  
|**/mp:SMSMP01**|Mit dieser CCMSetup-Eigenschaft wird der Verwaltungspunkt SMSMP01 zum Herunterladen der erforderlichen Clientinstallationsdateien angegeben.|  
|**/logon**|Mit dieser CCMSetup-Eigenschaft wird angegeben, dass die Installation beendet werden soll, wenn ein vorhandener Configuration Manager-Client auf dem Computer gefunden wird.|  
|**SMSSITECODE=AUTO**|Mit dieser Client.msi-Eigenschaft wird angegeben, dass vom Client versucht werden soll, den zu verwendenden Configuration Manager-Standortcode zu finden, beispielsweise mithilfe von Active Directory Domain Services.|  
|**FSP=SMSFP01**|Mit dieser Client.msi-Eigenschaft wird angegeben, dass der Fallbackstatuspunkt SMSFP01 verwendet werden soll, um vom Clientcomputer gesendete Zustandsmeldungen zu empfangen.|  

 Informationen zu allen Eigenschaften von „CCMSetup.exe“ finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="examples-for-installing-configuration-manager-clients-manually"></a>Beispiele für die manuelle Installation von Configuration Manager-Clients  
 Diese Beispiele gelten für Active Directory-Clients im Intranet und verwenden die folgenden Werte, um verschiedene Aspekte des Standorts darzustellen:  

 **MPSERVER** = Der Server, der den Verwaltungspunkt hostet   
**FSPSERVER** = Der Server, der den Fallbackstatuspunkt hostet  
**ABC** = Der Standortcode  
**contoso.com** = Domänenname  

 Alle Standortsystemserver werden mit einem Intranet-FQDN konfiguriert, und der Standort wird in der Active Directory-Gesamtstruktur des Clients veröffentlicht.  

 Melden Sie sich am Clientcomputer als lokaler Administrator an, ordnen Sie „\\\MPSERVER\SMS_ABC\Client“ ein Laufwerk (Z:) zu, ändern Sie die Befehlseingabeaufforderung in Laufwerk Z, und führen Sie dann einen der folgenden Befehle aus.  

 **Beispiel 1:**  

```  
CCMSetup.exe  
```  

> [!NOTE]  
>  In diesem Beispiel wird der Client ohne zusätzliche Eigenschaften installiert, sodass der Client automatisch mit den in den Active Directory-Domänendiensten veröffentlichten Clientinstallationseigenschaften konfiguriert wird. Der Client wird beispielsweise automatisch für den Standortcode (Netzwerkadresse des Clients muss sich in einer für die Clientzuweisung konfigurierten Begrenzungsgruppe befinden), für einen Verwaltungspunkt sowie für den Fallbackstatuspunkt konfiguriert, und es wird festgelegt, ob die Clientkommunikation nur über HTTPS erfolgen soll. Weitere Informationen zu den Clientinstallationseigenschaften, die für Active Directory-Clients automatisch konfiguriert werden können, finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager, die in Active Directory-Domänendiensten veröffentlicht wurden](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Beispiel 2:**  

```  
CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com  
```  

> [!NOTE]  
>  In diesem Beispiel wird die automatische Konfiguration außer Kraft gesetzt, die von Active Directory Domain Services bereitgestellt werden kann. Die Netzwerkadresse des Clients muss sich hier nicht in einer für die Clientzuweisung konfigurierten Begrenzungsgruppe befinden. Stattdessen werden bei der Installation der Standort, ein Intranetverwaltungspunkt und ein internetbasierter Verwaltungspunkt sowie ein Fallbackstatuspunkt angegeben, der Verbindungen aus dem Internet akzeptiert. Darüber hinaus wird festgelegt, dass ein Client-PKI-Zertifikat (sofern verfügbar) mit der längsten Gültigkeitsdauer verwendet werden soll.  

##  <a name="a-namebkmkclientlogonscripta-how-to-install-configuration-manager-clients-by-using-logon-scripts"></a><a name="BKMK_ClientLogonScript"></a> So installieren Sie Configuration Manager-Clients mithilfe von Anmeldeskripts  
 Configuration Manager unterstützt Anmeldeskripts bei der Installation der Configuration Manager-Clientsoftware. Sie können die Programmdatei **CCMSetup.exe** in einem Anmeldeskript verwenden, um die Clientinstallation auszulösen.  

 Bei der Anmeldeskriptinstallation werden dieselben Methoden wie bei der manuellen Clientinstallation verwendet. Sie können die Installationseigenschaft **/logon** für CCMSsetup.exe angeben, sodass der Client nur dann installiert wird, wenn noch keine Version des Clients auf dem Computer vorhanden ist. Dadurch wird verhindert, dass der Client jedesmal neu installiert wird, wenn das Anmeldeskript ausgeführt wird.  

 Wenn weder eine Installationsquelle, die die **/Source**-Eigenschaft verwendet, noch ein Verwaltungspunkt (mithilfe der **/MP**-Eigenschaft), von dem die Installation bezogen werden kann, angegeben wurde, kann „CCMSsetup.exe“ den Verwaltungspunkt finden, indem Active Directory Domain Services durchsucht wird. Dies funktioniert nur, wenn das Schema für Configuration Manager erweitert wurde und der Standort in den Active Directory Domain Services veröffentlicht ist. Alternativ können DNS oder WINS vom Client verwendet werden, um einen Verwaltungspunkt zu finden.  

##  <a name="a-namebkmkclientappa-how-to-install-configuration-manager-clients-by-using-a-package-and-program"></a><a name="BKMK_ClientApp"></a> So installieren Sie Configuration Manager-Clients mithilfe Paketen und Programmen  
 Sie können Configuration Manager zum Erstellen und Bereitstellen von Paketen und Programmen verwenden, mit denen die Clientsoftware für ausgewählte Computer in Ihrer Hierarchie upgegradet wird. Configuration Manager umfasst eine Paketdefinitionsdatei, mit der die Paketeigenschaften mit häufig verwendeten Werten aufgefüllt werden. Sie können das Verhalten der Clientinstallation anpassen, indem Sie zusätzliche Befehlszeileneigenschaften angeben.  

> [!NOTE]  
>  Mit dieser Methode können keine Upgrades von Configuration Manager 2007-Clients durchgeführt werden. Verwenden Sie stattdessen ein automatisches Clientupgrade, bei dem automatisch ein Paket erstellt und bereitgestellt wird, das die aktuelle Clientversion enthält. Weitere Informationen finden Sie unter [Aktualisieren von Clients in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  Weitere Informationen zum Migrieren von einer älteren Version des Configuration Manager-Clients finden Sie unter [Planen einer Strategie für die Clientmigration in System Center Configuration Manager](../../../core/migration/planning-a-client-migration-strategy.md).  

 Gehen Sie wie folgt vor, um ein Configuration Manager-Paket und -Programm für die Bereitstellung auf Configuration Manager-Clientcomputern zum Ausführen eines Upgrades der Clientsoftware zu erstellen.  

#### <a name="to-create-a-package-and-program-for-the-client-software"></a>So erstellen Sie ein Paket und Programm für die Clientsoftware  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Abschnitt **Anwendungsverwaltung**, und klicken Sie dann auf **Pakete**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Paket aus Definition erstellen**.  

4.  Wählen Sie im ** ** Assistenten zum Erstellen eines Pakets aus einer Definition auf der Seite **Paketdefinition**in der Dropdownliste **Herausgeber** die Option **Microsoft** aus. Wählen Sie in der Liste **Paketdefinition** die Option **Aktualisierung des Configuration Manager-Clients** aus, und klicken Sie dann auf **Weiter**.  

5.  Wählen Sie im Assistenten auf der Seite **Quelldateien** die Option **Dateien immer aus einem Quellordner abrufen**aus, und klicken Sie dann auf **Weiter**.  

6.  Wählen Sie auf der Seite **Quellordner** im **Assistent zum Erstellen eines Pakets aus einer Definition** die Option **Netzwerkpfad (UNC-Name)** aus, und geben Sie den Netzwerkpfad zu dem Computer und Ordner ein, der die Configuration Manager-Clientinstallationsdateien enthält.  

    > [!NOTE]  
    >  Für den Computer, auf dem die Configuration Manager-Bereitstellung ausgeführt wird, ist der Zugriff auf den von Ihnen angegebenen Netzwerkordner erforderlich. Ohne diesen Zugriff kann die Installation nicht ausgeführt werden.  

7.  Klicken Sie auf **Weiter** , und schließen Sie den Assistenten ab.  

8.  Wenn Sie die Eigenschaften für die Clientinstallation ändern möchten, können Sie die Befehlszeilenparameter für CCMSetup.exe im Dialogfeld **Eigenschaften von Automatisches Upgrade des Configuration Manager-Agents** auf der Registerkarte **Allgemein** ändern. Die Standardinstallationseigenschaften lauten **/noservice SMSSITECODE=AUTO**.  

9. Verteilen Sie das Paket an alle Verteilungspunkte, auf denen das Clientupgradepaket gehostet werden soll. Anschließend können Sie das Paket den Computersammlungen bereitstellen, die die upzugradenden Configuration Manager-Clients enthalten.  

##  <a name="a-namebkmkclientimagea-how-to-install-configuration-manager-clients-by-using-computer-imaging"></a><a name="BKMK_ClientImage"></a> So installieren Sie Configuration Manager-Clients mithilfe von Computerimages  
 Sie können die Configuration Manager-Clientsoftware auf einem Computer mit dem Masterimage vorinstallieren, der zur Erstellung von Computern in Ihrem Unternehmen verwendet wird. Zum Installieren des Clients auf einem Mastercomputer geben Sie keinen Standortcode für den Client an. Wenn Computer von diesem Masterimage mit Images versehen werden, enthalten diese den Configuration Manager-Client. Nach Abschluss der Installation muss für sie die Standortzuweisung ausgeführt werden.  

> [!IMPORTANT]  
>  Mit Images versehene Computer können nicht als Configuration Manager-Clients verwendet werden, bis die Configuration Manager-Clients einem Configuration Manager-Standort zugewiesen werden.  

 Sie müssen alle auf dem Computer mit dem Masterabbild gespeicherten, computerspezifischen Zertifikate entfernen. Wenn Sie beispielsweise PKI-Zertifikate (Public Key-Infrastruktur) verwenden, müssen Sie vor dem Erstellen des Computers aus dem Abbild die Zertifikate im ** ** privaten Speicher für **Computer** und **Benutzer** entfernen.  

 Wenn Clients Active Directory-Domänendienste nicht zum Suchen eines Verwaltungspunkts abfragen können, verwenden sie den vertrauenswürdigen Stammschlüssel, um vertrauenswürdige Verwaltungspunkte zu finden. Wenn alle mit einem Abbild versehenen Clients in derselben Hierarchie als Mastercomputer bereitgestellt werden, lassen Sie den vertrauenswürdigen Stammschlüssel unverändert. Wenn die Clients in verschiedenen Hierarchien bereitgestellt werden, entfernen Sie den vertrauenswürdigen Stammschlüssel, und stellen Sie den neuen vertrauenswürdigen Stammschlüssel auf diesen Clients im Voraus bereit. Weitere Informationen finden Sie unter  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

#### <a name="to-prepare-the-client-computer-for-imaging"></a>So bereiten Sie den Clientcomputer auf die Abbilderstellung vor  

1.  Installieren Sie die Configuration Manager-Clientsoftware manuell auf dem Computer mit dem Masterimage. Weitere Informationen finden Sie unter [Manuelles Installieren von Configuration Manager-Clients](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Geben Sie keinen Configuration Manager-Standortcode für den Client in den Befehlszeileneigenschaften der Datei „CCMSetup.exe“ an.  

2.  Geben Sie über eine Eingabeaufforderung **net stop ccmexec** ein, um sicherzustellen, dass der Dienst **SMS-Agent-Host** (Ccmexec.exe) auf dem Computer mit dem Masterabbild nicht ausgeführt wird.  

3.  Entfernen Sie alle im lokalen Computerspeicher auf dem Computer mit dem Masterabbild gespeicherten Zertifikate.  

4.  Wenn die Clients in anderen Configuration Manager-Hierarchien als der Computer mit dem Masterimage installiert werden, entfernen Sie den vertrauenswürdigen Stammschlüssel vom Computer mit dem Masterimage.  

5.  Erfassen Sie das Abbild des Mastercomputers mit Ihrer Imaging-Software.  

6.  Stellen Sie das Abbild auf den Zielcomputern bereit.  

##  <a name="a-namebkmkclientworkgroupa-how-to-install-configuration-manager-clients-on-workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> Installieren von Configuration Manager-Clients auf Arbeitsgruppencomputern  
 Configuration Manager unterstützt die Clientinstallation auf Computern in Arbeitsgruppen. Installieren Sie den Client mithilfe der in [Manuelles Installieren von Configuration Manager-Clients](#BKMK_Manual)angegebenen Methode auf Arbeitsgruppencomputern.  

 Zum Installieren des Configuration Manager-Clients auf Arbeitsgruppencomputern müssen die folgenden Voraussetzungen erfüllt sein:  

-   Der Client muss manuell auf jedem Arbeitsgruppencomputer installiert werden. Während der Installation muss der angemeldete Benutzer auf dem Arbeitsgruppencomputer über lokale Administratorrechte verfügen.  

-   Das Netzwerkzugriffskonto muss für den Standort konfiguriert sein, um auf Ressourcen in der Configuration Manager-Standortserverdomäne zugreifen zu können. Sie geben dieses Konto als Eigenschaft der Softwareverteilungskomponente an. Weitere Informationen finden Sie unter [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 Die Unterstützung von Arbeitsgruppencomputern ist durch eine Reihe von Faktoren begrenzt:  

-   Arbeitsgruppenclients können in den Active Directory-Domänendiensten nicht nach Verwaltungspunkten suchen und müssen stattdessen DNS, WINS oder einen anderen Verwaltungspunkt verwenden.  

-   Globales Roaming wird nicht unterstützt, da Clients in den Active Directory-Domänendiensten nicht nach Standortinformationen suchen können.  

-   Über die Active Directory-Ermittlungsmethoden können keine Computer in Arbeitsgruppen ermittelt werden.  

-   Sie können keine Software für Benutzer von Arbeitsgruppencomputern bereitstellen.  

-   Sie können die Clientpushinstallationsmethode nicht zum Installieren des Clients auf Arbeitsgruppencomputern verwenden.  

-   Arbeitsgruppenclients können Kerberos für die Authentifizierung nicht verwenden, sodass möglicherweise eine manuelle Genehmigung erforderlich ist.  

-   Ein Arbeitsgruppenclient kann nicht als Verteilungspunkt konfiguriert werden. Configuration Manager erfordert, dass Verteilungspunktcomputer Mitglied einer Domäne sind.  

#### <a name="to-install-the-client-on-workgroup-computers"></a>So installieren Sie den Client auf Arbeitsgruppencomputern  

1.  Achten Sie darauf, dass die Computer, auf denen der Client installiert werden soll, den oben genannten Anforderungen entsprechen.  

2.  Befolgen Sie die Anweisungen im Abschnitt [Manuelles Installieren von Configuration Manager-Clients](#BKMK_Manual).  

     Beispiel 1: **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com**  

    > [!NOTE]  
    >  In diesem Beispiel wird der Client für die Intranetclientverwaltung installiert. Außerdem werden der Standortcode und das DNS-Suffix zum Suchen eines Verwaltungspunkts angegeben.  

     Beispiel 2: **CCMSetup.exe FSP=fspserver.contoso.com**  

    > [!NOTE]  
    >  In diesem Beispiel muss sich der Client an einem in einer Begrenzungsgruppe konfigurierten Netzwerkort befinden, damit die automatische Standortzuweisung erfolgreich ausgeführt werden kann. Der Befehl umfasst einen Fallbackstatuspunkt auf dem Server FSPSERVER, um die Clientbereitstellung nachverfolgen und Clientkommunikationsprobleme identifizieren zu können.  

##  <a name="a-namebkmkclientinterneta-how-to-install-configuration-manager-clients-for-internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> So installieren Sie Configuration Manager-Clients für die internetbasierte Clientverwaltung  
 Wenn der Configuration Manager-Standort die internetbasierte Clientverwaltung für Clients unterstützt, die sich manchmal im Intranet und manchmal im Internet befinden, stehen Ihnen beim Installieren von Clients im Intranet zwei Optionen zur Verfügung:  

-   Sie können die Client.msi-Eigenschaft „CCMHOSTNAME=*&lt;Internet-FQDN des internetbasierten Verwaltungspunkts\>*“ einschließen, wenn Sie den Client beispielsweise mithilfe der manuellen Installation oder der Clientpushinstallation installieren. Beim Verwenden dieser Methode müssen Sie auch den Client direkt dem Standort zuweisen. Die automatische Standortzuweisung können Sie dabei nicht verwenden. Der Abschnitt [Manuelles Installieren von Configuration Manager-Clients](#BKMK_Manual) in diesem Thema bietet ein Beispiel zu dieser Konfigurationsmethode.  

-   Sie können den Client für die Intranetclientverwaltung installieren und dem Client dann einen internetbasierten Clientverwaltungspunkt zuweisen, indem Sie in der Systemsteuerung die Configuration Manager-Clienteigenschaften oder ein Skript verwenden. Beim Verwenden dieser Methode können Sie die automatische Clientzuweisung verwenden. Weitere Informationen finden Sie im Abschnitt [Konfigurieren von Clients für die internetbasierte Clientverwaltung nach der Clientinstallation](#BKMK_ConfigureIBCM_MP) in diesem Thema.  

 Wählen Sie eine der folgenden unterstützten Methoden aus, wenn Sie im Internet befindliche Clients installieren müssen, weil sie nur für Internetverbindungen konfiguriert sind oder weil sie vor ihrer Rückkehr ins Intranet installiert werden müssen:  

-   Stellen Sie einen Mechanismus bereit, mit dem Clients vorübergehend mithilfe eines virtuellen privaten Netzwerks (Virtual Private Network, VPN) eine Verbindung mit dem Intranet herstellen können, und installieren Sie die Clients mithilfe einer beliebigen angemessenen Clientinstallationsmethode.  

-   Verwenden Sie eine von Configuration Manager unabhängige Installationsmethode. Sie können die Clientinstallationsquelldateien z.B. auf Wechselmedien bündeln und diese mit Installationsanleitungen an Benutzer senden. Die Clientinstallationsquelldateien befinden sich im Ordner „*&lt;Installationspfad\>*\Client“ auf dem Configuration Manager Standortserver bzw. den Verwaltungspunkten. Schließen Sie ein Skript zum manuellen Kopieren des Clientordners ein, und installieren Sie den Client aus diesem Ordner mithilfe der jeweiligen CCMSetup-Befehlszeileneigenschaften.  

> [!NOTE]  
>  Configuration Manager unterstützt die direkte Installation eines Clients von einem internetbasierten Verwaltungspunkt oder von einem Internetbasierten Softwareupdatepunkt nicht.  

 Weil die Kommunikation zwischen über das Internet verwalteten Clients und internetbasierten Standortsystemen erforderlich ist, müssen Sie vor der Installation sicherstellen, dass auf diesen Clients auch PKI-Zertifikate installiert sind. Sie müssen diese Zertifikate unabhängig von Configuration Manager installieren. Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

#### <a name="to-install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>So installieren Sie Clients im Internet durch Angabe von CCMSetup-Befehlszeileneigenschaften  

1.  Befolgen Sie die Anweisungen im Abschnitt [Manuelles Installieren von Configuration Manager-Clients](#BKMK_Manual) und beziehen Sie immer Folgendes ein:  

    -   CCMSetup-Befehlszeileneigenschaft **/source:***&lt;lokaler Pfad zum kopierten Clientordner\>*  

    -   CCMSetup-Befehlszeileneigenschaft **/UsePKICert**  

    -   Client.msi-Eigenschaft **CCMHOSTNAME=***&lt;FQDN des internetbasierten Verwaltungspunkts\>*  

    -   Client.msi-Eigenschaft **SMSSIGNCERT=***&lt;lokaler Pfad zum exportierten Standortserver-Signaturzertifikat\>*  

    -   Client.msi-Eigenschaft **SMSSITECODE=***&lt;Standortcode des internetbasierten Verwaltungspunkts\>*  

    > [!NOTE]  
    >  Wenn der Standort über mehrere internetbasierte Verwaltungspunkte verfügt, können Sie einen beliebigen internetbasierten Verwaltungspunkt für die Eigenschaft CCMHOSTNAME angeben. Wenn ein Configuration Manager-Client eine Verbindung mit dem angegebenen internetbasierten Verwaltungspunkt herstellt, wird vom Verwaltungspunkt eine Liste aller auf dem Standort verfügbaren internetbasierten Verwaltungspunkte an den Client gesendet, der dann einen Verwaltungspunkt auswählt. Die Auswahl ist nicht deterministisch.  

2.  Geben Sie die CCMSetup-Befehlszeileneigenschaft **/NoCRLCheck**an, wenn Sie nicht wünschen, dass die Zertifikatsperrliste (Certificate Revocation List, CRL) vom Client überprüft wird.  

3.  Wenn Sie einen internetbasierten Fallbackstatuspunkt verwenden, geben Sie die Client.msi-Eigenschaft **FSP=***&lt;Internet-FQDN des internetbasierten Fallbackstatuspunkts\>* an.  

4.  Wenn Sie den Client für internetbasierte Clientverwaltung installieren, geben Sie die Client.msi-Eigenschaft **CCMALWAYSINF=1**an.  

5.  Überprüfen Sie, ob Sie zusätzliche CCMSetup-Befehlszeileneigenschaften angeben müssen. Beispielsweise kann es erforderlich sein, Kriterien für die Auswahl eines Zertifikats anzugeben, wenn der Client über mehrere gültige PKI-Zertifikate verfügt. Eine Liste der verfügbaren Eigenschaften finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

     Beispiel: **CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1**  

    > [!NOTE]  
    >  In diesem Beispiel werden die Clientquelldateien aus einem Ordner auf Laufwerk D mit Einstellungen zur Verwendung eines Client-PKI-Zertifikats installiert, wobei das Zertifikat mit der längsten Gültigkeitsdauer für die rein internetbasierte Clientverwaltung ausgewählt wird. Außerdem wird der Client zur Verwendung des internetbasierten Verwaltungspunkts SERVER1 und des internetbasierten Fallbackstatuspunkts in der Domäne contoso.com zugewiesen, und der Client wird dem Standort ABC zugewiesen.  

###  <a name="a-namebkmkconfigureibcmmpa-how-to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> So konfigurieren Sie Clients für die internetbasierte Clientverwaltung nach der Clientinstallation  
 Wenden Sie eines der folgenden Verfahren an, um den internetbasierten Verwaltungspunkt nach der Clientinstallation zuzuweisen. Für das erste Verfahren ist eine manuelle Konfiguration erforderlich, sodass dieses Verfahren zum Konfigurieren weniger Clients geeignet ist, während sich das zweite Verfahren besser eignet, wenn Sie viele Clients konfigurieren müssen.  

##### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>So konfigurieren Sie Clients für die internetbasierte Clientverwaltung nach der Clientinstallation durch Zuweisen des internetbasierten Verwaltungspunkts in den Configuration Manager-Eigenschaften  

1.  Doppelklicken Sie in der Systemsteuerung des Clientcomputers auf **Configuration Manager** , um die Eigenschaften anzuzeigen.  

2.  Geben Sie auf der Registerkarte **Internet** im Textfeld „Internet-FQDN“ den vollqualifizierten Domänennamen des internetbasierten Verwaltungspunkts ein.  

    > [!NOTE]  
    >  Die Registerkarte **Internet** ist nur verfügbar, wenn der Client über ein Client-PKI-Zertifikat verfügt.  

3.  Geben Sie die Proxyservereinstellungen ein, wenn der Internetzugriff des Clients über einen Proxyserver erfolgt.  

4.  Klicken Sie auf **OK**.  

##### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>So konfigurieren Sie Clients für die internetbasierte Clientverwaltung nach der Clientinstallation mithilfe eines Skripts  

1.  Öffnen Sie einen Text-Editor, z. B. Notepad.  

2.  Kopieren Sie Folgendes, und fügen Sie es in die Datei ein:  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the Internet-Based Management Point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

3.  Ersetzen Sie *mp.contoso.com* durch den Internet-FQDN des internetbasierten Verwaltungspunkts.  

    > [!NOTE]  
    >  Wenn Sie einen angegebenen internetbasierten Verwaltungspunkt löschen müssen, damit der Client so konfiguriert wird, dass kein internetbasierter Verwaltungspunkt verwendet wird, entfernen Sie den in Anführungszeichen eingeschlossenen Wert, sodass die Zeile wie folgt aussieht: **newInternetBasedManagementPointFQDN = ""**.  

4.  Speichern Sie die Datei mit der Erweiterung „.vbs“.  

5.  Verwenden Sie cscript, um das Skript mit einer der folgenden Methoden auf den Clientcomputern auszuführen:  

    -   Stellen Sie die Datei mithilfe eines Pakets und Programms auf vorhandenen Configuration Manager-Clients bereit.  

    -   Führen Sie die Datei auf vorhandenen Configuration Manager-Clients lokal aus, indem Sie in Windows Explorer auf die Skriptdatei doppelklicken.  

 Möglicherweise müssen Sie den Client neu starten, damit die neue Einstellung in diesem Skript wirksam wird.  

##  <a name="a-namebkmkprovisiona-how-to-provision-client-installation-properties-group-policy-and-software-update-based-client-installation"></a><a name="BKMK_Provision"></a> So stellen Sie Clientinstallationseigenschaften bereit (auf einer Gruppenrichtlinie oder auf einem Softwareupdate basierende Clientinstallation)  
 Mit Windows-Gruppenrichtlinien können Sie Configuration Manager-Clientinstallationseigenschaften für Computer in Ihrem Unternehmen bereitstellen. Diese Eigenschaften sind in der Registrierung des Computers gespeichert und werden beim Installieren der Clientsoftware gelesen. Normalerweise ist diese Prozedur für Configuration Manager nicht erforderlich. Bei manchen Clientinstallationsszenarien ist sie jedoch notwendig, z. B. für die folgenden:  

-   Sie verwenden die Methode zur Clientinstallation über Gruppenrichtlinieneinstellungen oder einen Softwareupdatepunkt und haben das Active Directory-Schema für Configuration Manager nicht erweitert.  

-   Sie möchten Clientinstallationseigenschaften auf bestimmten Computern außer Kraft setzen.  

> [!NOTE]  
>  Wenn Sie Installationseigenschaften mit dem Befehl CCMSetup.exe bereitstellen, werden die auf Computern bereitgestellten Installationseigenschaften nicht verwendet.  

 Eine administrative Vorlage für Gruppenrichtlinien mit dem Namen „ConfigMgrInstallation.adm“ ist auf dem Configuration Manager-Installationsmedium vorhanden und kann zur Bereitstellung von Installationseigenschaften für Clientcomputer verwendet werden. Gehen Sie wie folgt vor, um diese Vorlage zu konfigurieren und Computern in Ihrem Unternehmen zuzuweisen.  

#### <a name="to-configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>So konfigurieren Sie Clientinstallationseigenschaften mithilfe eines Gruppenrichtlinienobjekts und weisen diese zu  

1.  Importieren Sie die administrative Vorlage „ConfigMgrInstallation.adm“ mithilfe eines Editors wie dem Windows-Gruppenrichtlinienobjekt-Editor in ein neues oder vorhandenes Gruppenrichtlinienobjekt.  

    > [!NOTE]  
    >  Diese Datei befindet sich auf dem Configuration Manager-Installationsmedium im Ordner **TOOLS\ConfigMgrADMTemplates**.  

2.  Öffnen Sie die Eigenschaften der importierten Einstellung **Clientbereitstellungseigenschaften konfigurieren**.  

3.  Klicken Sie auf **Aktiviert**.  

4.  Geben Sie in das Feld **CCMSetup** die erforderlichen CCMSetup-Befehlszeileneigenschaften ein. Eine Liste aller CCMSetup-Befehlszeileneigenschaften mit Verwendungsbeispielen finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Weisen Sie den Computern das Gruppenrichtlinienobjekt zu, auf denen Sie die Configuration Manager-Clientinstallationseigenschaften bereitstellen möchten.  

 Informationen zur Windows-Gruppenrichtlinie finden Sie in Ihrer Windows Server-Dokumentation.  



<!--HONumber=Nov16_HO1-->


