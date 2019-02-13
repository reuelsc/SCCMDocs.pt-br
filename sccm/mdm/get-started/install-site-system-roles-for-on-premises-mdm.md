---
title: 'Instalar funções no MDM local '
titleSuffix: Configuration Manager
description: Instalar funções do sistema de sites para o gerenciamento de dispositivo móvel local no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5d81d385c48d9653e1596e6a5d9d1163e84f314
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141748"
---
# <a name="install-site-system-roles-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Instalar funções do sistema de site para o gerenciamento de dispositivo móvel local no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Gerenciamento de Dispositivo Móvel Local do System Center Configuration Manager exige as seguintes funções de sistema de sites na sua infraestrutura do site do Configuration Manager:  

- Ponto de registro  

- Ponto proxy do registro  

- Ponto de distribuição  

- Ponto de gerenciamento de dispositivo  

- Ponto de Conexão de Serviço  

  Se você estiver adicionando o Gerenciamento de Dispositivo Móvel Local à sua organização que tem a maioria dos computadores e dispositivos gerenciados usando o software cliente do Configuration Manager, você poderá ter a maioria das funções de sistema de sites já instaladas como parte de sua infraestrutura existente. Caso contrário, consulte [Adicionar funções do sistema de sites para o System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md) para obter informações completas sobre como adicioná-los ao seu site.  

> [!NOTE]  
>  Se você usar réplicas de banco de dados com a função de sistema de site do ponto de gerenciamento do dispositivo, os dispositivos recém-registrados inicialmente falharão ao se conectarem com o ponto de gerenciamento do dispositivo até que a réplica do banco de dados sincronize com eles. Essa falha de conexão ocorre porque a réplica de banco de dados não tem as informações necessárias sobre o dispositivo recém-registrado para estabelecer uma conexão bem-sucedida. As réplicas sincronizam a cada 5 minutos, portanto os dispositivos não conseguirão se conectar nos primeiros 5 minutos após o registro (geralmente 2 tentativas de conexão). Depois disso, o dispositivo se conectará com êxito.  

 Se você estiver usando funções de sistema de site existentes ou adicionando novas, você deverá configurá-las para serem usadas para gerenciar os dispositivos modernos. Siga as etapas abaixo para configurar o ponto de distribuição e o ponto de gerenciamento de dispositivo para funcionar corretamente com o Gerenciamento de Dispositivo Móvel Local:  

> [!NOTE]  
>  O branch atual do Configuration Manager só dá suporte para conexões de intranet de dispositivos para os pontos de distribuição e pontos de gerenciamento de dispositivo para Gerenciamento de Dispositivo Móvel Local. No entanto, se você também estiver gerenciando computadores Mac OS X, esses clientes exigirão conexões com a Internet para essas funções de sistema de sites. Nesse caso, quando você configura as propriedades do ponto de distribuição e o ponto de gerenciamento do dispositivo, você deve usar a configuração **Permitir conexões de intranet e Internet** como alternativa.  

### <a name="to-configure-site-system-roles-to-manage-modern-devices"></a>Para configurar as funções de sistema de site para gerenciar dispositivos modernos:  

1. No console do Configuration Manager, clique em **Administração** > **Visão Geral** > **Configuração do Site** > **Funções de Servidores e Sistema de Sites**.  

2. Selecione o servidor sistema de sites com ponto de distribuição ou o ponto de gerenciamento de dispositivo que deseja configurar, abra as propriedades para o **Sistema de Sites** e verifique se ele tem um FQDN especificado. Clique em **OK**.  

3. Abra as propriedades para a função de sistema de sites do ponto de distribuição. Na guia geral, verifique se o **HTTPS** foi selecionado e selecione **Permitir somente conexões da intranet**.  

    Se você também estiver gerenciando computadores Mac separadamente com o cliente do Configuration Manager, use **Permitir conexões de intranet e Internet** como alternativa.  

   > [!NOTE]  
   >  Os pontos de distribuição configurados para conexões de intranet exigem limites de site a serem configurados para eles. O branch atual do Configuration Manager só dá suporte a limites de intervalo IPv4 para o Gerenciamento de Dispositivo Móvel Local. Para obter mais informações sobre como configurar limites de site, consulte [Definir limites de site e grupos de limites para o System Center Configuration Manager](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

4. Clique na caixa de seleção próxima da opção **Permitir que os dispositivos móveis sejam conectados neste ponto de distribuição** e clique em **OK**.  

5. Abra as propriedades para a função de sistema de sites do ponto de gerenciamento. Na guia geral, verifique se o **HTTPS** foi selecionado e selecione **Permitir somente conexões da intranet**.  

    Se você também estiver gerenciando computadores Mac separadamente com o cliente do Configuration Manager, use **Permitir conexões de intranet e Internet** como alternativa.  

6. Clique na caixa de seleção próxima da opção **Permitir que dispositivos móveis e computadores Mac usem este ponto de gerenciamento**. Clique em **OK**.  

    Ele transforma, efetivamente, o ponto de gerenciamento em um ponto de gerenciamento do dispositivo.  

   Depois que as funções do sistema de sites foram adicionadas e configuradas para gerenciar dispositivos modernos, você precisará, então, configurar os servidores que hospedam as funções como pontos de extremidade confiáveis para registrar e se comunicar com os dispositivos gerenciados. Consulte [Configurar certificados para comunicações confiáveis do Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md) para obter mais informações.  
