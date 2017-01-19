---
title: "Hardwareinventur konfigurieren | Microsoft-Dokumentation | mobile Geräte"
description: "Konfigurieren von Hardwareinventur für mobile Geräte, die von Microsoft Intune und System Center Configuration Manager registriert werden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
caps.latest.revision: 7
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 6db22a2ddce1afb471cf8b603c6d98f7f0acbc15


---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-system-center-configuration-manager"></a>Konfigurieren von Hardwareinventur für mobile Geräte, die von Microsoft Intune und System Center Configuration Manager registriert werden

*Gilt für: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager können Sie die Hardwareinventur auf iOS-, Android- und Windows-Geräten mithilfe des Microsoft Intune-Connectors erfassen. Informationen zum Konfigurieren der Hardwareinventur finden Sie unter [Erweitern der Hardwareinventur in System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 Informationen zum Registrieren von Geräten bei Microsoft Intune finden Sie unter [Verwalten von mobilen Geräten mit Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

## <a name="hardware-inventory-for-mobile-devices"></a>Hardwareinventur für mobile Geräte  
 In den folgenden Tabellen sind die für die Hardwareinventur auf häufig verwendeten mobilen Plattformen verfügbaren Inventurklassen aufgelistet.  

 **iOS**  

|Hardwareinventurklasse|iOS|  
|------------------------------|---------|  
|Name|Device_ComputerSystem.DeviceName|  
|Eindeutige Geräte-ID|Device_ComputerSystem.UDID|  
|Seriennummer|Device_ComputerSystem.SerialNumber|  
|E-Mail-Adresse|Device_Email.OwnerEmailAddress|  
|Betriebssystemtyp|Nicht zutreffend|  
|Version des Betriebssystems|Device_OSInformation.OSVersion|  
|Buildversion|Nicht zutreffend|  
|Service Pack-Hauptversion|Nicht zutreffend|  
|Service Pack-Nebenversion|Nicht zutreffend|  
|Betriebssystemsprache|Nicht zutreffend|  
|Gesamtmenge des Speicherplatzes|Device_Memory.DeviceCapacity|  
|Freier Speicherplatz|Device_Memory.AvailableDeviceCapacity|  
|International Mobile Equipment Identity oder IMEI|Device_ComputerSystem.IMEI|  
|Mobile Equipment Identifier (MEID)|Device_ComputerSystem.MEID|  
|Hersteller|Nicht zutreffend|  
|Modell|ModelName|  
|Telefonnummer<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Netzbetreiber des Abonnenten|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Mobilfunktechnologie|Device_ComputerSystem.CellularTechnology|  
|WiFi-MAC|Device_WLAN.WiFiMAC|  

 **Android**  

> [!NOTE]  
>  **HINWEIS:** Android-Inventurklassen sind bei Verwendung der Android-Unternehmensportal-App verfügbar.  

|Hardwareinventurklasse|Android|  
|------------------------------|-------------|  
|Name|Nicht zutreffend|  
|Eindeutige Geräte-ID|Nicht zutreffend|  
|Seriennummer|Device_ComputerSystem.SerialNumber|  
|E-Mail-Adresse|Nicht zutreffend|  
|Betriebssystemtyp|Device_OSInformation.Platform|  
|Version des Betriebssystems|Device_OSInformation.Version|  
|Buildversion|Nicht zutreffend|  
|Service Pack-Hauptversion|Nicht zutreffend|  
|Service Pack-Nebenversion|Nicht zutreffend|  
|Betriebssystemsprache|Nicht zutreffend|  
|Gesamtmenge des Speicherplatzes|Device_Memory.StorageTotal|  
|Freier Speicherplatz|Device_Memory.StorageFree|  
|International Mobile Equipment Identity oder IMEI|Device_ComputerSystem.IMEI|  
|Mobile Equipment Identifier (MEID)|Nicht zutreffend|  
|Hersteller|Device_Info.Manufacturer|  
|Modell|Device_Info.Model|  
|Telefonnummer<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Netzbetreiber des Abonnenten|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Mobilfunktechnologie|Device_ComputerSystem.CellularTechnology|  
|WiFi-MAC|Device_WLAN.WiFiMAC|  

 **Windows Phone 8/8.1**  

|Hardwareinventurklasse|Windows Phone 8 und Windows Phone 8.1|  
|------------------------------|-------------------------------------------|  
|Name|Device_ComputerSystem.DeviceName|  
|Eindeutige Geräte-ID|Device_ComputerSystem.DeviceClientID|  
|Seriennummer|Nicht zutreffend|  
|E-Mail-Adresse|Device_Email.OwnerEmailAddress|  
|Betriebssystemtyp|Device_OSInformation.Platform|  
|Version des Betriebssystems|Device_ComputerSystem.SoftwareVersion|  
|Buildversion|Nicht zutreffend|  
|Service Pack-Hauptversion|Nicht zutreffend|  
|Service Pack-Nebenversion|Nicht zutreffend|  
|Betriebssystemsprache|Device_OSInformation.Language|  
|Gesamtmenge des Speicherplatzes|Nicht zutreffend|  
|Freier Speicherplatz|Nicht zutreffend|  
|International Mobile Equipment Identity oder IMEI|Nicht zutreffend|  
|Mobile Equipment Identifier (MEID)|Nicht zutreffend|  
|Hersteller|Device_ComputerSystem.DeviceManufacturer|  
|Modell|Device_ComputerSystem.DeviceModel|  
|Telefonnummer<sup>1</sup>|Nicht zutreffend|  
|Netzbetreiber des Abonnenten|Nicht zutreffend|  
|Mobilfunktechnologie|Nicht zutreffend|  
|WiFi-MAC|Nicht zutreffend|  

 **Windows RT**  

|Hardwareinventurklasse|Windows RT|  
|------------------------------|----------------|  
|Name|Device_ComputerSystem.DeviceName|  
|Eindeutige Geräte-ID|Device_ComputerSystem.DeviceName|  
|Seriennummer|Nicht zutreffend|  
|E-Mail-Adresse|Device_Email.OwnerEmailAddress|  
|Betriebssystemtyp|CCM_OperatingSystem.SystemType|  
|Version des Betriebssystems|Win32_OperatingSystem.Version|  
|Buildversion|Win32_OperatingSystem.BuildNumber|  
|Service Pack-Hauptversion|Win32_OperatingSystem.ServicePackMajorVersion|  
|Service Pack-Nebenversion|Win32_OperatingSystem.ServicePackMinorVersion|  
|Betriebssystemsprache|Nicht zutreffend|  
|Gesamtmenge des Speicherplatzes|Win32_PhysicalMemory.Capacity|  
|Freier Speicherplatz|Win32_OperatingSystem.FreePhysicalMemory|  
|International Mobile Equipment Identity oder IMEI|Nicht zutreffend|  
|Mobile Equipment Identifier (MEID)|Nicht zutreffend|  
|Hersteller|Win32_ComputerSystem.Manufacturer|  
|Modell|Win32_ComputerSystem.Model|  
|Telefonnummer<sup>1</sup>|Nicht zutreffend|  
|Netzbetreiber des Abonnenten|Nicht zutreffend|  
|Mobilfunktechnologie|Nicht zutreffend|  
|WiFi-MAC|Win32_NetworkAdapter.MACAddress|  

 <sup>1</sup> Die Telefonnummer wird mit Ausnahme der letzten 4 Ziffern mit „*“ maskiert.  

 Damit bei der Inventur die Telefonnummer erfasst wird, muss in das Gerät eine SIM-Karte eingelegt sein, und der Netzbetreiber muss für diese SIM-Karte eine Rufnummer bereitgestellt haben.  



<!--HONumber=Dec16_HO3-->


