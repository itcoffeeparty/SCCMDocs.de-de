---
title: "Umstellen der MDM-Autorität für bestimmte Benutzer (gemischte MDM-Autorität)"
titleSuffix: Configuration Manager
description: "Erfahren Sie, wie Sie die MDM-Autorität von einer MDM-Hybridlösung auf eigenständiges Intune umstellen."
keywords: 
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 643b33810c2862e2d1c602bfe941c36605ad2631
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2017
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Umstellen der MDM-Autorität für bestimmte Benutzer (gemischte MDM-Autorität) 

*Gilt für: System Center Configuration Manager (Current Branch)*    

Sie können eine gemischte MDM-Autorität im selben Mandanten konfigurieren, indem Sie einige Benutzer auswählen, die in Intune verwaltet werden sollen, und andere, die mit einer MDM-Hybridlösung (in Configuration Manager integriertes Intune) verwaltet werden sollen. Dieser Artikel enthält Informationen dazu, wie Sie die Migration von Benutzern zur eigenständigen Intune-Version in die Wege leiten können. Es wird davon ausgegangen, dass Sie die folgenden Schritte ausgeführt haben:
- Sie haben das Datenimport-Tool verwendet, um [(optional) Configuration Manager-Objekte in Intune zu importieren](migrate-import-data.md).
- Sie haben [Intune für die Benutzermigration vorbereitet](migrate-prepare-intune.md), um sicherzustellen, dass Benutzer und ihre Geräte nach der Migration weiterhin verwaltet werden.

> [!Note]    
> Wenn Sie entscheiden, Ihren Mandanten vollständig zurückzusetzen, wodurch alle Richtlinien, Apps und Geräteregistrierungen entfernt werden, wenden Sie sich zwecks Unterstützung an den Support.

Migrierte Benutzer und ihre Geräte werden in Intune verwaltet. Andere Geräte werden weiterhin in Configuration Manager verwaltet. Sie beginnen mit einer kleinen Testbenutzergruppe, um sicherzustellen, dass alles wie erwartet funktioniert. Anschließend migrieren Sie schrittweise weitere Benutzergruppen, bis Sie bereit sind, die MDM-Autorität auf Mandantenebene von Configuration Manager auf die eigenständige Intune-Version umzustellen. 

## <a name="things-to-know-before-you-migrate-users"></a>Was Sie vor dem Migrieren von Benutzern wissen sollten
- Während der gestaffelten Migration gelten alle bestehenden MDM-Richtlinien oder -Anwendungen in Configuration Manager weiterhin für hybride MDM-Geräte.
- Die Geräte für die Benutzer in der Sammlung im Zusammenhang mit dem Intune-Abonnement können sich bei der MDM-Hybridlösung registrieren. Alle Geräte, die mit nicht in der Sammlung enthaltenen Benutzern verknüpft sind, werden in Intune verwaltet, sofern der Benutzer über eine Intune-/EMS-Lizenz verfügt. 
- Wenn Sie einen Benutzer nach Intune migrieren, werden der Benutzer und die Geräte nach ca. 15 Minuten in Intune im Azure-Portal angezeigt.  
- Wenn Sie Benutzer zu eigenständigem Intune migrieren, verwalten Sie weiterhin die folgenden Einstellungen in Configuration Manager sowohl für eigenständiges Intune als auch für hybride MDM-Geräte:
    - [Apple Push Notification Service-Zertifikat](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)
    - [Programm zur Geräteregistrierung](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)
    - Registrierungsprofile
    - [Lizenzen für Apple Volume Purchase Program](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)
    - Unternehmensbezeichner 
    - [Codesignaturzertifikate](/sccm/mdm/deploy-use/enroll-hybrid-windows)
    - [Gerätekategorien](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)
    - [Registrierungs-Manager](/sccm/mdm/plan-design/device-enrollment-methods)
    - Terms and conditions
    - Windows SLKs
    - Branding des Unternehmensportals    
      
  > [!Important]    
  > Bearbeiten Sie die Richtlinien auf Mandantenebene weiterhin in der Configuration Manager-Konsole. Nachdem Sie [Ihre MDM-Autorität auf Mandantenebene](change-mdm-authority.md) auf Intune umgestellt haben, verwalten Sie diese Richtlinien in Intune in Azure. 
- Wir empfehlen, keine Benutzerkonten zu migrieren, die in Configuration Manager als Geräteregistrierungs-Manager hinzugefügt wurden. Wenn Sie später Ihre MDM-Autorität auf Mandantenebene auf Intune umstellen, werden diese Benutzerkonten ordnungsgemäß migriert. Wenn Sie das Benutzerkonto des Geräteregistrierungs-Managers vor der Umstellung der MDM-Autorität auf Mandantenebene migrieren, müssen Sie den Benutzer manuell als Geräteregistrierungs-Manager in Intune in Azure hinzufügen. Geräte, die mit einem Geräteregistrierungs-Manager registriert werden, lassen sich jedoch nicht erfolgreich migrieren. Sie müssen den Support bitten, diese Geräte zu migrieren. Weitere Informationen finden Sie unter [Hinzufügen eines Geräteregistrierungs-Managers](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).
- Geräte, die mit einem Geräteregistrierungs-Manager registriert wurden, und Geräte ohne [Benutzeraffinität](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) werden nicht automatisch zur neuen MDM-Autorität migriert. Informationen zum Wechseln der Verwaltungsautorität für diese MDM-Geräte finden Sie unter [Migrieren von Geräten ohne Benutzeraffinität](#migrate-devices-without-user-affinity).

## <a name="migrate-users-to-intune"></a>Migrieren von Benutzern zu Intune
Um zu testen, ob Ihre Intune-Konfigurationen wie erwartet funktionieren, migrieren Sie zunächst eine kleine Gruppe von Benutzern und deren Geräte. Nachdem Sie bestätigt haben, dass alles wie erwartet funktioniert, können Sie weitere AAD-Gruppen mit mehr Benutzern und ihren Geräten migrieren.

## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Migrieren einer Testbenutzergruppe zu eigenständigem Intune
Die Geräte für die Benutzer in der Sammlung im Zusammenhang mit dem Intune-Abonnement können sich bei der MDM-Hybridlösung registrieren. Wenn Sie einen Benutzer aus der Sammlung entfernen, werden seine registrierten Geräte zu eigenständigem Intune migriert, sofern dem Benutzer eine Intune-Lizenz zugewiesen wurde. Wenn Sie Benutzern, die Sie migrieren möchten, noch keine Lizenzen zugewiesen haben, siehe [Zuweisen von Intune-Lizenzen zu Ihren Benutzerkonten](https://docs.microsoft.com/intune/licenses-assign). In der Sammlung für das Intune-Abonnement können Sie Benutzersammlungen von Ihrer Hauptsammlung ausschließen, um die Benutzer in der ausgeschlossenen Sammlung zu migrieren. 

Im folgenden Beispiel enthält die Sammlung „Hybridbenutzer“ alle Mitglieder der Sammlung „Alle Benutzer“. Dies ermöglicht allen Benutzern, ein Gerät in der MDM-Hybridlösung zu registrieren. Um Benutzer zu eigenständigem Intune zu migrieren, wählen Sie „Sammlungen ausschließen“ aus und fügen eine Sammlung mit den zu migrierenden Benutzern hinzu. Wenn Sie bereit sind, weitere Benutzer zu migrieren, können Sie weitere ausgeschlossene Sammlungen hinzufügen, die diese Benutzer enthalten. 

![Ausschließen von Sammlungen](../media/migrate-excludecollections.png)

> [!Note] 
> Wenn Sie die Sammlung **Alle Benutzer** für das Intune-Abonnement ausgewählt haben, dürfen Sie keine Regel zum Ausschließen von Sammlungen hinzufügen. Erstellen Sie basierend auf der Sammlung **Alle Benutzer** eine neue Sammlung. Überprüfen Sie, ob die Sammlung die erwarteten Benutzer enthält. Bearbeiten Sie dann das Intune-Abonnement, um die neue Sammlung zu verwenden. Sie können Benutzersammlungen aus der neuen Sammlung ausschließen, um Benutzer zu migrieren. 

Um eine Testbenutzergruppe nach Intune zu migrieren, erstellen Sie eine Benutzersammlung, die die zu migrierenden Benutzer enthält. Schließen Sie dann die Benutzersammlung aus der für das Intune-Abonnement verwendeten Sammlung aus.   

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

## <a name="migrate-devices-without-user-affinity"></a>Migrieren von Geräten ohne Benutzeraffinität
Geräte, die mit einem Geräteregistrierungs-Manager registriert wurden, und Geräte ohne [Benutzeraffinität](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) werden nicht automatisch zur neuen MDM-Autorität migriert. Mit dem PowerShell-Cmdlet *Switch-MdmDeviceAuthority* können Sie in den folgenden Szenarien zwischen Intune- und Configuration Manager-Verwaltungsautoritäten wechseln: 

-   Szenario 1: Verwenden Sie das Cmdlet *Switch-MdmDeviceAuthority*, um ausgewählte Geräte zu migrieren und sicherzustellen, dass sie mithilfe von Intune in Azure verwaltet werden können. Anschließend können Sie zur Durchführung der Gerätemigration [die MDM-Autorität auf Intune für den Mandanten umstellen](migrate-change-mdm-authority.md). 
-   Szenario 2: Wenn Sie die MDM-Autorität auf Intune für den Mandanten umstellen möchten, können Sie die folgenden Aktionen durchführen, um Ihre Geräte ohne Benutzeraffinität zu migrieren:
    - Bevor Sie [die MDM-Autorität auf Intune für den Mandanten](migrate-change-mdm-authority.md) umstellen, stellen Sie mithilfe des Cmdlets die MDM-Autorität für Ihre Geräte ohne Benutzeraffinität um.    
    - Wenden Sie sich telefonisch an den Support, um die Geräte ohne Benutzeraffinität wechseln zu lassen, nachdem Sie die MDM-Autorität für den Mandanten auf Intune umgestellt haben.

Um die Verwaltungsautorität für diese MDM-Geräte zu wechseln, können Sie mit dem Cmdlet *Switch-MdmDeviceAuthority* zwischen Intune- und Configuration Manager-Verwaltungsautoritäten wechseln. 

### <a name="cmdlet-switch-mdmdeviceauthority"></a>Cmdlet *Switch-MdmDeviceAuthority*

#### <a name="synopsis"></a>ZUSAMMENFASSUNG
Mit dem Cmdlet wird die Verwaltungsautorität von MDM-Geräten ohne Benutzeraffinität (z.B. massenregistrierten Geräten) gewechselt. Das Cmdlet wechselt die Verwaltungsautoritäten zwischen Intune- und Configuration Manager-Verwaltungsautoritäten für die angegebenen Geräte, wenn Sie das Cmdlet ausführen.

### <a name="syntax"></a>SYNTAX
`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>PARAMETER
``` powershell
-Credential <PSCredential>
Credential for Intune Tenant Admin or Service Admin account to use when switching device management authorities. The user is prompted for credentials if the parameter is not specified.

-DeviceIds <Guid[]>
The ids of the MDM devices that need to have their management authority switched. The device ids are unique identifiers for the devices displayed by the Configuration Manager console.

-Force [<SwitchParameter>]
Specify parameter to disable the Should Continue prompt.<br>
 
-LogFilePath <string>
Path to log file location.
 
-LoggingLevel <SourceLevels>
The log level used to determine the type of logs that need to be written to the log file.
 
The following are the possible values for LoggingLevel:

  - ActivityTracing
  - All
  - Critical
  - Error
  - Information
  - Off
  - Verbose
  - Warning
 
-Confirm [<SwitchParameter>]
Prompts you for confirmation before executing the command.
 
-WhatIf [<SwitchParameter>]
Describes what would happen if you executed the command without actually executing the command.
 
<CommonParameters>
This cmdlet supports the common parameters: Verbose, Debug,
ErrorAction, ErrorVariable, WarningAction, WarningVariable,
OutBuffer, PipelineVariable, and OutVariable. For more information, see
[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).
```

### <a name="example-1"></a>Beispiel 1

``` powershell
C:\PS>Switch-MdmDeviceAuthority -Credential $creds -DeviceIds $deviceIds
 
  DeviceId       : 62e6ea43-18f8-4278-bcd4-a4baed2c6d24
  Success        : True
  FailureReason  :
  NewAuthority   : Intune
  CompletionTime : 11/15/2017 8:00:11 PM
 
Description
 
-----------
 
Successfully switched the management authority of the device from Configuration Manager to Intune.
```
### <a name="remarks"></a>HINWEISE
``` powershell
To see the examples, type: "get-help Switch-MdmDeviceAuthority -examples".
For more information, type: "get-help Switch-MdmDeviceAuthority -detailed".
For technical information, type: "get-help Switch-MdmDeviceAuthority -full".
For online help, type: "get-help Switch-MdmDeviceAuthority -online".
```

## <a name="next-steps"></a>Nächste Schritte
Nachdem Sie Benutzer migriert und die Intune-Funktionalität getestet haben, prüfen Sie, ob Sie zum [Umstellen der MDM-Autorität](migrate-change-mdm-authority.md) Ihres Intune-Mandanten von Configuration Manager auf Intune bereit sind. 