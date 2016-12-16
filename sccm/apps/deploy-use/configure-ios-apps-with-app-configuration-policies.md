---
title: Konfigurieren von iOS-Apps mit Konfigurationsrichtlinien | System Center Configuration Manager
description: "Vermeidung von Konfigurationsproblemen auf Geräten, die iOS 8 oder höher ausführen, durch Bereitstellung von Richtlinien zur Konfiguration von Apps an Benutzer vor dem Ausführen von Apps."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-app
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74d5d776-e37d-45de-bdba-43541b03d12c
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9cbf28afbbe69f9a027ffad2a699b9d6b625e690


---
# <a name="configure-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Configure iOS apps with app configuration policies in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Verwenden Sie Konfigurationsrichtlinien für Apps in System Center Configuration Manager, um Einstellungen anzugeben, die beim Ausführen einer App durch den Benutzer erforderlich sein können. Beispielsweise kann eine App vom Benutzer Folgendes anfordern:
- Eine benutzerdefinierte Portnummer
- Spracheinstellungen
- Sicherheitseinstellungen
- Brandingeinstellungen wie z. B. ein Unternehmenslogo

Wenn diese Einstellungen vom Benutzer nicht ordnungsgemäß eingegeben werden, kann dies zur erhöhten Belastung Ihres Helpdesks führen und auch die Annahme der neuen Apps verlangsamen..
Mit Konfigurationsrichtlinien für Apps können Sie diese Probleme beseitigen, da Sie diese Einstellungen für Benutzer in einer Richtlinie bereitstellen können, bevor die Benutzer die App ausführen. Die Einstellungen werden dann automatisch bereitgestellt, und der Benutzer muss keine weitere Aktion durchführen.
Sie stellen diese Richtlinien nicht direkt für Benutzer und Geräte bereit. Stattdessen verknüpfen Sie die Richtlinie mit einem Bereitstellungstyp, wenn Sie die Anwendung bereitstellen. Die Richtlinieneinstellungen werden immer dann verwendet, wenn die Anwendung danach sucht (in der Regel beim ersten Ausführen).

Konfigurationsrichtlinien für Apps sind derzeit nur auf Geräten mit iOS 8 und höher verfügbar, und unterstützen die folgenden Anwendungstypen:

- **App-Paket für iOS (*IPA-Datei)**
- **App-Paket für iOS aus App Store**

Weitere Informationen zu App-Installationstypen finden Sie unter [Introduction to application management (Einführung in die Anwendungsverwaltung)](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Erstellen einer Konfigurationsrichtlinie für Apps

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Anwendungsverwaltung** > **App-Konfigurationsrichtlinien**.
3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **App-Konfigurationsrichtlinien** auf **Neue App-Konfigurationsrichtlinie erstellen**.
4. Geben Sie auf der Seite **Allgemein** des **Assistent zum Erstellen einer App-Konfigurationsrichtlinie** die folgenden Informationen an:
    - **Name**: Geben Sie einen eindeutigen Namen für die Richtlinie an.
    - **Beschreibung**: Geben Sie optional eine Beschreibung für die Richtlinie an, mit der Sie sie identifizieren können.
    - **Zugewiesene Kategorien zum leichteren Suchen und Filtern**: Klicken Sie optional auf **Kategorien**, um Kategorien zu erstellen, und der Richtlinie zuzuweisen. Dies macht es einfacher für Sie, Elemente in der Configuration Manager-Konsole zu sortieren, und zu finden.
5. Wählen Sie auf der Seite **iOS-Richtlinie** aus, wie Sie die Informationen zur Konfigurationsrichtlinie angeben wollen:
    - **Specify name and value pairs (Name und Wert-Paare angeben)**: Sie können diese Option für Daten der Eigenschaftsliste verwenden, die keine Schachtelung verwenden.
    Name und Wert-Paare angeben
        - Klicken Sie auf **Neu**, um ein neues Paar hinzuzufügen.
        - Geben Sie im Dialogfeld **Name/Wert-Paar hinzufügen** folgendes an:
            - **Typ**: Wählen Sie aus der Liste den Typ des Werts aus, den Sie angeben möchten.
            - **Name**: Geben Sie den Namen des Eigenschaftslistenschlüssels an, für den Sie einen Wert angeben möchten.
            - **Wert**: Geben Sie den Wert an, der für den eingegebenen Schlüssel festgelegt wird.
        - Wechseln Sie zu einer Eigenschaftslistendatei: Verwenden Sie diese Option, wenn Sie bereits über eine XML-Datei zum Konfigurieren einer App verfügen, oder für komplexere Dateien, die Schachtelung verwenden.
        Zu einer Eigenschaftslistendatei navigieren
            - Geben Sie im Feld **App-Konfigurationsrichtlinie** die Informationen zur Eigenschaftsliste im richtigen XML-Format an.
            Weitere Informationen zu XML-Eigenschaftenlisten finden Sie unter [Understanding XML Property Lists (XML-Eigenschaftslisten verstehen)](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) in der iOS Developer Library.
            Das Format der XML-Eigenschaftenliste variiert je nach der App, die Sie konfigurieren. Wenden Sie sich an den Hersteller der App, um ausführliche Informationen über das genau zu verwendende Format zu erhalten.
            Intune unterstützt die folgenden Datentypen in einer Eigenschaftenliste:
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
            Weitere Informationen zu Datentypen finden Sie unter [About Property Lists (Über Eigenschaftslisten)](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) in der iOS Developer Library.
            Darüber hinaus unterstützt Intune die folgenden Tokentypen in der Eigenschaftsliste:
            ```
            {{userprincipalname}} - (Example: John@contoso.com)
            {{mail}} - (Example: John@contoso.com)
            {{partialupn}} - (Example: John)
            {{accountid}} - (Example: fc0dc142-71d8-4b12-bbea-bae2a8514c81)
            {{deviceid}} - (Example: b9841cd9-9843-405f-be28-b2265c59ef97)
            {{userid}} - (Example: 3ec2c00f-b125-4519-acf0-302ac3761822)
            {{username}} - (Example: John Doe)
            {{serialnumber}} - (Example: F4KN99ZUG5V2) for iOS devices
            {{serialnumberlast4digits}} - (Example: G5V2) for iOS devices

            The {{ and }} characters are used by token types only and must not be used for other purposes.
            ```
            Sie können auch auf **Datei auswählen** klicken, um eine zuvor erstellte XML-Datei zu importieren.
6. Klicken Sie auf **Weiter**. Falls Sie Fehler im XML-Code feststellen, müssen Sie diese korrigieren, bevor Sie fortfahren.
6. Schließen Sie den Assistenten ab.

Die neue App-Konfigurationsrichtlinie wird im Knoten **App-Konfigurationsrichtlinien** des Arbeitsbereichs **Softwarebibliothek** angezeigt.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Zuordnen einer Konfigurationsrichtlinie für Apps zu einer Configuration Manager-Anwendung

Um eine App-Konfigurationsrichtlinie mit der Bereitstellung einer iOS-App zuzuordnen, stellen Sie die Anwendung wie gewohnt bereit, indem Sie die Vorgehensweise im Thema [Bereitstellen von Anwendungen](/sccm/apps/deploy-use/deploy-applications) durchführen.
Klicken Sie auf der Seite **App-Konfigurationsrichtlinien** des **Assistenten zum Bereitstellen von Software** auf **Neu**. Wählend Sie anschließend im Dialogfeld **App-Konfigurationsrichtlinie auswählen** einen Bereitstellungstyp und eine App-Konfigurationsrichtlinie aus, die Sie zuordnen möchten.
Bei der Installation des Bereitstellungstyps werden die Einstellungen der App-Konfigurationsrichtlinie automatisch angewendet.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Beispiel für das Format für die XML-Konfigurationsdatei für mobile Apps

Wenn Sie eine Konfigurationsdatei für mobile Apps erstellen, können Sie mithilfe dieses Formats einen oder mehr der folgenden Werte angeben:

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>
```



<!--HONumber=Nov16_HO1-->


