---
title: "Neuigkeiten bei der hybriden Verwaltung mobiler Geräte mit Configuration Manager | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über die neuen Funktionen der Verwaltung mobiler Geräte, die für Hybridbereitstellungen mit Configuration Manager und Intune verfügbar sind."
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 94dc0335dab74bec7989753343418fae49b3ebe9
ms.openlocfilehash: ab011cb06b43b06fc6e2a89e2f413d35a541a111
ms.contentlocale: de-de
ms.lasthandoff: 07/14/2017

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Neuheiten bei der hybriden Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieser Artikel bietet Details zu den neuen Features für die Verwaltung mobiler Geräte (MDM), die für Hybridbereitstellungen mit System Center Configuration Manager und Intune verfügbar sind.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Kompatibilität mit Configuration Manager-Versionen  

 Jeder Abschnitt dieses Artikels listet Hybridfeatures in drei verschiedenen Kategorien auf. Verwenden Sie die folgenden Anleitungen, um die Kompatibilität der Features in jeder Kategorie mit verschiedenen Versionen von Configuration Manager zu bestimmen:  

|Featurekategorien|Beschreibung|
|-|-|
|**Neuheiten in Microsoft Intune** | Im Allgemeinen sollten alle in dieser Kategorie aufgelisteten Features in allen Configuration Manager-Releases, einschließlich Configuration Manager-Releases von System Center 2012 R2, verwendet werden können, da für diese Features nur der Intune-Dienst, aber keine zusätzlichen Funktionen in Configuration Manager erforderlich sind.|
|**Neuheiten in Configuration Manager Technical Preview**| Alle in dieser Kategorie aufgelisteten Features können nur mit dem angegebenen Technical Preview-Release verwendet werden. Um diese Features zu testen, müssen Sie die in der Featurebeschreibung angegebene Technical Preview-Version installieren. Weitere Informationen finden Sie unter [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Neuheiten in Configuration Manager (Current Branch)**| Alle in dieser Kategorie aufgelisteten Features können nur mit der angegebenen Version von Configuration Manager (Current Branch) verwendet werden, z.B. Version 1511 oder 1602. Wenn Sie eine ältere Version von Configuration Manager für die Hybridbereitstellung verwenden, müssen Sie ein Upgrade auf die in der Featurebeschreibung angegebene Configuration Manager-Version (Current Branch) ausführen. Weitere Informationen finden Sie unter [Upgrade auf System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|

## <a name="july-2017"></a>Juli 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Hinweise zum Ende des Supports für Android und Windows Phone hinzugefügt**

    Es wurden neue Hinweise zum Ende des Supports für Android- und Windows Phone-Versionen hinzugefügt. Details finden Sie unter [Hinweise](#notices).

## <a name="june-2017"></a>Juni 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Umstellen der MDM-Autorität**

  Ab Configuration Manager, Version 1610, und Microsoft Intune, Version 1705, können Sie Ihre MDM-Autorität ohne Unterstützung durch den Microsoft-Support und ohne Aufheben der Registrierung und erneutes Registrieren Ihrer vorhandenen verwalteten Geräte umstellen. Einzelheiten finden Sie unter [Umstellen der MDM-Autorität]( /sccm/mdm/deploy-use/change-mdm-authority).

- **Managed Browser- und App-Proxyintegration**

  Der Intune Managed Browser lässt sich jetzt in den Azure AD-Anwendungsproxydienst integrieren, damit Benutzer auf interne Websites zugreifen können, selbst wenn sie remote arbeiten. Benutzer des Browsers geben einfach wie gewohnt die Website-URL ein, und der Managed Browser leitet die Anfrage über das Anwendungsproxy-Webgateway weiter. Weitere Informationen finden Sie unter [Verwalten des Internetzugriffs mittels Richtlinien für Managed Browser](/intune/app-configuration-managed-browser).

- **Die Unternehmensportal-App für Android bietet nun eine neue Benutzeroberfläche für App-Schutzrichtlinien**

  Als Reaktion auf das Feedback von Kunden haben wir die Unternehmensportal-App für Android durch Hinzufügen der Schaltfläche **Auf Unternehmensinhalte zugreifen** geändert. Dies soll verhindern, dass Endbenutzer unnötigerweise den Registrierungsprozess durchlaufen, wenn sie lediglich auf Apps zugreifen müssen, die App-Schutzrichtlinien unterstützen, ein Feature zur Verwaltung mobiler Anwendungen durch Intune. Diese Änderungen werden auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](/intune/whats-new-app-ui) beschrieben.

- **Neue Menüaktion zum einfachen Entfernen des Unternehmensportals**

  Als Reaktion auf Benutzerfeedback wurde der Unternehmensportal-App für Android eine neue Menüaktion hinzugefügt, über die das Entfernen des Unternehmensportals von Ihrem Gerät eingeleitet wird. Über diese Aktion wird das Gerät aus der Intune-Verwaltung entfernt, damit die App vom Benutzer vom Gerät entfernt werden kann. Diese Änderungen werden auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](/intune/whats-new-app-ui) und in der [Android-Endbenutzerdokumentation](/intune-user-help/unenroll-your-device-from-intune-android) beschrieben.

- **Verbesserungen bei der App-Synchronisierung mit Windows 10 Creators Update**

  Die Unternehmensportal-App für Windows 10 löst jetzt automatisch eine Synchronisierung für App-Installationsanforderungen für Geräte mit Windows 10 Creators Update (Version 1703) aus. Dies reduziert das Problem, dass App-Installationen im Status „Synchronisierung ausstehend“ stecken bleiben. Darüber hinaus können Benutzer in der App manuell eine Synchronisierung auslösen. Diese Änderungen werden auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](/intune/whats-new-app-ui) beschrieben.

- **Neues benutzerfreundlicheres Windows 10-Unternehmensportal**

  Die Unternehmensportal-App für Windows 10 bietet eine exemplarische Vorgehensweise für Intune für Geräte, die nicht identifiziert oder registriert wurden. Die neue Anleitung umfasst Schritt-für-Schritt-Anweisungen, mit denen die Registrierung bei Azure Active Directory (erforderlich für Funktionen zum bedingten Zugriff) und die MDM-Registrierung (erforderlich für Funktionen zur Geräteverwaltung) durch den Benutzer erläutert werden. Auf die geführte Anleitung kann über die Hauptseite des Unternehmensportals zugegriffen werden. Benutzer können die App weiterhin verwenden, wenn die Registrierung und Anmeldung nicht abgeschlossen werden, haben jedoch lediglich Zugriff auf einen eingeschränkten Funktionsumfang.

  Dieses Update ist nur auf Geräten unter Windows 10 Anniversary Update (Build 1607) oder höher sichtbar. Diese Änderungen werden auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](/intune/whats-new-app-ui) beschrieben.

- **Verbesserungen an den App-Kacheln in der Unternehmensportal-App für iOS**

  Wir haben das Design der App-Kacheln auf der Startseite entsprechend der Brandingfarbe geändert, die Sie für das Unternehmensportal festlegen. Weitere Informationen finden Sie auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](/intune/whats-new-app-ui).

- **Kontoauswahl nun in der Unternehmensportal-App für iOS verfügbar**

  Benutzer von iOS-Geräten wird bei der Anmeldung am Unternehmensportal möglicherweise unsere neue Kontoauswahl angezeigt, wenn sie sich bei anderen Microsoft-Apps mit ihrem Geschäfts-, Schul- oder Unikonto anmelden. Weitere Informationen finden Sie auf der Seite mit den [Neuerungen auf der App-Benutzeroberfläche](/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Neuerungen in Configuration Manager Technical Preview 1706

- **Neue Richtlinieneinstellungen für die Verwaltung mobiler Anwendungen**    

  Die folgenden Richtlinieneinstellungen für die Verwaltung mobiler Anwendungen (Mobile Application Management, MAM) sind jetzt verfügbar:

  - **Bildschirmaufnahme blockieren (Nur Android-Geräte):** Gibt an, dass die Bildschirmaufnahmefunktionen des Geräts blockiert werden, wenn Sie diese App verwenden.
  - **Kontaktsynchronisierung deaktivieren:** Verhindert, dass die App Daten in der nativen App „Kontakte“ auf dem Gerät speichert.
  - **Drucken deaktivieren:** Verhindert, dass die App Geschäfts-, Schul- oder Unidaten druckt.

  Unter [Schützen von Apps mithilfe von App-Schutzrichtlinien in Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) finden Sie Informationen zu den neuen Richtlinieneinstellungen zum Schutz von Apps.

- **Neue Einstellungen für Windows-Konfigurationselemente**  <!-- 1354715 -->    

  Neue Windows-Konfigurationselemente sind verfügbar für die Einstellungskategorien Kennwort, Gerät, Speicher und Microsoft Edge. Weitere Informationen finden Sie unter [Neue Einstellungen für Windows-Konfigurationselemente](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).

- **Neue Konformitätsrichtlinienregeln für Geräte**    

  Sie können jetzt neue Optionen für Konformitätsrichtlinien konfigurieren, die zuvor nur in der eigenständigen Intune-Version verfügbar waren. Einzelheiten finden Sie unter [Verbesserungen bei Gerätekonformitätsrichtlinien](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Registrierungseinschränkungen bei Android und iOS** <!-- 1290826 -->      

  Administratoren können nun angeben, dass Benutzer private Android- oder iOS-Geräte nicht in ihrer Hybridumgebung registrieren können. Dies ermöglicht das Begrenzen registrierter Geräte auf vorab festgelegte unternehmenseigene Geräte bzw. auf iOS-Geräte, die ausschließlich mit dem Programm zur Geräteregistrierung registriert werden. Einzelheiten finden Sie unter [Registrierungseinschränkungen bei Android und iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).

- **Unterstützung für Entrust-Zertifizierungsstellen** <!-- 1350740 -->     

  Configuration Manager unterstützt jetzt Entrust-Zertifizierungsstellen. Dadurch können PFX-Zertifikate an Geräte übermittelt werden, die bei Microsoft Intune registriert sind.    

  Sie können Entrust als Zertifizierungsstelle konfigurieren, wenn Sie in Configuration Manager die Rolle „Zertifikatregistrierungspunkt“ hinzufügen. Beim Hinzufügen eines neuen Zertifikatprofils, das PFX-Zertifikate ausstellt, können Sie entweder eine Microsoft- oder Entrust-Zertifizierungsstelle auswählen.

  **Bekanntes Problem**: In der Technical Preview 1706 werden für Microsoft-Zertifizierungsstellen keine PFX-Zertifikate ausgestellt. Dies wirkt sich nicht auf importierte PFX-Zertifikate oder SCEP-Profile aus.

- **Cisco (IPsec)-Unterstützung für macOS-VPN-Profile**  <!-- 1321367 -->    

  Sie können ein macOS-VPN-Profil mit Cisco (IPsec) als Verbindungstyp erstellen. Weitere Informationen finden Sie unter [Erstellen von VPN-Profilen](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="april-2017"></a>April 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **„Meine Apps“ für Managed Browser verfügbar**

  „Meine Apps“ von Microsoft verfügt jetzt über eine bessere Unterstützung innerhalb von Managed Browser. Managed Browser-Benutzer, die keine Verwaltungsaufgaben ausführen müssen, gelangen direkt zum Dienst „Meine Apps“, wo sie auf die von ihrem Administrator bereitgestellten SaaS-Apps zugreifen können. Benutzer, die Verwaltungsaufgaben in Intune ausführen sollen, können weiterhin über das integrierte Managed Browser-Lesezeichen auf „Meine Apps“ zugreifen.

- **Neue Symbole für Managed Browser und das Unternehmensportal**

  Die Managed Browser-Symbole für die Android- und iOS-Versionen der App werden aktualisiert. Das neue Symbol enthält den aktualisierten Intune-Badge, damit es konsistenter mit anderen Apps in Enterprise Mobility + Security (EM+S) wird. Sie können das neue Symbol für Managed Browser auf der Seite [Aktualisierungen für die Benutzeroberfläche für Endbenutzer-Apps in Intune](/intune/whats-new/whats-new-in-intune-app-ui.md) finden.

  Das Unternehmensportal erhält auch aktualisierte Symbole für die Android-, iOS- und Windows-Versionen der App, um die Konsistenz mit anderen Apps in EM+S zu verbessern. Diese Symbole werden schrittweise von April bis Ende Mai auf den einzelnen Plattformen veröffentlicht.

- **Anmeldungsstatusanzeige im Android-Unternehmensportal**

  Ein Update der Android-Unternehmensportal-App zeigt eine Statusanzeige für den Anmeldevorgang an, wenn der Benutzer die App startet oder fortsetzt. Die Statusanzeige durchläuft die neuen Phasen, beginnend mit „Verbindung wird aufgebaut“, „Anmeldung“ und dann „Suchen nach Sicherheitsanforderungen“, bevor dem Benutzer der Zugriff auf die App gewährt wird. Die neuen Bildschirme für die Unternehmensportal-App für Android finden Sie auf der Seite [Neuigkeiten in der Benutzeroberfläche der Intune-App](/intune/whats-new/whats-new-in-intune-app-ui.md).

- **Verhindern, dass Apps auf SharePoint Online zugreifen**

  Sie können jetzt eine Richtlinie für den App-basierten bedingten Zugriff erstellen, um Apps, auf die keine Schutzrichtlinien angewendet wurden, am Zugriff auf [SharePoint Online](/InTune/deploy-use/mam-ca-for-sharepoint-online) zu hindern. Im Szenario des App-basierten bedingten Zugriffs können Sie Apps festlegen, die über das Azure-Portal auf SharePoint Online zugreifen können sollen.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Neuheiten in Configuration Manager Technical Preview 1704

- **Konfigurieren von Android-Apps mit Konfigurationsrichtlinien für Apps**

  Sie können Konfigurationsrichtlinien für Apps in System Center Configuration Manager (Configuration Manager) verwenden, um vorkonfigurierte Einstellungen bereitzustellen, wenn ein Benutzer eine App auf Android for Work-Geräten ausführt. Konfigurationsrichtlinien für Android-Apps stehen nur auf Geräten zur Verfügung, die Android for Work ausführen, und gelten für genehmigte Apps aus dem Play for Work-Store. Informationen zum Testen dieses Features finden Sie unter [Konfigurieren von Android-Apps mit Konfigurationsrichtlinien für Apps](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).

## <a name="march-2017"></a>März 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Neue Benutzeroberfläche für die Unternehmensportal-App für Android**

  Die Benutzeroberfläche der Unternehmensportal-App für Android hat nun ein moderneres Design. Die wichtigen Updates sind:

  - Farben: Die IT-Abteilung kann die Färbung der Kopfzeilen der Registerkarte „Unternehmensportal“ dem Branding gemäß festlegen.
  - Apps: Auf der Registerkarte **Apps** wurden die Schaltflächen **Empfohlene Apps** und **Alle Apps** aktualisiert.
  - Suche: Auf der Registerkarte **Apps** ist die Schaltfläche **Suche** nun eine unverankerte interaktive Schaltfläche.
  - Navigation in Apps: Die Ansicht **Alle Apps** enthält die Registerkartenansicht **Featured** (Highlights), **Alle** und **Kategorien**, um die Navigation zu vereinfachen.
  - Unterstützung: Die Registerkarten **Meine Geräte** und **An IT wenden** werden aktualisiert, um die Lesbarkeit zu verbessern.

  Weitere Informationen zu diesen Änderungen finden Sie unter [UI updates for Intune end user apps](/intune/whats-new/whats-new-in-intune-app-ui) (Aktualisierungen der Benutzeroberfläche der Intune-Apps für Endbenutzer).

- **Signierungsskript für das Windows 10-Unternehmensportal**

  Wenn Sie die Windows 10-Unternehmensportal-App herunterladen und querladen müssen, können Sie nun ein Skript verwenden, um den App-Signierungsprozess für Ihre Organisation zu vereinfachen und zu optimieren.  Unter [Microsoft Intune Signing Script for Windows 10 Company Portal (Microsoft Intune-Signierungsskript für das Windows 10-Unternehmensportal)](https://aka.ms/win10cpscript) in der TechNet Gallery können Sie das Skript sowie die Anweisungen zu dessen Verwendung herunterladen. Weitere Informationen zu dieser Ankündigung finden Sie unter [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) (Aktualisieren Ihrer Windows 10-Unternehmensportal-App) im Blog des Intune-Supportteams.

- **Verbesserte Unterstützung für Android-Benutzer in China**

  Da der Google Play Store in China nicht zur Verfügung steht, müssen Apps für Android-Geräte von chinesischen Marketplaces abgerufen werden. Das Unternehmensportal unterstützt diesen Workflow, indem Android-Benutzer in China umgeleitet werden, um die Unternehmensportal- und Outlook-Apps aus lokalen App Stores herunterzuladen. Dies verbessert die Benutzerfreundlichkeit, wenn Richtlinien für den bedingten Zugriff sowohl für die Verwaltung mobiler Geräte als auch für die Verwaltung mobiler Anwendungen aktiviert sind. Die Unternehmensportal- und Outlook-Apps für Android sind in den folgenden chinesischen App Stores verfügbar:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Sicherstellen, dass Ihre Unternehmensportal-Apps auf dem neuesten Stand sind**

  Im Dezember 2016 haben wir ein Update veröffentlicht, das die Erzwingung für die mehrstufige Authentifizierung für eine Gruppe von Benutzern ermöglicht, wenn diese ein Gerät registrieren, auf dem iOS, Android oder Windows bzw. Windows Phone in einer höheren Version als 8.1 installiert ist. Dies funktioniert nicht ohne bestimmte Baselineversionen der Unternehmensportal-App für Android (v5.0.3419.0+) und iOS (v2.1.17+).

  Die Verwaltungsfunktionen von Intune werden kontinuierlich verbessert, und viele Verbesserungen enthalten koordinierte Updates für die Unternehmensportal-Apps auf allen unterstützten Plattformen. Daher wird empfohlen, dass Sie immer die neuesten Versionen der Unternehmensportal-Apps auf Geräten installiert haben, um die Verbesserungen in Intune zu nutzen und die bestmögliche Benutzerfreundlichkeit zu gewährleisten.

  >[!Tip]
  > Verlangen Sie von Ihren Benutzern, dass sie auf ihren Geräten die automatische App-Aktualisierung über den entsprechenden App Store aktiviert ist. Wenn Sie die Android-Unternehmensportal-App auf einer Netzwerkfreigabe bereitgestellt haben, können Sie die neueste Version aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49140) herunterladen.

- **Microsoft Teams ist nun für MAM unter iOS und Android aktiviert**

  Die Microsoft Teams-Apps für iOS und Android sind nun für die Funktionen der Verwaltung mobiler Apps (MAM) von Intune aktiviert, sodass Sie Ihren Teams ermöglichen können, frei über Geräte hinweg zu arbeiten, wobei sichergestellt wird, dass Konversationen und Unternehmensdaten jederzeit geschützt werden. Weitere Informationen finden Sie in der [Microsoft Teams-Ankündigung](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) im Enterprise Mobility and Security-Blog.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Neuheiten in Configuration Manager Technical Preview 1703

- **Zusätzliche Unterstützung für Apple Volume Purchase Program-Szenarios**

   Ab Technical Preview 1703 verfügen Sie nun über Unterstützung für die folgenden Volume Purchase Program-Szenarios (VPP):

   - Gerätelizenzierung: Apps, die die Gerätelizenzierung unterstützen und auf Gerätesammlungen bereitgestellt werden, benötigen jetzt nur eine Lizenz pro Gerät.  Zuvor mussten Sie eine Lizenz für jeden Benutzer auf einem Gerät verwenden. Weitere Informationen finden Sie unter [Bereitstellen per Volumenlizenz erworbener iOS-Apps in Gerätesammlungen](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Verwendung von mehreren VPP-Token für einen einzelnen Hybrid-Mandanten, wobei beide Token für die Verwaltung von VPP-Apps verwendet werden.
   - Verwendung von VPP Education-Token mit der Möglichkeit zur Unterscheidung zwischen Unternehmens- und Education-Token.

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Die folgenden Features, die zuvor in Configuration Manager Technical Preview-Releases verfügbar waren, stehen nun in Hybridbereitstellungen mit Intune und Configuration Manager (Current Branch) Version 1702 zur Verfügung.

- [Unterstützung für Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Kompatibilitätseinstellungen für nicht kompatible Apps](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [PFX-Zertifikat-Erstellung und -Verteilung und S/MIME-Unterstützung](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [Android- und iOS-Versionen werden nicht mehr über den Erstellungsassistenten für hybrides MDM erreicht](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Die folgenden zusätzlichen Hybridfeatures sind auch in Version 1702 von Configuration Manager (Current Branch) enthalten:

- **Verbesserter Support für Apple Volume Purchase Program (VPP)**

  - Sie können jetzt sowohl Geräten als auch Benutzern lizenzierte Apps bereitstellen. Je nachdem, inwieweit die App Gerätelizenzierungen unterstützt, wird eine entsprechende Lizenz wie folgt beansprucht:

    | Configuration Manager-Version | Unterstützt die App Gerätelizenzierung? | Typ der Bereitstellungssammlung | Beanspruchte Lizenz |
    |-|-|-|-|
    |Früher als 1702|Ja|Benutzer|Benutzerlizenz|
    |Früher als 1702|Nein|Benutzer|Benutzerlizenz|
    |Früher als 1702|Ja|Gerät|Benutzerlizenz|
    |Früher als 1702|Nein|Gerät|Benutzerlizenz|
    |1702 und höher|Ja|Benutzer|Benutzerlizenz|
    |1702 und höher|Nein|Benutzer|Benutzerlizenz|
    |1702 und höher|Ja|Gerät|Gerätelizenz|
    |1702 und höher|Nein|Gerät|Benutzerlizenz|

  - Außerdem können Sie Apps bereitstellen und nachverfolgen, die Sie in iOS Volume Purchase Program für Bildungseinrichtungen erworben haben.

  - Sie können Configuration Manager jetzt mehrere Apple VPP-Tokens zuordnen.

  Weitere Informationen zu iOS-Apps, die über ein Volumenprogramm erworben wurden, finden Sie unter [Verwalten von iOS-Apps, die über ein Volumenprogramm erworben wurden](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Support für branchenspezifische Apps im Windows Store für Unternehmen**

  Sie können jetzt benutzerdefinierte branchenspezifische Apps aus dem Windows Store für Unternehmen synchronisieren.

- **Neue Überwachungstools für Mobile Threat Defense**

    Sie haben nun neue Möglichkeiten, den Kompatibilitätsstatus mit Ihrem Dienstanbieter für Mobile Threat Defense zu überwachen.

    Weitere Informationen finden Sie unter [How to monitor Mobile Threat Defense compliance (Überwachen der Kompatibilität von Mobile Threat Defense)](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="february-2017"></a>Februar 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Modernisieren der Unternehmensportal-Website**

  Die Unternehmensportal-Website unterstützt Apps, die für Benutzer ausgelegt sind, die nicht über verwaltete Geräte verfügen. Die Website richtet sich nach anderen Microsoft-Produkten und Diensten, indem sie ein neues kontrastreiches Farbschema, dynamische Illustrationen und ein „Hamburger-Menü“ verwendet, das Helpdesk-Kontaktinformationen und Informationen zu vorhandenen verwalteten Geräte enthält. Die Zielseite wird neu angeordnet, um für Benutzer verfügbare Apps mit Karussellsteuerelementen für unterstützte und vor kurzem aktualisierte Apps hervorzuheben. Vorher-Nachher-Bilder sind auf der Seite [UI-Updates](/intune/whats-new/whats-new-in-intune-app-ui) verfügbar.

- **Neue MDM-Serveradresse für Windows-Geräte**

  Die MDM-Serveradresse für die Registrierung von Windows- und Windows Phone-Geräten wurde von „manage.microsoft.com“ in „enrollment.manage.microsoft.com“ geändert. Benachrichtigen Sie Ihre Benutzer, dass „enrollment.manage.microsoft.com“ als Adresse des MDM-Servers verwendet werden soll, wenn sie bei der Registrierung eines Windows- oder und Windows Phone-Geräts zur Eingabe der Adresse aufgefordert werden. Dieses Update erfordert zudem, dass jeder CNAME-Eintrag im DNS, der von „EnterpriseEnrollment.contoso.com“ zu „manage.microsoft.com“ umleitet, durch einen CNAME-Eintrag im DNS ersetzt wird, der von „EnterpriseEnrollment.contoso.com“ zu „EnterpriseEnrollment-s.manage.microsoft.com“ umleitet. Weitere Informationen zu dieser Änderung finden Sie unter „http://aka.ms/intuneenrollsvrchange“.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Neuheiten in Configuration Manager Technical Preview 1702

- **Unterstützung für Android for Work**

  Sie können nun Android-Geräte mithilfe von Android for Work in hybriden MDM-Umgebungen mithilfe von Configuration Manager Technical Preview 1702 verwalten. Unterstützte Android-Geräte können jetzt als Android for Work-Geräte angemeldet werden, wodurch ein Arbeitsprofil auf dem Gerät erstellt wird, an das in Play for Work genehmigte Apps bereitgestellt werden können. Sie können auch Konfigurationselemente, Kompatibilitätsrichtlinien und Ressourcenzugriffsprofile für diese Geräte konfigurieren und bereitstellen. Weitere Informationen finden Sie unter [Unterstützung für Android for Work](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Kompatibilitätseinstellungen für nicht kompatible Apps**

  Sie können jetzt Regeln für nicht kompatible Apps für Android- und iOS-Apps in Kompatibilitätsrichtlinien erstellen. Geräte, auf denen die angegebenen Anwendungen installiert sind, werden als „nicht kompatibel“ gekennzeichnet und verlieren den Zugriff auf Unternehmensressourcen gemäß den geltenden Richtlinien für bedingten Zugriff. Weitere Informationen finden Sie unter [Verbesserungen bei Gerätekompatibilitätsrichtlinien für bedingten Zugriff](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **PFX-Zertifikat-Erstellung und -Verteilung und S/MIME-Unterstützung**

  Sie können jetzt PFX-Zertifikate für Benutzer in einer Hybridumgebung erstellen und bereitstellen. Diese Zertifikate können dann von Geräten, die der Benutzer registriert hat, für die E-Mail-Verschlüsselung und -Entschlüsselung mit S/MIME verwendet werden. Weitere Informationen finden Sie unter [Erstellen von PFX-Zertifikaten mit S-MIME-Unterstützung](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Unterstützung für zusätzliche Einstellungen für iOS-Konfigurationen**
   
    Ihnen stehen nun 42 zusätzliche iOS-Einstellungen zur Verfügung, die Sie als Teil eines Konfigurationselements konfigurieren können. Ein Großteil der Einstellungen (insgesamt 35) wurden für überwachte iOS-Geräte hinzugefügt. Weitere Informationen finden Sie unter [New compliance settings for iOS-Geräte (Neue Kompatibilitätseinstellungen für iOS-Geräte)](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## <a name="january-2017"></a>Januar 2017

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Android 7.1.1-Unterstützung**

  Intune unterstützt und verwaltet Android 7.1.1 jetzt vollständig.

- **Problembehandlung für inaktive iOS-Geräte oder die Verwaltungskonsole kann nicht mit ihnen kommunizieren**

  Wenn Benutzergeräte den Kontakt mit Intune verlieren, können Sie neue Problembehandlungsschritte vergeben, damit sie erneut Zugriff auf Unternehmensressourcen erhalten. Siehe [Geräte sind inaktiv oder die Verwaltungskonsole kann nicht mit ihnen kommunizieren](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Neuheiten in Configuration Manager Technical Preview 1701

- **Android- und iOS-Versionen werden nicht mehr über den Erstellungsassistenten für hybrides MDM erreicht**

  Ab Technical Preview 1701 für die hybride mobile Geräteverwaltung (MDM) müssen Sie nicht mehr bestimmte Android- und iOS-Versionen auswählen, wenn Sie neue Richtlinien und Profile für mit Intune verwaltete Geräte erstellen wollen. Durch diese Änderung können Hybridbereitstellungen schneller neue Android und iOS-Versionen unterstützen, ohne eine neue Configuration Manager-Version oder -Erweiterung zu benötigen. Weitere Informationen finden Sie unter [Android and iOS versions are no longer targetable in creation wizards (Android- und iOS-Versionen werden nicht mehr über den Erstellungsassistenten für hybrides MDM erreicht)](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="notices"></a>Benachrichtigungen

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Erinnerung zur Plattformunterstützung: Der Mainstream-Support für Windows Phone 8.1 endete am 11. Juli 2017.
<!-- 1327781 -->
*11. Juli 2017*

Die Windows Phone 8.1-Plattform hat das Ende des Mainstream-Supports erreicht. Der Support für den Windows 8.1-PC ist davon nicht betroffen.

Dies hat keine sofortigen Auswirkungen auf Windows Phone 8.1-Geräte, die über den Intune-Dienst verwaltet werden, auch nicht auf die Geräte, die in einer Hybrid-MDM-Lösung registriert sind. Registrierte Geräte funktionieren weiterhin, und alle Richtlinien, Konfigurationen und Apps werden weiterhin wie erwartet funktionieren. Beachten Sie, dass für die Windows Phone 8.1-Plattform im Intune-Dienst und für die Windows Phone 8.1-Unternehmensportal-App keine Verbesserungen mehr geplant sind.

Daher wird empfohlen, zum schnellstmöglichen Zeitpunkt ein Upgrade für berechtigte Windows Phone 8.1-Geräte auf Windows 10 Mobile durchzuführen.  

### <a name="end-of-support-for-android-43-and-lower"></a>Ende des Supports für Android 4.3 und niedriger
<!---1171127--->
*6. Juli 2017*

Verwaltete Apps und die Unternehmensportal-App für Android erfordern Android 4.4 oder höher für den Zugriff auf Unternehmensressourcen. Geräte, die nicht bis Anfang Oktober aktualisiert werden, können nicht mehr auf das Unternehmensportal oder diese Apps zugreifen. Ab Dezember werden alle registrierten Geräte deaktiviert und können dann nicht mehr auf Unternehmensressourcen zugreifen. Wenn Sie App-Schutzrichtlinien ohne MDM verwenden, erhalten Apps erhält keine Updates, und ihre Nutzungsqualität wird im Laufe der Zeit immer stärker abnehmen.


### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 und System Center 2012 R2 Configuration Manager (RTM): Die Unterstützung für die Verwaltung von hybriden Mobilgeräten endet am 10. April 2017.
*11. Januar 2017*

Die Unterstützung für System Center 2012 Configuration Manager SP1 und System Center 2012 R2 Configuration Manager RTM endete am 12. Juli 2016. In der Folge wird die Unterstützung für die mit dem Microsoft Intune-Dienst verbundenen Versionen für Hybrid-MDM am 10. April 2017 beendet. Nach diesem Datum wird Hybrid-MDM mit diesen Versionen nicht mehr funktionieren. Verwaltete Geräte werden grundsätzlich zu nicht verwalteten Geräten, weil der Intune-Connector nicht mehr mit dem Intune-Dienst verbunden ist. Configuration Manager-Daten (z.B. Richtlinien und Anwendungen) werden nicht an Intune übertragen und Daten von verwalteten Geräten werden bis zur Ausführung eines Upgrades nicht an Configuration Manager übermittelt.

Wenn Sie eine hybride Bereitstellung mit Configuration Manager 2012 SP1 oder R2 RTM ausführen, wird die Durchführung eines Upgrades auf Configuration Manager (Current Branch) oder das letzte unterstütze Service Pack für Configuration Manager 2012 (R2 SP1 oder SP2) noch vor dem 10. April 2017 empfohlen, um eine Dienstunterbrechung zu vermeiden.

Zusätzliche Ressourcen:
-   [Upgrade auf System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [Planen von Upgrades auf System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [Planen von Upgrades auf System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Upload in Unternehmensportal für Windows Phone 8 eingestellt
*25. Oktober 2016*

Die Funktion zum Hochladen einer signierten Unternehmensportal-App wurde aus der Configuration Manager-Konsole entfernt, da die Intune-Unterstützung für Windows 8, Windows Phone 8 und Windows RT veraltet ist und die Unterstützung für das Windows Phone 8-Unternehmensportal im November endet.  Bereits registrierte Windows 8-, Windows Phone 8- und Windows RT-Geräte werden weiterhin unterstützt, aber die Registrierung zusätzlicher Geräte bei diesen Plattformen wird nicht mehr unterstützt.


### <a name="see-also"></a>Siehe auch

- [Frühere Hybrid-MDM-Features](whats-new-hybrid-archive.md)
- [Neuigkeiten für MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)

