---
title: "Verwalten des Internetzugriffs mittels Richtlinien für verwaltete Browser | System Center Configuration Manager"
description: "Stellen Sie Intune Managed Browser bereit, um den Zugriff auf das Internet zu verwalten und einzuschränken."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 735c45b8-a545-4805-84e5-46204fabd1a6
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e5efee7b94f5c61a610fd9f9fa278c992f9c64b8


---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>Verwalten des Internetzugriffs mittels Richtlinien für verwaltete Browser mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager können Sie die Webbrowseranwendung Intune Managed Browser bereitstellen und der Anwendung eine Richtlinie für verwaltete Browser zuordnen. Die Richtlinie für verwaltete Browser konfiguriert die Liste "Zulassen" oder "Blockieren", um die Websites einzuschränken, die Benutzer des verwalteten Browsers besuchen können.  
  
 Da diese App eine verwaltete App ist, können Sie darauf auch Verwaltungsrichtlinien für mobile Anwendungen anwenden. Hierzu zählt beispielsweise, die Verwendung der Funktionen zum Ausschneiden, Kopieren und Einfügen zu steuern, Bildschirmaufnahmen zu verhindern und sicherzustellen, dass Links zu Inhalten, auf die Benutzer klicken, in anderen verwalteten Apps geöffnet werden. Weitere Informationen finden Sie unter [Schützen von Apps mit Verwaltungsrichtlinien für mobile Anwendungen](../../apps/deploy-use/protect-apps-using-mam-policies.md).  
  
> [!IMPORTANT]  
>  Wenn Benutzer den verwalteten Browser selbst installieren, wird er durch keine von Ihnen angegebenen Richtlinien verwaltet. Um sicherzustellen, dass der Browser von Configuration Manager verwaltet wird, muss die App deinstalliert werden, bevor Sie sie als verwaltete Anwendung bereitstellen können.  

 Sie können Richtlinien für verwaltete Browser für die folgenden Gerätetypen erstellen:  

-   Geräte unter Android 4 und höher  

-   Geräte unter iOS 7 und höher  

> [!NOTE]  
>  Weitere Informationen zur Intune Managed Browser-App und wie Sie sie herunterladen können, finden Sie unter [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) für iOS und [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) für Android.  
  
## <a name="create-a-managed-browser-policy"></a>Erstellen einer Richtlinie für verwaltete Browser  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Anwendungsverwaltung** > **Richtlinien für die Anwendungsverwaltung**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Anwendungsverwaltungsrichtlinie erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** den Namen und die Beschreibung für die Richtlinie ein, und klicken Sie dann auf **Weiter**.  

5.  Wählen Sie auf der Seite **Richtlinientyp** die Plattform aus, wählen Sie **Verwalteter Browser** als Richtlinientyp aus, und klicken Sie dann auf **Weiter**.  

     Wählen Sie auf der Seite **Verwalteter Browser** eine der folgenden Optionen aus:  

    -   **Der verwaltete Browser kann nur die unten aufgeführten URLs öffnen** – Geben Sie eine Liste mit URLs an, die der verwaltete Browser öffnen kann.  

    -   **Der verwaltete Browser kann die unten aufgeführten URLs nicht öffnen** – Geben Sie eine Liste mit URLs an, die der verwaltete Browser nicht öffnen kann.  

    > [!NOTE]  
    >  Eine Richtlinie für verwaltete Browser kann nicht sowohl zulässige als auch blockierte URLs enthalten.  

     Weitere Informationen zu den festlegbaren URL-Formaten finden Sie in diesem Thema unter **URL-Format für zulässige und blockierte URLs** .  

    > [!NOTE]  
    >  Mit dem Richtlinientyp **Allgemein** können Sie die Funktionalität von bereitgestellten Apps ändern, um sie an die Konformitäts- und Sicherheitsrichtlinien Ihres Unternehmens anzupassen. Sie können z. B. Ausschneide-, Kopier- und Einfügevorgänge innerhalb einer eingeschränkten App einschränken. Weitere Informationen zum Richtlinientyp „Allgemein“ finden Sie unter [Schützen von Apps mithilfe von Verwaltungsrichtlinien für mobile Anwendungen in System Center Configuration Manager](../../apps/deploy-use/protect-apps-using-mam-policies.md).  

6.  Schließen Sie den Assistenten ab.  

 Die neue Richtlinie wird im Knoten **Anwendungsverwaltungsrichtlinien** des Arbeitsbereichs **Softwarebibliothek** angezeigt.  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>Erstellen einer Softwarebereitstellung für die Managed Browser-App  
 Nachdem Sie die Richtlinie für verwaltete Browser erstellt haben, können Sie einen Softwarebereitstellungstyp für die Managed Browser-App erstellen. Sie müssen der Managed Browser-App eine Richtlinie "Allgemein" und eine Richtlinie "Verwalteter Browser" zuordnen.  
  
 Weitere Informationen finden Sie unter [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md).  
  
## <a name="security-and-privacy-for-the-managed-browser"></a>Sicherheit und Datenschutz für den verwalteten Browser  

-   Auf iOS-Geräten können von Benutzern besuchte Websites, deren Zertifikat abgelaufen oder nicht vertrauenswürdig ist, nicht geöffnet werden.  

-   Einstellungen, die Benutzer für den integrierten Browser auf ihren Geräten vornehmen, werden nicht vom verwalteten Browser verwendet. Dies liegt daran, da der verwaltete Browser keinen Zugriff auf diese Einstellungen hat.  

-   Wenn Sie die Option **Einfache PIN für Zugriff anfordern** oder **Unternehmensanmeldeinformationen für Zugriff anfordern** in einer Richtlinie für die Verwaltung mobiler Anwendung konfigurieren, die mit dem verwalteten Browser verknüpft ist, und ein Benutzer auf der Authentifizierungsseite auf den Hilfe-Link klickt, kann er beliebige Websites auch dann durchsuchen, wenn diese in der Richtlinie für verwaltete Browser einer Sperrliste hinzugefügt wurden.  

-   Der verwaltete Browser kann nur den Zugriff auf Websites blockieren, wenn darauf direkt zugegriffen wird. Der Zugriff auf die Website kann nicht blockiert werden, wenn dafür Zwischendienste (z. B. ein Übersetzungsdienst) verwendet werden.  

## <a name="reference-information"></a>Referenzinformationen  
  
###  <a name="url-format-for-allowed-and-blocked-urls"></a>URL-Format für zulässige und blockierte URLs  

Nachfolgend wird erläutert, welche Formate und Platzhalter Sie zum Festlegen von URLs in den Zulassungs- und Sperrlisten verwenden können.  

-   Sie können das Platzhaltersymbol '**\***"gemäß den Regeln in der nachfolgenden Liste mit zugelassenen Mustern verwenden.  

-   Stellen Sie sicher, dass Sie bei der Eingabe in die Liste allen URLs **http** oder **https** voranstellen.  

-   Sie können Portnummern in der Adresse angeben. Wenn Sie keine Portnummer angeben, werden folgende Werte verwendet:  

    -   Port 80 für http  

    -   Port 443 für https  

     Das Verwenden von Platzhaltern für die Portnummer wird nicht unterstützt: Beispiele: **http://www.contoso.com:\*** und **http://www.contoso.com: /\***  

-   In der folgenden Tabelle sind die zugelassenen Muster aufgeführt, die Sie zum Festlegen von URLs verwenden können:  

    |URL|Treffer|Stimmt nicht überein mit|  
    |---------|-------------|--------------------|  
    |http://www.contoso.com<br /><br /> Entspricht einer einzelnen Seite|www.contoso.com|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> contoso.com/|  
    |http://contoso.com<br /><br /> Entspricht einer einzelnen Seite|contoso.com/|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com|  
    |http://www.contoso.com/*<br /><br /> Entspricht allen URLs, die mit www.contoso.com beginnen|www.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com/videos/tvshows|host.contoso.com<br /><br /> host.contoso.com/images|  
    |http://*.contoso.com/\*<br /><br /> Entspricht allen Unterdomänen unter "contoso.com"|developer.contoso.com/resources<br /><br /> news.contoso.com/images<br /><br /> news.contoso.com/videos|contoso.host.com|  
    |http://www.contoso.com/images<br /><br /> Entspricht einem einzelnen Ordner|www.contoso.com/images|www.contoso.com/images/dogs|  
    |http://www.contoso.com:80<br /><br /> Entspricht einer einzelnen Seite mit einer Portnummer|http://www.contoso.com:80||  
    |https://www.contoso.com<br /><br /> Entspricht einer einzelnen, sicheren Seite|https://www.contoso.com|http://www.contoso.com|  
    |http://www.contoso.com/images/*<br /><br /> Entspricht einem einzelnen Ordner und allen Unterordnern|www.contoso.com/images/dogs<br /><br /> www.contoso.com/images/cats|www.contoso.com/videos|  

-   Es folgen Beispiele für einige der Eingaben, die Sie nicht festlegen können:  

    -   *.com  

    -   *.contoso/\*  

    -   www.contoso.com/*images  

    -   www.contoso.com/*images\*Schweine  

    -   www.contoso.com/page*  

    -   IP-Adressen  

    -   https://*  

    -   http://*  

    -   http://www.contoso.com :*  

    -   http://www.contoso.com: / *  

> [!NOTE]  
>  *. microsoft.com ist immer zulässig.  
  
### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>Lösen von Konflikten zwischen der Zulassungs- und Sperrliste  
 Wenn mehrere Richtlinien für verwaltete Browser für ein Gerät bereitgestellt werden und Einstellungen in Konflikt stehen, werden sowohl der Modus (zulassen oder blockieren) als auch die URL-Listen ausgewertet. Bei einem Konflikt gilt folgendes Verhalten:  

-   Wenn die Modi in jeder Richtlinie identisch sind, aber die URL-Listen voneinander abweichen, werden die URLs auf dem Gerät nicht erzwungen.  

-   Wenn die Modi in jeder Richtlinie voneinander abweichen, aber die URL-Listen identisch sind , werden die URLs auf dem Gerät nicht erzwungen.  

-   Wenn ein Gerät erstmals Richtlinien für verwaltete Browser empfängt und zwei Richtlinien in Konflikt stehen, werden die URLs auf dem Gerät nicht erzwungen. Sie können die Konflikte über den Knoten **Richtlinienkonflikte** des Arbeitsbereichs **Richtlinie** anzeigen.  

-   Wenn ein Gerät bereits ein Richtlinie für verwaltete Browser erhalten hat und eine zweite Richtlinie mit in Konflikt stehenden Einstellungen bereitgestellt wird, bleiben die ursprünglichen Einstellungen auf dem Gerät bestehen. Sie können die Konflikte über den Knoten **Richtlinienkonflikte** des Arbeitsbereichs **Richtlinie** anzeigen.  



<!--HONumber=Nov16_HO1-->


