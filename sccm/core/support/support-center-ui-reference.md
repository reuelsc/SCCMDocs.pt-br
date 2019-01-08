---
title: Referência de interface do usuário do Centro de Suporte
titleSuffix: Configuration Manager
description: Saiba como usar as ferramentas do Centro de Suporte.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df7d443a9f611278296c729949d5dfb764a43e9e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420770"
---
# <a name="support-center-user-interface-reference"></a>Referência de interface do usuário do Centro de Suporte

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo é uma referência que descreve a interface do usuário (IU) das ferramentas do Centro de Suporte:
- Centro de Suporte
- Visualizador de Log do Centro de Suporte
- Visualizador do Centro de Suporte



## <a name="support-center-reference"></a>Referência do Centro de Suporte

Esta seção descreve a interface do usuário para a ferramenta **Centro de Suporte**. 
- [Menu Janela](#bkmk_support-window)  
- [Guia Início](#bkmk_support-home)  
- [Guia Cliente](#bkmk_support-client)  
- [Guia Política](#bkmk_support-policy)  
- [Guia Conteúdo](#bkmk_support-content)  
- [Guia Inventário](#bkmk_support-inventory)  
- [Guia Solução de Problemas](#bkmk_support-troubleshoot)  
- [Guia Logs](#bkmk_support-logs)  


### <a name="bkmk_support-window"></a> Menu Janela

No canto superior esquerdo da janela do Centro de Suporte, selecione a seta na caixa azul para abrir esse menu.

#### <a name="local-machine-connection"></a>Conexão da Máquina Local
O Centro de Suporte coleta arquivos de log e executa a solução de problemas no cliente que está executando o Centro de Suporte.

#### <a name="remote-connection"></a>Conexão Remota
Estabelece uma conexão remota com outro cliente do Configuration Manager. Depois de conectar, o Centro de Suporte coleta arquivos de log e executa a solução de problemas no cliente ao qual ele está conectado.

#### <a name="about"></a>Sobre o
Fornece informações sobre o Centro de Suporte.

#### <a name="options"></a>Opções
Na caixa de diálogo **Opções** , você pode:
- Reduzir a movimentação de elementos animados da interface do usuário  
- Alterar a localização padrão para salvar arquivos do pacote de dados  
- Alterar a localização dos arquivos temporários    
- Redefinir os avisos. Novamente, as mensagens de aviso que você suprimiu antes reaparecem quando disparadas.  
- Redefinir o caminho de arquivo temporário para o padrão, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

#### <a name="exit"></a>Sair
Fechar Centro de Suporte.



### <a name="bkmk_support-home"></a> Guia Início

#### <a name="collect-selected-data"></a>Coletar dados selecionados
O Centro de Suporte coleta informações do cliente do Configuration Manager. Por padrão, ele coleta os seguintes tipos:
- Arquivos de log
- Coletor de Configuração do Cliente
- Sistema operacional

Para coletar outros tipos de informação, marque a caixa de seleção ao lado do nome para esse tipo.

Selecione na lista suspensa na parte inferior do botão **Coletar dados selecionados** na faixa de opções e, em seguida, selecione **Coletar todos os dados**. Essa ação coleta o conjunto completo de dados de estado do cliente.

Enquanto o Centro de Suporte estiver coletando dados, selecione **Cancelar coleta** para interrompê-la.

#### <a name="data-types"></a>Tipos de dados
Quando você marca a caixa de seleção para uma opção, o Centro de Suporte coleta esse tipo de dados na próxima vez que você seleciona **Coletar dados selecionados**. Os seguintes tipos estão disponíveis:  

- **Arquivos de log**: Arquivos de log do cliente, incluindo os logs de instalação  

- **Política**: coleção de políticas do cliente  

- **Certificados**: informações de chave pública para certificados do cliente. O Centro de Suporte não coleta as chaves privadas do certificado.  

- **Coletor de configuração do cliente**: informações de cliente do Configuration Manager. Não é possível desabilitar esse tipo de dados.  

- **Registro de cliente**: coleta informações de configuração de cliente do Registro. O Centro de Suporte coleta apenas as informações de Registro do Configuration Manager.  

- **WMI cliente**: informações de configuração de cliente da WMI. O Centro de Suporte não coleta política do cliente.  

- **Solução de problemas**: solução de problemas em tempo real para ajudar a diagnosticar problemas comuns de cliente do Active Directory, pontos de gerenciamento, rede, atribuições de política e registro.  

    > [!NOTE]  
    > Não há suporte para esse tipo de dados quando você faz uma conexão remota com outro cliente.  

- **Despejos de depuração**: execute um despejo de depuração do cliente e dos processos relacionados. Despejos de depuração podem ser grandes. Somente habilite essa opção ao realizar a solução de problemas de desempenho do cliente.  

    > [!WARNING]  
    > Coletar despejos de depuração fará com que os pacotes de dados tornem-se muito grandes (em alguns casos, várias centenas de MB).  
    >  
    > Os despejos de depuração podem conter informações confidenciais, como senhas, segredos de criptografia ou dados do usuário. Os despejos de depuração somente devem ser coletados por recomendação da equipe do Suporte da Microsoft. Os pacotes de dados que contêm despejos de depuração devem ser tratados com cuidado para protegê-los contra acesso não autorizado.  
    >  
    > Não há suporte para esse tipo de dados quando você faz uma conexão remota com outro cliente.  

- **Sistema operacional**: coleta informações de configuração sobre o computador local. Esses dados incluem informações sobre a instalação do Windows, adaptadores de rede e configuração de serviço do sistema. Não é possível desabilitar esse tipo de dados.  



### <a name="bkmk_support-client"></a> Guia Cliente

#### <a name="load-or-refresh"></a>Carregar ou Atualizar
O Centro de Suporte carrega ou atualiza os detalhes do cliente do Configuration Manager.

#### <a name="control-client-agent-service"></a>Serviço de agente de cliente de controle
Execute uma das ações a seguir no serviço do agente cliente do Configuration Manager (ccmexec) no cliente conectado:  

- **Reiniciar cliente**  

    > [!IMPORTANT]  
    > Se o serviço do agente cliente não for reiniciado com êxito, o cliente não poderá ser gerenciado pelo Configuration Manager até que o serviço seja iniciado.  

- **Iniciar cliente**  

- **Parar o cliente**  

    > [!IMPORTANT]  
    > O cliente não pode ser gerenciado pelo Configuration Manager até que o serviço seja iniciado.  

#### <a name="properties"></a>Propriedades
Ao carregar detalhes do cliente, o Centro de Suporte mostra as propriedades a seguir:  

- **ID do cliente**: um identificador exclusivo que o Configuration Manager usa para identificar o cliente  

- **ID de hardware**: um identificador exclusivo que o Configuration Manager usa para identificar o hardware do cliente  

- **Aprovado**: indica se o cliente está aprovado no Configuration Manager  

- **Estado do registro**: indica se o cliente está registrado no Configuration Manager  

- **Para a Internet**: indica se o cliente está na Internet  

- **Versão**: o número de versão do cliente do Configuration Manager instalado  

- **Código do site**: o código do site primário ao qual o cliente é atribuído  

- **MP atribuída**: o FQDN (nome de domínio totalmente qualificado) do ponto de gerenciamento atribuído ao cliente no momento  

- **MP residente**: o FQDN do ponto de gerenciamento residente  

- **MP do proxy**: o nome do host ou FQDN do ponto de gerenciamento de proxy (se houver)  

- **Código do site do proxy**: O código do site para o site secundário (se houver)  

- **Estado do proxy**: o estado do ponto de gerenciamento de proxy do cliente do Configuration Manager. Por exemplo, **Ativo** ou **Pendente**.  



### <a name="bkmk_support-policy"></a> Guia Política

Use as ações nessa guia, em vez da ferramenta [PolicySpy](/sccm/core/support/policy-spy) antiga.

#### <a name="load-policy"></a>Carregar política
Esta opção varia conforme o modo de exibição:

- **Carregar política real**: selecione **Real** no grupo Exibição e, em seguida, selecione essa opção no grupo Política. O Centro de Suporte carregará a política do cliente que você selecionou no momento.  

- **Carregar política solicitada**: selecione **Solicitado** no grupo Exibição e, em seguida, selecione essa opção no grupo Política. O Centro de Suporte carregará a política de cliente solicitada do cliente.  

- **Carregar política padrão**: selecione **Padrão** no grupo Exibição e, em seguida, selecione essa opção no grupo Política. O Centro de Suporte carregará a política padrão para esse cliente.  

Selecione a lista suspensa na parte inferior deste botão para obter opções adicionais:

- **Carregar ou atualizar tudo**: carrega ou atualiza a políticas real, solicitada e padrão ao mesmo tempo.  

#### <a name="actual-view"></a>Exibição real
Abre a exibição de política real

#### <a name="requested-view"></a>Exibição solicitada
Abre a exibição de política solicitada

#### <a name="default-view"></a>Exibição padrão
Abre a exibição de política padrão. (Essa política é o que os dispositivos obtêm quando você instala o cliente do Configuration Manager.)

#### <a name="request-and-evaluate-policy"></a>Solicitar e avaliar política
O Centro de Suporte solicita a política do cliente do ponto de gerenciamento e, em seguida, avalia essa política no cliente.

Selecione a lista suspensa na parte inferior deste botão para obter opções adicionais:  

- **Política de solicitação**: o Centro de Suporte solicita a política do cliente do ponto de gerenciamento.  

- **Avaliar política**: o Centro de Suporte avalia a política do cliente no cliente.  

- **Redefinir política para o padrão**: o Centro de Suporte informa ao cliente do Configuration Manager que ele deve reaplicar a política padrão. Ele remove todas as políticas de computador e de usuário no cliente.  

#### <a name="listen-for-policy-events"></a>Escutar eventos de política
O Centro de Suporte escuta eventos de política. Selecione esta opção novamente para desabilitar a escuta para eventos de política. Para exibir **Eventos de política**, selecione a seta na parte inferior dessa guia. 

#### <a name="clear-events"></a>Limpar eventos
O Centro de Suporte limpa os eventos de política.



### <a name="bkmk_support-content"></a> Guia Conteúdo

Exibir o conteúdo no cliente, incluindo conteúdo armazenado em cache. Monitore o progresso das implantações de aplicativos e da atualização de software. 

#### <a name="load-or-refresh"></a>Carregar ou Atualizar
*Aplica-se às exibições de Conteúdo e Cache*

O Centro de Suporte carrega ou atualiza a lista de conteúdo que está no cliente no momento.

#### <a name="invoke-trigger"></a>Invocar gatilho
Os seguintes itens nesse menu solicitam uma ação do cliente relacionada ao conteúdo:  

- **Serviços de Localização**  

    - **Atualizar locais de conteúdo**: Atualiza os pontos de distribuição usados por todos os downloads de conteúdo ativos.  

    - **Atualizar pontos de gerenciamento**: Atualiza a lista interna de pontos de gerenciamento usados pelo cliente.  

    - **Atingir tempo limite de solicitações de conteúdo**: se houver solicitações de localização de conteúdo em execução por muito tempo, essa ação interromperá a solicitação.  

  - **Avaliação de implantação de aplicativo**: Inicia uma tarefa que avalia os aplicativos implantados.  

  - **Avaliação de implantação de atualizações de software**: Inicia uma tarefa que avalia as atualizações de software implantadas.  

  - **Verificação de origem de atualizações de software**: Inicia uma tarefa que verifica os locais de origem da atualização.  

  - **Atualização de lista de origem do Windows Installer**: Inicia uma tarefa que atualiza o local de origem para instalações do Windows Installer (MSI).  

#### <a name="content-view"></a>Exibição de conteúdo
Veja aplicativos, pacotes e atualizações que são carregados no cliente. Ao selecionar um aplicativo, pacote ou a atualização, você pode exibir detalhes deste conteúdo. Para alguns aplicativos, você também pode fazer as seguintes ações:  

 - **Atualizar**: atualizar a exibição Detalhes  

 - **Verificar ou baixar**: verificar se um aplicativo está disponível para download  

 - **Instalar**: instalar o aplicativo  

 - **Desinstalar**: Desinstalar o aplicativo  

#### <a name="cache-view"></a>Exibição de cache
Exiba a configuração de cache do cliente e os detalhes sobre o conteúdo em cache. Quando você conecta o Centro de suporte a um cliente local, também pode fazer as seguintes ações:  

 - Para alterar a localização do cache, selecione **Alterar** ao lado do campo **Localização do cache**.  

 - Para ajustar o tamanho do cache, selecione **Alterar** ao lado do campo **Tamanho do cache**.  

 - Para limpar o cache do cliente, selecione **Limpar** ao lado do campo **Cache em uso**.  

Essa exibição mostra as propriedades a seguir:  

 - **Localização**: a localização de cada pasta de cache. Selecione o link para abrir a pasta no Windows Explorer.   
 - **ID de Conteúdo**  
 - **ID de cache**  
 - **Tamanho**  
 - **Última referência**: essa propriedade é a data quando o cliente leu ou gravou pela última vez neste item no cache.  

#### <a name="monitoring-view"></a>Exibição de Monitoramento
Selecione **Monitor** para exibir o progresso ativo da atualização de software e de implantações de atualização de aplicativo. Esta exibição mostra as mensagens de estado geradas no aplicativo e mensagens de evento WMI de atualizações de software.

Para cada evento, a exibição mostra as propriedades a seguir:  

 - **Tempo**: a hora em que o cliente gerou o evento  
 - **Tipo de tópico**: O tipo de mensagem de estado  
 - **ID do tópico**: ID da mensagem de estado, usada para mapear eventos nos arquivos de log  
 - **Tipo de ID do tópico**: o subtipo da mensagem de estado  
 - **ID de estado**: o resultado da ação que você está monitorando  
 - **Detalhes** e **Dados de evento**: mais informações sobre as mensagens de estado mostradas nesta exibição. Os detalhes do estado às vezes podem estar em branco.  



### <a name="bkmk_support-inventory"></a> Guia Inventário

#### <a name="load-or-refresh"></a>Carregar ou Atualizar
O Centro de Suporte carrega ou atualiza a lista de inventário do cliente para a exibição selecionada no momento.

#### <a name="invoke-trigger"></a>Invocar gatilho

> [!Note]  
> Para tarefas além de **Ciclo de relatório de medição de Software**:  
> - Se você solicitar a tarefa quando outra tarefa de inventário já estiver em execução, o cliente colocará a nova tarefa para ser executada após a conclusão da tarefa atual e de outras tarefas na fila.  
> - Acompanhe o progresso da tarefa no **InventoryAgent.log**.  

Os seguintes itens nesse menu solicitam uma ação do cliente relacionada ao inventário:  

 - **Ciclo de coleta de dados de descoberta (pulsação)**: dispara a tarefa do cliente usada para coletar informações de descoberta do dispositivo  

 - **Ciclo de coleta de arquivos**: dispara a tarefa de cliente usada para coletar arquivos locais  

 - **Ciclo de inventário de hardware**: dispara a tarefa do cliente usada para coletar dados de inventário de hardware  

 - **Ciclo de coleta de IDMIF**: dispara a tarefa do cliente usada para coletar dados IDMIF  

 - **Ciclo de inventário de software**: dispara a tarefa do cliente usada para coletar dados de inventário de software  

 - **Ciclo de relatório de medição de software**: Dispara a tarefa do cliente usada para criar um relatório de medição de software e enviá-lo para o ponto de gerenciamento. Acompanhe o progresso dessa tarefa no **SWMTRReportGen.log**.

 - **Enviar mensagens de estado não enviadas na fila**: Dispara a tarefa do cliente para liberar a fila de mensagens de estado.

 - **Advanced**  
     - **Ciclo de inventário de hardware (ressincronização completa)**  
     - **Ciclo de inventário de software (ressincronização completa)**  


#### <a name="views"></a>Exibições
Se um recurso não estiver habilitado, o modo de exibição não exibirá nenhum dado. 

- **Status**: mostrar os conjuntos de dados de inventário coletados pelo cliente  

- **DDR**: informações sobre os dados de descoberta do cliente coletados do cliente  

- **HINV**: informações sobre os dados de inventário de hardware coletados do cliente  

- **SINV**: informações sobre os dados de inventário de software coletados do cliente  

- **Coleta de arquivos**: informações sobre os arquivos coletados do cliente  

- **IDMIF**: informações sobre os dados IDMIF e NOIDMIF coletados do cliente  

- **Medição**: informações sobre os dados de medição de software coletados do cliente  



### <a name="bkmk_support-troubleshoot"></a> Guia Solução de Problemas

Solucione alguns dos problemas mais comuns com clientes do Configuration Manager:  
- Problemas com o Active Directory  
- Rede do Windows  
- Gerenciador de Configurações   
    - Pontos de gerenciamento  
    - Atribuição de política  
    - Registro  


> [!NOTE]  
> Essa guia não está disponível quando você se conecta a um cliente remoto do Configuration Manager.


#### <a name="start"></a>Início
Abre a solução de problemas do cliente

- **Active Directory**: consulta o Active Directory para obter informações do site do Configuration Manager publicadas  
- **MPCERTIFICATE**: Obtém certificados do ponto de gerenciamento  
- **MPLIST**: Obtém uma lista de pontos de gerenciamento  
- **MPKEYINFORMATION**: obtém informações de chave de criptografia do ponto de gerenciamento  
- **Rede**: Soluciona problemas com as redes  
- **Atribuições de política**: Recupera as atribuições de políticas  
- **Registro**: verifica se o cliente está registrado no site  

#### <a name="view-selected-log"></a>Exibir o log selecionado
Depois de selecionar uma linha na guia Solução de problemas, selecione essa ação para exibir o arquivo de log.

#### <a name="keep-previous-results"></a>Manter resultados anteriores
Se você tiver solucionado problemas do cliente e desejar tentar novamente a solução de problemas, escolha esta opção para manter os resultados da sua primeira tentativa. Caso contrário, o Centro de Suporte substituirá arquivos de log de solução de problemas anteriores.



### <a name="bkmk_support-logs"></a> Guia Logs

Esta seção lista os itens na guia **Logs** da ferramenta do Centro de Suporte. 

Essa guia é quase idêntica à ferramenta **Visualizador de Log**. A ferramenta **Visualizador de Log** não inclui os recursos **Configurar de registro em log do cliente** e **Registrar grupos em log** descritos nesta seção. A seção [Referência do Visualizador de Log do Centro de Suporte](#bkmk_log-viewer) fornece detalhes sobre as outras opções disponíveis nessa guia.

#### <a name="configure-client-logging"></a>Configurar Log do Cliente

Defina as seguintes opções: 
- **Nível de log do cliente**: detalhamento do log e tamanho do arquivo  
- **Contagem máxima de arquivos**: permita mais de um arquivo de log de um determinado tipo  
- **Tamanho máximo do arquivo**: o tamanho em bytes de qualquer arquivo de log antes que o cliente crie um log  

> [!NOTE]  
> Se você definir esses valores para um nível muito baixo, o cliente não poderá registrar nenhuma informação útil. Se você definir esses valores para um nível muito alto, os logs do cliente poderão consumir grandes quantidades de armazenamento.  

#### <a name="log-groups"></a>Grupos de log

Em vez de selecionar manualmente os arquivos de log usando o botão **Abrir logs**, use essa lista suspensa para abrir todos os arquivos de log associados com as seguintes áreas de recurso: 
- **Gerenciamento de Configuração Desejada**
- **Inventário**
- **Distribuição de software**
- **Atualizações de software**
- **Gerenciamento de aplicativo**
- **Política**
- **Registro do Cliente**
- **Implantação do sistema operacional**


## <a name="bkmk_log-viewer"></a> Referência do Visualizador de Log do Centro de Suporte

Esta seção descreve a interface do usuário para a ferramenta **Visualizador de Log do Centro de Suporte**. 

- [Menu Janela](#bkmk_log-window)  
- [Guia Início](#bkmk_log-home)  

A ferramenta **Visualizador de Log** é quase idêntica à guia **Logs** do **Centro de Suporte**. A ferramenta **Visualizador de Log** não inclui as opções para **Configurar registro em log do cliente** e **Registrar grupos em log**.


### <a name="bkmk_log-window"></a> Menu Janela

No canto superior esquerdo da janela do Visualizador de Log do Centro de Suporte, selecione a seta na caixa azul para abrir esse menu.

#### <a name="open-logs"></a>Abrir logs
Navegue até a localização dos arquivos de log para abrir. 

#### <a name="options"></a>Opções
Na caixa de diálogo **Opções** , você pode:
- Reduzir a movimentação de elementos animados da interface do usuário  
- Registre o Visualizador de Log como o aplicativo padrão para arquivos de log com as extensões de arquivo .log e .lo_  
- Redefinir os avisos. Novamente, as mensagens de aviso que você suprimiu antes reaparecem quando disparadas.  

#### <a name="about"></a>Sobre o
Exibe informações sobre o Visualizador de Log do Centro de Suporte

#### <a name="close"></a>Fechar
Fecha o Visualizador de Log do Centro de Suporte


### <a name="bkmk_log-home"></a> Guia Início

#### <a name="open-logs"></a>Abrir logs 
O Centro de Suporte solicitará que você selecione um ou mais arquivos de log para abrir.

Selecione a lista suspensa na parte inferior do botão **Abrir logs** na faixa de opções e selecione uma das seguintes opções adicionais: 
- **Abrir logs na exibição atual**: abre os arquivos de log selecionados na exibição atual  
- **Abrir logs em uma nova janela**: abre os arquivos de log selecionados em uma nova janela **Visualizador de Log**  

#### <a name="close-and-clear-logs"></a>Fechar e apagar logs
Fecha quaisquer arquivos de log abertos. Também apagar todas as entradas de arquivo de log exibidas na janela. O Centro de Suporte não exibirá essas entradas no futuro.

Selecione a lista suspensa na parte inferior do botão **Fechar e limpar logs** na faixa de opções e selecione uma das seguintes opções adicionais: 
- **Limpar todas as entradas**: Apagar todas as entradas de arquivo de log exibidas na janela. O Centro de Suporte não exibirá essas entradas no futuro.  
- **Fechar todos os logs**: Fecha os arquivos de log abertos  

#### <a name="find"></a>Localizar
Abre a caixa de diálogo **Localizar**. Insira uma cadeia de caracteres a ser pesquisada. Para evitar a correspondências de cadeias de caracteres curtas em outras cadeias de caracteres, você pode optar por combinar palavras inteiras. Você também pode optar por fazer uma correspondência que diferencie maiúsculas de minúsculas para a cadeia de caracteres.

#### <a name="find-next"></a>Localizar próximo
Depois de localizar uma correspondência para a cadeia de caracteres que você está pesquisando, essa opção levará você para a próxima correspondência.

#### <a name="find-previous"></a>Localizar anterior
Depois de localizar duas ou mais correspondências para a cadeia de caracteres que você está procurando, essa opção levará você à correspondência anterior.

#### <a name="options"></a>Opções

- **Atualização dinâmica**: monitore as alterações em um arquivo de log aberto. Esse recurso não funciona quando vários arquivos de log estão abertos. Essa opção é habilitada por padrão.  

- **Rolagem automática**: se você também escolher a opção **Atualização dinâmica**, essa opção rolará automaticamente a exibição do log para mostrar as entradas adicionadas recentemente. Esse recurso não funciona quando vários arquivos de log estão abertos. Essa opção é habilitada por padrão.  

- **Mostrar detalhes**: quando você seleciona uma mensagem de arquivo de log, a parte inferior da guia **Logs** exibe os detalhes da mensagem do arquivo de log. Essa opção é habilitada por padrão.  

- **Filtro rápido**: filtre as mensagens do arquivo de log em todos os arquivos de log abertos para localizar uma cadeia de caracteres específica. Você pode filtrar por texto de log, nome do componente e ID do thread. Para encontrar mensagens de log semelhantes, clique com o botão direito do mouse em uma mensagem de log e selecione **Filtro rápido** no texto do log.  

- **Quebrar o texto do log**: Quebre mensagens longas e multilinhas para ajustá-las a uma única coluna. Esse comportamento torna mais fácil ler essas mensagens. Essa opção é habilitada por padrão.  

- **Exibição de entrada de log bruta**: exibe as linhas de log não processadas.  

- **Filtros avançados**: abre a caixa de diálogo **Filtros avançados**. Para obter mais informações, confira [Filtros de arquivo de log avançados](#bkmk_adv-filters).  

- **Links de código de erro**: os códigos de erro no texto de log são realçados e clicáveis. Essa opção é habilitada por padrão.  

#### <a name="error-lookup"></a>Pesquisa de erro
Insira um código de erro para procurá-lo nos arquivos de log abertos no momento. Use os seguintes formatos de código de erro:
 - **inteiro de 32 bits (com sinal)**: Por exemplo, `-2147024891`  
 - **inteiro de 32 bits (sem sinal)**: Por exemplo, `2147942405`  
 - **hexadecimal de 32 bits**: Por exemplo, `0x80070005`  

#### <a name="decode-certificate"></a>Decodificar certificado
Na caixa de diálogo **Decodificar certificado**, cole o valor de certificado serializado para qualquer certificado no cliente. Encontre esse valor no Registro, nos arquivos de log ou no WMI. Selecione **Processo** para exibir informações gerais e detalhes no certificado. Essas informações incluem o caminho de certificação. Selecione **Exportar** para exportar o certificado como um arquivo **.cer**.



## <a name="bkmk_adv-filters"></a> Filtros avançados de arquivo de log

Filtros de arquivo de log avançados permitem incluir, excluir ou realçar cadeias de caracteres específicas. Essas cadeias de caracteres podem ocorrer em um arquivo de log ou grupo de arquivo de log ao examinar as entradas de arquivo de log. Use pesquisas com curinga ao criar um filtro. Quando você tiver uma combinação útil de filtros, salve-a como um *conjunto de filtros*. 

Filtros de arquivo de log avançados substituem os filtros rápidos. Use os dois juntos, mas filtros rápidos se aplicam somente aos dados de log exibidos. Filtros avançados determinam que dados são inicialmente exibidos antes de qualquer um a que ele aplica filtros rápidos.

Na caixa de diálogo Filtros avançados, você pode criar conjuntos de filtro complexos. Esses conjuntos de filtros pesquisam cadeias de caracteres entre vários componentes de arquivo de log. Esses componentes incluem mensagens, threads, níveis de log e componentes. Um conjunto de filtros contém várias instruções de filtro que você pode usar para incluir, excluir ou realçar mensagens de arquivo de log. Um filtro define uma coluna do arquivo de log na qual pesquisar, um operador e um valor. O valor pode conter expressões regulares, como o caractere *curinga* `*`.


### <a name="add-a-filter"></a>Adicionar um filtro

1. Na janela **Visualizador de Log** ou na guia **Logs** do Centro de Suporte, selecione **Filtros avançados**.  

2. Na caixa de diálogo Filtros avançados, selecione **Adicionar**. Em seguida, selecione uma destas opções para agir em entradas de log que correspondem ao seu filtro:  
    - **Incluir**  
    - **Excluir**  
    - **Destacar**  

3. Na caixa de diálogo **Configuração de filtro avançado**, escolha uma coluna e um operador:  

    - **Coluna**: escolha onde procurar cadeias de caracteres que correspondam ao seu filtro:  

         - **Texto de log**: pesquisar dentro do texto de um arquivo de log  

         - **Gravidade do log**: pesquise logs com um nível de gravidade específico. Defina esses níveis de gravidade no campo **Valor**.  

         - **Componente**: pesquise um componente específico por nome  

         - **ID do thread**: pesquise mensagens de log com uma ID de thread específica  

         - **Arquivo de origem**: pesquise mensagens de log que ocorrem em um arquivo de log específico  

    - **Operador**: escolha um operador para seu filtro  

4. Insira um valor para filtrar no campo **Valor**. Se o valor contiver expressões regulares, selecione **Habilitar a correspondência da expressão regular**.  


### <a name="manage-filter-sets"></a>Gerenciar conjuntos de filtros

  - Para editar um filtro, selecione o filtro e, em seguida, selecione **Editar**.  

  - Para excluir um filtro, selecione o filtro e, em seguida, selecione **Excluir**.  

  - Para limpar todos os filtros, selecione **Limpar**.  

  - Para salvar o conjunto atual de filtro, selecione **Salvar filtros**. Em seguida, salve o filtro definido como um arquivo **.filterset**.  

  - Para carregar um conjunto de filtros salvo, selecione **Carregar filtros**. Em seguida, navegue até um arquivo **.filterset** salvo anteriormente.  



## <a name="bkmk_viewer"></a> Referência de Visualizador do Centro de Suporte

Esta seção descreve a interface do usuário (IU) da ferramenta do **Visualizador do Centro de Suporte** do Configuration Manager. As guias disponíveis variam de acordo com o conteúdo do pacote de solução de problemas. O [menu Janela](#bkmk_viewer-window) e a [guia Início](#bkmk_viewer-home) são exibidos por padrão.
- [Menu Janela](#bkmk_viewer-window)
- [Guia Início](#bkmk_viewer-home)
- [Guia Configuração](#bkmk_viewer-config)
- [Guia Logs](#bkmk_viewer-logs)
- [Guia de despejos de depuração](#bkmk_viewer-debug)
- [Guia WMI](#bkmk_viewer-wmi)
- [Guia Registro](#bkmk_viewer-registry)
- [Guia Política](#bkmk_viewer-policy)
- [Guia Certificados](#bkmk_viewer-certs)
- [Guia Solução de Problemas](#bkmk_viewer-troubleshoot)


### <a name="bkmk_viewer-window"></a> Menu Janela

No canto superior esquerdo da janela do Visualizador do Centro de Suporte, selecione a seta na caixa azul para abrir esse menu.

#### <a name="open-bundle"></a>Abrir pacote
Navegue até a localização de um pacote de dados criado pelo Centro de Suporte.

#### <a name="about"></a>Sobre o
Exibe informações sobre o Visualizador do Centro de Suporte.

#### <a name="options"></a>Opções
Na caixa de diálogo **Opções** , você pode:
- Reduzir a movimentação de elementos animados da interface do usuário  
- Alterar a localização dos arquivos temporários    
- Redefinir os avisos. Novamente, as mensagens de aviso que você suprimiu antes reaparecem quando disparadas.  
- Redefinir o caminho de arquivo temporário para o padrão, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`  


#### <a name="exit"></a>Sair
Sai do Visualizador do Centro de Suporte


### <a name="bkmk_viewer-home"></a> Guia Início

#### <a name="open-bundle"></a>Abrir pacote
Navegue até a localização de um pacote de dados criado pelo Centro de Suporte.

#### <a name="open-log-file"></a>Abrir arquivo de log
Selecione um ou mais arquivos de log para abrir.

#### <a name="decode-certificate"></a>Decodificar certificado
Na caixa de diálogo **Decodificar certificado**, cole o valor de certificado serializado para qualquer certificado no cliente. Encontre esse valor no Registro, nos arquivos de log ou no WMI. Selecione **Processo** para exibir informações gerais e detalhes no certificado. Essas informações incluem o caminho de certificação. Selecione **Exportar** para exportar o certificado como um arquivo **.cer**.


### <a name="bkmk_viewer-config"></a> Guia Configuração

A guia **Configuração** da ferramenta do Visualizador do Centro de Suporte fornece as seguintes exibições usando dados recuperados de provedores de WMI:

#### <a name="client"></a>Cliente
Essa exibição mostra as mesmas informações que aparecem na guia **Cliente** do Centro de Suporte.

#### <a name="operating-system"></a>Sistema operacional
Detalhes do sistema operacional do cliente. Ele usa a classe [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem).

#### <a name="computer"></a>Computador
Detalhes do computador cliente. Ele usa a classe [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem).

#### <a name="services"></a>Serviços
Detalhes de serviços em execução no computador cliente. Ele usa a classe [Win32_Service](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-service).

#### <a name="network-adapters"></a>Adaptadores de rede
Detalhes de adaptadores de rede instalados no computador cliente. Ele usa a classe [Win32_NetworkAdapterConfiguration](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration).


### <a name="bkmk_viewer-logs"></a> Guia Logs

A guia **Logs** exibe uma lista dos arquivos de log incluídos no pacote. Cada linha nessa guia fornece o caminho, o nome e o tamanho do arquivo de log. 

#### <a name="open"></a>Abrir
Depois de selecionar um arquivo de log, selecione esse botão para abrir o **Visualizador de Log**. Ele fornece um subconjunto das funcionalidades vistas na guia Logs do Centro de Suporte.

#### <a name="decode-certificate"></a>Decodificar certificado
Na caixa de diálogo **Decodificar certificado**, cole o valor de certificado serializado para qualquer certificado no cliente. Encontre esse valor no Registro, nos arquivos de log ou no WMI. Selecione **Processo** para exibir informações gerais e detalhes no certificado. Essas informações incluem o caminho de certificação. Selecione **Exportar** para exportar o certificado como um arquivo **.cer**.


### <a name="bkmk_viewer-debug"></a> Guia de despejos de depuração

Cada linha nessa guia fornece detalhes sobre a depuração de arquivos de despejo que estão disponíveis para exportar. Use esta guia para exportar arquivos de despejo de depuração (.dmp) para análise posterior. Essa análise usa uma ferramenta de depuração, como o WinDbg. 

> [!WARNING]  
> Despejos de depuração podem conter informações confidenciais, como senhas, segredos de criptografia ou dados do usuário. Apenas coletar despejos de depuração na recomendação de funcionários de Suporte da Microsoft. Os pacotes de dados que contêm despejos de depuração devem ser tratados com cuidado para protegê-los contra acesso não autorizado.  

#### <a name="export"></a>Exportar
Salve uma cópia do arquivo de despejo de depuração selecionado.


### <a name="bkmk_viewer-wmi"></a> Guia WMI

Essa guia mostra o conjunto de dados de WMI do cliente do Configuration Manager incluído no pacote de dados. 

#### <a name="find"></a>Localizar
Abre a caixa de diálogo Localizar, que tem os seguintes recursos:  

- **Localizar**: Insira uma cadeia de caracteres a ser pesquisada no conjunto de dados da WMI. Dá suporte a caracteres curinga.  

- **Examinar**: Escolha se deseja pesquisar no conjunto de dados da WMI para encontrar um **nome de classe ou de instância**, uma **propriedade** ou um **valor** correspondente.  

- **Corresponder somente à cadeia de caracteres inteira**: Por padrão, a caixa de diálogo pesquisa cadeias de caracteres que contêm a cadeia de caracteres que você está procurando. Marque esta caixa de seleção para localizar apenas cadeias de caracteres que são uma correspondência exata para aquela que você forneceu.  

#### <a name="find-next"></a>Localizar próximo
Esse botão abre a próxima ocorrência da cadeia de caracteres que você forneceu na caixa de diálogo dentro do conjunto de dados WMI.

#### <a name="decode-certificate"></a>Decodificar certificado
Na caixa de diálogo **Decodificar certificado**, cole o valor de certificado serializado para qualquer certificado no cliente. Encontre esse valor no Registro, nos arquivos de log ou no WMI. Selecione **Processo** para exibir informações gerais e detalhes no certificado. Essas informações incluem o caminho de certificação. Selecione **Exportar** para exportar o certificado como um arquivo **.cer**.


### <a name="bkmk_viewer-registry"></a> Guia Registro

Use a guia **Registro** para exibir dados de Registro incluídos no pacote de dados e exportar dados para análise posterior.

#### <a name="export"></a>Exportar
Salve uma cópia da chave e das subchaves do Registro selecionadas como um arquivo de Registro (.reg).

#### <a name="find"></a>Localizar
Abre a caixa de diálogo Localizar, que tem os seguintes recursos:  

- **Localizar**: Insira uma cadeia de caracteres a ser pesquisada no conjunto de dados da WMI. Dá suporte a caracteres curinga.  

- **Examinar**: Escolha se deseja pesquisar no conjunto de dados da WMI para encontrar um **nome de classe ou de instância**, uma **propriedade** ou um **valor** correspondente.  

- **Corresponder somente à cadeia de caracteres inteira**: Por padrão, a caixa de diálogo pesquisa cadeias de caracteres que contêm a cadeia de caracteres que você está procurando. Marque esta caixa de seleção para localizar apenas cadeias de caracteres que são uma correspondência exata para aquela que você forneceu.  

#### <a name="find-next"></a>Localizar próximo
Esse botão abre a próxima ocorrência da cadeia de caracteres que você forneceu na caixa de diálogo dentro do conjunto de dados WMI.

#### <a name="decode-certificate"></a>Decodificar certificado
Na caixa de diálogo **Decodificar certificado**, cole o valor de certificado serializado para qualquer certificado no cliente. Encontre esse valor no Registro, nos arquivos de log ou no WMI. Selecione **Processo** para exibir informações gerais e detalhes no certificado. Essas informações incluem o caminho de certificação. Selecione **Exportar** para exportar o certificado como um arquivo **.cer**.


### <a name="bkmk_viewer-policy"></a> Guia Política

A guia **Política** é usada para exibir dados de política incluídos no pacote de dados. 

#### <a name="find"></a>Localizar
Abre a caixa de diálogo Localizar, que tem os seguintes recursos:  

- **Localizar**: Insira uma cadeia de caracteres a ser pesquisada no conjunto de dados da WMI. Dá suporte a caracteres curinga.  

- **Examinar**: Escolha se deseja pesquisar no conjunto de dados da WMI para encontrar um **nome de classe ou de instância**, uma **propriedade** ou um **valor** correspondente.  

- **Corresponder somente à cadeia de caracteres inteira**: Por padrão, a caixa de diálogo pesquisa cadeias de caracteres que contêm a cadeia de caracteres que você está procurando. Marque esta caixa de seleção para localizar apenas cadeias de caracteres que são uma correspondência exata para aquela que você forneceu.  

#### <a name="find-next"></a>Localizar próximo
Esse botão abre a próxima ocorrência da cadeia de caracteres que você forneceu na caixa de diálogo dentro do conjunto de dados WMI.

#### <a name="decode-certificate"></a>Decodificar certificado
Na caixa de diálogo **Decodificar certificado**, cole o valor de certificado serializado para qualquer certificado no cliente. Encontre esse valor no Registro, nos arquivos de log ou no WMI. Selecione **Processo** para exibir informações gerais e detalhes no certificado. Essas informações incluem o caminho de certificação. Selecione **Exportar** para exportar o certificado como um arquivo **.cer**.


### <a name="bkmk_viewer-certs"></a> Guia Certificados

A guia **Certificados** é usada para exibir certificados incluídos no pacote de dados e para exportá-los.

#### <a name="view-certificate"></a>Exibir certificado
Exibe informações sobre um certificado selecionado.

#### <a name="export"></a>Exportar
Abre uma caixa de diálogo **Salvar como** para salvar uma cópia do certificado selecionado.


### <a name="bkmk_viewer-troubleshoot"></a> Guia Solução de Problemas

Use a guia **Solução de problemas** guia para exibir arquivos de log criados usando a guia de Solução de Problemas do Centro de Suporte.

#### <a name="view-log"></a>Exibir log
Depois de selecionar uma linha na guia **Solução de problemas**, selecione essa opção para exibir o arquivo de log com o Visualizador de Log.
