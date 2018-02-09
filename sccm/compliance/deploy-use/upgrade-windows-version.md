---
title: "Aktualisieren von Windows-Geräten auf eine neuere Version"
titleSuffix: Configuration Manager
description: "Automatisches Upgrade von Geräten, die Windows 10 Desktop oder Windows 10 Mobile ausführen, auf eine andere Edition mit Configuration Manager."
ms.custom: na
ms.date: 01/26/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: 
caps.handback.revision: 
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95e3385ad9bca9c87e48d731ffeebfa387fece65
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Aktualisieren von Windows-Geräten mit der Editionsupgraderichtlinie in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Mit der **Editionsupgraderichtlinie** können Sie Geräte, auf denen eine der folgenden Windows 10-Versionen ausgeführt wird, automatisch auf eine andere Edition aktualisieren:

- Windows 10 Desktop
- Windows 10 Mobile

Die folgenden Upgradepfade werden unterstützt:

- Von Windows 10 Pro auf Windows 10 Enterprise
- Von Windows 10 Home auf Windows 10 Education
- Von Windows 10 Mobile auf Windows 10 Mobile Enterprise

Die Geräte müssen bei Microsoft Intune registriert sein oder die Configuration Manager-Clientsoftware ausführen. Diese Richtlinie ist derzeit nicht mit PCs konform, die von einer lokalen MDM verwaltet werden.

## <a name="before-you-start"></a>Vorbereitung  
 Bevor Sie beginnen, Geräte auf die neueste Version zu aktualisieren, benötigen Sie Folgendes:  

-   Für Desktop-Editionen von Windows 10: Einen gültigen Product Key für die Installation der neuen Windows-Version auf allen Geräten, die das Ziel dieser Richtlinie sind. Dieser Product Key kann ein Mehrfachaktivierungsschüssel oder ein generischer Volumenlizenzschlüssel sein. Ein generischer Volumenlizenzschlüssel wird auch als Clientsetupschlüssel für den Schlüsselverwaltungsdienst (KMS) bezeichnet. Weitere Informationen finden Sie unter [Planen der Volumenaktivierung](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Eine Liste der KMS-Clientsetupschlüssel finden Sie im Windows Server-Aktivierungshandbuch in [Anhang A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys). <!--496871-->  

-   Für Windows 10 Mobile: Eine XML-Lizenzdatei aus dem Microsoft Volume Licensing Service Center (VLSC). Diese Datei enthält die Lizenzierungsinformationen für die neue Windows-Version auf allen Geräten, die Ziel dieser Richtlinie sind.

- Zum Verwalten dieses Richtlinientyps muss Ihnen die Configuration Manager-Sicherheitsrolle **Hauptadministrator** zugewiesen sein.

## <a name="configure-the-edition-upgrade-policy"></a>Konfigurieren der Editionsupgraderichtlinie  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Windows 10-Editionsupgrade**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Editionsupgraderichtlinie erstellen**.  

4.  Klicken Sie auf **Richtlinie erstellen**.  

5.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Editionsupgraderichtlinien**die folgenden Informationen an:  

    -   **Name**: Geben Sie einen Namen für die Editionsupgraderichtlinie ein.  

    -   **Beschreibung** (optional): Geben Sie optional eine Beschreibung für die Richtlinie ein, damit Sie sie in der Intune-Konsole besser identifizieren können.  

    -   **SKU, auf die das Gerät aktualisiert werden soll**: Wählen Sie aus der Dropdownliste die Zieleditionen von Windows 10 Desktop oder Windows 10 Mobile aus.  

    -   **Lizenzinformationen** : Wählen Sie eine Option aus:  

        -   **Product Key**: Geben Sie einen gültigen Product Key für die Zieledition von Windows 10 Desktop ein.  

            > [!NOTE]  
            >  Nach der Erstellung einer Richtlinie mit einem Product Key können Sie den Product Key später nicht mehr bearbeiten. Configuration Manager zeigt den Schlüssel aus Sicherheitsgründen verdeckt an. Um den Product Key zu ändern, müssen Sie den gesamten Schlüssel erneut eingeben.  

        -   **Lizenzdatei**: Klicken Sie auf **Durchsuchen**, um eine gültige Lizenzdatei im XML-Format auszuwählen. Configuration Manager verwendet diese Lizenzdatei, um Windows 10 Mobile-Geräte zu aktualisieren.  

6.  Schließen Sie den Assistenten ab.  


## <a name="deploy-the-edition-upgrade-policy"></a>Bereitstellen der Editionsupgraderichtlinie  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Windows 10-Editionsupgrade**.  

3.  Wählen Sie die Windows 10-Editionsupgraderichtlinie aus, die Sie bereitstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

4.  Wählen Sie zunächst im Dialogfeld **Windows 10-Editionsupgrade bereitstellen** die Sammlung aus, für die Sie die Richtlinie bereitstellen möchten. Wählen Sie den Zeitplan aus, nach dem der Client die Richtlinie bewertet, und klicken Sie dann auf **OK**. Für PCs, die mit dem Configuration Manager-Client verwaltet werden, müssen Sie die Richtlinie auf einer Gerätesammlung bereitstellen. Für PCs, die bei Intune registriert sind, können Sie die Richtlinie für eine Benutzer- oder Gerätesammlung bereitstellen. 



## <a name="next-steps"></a>Nächste Schritte

Überwachen Sie diese Bereitstellung über den Knoten **Bereitstellungen** des Arbeitsbereichs **Überwachung**. Möglicherweise werden Fehler angezeigt, die auf eine erfolglose Bereitstellung hinweisen, zum Beispiel:
- **Für dieses Gerät nicht anwendbar**
- **Fehler bei der Konvertierung des Datentyps**

Diese Fehler bedeuten allerdings nicht, dass die Bereitstellung gescheitert ist. Vergewissern Sie sich am Ziel-PC, dass das Upgrade erfolgreich durchgeführt wurde.

Sobald der Client die gewünschte Richtlinie ausgewertet hat, wird sie innerhalb von zwei Stunden neu gestartet, um das Upgrade anzuwenden. Stellen Sie sicher, dass Sie jeden Benutzer informieren, dem Sie die Richtlinie bereitstellen, oder planen Sie die Ausführung der Richtlinie außerhalb der Arbeitsstunden der Benutzer.

Wenn der folgende Fehler in der Datei **DcmWmiProvider.log** auf dem Client auftritt, überprüfen Sie, ob Sie den richtigen Schlüssel für Ihr Aktivierungsszenario verwenden. Weitere Informationen finden Sie im Abschnitt [Bevor Sie beginnen](#before-you-start). Wenn Sie einen Schlüsselverwaltungsdienst für die Aktivierung nutzen, stellen Sie sicher, dass Sie einen [KMS-Clientsetupschlüssel](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) verwenden.  <!-- 496871 -->   

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`
