---
title: "Criar uma sequência de tarefas para capturar e restaurar o estado do usuário | Microsoft Docs"
description: "Use as sequências da tarefas do System Center Configuration Manager para capturar e restaurar dados de estado do usuário em cenários de implantação de sistema operacional."
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
caps.latest.revision: 7
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: c6ee0ed635ab81b5e454e3cd85637ff3e20dbb34
ms.openlocfilehash: 4b3668094d576b1b8710f08b384aa2f7c5eb0cca
ms.contentlocale: pt-br
ms.lasthandoff: 06/08/2017


---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-system-center-configuration-manager"></a>Criar uma sequência de tarefas para capturar e restaurar o estado de usuário no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode usar as sequências da tarefas do System Center Configuration Manager para capturar e restaurar dados de estado do usuário em cenários de implantação de sistema operacional no qual você deseja manter o estado do usuário do sistema operacional atual. Dependendo do tipo de sequência de tarefas criado, as etapas de captura e restauração podem ser adicionadas automaticamente como parte da sequência de tarefas. Em outros cenários, talvez seja necessário adicionar manualmente as etapas de captura e restauração à sequência de tarefas. Este tópico fornece as etapas que devem ser adicionadas a uma sequência de tarefas existente para capturar e restaurar dados de estado do usuário.  

##  <a name="BKMK_CaptureRestoreUserState"></a> Como capturar e restaurar dados de estado do usuário  
 Para capturar e restaurar o estado do usuário, é necessário adicionar as seguintes etapas à sequência de tarefas:  

-   **Solicitar Armazenamento de Estado**: essa etapa é necessária somente se você armazenar o estado do usuário no ponto de migração de estado.  

-   **Capturar Estado do Usuário**: essa etapa captura os dados de estado do usuário e os armazena no ponto de migração de estado ou localmente usando links.  

-   **Restaurar Estado do Usuário**: essa etapa restaura os dados de estado do usuário no computador de destino. Ele pode recuperar os dados de um ponto de migração de estado do usuário ou do computador de destino.  

-   **Liberar Armazenamento de Estado**: essa etapa é necessária somente se você armazenar o estado do usuário no ponto de migração de estado. Essa etapa remove dados do ponto de migração de estado.  

 Use os procedimentos a seguir para adicionar as etapas de sequência de tarefas necessárias para capturar e restaurar o estado do usuário. Para obter mais informações sobre a criação de sequências de tarefas, consulte [Gerenciar sequências de tarefas para automatizar tarefas](manage-task-sequences-to-automate-tasks.md).  

#### <a name="to-add-task-sequence-steps-to-capture-the-user-state"></a>Para adicionar etapas da sequência de tarefas para capturar o estado do usuário  

1.  Na lista **Sequência de Tarefa** , selecione uma sequência de tarefas e clique em **Editar**.  

2.  Se você estiver usando um ponto de migração de estado para armazenar o estado do usuário, adicione a etapa **Solicitar Armazenamento de Estado** à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado do Usuário**e clique em **Solicitar Armazenamento de Estado**. Especifique as propriedades e opções a seguir para a etapa **Solicitar Armazenamento de Estado** e clique em **Aplicar**.  

     Na guia **Propriedades** , especifique as seguintes opções:  

    -   Digite um nome e uma descrição para a etapa.  

    -   Clique em **Capturar estado do computador**.  

    -   Na caixa **Número de tentativas** , especifique o número de vezes que a sequência de tarefas tentará capturar os dados de estado do usuário caso ocorra um erro.  

    -   Na caixa **Atraso na repetição (em segundos)** , especifique quantos segundos a sequência de tarefas aguardará antes de repetir a captura dos dados.  

    -   Marque a caixa de seleção **Se a conta do computador não conseguir se conectar ao armazenamento de estado, use a conta de Acesso à Rede** para especificar se deseja usar a [Conta de Acesso à Rede](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#a-namebkmknaaa-network-access-account) do Configuration Manager para se conectar ao repositório de estado.  

     Na guia **Opções** , especifique as seguintes opções:  

    -   Marque a caixa de seleção **Continuar se houver erro** se quiser que a sequência de tarefas passe para a próxima etapa se a etapa atual falhar.  

    -   Especifique as condições que devem ser atendidas antes de continuar a sequência de tarefas se ocorrer um erro.  

3.  Adicione a etapa **Captura Estado do Usuário** à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado do Usuário**e clique em **Capturar Estado do Usuário**. Especifique as propriedades e opções a seguir para a etapa **Capturar Estado do Usuário** e clique em **OK**.  

    > [!IMPORTANT]  
    >  Quando você adicionar essa etapa à sequência de tarefas, configure também a variável de sequência de tarefas **OSDStateStorePath** para especificar onde os dados de estado do usuário são armazenados. Se você armazenar o estado do usuário localmente, não especifique uma pasta raiz, pois isso pode causar a falha da sequência de tarefas. Quando você armazenar os dados do usuário localmente, use sempre uma pasta ou subpasta. Para obter informações sobre essa variável, consulte [Capturar variáveis de ação da sequência de tarefas de estado de usuário](../understand/task-sequence-action-variables.md#BKMK_CaptureUserState).  

     Na guia **Propriedades** , especifique as seguintes opções:  

    -   Digite um nome e uma descrição para a etapa.  

    -   Especifique o pacote que contém o arquivo de origem da USMT usado para capturar os dados de estado do usuário.  

    -   Especifique os perfis de usuário a serem capturados:  

        -   Clique em **Capturar todos os perfis de usuário usando as opções padrão** para capturar todos os perfis de usuário.  

        -   Clique em **Personalizar captura de perfis de usuário** para especificar perfis de usuário individuais para capturar. Selecione o arquivo de configuração (miguser.xml, migsys.xml ou migapp.xml) que contém as informações de perfil do usuário. Você não pode usar o arquivo de configuração config.xml aqui, mas pode adicioná-lo manualmente à linha de comando do USMT usando as variáveis OSDMigrageAdditionalCaptureOptions e OSDMigrateAdditionalRestoreOptions.

    -   Selecione **Habilitar log detalhado** para especificar a quantidade de informações a serem gravadas nos arquivos de log em caso de erro.  

    -   Selecione **Ignorar arquivos que usam o sistema de arquivos com criptografia (EFS)**.  

    -   Selecione **Copiar usando o acesso ao sistema de arquivos** para especificar as seguintes definições:  

        -   **Continuar se alguns arquivos não puderem ser capturados**: essa configuração permite que a etapa da sequência de tarefas continue o processo de migração, mesmo que alguns arquivos não possam ser capturados. Se você desabilitar essa opção e um arquivo não puder ser capturado, a etapa da sequência falhará. Essa opção é habilitada por padrão.  

        -   **Capturar localmente usando links em vez de copiar arquivos**: essa configuração permite que você use o recurso de migração de link físico que está disponível no USMT 4.0. Essa configuração será ignorada se você usar versões do USMT anteriores ao USMT 4.0.  

        -   **Capturar em modo off-line (somente Windows PE)**: essa configuração permite que você capture o estado de uso do Windows PE sem inicializar o sistema operacional existente. Essa configuração será ignorada se você usar versões do USMT anteriores ao USMT 4.0.  

    -   Selecione **Capturar usando o VSS (Serviços de Cópias de Sombra de Volume)**. Essa configuração será ignorada se você usar versões do USMT anteriores ao USMT 4.0.  

     Na guia **Opções** , especifique as seguintes opções:  

    -   Marque a caixa de seleção **Continuar se houver erro** se quiser que a sequência de tarefas passe para a próxima etapa se a etapa atual falhar.  

    -   Especifique as condições que devem ser atendidas antes de continuar a sequência de tarefas se ocorrer um erro.  

4.  Se estiver usando um ponto de migração de estado para armazenar o estado do usuário, adicione a etapa [Liberar Repositório de Estado](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado do Usuário**e clique em **Liberar Armazenamento de Estado**. Especifique as propriedades e opções a seguir para a etapa **Liberar Armazenamento de Estado** e clique em **OK**.  

    > [!IMPORTANT]  
    >  A ação de sequência de tarefas executada antes da etapa **Liberar Armazenamento de Estado** deve ser bem-sucedida antes que a etapa **Liberar Armazenamento de Estado** seja iniciada.  

     Na guia **Propriedades** , insira um nome e uma descrição para a etapa.  

     Na guia **Opções** , especifique as seguintes opções:  

    -   Marque a caixa de seleção **Continuar se houver erro** se quiser que a sequência de tarefas passe para a próxima etapa se a etapa atual falhar.  

    -   Especifique as condições que devem ser atendidas para que a sequência de tarefas possa continuar se ocorrer um erro.  

 Implante essa sequência de tarefas para capturar o estado do usuário em um computador de destino. Para obter informações sobre como implantar sequências de tarefas, consulte [Implantar uma sequência de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

#### <a name="to-add-task-sequence-steps-to-restore-the-user-state"></a>Para adicionar etapas da sequência de tarefas para restaurar o estado do usuário  

1.  Na lista **Sequência de Tarefa** , selecione uma sequência de tarefas e clique em **Editar**.  

2.  Adicionar a etapa [Restaurar Estado do Usuário](../understand/task-sequence-steps.md#BKMK_RestoreUserState) à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado do Usuário**e clique em **Restaurar Estado do Usuário**. Essa etapa estabelece uma conexão com o ponto de migração de estado. Especifique as propriedades e opções a seguir para a etapa **Restaurar Estado do Usuário** e clique em **OK**.  

     Na guia **Propriedades** , especifique as seguintes propriedades:  

    -   Digite um nome e uma descrição para a etapa.  

    -   Especifique o pacote que contém a USMT para restaurar os dados de estado do usuário.  

    -   Especifique os perfis de usuário a serem restaurados:  

        -   Clique em **Restaurar todos os perfis de usuário usando as opções padrão** para restaurar todos os perfis de usuário.  

        -   Clique em **Personalizar restauração de perfil do usuário** para restaurar perfis de usuário individuais. Selecione o arquivo de configuração (miguser.xml, migsys.xml ou migapp.xml) que contém as informações de perfil do usuário. Você não pode usar o arquivo de configuração config.xml aqui, mas pode adicioná-lo manualmente à linha de comando do USMT usando as variáveis OSDMigrageAdditionalCaptureOptions e OSDMigrateAdditionalRestoreOptions.

    -   Selecione **Restaurar perfis de usuário do computador local** para fornecer uma nova senha para os perfis restaurados. Não é possível migrar senhas para perfis locais.  

        > [!NOTE]  
        >  Quando houver contas de usuário local e a etapa [Capturar Estado do Usuário](../understand/task-sequence-steps.md#BKMK_CaptureUserState) for usada com a opção **Capturar todos os perfis de usuário com opções padrão** marcada, é necessário selecionar a configuração **Restaurar perfis de usuário do computador local** na etapa [Restaurar Estado do Usuário](../understand/task-sequence-steps.md#BKMK_RestoreUserState); caso contrário, a sequência de tarefas falhará.  

    -   Selecione **Continuar, se alguns arquivos não forem restaurados** se quiser que a etapa **Restaurar Estado do Usuário** para continuar se um arquivo não puder ser restaurado.  

         Se você armazenar o estado do usuário usando links locais e a restauração não for bem-sucedida, o usuário administrativo poderá excluir manualmente os links físicos criados para armazenar os dados ou a sequência de tarefas pode executar a ferramenta USMTUtils. Se você usar o USMTUtils para excluir link físico, adicione uma etapa [Reiniciar Computador](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer) depois de executar USMTUtils.  

    -   Selecione **Habilitar log detalhado** para especificar a quantidade de informações a serem gravadas nos arquivos de log em caso de erro.  

     Na guia **Opções** , especifique as seguintes opções:  

    -   Marque a caixa de seleção **Continuar se houver erro** se quiser que a sequência de tarefas passe para a próxima etapa se a etapa atual falhar.  

    -   Especifique as condições que devem ser atendidas antes de continuar a sequência de tarefas se ocorrer um erro.  

3.  Se estiver usando um ponto de migração de estado para armazenar o estado do usuário, adicione a etapa [Liberar Repositório de Estado](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado do Usuário**e clique em **Liberar Armazenamento de Estado**. Especifique as propriedades e opções a seguir para a etapa **Liberar Armazenamento de Estado** e clique em **OK**.  

    > [!IMPORTANT]  
    >  A ação de sequência de tarefas executada antes da etapa **Liberar Armazenamento de Estado** deve ser bem-sucedida antes que a etapa **Liberar Armazenamento de Estado** seja iniciada.  

     Na guia **Propriedades** , insira um nome e uma descrição para a etapa.  

     Na guia **Opções** , especifique as seguintes opções:  

    -   Marque a caixa de seleção **Continuar se houver erro** se quiser que a sequência de tarefas passe para a próxima etapa se a etapa atual falhar.  

    -   Especifique as condições que devem ser atendidas para que a sequência de tarefas possa continuar se ocorrer um erro.  

 Implante essa sequência de tarefas para restaurar o estado do usuário em um computador de destino. Para obter mais informações sobre como implantar sequências de tarefas, consulte [Implantar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

## <a name="next-steps"></a>Próximas etapas
[Monitorar a implantação da sequência de tarefas](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)

