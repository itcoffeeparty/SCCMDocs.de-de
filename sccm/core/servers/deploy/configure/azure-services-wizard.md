---
title: Konfigurieren von Azure-Diensten
titleSuffix: Configuration Manager
description: Verbinden Sie Ihre Configuration Manager-Umgebung mit Azure-Diensten für die Cloudverwaltung, Upgradebereitschaft, den Microsoft Store für Unternehmen und die Operations Management Suite.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b86c73f3f5662a00ca0b7f80b0c785c37aff0b1a
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Konfigurieren von Azure-Diensten zur Verwendung mit dem Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit dem **Assistenten für Azure-Dienste** können Sie die Konfiguration der von Ihnen mit Configuration Manager verwendeten Azure-Clouddienste vereinfachen. Dieser Assistent bietet eine Erfahrung mit der allgemeinen Konfiguration durch Verwendung der Registrierungen für Azure AD-Web-Apps (Azure Active Directory). Diese Apps bieten Einzelheiten zu Abonnements und Konfiguration. Zudem authentifizieren sie die Kommunikation bei Azure AD. Durch die App müssen Sie nicht jedes Mal dieselben Informationen erneut eingeben, wenn Sie mit Azure eine neue Komponente oder einen neuen Dienst für Configuration Manager einrichten.



## <a name="available-services"></a>Verfügbare Dienste

Konfigurieren Sie die folgenden Azure-Dienste mithilfe dieses Assistenten:  

-   **Cloud Management**: Mit diesem Dienst können Standort und Clients sich mit Azure AD authentifizieren. Durch diese Authentifizierung werden weitere Szenarios aktiviert, wie z.B.:  

    - [Installieren und Zuweisen von Windows 10-Clients in Configuration Manager mit Authentifizierung über Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

    - [Configure Azure AD User Discovery (Konfigurieren der Azure AD-Benutzerermittlung)](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Unterstützung bestimmter [Cloud Management Gateway-Szenarios](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

-   **OMS-Connector**: [Stellen Sie eine Verbindung mit Operations Management Suite her](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS). Synchronisieren Sie Daten wie Sammlungen für die OMS-Protokollanalyse.  

-   **Connector für Upgradebereitschaft**: Stellen Sie eine Verbindung mit der [Upgradebereitschaft](/sccm/core/clients/manage/upgrade/upgrade-analytics) von Windows Analytics her. Anzeigen von Clientupgrade-Kompatibilitätsdaten.  

-   **Microsoft Store für Unternehmen**: Stellen Sie eine Verbindung mit [Microsoft Store für Unternehmen](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) her. Hier erhalten Sie Store-Apps für Ihre Organisation, die Sie mit Configuration Manager bereitstellen können.  

### <a name="service-details"></a>Dienstdetails

Die folgende Tabelle enthält Einzelheiten zu den einzelnen Diensten.  

- **Mandanten**: Die Anzahl der konfigurierbaren Dienstinstanzen. Bei jeder Instanz muss es sich um einen anderen Azure-Mandanten handeln.  

- **Clouds**: Die globale Azure-Cloud wird von sämtlichen Diensten unterstützt. Private Clouds wie die Azure US Government Cloud werden jedoch nicht von allen Diensten unterstützt.  

- **Web-App**: Gibt an, ob der Dienst eine Azure AD-App vom Typ *Web-App/API* verwendet, die in Configuration Manager auch als Server-App bezeichnet wird.  

- **Native App**: Gibt an, ob der Dienst eine Azure AD-App vom Typ *Nativ* verwendet, die in Configuration Manager auch als Client-App bezeichnet wird.  

- **Aktionen**: Gibt an, ob Sie diese App im Assistent für Azure-Dienste von Configuration Manager importieren oder erstellen können.  


|Dienst  |Mandanten  |Clouds  |Web-App  |Native App  |Aktionen  |
|---------|---------|---------|---------|---------|---------|
|Cloudverwaltung mit</br>Azure AD-Benutzerermittlung | Mehrere | Öffentlich | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | Importieren, Erstellen |
|OMS-Connector | Einem | Öffentlich, privat | ![Unterstützt](media/green_check.png) | ![Nicht unterstützt](media/Red_X.png) | Importieren |
|Upgradebereitschaft | Einem | Öffentlich | ![Unterstützt](media/green_check.png) | ![Nicht unterstützt](media/Red_X.png) | Importieren |
|Microsoft Store für</br>Unternehmen und Bildung | Einem | Öffentlich | ![Unterstützt](media/green_check.png) | ![Nicht unterstützt](media/Red_X.png) | Importieren, Erstellen |


### <a name="about-azure-ad-apps"></a>Informationen zu Azure AD-Apps

Für verschiedene Azure-Dienste sind unterschiedliche Konfigurationen erforderlich. Diese nehmen Sie im Azure-Portal vor. Darüber hinaus sind für die Apps der einzelnen Dienste möglicherweise separate Berechtigungen für Azure-Ressourcen erforderlich.  

Sie können für mehrere Dienste eine einzige App verwenden. In Configuration Manager und Azure AD muss nur ein Objekt verwaltet werden. Wenn der Sicherheitsschlüssel für die App abläuft, müssen Sie lediglich einen Schlüssel aktualisieren.

Die sicherste Konfiguration erzielen Sie, indem Sie für die einzelnen Dienste separate Apps verwenden. Für die App eines Dienstes sind möglicherweise zusätzliche Berechtigungen erforderlich, die für einen anderen Dienst nicht erforderlich sind. Durch die Verwendung einer App für verschiedene Dienste können mehr Berechtigungen für die App bereitgestellt werden als erforderlich. 

Wenn Sie weitere Azure-Dienste im Assistenten erstellen, kann Configuration Manager allgemeine Informationen zwischen Diensten wiederverwenden. Dadurch müssen Sie die gleichen Informationen nicht mehrmals eingeben. 

Weitere Informationen zu den erforderlichen App-Berechtigungen und Konfigurationen für die einzelnen Dienste finden Sie im zugehörigen Configuration Manager-Artikel unter [Verfügbare Dienste](#available-services). 

Weitere Informationen zu Azure-Apps finden Sie in den folgenden Artikeln:
- [Authentifizierung und Autorisierung in Azure App Service](/azure/app-service/app-service-authentication-overview)
- [Web-App-Übersicht](/azure/app-service-web/app-service-web-overview)
- [Grundlagen der Anwendungsregistrierung in Azure AD](/azure/active-directory/develop/active-directory-authentication-scenarios#basics-of-registering-an-application-in-azure-ad)  
- [Registrieren Sie Ihrer Anwendung bei Ihrem Azure Active Directory-Mandanten](/azure/active-directory/active-directory-app-registration)



## <a name="before-you-begin"></a>Vorbereitung

Nachdem Sie entschieden haben, mit welchem Dienst Sie sich verbinden möchten, sollten Sie sich die Tabelle unter [Dienstdetails](#service-details) ansehen. Diese Tabelle enthält die Informationen, die Sie zum Ausführen des Assistenten für Azure-Dienste benötigen. Besprechen Sie dies vorab mit Ihrem Azure AD-Administrator. Entscheiden Sie, ob Sie die Apps im Voraus manuell im Azure-Portal erstellen und die App-Details anschließend in Configuration Manager importieren möchten. Alternativ können Sie die Apps mithilfe von Configuration Manager direkt in Azure AD erstellen. Lesen Sie die Informationen in den anderen Abschnitten dieses Artikels, um die notwendigen Daten von Azure AD erfassen.

Bei einigen Diensten müssen die Azure AD-Apps über bestimmte Berechtigungen verfügen. Überprüfen Sie die Informationen für die einzelnen Dienste, um alle erforderlichen Berechtigungen zu bestimmen. Bevor Sie eine Web-App importieren können, muss diese z.B. zunächst von einem Administrator im [Azure-Portal](https://portal.azure.com) erstellt werden. Bei der Konfiguration der Upgradebereitschaft oder des OMS-Connectors müssen Sie Ihrer neu registrierten Berechtigung *Mitwirkender* für die Ressourcengruppe erteilen, die den relevanten OMS-Arbeitsbereich enthält. Mit dieser Berechtigung kann Configuration Manager auf diesen Arbeitsbereich zugreifen. Suchen Sie beim Zuweisen der Berechtigung im Blatt **Benutzer hinzufügen** nach dem Namen der App-Registrierung. Dieser Prozess ist mit [Bereitstellen von Configuration Manager mit Berechtigungen in OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) identisch. Ein Azure-Administrator muss diese Berechtigungen zuweisen, bevor Sie die App in Configuration Manager importieren können.



## <a name="start-the-azure-services-wizard"></a>Starten des Assistenten für Azure-Dienste

1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Clouddienste**, und wählen Sie anschließend den Knoten **Azure-Dienste** aus.  

2.  Klicken Sie im Menüband auf der Registerkarte **Start** in der Gruppe **Azure-Dienste** auf **Azure-Dienste konfigurieren**.  

3.  Gehen Sie auf der Seite **Azure-Dienste** des Assistenten für Azure-Dienste wie folgt vor:  

    1. Geben Sie einen **Namen** für das Objekt in Configuration Manager an.  

    2. Geben Sie eine optionale **Beschreibung** an, mit der Sie den Dienst identifizieren können.  

    3. Wählen Sie den Azure-Dienst aus, den Sie mit Configuration Manager verbinden möchten.  

4. Klicken Sie auf **Weiter**, um mit der Seite [Azure-App-Eigenschaften](#azure-app-properties) des Assistenten für Azure-Dienste fortzufahren.  



## <a name="azure-app-properties"></a>Azure-App-Eigenschaften

Wählen Sie auf der Seite **App** des Assistenten für Azure-Dienste zunächst die **Azure-Umgebung** aus der Liste aus. In der Tabelle unter [Dienstdetails](#service-details) finden Sie Informationen darüber, welche Umgebung derzeit für den Dienst verfügbar ist.

Die restlichen Inhalte der Seite „App“ variieren je nach angegebenem Dienst. In der Tabelle unter [Dienstdetails](#service-details) finden Sie Informationen darüber, welche Art von App der Dienst verwendet, und welche Aktion Sie verwenden können. 
- Klicken Sie auf **Durchsuchen**, wenn die App Import- und Erstellaktionen unterstützt. Durch diese Aktion wird das Dialogfeld [Server-App](#server-app-dialog) oder das Dialogfeld [Client-App](#client-app-dialog) geöffnet.
- Klicken Sie auf **Importieren**, wenn die App nur die Importaktion unterstützt. Durch diese Aktion wird das Dialogfeld [Apps importieren (Server)](#import-apps-dialog-server) oder das Dialogfeld [Apps importieren (Client)](#import-apps-dialog-client) geöffnet.

Klicken Sie nach Angabe der Apps auf dieser Seite auf **Weiter**, um mit der Seite [Konfiguration oder Ermittlung](#configuration-or-discovery) des Assistenten für Azure-Dienste fortzufahren.

### <a name="web-app"></a>Web-App

Diese App ist eine Azure-AD-App vom Typ *Web-App/API*, die in Configuration Manager auch als Server-App bezeichnet wird.

#### <a name="server-app-dialog"></a>Dialogfeld „Server-App“

Wenn Sie auf der Seite „App“ des Assistenten für Azure-Dienste bei der **Web-App** auf **Durchsuchen** klicken, wird das Dialogfeld „Server-App“ geöffnet. Es zeigt eine Liste an, die folgende Eigenschaften sämtlicher vorhandener Web-Apps enthält:
- Anzeigename des Mandanten
- App-Anzeigename
- Diensttyp

Sie können über das Dialogfeld „Server-App“ drei Aktionen ausführen:
- Wenn Sie eine vorhandene Web-App wiederverwenden möchten, wählen Sie diese aus der Liste aus. 
- Klicken Sie auf **Importieren**, um das Dialogfeld [Apps importieren](#import-apps-dialog-server) zu öffnen.
- Klicken Sie auf **Erstellen**, um das Dialogfeld [Serveranwendung erstellen](#create-server-application-dialog) zu öffnen.

Klicken Sie nach dem Auswählen, Importieren oder Erstellen einer Web-App auf **OK**, um das Dialogfeld „Server-App“ zu schließen. Diese Aktion kehrt zur Seite [App](#azure-app-properties) des Assistenten für Azure-Dienste zurück.

#### <a name="import-apps-dialog-server"></a>Dialogfeld „Apps importieren (Server)“

Wenn Sie auf der Seite „App“ des Assistenten für Azure-Dienste im Dialogfeld „Server-App“ auf **Importieren** klicken, wird das Dialogfeld „Apps importieren“ geöffnet. Auf dieser Seite können Sie die Informationen zu einer Azure AD-Web-App eingeben, die bereits im Azure-Portal erstellt wurde. Zudem werden Metadaten zu dieser Web-App in Configuration Manager importiert. Geben Sie die folgenden Informationen an:
- **Name des Azure AD-Mandanten**
- **Azure AD-Mandanten-ID**
- **Anwendungsname**: Ein Anzeigename für die App.
- **Client-ID**
- **Geheimer Schlüssel**
- **Ablauf des geheimen Schlüssels**: Wählen Sie im Kalender ein Datum in der Zukunft aus. 
- **App-ID-URI**: Dieser Wert muss bei Ihrem Azure AD-Mandanten eindeutig sein. Es handelt sich dabei um das Zugriffstoken, das der Configuration Manager-Client verwendet, um Zugriff auf den Dienst anzufordern. Dieser Wert lautet standardmäßig „https://ConfigMgrService“.  

Klicken Sie nach Eingabe der Informationen auf **Überprüfen**. Klicken Sie anschließend auf **OK**, um das Dialogfeld „Apps importieren“ zu schließen. Diese Aktion kehrt entweder zur Seite [App](#azure-app-properties) des Assistenten für Azure-Dienste oder zum Dialogfeld [Server-App](#server-app-dialog) zurück.

#### <a name="create-server-application-dialog"></a>Dialogfeld „Serveranwendung erstellen“

Wenn Sie im Dialogfeld „Server-App“ auf **Erstellen** klicken, wird das Dialogfeld „Serveranwendung erstellen“ geöffnet. Auf dieser Seite wird die Erstellung einer Web-App in Azure AD automatisiert. Geben Sie die folgenden Informationen an:
- **Anwendungsname**: Ein Anzeigename für die App.
- **URL für Homepage**: Dieser Wert wird nicht von Configuration Manager verwendet, ist jedoch für Azure AD erforderlich. Dieser Wert lautet standardmäßig „https://ConfigMgrService“.  
- **App-ID-URI**: Dieser Wert muss bei Ihrem Azure AD-Mandanten eindeutig sein. Es handelt sich dabei um das Zugriffstoken, das der Configuration Manager-Client verwendet, um Zugriff auf den Dienst anzufordern. Dieser Wert lautet standardmäßig „https://ConfigMgrService“.  
- **Gültigkeitsdauer des geheimen Schlüssels**: Klicken Sie auf die Dropdownliste, und wählen Sie entweder **1 Jahr** oder **2 Jahre** aus. Ein Jahr ist der Standardwert.

Klicken Sie auf **Anmelden**, um sich bei Azure als Administrator zu authentifizieren. Diese Anmeldeinformationen werden nicht in Configuration Manager gespeichert. Für diese Persona sind keine Berechtigungen in Configuration Manager erforderlich. Zudem muss das Konto nicht mit dem Konto identisch sein, auf dem der Assistent für Azure-Dienste ausgeführt wird. Nach einer erfolgreichen Authentifizierung in Azure, wird zu Referenzzwecken der **Name des Azure AD-Mandanten** auf der Seite angezeigt. 

Klicken Sie auf **OK**, um die Web-App in Azure AD zu erstellen und das Dialogfeld „Serveranwendung erstellen“ zu schließen. Diese Aktion kehrt zum Dialogfeld [Server-App](#server-app-dialog) zurück.


### <a name="native-client-app"></a>Native Client-App
    
Diese App ist eine Azure-AD-App vom Typ *Nativ*, die in Configuration Manager auch als Client-App bezeichnet wird.

#### <a name="client-app-dialog"></a>Dialogfeld „Client-App“

Wenn Sie auf der Seite „App“ des Assistenten für Azure-Dienste bei der **Nativen Client-App** auf **Durchsuchen** klicken, wird das Dialogfeld „Client-App“ geöffnet. Es zeigt eine Liste an, die folgende Eigenschaften sämtlicher vorhandener nativer Apps enthält:
- Anzeigename des Mandanten
- App-Anzeigename
- Diensttyp

Sie können über das Dialogfeld „Client-App“ drei Aktionen ausführen:
- Wenn Sie eine vorhandene native App wiederverwenden möchten, wählen Sie diese aus der Liste aus. 
- Klicken Sie auf **Importieren**, um das Dialogfeld [Apps importieren](#import-apps-dialog-client) zu öffnen.
- Klicken Sie auf **Erstellen**, um das Dialogfeld [Clientanwendung erstellen](#create-client-application-dialog) zu öffnen.

Klicken Sie nach dem Auswählen, Importieren oder Erstellen einer nativen App auf **OK**, um das Dialogfeld „Client-App“ zu schließen. Diese Aktion kehrt zur Seite [App](#azure-app-properties) des Assistenten für Azure-Dienste zurück.

#### <a name="import-apps-dialog-client"></a>Dialogfeld „Apps importieren (Client)“

Wenn Sie beim Dialogfeld „Client-App“ auf **Importieren** klicken, wird das Dialogfeld „Apps importieren“ geöffnet. Auf dieser Seite können Sie die Informationen zu einer nativen Azure AD-App eingeben, die bereits im Azure-Portal erstellt wurde. Zudem werden Metadaten zu dieser nativen App in Configuration Manager importiert. Geben Sie die folgenden Informationen an:
- **Anwendungsname**: Ein Anzeigename für die App.
- **Client-ID** 

Klicken Sie nach Eingabe der Informationen auf **Überprüfen**. Klicken Sie anschließend auf **OK**, um das Dialogfeld „Apps importieren“ zu schließen. Diese Aktion kehrt zum Dialogfeld [Client-App](#client-app-dialog) zurück.

#### <a name="create-client-application-dialog"></a>Dialogfeld „Clientanwendung erstellen“

Wenn Sie im Dialogfeld „Client-App“ auf **Erstellen** klicken, wird das Dialogfeld „Clientanwendung erstellen“ geöffnet. Auf dieser Seite wird die Erstellung einer nativen App in Azure AD automatisiert. Geben Sie die folgenden Informationen an:
- **Anwendungsname**: Ein Anzeigename für die App.
- **Antwort-URL**: Dieser Wert wird nicht von Configuration Manager verwendet, ist jedoch für Azure AD erforderlich. Dieser Wert lautet standardmäßig „https://ConfigMgrService“. 

Klicken Sie auf **Anmelden**, um sich bei Azure als Administrator zu authentifizieren. Diese Anmeldeinformationen werden nicht in Configuration Manager gespeichert. Für diese Persona sind keine Berechtigungen in Configuration Manager erforderlich. Zudem muss das Konto nicht mit dem Konto identisch sein, auf dem der Assistent für Azure-Dienste ausgeführt wird. Nach einer erfolgreichen Authentifizierung in Azure, wird zu Referenzzwecken der **Name des Azure AD-Mandanten** auf der Seite angezeigt. 

Klicken Sie auf **OK**, um die native App in Azure AD zu erstellen und das Dialogfeld „Clientanwendung erstellen“ zu schließen. Diese Aktion kehrt zum Dialogfeld [Client-App](#client-app-dialog) zurück.


## <a name="configuration-or-discovery"></a>Konfiguration oder Ermittlung

Nach der Angabe der Web-Apps und nativen Apps auf der Seite „Apps“ fährt der Assistent für Azure-Dienste mit der Seite **Konfiguration** oder der Seite **Ermittlung** fort. Dies hängt von dem Dienst ab, mit dem Sie eine Verbindung herstellen. Die Details auf dieser Seite variieren abhängig vom jeweiligen Dienst. Weitere Informationen finden Sie in den folgenden Artikeln:  

-   Dienst **Cloud Management**, Seite **Erkennung**: [Konfigurieren der Azure AD-Benutzerermittlung](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

-   Dienst **OMS-Connector**, Seite **Konfiguration**: [Konfigurieren der Verbindung mit OMS](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#use-the-azure-services-wizard-to-configure-the-connection-to-oms)  

-   Dienst **Connector für Upgradebereitschaft**, Seite **Konfiguration**: [Verwenden des Azure-Assistenten zum Erstellen der Verbindung](/sccm/core/clients/manage/upgrade/upgrade-analytics#use-the-azure-wizard-to-create-the-connection)  

-   Dienst **Microsoft Store für Unternehmen**, Seite **Konfigurationen**: [Einrichten der Synchronisierung mit Microsoft Store für Unternehmen](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#for-configuration-manager-version-1706-and-later)  


Schließlich können Sie den Assistenten für Azure-Dienste über die Seiten „Zusammenfassung“, „Status“ und „Abschluss“ abschließen. Sie haben die Konfiguration eines Azure-Diensts in Configuration Manager abgeschlossen. Anhand dieser Anleitung können Sie auch weitere Azure-Dienste konfigurieren.


## <a name="view-the-configuration-of-an-azure-service"></a>Anzeigen der Konfiguration eines Azure-Diensts
Sie können die Eigenschaften eines Azure-Diensts anzeigen lassen, den Sie zur Verwendung konfiguriert haben. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Clouddienste**, und wählen Sie **Azure-Dienste** aus. Wählen Sie den Dienst aus, den Sie anzeigen oder bearbeiten möchten, und klicken Sie anschließend auf **Eigenschaften**.

Wenn Sie einen Dienst auswählen und anschließend im Menüband auf **Löschen** klicken, wird durch diese Aktion die Verbindung in Configuration Manager gelöscht. Die App in Azure AD wird dadurch nicht entfernt. Bitten Sie Ihren Azure-Administrator, die App zu löschen, wenn sie nicht mehr benötigt wird. Alternativ können Sie den Assistenten für Azure-Dienste ausführen, um die App zu importieren.<!--483440-->


## <a name="cloud-management-data-flow"></a>Datenfluss bei der Cloudverwaltung

Bei dem folgenden Diagramm handelt es sich um einen konzeptionellen Datenfluss zwischen Configuration Manager, Azure AD und verbundenen Clouddiensten. In diesem konkreten Beispiel wird der Dienst **Cloudverwaltung** verwendet, der einen Windows 10-Client sowie Server- und Client-Apps umfasst. Die Abläufe bei anderen Diensten sind vergleichbar.

![Datenflussdiagramm für Configuration Manager mit Azure AD und Cloudverwaltung](media/aad-auth.png)

1.  Der Configuration Manager-Administrator importiert oder erstellt die Client- und Server-Apps in Azure AD.  

2.  Die Methode für die Azure AD-Benutzerermittlung in Configuration Manager wird ausgeführt. Der Standort verwendet das Token der Azure AD-Server-App für die Abfrage von Microsoft Graph nach Benutzerobjekten.  

3.  Der Standort speichert Daten zu den Benutzerobjekten. Weitere Informationen finden Sie unter [Azure AD-Benutzerermittlung](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).  

4.  Der Configuration Manager-Client fordert das Azure AD-Benutzertoken an. Der Client stellt den Anspruch mit der Anwendungs-ID der Azure AD-Client-App und der Server-App als Zielgruppe. Weitere Informationen finden Sie unter [Ansprüche in Azure AD-Sicherheitstokens](/azure/active-directory/develop/active-directory-authentication-scenarios#claims-in-azure-ad-security-tokens).  

5.  Der Client authentifiziert sich bei dem Standort durch die Bereitstellung des Azure AD-Tokens für Cloud Management Gateway und/oder den lokalen HTTPS-fähigen Verwaltungspunkt.  


