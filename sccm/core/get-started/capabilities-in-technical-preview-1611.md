---
title: Recursos no Technical Preview 1611
titleSuffix: Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1611."
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
caps.latest.revision: 
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: b56aee663319861427048fb722b1cdc0b5cc664d
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1611-for-system-center-configuration-manager"></a>Funcionalidades do Technical Preview 1611 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*



Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1611. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    

**Problemas conhecidos nesse Technical Preview:**   
- ***Status de pré-requisito***: quando você instala a versão 1611, o status geral de pré-requisitos pode ser mostrado como aprovado com avisos, mas não listará quais pré-requisitos causaram os avisos. Isso pode ser provocado pelos dois pré-requisitos a seguir:
  - Opções de Memória de Criação de Índice do SQL
  - Verifica se há suporte para a versão do SQL Server  

 Como esses são apenas avisos, eles podem ser ignorados.

- ***PowerShell***: ao conectar-se ao Windows PowerShell no console do Configuration Manager, você poderá receber o seguinte erro: **Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml não é assinado digitalmente**.  

   Você pode resolver esse problema substituindo alguns arquivos por versões assinadas da versão 1610. Copie todos os arquivos com as seguintes extensões da pasta **&lt;diretório de instalação>\AdminConsole\bin\** na sua instalação da versão 1610: **.psd1**, **.ps1xml** e **.psm1**. Cole esses arquivos na pasta **&lt;diretório de instalação>\AdminConsole\bin\** da sua instalação do Technical Preview 1611, substituindo a versão 1611 dos arquivos.


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Conteúdo de armazenamento prévio em cache para sequências de tarefas e implantações disponíveis
Nesta visualização técnica, para sequências de tarefas e implantações disponíveis, você pode optar por usar o recurso de armazenamento prévio em cache para que os clientes baixem apenas conteúdo relevante antes de um usuário instalar o conteúdo.

Por exemplo, digamos que você deseja implantar uma sequência de tarefas de atualização in-loco do Windows 10, deseja apenas uma sequência de tarefas para todos os usuários e tem várias arquiteturas e/ou idiomas. No Branch Atual, se você criar uma implantação disponível e, em seguida, o usuário clicar em **Instalar** no Centro de Software, o conteúdo será baixado neste momento. Isso acrescenta um tempo antes que a instalação esteja pronta para iniciar. Como alternativa, no Branch Atual, se você criar uma implantação de sequência de tarefas disponível, todo o conteúdo referenciado na sequência de tarefas será baixado. Isso inclui o pacote de atualização do sistema operacional para todas as arquiteturas e idiomas. Se cada um tiver aproximadamente 3 GB de tamanho, o pacote de download poderá ser bastante grande.

O recurso de conteúdo de armazenamento prévio em cache oferece a opção de permitir que o cliente baixe apenas o conteúdo aplicável assim que receber a implantação. Portanto, quando o usuário clicar em **Instalar** no Centro de Software, o conteúdo estará pronto e a instalação iniciará rapidamente, pois o conteúdo está no disco rígido local.

### <a name="to-configure-the-pre-cache-feature"></a>Para configurar o recurso de armazenamento prévio em cache

1. Crie pacotes de atualização de sistema operacional para arquiteturas e idiomas específicos. Especifique a arquitetura e o idioma na guia **Fonte de Dados** do pacote. Para o idioma, use a conversão decimal (por exemplo, 1033 é o decimal para inglês e 0x0409 é o equivalente hexadecimal). Para ver mais detalhes, veja [Criar uma sequência de tarefas para atualizar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Os valores de arquitetura e idioma são usados para corresponder condições de etapa de sequência de tarefas que você criará na próxima etapa para determinar se o pacote de atualização do sistema operacional deve ser previamente armazenado em cache.
2. Crie uma sequência de tarefas com etapas condicionais para diferentes idiomas e arquiteturas. Por exemplo, para a versão em inglês, você pode criar uma etapa com o seguinte:

    ![Propriedades de armazenamento prévio em cache](media/precacheproperties2.png)

    ![Opções de armazenamento prévio em cache](media/precacheoptions2.png)  

3. Implantar a sequência de tarefas. Para o recurso de armazenamento prévio em cache, configure o seguinte:
    - Na guia **Geral**, selecione **Conteúdo previamente baixado para esta sequência de tarefas**.
    - Na guia **Configurações de implantação**, configure a sequência de tarefas com **Disponível** para **Finalidade**. Se você criar uma implantação **Obrigatória**, a funcionalidade de armazenamento prévio em cache não funcionará.
    - Na guia **Agendamento**, para a configuração **Agendar quando essa implantação estará disponível**, escolha uma hora futura que conceda aos clientes tempo suficiente para armazenar previamente em cache o conteúdo para a implantação disponibilizada para os usuários. Por exemplo, você pode definir o tempo disponível para 3 horas no futuro para oferecer tempo suficiente para o conteúdo ser previamente armazenado em cache.  
    - Na guia **Pontos de Distribuição**, defina as configurações **Opções de implantação**. Se o conteúdo não tiver sido armazenado previamente em cache em um cliente antes de um usuário iniciar a instalação, essas configurações serão usadas.


### <a name="user-experience"></a>Experiência do usuário
- Quando o cliente receber a política de implantação, ele começará a armazenar previamente o conteúdo em cache. Isso inclui todo o conteúdo referenciado (todos os demais tipos de pacote) e somente o pacote atualização do sistema operacional que corresponder ao cliente, com base nas condições que você definir na sequência de tarefas.
- Quando a implantação for disponibilizada para os usuários (a configuração na guia **Agendamento** da implantação), uma notificação será exibida para informar os usuários sobre a nova implantação e ela ficará visível no Centro de Software. O usuário poderá acessar o Centro de Software e clicar em **Instalar** para iniciar a instalação.
- Se o conteúdo não tiver sido armazenado previamente em cache em sua totalidade, ele usará as configurações especificadas na guia **Opções de Implantação** da implantação. É recomendável que haja tempo suficiente desde que a implantação é criada até o momento em que ela se fica disponível para os usuários, a fim de conceder aos clientes tempo suficiente para armazenar previamente o conteúdo em cache.


## <a name="see-also"></a>Consulte também
[Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md)
