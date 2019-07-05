---
title: CMPivot para dados em tempo real
titleSuffix: Configuration Manager
description: Saiba como usar o CMPivot no Configuration Manager para consultar clientes em tempo real.
ms.date: 05/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3626514d4cd7f2d26e3c198931eb6fad49123dd2
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67551303"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>O CMPivot para dados em tempo real no Configuration Manager

<!--1358456-->

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager sempre forneceu um grande armazenamento centralizado de dados do dispositivo, que os clientes usam para fins de relatório. O site normalmente coleta esses dados semanalmente. Da versão 1806 em diante, o CMPivot é um novo utilitário no console que agora dá acesso ao estado dos em tempo real dos dispositivos no seu ambiente. Ele executa imediatamente uma consulta em todos os dispositivos atualmente conectados na coleção de destino e retorna os resultados. Então filtre e agrupe esses dados na ferramenta. Ao fornecer dados em tempo real de clientes online, você pode responder a perguntas de negócios com mais rapidez, solucionar problemas e responder a incidentes de segurança.

Por exemplo, na [mitigação das vulnerabilidades do canal de execução especulativa](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), um dos requisitos é atualizar o BIOS do sistema. Você pode usar o CMPivot para consultar rapidamente as informações do BIOS do sistema e localizar clientes que não estejam em conformidade.

 > [!Tip]  
 > Alguns softwares de segurança podem bloquear scripts em execução de c:\windows\ccm\scriptstore. Isso pode impedir a execução bem-sucedida das consultas do CMPivot. Alguns softwares de segurança também podem gerar alertas ou eventos de auditoria ao executar o CMPivot PowerShell.


## <a name="prerequisites"></a>Pré-requisitos

Os seguintes componentes são necessários para usar o CMPivot:

- Atualize os dispositivos de destino para a versão mais recente do cliente do Configuration Manager.  

- Permissões para CMPivot:
  - Permissão de **Leitura** no objeto **Scripts SMS**
  - Permissão para **Executar Scripts** na **Coleção**
  - Permissão de **Leitura** nos **Relatórios de Inventário**
  - O escopo padrão. 

- Os clientes de destino exigem no mínimo o PowerShell versão 4.

- Para coletar dados para as entidades a seguir, os clientes de destino exigem o PowerShell versão 5.0:  
  - Administradores
  - Conexão
  - IPConfig
  - SMBConfig

 
## <a name="limitations"></a>Limitações

- Em uma hierarquia, conecte o console do Configuration Manager a um *site primário* para executar o CMPivot. A ação **Iniciar o CMPivot** não aparece no console quando ele está conectado a um CAS (site de administração central).
  - Começando no Configuration Manager versão 1902, você pode executar o CMPivot de um CAS. Em alguns ambientes, são necessárias permissões adicionais. Para obter mais informações, confira [CMPivot starting in version 1902](#bkmk_cmpivot1902) (CMPivot começando na versão 1902).

- O CMPivot somente retorna dados para clientes conectados ao site atual.  

- Se uma coleção de dispositivos contiver dispositivos de outro site, os resultados do CMPivot serão somente de dispositivos no site atual.  

- Você não pode personalizar propriedades de entidade, colunas para resultados nem ações em dispositivos.  

- Somente uma instância do CMPivot pode ser executada por vez em um computador que esteja executando o console do Configuration Manager.  

- Na versão 1806, a consulta da entidade **Administrators** só funciona se o grupo se chama "Administrators". Ela não funcionará se o nome do grupo estiver traduzido. Por exemplo, "Administrateurs" em francês.<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>Iniciar o CMPivot

1. No console do Configuration Manager, conecte-se ao site primário. Vá para o workspace **Ativos e Conformidade** e selecione o nó **Coleções de Dispositivos**. Selecione uma coleção de destino e clique em **Iniciar CMPivot** na faixa de opções para iniciar a ferramenta.  

    > [!Tip]  
    > Se você não visualizar essa opção, verifique as seguintes configurações:  
    > 
    > - Com um administrador de site, confirme se a sua conta tem as permissões necessárias. Para obter mais informações, veja [Pré-requisitos](#prerequisites).  
    > 
    > - Conecte o console a um *site primário*.  

2. A interface fornece mais informações sobre o uso da ferramenta.  

     - Insira manualmente as cadeias de caracteres de consulta na parte superior ou clique nos links na documentação em linha.  

     - Clique em uma das **Entidades** para adicioná-la à cadeia de caracteres de consulta.  

     - Os links para **Operadores de Tabela**, **Funções de Agregação** e **Funções Escalares** abrem a documentação de referência da linguagem no navegador da Web. O CMPivot usa a [KQL (Linguagem de Consulta Kusto)](https://docs.microsoft.com/azure/kusto/query/).  

3. Mantenha a janela do CMPivot aberta para exibir os resultados de clientes. Quando você fecha a janela do CMPivot, a sessão é concluída.  

    > [!Note]  
    > Se a consulta tiver sido enviada, os clientes ainda enviarão uma resposta de mensagem de estado ao servidor.  



## <a name="how-to-use-cmpivot"></a>Como usar o CMPivot

![Amostra de janela do CMPivot](media/1358456-cmpivot-sample.png)

A janela do CMPivot contém os seguintes elementos:  

1. A coleção que o CMPivot atualmente tem como destino está na barra de título na parte superior e na barra de status na parte inferior da janela. Por exemplo, "PM_Team_Machines" na captura de tela acima.  

2. O painel à esquerda lista as **Entidades** disponíveis nos clientes. Algumas entidades dependem da WMI, enquanto outras usam o PowerShell para obter dados de clientes.   

    - Clique com o botão direito do mouse em uma entidade para as seguintes ações:  

       - **Inserir**: Adicione a entidade à consulta na posição atual do cursor. A consulta não é executada automaticamente. Essa ação é o padrão quando você clica duas vezes em uma entidade. Use essa ação ao criar uma consulta.  

       - **Consultar tudo**: Execute uma consulta para essa entidade incluindo todas as propriedades. Use essa ação para consultar rapidamente uma única entidade.  

       - **Consultar por dispositivo**: Execute uma consulta para essa entidade e agrupe os resultados. Por exemplo, `Disk | summarize dcount( Device ) by Name`  

    - Expanda uma entidade para ver as propriedades específicas disponíveis para cada entidade. Clique duas vezes em uma propriedade para adicioná-la à consulta na posição atual do cursor.  

3. A guia **Início** mostra informações gerais sobre o CMPivot, incluindo links para exemplos de consultas e documentação de suporte.  

4. A guia **Consulta** exibe o painel consulta, o painel de resultados e a barra de status. A guia de consulta é selecionada no exemplo de captura de tela acima.  

5. É no painel de consulta que você compila ou digita uma consulta a ser executada em clientes na coleção.  

    - O CMPivot usa um subconjunto da [KQL (Linguagem de Consulta Kusto)](https://docs.microsoft.com/azure/kusto/query/).  

    - Corte, copie ou cole o conteúdo no painel de consulta.  
    <!-- markdownlint-disable MD038 -->
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

      - **Dinamizar Para**: Consulte outra entidade neste dispositivo.  

      - **Executar Script**: Inicie o assistente de Execução de Script para executar um script do PowerShell existente neste dispositivo. Para obter mais informações, veja [Executar um script](/sccm/apps/deploy-use/create-deploy-scripts#run-a-script).  

      - **Controle Remoto**: Inicie uma sessão de Controle Remoto do Configuration Manager neste dispositivo. Para obter mais informações, consulte [Como administrar remotamente um computador de cliente do Windows](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer).  

      - **Gerenciador de Recursos**: Inicie o Gerenciador de Recursos do Configuration Manager para esse dispositivo. Para obter mais informações, veja [Exibir inventário de hardware](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory) ou [Exibir inventário de software](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).  

   - Clique com o botão direito do mouse em qualquer célula não do dispositivo para executar as seguintes ações adicionais:  

     - **Copiar**: Copie o texto da célula para a área de transferência.  

     - **Mostrar dispositivos com**: Consulte dispositivos com esse valor para essa propriedade. Por exemplo, nos resultados da consulta `OS`, selecione essa opção em uma célula na linha Versão: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Mostrar dispositivos sem**: Consulte dispositivos sem esse valor para essa propriedade. Por exemplo, nos resultados da consulta `OS`, selecione essa opção em uma célula na linha Versão: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Procure no Bing**: Inicie o navegador da Web padrão para www.bing.com com esse valor como a cadeia de caracteres de consulta.  

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


### <a name="example-1-stop-a-running-service"></a>Exemplo 1: Parar um serviço em execução

O administrador de segurança solicita que você interrompa e desabilite o serviço Navegador do Computador assim que possível em todos os dispositivos do departamento de contabilidade. Você inicia o CMPivot em uma coleção de todos os dispositivos em contabilidade e seleciona **Consultar todos** na entidade **Serviço**. 

`Service`

Conforme os resultados aparecem, você clica com o botão direito do mouse na coluna **Nome** e seleciona **Agrupar por**. 

`Service | summarize dcount( Device ) by Name`

Na linha para o serviço **Navegador**, você clica no número vinculado por hiperlink na coluna **dcount_** . 

`Service | where (Name == 'Browser') | summarize count() by Device`

Você faz a seleção múltipla de todos os dispositivos, clica com o botão direito do mouse na seleção e escolhe **Executar Script**. Essa ação inicializa o Assistente de Execução de Script no qual você executa um script existente que você tem para interromper e desabilitar um serviço. Com CMPivot, você responde rapidamente ao incidente de segurança para todos os computadores ativos, exibindo os resultados no assistente Executar Script. Você então acompanha para criar uma linha de base de configuração para corrigir outros computadores na coleção conforme eles ficarem ativos no futuro. 

![Exemplo de CMPivot para serviço de Navegador e a ação de Executar Script](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Exemplo 2: Resolver proativamente falhas de aplicativo  

Para ser proativo com manutenção operacional, uma vez por semana você executa o CMPivot em relação a uma coleção de servidores que você gerencia e seleciona **Consultar todos** na entidade **AppCrash**. Você clica com o botão direito do mouse na coluna **FileName** e seleciona **Classificar em Ordem Crescente**. Um dispositivo retorna sete resultados para sqlsqm.exe com um carimbo de data/hora aproximadamente às 3h diariamente. Você seleciona o nome do arquivo em uma das linhas, clica com o botão direito do mouse nele e seleciona **Aplicar Bing**. Procurando os resultados da pesquisa no navegador da Web, localize um artigo de Suporte da Microsoft para esse problema com mais informações e resolução. 


### <a name="example-3-bios-version"></a>Exemplo 3: Versão da BIOS

Para [mitigar vulnerabilidades do canal lateral de execução especulativa](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), um dos requisitos é atualizar o BIOS do sistema. Você começa com uma consulta para a entidade **BIOS**. Em seguida, usa **Agrupar por** para agrupar pela propriedade **Versão**. Então clica com o botão direito do mouse em um valor específico, como "LENOVO – 1140" e seleciona **Mostrar dispositivos com**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Exemplo 4: Espaço livre em disco

Você precisa armazenar temporariamente um arquivo grande em um servidor de arquivos de rede, mas não tem certeza de qual tem capacidade suficiente. Inicie o CMPivot em uma coleção de servidores de arquivos e consulte a entidade **Disk**. Modifique a consulta para CMPivot para retornar rapidamente uma lista de servidores ativos contendo dados de armazenamento em tempo real:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="bkmk_cmpivot"></a> CMPivot começando na versão 1810
<!--1359068, 3607759-->

O CMPivot inclui as seguintes melhorias começando no Configuration Manager versão 1810:

- [Desempenho e utilitário do CMPivot](#bkmk_cmpivot-perf)
- [Funções escalares](#bkmk_cmpivot-functions)  
- [Visualizações de renderização](#bkmk_cmpivot-charts)  
- [Inventário de hardware](#bkmk_cmpivot-hinv)  
- [Operadores escalares](#bkmk_cmpivot-operators)  
- [Resumo da consulta](#bkmk_cmpivot-summary)  
- [Mensagens de status de auditoria](#cmpivot-audit-status-messages)

### <a name="bkmk_cmpivot-perf"></a> Desempenho e utilitário do CMPivot

- O CMPivot retornará até 100 mil células em vez de 20 mil linhas.
  - Se a entidade tiver 5 propriedades, o que significa 5 colunas, serão mostradas até 20.000 linhas.
  - Para uma entidade com 10 propriedades, serão mostradas até 10.000 linhas.
  - O total de dados mostrado será menor ou igual a 100.000 células.
- Na guia Resumo da Consulta, selecione a contagem de dispositivos com falha e offline e, em seguida, selecione a opção para **Criar coleção**. Essa opção facilita o direcionamento desses dispositivos com uma implantação de correção.
- Salve consultas **Favoritas** clicando no ícone de pasta.
   ![Exemplo de salvamento de uma consulta favorita no CMPivot](media/cmpivot-favorite.png)

- Os clientes atualizados para a versão 1810 retornam uma saída menor que 80 KB para o site por meio de um canal de comunicação rápido.
  - Essa alteração aumenta o desempenho da exibição da saída do script ou da consulta.
  - Se a saída do script ou da consulta for maior que 80 KB, o cliente enviará os dados por meio de uma mensagem de estado.
  - Se o cliente não tiver atualizado para a versão 1810 do cliente, ele continuará usando mensagens de estado.

### <a name="bkmk_cmpivot-functions"></a> Funções escalares
O CMPivot dá suporte para as funções escalares a seguir:
- **ago()** : subtrai o intervalo de tempo determinado da hora atual UTC do relógio  
- **datetime_diff()** : calcula a diferença do calendário entre dois valores de data e hora  
- **now()** : retorna a hora atual UTC do relógio  
- **bin()** : arredonda os valores até um número inteiro múltiplo de um determinado tamanho de compartimento  

> [!Note]  
> O tipo de dados de data e hora representa um momento no tempo, geralmente expresso como uma data e hora do dia. Valores de hora são medidos em unidades de 1 segundo. Um valor de data e hora está sempre no fuso horário UTC. Sempre expresse literais de data e hora no formato ISO 8601, por exemplo, `yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>Exemplos
- `datetime(2015-12-31 23:59:59.9)`: um literal de data e hora específico   
- `now()`: a hora atual  
- `ago(1d)`: a hora atual menos um dia  


### <a name="bkmk_cmpivot-charts"></a> Visualizações de renderização

O CMPivot agora inclui suporte básico para o [operador de renderização](https://docs.microsoft.com/azure/kusto/query/renderoperator) da KQL. Esse suporte inclui os seguintes tipos:  
- **barchart**: a primeira coluna é o eixo x e pode ser texto, datetime ou numérico. A segunda coluna deve ser numérica e é exibida como uma faixa horizontal.  
- **columnchart**: como barchart, com faixas verticais, em vez de faixas horizontais.  
- **piechart**: a primeira coluna é a cor do eixo, a segunda coluna é numérica.  
- **timechart**: gráfico de linha. A primeira coluna é o eixo x e deve ser datetime. A segunda coluna é o eixo y.  

#### <a name="example-bar-chart"></a>Exemplo: gráfico de barras
A consulta a seguir renderiza os aplicativos usados mais recentemente como um gráfico de barras:

```
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```
![Exemplo de visualização de gráfico de barras CMPivot](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>Exemplo: gráfico de tempo
Para renderizar gráficos de tempo, use o novo operador **bin()** para agrupar eventos no tempo. A consulta seguinte mostra quando os dispositivos iniciaram nos últimos sete dias:

``` 
OperatingSystem 
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```
![Exemplo de visualização de gráfico de tempo CMPivot](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>Exemplo: gráfico de pizza
A consulta a seguir exibe todas as versões de sistema operacional em um gráfico de pizza:

```
OperatingSystem 
| summarize count() by Caption
| render piechart
```
![Exemplo de visualização de gráfico de pizza CMPivot](media/1359068-cmpivot-piechart.png)


### <a name="bkmk_cmpivot-hinv"></a> Inventário de hardware
Use o CMPivot para consultar qualquer classe de inventário de hardware. Essas classes incluem todas as extensões personalizadas que você fez ao inventário de hardware. O CMPivot imediatamente retorna resultados em cache da última verificação de inventário de hardware no banco de dados do site. Ao mesmo tempo, ele atualiza os resultados, se necessário, com os dados dinâmicos de qualquer cliente online.

A saturação de cor dos dados na tabela de resultados ou no gráfico indica se os dados estão armazenados em cache ou ativos. Por exemplo, azul-escuro representa dados em tempo real de um cliente online. Azul claro corresponde a dados armazenados em cache.

#### <a name="example"></a>Exemplo
```
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```
![Exemplo de consulta de inventário CMPivot com visualização de gráfico de coluna](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>Limitações
- Não há suporte para as seguintes entidades de inventário de hardware:  
    - Propriedades de matriz, por exemplo, endereço IP  
    - Real32/Real64 <!--example?-->  
    - Propriedades do objeto inserido <!--example?-->  
- Nomes de entidade de inventário devem começar com um caractere
- Não é possível substituir as entidades internas criando uma entidade de inventário de mesmo nome  


### <a name="bkmk_cmpivot-operators"></a> Operadores escalares
O CMPivot inclui os seguintes operadores escalares:  

> [!Note]  
> - LHS: cadeia de caracteres à esquerda do operador  
> - RHS: cadeia de caracteres à direita do operador  


|Operador|Descrição|Exemplo (produz verdadeiro)|
|--------|-----------|---------------------|
|==|Igual a|`"aBc" == "aBc"`|
|!=|Diferente de|`"abc" != "ABC"`|
|como|LHS contém uma correspondência para RHS|`"FabriKam" like "%Brik%"`|
|!like|LHS não contém uma correspondência para RHS|`"Fabrikam" !like "%xyz%"`|
|contém|RHS ocorre como uma subsequência de LHS|`"FabriKam" contains "BRik"`|
|!contains|RHS não ocorre em LHS|`"Fabrikam" !contains "xyz"`|
|startswith|RHS é uma subsequência inicial de LHS|`"Fabrikam" startswith "fab"`|
|!startswith|RHS não é uma subsequência inicial de LHS|`"Fabrikam" !startswith "kam"`|
|endswith|RHS é uma subsequência de fechamento de LHS|`"Fabrikam" endswith "Kam"`|
|!endswith|RHS não é uma subsequência de fechamento de LHS|`"Fabrikam" !endswith "brik"`|


### <a name="bkmk_cmpivot-summary"></a> Resumo da consulta

Selecione a guia **Resumo da Consulta** guia na parte inferior da janela do CMPivot. Esse status ajuda a identificar clientes que estão offline ou solucionar problemas de erros que podem ocorrer. Selecione um valor na coluna de contagem para abrir uma lista de dispositivos específicos com esse status. 

Por exemplo, selecione a contagem de dispositivos com um status de Falha. Veja a mensagem de erro específica e exporte uma lista desses dispositivos. Se o erro for que um cmdlet específico não é reconhecido, crie uma coleção da lista de dispositivos exportados para implantar uma atualização do Windows PowerShell.  

### <a name="cmpivot-audit-status-messages"></a>Mensagens de status de auditoria do CMPivot

Começando na versão 1810, quando você executa o CMPivot, uma mensagem de status de auditoria é criada com a **MessageID 40805**. Você pode exibir as mensagens de status acessando **Monitoramento** < **Status do Sistema** < **Consultas de Mensagens de Status**. Você pode executar **Todas as Mensagens de Status de Auditoria de um Usuário Específico**, **Todas as Mensagens de Status de Auditoria de um Site Específico** ou criar sua própria consulta de mensagem de status.

O formato a seguir é usado para a mensagem:

MessageId 40805: O usuário &lt;Nome-de-Usuário> executou o script &lt;GUID-do-Script> com o hash &lt;Hash-do-Script> na coleção &lt;ID-da-Coleção>.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 é o GUID do Script do CMPivot.
- O Hash do Script pode ser visto no arquivo scripts.log do cliente.
- Você também pode ver o hash armazenado na pontuação de script do cliente. O nome do arquivo no cliente é &lt;Script-Guid>_&lt;Script-Hash>.
    - Nome do arquivo de exemplo: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![Exemplo de mensagem de status de auditoria do CMPivot](media/cmpivot-audit-status-message.png)

## <a name="bkmk_cmpivot1902"></a> CMPivot começando na versão 1902
<!--3610960-->
Começando no Configuration Manager versão 1902, agora você pode executar o CMPivot do CAS (site de administração central) em uma hierarquia. O site primário ainda gerencia a comunicação com o cliente. Quando o CMPivot é executado do site de administração central, ele se comunica com o site primário pelo canal de assinatura de mensagem de alta velocidade. Essa comunicação não depende da replicação padrão do SQL entre sites.

Executar o CMPivot no CAS exigirá permissões adicionais quando o SQL ou o provedor não estiver no mesmo computador ou no caso da configuração SQL Always On. Com essas configurações remotas, você tem um "cenário de salto duplo" para o CMPivot.

Para fazer o CMPivot funcionar no CAS nesse “cenário de salto duplo”, você pode definir a delegação restrita. Para entender as implicações de segurança dessa configuração, leia o artigo [Delegação restrita de Kerberos](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview). Se você tiver mais de uma configuração remota, como SQL ou o Provedor do SCCM, sendo colocada com o CAS ou não, talvez precise de uma combinação de configurações de permissão. Abaixo estão as etapas que você precisa executar:

### <a name="cas-has-a-remote-sql-server"></a>O CAS tem um SQL Server remoto

1. Vá para o servidor SQL de cada site primário.
   1. Adicione o SQL Server remoto e o servidor do site do CAS ao grupo [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess).
   ![Grupo Configmgr_DviewAccess no SQL Server do site primário](media/cmpivot-dviewaccess-group.png)
1. Vá para Usuários e Computadores do Active Directory.
   1. Para cada servidor do site primário, clique com botão direito do mouse e selecione **Propriedades**.
      1. Na guia Delegação, escolha a terceira opção, **Confiar no computador para delegação apenas a serviços especificados**. 
      1. Escolha **Usar apenas Kerberos**.
      1. Adicione serviço do SQL Server do CAS com a porta e a instância.
      1. Verifique se essas alterações se alinham à política de segurança da sua empresa!
   1. Para o site do CAS, clique com o botão direito do mouse e selecione **Propriedades**.
      1. Na guia Delegação, escolha a terceira opção, **Confiar no computador para delegação apenas a serviços especificados**. 
      1. Escolha **Usar apenas Kerberos**.
      1. Adicione o serviço do SQL Server de cada site primário com a porta e a instância.
      1. Verifique se essas alterações se alinham à política de segurança da sua empresa!

   ![Exemplo de delegação do CMPivot AD de salto duplo](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>O CAS tem um provedor remoto

1. Vá para o servidor SQL de cada site primário.
   1. Adicione a conta do computador do provedor e o servidor do site do CAS ao grupo [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess).
1. Vá para Usuários e Computadores do Active Directory.
   1. Selecione o computador do provedor do CAS, clique com botão direito do mouse e selecione **Propriedades**.
      1. Na guia Delegação, escolha a terceira opção, **Confiar no computador para delegação apenas a serviços especificados**. 
      1. Escolha **Usar apenas Kerberos**.
      1. Adicione o serviço do SQL Server de cada site primário com a porta e a instância.
      1. Verifique se essas alterações se alinham à política de segurança da sua empresa!
   1. Selecione o servidor do site de CAS, clique com botão direito do mouse e selecione **Propriedades**.
      1. Na guia Delegação, escolha a terceira opção, **Confiar no computador para delegação apenas a serviços especificados**. 
      1. Escolha **Usar apenas Kerberos**.
      1. Adicione o serviço do SQL Server de cada site primário com a porta e a instância.
      1. Verifique se essas alterações se alinham à política de segurança da sua empresa!
1. Reinicie o computador do provedor remoto do CAS.

### <a name="sql-always-on"></a>SQL Always On

1. Vá para o servidor SQL de cada site primário.
   1. Adicione o servidor do site do CAS ao grupo [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess).
1. Vá para Usuários e Computadores do Active Directory.
   1. Para cada servidor do site primário, clique com botão direito do mouse e selecione **Propriedades**.
      1. Na guia Delegação, escolha a terceira opção, **Confiar no computador para delegação apenas a serviços especificados**. 
      1. Escolha **Usar apenas Kerberos**.
      1. Adicione as contas de serviço do SQL Server do CAS para os nós do SQL com a porta e a instância.
      1. Verifique se essas alterações se alinham à política de segurança da sua empresa!
   1. Selecione o servidor do site de CAS, clique com botão direito do mouse e selecione **Propriedades**.
      1. Na guia Delegação, escolha a terceira opção, **Confiar no computador para delegação apenas a serviços especificados**. 
      1. Escolha **Usar apenas Kerberos**.
      1. Adicione o serviço do SQL Server de cada site primário com a porta e a instância.
      1. Verifique se essas alterações se alinham à política de segurança da sua empresa!
1. Verifique se o [SPN foi publicado](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs) para o nome do ouvinte do SQL do CAS e para cada nome de ouvinte do SQL primário.
1. Reinicie os servidores SQL primários.
1. Reinicie o servidor do site do CAS e os servidores SQL do CAS.


## <a name="inside-cmpivot"></a>Dentro do CMPivot

O CMPivot envia consultas para os clientes que usam o "canal rápido" do Configuration Manager. Esse canal de comunicação do servidor para o cliente também é usado por outros recursos, como ações de notificação do cliente, status do cliente e Endpoint Protection. Os clientes retornarão os resultados por meio do sistema de mensagens de estado igualmente rápido. As mensagens de estado são armazenadas temporariamente no banco de dados. Para obter mais informações sobre as portas usadas para a notificação do cliente, confira o artigo [Portas](/sccm/core/plan-design/hierarchy/ports#BKMK_PortsClient-MP).

As consultas e os resultados são todos somente texto. As entidades **InstallSoftware** e **Processo** retornam alguns dos maiores conjuntos de resultados. Durante o teste de desempenho, o maior tamanho do arquivo de mensagem de estado de um cliente para essas consultas foi menor que **1 KB**. Dimensionado para um ambiente grande com 50 mil clientes ativos, essa consulta única geraria menos de 50 MB de dados pela rede. Todos os itens na página de boas-vindas que estiverem sublinhados retornarão menos de mil informações por cliente.

![Exemplo de entidades sublinhadas do CMPivot](media/cmpivot-underlined-entities.png)

Começando no Configuration Manager 1810, o CMPivot pode consultar dados de inventário de hardware, incluindo as classes de inventário de hardware estendido. Essas novas entidades (entidades não sublinhadas na página de boas-vindas) podem retornar conjuntos de dados muito maiores, dependendo da quantidade de dados definida para uma propriedade de inventário de hardware específica. Por exemplo, a entidade "InstalledExecutable" pode retornar vários MB de dados por cliente, dependendo dos dados específicos sendo consultados. Preste atenção no desempenho e na escalabilidade dos seus sistemas ao retornar conjuntos de dados de inventário de hardware maiores de coleções maiores usando o CMPivot.

Uma consulta atinge o tempo limite após uma hora. Por exemplo, uma coleção tem 500 dispositivos e 450 dos clientes estão online no momento. Esses dispositivos ativos recebem a consulta e retornam os resultados quase imediatamente. Se você deixar a janela CMPivot aberta, conforme os outros 50 clientes ficarem online, eles também receberão a consulta e retornarão resultados. 

## <a name="log-files"></a>Arquivos de log

 As interações do CMPivot são registradas nos seguintes arquivos de log:

**No lado do servidor:**
- SmsProv.log
- BgbServer.log
- StateSys.log

**No lado do cliente:**
 - CCMNotificationAgent.log
 - Scripts.log
 - StateMessage.log

Para obter mais informações, confira [Arquivos de log](/sccm/core/plan-design/hierarchy/log-files) e [Solução de problemas do CMPivot](/sccm/core/servers/manage/cmpivot-tsg).

## <a name="next-steps"></a>Próximas etapas
 
[Solução de problemas do CMPivot](/sccm/core/servers/manage/cmpivot-tsg)

[Criar e executar scripts do PowerShell](/sccm/apps/deploy-use/create-deploy-scripts)


