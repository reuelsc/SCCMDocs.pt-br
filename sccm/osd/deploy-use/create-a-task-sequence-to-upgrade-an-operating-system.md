---
title: "Criar uma sequência de tarefas para atualizar um sistema operacional | Configuration Manager"
description: "Sequências de tarefas no System Center Configuration Manager podem atualizar automaticamente um sistema operacional do Windows 7 ou posterior para o Windows 10."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fe70a3bfddcc0638a27eccb04324c4e6e2ace1d4


---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Crie uma sequência de tarefas para atualizar um sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use sequências de tarefas no System Center Configuration Manager para atualizar automaticamente um sistema operacional do Windows 7 ou posterior para o Windows 10 em um computador de destino. Você cria uma sequência de tarefas que faz referência à imagem do sistema operacional que você deseja instalar no computador de destino e qualquer outro conteúdo adicional, como aplicativos ou atualizações de software que você deseja instalar. A sequência de tarefas para atualizar um sistema operacional faz parte do cenário [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md).  

##  <a name="a-namebkmkupgradeosa-create-a-task-sequence-to-upgrade-an-operating-system"></a><a name="BKMK_UpgradeOS"></a> Criar uma sequência de tarefas para atualizar um sistema operacional  
 Para atualizar o sistema operacional em computadores para o Windows 10, você pode criar uma sequência de tarefas e selecionar a opção **Atualizar um sistema operacional do pacote de atualização** no assistente Criar Sequência de Tarefas. O assistente adicionará as etapas para atualizar o sistema operacional, aplicar atualizações de software e instalar aplicativos. Antes de criar a sequência de tarefas, o seguinte deve estar disponível:  

-   **Necessária**  

     - O [pacote de atualização do sistema operacional](../get-started/manage-operating-system-upgrade-packages.md) do Windows 10 deve estar disponível no console do Configuration Manager.  

-   **Necessário (se usado)**  

    -   As [atualizações de software](../../sum/get-started/synchronize-software-updates.md) devem estar sincronizadas no console do Configuration Manager.  

    -   Os [aplicativos](../../apps/deploy-use/create-applications.md) devem ser adicionados ao console do Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>Para criar uma sequência de tarefas que atualiza um sistema operacional  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente para Criar Sequência de Tarefas.  

4.  Na página **Criar uma nova sequência de tarefas** , clique em **Atualizar um sistema operacional do pacote de atualização**e, em seguida, clique em **Avançar**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Nome da sequência de tarefas**: especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: especifique uma descrição da tarefa executada pela sequência de tarefas.  

6.  Na página **Atualizar o sistema operacional Windows** , especifique as seguintes configurações e, em seguida, clique em **Avançar**.  

    -   **Atualizar pacote**: especifique o pacote de atualização que contenha os arquivos de origem de atualização do sistema operacional. Você pode verificar se você selecionou o pacote de atualização correto examinando as informações no painel **Propriedades** . Para obter mais informações, consulte [Gerenciar pacotes de atualização do sistema operacional](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Índice de edição**: se houver vários índices de edição do sistema operacional disponíveis no pacote, selecione o índice de edição desejado. Por padrão, o primeiro item é selecionado.  

    -   **Chave do produto (Product Key)**: especifique a chave do produto (Product Key) do sistema operacional Windows que será instalada. Você pode especificar as chaves de licença de volume codificadas e as chaves do produto padrão. Se você usar uma chave de produto sem codificação, cada grupo de 5 caracteres deverá ser separado por um traço (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quando a atualização é para uma edição de licença de volume, a chave do produto não é necessária. Você só precisa de uma chave do produto quando a atualização é para uma edição de varejo do Windows.  

7.  Na página **Incluir Atualizações** , especifique se deseja instalar as atualizações de software necessárias, todas as atualizações ou nenhuma e clique em **Próximo**. Se optar pela instalação das atualizações de software, o Configuration Manager instalará somente aquelas que fizerem parte das coleções das quais o computador de destino é membro.  

8.  Na página **Instalar Aplicativos** , especifique os aplicativos a instalar no computador de destino e clique em **Próximo**. Se você especificar vários aplicativos, será possível também definir a continuação da sequência de tarefas em caso de falha na instalação de algum aplicativo.  

9. Conclua o assistente.  

## <a name="download-package-content-task-sequence-step"></a>Baixar etapa de sequência de tarefas do conteúdo do pacote  
 A etapa [Baixar Conteúdo do Pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) pode ser usada antes da etapa **Atualizar o Sistema Operacional** nos seguintes cenários:  

-   Use uma sequência de tarefas de atualização única que possa funcionar com plataformas x86 e x64. Para fazer isso, inclua duas etapas **Baixar Conteúdo do Pacote** no grupo **Preparar para Atualização** com condições para detectar a arquitetura do cliente e baixar apenas o Pacote de atualização do sistema operacional apropriado. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável e use a variável para o caminho de mídia na etapa **Atualizar Sistema Operacional** .  

-   Para baixar um pacote de drivers aplicáveis dinamicamente, use duas etapas **Baixar Conteúdo do Pacote** com condições para detectar o tipo de hardware apropriado para cada pacote de drivers. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável e use a variável para o valor **Conteúdo de Teste** na seção de drivers da etapa **Atualizar Sistema Operacional** .  

   > [!NOTE]
   > Quando há mais de um pacote, o Configuration Manager adiciona um sufixo numérico ao nome da variável. Por exemplo, se você especificar uma variável de %mycontent% como uma variável personalizada, essa será a raiz de onde todo o conteúdo referenciado está armazenado (que podem ser vários pacotes). Quando você faz referência à variável em uma etapa posterior, como Atualizar Sistema Operacional, ele é usado com um sufixo numérico. Neste exemplo, %mycontent01% ou %mycontent02%, em que o número corresponde à ordem na qual o pacote está listado nesta etapa.

## <a name="optional-post-processing-task-sequence-steps"></a>Etapas opcionais de sequência de tarefas de pós-processamento  
 Depois de criar a sequência de tarefas, você pode configurar edições adicionais como etapas para desinstalar aplicativos com problemas de compatibilidade conhecidos ou adicionar ações de pós-processamento para execução depois que o computador for reiniciado e a atualização do Windows 10 for bem-sucedida. Adicione estas etapas adicionais no grupo de pós-processamento da sequência de tarefas.  

> [!NOTE]  
>  Como esta sequência de tarefas não é linear, existem condições nas etapas que podem afetar os resultados da sequência de tarefas, dependendo se ela atualizar o computador cliente com êxito ou se tiver de reverter o computador cliente para a versão do sistema operacional original.  

## <a name="optional-rollback-task-sequence-steps"></a>Etapas de sequência de tarefas de reversão opcional  
 Quando algo dá errado com o processo de atualização depois que o computador for reiniciado, a instalação vai reverter a atualização para o sistema operacional anterior e a sequência de tarefas continuará com as etapas no grupo de reversão. Depois de criar a sequência de tarefas, você pode adicionar etapas opcionais para o grupo de reversão.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Pasta e arquivos removidos após o computador reiniciar  
 Quando a sequência de tarefas para atualizar um sistema operacional para Windows 10 e todas as outras etapas da sequência de tarefas forem concluídas, os scripts de pós-processamento e reversão não são removidos quando o computador for reiniciado.  Esses arquivos de script não contêm informações confidenciais.  



<!--HONumber=Nov16_HO1-->


