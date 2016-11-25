---
title: Gerenciar aplicativos iOS adquiridos por volume | System Center Configuration Manager
description: "Implante, gerencie e monitore licenças de aplicativos adquiridos por meio da loja de aplicativos iOS."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5e7cead-e257-405b-a2aa-b0130e48dc40
caps.latest.revision: 23
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4289f4853f77392df420e44e179961609f83683f


---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Manage volume-purchased iOS apps with System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*



 A lojas de aplicativos iOS possibilita adquirir várias licenças de um aplicativo que você deseja executar em sua empresa. Isso ajuda a reduzir a sobrecarga administrativa de controlar várias cópias de aplicativos adquiridas.  

 O System Center Configuration Manager ajuda a implantar e gerenciar aplicativos iOS comprados por meio desse programa, importando as informações de licença da loja de aplicativos e acompanhando quantas licenças você usou.  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gerenciar aplicativos adquiridos por volume para dispositivos iOS  
 Você adquire várias licenças para aplicativos iOS por meio do VPP (Programa de compra por volume) da Apple. Isso envolve configurar uma conta de VPP da Apple no site da Apple e carregar o token de VPP da Apple no Configuration Manager, o que proporciona os seguintes recursos:  

-   Sincronizar informações de compra por volume com o Configuration Manager.  

-   Os aplicativos que você adquiriu são exibidos no console do Configuration Manager.  

-   Você pode implantar e monitorar esses aplicativos, bem como controlar o número de licenças que foram usadas para cada aplicativo.  

-   O Configuration Manager pode ajudá-lo a recuperar licenças for necessário, desinstalando aplicativos adquiridos por volume que você tiver implantado para usuários.  

## <a name="before-you-start"></a>Antes de começar  
 Antes de começar, você precisará obter um token de VPP da Apple e carregá-lo no Configuration Manager.  

> [!IMPORTANT]  
>  -   Atualmente, cada organização pode ter apenas uma conta e um token de VPP.  
> -   Há suporte apenas para o Apple Volume Purchase Program for Business.  
> -   Depois de associar uma conta de VPP da Apple ao Intune, não é possível associar posteriormente uma conta diferente. Por esse motivo, é muito importante que mais de uma pessoa tenha os detalhes da conta que você usa.  
> -   Se você já tiver usado um token de VPP com um produto de MDM diferente em sua conta existente de VPP da Apple, será necessário gerar um novo para ser usado com o Configuration Manager.  
> -   Cada token é válido por um ano.  
> -   Por padrão, o Configuration Manager sincroniza com o serviço de VPP da Apple duas vezes por dia para garantir que suas licenças sejam sincronizadas com o Configuration Manager.  
>   
>      Somente as alterações em suas licenças são sincronizadas. No entanto, uma vez a cada 7 dias uma sincronização completa será executada.  
>   
>      Quando você clica em **Sincronizar** para executar uma sincronização manual, sempre será executada uma sincronização completa.  
> -   Se você precisa recuperar ou restaurar o banco de dados do Configuration Manager, é recomendável executar uma sincronização manual para garantir que os dados de licença sincronizados estejam atualizados.  
> -   Enquanto você pode implantar aplicativos iOS adquiridos por volume para coleções de usuários ou dispositivos, os aplicativos de VPP que você implantar em um dispositivo sem usuário (por exemplo, um dispositivo registrado sem afinidade do usuário, usando o DEP (programa de registro de dispositivo) ou o Apple Configurator) não serão instalados.  

 Além disso, você precisa ter importado um certificado do APNs (Apple Push Notification Service) válido para que possa gerenciar dispositivos iOS, incluindo a implantação de aplicativos. Para obter mais informações, consulte [Set up iOS hybrid device management](../../mdm/deploy-use/set-up-ios-hybrid-device-management.md) (Configurar o gerenciamento de dispositivo híbrido iOS).  

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Etapa 1: obter e carregar um token de VPP da Apple  
  
1.  No console do Configuration Manager, clique em **Administração** > **Serviços em Nuvem** > **Tokens do Apple Volume Purchase Program**.   
  
3.  Na guia **Início**, no grupo **Tokens do Apple Volume Purchase Program**, clique em **Adicionar token do Apple Volume Purchase Program**.  

4.  Na página **Geral** do assistente **Adicionar token do Apple Volume Purchase Program**, configure o seguinte:   

    -   **Nome** – insira um nome para esse token, uma vez que ele será exibido no console do Configuration Manager.  

    -   **Token** – clique em **Procurar** e selecione o token de VPP baixado do site da Apple.  

         Clique no link **Ver Conta VPP da Apple** e, se ainda não tiver feito isso, inscreva-se no programa de compra por volume empresarial ou educacional. Depois de se inscrever, baixe o token de VPP da Apple para sua conta.  

    -   **Descrição** – opcionalmente, insira uma descrição que ajudará você a identificar esse token de VPP no console do Configuration Manager.  

    -   **Categorias atribuídas para aprimorar a pesquisa e a filtragem** – você também pode atribuir categorias para o token de VPP para facilitar a pesquisa no console do Configuration Manager.  

5.  Clique em **Avançar** e conclua o assistente.  
  
No nó **Tokens do Apple Volume Purchase Program**, você pode ver informações sobre o token de VPP da Apple, inclusive quando foi a última atualização, quando ele expirará e quando foi sincronizado pela última vez. 
  
A qualquer momento, é possível sincronizar completamente os dados mantidos pela Apple usando o Configuration Manager clicando em **Sincronizar** na guia **Início** do grupo **Sincronização** grupo.  
  
## <a name="step-2---deploy-a-volume-purchased-app"></a>Etapa 2: implantar um aplicativo comprado por volume  

1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Informações sobre Licença para Aplicativos da Loja**.  

3.  Escolha o aplicativo que deseja implantar e, na guia **Início**, no grupo **Criar**, clique em **Criar Aplicativo**.
É criado um aplicativo do Configuration Manager contendo o aplicativo da Windows Store para Empresas. Em seguida, é possível implantar e monitorar o aplicativo, como você faria com qualquer outro aplicativo do Configuration Manager.

    > [!IMPORTANT]  
    > É necessário escolher a finalidade da implantação **Obrigatória**. Atualmente, não há suporte para instalações disponíveis.

 Quando você implantar o aplicativo, uma licença será usada por cada usuário que instalar o aplicativo.  

 Para recuperar uma licença, você deve alterar a ação de implantação para **Desinstalar**. A licença será recuperada quando o aplicativo for desinstalado.  

## <a name="step-3---monitor-ios-vpp-apps"></a>Etapa 3 - Monitorar aplicativos de VPP iOS  
 O nó **Informações sobre Licença para Aplicativos da Loja** do espaço de trabalho **Biblioteca de Software** exibe informações sobre os aplicativos iOS adquiridos por volume, incluindo o número total de licenças que você tem para cada aplicativo e quantos foram implantados.

 Você também pode monitorar o uso de licença de todos os aplicativos de VPP adquiridos usando o relatório **Aplicativos do Apple Volume Purchase Program para iOS com contagens de licença**.  

 Este relatório exibe o nome de cada aplicativo com o número total de licenças que você adquiriu, o número de licenças disponíveis e muito mais.  

 Para obter ajuda para executar relatórios do Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  



<!--HONumber=Nov16_HO1-->


