---
title: Planen des Cloudverwaltungsgateways | Microsoft-Dokumentation
description: 
ms.date: 11/22/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1f8fbd8a16548ab2c34f5d3dac2b439f3908cea9
ms.openlocfilehash: e6befef692518a5622250af1c71d517b435f9058

---

# <a name="plan-for-cloud-management-gateway-in-configuration-manager"></a>Planen des Cloudverwaltungsgateways in Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1610 stellt das Cloudverwaltungsgateway eine einfache Methode für die Verwaltung von Configuration Manager-Clients im Internet dar. Dieser Dienst, der in Microsoft Azure bereitgestellt wird und ein Azure-Abonnement erfordert, stellt mithilfe einer neuen Rolle namens Cloudverwaltungsgateway-Connectorpunkt eine Verbindung zu Ihrer lokalen Configuration Manager-Infrastruktur her. Nachdem er bereitgestellt und konfiguriert wurde, können Clients auf lokale Configuration Manager-Standortsystemrollen zugreifen, unabhängig davon, ob sie mit dem internen, privaten Netzwerk oder über das Internet verbunden sind.

Sie verwenden die Configuration Manager-Konsole zum Bereitstellen des Diensts in Azure, fügen die Cloudverwaltungsgateway-Connectorpunktrolle hinzu und konfigurieren Standortsystemrollen, um den Cloudverwaltungsgateway-Datenverkehr zuzulassen. Der Cloudverwaltungsgateway unterstützt derzeit nur die Rollen „Verwaltungspunkt“ und „Softwareupdatepunkt“.

Client-Zertifikate und Zertifikate für Secure Socket Layer (SSL) sind erforderlich, um Computer zu authentifizieren und die Kommunikation zwischen den verschiedenen Ebenen des Diensts verschlüsseln. In der Regel erhalten die Clientcomputer ein Clientzertifikat über das Durchsetzen von Gruppenrichtlinien. Zum Verschlüsseln des Datenverkehrs zwischen Clients und Standortsystemserver, der die Rollen hostet, müssen Sie ein benutzerdefiniertes SSL-Zertifikat von der Zertifizierungsstelle erstellen. Zusätzlich zu diesen beiden Zertifikattypen müssen Sie auch ein Verwaltungszertifikat in Azure einrichten, mit dem Configuration Manager den Cloudverwaltungsgateway-Dienst bereitstellen kann.

## <a name="requirements-for-cloud-management-gateway"></a>Anforderungen für das Cloudverwaltungsgateway

-   Die Clientcomputer und der Standortsystemserver führen den Cloudverwaltungsgateway-Connectorpunkt aus.

-   Benutzerdefinierte SSL-Zertifikate der internen Zertifizierungsstelle: Werden zum Verschlüsseln der Kommunikation der Clientcomputer und zum Authentifizieren der Identität des Cloudverwaltungsgateway-Diensts verwendet.

-   Azure-Abonnement für Clouddienste.

-   Azure-Verwaltungszertifikat ‒ Wird zur Authentifizierung von Configuration Manager mit Azure verwendet.

## <a name="limitations-of-cloud-management-gateway"></a>Einschränkungen des Cloudverwaltungsgateways

-   Der Cloudverwaltungsgateway unterstützt nur die Rollen „Verwaltungspunkt“ und „Softwareupdatepunkt“.

-   Die folgenden Funktionen in Configuration Manager werden derzeit für den Cloudverwaltungsgateway nicht unterstützt:

    -   Clientbereitstellung und -aktualisierung mit Clientpush

    -   Automatische Standortzuweisung

    -   Richtlinien für Benutzer

    -   Anwendungskatalog (einschließlich Softwaregenehmigungsanforderungen)

    -   Vollständige Betriebssystembereitstellung (OSD)

    -   Configuration Manager-Konsole

    -   Remotetools

    -   Berichterstellungswebsite

    -   Wake-On-LAN

    -   Mac-, Linux- und UNIX-Clients

    -   Azure Resource Manager

    -   Peercache

    -   Lokale Verwaltung mobiler Geräte

## <a name="cost-of-cloud-management-gateway"></a>Kosten des Cloudverwaltungsgateways

>[!IMPORTANT]
>Die nachfolgenden Kosteninformationen stellen lediglich Schätzwerte dar. Ihre Umgebung weist möglicherweise andere Variablen auf, die sich auf die Gesamtkosten für die Verwendung eines Cloudverwaltungsgateways auswirken.

Das Cloudverwaltungsgateway verwendet die folgende Funktionen von Microsoft Azure, die das Azure-Abonnementkonto belasten:

-   Virtuelle Maschine

    -   Das Cloudverwaltungsgateway erfordert derzeit einen virtuellen Computer der Größe Standard\_A2. Beim Erstellen des Diensts können Sie auswählen, wie viele virtuelle Computer der Dienst unterstützen soll (die Standardeinstellung lautet „1“).

    -   Beachten Sie für Ihre Schätzung, dass ein einzelner virtueller Azure-Computer der Größe Standard\_A2 ca. 2.000 internetbasierte Clients gleichzeitig unterstützen kann.

    -   Der [Azure-Preisrechner](https://azure.microsoft.com/en-us/pricing/calculator/) hilft Ihnen, die potenziellen Kosten zu ermitteln.

      >[!NOTE]
      >Die Kosten für virtuelle Computer variieren je nach Region.

-   Ausgehende Datenübertragungen

    -   Für die von dem Dienst übertragenen Daten fallen Gebühren an. Beachten Sie die [Preisübersicht „Bandbreite“ für Azure](https://azure.microsoft.com/en-us/pricing/details/bandwidth/), um die potenziellen Kosten zu ermitteln.

    -   Rechnen Sie als Schätzwert mit ca. 100 MB pro Client und Monat für internetbasierte Clients, mit denen stündlich Richtlinien aktualisiert werden.

    >[!NOTE]
    > Durch das Ausführen weiterer unterstützter Aktionen über das Cloudverwaltungsgateway (wie z.B. die Bereitstellung von Softwareaktualisierungen oder Anwendungen) erhöht sich die Menge der ausgehenden Datenübertragungen aus Azure.

-   Inhaltsspeicher

    -   Internetbasierte Clients, die mit dem Cloudverwaltungsgateway verwaltet werden, erhalten Softwareaktualisierungsinhalte von Windows Update kostenlos.

    -   Alle anderen benötigten Inhalte (wie Anwendungen) müssen mit einem cloudbasierten Verteilungspunkt verteilt werden. Das Cloudverwaltungsgateway unterstützt derzeit nur den Cloudverteilungspunkt für das Senden von Inhalten an Clients.

    - Im Artikel über die [cloudbasierte Verteilung](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution) finden Sie weitere Informationen zu den Kosten.

## <a name="next-steps"></a>Nächste Schritte

[Einrichten des Cloudverwaltungsgateways](setup-cloud-management-gateway.md)



<!--HONumber=Dec16_HO3-->


