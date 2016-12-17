---
title: "Schützen von Daten mit Remotezurücksetzung, Remotesperre oder Kennungsrücksetzung mithilfe von System Center Configuration Manager"
description: "Schützen von Gerätedaten mit vollständigem Zurücksetzen, selektivem Zurücksetzen, Remotesperre oder Kennungsrücksetzung mithilfe von System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
caps.latest.revision: 18
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 49a2220616bb6c6734643885bf969245e4c67c77

---
# <a name="protect-data-with-remote-wipe-lock-or-passcode-reset-using-system-center-configuration-manager"></a>Schützen von Daten mit Remotezurücksetzung, Remotesperre oder Kennungsrücksetzung mithilfe von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In Configuration Manager sind Funktionen zum selektiven und vollständigen Zurücksetzen, zum Remotesperren und zur Kennungsrücksetzung verfügbar. Auf mobilen Geräten können sensible Unternehmensdaten gespeichert sein, mit denen auf zahlreiche Unternehmensressourcen zugegriffen werden kann. Zum Schutz von Geräten können Sie folgende Aktionen ausführen:  

-   Sie können mit einem vollständigen Zurücksetzen des Geräts die Werkseinstellungen wiederherstellen.  

-   Sie können mit einem selektiven Zurücksetzen nur die Firmendaten entfernen.  

-   Sie können ein Gerät, das möglicherweise verlorengegangen ist, mithilfe einer Remotesperre sichern.  

-   Sie können eine Kennungsrückstellung ausführen.  

##  <a name="full-wipe"></a>vollständiges Zurücksetzen  
 Sie können das Zurücksetzen eines Geräts veranlassen, wenn Sie ein verlorengegangenes Gerät sichern oder ein Gerät von der aktiven Verwendung abkoppeln möchten.  

 Veranlassen Sie ein **vollständiges Zurücksetzen** , um bei einem Gerät die Werkseinstellungen wiederherzustellen. Hierdurch werden alle Firmen- und Benutzerdaten sowie -einstellungen entfernt.  Sie können auf Geräten mit Windows Phone, iOS, Android und Windows 10 eine vollständige Zurücksetzung ausführen.  

> [!NOTE]
> Beim Zurücksetzen von Windows 10-Geräten in Versionen vor Version 1511 mit weniger als 4 GB RAM reagiert das Gerät möglicherweise nicht mehr. [Weitere Informationen](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram)

### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>So leiten Sie eine Remotezurücksetzung über die Configuration Manager-Konsole ein  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** und dann auf **Geräte**. Sie können alternativ auf **Gerätesammlungen** klicken und eine Sammlung auswählen.  

2.  Wählen Sie das Gerät aus, das Sie außer Kraft oder zurücksetzen möchten.  

3.  Klicken Sie in der **Gerätegruppe** auf **Remotegeräteaktionen**, und wählen Sie dann **Außerkraftsetzen/Zurücksetzen**aus.  

## <a name="selective-wipe"></a>selektives Zurücksetzen  
 Veranlassen Sie ein **selektives Zurücksetzen** , um beim Gerät nur die Firmendaten zu entfernen. In der folgenden Tabelle wird nach Plattform sortiert beschrieben, welche Daten bei einem selektiven Zurücksetzen entfernt werden und mit welchen Auswirkungen auf verbleibende Daten zu rechnen ist.  

 **iOS**  

|Beim Abkoppeln eines Geräts entfernte Inhalte|iOS|  
|--------------------------------------------|---------|  
|Unternehmens-Apps und die entsprechenden Daten, die mit Configuration Manager und Intune installiert wurden.|Apps werden deinstalliert. Daten von Unternehmens-Apps werden entfernt.|  
|VPN- und WLAN-Profile|Entfernt.|  
|Zertifikate|Entfernt und gesperrt.|  
|Einstellungen|Entfernt, mit Ausnahme von: **Sprachroaming zulassen**, **Datenroaming zulassen** und **Automatische Synchronisierung beim Roaming zulassen**.|  
|Verwaltungs-Agent|Das Verwaltungsprofil wird entfernt.|  
|E-Mail-Profile|Für E-Mail-Profile, die von Intune bereitgestellt wurden, werden das E-Mail-Konto und die E-Mails entfernt.|  

 **Android und Android Samsung KNOX**  

|Beim Abkoppeln eines Geräts entfernte Inhalte|Android|Samsung KNOX|  
|--------------------------------------------|-------------|------------------|  
|Unternehmens-Apps und die entsprechenden Daten, die mit Configuration Manager und Intune installiert wurden.|Apps und Daten bleiben installiert.|Apps werden deinstalliert.|  
|VPN- und WLAN-Profile|Entfernt.|Entfernt.|  
|Zertifikate|Gesperrt.|Gesperrt.|  
|Einstellung|Anforderungen entfernt.|Anforderungen entfernt.|  
|Verwaltungs-Agent|Die Berechtigung „Geräteadministrator“ wird gesperrt.|Die Berechtigung „Geräteadministrator“ wird gesperrt.|  
|E-Mail-Profile|Nicht zutreffend.|Für E-Mail-Profile, die von Intune bereitgestellt wurden, werden das E-Mail-Konto und die E-Mails entfernt.|  

 **Windows 10, Windows 8.1, Windows RT 8.1 und Windows RT**  

|Beim Abkoppeln eines Geräts entfernte Inhalte|Windows 10, Windows 8.1 und Windows RT 8.1|Windows RT|  
|---------------------------------|-------------|-----------|
|Unternehmens-Apps und die entsprechenden Daten, die mit Configuration Manager und Intune installiert wurden.|Anwendungen werden deinstalliert, und Sideload-Schlüssel werden entfernt. Bei Anwendungen, bei denen die selektive Zurücksetzung von Windows verwendet wird, wird der Verschlüsselungsschlüssel gesperrt und die Daten sind nicht mehr verfügbar.|Sideload-Schlüssel werden entfernt, Anwendungen bleiben jedoch installiert.|  
|VPN- und WLAN-Profile|Entfernt.|Nicht zutreffend.|  
|Zertifikate|Entfernt und gesperrt.|Nicht zutreffend.|  
|Einstellung|Anforderungen entfernt.||  
|Verwaltungs-Agent|Nicht zutreffend. Der Verwaltungs-Agent ist integriert.|Nicht zutreffend. Der Verwaltungs-Agent ist integriert.|  
|E-Mail-Profile|Entfernt EFS-aktivierte E-Mails, darunter die E-Mail-App für Windows-E-Mails und -Anlagen.|Nicht zutreffend.|  

 **Windows 10 Mobile, Windows Phone 8.0 und Windows Phone 8.1**  


 |Beim Abkoppeln eines Geräts entfernte Inhalte|Windows 10 Mobile, Windows Phone 8.0 und Windows Phone 8.1|  
|-|-|
|Unternehmens-Apps und die entsprechenden Daten, die mit Configuration Manager und Intune installiert wurden.|Apps werden deinstalliert. Daten von Unternehmens-Apps werden entfernt.|  
|VPN- und WLAN-Profile|Für Windows 10 Mobile und Windows Phone 8.1 entfernt|  
|Zertifikate|Für Windows Phone 8.1 entfernt.|  
|Verwaltungs-Agent|Nicht zutreffend. Der Verwaltungs-Agent ist integriert|  
|E-Mail-Profile|Entfernt (mit Ausnahme von Windows Phone 8.0)|  

 Die folgenden Einstellungen werden ebenfalls aus Windows 10 Mobile- und Windows Phone 8.1-Geräten entfernt:  

-   Anfordern eines Kennworts zum Entsperren mobiler Geräte  

-   Einfache Kennwörter zulassen  

-   Minimale Kennwortlänge  

-   Erforderlicher Kennworttyp  

-   Kennwortablauf (Tage)  

-   Kennwortverlauf speichern  

-   Anzahl zulässiger wiederholter Anmeldefehler, bevor das Gerät zurückgesetzt wird  

-   Minuten der Inaktivität, bevor ein Kennwort erforderlich ist  

-   Erforderlicher Kennworttyp – Mindestanzahl von Zeichensätzen  

-   Kamera zulassen  

-   Verschlüsselung auf mobilem Gerät anfordern  

-   Wechselspeichermedien zulassen  

-   Webbrowser zulassen  

-   App Store zulassen  

-   Bildschirmaufnahme zulassen  

-   Geolocation zulassen  

-   Microsoft-Konto zulassen  

-   Kopieren und Einfügen zulassen  

-   WLAN-Tethering zulassen  

-   Automatische Verbindung mit unverschlüsselten WLAN-Hotspots zulassen  

-   Berichterstellung für WLAN-Hotspots zulassen  

-   Zurücksetzen auf Werkseinstellungen zulassen  

-   Bluetooth zulassen  

-   NFC zulassen  

-   WLAN zulassen  

### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>So leiten Sie eine Remotezurücksetzung über die Configuration Manager-Konsole ein  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** und dann auf **Geräte**. Sie können alternativ auf **Gerätesammlungen** klicken und eine Sammlung auswählen.  

2.  Wählen Sie das Gerät aus, das Sie außer Kraft oder zurücksetzen möchten.  

3.  Klicken Sie in der **Gerätegruppe** auf **Remotegeräteaktionen**, und wählen Sie dann **Außerkraftsetzen/Zurücksetzen**aus.  

## <a name="wiping-encrypting-file-system-efs-enabled-content"></a>Zurücksetzen EFS-aktivierter Inhalte  
 Das selektive Zurücksetzen von EFS-verschlüsselten Inhalten wird von Windows 8.1 und Windows RT 8.1 unterstützt. Folgendes gilt für das selektive Zurücksetzen von EFS-aktivierten Inhalten:  

-   Nur Apps und Daten, die mit derselben Internetdomäne wie das Intune-Konto von EFS geschützt werden, werden selektiv zurückgesetzt. Weitere Informationen finden Sie unter [Windows Selective Wipe for Device Data Management](http://technet.microsoft.com/library/dn486874.aspx)(in englischer Sprache).  

-   Wenn Änderungen an der EFS zugeordneten Domäne vorgenommen werden, können die Änderungen bis zu 48 Stunden dauern, bevor Apps und Daten selektiv zurückgesetzt werden können, die die neue Domäne verwenden.  

-   Jede bei Intune registrierte Domäne wird zurückgesetzt.  

 Folgende Daten und Apps werden derzeit vom selektiven Zurücksetzen mit EFS unterstützt:  

-   E-Mail-App für Windows  

-   Arbeitsordner  

-   Von EFS verschlüsselte Dateien und Ordner Weitere Informationen finden Sie unter [Vorgehensweisen bei Verwendung des verschlüsselnden Dateisystems](http://support.microsoft.com/kb/223316).  

### <a name="best-practices-for-selective-wipe"></a>Bewährte Methoden für selektives Zurücksetzen  

-   Zum erfolgreichen Zurücksetzen der E-Mail-Funktion stellen Sie E-Mail-Profile auf Geräten mit iOS und Windows Phone 8.1 bereit.  

-   Zum erfolgreichen Zurücksetzen von Apps stellen Sie sicher, dass die Apps über die App-Verwaltung für mobile Geräte verteilt werden.  

-   Legen Sie für iOS die Einstellung „Sicherung auf iCloud zulassen“ auf „Nicht zulassen“ fest, damit Benutzer Inhalte nicht über die iCloud wiederherstellen können.  

-   Wenn ein Konto deaktiviert wurde, wird das Konto nach einem Jahr von Intune außer Kraft gesetzt, und eine selektive Zurücksetzung wird ausgeführt.  

##  <a name="passcode-reset"></a>Zurücksetzen der Kennung  
 Wenn ein Benutzer seine Kennung vergisst, können Sie die Kennung von einem Gerät entfernen oder eine neue temporäre Kennung auf einem Gerät erzwingen. In der folgenden Tabelle ist die Funktionsweise der Kennungszurücksetzung auf verschiedenen mobilen Plattformen aufgeführt.  

|Plattform|Zurücksetzen der Kennung|  
|--------------|--------------------|  
|iOS|Wird für das Löschen der Kennung von einem Gerät unterstützt. Es wird keine neue temporäre Kennung erstellt.|  
|Android|Wird unterstützt. Zudem wird eine temporäre Kennung erstellt.|  
|Windows 10|Derzeit nicht unterstützt.|  
|Windows Phone 8 und Windows Phone 8.1|Unterstützt|  
|Windows RT 8.1 und Windows RT|Nicht unterstützt|  
|Windows 8.1|Nicht unterstützt|  

### <a name="to-reset-the-passcode-on-a-mobile-device-remotely-in-configuration-manager"></a>So setzen Sie die Kennung auf einem mobilen Gerät remote in Configuration Manager zurück  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** und dann auf **Geräte**. Sie können alternativ auf **Gerätesammlungen** klicken und eine Sammlung auswählen.  

2.  Wählen Sie die Geräte aus, auf denen die Kennung zurückgesetzt werden soll.  

3.  Klicken Sie in der **Gerätegruppe** auf **Remotegeräteaktionen**, und wählen Sie dann **Zurücksetzen der Kennung**aus.  

### <a name="to-show-the-state-of-the-passcode-reset"></a>So zeigen Sie den Zustand beim Zurücksetzen der Kennung an  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** und dann auf **Geräte**. Sie können alternativ auf **Gerätesammlungen** klicken und eine Sammlung auswählen.  

2.  Wählen Sie die Geräte aus, auf denen Sie den Zustand beim Zurücksetzen der Kennung anzeigen möchten.  

3.  Klicken Sie in der **Gerätegruppe** auf **Remotegeräteaktionen**, und wählen Sie dann **Kennungszustand anzeigen**aus.  

##  <a name="remote-lock"></a>Remotesperre  
 Wenn ein Benutzer sein Gerät verliert, können Sie es remote sperren. In der folgenden Tabelle ist die Funktionsweise der Remotesperrung auf verschiedenen mobilen Plattformen aufgeführt.  

|Plattform|Remotesperre|  
|--------------|-----------------|  
|iOS|Unterstützt|  
|Android|Unterstützt|  
|Windows 10|Derzeit nicht unterstützt.|  
|Windows Phone 8 und Windows Phone 8.1|Unterstützt|  
|Windows RT 8.1 und Windows RT|Unterstützt, wenn der aktuelle Benutzer des Geräts derjenige ist, der das Gerät registriert hat.|  
|Windows 8.1|Unterstützt, wenn der aktuelle Benutzer des Geräts derjenige ist, der das Gerät registriert hat.|  

### <a name="to-lock-a-mobile-device-remotely-through-the-configuration-manager-console"></a>So sperren Sie ein mobiles Gerät remote über die Configuration Manager-Konsole  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** und dann auf **Geräte**. Sie können alternativ auf **Gerätesammlungen** klicken und eine Sammlung auswählen.  

2.  Wählen Sie die zu sperrenden Geräte aus.  

3.  Klicken Sie in der **Gerätegruppe** auf **Remotegeräteaktionen**, und wählen Sie dann **Remotesperre**aus.  

### <a name="to-show-the-state-of-the-remote-lock"></a>So zeigen Sie den Zustand der Remotesperre an  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** und dann auf **Geräte**. Sie können alternativ auf **Gerätesammlungen** klicken und eine Sammlung auswählen.  

2.  Wählen Sie die Geräte aus, auf denen Sie den Zustand der Remotesperre anzeigen möchten.  

3.  Klicken Sie in der **Gerätegruppe** auf **Remotegeräteaktionen**, und wählen Sie dann **Zustand der Remotesperre anzeigen**aus.  

## <a name="see-also"></a>Siehe auch  
 [Windows Selective Wipe for Device Data Management](http://technet.microsoft.com/library/dn486874.aspx)   
 [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune (Hybride Verwaltung mobiler Geräte mit System Center Configuration Manager und Microsoft Intune)](../../mdm/plan-design/hybrid-mobile-device-management.md)



<!--HONumber=Nov16_HO1-->

