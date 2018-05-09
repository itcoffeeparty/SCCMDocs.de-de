---
title: Manage volume-purchased iOS apps
titleSuffix: Configuration Manager
description: Sie können Lizenzen für Apps, die Sie über den Apple iOS App Store erworben haben, bereitstellen, verwalten und nachverfolgen.
ms.date: 03/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f94cc80d41eb346cb1d4c2fc314d310005c7b5f2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Verwalten von iOS-Apps, die über ein Volumenprogramm erworben wurden, mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*



 Der Apple iOS App Store bietet die Möglichkeit, mehrere Lizenzen für eine App zu kaufen, die in Ihrem Unternehmen ausgeführt werden soll. Dadurch können Sie den Verwaltungsaufwand reduzieren, der durch das Nachverfolgen mehrerer von Ihnen erworbener App-Kopien entsteht.  

 Der Configuration Manager unterstützt Sie bei der Bereitstellung und Verwaltung von iOS-Apps, die Sie über das Programm erworben haben. Sie können die Lizenzinformationen aus dem App Store importieren und die Anzahl der von Ihnen verwendeten Lizenzen verfolgen.  



## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Verwalten von Apps für iOS-Geräte, die über ein Volumenprogramm erworben wurden  
 Sie erwerben mehrere Lizenzen für iOS-Apps über das Programm „Volume Purchase Program“ (VPP) von Apple. Dieser Prozess umfasst zunächst die Einrichtung eines Apple VPP-Kontos auf der Apple-Website. Laden Sie dann das Apple VPP-Token in Configuration Manager hoch, um die folgenden Möglichkeiten zu erhalten:  

-   Synchronisieren Ihrer Volume Purchase-Informationen mit Configuration Manager  
 
- Synchronisieren von Apps aus dem Apple Volume Purchase Program für Unternehmen und aus dem Apple Volume Purchase Program für Bildungseinrichtungen  

- Zuordnen mehrerer Apple VPP-Token zu Configuration Manager  

-   Anzeigen erworbener Apps in der Configuration Manager-Konsole  

-   Bereitstellen und Überwachen dieser Apps  

-   Verfolgen der Anzahl von Lizenzen, die für die einzelnen Apps verwendet werden   

-   Ggf. Freigeben von Lizenzen mithilfe von Configuration Manager durch Deinstallieren von Apps, die per Volumenlizenz erworben und bereitgestellt wurden  



## <a name="before-you-start"></a>Vorbereitung  
 Bevor Sie beginnen, müssen Sie ein VPP-Token von Apple abrufen und es in Configuration Manager hochladen.  

-   Wenn Sie zuvor ein VPP-Token für ein anderes Produkt für die Verwaltung mobiler Geräte in Ihrem vorhandenen Apple VPP-Konto verwendet haben, müssen Sie für die Verwendung mit Configuration Manager ein neues erstellen.  
-   Jedes Token ist ein Jahr lang gültig.  
-   Standardmäßig wird Configuration Manager zweimal am Tag mit dem Apple VPP-Dienst synchronisiert, um sicherzustellen, dass Ihre Lizenzen mit Configuration Manager synchronisiert sind. Dabei werden nur Änderungen an Ihren Lizenzen synchronisiert. Eine vollständige Synchronisierung wird einmal pro Woche ausgeführt. Wenn Sie **Sync** auswählen, um eine manuelle Synchronisierung durchzuführen, wird durch diese Aktion immer eine vollständige Synchronisierung ausgelöst.  
-   Wenn Sie eine Configuration Manager-Datenbank wiederherstellen müssen, sollten Sie im Anschluss daran eine manuelle Synchronisierung ausführen. So stellen Sie sicher, dass die synchronisierten Lizenzdaten auf dem aktuellen Stand sind.  
-   Darüber hinaus müssen Sie ein gültiges APNs-Zertifikat (Apple Push Notification Service) von Apple importieren. Dieses Zertifikat erlaubt die Verwaltung von iOS-Geräten, einschließlich App-Bereitstellung. Weitere Informationen finden Sie unter [Set up iOS hybrid device management (Einrichten der hybriden Verwaltung von iOS-Geräten)](enroll-hybrid-ios-mac.md).  
-   Configuration Manager unterstützt bis zu 3.000 VPP-Token.

Sie können lizenzierte Apps sowohl für Geräte als auch für Benutzer bereitstellen. Je nachdem, inwieweit die App Gerätelizenzierungen unterstützt, wird eine entsprechende Lizenz wie folgt beansprucht:

|Unterstützt die App Gerätelizenzierung?|Typ der Bereitstellungssammlung|Beanspruchte Lizenz|
|---|---|---|
|Ja|Benutzer|Benutzerlizenz|
|Nein|Benutzer|Benutzerlizenz|
|Ja|Gerät|Gerätelizenz|
|Nein|Gerät|Benutzerlizenz|



## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Schritt 1: Abrufen und Hochladen eines Apple VPP-Tokens  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Cloud Services** > **Apple Volume Purchase Program Tokens** (Apple Volume Purchase Program-Token) aus.   

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Apple Volume Purchase Program Tokens** (Apple Volume Purchase Program-Token) **Add Apple Volume Purchase Program Token** (Apple Volume Purchase Program-Token hinzufügen) aus.  

4.  Konfigurieren Sie auf der Seite **Allgemein** des **Assistenten zum Hinzufügen von Apple Volume Purchase Program-Token** die folgenden Einstellungen:   

    -   **Name**: Geben Sie einen Namen für dieses Token ein, der in der Configuration Manager-Konsole angezeigt werden soll.  

    -   **Token**: Klicken Sie auf **Durchsuchen**, und wählen Sie das VPP-Token aus, das Sie von der Apple-Website heruntergeladen haben.  

         Klicken Sie auf den Link zur **Anzeige des Apple VPP-Kontos**. Wenn Sie sich nicht bereits für das Volume Purchase Program für Unternehmen oder Bildungseinrichtungen registriert haben, registrieren Sie sich jetzt. Sobald Sie registriert sind, laden Sie das Apple VPP-Token für Ihr Konto herunter.  

    -   **Beschreibung**: Wenn Sie möchten, können Sie eine Beschreibung eingeben, anhand derer Sie dieses Token in der Configuration Manager-Konsole erkennen können.  

    -   **Zur Verbesserung der Suche und Filterung zugewiesene Kategorien**: Optional können Sie dem VPP-Token Kategorien zuweisen, um die Suche in der Configuration Manager-Konsole zu erleichtern.  
    -   **Apple ID**: Geben Sie die E-Mail-ID von Apple ein, die dem VPP-Token zugeordnet ist.
    -   **Tokentyp**: Wählen Sie den Typ des VPP-Tokens aus, den Sie verwenden möchten. Sie können zwischen den Tokentypen **Business** und **EDU** wählen.

5.  Wählen Sie **Weiter** aus, und schließen Sie den Assistenten ab.  

Über den Knoten **Apple Volume Purchase Program-Token** können Sie jetzt Informationen zum Apple VPP-Token anzeigen. Diese Ansicht enthält den Zeitpunkt der letzten Aktualisierung, das Ablaufdatum und den Zeitpunkt der letzten Synchronisierung.

Die von Apple gespeicherten Daten können jederzeit mit Configuration Manager vollständig synchronisiert werden, indem Sie im Menüband **Synchronisieren** auswählen.  



## <a name="step-2---deploy-a-volume-purchased-app"></a>Schritt 2: Bereitstellen einer im Rahmen des Volumenprogramms erworbenen App  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **License Information for Store Apps** (Lizenzinformationen für Store-Apps) aus.  

3.  Wählen Sie zunächst die App aus, die Sie bereitstellen möchten. Klicken Sie anschließend auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Anwendung erstellen**.
Die Configuration Manager-Anwendung, die erstellt wird, enthält die App „Microsoft Store für Unternehmen“. Sie können diese App dann wie jede andere Configuration Manager-App bereitstellen und überwachen.  

    > [!IMPORTANT]  
    > Wählen Sie als Bereitstellungszweck **Erforderlich** aus. Verfügbare Installationen werden derzeit nicht unterstützt.

 Wenn Sie die App bereitstellen, wird eine Lizenz je Benutzer verwendet, bei einer gerätebasierten Installation eine Lizenz je Gerät. Wenn eine Gerätesammlung das Ziel einer App ist, die Gerätelizenzierung unterstützt, wird eine Gerätelizenz beansprucht. Wenn eine Gerätesammlung das Ziel einer App ist, die Gerätelizenzierung nicht unterstützt, wird eine Benutzerlizenz beansprucht. 

 Wenn Sie eine App im Knoten **Lizenzinformationen für Store-Apps** erstellen, wird die App den Lizenzen des Tokens der von Ihnen ausgewählten App zugeordnet. Es besteht z.B die Möglichkeit, dass Sie im Knoten zwei Versionen der gleichen App sehen. Dieses Verhalten liegt daran, dass jede Version der App einem anderen Apple VPP-Token zugeordnet ist. In diesem Fall könnten Sie Apps von jedem Token erstellen und diese einzeln bereitstellen.

 Um eine Lizenz freizugeben, müssen Sie eine neue Bereitstellung für die App mit der Bereitstellungsaktion **Deinstallieren** erstellen. Sie können die Bereitstellungsaktion nicht in der ursprünglichen Bereitstellung ändern. Die Lizenz wird freigegeben, sobald die App deinstalliert ist.  



## <a name="step-3---monitor-ios-vpp-apps"></a>Schritt 3: Überwachen von iOS VPP-Apps  
 Auf dem Knoten **License Information for Store Apps** (Lizenzinformationen für Store-Apps) im Arbeitsbereich **Softwarebibliothek** werden Informationen über per Volumenlizenz erworbene iOS-Apps angezeigt. Diese Informationen enthalten auch die Gesamtzahl der Lizenzen, die Sie für jede App besitzen, sowie die Anzahl, die bereitgestellt wurde. Zusätzlich wird angezeigt, welchem VPP-Token die App zugeordnet ist und welchen Typ sie aufweist.

 Zudem können Sie auch die Lizenzverwendung für alle von Ihnen erworbenen VPP-Apps mithilfe des Berichts **Apple Volume Purchase Program apps for iOS with license counts** (Apple Volume Purchase Program-Apps für iOS mit Lizenzanzahl) überwachen.  

 In diesem Bericht wird der Name jeder Anwendung zusammen mit der Gesamtzahl der erworbenen Lizenzen, der Anzahl der verfügbaren Lizenzen und weiteren Informationen angezeigt.  

 Informationen zum Ausführen von Configuration Manager-Berichten finden Sie unter [Reporting in System Center Configuration Manager (Berichterstellung in System Center Configuration Manager)](../../core/servers/manage/reporting.md).  



## <a name="delete-an-apple-vpp-token"></a>Löschen eines Apple VPP-Tokens  
<!--505268-->

Verwenden Sie die folgende Schritte, um ein Token aus Configuration Manager löschen:  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Clouddienste**, und wählen Sie **Apple Volume Purchase Program-Token**.  

2. Wählen Sie das zu löschende Token aus.  

3. Klicken Sie im Menüband auf die Option **Löschen**.  

