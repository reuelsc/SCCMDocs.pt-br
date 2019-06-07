---
title: CMTrace
titleSuffix: Configuration Manager
description: Saiba mais sobre como usar a ferramenta CMTrace para exibir arquivos de log para o Configuration Manager.
ms.date: 05/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 332cdf00256ccfbac07b352c22b232edd4ba9363
ms.sourcegitcommit: 7dd42b5a280e64feb69a947dae082fdaf1571272
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66716162"
---
# <a name="cmtrace"></a>CMTrace

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

CMTrace é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). Ele permite exibir e monitorar arquivos de log, incluindo os seguintes tipos:  

- Arquivos de log no formato do Configuration Manager ou o CCM (gerenciador de componente de cliente)  

- Arquivo de texto Unicode ou ASCII simples, como logs do Windows Installer  

A ferramenta ajuda a analisar arquivos de log por meio de destaque, filtragem e pesquisa de erro.

Começando na versão 1806, a ferramenta de visualização de log CMTrace é instalada automaticamente junto com o cliente do Configuration Manager. Ela é adicionada ao diretório de instalação do cliente, que por padrão é `%WinDir%\CCM\CMTrace.exe`.<!--1357971-->

> [!Note]  
> O CMTrace não é registrado automaticamente no Windows para abrir a extensão de arquivo .log. Para obter mais informações, veja [Associações de arquivo](#file-associations).  



## <a name="usage"></a>Uso

Execute **CMTrace.exe**. Na primeira vez que você executa a ferramenta, vê um prompt para associação de arquivo. Para obter mais informações, veja [Associações de arquivo](#file-associations).

Você executa a maioria das ações no CMTrace usando os menus a seguir:
- [File](#file-menu)
- [Ferramentas](#tools-menu)


### <a name="file-menu"></a>Menu Arquivo

As seguintes ações estão disponíveis no menu **Arquivo**:  
- [Abrir](#open)
- [Abrir no Servidor](#open-on-server)
- [Imprimir](#print)
- [Preferências](#preferences)

No menu Arquivo também lista os últimos oito arquivos recentes. Reabra um desses logs rapidamente selecionando-os no menu Arquivo. 

#### <a name="open"></a>Abrir
Exibe a caixa de diálogo Abrir para procurar um arquivo de log. 

Filtre a exibição para os arquivos dos seguintes tipos: 
- Arquivos de Log (\*.log)  
- Arquivos de log antigos (\*.lo_) 
- Todos os arquivos (\*.\*)

As duas opções a seguir não são selecionadas por padrão:  

- **Ignorar linhas existentes**: quando selecionadas, o CMTrace ignora o conteúdo existente do arquivo de log selecionado e exibe novas linhas somente conforme elas são adicionadas. Use essa opção para monitorar apenas novas ações quando o histórico completo do arquivo de log não for necessário.  

- **Mesclar arquivos selecionados**: se você habilitar essa opção e selecionar mais de um arquivo de log, o CMTrace mesclará os logs selecionados na exibição. Ele os exibe como se fossem um único arquivo de log. O log mesclado atualiza o mesmo e dá suporte a todos os outros recursos de CMTrace como se fosse um único arquivo de log.  


#### <a name="open-on-server"></a>Abrir no Servidor
Procure a pasta de logs do Configuration Manager em um computador do sistema de sites com a caixa de diálogo Procurar padrão. Você também pode procurar na rede por um computador remoto.   

Ao selecionar um computador remoto para procurar, o CMTrace verifica o compartilhamento do Configuration Manager. Se ele não conseguir localizar um compartilhamento de arquivos de log do Configuration Manager, exibirá uma mensagem de erro.  

Para se conectar diretamente a um computador conhecido sem navegar, use a ação [Abrir](#open). Em seguida, insira um nome do servidor e compartilhamento usando o formato UNC.

#### <a name="print"></a>Imprimir
Exiba a caixa de diálogo de Impressão do Windows padrão. Essa ação envia o arquivo de log atual para uma impressora. Ele formata a saída de acordo com as configurações na guia Impressão das Preferências do CMTrace.

#### <a name="preferences"></a>Preferências
Defina as configurações do CMTrace. As seguintes opções estão disponíveis:  

- Guia**Geral**  

     - **Intervalo de Atualização**: controla a frequência com que o CMTrace verifica se há alterações nos arquivos de log e carrega as novas linhas. Por padrão, esse valor é de 500 milissegundos.  

     - **Realçar**: define a cor que o CMTrace usa ao destacar as linhas de log que você escolhe. Por padrão, essa cor é amarelo básico (vermelho: 255, verde: 255, azul: 0).  

     - **Colunas**: configura as colunas visíveis na exibição de log e a ordem em que aparecem. Por padrão, exibe o Texto de Log, Componente, Data/Hora e Thread.  

- Guia **Impressão**  

     - **Colunas**: configure quais colunas ele usa ao imprimir arquivos de log e a ordem em que aparecem. Por padrão, ele imprime as mesmas colunas que exibe.  

     - **Orientação**: define a orientação de impressão padrão ao imprimir arquivos de log. Substitua essa configuração na caixa de diálogo Imprimir. Por padrão, ele usa a orientação Retrato.  
 
- Guia **Avançado**  

     - **Intervalo de Atualização**: força o CMTrace a atualizar a exibição de log em um intervalo especificado ao carregar um grande número de linhas. Por padrão, essa opção é desabilitada com um valor de zero.  

        > [!Note]  
        > Em geral, não modifique o **Intervalo de Atualização**. Isso pode aumentar significativamente a quantidade de tempo que leva para abrir arquivos de log grandes. 


### <a name="tools-menu"></a>Menu Ferramentas
As seguintes ações estão disponíveis no menu **Ferramentas**:  
- [Localizar](#find)
- [Localizar Próximo](#find-next)
- [Copiar para a Área de Transferência](#copy-to-clipboard)
- [Destacar](#highlight)
- [Filtrar](#filter)
- [Pesquisa de Erro](#error-lookup)
- [Pausar](#pause)
- [Mostrar/Ocultar Detalhes](#showhide-details)
- [Mostrar/Ocultar Painel de Informações](#showhide-info-pane)

#### <a name="find"></a>Localizar
Pesquise o arquivo de log aberto para uma cadeia de caracteres de texto especificada.  

#### <a name="find-next"></a>Localizar Próximo
Localiza a próxima cadeia de caracteres correspondente, conforme você especificou anteriormente na caixa de diálogo Localizar.  

#### <a name="copy-to-clipboard"></a>Copiar para a Área de Transferência
Copia as linhas selecionadas como texto sem formatação para a área de transferência do Windows. Se você estiver analisando os arquivos de log do CCM e do Configuration Manager, ele copiará as colunas na mesma ordem da exibição. Ele separa cada coluna por um caractere de tabulação. Use esta ação ao copiar os logs para mensagens de email ou outros documentos.  

#### <a name="highlight"></a>Destacar
Insira uma cadeia de caracteres que usa o CMTrace para pesquisar o texto de cada entrada de log. Ele então destaca qualquer texto de log que corresponde à cadeia de caracteres que você insere.  

- O destaque usa a cor especificada nas Preferências.  

- Para desligar o destaque, limpando a cadeia de caracteres desse campo.  

- Se você inserir um número decimal ou hexadecimal, o CMTrace tentará combinar o valor com a coluna de Thread. Use esse comportamento para destacar o processamento de um único thread, sem filtrar outros threads que possam interagir com eles.  

- Para comparar cadeias de caracteres por caso, habilite a opção para **Diferenciar maiúsculas de minúsculas**.  
 
#### <a name="filter"></a>Filtro
Mostrar ou ocultar linhas de log com base nos critérios especificados. Aplica filtros a qualquer uma das quatro colunas, não importa se elas estão visíveis. Essas configurações se aplicam a cada arquivo de log aberto. 

Exemplos:
<!--SCCMDocs issue #603-->
- Filtre **SMSTS.log** no texto de entrada que contém "a ação" ou "o grupo". 
- Filtre **InventoryAgent.log** no ponto em que o texto de entrada contém "destino".


#### <a name="error-lookup"></a>Pesquisa de Erro
Digite ou cole um código de erro no formato decimal ou hexadecimal para exibir uma descrição. Possíveis origens do erro incluem: Windows, WMI ou Winhttp.

#### <a name="pause"></a>Pausar
Suspender ou reiniciar o monitoramento de log. Os casos de uso a seguir estão algumas das possíveis razões para usar essa ação:  

- Quando o CMTrace está exibindo informações do arquivo de log muito rapidamente  

- Quando você pausa o monitoramento de log, as informações exibidas CMTrace não serão perdidas se o arquivo atual mudar para um novo log  

- Quando você deseja impedir que o CMTrace exiba novos dados enquanto você examina o arquivo de log  

#### <a name="showhide-details"></a>Mostrar/Ocultar Detalhes
Mostrar ou ocultar todas as colunas que não o texto de log. Ele também expande a coluna de texto de log para a largura da janela. Use essa ação quando você estiver exibindo os logs em um computador com baixa resolução de tela. Exibe mais do texto de log.  

> [!Note]   
> Ao exibir os arquivos de texto sem formatação, o CMTrace automaticamente oculta detalhes porque eles estão sempre vazios.  
 
#### <a name="showhide-info-pane"></a>Mostrar/Ocultar Painel de Informações
Mostrar ou ocultar o painel de informações. Use essa ação quando você estiver exibindo os logs em um computador com baixa resolução de tela. Exibe mais detalhes de registro em log.  



## <a name="log-pane"></a>Painel de log

O painel de log está na parte superior da janela CMTrace. Exibe linhas de arquivos de log. 

Quando você seleciona uma linha, ela é destacada temporariamente usando o esquema de cores de seleção do Windows. 

Linhas destacadas correspondem aos critérios definidos com a opção **Destaque** no menu **Ferramentas**. O realce usa a cor que você especifica em **Preferências**.

O CMTrace exibe linhas com erros usando uma tela de fundo vermelha e a cor do texto amarela. Nos logs de formato do CCM, as entradas de log têm um valor de tipo explícito que indica a entrada como um erro. Para os outros formatos de log, o CMTrace faz uma pesquisa que diferencia maiúsculas de minúsculas em cada entrada para qualquer "erro" que corresponda à cadeia de caracteres de texto.

Ele exibe linhas com avisos usando uma tela de fundo amarela. Nos logs de formato do CCM, as entradas de log têm um valor de tipo explícito que indica a entrada como um aviso. Para os outros formatos de log, o CMTrace faz uma pesquisa que diferencia maiúsculas de minúsculas em cada entrada para qualquer "aviso" que corresponda à cadeia de caracteres de texto.



## <a name="info-pane"></a>Painel de informações

O painel de informações está na parte inferior da janela CMTrace. Ele contém os seguintes recursos:   

- Detalhes sobre a entrada de log selecionada no momento  

- Uma caixa de texto que exibe o texto de log  

- Ele exibe retornos de carro para que o texto formatado seja mais fácil de ler  

- Entradas longas mais fáceis de ler que não são totalmente visíveis no painel de Log  

Mostrar ou ocultar o painel de Informações com a opção **Mostrar/Ocultar Painel de Informações** no menu **Ferramentas**. Se o painel de informações ocupar mais da metade da janela de log, o CMTrace a ocultará automaticamente.


### <a name="progress-bar"></a>Barra de progresso

Quando você abre um arquivo de log pela primeira vez, o CMTrace substitui o painel de Informações por uma barra de progresso. Esse progresso indica quanto dos conteúdos existentes do arquivo são carregados. O progresso atinge 100%, o CMTrace remove a barra de progresso e a substitui pelo painel de Informações. Quando você carrega arquivos grandes, esse comportamento fornece uma indicação de quanto tempo o carregamento pode demorar.


### <a name="status-bar"></a>Barra de status

Para o formato do Configuration Manager e os arquivos de log no formato CCM, a barra de status exibe o tempo decorrido para as entradas de log selecionadas. Se você selecionar uma única entrada, a ferramenta exibirá a hora da primeira entrada de log para a entrada selecionada. Se você selecionar várias entradas, ele calculará o tempo da entrada selecionada da mais alta para a mais baixa. O CMTrace formata essas informações da seguinte maneira:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`



## <a name="windows-shell-integration"></a>Integração ao shell do Windows

O CMTrace dá suporte para [associações de arquivo](#file-associations) e ações do tipo ["arrastar e soltar"](#drag-and-drop).


### <a name="file-associations"></a>Associações de arquivo 

O CMTrace pode associar-se a extensões de nome de arquivo .log e .lo_. Quando o programa é iniciado, ele verifica o Registro para determinar se ele já está associado a essas extensões de nome de arquivo. Se CMTrace ainda não estiver associado a nenhuma extensão de nome de arquivo, você será solicitado a associar as extensões de nome de arquivo do CMTrace. Se você selecionar **Não me perguntar novamente**, o CMTrace ignorará essa verificação sempre que for executado neste computador.


### <a name="drag-and-drop"></a>Arrastar e soltar

O CMTrace é compatível com a funcionalidade básica do tipo "arrastar e soltar". Arraste um arquivo de log do Windows Explorer no CMTrace para abri-lo.



## <a name="other-tips"></a>Outras dicas

### <a name="last-directory-registry-key"></a>Chave do Registro do último diretório
<!--511280-->
Por padrão, o CMTrace salva o último local de log que você abriu. Esse comportamento é útil no servidor do site, uma vez que ele sempre usa como o padrão o caminho de logs. 

Na primeira vez que você inicializá-lo em um cliente, ele usará como padrão o diretório de trabalho atual. Esse local pode ser o caminho no qual você salvou o CMTrace ou um caminho como `%userprofile%\Desktop`. 

O valor **Último Diretório** na chave do Registro `HKEY_CURRENT_USER\Software\Microsoft\Trace32` controla esse local padrão. Se você definir esse valor como `%windir%\CCM\Logs` nos seus clientes, o CMTrace abrirá arquivos no local de log do cliente na primeira vez que você o executar.


## <a name="see-also"></a>Consulte também

[Arquivos de log](/sccm/core/plan-design/hierarchy/log-files)
