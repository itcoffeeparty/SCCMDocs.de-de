---
title: Verwalten von Apps aus dem Microsoft Store für Unternehmen
titleSuffix: Configuration Manager
description: Verwalten Sie Apps aus dem Microsoft Store für Unternehmen, und stellen Sie sie mithilfe von System Center Configuration Manager bereit.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4999784140ece9df49a28063e8660566f7206df0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-system-center-configuration-manager"></a>Verwalten von Apps aus dem Microsoft Store für Unternehmen mit System Center Configuration Manager
Im [Microsoft Store für Unternehmen](https://www.microsoft.com/business-store) können Sie Windows-Apps für Ihre Organisation finden und entweder einzeln oder per Volumenlizenz erwerben. Indem Sie den Store mit Configuration Manager verbinden, können Sie die Liste der erworbenen Apps mit Configuration Manager synchronisieren. Sie können anschließend diese Apps in der Configuration Manager-Konsole anzeigen und sie bereitstellen, wie Sie jede andere App bereitstellen würden.


## <a name="online-and-offline-apps"></a>Online- und Offline-Apps

Der Microsoft Store für Unternehmen unterstützt zwei Typen von Apps:

- **Online** – Dieser Lizenztyp setzt voraus, dass Benutzer und Geräte mit dem Store verbunden sind, um eine App und ihre Lizenz zu erhalten. Windows 10-Geräte müssen in die Azure Active Directory-Domäne eingebunden sein.
- **Offline:** Ermöglicht das Zwischenspeichern von Apps und Lizenzen für die direkte Bereitstellung in Ihrem lokalen Netzwerk. Geräte müssen keine Verbindung mit dem Store oder mit dem Internet herstellen.

[Erfahren Sie mehr](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) über den Microsoft Store für Unternehmen.

Configuration Manager unterstützt das Verwalten von Apps für Microsoft Store für Unternehmen auf Windows 10-Geräten, auf denen der Konfigurations-Manager-Client ausgeführt wird, sowie auf Windows 10-Geräten, die in Microsoft Intune registriert sind. Configuration Manager bietet die folgenden Funktionen für Online- und Offline-Apps.

> [!IMPORTANT]
> Für die Verwendung von Microsoft Store für Unternehmen muss auf einem Windows 10-Gerät das Release von November 2015 (1511) oder höher ausgeführt werden.


|Funktion|Offline-Apps|Online-Apps|
|------------|------------|------------|
|Synchronisieren von App-Daten mit Configuration Manager<br>(Synchronisierung erfolgt alle 24 Stunden)|Ja|Ja|
|Erstellen von Configuration Manager-Anwendungen aus Store-Apps|Ja|Ja|
|Unterstützung für kostenlose Apps aus dem Store|Ja|Ja|
|Unterstützung für kostenpflichtige Apps aus dem Store|Nein|Ja<sup>1</sup>|
|Unterstützen von erforderlichen Bereitstellungen für Benutzer- oder Gerätesammlungen|Ja|Ja|
|Unterstützen von verfügbaren Bereitstellungen für Benutzer- oder Gerätesammlungen|Ja|Ja|
|Unterstützung von branchenspezifischen Apps aus dem Store|Ja|Ja|

<sup>1</sup> Sie müssen Windows 10 Creators Update oder höher ausführen, um online lizenzierte Apps für Windows 10-PCs mit dem Konfigurations-Manager-Client bereitzustellen.

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Bereitstellen von Online-Apps mithilfe von Microsoft Store für Unternehmen mit PCs, die den Configuration Manager-Client ausführen
Vor der Bereitstellung von Microsoft Store für Unternehmen-Apps auf PCs, die den vollständigen Configuration Manager-Client ausführen, ist Folgendes zu beachten:

- Für die vollständige Funktionalität muss auf PCs Windows 10 Creators Update oder höher ausgeführt werden.
- Ein PC muss mit Azure Active Directory im gleichen Mandanten verknüpft sein, in dem Microsoft Store für Unternehmen als Verwaltungstool registriert wurde.
- Wenn PCs mit dem integrierten Administratorkonto angemeldet sind, können sie nicht auf Microsoft Store für Unternehmen-Apps zugreifen.
- PCs benötigen eine aktive Internetverbindung zum Microsoft Store für Unternehmen.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Hinweise für PCs mit früheren Versionen von Windows 10
Auf PCs mit einer früheren Version von Windows 10 als Creators Update (mit dem Configuration Manager-Client) gelten die folgenden Funktionen:


- Wenn die Installation erzwungen wird, entweder vom Benutzer, der die Anwendung installiert, von der Anwendung, die ihren Stichtag für die Installation erreicht, oder durch eine erneute Bewertung nach der Installation für erforderliche Bereitstellungen:
    - Die Anwendung wird durch den Start der Microsoft Store für Unternehmen-App „erzwungen“. 
    - Endbenutzer müssen dann die Installation aus dem Store abschließen, bevor die App installiert wird.
    - In der Configuration Manager-Konsole meldet der Status der Anwendung folgenden Fehler „Die Microsoft Store-App wurde auf dem Client-PC geöffnet und wartet auf den Abschluss der Installation durch den Benutzer.“
- Im nächsten Evaluierungszyklus für die Anwendung:
    - Wenn die Anwendung vom Endbenutzer aus dem Store installiert wurde, meldet die Anwendung den Status **Erfolg**. 
    - Wenn der Endbenutzer nicht versucht hat, die Anwendung aus dem Store zu installieren:
        - Erforderliche Bereitstellungen versuchen, den Store zu starten und die Installation der Anwendung erneut zu erzwingen.
        - Verfügbare Bereitstellungen werden nicht erneut erzwungen.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Weitere Hinweise für PCs mit früheren Versionen von Windows 10:

- Sie können keine branchenspezifischen Apps aus dem Microsoft Store für Unternehmen bereitstellen.
- Wenn Sie kostenpflichtige Apps aus dem Store bereitstellen, müssen Endbenutzer sich im Store anmelden und die App selbst erwerben.
- Wenn Sie eine Gruppenrichtlinie bereitstellen, die den Zugriff auf die Benutzerversion von Microsoft Store deaktiviert, funktionieren Bereitstellungen aus Microsoft Store für Unternehmen nicht, auch wenn Microsoft Store für Unternehmen aktiviert ist.


## <a name="set-up-microsoft-store-for-business-synchronization"></a>Einrichten der Synchronisierung mit Microsoft Store für Unternehmen
Durch das Synchronisieren der Liste der Apps, die von Ihrem Unternehmen erworben wurden, werden Ihnen diese Apps in der Configuration Manager-Konsole angezeigt.

<!-- Remove below after 1802... -->
### <a name="for-configuration-manager-versions-prior-to-1706"></a>Für Versionen des Configuration Manager vor 1706

**Registrieren Sie Configuration Manager als „Webanwendung und/oder Web-API“-Verwaltungstool in Azure Active Directory. Durch diese Aktion erhalten Sie eine Client-ID, die Sie später benötigen.**
1. Wählen Sie im Active Directory-Knoten von [https://manage.windowsazure.com](https://manage.windowsazure.com) Ihr Azure Active Directory aus, und klicken Sie dann auf **Anwendungen** > **Hinzufügen**.
2.  Klicken Sie auf **Eine von meinem Unternehmen entwickelte Anwendung hinzufügen**.
3.  Geben Sie einen Namen für die Anwendung ein, wählen Sie **Webanwendung** und/oder **Web-API** aus, und klicken Sie anschließend auf den Pfeil **Weiter**.
4.  Geben Sie die gleiche URL für die **Registrierungs-URL** und die **App-ID-URI** ein. Dabei kann es sich um eine beliebige URL handeln, die nicht in eine reale Adresse aufgelöst werden muss. Sie können z.B. *https://yourdomain/sccm* eingeben.
5.  Schließen Sie den Assistenten ab.

**Erstellen eines Clientschlüssels für das registrierte Verwaltungstool in Azure Active Directory**
1.  Markieren Sie die Anwendung, die Sie erstellt haben, und klicken Sie auf **Konfigurieren**.
2.  Wählen Sie unter **Schlüssel** eine Dauer aus der Liste aus, und klicken Sie anschließend auf **Speichern**. Diese Aktion erstellt einen neuen Clientschlüssel. Verlassen Sie diese Seite nicht, bevor Sie Microsoft Store für Unternehmen erfolgreich in Configuration Manager eingebunden haben.

**Konfigurieren Sie im Microsoft Store für Unternehmen Configuration Manager als Speicherverwaltungstool**
1.  Öffnen Sie [https://businessstore.microsoft.com/managementtools](https://businessstore.microsoft.com/managementtools), und melden Sie sich an, wenn Sie dazu aufgefordert werden.
2.  Akzeptieren Sie gegebenenfalls die Nutzungsbedingungen.
3.  Klicken Sie unter **Verwaltungstools** auf **Verwaltungstool hinzufügen**.
4.  Geben Sie unter **Tool nach Namen suchen** den Namen der App ein, die Sie zuvor in AAD erstellt haben, und klicken Sie anschließend auf **Hinzufügen**.
5.  Klicken Sie neben der Anwendung, die Sie importiert haben, auf **Aktivieren**.
6.  Wählen Sie auf der Seite **Verwalten > Kontoinformationen** die Option **Offline lizenzierte Apps anzeigen** aus, wenn Sie den Einkauf offline lizenzierter Anwendungen zulassen möchten.

**Hinzufügen des Store-Kontos zu Configuration Manager**

1. Stellen Sie sicher, dass Sie mindestens eine App aus dem Microsoft Store für Unternehmen erworben haben. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Clouddienste**, und klicken Sie dann auf **Microsoft Store für Unternehmen**.
2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Microsoft Store für Unternehmen** auf **Microsoft Store für Unternehmen-Konto hinzufügen**. 
3.  Fügen Sie Mandanten-ID, Client-ID und Clientschlüssel aus Azure Active Directory hinzu, und schließen Sie den Assistenten ab.
4. Sobald Sie fertig sind, wird Ihr Konto unter **Microsoft Store für Unternehmen** in der Configuration Manager-Konsole aufgeführt.

### <a name="for-configuration-manager-version-1706-and-later"></a>Für Versionen des Configuration Manager ab 1706 und höher
<!-- ...remove above after 1802 -->

1. Wechseln Sie in der Konsole zu **Verwaltung** > **Clouddienste** > **Azure-Dienste**, und klicken Sie dann auf **Azure-Dienste konfigurieren**, um den **Assistent für Azure-Dienste** zu starten.
2. Wählen Sie auf der Seite **Azure-Dienste** den Dienst aus, den Sie konfigurieren möchten, und klicken Sie dann auf **Weiter**.
3. Geben Sie auf der Seite **Allgemein** einen Anzeigenamen für den Azure-Dienstnamen und eine optionale Beschreibung ein, und klicken Sie dann auf **Weiter**.
4. Auf der **App** Seite geben Sie Ihre Azure-Umgebung an und klicken dann auf **Durchsuchen**, um das Fenster **Server-App** zu öffnen.
5. Wählen Sie im Fenster **Server App** (Server-App) die Server-App aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**. Server-Apps sind Azure-Web-Apps, die Konfigurationen für Ihr Azure-Konto enthalten, einschließlich Ihrer Mandanten-ID, Client-ID und eines geheimen Schlüssels für Clients. Wenn Sie nicht über eine verfügbare Server-App verfügen, führen Sie eine der folgenden Aktionen durch:
    - **Erstellen**: Um eine neue Server-App zu erstellen, klicken Sie auf **Erstellen**. Geben Sie einen Anzeigenamen für die App und den Mandanten an. Nachdem Sie sich bei Azure angemeldet haben, erstellt Configuration Manager die Web-App für Sie in Azure, einschließlich der Client-ID und des geheimen Schlüssels für den Gebrauch mit der Web-App. Diese Werte können Sie später im Azure-Portal anzeigen.
    - **Importieren**: Um eine Web-App zu verwenden, die in Ihrem Azure-Abonnement bereits vorhanden ist, klicken Sie auf **Importieren**. Geben Sie einen Anzeigenamen für die App und den Mandanten an. Geben Sie dann die Mandanten-ID, die Client-ID und den geheimen Schlüssel für die Azure-Web-App an, die Configuration Manager verwenden soll. Nachdem Sie die Informationen **überprüft** haben, klicken Sie auf **OK**, um fortzufahren. 
6. Überprüfen Sie die Seite **Informationen**, und schließen Sie alle zusätzlichen Schritte und Konfigurationen so wie angegeben ab. Diese Konfigurationen sind erforderlich, um den Dienst mit Configuration Manager zu verwenden. Beispielsweise um den Microsoft Store für Unternehmen zu konfigurieren:
    - In Azure müssen Sie Configuration Manager als Web-Anwendung oder Web-API registrieren und die Client-ID notieren. Außerdem geben Sie einen Clientschlüssel für die Verwendung durch das Verwaltungstool (das ist Configuration Manager) an.
    - Im Portal von Microsoft Store für Unternehmen müssen Sie Configuration Manager als Speicherverwaltungstool angeben, die Unterstützung für offline lizenzierte Apps aktivieren und anschließen mindestens eine App kaufen. 
7. Klicken Sie zum Fortfahren auf **Weiter**.
8. Schließen Sie auf der Seite **App Configurations** (App-Konfigurationen) die Konfigurationen für den App-Katalog und die Sprache für diesen Dienst ab, und klicken Sie dann auf **Weiter**.
9. Nach Abschluss des Assistenten zeigt die Configuration Manager-Konsole, dass Sie **Microsoft Store for Business** als **Clouddiensttyp** konfiguriert haben.




## <a name="create-and-deploy-a-configuration-manager-application-from-a-microsoft-store-for-business-app"></a>Erstellen und Bereitstellen einer Configuration Manager-App aus einer Microsoft Store für Unternehmen-App
Nach der Synchronisierung können Sie Store-Apps genau wie andere Apps erstellen und bereitstellen.

1.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** der Configuration Manager-Konsole den Eintrag **Anwendungsverwaltung**, und klicken Sie anschließend auf **Lizenzinformationen für Store-Apps**.
2.  Wählen Sie zunächst die App aus, die Sie bereitstellen möchten. Klicken Sie anschließend auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Anwendung erstellen**.
Eine Configuration Manager-App wird erstellt, die eine App aus dem Microsoft Store für Unternehmen enthält. Sie können diese App dann wie jede andere Configuration Manager-App bereitstellen und überwachen.

> [!IMPORTANT]
> Bei Geräten, die in Microsoft Intune registriert wurden, stehen bereitgestellte Apps nur für den Benutzer zur Verfügung, der das Gerät ursprünglich registriert hat. Andere Benutzer können nicht auf die App zugreifen.

## <a name="next-steps"></a>Nächste Schritte

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsmanagement**, und klicken Sie anschließend auf **Lizenzinformationen für Store-Apps**.

Sie können die Informationen für jede Store-App anzeigen, die Sie verwalten. Zu diesen Informationen zählen der App-Name, die Plattform, die Anzahl von Lizenzen, die Sie für die App besitzen und die Anzahl von verfügbaren Lizenzen.

Nach der Bereitstellung von Online-Apps stammen sämtliche Updates für diese App direkt von Microsoft Store. Darüber hinaus überprüft Configuration Manager nicht die Versionskompatibilität von Online-Apps, sondern nur, ob Windows die App als installiert meldet.  

Wenn Sie Offline-Apps für Windows 10-Geräte mit dem Konfigurations-Manager-Client bereitstellen, sollten Sie es den Benutzern nicht ermöglichen, Anwendungen über externe Quellen zu aktualisieren, bei denen es sich nicht um Bereitstellungen von Configuration Manager handelt. Die Steuerung der Updates von Offline-Apps ist in Umgebungen mit mehreren Benutzern (z.B. Kursräumen) besonders wichtig. [Gruppenrichtlinien](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy) sind eine Möglichkeit zum Deaktivieren von Microsoft Store. 

Wenn der Administrator von Microsoft Store für Unternehmen eine Offline-App erworben hat, veröffentlichen Sie diese nicht für Benutzer über den Store. Durch diese Konfiguration wird sichergestellt, dass Benutzer die App nicht installieren oder online aktualisieren können. Die Benutzer erhalten ausschließlich Offlineupdates für die App über Configuration Manager. 
