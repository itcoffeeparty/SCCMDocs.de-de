---
title: "Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk | Configuration Manager"
description: Verwenden Sie Bereitstellungen mit startbaren Medien in System Center Configuration Manager zum Bereitstellen des Betriebssystem beim Starten des Zielcomputers.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f5bdba0f609f51b988dbfdc0b0c8b204405f834a


---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei Bereitstellungen mit startbaren Medien in System Center Configuration Manager können Sie das Betriebssystem beim Starten des Zielcomputers bereitstellen. Beim Starten des Zielcomputers werden die Tasksequenz, das Betriebssystemabbild sowie sämtlicher anderer erforderlicher Inhalt aus dem Netzwerk abgerufen. Da dieser Inhalt nicht auf den Medien enthalten ist, können Sie den Inhalt aktualisieren, ohne die Medien neu erstellen zu müssen.  

 Sie können in den folgenden Betriebssystembereitstellungsszenarien die Betriebssysteme mithilfe von Multicasting über das Netzwerk bereitstellen:  

-   [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](replace-an-existing-computer-and-transfer-settings.md)  

 Führen Sie die Schritte in einem der Betriebssystembereitstellungsszenarien aus, und verwenden Sie dann die folgenden Abschnitte, um startbare Medien zum Bereitstellen des Betriebssystems zu verwenden.  

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen  
 Wenn Sie startbare Medien verwenden, um den Bereitstellungsprozess für das Betriebssystem zu starten, müssen Sie die Bereitstellung konfigurieren, um das Betriebssystem für die Medien zur Verfügung zu stellen. Sie können dies auf der Seite der **Bereitstellungseinstellungen** des Assistenten oder der Registerkarte für die **Bereitstellungseinstellungen** in den Eigenschaften für die Bereitstellung konfigurieren.  Konfigurieren Sie eine der folgenden Optionen für die Einstellung **Verfügbar machen für** :  

-   **Configuration Manager-Clients, Medien und PXE**  

-   **Nur Medien und PXE**  

-   **Nur Medien und PXE (ausgeblendet)**  

## <a name="create-the-bootable-media"></a>Erstellen der startbaren Medien  
 Sie können angeben, ob das startbare Medium ein USB-Flashlaufwerk oder ein CD/DVD-Satz ist. Der Computer, der die Medien startet, muss die Option unterstützen, die Sie als startbares Laufwerk auswählen. Weitere Informationen finden Sie unter [Erstellen startbarer Medien](create-bootable-media.md).  

##  <a name="a-namebkmkdeploya-install-the-operating-system-from-bootable-media"></a><a name="BKMK_Deploy"></a> Installieren des Betriebssystems von startbaren Medien  
 Legen Sie die startbaren Medien in ein startfähiges Laufwerk des Computer ein. Schalten Sie dann den Computer ein, um das Betriebssystem zu installieren.  



<!--HONumber=Nov16_HO1-->


