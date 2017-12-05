---
title: "Assistent für Azure-Dienste"
titleSuffix: Configuration Manager
description: "Informationen zum Assistent für Azure-Dienste in System Center Configuration Manager"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 7646e8bc368e5c01ddef41592c513f7bd1643cdb
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Konfigurieren von Azure-Diensten zur Verwendung mit dem Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab der Current Branch-Version 1706 kommt der **Assistent für Azure-Dienste** zum Einsatz, um die Konfiguration der von Ihnen verwendeten Azure-Dienste mit Configuration Manager zu vereinfachen.

Dieser Assistent bietet allgemeine Konfigurationsfunktionen durch die **Web-App-Registrierung von Azure AD**, um Details zu Abonnements und Konfigurationen bereitzustellen und Kommunikation mit Azure AD zu authentifizieren. Durch die Web-App müssen sie nicht jedes Mal dieselben Informationen erneut eingeben, wenn Sie mit Azure eine neue Komponente oder einen neuen Dienst für den Configuration Manager einrichten.

Die folgenden Azure-Dienste werden mithilfe des Assistenten der Azure-Dienste konfiguriert:
-   **Cloud Management**  (Cloudverwaltung)  
    [Enable clients to authenticate by using Azure Active Directory (Authentifizieren von Clients mithilfe von Azure Active Directory ermöglichen)](/sccm/core/clients/deploy/deploy-clients-cmg-azure) (Azure AD). Sie können ebenfalls die [Azure AD-Benutzerermittlung konfigurieren](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
-   **OMS-Connector**
    [ Hiermit können Sie eine Verbindung mit der Operations Manager-Suite (OMS) herstellen](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) und Daten wie Sammlungen mit OMS Log Analytics synchronisieren.
-   **Upgrade Readiness (Upgradebereitschaft)**
    [Connect to Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) (Verbinden Sie sich mit Upgrade Readiness), um Daten zur Kompatibilität von Clientupgrades anzuzeigen.
-   **Windows Store for Business**: Mit diesem Dienst können Sie sich mit dem Onlineshop [Windows Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) verbinden, um Apps für Ihre Organisation mit dem Configuration Manager bereitzustellen.

Wenn Sie den Assistenten verwenden, um einen Dienst zu konfigurieren, sind einige gängige Aktionen verfügbar.
Dazu gehören:
-   *Konfigurieren der Azure-Umgebung*: Wählen Sie auf der **App**-Seite des Assistenten die **Azure-Umgebung** aus, die Sie verwenden. Lassen Sie den Inhalt jedes Dienstes anzeigen, um zu erfahren, ob dieser nur die öffentliche oder auch die private Azure-Cloud unterstützt.
-   *Erstellen oder Importieren einer Server-App*: Auf der **App**-Seite des Assistenten können Sie Registrierungsmetadaten von Azure-Web-Apps **erstellen** und **importieren**. Je nachdem, welchen Dienst Sie konfigurieren, sind andere Optionen verfügbar. Darüber hinaus können einige Dienste eine zusätzliche App erfordern. Der Dienst **Cloud Management** erfordert eine **native Client-App**, mit der Clients die Kommunikation mit Azure-Diensten direkt authentifizieren können.


Weitere Informationen zu Azure-Web-Apps finden Sie unter [Authentifizierung und Autorisierung in Azure App Service](/azure/app-service/app-service-authentication-overview) und [Web-Apps – Übersicht](/azure/app-service-web/app-service-web-overview).


## <a name="webapp"></a> Erstellen oder Importieren einer Web-App-Registrierung von Azure AD zur Verwendung mit Configuration Manager

Die Web-App-Registrierung für Azure-Dienste verbindet Ihren Configuration Manager-Standort mit Azure AD und ist eine Voraussetzung dafür, Azure-Dienste mit Ihrer Infrastruktur zu verwenden. Dazu ist Folgendes erforderlich:

1.  Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Clouddienste**, und klicken Sie dann auf **Azure-Dienste**.
2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Azure-Dienste** auf **Azure-Dienste konfigurieren**.
3.  Wählen Sie auf der Seite **Azure-Dienste** des Assistenten für Azure-Dienste den Azure-Dienst aus, den Sie mit Configuration Manager verbinden möchten.
4.  Geben Sie auf der Seite **Allgemein** des Assistenten einen Namen und eine Beschreibung für den Azure-Dienst ein.
5.  Wählen Sie in der Liste auf der **App**-Seite des Assistenten Ihre Azure-Umgebung aus, und klicken Sie auf **Durchsuchen**, um die *Web-App* und die *native Client-App* auszuwählen, mit denen der Azure-Dienst konfiguriert wird.

    **Web-App:** Mit „Durchsuchen“ wird das Server-App-Fenster geöffnet.    
      Wählen Sie im Fenster **Server-App** die Server-App aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**. Server-Apps sind die Web-Apps-Registrierungen von Azure AD, die die Konfigurationen für Ihr Azure-Konto enthalten, einschließlich Ihrer Mandanten-ID, Client-ID und eines geheimen Schlüssels für Clients.
    Wenn Sie nicht über eine verfügbare App verfügen, verwenden Sie eine der folgenden:

    - **Create** (Erstellen): Automatisieren Sie die Erstellung einer Web-App-Registrierung für Azure AD anhand der Informationen, die Sie in der Configuration Manager-Konsole eingeben. Geben Sie einen Anzeigenamen für die App, die URL der Homepage, den URI der App-ID und eine Gültigkeitsdauer für den geheimen Schlüssel an. Standardmäßig ist die Gültigkeitsdauer des geheimen Schlüssels ein Jahr.
        
        Um den Vorgang fortzusetzen, müssen Sie sich mit Ihren Azure AD-Anmeldeinformationen anmelden, um dort die Erstellung der Web-App abzuschließen. Das Konto, das Sie verwenden, um sich bei Azure anzumelden, muss nicht dasselbe sein, auf dem der Assistent für Azure-Dienste ausgeführt wird. Nachdem Sie sich bei Azure angemeldet haben, erstellt Configuration Manager die Web-App in Azure für Sie, einschließlich der Client-ID und des geheimen Schlüssels für die Web-App. Später können Sie diese im Azure-Portal anzeigen.

        Wenn Sie die Option *Create* verwenden, um eine Web-App zu konfigurieren, kann der Configuration Manager die Web-App für Sie in Azure AD erstellen.
    
    - **Import** (Importieren): Geben Sie Informationen zu einer Web-App-Registrierung von Azure AD ein, die bereits im **Azure-Portal** erstellt wurde, um Metadaten zu dieser Registrierung in Configuration Manager zu importieren. Stellen Sie einen Anzeigenamen für die App und den Mandanten bereit, und geben Sie dann die Mandanten-ID, Client-ID und den geheimen Schlüssel für die Web-App an, die Configuration Manager verwenden soll. Nachdem Sie die Informationen überprüft haben, klicken Sie auf **OK**, um fortzufahren.
        > [!NOTE]
        > Bevor Sie **Import** verwende können, muss eine App-Registrierung von Azure AD des Typs *Web-App/API* im [Azure-Portal](https://portal.azure.com) erstellt werden. Weitere Informationen zum Erstellen einer App-Registrierung finden Sie unter [Registrieren Ihrer Anwendung bei Ihrem Azure Active Directory-Mandanten](/azure/active-directory/active-directory-app-registration). Beim Konfigurieren der Upgradebereitschaft oder von Operations Management Suite müssen Sie auch dem *Mitwirkenden* an Ihrer neu registrierten Web-App Berechtigungen für die Ressourcengruppe erteilen, die den relevanten OMS-Arbeitsbereich enthält, damit Configuration Manager auf diesen Arbeitsbereich zugreifen kann. Dazu müssen Sie beim Zuweisen der Berechtigungen auf dem Blatt **Benutzer hinzufügen** nach dem Namen der App-Registrierung suchen. Beim [Bereitstellen von OMS-Berechtigungen für Configuration Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) für Verbindungen mit [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm) wenden Sie das gleiche Verfahren an. Diese Berechtigungen müssen zugewiesen werden, bevor die App in Configuration Manager importiert wird.


    **Native Client-App:** Mit „Durchsuchen“ wird das Client-App-Fenster geöffnet.  
     Wählen Sie im Fenster **Client-App** die Client-App aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.

     Wenn Sie nicht über eine verfügbare Client-App verfügen, verwenden Sie eine der folgenden:
     - **Erstellen**: Um eine neue Client-App zu erstellen, klicken Sie auf **Erstellen**. Geben Sie dann einen Anzeigenamen für die App und den Umleitungs-URI an.

         Um den Vorgang fortzusetzen, müssen Sie sich mit Ihren Azure AD-Anmeldeinformationen anmelden, um dort die Erstellung der Web-App durchzuführen. Das Konto, das Sie verwenden, um sich bei Azure anzumelden, muss nicht dasselbe sein, auf dem der Assistent für Azure-Dienste ausgeführt wird. Nachdem Sie sich bei Azure angemeldet haben, erstellt Configuration Manager die native Client-App in Azure AD für Sie, einschließlich der Client-ID und geheimem Schlüssel. Später können Sie diese im [Azure-Portal](https://portal.azure.com) anzeigen. 

     - **Import** (Importieren): Nutzen Sie eine Client-App, die bereits in Ihrem Azure-Abonnement vorhanden ist. Geben Sie einen Anzeigenamen für die App und die Client-ID an. Klicken Sie dann auf **OK** , um den Vorgang fortzusetzen.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  (Nur beim Konfigurieren des **Cloud Management**-Diensts) Klicken Sie auf der Seite **Ermittlung** des Assistenten auf **Azure Active Directory-Benutzerermittlung aktivieren**, und klicken Sie dann auf **Einstellungen**.
Konfigurieren Sie im Dialogfeld **Einstellungen der Azure AD-Benutzerermittlung** einen Zeitplan für die Ermittlung. Sie können auch die Deltaermittlung aktivieren, bei der nur eine Überprüfung auf neue oder geänderte Konten in Azure AD erfolgt. Erfahren Sie mir über die [Azure AD User Discovery (Azure AD-Benutzerermittlung](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

7.  Schließen Sie den Assistenten ab.

Nun haben Sie die Konfiguration eines Azure-Diensts in Configuration Manager abgeschlossen. Anhand dieser Anleitung können Sie auch weitere Azure-Dienste konfigurieren.

## <a name="view-the-configuration-of-an-azure-service"></a>Anzeigen der Konfiguration eines Azure-Diensts
Sie können die Eigenschaften eines Azure-Diensts anzeigen lassen, den Sie zur Verwendung konfiguriert haben.

Navigieren Sie in der Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Azure-Dienste**. Wählen Sie anschließend den Dienst, den Sie anzeigen oder bearbeiten wollen, und klicken Sie dann auf **Properties** (Eigenschaften).
