---
title: Vorbereiten von Intune für die Benutzermigration
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Intune in Azure auf die Migration von Benutzern aus einer MDM-Hybridlösung vorbereiten.
keywords: ''
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: ''
ms.technology: ''
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.openlocfilehash: 8d636f2c46f3fa14fbc76a605d2cf55a2c0375c6
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="prepare-intune-for-user-migration"></a>Vorbereiten von Intune für die Benutzermigration 

*Gilt für: System Center Configuration Manager (Current Branch)*    

Bevor Sie Benutzer aus einer MDM-Hybridlösung (in Configuration Manager integriertes Intune) in eine eigenständige Intune-Lösung migrieren, müssen Sie Schritte zur Vorbereitung von Intune unternehmen. Anhand dieser Schritte können Sie sicherstellen, dass Ihre migrierten Benutzer und deren Geräte weiterhin verwaltet werden. Wenn Sie diese Schritte durchführen und die Migration zu Intune starten, sollte dies von den Benutzern unbemerkt erfolgen.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Beheben von während der Sammlung und des Imports von Daten gefundenen Problemen
Wenn Sie den Prozess zum [Importieren von Configuration Manager-Daten in Microsoft Intune](migrate-import-data.md) durchlaufen haben, hat Ihnen das Datenimport-Tool von Intune eine Übersicht über alle Objekte geliefert, die es nicht importieren konnte. Einige der typischen Probleme, auf die Sie wahrscheinlich gestoßen sind, sowie Schritte, die Sie unternehmen können, um das Problem in Intune zu beheben, sind in der folgenden Tabelle aufgelistet: 

|Problem  |Reparieren  |
|---------|---------|
|Sammlungen, die auf einer direkten oder komplexen Mitgliedschaft basieren, werden nicht automatisch migriert.|Sie müssen Azure Active Directory-Gruppen (AAD) in Azure erstellen, um die Sammlung zu ersetzen, die nicht importiert wurde. Anschließend müssen Sie das Objekt der Gruppe zuweisen.|
|Richtlinien nicht importierbar |Sie müssen die Richtlinie in Intune neu erstellen.|
|Bereitstellung für ein Objekt nicht importiert|Sie müssen das Objekt der Gruppe zuweisen. Die Gruppe muss dieselben Benutzer aus der Sammlung für die Bereitstellung enthalten.|

## <a name="create-intune-objects"></a>Erstellen von Intune-Objekten 
Wenn Sie den Prozess zum [Importieren von Configuration Manager-Daten in Microsoft Intune](migrate-import-data.md) durchlaufen und Probleme während des Importvorgangs behoben haben, müssen Sie überprüfen, ob die importierten Objekte ordnungsgemäß konfiguriert sind. Erstellen Sie außerdem alle zusätzlichen Objekte (Richtlinien, Profile, Anwendungen usw.) in Intune, die Sie in Ihrer Organisation benötigen. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Zuweisen von Intune-Lizenzen zu migrierten Benutzern
In Configuration Manager fügen Sie dem Intune-Abonnement eine Sammlung hinzu, und die Mitglieder der Sammlung haben die Möglichkeit, ihre Geräte zu registrieren. Während eine Intune-Lizenz für registrierte Geräte reserviert ist, sind diese Lizenzen nicht spezifisch dem Benutzer oder Gerät zugeordnet. Beispielsweise finden Sie in AAD keine Intune-Lizenz für einen Benutzer, der über ein registriertes Gerät verfügt. In eigenständigem Intune müssen Sie jedoch für jeden Benutzer eine Intune-Lizenz konfigurieren. Sie müssen dies tun, BEVOR Sie einen Benutzer zu eigenständigem Intune migrieren. Dadurch wird sichergestellt, dass die Benutzer und ihre Geräte nach der Umstellung der MDM-Autorität von Intune verwaltet werden. Weitere Informationen finden Sie unter [Zuweisen von Intune-Lizenzen zu Benutzerkonten](https://docs.microsoft.com/intune/licenses-assign). 

## <a name="verify-intune-user-groups"></a>Überprüfen von Intune-Benutzergruppen
Ihre Benutzer und Gruppen sind wahrscheinlich bereits im AAD vorhanden, da Sie die Verzeichnissynchronisierung konfiguriert haben. Um sicherzustellen, dass Ihre Benutzer der richtigen Benutzergruppe angehören, empfehlen wir Ihnen, Ihre Intune-Benutzergruppen zu überprüfen. Sie ordnen diesen Gruppen Richtlinien, Profile, Apps usw. zu. Stellen Sie sicher, dass die Benutzer, die Sie zu eigenständigem Intune migrieren, zu den richtigen Gruppen gehören. 

## <a name="configure-role-based-administration-control-rbac"></a>Konfigurieren der rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC)
Konfigurieren Sie im Rahmen der Migration alle notwendigen RBAC-Rollen in Intune, und ordnen Sie diesen Rollen Benutzer zu. Beachten Sie, dass es Unterschiede bei der RBAC in Configuration Manager und Intune gibt, wie z. B. das Eingrenzen von Ressourcen. Einzelheiten finden Sie unter [Rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) mit Intune](https://docs.microsoft.com/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Zuweisen von Apps und Richtlinien zu AAD-Gruppen
Wenn Sie die Phase [Importieren von Configuration Manager-Daten in Microsoft Intune](migrate-import-data.md) des Migrationsprozesses durchlaufen haben, um verschiedene Configuration Manager-Objekte in Intune zu migrieren, sind viele Ihrer Objekte möglicherweise bereits AAD-Gruppen zugeordnet. Allerdings sollten Sie sicherstellen, dass alle Objekte (Apps, Richtlinien, Profile usw.) den richtigen AAD-Gruppen zugeordnet sind. Wenn Sie Objekte richtig zuordnen, werden die Geräte des Benutzers automatisch konfiguriert, nachdem der Benutzer migriert wurde, und die Migration sollte für Benutzer unbemerkt erfolgen. Einzelheiten zur Zuordnung der Objekte zu einer AAD-Gruppe finden Sie in den folgenden Artikeln: 
- [Zuweisen von Richtlinien](https://docs.microsoft.com/intune/get-started-policies) 
- [Zuweisen von Profilen](https://docs.microsoft.com/intune/device-profile-assign) 
- [Zuweisen von Apps](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Richtlinien für Geschäftsbedingungen
Genau wie andere Richtlinien auf Mandantenebene werden auch die Richtlinien für Geschäftsbedingungen automatisch zu Intune migriert, sobald die gemischte Autorität für Ihren Mandanten aktiviert ist.  Sie müssen die Geschäftsbedingungen jedoch einer Gruppe zuordnen, die migrierte Benutzer enthält. Dadurch können Sie genau über die Akzeptanz bei migrierten Benutzern berichten. Zudem können Sie sicherstellen, dass die Geschäftsbedingungen für künftige Aktualisierungen von Geschäftsbedingungen oder Geräteregistrierungen richtig abgestimmt sind. Benutzer müssen die Bedingungen nicht erneut akzeptieren, es sei denn, es werden Änderungen an der Richtlinie in der Configuration Manager-Konsole vorgenommen. Weitere Informationen finden Sie unter [Zuweisen von Geschäftsbedingungen](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Konfigurieren des Exchange Connectors
Wenn Sie Exchange verwenden und in Configuration Manager über einen lokalen Exchange Connector verfügen, müssen Sie [den lokalen Exchange Connector in Intune konfigurieren](https://docs.microsoft.com/intune/exchange-connector-install). Beachten Sie auch die Informationen in den folgenden Abschnitten, um die Migration zum Intune Exchange Connector durchzuführen und sicherzustellen, dass der bedingte Zugriff nach der Migration ordnungsgemäß funktioniert.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>PowerShell-Skripts für die Migration zum Intune Exchange Connector 
Es sind PowerShell-Skripts verfügbar, die Sie bei der Vorbereitung der Migration Ihrer Exchange-Geräte vom Configuration Manager Exchange Connector zum Intune Exchange Connector unterstützen. Die Ausführung dieser Skripts ist optional. Allerdings wird deren Ausführung empfohlen, um inaktive Geräte, die Intune an der Erkennung nicht benötigter Geräte hindern, aus Exchange zu entfernen. Durch die Ausführung der Skripts wird sichergestellt, dass die über Exchange erkannten Geräte mit den bei Intune registrierten Geräten so reibungslos wie möglich zusammengeführt werden können. Führen Sie vor der Einrichtung des Intune Exchange Connectors diese Skripts aus. Die PowerShell-Skripts sind Bestandteil der Intune-Datenimporterinstallation, mit denen Sie im nächsten Artikel [Configuration Manager-Daten in Microsoft Intune importieren](migrate-import-data.md). Um weitere Informationen zu erhalten und die Skripts herunterzuladen, besuchen Sie die GitHub-Seite [Microsoft Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer) (Microsoft Intune-Datenimporter).

### <a name="steps-to-ensure-conditional-access-works-properly-after-user-migration"></a>Schritte zum Prüfen des bedingten Zugriffs nach der Benutzermigration
Damit der bedingte Zugriff nach der Migration von Benutzern ordnungsgemäß funktioniert und um sicherzustellen, dass Ihre Benutzer weiterhin Zugriff auf ihren E-Mail-Server haben, stellen Sie sicher, dass Folgendes zutrifft:
- Wenn die Exchange ActiveSync-Standardeinstellung für die Zugriffsebene (DefaultAccessLevel) auf „Blockieren“ oder „Quarantäne“ festgelegt ist, verlieren Geräte möglicherweise den Zugriff auf E-Mails. 
- Wenn der Exchange Connector in Configuration Manager installiert ist und die Einstellung **Zugriffsebene bei nicht durch eine Regel verwalteten mobilen Geräten** den Wert **Zugriff erlauben** hat, müssen Sie den [lokalen Exchange Connector](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) in Intune installieren, bevor Sie Benutzer migrieren. Konfigurieren Sie die Standardeinstellung für die Zugriffsebene in Intune auf dem Blatt **Lokales Exchange** in **Erweiterte Zugriffseinstellungen für Exchange ActiveSync**. Weitere Informationen finden Sie unter [Konfigurieren des lokalen Exchange-Zugriffs](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Verwenden Sie die gleiche Konfiguration für beide Connectors. Der zuletzt konfigurierte Connector überschreibt die zuvor vom anderen Connector geschriebenen ActiveSync-Organisationseinstellungen. Wenn Sie die Connectors unterschiedlich konfigurieren, kann es zu unerwarteten Änderungen beim bedingten Zugriff kommen.
- Entfernen Sie Benutzer aus den Einstellungen für bedingten Zugriff in Configuration Manager, sobald sie zu eigenständigem Intune migriert wurden.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Konfigurieren des Microsoft Intune Certificate Connectors
Wenn Sie den Registrierungsdienst für Netzwerkgeräte (Network Device Enrollment Service, NDES) zum Ausstellen von Zertifikaten mithilfe des Simple Certificate Enrollment-Protokolls (SCEP) verwenden, müssen Sie den Microsoft Intune Certificate Connector konfigurieren. Der Computer, der den NDES-Connector in Intune hostet, darf nicht derselbe Computer sein, der den NDES-Connector in Configuration Manager hostet. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von SCEP-Zertifikaten mit Intune](https://docs.microsoft.com/en-us/intune/certificates-scep-configure). 

> [!Important]    
> Nachdem Sie den Connector konfiguriert haben, müssen Sie importierte SCEP-Profile so ändern, dass sie auf die neue Server-URL verweisen.

## <a name="next-step"></a>Nächste Schritte
Nachdem Sie Intune für die Migration vorbereitet haben, sind Sie bereit, eine Reihe von Testbenutzern zu eigenständigem Intune zu migrieren. Einzelheiten finden Sie unter [Ändern der MDM-Autorität für bestimmte Benutzer (gemischte MDM-Autorität)](migrate-mixed-authority.md).


