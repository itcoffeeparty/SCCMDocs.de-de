---
title: Erstellen von Abfragen | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie in System Center Configuration Manager Abfragen erstellen und importieren. Enthält Beispiele für Abfragen und Tipps."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 89bd798339489071fdb69325c957fefda32621e9


---
# <a name="how-to-create-queries-in-system-center-configuration-manager"></a>Erstellen von Abfragen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Gehen Sie wie in den folgenden Abschnitten in diesem Thema beschrieben vor, um in System Center Configuration Manager Abfragen zu erstellen oder zu importieren.  

-   [How to Create Queries](#BKMK_Create)  

-   [How to Import Queries](#BKMK_Import)  

-   [Example WQL Queries](#BKMK_Example)  

##  <a name="a-namebkmkcreatea-how-to-create-queries"></a><a name="BKMK_Create"></a> Erstellen von Abfragen  
 Mit diesem Verfahren können Sie Abfragen in Configuration Manager erstellen.  

#### <a name="to-create-a-query"></a>So erstellen Sie eine Abfrage  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Klicken Sie im Arbeitsbereich **Überwachung** auf **Abfragen** und dann auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Abfrage erstellen**.  

3.  Geben Sie auf der Registerkarte **Allgemein** im **Abfrageerstellungs-Assistenten**einen eindeutigen Namen und optional einen Kommentar für die Abfrage an.  

4.  Wenn Sie eine bestehende Abfrage als Basis für die neue Abfrage importieren möchten, klicken Sie auf **Abfrageanweisung importieren** , dann im Dialogfeld **Abfrage durchsuchen** auf eine zu importierende Abfrage, dann auf **OK**.  

5.  Wählen Sie den Objekttyp, den die Abfrage zurückgeben soll, aus der Liste **Objekttyp** aus. In der folgenden Tabelle sind einige Beispiele für Objekttypen aufgeführt, nach denen Sie suchen können:  

    |Objekttyp|Beschreibung|  
    |-----------------|-----------------|  
    |**Systemressource**|Ermöglicht die Suche nach typischen Systemattributen wie NetBIOS-Name von Geräten, Clientversion, IP-Adresse des Clients und Active Directory-Domänendienstinformationen.|  
    |**Benutzerressource**|Ermöglicht die Suche nach typischen Benutzerinformationen wie Benutzernamen, Benutzergruppennamen und Sicherheitsgruppennamen.|  
    |**Bereitstellung**|Ermöglicht die Suche nach typischen Bereitstellungsinformationen wie Bereitstellungsnamen, Zeitplan sowie Sammlung, der die Bereitstellung zugewiesen wurde.|  

6.  Klicken Sie auf **Abfrageanweisung bearbeiten**, um das Dialogfeld *&lt;Abfragename\>***Eigenschaften der Abfrageanweisung** zu öffnen.  

7.  Geben Sie auf der Registerkarte **Allgemein** im Dialogfeld *&lt;Abfragename\>* **Eigenschaften der Abfrageanweisung** die Attribute an, die von dieser Abfrage zurückgegeben werden, sowie die Anzeigeart. Klicken Sie auf das Symbol **Neu** , um ein neues Attribut hinzuzufügen. Sie können auch auf **Abfragesprache anzeigen** klicken, um die Abfrage direkt in WMI Query Language (WQL) einzugeben oder zu ändern. Beispiele für WMI-Abfragen finden Sie im Abschnitt [Example WQL queries](#BKMK_Example) in diesem Thema.  

    > [!TIP]  
    >  Die folgende MSDN-Referenzdokumentation enthält Informationen zum Erstellen eigener WQL-Abfragen:  
    >   
    >  -   [WQL (SQL für WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [WHERE-Klausel](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [WQL-Operatoren](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  Geben Sie auf der Registerkarte **Kriterien** im Dialogfeld *&lt;Abfragename\>***Eigenschaften der Abfrageanweisung** Kriterien zum Optimieren der Abfrageergebnisse an. Sie könnten beispielsweise nur Ressourcen mit dem Standortcode **XYZ** in den Abfrageergebnissen zurückgeben lassen. Sie können mehrere Kriterien für eine Abfrage konfigurieren.  

    > [!IMPORTANT]  
    >  Wenn Sie eine Abfrage ohne Kriterien erstellen, gibt diese alle Geräte in der Sammlung **Alle Systeme** aus.  

9. Auf der Registerkarte **Verknüpfungen** im Dialogfeld *&lt;Abfragename\>***Eigenschaften der Abfrageanweisung** können Sie Daten aus zwei verschiedenen Attributen in Ihren Abfrageergebnissen kombinieren. Von Configuration Manager werden zwar automatisch Abfrageverknüpfungen erstellt, wenn verschiedene Attribute für die Abfrageergebnisse ausgewählt werden, doch die Registerkarte **Verknüpfungen** bietet erweiterte Optionen. Die folgende Tabelle enthält die Attributklassen, die von System Center Configuration Manager 2012 unterstützt werden:  

    |Verknüpfungstyp|Beschreibung|  
    |---------------|-----------------|  
    |Innerhalb|Zeigt nur übereinstimmende Ergebnisse an und wird immer von automatisch erstellten Verknüpfungen verwendet.|  
    |Links|Zeigt alle Ergebnisse für das Basisattribut und nur die übereinstimmenden Ergebnisse für das Verknüpfungsattribut an.|  
    |Rechts|Zeigt alle Ergebnisse für das Verknüpfungsattribut und lediglich die übereinstimmenden Ergebnisse für das Basisattribut an.|  
    |Vollständig|Zeigt alle Ergebnisse für das Basisattribut und für das Verknüpfungsattribut an.|  

     Weitere Informationen zum Verwenden von Verknüpfungsoperationen finden Sie in der SQL Server-Dokumentation.  

10. Klicken Sie auf **OK**, um das Dialogfeld *&lt;Abfragename\>***Eigenschaften der Abfrageanweisung** zu schließen.  

11. Geben Sie auf der Registerkarte **Allgemein** des **Abfrageerstellungs-Assistenten**an, ob die Ergebnisse der Abfrage auf die Mitglieder einer bestimmten Sammlung begrenzt werden sollen oder ob bei jeder Ausführung der Abfrage nach einer Sammlung gefragt werden soll.  

12. Schließen Sie den Abfrageerstellungs-Assistenten ab. Die neue Abfrage wird im Knoten **Abfragen** des Arbeitsbereichs **Überwachung** angezeigt.  

##  <a name="a-namebkmkimporta-how-to-import-queries"></a><a name="BKMK_Import"></a> Importieren von Abfragen  
 Verwenden Sie dieses Verfahren, um eine Abfrage in Configuration Manager zu importieren. Informationen zum Exportieren von Abfragen finden Sie unter [Verwalten von Abfragen in Configuration Manager](../../../core/servers/manage/manage-queries.md).  

#### <a name="to-import-a-query"></a>So importieren Sie eine Abfrage  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Klicken Sie im Arbeitsbereich **Überwachung** auf **Abfragen** und dann auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Objekte importieren**.  

3.  Klicken Sie auf der Seite **MOF-Dateiname** des **Assistenten zum Importieren von Objekten**auf **Durchsuchen** , um die MOF-Datei (Managed Object Format) mit der zu importierenden Abfrage auszuwählen.  

4.  Überprüfen Sie die Informationen zur Abfrage, die importiert werden soll, und schließen Sie den Assistenten ab. Die neue Abfrage wird im Knoten **Abfragen** des Arbeitsbereichs **Überwachung** angezeigt.  

##  <a name="a-namebkmkexamplea-example-wql-queries"></a><a name="BKMK_Example"></a> Example WQL queries  
 Dieser Abschnitt enthält Beispiele für WMI-Abfragen, die Sie in Ihrer Hierarchie verwenden oder für andere Zwecke ändern können. Um diese Abfragen zu verwenden, klicken Sie im Dialogfeld **Eigenschaften der Abfrageanweisung** auf **Abfragesprache anzeigen** , und fügen Sie die Abfrage dann per Kopieren und Einfügen in das Feld **Abfrageanweisung** ein.  

> [!TIP]  
>  Verwenden Sie das Platzhalterzeichen **%** , um eine beliebige Zeichenfolge anzugeben. **%Visio%** gibt beispielsweise „Microsoft Office Visio 2010“ zurück.  

### <a name="computers-that-run-windows-7"></a>Computer, auf denen Windows 7 ausgeführt wird  
 Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen und die Betriebssystemversion aller Computer mit Windows 7 zurückgegeben.  

> [!TIP]  
>  Um Computer zurückzugeben, auf denen Windows Server 2008 R2 ausgeführt wird, ändern Sie **%Workstation 6.1%** in **%Server 6.1%**.  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Computer, auf denen ein bestimmtes Softwarepaket installiert ist  
 Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen und den Softwarepaketnamen aller Computer zurückzugeben, auf denen ein bestimmtes Softwarepaket installiert ist. In diesem Beispiel werden alle Computer angezeigt, auf denen eine Version von Microsoft Visio installiert ist. Ersetzen Sie **%Visio%** durch das Softwarepaket, nach dem Sie mit der Abfrage suchen.  

> [!TIP]  
>  Diese Abfrage sucht anhand der Namen, die in der Liste der Programme in der Windows-Systemsteuerung angezeigt werden, nach dem Softwarepaket.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "%Visio%"  
```  

### <a name="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit-ou"></a>Computer in einer bestimmten Active Directory-Domänendienste-Organisationseinheit (OU)  
 Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen und den Namen der Organisationseinheit aller Computer in einer bestimmten Organisationseinheit zurückzugeben. Ersetzen Sie den Text **OU Name** durch den Namen der Organisationseinheit, nach der Sie mit der Abfrage suchen.  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Computer mit einem bestimmten NetBIOS-Namen  
 Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen aller Computer zurückzugeben, die mit einer bestimmten Zeichenfolge beginnen. In diesem Beispiel gibt die Abfrage alle Computer mit einem NetBIOS-Namen zurück, der mit **ABC**beginnt.  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="a-namebkmkdevicetypea-devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> Geräte eines bestimmten Typs  
 Gerätetypen werden in der Configuration Manager-Datenbank unter der Ressourcenklasse **sms_r_system** und dem Attributnamen **AgentEdition** gespeichert. Verwenden Sie die folgende Abfrage, um nur die Geräte abzurufen, die mit der angegebenen Agent-Edition des Gerätetyps übereinstimmen:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

 Verwenden Sie einen der folgenden Werte für *&lt;Geräte-ID\>*:  

|Gerätetyp|Wert von „AgentEdition“|  
|-----------------|---------------------------|  
|Windows-Desktop oder -Laptop|0|  
|Windows-ARM-basiertes Gerät (mit Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Macintosh-Computer|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|iOS|8|  
|iPad|9|  
|iPod Touch|10|  
|Android|11|  
|Intel-System auf einem Chip|12|  
|UNIX- und Linux-Server|13|  

 Wenn die Abfrage z. B. nur Macintosh-Computer zurückgeben soll, verwenden Sie die folgende Abfrage:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="see-also"></a>Siehe auch  
 [Vorgänge und Wartungstasks für Abfragen in System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)



<!--HONumber=Dec16_HO3-->


