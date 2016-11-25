---
title: "Definir as configurações do cliente | System Center Configuration Manager"
description: "Selecione as configurações do cliente no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9e3162e04da90748379145e37f6b378badab97d3

---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Como definir as configurações do cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você gerencia todas as configurações de cliente no System Center Configuration Manager no nó **Configurações do Cliente** no espaço de trabalho **Administração** do console do Configuration Manager. Modifique as configurações padrão quando quiser definir as configurações para todos os usuários e dispositivos na hierarquia que não possuírem configurações personalizadas aplicadas. Se você quiser aplicar configurações diferentes a apenas alguns usuários ou dispositivos, crie configurações personalizadas e implante-as às coleções.  

> [!NOTE]  
>  É possível também usar itens de configuração para gerenciar clientes para avaliar, acompanhar e corrigir a conformidade de configuração de dispositivos. Para mais informações, consulte [Garantir a conformidade do dispositivo com o System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="a-namebkmkdefaultclientsettingsa-how-to-configure-the-default-client-settings"></a><a name="BKMK_DefaultClientSettings"></a> Como definir as configurações padrão do cliente  

 Use o procedimento a seguir para definir as configurações padrão de cliente para todos os clientes da hierarquia.  

#### <a name="to-configure-the-default-client-settings"></a>Para definir as configurações padrão do cliente  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**e selecione **Configurações do Cliente Padrão**.  

3.  Na guia **Início** , clique em **Propriedades**.  

4.  Exiba e defina as configurações do cliente para cada grupo de configurações no painel de navegação. Para obter mais informações sobre cada configuração, consulte [Sobre a configuração de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

5.  Clique em **OK** para fechar a caixa de diálogo **Configurações do Cliente Padrão** .  

 Os computadores cliente serão definidos com essas configurações durante o próximo download da política do cliente. Para iniciar a recuperação de política para um único cliente, consulte [Iniciar recuperação de política de um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) em [Como gerenciar clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="a-namebkmkcustomclientsettingsa-how-to-create-and-deploy-custom-client-settings"></a><a name="BKMK_CustomClientSettings"></a> Como criar e implantar configurações personalizadas do cliente  
 Use o procedimento a seguir para configurar e implantar configurações personalizadas para uma coleção selecionada de usuários ou dispositivos. Ao implantar essas configurações personalizadas, elas substituirão as configurações do cliente padrão.  

> [!NOTE]  
>  Para começar esse procedimento, verifique se você tem uma coleção que contenha os usuários ou os dispositivos que requerem essas configurações personalizadas do cliente.  

#### <a name="to-configure-and-deploy-custom-client-settings"></a>Para configurar e implantar configurações personalizadas do cliente  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Configurações Personalizadas do Cliente**e clique em uma das seguintes opções, de acordo com o que desejar, criar configurações personalizadas do cliente para dispositivos ou para usuários:  

    -   **Criar configurações personalizadas do dispositivo do cliente**  

    -   **Criar configurações personalizadas do usuário**  

4.  Na caixa de diálogo **Criar Configurações Personalizadas do Dispositivo** ou **Criar Configurações Personalizadas do Usuário** , especifique um nome exclusivo para as configurações personalizadas e uma descrição opcional.  

5.  Marque uma ou mais caixas de seleção disponíveis que exibem um grupo de configurações.  

6.  Clique nas primeiras configurações de grupo no painel de navegação e exiba e defina as configurações personalizadas disponíveis. Repita esse processo para as configurações de grupo remanescentes. Para obter informações sobre cada configuração, consulte [Sobre configurações de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

7.  Clique em **OK** para fechar a caixa de diálogo **Criar Configurações Personalizadas do Dispositivo** ou **Criar Configurações Personalizadas do Usuário** .  

8.  Selecione a configuração personalizada do cliente que você acabou de criar. Na guia **Início** , no grupo **Configurações do Cliente** , clique em **Implantar**.  

9. Na caixa de diálogo **Selecionar Coleção** , selecione a coleção que contém os dispositivos ou os usuários aos quais serão atribuídas as definições de configurações personalizadas e clique em **OK**. Você pode verificar a coleção selecionada se clicar na guia **Implantações** do painel de detalhes.  

10. Exiba a ordem da configuração personalizada do cliente que você acabou de criar. Quando você tem várias configurações personalizadas do cliente, elas são aplicadas de acordo com o número da ordem. Se houver qualquer conflito, a configuração com o menor número de ordem substituirá as demais. Para alterar o número da ordem, na guia **Início** , no grupo **Configurações do Cliente** , clique em **Mover Item para Cima** ou **Mover Item para Baixo**.  

 Os computadores cliente serão definidos com essas configurações durante o próximo download da política do cliente. Para iniciar a recuperação de política para um único cliente, consulte [Iniciar recuperação de política de um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) em [Como gerenciar clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="a-namebkmkresultantclientsettingsa-how-to-view-resultant-client-settings"></a><a name="BKMK_ResultantClientSettings"></a> Como exibir as configurações de cliente resultantes  
 Quando várias configurações de cliente foram implantadas no mesmo dispositivo, usuário ou grupo de usuários, a atribuição de propriedades e combinação das configurações podem ser complexas. Use o procedimento a seguir para exibir as configurações do cliente resultante calculadas.  

#### <a name="to-view-the-resultant-client-settings"></a>Para exibir as configurações do cliente resultante  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Dispositivos**, **Usuários**ou **Coleções de Usuários**.  

3.  Selecione um dispositivo, usuário ou grupo de usuários no grupo **Configurações do Cliente** , selecione **Configurações do Cliente Resultante**.  Alternativamente, é possível clicar com o botão direito do mouse no dispositivo, usuário ou grupo de usuários, selecionar **Configurações do Cliente**e clicar em **Configurações do Cliente Resultante**.  

4.  Selecione uma configuração de cliente no painel esquerdo e as configurações resultantes são exibidas.  

    > [!NOTE]  
    >  Para exibir as configurações do cliente resultante, o usuário conectado deve ter acesso de leitura às Configurações do Cliente.  

    > [!NOTE]  
    >  As configurações resultantes exibidas são somente para leitura. Para modificar as configurações, use os procedimentos acima.  



<!--HONumber=Nov16_HO1-->


