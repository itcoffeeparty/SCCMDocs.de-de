---
title: "Veröffentlichung und das Active Directory-Schema | Microsoft-Dokumentation"
description: "Das Erweitern des Active Directory-Schemas für System Center Configuration Manager vereinfacht das Bereitstellen und Konfigurieren von Clients."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
caps.latest.revision: 17
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2083a2ca7a199771f26981cdbe04e4e2ef6e8958
ms.openlocfilehash: 3bd18e2de76d886b275c80d0dce3b824f2598008


---
# <a name="prepare-active-directory-for-site-publishing"></a>Vorbereiten von Active Directory für die Veröffentlichung eines Standorts

*Gilt für: System Center Configuration Manager (Current Branch)*

Beim Erweitern des Active Directory-Schemas für System Center Configuration Manager führen Sie neue Strukturen in Active Directory ein, die von Configuration Manager-Standorten zum Veröffentlichen wichtiger Informationen an einem sicheren Speicherort genutzt werden, wo Clients einfach auf sie zugreifen können.  

 Zur Verwaltung lokaler Clients empfehlen wir den Einsatz von Configuration Manager mit einem erweiterten Active Directory-Schema. Ein erweitertes Schema kann die Bereitstellung und Konfiguration von Clients erleichtern und ermöglicht Clients, Ressourcen einfach zu finden, wie z.B. Inhaltsserver und weitere Dienste, die von den verschiedenen Configuration Manager-Standortsystemrollen bereitgestellt werden.  

-   Wenn Sie nicht mit den Vorteilen eines erweiterten Schemas in einer Configuration Manager-Bereitstellung vertraut sind, kann Sie der Artikel [Schemaerweiterungen für System Center Configuration Manager](../../../core/plan-design/network/schema-extensions.md) bei der Entscheidung unterstützen.  

-   Wenn Sie kein erweitertes Schema verwenden, können Sie andere Methoden wie z.B. DNS und WINS konfigurieren, um Dienste und Standortsystemserver zu identifizieren. Diese Methoden der Dienstidentifizierung erfordern zusätzliche Konfigurationen und stellen nicht die bevorzugte Methode für die Dienstidentifizierung durch Clients dar. Weitere Informationen finden Sie unter [Verstehen, wie Clients Standortressourcen und -dienste für System Center Configuration Manager suchen](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   Wenn Ihr Active Directory-Schema für Configuration Manager 2007 oder System Center 2012 Configuration Manager erweitert wurde, müssen Sie keine weiteren Schritte durchführen. Die Active Directory-Schemaerweiterungen sind unverändert und bereits vorhanden.  

Das Erweitern des Schemas für jede Gesamtstruktur ist eine einmalige Aktion. Zum Erweitern und anschließenden Nutzen des erweiterten Active Directory-Schemas führen Sie die folgenden Schritte aus:  

## <a name="step-1-extend-the-schema"></a>Schritt 1: Erweitern des Schemas  
Für das Erweitern des Schemas für Configuration Manager wird Folgendes benötigt:  

-   Sie müssen ein Konto nutzen, das Mitglied der Sicherheitsgruppe „Schema-Admins“ ist.  

-   Sie müssen am Schemamaster-Domänencontroller angemeldet sein.  

-   Führen Sie das Tool **Extadsch.exe** aus, oder verwenden Sie das Befehlszeilenprogramm LDIFDE mit der Datei **ConfigMgr_ad_schema.ldf** . Das Tool und die Datei befinden sich beide auf dem Configuration Manager-Installationsmedium im Ordner **SMSSETUP\BIN\X64**.  

#### <a name="option-a-use-extadschexe"></a>Option A: Verwenden von „Extadsch.exe“  

1.  Führen Sie **extadsch.exe** zum Hinzufügen der neuen Klassen und Attribute zum Active Directory-Schema aus.  

    > [!TIP]  
    >  Führen Sie dieses Tool über die Befehlszeile aus, um während der Ausführung Feedback anzuzeigen.  

2.  Überprüfen Sie in der Datei „extadsch.log“ im Stammverzeichnis des Systemlaufwerks, ob die Schemaerweiterung erfolgreich war.  

#### <a name="option-b-use-the-ldif-file"></a>Option B: Verwenden der LDIF-Datei  

1.  Bearbeiten Sie die Datei **ConfigMgr_ad_schema.ldf** zum Definieren der Active Directory-Stammdomäne, die Sie erweitern möchten:  

    -   Alle Vorkommen des Texts **DC=x** in der Datei müssen durch den vollständigen Namen der zu erweiternden Domäne ersetzt werden.  

    -   Beispiel: Lautet der vollständige Name der zu erweiternden Domäne „widgets.microsoft.com“, ändern Sie in der Datei jedes Vorkommen von „DC=x“ in **DC=widgets, DC=microsoft, DC=com**.  

2.  Importieren Sie den Inhalt der Datei **ConfigMgr_ad_schema.ldf** mithilfe des Befehlszeilenprogramms LDIFDE in Active Directory-Domänendienste:  

    -   Durch die folgende Befehlszeile werden z.B. die Schemaerweiterungen in Active Directory Domain Services importiert, die ausführliche Protokollierung aktiviert und eine Protokolldatei während des Importvorgangs erstellt: **ldifde -i -f ConfigMgr_ad_schema.ldf -v -j &lt;Speicherort der Protokolldatei\>**  

3.  Sie können prüfen, ob die Schemaerweiterung erfolgreich war, indem Sie die Protokolldatei untersuchen, die mithilfe der Befehlszeile aus dem vorherigen Schritt erstellt wurde.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Schritt 2.  Erstellen des System Management-Containers und Gewähren von Standortberechtigungen für den Container  
 Nach dem Erweitern des Schemas müssen Sie in Active Directory Domain Services (AD DS) den Container **Systemverwaltung** erstellen:  

-   Sie erstellen diesen Containers einmal in jeder Domäne, die über einen primären oder sekundären Standort verfügt, der Daten in Active Directory veröffentlicht.  

-   Jedem Container erteilen Sie Berechtigungen für das Computerkonto jedes primären und sekundären Standortservers, der Daten in dieser Domäne veröffentlicht. Jedes Konto benötigt **Vollzugriff** auf den Container, wobei die erweiterte Berechtigung **Anwenden auf** **Dieses und alle untergeordneten Objekte** entsprechen muss.  

#### <a name="to-add-the-container"></a>So fügen Sie den Container hinzu  

1.  Verwenden Sie ein Konto, das im Container **System** in den Active Directory-Domänendiensten über die Berechtigung **Alle untergeordneten Objekte erstellen** verfügt.  

2.  Führen Sie **ADSI Bearbeiten** (adsiedit.msc) aus, und stellen Sie eine Verbindung mit der Domäne des Standortservers her.  

3.  Erstellen des Containers:  

    -   Erweitern Sie **Domäne** &lt;vollständig qualifizierter Domänenname des Computers\>, erweitern Sie &lt;definierter Name\>, klicken Sie mit der rechten Maustaste auf **CN=System**, klicken Sie auf **Neu** und dann auf **Objekt**.  

    -   Wählen Sie im Dialogfeld **Objekt erstellen** die Option **Container**aus, und klicken Sie auf **Weiter**.  

    -   Geben Sie in das Feld **Wert** die Zeichenfolge **System Management**ein, und klicken Sie dann auf **Weiter**.  

4.  Zuweisen von Berechtigungen:  

    > [!NOTE]  
    >  Nach Wunsch können Sie mit anderen Tools wie „Active Directory-Benutzer und -Computer“ (dsa.msc) dem System Management-Container Berechtigungen hinzufügen.  

    -   Klicken Sie mit der rechten Maustaste auf **CN=System Management**, und klicken Sie dann auf **Eigenschaften**.  

    -   Wählen Sie die Registerkarte **Sicherheit** aus, klicken Sie auf **Hinzufügen**, und fügen Sie anschließend das Computerkonto des Standortservers mit der  
        Berechtigung **Vollzugriff** hinzu.  

    -   Klicken Sie auf **Erweitert**, wählen Sie das Computerkonto des Standortservers aus, und klicken Sie dann auf **Bearbeiten**.  

    -   Wählen Sie in der Liste **Übernehmen für** den Eintrag **Dieses und alle untergeordneten Objekte**aus.  

5.  Klicken Sie auf **OK**, um das Dialogfeld zu schließen und die Konfiguration zu speichern.  

## <a name="step-3-configure-sites-to-publish-to-active-directory-domain-services"></a>Schritt 3. Konfigurieren von Standorten zur Veröffentlichung in Active Directory-Domänendienste  
 Nachdem der Container konfiguriert wurde, Berechtigungen gewährt wurden und Sie einen primären Configuration Manager-Standort installiert haben, können Sie diesen Standort für das Veröffentlichen von Daten in Active Directory konfigurieren.  

 Informationen zum Veröffentlichen finden Sie unter [Publish site data for System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md).  



<!--HONumber=Dec16_HO3-->


