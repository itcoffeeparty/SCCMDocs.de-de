---
title: Konfigurieren der Remotesteuerung | Microsoft Docs
description: Richten Sie die Remotesteuerung in System Center Configuration Manager ein.
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 88828e68bc4aff216e83807ea8288c7d42c60cbd
ms.openlocfilehash: cbfa9dc6cb37518c0a561700272cc882b0041350


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Konfigurieren der Remotesteuerung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

 In diesem Verfahren wird die Konfiguration der Clientstandardeinstellungen für die Remotesteuerung beschrieben. Es gilt für alle Computer in der Hierarchie. Wenn diese Einstellungen nur auf manche Computer angewendet werden sollen, erstellen Sie eine benutzerdefinierte Geräteclienteinstellung und weisen sie einer Sammlung mit den Computern zu, die Sie in einer Remotesteuerungssitzung verwenden möchten. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md). 

Für die Verwendung der Remoteunterstützung oder des Remotedesktops müssen sie auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, installiert und konfiguriert sein. Weitere Informationen zum Installieren und Konfigurieren der Remoteunterstützung oder des Remotedesktops finden Sie in der Windows-Dokumentation.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>So aktivieren Sie die Remotesteuerung und konfigurieren die Clienteinstellungen  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie im Dialogfeld **Standard** die Option **Remotetools** aus.  

6.  Konfigurieren Sie die Remotesteuerungs-, Remoteunterstützungs- und Remotedesktop-Clienteinstellungen. Eine Liste der Remotetools-Clienteinstellungen, die Sie konfigurieren können, finden Sie unter [Remotetools](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

    Sie können den Firmennamen ändern, der im Dialogfeld **ConfigMgr-Remotesteuerung** angezeigt wird, indem Sie in den Clienteinstellungen **Computer-Agent** einen Wert für **Im Softwarecenter angezeigter Organisationsname** konfigurieren.  

 Die Clientcomputer werden beim nächsten Download der Clientrichtlinien mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Abrufens von Richtlinien für einen einzelnen Client finden Sie unter [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Dec16_HO1-->


