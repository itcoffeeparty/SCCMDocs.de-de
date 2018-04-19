---
title: Konfigurieren von Microsoft Edge-Einstellungen
titleSuffix: Configuration Manager
description: Konfigurieren von Einstellungen für den Microsoft Edge-Webbrowser auf Windows 10-Clients
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: cb162e030249b02018af52ad3266b6b8df5ce355
ms.sourcegitcommit: aed99ba3c5e9482199cb3fc5c92f6f3a160cb181
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="configure-microsoft-edge-settings-in-system-center-configuration-manager"></a>Konfigurieren von Microsoft Edge-Einstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

<!-- 1357310 -->
Kunden, die den [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256)-Webbrowser auf Windows 10-Clients verwenden, erstellen ab der Version 1802 eine Richtlinie für Configuration Manager-Konformitätseinstellungen, um verschiedene Microsoft Edge-Einstellungen zu konfigurieren. 

Diese Richtlinie gilt nur für Clients unter Windows 10 ab Version 1703. <!--511552-->


## <a name="policy-settings"></a>Richtlinieneinstellungen
Diese Richtlinie umfasst derzeit die folgenden Einstellungen:
- **Microsoft Edge-Browser als Standard** festlegen: Konfiguriert die Windows 10-Standard-App-Einstellung für Webbrowser auf Microsoft.
- **Dropdown in der Adressleiste zulassen:**: erfordert Version 1703 von Windows 10 oder höher. Weitere Informationen finden Sie unter der [AllowAddressBarDropdown-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Synchronisierung von Favoriten zwischen Microsoft-Browsern zulassen**: Erfordert Windows 10 Version 1703 oder höher. Weitere Informationen finden Sie unter der [SyncFavoritesBetweenIEAndMicrosoftEdge-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Das Löschen von Browserdaten beim Beenden zulassen**: Erfordert Windows 10 Version 1703 oder höher. Weitere Informationen finden Sie unter der [ClearBrowsingDataOnExit-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **DNT-Kopfzeilen zulassen**: Weitere Informationen finden Sie unter der [AllowDoNotTrack-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Autoausfüllen zulassen**: Weitere Informationen finden Sie unter der [AllowAutofill-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Cookies zulassen**: Weitere Informationen finden Sie unter der [AllowCookies-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Popupblocker zulassen**: Weitere Informationen finden Sie unter der [AllowPopups-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Suchvorschläge in Adressleiste zulassen**: Weitere Informationen finden Sie unter der [AllowSearchSuggestionsinAddressBar-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Senden von Intranetdatenverkehr an Internet Explorer zulassen**: Weitere Informationen finden Sie unter der [SendIntranetTraffictoInternetExplorer-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Kennwort-Manager zulassen**: Weitere Informationen finden Sie unter der [AllowPasswordManager-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Entwicklertools zulassen**: Weitere Informationen finden Sie unter der [AllowDeveloperTools-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Erweiterungen zulassen**: Weitere Informationen finden Sie unter der [AllowExtensions-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).



## <a name="create-the-microsoft-edge-browser-profile"></a>Erstellen des Microsoft Edge-Browserprofils

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**. Erweitern Sie **Konformitätseinstellungen**, und wählen Sie den neuen Knoten **Microsoft Edge-Browserprofile** aus. Klicken Sie auf die Menübandoption **Richtlinie für den Microsoft Edge-Browser erstellen**.
2. Geben Sie einen **Namen** für die Richtlinie ein, geben Sie optional eine **Beschreibung** ein, und klicken Sie auf **Weiter**.
3. Ändern Sie auf der Seite **Einstellungen** den Wert für die Einstellungen, die in diese Richtlinie einbezogen werden sollen, zu **Konfiguriert**, und klicken Sie auf **Weiter**.
4. Wählen Sie auf der Seite **Unterstützte Plattformen** die Betriebssystemversionen und -architekturen aus, für die diese Richtlinie gelten soll, und klicken Sie auf **Weiter**. 
5. Schließen Sie den Assistenten ab.



## <a name="deploy-the-policy"></a>Bereitstellen der Richtlinie

1. Wählen Sie Ihre Richtlinie aus, und klicken Sie auf die Menübandoption **Bereitstellen**.
2. Klicken Sie auf **Durchsuchen**, um die Benutzer- oder Gerätesammlung auszuwählen, in der die Richtlinie bereitgestellt werden soll. 
3. Wählen Sie nach Bedarf weitere Optionen aus. 
    a. Generieren Sie Warnungen, wenn die Richtlinie nicht konform ist. 
    b. Legen Sie den Zeitplan fest, nach dem der Client die Konformität des Geräts mit dieser Richtlinie auswertet.
4. Klicken Sie auf **OK**, um die Bereitstellung zu erstellen.



## <a name="next-steps"></a>Nächste Schritte

Wie bei jeder anderen Richtlinie für Konformitätseinstellungen gleicht der Client die Einstellungen gemäß dem von Ihnen angegebenen Zeitplan ab. In der Configuration Manager-Konsole können Sie die [Gerätekonformität überwachen und Berichte anzeigen](/sccm/compliance/deploy-use/monitor-compliance-settings).
