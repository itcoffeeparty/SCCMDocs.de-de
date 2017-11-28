---
title: "Umstellen der MDM-Autorität für bestimmte Benutzer (gemischte MDM-Autorität)"
titleSuffix: Configuration Manager
description: "Erfahren Sie, wie Sie die MDM-Autorität von einer MDM-Hybridlösung auf eigenständiges Intune umstellen."
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/14/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 31d1d84c225d041f644669f0d3279e6bcd3f75ba
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Umstellen der MDM-Autorität für bestimmte Benutzer (gemischte MDM-Autorität) 

*Gilt für: System Center Configuration Manager (Current Branch)*    

Sie können eine gemischte MDM-Autorität im selben Mandanten konfigurieren, indem Sie einige Benutzer auswählen, die in Intune verwaltet werden sollen, und andere, die mit einer MDM-Hybridlösung (in Configuration Manager integriertes Intune) verwaltet werden sollen. Dieses Thema enthält Informationen dazu, wie Sie mit dem Verschieben von Benutzern in eigenständiges Intune beginnen können, und geht davon aus, dass Sie die folgenden Schritte ausgeführt haben:
- Sie haben das Datenimport-Tool verwendet, um [(optional) Configuration Manager-Objekte in Intune zu importieren](migrate-import-data.md).
- Sie haben [Intune für die Benutzermigration vorbereitet](migrate-prepare-intune.md), um sicherzustellen, dass Benutzer und ihre Geräte nach der Migration weiterhin verwaltet werden.

> [!Note]    
> Wenn Sie entscheiden, Ihren Mandanten vollständig zurückzusetzen, wodurch alle Richtlinien, Anwendungen und Geräteregistrierungen entfernt werden, wenden Sie sich zwecks Unterstützung an den Support.

Migrierte Benutzer und ihre Geräte werden in Intune verwaltet. Andere Geräte werden weiterhin in Configuration Manager verwaltet. Sie beginnen mit einer kleinen Testbenutzergruppe, um sicherzustellen, dass alles wie erwartet funktioniert. Anschließend migrieren Sie schrittweise weitere Benutzergruppen, bis Sie bereit sind, die MDM-Autorität auf Mandantenebene von Configuration Manager auf eigenständiges Intune umzustellen. 

## <a name="things-to-know-before-you-migrate-users"></a>Was Sie vor dem Migrieren von Benutzern wissen sollten
- Während der gestaffelten Migration gelten alle bestehenden MDM-Richtlinien oder -Anwendungen in Configuration Manager weiterhin für hybride MDM-Geräte.
- Benutzer werden einer AAD-Gruppe hinzugefügt, die Sie als Migrationsgruppe festlegen. Alle Geräte, die den Benutzern der Migrationsgruppe zugeordnet sind, werden in Intune verwaltet.
- Wenn Geräte zur AAD-Gruppe hinzugefügt werden, werden sie ignoriert, es sei denn, es handelt sich um ein Gerät ohne zugeordneten Benutzer.
- Nicht zu einer AAD-Gruppe gehörende Benutzer, die für die Migration markiert ist, erben automatisch die MDM-Autorität auf Mandantenebene (Configuration Manager).
- Wenn Sie einen Benutzer zu Intune migrieren, werden der Benutzer und Geräte nach ca. 15 Minuten in Intune im Azure-Portal angezeigt.  
- Wenn Sie Benutzer zu eigenständigem Intune migrieren, verwalten Sie weiterhin die folgenden Einstellungen in Configuration Manager sowohl für eigenständiges Intune als auch für hybride MDM-Geräte:
    - [Apple Push Notification Service-Zertifikat](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)
    - [Programm zur Geräteregistrierung](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)
    - Registrierungsprofile
    - [Lizenzen für Apple Volume Purchase Program](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)
    - Unternehmensbezeichner 
    - [Codesignaturzertifikate](/sccm/mdm/deploy-use/enroll-hybrid-windows)
    - [Gerätekategorien](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)
    - [Registrierungs-Manager](/sccm/mdm/plan-design/device-enrollment-methods)
    - Geschäftsbedingungen
    - Windows SLKs
    - Branding des Unternehmensportals    
      
> [!Important]    
  > Bearbeiten Sie die Richtlinien auf Mandantenebene weiterhin in der Configuration Manager-Konsole. Nachdem Sie [Ihre MDM-Autorität auf Mandantenebene](change-mdm-authority.md) auf Intune umgestellt haben, verwalten Sie diese Richtlinien in Intune in Azure. 
- Wir empfehlen, keine Benutzerkonten zu migrieren, die in Configuration Manager als Geräteregistrierungs-Manager hinzugefügt wurden. Wenn Sie später Ihre MDM-Autorität auf Mandantenebene auf Intune umstellen, werden diese Benutzerkonten ordnungsgemäß migriert. Wenn Sie das Benutzerkonto des Geräteregistrierungs-Managers vor der Umstellung der MDM-Autorität auf Mandantenebene migrieren, müssen Sie den Benutzer manuell als Geräteregistrierungs-Manager in Intune in Azure hinzufügen. Geräte, die mit einem Geräteregistrierungs-Manager registriert werden, lassen sich jedoch nicht erfolgreich migrieren. Sie müssen den Support bitten, diese Geräte zu migrieren. Weitere Informationen finden Sie unter [Hinzufügen eines Geräteregistrierungs-Managers](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).
- Geräte, die mit einem Geräteregistrierungs-Manager registriert wurden, und Geräte, denen keine Benutzer zugeordnet sind, werden nicht zur neuen MDM-Autorität migriert. Bei diesen Geräten müssen Sie den Support einschalten, der Ihnen bei den einzelnen Geräten hilft. Lassen Sie den Support keine Zurücksetzung der MDM-Autorität ausführen, da ansonsten die Daten in Intune gelöscht werden. Das [Umstellen der MDM-Autorität](migrate-change-mdm-authority.md) muss über die Configuration Manager-Konsole erfolgen.

## <a name="migrate-users-to-intune"></a>Migrieren von Benutzern zu Intune
Um zu testen, ob Ihre Intune-Konfigurationen wie erwartet funktionieren, migrieren Sie zunächst eine kleine Gruppe von Benutzern und deren Geräte. Nachdem Sie bestätigt haben, dass alles wie erwartet funktioniert, können Sie weitere AAD-Gruppen mit mehr Benutzern und ihren Geräten migrieren.

## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Migrieren einer Testbenutzergruppe zu eigenständigem Intune
Die Geräte für die Benutzer in der Sammlung im Zusammenhang mit dem Intune-Abonnement können sich bei der MDM-Hybridlösung registrieren. Wenn Sie einen Benutzer aus der Sammlung entfernen, werden seine registrierten Geräte zu eigenständigem Intune migriert, sofern dem Benutzer eine Intune-Lizenz zugewiesen wurde. Wenn Sie Benutzern, die Sie migrieren möchten, noch keine Lizenzen zugewiesen haben, siehe [Zuweisen von Intune-Lizenzen zu Ihren Benutzerkonten](https://docs.microsoft.com/intune/licenses-assign). In der Sammlung für das Intune-Abonnement können Sie Benutzersammlungen von Ihrer Hauptsammlung ausschließen, um die Benutzer in der ausgeschlossenen Sammlung zu migrieren. 

Im folgenden Beispiel enthält die Sammlung „Hybridbenutzer“ alle Mitglieder der Sammlung „Alle Benutzer“. Dies ermöglicht allen Benutzern, ein Gerät in der MDM-Hybridlösung zu registrieren. Um Benutzer zu eigenständigem Intune zu migrieren, wählen Sie „Sammlungen ausschließen“ aus und fügen eine Sammlung mit den zu migrierenden Benutzern hinzu. Wenn Sie bereit sind, weitere Benutzer zu migrieren, können Sie weitere ausgeschlossene Sammlungen hinzufügen, die diese Benutzer enthalten. 

![Ausschließen von Sammlungen](../media/migrate-excludecollections.png)

> [!Note] 
> Wenn Sie die Sammlung **Alle Benutzer** für das Intune-Abonnement ausgewählt haben, dürfen Sie keine Regel zum Ausschließen von Sammlungen hinzufügen. Erstellen Sie basierend auf der Sammlung **Alle Benutzer** eine neue Sammlung. Überprüfen Sie, ob die Sammlung die erwarteten Benutzer enthält. Bearbeiten Sie dann das Intune-Abonnement, um die neue Sammlung zu verwenden. Sie können Benutzersammlungen aus der neuen Sammlung ausschließen, um Benutzer zu migrieren. 

Um eine Testbenutzergruppe zu Intune zu migrieren, erstellen Sie eine Benutzersammlung, die die zu migrierenden Benutzer enthält. Schließen Sie dann die Benutzersammlung aus der für das Intune-Abonnement verwendeten Sammlung aus.   

Das folgende Diagramm bietet einen Überblick über die Funktionsweise der Benutzermigration.

 ![Gemischte Autorität: Übersicht](../media/migrate-mixedauthority.svg)

1. Stellen Sie sicher, dass der Benutzer über eine Intune-/EMS-Lizenz verfügt. 
2. Erstellen Sie eine Sammlung, die von der Sammlung für das Intune-Abonnement ausgeschlossen werden soll. Bei diesem Beispiel enthält die Sammlung **Alle Hybridbenutzer** eine Regel zum Ausschließen von Benutzern in der Sammlung **Migrationspilot**. **Benutzer1** ist Mitglied der Sammlung **Migrationspilot** und wird von der Sammlung **Alle Hybridbenutzer** ausgeschlossen. 
3. Die Geräte von **Benutzer1** werden jetzt mithilfe von Intune im Azure-Portal verwaltet. 
4. Alle anderen Geräte können weiter über die Configuration Manager-Konsole verwaltet werden. 

## <a name="verify-intune-standalone-functionality"></a>Überprüfen der Funktionalität von eigenständigem Intune
Nachdem Sie eine kleine Benutzergruppe migriert haben, vergewissern Sie sich, dass die Geräte der Benutzer in Intune aufgelistet sind. Wechseln Sie zum Blatt **Geräte**, und wählen Sie **Alle Geräte** aus. 

Überprüfen Sie anschließend, ob Ihre Richtlinien, Profile, Anwendungen usw. wie erwartet auf den Benutzergeräten funktionieren.

## <a name="migrate-additional-users"></a>Migrieren zusätzliche Benutzer
Nachdem Sie sich vergewissert haben, dass eigenständiges Intune wie erwartet funktioniert, können Sie mit der Migration weiterer Benutzer beginnen. Ebenso wie Sie eine Sammlung mit einer Reihe von Testbenutzern erstellt haben, erstellen Sie Sammlungen, die Benutzer enthalten, die migriert werden sollen. Schließen Sie diese Sammlungen von der Sammlung aus, die dem Intune- Abonnement zugeordnet ist. Weitere Informationen finden Sie unter [Ihrem Intune-Abonnement zugeordnete Sammlungen](#collection-associated-with-your-intune-subscription).

## <a name="next-steps"></a>Nächste Schritte
Nachdem Sie Benutzer migriert und die Intune-Funktionalität getestet haben, prüfen Sie, ob Sie zum [Umstellen der MDM-Autorität](migrate-change-mdm-authority.md) Ihres Intune-Mandanten von Configuration Manager auf Intune bereit sind. 