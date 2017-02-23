---
title: "Verwalten von Apps aus dem Windows Store für Unternehmen | Microsoft-Dokumentation"
description: "Verwalten Sie Apps aus dem Windows Store für Unternehmen, und stellen Sie sie mithilfe von System Center Configuration Manager bereit."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f955b5aadfc617e08d5d933dee8e42de838f83c0
ms.openlocfilehash: bf2937f5ba86db19d9cb40e2c98cbb8ba365f7eb

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Verwalten von Apps aus dem Windows Store für Unternehmen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Im [Windows Store für Unternehmen](https://www.microsoft.com/business-store) können Sie Apps für Ihre Organisation suchen, und entweder einzeln oder per Volumenlizenz erwerben. Durch Herstellen einer Verbindung des Store mit Configuration Manager können Sie die Liste der Apps, die Sie erworben haben, mit Configuration Manager synchronisieren, sie in der Configuration Manager-Konsole anzeigen, und wie jede andere App auch bereitstellen.


## <a name="online-and-offline-apps"></a>Online- und Offline-Apps

Der Windows Store für Unternehmen unterstützt zwei Typen von Apps:

- **Online**: Dieser Lizenztyp setzt voraus, dass Benutzer und Geräte mit dem Store verbunden sind, um eine App und ihre Lizenz zu erhalten. Windows 10-Geräte müssen in die Azure Active Directory-Domäne eingebunden sein.
- **Offline**: Organisationen können Apps und Lizenzen zwischenspeichern und sie direkt in ihren lokalen Netzwerken bereitstellen, ohne eine Verbindung zum Store herzustellen bzw. ohne dass eine Internetverbindung nötig ist.

Erfahren Sie mehr über den [Windows Store für Unternehmen](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview).

Configuration Manager unterstützt die Verwaltung von Apps aus dem Windows Store für Unternehmen auf Windows 10-Geräten, auf denen der Configuration Manager-Client ausgeführt wird, und auf Windows 10-Geräten, die bei Microsoft Intune registriert sind (Hybridkonfiguration). Configuration Manager bietet die folgenden Funktionen für Online- und Offline-Apps.

> [!IMPORTANT]
> Um diese Funktionen verwenden zu können, muss auf den Windows 10-Geräten das Release vom November 2015 (1511) oder höher ausgeführt werden.

|Funktion|Offline-Apps|Offline-Apps|
|------------|------------|------------|
|Synchronisieren von App-Daten mit Configuration Manager<br>(Die Synchronisierung findet alle 24 Stunden statt, oder es kann eine sofortige Synchronisierung ausgeführt werden.)|Ja|Ja|
|Erstellen von Configuration Manager-Anwendungen aus Store-Apps|Ja|Ja|
|Unterstützung für kostenlose Apps aus dem Store|Ja|Ja<sup>1</sup>|
|Unterstützung für kostenpflichtige Apps aus dem Store|Nein|Ja<sup>1</sup>|
|Unterstützen von erforderlichen Bereitstellungen für Benutzer- oder Gerätesammlungen|Ja|Ja<sup>1</sup>|
|Unterstützen von verfügbaren Bereitstellungen für Benutzer- oder Gerätesammlungen|Ja<sup>2</sup>|Nein|

<sup>1</sup>Nur von Intune verwaltete Geräte werden unterstützt. Sie können eine Online-Anwendung in der Configuration Manager-Konsole erstellen und auf einem Gerät bereitstellen, das durch den Configuration Manager-Client verwaltet wird, allerdings funktioniert dieser Vorgang nicht. Ihre Benutzer werden auf die entsprechende Seite im App Store weitergeleitet, um die App dort manuell zu installieren.

<sup>2</sup>Nur Geräte werden unterstützt, die mit dem Configuration Manager-Client verwaltet werden.

<!--- ## Activate the Windows Store for Business capability
Because this is a pre-release feature, before you can connect Configuration Manager to the Windows Store for Business, you must take the following steps:

**Give your consent to use pre-release features**
1. In the **Administration** workspace of the Configuration Manager console, choose **Site Configuration** > **Sites**.
2. Select the top-level site in your hierarchy, then, open **Hierarchy Settings**.
3. In the **Hierarchy Settings Properties** dialog box, check the box, **Consent to use Pre-Release** features.
4. Choose **OK**.

**Activate the Windows Store for Business capability**
1. In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Features**.
2. Select **Windows Store for Business Integration**, and then in the **Home** tab, in the **Features** group, choose **Turn on**.
3. Close and re-open the Configuration Manager console.
4. You'll now see the node **Windows Store for Business** in the **Administration** workspace under **Cloud Services**. --->

## <a name="set-up-windows-store-for-business-synchronization"></a>Einrichten der Synchronisierung mit Windows Store für Unternehmen

> [!IMPORTANT]
> Wenn Sie eine Verbindung zwischen Configuration Manager und dem Windows Store für Unternehmen herstellen, müssen Sie einen Ordner angeben, in dem App-Inhalte, die aus dem Store synchronisiert werden, gespeichert werden.
Um sicherzustellen, dass es sich um einen sicheren Ordner handelt, und dass der Inhalt auf Geräten bereitgestellt werden kann, müssen Sie sichergehen, dass die folgenden Berechtigungen vorhanden sind:
-    Der Computer, auf dem Sie die Standortsystemrolle „Dienstverbindungspunkt“ installieren (der Standort der obersten Ebene in der Hierarchie), muss über Lese- und Schreibberechtigungen für den Ordner verfügen, den Sie bei der Verwendung des Kontos **Computer$** angegeben haben.
-    Der Autor der App muss über Leseberechtigungen für den angegebenen Ordner verfügen.
-    Das Konto **Computer$** jedes Computers, der eine Instanz des SMS-Anbieters hostet, muss den angegebenen Ordner verwenden können.


Registrieren Sie Configuration Manager über Webanwendung oder Web-API als Verwaltungstool in Azure Active Directory. Sie erhalten eine Client-ID, die Sie später benötigen.
1. Wählen Sie im Active Directory-Knoten [https://manage.windowsazure.com](https://manage.windowsazure.com) Ihr Azure Active Directory aus, und wählen Sie anschließend **Anwendungen** > **Hinzufügen** aus.
2.  Wählen Sie **Eine von meinem Unternehmen entwickelte Anwendung hinzufügen** aus.
3.  Geben Sie einen Namen für die Anwendung ein, wählen Sie **Webanwendung** und/oder **Web-API** und anschließend **Weiter** aus.
4.  Geben Sie die gleiche URL für die **Registrierungs-URL** und die **App-ID-URI** ein. Dabei kann es sich um eine beliebige URL handeln, die nicht in eine reale Adresse aufgelöst werden muss. Sie können z.B. *https://yourdomain/sccm* eingeben.
5.  Beenden Sie den Assistenten.

Erstellen Sie in Azure Active Directory einen Clientschlüssel für das registrierte Verwaltungstool.
1.  Markieren Sie die Anwendung, die Sie soeben erstellt haben, und wählen Sie **Konfigurieren** aus.
2.  Wählen Sie unter **Schlüssel** eine Dauer aus der Liste und anschließend **Speichern** aus. Dadurch wird ein neuer Clientschlüssel erstellt. Verlassen Sie diese Seite nicht, bevor Sie Windows Store für Unternehmen erfolgreich in Configuration Manager eingebunden haben.

Konfigurieren Sie im Windows Store für Unternehmen Configuration Manager als Speicherverwaltungstool.
1.  Öffnen Sie [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools), und melden Sie sich nach entsprechender Aufforderung an.
2.  Akzeptieren Sie gegebenenfalls die Nutzungsbedingungen.
3.  Klicken Sie unter **Management Tools** (Verwaltungstools) auf **Add a management tool** (Verwaltungstool hinzufügen).
4.  Geben Sie unter **Search for the tool by name** (Tool nach Namen suchen) den Namen der App ein, die Sie zuvor in Azure Active Directory erstellt haben, und wählen Sie anschließend **Hinzufügen** aus.
5.  Wählen Sie neben der Anwendung, die Sie gerade importiert haben, **Aktivieren** aus.
6.  Wählen Sie auf der Seite **Manage > Account Information** (Verwalten > Kontoinformationen) die Option **Show Offline-Licensed Apps** (Offline lizenzierte Apps anzeigen) aus, wenn Sie den Einkauf offline lizenzierter Anwendungen zulassen möchten.

> [!Note]
> Wenn Sie zur Bereitstellung von Windows Store für Business-Apps mehrere Verwaltungstools verwenden, konnten Sie zuvor nur eines dieser Tools dem Windows Store für Business-Apps zuordnen. Sie können dem Store jetzt mehrere Verwaltungstools zuordnen, z. B. Intune und Configuration Manager.

Fügen Sie das Store-Konto zu Configuration Manager hinzu.

1. Stellen Sie sicher, dass Sie mindestens eine App aus dem Windows Store für Unternehmen gekauft haben. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Cloud Services**, und wählen Sie dann **Windows Store für Unternehmen** aus.
2.  Wählen Sie auf der Registerkarte **Start** in der Gruppe **Windows Store für Unternehmen** **Add Windows Store for Business Account** (Windows Store für Unternehmen-Konto hinzufügen) aus.
3.  Fügen Sie die Mandanten-ID, Client-ID und den geheimen Clientschlüssel aus Azure Active Directory hinzu, und schließen Sie den Assistenten ab.
4. Sobald Sie fertig sind, wird das von Ihnen eingerichtete Konto in der Liste **Windows Store für Unternehmen** der Configuration Manager-Konsole aufgeführt.

Ändern Sie die App-Sprachen, die Benutzern im Anwendungskatalog zum Herunterladen angezeigt werden.

1.    Klicken Sie im Arbeitsbereich **Verwaltung** der Configuration Manager-Konsole auf **Cloud Services** > **Updates und Wartung** > **Windows Store für Unternehmen**.
2.    Wählen Sie Ihr Windows Store für Unternehmen-Konto und anschließend **Eigenschaften** aus.
3.    Wählen Sie die Registerkarte **Sprache** aus.
4.    Fügen Sie die Sprachen hinzu, die im Anwendungskatalog angezeigt werden sollen, oder entfernen Sie sie. Wählen Sie die Standardsprache des Anwendungskatalogs aus, die den Benutzern zur Verfügung gestellt wird.

>[!IMPORTANT]
>Wenn Sie die Sprachen ändern, die synchronisiert werden, müssen Sie in diesem Release den SMS-Executive-Dienst auf dem Standortserver neu starten, bevor die Spracheinstellungen wirksam werden.


Ändern Sie den geheimen Clientschlüssels aus Azure Active Directory.

1.    Klicken Sie im Arbeitsbereich **Verwaltung** der Configuration Manager-Konsole auf **Cloud Services** > **Updates und Wartung** > **Windows Store für Unternehmen**.
2.    Wählen Sie Ihr Windows Store für Unternehmen-Konto und anschließend **Eigenschaften** aus.
3.    Geben Sie im Dialogfeld **Windows Store for Business Account Properties** (Windows Store für Unternehmen-Kontoeigenschaften) einen neuen Schlüssel in das Feld **Client secret key** (Geheimer Clientschlüssel) ein, und wählen Sie anschließend **Überprüfen** aus. Sobald die Überprüfung abgeschlossen ist, wählen Sie **Übernehmen** aus, und schließen Sie dann das Dialogfeld.

## <a name="sync-apps-from-the-store-with-configuration-manager"></a>Synchronisieren von Apps aus dem Store mit Configuration Manager

Die Synchronisierung findet alle 24 Stunden statt, oder es kann eine sofortige Synchronisierung mithilfe dieses Vorgangs ausgeführt werden:

1. Klicken Sie im Arbeitsbereich **Verwaltung** der Configuration Manager-Konsole auf **Cloud Services** > **Updates und Wartung** > **Windows Store für Unternehmen**.
3.    Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Synchronisieren** auf **Jetzt synchronisieren**.
4.    Die App, die Sie erworben haben, wird im Knoten **License Information for Store Apps** (Lizenzinformationen für Store-Apps) des Arbeitsbereichs **Anwendungsverwaltung** angezeigt.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Erstellen und Bereitstellen einer Configuration Manager-Anwendung aus einer App aus dem Windows Store für Unternehmen

Bei dieser Vorgehensweise wird davon ausgegangen, dass Sie mindestens eine kostenlose App oder mindestens eine kostenpflichtige online-lizenzierte App aus dem Windows Store für Unternehmen erworben haben.

1.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** der Configuration Manager-Konsole **Anwendungsmanagement**, und wählen Sie anschließend **License Information for Store Apps** (Lizenzinformationen für Store-Apps) aus.
2.  Wählen Sie zunächst die App aus, die Sie bereitstellen möchten. Wählen Sie anschließend auf der Registerkarte **Start** in der Gruppe **Erstellen** **Anwendung erstellen** aus.
Eine Configuration Manager-App wird erstellt, die eine App aus dem Windows Store für Unternehmen enthält. Sie können diese Anwendung wie jede andere Configuration Manager-Anwendung bereitstellen und überwachen.

> [!IMPORTANT]
> Für Geräte, die bei Intune registriert sind, stehen bereitgestellte Apps nur für diejenigen Benutzer zur Verfügung, die sie ursprünglich registriert haben. Andere Benutzer können die App nicht verwenden.

## <a name="monitor-windows-store-for-business-apps"></a>Überwachen von Apps aus dem Windows Store für Unternehmen

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsmanagement**, und wählen Sie anschließend **License Information for Store Apps** (Lizenzinformationen für Store-Apps) aus.

Sie können für jede von Ihnen verwaltete Store-App Informationen anzeigen, wie den Namen, die Plattform, die Anzahl der Lizenzen, die Sie für diese App besitzen, sowie die Anzahl der Lizenzen, die Ihnen zur Verfügung stehen.



<!--HONumber=Feb17_HO3-->


