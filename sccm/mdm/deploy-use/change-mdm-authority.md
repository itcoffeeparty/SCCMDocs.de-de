---
title: "Umstellen der MDM-Autorität"
titleSuffix: Configuration Manager
description: "Erfahren Sie, wie Sie die MDM-Autorität von Configuration Manager (hybrid) auf Intune Standalone umstellen."
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/17/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: c61a44cce443a7ff210a626d114068691541aaae
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="change-your-mdm-authority"></a>Umstellen der MDM-Autorität
Ab Configuration Manager Version 1610 können Sie Ihre MDM-Autorität ohne Unterstützung durch den Microsoft-Support und ohne Aufheben der Registrierung und erneutes Registrieren Ihrer vorhandenen verwalteten Geräte umstellen. Dieser Artikel erläutert die Schritte, die ausgeführt werden müssen, um einen vorhandenen Microsoft Intune-Mandanten, der über die Configuration Manager-Konsole (hybrid) konfiguriert wurde, auf eigenständiges Intune umzustellen. Nachdem Sie die Schritte in diesem Artikel abgeschlossen haben, werden die Geräte von Microsoft Intune im [Azure-Portal](https://portal.azure.com) verwaltet. 

> [!Note]    
> Wenn Sie einen vorhandenen Microsoft Intune-Mandanten, dessen MDM-Autorität Intune ist, auf Configuration Manager (hybrid) ändern möchten, finden Sie weitere Informationen unter [Umstellen der MDM-Autorität](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority).

> [!Important]    
> Dieser Artikel behandelt die Umstellung Ihrer MDM-Autorität, wenn bisher noch keine Benutzer migriert wurden. Informationen zum Umstellen Ihrer MDM-Autorität, nachdem Sie [eine Teilmenge von Benutzern migriert](migrate-hybridmdm-to-intunesa.md) haben, finden Sie unter [Umstellen der MDM-Autorität](migrate-change-mdm-authority.md).

## <a name="key-considerations"></a>Wichtige Überlegungen
Nachdem Sie auf die neue MDM-Autorität umgestellt haben, gibt es wahrscheinlich eine Übergangszeit (bis zu acht Stunden), bevor das Gerät eingecheckt und mit dem Dienst synchronisiert wird. Sie müssen Einstellungen in der neuen MDM-Autorität (Intune standalone) konfigurieren, um sicherzustellen, dass registrierte Geräte nach der Umstellung weiterhin verwaltet und geschützt werden. Berücksichtigen Sie die folgenden Überlegungen:
- Geräte müssen nach der Umstellung eine Verbindung mit dem Dienst herstellen, damit die Einstellungen der neuen MDM-Autorität (eigenständiges Intune) die vorhandenen Einstellungen auf dem Gerät ersetzen.
- Nachdem Sie die MDM-Autorität umgestellt haben, verbleiben einige der grundlegenden Einstellungen (z.B. Profile) aus der vorherigen MDM-Autorität (hybrid) bis zu sieben Tage lang auf dem Gerät. Es wird empfohlen, Apps und Einstellungen (Richtlinien, Profile, Apps usw.) so schnell wie möglich in der neuen MDM-Autorität zu konfigurieren. Stellen Sie die Einstellungen auch für die Benutzergruppen bereit, in denen Benutzer mit bereits registrierten Geräten enthalten sind. Wenn ein Gerät nach der Umstellung der MDM-Autorität eine Verbindung mit dem Dienst herstellt, erhält es die neuen Einstellungen von der neuen MDM-Autorität. Alle neuen zugeordneten Richtlinien überschreiben vorhandene Richtlinien auf dem Gerät.
- Nachdem Sie auf die neue MDM-Autorität umgestellt haben, kann es bis zu einer Woche dauern, bis die Konformitätsinformationen im [Azure-Portal](https://portal.azure.com) ordnungsgemäß gemeldet werden. Allerdings sind die Kompatibilitätszustände in Azure Active Directory und auf dem Gerät richtig, sodass das Gerät weiterhin geschützt ist.
- Geräte, denen keine Benutzer zugeordnet sind (dies ist typischerweise der Fall, wenn Sie das iOS-Programm zur Geräteregistrierung oder die Massenregistrierung verwenden), werden nicht zur neuen MDM-Autorität migriert. Für diese Geräte müssen Sie sich mit dem Support in Verbindung setzen, um Hilfe beim Verschieben dieser Geräte zur neuen MDM-Autorität zu erhalten.

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Vorbereiten der Umstellung der MDM-Autorität auf Intune standalone
Überprüfen Sie die folgenden Informationen, um die Umstellung der MDM-Autorität vorzubereiten:
- Sie benötigen Configuration Manager, Version 1610 oder höher, damit die Option zum Umstellen der MDM-Autorität verfügbar ist.
- Es kann bis zu acht Stunden dauern, bis ein Gerät eine Verbindung mit dem Dienst herstellt, nachdem Sie auf die neue MDM-Autorität umgestellt haben.
- Stellen Sie sicher, dass allen Benutzern, die momentan hybrid verwaltet werden, eine Intune-/EMS-Lizenz zugewiesen wurde, bevor Sie die MDM-Autorität umstellen. Mit diesen Lizenzen wird sichergestellt, dass die Benutzer und ihre Geräte nach der Umstellung der MDM-Autorität von Intune standalone verwaltet werden. Weitere Informationen finden Sie unter [Zuweisen von Intune-Lizenzen zu Benutzerkonten](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Stellen Sie sicher, dass dem Konto des Administratorbenutzers eine Intune-/EMS-Lizenz zugewiesen wurde, und vergewissern Sie sich, dass sich das Konto des Administratorbenutzers in Intune anmelden kann, bevor Sie die MDM-Autorität umstellen. Für die MDM-Autorität sollte im [Azure-Portal](https://portal.azure.com) in Intune vor der Umstellung der MDM-Autorität **Auf Configuration Manager setzen** (hybrider Mandant) angezeigt werden.
- Während der Umstellung der MDM-Autorität sollte es keine wahrnehmbaren Auswirkungen auf die Endbenutzer geben. 

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Umstellen der MDM-Autorität auf Intune standalone
Die Umstellung der MDM-Autorität auf Intune standalone umfasst die folgenden allgemeinen Schritte:  
- Verwenden Sie in der Configuration Manager-Konsole die Option **MDM-Autorität auf Microsoft Intune umstellen**, um das vorhandene Microsoft Intune-Abonnement zu entfernen.
- Konfigurieren Sie im [Azure-Portal](https://portal.azure.com) die neuen Einstellungen und Apps der neuen MDM-Autorität (Intune), und stellen Sie sie bereit.
- Wenn Geräte das nächste Mal eine Verbindung mit dem Dienst herstellen, werden sie synchronisiert und erhalten die neuen Einstellungen von der neuen MDM-Autorität.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>So stellen Sie die MDM-Autorität auf Intune standalone um
1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** &gt; **Übersicht** &gt; **Clouddienste** &gt; **Microsoft Intune-Abonnement**, und löschen Sie Ihr vorhandenes Intune-Abonnement.
2. Wählen Sie **MDM-Autorität auf Microsoft Intune umstellen** aus, und klicken Sie dann auf **Weiter**.
   ![Herunterladen der APNs-Zertifikatanforderung](./media/mdm-change-delete-subscription.png)
3. Melden Sie sich bei dem Intune-Mandanten an, den Sie ursprünglich beim Festlegen der MDM-Autorität in Configuration Manager verwendet haben.
4. Klicken Sie auf **Weiter** , und schließen Sie den Assistenten ab.
5. Die MDM-Autorität ist nun auf **Microsoft Intune** festgelegt. Das Intune-Abonnement sollte nicht mehr im Knoten „Microsoft Intune-Abonnements“ der Configuration Manager-Konsole angezeigt werden. 
6. Um sicherzustellen, dass die MDM-Autorität festgelegt ist, gehen Sie folgendermaßen vor: a. Melden Sie sich [im Azure-Portal](https://portal.azure.com) unter Verwendung des Intune-Mandanten an, den Sie zuvor verwendet haben. 
    b. Wählen Sie **Weitere Dienste** > **Überwachung + Verwaltung** > **Intune** > **Geräteregistrierung**. Die MDM-Autorität wird auf dem Blatt **Übersicht** rechts oben angezeigt. 

## <a name="next-steps"></a>Nächste Schritte
Sobald die Umstellung der MDM-Autorität abgeschlossen ist, überprüfen Sie die folgenden Schritte:
- Wenn der Intune-Dienst erkennt, dass die MDM-Autorität eines Mandanten umgestellt wurde, sendet er eine Benachrichtigung an alle registrierten Geräte, damit sie beim Dienst eingecheckt und synchronisiert werden (außerhalb der regelmäßigen geplanten Eincheckvorgänge). Nach der Umstellung der MDM-Autorität für den Mandanten von hybrid auf Intune standalone stellen daher alle Geräte, die eingeschaltet und online sind, eine Verbindung mit dem Dienst her, erhalten die neue MDM-Autorität und werden zukünftig von Intune standalone verwaltet. Es gibt keine Unterbrechung bei Verwaltung und Schutz dieser Geräte.
- Geräte, die während (oder kurz nach) der Umstellung der MDM-Autorität ausgeschaltet oder offline sind, stellen unter der neuen MDM-Autorität eine Verbindung mit dem Dienst her und werden synchronisiert, sobald sie eingeschaltet werden und online sind.  
- Benutzer können schnell auf die neue MDM-Autorität umstellen, indem sie manuell einen Eincheckvorgang des Geräts beim Dienst starten. Benutzer können dies problemlos mithilfe der Unternehmensportal-App und dem Initiieren einer Überprüfung der Gerätekonformität erreichen.
- Um zu überprüfen, ob nach der Umstellung der MDM-Autorität und dem Einchecken und Synchronisieren der Geräte beim Dienst alles ordnungsgemäß funktioniert, suchen Sie im [Azure-Portal](https://portal.azure.com) nach den Geräten. Die Geräte, die zuvor von Configuration Manager (hybrid) verwaltet wurden, werden jetzt in Intune als verwaltete Geräte angezeigt.    
- Es gibt eine Übergangszeit, bis ein Gerät beim Dienst eingecheckt wird, wenn das Gerät während der Umstellung der MDM-Autorität offline war. Um sicherzustellen, dass das Gerät während dieser Übergangszeit geschützt und funktionsfähig bleibt, verbleiben die folgenden Profile bis zu sieben Tage lang (oder bis das Gerät eine Verbindung mit der neuen MDM-Autorität herstellt und die neuen Einstellungen empfängt, die die vorhandenen überschreiben) auf dem Gerät:
    - E-Mail-Profil
    - VPN-Profil
    - Zertifikatprofil
    - WLAN-Profil
    - Konfigurationsprofile
- Stellen Sie sicher, dass die neuen Einstellungen, mit denen die vorhandenen Einstellungen überschrieben werden sollen, den gleichen Namen aufweisen wie die vorherigen, damit die alten Einstellungen tatsächlich überschrieben werden. Andernfalls weisen die Geräte möglicherweise redundante Profile und Richtlinien auf.    

  > [!TIP]   
  > Es empfiehlt sich, alle Verwaltungseinstellungen und Konfigurationen sowie Bereitstellungen kurz nach Abschluss der Umstellung der MDM-Autorität zu erstellen. Dadurch wird sichergestellt, dass Geräte in der Übergangszeit geschützt und aktiv verwaltet werden.   
-  Führen Sie nach der Umstellung der MDM-Autorität die folgenden Schritte aus, um zu überprüfen, ob neue Geräte erfolgreich bei der neuen Autorität registriert werden:   
    - Registrieren eines neuen Geräts
    - Stellen Sie sicher, dass das neu registrierte Gerät im [Azure-Portal](https://portal.azure.com) angezeigt wird.
    - Führen Sie über das [Azure-Portal](https://portal.azure.com) auf dem Gerät eine Aktion aus, z.B. Remotesperre. Wenn sie erfolgreich ist, wird das Gerät durch die neue MDM-Autorität verwaltet.
- Wenn Sie Probleme mit bestimmten Geräten haben, können Sie die Registrierung der Geräte aufheben und sie erneut registrieren, damit sie so schnell wie möglich mit der neuen Autorität verbunden und von ihr verwaltet werden.