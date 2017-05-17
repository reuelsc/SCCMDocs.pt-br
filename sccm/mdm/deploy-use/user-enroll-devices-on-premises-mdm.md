---
title: "Como os usuários registram dispositivos com o MDM local – Configuration Manager | Microsoft Docs"
description: "Entenda como os usuários registram dispositivos com o Gerenciamento de Dispositivo Móvel local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 507bad02c6e028f09a8b0c8a566ac55f7c3942a5
ms.openlocfilehash: 8c7438c2cc0bc66654eb3e74de10553df53181d9
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="how-users-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Como os usuários registram dispositivos com o Gerenciamento de Dispositivo Móvel local no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Com o Gerenciamento de Dispositivo Móvel Local do System Center Configuration Manager, os usuários poderão registrar dispositivos se receberam permissão de registro (por meio das configurações do cliente atualizadas) e se seus dispositivos tiverem o certificado raiz necessário instalado para ter uma comunicação confiável com os servidores que hospedam as funções do sistema de sites necessárias. Para obter mais informações sobre como configurar o registro, veja [Configurar o registro de dispositivo para o Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md).  

> [!NOTE]  
>  O branch atual do Configuration Manager dá suporte ao registro no Gerenciamento de Dispositivo Móvel Local para dispositivos que executam os seguintes sistemas operacionais:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(a partir do Configuration Manager versão 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

As seguintes tarefas explicam como registrar e verificar o registro de computadores e dispositivos para o Gerenciamento de Dispositivo Móvel Local:  

-   [Registrar um computador com Windows 10](#bkmk_enrollDesk)  

-   [Registrar um dispositivo Windows 10 Mobile](#bkmk_enrollMob)  

-   [Verificar registro do dispositivo](#bkmk_verify)  

##  <a name="bkmk_enrollDesk"></a> Registrar um computador com Windows 10  

1.  Em um computador com Windows 10, vá para **Configurações**.  

2.  Clique em **Contas**e em **Acesso corporativo**.  

3.  Em Acesso Corporativo sob **Conectar-se ao trabalho ou à escola**, clique em **Conectar**, insira seu endereço de email comercial e clique em **Continuar**.  

4.  Insira o FQDN do servidor que hospeda a função do sistema de sites do ponto de registro e clique em **Continuar**.  

5.  Em Conectando a um serviço, insira sua senha de email comercial e clique em **Entrar**.  

6.  Clique em **Ignorar** para memorizar as informações de entrada e, após alguns instantes, o dispositivo estará conectado.  

##  <a name="bkmk_enrollMob"></a> Registrar um dispositivo Windows 10 Mobile  

1.  Em um dispositivo Windows 10 Mobile, vá para **Configurações**.  

2.  Clique em **Contas**e em **Acesso corporativo**.  

3.  Clique em **Conectar**.  

4.  Insira seu endereço de email comercial e o FQDN do servidor que hospeda a função do sistema de sites do ponto proxy do registro. Clique em **Conectar**.  

5.  Na próxima tela, insira seu endereço de email comercial e a senha e clique em **Entrar**. Após alguns instantes, o dispositivo é registrado. Clique em **Concluído**.  

##  <a name="bkmk_verify"></a> Verificar registro do dispositivo  
 É possível verificar se os dispositivos foram registrados com êxito no console do Configuration Manager.  

1.  Inicie o console do Configuration Manager.  

2.  Clique em **Ativos e Conformidade** > **Visão Geral** > **Dispositivos**. O dispositivo registrado aparecerá na lista.  

