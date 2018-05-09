---
title: Verwalten des Zugriffs auf Skype for Business Online
titleSuffix: Configuration Manager
description: Enthält Informationen zum Verwenden der Richtlinie für bedingten Zugriff, um Skype for Business Online zu verwalten.
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4a88706233e85be6960585963c26bd740e9ff6ed
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="manage-skype-for-business-online-access"></a>Verwalten des Zugriffs auf Skype for Business Online

*Gilt für: System Center Configuration Manager (Current Branch)*


Verwenden Sie die Richtlinie für bedingten Zugriff für Skype for Business Online zum Verwalten des Zugriffs auf Skype for Business Online anhand der Bedingungen, die Sie angeben.  


 Wenn ein Zielbenutzer versucht, Skype for Business Online auf seinem Gerät zu verwenden, wird folgende Bewertung durchgeführt:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Erforderliche Komponenten  

-   Aktivieren Sie die [moderne Authentifizierung](https://aka.ms/SkypeModernAuth) für Skype for Business Online.   

-   Alle Benutzer müssen Skype for Business Online verwenden. Wenn Sie eine Bereitstellung sowohl mit Skype for Business Online als auch Skype for Business On-Premises (Lokal) haben, wird die Richtlinie für bedingten Zugriff nicht für lokale Benutzer angewendet.  

-   Das Gerät, das Zugriff auf Skype for Business Online benötigt, muss folgende Voraussetzungen erfüllen:  

    -   Es muss ein Android- oder iOS-Gerät sein

    -   Es muss bei Microsoft Intune registriert sein

    -   Es muss mit allen bereitgestellten Microsoft Intune-Konformitätsrichtlinien übereinstimmen

 Azure Active Directory speichert den Gerätestatus, der den Zugriff, entsprechend den von Ihnen angegebenen Bedingungen, gewährt oder blockiert.  
Wenn eine Bedingung nicht erfüllt wird, werden dem Benutzer bei der Anmeldung die folgenden Meldungen angezeigt:  

-   Wenn das Gerät nicht bei Microsoft Intune oder in Azure Active Directory registriert ist, werden dem Benutzer Anweisungen zum Installieren der Unternehmensportal-App und zum Registrieren des Geräts angezeigt.  

-   Wenn das Gerät nicht konform ist, wird dem Benutzer eine Nachricht angezeigt, die auf die Unternehmensportal-Website oder die Unternehmensportal-App weiterleitet. Auf dem Unternehmensportal gibt es Informationen zu dem Problem und dessen Behebung.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Konfigurieren des bedingten Zugriffs für Skype for Business Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Schritt 1: Konfigurieren von Active Directory-Sicherheitsgruppen  
 Bevor Sie beginnen, konfigurieren Sie Azure Active Directory-Sicherheitsgruppen für die bedingte Zugriffsichtlinie. Konfigurieren Sie diese Gruppen im Office 365 Admin Center. Diese Gruppen enthalten die Benutzer, die von der Richtlinie beinhaltet oder ausgenommen werden. Bei Benutzern, für die eine Richtlinie gelten soll, muss jedes von ihnen verwendete Gerät die Richtlinie erfüllen, damit sie auf Ressourcen zugreifen können.  

 Sie können zwei Typen von Gruppen angeben, die für die Skype for Business-Richtlinie verwendet werden sollen:  

-   **Zielgruppen** beinhalten Benutzer, für die die Richtlinie gelten soll  

-   **Ausgenommene Gruppen** beinhalten Benutzer, die von der Richtlinie nicht gelten soll  
    Wenn ein Benutzer in beiden Gruppen ist, wird er von der Richtlinie ausgenommen.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Schritt 2: Konfigurieren und Bereitstellen einer Kompatibilitätsrichtlinie  
 Erstellen Sie für alle Geräte, für die die Skype for Business Online-Richtlinie gelten soll, eine Konformitätsrichtlinie und stellen sie bereit.  

 Ausführliche Informationen zum Konfigurieren der Konformitätsrichtlinie finden Sie unter [Konfigurieren der Konformitätsrichtlinien für Geräte](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Wenn Sie keine Konformitätsrichtlinie bereitgestellt haben und dann die Skype for Business Online-Richtlinie aktivieren, ist allen Zielgeräten der Zugriff erlaubt, sofern sie bei Microsoft Intune registriert sind.  


### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Schritt 3: Konfigurieren der Skype for Business Online-Richtlinie  
 Konfigurieren Sie die Richtlinie so, dass nur verwaltete und konforme Geräte auf Skype for Business Online zugreifen dürfen. Diese Richtlinie ist in Azure Active Directory gespeichert.  

1.  Klicken Sie in der [Microsoft Intune-Verwaltungskonsole](https://manage.microsoft.com)auf **Richtlinie** > **Bedingter Zugriff** > **Skype for Business Online Richtlinie**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Wählen Sie **Richtlinie für bedingten Zugriff aktivieren** aus.  

3.  Unter **Anwendungszugriff**können Sie optional eine bedingte Zugriffsrichtlinie auf Folgendes anwenden:  

    -   iOS  

    -   Android  

4.  Klicken Sie unter **Zielgruppen** auf **Ändern**, um die Active Directory-Sicherheitsgruppen auszuwählen, für die die Richtlinie gelten soll. Sie können diese Richtlinie für alle Benutzer oder nur für ausgewählte Benutzergruppen festlegen.  

5.  Klicken Sie unter **Ausgenommene Gruppen**optional auf **Ändern** , um die Active Directory-Sicherheitsgruppen auszuwählen, die von dieser Richtlinie ausgenommen werden.  

6.  Klicken Sie abschließend auf **Speichern**.  

 Sie haben jetzt den bedingten Zugriff für Skype for Business Online konfiguriert. Die Richtlinie für bedingten Zugriff wird sofort wirksam und muss nicht explizit bereitgestellt werden.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>Überwachen der Richtlinien für Konformität und bedingten Zugriff  
 Im Arbeitsbereich „Gruppen“ können Sie den Status beim bedingten Zugriff Ihrer Geräte anzeigen.  

 Wählen Sie eine beliebige Gruppe von Mobilgeräten und anschließend auf der Registerkarte **Geräte** einen der folgenden **Filter**aus:  

-   **Geräte, die nicht bei AAD registriert sind** werden für Skype for Business Online blockiert

-   **Geräte, die nicht konform sind** werden für Skype for Business Online blockiert  

-   **Geräte, die bei AAD registriert und konform sind**, können auf Skype for Business Online zugreifen  

### <a name="see-also"></a>Weitere Informationen:  

 [Manage device compliance policies in System Center Configuration Manager (Verwalten von Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager)](../../protect/deploy-use/device-compliance-policies.md)
