---
title: CMPivot para dados em tempo real
titleSuffix: Configuration Manager
description: Saiba como usar o CMPivot no Configuration Manager para consultar clientes em tempo real.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0766bc765712fc493f01eb5aa807426ec44fa5d7
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385937"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>O CMPivot para dados em tempo real no Configuration Manager

<!--1358456-->

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager sempre forneceu um grande armazenamento centralizado de dados do dispositivo, que os clientes usam para fins de relatório. O site normalmente coleta esses dados semanalmente. Da versão 1806 em diante, o CMPivot é um novo utilitário no console que agora dá acesso ao estado dos em tempo real dos dispositivos no seu ambiente. Ele executa imediatamente uma consulta em todos os dispositivos atualmente conectados na coleção de destino e retorna os resultados. Então filtre e agrupe esses dados na ferramenta. Ao fornecer dados em tempo real de clientes online, você pode responder a perguntas de negócios com mais rapidez, solucionar problemas e responder a incidentes de segurança.

Por exemplo, na [mitigação das vulnerabilidades do canal de execução especulativa](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), um dos requisitos é atualizar o BIOS do sistema. Você pode usar o CMPivot para consultar rapidamente as informações do BIOS do sistema e localizar clientes que não estejam em conformidade.



## <a name="prerequisites"></a>Pré-requisitos

Os seguintes componentes são necessários para usar o CMPivot:

- Atualize os dispositivos de destino para a versão mais recente do cliente do Configuration Manager.  

- O administrador do Configuration Manager precisa da permissão de **Leitura** no objeto **Scripts do SMS** e a permissão **Executar Scripts** no objeto **Coleção**. A função **Executor de Scripts** tem essas permissões. Para saber mais, veja [Funções de segurança para scripts](/sccm/apps/deploy-use/create-deploy-scripts#bkmk_ScriptRoles).  

- Para coletar dados para as entidades a seguir, os clientes de destino exigem o PowerShell versão 5.0:  
    - Administradores
    - Conexão
    - IPConfig
    - SMBConfig 



## <a name="limitations"></a>Limitações

- Em uma hierarquia, conecte o console do Configuration Manager a um *site primário* para executar o CMPivot. A ação **Iniciar o CMPivot** não aparece no console quando ele está conectado a um site de administração central.  

- O CMPivot somente retorna dados para clientes conectados ao site atual.  

- Se uma coleção de dispositivos contiver dispositivos de outro site, os resultados do CMPivot serão somente de dispositivos no site atual.  

- Você não pode personalizar propriedades de entidade, colunas para resultados nem ações em dispositivos.  

- Somente uma instância do CMPivot pode ser executada por vez em um computador que esteja executando o console do Configuration Manager.  



## <a name="start-cmpivot"></a>Iniciar o CMPivot

1. No console do Configuration Manager, conecte-se ao site primário. Vá para o espaço de trabalho **Ativos e Conformidade** e selecione o nó **Coleções de Dispositivos**. Selecione uma coleção de destino e clique em **Iniciar CMPivot** na faixa de opções para iniciar a ferramenta.  

    > [!Tip]  
    > Se você não visualizar essa opção, verifique as seguintes configurações:  
    > 
    > - Com um administrador de site, confirme se a sua conta tem as permissões necessárias. Para obter mais informações, veja [Pré-requisitos](#prerequisites).  
    > 
    > - Conecte o console a um *site primário*.  

2. A interface fornece mais informações sobre o uso da ferramenta.  

     - Insira manualmente as cadeias de caracteres de consulta na parte superior ou clique nos links na documentação em linha.  

     - Clique em uma das **Entidades** para adicioná-la à cadeia de caracteres de consulta.  

     - Os links para **Operadores de Tabela**, **Funções de Agregação** e **Funções Escalares** abrem a documentação de referência da linguagem no navegador da Web. O CMPivot usa a mesma linguagem de consulta do [Azure Log Analytics](https://docs.loganalytics.io/docs/Language-Reference/Change-log).  

3. Mantenha a janela do CMPivot aberta para exibir os resultados de clientes. Quando você fecha a janela do CMPivot, a sessão é concluída.  

    > [!Note]  
    > Se a consulta tiver sido enviada, os clientes ainda enviarão uma resposta de mensagem de estado ao servidor.  



## <a name="how-to-use-cmpivot"></a>Como usar o CMPivot

![Amostra de janela do CMPivot](media/1358456-cmpivot-sample.png)

A janela do CMPivot contém os seguintes elementos:  

1. A coleção que o CMPivot atualmente tem como destino está na barra de título na parte superior e na barra de status na parte inferior da janela. Por exemplo, **Todos os Sistemas** na captura de tela acima.  

2. O painel à esquerda lista as **Entidades** disponíveis nos clientes. Algumas entidades dependem da WMI, enquanto outras usam o PowerShell para obter dados de clientes.   

    - Clique com o botão direito do mouse em uma entidade para as seguintes ações:  

       - **Inserir**: adicione a entidade à consulta na posição atual do cursor. A consulta não é executada automaticamente. Essa ação é o padrão quando você clica duas vezes em uma entidade. Use essa ação ao criar uma consulta.  

       - **Consultar tudo**: execute uma consulta para essa entidade incluindo todas as propriedades. Use essa ação para consultar rapidamente uma única entidade.  

       - **Consultar por dispositivo**: execute uma consulta para essa entidade e agrupe os resultados. Por exemplo, `Disk | summarize dcount( Device ) by Name`  

    - Expanda uma entidade para ver as propriedades específicas disponíveis para cada entidade. Clique duas vezes em uma propriedade para adicioná-la à consulta na posição atual do cursor.  

3. A guia **Início** mostra informações gerais sobre o CMPivot, incluindo links para exemplos de consultas e documentação de suporte.  

4. A guia **Consulta** exibe o painel consulta, o painel de resultados e a barra de status. A guia de consulta é selecionada no exemplo de captura de tela acima.  

5. É no painel de consulta que você compila ou digita uma consulta a ser executada em clientes na coleção.  

    - O CMPivot usa um subconjunto da mesma linguagem de consulta que o [Azure Log Analytics](https://docs.loganalytics.io/docs/Language-Reference/Change-log).  

    - Corte, copie ou cole o conteúdo no painel de consulta.  

    - Por padrão, esse painel usa o IntelliSense. Por exemplo, se você começar a digitar `D`, o IntelliSense sugerirá todas as entidades que começam com essa letra. Selecione uma opção e pressione a tecla Tab para inseri-la. Digite uma caractere de barra vertical e um espaço `| ` e, em seguida, o IntelliSense sugerirá que todos os operadores de tabela. Insira `summarize` e digite um espaço e o IntelliSense sugerirá todas as funções de agregação. Para obter mais informações sobre esses operadores e funções, clique na guia **Início** no CMPivot.  

    - O painel de consulta também oferece as seguintes opções:  

        - Executar a consulta.  

        - Avançar e recuar na lista do histórico de consultas.  

        - Criar uma coleção de associação direta.  

        - Exportar os resultados da consulta para CSV ou para a área de transferência.  

6. O painel de resultados exibe os dados retornados por clientes ativos para a consulta.  

    - As colunas disponíveis variam com base na entidade e na consulta.  

    - Clique em um nome de coluna para classificar os resultados pela propriedade.  

    - Clique com o botão direito do mouse em qualquer nome de coluna para agrupar os resultados pelas mesmas informações nessa coluna ou classificar os resultados.  

    - Clique com o botão direito do mouse no nome do dispositivo para executar as seguintes ações no dispositivo:  

       - **Dinamizar para**: consulte outra entidade neste dispositivo.  

       - **Executar Script**: inicialize o assistente de Execução de Script para executar um script do PowerShell existente neste dispositivo. Para obter mais informações, veja [Executar um script](/sccm/apps/deploy-use/create-deploy-scripts#run-a-script).  

       - **Controle Remoto**: inicialize uma sessão de Controle Remoto do Configuration Manager neste dispositivo. Para obter mais informações, consulte [Como administrar remotamente um computador de cliente do Windows](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer).  

       - **Gerenciador de Recursos**: inicialize o Gerenciador de Recursos do Configuration Manager para esse dispositivo. Para obter mais informações, veja [Exibir inventário de hardware](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory) ou [Exibir inventário de software](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).  

    - Clique com o botão direito do mouse em qualquer célula não do dispositivo para executar as seguintes ações adicionais:  

       - **Copiar**: copie o texto da célula para a área de transferência.  

       - **Mostrar dispositivos com**: consulte dispositivos com esse valor para essa propriedade. Por exemplo, nos resultados da consulta `OS`, selecione essa opção em uma célula na linha Versão: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

       - **Mostrar dispositivos sem**: consulte dispositivos sem esse valor para essa propriedade. Por exemplo, nos resultados da consulta `OS`, selecione essa opção em uma célula na linha Versão: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

       - **Aplicar Bing**: inicialize o navegador da Web padrão para www.bing.com com esse valor como a cadeia de caracteres de consulta.  

    - Clique em qualquer texto com hiperlink para dinamizar o modo de exibição nessas informações específicas.  

    - O painel de resultados não mostra mais de 20 mil linhas. Ajuste a consulta para filtrar ainda mais os dados ou reinicialize o CMPivot em uma coleção menor.  

7. A barra de status mostra as informações a seguir (da esquerda para a direita):  

    - O status da consulta atual para a coleção de destino. Esse status inclui:  
        - O número de clientes ativos que concluiu a consulta (3)  
        - O número do total de clientes (5)  
        - O número de clientes offline (2)  
        - Todos os clientes que retornaram uma falha (0)  

        Por exemplo: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

    - A ID da operação de cliente. Por exemplo: `id(16780221)`  

    - A coleção atual. Por exemplo: `PM_Team_Machines`  

    - O número total de linhas no painel de resultados. Por exemplo, `1 objects`  



## <a name="example-scenarios"></a>Cenários de exemplo

As seções a seguir apresentam exemplos de como usar o CMPivot em seu ambiente:


### <a name="example-1-stop-a-running-service"></a>Exemplo 1: parar um serviço em execução

O administrador de segurança solicita que você interrompa e desabilite o serviço Navegador do Computador assim que possível em todos os dispositivos do departamento de contabilidade. Você inicia o CMPivot em uma coleção de todos os dispositivos em contabilidade e seleciona **Consultar todos** na entidade **Serviço**. 

`Service`

Conforme os resultados aparecem, você clica com o botão direito do mouse na coluna **Nome** e seleciona **Agrupar por**. 

`Service | summarize dcount( Device ) by Name`

Na linha para o serviço **Navegador**, você clica no número vinculado por hiperlink na coluna **dcount_**. 

`Service | where (Name == 'Browser') | summarize count() by Device`

Você faz a seleção múltipla de todos os dispositivos, clica com o botão direito do mouse na seleção e escolhe **Executar Script**. Essa ação inicializa o Assistente de Execução de Script no qual você executa um script existente que você tem para interromper e desabilitar um serviço. Com CMPivot, você responde rapidamente ao incidente de segurança para todos os computadores ativos, exibindo os resultados no assistente Executar Script. Você então acompanha para criar uma linha de base de configuração para corrigir outros computadores na coleção conforme eles ficarem ativos no futuro. 

![Exemplo de CMPivot para serviço de Navegador e a ação de Executar Script](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Exemplo 2: resolver proativamente falhas de aplicativo  

Para ser proativo com manutenção operacional, uma vez por semana você executa o CMPivot em relação a uma coleção de servidores que você gerencia e seleciona **Consultar todos** na entidade **AppCrash**. Você clica com o botão direito do mouse na coluna **FileName** e seleciona **Classificar em Ordem Crescente**. Um dispositivo retorna sete resultados para sqlsqm.exe com um carimbo de data/hora aproximadamente às 3h diariamente. Você seleciona o nome do arquivo em uma das linhas, clica com o botão direito do mouse nele e seleciona **Aplicar Bing**. Procurando os resultados da pesquisa no navegador da Web, localize um artigo de Suporte da Microsoft para esse problema com mais informações e resolução. 


### <a name="example-3-bios-version"></a>Exemplo 3: versão do BIOS

Para [mitigar vulnerabilidades do canal lateral de execução especulativa](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), um dos requisitos é atualizar o BIOS do sistema. Você começa com uma consulta para a entidade **BIOS**. Em seguida, usa **Agrupar por** para agrupar pela propriedade **Versão**. Então clica com o botão direito do mouse em um valor específico, como "LENOVO – 1140" e seleciona **Mostrar dispositivos com**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Exemplo 4: espaço livre em disco

Você precisa armazenar temporariamente um arquivo grande em um servidor de arquivos de rede, mas não tem certeza de qual tem capacidade suficiente. Você inicia o CMPivot em relação a uma coleção de servidores de arquivos e consulta a entidade **Disco**. Você modifica a consulta para CMPivot para retornar rapidamente uma lista de servidores ativos contendo dados de armazenamento em tempo real:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`



## <a name="inside-cmpivot"></a>Dentro do CMPivot

O CMPivot envia consultas para os clientes que usam o "canal rápido" do Configuration Manager. Esse canal de comunicação do servidor para o cliente também é usado por outros recursos, como ações de notificação do cliente, status do cliente e Endpoint Protection. Os clientes retornarão os resultados por meio do sistema de mensagens de estado igualmente rápido. As mensagens de estado são armazenadas temporariamente no banco de dados. 

As consultas e os resultados são todos somente texto. As entidades **InstallSoftware** e **Processo** retornam alguns dos maiores conjuntos de resultados. Durante o teste de desempenho, o maior tamanho do arquivo de mensagem de estado de um cliente para essas consultas foi menor que **1 KB**. Dimensionado para um ambiente grande com 50 mil clientes ativos, essa consulta única geraria menos de 50 MB de dados pela rede.  

Uma consulta atinge o tempo limite após uma hora. Por exemplo, uma coleção tem 500 dispositivos e 450 dos clientes estão online no momento. Esses dispositivos ativos recebem a consulta e retornam os resultados quase imediatamente. Se você deixar a janela CMPivot aberta, conforme os outros 50 clientes ficarem online, eles também receberão a consulta e retornarão resultados. 



## <a name="see-also"></a>Consulte também
[Criar e executar scripts do PowerShell](/sccm/apps/deploy-use/create-deploy-scripts)
