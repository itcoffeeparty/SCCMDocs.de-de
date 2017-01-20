---
title: Erweitern der Hardwareinventur | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie die Hardwareinventur in System Center Configuration Manager erweitern können."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
caps.latest.revision: 10
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: cf325aec385f570b297f753f37c2c39abe93154f


---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>Erweitern der Hardwareinventur in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager-Hardwareinventur liest Informationen zu Geräten von Windows-PCs mithilfe der Windows-Verwaltungsinstrumentation (WMI). Bei WMI handelt es sich um die Microsoft-Implementierung von WBEM (Web-Based Enterprise Management), einem Industriestandard für den Zugriff auf Verwaltungsinformationen in einer Unternehmensumgebung. In vorherigen Versionen von Configuration Manager waren Sie in der Lage, die Hardwareinventur durch Ändern der Datei "sms_def.mof" auf dem Standortserver zu erweitern. In dieser Datei war eine Liste der WMI-Klassen enthalten, die von der Configuration Manager-Hardwareinventur gelesen werden konnte. Durch das Bearbeiten dieser Datei war es Ihnen möglich, vorhandene Klassen zu aktivieren und zu deaktivieren sowie neue Klassen in der Inventur zu erstellen.  

 Die Datei „Configuration.mof“ wird zur Definition der Datenklassen verwendet, die von der Hardwareinventur auf dem Client inventarisiert werden. Sie wurde seit Configuration Manager 2012 nicht geändert. Datenklassen können erstellt werden, um vorhandene oder benutzerdefinierte WMI-Repositorydatenklassen oder -Registrierungsschlüssel auf Clientsystemen zu inventarisieren.  

 Die Datei "Configuration.MOF" wird auch definiert und registriert die WMI-Anbietern, die Geräteinformationen während der Hardwareinventur zugreifen. Durch das Registrieren von Anbietern werden der zu verwendende Anbietertyp sowie die vom Anbieter unterstützten Klassen definiert.  

 Wenn Configuration Manager-Clients Richtlinien fordern, z.B. während deren Standard-Clientrichtlinien-Abrufintervall, wird die Datei „Configuration.MOF“ an den Richtlinientext angefügt. Diese Datei wird dann heruntergeladen und von Clients kompiliert. Beim Hinzufügen, ändern oder Löschen von Datenklassen aus der Datei "Configuration.MOF" Kompilieren Clients automatisch diese Änderungen Datenklassen Lagerbestand bezieht. Zum Inventarisieren neuer oder geänderter Datenklassen auf Configuration Manager-Clients sind keine weiteren Aktionen erforderlich. Diese Datei befindet sich auf primären Standortservern in **<Configuration Manager-Installationsort\>\Inboxes\clifiles.src\hinv\\**.  

 In Configuration Manager bearbeiten Sie nicht mehr die Datei „sms_def.mof“ wie in Configuration Manager 2007. Stattdessen aktivieren und deaktivieren Sie WMI-Klassen und fügen neue durch die Hardwareinventur zu erfassende Klassen mithilfe von Clienteinstellungen hinzu. Configuration Manager stellt die folgenden Methoden zum Erweitern der Hardwareinventur zur Verfügung.  

> [!NOTE]  
>  Wenn Sie die Datei „Configuration.mof“ zum Hinzufügen benutzerdefinierter Inventarklassen manuell geändert haben, werden diese Änderungen beim Aktualisieren auf die Version 1602 überschrieben. Wenn Sie benutzerdefinierte Klassen nach der Aktualisierung weiterhin verwenden möchten, müssen Sie sie nach dem Aktualisieren auf 1602 dem Abschnitt „Added extensions“ (Hinzugefügte Erweiterungen) der Datei „Configuration.mof“ hinzufügen.  
> Sie dürfen jedoch nichts bearbeiten, was oberhalb dieses Abschnitts liegt, da diese Abschnitte für die Änderungen durch Configuration Manager reserviert sind. Eine Sicherung Ihrer benutzerdefinierten Datei „Configuration.mof“ finden Sie unter:  
> **<Configuration Manager-Installationsverzeichnis\>\data\hinvarchive\\**.  

|Methode|Weitere Informationen|  
|------------|----------------------|  
|Aktivieren oder Deaktivieren von vorhandenen Inventurklassen|Sie können die Standardinventurklassen, die von Configuration Manager verwendet werden, aktivieren oder deaktivieren, oder Sie können benutzerdefinierte Clienteinstellungen erstellen, mit denen Sie verschiedene Hardwareinventurklassen aus bestimmten Clientsammlungen sammeln können. Weitere Informationen finden Sie im Verfahren [So aktivieren oder deaktivieren Sie vorhandene Inventurklassen](#BKMK_Enable) in diesem Thema.|  
|Hinzufügen einer neuen Inventurklasse|Sie können eine neue inventurklasse aus dem WMI-Namespace, der ein anderes Gerät hinzufügen. Weitere Informationen finden Sie im Verfahren [So fügen Sie eine neue Inventurklasse hinzu](#BKMK_Add) in diesem Thema.|  
|Importieren und Exportieren von Hardwareinventurklassen|Sie können MOF-Dateien (Managed Object Format) importieren und exportieren, die Inventurklassen aus der Configuration Manager-Konsole enthalten. Weitere Informationen finden Sie in den Verfahren [So importieren Sie Hardwareinventurklassen](#BKMK_Import) und [So exportieren Sie Hardwareinventurklassen](#BKMK_Export) dieses Themas.|  
|Erstellen von NOIDMIF-Dateien|Verwenden Sie NOIDMIF-Dateien zum Sammeln von Informationen zu Clientgeräten, die nicht von Configuration Manager inventarisiert werden können. Möglicherweise möchten z. B. Gerät Asset Informationen sammeln, die nur als Etikett auf dem Gerät vorhanden ist. NOIDMIF-Inventur wird automatisch das Clientgerät, dem er entnommen wurde zugeordnet. Weitere Informationen finden Sie unter [So erstellen Sie NOIDMIF-Dateien](#BKMK_NOIDMIF) in diesem Thema.|  
|IDMIF-Dateien erstellen|Verwenden Sie IDMIF-Dateien zum Sammeln von Informationen zu Beständen in Ihrer Organisation, die keinem Configuration Manager-Client zugeordnet sind, z.B. Projektoren, Fotokopierer und Netzwerkdrucker. Weitere Informationen finden Sie unter [So erstellen Sie IDMIF-Dateien](#BKMK_IDMIF) in diesem Thema.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Verfahren zum Erweitern der Hardwareinventur  
 Verwenden Sie die folgenden Verfahren zum Erweitern der Hardwareinventur, wie in der Tabelle oben beschrieben.  

 Diese Vorgehensweisen können Sie die Standard-Clienteinstellungen für die Hardwareinventur konfigurieren, und sie gelten für alle Clients in Ihrer Hierarchie. Wenn diese Einstellungen nur auf manche Clients angewendet werden sollen, erstellen Sie eine benutzerdefinierte Clientgeräteeinstellung, und weisen Sie diese einer Sammlung mit den Geräten zu, die Sie inventarisieren möchten. Weitere Informationen zum Erstellen benutzerdefinierter Clienteinstellungen finden Sie unter [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="a-namebkmkenablea-to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> So aktivieren oder deaktivieren Sie vorhandene Inventurklassen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Clienteinstellungen**.  

3.  Klicken Sie auf **Clientstandardeinstellungen**.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie im Dialogfeld **Clientstandardeinstellungen** auf **Hardwareinventur**.  

6.  Klicken Sie in der Liste **Geräteeinstellungen** auf **Klassen festlegen**.  

7.  Wählen Sie im Dialogfeld **Hardwareinventurklassen** die Klassen oder Klasseneigenschaften aus, die von der Hardwareinventur gesammelt werden sollen, oder heben Sie deren Markierung auf. Sie können Klassen erweitern, damit einzelne Eigenschaften in der betreffenden Klasse aktiviert oder deaktiviert werden können. Verwenden Sie für die Suche nach einzelnen Klassen das Feld **Inventurklassen suchen** .  

    > [!IMPORTANT]  
    >  Wenn Sie neue Klassen zur Configuration Manager-Hardwareinventur hinzufügen, vergrößert sich die Inventurdatei, die gesammelt und an den Standortserver gesendet wird. Dies kann sich negativ auf die Leistung des Netzwerks und des Configuration Manager-Standorts auswirken. Aktivieren Sie nur die Inventurklassen, die Sie sammeln möchten.  

8.  Klicken Sie auf **OK** , um die Änderungen zu speichern und das Dialogfeld **Hardwareinventurklassen** zu schließen.  

###  <a name="a-namebkmkadda-to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a> So fügen Sie eine neue Inventurklasse hinzu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

    > [!IMPORTANT]  
    >  Sie können inventurklassen nur auf dem Server auf oberster Ebene in der Hierarchie und durch Ändern der Standardeinstellungen für den Client hinzufügen. Diese Option ist nicht verfügbar, wenn Sie benutzerdefinierte Geräteeinstellungen erstellen.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Clienteinstellungen**.  

3.  Klicken Sie auf **Clientstandardeinstellungen**.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie im Dialogfeld **Clientstandardeinstellungen** auf **Hardwareinventur**.  

6.  Klicken Sie in der Liste **Geräteeinstellungen** auf **Klassen festlegen**.  

7.  Klicken Sie im Dialogfeld **Hardwareinventurklassen** auf **Hinzufügen**.  

8.  Klicken Sie im Dialogfeld **Hardwareinventurklasse hinzufügen** auf **Verbinden**.  

9. Geben Sie im Dialogfeld **WMI-Verbindung herstellen** den Namen des Computers, von dem die WMI-Klassen abgerufen werden, sowie den WMI-Namespace ein, der zum Abrufen der Klassen verwendet werden soll. Klicken Sie auf **Rekursiv**, wenn Sie alle Klassen unterhalb des angegebenen WMI-Namespaces abrufen möchten. Wenn es sich bei dem Computer, zu dem Sie eine Verbindung herstellen, nicht um einen lokalen Computer handelt, geben Sie Anmeldeinformationen für ein Konto an, das über die Berechtigung verfügt, auf WMI auf dem Remotecomputer zuzugreifen.  

10. Klicken Sie auf **Verbinden**.  

11. Wählen Sie im Dialogfeld **Hardwareinventurklasse hinzufügen** in der Liste **Inventurklassen** die WMI-Klassen aus, die Sie der Configuration Manager-Hardwareinventur hinzufügen möchten.  

12. Wenn Sie Informationen zur ausgewählten WMI-Klasse bearbeiten möchten, klicken Sie auf **Bearbeiten**, und geben Sie im Dialogfeld **Klassenkennzeichner** die folgenden Informationen an:  

    -   **Anzeigename** – Legen Sie einen Anzeigenamen für die Klasse fest, der im Ressourcen-Explorer angezeigt wird.  

    -   **Eigenschaften** – Legen Sie die Einheiten fest, in denen jede Eigenschaft der WMI-Klasse angezeigt wird.  

     Sie können Eigenschaften auch als Schlüsseleigenschaft angeben, mit der jede Instanz der Klasse eindeutig bestimmt werden kann. Wenn kein Schlüssel für die Klasse definiert ist, und mehrere Instanzen der Klasse vom Client gemeldet werden, wird nur die aktuelle Instanz, die gefunden wird, in der Datenbank gespeichert.  

     Klicken Sie nach Abschluss der Konfiguration der Eigenschaften auf **OK** , um das Dialogfeld **Klassenkennzeichner** zu schließen.  

13. Klicken Sie auf "OK", um das Dialogfeld **Hardwareinventurklasse hinzufügen** zu schließen.  

14. Klicken Sie auf **OK** , um das Dialogfeld **Hardwareinventurklassen** zu schließen.  

15. Klicken Sie auf **OK** , um das Dialogfeld **Clientstandardeinstellungen** zu schließen.  

###  <a name="a-namebkmkimporta-to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> So importieren Sie Hardwareinventurklassen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Clienteinstellungen**.  

3.  Klicken Sie auf **Clientstandardeinstellungen**.  

    > [!IMPORTANT]  
    >  Sie können Inventurklassen nur importieren, wenn Sie die Clientstandardeinstellungen ändern. Sie können jedoch benutzerdefinierte Clienteinstellungen zum Importieren von Informationen, die nicht mit eine Änderung des Schemas, z. B. das Ändern der Eigenschaft aus einer vorhandenen Klasse enthält **True** auf **False**.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie im Dialogfeld **Clientstandardeinstellungen** auf **Hardwareinventur**.  

6.  Klicken Sie in der Liste **Geräteeinstellungen** auf **Klassen festlegen**.  

7.  Klicken Sie im Dialogfeld **Hardwareinventurklassen** auf **Importieren**.  

8.  In der **importieren** wählen Sie im Dialogfeld Managed Object Format (MOF) Datei, die Sie importieren möchten, und klicken Sie dann auf **OK**.  

9. Überprüfen Sie im Dialogfeld **Importzusammenfassung** die Elemente, die importiert werden, und klicken Sie dann auf **Importieren**.  

###  <a name="a-namebkmkexporta-to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> So exportieren Sie Hardwareinventurklassen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Clienteinstellungen**.  

3.  Klicken Sie auf **Clientstandardeinstellungen**.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie im Dialogfeld **Clientstandardeinstellungen** auf **Hardwareinventur**.  

6.  Klicken Sie in der Liste **Geräteeinstellungen** auf **Klassen festlegen**.  

7.  Klicken Sie im Dialogfeld **Hardwareinventurklassen** auf **Exportieren**.  

    > [!NOTE]  
    >  Wenn Sie Klassen exportieren, werden alle aktuell ausgewählten Klassen exportiert.  

8.  Legen Sie im Dialogfeld **Exportieren** die MOF (Managed Object Format)-Datei fest, in die Sie die Klassen exportieren möchten, und klicken Sie dann auf **Speichern**.  

## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Verwenden von MIF (Management Information Format)-Dateien zum Erweitern der Hardwareinventur  
 Verwenden Sie MIF (Management Information Format)-Dateien zum Erweitern von Hardwareinventurinformationen, die Configuration Manager von Clients sammelt. Während der Hardwareinventur werden die in MIF-Dateien gespeicherten Informationen dem Clientinventurbericht hinzugefügt und in der Standortdatenbank gespeichert, wo Sie die Daten auf die gleiche Weise wie Standard-Clientinventurdaten verwenden können. Es gibt zwei Arten von MIF-Dateien, NOIDMIF- und IDMIF.

> [!IMPORTANT]  
>  Vor dem Hinzufügen von Informationen aus MIF-Dateien an die Configuration Manager-Datenbank müssen Sie Klasseninformationen für sie erstellen oder importieren. Weitere Informationen finden Sie in den Abschnitten [So fügen Sie eine neue Inventurklasse hinzu](#BKMK_Add) und [So importieren Sie Hardwareinventurklassen](#BKMK_Import) dieses Themas.  

###  <a name="a-namebkmknoidmifa-to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> So erstellen Sie NOIDMIF-Dateien  
 NOIDMIF-Dateien können verwendet werden, um einer Client-Hardwareinventur Informationen hinzuzufügen, die normalerweise nicht durch Configuration Manager gesammelt werden können und einem bestimmten Client-Gerät zugeordnet sind. Von vielen Unternehmen werden beispielsweise alle Computer in der Organisation mit einer Mediennummer beschriftet, die dann per Hand katalogisiert wird. Wenn Sie eine NOIDMIF-Datei erstellen, können diese Informationen der Configuration Manager-Datenbank hinzugefügt und für Abfragen und Berichte verwendet werden. Weitere Informationen zum Erstellen von NOIDMIF-Dateien finden Sie in der Configuration Manager SDK-Dokumentation.  

> [!IMPORTANT]  
>  Wenn Sie eine NOIDMIF-Datei erstellen, müssen Sie diese in einem ANSI-codierten Format speichern. In UTF-8-codiertem Format gespeicherte NOIDMIF-Dateien können nicht von Configuration Manager gelesen werden.  

 Nachdem Sie eine NOIDMIF-Datei erstellt haben, speichern Sie diese im Ordner *%windir%***\System32\CCM\Inventory\Noidmifs** Ordner auf jedem Client. Während des nächsten geplanten Hardwareinventurzyklus sammelt Configuration Manager Informationen aus NOIDMIF-Dateien in diesem Ordner.  

###  <a name="a-namebkmkidmifa-to-create-idmif-files"></a><a name="BKMK_IDMIF"></a> So erstellen Sie IDMIF-Dateien  
 Mithilfe von IDMIF-Dateien können Sie der Configuration Manager-Datenbank Informationen zu Beständen hinzufügen, die normalerweise nicht von Configuration Manager inventarisiert werden können und keinem bestimmten Clientgerät zugeordnet sind. In den IDMIF-Dateien können Sie z.B. Informationen zu Projektoren, DVD-Playern, Fotokopierern oder anderen Geräten sammeln, auf denen kein Configuration Manager-Client vorhanden ist. Weitere Informationen zum Erstellen von IDMIF-Dateien finden Sie in der Configuration Manager SDK-Dokumentation.  

 Nachdem Sie eine IDMIF-Datei erstellt haben, speichern Sie diese im Ordner *%windir%***\System32\CCM\Inventory\Idmifs** Ordner auf den Clientcomputern. Während des nächsten geplanten Hardwareinventurzyklus wird Configuration Manager Informationen aus dieser Datei sammeln. Sie müssen für die in der Datei enthaltenen Informationen neue Klassen deklarieren, indem Sie sie hinzufügen oder importieren.  

> [!NOTE]
> MIF-Dateien können große Datenmengen enthalten. Das Sammeln dieser Daten kann sich negativ auf die Leistung Ihres Standorts auswirken. Aktivieren Sie die MIF-Sammlung nur im Bedarfsfall, und konfigurieren Sie die Option **Maximale benutzerdefinierte MIF-Dateigröße (KB)** in den Einstellungen der Hardwareinventur. Weitere Informationen finden Sie unter [Einführung in die Hardwareinventur in System Center Configuration Manager](introduction-to-hardware-inventory.md).



<!--HONumber=Dec16_HO3-->


