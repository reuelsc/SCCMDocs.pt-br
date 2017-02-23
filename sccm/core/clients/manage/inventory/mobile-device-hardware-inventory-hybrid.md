---
title: "Configurar o inventário de dispositivo móvel – Configuration Manager | Microsoft Docs"
description: "Configurar o inventário de hardware para dispositivos móveis registrados pelo Microsoft Intune e pelo System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
caps.latest.revision: 7
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3743c80b0c2b5142f3a537ba3855ffd14794d42b
ms.openlocfilehash: 13fd8d5e2ee6c2381129282aefa5e7b1aaf361eb


---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-system-center-configuration-manager"></a>Como configurar o inventário de hardware para dispositivos móveis registrados pelo Microsoft Intune e pelo System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

No Configuration Manager, você pode coletar o inventário de hardware em dispositivos iOS, Android e Windows usando o conector do Microsoft Intune. Para obter informações sobre como configurar o inventário de hardware personalizado, consulte [Como estender o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 Para obter informações sobre como registrar dispositivos no Microsoft Intune, consulte [Gerenciar dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

## <a name="hardware-inventory-for-mobile-devices"></a>Inventário de hardware para dispositivos móveis  
 As tabelas a seguir listam as classes de inventário de hardware disponíveis em plataformas móveis comumente usadas.  

 **iOS**  

|Classe de inventário de hardware|iOS|  
|------------------------------|---------|  
|Nome|Device_ComputerSystem.DeviceName|  
|Identificação de dispositivo exclusivo|Device_ComputerSystem.UDID|  
|Número de Série|Device_ComputerSystem.SerialNumber|  
|Endereço de email|Device_Email.OwnerEmailAddress|  
|Tipo de sistema operacional|Não aplicável|  
|Versão do Sistema Operacional|Device_OSInformation.OSVersion|  
|Versão da compilação|Não aplicável|  
|Versão principal do service pack|Não aplicável|  
|Versão secundária do service pack|Não aplicável|  
|Idioma do sistema operacional|Não aplicável|  
|Espaço de armazenamento total|Device_Memory.DeviceCapacity|  
|Espaço livre de armazenamento|Device_Memory.AvailableDeviceCapacity|  
|Identidade de Equipamentos Móveis Internacional ou IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|Identificador de equipamentos móveis (MEID)|Device_ComputerSystem.MEID|  
|Fabricante|Não aplicável|  
|Modelo|ModelName|  
|Número de telefone<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Operadora do assinante|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Tecnologia celular|Device_ComputerSystem.CellularTechnology|  
|MAC Wi-Fi|Device_WLAN.WiFiMAC|  

 **Android**  

> [!NOTE]  
>  **Observação:** classes de inventário Android estão disponível ao usar o aplicativo Portal da Empresa do Android.  

|Classe de inventário de hardware|Android|  
|------------------------------|-------------|  
|Nome|Não aplicável|  
|Identificação de dispositivo exclusivo|Não aplicável|  
|Número de Série|Device_ComputerSystem.SerialNumber|  
|Endereço de email|Não aplicável|  
|Tipo de sistema operacional|Device_OSInformation.Platform|  
|Versão do Sistema Operacional|Device_OSInformation.Version|  
|Versão da compilação|Não aplicável|  
|Versão principal do service pack|Não aplicável|  
|Versão secundária do service pack|Não aplicável|  
|Idioma do sistema operacional|Não aplicável|  
|Espaço de armazenamento total|Device_Memory.StorageTotal|  
|Espaço livre de armazenamento|Device_Memory.StorageFree|  
|Identidade de Equipamentos Móveis Internacional ou IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|Identificador de equipamentos móveis (MEID)|Não aplicável|  
|Fabricante|Device_Info.Manufacturer|  
|Modelo|Device_Info.Model|  
|Número de telefone<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Operadora do assinante|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Tecnologia celular|Device_ComputerSystem.CellularTechnology|  
|MAC Wi-Fi|Device_WLAN.WiFiMAC|  

 **Windows Phone 8/8.1**  

|Classe de inventário de hardware|Windows Phone 8 e Windows Phone 8.1|  
|------------------------------|-------------------------------------------|  
|Nome|Device_ComputerSystem.DeviceName|  
|Identificação de dispositivo exclusivo|Device_ComputerSystem.DeviceClientID|  
|Número de Série|Não aplicável|  
|Endereço de email|Device_Email.OwnerEmailAddress|  
|Tipo de sistema operacional|Device_OSInformation.Platform|  
|Versão do Sistema Operacional|Device_ComputerSystem.SoftwareVersion|  
|Versão da compilação|Não aplicável|  
|Versão principal do service pack|Não aplicável|  
|Versão secundária do service pack|Não aplicável|  
|Idioma do sistema operacional|Device_OSInformation.Language|  
|Espaço de armazenamento total|Não aplicável|  
|Espaço livre de armazenamento|Não aplicável|  
|Identidade de Equipamentos Móveis Internacional ou IMEI (IMEI)|Não aplicável|  
|Identificador de equipamentos móveis (MEID)|Não aplicável|  
|Fabricante|Device_ComputerSystem.DeviceManufacturer|  
|Modelo|Device_ComputerSystem.DeviceModel|  
|Número de telefone<sup>1</sup>|Não aplicável|  
|Operadora do assinante|Não aplicável|  
|Tecnologia celular|Não aplicável|  
|MAC Wi-Fi|Não aplicável|  

 **Windows RT**  

|Classe de inventário de hardware|Windows RT|  
|------------------------------|----------------|  
|Nome|Device_ComputerSystem.DeviceName|  
|Identificação de dispositivo exclusivo|Device_ComputerSystem.DeviceName|  
|Número de Série|Não aplicável|  
|Endereço de email|Device_Email.OwnerEmailAddress|  
|Tipo de sistema operacional|CCM_OperatingSystem.SystemType|  
|Versão do Sistema Operacional|Win32_OperatingSystem.Version|  
|Versão da compilação|Win32_OperatingSystem.BuildNumber|  
|Versão principal do service pack|Win32_OperatingSystem.ServicePackMajorVersion|  
|Versão secundária do service pack|Win32_OperatingSystem.ServicePackMinorVersion|  
|Idioma do sistema operacional|Não aplicável|  
|Espaço de armazenamento total|Win32_PhysicalMemory.Capacity|  
|Espaço livre de armazenamento|Win32_OperatingSystem.FreePhysicalMemory|  
|Identidade de Equipamentos Móveis Internacional ou IMEI (IMEI)|Não aplicável|  
|Identificador de equipamentos móveis (MEID)|Não aplicável|  
|Fabricante|Win32_ComputerSystem.Manufacturer|  
|Modelo|Win32_ComputerSystem.Model|  
|Número de telefone<sup>1</sup>|Não aplicável|  
|Operadora do assinante|Não aplicável|  
|Tecnologia celular|Não aplicável|  
|MAC Wi-Fi|Win32_NetworkAdapter.MACAddress|  

 <sup>1</sup> O número do telefone é mascarado com *, exceto os últimos 4 dígitos.  

 Para o inventário coletar o número de telefone, o dispositivo deve ter um cartão SIM inserido e um número de telefone provisionado pela carrier ao SIM.  



<!--HONumber=Jan17_HO4-->


