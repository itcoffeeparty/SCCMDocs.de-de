---
title: "Umstellen der MDM-Autorität auf Intune"
description: "Erfahren Sie, wie die MDM-Autorität von Configuration Manager (hybrid) auf Intune standalone umgestellt wird."
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/14/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.openlocfilehash: 12218472aa3f06ae041134f6cc092430e406c542
ms.sourcegitcommit: 948644072bd158b156f782a4376bcd50fac7c73a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2017
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Umstellen der MDM-Autorität auf Intune standalone

*Gilt für: System Center Configuration Manager (Current Branch)*    

Sie können einen vorhandenen Microsoft Intune-Mandanten, der über die Configuration Manager-Konsole (hybrides MDM) konfiguriert wurde, auf Intune standalone umstellen. Das Umstellen der MDM-Autorität auf Mandantenebene auf Intune ist die letzte Phase im Prozess zum [Migrieren von hybriden MDM-Benutzern und -Geräten zu Intune standalone](migrate-hybridmdm-to-intunesa.md) in der reinen Cloudkonfiguration.    

> [!Important]    
> Informationen zum Umstellen der MDM-Autorität, ohne zuvor hybride MDM-Benutzer zu Intune zu migrieren, finden Sie unter [Umstellen der MDM-Autorität](change-mdm-authority.md).

Mit den Schritten in diesem Thema stellen Sie die MDM-Autorität für einen Mandanten auf Intune um und migrieren alle Geräte, die bisher noch nicht migriert wurden, zu Intune standalone. Dieses Thema bietet Informationen dazu, wie Sie einen vorhandenen, über die Configuration Manager-Konsole (hybrid) konfigurierten Microsoft Intune-Mandanten auf Intune standalone umstellen. Dabei wird vorausgesetzt, dass Sie die folgenden Schritte bereits ausgeführt haben:
- Sie haben das [Intune-Datenimporttool](migrate-import-data.md) verwendet, um Configuration Manager-Objekte in Intune zu importieren. 
- Sie haben [Intune für die Benutzermigration vorbereitet](migrate-prepare-intune.md), um sicherzustellen, dass Benutzer und ihre Geräte nach der Migration weiterhin verwaltet werden.
- Sie haben die [MDM-Autorität für bestimmte Benutzer umgestellt (gemischte MDM-Autorität)](migrate-mixed-authority.md), um damit zu beginnen, Benutzergeräte über das Azure-Portal zu verwalten.


## <a name="users-and-devices-that-have-not-been-migrated"></a>Nicht migrierte Benutzer und Geräte
Sie haben bereits viele Benutzer migriert und die Intune-Funktionen getestet, um sicherzustellen, dass alles erwartungsgemäß funktioniert. Daher wurden Ihre Richtlinien, Profile, Apps usw. in Intune konfiguriert, und Sie haben die Objekte gründlich auf Geräten getestet. Nach der Umstellung der MDM-Autorität sollten keine neuen Konfigurationen für Ihre Richtlinien auf Mandantenebene erforderlich sein. Wenn es jedoch um Benutzer und Geräte geht, die zuvor nicht migriert wurden, finden Sie im Folgenden einige Informationen dazu, womit Sie nach der Umstellung der MDM-Autorität rechnen müssen:    
- Es gibt wahrscheinlich eine Übergangszeit (bis zu acht Stunden), bevor ein Gerät eingecheckt und mit dem Dienst synchronisiert wird.
- Geräte müssen nach der Umstellung eine Verbindung mit dem Dienst herstellen, damit die Einstellungen der neuen MDM-Autorität (Intune standalone) die vorhandenen Einstellungen auf dem Gerät ersetzen.
- Einige der grundlegenden Einstellungen (z.B. Profile) aus der vorherigen MDM-Autorität (hybrid) verbleiben bis zu sieben Tage lang auf dem Gerät. 
- Geräte, denen keine Benutzer zugeordnet sind (dies ist typischerweise der Fall, wenn Sie das iOS-Programm zur Geräteregistrierung oder die Massenregistrierung verwenden), werden nicht zur neuen MDM-Autorität migriert. Für diese Geräte müssen Sie sich mit dem Support in Verbindung setzen, um Hilfe beim Verschieben dieser Geräte zur neuen MDM-Autorität zu erhalten.

## <a name="prerequisites"></a>Voraussetzungen
Überprüfen Sie die folgenden Informationen, um die Umstellung der MDM-Autorität vorzubereiten:
- Sie benötigen Configuration Manager, Version 1610 oder höher, damit die Option zum Umstellen der MDM-Autorität verfügbar ist.
- Stellen Sie sicher, dass allen Benutzern, die momentan durch hybrides MDM verwaltet werden, eine Intune-/EMS-Lizenz zugewiesen wurde, bevor Sie die MDM-Autorität umstellen. Mit diesen Lizenzen wird sichergestellt, dass die Benutzer und ihre Geräte nach der Umstellung der MDM-Autorität von Intune standalone verwaltet werden. Weitere Informationen finden Sie unter [Zuweisen von Intune-Lizenzen zu Benutzerkonten](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Stellen Sie sicher, dass dem Konto des Administratorbenutzers eine Intune-/EMS-Lizenz zugewiesen wurde.

### <a name="change-the-mdm-authority-to-intune"></a>Umstellen der MDM-Autorität auf Intune
Verwenden Sie das folgende Verfahren, um die MDM-Autorität auf Mandantenebene auf Intune umzustellen.

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** &gt; **Übersicht** &gt; **Clouddienste** &gt; **Microsoft Intune-Abonnement**, und löschen Sie Ihr vorhandenes Intune-Abonnement.
2.  Wählen Sie **MDM-Autorität auf Microsoft Intune umstellen** aus, und klicken Sie dann auf **Weiter**.

    ![Dialogfeld zum Entfernen von Microsoft Intune-Abonnements](media/mdm-change-delete-subscription.png)
3.  Melden Sie sich bei dem Intune-Mandanten an, den Sie ursprünglich beim Festlegen der MDM-Autorität in Configuration Manager verwendet haben.
4.  Klicken Sie auf **Weiter** , und schließen Sie den Assistenten ab.
5.  Die MDM-Autorität wurde jetzt zurückgesetzt. Das Intune-Abonnement wird nicht mehr im Knoten „Microsoft Intune-Abonnements“ der Configuration Manager-Konsole angezeigt.
6.  Melden Sie sich [im Azure-Portal bei Intune ](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/overview) an, und verwenden Sie dabei den gleichen Mandanten wie zuvor.    

  > [!Important]    
  > Verwenden Sie nicht die klassische Intune-Konsole. Sie müssen sich über das Azure-Portal bei Intune anmelden.
7.  Vergewissern Sie sich, dass die MDM-Autorität auf **Microsoft Intune** umgestellt wurde. 

## <a name="next-steps"></a>Nächste Schritte
Sobald die Umstellung der MDM-Autorität abgeschlossen ist, überprüfen Sie die folgenden Informationen:
- Während der Umstellung der MDM-Autorität sollte es keine wahrnehmbaren Auswirkungen auf die Endbenutzer geben. 
- Sie müssen Richtlinien auf Mandantenebene nicht neu konfigurieren. 
- Nach der Umstellung der MDM-Autorität können Sie Richtlinien auf Mandantenebene über das Azure-Portal in Intune bearbeiten.
-  Führen Sie nach der Umstellung der MDM-Autorität die folgenden Schritte aus, um zu überprüfen, ob neue Geräte erfolgreich bei der neuen Autorität registriert werden:   
    - Registrieren eines neuen Geräts
    - Stellen Sie sicher, dass das neu registrierte Gerät in Intune angezeigt wird.
    - Führen Sie über die Verwaltungskonsole auf dem Gerät eine Aktion aus, z.B. Remotesperre. Wenn sie erfolgreich ist, wird das Gerät durch die neue MDM-Autorität verwaltet.
- Wenn Sie Probleme mit bestimmten Geräten haben, können Sie die Registrierung der Geräte aufheben und sie erneut registrieren, damit sie so schnell wie möglich mit der neuen Autorität verbunden und von ihr verwaltet werden.
- Für nicht migrierte Benutzer und Geräte gilt Folgendes:
    - Stellen Sie sicher, dass die Geräte jetzt auf dem Blatt **Geräte** als verwaltete Geräte angezeigt werden. Bevor diese Geräte nach der Umstellung der MDM-Autorität angezeigt werden, müssen sie beim Dienst eingecheckt und synchronisiert werden. 
    - Wenn der Intune-Dienst erkennt, dass die MDM-Autorität eines Mandanten umgestellt wurde, sendet er eine Benachrichtigung an alle registrierten Geräte, damit sie beim Dienst eingecheckt und synchronisiert werden (außerhalb der regelmäßigen geplanten Eincheckvorgänge). Nach der Umstellung der MDM-Autorität für den Mandanten von hybrid auf Intune standalone stellen daher alle Geräte, die eingeschaltet und online sind, eine Verbindung mit dem Dienst her, erhalten die neue MDM-Autorität und werden ab diesem Zeitpunkt von Intune standalone verwaltet. Es gibt keine Unterbrechung bei Verwaltung und Schutz dieser Geräte.
    - Geräte, die während (oder kurz nach) der Umstellung der MDM-Autorität ausgeschaltet oder offline sind, stellen unter der neuen MDM-Autorität eine Verbindung mit dem Dienst her und werden synchronisiert, sobald sie eingeschaltet werden und online sind.  
    - Benutzer können schnell auf die neue MDM-Autorität umstellen, indem sie manuell einen Eincheckvorgang des Geräts beim Dienst starten. Benutzer können den Eincheckvorgang problemlos durchführen, indem sie die Unternehmensportal-App verwenden und eine Überprüfung der Gerätekonformität initiieren.
    - Es gibt eine Übergangszeit, bis ein Gerät beim Dienst eingecheckt wird, wenn das Gerät während der Umstellung der MDM-Autorität offline war. Um sicherzustellen, dass das Gerät während dieser Übergangszeit geschützt und funktionsfähig bleibt, verbleiben die folgenden Profile bis zu sieben Tage lang (oder bis das Gerät eine Verbindung mit der neuen MDM-Autorität herstellt und die neuen Einstellungen empfängt, die die vorhandenen überschreiben) auf dem Gerät:
        - E-Mail-Profil
        - VPN-Profil
        - Zertifikatprofil
        - WLAN-Profil
        - Konfigurationsprofile
    - Wenden Sie sich an den Support, um Unterstützung bei der Umstellung der MDM-Autorität für Geräte zu erhalten, die keinem Benutzer zugewiesen sind. 
