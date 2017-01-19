---
title: Konfigurieren der Sicherheit in System Center Configuration Manager | Microsoft-Dokumentation
description: "Konfigurieren von sicherheitsbezogenen Vorgängen für System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: c486c196335174290a925ca59fe42b806d50889d


---
# <a name="configure-security-in-system-center-configuration-manager"></a>Konfigurieren der Sicherheit in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Anhand der Informationen in diesem Thema können Sie die folgenden sicherheitsbezogenen Optionen für System Center Configuration Manager konfigurieren:  

-   [Configure Settings for Client PKI Certificates](#BKMK_ConfigureClientPKI)  

-   [Konfigurieren von Signierung und Verschlüsselung](#BKMK_ConfigureSigningEncryption)  

-   [Configure Role-Based Administration](#BKMK_ConfigureRBA)  

-   [Manage Accounts that are Used by Configuration Manager](#BKMK_ManageAccounts)  

##  <a name="a-namebkmkconfigureclientpkia-configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a> Konfigurieren von Einstellungen für Client-PKI-Zertifikate  
Wenn Sie Public Key-Infrastrukturzertifikate (PKI) für Clientverbindungen mit Standortsystemen verwenden möchten, von denen Internet Information Services (IIS) verwendet werden, konfigurieren Sie die Einstellungen für diese Zertifikate mithilfe des folgenden Verfahrens.  

#### <a name="to-configure-client-pki-certificate-settings"></a>So konfigurieren Sie Einstellungen von Client-PKI-Zertifikaten  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Bereich **Verwaltung** den Knoten **Standortkonfiguration**, klicken Sie auf **Standorte**und dann auf den zu konfigurierenden primären Standort.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Kommunikation mit Clientcomputern** .  

    Diese Registerkarte ist nur an einem primären Standort verfügbar. Wenn die Registerkarte **Kommunikation mit Clientcomputern** nicht angezeigt wird, sollten Sie sicherstellen, dass Sie nicht mit einem Standort der zentralen Verwaltung oder einem sekundären Standort verbunden sind.  

4.  Klicken Sie auf **Nur HTTPS** , wenn Sie möchten, dass von Clients, die dem Standort zugewiesen sind, immer ein Client-PKI-Zertifikat verwendet wird, wenn eine Verbindung mit Standortsystemen mit IIS hergestellt wird. Klicken Sie alternativ auf **HTTPS oder HTTP** , wenn Sie die Verwendung eines Client-PKI-Zertifikats nicht erzwingen möchten.  

5.  Wenn Sie die Option **HTTPS oder HTTP**ausgewählt haben und für HTTP-Verbindungen ein Client-PKI-Zertifikat verwenden möchten, klicken Sie auf **PKI-Clientzertifikat (Clientauthentifizierungsfunktion) verwenden, sofern dieses verfügbar ist** . Zur Authentifizierung bei Standortsystemen wird vom Client dieses Zertifikat anstatt eines selbstsignierten Zertifikats verwendet. Wenn Sie **Nur HTTPS**auswählen, wird diese Option automatisch ausgewählt.  

    Wenn erkannt wird, dass Clients sich im Internet befinden oder für internetbasierte Clientverwaltung konfiguriert sind, wird immer ein Client-PKI-Zertifikat verwendet.  

6.  Klicken Sie auf **Ändern** , um die Clientauswahlmethode Ihrer Wahl zu konfigurieren, wenn auf einem Client mehrere gültige PKI-Zertifikate verfügbar sind. Klicken Sie dann auf **OK**.  

    Weitere Informationen zur Clientauswahlmethode finden Sie unter [Planning for PKI client certificate selection (Planen der PKI-Clientzertifikatauswahl)](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

7.  Legen Sie mithilfe des Kontrollkästchens fest, ob die Überprüfung der Zertifikatsperrlisten von Clients ausgeführt werden soll.  

    Weitere Informationen zur Überprüfung der Zertifikatsperrlisten durch Clients finden Sie unter [Planning for PKI certificate revocation (Planen der PKI-Zertifikatsperrung)](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

8.  Wenn Sie Zertifikate vertrauenswürdiger Zertifizierungsstellen (CA) für Clients angeben müssen, klicken Sie auf **Festlegen**, importieren die Dateien der Stamm-Zertifizierungsstellenzertifikate und klicken dann auf **OK**.  

    Weitere Informationen zu dieser Einstellung finden Sie unter [Planning for the PKI Trusted Root certificates and the Certificate Issuers List (Planen von vertrauenswürdigen PKI-Stammzertifikaten, und der Liste der Zertifikataussteller)](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRootCAs).  

9. Klicken Sie auf **OK** , um das Eigenschaftendialogfeld für den Standort zu schließen.  

Wiederholen Sie diesen Vorgang für alle primären Standorte in der Hierarchie.  

##  <a name="a-namebkmkconfiguresigningencryptiona-configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a> Konfigurieren von Signierung und Verschlüsselung  
Konfigurieren Sie für Standortsysteme die sichersten Einstellungen für Signierung und Verschlüsselung, die von allen Clients des Standorts unterstützt werden können. Diese Einstellungen sind vor allem dann wichtig, wenn Sie Kommunikation zwischen Clients und Standortsystemen mithilfe selbstsignierter Zertifikate und über HTTP zulassen.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>So konfigurieren Sie die Signierung und Verschlüsselung für einen Standort  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Bereich **Verwaltung** den Knoten **Standortkonfiguration**, klicken Sie auf **Standorte**und dann auf den zu konfigurierenden primären Standort.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Signierung und Verschlüsselung** .  

    Diese Registerkarte ist nur an einem primären Standort verfügbar. Wenn die Registerkarte **Signierung und Verschlüsselung** nicht angezeigt wird, sollten Sie sicherstellen, dass Sie nicht mit einem Standort der zentralen Verwaltung oder einem sekundären Standort verbunden sind.  

4.  Konfigurieren Sie die gewünschten Optionen für die Signierung und Verschlüsselung, und klicken Sie dann auf **OK**.  

    > [!WARNING]  
    >  Wählen Sie die Option **SHA-256 erforderlich** nur dann aus, wenn Sie überprüft haben, ob dieser Hashalgorithmus von allen Clients, die dem Standort zugewiesen werden könnten, unterstützt wird bzw. ob ein gültiges PKI-Zertifikat zur Authentifizierung für die Clients verfügbar ist. Möglicherweise müssen Sie Updates oder Hotfixes auf Clients installieren, damit SHA-256 unterstützt wird. Beispielsweise muss auf Computern mit Windows Server 2003 SP2 das im [KB-Artikel 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666)genannte Hotfix installiert werden.  
    >   
    >  Wenn Sie diese Option auswählen, wenn SHA-256 von Clients nicht unterstützt wird und selbstsignierte Zertifikate verwendet werden, werden die Zertifikate von Configuration Manager zurückgewiesen. In diesem Szenario wird von der Komponente SMS_MP_CONTROL_MANAGER eine Meldung mit der ID 5443 protokolliert.  

5.  Klicken Sie auf **OK** , um das Dialogfeld **Eigenschaften** für den Standort zu schließen.  

Wiederholen Sie diesen Vorgang für alle primären Standorte in der Hierarchie.  

##  <a name="a-namebkmkconfigurerbaa-configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a> Konfigurieren der rollenbasierten Verwaltung  
Bei der rollenbasierten Verwaltung werden Sicherheitsrollen, Sicherheitsbereiche und zugewiesene Sammlungen kombiniert, um den Verwaltungsbereich für jeden Administrator zu definieren. Zu einem Verwaltungsbereich gehören die Objekte, die ein Administrator in der Configuration Manager-Konsole anzeigen kann, und die Tasks im Zusammenhang mit diesen Objekten, die der Administrator ausführen darf. Die Konfigurationen der rollenbasierten Verwaltung werden auf jeden Standort in einer Hierarchie angewendet.  

Die folgenden Links führen zu den relevanten Abschnitten des Themas [Configure role-based administration for System Center Configuration Manager (Konfigurieren der rollenbasierten Verwaltung für System Center Configuration Manager)](../../../core/servers/deploy/configure/configure-role-based-administration.md):  

-   [Create custom security roles (Erstellen benutzerdefinierter Sicherheitsrollen)](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)  

-   [Konfigurieren von Sicherheitsrollen](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole)  

-   [Konfigurieren von Sicherheitsbereichen für ein Objekt](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope)  

-   [Konfigurieren von Sammlungen zum Verwalten der Sicherheit](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl)  

-   [Erstellen eines neuen Administrators](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_Create_AdminUser)  

-   [Modify the administrative scope of an administrative user (Ändern des Verwaltungsbereichs eines Administrators)](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)  

> [!IMPORTANT]  
>  Von Ihrem eigenen Verwaltungsbereich wird definiert, welche Objekte und Einstellungen Sie zuweisen können, wenn Sie die rollenbasierte Verwaltung für einen anderen Administrator konfigurieren. Informationen zum Planen für rollenbasierte Verwaltung finden Sie unter [Fundamentals of role-based administration for System Center Configuration Manager (Grundlagen der rollenbasierten Verwaltung für System Center Configuration Manager)](../../../core/understand/fundamentals-of-role-based-administration.md).  

##  <a name="a-namebkmkmanageaccountsa-manage-accounts-that-are-used-by-configuration-manager"></a><a name="BKMK_ManageAccounts"></a> Verwalten von Konten, die von Configuration Manager verwendet werden  
In Configuration Manager werden Windows-Konten für zahlreiche verschiedene Tasks und Verwendungen unterstützt.  

Gehen Sie wie folgt vor, um anzuzeigen, welche Konten für verschiedene Tasks konfiguriert sind, und um die Kennwörter zu verwalten, die in Configuration Manager für die einzelnen Konten verwendet werden.  

#### <a name="to-manage-accounts-that-are-used-by-configuration-manager"></a>So verwalten Sie Konten, die von Configuration Manager verwendet werden  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Sicherheit**, und klicken Sie dann auf **Konten**, um die Konten anzuzeigen, die für Configuration Manager konfiguriert sind.  

3.  Wenn Sie das Kennwort für ein Konto ändern möchten, das für Configuration Manager konfiguriert ist, wählen Sie das Konto aus.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie auf **Festlegen**, um das Dialogfeld **Windows-Benutzerkonto** zu öffnen, und geben Sie das neue Kennwort ein, das in Configuration Manager für das Konto verwendet werden soll.  

    > [!NOTE]  
    >  Das angegebene Kennwort muss mit dem Kennwort übereinstimmen, das in Active Directory-Benutzer und -Computer für das Konto angegeben wurde.  

6.  Klicken Sie auf **OK** , um das Verfahren abzuschließen.  



<!--HONumber=Dec16_HO3-->


