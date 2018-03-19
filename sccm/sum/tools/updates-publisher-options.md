---
title: "Configurar opções"
titleSuffix: Configuration Manager
description: "Configurar opções para usar o System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 0080e8067c0689d4a681a135b16d62b4af4f0fb8
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="configure-options-for-updates-publisher"></a>Configurar opções para o Updates Publisher

*Aplica-se ao: System Center Updates Publisher*

Analise e defina as opções e configurações relacionadas que afetam a operação do Updates Publisher.

Para acessar as opções do Updates Publisher, no canto superior esquerdo do console, clique em **Updates Publisher**, guia **Propriedades** e escolha **Opções**.

![Opções](media/properties1.png)   


As opções estão divididas assim:

-   Update Server
-   ConfigMgr Server
-   Configurações Proxy
-   Editores Confiáveis
-   Avançado
-   Atualizações
-   Registrando em log

## <a name="update-server"></a>Update Server
Você deve configurar o Updates Publisher para trabalhar com um servidor de atualização como o Windows Server Update Services (WSUS) antes de poder [publicar atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher#publish-updates-and-bundles). Isso inclui a especificação do servidor, métodos para se conectar a esse servidor quando ele for remoto com relação ao console e um certificado a ser usado para assinar digitalmente as atualizações publicadas.

-   **Configurar um servidor de atualização**. Ao configurar um servidor de atualização, selecione o servidor WSUS de nível superior (servidor de atualização) em sua hierarquia do Configuration Manager para que todos os sites filho tenham acesso às atualizações que você publicar.

  Se o servidor de atualização for remoto com relação ao seu servidor do Updates Publisher, especifique o FQDN (Nome de domínio totalmente qualificado) do servidor e se você se conectará por SSL. Quando você se conecta por SSL, a porta padrão muda de 8530 para 8531. Certifique-se de que a porta configurada corresponda à porta que está sendo usada por seu servidor de atualização.

    > [!TIP]  
    > Se você não configurar um servidor de atualização, ainda poderá usar o Updates Publisher para criar atualizações de software.

-   **Configure o certificado de autenticação**. Você deve configurar e conectar-se com êxito a um servidor de atualização antes de poder configurar o certificado de autenticação.

    O Updates Publisher usa o certificado de autenticação para assinar as atualizações de software que são publicadas no servidor de atualização. A publicação falhará se o certificado digital não estiver disponível no repositório de certificados do servidor de atualização ou no computador que executa o Updates Publisher.

    Para saber mais sobre como adicionar o certificado ao repositório de certificados, confira [Certificados e segurança para o Updates Publisher](/sccm/sum/tools/updates-publisher-security).

    Se um certificado digital não for detectado automaticamente para o servidor de atualização, escolha uma das seguintes opções:

    -   **Procurar**: a opção de procurar só estará disponível quando o servidor de atualização for instalado no servidor onde você executa o console. Depois de selecionar um certificado você deve escolher **Criar** para adicionar o certificado ao repositório de certificados do WSUS no servidor de atualização. Você deve inserir a senha do arquivo **.pfx** para os certificados selecionados por esse método.

    -   **Criar:** use essa opção para criar um novo certificado. Isso também adiciona o certificado ao repositório de certificados do WSUS no servidor de atualização.

    **Se você criar seu próprio certificado de autenticação**, configure o seguinte:

    -   Habilite a opção **Permitir que a chave privada seja exportada**.

    -   Defina **Uso de Chave** como assinatura digital.

    -   Defina **Tamanho mínimo da chave** como um valor igual ou maior do que 2048 bits.

    Use a opção **Remover** para remover um certificado do repositório de certificados do WSUS. Essa opção estará disponível quando o servidor de atualização for local com relação ao console do Updates Publisher usado, ou quando você usar **SSL** para se conectar a um servidor de atualização remoto.

## <a name="configmgr-server"></a>ConfigMgr Server
Use essas opções ao usar o Configuration Manager com o Updates Publisher.

-   **Especifique o servidor do Configuration Manager:** depois de habilitar o suporte para o Configuration Manager, especifique o local do servidor de site de nível superior de sua hierarquia do Configuration Manager. Se esse servidor for remoto com relação à instalação do Updates Publisher, especifique o FQDN do servidor do site. Escolha **Conexão de Teste** para garantir que você possa se conectar ao servidor do site.

-   **Configurar limites:** os limites são usados quando você publica atualizações com um tipo de publicação Automática. Os valores do limite ajudam a determinar quando o conteúdo completo de uma atualização é publicado em vez de apenas os metadados. Para conhecer mais tipos de publicação, veja [Atribuir atualizações a uma publicação](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)

    Habilite um ou os dois limites a seguir:

    -   **Limite de contagem de solicitação do cliente:** define quantos clientes devem solicitar uma atualização antes que o Updates Publisher possa publicar automaticamente o conjunto completo de conteúdo para essa atualização. Até que o número especificado de clientes solicite a atualização, apenas os metadados das atualizações são publicados.

    -   **Limite de tamanho de origem do pacote (MB):** isso impede a publicação automática de atualizações que ultrapassam o tamanho especificado. Se o tamanho das atualizações ultrapassar esse valor, apenas os metadados serão publicados. Atualizações menores do que o tamanho especificado podem ter seu conteúdo completo publicado.

## <a name="proxy-settings"></a>Configurações Proxy
O Updates Publisher usa as configurações de proxy quando você importa catálogos de software da Internet ou publica atualizações na Internet.

-   Especifique o endereço IP ou FQDN de um servidor proxy. Há suporte para IPv4 e IPv6.

-   Se o servidor proxy autenticar os usuários para acesso à Internet, especifique o nome do Windows. Não há suporte para um nome UPN (nome de entidade universal).

## <a name="trusted-publishers"></a>Editores Confiáveis
Quando você importar um catálogo de atualizações, a origem desse catálogo (com base em seu certificado), será adicionada como um editor confiável. Da mesma forma, quando você publica uma atualização, a origem do certificado de atualizações é adicionada como um editor confiável.

Você pode exibir detalhes do certificado para cada editor e remover um editor da lista de editores confiáveis.

O conteúdo de editores não confiáveis pode danificar os computadores dos clientes quando o cliente verifica se há atualizações. Aceite o conteúdo somente de editores confiáveis.

## <a name="advanced"></a>Avançado
As opções avançadas incluem as seguintes:

-   **Local do repositório:** veja e modifique o local do arquivo de Banco de Dados, **scupdb.sdf**. Esse arquivo é o repositório para o Updates Publisher.

-   **Carimbo de hora:** quando habilitado, um carimbo de hora é adicionado às atualizações assinadas por você, identificando quando foram assinadas. Uma atualização que foi assinada enquanto um certificado era válido pode ser usada após a expiração desse certificado de autenticação. Por padrão, as atualizações de software não podem ser implantadas após a expiração do certificado de assinatura.

-   **Verificar se há atualizações nos catálogos inscritos:** sempre que o Updates Publisher é iniciado, ele pode procurar automaticamente por atualizações para os catálogos nos quais você se inscreveu. Quando uma atualização de catálogo é encontrada, os detalhes são fornecidos como **Alertas Recentes** na janela **Visão Geral** do **Espaço de Trabalho de Atualizações**.

-   **Revogação de certificado:** escolha esta opção para habilitar verificações de revogação de certificado.

-   **Publicação de origem local:** o Updates Publisher pode usar uma cópia local de uma atualização que você está publicando antes de baixar essa atualização da Internet. O local deve ser uma pasta no computador que executa o Updates Publisher. Por padrão, esse local é **Meus Documents\LocalSourcePublishing.** Use isso quando você tiver baixado anteriormente uma ou mais atualizações ou tiver feito modificações em uma atualização que você deseja implantar.

-   **Assistente para Limpeza de Atualizações de Software:** inicie o assistente para limpeza de atualizações. O assistente expira atualizações que estão no servidor de atualização, mas que não estão no repositório do Updates Publisher. Consulte [Expirar atualizações sem referência](#expire-unreferenced-software-updates) para obter mais detalhes.

## <a name="updates"></a>Atualizações
 O Updates Publisher pode verificar automaticamente novas atualizações sempre que é aberto. Você também pode aceitar receber builds de visualização do Updates Publisher.

Para verificar manualmente se há atualizações no console do Updates Publisher, clique em ![Propriedades](media/properties2.png)  
para abrir as **Propriedades do Updates Publisher** e escolha **Verificar se há atualização**.

Quando o Updates Publisher encontra uma nova atualização, ele exibe a janela **Atualização Disponível** e você pode optar por instalá-la. Se você optar por não instalar a atualização, ela será oferecida na próxima vez que você abrir o console.

## <a name="logging"></a>Registrando em log
O Updates Publisher registra informações básicas sobre o Updates Publisher em **&lt;* caminho*&gt;\Windows\Temp\UpdatesPublisher.log**.

Use o bloco de notas ou o **CMTrace** para exibir o log. CMTrace é a ferramenta de arquivo de log do Configuration Manager localizada na pasta **\SMSSetup\Tools** da mídia de origem do Configuration Manager.

Você pode alterar o tamanho do log e seu nível de detalhes.

Quando você habilita o registro em log de banco de dados, as informações sobre as consultas executadas no banco de dados do Updates Publisher são incluídas. O uso do registro em log de banco de dados pode diminuir o desempenho do computador com o Updates Publisher.

Para exibir o arquivo de log, no console, clique em ![Propriedades](media/properties2.png) para abrir as **Propriedades do Updates Publisher** e, em seguida, escolha **Exibir arquivo de log**.

## <a name="expire-unreferenced-software-updates"></a>Expirar atualizações de software sem referência
Você pode executar o **Assistente para Limpeza de Atualização de Software** para expirar atualizações que estão em seu servidor de atualização, mas não no repositório do Updates Publisher. Isso notifica o Configuration Manager, que remove essas atualizações de quaisquer implantações futuras.

O ato de expiração de uma atualização não pode ser revertido. Apenas execute essa tarefa quando tiver certeza de que as atualizações de software selecionadas não são mais necessárias para sua organização.

### <a name="to-remove-expired-software-updates"></a>Para remover as atualizações de software expiradas
1.  No console do Updates Publisher, clique em ![Propriedades](media/properties2.png) para abrir as **Propriedades do Updates Publisher** e escolha **Opções**.

2.  Escolha **Avançado** e, em **Assistente para Limpeza de Atualização de Software,** escolha **Iniciar**.

3.  Selecione as atualizações de software que você deseja expirar e depois escolha **Avançar**.

4.  Depois de revisar suas seleções, escolha **Avançar** para aceitar as seleções e expirar essas atualizações.

5.  Após a conclusão do assistente, escolha **Fechar** para concluir o assistente.
