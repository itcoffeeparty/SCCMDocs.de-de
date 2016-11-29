---
title: "Schützen von Apps mithilfe von Verwaltungsrichtlinien für mobile Anwendungen | System Center Configuration Manager"
description: "Ändern der Funktionalität von bereitgestellten Apps, damit sie den Kompatibilitäts- und Sicherheitsrichtlinien Ihres Unternehmens entsprechen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b7936-a5ca-45c5-8bef-10424eb2e091
caps.latest.revision: 13
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: dfbf6b2001e3259abb7246ab463682b0ead4f4e8


---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>Schützen von Apps mithilfe von Verwaltungsrichtlinien für mobile Anwendungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit den Richtlinien für die Anwendungsverwaltung können Sie in System Center Configuration Manager die Funktionalität von Apps ändern, die Sie bereitstellen, um sie mit den Kompatibilitäts- und Sicherheitsrichtlinien Ihres Unternehmens in Einklang zu bringen. Sie können z. B. Ausschneide-, Kopier- und Einfügevorgänge innerhalb einer eingeschränkten App einschränken oder eine App so konfigurieren, dass alle Weblinks innerhalb eines verwalteten Browsers geöffnet werden. Anwendungsverwaltungsrichtlinien unterstützen Folgendes:  

-   Geräte unter Android 4 und höher  

-   Geräte unter iOS 7 und höher.  

Neben der Verwaltung von Geräten können Sie Verwaltungsrichtlinien für mobile Apps auch zum Schutz von Apps auf Geräten verwenden, die nicht von Intune verwaltet werden. Mit dieser neuen Funktion können Sie Verwaltungsrichtlinien für mobile Apps auf Apps anwenden, die eine Verbindung mit Office 365-Diensten herstellen. Diese Funktion wird nicht für Apps unterstützt, die eine Verbindung mit lokalem Exchange oder SharePoint herstellen.  
Um diese neue Funktion zu verwenden, müssen Sie das Azure-Vorschauportal verwenden. Die folgenden Themen können Ihnen bei den ersten Schritten helfen:  
-   [Erste Schritte mit Verwaltungsrichtlinien für mobile Apps im Azure-Portal](https://technet.microsoft.com/library/mt627830.aspx)  
-   [Erstellen und Bereitstellen von Verwaltungsrichtlinien für mobile Apps mit Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  

Im Gegensatz zu Konfigurationselementen und -baselines in Configuration Manager wird eine Richtlinie für die Anwendungsverwaltung nicht direkt bereitgestellt. Stattdessen verknüpfen Sie die Richtlinie mit dem Anwendungsbereitstellungstyp, den Sie einschränken möchten. Wenn der App-Bereitstellungstyp bereitgestellt wird und auf Geräten installiert ist, werden die von Ihnen angegebenen Einstellungen wirksam.  

Zum Anwenden von Einschränkungen auf eine App muss die App das Microsoft Intune App Software Development Kit (SDK) enthalten. Es gibt zwei Möglichkeiten, um diesen App-Typ zu beziehen:  

-   **Verwenden einer richtlinienverwalteten App** (Android und iOS): Verfügt über das integrierte App SDK. Um diesen App-Typ hinzuzufügen, geben Sie in einem App Store wie iTunes Store oder Google Play einen Link zur App an. Es ist keine weitere Bearbeitung für diesen App-Typ erforderlich. Eine Liste der richtlinienverwalteten Apps, die für IOS- und Android-Geräte verfügbar sind, finden Sie unter [Verwaltete Apps für Microsoft Intune-Verwaltungsrichtlinien für mobile Anwendungen](https://technet.microsoft.com/en-us/library/dn708489.aspx).  

-   **Verwenden einer „umschlossenen“ App** (Android und iOS): Apps, die mithilfe des **Microsoft Intune App Wrapping Tool**neu gepackt werden, sodass sie das App SDK enthalten. Dieses Tool wird normalerweise verwendet, um Unternehmensanwendungen zu verarbeiten, die intern erstellt wurden. Es kann nicht verwendet werden, um Apps zu verarbeiten, die aus dem App Store heruntergeladen wurden. Weitere Informationen finden Sie unter [Vorbereiten von iOS-Apps für die Verwaltung mobiler Anwendungen mit dem Microsoft Intune App Wrapper-Tool](https://technet.microsoft.com/en-us/library/dn878028.aspx) und [Vorbereiten von Android-Apps für die Verwaltung von mobilen Anwendungen mit dem Microsoft Intune App Wrapper-Tool](https://technet.microsoft.com/en-us/library/mt147413.aspx).  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>Erstellen und Bereitstellen einer App mit einer Verwaltungsrichtlinie für mobile Anwendungen  
  
##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>Schritt 1: Abrufen des Links zu einer richtlinienverwalteten App oder Erstellen einer umschlossenen App  

-   **So rufen Sie einen Link zu einer richtlinienverwalteten App ab** – Suchen Sie im App Store die URL der richtlinienverwalteten App, die Sie bereitstellen möchten, und notieren Sie sie.  

     Die URL der Microsoft Word für iPad-App ist beispielsweise **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  

-   **So erstellen Sie eine umschlossene App** : Verwenden Sie die Informationen in den Themen [Vorbereiten von iOS-Apps für die Verwaltung mobiler Anwendungen mit dem Microsoft Intune App Wrapper-Tool](https://technet.microsoft.com/en-us/library/dn878028.aspx) und [Vorbereiten von Android-Apps für die Verwaltung von mobilen Anwendungen mit dem Microsoft Intune App Wrapper-Tool](https://technet.microsoft.com/en-us/library/mt147413.aspx) , um eine umschlossene App zu erstellen.  

     Das Tool erstellt eine verarbeitete App und eine zugehörige Manifestdatei. Sie verwenden diese Dateien beim Erstellen einer Configuration Manager-Anwendung, in der die App enthalten ist.  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>Schritt 2: Erstellen einer Configuration Manager-Anwendung, in der eine App enthalten ist  
 Die Vorgehensweise zum Erstellen der Configuration Manager-Anwendung hängt davon ab, ob Sie eine richtlinienverwaltete App (externer Link) verwenden oder eine App, die mit dem Microsoft Intune App Wrapping Tool für iOS (App-Paket für iOS) erstellt wurde. Verwenden Sie eines der folgenden Verfahren, um die Configuration Manager-Anwendung zu erstellen.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Anwendung erstellen** , um den Assistenten zum Erstellen von Anwendungen zu öffnen.  

4.  Wählen Sie auf der Seite **Allgemein** die Option **Informationen zu dieser Anwendung automatisch anhand der Installationsdateien erkennen**aus.  

5.  Wählen Sie in der Dropdownliste **Typ** die Option **App package for iOS (\*.ipa file)** (iOS-App-Paketdatei (*.ipa)) aus.  

6.  Klicken Sie auf **Durchsuchen** , um das zu importierende App-Paket auszuwählen, und klicken Sie dann auf **Weiter**.  

7.  Geben Sie auf der Seite **Allgemeine Informationen** die Beschreibung und Kategorieinformationen ein, die Benutzern im Unternehmensportal angezeigt werden sollen.  

8.  Schließen Sie den Assistenten ab.  

 Die neue Anwendung wird im Knoten **Anwendungen** des Arbeitsbereichs **Softwarebibliothek** angezeigt.  
  
### <a name="create-an-application-containing-a-link-to-a-policy-managed-app"></a>Erstellen einer Anwendung mit einem Link zu einer richtlinienverwalteten App  
  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.  
  
3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Anwendung erstellen** , um den Assistenten zum Erstellen von Anwendungen zu öffnen.  

4.  Wählen Sie auf der Seite **Allgemein** die Option **Informationen zu dieser Anwendung automatisch anhand der Installationsdateien erkennen**aus.  

5.  Wählen Sie in der Dropdownliste **Typ** eine der folgenden Optionen aus:  

    -   Für iOS: **App-Paket für iOS aus App Store**  

    -   Für Android: **App-Paket für Android in Google Play**  

6.  Geben Sie die URL für die App (aus Schritt 1) ein, und klicken Sie dann auf **Weiter**.  

7.  Geben Sie auf der Seite **Allgemeine Informationen** die Beschreibung und Kategorieinformationen ein, die Benutzern im Unternehmensportal angezeigt werden sollen.  

8.  Schließen Sie den Assistenten ab.  

 Die neue Anwendung wird im Knoten **Anwendungen** des Arbeitsbereichs **Softwarebibliothek** angezeigt.  

##  <a name="step-3-create-an-application-management-policy"></a>Schritt 3: Erstellen einer Anwendungsverwaltungsrichtlinie  
 Als Nächstes erstellen Sie eine Anwendungsverwaltungsrichtlinie, die Sie der Anwendung zuordnen. Sie können eine Richtlinie vom Typ "Allgemein" oder "Verwalteter Browser" erstellen.  
  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Anwendungsverwaltung** > **Richtlinien für die Anwendungsverwaltung**.  
3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Anwendungsverwaltungsrichtlinie erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** den Namen und die Beschreibung für die Richtlinie ein, und klicken Sie dann auf **Weiter**.  

5.  Wählen Sie auf der Seite **Richtlinientyp** die Plattform und den Richtlinientyp für diese Richtlinie aus, und klicken Sie dann auf **Weiter**. Die folgenden Richtlinientypen sind verfügbar:  

    -   **Allgemein**: Mit dem Richtlinientyp „Allgemein“ können Sie die Funktionalität von bereitgestellten Apps ändern, um sie an die Compliance- und Sicherheitsrichtlinien Ihres Unternehmens anzupassen. Sie können z. B. Ausschneide-, Kopier- und Einfügevorgänge innerhalb einer eingeschränkten App einschränken.  

    -   **Verwalteter Browser**: Konfigurieren Sie, ob das Öffnen einer Liste von URLs durch den verwalteten Browser zugelassen oder blockiert werden soll. Mit dem Richtlinientyp "Verwalteter Browser" können Sie die Funktionalität der Intune Managed Browser-App ändern. Dies ist ein Webbrowser, mit dem Sie die von Benutzern ausführbaren Aktionen verwalten können. Legen Sie beispielsweise fest, welche Websites sie besuchen können und wie Links zu Inhalten innerhalb des Browsers geöffnet werden. Erfahren Sie mehr über die  [Intune Managed Browser-App für iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) und die [Intune Managed Browser-App für Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).  

6.  Konfigurieren Sie auf der Seite **iOS-Richtlinie** oder **Android-Richtlinie** die folgenden Werte nach Bedarf, und klicken Sie dann auf **Weiter**. Die Optionen unterscheiden sich je nach Gerätetyp, für den Sie die Richtlinie konfigurieren.  

|Wert|Weitere Informationen|  
|-----------|----------------------|  
|**Einschränken von anzuzeigenden Webinhalten in einem unternehmensverwalteten Browser**|Wenn diese Einstellung aktiviert ist, werden alle Links aus der App in Managed Browser geöffnet. Sie müssen diese App auf Geräten bereitstellen, damit diese Option funktioniert.|  
|**Verhindern von Android-Sicherungen** oder **Verhindern von iTunes- und iCloud-Sicherungen**|Deaktiviert die Sicherung von Informationen aus der App.|  
|**App Übertragung von Daten an andere Apps erlauben**|Gibt die Apps an, denen diese App Daten senden kann. Sie können auswählen, die Datenübertragung an eine beliebige App nicht zu erlauben, nur die Übertragung an andere eingeschränkte Apps zu erlauben oder die Übertragung an beliebige Apps zuzulassen.<br /><br /> Um für iOS-Geräte den Austausch von Dokumenten zwischen verwalteten und nicht verwalteten Apps zu verhindern, müssen Sie eine Sicherheitsrichtlinie für mobile Geräte konfigurieren und bereitstellen, die die Einstellung **Verwaltete Dokumente in anderen nicht verwalteten Apps zulassen**deaktiviert.<br /><br /> Bei Zulassung der Übertragung nur auf andere eingeschränkte Apps werden die Intune PDF- und Image-Viewer (sofern bereitgestellt) verwendet, um den Inhalt der jeweiligen Typen zu öffnen.|  
|**App Empfang von Daten aus anderen Apps erlauben**|Gibt die Apps an, von denen diese App Daten empfangen kann. Sie können auswählen, die Datenübertragung von einer beliebigen App nicht zu erlauben, nur die Übertragung von anderen eingeschränkten Apps zu erlauben oder die Übertragung von beliebigen Apps zuzulassen.|  
|**"Speichern unter" verhindern**|Deaktiviert die Verwendung der **Speichern unter** -Option in jeder App, die diese Richtlinie verwendet.|  
|**Beschränken von Ausschneiden, Kopieren und Einfügen mit anderen Apps**|Gibt an, wie Ausschneiden, Kopieren und Einfügen mit der App verwendet werden kann. Wählen Sie aus:<br /><br /> **Blockiert** – Ausschneiden, Kopieren und Einfügen zwischen dieser App und anderen Apps nicht zulassen.<br /><br /> **Richtlinienverwaltete Apps** – Nur Ausschneiden, Kopieren und Einfügen zwischen dieser App und anderen eingeschränkten Apps zulassen.<br /><br /> **Richtlinienverwaltete Apps mit Einfügen** – Ermöglicht das Einfügen von aus dieser App ausgeschnittenen oder kopierten Daten nur in andere eingeschränkte Apps. Einfügen der aus beliebigen Apps ausgeschnittenen oder kopierten Daten in diese App zulassen.<br /><br /> **Jede App** – Keine Einschränkungen beim Ausschneiden, Kopieren und Einfügen in oder aus dieser App.|  
|**Einfache PIN für Zugriff erforderlich**|Der Benutzer muss eine PIN-Nummer eingeben, um die App zu verwenden. Benutzer werden aufgefordert, diese beim ersten Ausführen der App zu erstellen.|  
|**Anzahl der Versuche vor dem Zurücksetzen der PIN**|Geben Sie die Anzahl der möglichen PIN-Eingabeversuche, bevor der Benutzer die PIN zurücksetzen muss.|  
|**Unternehmensanmeldeinformationen für Zugriff erforderlich**|Erfordert, dass der Benutzer die Unternehmensanmeldeinformationen eingeben muss, bevor er auf die Anwendung zugreifen kann.|  
|**Gerätekonformität mit Unternehmensrichtlinien für Zugriff erforderlich**|Lässt die Verwendung der App nur dann zu, wenn das Gerät nicht per Jailbreak oder Rooting manipuliert wurde.|  
|**Überprüfen der Zugriffsanforderungen nach (Minuten)**|Geben Sie im Feld **Timeout** den Zeitraum ein, bevor die Zugriffsanforderungen für die App nach dem Starten der App erneut geprüft werden müssen.<br /><br /> Wenn das Gerät offline ist, geben Sie im Feld **Offline-Toleranzperiode** den Zeitraum ein, bevor die Zugriffsanforderungen für die App erneut geprüft werden.|  
|**App-Daten verschlüsseln**|Gibt an, dass alle mit dieser App verknüpften Daten verschlüsselt werden, einschließlich extern gespeicherte Daten, z. B. SD-Karten.<br /><br /> **Verschlüsselung für iOS**<br /><br /> Bei Apps, die einer Configuration Manager-Verwaltungsrichtlinie für mobile Anwendungen zugeordnet sind, werden Daten im Ruhezustand mit vom Betriebssystem bereitgestellter Verschlüsselung auf Geräteebene verschlüsselt. Dies wird durch die Geräte-PIN-Richtlinie aktiviert, die vom IT-Administrator festgelegt werden muss. Wenn eine PIN erforderlich ist, werden die Daten gemäß den Einstellungen in der mobilen Anwendungsverwaltungsrichtlinie verschlüsselt. Wie in der Apple-Dokumentation angegeben, [sind die von iOS 7 verwendeten Module FIPS 140-2-zertifiziert](http://support.apple.com/en-us/HT202739).<br /><br /> **Verschlüsselung für Android**<br /><br /> Bei Apps, die einer Configuration Manager-Verwaltungsrichtlinie für mobile Anwendungen zugeordnet sind, wird die Verschlüsselung von Microsoft bereitgestellt. Daten werden während der E/A-Dateivorgänge gemäß der Einstellung in der mobilen Anwendungsverwaltungsrichtlinie synchron verschlüsselt. Verwaltete Apps auf Android verwenden AES-128-Verschlüsselung im CBC-Modus mit den Plattform-Kryptografie-Bibliotheken. Die Verschlüsselungsmethode ist nicht FIPS 140-2-zertifiziert. Inhalt auf dem Speicher des Geräts wird immer verschlüsselt.|  
    |**Blockieren von Bildschirmaufnahmen** (nur Android-Geräte)|Gibt an, dass die Screen Capture-Funktionen des Geräts blockiert werden, wenn Sie diese App verwenden.|  

7.  Wählen Sie auf der Seite **Verwalteter Browser** aus, ob der verwaltete Browser nur URLs in der Liste öffnen darf oder ob das Öffnen der URLs in der Liste durch den verwalteten Browser blockiert ist. Verwalten Sie die URLs in der Liste, und klicken Sie dann auf **Weiter**.  

    > [!WARNING]  
    >  Weitere Informationen finden Sie unter [Manage Internet access using managed browser policies (Verwalten des Internetzugriffs mit Richtlinien für Managed Browser)](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).  
  
8.  Schließen Sie den Assistenten ab.  

 Die neue Richtlinie wird im Knoten **Anwendungsverwaltungsrichtlinien** des Arbeitsbereichs **Softwarebibliothek** angezeigt.  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>Schritt 4: Zuordnen der Anwendungsverwaltungsrichtlinie zu einem Bereitstellungstyp  
 
 Wenn ein Bereitstellungstyp für eine App erstellt wird, die eine Anwendungsverwaltungsrichtlinie erfordert, erkennt Configuration Manager, dass beim Bereitstellen der App eine Anwendungsverwaltungsrichtlinie mit diesem Bereitstellungstyp verknüpft werden muss, und Sie werden aufgefordert, eine Anwendungsverwaltungsrichtlinie zuzuordnen. Bei Managed Browser müssen Sie sowohl eine Richtlinie "Allgemein" als auch eine Richtlinie "Verwalteter Browser" zuordnen. Weitere Informationen finden Sie unter [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md).  
  
> [!IMPORTANT]  
>  Wenn die Anwendung bereits bereitgestellt ist, tritt bei der Bereitstellung für den neuen Bereitstellungstyp solange ein Fehler auf, bis diese Zuordnung erfolgt ist. Sie können die Zuordnung unter **Eigenschaften** für die Anwendung auf der Registerkarte **Anwendungsverwaltung** vornehmen.  

> [!IMPORTANT]  
>  Für Geräte, die ältere Betriebssysteme als iOS 7.1 ausführen, werden verknüpfte Richtlinien nicht entfernt, wenn die App deinstalliert wird.  
>   
>  Wenn das Gerät über Configuration Manager registriert wird, werden die Richtlinien nicht aus den Apps entfernt. Apps, auf die Richtlinien angewendet wurden, behalten die Richtlinieneinstellungen auch dann bei, wenn die App deinstalliert und neu installiert wurde.  

##  <a name="step-5-monitor-the-app-deployment"></a>Schritt 5: Überwachen der App-Bereitstellung  
 Nachdem Sie eine mit einer Verwaltungsrichtlinie für mobile Anwendungen verknüpfte App erstellt und bereitgestellt haben, können Sie die App überwachen und Richtlinienkonflikte lösen.  
  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Übersicht** > **Bereitstellungen**.  
  
3.  Wählen Sie die Bereitstellung aus, und klicken Sie auf der Registerkarte **Startseite** auf **Eigenschaften**.  

4.  Klicken Sie im Detailbereich für die Bereitstellung unter **Zugehörige Objekte** auf **Anwendungsverwaltungsrichtlinien**.  

 Weitere Informationen zum Überwachen von Anwendungen finden Sie unter [Überwachen von Anwendungen](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

##  <a name="how-policy-conflicts-are-resolved"></a>Wie Richtlinienkonflikte gelöst werden  
 Wenn bei einer Verwaltungsrichtlinie für mobile Anwendungen bei der ersten Bereitstellung für den Benutzer oder das Gerät ein Konflikt auftritt, wird der jeweilige in Konflikt stehende Einstellungswert aus der Richtlinie für die App entfernt, und die App verwendet einen vorgegebenen Konfliktwert.  

 Wenn bei einer späteren Bereitstellung ein Konflikt in der Verwaltungsrichtlinie für mobile Anwendungen für den Benutzer oder das Gerät auftritt, wird der jeweilige in Konflikt stehende Einstellungswert nicht in der Richtlinie für die App aktualisiert, und die App verwendet den vorhandenen Wert für diese Einstellung.  

 In Fällen, in denen das Gerät oder der Benutzer zwei in Konflikt stehende Richtlinien erhält, gilt Folgendes:  

-   Wenn bereits eine Richtlinie mit dem Gerät bereitgestellt wurde, werden die vorhandenen Richtlinieneinstellungen nicht überschrieben.  

-   Wenn keine Richtlinie für das Gerät bereitgestellt wurde und zwei widersprüchliche Einstellungen bereitgestellt werden, wird die in das Gerät integrierte Standardeinstellung verwendet.  

##  <a name="available-policy-managed-apps"></a>Verfügbare richtlinienverwaltete Apps  
 Eine Liste der richtlinienverwalteten Apps, die für IOS- und Android-Geräte verfügbar sind, finden Sie unter [Microsoft Intune-Anwendungspartner](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune-partners).  



<!--HONumber=Nov16_HO1-->


