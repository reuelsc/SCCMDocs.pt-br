---
title: Criar aplicativos
titleSuffix: Configuration Manager
description: Crie aplicativos com tipos de implantação, métodos de detecção e requisitos para instalação do software.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 947dfac82db43e5cb21d8304d31be23219bb83aa
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456644"
---
# <a name="create-applications-in-configuration-manager"></a>Criar aplicativos no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um aplicativo do Configuration Manager define os metadados sobre o aplicativo. Um aplicativo tem um ou mais tipos de implantação. Esses tipos de implantação incluem os arquivos de instalação e as informações necessárias para instalação do software em dispositivos. Um tipo de implantação também tem regras, como métodos de detecção e requisitos. Essas regras especificam quando e como o cliente deve instalar o software.  

Crie aplicativos usando os seguintes métodos:  

-   Crie automaticamente um aplicativo e tipos de implantação lendo os arquivos de instalação do aplicativo:  
    - [Criar um aplicativo](#bkmk_create) e [detectar automaticamente](#bkmk_auto-app) as informações do aplicativo
    - [Criar um tipo de implantação](#bkmk_create-dt) e [identificar automaticamente](#bkmk_auto-dt) as informações do tipo de implantação

-   Crie um aplicativo manualmente e, mais tarde, adicione tipos de implantação:  
    - [Criar um aplicativo](#bkmk_create) e [especificar manualmente](#bkmk_manual-app) as informações do aplicativo
    - [Criar um tipo de implantação](#bkmk_create-dt) e [especificar manualmente](#bkmk_manual-dt) as informações de tipo de implantação

-   [Importar um aplicativo](#bkmk_import) de um arquivo  

Este artigo também inclui as seguintes informações para configurar um tipo de implantação:  
- [Conteúdo](#bkmk_dt-content)
- [Método de detecção](#bkmk_dt-detect)
- [Experiência do Usuário](#bkmk_dt-ux)
- [Requirements](#bkmk_dt-require)
- [Códigos de retorno](#bkmk_dt-return)
- [Dependências](#bkmk_dt-depend)



## <a name="bkmk_create"></a> Criar um aplicativo  

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Aplicativos**.  

2.  Na guia **Início** da faixa de opções, no grupo **Criar**, clique em **Criar Aplicativo**.  

Em seguida, detecte automaticamente ou especifique manualmente as informações do aplicativo:  

-   [Detecte automaticamente](#bkmk_auto-app) as informações do aplicativo para criar um aplicativo básico com um único tipo de implantação. Por exemplo, um arquivo do Windows Installer sem dependências nem requisitos. Depois de criar um aplicativo usando esse procedimento, edite-o conforme o necessário. Você pode adicionar ou alterar os tipos de implantação e adicionar métodos de detecção, dependências ou requisitos.  

-   [Especifique manualmente](#bkmk_manual-app) as informações do aplicativo para criar aplicativos mais complexos. Defina mais de um tipo de implantação, dependências, métodos de detecção ou requisitos.  


### <a name="bkmk_auto-app"></a> Detectar automaticamente as informações do aplicativo  

1.  Na página **Geral** do Assistente para Criar Aplicativo, selecione **Detectar automaticamente informações sobre este aplicativo em arquivos de instalação**.  

2.  Na lista suspensa **Tipo** , selecione o tipo de arquivo de instalação do aplicativo que deseja usar para detectar as informações do aplicativo. Para obter mais informações sobre os tipos de instalação disponíveis, confira [Tipos de implantação com suporte do Configuration Manager](/sccm/apps/deploy-use/create-applications#bkmk_deploy-types).  

3.  Na caixa **Local**, especifique o arquivo de instalação do aplicativo que você deseja usar para detectar as informações do aplicativo. Esse local é um caminho de rede (`\\server\share\filename`) ou um link do repositório. É necessário ter acesso ao caminho de rede e às subpastas que incluem o conteúdo do aplicativo.  

    > [!IMPORTANT]  
    >  Quando você seleciona **Windows Installer (\*arquivo .msi)** como um tipo de aplicativo, o site importa todos os arquivos da pasta especificada. Em seguida, ele envia esses arquivos aos pontos de distribuição. Verifique se a pasta especificada contém apenas os arquivos necessários instalar o aplicativo. A Microsoft testou o Configuration Manager para dar suporte a até 20 mil arquivos no pacote de aplicativos. Se o aplicativo tiver mais arquivos, considere a possibilidade de criar vários aplicativos com menos arquivos.    

4.  Na página **Importar Informações** do Assistente para Criar Aplicativo, examine as informações e clique em **Avançar**. Se necessário, clique em **Anterior** para voltar e corrigir erros.  

5.  Na página **Informações Gerais** do Assistente para Criar Aplicativo, especifique as seguintes informações:  

    > [!NOTE]  
    >  Se o Configuration Manager detectar automaticamente essas informações dos arquivos de instalação do aplicativo, elas já estarão populadas aqui. Além disso, as opções exibidas podem ser diferentes dependendo do tipo de aplicativo que você criar.  

    -   Informações gerais sobre o aplicativo, como o **Nome**, os **Comentários do administrador**, o **Publicador** e a **Versão do software** do aplicativo. Para ajudá-lo a localizar o aplicativo no console do Configuration Manager, especifique uma **Referência opcional** ou selecione **Categorias administrativas**.  

    -   **Programa de instalação**: especifique o programa de instalação e as propriedades necessárias para instalar o tipo de implantação do aplicativo.  

        > [!TIP]  
        >  Se o programa de instalação não for exibido, escolha **Procurar** e procure o local do programa de instalação.  

    -   **Comportamento da instalação**: selecione uma das três opções de como o Configuration Manager deve instalar esse tipo de implantação. Para obter mais informações sobre essas opções, confira [Experiência de Usuário](#bkmk_dt-ux).  

    -   **Usar uma conexão VPN automática (se configurada)**: se você implantou um perfil de VPN para o dispositivo no qual o usuário inicia o aplicativo, conecte-se à VPN quando o aplicativo for iniciado. Essa opção é somente para Windows 8.1 e Windows Phone 8.1. Em dispositivos Windows Phone 8.1, se você implantar mais de um perfil de VPN no dispositivo, não haverá suporte para conexões VPN automáticas. Para obter mais informações, consulte [Perfis de VPN](/sccm/protect/deploy-use/vpn-profiles).  

    - **Provisionar este aplicativo para todos os usuários no dispositivo**<!--1358310-->: começando na versão 1806, é possível provisionar um aplicativo com um pacote do aplicativo do Windows para todos os usuários no dispositivo. Para obter mais informações, confira [Criar aplicativos Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).  

       > [!Tip]  
       > Se você estiver modificando um aplicativo existente, essa configuração estará na guia **Experiência do Usuário** das propriedades de tipo de implantação do pacote do aplicativo do Windows.  

6.  Escolha **Avançar**, examine as informações do aplicativo na página **Resumo** e, em seguida, conclua o Assistente para Criar Aplicativo.  

Agora o novo aplicativo aparece no nó **Aplicativos** do console do Configuration Manager. Você concluiu a criação de um aplicativo. 

Para adicionar mais tipos de implantação ou definir outras configurações, confira [Criar tipos de implantação para o aplicativo](#bkmk_create-dt).  


### <a name="bkmk_manual-app"></a> Especificar manualmente as informações do aplicativo  

1.  Na página **Geral** do Assistente para Criar Aplicativo, selecione **Especificar manualmente as informações do aplicativo** e escolha **Avançar**.  

2.  Especifique as **Informações gerais** sobre o aplicativo:  

    - O **Nome** do aplicativo é obrigatório e precisa ter menos de 256 caracteres.  

    - **Comentários do administrador**, **Publicador** e **Versão do Software** são metadados adicionais para descrever ainda mais o aplicativo.  

    - Para ajudá-lo a localizar o aplicativo no console do Configuration Manager, especifique uma **Referência opcional** ou selecione **Categorias administrativas**.  

    - **Data de publicação**  

    - Selecione usuários ou grupos que são responsáveis por este aplicativo como **Proprietários** e **Contatos de suporte**. Por padrão, esses valores são definidos como seu nome de usuário.  

3.  Na página **Catálogo de Aplicativos** do Assistente para Criar Aplicativo, especifique as seguintes informações:  

    -   **Idioma selecionado**: na lista suspensa, selecione a versão de idioma do aplicativo que deseja configurar. Escolha **Adicionar/Remover** para configurar mais idiomas para esse aplicativo.  

    -   **Nome do aplicativo localizado**: especifique o nome do aplicativo no idioma selecionado.  

        > [!IMPORTANT]  
        > Um nome de aplicativo localizado é necessário para cada versão de idioma que você configura.  

    -   **Categorias do usuário**: escolha **Editar** para especificar as categorias do aplicativo no idioma selecionado. Os usuários do Centro de Software usam essas categorias para filtrar e classificar os aplicativos disponíveis.  

    -   **Documentação do usuário**: especifique o local de um arquivo no qual os usuários do Centro de Software podem obter mais informações sobre este aplicativo. Esse local é um endereço de site ou um caminho de rede e um nome de arquivo. Verifique se os usuários têm acesso a esse local.  

    -   **Texto do link**: especifique o texto que é exibido no lugar da URL do aplicativo.  

    -   **URL de privacidade**: especifique um endereço de site para a política de privacidade do aplicativo.  

    -   **Descrição localizada**: insira uma descrição deste aplicativo no idioma selecionado.  

    -   **Palavras-chave**: insira uma lista de palavras-chave no idioma selecionado. Essas palavras-chave ajudam os usuários do Centro de Software a pesquisar o aplicativo.  

    -   **Ícone**: clique em **Procurar** para selecionar um ícone para este aplicativo. Se você não especificar um ícone, o Configuration Manager usará um ícone padrão. Os ícones podem ter dimensões de pixel de até 512 x 512.  

    -   **Exibir como um aplicativo em destaque e realçá-lo no Portal da Empresa**: essa opção exibe o aplicativo em destaque no Portal da Empresa em dispositivos móveis.  

4.  Na página **Tipos de Implantação** do Assistente para Criar Aplicativo, escolha **Adicionar** para criar um novo tipo de implantação. Para obter mais informações, consulte [Criar tipos de implantação para o aplicativo](#bkmk_create-dt).  

5.  Escolha **Avançar**, examine as informações do aplicativo na página **Resumo** e, em seguida, conclua o Assistente para Criar Aplicativo.  

Agora o novo aplicativo aparece no nó **Aplicativos** do console do Configuration Manager.  



## <a name="bkmk_create-dt"></a> Criar tipos de implantação para o aplicativo  

Se você [detectar automaticamente as informações do aplicativo](#bkmk_auto-app), talvez não seja necessário concluir algumas das etapas desta seção.  

> [!Note]  
> Quando você exibe as propriedades de um tipo de implantação existente, as seções a seguir correspondem às guias da janela Propriedades do tipo de implantação:  
> - [Conteúdo](#bkmk_dt-content)
> - [Método de detecção](#bkmk_dt-detect)
> - [Experiência do Usuário](#bkmk_dt-ux)
> - [Requirements](#bkmk_dt-require)
> - [Códigos de retorno](#bkmk_dt-return)
> - [Dependências](#bkmk_dt-depend)
>  
> Para obter informações sobre a guia **Comportamento da Instalação** nas propriedades de um tipo de implantação, confira [Verificar se há arquivos executáveis](/sccm/apps/deploy-use/deploy-applications#bkmk_exe-check).  


### <a name="start-the-create-deployment-type-wizard"></a>Iniciar o assistente para Criar Tipo de Implantação  

Há três maneiras de iniciar o Assistente para Criar Tipo de Implantação:

- **No nó Aplicativos**: no console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Aplicativos**. Selecione um aplicativo e, em seguida, clique em **Criar Tipo de Implantação** na faixa de opções.  

- **Ao criar um aplicativo**: quando você [Especificar manualmente as informações do aplicativo](#bkmk_manual-app) no assistente para Criar Aplicativo, clique em **Adicionar** na página Tipos de Implantação.  

- **Nas propriedades do aplicativo**: selecione um aplicativo existente no nó **Aplicativos** e clique em **Propriedades**. Mude para a guia **Tipos de Implantação** e, em seguida, clique em **Adicionar**.

Em seguida, use um dos procedimentos a seguir para [identificar automaticamente](#bkmk_auto-dt) ou [especificar manualmente](#bkmk_manual-dt) as informações do tipo de implantação.  


### <a name="bkmk_auto-dt"></a> Identificar automaticamente as informações do tipo de implantação  

1.  Na página **Geral** do Assistente para Criar Tipo de Implantação:  

    1. Selecione o **Tipo** de arquivo de instalação do aplicativo para detectar as informações do tipo de implantação.  

    2. Selecione **Identificar automaticamente as informações sobre esse tipo de implantação por meio dos arquivos de instalação**.  

    3.  Na caixa **Local**, especifique o tipo de arquivo de instalação de aplicativo que deseja usar para detectar as informações do tipo de implantação. Esse local é um caminho de rede (`\\server\share\filename`) ou um link do repositório. É necessário ter acesso ao caminho de rede e às subpastas que incluem o conteúdo do aplicativo.  

2.  Na página **Importar Informações** do assistente para Criar Tipo de Implantação, examine as informações e clique em **Avançar**. Se necessário, clique em **Anterior** para voltar e corrigir erros.  

3.  Na página **Informações Gerais** do Assistente para Criar Tipo de Implantação, especifique as seguintes informações:  

    > [!NOTE]  
    >  Algumas das informações do tipo de implantação podem já estar presentes se elas tiverem sido lidas dos arquivos de instalação do aplicativo. Além disso, as opções exibidas podem variar, dependendo do tipo de implantação criado.  

    -   **Informações gerais** sobre o tipo de implantação:      
        - O **Nome** é obrigatório  

        - **Comentários do administrador** para descrevê-lo melhor  

        - Os **Idiomas** que estão disponíveis para ele   

    -   **Programa de instalação**: especifique o programa de instalação e as propriedades que você precisa para instalar o tipo de implantação.  

    -   **Comportamento da instalação**: selecione uma das três opções de como o Configuration Manager deve instalar esse tipo de implantação. Para obter mais informações sobre essas opções, confira [Experiência de Usuário](#bkmk_dt-ux).  

    -   **Usar uma conexão VPN automática (se configurada)**: se você implantou um perfil de VPN para o dispositivo no qual o usuário inicia o aplicativo, conecte-se à VPN quando o aplicativo for iniciado. Essa opção é somente para Windows 8.1 e Windows Phone 8.1. Em dispositivos Windows Phone 8.1, se você implantar mais de um perfil de VPN no dispositivo, não haverá suporte para conexões VPN automáticas. Para obter mais informações, consulte [Perfis de VPN](/sccm/protect/deploy-use/vpn-profiles).  

4.  Escolha **Avançar** e, em seguida, continue nas [Opções de tipo de conteúdo de implantação](#bkmk_dt-content).  


### <a name="bkmk_manual-dt"></a> Especificar manualmente as informações do tipo de implantação  

1.  Na página **Geral** do assistente para Criar Tipo de Implantação, na lista suspensa **Tipo**, escolha o tipo de arquivo de instalação do aplicativo para esse tipo de implantação. 

2.  Selecione **Especificar manualmente as informações de tipo de implantação** e, em seguida, clique em **Avançar**.

3.  Na página **Informações Gerais** do Assistente para Criar Tipo de Implantação, especifique um **Nome** para o tipo de implantação. Opcionalmente, especifique **Comentários do administrador**, selecione os **Idiomas** para esse tipo de implantação e clique em **Avançar**.  

4.  Continue nas [Opções de conteúdo do tipo de implantação](#bkmk_dt-content).  

### <a name="bkmk_dt-content"></a> Opções de **conteúdo** do tipo de implantação  

Na página **Conteúdo**, especifique as seguintes informações:  

> [!Note]  
> Quando você exibe as propriedades de um tipo de implantação existente, algumas dessas opções são exibidas na guia **Conteúdo** e outras na guia **Programas**.  

- **Local do conteúdo**: especifique o local do conteúdo para esse tipo de implantação ou selecione **Procurar** para escolher a pasta de conteúdo do tipo de implantação.  

    > [!IMPORTANT]  
    >  A conta Sistema do computador servidor do site precisa ter permissões para o local do conteúdo especificado.  

    - **Manter o conteúdo no cache do cliente**: o cliente do Configuration Manager mantém indefinidamente em seu cache o conteúdo do tipo de implantação. O cliente mantém o conteúdo, mesmo quando o aplicativo já está instalado. Essa opção é útil em algumas implantações, como software baseado no Windows Installer. O Windows Installer precisa de uma cópia local do conteúdo de origem para aplicar as atualizações. Essa opção reduz o espaço disponível em cache. Se você selecionar essa opção, uma implantação grande poderá falhar futuramente se o cache não tiver espaço suficiente.  

- **Programa de instalação**: especifique o nome do programa de instalação e todos os parâmetros de instalação necessários.  

    - **A instalação é iniciada em**: opcionalmente, especifique a pasta que contém o programa de instalação para o tipo de implantação. Essa pasta pode ser um caminho absoluto no cliente ou um caminho para a pasta do ponto de distribuição que tem os arquivos de instalação.  

- **Desinstalar programa**: opcionalmente, especifique o nome do programa de desinstalação e os parâmetros necessários.  

    - **A desinstalação é iniciada em**: opcionalmente, especifique a pasta que contém o programa de desinstalação para o tipo de implantação. Essa pasta pode ser um caminho absoluto no cliente. Também pode ser um caminho relativo em um ponto de distribuição da pasta com o pacote.  

- **Reparar o programa**: opcionalmente, começando na versão 1810, para tipos de implantação do Windows Installer e o instalador de Script, especifique o nome do programa reparo e todos os parâmetros necessários.<!--1357866-->  

    - **Reparo inicia em**: opcionalmente, especifique a pasta que contém o programa de reparo para o tipo de implantação. Essa pasta pode ser um caminho absoluto no cliente. Também pode ser um caminho relativo em um ponto de distribuição da pasta com o pacote.  

- **Execute o programa de instalação e desinstalação como um processo de 32 bits em clientes de 64 bits**: use o arquivo de 32 bits e os locais de Registro em computadores Windows para executar o programa de instalação para o tipo de implantação.  


#### <a name="deployment-type-properties-content-options"></a>Opções de **Conteúdo** das propriedades do tipo de implantação
Quando você exibe as propriedades de um tipo de implantação, as opções a seguir aparecem somente na guia **Conteúdo**:

- **Configurações de conteúdo de desinstalação**:  

    - **Igual ao conteúdo de instalação**: se o conteúdo de instalação e desinstalação forem os mesmos, selecione essa opção. Essa opção é o padrão.  

    - **Sem conteúdo de desinstalação**: se o aplicativo não precisar de conteúdo para desinstalação, selecione essa opção.  

    - **Diferente do conteúdo da instalação**: se o conteúdo de desinstalação for diferente do conteúdo de instalação, selecione essa opção.  

        - **Local do conteúdo de desinstalação**: especifique o caminho de rede para o conteúdo que é usado para desinstalar o aplicativo.  

- **Permitir que os clientes usem pontos de distribuição do grupo de limites do site padrão**: especifique se os clientes devem baixar e instalar o software de um ponto de distribuição no grupo de limites do site padrão, quando o conteúdo não está disponível em um ponto de distribuição nos grupos de limites atuais ou vizinhos.  

- **Opções de implantação**: especifique se os clientes devem baixar o aplicativo ao usarem um ponto de distribuição de um vizinho ou os grupos de limites do site padrão.  

- **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações, confira [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache). Começando na versão 1802, o BranchCache está sempre habilitado nos clientes. Essa configuração foi removida, pois os clientes usam o BranchCache quando há suporte para ele no ponto de distribuição.  


### <a name="bkmk_dt-detect"></a> Opções de **Método de Detecção** do tipo de implantação   

Este procedimento configura um método de detecção que indica a presença do tipo de implantação. Em outras palavras, se o dispositivo Windows já tem o aplicativo instalado. Use um dos dois métodos a seguir para criar um método de detecção:  
- [Configurar regras para detectar a presença desse tipo de implantação](#bkmk_detect-rule)
- [Usar um script personalizado para detectar a presença desse tipo de implantação](#bkmk_detect-script)


#### <a name="bkmk_detect-rule"></a> Configurar regras para detectar a presença desse tipo de implantação

1.  Na página **Método de Detecção**, a opção para **Configurar regras para detectar a presença desse tipo de implantação** é selecionada por padrão. Clique em **Adicionar Cláusula**.  

2.  Na caixa de diálogo **Regra de Detecção**, clique na lista suspensa **Tipo de configuração**. Selecione um dos seguintes métodos para detectar a presença do tipo de implantação:  

    - **Sistema de Arquivos**: detecte se um arquivo ou uma pasta especificada existe em um dispositivo. Essa detecção indica que o aplicativo está instalado. Especifique os seguintes detalhes adicionais:  

        - **Tipo**: selecione se é um arquivo ou uma pasta.  

        - **Caminho** (obrigatório): insira ou navegue até o caminho local no dispositivo que inclui o arquivo ou a pasta. Por exemplo, `C:\Program Files`. Não é possível especificar um caminho de rede compartilhada. Se você clicar **Procurar**, procure o sistema de arquivos local ou conecte-se a um cliente representativo para procurar.  

        - **Nome do arquivo ou da pasta** (obrigatório): especifique o nome do arquivo ou da pasta específico a ser detectado no caminho acima. Se o cliente detectar esse arquivo ou pasta no dispositivo, ele considerará que o aplicativo está instalado no dispositivo.  

        - **Este arquivo ou pasta está associada com um aplicativo de 32 bits em sistemas de 64 bits**: essa opção é selecionada por padrão. O cliente verifica primeiro os locais de arquivo de 32 bits buscando o arquivo ou a pasta especificada. Se o arquivo ou a pasta não for encontrada, o cliente pesquisará nos locais de 64 bits.  

    - **Registro**: detecte se uma chave do Registro ou um valor de registro especificado existe em um dispositivo cliente. Essa detecção indica que o aplicativo está instalado. Especifique os seguintes detalhes adicionais:  

        - **Hive** (obrigatório): escolha um hive do Registro na lista suspensa. Por exemplo, `HKEY_LOCAL_MACHINE`.  

        - **Chave** (obrigatório): especifique a chave do Registro a ser pesquisada no hive acima. Por exemplo, `SOFTWARE\Microsoft\Office`.  

        - **Valor** (opcional): insira um valor específico a ser detectado na chave acima. Se você quiser que o cliente detecte o valor (padrão), habilite a opção para **Usar o valor de chave do Registro (padrão) para detecção**. Quando você inserir um valor ou habilitar essa opção, será necessário selecionar um **Tipo de Dados**.  

        - **Esta chave do Registro está associada a um aplicativo de 32 bits em sistemas de 64 bits**: selecione essa opção para verificar primeiro os locais do Registro de 32 bits buscando a chave do Registro especificada. Se a chave do Registro não for encontrada, o cliente pesquisará nos locais de 64 bits.  

    - **Windows Installer**: detecte se um arquivo do Windows Installer especificado existe em um dispositivo cliente. Essa detecção indica que o aplicativo está instalado. Especifique o **Código do produto** de MSI a ser detectado no cliente. Se você clicar em **Procurar**, selecione o arquivo MSI do qual o código do produto deve ser lido. 

3.  Na parte inferior da janela Regra de Detecção, especifique se o item precisa existir ou atender a uma regra. Por exemplo, se você detectar um arquivo, a seguinte opção será selecionada por padrão: **A configuração do sistema de arquivos precisa existir no sistema de destino para indicar a presença deste aplicativo**. Selecione a outra opção para criar uma regra de detecção com base nas propriedades do arquivo ou da pasta. Essas propriedades incluem a data de modificação, a data de criação, a versão ou o tamanho. Esses critérios de regra são diferentes para cada tipo de configuração.  

4.  Clique em **OK** para fechar a caixa de diálogo **Regra de Detecção**.  

Ao criar mais de um método de detecção para um tipo de implantação, crie uma lógica mais complexa agrupando as cláusulas. 

Continue na próxima seção sobre como usar um script personalizado como um método de detecção. Ou acesse as opções de [Experiência do Usuário](#bkmk_dt-ux) do tipo de implantação.


#### <a name="bkmk_detect-script"></a> Usar um script personalizado para verificar a presença de um tipo de implantação  

1.  Na página **Método de Detecção**, marque a caixa **Usar um script personalizado para verificar a presença de um tipo de implantação**. Em seguida, clique em **Editar**.  

2.  Na caixa de diálogo **Editor de Scripts**, clique na lista suspensa **Tipo de Script**. Selecione uma das linguagens de script a seguir para detectar o tipo de implantação: PowerShell, VBScript ou JScript.  

3.  Na caixa **Conteúdo do script**, insira o script que você deseja usar ou cole o conteúdo de um script existente. Escolha **Abrir** para navegar até um script existente salvo. Clique em **Limpar** para remover o texto no campo Conteúdo do script. Se necessário, habilite a opção para **Executar o script como um processo de 32 bits em clientes de 64 bits**.  

    > [!NOTE]  
    >  O tamanho máximo de um script é 32 KB.  

4.  Clique em **OK** para salvar o script e fechar a caixa de diálogo **Editor de Scripts**. Voltando ao assistente para Criar Tipo de Implantação, os campos **Tipo de Script** e **Tamanho do Script** são atualizados com detalhes sobre o seu script.   


#### <a name="about-custom-script-detection-methods"></a>Sobre os métodos de detecção de script personalizados  

O Configuration Manager verifica os resultados por meio do script. Ele lê os valores gravados pelo script no fluxo de saída padrão (STDOUT), no fluxo de erro padrão (STDERR) e no código de saída. Se o script for encerrado com um valor diferente de zero, ele falhará e o status de detecção do aplicativo será *Desconhecido*. Se o código de saída for zero e STDOUT tiver dados, o status de detecção do aplicativo será *Instalado*.

Use as tabelas a seguir para verificar na saída de um script se um aplicativo foi instalado:  

**Código de saída zero:**  
|STDOUT|STDERR|Resultado do script|Estado de detecção do aplicativo|
|---------|---------|---------|---------|
|Vazio|Vazio|Êxito|Não instalado|
|Vazio|Não está vazio|Falha|Desconhecida|
|Não está vazio|Vazio|Êxito|Instalado|
|Não está vazio|Não está vazio|Êxito|Instalado|


**Código de saída diferente de zero:**  
|STDOUT|STDERR|Resultado do script|Estado de detecção do aplicativo|
|---------|---------|---------|---------|
|Vazio|Vazio|Falha|Desconhecida|
|Vazio|Não está vazio|Falha|Desconhecida|
|Não está vazio|Vazio|Falha|Desconhecida|
|Não está vazio|Não está vazio|Falha|Desconhecida|


**Exemplos de VBScript**

Use os exemplos de VBScript a seguir para escrever seus próprios scripts de detecção de aplicativos:  

Exemplo 1: o script retorna um código de saída diferente de zero. Esse código indica que o script não foi executado com êxito. Nesse caso, o estado de detecção do aplicativo é desconhecido.  
``` VBScript
WScript.Quit(1)
```

Exemplo 2: o script retorna um código de saída igual a zero, mas o valor de STDERR não está vazio. Esse resultado indica que o script não foi executado com êxito. Nesse caso, o estado de detecção do aplicativo é desconhecido.  
``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

Exemplo 3: o script retorna um código de saída igual a zero, o que indica que ele foi executado com êxito. No entanto, o valor de STDOUT está vazio, o que indica que o aplicativo não está instalado.  
``` VBScript
WScript.Quit(0)
```

Exemplo 4: o script retorna um código de saída igual a zero, o que indica que ele foi executado com êxito. O valor de STDOUT não está vazio, o que indica que o aplicativo está instalado.  
``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

Exemplo 5: o script retorna um código de saída igual a zero, o que indica que ele foi executado com êxito. Os valores de STDOUT e STDERR não estão vazios, o que indica que o aplicativo está instalado.  
``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```


### <a name="bkmk_dt-ux"></a> Opções de **experiência de usuário** do tipo de implantação   

Essas configurações especificam como o cliente instala o aplicativo nos dispositivos e o que é visto pelo usuário.  

Na página **Experiência do Usuário** , especifique as seguintes informações:  

- **Comportamento da instalação**: na lista suspensa, escolha uma das seguintes opções:  

    - **Instalar para o usuário**: o cliente instala o aplicativo apenas para o usuário a quem você implanta o aplicativo.  

    - **Instalar para o sistema**: o cliente instala o aplicativo apenas uma vez. Ele está disponível para todos os usuários.  

    - **Instalar para o sistema se o recurso for dispositivo, caso contrário, instalar para o usuário**: se você implantar o aplicativo em um dispositivo, o cliente o instalará para todos os usuários. Se você implantar o aplicativo para um usuário, o cliente o instalará apenas para esse usuário.  

- **Requisito de logon**: selecione uma das seguintes opções:  

    - **Somente quando um usuário tiver efetuado logon**  

    - **Se um usuário tiver ou não efetuado logon**  

    - **Somente quando nenhum usuário tiver efetuado logon**  

    > [!NOTE]  
    >  Essa opção usa como padrão **Somente quando um usuário estiver conectado**. Se você selecionar **Instalar para o usuário** na lista suspensa **Comportamento da instalação**, não poderá alterar essa opção.  

- **Visibilidade do programa de instalação**: especifique o modo no qual o tipo de implantação é executado nos dispositivos cliente. Selecione uma das seguintes opções:  

    - **Maximizado**: o tipo de implantação é executado maximizado em dispositivos cliente. Os usuários veem todas as atividades de instalação.  

    - **Normal**: o tipo de implantação é executado no modo normal com base em padrões do sistema e do programa. Esse modo é o padrão.  

    - **Minimizado**: o tipo de implantação é executado minimizado em dispositivos cliente. Os usuários podem ver a atividade de instalação na área de notificação ou na barra de tarefas.  

    - **Oculto**: o tipo de implantação é executado no modo oculto nos dispositivos cliente. Os usuários não veem nenhuma atividade de instalação.  

- **Permitir que os usuários exibam e interajam com o programa de instalação**: especifique se um usuário pode interagir com a instalação do tipo de implantação para configurar as opções de instalação.  

    > [!NOTE]  
    >  Se você selecionar a opção **Instalar para o usuário** na lista suspensa **Comportamento da instalação**, essa opção estará habilitada por padrão.  

    > [!IMPORTANT]  
    > Começando na versão 1802, quando você seleciona o comportamento **Instalar para o sistema**, essa configuração é opcional. Essa alteração existe principalmente para permitir que um usuário final interaja com a instalação durante uma sequência de tarefas. Por exemplo, para executar um processo de instalação que solicita ao usuário final que escolha várias opções. Alguns instaladores de aplicativos não podem silenciar os prompts de usuário ou o processo de instalação pode exigir valores de configuração específicos conhecidos apenas pelo usuário. <!--1356976-->  
    >  
    > A instalação no contexto do sistema e a permissão para os usuários interagirem com a instalação não é uma configuração segura. Para obter mais informações, consulte [Segurança e privacidade do gerenciamento de aplicativos](/sccm/apps/plan-design/security-and-privacy-for-application-management#bkmk_interact).  

- **Máximo de tempo de execução permitido (minutos)**: especifique o tempo máximo em minutos em que você espera que o tipo de implantação seja executado no computador cliente. Especifique essa configuração como um número inteiro maior que zero. O valor padrão é 120 minutos (duas horas).  

    Use esse valor para as seguintes ações:  

    - Monitorar os resultados do tipo de implantação.  

    - Para verificar se um tipo de implantação está instalado ao definir as janelas de manutenção nos dispositivos clientes. Quando uma janela de manutenção está ativa, um tipo de implantação será iniciado somente se houver tempo suficiente disponível na janela de manutenção para acomodar a configuração **Máximo tempo de execução permitido**.  

    > [!IMPORTANT]  
    >  Um conflito poderá ocorrer se o **Tempo de execução máximo permitido** for maior do que a janela de manutenção agendada. Se o usuário definir o tempo de execução máximo com um período superior ao tamanho de qualquer janela de manutenção disponível, esse tipo de implantação não será executado.  

- **Tempo estimado para instalação (minutos)**: especifique o tempo estimado para a instalação do tipo de implantação. Os usuários veem esse tempo no Centro de Software.  


#### <a name="deployment-type-properties-user-experience-options"></a>Opções de **Experiência do Usuário** das propriedades do tipo de implantação
Quando você exibe as propriedades de um tipo de implantação, as opções a seguir são exibidas somente na guia **Experiência do Usuário**:

Impor um comportamento de pós-instalação específico. Selecione uma das seguintes opções:  

- **Determinar o comportamento com base em códigos de retorno**: manipule as reinicializações com base nos códigos configurados na guia [Códigos de Retorno](#bkmk_dt-return). O Centro de Software exibe **Pode Exigir uma Reinicialização**. Se um usuário estiver conectado durante a instalação, ele receberá avisos, dependendo da configuração de Experiência do Usuário *da implantação*.  

- **Nenhuma ação específica**: nenhuma reinicialização é necessária após a instalação. O Centro de Software relata que nenhuma reinicialização é necessária.  

- **O programa de instalação do software pode forçar uma reinicialização do dispositivo**: o Configuration Manager não controla nem inicia uma reinicialização, mas a instalação real pode fazer isso sem aviso. Use essa configuração para impedir que o Configuration Manager relate falha de instalação quando o instalador inicia uma reinicialização. O Centro de Software exibe **Pode Exigir uma Reinicialização**.  

- **O cliente do Configuration Manager forçará uma reinicialização obrigatória do dispositivo**: o Configuration Manager força uma reinicialização do dispositivo após uma instalação bem-sucedida. O Centro de Software relata que uma reinicialização é necessária. Se um usuário estiver conectado durante a instalação, ele receberá avisos, dependendo da configuração de Experiência do Usuário *da implantação*.  


### <a name="bkmk_dt-require"></a> **Requisitos** do tipo de implantação

Antes de instalar o tipo de implantação, o Configuration Manager verifica esses requisitos nos dispositivos. Use os requisitos para refinar e controlar ainda mais os dispositivos ou usuários que recebem esse aplicativo. Por exemplo, se você implantar o aplicativo em uma coleção de usuários, especifique os requisitos de hardware do aplicativo aqui. 

1.  Na página **Requisitos**, clique em **Adicionar** para abrir a caixa de diálogo **Criar Requisito**.  

2.  Na lista suspensa **Categoria**, selecione se esse requisito refere-se a um **Dispositivo** ou a um **Usuário**.  

    Selecione **Personalizado** para usar uma condição global criada anteriormente. Ao selecionar **Personalizar**, você também pode escolher **Criar** para criar uma nova condição global. Para obter mais informações sobre condições globais, consulte [Como criar condições globais no Configuration Manager](/sccm/apps/deploy-use/create-global-conditions).  

    > [!IMPORTANT]  
    >  Se você implantar o aplicativo em uma coleção de dispositivos, o cliente ignorará os requisitos da categoria **Usuário** e a condição **Dispositivo Primário**.  

3.  Na lista suspensa **Condição**, selecione a condição para avaliar se o usuário ou o dispositivo atende aos requisitos de instalação. O conteúdo dessa lista varia de acordo com a categoria selecionada.  

4.  Na lista suspensa **Operador**, selecione o operador a ser usado. Esse operador compara a condição selecionada com o valor especificado. Ele avalia se o usuário ou o dispositivo atende ao requisito de instalação. Os operadores disponíveis variam dependendo da condição selecionada.  

    > [!Note]  
    >  Os requisitos disponíveis variam de acordo com o tipo de dispositivo utilizado pelo tipo de implantação.  

5.  Na caixa **Valor**, especifique os valores a serem usados para comparação. Esses valores, junto com a condição e o operador selecionados, avaliam se o usuário ou o dispositivo atende aos requisitos de instalação. Os valores disponíveis variam de acordo com a condição e o operador selecionados.  

6.  Escolha **OK** para salvar o requisito e feche a caixa de diálogo **Criar Requisito**.  


### <a name="bkmk_dt-depend"></a> **Dependências** do tipo de implantação  

As dependências definem um ou mais tipos de implantação de outro aplicativo que o cliente precisa instalar antes de instalar esse tipo de implantação.   

> [!IMPORTANT]  
>  Em alguns casos, um tipo de implantação é dependente de um tipo de implantação que também tem dependências. O número máximo de dependências com suporte na cadeia é cinco.  

1.  Na página **Dependências**, clique em **Adicionar**.  

2.  Na janela Adicionar Dependência, insira o **Nome do grupo de dependência**. Esse nome refere-se a esse grupo de dependências do aplicativo.  

3.  Na janela Adicionar Dependência, clique em **Adicionar**.  

4.  Na janela **Especificar Aplicativo Necessário**, selecione um aplicativo disponível e pelo menos um de seus tipos de implantação a serem usados como uma dependência.  

    > [!TIP]  
    >  Clique em **Exibir** para exibir as propriedades do aplicativo selecionado ou do tipo de implantação.  

5.  Clique em **OK** para fechar a janela **Especificar Aplicativo Necessário**.  

6.  Se você quiser que o cliente instale o aplicativo dependente automaticamente, selecione **Instalação Automática** ao lado da dependência.  

    > [!NOTE]  
    >  Você não precisa implantar um aplicativo dependente para o cliente para instalá-lo automaticamente.  

7.  Se você adicionar mais de uma dependência, use os botões **Aumentar Prioridade** e **Diminuir Prioridade**. Essas ações alteram a ordem na qual o cliente avalia cada dependência.  

8.  Clique em **OK** para fechar a janela **Adicionar Dependência**.  


### <a name="bkmk_dt-return"></a> **Códigos de Retorno** do tipo de implantação

> [!Note]  
> Esta página não está no assistente para Criar Tipo de Implantação. Ela é uma guia apenas nas propriedades de um tipo de implantação existente.  

Especifique os códigos de retorno para controlar os comportamentos depois que o tipo de implantação for concluído. Por exemplo, sinalizar que uma reinicialização é necessária, que a instalação foi concluída ou personalizar o texto mostrado aos usuários. 

1. Na guia **Códigos de Retorno** da janela Propriedades do tipo de implantação, clique em **Adicionar**.  

2. Na janela Adicionar Código de Retorno, especifique o **Valor do Código de Retorno** que você espera desse tipo de implantação. Esse valor é qualquer inteiro positivo ou negativo entre `-2147483648` e `2147483647`.  

3. Selecione uma **Tipo de Código** na lista suspensa. Essa configuração define como o Configuration Manager interpreta o código de retorno especificado desse tipo de implantação. Os tipos disponíveis variam com base na tecnologia do tipo de implantação.   

    - **Êxito (sem reinicialização)**: o tipo de implantação foi instalado com êxito e não é necessário reinicializar.  

    - **Falha (sem reinicialização)**: o tipo de implantação não foi instalado.  

    - **Reinicialização Forçada**: o tipo de implantação foi instalado com êxito, mas requer que o dispositivo seja reiniciado. Nada mais poderá ser instalado até que o dispositivo seja reiniciado.  

    - **Reinicialização Suave**: o tipo de implantação foi instalado com êxito, mas solicita que o dispositivo seja reiniciado. Outras instalações podem ocorrer antes que o dispositivo seja reiniciado.    

    - **Repetição Rápida**: outra instalação já está em andamento no dispositivo. O cliente tentará novamente a cada duas horas, até o total de 10 vezes.  

4. Opcionalmente, insira um **Nome** e uma **Descrição** para esse código de retorno. Esse texto é exibido ao usuário.  

5. Clique em **OK** para fechar a janela Adicionar Código de Retorno.  


#### <a name="example-non-zero-success"></a>Exemplo: êxito para diferente de zero
Você está implantando um aplicativo que retorna um código de saída `1` quando é instalado com êxito. Por padrão, o Configuration Manager detecta esse código de retorno diferente de zero como uma falha. Especifique o Valor do Código de Retorno como `1` e selecione o Tipo de Código **Êxito (sem reinicialização)**. Agora o Configuration Manager interpreta esse código de retorno como êxito para esse tipo de implantação.


#### <a name="default-return-codes"></a>Códigos de retorno padrão
Quando você cria alguns tipos de implantação, o Configuration Manager adiciona automaticamente os códigos de retorno a seguir, que são comuns para essa tecnologia:  

**Windows Installer (arquivo \*.msi)**  
|Valor    |Tipo de código|
|---------|---------|
|0        |Êxito (sem reinicialização)|
|1707     |Êxito (sem reinicialização)|
|3010     |Reinicialização Suave|
|1641     |Reinicialização Forçada|
|1618     |Repetição Rápida|

**Instalador de Script**  
|Valor    |Tipo de código|
|---------|---------|
|0        |Êxito (sem reinicialização)|
|1641     |Reinicialização Forçada|
|3010     |Reinicialização Suave|
|1618     |Repetição Rápida|

**Pacote do aplicativo do Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)**  
|Valor    |Tipo de código|
|---------|---------|
|15605    |Repetição Rápida|
|15618    |Repetição Rápida|



## <a name="bkmk_appv"></a> Opções adicionais para tipos de implantação App-V  

Configure opções adicionais que são exclusivas para tipos de implantação App-V (aplicativos virtuais).  

### <a name="bkmk_appv-content"></a> Opções de **Conteúdo** do tipo de implantação App-V  

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Aplicativos**.  

2.  Selecione um aplicativo com um tipo de implantação App-V e, em seguida, clique em **Propriedades**.  

3.  Nas propriedades do aplicativo, mude para a guia **Tipos de Implantação**. Selecione o tipo de implantação App-V e, em seguida, clique em **Editar**.  

4.  Nas propriedades do tipo de implantação, mude para a guia **Conteúdo**. Configure as opções a seguir conforme o necessário:  

    -   **Manter o conteúdo no cache do cliente**: o cliente do Configuration Manager não excluirá do seu cache o conteúdo desse tipo de implantação.  

    -   **Carregar conteúdo no cache do App-V antes de iniciar**: antes que o aplicativo seja iniciado, o cliente do Configuration Manager carrega no cache do App-V todo o conteúdo desse tipo de implantação. O cliente não fixa o conteúdo no cache. Ele exclui o conteúdo conforme o necessário.  

5.  Clique em **OK** para fechar as propriedades do tipo de implantação. Em seguida, clique em **OK** para fechar as propriedades do aplicativo.  


### <a name="bkmk_appv-pub"></a> Opções de **Publicação** do tipo de implantação App-V   

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Aplicativos**.  

2.  Selecione um aplicativo com um tipo de implantação App-V e, em seguida, clique em **Propriedades**.  

3.  Nas propriedades do aplicativo, mude para a guia **Tipos de Implantação**. Selecione o tipo de implantação App-V e, em seguida, clique em **Editar**.  

4.  Nas propriedades do tipo de implantação, mude para a guia **Publicação**. Selecione os itens no aplicativo virtual que você deseja publicar.  

5.  Clique em **OK** para fechar as propriedades do tipo de implantação. Em seguida, clique em **OK** para fechar as propriedades do aplicativo.  



## <a name="bkmk_import"></a> Importar um aplicativo  

Use o procedimento a seguir para importar um aplicativo no Configuration Manager: 

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Aplicativos**.   

2.  Na faixa de opções, na guia **Início** e no grupo **Criar**, clique em **Importar Aplicativo**.  

3.  Na página **Geral** do Assistente para Importação de Aplicativo, especifique o caminho de rede do **Arquivo** a ser importado. Por exemplo, `\\server\share\file.zip`. Esse é um arquivo compactado válido (formato ZIP) de um aplicativo do Configuration Manager exportado.  

4.  Na página **Conteúdo do Arquivo**, selecione a ação a ser tomada se esse aplicativo for uma cópia de um aplicativo existente. Crie um aplicativo ou ignore a cópia e adicione uma nova revisão do aplicativo existente.  

5.  Na página **Resumo**, examine as ações e conclua o assistente.  

O novo aplicativo aparece no nó **Aplicativos**.  

> [!TIP]  
>  O cmdlet do Windows PowerShell **Import-CMApplication** tem a mesma função que esse procedimento. Para obter mais informações, consulte [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  

Para obter mais informações de como exportar um aplicativo, consulte [Tarefas de gerenciamento de aplicativos](/sccm/apps/deploy-use/management-tasks-applications). 



## <a name="bkmk_deploy-types"></a> Tipos de implantação com suporte  

O Configuration Manager dá suporte aos seguintes tipos de implantação de aplicativos:

| Nome do tipo de implantação | Descrição |   
|--------------------------|----------------------|  
| **Windows Installer (arquivo \*.msi)** | Um arquivo do Windows Installer. |  
| **Pacote do aplicativo do Windows (\*.appx, \*.appxbundle)** | Para o Windows 8 ou posteriores. Selecione um arquivo de pacote do aplicativo do Windows ou um pacote do lote de aplicativo do Windows. |  
| **Pacote do aplicativo do Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** | Começando na versão 1806, para os novos formatos pacote do aplicativo (.msix) e lote de aplicativo (.msixbundle) do Windows 10. Selecione um arquivo de pacote do aplicativo do Windows ou um pacote do lote de aplicativo do Windows.<!--1357427--> |  
| **Pacote do aplicativo do Windows (na Windows Store)** | Para o Windows 8 ou posteriores. Especifique um link para o aplicativo na Windows Store ou procure o repositório para selecionar o aplicativo.<sup>[Observação 1](#bkmk_note1)</sup> |  
| **Instalador de Script** | Especifique um script ou programa que é executado em clientes Windows para instalar conteúdo ou executar uma ação. Use esse tipo de implantação para instaladores setup.exe ou wrappers de script. |  
| **Microsoft Application Virtualization 4** | Um manifesto do Microsoft App-V v4. |  
| **Microsoft Application Virtualization 5** | Um arquivo de pacote do Microsoft App-V v5. |  
| **Pacote do aplicativo do Windows Phone (arquivo \*.xap)** | Um arquivo de pacote do aplicativo do Windows Phone. |  
| **Pacote do aplicativo do Windows Phone (na Loja do Windows Phone)** | Especifique um link para o aplicativo na Windows Store. |  
| **Pacote de aplicativo para iOS (\*arquivo .ipa)** | Um arquivo de pacote do aplicativo do iOS da Apple. |  
| **Pacote de aplicativo para iOS da App Store** | Especifique um link para o aplicativo iOS na Apple Store. |  
| **Pacote do aplicativo para Android (arquivo \*.apk)** | Um arquivo de pacote do aplicativo Android. |  
| **Pacote do aplicativo para Android no Google Play** | Especifique um link para o aplicativo na Google Play Store. |  
| **Mac OS X** | Para computadores macOS que executam o cliente do Configuration Manager. Crie um arquivo .cmmac com a ferramenta **CMAppUtil**. |  
| **Aplicativo Web** | Especifique um link para um aplicativo Web. Esse tipo de implantação instala um atalho para o aplicativo Web no dispositivo do usuário.<sup>[Observação 2](#bkmk_note2)</sup> |  
| **Windows Installer por meio do MDM (\*.msi)** | Crie e implante aplicativos baseados no Windows Installer em dispositivos Windows 10. Para obter mais informações, confira [Implantar aplicativos do Windows Installer em dispositivos Windows 10 registrados no MDM](/sccm/apps/get-started/creating-windows-applications#bkmk_mdm-msi). |  

#### <a name="bkmk_note1"></a> Observação 1: pacote do aplicativo do Windows (na Windows Store)
Para implantar o aplicativo como um link para a Windows Store, configure a política de grupo **Desligar o aplicativo Store**. Defina essa política como **Desabilitada** ou **Não Configurada**. Se você habilitar essa configuração, os clientes não poderão se conectar à Windows Store para baixar e instalar aplicativos.

Os clientes do Windows sempre avaliam os tipos de implantação que usam um link para um repositório antes de outros tipos de implantação. Em seguida, o cliente avalia os tipos de implantação por prioridade. 

#### <a name="bkmk_note2"></a> Observação 2: aplicativo Web  
Se você instalou o navegador gerenciado do Microsoft Intune em dispositivos iOS ou Android, verifique se os usuários podem usar somente o navegador gerenciado para abrir o aplicativo. No endereço do site, substitua **http** por **http-intunemam** ou **https** por **https-intunemam**. Por exemplo: 
- `http-intunemam://<path to web app>`
- `https-intunemam://<path to web app>`

Use os [requisitos do aplicativo](#bkmk_dt-require) do Configuration Manager para assegurar que os aplicativos Web que usam o navegador gerenciado sejam instalados apenas em dispositivos iOS e Android. 

Para obter mais informações sobre o navegador gerenciado do Intune, confira [Gerenciar o acesso à Internet usando políticas de navegador gerenciado](/sccm/apps/deploy-use/manage-internet-access-using-managed-browser-policies).



## <a name="next-steps"></a>Próximas etapas

Depois de criar um aplicativo no Configuration Manager, a próxima etapa é [implantá-lo](/sccm/apps/deploy-use/deploy-applications).

Para obter mais informações sobre a criação de aplicativos em diferentes plataformas de sistema operacional, confira os seguintes artigos:  
- [Criar aplicativos do Windows](/sccm/apps/get-started/creating-windows-applications)
- [Criar aplicativos para dispositivos móveis](/sccm/mdm/deploy-use/create-applications) (iOS, Windows Mobile e Android)  
- [Criar aplicativos para Mac](/sccm/apps/get-started/creating-mac-computer-applications)
- [Criar aplicativos de servidores Linux e UNIX](/sccm/apps/get-started/creating-linux-and-unix-server-applications)
- [Criar aplicativos Windows Embedded](/sccm/apps/get-started/creating-windows-embedded-applications)

