---
title: "Definir as configurações do cliente | Microsoft Docs"
description: "Selecione as configurações do cliente no System Center Configuration Manager."
ms.custom: na
ms.date: 12/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 809c7938968b4a6efce6ef37fe7b7baf2c9dd3e7
ms.openlocfilehash: 77e17786302c885052c8861107a49ff826accb65

---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Como definir as configurações do cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Gerencie todas as configurações de cliente no System Center Configuration Manager em **Administração** > **Configurações do Cliente**. Modifique as configurações padrão quando quiser definir as configurações para todos os usuários e dispositivos na hierarquia que não possuírem configurações personalizadas aplicadas. Se você quiser aplicar configurações diferentes a apenas alguns usuários ou dispositivos, crie configurações personalizadas e implante-as às coleções.  

Para obter informações sobre cada configuração, consulte [Sobre configurações de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  É possível também usar itens de configuração para gerenciar clientes para avaliar, acompanhar e corrigir a conformidade de configuração de dispositivos. Para mais informações, consulte [Garantir a conformidade do dispositivo com o System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="configure-the-default-client-settings"></a>Definir as configurações padrão do cliente    

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  

3.  Na guia **Início**, escolha **Propriedades**.  

4.  Exiba e defina as configurações do cliente para cada grupo de configurações no painel de navegação.  

 Os computadores cliente serão definidos com essas configurações durante o próximo download da política do cliente. Para iniciar a recuperação de política para um único cliente, consulte [Iniciar recuperação de política de um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) em [Como gerenciar clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="create-and-deploy-custom-client-settings"></a>Criar e implantar configurações personalizadas do cliente  
Ao implantar essas configurações personalizadas, elas substituirão as configurações do cliente padrão. Para começar esse procedimento, verifique se você tem uma coleção que contenha os usuários ou os dispositivos que requerem essas configurações personalizadas do cliente.  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Configurações Personalizadas do Cliente** e escolha entre:  

    -   **Criar configurações personalizadas do dispositivo do cliente**  

    -   **Criar configurações personalizadas do usuário**  

4.  Especifique um nome exclusivo e uma descrição opcional.  

5.  Marque uma ou mais caixas de seleção que exibem um grupo de configurações.  

6.  Clique em cada grupo de configurações no painel de navegação e defina as configurações disponíveis, depois clique em **OK**.   

8.  Selecione a configuração personalizada do cliente que você criou. Na guia **Início**, no grupo **Configurações do Cliente**, escolha **Implantar**.  

9. Na caixa de diálogo **Selecionar Coleção**, selecione a coleção apropriada e escolha **OK**. Você pode verificar a coleção selecionada se clicar na guia **Implantações** do painel de detalhes.  

10. Exiba a ordem da configuração personalizada do cliente que você acabou de criar. Quando você tem várias configurações personalizadas do cliente, elas são aplicadas de acordo com o número da ordem. Se houver qualquer conflito, a configuração com o menor número de ordem substituirá as demais. Para alterar o número da ordem, na guia **Início**, no grupo **Configurações do Cliente**, escolha **Mover Item para Cima** ou **Mover Item para Baixo**.  

 Os computadores cliente serão definidos com essas configurações durante o próximo download da política do cliente. Para iniciar a recuperação de política para um único cliente, consulte [Iniciar recuperação de política de um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) em [Como gerenciar clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="view-client-settings"></a>Exibir configurações do cliente  
 Quando várias configurações de cliente foram implantadas no mesmo dispositivo, usuário ou grupo de usuários, a atribuição de propriedades e combinação das configurações podem ser complexas. Para exibir as configurações do cliente:  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Dispositivos** > **Usuários** ou **Coleções do Usuário**.  

3.  Selecione um dispositivo, usuário ou grupo de usuários no grupo **Configurações do Cliente** , selecione **Configurações do Cliente Resultante**.  

4.  Selecione uma configuração de cliente no painel esquerdo, e as configurações serão exibidas. Nesse modo, as configurações são somente leitura. 

    > [!NOTE]  
    >  Para exibir as configurações do cliente, você deve ter acesso de leitura às Configurações do Cliente.  

    


<!--HONumber=Dec16_HO3-->


