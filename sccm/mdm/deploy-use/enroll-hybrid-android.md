---
title: "Einrichten einer hybriden Geräteverwaltung für Android mit System Center Configuration Manager und Microsoft Intune | Microsoft-Dokumentation"
description: "Bereiten Sie die Verwaltung mobiler Android-Geräte mit Configuration Manager und Intune vor."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 86620254897aa9a775dc433de7010b5814c1ec3e
ms.openlocfilehash: af6fa2dfae5549e89c46d05d0cef1e24342558f9
ms.contentlocale: de-de
ms.lasthandoff: 07/06/2017


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Einrichten einer hybriden Geräteverwaltung für Android mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema hilft dem IT-Administrator bei der Aktivierung der Hybridregistrierung von Android- und Android for Work-Geräten. Der IT-Administrator kann nun mit System Center Configuration Manager Geräte mit einem konfigurierten Abonnement von Microsoft Intune verwalten. Benutzer können die Unternehmensportal-App für Android von Google Play herunterladen; mit dieser App können sie Android-Geräte (einschließlich Samsung KNOX Standard) und Android for Work-Geräte registrieren.

Als Configuration Manager-Administrator können Sie Kompatibilitätseinstellungen verwalten, Android-Geräte zurücksetzen oder löschen, Apps bereitstellen und die Software- und Hardwareinventur erfassen. Wenn die Android-Unternehmensportal-App auf Geräten nicht installiert ist, stehen Ihnen nicht alle Verwaltungsfunktionen zur Verfügung (z.B. Inventur- und Konformitätseinstellungen), aber Sie können trotzdem Apps auf Android-Geräten bereitstellen.  

## <a name="enable-android-enrollment"></a>Aktivieren der Android-Registrierung  
Mit den folgenden Schritten kann Configuration Manager Android-Geräte ohne Arbeitsprofil verwalten (also die „klassische Android“-Registrierung).

1. Bevor Sie die Registrierung einer Plattform einrichten, können Sie die Voraussetzungen und Schritte in [Einrichten der hybriden Verwaltung mobiler Geräte](setup-hybrid-mdm.md) erfüllen und ausführen.  
2. Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Übersicht** > **Clouddienste** > **Microsoft Intune-Abonnement**, und wählen Sie Ihr Intune-Abonnement aus.  
3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Abonnement** auf **Plattformen konfigurieren** > **Android**.  
4. Wählen Sie im Dialogfeld **Eigenschaften von Microsoft Intune-Abonnement** die Registerkarte **Android** aus, und aktivieren Sie das Kontrollkästchen **Android-Registrierung aktivieren**.  

 Nachdem Sie die Einrichtung abgeschlossen haben, müssen Sie Ihre Benutzer darüber informieren, wie diese ihre Geräte registrieren sollen. Informationen hierzu finden Sie unter [Informieren der Benutzer über den Einsatz von Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Diese Informationen gelten für mobile Geräte, die mit Microsoft Intune und Configuration Manager verwaltet werden.

## <a name="enable-android-for-work-enrollment"></a>Aktivieren der Registrierung für Android for Work
Mit den folgenden Schritten kann Configuration Manager Android-Geräte ohne Arbeitsprofil verwalten.

1. Erstellen Sie auf https://accounts.google.com/SignUp ein Google-Konto, das Sie als Administratorkonto für Android for Work verwenden. Oder melden Sie sich mit dem Konto an, das mit allen Verwaltungsaufgaben von Android for Work für diesen Intune-Mandanten verknüpft ist. Dieses Google-Konto kann auch für mehrere Administratoren des Android-Geräts freigegeben werden. Mit diesem Google-Konto verwaltet und veröffentlicht Ihre Organisation Apps in der Play for Work-Konsole. Sie verwenden dieses Konto, um Apps im Play for Work-Store zu genehmigen. Deshalb sollten Sie den Kontonamen und das Kennwort nicht vergessen.
2. Aktivieren Sie die Android-Registrierung, indem Sie das Google-Konto an den von Configuration Manager verwalteten Intune-Mandanten binden:
   1. Wählen Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** **Übersicht** > **Clouddienste** > **Microsoft Intune-Abonnements** aus. Wählen Sie anschließend Ihr Intune-Abonnement aus.
   2. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Abonnement** **Plattformen konfigurieren** > **Android for Work** aus.
   3. Klicken Sie im Dialogfeld auf **Android for Work in der Intune-Konsole konfigurieren**. Die Intune-Konsole wird in Ihrem Webbrowser geöffnet.
   4. Verwenden Sie Ihre Administratoranmeldeinformationen für Intune, um sich im Intune-Portal anzumelden.
   5. Wählen Sie **Konfigurieren** aus, um die Android for Work-Website von Google Play zu öffnen.
   6. Geben Sie auf der Google-Anmeldeseite die Anmeldeinformationen Ihres Google-Kontos aus dem ersten Schritt ein, und machen Sie anschließen Angaben zu Ihrem Unternehmen.
3. Wenn Sie zum Intune-Portal zurückkehren, ist Android for Work aktiviert, und Sie haben drei verschiedene Registrierungsoptionen für Android for Work-Geräte:
   - **Verwalten aller Geräte als Android** (deaktiviert) Alle Android-Geräte, einschließlich der Geräte, die Android for Work unterstützen, werden als herkömmliche Android-Geräte registriert.
   - **Verwalten aller unterstützter Geräte als Android for Work** (aktiviert) Alle Geräte, die Android for Work unterstützen, werden als Android for Work-Geräte registriert. Jedes Android-Gerät, das Android for Work nicht unterstützt, wird als herkömmliches Android-Gerät registriert.
   - **Unterstützte Geräte nur für Benutzer in diesen Gruppen wie Android for Work verwalten** (nur für gewisse Gruppen aktiviert) Damit können Sie eine eingeschränkte Zielbenutzergruppe für die Verwaltung mit Android for Work festlegen. Geräte, die Android for Work unterstützen, werden nur dann als Android for Work-Geräte registriert, wenn sie von Mitgliedern der ausgewählten Gruppe registriert werden. Alle anderen Geräte werden als Android-Geräte registriert.

> [!NOTE]
> Ein bekanntes Problem verhindert, dass die Option **Unterstützte Geräte nur für Benutzer dieser Gruppen als Android for Work verwalten** ordnungsgemäß ausgeführt wird. Geräte von Benutzern in den angegebenen Azure AD-Gruppen werden als Android anstelle von Android for Work registriert. Für die Aktivierung von Android for Work müssen Sie die Option **Verwalten aller unterstützter Geräte als Android for Work** verwenden.


Nachdem Sie die Einrichtung abgeschlossen haben, müssen Sie Ihre Benutzer darüber informieren, wie diese ihre Geräte registrieren sollen. Informationen hierzu finden Sie unter [Informieren der Benutzer über den Einsatz von Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Diese Informationen gelten für mobile Geräte, die mit Microsoft Intune und Configuration Manager verwaltet werden.

Sobald die Bindung abgeschlossen ist, finden Sie den Namen des Kontos und der Organisation im Intune-Portal. An dieser Stelle können Sie beide Browser schließen.

### <a name="enroll-an-android-for-work-device"></a>Registrieren eines Android for Work-Geräts
Ihre Endbenutzer registrieren Android for Work-Geräte so ähnlich wie Android-Geräte. Benutzer können die Unternehmensportal-App für Android auf Ihre mobilen Geräte herunterladen und diese installieren. Die App fordert sie auf, als Teil der Registrierung ein Arbeitsprofil zu erstellen. Nachdem das Arbeitsprofil erstellt wurde, müssen Benutzer zur verwalteten Version des Unternehmensportals wechseln. Das verwaltetet Unternehmensportal ist mit einem kleinen, orangen Koffer in der rechten unteren Ecke gekennzeichnet.

### <a name="manage-android-for-work-devices"></a>Verwaltung von Android for Work-Geräten
Nachdem Sie die Registrierung mit Android for Work aktiviert haben, können Sie die folgenden Verwaltungsaufgaben für Android for Work-Geräte ausführen:
- [Genehmigen von Apps](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Erstellen von Konfigurationselementen](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Verwalten der Kompatibilitätseinstellungen](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Verwalten von E-Mail-Profilen](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Selektives Zurücksetzen des Arbeitsprofils](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< Vorheriger Schritt](create-service-connection-point.md) [Nächster Schritt >](set-up-additional-management.md)

