---
title: Ponto de distribuição de recepção
titleSuffix: Configuration Manager
description: Saiba mais sobre as configurações e limitações para usar um ponto de distribuição por pull com o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a5336db0bd16d4845650bae775f2eff895e617fb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142265"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>Usar um ponto de distribuição por pull com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Quando você distribui conteúdo para um ponto de distribuição padrão no console do Configuration Manager, o servidor do site envia o conteúdo por push ao ponto de distribuição. O ponto de distribuição por pull obtém o conteúdo baixando-o de um local de origem, como um cliente.  

Quando você distribui conteúdo para vários pontos de distribuição, os pontos de distribuição de pull ajudam a reduzir a carga de processamento no servidor do site. Eles também podem acelerar a transferência de conteúdo para cada servidor. Normalmente, o componente gerenciador de distribuição no servidor do site envia conteúdo para cada ponto de distribuição. Nesse caso, o site transfere o processo de transferência de conteúdo para os pontos de distribuição de pull.  

Você pode configurar pontos de distribuição individuais para serem pontos de distribuição de recepção. Para cada ponto de distribuição por pull, especifique um ou mais pontos de distribuição de origem do qual ele possa obter o conteúdo. Um ponto de distribuição por pull só pode baixar conteúdo de um ponto de distribuição especificado como ponto de distribuição de origem. 

Quando você distribui conteúdo para um ponto de distribuição por pull no console, o servidor do site envia uma notificação. Em seguida, o ponto de distribuição por pull baixa o conteúdo de um ponto de distribuição de origem. Um ponto de distribuição por pull gerencia a transferência de conteúdo baixando de um ponto de distribuição que já tem uma cópia do conteúdo.  

Os pontos de distribuição de pull dão suporte às mesmas configurações e funcionalidades que os pontos de distribuição típicos. Por exemplo, um ponto de distribuição por pull dá suporte para: 
- Configurações de multicast e PXE
- Validação de conteúdo
- Distribuição de conteúdo sob demanda
- Comunicações HTTP ou HTTPS de clientes
- As mesmas opções de certificado que os outros pontos de distribuição
- Gerenciar individualmente ou como membro de um grupo de pontos de distribuição  

> [!IMPORTANT]  
> Embora um ponto de distribuição de recepção dê suporte à comunicação por meio dos protocolos HTTP e HTTPS, ao usar o console do Configuration Manager, você só poderá especificar pontos de distribuição de origem configurados para HTTP. É possível usar o SDK do Configuration Manager para especificar um ponto de distribuição de origem configurado para HTTPS.  

Configure um ponto de distribuição por pull ao instalar o ponto de distribuição. Depois de criar um ponto de distribuição, configure-o como ponto de distribuição por pull editando as propriedades de função. Para obter mais informações de como habilitar um ponto de distribuição como um ponto de distribuição por pull, confira [Ponto de distribuição por pull](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pull-distribution-point).  

Remova a configuração de ponto de distribuição por pull, editando as propriedades do ponto de distribuição. Quando você remove a configuração de ponto de distribuição por pull, ele retorna à operação normal. O servidor do site gerencia as próximas transferências de conteúdo para o ponto de distribuição.  



### <a name="distribution-process"></a>Processo de distribuição

Quando você distribui conteúdo para um ponto de distribuição por pull, ocorre a seguinte sequência de eventos:

-   Assim que você distribui conteúdo para um ponto de distribuição por pull no console, o componente Gerenciador de Transferência de Pacote no servidor do site verifica o banco de dados do site para confirmar se o conteúdo está disponível em um ponto de distribuição de origem. Se ele não conseguir confirmar que o conteúdo está em um ponto de distribuição de origem do ponto de distribuição por pull, ele repetirá a verificação a cada 20 minutos até que o conteúdo esteja disponível.  

-   Quando o Gerenciador de Transferência de Pacote confirma que o conteúdo está disponível, ele notifica o ponto de distribuição de recepção para que ele baixe o conteúdo. Se essa notificação falhar, ele tentará novamente com base nas **Configurações de repetição** do componente Distribuição de Software para pontos de distribuição por pull. Quando o ponto de distribuição por pull recebe essa notificação, ele tenta baixar o conteúdo de seus pontos de distribuição de origem.  

-   Enquanto o ponto de distribuição por pull baixa o conteúdo, o Gerenciador de Transferência de Pacote sonda o status com base nas **Configurações de sondagem de status** do componente Distribuição de Software dos pontos de distribuição por pull.  Quando o ponto de distribuição de recepção concluir o download do conteúdo, ele enviará esse status a um ponto de gerenciamento.  



## <a name="configure-site-component-settings"></a>Definir configurações de componentes do site

Ao usar um ponto de distribuição por pull, examine e defina as seguintes configurações de componentes do site:  

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2.  Selecione o site. Na faixa de opções, clique em **Configurar componentes do site** e selecione **Distribuição de Software**.  

3. Mude para a guia **Ponto de distribuição por pull**.  

4.  No grupo **Configurações de repetição**, examine os seguintes valores:  

    -   **Número de repetições**: o número de vezes que o Gerenciador de Transferência de Pacote tenta notificar o ponto de distribuição de recepção para baixar o conteúdo. Depois de tentar esse número de vezes, o Gerenciador de Transferência de Pacote cancelará a transferência. Esse valor é 30 por padrão.  

    -   **Atraso antes de tentar novamente (minutos)**: o número de minutos que o Gerenciador de Transferência de Pacote espera entre as tentativas. Esse valor é 20 por padrão.  

5.  No grupo **Configurações de sondagem de status**, examine os seguintes valores:  

    -   **Número de sondagens**: o número de vezes que o Gerenciador de Transferência de Pacote contata o ponto de distribuição de recepção para recuperar o status do trabalho. Se o Gerenciador de Transferência de Pacote tentar esse número de vezes antes que o trabalho seja concluído, ele cancelará a transferência. Esse valor é 72 por padrão.   

    -   **Atraso antes de tentar novamente (minutos)**: o número de minutos que o Gerenciador de Transferência de Pacote espera entre as tentativas. Esse valor é 60 por padrão.   
    
    > [!NOTE]  
    >  Quando o Gerenciador de Transferência de Pacote cancela um trabalho porque ele excedeu o número de tentativas de sondagem, o ponto de distribuição por pull continua a baixar o conteúdo. Ao terminar, o ponto de distribuição por pull envia a mensagem de status apropriada e o console reflete o novo status.  
    


## <a name="limitations"></a>Limitações 

-   Não é possível configurar um ponto de distribuição na nuvem como um ponto de distribuição por pull.  

-   Não é possível configurar a função de ponto de distribuição em um servidor do site como um ponto de distribuição por pull.  

-   A definição do conteúdo de pré-configuração substitui a configuração de ponto de distribuição por pull. Se você habilitar a opção **Habilitar este ponto de distribuição para conteúdo pré-configurado** em um ponto de distribuição por pull, ele passará a esperar o conteúdo. Ele não passará a efetuar pull do conteúdo do ponto de distribuição de origem. Como um ponto de distribuição padrão habilitado para conteúdo pré-teste, ele não recebe conteúdo do servidor do site. Para obter mais informações, confira [Conteúdo pré-teste](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  

-   Um ponto de distribuição por pull não usa configurações de agendamento ou de limite de taxa. Quando você configura um ponto de distribuição que já está instalado para ser um ponto de distribuição por pull, as configurações de agendamento e de limite de taxa são salvas, mas não são usadas. Se, mais tarde, você remover a configuração do ponto de distribuição de recepção, as configurações de agendamento e limite de taxa serão implementadas conforme definido anteriormente.  

    > [!NOTE]  
    >  As guias **Agendamento** e **Limites de Taxa** não ficam visíveis nas propriedades do ponto de distribuição.  

-   Os pontos de distribuição por pull não usam as configurações na guia **Geral** das **Propriedades do Componente de Distribuição de Software** de cada site. Essas configurações incluem **Distribuição simultânea** e **Repetição multicast**.  

-   Para transferir conteúdo de um ponto de distribuição de origem em uma floresta remota, instale o cliente do Configuration Manager no ponto de distribuição por pull. Além disso, configure uma conta de acesso à rede que possa acessar o ponto de distribuição de origem. Começando na versão 1806, se você habilitar a opção do site para **Usar certificados gerados pelo Configuration Manager para o sistema de sites HTTP**, não será necessário usar uma conta de acesso à rede.<!--1358228-->  

-   Se o ponto de distribuição por pull também for um cliente do Configuration Manager, a versão do cliente precisará ser a mesma que a do site do Configuration Manager que instala esse ponto de distribuição por pull. O ponto de distribuição por pull usa o CCMFramework comum entre o ponto de distribuição por pull e o cliente do Configuration Manager.  



## <a name="about-source-distribution-points"></a>Sobre os pontos de distribuição de origem  

Ao configurar o ponto de distribuição por pull, especifique um ou mais pontos de distribuição de origem:  

-   O assistente exibe apenas os pontos de distribuição qualificados para serem pontos de distribuição de origem.  

-   Um ponto de distribuição de recepção pode ser especificado como um ponto de distribuição de origem para outro ponto de distribuição de recepção.  

-   Somente os pontos de distribuição com suporte para HTTP podem ser especificados como pontos de distribuição de origem quando o console do Configuration Manager é usado.  

-   Use o SDK do Configuration Manager para especificar um ponto de distribuição de origem que está configurado para HTTPS. Para usar um ponto de distribuição de origem que está configurado para HTTPS, instale o cliente do Configuration Manager no ponto de distribuição por pull.  

-   Começando na versão 1806, se os escritórios remotos tiverem uma conexão melhor com a Internet ou para reduzir a carga em seus links de WAN, use um [ponto de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) no Microsoft Azure como a origem. O ponto de distribuição por pull precisa de acesso à Internet para se comunicar com o Microsoft Azure. O conteúdo precisa ser distribuído ao ponto de distribuição na nuvem de origem.<!--1321554-->  

    > [!Note]  
    > Esse recurso pode incorrer em encargos para sua assinatura do Azure para armazenamento e rede para saída de dados. Para obter mais informações, confira o [Custo do uso de um ponto de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost).  


> [!Tip]  
> Quando um ponto de distribuição de recepção baixa conteúdo de um ponto de distribuição de origem, o ponto de distribuição de recepção é contado como um cliente na coluna **Cliente Acessado (Exclusivo)** do relatório **Resumo de uso do ponto de distribuição** .  


### <a name="source-priorities"></a>Prioridades de origem

-   Atribua uma prioridade separada para cada ponto de distribuição de origem, ou atribua vários pontos de distribuição de origem à mesma prioridade.  

-   A prioridade determina a ordem na qual o ponto de distribuição por pull solicita o conteúdo dos seus pontos de distribuição de origem.  

-   Pontos de distribuição de recepção inicialmente entram em contato com um ponto de distribuição de origem com o menor valor de prioridade. Se houver vários pontos de distribuição de origem com a mesma prioridade, o ponto de distribuição por pull selecionará aleatoriamente uma das origens com prioridade.  

-   Se o conteúdo não estiver disponível em uma origem selecionada, o ponto de distribuição por pull tentará baixar o conteúdo de outro ponto de distribuição com a mesma prioridade.  

-   Se o conteúdo não estiver em nenhum dos pontos de distribuição com uma determinada prioridade, o ponto de distribuição por pull tentará baixar o conteúdo de um ponto de distribuição de origem com o próximo nível de prioridade. Ele continuará a pesquisa até que o conteúdo seja localizado.   

- Se o conteúdo não estiver em nenhum dos pontos de distribuição de origem atribuídos, o ponto de distribuição por pull esperará 30 minutos e, em seguida, iniciará o processo novamente.  



## <a name="inside-the-pull-distribution-point"></a>Dentro do ponto de distribuição por pull 

-   Para gerenciar a transferência de conteúdo, os pontos de distribuição por pull usam o componente **CCMFramework**. O cliente do Configuration Manager inclui esse componente.  

-   Quando você habilita o ponto de distribuição por pull, o site instala **pulldp.msi**. Esse instalador também adiciona o componente CCMFramework. A estrutura não exige o cliente do Configuration Manager.  

-   Depois que o ponto de distribuição por pull é instalado, ele usa principalmente o serviço **CCMExec** para funcionar.  

-   Quando o ponto de distribuição por pull transfere conteúdo, ele usa o **BITS** (Serviço de Transferência Inteligente em Segundo Plano) interno do Windows. O ponto de distribuição por pull não exige que você instale a extensão do BITS para o servidor IIS.<!--sms.503672 -Clarified BITS use-->

-  Para obter detalhes operacionais, confira os seguintes arquivos de log no ponto de distribuição por pull:  
    - **DataTransferService.log**
    - **PullDP.log**



## <a name="see-also"></a>Consulte também  
 [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
