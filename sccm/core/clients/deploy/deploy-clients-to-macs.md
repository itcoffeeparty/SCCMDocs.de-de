---
title: Mac-Clients bereitstellen | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie Clients auf Macintosh-Computern in System Center Configuration Manager bereitstellen können."
ms.custom: na
ms.date: 11/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 66071227fd10a43f7cd4e64508494d485392ffcd
ms.openlocfilehash: 6cbddd623767522a0026e0736b1f647fddbecfb6


---
# <a name="how-to-deploy-clients-to-macs-in-system-center-configuration-manager"></a>How to deploy clients to Macs in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema beschreibt, wie der Configuration Manager-Client auf Macintosh-Computern installiert wird.

## <a name="prerequisites-and-preparatory-steps"></a>Voraussetzungen und vorbereitende Schritte

### <a name="mac-prerequisites"></a>Voraussetzungen für Macintosh-Computer

Stellen Sie vor der Installation des Clients sicher, dass die Macintosh-Computer den Voraussetzungen entsprechen, wie in [Supported operating systems for Macs (Unterstützte Betriebssysteme für Macs)](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers) beschrieben.  

### <a name="certificate-requirements"></a>Zertifikatanforderungen
Die Clientinstallation und -verwaltung für Macintosh-Computer erfordert PKI-Zertifikate (Public Key-Infrastruktur). Durch PKI-Zertifikate wird die Kommunikation zwischen den Macintosh-Computern und dem Configuration Manager-Standort mithilfe gegenseitiger Authentifizierung und verschlüsselter Datenübertragungen gesichert. Configuration Manager kann ein Benutzerclientzertifikat mithilfe der Microsoft-Zertifikatdienste mit einer Unternehmenszertifizierungsstelle (CA) sowie den Configuration Manager-Standortsystemrollen für Registrierungsspunkt und Registrierungsproxypunkt anfordern und installieren. Sie können auch unabhängig von Configuration Manager ein Computerzertifikat anfordern und installieren, sofern das Zertifikat die Anforderungen für Configuration Manager erfüllt.   
  
Im Gegensatz zu Configuration Manager-Clients unter Windows wird die Zertifikatsperrüberprüfung auf Configuration Manager-Macintosh-Clients immer durchgeführt. Sie können diese Funktion zur Überprüfung der Zertifikatsperrliste (Certificate Revocation List, CRL) nicht deaktivieren.  
  
Wenn Mac-Clients den Zertifikatsperrstatus für ein Serverzertifikat nicht bestätigen können, weil die Zertifikatsperrliste nicht gefunden werden kann, ist keine erfolgreiche Verbindung mit Configuration Manager-Standortsystemen (beispielsweise mit Verwaltungspunkten und Verteilungspunkten) möglich. Überprüfen Sie den Entwurf der Zertifikatsperrliste insbesondere für Mac-Clients, die sich in einer anderen Gesamtstruktur als die ausstellende Zertifizierungsstelle befinden, um sicherzustellen, dass ein Sperrlisten-Verteilungspunkt für die Verbindung mit Standortsystemservern von den Mac-Clients gefunden und eine Verbindung damit hergestellt werden kann.  

Legen Sie vor dem Installieren des Configuration Manager-Clients auf einem Macintosh-Computer fest, wie das Clientzertifikat installiert werden soll:  

-   Verwenden Sie die Configuration Manager-Registrierung mithilfe des Tools CMEnroll, und führen Sie die im nächsten Abschnitt dieses Themas beschriebenen Schritte aus. Die automatische Zertifikatserneuerung wird bei der Anmeldung nicht unterstützt, sodass Sie Macintosh-Computer vor dem Ablaufdatum des installierten Zertifikats erneut anmelden müssen.  

-   Verwenden Sie eine von Configuration Manager unabhängige Zertifikatanforderungs- und -installationsmethode. Informationen zu dieser Installationsmethode finden Sie im Abschnitt [Use a certificate request and installation method that is independent from Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager) in diesem Thema.  

Weitere Informationen zur Zertifikatanforderung für Macintosh-Clients und zu anderen PKI-Zertifikaten, die zur Unterstützung von Macintosh-Computern erforderlich sind, finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

Macintosh-Clients werden automatisch dem Configuration Manager-Standort zugewiesen, von dem aus sie verwaltet werden. Macintosh-Clients werden als reine Internetclients installiert, selbst wenn die Kommunikation auf das Intranet beschränkt ist. Diese Clientkonfiguration bedeutet, dass die Kommunikation zwischen den Clients und den Standortsystemrollen (Verwaltungspunkte und Verteilungspunkte) am zugewiesenen Standort erfolgt, wenn Sie diese Standortsystemrollen so konfigurieren, dass Clientverbindungen aus dem Internet zulässig sind. Eine Kommunikation mit Standortsystemrollen außerhalb des zugewiesenen Standorts findet auf Macintosh-Computern nicht statt.  

> [!IMPORTANT]  
>  Der Configuration Manager-Macintosh-Client kann nicht zum Herstellen der Verbindung mit einem Verwaltungspunkt verwendet werden, der für die Verwendung eines [Datenbankreplikats](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) konfiguriert ist.  


### <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Bereitstellen eines Webserverzertifikats für Standortsystemserver  
Wenn diese Standortsysteme nicht darüber verfügen, stellen Sie ein Webserverzertifikat den Computern mit diesen Standortsystemrollen bereit:  

-   Verwaltungspunkt  

-   Verteilungspunkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

Im Webserverzertifikat muss der Internet-FQDN, der in den Eigenschaften des Standortsystems angegeben ist, enthalten sein. Auf den Server muss kein Zugriff über das Internet möglich sein, um Mac-Computer zu unterstützen. Wenn Sie keine internetbasierte Clientverwaltung benötigen, können Sie den Wert des Intranet-FQDN für den Internet-FQDN angeben.  

Geben Sie den Wert des Internet-FQDN für das Standortsystem im Webserverzertifikat für den Verwaltungspunkt, den Verteilungspunkt und den Registrierungsproxypunkt an. 

Eine Beispielbereitstellung, bei der dieses Webserverzertifikat erstellt und installiert wird, finden Sie unter [Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

 

### <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Bereitstellen eines Clientauthentifizierungszertifikat für Standortsystemserver  
 Falls in den Standortsystemen nicht vorhanden, müssen Sie auf den entsprechenden Computern, auf denen sich die folgenden Standortsystemrollen befinden, ein Clientauthentifizierungszertifikat bereitstellen:  

-   Verwaltungspunkt  

-   Verteilungspunkt  

 Eine Beispielbereitstellung, bei der das Clientzertifikat für Verwaltungspunkte erstellt und installiert wird, finden Sie unter [Bereitstellen des Clientzertifikats für Windows-Computer](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)  

 Eine Beispielbereitstellung, bei der das Clientzertifikat für Verteilungspunkte erstellt und installiert wird, finden Sie unter [Bereitstellen des Clientzertifikats für Verteilungspunkte](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### <a name="prepare-the-client-certificate-template-for-macs"></a>Vorbereiten der Clientzertifikatvorlage für Mac-Computer  

> [!NOTE]  
>  Sie müssen über ein Active Directory-Benutzerkonto verfügen, um das Configuration Manager-Registrierungstool ausführen zu können.  

 Die Zertifikatvorlage muss über die Berechtigungen **Lesen** und **Anmelden** für das Benutzerkonto verfügen, mit dem das Zertifikat auf dem Macintosh-Computer angemeldet wird.  

 Informationen hierzu finden Sie unter [Bereitstellen des Clientzertifikats für Macintosh-Computer](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  

### <a name="configure-the-management-point-and-distribution-point"></a>Konfigurieren des Verwaltungspunkts und Verteilungspunkts  
 Konfigurieren Sie Verwaltungspunkte für die folgenden Optionen:  

-   HTTPS  

-   Clientverbindungen aus dem Internet zulassen. Dieser Konfigurationswert wird benötigt, um Macintosh-Computer zu verwalten. Dies bedeutet jedoch nicht, dass Zugriff auf Standortsystemserver über das Internet möglich sein muss.  

-   Verwendung dieses Verwaltungspunkts durch mobile Geräte und Macintosh-Computer zulassen  

 Verteilungspunkte sind zum Installieren des Clients nicht erforderlich. Sie müssen jedoch Verteilungspunkte konfigurieren, um Clientverbindungen aus dem Internet zuzulassen, wenn Sie nach der Installation des Clients auf diesen Computern Software bereitstellen möchten.  

 
##### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>So konfigurieren Sie Verwaltungspunkte und Verteilungspunkte für die Unterstützung von Macintosh-Computern  

Bevor Sie das Verfahren anwenden, vergewissern Sie sich, dass der Standortsystemserver, auf dem der Verwaltungspunkt und der Verteilungspunkt ausgeführt werden, mit einem Internet-FQDN konfiguriert ist. Wenn von diesen Servern keine internetbasierte Clientverwaltung unterstützt wird, können Sie den Intranet-FQDN als Wert des Internet-FQDN angeben. 

Die Standortsystemrollen müssen sich an einem primären Standort befinden.  


1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Standortkonfiguration** > **Server und Standortsystemrollen** und anschließend den Server aus, der über die entsprechenden Standortsystemrollen verfügt.  

3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **Verwaltungspunkt**. Klicken Sie auf die **Eigenschaften** der Rolle. Konfigurieren Sie im Dialogfeld **Eigenschaften des Verwaltungspunkts** diese Optionen:  

    1.  Wählen Sie **HTTPS** aus.  

    2.  Wählen Sie **Nur Internetverbindungen zulassen** oder **Intranet- und Internet-Clientverbindungen zulassen** aus. Diese Optionen erfordern einen Internet- oder Intranet-FQDN.  

    3.  Aktivieren Sie **Verwendung dieses Verwaltungspunkts durch mobile Geräte und Macintosh-Computer zulassen**.  

4.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **Verwaltungspunkt**. Klicken Sie auf die **Eigenschaften** der Rolle. Konfigurieren Sie im Dialogfeld **Eigenschaften des Verteilungspunkts** diese Optionen:  

    -   Wählen Sie **HTTPS** aus.  

    -   Wählen Sie **Nur Internetverbindungen zulassen** oder **Intranet- und Internet-Clientverbindungen zulassen** aus. Diese Optionen erfordern einen Internet- oder Intranet-FQDN.  

    -   Klicken Sie auf **Zertifikat importieren**, suchen Sie die exportierte Clientzertifikatdatei für den Verteilungspunkt, und geben Sie das Kennwort an.  

5.  Wiederholen Sie die Schritte 2 bis 4 für alle Verwaltungspunkte und Verteilungspunkte an primären Standorten, die mit Mac-Computern verwendet werden sollen.  

### <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Konfigurieren des Anmeldungsproxypunkts und Anmeldungspunkts  
 Sie müssen diese beiden Standortsystemrollen am gleichen Standort installieren. Eine Installation auf dem gleichen Standortsystemserver oder in der gleichen Active Directory-Gesamtstruktur ist jedoch nicht erforderlich.  

 Weitere Informationen zur Platzierung von und den Überlegungen für Standortsystemrollen finden Sie im Abschnitt [Standardsystemrollen](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) unter [Planen für Standortsystemserver und Standortsystemrollen für System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Mithilfe dieser Verfahren werden die Standortsystemrollen für die Unterstützung von Macintosh-Computern konfiguriert. Wählen Sie abhängig davon, ob Sie zur Unterstützung von Macintosh-Computern einen neuen Standortsystemserver installieren oder einen vorhandenen Standortsystemserver verwenden, eines der folgenden Verfahren aus:  

-   [Neuer Standortsystemserver](#new-site-system-server)  

-   [Bestehender Standortsystemserver](#existing-site-system-server)  

####  <a name="new-site-system-server"></a>neuer Standortsystemserver  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** >  **Standortkonfiguration** > **Server und Standortsystemrollen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Standortsystemserver erstellen** aus.  

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für das Standortsystem an.  Stellen Sie sicher, dass Sie einen Wert für den Internet-FQDN angeben. Wenn über das Internet kein Zugriff auf den Server möglich ist, verwenden Sie den Intranet-FQDN.  

5.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Anmeldungsproxypunkt** und **Anmeldungspunkt** aus.  

6.  Überprüfen Sie auf der Seite **Anmeldungsproxypunkt** die Einstellungen, und nehmen Sie ggf. Änderungen vor.  

7.  Überprüfen Sie auf der Seite **Anmeldungsproxyeinstellungen** die Einstellungen, und nehmen Sie ggf. Änderungen vor. Schließen Sie anschließend den Assistenten ab.  

#### <a name="existing-site-system-server"></a>bestehender Standortsystemserver  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** >  **Standortkonfiguration** > **Server und Standortsystemrollen** und anschließend den Server aus, den Sie zum Unterstützen von Mac-Computern verwenden möchten.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Standortsystemrollen hinzufügen** aus.  

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an, und klicken Sie dann auf **Weiter**. Stellen Sie sicher, dass Sie einen Wert für den Internet-FQDN angeben. Wenn über das Internet kein Zugriff auf den Server möglich ist, verwenden Sie den Intranet-FQDN.   

5.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Anmeldungsproxypunkt** und **Anmeldungspunkt** aus.  

6.  Überprüfen Sie auf der Seite **Anmeldungsproxypunkt** die Einstellungen, und nehmen Sie ggf. Änderungen vor.  

7.  Überprüfen Sie auf der Seite **Anmeldungsproxyeinstellungen** die Einstellungen, und nehmen Sie ggf. Änderungen vor. Schließen Sie anschließend den Assistenten ab.  

### <a name="optional-install-the-reporting-services-point"></a>Optional: Installieren Sie den Reporting Services-Punkt  
 Installieren Sie den Reporting Services-Punkt, wenn Sie Berichte für Macintosh-Computer ausführen möchten.  

 Weitere Informationen zum Installieren und Konfigurieren eines Reporting Services-Punkts finden Sie unter [Konfigurieren der Berichterstellung in System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).  


##  <a name="install-and-configure-the-client-for-macs"></a>Installieren und Konfigurieren des Clients für Macintosh-Computer  


### <a name="configure-client-settings-for-enrollment"></a>Konfigurieren Sie die Clienteinstellungen für die Anmeldung  
 Sie müssen zum Konfigurieren der Anmeldung für Macintosh-Computer die Clientstandardeinstellungen verwenden. Benutzerdefinierte Clienteinstellungen dürfen hierzu nicht verwendet werden.  

 Weitere Informationen zu Clienteinstellungen finden Sie unter [About client settings in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

 Dies ist in Configuration Manager zum Anfordern und Installieren des Zertifikats auf dem Macintosh-Computer erforderlich.  

#### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>So konfigurieren Sie die Clientstandardeinstellungen für Configuration Manager zum Registrieren von Zertifikaten für Macintosh-Computer  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** >  **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie den Abschnitt **Anmeldung** aus, und konfigurieren Sie dann diese Einstellungen:  

    1.  **Benutzern die Registrierung mobiler Geräte und von Macintosh-Computern gestatten: Ja**  

    2.  **Anmeldungsprofil:** Wählen Sie **Profil festlegen**.  

6.  Wählen Sie im Dialogfeld **Anmeldungsprofil für mobile Geräte** **Erstellen**.  

7.  Geben Sie im Dialogfeld **Anmeldungsprofil erstellen** einen Namen für dieses Anmeldungsprofil ein, und konfigurieren Sie dann den **Verwaltungsstandortcode**. Wählen Sie den primären Configuration Manager-Standort aus, der die Verwaltungspunkte enthält, von denen die Macintosh-Computer verwaltet werden sollen.  

    > [!NOTE]  
    >  Wenn ein Auswählen des Standorts nicht möglich ist, achten Sie darauf, dass mindestens ein Verwaltungspunkt am Standort für die Unterstützung mobiler Geräte konfiguriert ist.  

8.  Wählen Sie **Hinzufügen** aus.  

9. Wählen Sie im Dialogfeld **Zertifizierungsstelle für mobile Geräte hinzufügen** den Server der Zertifizierungsstelle aus, von der Zertifikate für Macintosh-Computer ausgestellt werden.  

10. Wählen Sie im Dialogfeld **Anmeldungsprofil erstellen** die Zertifikatvorlage für Macintosh-Computer aus, die Sie in Schritt 3 erstellt haben.  

11. Klicken Sie auf **OK**, um das Dialogfeld **Anmeldungsprofil**, und anschließend das Dialogfeld **Clientstandardeinstellungen** zu schließen.  

    > [!TIP]  
    >  Wenn Sie das Clientrichtlinienintervall ändern möchten, verwenden Sie in der Clienteinstellungsgruppe **Clientrichtlinie** die Clienteinstellung **Clientrichtlinien-Abrufintervall** .  

 Alle Benutzer werden mit diesen Einstellungen beim nächsten Herunterladen der Clientrichtlinie konfiguriert. Informationen zum Initiieren des Richtlinienabrufs für einen einzelnen Client finden Sie unter [Initiieren des Richtlinienabrufs für einen Configuration Manager-Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Zusätzlich zu den Clienteinstellungen für die Registrierung müssen Sie unbedingt auch die folgenden Configuration Manager-Clientgeräteeinstellungen konfigurieren:  

-   **Hardwareinventur**: Aktivieren und konfigurieren Sie dies, wenn Sie Hardwareinventurdaten von Macintosh- und Windows-Clientcomputern sammeln möchten. Weitere Informationen finden Sie unter [Erweitern der Hardwareinventur in System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

-   **Konformitätseinstellungen**: Aktivieren und konfigurieren Sie dies, wenn Sie Einstellungen von Macintosh- und Windows-Clientcomputern auswerten und wiederherstellen möchten. Weitere Informationen finden Sie unter [Planen und Konfigurieren von Kompatibilitätseinstellungen](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

> [!NOTE]  
>  Weitere Informationen zu Configuration Manager-Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

### <a name="download-the-client-source-files-for-macs"></a>Die Clientquelldateien für Macintosh-Computer herunterladen  
 Bevor Sie den Configuration Manager-Client auf Macintosh-Computern installieren und verwalten können, müssen Sie die folgenden Programme herunterladen und installieren:  

-   **Ccmsetup**: Verwenden Sie diese Anwendung, um den Configuration Manager-Client auf Macintosh-Computern zu installieren.  

-   **CMDiagnostics**: Verwenden Sie dieses Tool, um Diagnoseinformationen zu dem auf Macintosh-Computern installierten Configuration Manager-Client zu sammeln.  

-   **CMUninstall**: Verwenden Sie diese Anwendung, um den Configuration Manager-Client auf Macintosh-Computern zu installieren.  

-   **CMAppUtil**: Verwenden Sie dieses Tool, um Apple-Anwendungspakete in ein Format zu konvertieren, das als Configuration Manager-Anwendung bereitgestellt werden kann.  

-   **CMEnroll**: Verwenden Sie dieses Tool, um das Clientzertifikat für einen Macintosh-Computer anzufordern und zu installieren, damit Sie den Configuration Manager-Client installieren können.  

> [!IMPORTANT]  
>  Wenn Sie einen neuen Client für Macintosh-Computer installieren, müssen Sie möglicherweise auch Configuration Manager-Updates installieren, um die neuen Clientinformationen in der Configuration Manager-Konsole darzustellen.  

##### <a name="to-download-and-install-the-mac-os-x-client-files"></a>So können Sie die Mac OS X-Clientdateien herunterladen und installieren  

1.  Laden Sie das Mac OS X-Clientdateipaket, **ConfigmgrMacClient.msi**, herunter, und speichern Sie es auf einem Computer mit Windows.  

     Diese Datei wird nicht auf den Configuration Manager-Installationsmedien bereitgestellt. Diese Datei steht im [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184)als Download zur Verfügung.  

2.  Führen Sie auf dem Windows-Computer die soeben heruntergeladene Datei **ConfigmgrMacClient.msi** aus, um das Mac-Clientpaket „Macclient.dmg“ in einem Ordner auf der lokalen Festplatte (standardmäßig **C:\Programme (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**) zu extrahieren.  

3.  Kopieren Sie die Datei Macclient.dmg in einen Ordner auf dem Macintosh-Computer.  

4.  Führen Sie auf dem Macintosh-Computer die Datei Macclient.dmg aus, um die Dateien in einem Ordner auf der lokalen Festplatte zu extrahieren.  

5.  Überprüfen Sie im Ordner, ob die Dateien Ccmsetup und CMClient.pkg extrahiert wurden und ein Ordner mit dem Namen Tools erstellt wurde, in dem die Tools CMDiagnostics, CMUninstall, CMAppUtil und CMEnroll enthalten sind.  

### <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Installieren Sie den Client, und melden Sie anschließend das Clientzertifikat auf dem Macintosh-Computer an  
 Mithilfe dieses Verfahrens wird der Client installiert. Anschließend wird das Tool CMEnroll ausgeführt, um das Clientzertifikat für einen Macintosh-Computer anzufordern und zu installieren, sodass Sie diesen Computer anschließend mithilfe von Configuration Manager verwalten können.  

 Sie können den Client mithilfe des Assistenten für Macintosh-Computeranmeldung anmelden, ohne das Tool „CMEnroll“ zu verwenden, wie in [Registrieren des Clients mithilfe des Assistenten für die Macintosh-Registrierung](#enroll-the-client-by-using-the-mac-computer-enrollment-wizard) beschrieben.  

#### <a name="to-install-the-client-and-enroll-the-certificate-by-using-the-cmenroll-tool"></a>So installieren Sie den Client und melden das Zertifikat mithilfe des Tools „CMEnroll“ an  

1.  Navigieren Sie auf dem Macintosh-Computer zu dem Ordner, in dem Sie den Inhalt der Datei Macclient.dmg extrahiert haben.  

2.  Geben Sie die folgende Befehlszeile ein: **sudo ./ccmsetup**  

3.  Warten Sie, bis die Meldung **Installation abgeschlossen** angezeigt wird. Vom Installationsprogramm wird eine Meldung angezeigt, dass Sie den Computer jetzt neu starten müssen. Führen Sie den Neustart nicht aus, sondern fahren Sie mit dem nächsten Schritt fort.  

4.  Geben Sie im Ordner „Extras“ auf dem Macintosh-Computer Folgendes ein: **sudo ./CMEnroll -s &lt;Name_des_Anmeldungsproxyservers> -ignorecertchainvalidation -u &lt;'Benutzername'>**  

    Nach der Clientinstallation wird der Assistent für die Macintosh-Computeranmeldung geöffnet, um Ihnen beim Anmelden des Macintosh-Computers zu helfen. Informationen zum Anmelden des Clients mit dieser Methode finden Sie unter [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) in diesem Thema.  

5. Geben Sie das Kennwort für das Active Directory-Benutzerkonto ein.  Wenn Sie diesen Befehl eingeben, müssen Sie zwei Kennwörter eingeben: Zuerst müssen Sie das Kennwort für das Administratorkonto eingeben, um den Befehl auszuführen. Die zweite Eingabeaufforderung bezieht sich auf das Active Directory-Benutzerkonto. Da beide Eingabeaufforderungen identisch aussehen, achten Sie darauf, dass Sie die richtige Reihenfolge einhalten.  

    Der Benutzername kann die folgenden Formate aufweisen:  

    -   'Domäne\Name'. Beispiel: 'contoso\mrankenburg'  

    -   'user@domain'. Beispiel: 'mnorth@contoso.com'  

     Der Benutzername und das zugehörige Kennwort müssen mit den entsprechenden Angaben eines Active Directory-Benutzerkontos übereinstimmen, für das in der Mac-Clientzertifikatvorlage die Berechtigungen Lesen und Anmelden zugewiesen wurden.  

     Beispiel: Wenn der Name des Registrierungsproxypunkt-Servers **server02.contoso.com**lautet und dem Benutzernamen **contoso\mnorth** Berechtigungen für die Macintosh-Computer-Clientzertifikatvorlage erteilt wurden, geben Sie Folgendes ein: **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  Wenn der Benutzername eins der Zeichen **&lt;> "+=,** enthält, tritt ein Fehler bei der Anmeldung auf. Um dieses Problem zu beheben, rufen Sie ein Out-of-Band-Zertifikat mit einem Benutzernamen ab, der diese Zeichen nicht enthält.  
    >  
    >  Zur Verbesserung der Benutzerfreundlichkeit können Sie ein Skript für die Installationsschritte und -befehle erstellen, sodass die Benutzer nur ihren Benutzernamen und ihr Kennwort angeben müssen.  

5.  Warten Sie, bis die Meldung angezeigt wird, dass die **Anmeldung erfolgreich** war.  

6.  Öffnen Sie auf dem Macintosh-Computer ein Terminalfenster, und nehmen Sie folgende Änderungen vor, um das registrierte Zertifikat auf Configuration Manager zu beschränken:  

    a.  Geben Sie den Befehl **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**ein.  

    b.  Klicken Sie im Dialogfeld **Schlüsselbundverwaltung** im Abschnitt **Schlüsselbunde** auf **System**, und im Abschnitt **Kategorie** anschließend auf **Schlüssel**.  

    c.  Erweitern Sie die Schlüssel, um die Clientzertifikate anzuzeigen. Wenn Sie das Zertifikat mit einem gerade installierten privaten Schlüssel identifiziert haben, doppelklicken Sie auf dem Schlüssel.  

    d.  Wählen Sie auf der Registerkarte **Zugriffssteuerung** die Option **Confirm before allowing access** (Bestätigen, bevor Zugriff zugelassen wird) aus.  

    e.  Navigieren Sie zum Ordner **/Library/Application Support/Microsoft/CCM**, wählen Sie **CCMClient** aus, und wählen Sie dann **Hinzufügen** aus.  

    f.  Wählen Sie **Änderungen sichern** aus, und schließen Sie das Dialogfeld **Schlüsselbundverwaltung**.  

7.  Starten Sie den Macintosh-Computer neu.  

 Überprüfen Sie, ob die Clientinstallation erfolgreich ausgeführt wurde. Öffnen Sie hierzu auf dem Macintosh-Computer in den **Systemeinstellungen** das Element **Configuration Manager** . Sie können auch die Sammlung **Alle Systeme** aktualisieren und anzeigen, um sicherzustellen, dass der Macintosh-Computer jetzt in der Sammlung als verwalteter Client angezeigt wird.  

> [!TIP]  
>  Sie können Probleme mit dem Mac-Client mithilfe des Programms CMDiagnostics beheben, das im Mac OS X-Clientpaket enthalten ist. Damit können die folgenden Diagnoseinformationen gesammelt werden:  
>   
>  -   Eine Liste der ausgeführten Prozesse  
> -   Die Version des Mac OS X-Betriebssystems  
> -   Mac OS X-Absturzberichte, die sich auf den Configuration Manager-Client beziehen, einschließlich **CCM\*.crash** und **System Preference.crash**.  
> -   Die BOM-Datei (Bill of Materials) und die Eigenschaftenlistendatei (PLIST-Datei), die im Rahmen der Configuration Manager-Clientinstallation erstellt wurden  
> -   Der Inhalt des Ordners /Library/Application Support/Microsoft/CCM/Logs  
>   
>  Die von CmDiagnostics gesammelten Informationen werden einer ZIP-Datei hinzugefügt, die auf dem Desktop des Computers gespeichert und „cmdiag-*<Hostname\>***-***<Datum und Uhrzeit\>*.zip“ benannt wird.  

####  <a name="enroll-the-client-by-using-the-mac-computer-enrollment-wizard"></a>So registrieren Sie den Client mithilfe des Assistenten für die Macintosh-Computeranmeldung  

1.  Nach der Installation des Clients wird der Assistent für die Computeranmeldung wird geöffnet. Wird der Assistent nicht geöffnet, oder haben Sie ihn versehentlich geschlossen, dann klicken Sie auf der Einstellungsseite von **Configuration Manager** auf **Anmelden** , um den Assistenten zu öffnen.  

2.  Geben Sie auf der zweiten Seite des Assistenten die folgenden Informationen ein:  

    -   **Benutzername** : Der Benutzername kann die folgenden Formate aufweisen:  

        -   'Domäne\Name'. Beispiel: 'contoso\mrankenburg'  

        -   'user@domain'. Beispiel: 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  Wenn Sie in das Feld **Benutzername** eine E-Mail-Adresse eingeben, wird von Configuration Manager automatisch der Domänenname der E-Mail-Adresse und der Standardname des Registrierungsproxypunkt-Servers für das Feld **Servername** verwendet. Wenn der Domänenname und der Servername nicht mit dem Namen des Anmeldungsproxypunkt-Servers übereinstimmen, müssen Sie die Benutzer über den richtigen Namen informieren, damit sie diesen bei der Anmeldung ihrer Macintosh-Computer eingeben können.  

         Der Benutzername und das zugehörige Kennwort müssen mit den entsprechenden Angaben eines Active Directory-Benutzerkontos übereinstimmen, für das in der Mac-Clientzertifikatvorlage die Berechtigungen Lesen und Anmelden zugewiesen wurden.  

    -   **Kennwort** – Geben Sie ein passendes Kennwort für den angegebenen Benutzernamen ein.  

    -   **Servername** – Geben Sie den Namen des Registrierungsproxypunkt-Servers ein.  

3.  Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen, und schließen Sie dann den Assistenten ab.  

## <a name="maintenance-tasks-for-mac-clients"></a>Wartungsaufgaben für Macintosh-Clients

###  <a name="uninstalling-the-mac-client"></a>Deinstallieren des Mac-Clients  

1.  Öffnen Sie auf dem Macintosh-Computer ein Terminal-Fenster, und navigieren Sie zu dem Ordner, in dem Sie den Inhalt der Datei macclient.dmg extrahiert haben, die Sie heruntergeladen haben.  

2.  Navigieren Sie zum Ordner Tools, und geben Sie die folgende Befehlszeile ein:  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  Durch die Eigenschaft **-c** werden bei der Deinstallation des Clients auch die Absturzprotokolle und die Protokolldateien des Clients entfernt. Ihre Angabe ist optional, stellt aber eine bewährte Methode dar, um Verwirrungen bei einer späteren erneuten Installation zu vermeiden.  

3.  Entfernen Sie bei Bedarf manuell das Clientauthentifizierungszertifikat, das von Configuration Manager verwendet wurde, oder widerrufen Sie es. Von „CMUninstall“ wird dieses Zertifikat nicht entfernt oder widerrufen.  

###  <a name="renewing-the-mac-client-certificate"></a>Erneuern des Zertifikats für den Macintosh-Client  
 Verwenden Sie eines der folgenden Verfahren, um das Zertifikat für den Macintosh-Client zu erneuern:  

-   [Assistent zum Verlängern von Zertifikaten](#renew-certificate-wizard)  

-   [Manuelles Verlängern des Zertifikats](#renew-certificate-manually)  

####  <a name="renew-certificate-wizard"></a>Assistent zum Verlängern von Zertifikaten  

1.  Konfigurieren Sie in der Datei „ccmclient.plist“ die folgenden Werte als *Zeichenfolgen*, mit denen gesteuert wird, wann der Assistent zum Verlängern von Zertifikaten geöffnet wird:  

    -   **RenewalPeriod1** – Hiermit wird der erste Erneuerungszeitraum (in Sekunden) angegeben, in dem Benutzer das Zertifikat erneuern können. Der Standardwert beträgt 3.888.000 Sekunden (45 Tage). Legen Sie keinen Wert kleiner als 300 fest, da der Zeitraum auf den Standardwert zurückgesetzt wird. 


    -   **RenewalPeriod2** – Hiermit wird der zweite Erneuerungszeitraum (in Sekunden) angegeben, in dem Benutzer das Zertifikat erneuern können. Der Standardwert beträgt 259.200 Sekunden (3 Tage). Wenn dieser Wert konfiguriert ist und größer gleich 300 Sekunden und kleiner gleich **RenewalPeriod1** ist, wird der Wert verwendet. Wenn **RenewalPeriod1** größer als 3 Tage ist, wird ein Wert von 3 Tagen für **RenewalPeriod2**verwendet.  Wenn **RenewalPeriod1** kleiner als 3 Tage ist, dann wird **RenewalPeriod2** auf denselben Wert wie **RenewalPeriod1**festgelegt.  

    -   **RenewalReminderInterval1** – Gibt das Intervall an (in Sekunden), in dem Benutzern während des ersten Erneuerungszeitraums der Assistent zum Erneuern von Zertifikaten angezeigt wird. Der Standardwert beträgt 86.400 Sekunden (1 Tag). Wenn **RenewalReminderInterval1** größer als 300 Sekunden, aber kleiner als der für **RenewalPeriod1**konfigurierte Wert ist, wird der konfigurierte Wert verwendet. Andernfalls wird der Standardwert 1 Tag verwendet.  

    -   **RenewalReminderInterval2** – Gibt das Intervall an (in Sekunden), in dem Benutzern während des zweiten Erneuerungszeitraums der Assistent zum Erneuern von Zertifikaten angezeigt wird. Der Standardwert beträgt 28.800 Sekunden (8 Stunden). Wenn **RenewalReminderInterval2** größer als 300 Sekunden, aber kleiner oder gleich **RenewalReminderInterval1** und kleiner oder gleich **RenewalPeriod2**ist, wird der konfigurierte Wert verwendet. Andernfalls wird ein Wert von 8 Stunden verwendet.  

     **Beispiel:** Werden die Standardwerte nicht geändert, dann wird der Assistent 45 Tage vor Ablauf des Zertifikats alle 24 Stunden geöffnet.  In den letzten 3 Tagen vor Zertifikatsablauf wird der Assistent alle 8 Stunden geöffnet.  

     **Beispiel:** Legen Sie mit der folgenden Befehlszeile oder einem Skript den ersten Erneuerungszeitraum auf 20 Tage fest.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  Wenn der Assistent zum Erneuern von Zertifikaten geöffnet wird, sind die Felder **Benutzername** und **Servername** normalerweise bereits ausgefüllt, und der Benutzer muss lediglich ein Kennwort eingeben, um das Zertifikat zu erneuern.  

    > [!NOTE]  
    >  Wird der Assistent nicht geöffnet, oder haben Sie ihn versehentlich geschlossen, dann klicken Sie auf der Einstellungsseite von **Configuration Manager** auf **Erneuern** , um den Assistenten zu öffnen.  

####  <a name="renewing-the-mac-client-certificate-manually"></a>Manuelles Erneuern des Zertifikats für den Macintosh-Client  
 Der typische Gültigkeitszeitraum für das Macintosh-Clientzertifikat beträgt 1 Jahr. Das während der Registrierung angeforderte Benutzerzertifikat wird von Configuration Manager nicht automatisch erneuert, weswegen Sie wie folgt vorgehen müssen, um das Zertifikat zu erneuern.  

> [!IMPORTANT]  
>  Wenn das Zertifikat abläuft, müssen Sie den Macintosh-Client deinstallieren, neu installieren und dann erneut anmelden.  

 Durch dieses Verfahren wird die SMS-ID entfernt, die zur Anforderung eines neuen Zertifikats für denselben Macintosh-Computer erforderlich ist. Wenn Sie die Client-SMS-ID entfernen und ersetzen, wird der gesamte gespeicherte Clientverlauf, wie beispielsweise der Bestand, nach dem Löschen des Clients über die Configuration Manager-Konsole gelöscht.  

1.  Erstellen Sie für die Mac-Computer, deren Benutzerzertifikate verlängert werden müssen, eine Gerätesammlung.  

    > [!WARNING]  
    >  Der Gültigkeitszeitraum des für Macintosh-Computer registrierten Zertifikats wird von Configuration Manager nicht überwacht. Dies müssen Sie unabhängig von Configuration Manager übernehmen, um die Macintosh-Computer zu identifizieren, die dieser Sammlung hinzugefügt werden müssen.  

2.  Starten Sie im Arbeitsbereich **Bestand und Kompatibilität** den **Assistenten zum Erstellen von Konfigurationselementen**.  

3.  Geben Sie auf der Seite **Allgemein** des Assistenten die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Typ:Mac OS X**  

4.  Vergewissern Sie sich auf der Seite **Unterstützte Plattformen** des Assistenten, dass alle Versionen von Mac OS X ausgewählt sind.  

5.  Wählen Sie auf der Seite **Einstellungen** des Assistenten **Neu**, und geben Sie anschließend im Dialogfeld **Einstellung erstellen** die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Einstellungstyp:Skript**  

    -   **Datentyp:Zeichenfolge**  

6.  Wählen Sie im Dialogfeld **Einstellung erstellen** für **Ermittlungsskript** **Skript hinzufügen** aus, um ein Skript anzugeben, mit dem Mac-Computer ermittelt werden können, die über eine konfigurierte SMSID verfügen.  

7.  Geben Sie im Dialogfeld **Ermittlungsskript bearbeiten** das folgende Shellskript ein:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Wählen Sie **OK**, um das Dialogfeld **Ermittlungsskript bearbeiten** zu schließen.  

9. Wählen Sie im Dialogfeld **Einstellung erstellen** für **Wiederherstellungsskript (optional)** **Skript hinzufügen** aus, um ein Skript anzugeben, mit dem die SMSID von Mac-Computern entfernt wird, wenn sie gefunden wird.  

10. Geben Sie im Dialogfeld **Wiederherstellungsskript erstellen** das folgende Shellskript ein:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Wählen Sie **OK** aus, um das Dialogfeld **Wiederherstellungsskript erstellen** zu schließen.  

12. Klicken Sie auf der Seite **Kompatibilitätsregeln** des Assistenten auf **Neu**, und geben Sie anschließend im Dialogfeld **Regel erstellen** die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Ausgewählte Einstellung:** Wählen Sie **Durchsuchen** aus, und wählen Sie anschließend das Ermittlungsskript aus, das Sie zuvor angegeben haben.  

    -   Geben Sie im Feld **die folgenden Werte** **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**ein.  

    -   Aktivieren Sie die Option **Das angegebene Wiederherstellungsskript ausführen, wenn diese Einstellung nicht kompatibel ist**.  

13. Beenden Sie den Assistenten zum Erstellen von Konfigurationselementen.  

14. Erstellen Sie eine Konfigurationsbaseline mit dem Konfigurationselement, das Sie gerade erstellt haben, und stellen Sie es für die Gerätesammlung bereit, die Sie in Schritt 1 erstellt haben.  

     Weitere Informationen zum Erstellen und Bereitstellen von Konfigurationsbaselines finden Sie unter [Erstellen von Konfigurationsbaselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) und [Bereitstellen von Konfigurationsbaselines in System Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. Führen Sie auf Macintosh-Computern, auf denen die SMS-ID entfernt wurde, den folgenden Befehl aus, um ein neues Zertifikat zu installieren:  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Geben Sie das Kennwort für das Administratorkonto ein, wenn Sie dazu aufgefordert werden, um den Befehl auszuführen. Geben Sie dann das Kennwort für das Active Directory-Benutzerkonto ein.  

16. Öffnen Sie auf dem Macintosh-Computer ein Terminalfenster, und nehmen Sie folgende Änderungen vor, um das registrierte Zertifikat auf Configuration Manager zu beschränken:  

    a.  Geben Sie den Befehl **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**ein.  

    b.  Wählen Sie im Dialogfeld **Schlüsselbundverwaltung** im Abschnitt **Schlüsselbunde** **System** aus, und im Abschnitt **Kategorie** anschließend **Schlüssel**.  

    c.  Erweitern Sie die Schlüssel, um die Clientzertifikate anzuzeigen. Wenn Sie das Zertifikat mit einem gerade installierten privaten Schlüssel identifiziert haben, doppelklicken Sie auf dem Schlüssel.  

    d.  Wählen Sie auf der Registerkarte **Zugriffssteuerung** die Option **Confirm before allowing access** (Bestätigen, bevor Zugriff zugelassen wird) aus.  

    e.  Navigieren Sie zum Ordner **/Library/Application Support/Microsoft/CCM**, wählen Sie **CCMClient** aus, und wählen Sie dann **Hinzufügen** aus.  

    f.  Wählen Sie **Änderungen sichern** aus, und schließen Sie das Dialogfeld **Schlüsselbundverwaltung**.  

17. Starten Sie den Macintosh-Computer neu.  

##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Verwenden einer von Configuration Manager unabhängigen Zertifikatanforderungs- und -installationsmethode  
 Wenn Sie keine Configuration Manager-Anmeldung verwenden, sondern das Clientzertifikat unabhängig von Configuration Manager anfordern und installieren, gibt es bei den Konfigurationsschritten kleine Unterschiede.

Beginnen Sie, indem Sie *nur* diese Schritte ausführen:

a. [Stellen Sie ein Webserverzertifikat für Standortsystemserver bereit](#deploy-a-web-server-certificate-to-site-system-servers)

b. [Stellen Sie ein Clientauthentifizierungszertifikat für Standortsystemserver bereit](#deploy-a-client-authentication-certificate-to-site-system-servers)

c. [Konfigurieren Sie den Verwaltungspunkt und den Verteilungspunkt](#configure-the-management-point-and-distribution-point)

d. [Optional: Installieren Sie den Reporting Services-Punkt](#optional:-install-the-reporting-services-point)

e. [Laden Sie die Clientquelldateien für Macintosh-Computer herunter](#download-the-client-source-files-forMacs)  
  

#### <a name="to-install-the-client-certificate-independently-from-configuration-manager-and-install-the-client"></a>So installieren Sie das Clientzertifikat unabhängig von Configuration Manager und den Client  

1.  Gehen Sie zur Installation des Clientzertifikats unabhängig von Configuration Manager gemäß den Anweisungen der ausgewählten Methode zur Zertifikatbereitstellung vor, um das Clientzertifikat anzufordern und auf dem Macintosh-Computer zu installieren.  

2.  Navigieren Sie zu dem Ordner, in dem Sie den Inhalt der von der Microsoft Download Center-Website heruntergeladenen Datei macclient.dmg extrahiert haben.  

3.  Geben Sie die folgende Befehlszeile ein: **sudo ./ccmsetup -MP <Verwaltungspunkt_Internet-FQDN\> -SubjectName <Wert für Zertifikatantragsteller\>**.  Beim Wert für den Zertifikatantragsteller muss die Groß-/Kleinschreibung beachtet werden, daher muss dieser genauso eingegeben werden, wie er in den Zertifikatdetails angezeigt wird.  

     Beispiel: Wenn der Internet-FQDN in den Standortsystemeigenschaften **server03.contoso.com** lautet und das Macintosh-Client-Zertifikat den FQDN von **mac12.contoso.com **als allgemeinen Namen für den Zertifikatantragsteller verwendet, geben Sie Folgendes ein: **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  Warten Sie, bis die Meldung **Installation abgeschlossen** angezeigt wird, und starten Sie anschließend den Macintosh-Computer neu.  

5.  Öffnen Sie auf dem Macintosh-Computer ein Terminal-Fenster, und nehmen Sie diese Änderungen vor, um sicherzustellen, dass Configuration Manager auf dieses Zertifikat zugreifen kann:  

    a.  Geben Sie den Befehl **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**ein.  

    b.  Klicken Sie im Dialogfeld **Schlüsselbundverwaltung** im Abschnitt **Schlüsselbunde** auf **System**, und im Abschnitt **Kategorie** anschließend auf **Schlüssel**.  

    c.  Erweitern Sie die Schlüssel, um die Clientzertifikate anzuzeigen. Wenn Sie das Zertifikat mit einem gerade installierten privaten Schlüssel identifiziert haben, doppelklicken Sie auf dem Schlüssel.  

    d.  Wählen Sie auf der Registerkarte **Zugriffssteuerung** die Option **Confirm before allowing access** (Bestätigen, bevor Zugriff zugelassen wird) aus.  

    e.  Navigieren Sie zum Ordner **/Library/Application Support/Microsoft/CCM**, wählen Sie **CCMClient** aus, und wählen Sie dann **Hinzufügen** aus.  

    f.  Wählen Sie **Änderungen sichern** aus, und schließen Sie das Dialogfeld **Schlüsselbundverwaltung**.  

6.  Wenn Sie über mehrere Zertifikate mit dem gleichen Wert für den Antragsteller verfügen, müssen Sie die Seriennummer des Zertifikats angeben, um das für den Configuration Manager-Client zu verwendende Zertifikat zu bestimmen. Verwenden Sie hierzu den folgenden Befehl: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<Seriennummer\>"**.  

     Beispiel: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Überprüfen Sie, ob die Clientinstallation erfolgreich ausgeführt wurde. Öffnen Sie hierzu auf dem Macintosh-Computer in den **Systemeinstellungen** das Element **Configuration Manager**. Sie können auch die Sammlung **Alle Systeme** aktualisieren und anzeigen, um sicherzustellen, dass der Macintosh-Computer in der Sammlung als verwalteter Client angezeigt wird.  

### <a name="renewing-the-mac-client-certificate"></a>Erneuern des Zertifikats für den Macintosh-Client  
 Gehen Sie folgendermaßen vor, bevor Sie das Computerzertifikat auf Macintosh-Computern erneuern.  

 Bei diesem Verfahren wird die SMS-ID entfernt, welche vom Client zur Verwendung eines neuen oder erneuerten Zertifikats auf dem Macintosh-Computer benötigt wird.  

> [!IMPORTANT]  
>  Wenn Sie die Client-SMS-ID entfernen und ersetzen, wird der gesamte gespeicherte Clientverlauf, wie beispielsweise der Bestand, nach dem Löschen des Clients über die Configuration Manager-Konsole gelöscht.  

#### <a name="to-renew-the-mac-client-certificate"></a>So erneuern Sie das Macintosh-Clientzertifikat  

1.  Erstellen Sie für die Mac-Computer, deren Benutzerzertifikate verlängert werden müssen, eine Gerätesammlung.  

2.  Starten Sie im Arbeitsbereich **Bestand und Kompatibilität** den **Assistenten zum Erstellen von Konfigurationselementen**.  

3.  Geben Sie auf der Seite **Allgemein** des Assistenten die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Typ:Mac OS X**  

4.  Vergewissern Sie sich auf der Seite **Unterstützte Plattformen** des Assistenten, dass alle Versionen von Mac OS X ausgewählt sind.  

5.  Klicken Sie auf der Seite **Einstellungen** des Assistenten auf **Neu** , und geben Sie anschließend im Dialogfeld **Einstellung erstellen** die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Einstellungstyp:Skript**  

    -   **Datentyp:Zeichenfolge**  

6.  Klicken Sie im Dialogfeld **Einstellung erstellen** für **Ermittlungsskript**auf **Skript hinzufügen** , um ein Skript anzugeben, mit dem Macintosh-Computer ermittelt werden können, die über eine konfigurierte SMS-ID verfügen.  

7.  Geben Sie im Dialogfeld **Ermittlungsskript bearbeiten** das folgende Shellskript ein:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Wählen Sie **OK** aus, um das Dialogfeld **Ermittlungsskript bearbeiten** zu schließen.  

9. Wählen Sie im Dialogfeld **Einstellung erstellen** für **Wiederherstellungsskript (optional)** **Skript hinzufügen** aus, um ein Skript anzugeben, mit dem die SMSID von Mac-Computern entfernt wird, wenn sie gefunden wird.  

10. Geben Sie im Dialogfeld **Wiederherstellungsskript erstellen** das folgende Shellskript ein:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Wählen Sie **OK** aus, um das Dialogfeld **Wiederherstellungsskript erstellen** zu schließen.  

12. Wählen Sie auf der Seite **Konformitätsregeln** des Assistenten **Neu** aus, und geben Sie anschließend im Dialogfeld **Regel erstellen** die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Ausgewählte Einstellung:** Wählen Sie **Durchsuchen** aus, und wählen Sie anschließend das Ermittlungsskript aus, das Sie zuvor angegeben haben.  

    -   Geben Sie im Feld **die folgenden Werte** **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**ein.  

    -   Aktivieren Sie die Option **Das angegebene Wiederherstellungsskript ausführen, wenn diese Einstellung nicht kompatibel ist**.  

13. Beenden Sie den Assistenten zum Erstellen von Konfigurationselementen.  

14. Erstellen Sie eine Konfigurationsbasislinie mit dem Konfigurationselement, das Sie gerade erstellt haben, und stellen Sie es für die Gerätesammlung bereit, die Sie in Schritt 1 erstellt haben.  

     Weitere Informationen zum Erstellen und Bereitstellen von Konfigurationsbaselines finden Sie unter [Erstellen von Konfigurationsbaselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Führen Sie den folgenden Befehl aus, nachdem Sie ein neues Zertifikat auf Macintosh-Computern mit entfernter SMS-ID installiert haben, um den Client so zu konfigurieren, dass das neue Zertifikat verwendet wird:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. Wenn Sie über mehrere Zertifikate mit dem gleichen Wert für den Antragsteller verfügen, müssen Sie die Seriennummer des Zertifikats angeben, um das für den Configuration Manager-Client zu verwendende Zertifikat zu bestimmen. Verwenden Sie hierzu den folgenden Befehl: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<Seriennummer\>"**.  

     Beispiel: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Starten Sie den Macintosh-Computer neu.  



<!--HONumber=Dec16_HO3-->


