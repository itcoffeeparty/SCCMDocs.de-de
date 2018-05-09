---
title: 'Registrieren von Geräten mit dem Geräteregistrierungs-Manager '
titleSuffix: Configuration Manager
description: Registrieren Sie unternehmenseigene Geräte mit dem Geräteregistrierungs-Managerkonto mit System Center Configuration Manager.
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a691bc98a26cdf56d22c03840997d9e0a380b7b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>Registrieren von Geräten mit dem Geräteregistrierungs-Manager mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit Intune können Organisationen eine Vielzahl mobiler Geräte mit einem einzelnen Benutzerkonto verwalten. Das Konto *Geräteregistrierungsmanager* (DEM) ist ein spezielles Benutzerkonto zum Registrieren von Geräten. Fügen Sie dem DEM-Konto vorhandene Benutzer hinzu, damit diese bestimmte DEM-Funktionen erhalten. Jedes registrierte Gerät verwendet eine Einzellizenz. Wir empfehlen die Verwendung von Geräten über dieses Konto als gemeinsam genutzte Geräte mit keiner Benutzeraffinität anstelle von persönlichen, dedizierten Geräten.  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>Registrieren von firmeneigenen Geräten mit dem Geräteregistrierungs-Manager  
 Sie können beispielsweise einem Speicher-Manager oder Supervisor ein Benutzerkonto für einen Geräteregistrierungs-Manager zuweisen, um ihm folgende Möglichkeiten zu geben:  

-   Registrieren von bis zu 1.000 Geräten für die Verwaltung  
-   Verwenden der Unternehmensportal-App, um Unternehmens-Apps zu installieren  
-   Konfigurieren des Zugriffs auf Unternehmensdaten  

Die folgenden Einschränkungen gelten für Geräte, die über ein Konto des Geräteregistrierungs-Managers verwaltet werden:

- Der Speicher-Manager kann das Gerät nicht über das Unternehmensportal zurücksetzen.  
- Geräte können nicht mit dem Arbeitsbereich oder Azure Active Directory verknüpft sein. Dadurch wird verhindert, dass diese Geräte den bedingten Zugriff verwenden.
-  Stellen Sie die Unternehmensportal-App als eine **Erforderliche Installation** auf dem Benutzerkonto des Geräteregistrierungs-Manager bereit, um Unternehmens-Apps für Geräte bereitzustellen, die mit dem Geräteregistrierungs-Manager verwaltet. Der Geräteregistrierungs-Manager kann dann die Unternehmensportal-App starten, um zusätzliche Apps zu installieren.
- Zur Verbesserung der Leistung zeigt die Unternehmensportal-App nur das lokale Gerät an. Die Remoteverwaltung anderer DEM-Geräte kann nur vom Administrator in der Configuration Manager-Konsole ausgeführt werden
- Die Unternehmensportal-Website ist nicht für Konten des Geräteregistrierungs-Managers verfügbar. Verwenden Sie die Unternehmensportal-App.
- Wenn Sie DEM für die Registrierung von iOS-Geräten verwenden, können Sie für die Registrierung der Geräte nicht Apple Configurator oder das Apple-Programm zur Geräteregistrierung (DEP) verwenden. (nur iOS) 

 **Beispiele für ein Szenario des Geräteregistrierungs-Managers:**   
Ein Restaurant möchte Point-of-Sale-Tablets für sein Bedienpersonal und Bestellmonitore für seine Küchenmitarbeiter. Die Mitarbeiter müssen niemals auf Unternehmensdaten zugreifen und sich nie als Benutzer anmelden. Der Intune-Administrator erstellt ein Konto für den Geräteregistrierungs-Manager und registriert die firmeneigenen Geräte mit diesem Konto. Alternativ kann der Administrator die Anmeldeinformationen des Geräteregistrierungs-Managers einem Restaurant-Manager geben, sodass dieser die Geräte registrieren und verwalten kann.  

 Der Administrator oder Manager kann rollenspezifische Apps auf den Restaurantgeräten bereitstellen. Ein Administrator kann auch ein Gerät in der Konsole auswählen und es aus der Verwaltung mobiler Geräte entfernen.  

#### <a name="add-a-device-enrollment-manager"></a>Hinzufügen eines Geräteregistrierungs-Managers  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Clouddienste**, und klicken Sie auf **Microsoft Intune-Abonnements**. Wählen Sie das Microsoft Intune-Abonnement aus, dem Sie einen Geräteregistrierungs-Manager hinzufügen möchten, und klicken Sie dann auf **Eigenschaften**.  

3.  Klicken Sie im Dialogfeld „Microsoft Intune-Abonnementeigenschaften“ auf die Registerkarte **Geräteregistrierungs-Manager**.  

4.  Klicken Sie auf **Hinzufügen/Entfernen**.  

5.  Geben Sie im Dialogfeld **Geräteregistrierungs-Manager** den Benutzernamen des Benutzers ein, den Sie als Geräteregistrierungs-Manager hinzufügen möchten, und klicken Sie dann auf **Suchen**. Wählen Sie den Benutzer aus, den Sie als Geräteregistrierungs-Manager hinzufügen möchten, und klicken Sie auf **Hinzufügen**.  

6.  Bestätigen Sie das Benutzerkonto, das ein Geräteregistrierungs-Manager werden soll, und klicken Sie auf **Hinzufügen/Entfernen**.  Eine Abonnementlizenz ist für jeden Benutzer erforderlich, der auf den Dienst zugreift, und der *Geräteregistrierungs-Manager* kann kein Intune-Administrator sein. Stellen Sie fest, ob Sie weitere Lizenzen benötigen, bevor Sie diese Funktion verwenden.  

7.  Der Geräteregistrierungs-Manager kann nun Mobilgeräte über das Verfahren registrieren, das ein Endbenutzer für ein BYOD-Szenario (Bring Your Own Device) im Unternehmensportal verwendet.  

#### <a name="delete-a-device-enrollment-manager-from-intune"></a>Löschen eines Geräteregistrierungs-Managers aus Intune  
Wenn Sie einen Geräteregistrierungs-Manager löschen, wirkt sich dies nicht auf registrierte Geräte aus. Wenn ein Geräteregistrierungs-Manager gelöscht wird:  
- Wird keine Registrierung eines registrierten Geräts aufgehoben  
- werden registrierte Geräte weiterhin vollständig verwaltet  
- bleiben die gelöschten Kontoanmeldedaten für den Geräteregistrierungs-Manager für die Anmeldung beim Unternehmensportal zum Zugriff auf Apps gültig  
- können über die Kontoanmeldedaten für den Geräteregistrierungs-Manager weiterhin keine Geräte zurückgesetzt oder deaktiviert werden  
- bleibt die Beziehung des gelöschten Geräteregistrierungs-Manager-Kontos zu registrierten Geräten bestehen, es können jedoch keine zusätzlichen Geräte registriert werden.

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  
2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Clouddienste**, und klicken Sie auf **Microsoft Intune-Abonnements**. Wählen Sie das Microsoft Intune-Abonnement aus, dem Sie einen Geräteregistrierungs-Manager hinzufügen möchten, und klicken Sie dann auf **Eigenschaften**.  
3.  Klicken Sie im Dialogfeld „Microsoft Intune-Abonnementeigenschaften“ auf die Registerkarte **Geräteregistrierungs-Manager**.  
4.  **Suchen** Sie nach dem Geräteregistrierungs-Manager, den Sie löschen möchten, klicken Sie auf **Entfernen** und dann auf **OK**.  
