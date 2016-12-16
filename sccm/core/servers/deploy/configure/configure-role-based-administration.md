---
title: Konfigurieren der rollenbasierten Verwaltung | System Center Configuration Manager
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8c67fb351fff7f362ca3845c2cc67d222b6477b8


---
# <a name="configure-role-based-administration-for-system-center-configuration-manager"></a>Konfigurieren der rollenbasierten Verwaltung für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei der rollenbasierten Verwaltung in System Center Configuration Manager werden Sicherheitsrollen, Sicherheitsbereiche und zugewiesene Sammlungen kombiniert, um den Verwaltungsbereich für jeden Administrator zu definieren. Zu einem Verwaltungsbereich gehören die Objekte, die ein Administrator in der Configuration Manager-Konsole anzeigen kann, und die Tasks im Zusammenhang mit diesen Objekten, die der Administrator ausführen darf. Die Konfigurationen der rollenbasierten Verwaltung werden auf jeden Standort in einer Hierarchie angewendet.  

 Wenn Sie mit den Konzepten der rollenbasierten Verwaltung noch nicht vertraut sind, finden Sie unter [Grundlagen der rollenbasierten Verwaltung für System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md) weitere Informationen.  

 Verwenden Sie die folgenden Informationen und Verfahren, um die rollenbasierte Verwaltung und entsprechende Sicherheitseinstellungen zu erstellen und zu konfigurieren.  

-   [Erstellen benutzerdefinierter Sicherheitsrollen](#BKMK_CreateSecRole)  

-   [Konfigurieren von Sicherheitsrollen](#BKMK_ConfigSecRole)  

-   [Konfigurieren von Sicherheitsbereichen für ein Objekt](#BKMK_ConfigSecScope)  

-   [Konfigurieren von Sammlungen zum Verwalten der Sicherheit](#BKMK_ConfigColl)  

-   [Erstellen eines neuen Administrators](#BKMK_Create_AdminUser)  

-   [Ändern des Verwaltungsbereichs eines Administrators](#BKMK_ModAdminUser)  

##  <a name="a-namebkmkcreatesecrolea-create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a> Erstellen benutzerdefinierter Sicherheitsrollen  
 In Configuration Manager sind mehrere integrierte Sicherheitsrollen verfügbar. Wenn Sie zusätzliche Sicherheitsrollen benötigen, können Sie eine benutzerdefinierte Sicherheitsrolle erstellen, indem Sie von einer vorhandenen Sicherheitsrolle eine Kopie erstellen und diese dann ändern. Sie könnten eine benutzerdefinierte Sicherheitsrolle erstellen, um Administratoren zusätzliche Sicherheitsberechtigungen zu erteilen, welche für die Administratoren erforderlich, in der aktuell zugewiesenen Sicherheitsrolle jedoch nicht enthalten sind. Wenn Sie eine benutzerdefinierte Sicherheitsrolle verwenden, können Sie ihnen nur die erforderlichen Berechtigungen erteilen und vermeiden, eine Sicherheitsrolle zuzuweisen, mit der Sie mehr Berechtigungen erteilen, als erforderlich sind.  

 Wenden Sie das folgende Verfahren an, um eine neue Sicherheitsrolle mithilfe einer vorhandenen Sicherheitsrolle als Vorlage zu erstellen.  

#### <a name="to-create-custom-security-roles"></a>So erstellen Sie benutzerdefinierte Sicherheitsrollen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Sicherheit**, und klicken Sie dann auf **Sicherheitsrollen**.  

     Verwenden Sie eines der folgenden Verfahren, um die neue Sicherheitsrolle zu erstellen:  

    -   Führen Sie die folgenden Aktionen aus, um eine neue benutzerdefinierte Sicherheitsrolle zu erstellen:  

        1.  Wählen Sie eine vorhandene Sicherheitsrolle aus, die Sie als Quelle für die neue Sicherheitsrolle verwenden möchten.  

        2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Sicherheitsrolle** auf **Kopieren**. Damit erstellen Sie eine Kopie der Quellsicherheitsrolle.  

        3.  Geben Sie im Assistenten zum Kopieren von Sicherheitsrollen einen Namen ** ** für die neue benutzerdefinierte Sicherheitsrolle an.  

        4.  Erweitern Sie in **Zuweisungen von Sicherheitsvorgängen**alle Knoten unter **Sicherheitsvorgänge** , um die verfügbaren Aktionen anzuzeigen.  

        5.  Wenn Sie die Einstellung für einen Sicherheitsvorgang ändern möchten, klicken Sie in der Spalte **Wert** auf den Pfeil nach unten und wählen dann entweder **Ja** oder **Nein**aus.  

            > [!CAUTION]  
            >  Wenn Sie eine benutzerdefinierte Sicherheitsrolle konfigurieren, achten Sie darauf, keine Berechtigungen zu erteilen, die für die Administratoren, die der neuen Sicherheitsrolle zugewiesen sind, nicht erforderlich sind. Beispielsweise erteilen Sie mit dem Wert **Ändern** für den Sicherheitsvorgang **Sicherheitsrollen** Administratoren die Berechtigung zum Ändern jeder zugänglichen Sicherheitsrolle, auch dann, wenn die Administratoren dieser Sicherheitsrolle nicht zugewiesen sind.  

        6.  Wenn Sie die Berechtigungen konfiguriert haben, klicken Sie auf **OK** , um die neue Sicherheitsrolle zu speichern.  

    -   Wenn Sie eine Sicherheitsrolle importieren möchten, die aus einer anderen Configuration Manager-Hierarchie exportiert wurde, führen Sie die folgenden Aktionen aus:  

        1.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Sicherheitsrolle importieren**.  

        2.  Geben Sie die XML-Datei an, die die zu importierende Sicherheitsrollenkonfiguration enthält, und klicken Sie auf **Öffnen** , um den Vorgang abzuschließen und die Sicherheitsrolle zu speichern.  

            > [!NOTE]  
            >  Wenn Sie eine Sicherheitsrolle importiert haben, können Sie die Eigenschaften der Sicherheitsrolle bearbeiten, um die entsprechenden Objektberechtigungen zu ändern.  

##  <a name="a-namebkmkconfigsecrolea-configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a> Konfigurieren von Sicherheitsrollen  
 Die Gruppen von Sicherheitsberechtigungen, die für eine Sicherheitsrolle definiert sind, werden als Zuweisungen von Sicherheitsvorgängen bezeichnet. Von Zuweisungen von Sicherheitsvorgängen wird eine Kombination von Objekttypen und Aktionen repräsentiert, die für jeden Objekttyp verfügbar ist. Sie können ändern, welche Sicherheitsvorgänge für jede benutzerdefinierte Sicherheitsrolle verfügbar sind. Sie können jedoch nicht die in Configuration Manager integrierten Sicherheitsrollen ändern.  

 Wenden Sie das folgende Verfahren an, um die Sicherheitsvorgänge für eine Sicherheitsrolle zu ändern.  

#### <a name="to-modify-security-roles"></a>Ändern von Sicherheitsrollen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Sicherheit**, und klicken Sie dann auf **Sicherheitsrollen**.  

3.  Wählen Sie die benutzerdefinierte Sicherheitsrolle, die Sie ändern möchten, aus.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie auf die Registerkarte **Berechtigungen** .  

6.  Erweitern Sie in **Zuweisungen von Sicherheitsvorgängen**alle Knoten unter **Sicherheitsvorgänge** , um die verfügbaren Aktionen anzuzeigen.  

7.  Wenn Sie die Einstellung für einen Sicherheitsvorgang ändern möchten, klicken Sie in der Spalte **Wert** auf den Pfeil nach unten und wählen dann entweder **Ja** oder **Nein**aus.  

    > [!CAUTION]  
    >  Wenn Sie eine benutzerdefinierte Sicherheitsrolle konfigurieren, achten Sie darauf, keine Berechtigungen zu erteilen, die für die Administratoren, die der neuen Sicherheitsrolle zugewiesen sind, nicht erforderlich sind. Beispielsweise erteilen Sie mit dem Wert **Ändern** für den Sicherheitsvorgang **Sicherheitsrollen** Administratoren die Berechtigung zum Ändern jeder zugänglichen Sicherheitsrolle, auch dann, wenn die Administratoren dieser Sicherheitsrolle nicht zugewiesen sind.  

8.  Wenn Sie mit dem Konfigurieren der Zuweisungen von Sicherheitsvorgängen fertig sind, klicken Sie auf **OK** , um die neue Sicherheitsrolle zu speichern.  

##  <a name="a-namebkmkconfigsecscopea-configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a> Konfigurieren von Sicherheitsbereichen für ein Objekt  
 Sie verwalten die Zuweisung eines Sicherheitsbereichs für ein Objekt vom Objekt aus, nicht vom Sicherheitsbereich aus. Die einzigen direkten Konfigurationen, die von Sicherheitsbereichen unterstützt werden, sind Änderungen an Namen und Beschreibung der Sicherheitsbereiche. Wenn Sie den Namen oder die Beschreibung eines Sicherheitsbereichs beim Anzeigen der Eigenschaften des Sicherheitsbereichs ändern möchten, benötigen Sie die Berechtigung **Ändern** für das sicherungsfähige Objekt **Sicherheitsbereiche** .  

 Wenn Sie ein neues Objekt in Configuration Manager erstellen, wird das Objekt allen Sicherheitsbereichen zugeordnet, die ihrerseits den Sicherheitsrollen des Kontos zugeordnet sind, das für die Erstellung des Objekts verwendet wurde, sofern mit diesen Sicherheitsrollen die Berechtigungen **Erstellen** oder **Sicherheitsbereiche festlegen** erteilt werden. Sie können erst nach dem Erstellen eines Objekts die Sicherheitsbereiche, denen es zugewiesen ist, ändern.  

 Beispielsweise sind Sie einer Sicherheitsrolle zugewiesen, durch die Sie über die Berechtigung zum Erstellen einer neuen Begrenzungsgruppe verfügen. Wenn Sie eine neue Begrenzungsgruppe erstellen, ist keine Option verfügbar, der Sie bestimmte Sicherheitsbereiche zuweisen könnten. Stattdessen werden die Sicherheitsbereiche, die in den Sicherheitsrollen verfügbar sind, denen Sie zugewiesen sind, automatisch der neuen Begrenzungsgruppe zugewiesen. Wenn Sie die neue Begrenzungsgruppe gespeichert haben, können Sie die Sicherheitsbereiche bearbeiten, die der neuen Begrenzungsgruppe zugewiesen sind.  

 Wenden Sie das folgende Verfahren an, um die Sicherheitsbereiche zu konfigurieren, die einem Objekt zugewiesen sind.  

#### <a name="to-configure-security-scopes-for-an-object"></a>So konfigurieren Sie Sicherheitsbereiche für ein Objekt  

1.  Wählen Sie in der Configuration Manager-Konsole ein Objekt aus, das einem Sicherheitsbereich zugewiesen werden kann.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Klassifizieren** auf **Sicherheitsbereiche festlegen**.  

3.  Aktivieren bzw. deaktivieren Sie im Dialogfeld **Sicherheitsbereiche festlegen** die Sicherheitsbereiche, denen dieses Objekt zugeordnet sein soll. Jedes Objekt, von dem die Zuweisung zu Sicherheitsbereichen unterstützt wird, muss mindestens einem Sicherheitsbereich zugewiesen werden.  

4.  Klicken Sie auf **OK** , um die zugewiesenen Sicherheitsbereiche zu speichern.  

    > [!NOTE]  
    >  Wenn Sie ein neues Objekt erstellen, können Sie es mehreren Sicherheitsbereichen zuweisen. Wenn Sie die Anzahl der Sicherheitsbereiche, denen das Objekt zugewiesen ist, ändern möchten, müssen Sie diese Zuweisung nach der Erstellung des Objekts ändern.  

##  <a name="a-namebkmkconfigcolla-configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a> Konfigurieren von Sammlungen zum Verwalten der Sicherheit  
 Es gibt keine Verfahren zum Konfigurieren von Sammlungen für die rollenbasierte Verwaltung. Bei Sammlungen ist keine Konfiguration für die rollenbasierte Verwaltung verfügbar. Stattdessen weisen Sie Sammlungen einem Administrator zu, wenn Sie den Administrator konfigurieren. Von den Sicherheitsvorgängen der Sammlung, die in den zugewiesenen Sicherheitsrollen der Benutzer aktiviert werden, wird bestimmt, welche Berechtigungen ein Administrator für Sammlungen und Sammlungsressourcen (Sammlungsmitglieder) hat.  

 Wenn Administratoren über Berechtigungen für eine Sammlung verfügen, verfügen sie auch über Berechtigungen für Sammlungen, die auf diese Sammlung begrenzt sind. Beispielsweise wird in Ihrer Organisation eine Sammlung namens „Alle Desktopcomputer“ verwendet, und eine Sammlung namens „Alle Desktopcomputer in Europa“ wurde auf die Sammlung „Alle Desktopcomputer“ beschränkt. Administratoren, die Berechtigungen für die Sammlung „Alle Desktopcomputer“ haben, verfügen über die gleichen Berechtigungen für die Sammlung „Alle Desktopcomputer in Europa“. Zusätzlich können Administratoren die Berechtigungen **Löschen** und **Ändern** nicht bei Sammlungen verwenden, die ihnen direkt zugeordnet sind. Sie können die Berechtigungen jedoch bei Sammlungen verwenden, die auf die direkt zugeordneten Sammlungen beschränkt sind. Im vorigen Beispiel können Administratoren die Sammlung „Alle Desktopcomputer in Europa“ ändern und löschen. Sie können jedoch nicht die Sammlung „Alle Desktopcomputer“ ändern oder löschen.  

##  <a name="a-namebkmkcreateadminusera-create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a> Erstellen eines neuen Administrators  
 Erstellen Sie in Configuration Manager Administratoren, und geben Sie das Windows-Konto des Benutzers bzw. der Benutzergruppe an, um Individuen oder Mitgliedern von Sicherheitsgruppen einen Verwaltungszugriff auf Configuration Manager zu gewähren. Jedem Administrator in Configuration Manager müssen mindestens eine Sicherheitsrolle und ein Sicherheitsbereich zugewiesen werden. Sie können auch Sammlungen zuweisen, um den Verwaltungsbereich des Administrators zu begrenzen.  

 Wenden Sie die folgenden Verfahren an, um neue Administratoren zu erstellen.  

#### <a name="to-create-a-new-administrative-user"></a>So erstellen Sie einen neuen Administrator  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Sicherheit**, und klicken Sie dann auf **Administratoren**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Benutzer oder Gruppe hinzufügen**.  

4.  Klicken Sie auf **Durchsuchen** , und wählen Sie dann das für diesen Administrator zu verwendende Benutzerkonto bzw. die zu verwendende Gruppe aus.  

    > [!NOTE]  
    >  Für die konsolenbasierte Verwaltung können nur Domänenbenutzer oder Sicherheitsgruppen als Administratoren angegeben werden.  

5.  Klicken Sie unter **Zugeordnete Sicherheitsrollen**auf **Hinzufügen** , um eine Liste der verfügbaren Sicherheitsrollen anzuzeigen. Aktivieren Sie das Kontrollkästchen für mindestens eine Sicherheitsrolle, und klicken Sie dann auf **OK**.  

6.  Wählen Sie eine der folgenden beiden Optionen aus, um das Verhalten im Zusammenhang mit sicherungsfähigen Objekten für den neuen Benutzer zu definieren:  

    -   **Alle sicherungsfähigen Objekte, die für die zugeordneten Sicherheitsrollen relevant sind**: Bei Auswahl dieser Option wird der Administrator dem Sicherheitsbereich **Alle** sowie den integrierten Sammlungen **Alle Systeme**und **Alle Benutzer und Benutzergruppen** der Stammebene zugeordnet. Über die dem Benutzer zugewiesenen Sicherheitsrollen wird dessen Zugriff auf Objekte definiert. Von diesem Administrator erstellte neue Objekte werden dem Sicherheitsbereich **Standard** zugewiesen.  

    -   **Nur sicherungsfähige Objekte in angegebenen Sicherheitsbereichen oder Sammlungen**: Bei Auswahl dieser Option wird der Administrator dem Sicherheitsbereich **Standard** sowie den Sammlungen **Alle Systeme** und **Alle Benutzer und Benutzergruppen** zugeordnet. Welche Sicherheitsbereiche und Sammlungen tatsächlich verfügbar sind, ist jedoch abhängig vom Benutzerkonto, anhand dessen der neue Administrator erstellt wurde. Mit dieser Option ist es möglich, Sicherheitsbereiche und Sammlungen hinzuzufügen und zu entfernen, um den Verwaltungsbereich des Administrators anzupassen.  

    > [!IMPORTANT]  
    >  Mit den vorangehenden Optionen werden alle zugewiesenen Sicherheitsbereiche und Sammlungen jeder Sicherheitsrolle zugeordnet, die dem Administrator zugewiesen ist. Mit einer dritten Option, **Nur sicherungsfähige Objekte, die von den Sicherheitsrollen des Administrators bestimmt sind**, können einzelne Sicherheitsrollen bestimmten Sicherheitsbereichen und Sammlungen zugeordnet werden. Diese dritte Option steht erst nach dem Erstellen des neuen Administrators beim Ändern des Administrators zur Verfügung.  

7.  Fahren Sie abhängig von der in Schritt 6 vorgenommenen Auswahl wie folgt fort:  

    -   Wenn Sie die Option **Alle sicherungsfähigen Objekte, die für die zugeordneten Sicherheitsrollen relevant sind**ausgewählt haben, klicken Sie auf **OK** , um dieses Verfahren abzuschließen.  

    -   Wenn Sie **Nur sicherungsfähige Objekte in angegebenen Sicherheitsbereichen oder Sammlungen**ausgewählt haben, können Sie auf **Hinzufügen** klicken, um weitere Sammlungen und Sicherheitsbereiche auszuwählen, oder ein oder mehrere Objekte in der Liste auswählen und auf **Entfernen** klicken, um sie zu entfernen. Klicken Sie auf **OK** , um dieses Verfahren abzuschließen.  

##  <a name="a-namebkmkmodadminusera-modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a> Ändern des Verwaltungsbereichs eines Administrators  
 Sie können den Verwaltungsbereich eines Administrators ändern, indem Sie Sicherheitsrollen, Sicherheitsbereiche und dem Benutzer zugeordnete Sammlungen hinzufügen oder entfernen. Jedem Administrator müssen mindestens eine Sicherheitsrolle und ein Sicherheitsbereich zugeordnet sein. Möglicherweise müssen Sie dem Verwaltungsbereich des Benutzers zunächst eine oder mehrere Sammlungen zuweisen. Für die meisten Sicherheitsrollen ist eine Interaktion mit Sammlungen erforderlich, sodass sie ohne eine zugewiesene Sammlung nicht funktionsfähig sind.  

 Wenn Sie einen Administrator bearbeiten, können Sie das Verhalten beim Zuordnen von sicherungsfähigen Objekten zu den zugewiesenen Sicherheitsrollen ändern. Die folgenden drei Verhaltensweisen stehen zur Auswahl:  

-   **Alle sicherungsfähigen Objekte, die für die zugeordneten Sicherheitsrollen relevant sind**: Bei Auswahl dieser Option wird der Administrator dem Bereich **Alle** sowie den integrierten Sammlungen **Alle Systeme**und **Alle Benutzer und Benutzergruppen**der Stammebene zugeordnet. Über die dem Benutzer zugewiesenen Sicherheitsrollen wird dessen Zugriff auf Objekte definiert.  

-   **Nur sicherungsfähige Objekte in angegebenen Sicherheitsbereichen oder Sammlungen**: Bei Auswahl dieser Option wird der Administrator den gleichen Sicherheitsbereichen und Sammlungen zugeordnet, die dem zur Konfiguration des Administrators verwendeten Konto zugeordnet sind. Mit dieser Option ist es möglich, Sicherheitsrollen und Sammlungen hinzuzufügen und zu entfernen, um den Verwaltungsbereich des Administrators anzupassen.  

-   **Nur sicherungsfähige Objekte, die von den Sicherheitsrollen des Administrators bestimmt sind**: Mit dieser Option können Sie Zuordnungen zwischen einzelnen Sicherheitsrollen und bestimmten Sicherheitsbereichen und Sammlungen für den Benutzer erstellen.  

    > [!NOTE]  
    >  Diese Option ist nur verfügbar, wenn Sie die Eigenschaften eines vorhandenen Administrators ändern.  

Von der aktuellen Konfiguration für das Verhalten im Zusammenhang mit sicherungsfähigen Objekten ist abhängig, welches Verfahren Sie verwenden müssen, um zusätzliche Sicherheitsrollen zuzuweisen. Wenden Sie, abhängig von den Optionen für sicherungsfähige Objekte, die folgenden Verfahren zur Verwaltung eines Administrators an.  

 Gehen Sie wie folgt vor, um die Konfiguration für sicherungsfähige Objekte für einen Administrator anzuzeigen und zu verwalten:  

#### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>So zeigen Sie das Verhalten im Zusammenhang mit sicherungsfähigen Objekten für einen Administrator an und verwalten es  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Sicherheit**, und klicken Sie dann auf **Administratoren**.  

3.  Wählen Sie den Administrator aus, den Sie ändern möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie auf die Registerkarte **Sicherheitsbereiche** , um die Konfiguration für sicherungsfähige Objekte für diesen Administrator anzuzeigen.  

6.  Zum Ändern des Verhaltens im Zusammenhang mit sicherungsfähigen Objekten wählen Sie die gewünschte Option aus. Nach dem Ändern der Konfiguration erhalten Sie im entsprechenden Verfahren weitere Hinweise zum Konfigurieren von Sicherheitsbereichen und Sammlungen sowie Sicherheitsrollen für den Administrator.  

7.  Klicken Sie auf **OK** , um das Verfahren abzuschließen.  

 Gehen Sie wie folgt vor, um einen Administrator zu ändern, für den als Verhalten im Zusammenhang mit sicherungsfähigen Objekten **Alle sicherungsfähigen Objekte, die für die zugeordneten Sicherheitsrollen relevant sind**ausgewählt wurde:  

#### <a name="option-all-securable-objects-that-are-relevant-to-their-associated-security-roles"></a>Option: Alle sicherungsfähigen Objekte, die für die zugeordneten Sicherheitsrollen relevant sind  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Sicherheit**, und klicken Sie dann auf **Administratoren**.  

3.  Wählen Sie den Administrator aus, den Sie ändern möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie auf die Registerkarte **Sicherheitsbereiche** , um zu bestätigen, dass für den Administrator die Option **Alle sicherungsfähigen Objekte, die für die zugeordneten Sicherheitsrollen relevant sind**konfiguriert wurde.  

6.  Klicken Sie auf die Registerkarte **Sicherheitsrollen** , um die zugewiesenen Sicherheitsrollen zu ändern.  

    -   Wenn Sie diesem Administrator weitere Sicherheitsrollen hinzufügen möchten, klicken Sie auf **Hinzufügen**, aktivieren Sie das Kontrollkästchen für jede weitere zuzuweisende Sicherheitsrolle, und klicken Sie dann auf **OK**.  

    -   Wenn Sie Sicherheitsrollen entfernen möchten, wählen Sie die entsprechenden Sicherheitsrollen in der Liste aus, und klicken Sie dann auf **Entfernen**.  

7.  Wenn Sie das Verhalten im Zusammenhang mit sicherungsfähigen Objekten ändern möchten, klicken Sie auf die Registerkarte **Sicherheitsbereiche** , und wählen Sie die gewünschte Option aus. Nach dem Ändern der Konfiguration erhalten Sie im entsprechenden Verfahren weitere Hinweise zum Konfigurieren von Sicherheitsbereichen und Sammlungen sowie Sicherheitsrollen für den Administrator.  

    > [!NOTE]  
    >  Wenn für das Verhalten im Zusammenhang mit sicherungsfähigen Objekten die Option **Alle sicherungsfähigen Objekte, die für die zugeordneten Sicherheitsrollen relevant sind**ausgewählt ist, können Sie Sicherheitsbereiche und Sammlungen weder hinzufügen noch entfernen.  

8.  Klicken Sie auf **OK** , um dieses Verfahren abzuschließen.  

 Gehen Sie wie folgt vor, um einen Administrator zu ändern, für den als Verhalten im Zusammenhang mit sicherungsfähigen Objekten **Nur sicherungsfähige Objekte in angegebenen Sicherheitsbereichen oder Sammlungen**ausgewählt wurde:  

#### <a name="option-only-securable-objects-in-specified-security-scopes-or-collections"></a>Option: Nur sicherungsfähige Objekte in angegebenen Sicherheitsbereichen oder Sammlungen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Sicherheit**, und klicken Sie dann auf **Administratoren**.  

3.  Wählen Sie den Administrator aus, den Sie ändern möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie auf die Registerkarte **Sicherheitsbereiche** , um zu bestätigen, dass für den Benutzer die Option **Nur sicherungsfähige Objekte in angegebenen Sicherheitsbereichen oder Sammlungen**konfiguriert wurde.  

6.  Klicken Sie auf die Registerkarte **Sicherheitsrollen** , um die zugewiesenen Sicherheitsrollen zu ändern.  

    -   Wenn Sie diesem Benutzer weitere Sicherheitsrollen hinzufügen möchten, klicken Sie auf **Hinzufügen**, aktivieren Sie das Kontrollkästchen für jede weitere zuzuweisende Sicherheitsrolle, und klicken Sie dann auf **OK**.  

    -   Wenn Sie Sicherheitsrollen entfernen möchten, wählen Sie die entsprechenden Sicherheitsrollen in der Liste aus, und klicken Sie dann auf **Entfernen**.  

7.  Wenn Sie die Sicherheitsbereiche und Sammlungen, die Sicherheitsrollen zugeordnet sind, ändern möchten, klicken Sie auf die Registerkarte **Sicherheitsbereiche** .  

    -   Wenn Sie allen diesem Administrator zugewiesenen Sicherheitsrollen neue Sicherheitsbereiche oder Sammlungen zuordnen möchten, klicken Sie auf **Hinzufügen** , und wählen Sie eine der vier Optionen aus. Wenn Sie **Sicherheitsbereich** oder **Sammlung**auswählen, aktivieren Sie das Kontrollkästchen für mindestens ein Objekt, um die Auswahl abzuschließen, und klicken Sie dann auf **OK**.  

    -   Wenn Sie einen Sicherheitsbereich oder eine Sammlung entfernen möchten, wählen Sie das Objekt aus, und klicken Sie dann auf **Entfernen**.  

8.  Klicken Sie auf **OK** , um dieses Verfahren abzuschließen.  

 Gehen Sie wie folgt vor, um einen Administrator zu ändern, für den als Verhalten im Zusammenhang mit sicherungsfähigen Objekten **Nur sicherungsfähige Objekte, die von den Sicherheitsrollen des Administrators bestimmt sind**ausgewählt wurde:  

#### <a name="option-only-securable-objects-as-determined-by-the-security-roles-of-the-administrative-user"></a>Option: Nur sicherungsfähige Objekte, die von den Sicherheitsrollen des Administrators bestimmt sind  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Sicherheit**, und klicken Sie dann auf **Administratoren**.  

3.  Wählen Sie den Administrator aus, den Sie ändern möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie auf die Registerkarte **Sicherheitsbereiche** , um zu bestätigen, dass für den Administrator die Option **Nur sicherungsfähige Objekte in angegebenen Sicherheitsbereichen oder Sammlungen**konfiguriert wurde.  

6.  Klicken Sie auf die Registerkarte **Sicherheitsrollen** , um die zugewiesenen Sicherheitsrollen zu ändern.  

    -   Wenn Sie diesem Administrator zusätzliche Sicherheitsrollen zuweisen möchten, klicken Sie auf **Hinzufügen**. Wählen Sie im Dialogfeld **Sicherheitsrolle hinzufügen** mindestens eine verfügbare Sicherheitsrolle aus, klicken Sie auf **Hinzufügen**, und wählen Sie dann einen Objekttyp aus, der den ausgewählten Sicherheitsrollen zugeordnet werden soll. Wenn Sie **Sicherheitsbereich** oder **Sammlung**auswählen, aktivieren Sie das Kontrollkästchen für mindestens ein Objekt, um die Auswahl abzuschließen, und klicken Sie dann auf **OK**.  

        > [!NOTE]  
        >  Sie müssen mindestens einen Sicherheitsbereich konfigurieren, damit die ausgewählten Sicherheitsrollen dem Administrator zugewiesen werden können. Wenn Sie mehrere Sicherheitsrollen auswählen, wird jeder konfigurierte Sicherheitsbereich und jede Sammlung jeder ausgewählten Sicherheitsrolle zugeordnet.  

    -   Wenn Sie Sicherheitsrollen entfernen möchten, wählen Sie die entsprechenden Sicherheitsrollen in der Liste aus, und klicken Sie dann auf **Entfernen**.  

7.  Wenn Sie die Sicherheitsbereiche und Sammlungen, die einer bestimmten Sicherheitsrolle zugeordnet sind, ändern möchten, klicken Sie auf die Registerkarte **Sicherheitsbereiche** , wählen Sie die Sicherheitsrolle aus, und klicken Sie dann auf **Bearbeiten**.  

    -   Wenn Sie dieser Sicherheitsrolle neue Objekte zuordnen möchten, klicken Sie auf **Hinzufügen**, und wählen Sie einen Objekttyp aus, der den ausgewählten Sicherheitsrollen zugeordnet werden soll. Wenn Sie **Sicherheitsbereich** oder **Sammlung**auswählen, aktivieren Sie das Kontrollkästchen für mindestens ein Objekt, um die Auswahl abzuschließen, und klicken Sie dann auf **OK**.  

        > [!NOTE]  
        >  Sie müssen mindestens einen Sicherheitsbereich konfigurieren.  

    -   Wenn Sie einen dieser Sicherheitsrolle zugeordneten Sicherheitsbereich oder eine Sammlung entfernen möchten, wählen Sie das Objekt aus, und klicken Sie dann auf **Entfernen**.  

    -   Wenn Sie das Ändern der zugeordneten Objekte abgeschlossen haben, klicken Sie auf **OK**.  

8.  Klicken Sie auf **OK** , um dieses Verfahren abzuschließen.  

    > [!CAUTION]  
    >  Wenn Administratoren durch eine Sicherheitsrolle die Berechtigung zum Bereitstellen von Sammlungen gewährt wird, können diese Administratoren Objekte von jedem Sicherheitsbereich aus verteilen, in dem Sie über die Berechtigung **Lesen** für das Objekt verfügen. Dies gilt auch dann, wenn dieser Sicherheitsbereich einer anderen Sicherheitsrolle zugewiesen ist.  



<!--HONumber=Nov16_HO1-->


