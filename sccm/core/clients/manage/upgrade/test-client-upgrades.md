---
title: "Testar atualizações do cliente em uma coleção de pré-produção | Microsoft Docs"
description: "Teste atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager."
ms.custom: na
ms.date: 12/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
caps.latest.revision: 10
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 52d2e088b8db3c2e9a0af640ca3db72b9fd7af60
ms.openlocfilehash: 250c9312b932670c408554f3968ae43ae4f3dbaa


---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-system-center-configuration-manager"></a>Como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É possível testar uma nova versão do cliente do Configuration Manager em uma coleção de pré-produção antes de atualizar o restante do site com ele.  Quando você fizer isso, apenas os dispositivos que fazem parte da coleção de teste serão atualizados. Depois de ter a oportunidade de testar o cliente você pode promover o cliente, o que torna a nova versão do software cliente disponível para o restante do site.

> [!NOTE]
> Para promover um cliente de teste para a produção, você deve estar conectado como um usuário com a função de segurança de **administrador completo** e um escopo de segurança de **Tudo**. Para obter mais informações, consulte [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration). Você também deve estar conectado a um servidor conectado ao site da administração central ou a um site primário autônomo de nível superior.

 Há três etapas básicas para testar os clientes em pré-produção.  

1.  Configurar atualizações automáticas do cliente para usar uma coleção de pré-produção.  

2.  Instalar uma atualização do Configuration Manager que inclui uma nova versão do cliente.  

3.  Promover o novo cliente para produção.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Para configurar atualizações automáticas do cliente para usar uma coleção de pré-produção  

1. [Configure uma coleção](..\collections\create-collections.md) que contém os computadores nos quais você deseja implantar o cliente de pré-produção. Não inclua computadores de grupo de trabalho em coleções de pré-produção. Eles não podem usar a autenticação necessária para o ponto de distribuição acessar o pacote de cliente de pré-produção.   

1.  No console do Configuration Manager, abra **Administração** > **Configuração do Site** > **Sites** e selecione **Configurações da Hierarquia**.  

     Na guia **Atualização de cliente** das **Propriedades de configurações de hierarquia**:  

    -   Selecione **Atualizar todos os clientes na coleção de pré-produção automaticamente usando o cliente de pré-produção**  

    -   Digite o nome de uma coleção para usar como uma coleção de pré-produção  

![Testar atualizações do cliente](media/test-client-upgrades.png)


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>Para instalar uma atualização do Configuration Manager que inclui uma nova versão do cliente  

1.  No console do Configuration Manager, abra **Administração** > **Serviços de Nuvem** > **Atualizações e Serviços**, selecione uma atualização **Disponível** e escolha **Instalar Pacote de Atualização**  

     Para obter mais informações, consulte [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Durante a instalação da atualização, na página do assistente **Opções de Cliente**, selecione **Teste na coleção de pré-produção**.  

3.  Conclua o restante do assistente e instale o pacote de atualização.  

     Depois que o assistente for concluído, os clientes na coleção de pré-produção começarão a implantar o cliente atualizado. Você pode monitorar a implantação de clientes atualizados acessando **Monitoramento** > **Status do Cliente** > **Implantação de Cliente de Pré-produção**. Para obter mais informações, consulte [Como monitorar o status de implantação do cliente no System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > O status da implantação em computadores que hospedam funções de sistema de sites em uma coleção de pré-produção pode ser relatado como **Não compatível** mesmo que o cliente tenha sido implantado com êxito. Quando você promove o cliente para produção, o status da implantação é relatado corretamente.

##  <a name="to-promote-the-new-client-to-production"></a>Para promover o novo cliente para produção  

1.  No console do Configuration Manager, abra **Administração** > **Serviços de Nuvem** > **Atualizações e Manutenção** e escolha **Promover o Cliente de Pré-produção**.

    > [!TIP]
    > O botão **Promover o Cliente de Pré-produção** também está disponível quando você está monitorando implantações de cliente no console em **Monitoramento** > **Status do Cliente** > **Implantação de Cliente de Pré-produção**.

2.  Examine as versões de cliente em produção e pré-produção, verifique se a coleção correta de pré-produção está especificada, clique em **Promover** e, em seguida, em **Sim**.  

3.  Após a caixa de diálogo fechar, a versão atualizada do cliente substituirá a versão do cliente em uso na sua hierarquia. Em seguida, você poderá atualizar os clientes de todo o seu site. Consulte [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) para obter mais informações.  



<!--HONumber=Jan17_HO1-->


