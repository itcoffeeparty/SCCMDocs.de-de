---
title: "Bewährte Methoden für die Clientbereitstellung | Microsoft-Dokumentation"
description: "Bewährte Methoden für die Clientbereitstellung in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: 11
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 49b2520a82614bedc7bcc077604e0b89885119c2


---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>Bewährte Methoden für die Clientbereitstellung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenden Sie die folgenden bewährten Methoden an, um Clients auf Computern in System Center Configuration Manager bereitzustellen.  

## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Verwenden einer auf Softwareupdate basierenden Clientinstallation für Active Directory-Computer  
 Diese Clientbereitstellungsmethode hat den Vorteil, dass sie bereits vorhandene Windows-Technologien verwendet, nur geringfügige Konfigurationen in Configuration Manager erfordert, am einfachsten für Firewalls zu konfigurieren und außerdem die sicherste ist. Durch die Verwendung von Sicherheitsgruppen und der WMI-Filterung für die Gruppenrichtlinienkonfiguration sind Sie außerdem sehr flexibel bei der Steuerung, auf welchen Computern der Configuration Manager-Client installiert wird.  

 Weitere Informationen finden Sie unter [Installieren von Configuration Manager-Clients mithilfe von auf Softwareupdate basierender Installation](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Erweitern Sie das Active Directory-Schema, und veröffentlichen Sie den Standort, damit Sie CCMSetup ohne Befehlszeilenoptionen ausführen können.  
 Wenn Sie das Active Directory-Schema für Configuration Manager erweitert haben, und der Standort in Active Directory Domain Services veröffentlicht wird, werden viele Clientinstallationseigenschaften in Active Directory Domain Services veröffentlicht. Wenn diese Clientinstallationseigenschaften von einem Computer gefunden werden können, kann er sie im Rahmen der Configuration Manager-Clientbereitstellung verwenden. Da diese Informationen automatisch generiert werden, wird das Risiko eines Fehlers durch manuelle Eingabe der Installationseigenschaften beseitigt.  

 Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager, die in Active Directory-Domänendiensten veröffentlicht wurden](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="when-you-have-many-clients-to-deploy-plan-a-phased-rollout-outside-business-hours"></a>Wenn Sie viele Clients bereitstellen müssen, planen Sie ein Rollout in mehreren Phasen und außerhalb der Geschäftszeiten ein.  
 Verringern Sie die Auswirkung auf die Prozessoranforderungen auf dem Standortserver, indem Sie ein Rollout der Clients in mehreren Phasen über einen längeren Zeitraum einplanen. Stellen Sie Clients außerhalb der Geschäftszeiten bereit, sodass den wichtigen Unternehmensdiensten tagsüber mehr Bandbreite zur Verfügung steht und die Benutzer nicht durch Computer behindert werden, die langsam sind oder zur Fertigstellung der Installation neu gestartet werden müssen.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Aktivieren von automatischem Upgrade nach Abschluss Ihrer wichtigsten Clientbereitstellung  
 Automatische Clientupgrades sind nützlich bei einer geringen Anzahl von Clientcomputern, die von Ihrer Hauptmethode für die Clientinstallation nicht erfasst wurden. Dies kann beispielsweise der Fall sein, wenn einige Clients während der Bereitstellung des Clientupgrades offline waren. Daraufhin führen Sie das Clientupgrade für diese Computer mithilfe dieser Methode aus, sobald die Computer wieder aktiv sind.  

> [!NOTE]  
>  Durch Leistungsverbesserungen in Configuration Manager können Sie automatische Upgrades als primäre Upgrademethode für Clients verwenden. Die Leistung hängt jedoch von Ihrer Hierarchieinfrastruktur ab, wie etwa von der Anzahl der Clients.  

 Weitere Informationen zu automatischen Clientupgrademethoden finden Sie unter [Aktualisieren von Clients für Windows-Computer in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Verwenden Sie bei der Installation des Clients mit client.msi-Eigenschaften SMSMP und FSP.  
 Durch die Eigenschaft SMSMP wird der erste Verwaltungspunkt für den Client zur Kommunikation angegeben und die Abhängigkeit von Dienstidentifizierungslösungen wie Active Directory-Domänendiensten, DNS und WINS beseitigt.  

 Verwenden Sie die FSP-Eigenschaft, und installieren Sie einen Fallbackstatuspunkt, sodass Sie die Clientinstallation und -zuordnung überwachen und Kommunikationsprobleme ermitteln können.  

 Weitere Informationen zu diesen Optionen finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="if-you-want-to-use-client-languages-other-than-english-install-the-client-language-packs-before-you-install-the-clients"></a>Wenn Sie von Englisch abweichende Clientsprachen verwenden möchten, installieren Sie die Clientsprachpakete, bevor Sie die Clients installieren.  
 Wenn Sie Clientsprachpakete nach der Installation von Clients an einem Standort installieren, müssen Sie die Clients erneut installieren, bevor diese die zusätzlichen Sprachen verwenden können. Für Clients mobiler Geräte bedeutet dies, dass Sie das mobile Gerät zurücksetzen und erneut anmelden müssen.  

 Weitere Informationen zum Hinzufügen der Unterstützung für zusätzliche Clientsprachen finden Sie unter [Sprachpakete in System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

## <a name="plan-and-prepare-any-required-pki-certificates-in-advance"></a>Planen und Vorbereiten erforderlicher PKI-Zertifikate im Voraus  
 Zur Verwaltung von Geräten im Internet, angemeldeten mobilen Geräte und Macintosh-Computern müssen PKI-Zertifikate in den Standortsystemen (Verwaltungspunkte und Verteilungspunkte) sowie auf den Clientgeräten vorhanden sein. Für viele Kunden bedeutet dies einen gesteigerten Planungs- und Vorbereitungsaufwand, insbesondere wenn ihr PKI von einem separaten Team verwaltet wird. In Produktionsnetzwerken benötigen Sie für die Verwendung neuer Zertifikate möglicherweise die Genehmigung des Änderungsmanagements, müssen die Standortsystemserver neu starten, oder die Benutzer müssen sich eventuell für die neue Gruppenmitgliedschaft ab- und wieder anmelden. Außerdem müssen Sie möglicherweise ausreichend Zeit für das Replizieren von Sicherheitsberechtigungen und für sämtliche neuen Zertifikatvorlagen einplanen.  

 Weitere Informationen zu den erforderlichen PKI-Zertifikaten finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Konfigurieren Sie sämtliche erforderlichen Clienteinstellungen und Wartungsfenster, bevor Sie Clients installieren  
 Obwohl Sie Clienteinstellungen und Wartungsfenster vor oder nach dem Installieren von Clients konfigurieren können, sollten Sie alle erforderlichen Einstellungen vornehmen, bevor Sie Clients installieren, sodass diese Einstellungen verwendet werden, sobald der Client installiert ist. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md)  

 Konfigurieren Sie Wartungsfenster für Server und für Windows Embedded-Geräte, um die Geschäftskontinuität für diese meist geschäftskritischen Computer sicherzustellen. Durch Wartungsfenster wird beispielsweise sichergestellt, dass von erforderlichen Softwareupdates und Antischadsoftware die Computer nicht innerhalb der Geschäftszeiten neu gestartet werden.  

> [!IMPORTANT]  
>  Bei Windows 10-Computern, die Sie mit UWF (Unified Write Filter) schützen möchten, müssen Sie das Gerät für UWF konfigurieren, bevor Sie den Client installieren. Auf diese Weise kann Configuration Manager den Client mit einem benutzerdefinierten Anmeldeinformationsanbieter installieren, durch den Benutzer mit geringen Rechten von der Anmeldung beim Gerät im Wartungsmodus ausgeschlossen werden.  

## <a name="for-mac-computers-and-mobile-devices-that-are-enrolled-by-configuration-manager-plan-your-user-enrollment-experience"></a>Planen Sie eine benutzerfreundliche Anmeldung für Macintosh-Computer und mobile Geräte, die von Configuration Manager angemeldet werden  
 Wenn Benutzer ihre eigenen Macintosh-Computer und mobilen Geräte über Configuration Manager registrieren, planen Sie einen benutzerfreundlichen Weg, und bereiten Sie diesen vor. Sie können für den Installations- und Anmeldungsprozess per Webseite beispielsweise ein Skript erstellen, sodass die Benutzer ein Mindestmaß der erforderlichen Informationen eingeben müssen, und Sie ihnen Anweisungen über einen Link in einer E-Mail senden können.  

## <a name="when-you-manage-windows-embedded-devices-use-file-based-write-filters-fbwf-rather-than-enhanced-write-filters-ewf-for-higher-scalability"></a>Wenn Sie Windows Embedded-Geräte verwalten, verwenden Sie für eine bessere Skalierbarkeit dateibasierte Schreibfilter (File Based Write Filter, FBWF) anstelle von erweiterten Schreibfiltern (Enhanced Write Filter, EWF).  
 Für Embedded-Geräte, die erweiterte Schreibfilter (EWF) verwenden, treten wahrscheinlich Neusynchronisierungen von Zustandsmeldungen auf. Wenn Sie nur einige Embedded-Geräte mit erweiterten Schreibfiltern verwenden, bemerken Sie dies möglicherweise nicht. Wenn Sie jedoch viele Embedded-Geräte haben, von denen die Informationen neu synchronisiert werden, wie etwa das Versenden des vollständigen Inventars anstelle des Deltainventars, dann kann dies zu einem merkbaren Anstieg an Netzwerkpaketen und einer höheren Prozessorauslastung auf dem Standortserver führen.  

 Wenn Sie die Wahl haben, welche Art von Schreibfilter Sie aktivieren möchten, wählen Sie für die Netzwerk- und Prozessoreffizienz auf dem Configuration Manager-Client die dateibasierten Schreibfilter aus, und konfigurieren Sie Ausnahmen, um den Clientzustand sowie Inventurdaten zwischen den Geräteneustarts beizubehalten. Weitere Informationen zu Schreibfiltern finden Sie unter   [Planen der Clientbereitstellung für Windows Embedded-Geräte in System Center Configuration Manager](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Weitere Informationen zur maximalen Anzahl von Windows Embedded-Clients, die von einem primären Standort unterstützt werden können, finden Sie unter [Supported operating systems for sites and clients for System Center Configuration Manager](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) (Unterstützte Betriebssysteme für Standorte und Clients für System Center Configuration Manager).  



<!--HONumber=Dec16_HO3-->


