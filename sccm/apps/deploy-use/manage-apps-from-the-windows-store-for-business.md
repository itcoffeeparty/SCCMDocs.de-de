---
title: "Verwalten von Apps aus dem Windows Store für Unternehmen | System Center Configuration Manager"
description: "Verwalten Sie Apps aus dem Windows Store für Unternehmen, und stellen Sie sie mithilfe von System Center Configuration Manager bereit."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e293b2ec4debf7a8513f1e3544ac234616f04d7

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Verwalten von Apps aus dem Windows Store für Unternehmen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Im [Windows Store für Unternehmen](https://www.microsoft.com/business-store) können Sie Apps für Ihre Organisation finden und entweder einzeln oder per Volumenlizenz erwerben. Durch Herstellen einer Verbindung des Store mit Configuration Manager können Sie die Liste der Apps, die Sie erworben haben, mit Configuration Manager synchronisieren, sie in der Configuration Manager-Konsole anzeigen und wie jede andere App auch bereitstellen.


## <a name="online-and-offline-apps"></a>Online- und Offline-Apps

Der Windows Store für Unternehmen unterstützt zwei Typen von Apps:

- **Online** – Dieser Lizenztyp setzt voraus, dass Benutzer und Geräte mit dem Store verbunden sind, um eine App und ihre Lizenz zu erhalten. Windows 10-Geräte müssen in die Azure Active Directory-Domäne eingebunden sein.
- **Offline** – Organisationen können Apps und Lizenzen zwischenspeichern und sie direkt in ihren lokalen Netzwerken bereitstellen, ohne eine Verbindung zum Store herzustellen bzw. ohne Internetverbindung.

[Erfahren Sie mehr](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview) über den Windows Store für Unternehmen.

Configuration Manager unterstützt die Verwaltung von Apps aus dem Windows Store für Unternehmen sowohl auf Windows 10-Geräten, auf denen der Configuration Manager-Client ausgeführt wird, als auch auf Windows 10-Geräten, die bei Microsoft Intune registriert sind (sogenannte Mischkonfiguration). Configuration Manager bietet die folgenden Funktionen für Online- und Offline-Apps.

> [!IMPORTANT]
> Um diese Funktion verwenden zu können, muss auf den Windows 10-Geräten das Release vom November 2015 (1511) oder höher ausgeführt werden.

|Funktion|Offline-Apps|Offline-Apps|
|------------|------------|------------|
|Synchronisieren von App-Daten mit Configuration Manager<br>(Synchronisierung erfolgt alle 24 Stunden)|Ja|Ja|
|Erstellen von Configuration Manager-Anwendungen aus Store-Apps|Ja|Ja|
|Unterstützung für kostenlose Apps aus dem Store|Ja|Ja|
|Unterstützung für kostenpflichtige Apps aus dem Store|Nein|Nein|
|Unterstützen von erforderlichen Bereitstellungen für Benutzer- oder Gerätesammlungen|Ja|Ja<sup>1</sup>|
|Unterstützen von verfügbaren Bereitstellungen für Benutzer- oder Gerätesammlungen|Ja<sup>3</sup>|Nein<sup>2</sup>|

<sup>1</sup>Unterstützt nur Geräte, die von Intune verwaltetet werden. Sie können zwar eine Online-Anwendung in der Configuration Manager-Konsole erstellen und auf einem Gerät bereitstellen, das durch den Configuration Manager-Client verwaltet wird. Dennoch funktioniert dieser Vorgang nicht. Endbenutzer werden auf die entsprechende Seite im App Store weitergeleitet und müssen die App dort manuell installieren.

<sup>2</sup>Online-Apps können je nach Verfügbarkeit für Benutzer- oder Gerätesammlungen auf Geräten bereitgestellt werden, die ausschließlich über den Configuration Manager-Client verwaltet werden. Wenn Endbenutzer jedoch die App im Softwarecenter auswählen, werden sie zum Windows Store für Unternehmen weitergeleitet und müssen die App dort manuell installieren. Verfügbare Bereitstellungen für Geräte, die bei Microsoft Intune registriert sind, werden nicht unterstützt.

<sup>3</sup>Nur von Intune verwaltete Geräte werden nicht unterstützt.

> [!IMPORTANT]
> Wenn Ihre Configuration Manager-Hierarchie einen Standort der zentralen Verwaltung und mindestens einen primären Standort enthält, tritt in diesem Release bei der Bereitstellung von Offline-Apps aus dem Windows Store für Unternehmen für Geräte, die von Intune verwaltet werden, ein Fehler auf.


## <a name="activate-the-windows-store-for-business-capability"></a>Aktivieren der Funktionen des Windows Store für Unternehmen
Hierbei handelt es sich um ein Vorabfeature. Bevor Sie eine Verbindung zwischen Configuration Manager und dem Windows Store für Unternehmen herstellen können, müssen Sie daher die folgenden Schritte ausführen:

**Zustimmen zur Verwendung von Vorabfeatures**
1. Klicken Sie im Arbeitsbereich **Administration** der Configuration Manager-Konsole auf **Standortkonfiguration** > **Standorte**.
2. Wählen Sie den obersten Standort in Ihrer Hierarchie aus, und öffnen Sie anschließend die **Hierarchieeinstellungen**.
3. Aktivieren Sie im Dialogfeld **Eigenschaften von Hierarchieeinstellungen** das Kontrollkästchen **Verwendung von Vorabfeatures zustimmen**.
4. Klicken Sie auf **OK**.

**Aktivieren der Funktionen des Windows Store für Unternehmen**
1. Klicken Sie im Arbeitsbereich **Verwaltung** der Configuration Manager-Konsole auf **Clouddienste** > **Updates und Wartung** > **Features**.
2. Wählen Sie **Integration von Windows Store für Unternehmen ** aus, und klicken Sie anschließend auf der Registerkarte **Start**, in der Gruppe **Features** auf **Aktivieren**.
3. Schließen und öffnen Sie die Configuration Manager-Konsole erneut.
4. Jetzt sehen Sie den Knoten **Windows Store für Unternehmen** im Arbeitsbereich **Verwaltung** unter **Clouddienste**.

## <a name="set-up-windows-store-for-business-synchronization"></a>Einrichten der Synchronisierung mit Windows Store für Unternehmen

**Registrieren Sie Configuration Manager über „Webanwendung und/oder Web-API“ als Verwaltungstool in Azure Active Directory. Sie erhalten eine Client-ID, die Sie später benötigen.**
1. Wählen Sie im Active Directory-Knoten, [https://manage.windowsazure.com](https://manage.windowsazure.com), Ihr Azure Active Directory aus, und klicken Sie anschließend auf **Anwendungen** > **Hinzufügen**.
2.  Klicken Sie auf **Eine von meinem Unternehmen entwickelte Anwendung hinzufügen**.
3.  Geben Sie einen Namen für die Anwendung ein, wählen Sie **Webanwendung** und/oder **Web-API** aus, und klicken Sie anschließend auf den Pfeil **Weiter**.
4.  Geben Sie die gleiche URL für die **Registrierungs-URL** und die **App-ID-URI** ein. Dabei kann es sich um eine beliebige URL handeln, die nicht in eine reale Adresse aufgelöst werden muss. Sie können z.B. *https://yourdomain/sccm* eingeben.
5.  Schließen Sie den Assistenten ab.

**Erstellen eines Clientschlüssels für das registrierte Verwaltungstool in Azure Active Directory**
1.  Markieren Sie die Anwendung, die Sie soeben erstellt haben, und klicken Sie auf **Konfigurieren**.
2.  Wählen Sie unter **Schlüssel** eine Dauer aus der Liste aus, und klicken Sie anschließend auf **Speichern**. Dadurch wird ein neuer Clientschlüssel erstellt. Verlassen Sie diese Seite nicht, bevor Sie Windows Store für Unternehmen erfolgreich in Configuration Manager eingebunden haben.

**Konfigurieren von Configuration Manager als Speicherverwaltungstool im Windows Store für Unternehmen**
1.  Öffnen Sie [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools), und melden Sie sich nach entsprechender Aufforderung an.
2.  Akzeptieren Sie gegebenenfalls die Nutzungsbedingungen.
3.  Klicken Sie unter **Verwaltungstools** auf **Verwaltungstool hinzufügen**.
4.  Geben Sie unter **Tool nach Namen suchen** den Namen der App ein, die Sie zuvor in AAD erstellt haben, und klicken Sie anschließend auf **Hinzufügen**.
5.  Klicken Sie neben der Anwendung, die Sie gerade importiert haben, auf **Aktivieren**.
6.  Wählen Sie auf der Seite **Verwalten > Kontoinformationen** die Option **Offline lizenzierte Apps anzeigen** aus, wenn Sie den Einkauf offline lizenzierter Anwendungen zulassen möchten.

**Hinzufügen des Store-Kontos zu Configuration Manager**

1. Vergewissern Sie sich, dass Sie mindestens eine App aus dem Windows Store für Unternehmen erworben haben. Erweitern Sie im Arbeitsbereich **Verwaltung** der Configuration Manager-Konsole **Clouddienste**, und klicken Sie anschließend auf **Windows Store für Unternehmen**.
2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Windows Store für Unternehmen** auf **Windows Store für Unternehmen-Konto hinzufügen**.
3.  Fügen Sie Mandanten-ID, Client-ID und Clientschlüssel aus Azure Active Directory hinzu, und schließen Sie den Assistenten ab.
4. Sobald Sie fertig sind, wird das von Ihnen konfigurierte Konto in der Liste **Windows Store für Unternehmen** der Configuration Manager-Konsole aufgeführt.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Erstellen und Bereitstellen einer Configuration Manager-Anwendung aus einer App aus dem Windows Store für Unternehmen
1.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** der Configuration Manager-Konsole **Anwendungsmanagement**, und klicken Sie anschließend auf **Lizenzinformationen für Store-Apps**.
2.  Wählen Sie zunächst die App aus, die Sie bereitstellen möchten. Klicken Sie anschließend auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Anwendung erstellen**.
Eine Configuration Manager-App wird erstellt, die eine App aus dem Windows Store für Unternehmen enthält. Sie können diese Anwendung wie jede andere Configuration Manager-Anwendung bereitstellen und überwachen.

> [!IMPORTANT]
> Für Geräte, die bei Intune registriert sind, stehen bereitgestellte Apps nur für diejenigen Benutzer zur Verfügung, die sie ursprünglich registriert haben. Andere Benutzer können nicht auf die App zugreifen.

## <a name="monitor-windows-store-for-business-apps"></a>Überwachen von Apps aus dem Windows Store für Unternehmen

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsmanagement**, und klicken Sie anschließend auf **Lizenzinformationen für Store-Apps**.

Sie können für jede von Ihnen verwaltete Store-App Informationen anzeigen, wie den Namen, die Plattform, die Anzahl der Lizenzen, die Sie für diese App besitzen, sowie die Anzahl der Lizenzen, die Ihnen zur Verfügung stehen.



<!--HONumber=Nov16_HO1-->


