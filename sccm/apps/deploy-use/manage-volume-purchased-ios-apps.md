---
title: Verwalten von per Volumenlizenz erworbenen iOS-Apps | Microsoft-Dokumentation
description: "Sie können Lizenzen für Apps, die Sie über den iOS App Store erworben haben, bereitstellen, verwalten und nachverfolgen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5e7cead-e257-405b-a2aa-b0130e48dc40
caps.latest.revision: 23
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: cd9edf61d151ac8334ace0bf668fa4c919d8c75b


---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Verwalten von iOS-Apps, die über ein Volumenprogramm erworben wurden, mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*



 Der iOS App Store bietet die Möglichkeit, mehrere Lizenzen für eine App zu kaufen, die in Ihrem Unternehmen ausgeführt werden soll. Dadurch können Sie den Verwaltungsaufwand reduzieren, der durch das Nachverfolgen mehrerer App-Kopien entsteht, die Sie erworben haben.  

 System Center Configuration Manager unterstützt Sie nun bei der Bereitstellung und Verwaltung von iOS-Apps, die über das Programm erworben wurden, indem die Lizenzinformationen aus dem App-Store importiert werden, und die Anzahl der Lizenzen, die Sie verwendet haben, nachverfolgt wird.  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Verwalten von Apps für iOS-Geräte, die über ein Volumenprogramm erworben wurden  
 Sie erwerben mehrere Lizenzen für iOS-Apps über das Programm „Volume Purchase Program“ (VPP) von Apple. Dies umfasst das Einrichten eines Apple VPP-Kontos auf der Apple-Website, und das Hochladen des Apple VPP-Tokens zu Configuration Manager. Dadurch haben Sie folgende Möglichkeiten:  

-   Sie können Ihre Volume Purchase-Informationen mit Configuration Manager synchronisieren.  

-   Erworbene Apps werden in der Configuration Manager-Konsole angezeigt.  

-   Sie können diese Apps bereitstellen und überwachen, und die Anzahl von Lizenzen für die verwendeten Apps nachverfolgen.  

-   Configuration Manager kann Sie dabei unterstützen, bei Bedarf Lizenzen durch Deinstallieren von Apps freizugeben, die per Volumenlizenz erworben und für Benutzer bereitgestellt wurden.  

## <a name="before-you-start"></a>Vorbereitung  
 Bevor Sie beginnen, müssen Sie ein VPP-Token von Apple abrufen und es in Configuration Manager hochladen.  

> [!IMPORTANT]  
>  -   Derzeit kann jede Organisation nur über ein VPP-Konto und -Token verfügen.  
> -   Es wird nur das Apple Volume Purchase Program für Unternehmen unterstützt.  
> -   Sobald Sie Intune ein Apple VPP-Konto zugeordnet haben, können Sie anschließend kein anderes Konto zuordnen. Aus diesem Grund müssen Sie sicherstellen, dass mehreren Personen die Details des verwendeten Kontos bekannt sind.  
> -   Wenn Sie zuvor ein VPP-Token für ein anderes Produkt für die Verwaltung mobiler Geräte in Ihrem vorhandenen Apple VPP-Konto verwendet haben, müssen Sie für die Verwendung mit Configuration Manager ein neues erstellen.  
> -   Jedes Token ist ein Jahr lang gültig.  
> -   Standardmäßig wird Configuration Manager zweimal am Tag mit dem Apple VPP-Dienst synchronisiert, um sicherzustellen, dass Ihre Lizenzen mit Configuration Manager synchronisiert sind.  
>   
>      Dabei werden nur Änderungen an Ihren Lizenzen synchronisiert. Allerdings wird einmal pro Woche eine vollständige Synchronisierung ausgeführt.  
>   
>      Wenn Sie bei **Synchronisierung** auswählen, dass eine manuelle Synchronisierung ausgeführt werden soll, wird immer eine vollständige Synchronisierung ausgeführt.  
> -   Wenn Sie eine Configuration Manager-Datenbank wiederherstellen müssen, sollten Sie im Anschluss daran eine manuelle Synchronisierung ausführen, um sicherzustellen, dass die synchronisierten Lizenzdaten auf dem aktuellen Stand sind.  
> -   Per Volumenlizenz erworbene iOS-Apps können für Benutzer- oder Gerätesammlungen bereitgestellt werden. VPP-Apps, die Sie für ein Gerät ohne einen Benutzer bereitstellen (z.B. für ein Gerät, das Sie ohne Benutzeraffinität mit dem Device Enrollment Program (DEP) oder mit Apple Configurator registrieren) werden dagegen nicht installiert.  

 Darüber hinaus müssen Sie ein gültiges APNs-Zertifikat (Apple Push Notification Service) von Apple importieren, damit Sie iOS-Geräte verwalten und Apps bereitstellen können. Weitere Informationen finden Sie unter [Set up iOS hybrid device management (Einrichten der hybriden Verwaltung von iOS-Geräten)](../../mdm/deploy-use/enroll-hybrid-ios-mac.md).  

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Schritt 1: Abrufen und Hochladen eines Apple VPP-Tokens  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Cloud Services** > **Apple Volume Purchase Program Tokens** (Apple Volume Purchase Program-Token) aus.   

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Apple Volume Purchase Program Tokens** (Apple Volume Purchase Program-Token) **Add Apple Volume Purchase Program Token** (Apple Volume Purchase Program-Token hinzufügen) aus.  

4.  Konfigurieren Sie auf der Seite **Allgemein** des **Assistenten zum Hinzufügen von Apple Volume Purchase Program-Token** folgende Optionen:   

    -   **Name**: Geben Sie einen Namen für dieses Token ein, der dann in der Configuration Manager-Konsole angezeigt wird.  

    -   **Token**: Klicken Sie auf **Durchsuchen**, und wählen Sie das VPP-Token aus, das Sie von der Apple-Website heruntergeladen haben.  

         Klicken Sie auf den Link **See Apple VPP account** (Siehe Apple VPP-Konto). Wenn Sie sich nicht bereits für das Volume Purchase Program für Unternehmen oder Bildungseinrichtungen registriert haben, registrieren Sie sich jetzt. Sobald Sie registriert sind, laden Sie das Apple VPP-Token für Ihr Konto herunter.  

    -   **Beschreibung**: Wenn Sie möchten, können Sie eine Beschreibung eingeben, anhand derer Sie dieses VPP-Token in der Configuration Manager-Konsole erkennen können.  

    -   **Zur Verbesserung der Suche und Filterung zugewiesene Kategorien**: Optional können Sie dem VPP-Token Kategorien zuweisen, um die Suche in der Configuration Manager-Konsole zu erleichtern.  

5.  Wählen Sie **Weiter** aus, und schließen Sie den Assistenten ab.  

Über den Knoten **Apple Volume Purchase Program Tokens** (Apple Volume Purchase Program-Token) werden nun Informationen zum Apple VPP-Token angezeigt, einschließlich der letzten Aktualisierung, des Ablaufdatums und der letzten Synchronisierung.

Die von Apple gespeicherten Daten können jederzeit mit Configuration Manager vollständig synchronisiert werden. Wählen Sie hierzu auf der Registerkarte **Startseite** in der Gruppe **Synchronisieren** **Synchronisieren** aus.  

## <a name="step-2---deploy-a-volume-purchased-app"></a>Schritt 2: Bereitstellen einer im Rahmen des Volumenprogramms erworbenen App  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **License Information for Store Apps** (Lizenzinformationen für Store-Apps) aus.  

3.  Wählen Sie zunächst die App aus, die Sie bereitstellen möchten. Klicken Sie anschließend auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Anwendung erstellen**.
Die Configuration Manager-Anwendung, die erstellt wird, enthält die App „Windows Store für Unternehmen“. Sie können diese Anwendung wie jede andere Configuration Manager-Anwendung bereitstellen und überwachen.

    > [!IMPORTANT]  
    > Wählen Sie als Bereitstellungszweck **Erforderlich** aus. Verfügbare Installationen werden derzeit nicht unterstützt.

 Wenn Sie die Anwendung bereitstellen, wird eine Lizenz von jedem Benutzer verwendet, der die App installiert.  

 Zum Freigeben einer Lizenz müssen Sie die Bereitstellungsaktion in **Deinstallieren**ändern. Die Lizenz wird freigegeben, sobald die App deinstalliert ist.  

## <a name="step-3---monitor-ios-vpp-apps"></a>Schritt 3: Überwachen von iOS VPP-Apps  
 Auf dem Knoten **License Information for Store Apps** (Lizenzinformationen für Store-Apps) im Arbeitsbereich **Softwarebibliothek** werden Informationen über per Volumenlizenz erworbene iOS-Apps angezeigt. Diese Informationen enthalten auch die Gesamtzahl der Lizenzen, die Sie für jede App besitzen, sowie die Anzahl, die bereitgestellt wurde.

 Zudem können Sie auch die Lizenzverwendung für alle von Ihnen erworbenen VPP-Apps mithilfe des Berichts **Apple Volume Purchase Program apps for iOS with license counts** (Apple Volume Purchase Program-Apps für iOS mit Lizenzanzahl) überwachen.  

 In diesem Bericht wird der Name jeder Anwendung zusammen mit der Gesamtzahl der erworbenen Lizenzen, der Anzahl der verfügbaren Lizenzen und weiteren Informationen angezeigt.  

 Informationen zum Ausführen von Configuration Manager-Berichten finden Sie unter [Reporting in System Center Configuration Manager (Berichterstellung in System Center Configuration Manager)](../../core/servers/manage/reporting.md).  



<!--HONumber=Dec16_HO3-->


