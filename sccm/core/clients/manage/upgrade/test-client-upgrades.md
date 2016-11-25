---
title: "Testar atualizações do cliente em uma coleção de pré-produção | System Center Configuration Manager"
description: "Teste atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e648b94a475bda2b35d69ff0a8863d2e0d248fb


---
# <a name="how-to-test-client-upgrades-in-a-preproduction-collection-in-system-center-configuration-manager"></a>Como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para atualizar o cliente do Configuration Manager em PCs e dispositivos com Windows, você pode testar uma nova versão do cliente em uma coleção de pré-produção antes de atualizar o restante do site com ela.  Quando você faz isso, somente os dispositivos que fazem parte da coleção de pré-produção são atualizados para o novo cliente. Depois de ter a oportunidade de testar o cliente nesta coleção de pré-produção, você pode promover o cliente, o que torna a nova versão do software cliente disponível para o restante do site.  

 Há três etapas básicas para testar os clientes em pré-produção  

1.  [Para configurar atualizações automáticas do cliente para usar uma coleção de pré-produção](#BKMK_config) para usar uma coleção de pré-produção.  

2.  [Para instalar uma atualização do Configuration Manager que inclui uma nova versão do cliente](#BKMK_install) que inclui uma nova versão do cliente. Durante a instalação, especifique para usar uma coleção de pré-produção para o novo software cliente.  

3.  [Para promover o novo cliente para produção](#BKMK_promote) depois de testá-lo suficientemente em pré-produção.  

> [!TIP]  
>  Se você estiver atualizando a infraestrutura do servidor de uma versão anterior do Configuration Manager \(como o Configuration Manager 2007 ou o System Center 2012 Configuration Manager\), será recomendável que conclua as atualizações do servidor, incluindo a instalação de todas as atualizações da ramificação atual, antes de atualizar os clientes do Configuration Manager.   A atualização mais recente da ramificação atual contém a última versão do cliente, de modo que é melhor fazer atualizações do cliente depois que você tiver instalado todas as atualizações do Configuration Manager que deseja usar.  

##  <a name="a-namebkmkconfiga-to-configure-automatic-client-upgrades-to-use-a-preproduction-collection"></a><a name="BKMK_config"></a> Para configurar atualizações automáticas do cliente para usar uma coleção de pré-produção  

1. Configure uma coleção que contém os computadores nos quais você deseja implantar o cliente de pré-produção. Para obter mais informações sobre como realizar esta etapa, consulte [Como criar coleções](..\collections\create-collections.md).

> [!NOTE]
> Não inclua computadores de grupo de trabalho em coleções de pré-produção. Computadores de grupo de trabalho não podem usar a autenticação necessária para o ponto de distribuição acessar o pacote de cliente de pré-produção.   

1.  No console do Configuration Manager, abra **Administração** > **Configuração do Site** > **Sites** e clique em **Configurações da Hierarquia**.  

     Na guia **Atualização de cliente** das **Propriedades de configurações de hierarquia**:  

    -   Selecione **Atualizar todos os clientes na coleção de pré-produção automaticamente usando o cliente de pré-produção**  

    -   Digite o nome de uma coleção para usar como uma coleção de pré-produção  

2.  Clique em **OK** para salvar as configurações de Atualização de Cliente.  

##  <a name="a-namebkmkinstalla-to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a><a name="BKMK_install"></a> Para instalar uma atualização do Configuration Manager que inclui uma nova versão do cliente  

1.  No console do Configuration Manager, abra **Administração** > **Serviços de Nuvem** > **Atualizações e Serviços**, selecione uma atualização **Disponível** e clique em **Instalar Pacote de Atualização**  

     Para obter mais informações, consulte [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Durante a instalação da atualização, na página **Opções de Cliente** do assistente, selecione **Teste na coleção de pré-produção**e clique em **Avançar**.  

3.  Conclua o restante do assistente e instale o pacote de atualização.  

     Depois que o assistente for concluído, os clientes na coleção de pré-produção começarão a implantar o cliente atualizado. Você pode monitorar a implantação de clientes atualizados acessando **Monitoramento** > **Status do Cliente** > **Implantação de Cliente de Pré-produção**. Para obter mais informações, consulte [Como monitorar o status de implantação do cliente no System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > O status da implantação em computadores que hospedam funções de sistema de sites em uma coleção de pré-produção pode ser relatado como **Não Iniciado** mesmo que o cliente tenha sido implantado com êxito. Quando você promove o cliente para produção, o status da implantação é relatado corretamente.

##  <a name="a-namebkmkpromotea-to-promote-the-new-client-to-production"></a><a name="BKMK_promote"></a> Para promover o novo cliente para produção  

1.  No console do Configuration Manager, abra **Administração** > **Serviços de Nuvem** > **Atualizações e Manutenção** e clique em **Promover o Cliente de Pré-produção**.

    > [!TIP]
    > O botão **Promover o Cliente de Pré-produção** também está disponível quando você está monitorando implantações de cliente no console em **Monitoramento** > **Status do Cliente** > **Implantação de Cliente de Pré-produção**.

2.  Na caixa de diálogo, analise as versões de cliente em produção e pré-produção, verifique se a coleção correta de pré-produção está especificada e clique em **Promover**. Na caixa de confirmação, clique em **Sim**.  

3.  Após a caixa de diálogo fechar, a versão atualizada do cliente substituirá a versão atual do cliente em uso na sua hierarquia. Em seguida, você poderá atualizar os clientes de todo o seu site. Consulte [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) para obter mais informações.  



<!--HONumber=Nov16_HO1-->


