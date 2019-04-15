---
title: Perfis do OneDrive for Business
titleSuffix: Configuration Manager
description: Redirecione as pastas conhecidas do Windows para o OneDrive for Business usando um perfil do OneDrive for Business no Configuration Manager.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 22fcc8704651d75b4123e7942d14b861b3f6c099
ms.sourcegitcommit: d4b0e44e6bb06a830d0887493528d9166a15154b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 04/11/2019
ms.locfileid: "59506289"
---
# <a name="onedrive-for-business-profiles"></a>Perfis do OneDrive for Business

A partir da versão 1902 do Configuration Manager, é possível criar perfis do OneDrive for Business para mover as pastas conhecidas do Windows para o OneDrive for Business. Essas pastas incluem a Área de Trabalho, Documentos e Imagens. Em cada perfil, é possível especificar configurações para mover as pastas conhecidas do Windows. Confira mais informações do OneDrive for Business em [Redirecionar e mover pastas conhecidas do Windows para o OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders). <!--3556021-->

## <a name="prerequisites"></a>Pré-requisitos

- [Encontrar a ID do locatário do Office 365](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- Implantar a versão do cliente de sincronização do OneDrive 18.111.0603.0004 ou posterior. Confira mais informações em [Implantar aplicativos do OneDrive usando o System Center Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

## <a name="bkmk_odfb"></a> Mover as pastas conhecidas do Windows para o OneDrive
<!--3556021-->
Use o Configuration Manager para mover pastas conhecidas do Windows para o OneDrive for Business. Essas pastas incluem a Área de Trabalho, Documentos e Imagens. Para simplificar suas atualizações do Windows 10, implante essas configurações para clientes do Windows 7 antes de implantar uma sequência de tarefas. 

1. No console do Configuration Manager, acesse o workspace **Ativos e Conformidade**, expanda **Configurações de conformidade** e selecione o nó **Perfis do OneDrive for Business**.  

   ![Nó de Perfis do OneDrive for Business](media/onedrive-for-business-profiles-node.png)
2. Na Faixa de Opções, selecione **Criar Perfil do OneDrive for Business**.  

3. Especifique um nome para identificar essa política e selecione **Próximo**.  

4. Selecione as plataformas que serão provisionadas com este perfil do OneDrive for Business. Ao terminar de selecionar as plataformas, clique em **Próximo**.

    ![Selecionar as plataformas para o perfil OneDrive for Business](media/onedrive-for-business-profile-select-platforms.png) 

5. Na página **Configurações**:

    1. Especifique a ID do locatário do Office 365.  

    2. Selecione uma das opções a seguir para mover as pastas conhecidas para o OneDrive:  

        - **Solicitar que os usuários movam as pastas conhecidas do Windows no OneDrive**: com essa opção, o usuário vê um assistente para mover os arquivos deles. Caso eles optem por adiar ou recusem mover as pastas, o OneDrive os lembrará periodicamente.  

        - **Mover silenciosamente as pastas conhecidas do Windows para o OneDrive**: quando essa política se aplica ao dispositivo, o cliente do OneDrive redireciona automaticamente as pastas conhecidas para o OneDrive for Business.  

            - **Mostrar uma notificação aos usuários depois que as pastas forem redirecionadas**: se você habilitar essa opção, o cliente do OneDrive notificará o usuário depois que mover as pastas.  

    3. **Impedir que os usuários redirecionem as pastas conhecidas do Windows de volta para o PC**: desabilita a opção no cliente do OneDrive for Business que permite aos usuários mover essas pastas de volta para o dispositivo.  

       ![Configurações de Mudança de Pastas Conhecidas do OneDrive for Business](media/onedrive-for-business-profile-move-folder-settings.png)

6. Conclua o assistente e implante a política.  


## <a name="deploy-the-onedrive-for-business-profile"></a>Implantar o Perfil do OneDrive for Business

1. No console do Configuration Manager, acesse o workspace **Ativos e Conformidade**, expanda **Configurações de conformidade** e selecione o nó **Perfis do OneDrive for Business**.  


2. Selecione o perfil e clique em **Implantar**, na faixa de opções.

3. Especifique as seguintes configurações para sua implantação:

   1. **Coleção**: clique em **Procurar...** e selecione a coleção para a qual você deseja implantar o perfil.  
   1. **Gerar um alerta**:

      - **Quando está abaixo da conformidade**: o percentual mínimo de conformidade do cliente a ser mantido; caso contrário, um alerta será gerado.
      -  **Data e hora**: a data em que o primeiro alerta é gerado com base na conformidade do perfil.
      - **Gerar alerta do System Center Operations Manager**: envia um alerta de conformidade para o System Center Operations Manager.
   1. **Agendamento**:

      - **Agendamento simples**: por padrão, essa configuração usa um agendamento simples para iniciar a avaliação de conformidade a cada sete dias.
      - **Agendamento personalizado**: define quando executar a avaliação de conformidade. O horário de início é baseado na hora local do computador que executa o console do Configuration Manager no momento em que a agenda é criada ou você pode usar o UTC.
 
      ![Implantar o perfil do OneDrive for Business](media/onedrive-for-business-deploy-profile.png)

4. Clique em **OK** para implantar o Perfil do OneDrive for Business.


## <a name="next-steps"></a>Próximas etapas

[Criar perfis de conexão remota](/sccm/compliance/deploy-use/create-remote-connection-profiles)
