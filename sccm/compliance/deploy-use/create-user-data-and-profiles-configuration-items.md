---
title: Criar itens de configuração de perfis e dados de usuário
titleSuffix: Configuration Manager
description: Use os itens de configuração de perfis e dados do usuário no System Center Configuration Manager para gerenciar redirecionamento de pastas, arquivos offline e perfis móveis.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: e6ae7f6b14da4f5959e336e08bec0e71896425ff
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129911"
---
# <a name="create-user-data-and-profiles-configuration-items-in-system-center-configuration-manager"></a>Criar itens de configuração de perfis e dados de usuário no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os itens de configuração de perfis e dados do usuário no System Center Configuration Manager contêm configurações que podem gerenciar o redirecionamento de pasta, arquivos offline e perfis móveis em computadores que executam o Windows 8 e posterior para usuários em sua hierarquia. Por exemplo, você pode:  

- Redirecionar a pasta de Documentos do usuário para um compartilhamento de rede.  

- Garantir que arquivos especificados armazenados na rede estejam disponíveis no computador do usuário quando a conexão de rede não estiver disponível.  

- Configurar quais arquivos no perfil móvel do usuário são sincronizados com um compartilhamento de rede quando o usuário fizer logon e logoff.  

  Ao contrário de outros itens de configuração no Configuration Manager, você não adiciona itens de configuração de perfis e dados de usuário a uma linha de base de configuração que será implantada. Em vez disso, você implanta o item de configuração diretamente usando a caixa de diálogo **Implantar Item de Configuração de Perfis e Dados de Usuário** .  

> [!IMPORTANT]  
>  Só é possível implantar itens de configuração de perfis e dados de usuário a coleções de usuários.  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>Habilitar perfis e dados do usuário para as configurações de conformidade  
 Use o procedimento a seguir para definir a configuração de cliente padrão para as configurações de conformidade dos perfis e dados do usuário, que se aplicarão a todos os computadores na sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns computadores, crie uma configuração personalizada do cliente de dispositivo e a atribua a uma coleção que contém os computadores nos quais deseja usar as configurações de perfis e dados do usuário. Para obter mais informações sobre como criar configurações personalizadas do dispositivo, consulte [Como definir as configurações do cliente](../../core/clients/deploy/configure-client-settings.md).  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente** > **Configurações Padrão**.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na caixa de diálogo **Configurações Padrão** , clique em **Configurações de Conformidade**.  

6.  Na lista suspensa **Habilitar Perfis e Dados do Usuário** , selecione **Sim**.  

7.  Clique em **OK** para fechar a caixa de diálogo **Configurações Padrão** .  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>Criar um item de configuração de perfis e dados de usuário  

1. No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Dados e Perfis do Usuário**.  

2. Na guia **Início** , no grupo **Criar** , clique em **Criar Item de Configuração de Perfis e Dados de Usuário**.  

3. Na página **Geral** do **Assistente para Criar Item de Configuração de Perfis e Dados de Usuário**, especifique as seguintes informações:  

   -   **Nome:** insira um nome exclusivo para o item de configuração. Você pode usar no máximo 256 caracteres.  

   -   **Descrição:** forneça uma descrição que ofereça uma visão geral do item de configuração e outras informações relevantes que ajudam a identificá-lo no console do Configuration Manager. Você pode usar no máximo 256 caracteres.  

   -   **Redirecionamento de pasta:** marque esta caixa se desejar definir as configurações de redirecionamento de pasta para este item de configuração.  

   -   **Arquivos offline:** marque esta caixa se você desejar definir as configurações de arquivos offline para este item de configuração.  

   -   **Perfis de usuário móvel:** marque esta caixa se desejar definir as configurações de perfis de usuário móvel para este item de configuração.  

4. Na página **Redirecionamento de Pasta** do **Assistente para Criar Item de Configuração de Perfis e Dados de Usuário**, especifique como deseja que os computadores cliente dos usuários que recebem esse item de configuração gerenciem o redirecionamento de pasta. Você pode definir configurações para qualquer dispositivo em que o usuário fizer logon ou apenas nos dispositivos primários do usuário. Para obter mais informações sobre o redirecionamento de pasta, veja a documentação do Windows Server.  

   > [!NOTE]  
   >  Esta página será exibida apenas se você tiver marcado **Redirecionamento de pasta** na página **Geral** do assistente.  

5. Na página **Arquivos Offline** do **Assistente para Criar Item de Configuração de Perfis e Dados de Usuário**, é possível habilitar ou desabilitar o uso de arquivos offline para os usuários que recebem esse item de configuração e definir as configurações para o comportamento dos arquivos offline. Você também pode especificar os arquivos offline que sempre estarão disponíveis em qualquer computador que o usuário fizer logon. Para obter mais informações sobre arquivos offline, veja a documentação do Windows Server.  

   > [!NOTE]  
   >  Esta página será exibida apenas se você tiver marcado **Arquivos offline** na página **Geral** do assistente.  

6. Na página **Perfis Móveis** do **Assistente para Criar Item de Configuração de Perfis e Dados de Usuário**, é possível configurar se os perfis móveis estarão disponíveis em computadores que o usuário faz logon e também configurar outras informações sobre o comportamento desses perfis. Para obter mais informações sobre perfis móveis, veja a documentação do Windows Server.  

   > [!NOTE]  
   >  Esta página será exibida apenas se você tiver marcado **Perfis de usuário móvel** na página **Geral** do assistente.  

7. Conclua o assistente.  

   O novo item de configuração de perfis e dados de usuário é mostrado no nó **Perfis e Dados de Usuário** do workspace **Ativos e Conformidade**.  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>Implantar um item de configuração de perfis e dados de usuário  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Dados e Perfis do Usuário**.  

3.  Selecione o item de configuração de perfis e dados de usuário que deseja implantar e, na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

4.  Na caixa de diálogo **Implantar Item de Configuração de Perfis e Dados de Usuário** , especifique as informações a seguir.  

    -   **Coleção** - Clique em **Procurar** para selecionar a coleção na qual deseja implantar o item de configuração.  

        > [!IMPORTANT]  
        >  Só é possível implantar itens de configuração de perfis e dados de usuário a coleções de usuários.  

    -   **Corrigir regras não compatíveis quando houver suporte** – Habilite esta opção para corrigir automaticamente todas as regras que são avaliadas como não compatíveis em computadores cliente.  

    -   **Permitir correção fora da janela de manutenção** – Se uma janela de manutenção foi configurada para a coleção na qual você está implantando o item de configuração, habilite esta opção para permitir que as configurações de conformidade corrijam o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Gerar um alerta** – Habilite esta opção para configurar um alerta que será gerado se a conformidade do item de configuração for menor que um percentual especificado por uma data e hora determinadas. Você também pode especificar se deseja que um alerta seja enviado para o System Center Operations Manager.  

    -   **Especificar o agendamento de avaliação de conformidade para este item de configuração** - Especifica o agendamento pelo qual o item de configuração implantado é avaliado nos computadores cliente. Pode ser um agendamento simples ou personalizado.  

5.  Clique em **OK** para fechar a caixa de diálogo **Implantar Item de Configuração de Perfis e Dados de Usuário** e criar a implantação.  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>Monitorar um item de configuração de perfis e dados de usuário  
 Você monitora esse tipo de item de configuração da mesma maneira que monitora outras configurações de conformidade.  

 Para mais informações, consulte [Como monitorar configurações de conformidade](../../compliance/deploy-use/monitor-compliance-settings.md).  
