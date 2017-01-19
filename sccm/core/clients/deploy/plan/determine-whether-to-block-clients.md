---
title: Blockieren von Clients | Microsoft-Dokumentation
description: "Hier finden Sie Informationen zum Blockieren des Clientzugriffs aus Gründen der Systemsicherheit mithilfe von System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
caps.latest.revision: 8
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: c1b3b3e7fe756ce3e0c82ffc15693999d8e817d2


---
# <a name="determine-whether-to-block-clients-in-system-center-configuration-manager"></a>Bestimmen, ob Clients blockiert werden sollen, in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn ein Clientcomputer oder ein mobiles Clientgerät nicht mehr vertrauenswürdig ist, kann der Client in der System Center 2012 Configuration Manager-Konsole blockiert werden. Blockierte Clients werden von der Configuration Manager-Infrastruktur abgewiesen, sodass sie nicht mit Standortsystemen kommunizieren können, um Richtlinien herunterzuladen, Inventurdaten hochzuladen oder Zustands- bzw. Statusmeldungen zu senden.  

 Sie können einen Client nur von dem ihm zugewiesenen Standort aus blockieren und zulassen, nicht jedoch von einem sekundären Standort oder einem Standort der zentralen Verwaltung.  

> [!IMPORTANT]  
>  Das Blockieren in Configuration Manager trägt zwar zu einer erhöhten Sicherheit des Configuration Manager-Standorts bei. Sie sollten sich jedoch beim Schutz des Standorts vor nicht vertrauenswürdigen Computern oder mobilen Geräten nicht auf dieses Feature verlassen, wenn Sie Clients die Kommunikation mit Standortsystemen über HTTP gestatten. In diesem Fall könnte der Client nämlich mit einem neuen selbstsignierten Zertifikat und einer neuen Hardware-ID dem Standort erneut beitreten. Verwenden Sie stattdessen das Feature „Blockierung“ zum Blockieren verlorener oder gefährdeter Startmedien, die Sie zum Bereitstellen von Betriebssystemen und in dem Fall verwenden, wenn HTTPS-Clientverbindungen von Standortsystemen akzeptiert werden.  

 Clients, von denen das ISV-Proxyzertifikat für den Zugriff auf den Standort verwendet wird, können nicht blockiert werden. Weitere Informationen zum ISV-Proxyzertifikat finden Sie im System Center Configuration Manager Software Development Kit (SDK).  

 Wenn an Ihrem Standort HTTPS-Clientverbindungen zugelassen werden und eine Zertifikatsperrliste (Certificate Revocation List, CRL) von Ihrer Public Key-Infrastruktur (PKI) unterstützt wird, ziehen Sie zunächst eine Zertifikatsperre zur Verteidigung gegen gefährdete Zertifikate in Betracht. Das Blockieren von Clients in Configuration Manager bietet eine zweite Stufe der Verteidigung, mit der die Standorthierarchie geschützt wird.  

##  <a name="a-namebkmkblockvscrla-considerations-for-blocking-clients"></a><a name="BKMK_Block_vs_CRL"></a> Überlegungen zum Blockieren von Clients  

-   Diese Option ist für HTTP- und HTTPS-Clientverbindungen verfügbar, jedoch ist die Sicherheit bei Clientverbindungen mit Standortsystemen über HTTP eingeschränkt.  

-   Der Configuration Manager-Administrator kann einen Client blockieren. Diese Aktion findet innerhalb der Configuration Manager-Konsole statt.  

-   Die Clientkommunikation wird lediglich von der Configuration Manager-Hierarchie zurückgewiesen.  

    > [!NOTE]  
    >  Derselbe Client könnte sich bei einer anderen Configuration Manager-Hierarchie registrieren.  

-   Der Client wird sofort vom Configuration Manager-Standort blockiert.  

-   Schützt Standortsysteme vor möglicherweise kompromittierten Computern und mobilen Geräten.  

## <a name="considerations-for-using-certificate-revocation"></a>Überlegungen zum Verwenden der Zertifikatsperrung  

-   Diese Option ist für HTTPS-Windows-Clientverbindungen verfügbar, wenn eine Zertifikatsperrliste (Certificate Revocation List, CRL) von der Public Key-Infrastruktur unterstützt wird.  

     Macintosh-Clients führen die Überprüfung der Zertifikatsperrlisten immer aus. Diese Funktionalität kann nicht deaktiviert werden.  

     Obwohl von Clients für mobile Geräte keine Zertifikatssperrlisten zum Überprüfen der Zertifikate für Standortsysteme verwendet werden, können ihre Zertifikate von Configuration Manager gesperrt und überprüft werden.  

-   Der Public Key-Infrastrukturadministrator kann ein Zertifikat sperren. Diese Aktion findet außerhalb der Configuration Manager-Konsole statt.  

-   Die Clientkommunikation kann von einem beliebigen Computer oder mobilen Gerät zurückgewiesen werden, für den dieses Clientzertifikat erforderlich ist.  

-   Zwischen dem Sperren eines Zertifikats und dem Herunterladen der geänderten Zertifikatsperrliste (Certificate Revocation List, CRL) tritt möglicherweise eine Verzögerung auf.  

-   Bei vielen PKI-Bereitstellungen handelt es sich dabei um mindestens einen Tag. Bei Active Directory-Zertifikatdienste beläuft sich der Standardablaufzeitraum auf eine Woche für eine vollständige Zertifikatsperrliste und einen Tag für eine Delta-Zertifikatsperrliste.  

-   Schützt Standortsysteme und Clients vor gefährdeten Computern und mobilen Geräten.  

    > [!NOTE]  
    >  Darüber hinaus können Sie Standortsysteme, auf denen IIS ausgeführt wird, durch Verwenden einer Zertifikatvertrauensliste (Certificate Trust List, CTL) in IIS vor unbekannten Clients schützen.  



<!--HONumber=Dec16_HO3-->


