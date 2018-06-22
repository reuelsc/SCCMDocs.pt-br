---
title: Criar aplicativos
titleSuffix: Configuration Manager
description: Crie aplicativos com tipos de implantação, métodos de detecção e requisitos para instalação do software.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9b90dfcc0916f62905af777e45222ceebf8300f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341859"
---
# <a name="create-applications-with-system-center-configuration-manager"></a>Criar aplicativos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um aplicativo do Configuration Manager tem um ou mais tipos de implantação. Esses tipos de implantação incluem os arquivos de instalação e as informações necessárias para instalação do software em dispositivos. Um tipo de implantação também tem regras, como métodos de detecção e requisitos, que especificam quando e como o cliente instala o software.  

 Crie aplicativos usando os seguintes métodos:  

-   Crie automaticamente os aplicativos e tipos de implantação, lendo os arquivos de instalação do aplicativo.  

-   Crie manualmente o aplicativo e adicione tipos de implantação posteriormente.  

-   Importe um aplicativo de um arquivo.  

> [!NOTE]  
>  Para obter informações detalhadas sobre como criar aplicativos iOS, Windows Phone e Android, consulte [Criar aplicativos para dispositivos móveis](../../mdm/deploy-use/create-applications.md).  



## <a name="start-the-create-application-wizard"></a>Iniciar o assistente para criar aplicativo  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Aplicativo**.  



## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>Especifique se deseja detectar automaticamente ou definir manualmente as informações do aplicativo  

-   Detecte automaticamente as informações do aplicativo para criar um aplicativo básico com um único tipo de implantação. Por exemplo, um arquivo do Windows Installer sem dependências nem requisitos. Criado o aplicativo com esse procedimento, você pode editá-lo conforme necessário para adicionar ou alterar os tipos de implantação e adicionar métodos de detecção, dependências ou requisitos.  

-   Especifique manualmente as informações do aplicativo para criar aplicativos mais complexos e com vários tipos de implantação, dependências, métodos de detecção ou requisitos.  

### <a name="automatically-detect-application-information"></a>Detectar automaticamente as informações do aplicativo  

1.  Na página **Geral** do Assistente para Criar Aplicativo, selecione **Detectar automaticamente informações sobre este aplicativo em arquivos de instalação**.  

2.  Na lista suspensa **Tipo** , selecione o tipo de arquivo de instalação do aplicativo que deseja usar para detectar as informações do aplicativo. Para obter informações sobre os tipos de instalação disponíveis, consulte [Tipos de implantação com suporte do Configuration Manager](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) neste tópico.  

3.  Na caixa **Local**, especifique o caminho UNC (no formato *\\\\servidor\\compartilhamento\\\nome do arquivo*) ou o link do repositório para o arquivo de instalação do aplicativo que você deseja usar para detectar informações do aplicativo. Como alternativa, clique em **Procurar** para localizar o arquivo de instalação.  

    > [!IMPORTANT]  
    >  Quando você seleciona **Windows Installer (\*arquivo. msi)** como um tipo de aplicativo, todos os arquivos na pasta especificada são importados e enviados aos pontos de distribuição. Verifique se a pasta especificada contém apenas os arquivos necessários instalar o aplicativo. O Configuration Manager foi testado para dar suporte a até 20.000 arquivos de aplicativo no pacote do aplicativo. Se o aplicativo tiver mais arquivos, considere a criação de vários aplicativos com um número menor de arquivos.  

    >  É necessário ter acesso ao caminho UNC que contém o aplicativo e a todas as subpastas que incluem o conteúdo do aplicativo.  

4.  Na página **Importar Informações** do Assistente para Criar Aplicativo, examine as informações que foram importadas e, em seguida, escolha **Avançar**. Caso seja necessário, escolha **Anterior** para voltar e corrigir quaisquer erros.  

5.  Na página **Informações Gerais** do Assistente para Criar Aplicativo, especifique as seguintes informações:  

    > [!NOTE]  
    >  Se o Configuration Manager detectar automaticamente essas informações dos arquivos de instalação do aplicativo, elas já estarão populadas aqui. Além disso, as opções exibidas podem ser diferentes dependendo do tipo de aplicativo que você criar.  

    -   Informações gerais sobre o aplicativo, como o nome do aplicativo, comentários e versão. Para ajudá-lo a encontrar o aplicativo no console do Configuration Manager, especifique uma referência opcional.  

    -   **Programa de instalação**: especifique o programa de instalação e as propriedades necessárias para instalar o tipo de implantação do aplicativo.  

        > [!TIP]  
        >  Se o programa de instalação não for exibido, escolha **Procurar** e procure o local do programa de instalação.  

    -   **Comportamento da instalação**: especifique se o tipo de implantação do aplicativo é instalado somente para o usuário conectado no momento ou para todos os usuários. Uma terceira opção é instalar para todos os usuários se ele é implantado em um dispositivo ou somente para um usuário específico se ele é implantado em um usuário.  

    -   **Use uma conexão VPN automática (se configurada)**: Se um perfil VPN tiver sido implantado para o dispositivo no qual o aplicativo é iniciado, inicie a conexão VPN quando o aplicativo for iniciado (somente Windows 8.1 e Windows Phone 8.1).  

         Em dispositivos Windows Phone 8.1, não há suporte para conexões VPN automáticas se mais de um perfil de VPN é implantado no dispositivo.  

         Para obter mais informações, consulte [Perfis de VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Escolha **Avançar**, examine as informações do aplicativo na página **Resumo** e, em seguida, conclua o Assistente para Criar Aplicativo.  

O novo aplicativo aparece no nó **Aplicativos** no console do Configuration Manager e você concluiu o processo de criação de aplicativo. Se quiser adicionar mais tipos de implantação ao aplicativo, consulte [Criar tipos de implantação para o aplicativo](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) neste tópico.  

### <a name="manually-specify-application-information"></a>Especificar manualmente as informações do aplicativo  

1.  Na página **Geral** do Assistente para Criar Aplicativo, selecione **Especificar manualmente as informações do aplicativo** e escolha **Avançar**.  

2.  Especifique informações gerais sobre o aplicativo, como o nome do aplicativo, comentários e versão. Para ajudá-lo a encontrar o aplicativo no console do Configuration Manager, especifique uma referência opcional.  

3.  Na página **Catálogo de Aplicativos** do Assistente para Criar Aplicativo, especifique as seguintes informações:  

    -   **Idioma selecionado**: na lista suspensa, selecione a versão de idioma do aplicativo que deseja configurar. Escolha **Adicionar/Remover** para configurar mais idiomas para esse aplicativo.  

    -   **Nome do aplicativo localizado**: especifique o nome do aplicativo no idioma que você selecionou na lista suspensa **Idioma selecionado** .  

        > [!IMPORTANT]  
        >  Você deve especificar um nome de aplicativo localizado para cada versão do idioma configurado.  

    -   **Categorias de usuário**: escolha **Editar** para especificar as categorias de aplicativo no idioma selecionada na lista suspensa **Idioma Selecionado**. Os usuários do Centro de Software podem usar essas categorias selecionadas para ajudar a filtrar e classificar os aplicativos disponíveis.  

    -   **Documentação do usuário**: escolha **Procurar** para especificar o local de um arquivo que os usuários do Centro de Software podem ler para obter mais informações sobre esse aplicativo. Esse local é uma URL ou um caminho de rede e nome de arquivo.

    -   **Texto do link**: especifique o texto que é exibido no lugar da URL do aplicativo.  

    -   **URL de Privacidade do Aplicativo**: especifique uma URL vinculada à política de privacidade para o aplicativo.  

    -   **Descrição localizada**: digite uma descrição para esse aplicativo no idioma que você selecionou na lista suspensa **Idioma selecionado** .  

    -   **Palavras-chave**: digite uma lista de palavras-chave no idioma que você selecionou na lista suspensa **Idioma selecionado** . Essas palavras-chave ajudam os usuários do Centro de Software a pesquisar o aplicativo.  

    -   **Ícone**: escolha **Procurar** para selecionar um ícone para esse aplicativo entre os ícones disponíveis. Se você não especificar um ícone, um ícone padrão será usado para esse aplicativo. Agora, você pode definir um ícone com dimensões de até 512 x 512 pixels.

    -   **Exibir como um aplicativo em destaque e realçá-lo no portal da empresa**: essa opção exibe o aplicativo em destaque no portal da empresa.  

4.  Na página **Tipos de Implantação** do Assistente para Criar Aplicativo, escolha **Adicionar** para criar um novo tipo de implantação.  

 Para obter mais informações, consulte [Criar tipos de implantação para o aplicativo](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application).  

5.  Escolha **Avançar**, examine as informações do aplicativo na página **Resumo** e, em seguida, conclua o Assistente para Criar Aplicativo.  

O novo aplicativo aparece no nó **Aplicativos** do console do Configuration Manager.  



##  <a name="create-deployment-types-for-the-application"></a>Criar tipos de implantação para o aplicativo  
 Se você detectar as informações do aplicativo automaticamente, talvez não precise concluir algumas das etapas destes procedimentos.  

### <a name="start-the-create-deployment-type-wizard"></a>Iniciar o assistente para criar tipo de implantação  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Selecione um aplicativo e, em seguida, na guia **Início**, no grupo **Aplicativo**, escolha **Criar Tipo de Implantação**.  

> [!TIP]  
>  Você também pode iniciar o Assistente para Criar Tipo de Implantação no Assistente para Criar Aplicativo e na guia **Tipos de Implantação** da caixa de diálogo **Propriedades** do *<nome do aplicativo\>*.  

### <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-set-up-the-information"></a>Especifique se deseja detectar automaticamente as informações do tipo de implantação ou configurar as informações manualmente  
 Use um dos procedimentos a seguir para detectar automaticamente ou definir manualmente as informações do tipo de implantação.  

#### <a name="automatically-detect-deployment-type-information"></a>Detectar automaticamente as informações do tipo de implantação  

1.  Na página **Geral** do Assistente para Criar Tipo de Implantação, selecione **Identificar automaticamente as informações sobre esse tipo de implantação nos arquivos de instalação**.  

2.  Na caixa **Tipo**, selecione o tipo de arquivo de instalação de aplicativo que deseja usar para detectar as informações do tipo de implantação.  

3.  Na caixa **Local**, especifique o caminho de rede ou o link do repositório para os arquivos de instalação do aplicativo. O Configuration Manager usa esses arquivos para detectar as informações de tipo de implantação. Você também pode escolher **Procurar** para localizar o arquivo de instalação.  

    > [!NOTE]  
    >  É necessário ter acesso ao caminho de rede que contém o aplicativo e a todas as subpastas que incluem o conteúdo do aplicativo.  

4.  Na página **Importar Informações** do Assistente para Criar Tipo de Implantação, examine as informações que foram importadas e escolha **Avançar**. Você também pode escolher **Anterior** para voltar e corrigir quaisquer erros.  

5.  Na página **Informações Gerais** do Assistente para Criar Tipo de Implantação, especifique as seguintes informações:  

    > [!NOTE]  
    >  Algumas das informações do tipo de implantação podem já estar presentes se elas tiverem sido lidas dos arquivos de instalação do aplicativo. Além disso, as opções exibidas podem variar, dependendo do tipo de implantação criado.  

    -   Informações gerais sobre o tipo de implantação, como nome, comentários do administrador e idiomas disponíveis.  

    -   **Programa de instalação**: especifique o programa de instalação e as propriedades que você precisa para instalar o tipo de implantação.  

    -   **Comportamento da instalação**: especifique se deseja instalar o tipo de implantação para o usuário atual ou para todos os usuários. Uma terceira opção é instalar para todos os usuários se ele é implantado em um dispositivo ou somente para um usuário específico se ele é implantado em um usuário.  

    -   **Use uma conexão VPN automática (se configurada)**: Se um perfil VPN tiver sido implantado para o dispositivo no qual o aplicativo é iniciado, inicie a conexão VPN quando o aplicativo for iniciado (somente Windows 8.1 e Windows Phone 8.1). Se vários perfis VPN foram implantados em um dispositivo Windows 8.1, o primeiro perfil VPN implantado será usado por padrão.  

         Em dispositivos Windows Phone 8.1, não há suporte para conexões VPN automáticas se mais de um perfil de VPN é implantado no dispositivo.  

         Para obter mais informações, consulte [Perfis de VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Escolha **Avançar** e continue para [Especificar as opções de conteúdo para o tipo de implantação](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

#### <a name="manually-set-up-the-deployment-type-information"></a>Configurar manualmente as informações do tipo de implantação  

1.  Na página **Geral** do assistente para Criar Tipo de Implantação, na lista suspensa **Tipo**, escolha o tipo de arquivo de instalação do aplicativo para esse tipo de implantação. 

2.  Selecione **Especificar manualmente as informações de tipo de implantação** e, em seguida, clique em **Avançar**.

3.  Na página **Informações Gerais** do Assistente para Criar Tipo de Implantação, especifique um nome para o tipo de implantação. Opcionalmente, especifique uma descrição e os idiomas para esse tipo de implantação e, em seguida, clique em **Avançar**.  

4.  Continuar para [Especificar as opções de conteúdo para o tipo de implantação](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

###  <a name="specify-content-options-for-the-deployment-type"></a>Especificar as opções de conteúdo para o tipo de implantação  

1.  Na página **Conteúdo** do Assistente para Criar Tipo de Implantação, especifique as seguintes informações:  

    -   **Local do conteúdo**: especifique o local do conteúdo para esse tipo de implantação ou selecione **Procurar** para escolher a pasta de conteúdo do tipo de implantação.  

        > [!IMPORTANT]  
        >  A Conta do Sistema do computador do servidor do site deve ter permissões ao local do conteúdo que você especifica.  

    -   **Desinstalar as configurações do conteúdo**: especifique uma das seguintes opções:
        - **Igual ao conteúdo de instalação**: se o conteúdo de instalação e desinstalação forem os mesmos, selecione essa opção. Essa opção é o padrão.
        - **Sem conteúdo de desinstalação**: se o aplicativo não precisar de conteúdo para desinstalação, selecione essa opção.
        - **Diferente do conteúdo da instalação**: se o conteúdo de desinstalação for diferente do conteúdo de instalação, selecione essa opção. Em seguida, especifique o local do conteúdo de aplicativo usado para desinstalar o aplicativo.
5. Clique em **OK** para fechar a caixa de diálogo Propriedades do tipo de implantação.

    -   **Persistir o conteúdo no cache do cliente**: selecione essa opção para especificar se o cliente retém o conteúdo no cache por tempo indeterminado. O cliente retém o conteúdo, mesmo se o aplicativo já está instalado. Essa opção é útil em algumas implantações, como software baseado no Windows Installer. O Windows Installer precisa de uma cópia local do conteúdo de origem para aplicar as atualizações. Apesar disso, essa opção reduz o espaço disponível em cache. Selecionar essa opção pode causar uma falha em uma implantação grande posteriormente se o cache não tiver espaço suficiente.  

    -   **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: para reduzir a carga na rede, selecione essa opção. Os clientes baixam o conteúdo de outros clientes locais na rede que já baixaram e armazenaram o conteúdo em cache. Essa opção utiliza a tecnologia Windows BranchCache.  

    -   **Programa de instalação**: especifique o nome do programa de instalação e os parâmetros de instalação necessários ou escolha **Procurar** para localizar o arquivo de instalação.  

    -   **A instalação é iniciada em**: opcionalmente, especifique a pasta que contém o programa de instalação para o tipo de implantação. Essa pasta pode ser um caminho absoluto no cliente ou um caminho para a pasta do ponto de distribuição que contém os arquivos de instalação.  

    -   **Desinstalar programa**: opcionalmente, especifique o nome do programa de desinstalação e os parâmetros necessários ou escolha **Procurar** para localizá-lo.  

    -   **A desinstalação é iniciada em**: opcionalmente, especifique a pasta que contém o programa de desinstalação para o tipo de implantação. Essa pasta pode ser um caminho absoluto no cliente. Também pode ser um caminho relativo em um ponto de distribuição da pasta com o pacote.  

    -   **Execute o programa de instalação e desinstalação como um processo de 32 bits em clientes de 64 bits**: use o arquivo de 32 bits e os locais de Registro em computadores Windows para executar o programa de instalação para o tipo de implantação.  

2.  Escolha **Próxima**.  

### <a name="set-up-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>Configurar métodos de detecção para indicar a presença do tipo de implantação (somente computadores Windows)  
 Este procedimento configura um método de detecção que indica se o tipo de implantação já está instalado.  

1.  Na página **Método de Detecção** do Assistente para Criar Tipo de Implantação, selecione **Configurar regras para detectar a presença desse tipo de implantação** e escolha **Adicionar Cláusula**.  

    > [!NOTE]  
    >  Você também pode selecionar **Usar um script personalizado para detectar a presença desse tipo de implantação**. Para obter mais informações, consulte [Usar um script personalizado para verificar a presença de um tipo de implantação](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type).  

2.  Na caixa de diálogo **Regra de Detecção**, na lista suspensa **Tipo de configuração**, selecione o método que você quer usar para detectar a presença do tipo de implantação. Você pode escolher entre os seguintes métodos disponíveis:  

    -   **Sistema de Arquivos**: detecte se uma pasta ou um arquivo especificado existe em um dispositivo cliente. Essa detecção indica que o aplicativo está instalado.  

        > [!NOTE]  
        >  O tipo de configuração **Sistema de arquivos** não dá suporte à especificação de um caminho UNC para um compartilhamento de rede no campo Caminho. Você só pode especificar um caminho local no dispositivo do cliente.  
        >   
        >  Para verificar os locais de arquivo de 32 bits para a pasta ou o arquivo especificado, primeiro selecione a opção **Esta pasta ou este arquivo está associado a um aplicativo de 32 bits em sistemas de 64 bits**. Se a pasta ou o arquivo não for encontrado, locais de 64 bits serão pesquisados.  

    -   **Registro**: detecte se uma chave do Registro ou um valor de registro especificado existe em um dispositivo cliente. Essa detecção indica que o aplicativo está instalado.  

        > [!NOTE]  
        >  Para verificar locais de registro de 32 bits para a chave do Registro especificada, primeiro selecione a opção **Esta chave do Registro está associada a um aplicativo de 32 bits em sistemas de 64 bits**. Se a chave do Registro não for encontrada, os locais de 64 bits serão pesquisados.  

    -   **Windows Installer**: detecte se um arquivo do Windows Installer especificado existe em um dispositivo cliente. Essa detecção indica que o aplicativo está instalado.  

3.  Especifique detalhes sobre o item a ser detectado se esse tipo de implantação for instalado. Por exemplo, você pode usar um arquivo, uma pasta, uma chave do Registro ou um valor de Registro, ou um código de produto do Windows Installer.  

4.  Especifique se o item deve existir ou atender a uma regra. Por exemplo, se você detectar um arquivo, selecione **A configuração do sistema de arquivos deve existir no sistema de destino para indicar a presença deste aplicativo**.  

5.  Escolha **Avançar** para fechar a caixa de diálogo **Regra de Detecção**.  

####  <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a>Use um script personalizado para verificar a presença de um tipo de implantação  

1.  Na página **Método de Detecção** do Assistente para Criar Tipo de Implantação, selecione a caixa **Usar um script personalizado para detectar a presença desse tipo de implantação** e, em seguida, escolha **Editar**.  

2.  Na caixa de diálogo **Editor de Scripts**, na lista suspensa **Tipo de script** selecione a linguagem de script que você quer usar para detectar o tipo de implantação.  

3.  Na caixa **Conteúdo de script**, insira o script que deseja usar. Você também pode colar o conteúdo de um script existente nesse campo ou escolher **Abrir** para procurar um script salvo existente. O Configuration Manager verifica os resultados por meio do script. Ele lê os valores gravados pelo script no fluxo de saída padrão (STDOUT), no fluxo de erro padrão (STDERR) e no código de saída. Se o script for encerrado com um valor diferente de zero, o script falhará e o status de detecção do aplicativo será desconhecido. Se o código de saída for zero e STDOUT tiver dados, o status de detecção do aplicativo será Instalado.  

 Use a seguinte tabela para verificar se um aplicativo está instalado por meio da saída de um script:  

|Código de saída do script|Detalhes|
|--------------------------------|-----------------|
|0|**Dados lidos de STDOUT**: vazio<br /><br /> **Dados lidos de STDERR**: vazio<br /><br /> **Resultado do script**: êxito<br /><br /> **Estado de detecção do aplicativo**: não instalado|  
|0|**Dados lidos de STDOUT**: vazio<br /><br /> **Dados lidos de STDERR**: não vazio<br /><br /> **Resultado do script**: falha<br /><br /> **Estado de detecção do aplicativo**: desconhecido|  
|0|**Dados lidos de STDOUT**: não vazio<br /><br /> **Dados lidos de STDERR**: vazio<br /><br /> **Resultado do script**: êxito<br /><br /> **Estado de detecção do aplicativo**: instalado|  
|0|**Dados lidos de STDOUT**: não vazio<br /><br /> **Dados lidos de STDERR**: não vazio<br /><br /> **Resultado do script**: êxito<br /><br /> **Estado de detecção do aplicativo**: instalado|  
|Valor diferente de zero|**Dados lidos de STDOUT**: vazio<br /><br /> **Dados lidos de STDERR**: vazio<br /><br /> **Resultado do script**: falha<br /><br /> **Estado de detecção do aplicativo**: desconhecido|  
|Valor diferente de zero|**Dados lidos de STDOUT**: vazio<br /><br /> **Dados lidos de STDERR**: não vazio<br /><br /> **Resultado do script**: falha<br /><br /> **Estado de detecção do aplicativo**: desconhecido|  
|Valor diferente de zero|**Dados lidos de STDOUT**: não vazio<br /><br /> **Dados lidos de STDERR**: vazio<br /><br /> **Resultado do script**: falha<br /><br /> **Estado de detecção do aplicativo**: desconhecido|  
|Valor diferente de zero|**Dados lidos de STDOUT**: não vazio<br /><br /> **Dados lidos de STDERR**: não vazio<br /><br /> **Resultado do script**: falha<br /><br /> **Estado de detecção do aplicativo**: desconhecido|  

A tabela a seguir apresenta scripts de exemplo do Microsoft VB (Visual Basic) que você pode usar para gravar seus próprios scripts de detecção de aplicativo.  

|Script de exemplo do Visual Basic|Descrição|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|O script retorna um código de saída que não é zero, o que indica que ele não foi executado com êxito. Nesse caso, o estado de detecção do aplicativo é desconhecido.|  
|**WScript.StdErr.Write "Falha de script"**<br /><br /> **WScript.Quit(0)**|O script retorna um código de saída zero, mas o valor de STDERR não está vazio. Esse resultado indica que o script não foi executado com êxito. Nesse caso, o estado de detecção do aplicativo é desconhecido.|  
|**WScript.Quit(0)**|O script retorna um código de saída igual a zero, o que indica que ele foi executado com êxito. No entanto, o valor para STDOUT está vazio, que indica que o aplicativo não está instalado.|  
|**WScript.StdOut.Write "O aplicativo está instalado"**<br /><br /> **WScript.Quit(0)**|O script retorna um código de saída igual a zero, o que indica que ele foi executado com êxito. O valor para STDOUT não está vazio, o que indica que o aplicativo está instalado.|  
|**WScript.StdOut.Write "O aplicativo está instalado"**<br /><br /> **WScript.StdErr.Write "Concluído"**<br /><br /> **WScript.Quit(0)**|O script retorna um código de saída igual a zero, o que indica que ele foi executado com êxito. Os valores para STDOUT e STDERR não está vazios, o que indica que o aplicativo está instalado.|  

 > [!NOTE]  
 >  O tamanho máximo que você pode usar para um script é 32 quilobytes (KB).  

4.  Escolha **OK** para fechar a caixa de diálogo **Editor de Scripts**.  

### <a name="specify-user-experience-options-for-the-deployment-type"></a>Especificar opções de experiência do usuário para o tipo de implantação  
 Essas configurações especificam como o cliente instala o aplicativo nos dispositivos e o que é visto pelo usuário.  

1.  Na página **Experiência do Usuário** do Assistente para Criar Tipo de Implantação, especifique as seguintes informações:  

    -   **Comportamento da instalação**: na lista suspensa, escolha uma das seguintes opções:  

        -   **Instalar para o Usuário**: o aplicativo é instalado somente para o usuário no qual ele é implantado.  

        -   **Instalar para o sistema**: o aplicativo é instalado apenas uma vez e fica disponível para todos os usuários.  

        -   **Instalar para o Sistema se o recurso for um dispositivo; caso contrário, instalar como usuário**: se o aplicativo for implantado em um dispositivo, o cliente o instalará para todos os usuários. Se o aplicativo é implantado em um usuário, o cliente o instala apenas para esse usuário.  

    -   **Requisito de logon**: especifique os requisitos de logon para esse tipo de implantação por meio das seguintes opções:  

        -   **Somente quando um usuário tiver efetuado logon**  

        -   **Se um usuário tiver ou não efetuado logon**  

        -   **Somente quando nenhum usuário tiver efetuado logon**  

        > [!NOTE]  
        >  Essa opção usa como padrão **Somente quando um usuário estiver conectado**. Se você selecionar **Instalar para o usuário** na lista suspensa **Comportamento da instalação**, não poderá alterar essa opção.  

    -   **Visibilidade do programa de instalação**: especifique o modo no qual o tipo de implantação é executado nos dispositivos cliente. As seguintes opções estão disponíveis:  

        -   **Maximizado**: o tipo de implantação é executado maximizado em dispositivos cliente. Os usuários veem todas as atividades de instalação.  

        -   **Normal**: o tipo de implantação é executado no modo normal com base em padrões do sistema e do programa. Esse modo é o padrão.  

        -   **Minimizado**: o tipo de implantação é executado minimizado em dispositivos cliente. Os usuários podem ver a atividade de instalação na área de notificação ou na barra de tarefas.  

        -   **Oculto**: o tipo de implantação é executado no modo oculto nos dispositivos cliente. Os usuários não veem nenhuma atividade de instalação.  

    -   **Permitir que os usuários exibam e interajam com o programa de instalação**: especifique se um usuário pode interagir com a instalação do tipo de implantação para configurar as opções de instalação.  

        > [!NOTE]  
        >  Se você selecionar a opção **Instalar para o usuário** na lista suspensa **Comportamento da instalação**, essa opção estará habilitada por padrão.  

        > [!IMPORTANT]
        > A partir da versão 1802, essa configuração é opcional ao selecionar o comportamento **Instalar para o sistema**. Essa alteração existe principalmente para permitir que um usuário final interaja com a instalação durante uma sequência de tarefas. Por exemplo, para executar um processo de instalação que solicita ao usuário final que escolha várias opções. Alguns instaladores de aplicativos não podem silenciar os prompts de usuário ou o processo de instalação pode exigir valores de configuração específicos conhecidos apenas pelo usuário. <!--1356976-->
        > 
        > A instalação no contexto do sistema e permissão de que os usuários interajam com a instalação não é uma configuração segura. Para obter mais informações, consulte [Segurança e privacidade do gerenciamento de aplicativos](/sccm/apps/plan-design/security-and-privacy-for-application-management#bkmk_interact).

    -   **Tempo de execução máximo permitido (minutos)**: especifique o tempo máximo previsto para que o programa seja executado no computador cliente. Essa configuração pode ser definida como um número inteiro maior que zero. A configuração padrão é 120 minutos.  

         Esse valor é usado para:  

        -   Monitore os resultados do tipo de implantação.  

        -   Verifique se um tipo de implantação é instalado quando janelas de manutenção são definidas em dispositivos cliente. Quando uma janela de manutenção estiver ativa, um programa será iniciado somente se houver tempo suficiente disponível na janela de manutenção para acomodar a configuração **Tempo de Execução Máximo Permitido**.  

        > [!IMPORTANT]  
        >  Um conflito poderá ocorrer se o **Tempo de execução máximo permitido** for maior do que a janela de manutenção agendada. Se o usuário definir o tempo de execução máximo com um período superior ao tamanho de qualquer janela de manutenção disponível, esse tipo de implantação não será executado.  

    -   **Tempo estimado para instalação (minutos)**: especifique o tempo estimado para a instalação do tipo de implantação. Os usuários veem esse tempo no Centro de Software.  

    -   **Especificar o comportamento de reinicialização específico**: especifique a ação pós-instalação. As seguintes opções estão disponíveis:  

        -   **Determinar o comportamento com base em códigos de retorno**: manipule as reinicializações com base nos códigos configurados na guia Códigos de Retorno. O Centro de Software exibe **Pode Exigir uma Reinicialização**. Se um usuário estiver conectado durante a instalação, ele poderá receber uma solicitação, dependendo da configuração Experiência do Usuário da implantação.  

        -   **Nenhuma ação específica**: nenhuma reinicialização é necessária após a instalação. O Centro de Software relata que nenhuma reinicialização é necessária.  
        -   **O programa de instalação do software pode forçar uma reinicialização do dispositivo**: o Configuration Manager não controla nem inicia uma reinicialização, mas a instalação real pode fazer isso sem aviso. Use essa configuração para impedir que o Configuration Manager relate falha de instalação quando o instalador inicia uma reinicialização. O Centro de Software exibe **Pode Exigir uma Reinicialização**.  

        -   **O cliente do Configuration Manager forçará uma reinicialização obrigatória do dispositivo**: o Configuration Manager força uma reinicialização do dispositivo após uma instalação bem-sucedida. O Centro de Software relata que uma reinicialização é necessária. Se um usuário estiver conectado durante a instalação, ele poderá receber uma solicitação, dependendo da configuração Experiência do Usuário da implantação.

### <a name="specify-requirements-for-the-deployment-type"></a>Especificar os requisitos para o tipo de implantação  

1.  Na página **Requisitos** do Assistente para Criar Tipo de Implantação, escolha **Adicionar** para abrir a caixa de diálogo **Criar Requisito** e adicione um novo requisito.  

    > [!NOTE]  
    >  Você também pode adicionar novos requisitos na guia **Requisitos** da caixa de diálogo **Propriedades** do *<nome do tipo de implantação\>*.  

2.  Na lista suspensa **Categoria**, escolha se esse requisito refere-se a um dispositivo ou um usuário. Selecione **Personalizado** para usar uma condição global criada anteriormente. Ao selecionar **Personalizar**, você também pode escolher **Criar** para criar uma nova condição global. Para obter mais informações sobre condições globais, consulte [Como criar condições globais no Configuration Manager](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  Se você implantar o aplicativo em uma coleção de dispositivos, o cliente ignorará os requisitos da categoria **Usuário** e a condição **Dispositivo Primário**.  
    >   
    >  Se você usou o System Center 2012 R2 Configuration Manager SP1 para criar um pacote do Windows e um programa ou uma sequência de tarefas que tem o Windows 10 como requisito e, em seguida, atualizou para o System Center Configuration Manager, os requisitos do Windows 10 podem ser removidos. Para corrigir esse problema, especifique os requisitos novamente. Embora o requisito tenha sido removido da exibição de requisitos, ele ainda é processado corretamente nos dispositivos.  

3.  Na lista suspensa **Condição** , selecione a condição que você deseja usar para avaliar se o usuário ou o dispositivo atende aos requisitos de instalação. O conteúdo dessa lista varia de acordo com a categoria selecionada.  

4.  Na lista suspensa **Operador**, selecione o operador a ser usado. Esse operador compara a condição selecionada com o valor especificado. Ele avalia se o usuário ou o dispositivo atende aos requisitos de instalação. Os operadores disponíveis variam dependendo da condição selecionada.  

    > [!IMPORTANT]  
    >  Os requisitos disponíveis variam de acordo com o tipo de dispositivo utilizado pelo tipo de implantação.  

5.  Na caixa **Valor**, especifique os valores a serem usados. Esses valores, junto com a condição e o operador selecionados, avaliam se o usuário ou o dispositivo atende aos requisitos de instalação. Os valores disponíveis variam de acordo com a condição e o operador selecionados.  

6.  Escolha **OK** para salvar o requisito e feche a caixa de diálogo **Criar Requisito**.  

### <a name="specify-dependencies-for-the-deployment-type"></a>Especificar as dependências para o tipo de implantação  
 As dependências definem um ou mais tipos de implantação de outro aplicativo que deve ser instalado antes um tipo de implantação ser instalado. Você pode configurar os tipos de implantação dependentes para instalar automaticamente antes que um tipo de implantação seja instalado.  

> [!IMPORTANT]  
>  Em alguns casos, um tipo de implantação é dependente de um tipo de implantação que também tem dependências. O número máximo de dependências com suporte na cadeia é cinco.  

1.  Na página **Requisitos** do Assistente para Criar Tipo de Implantação, escolha **Adicionar**.  

    > [!IMPORTANT]  
    >  Você também pode adicionar novas dependências na guia **Dependências** da caixa de diálogo **Propriedades** do *<nome do tipo de implantação\>*.  

2.  Na caixa de diálogo **Adicionar Dependência**, escolha **Adicionar**.  

3.  Na caixa de diálogo **Especificar Aplicativo Necessário** , selecione um aplicativo existente e um dos tipos de implantação de aplicativos para usar como uma dependência.  

    > [!TIP]  
    >  Você pode escolher **Exibir** para exibir as propriedades do tipo de aplicativo ou de implantação selecionado.  

4.  Escolha **OK** para fechar a caixa de diálogo **Especificar aplicativo necessário**.  

5.  Se você deseja que um aplicativo dependente seja instalado automaticamente, selecione **Instalação Automática** ao lado do aplicativo dependente.  

    > [!NOTE]  
    >  Você não precisa implantar um aplicativo dependente para que ele seja instalado automaticamente.  

6.  Na caixa de diálogo **Adicionar Dependência**, em **Nome do grupo de dependências**, insira um nome para indicar esse grupo de dependências de aplicativo.  

7.  Opcionalmente, use os botões **Aumentar Prioridade** e **Diminuir Prioridade**. Essas ações alteram a ordem na qual o cliente avalia cada dependência.  

8.  Escolha **OK** para fechar a caixa de diálogo **Adicionar Dependência**.  

### <a name="confirm-the-deployment-type-settings-and-finish-the-wizard"></a>Confirme as configurações de tipo de implantação e conclua o assistente  

1.  Examine o **Resumo**. Escolha **Avançar** para criar o tipo de implantação. Escolha **Anterior** para voltar e alterar as configurações do tipo de implantação.  

2.  Após a conclusão da página **Andamento** do assistente, examine as ações executadas por ele e escolha **Fechar** para concluí-lo.  

3.  Se você iniciou o Assistente para Criar Tipo de Implantação por meio do Assistente para Criar Aplicativo, você retorna à página **Tipos de Implantação** do Assistente para Criar Aplicativo.  



## <a name="set-up-additional-options-for-deployment-types-that-contain-virtual-applications"></a>Configurar opções adicionais para tipos de implantação que contêm aplicativos virtuais  
 Use os procedimentos a seguir para configurar opções adicionais para os tipos de implantação que incluem aplicativos virtuais.  

### <a name="set-up-content-options-for-application-virtualization-app-v-deployment-types"></a>Configurar opções de conteúdo para tipos de implantação do App-V (Application Virtualization)  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Aplicativos**.  

2.  Na lista **Aplicativos**, selecione um aplicativo que tenha um tipo de implantação do App-V. Em seguida, na guia **Início**, no grupo **Propriedades**, escolha **Propriedades**.  

3.  Na caixa de diálogo **Propriedades** do *<Nome do Aplicativo\>*, na guia **Tipos de Implantação**, selecione um tipo de implantação do App-V e escolha **Editar**.  

4.  Na caixa de diálogo **Propriedades** do *<Nome do Tipo de Implantação\>*, na guia **Conteúdo**, configure as seguintes opções, se necessário:  

    -   **Persistir o conteúdo no cache do cliente**: selecione essa opção para garantir que o conteúdo desse tipo de implantação não seja excluído do cache do cliente do Configuration Manager.  

    -   **Carregar conteúdo no cache do App-V antes de iniciar**: selecione esta opção para garantir que todo o conteúdo do aplicativo virtual seja carregado no cache do App-V antes de o aplicativo ser iniciado. Essa opção também garante que o conteúdo do aplicativo não seja fixado no cache. O cliente exclui o conteúdo, conforme necessário.  

5.  Escolha **OK** para fechar a caixa de diálogo **Propriedades** do *<Nome do Tipo de Implantação\>*.  

6.  Escolha **OK** para fechar a caixa de diálogo *<Nome do Aplicativo\>* **Propriedades**.  

### <a name="set-up-publishing-options-for-app-v-deployment-types"></a>Configurar opções de publicação dos tipos de implantação do App-V  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Aplicativos**.  

3.  Na lista **Aplicativos**, selecione um aplicativo que tenha um tipo de implantação do App-V. Em seguida, na guia **Início**, no grupo **Propriedades**, escolha **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** do *<Nome do Aplicativo\>*, na guia **Tipos de Implantação**, selecione um tipo de implantação do App-V e escolha **Editar**.  

5.  Na caixa de diálogo **Propriedades** do *<Nome do Tipo de Implantação\>*, na guia **Publicação**, selecione os itens no aplicativo virtual que deseja publicar.  

6.  Escolha **OK** para fechar a caixa de diálogo **Propriedades** do *<Nome do Tipo de Implantação\>*.  

7.  Escolha **OK** para fechar a caixa de diálogo *<Nome do Aplicativo\>* **Propriedades**.  



## <a name="import-an-application"></a>Importar um aplicativo  
 Use o procedimento a seguir para importar um aplicativo para o Configuration Manager. Para obter informações sobre como exportar um aplicativo, consulte [Tarefas de gerenciamento para aplicativos do System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md).  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.   

3.  Na guia **Início**, no grupo **Criar**, escolha **Importar Aplicativo**.  

4.  Na página **Geral** do **Assistente para Importar Aplicativo**, escolha **Procurar**. Em seguida, especifique um caminho de rede para o arquivo .zip com o aplicativo a ser importado.  

5.  Na página **Conteúdo do Arquivo**, selecione a ação a ser tomada se o aplicativo que você está tentando importar for uma duplicata de um aplicativo existente. Você pode criar um novo aplicativo ou ignorar o duplicado e adicionar uma nova revisão do aplicativo existente.  

6.  Na página **Resumo**, examine as ações a serem executadas e conclua o assistente.  

 O novo aplicativo aparece no nó **Aplicativos**.  

> [!TIP]  
>  O cmdlet do Windows PowerShell **Import-CMApplication** tem a mesma função que esse procedimento. Para obter mais informações, consulte [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  



##  <a name="deployment-types-supported-by-configuration-manager"></a>Tipos de implantação com suporte do Configuration Manager  

|Nome do tipo de implantação|Mais informações|  
|--------------------------|----------------------|  
|**Windows Installer (arquivo \*.msi)**|Cria um tipo de implantação por meio de um arquivo do Windows Installer.|  
|**Pacote do aplicativo do Windows (\*.appx, \*.appxbundle)**|Cria um tipo de implantação para o Windows 8 ou posterior. Selecione um arquivo de pacote do aplicativo do Windows ou um pacote do lote de aplicativo do Windows.|  
|**Pacote do aplicativo do Windows (na Windows Store)**|Cria um tipo de implantação para o Windows 8 ou posterior. Especifique um link para o aplicativo na Windows Store ou procure o repositório para selecionar o aplicativo.<br /><br /> Para implantar o aplicativo como um link para a Windows Store, defina a configuração da política de grupo **Desligar o aplicativo da Loja** como **Desabilitado** ou **Não configurado**. Se essa configuração estiver habilitada, os clientes não poderão se conectar à Windows Store para baixar e instalar aplicativos.<br /><br /> Os tipos de implantação do Windows 8 que usam um link para um repositório são sempre avaliados antes de outros tipos de implantação, independentemente de sua prioridade.|  
|**Instalador de Script**|Cria um tipo de implantação que especifica um script que é executado em dispositivos clientes para instalar o conteúdo ou executar uma ação.|  
|**Microsoft Application Virtualization 4**|Cria um tipo de implantação por meio de um manifesto do Microsoft Application Virtualization 4|  
|**Microsoft Application Virtualization 5**|Cria um tipo de implantação de um arquivo de pacote do Microsoft Application Virtualization 5.|  
|**Pacote do aplicativo do Windows Phone (arquivo \*.xap)**|Cria um tipo de implantação de um arquivo de pacote do aplicativo do Windows Phone.|  
|**Pacote do aplicativo do Windows Phone (na Loja do Windows Phone)**|Cria um tipo de implantação especificando um link para o aplicativo na Loja do Windows Phone.|  
|**Pacote de aplicativo para iOS (\*arquivo .ipa)**|Cria um tipo de implantação de um arquivo de pacote de aplicativo do iOS.|  
|**Pacote de aplicativo para iOS da App Store**|Cria um tipo de implantação especificando um link para o aplicativo do iOS na Loja de Aplicativos.|  
|**Pacote do aplicativo para Android (arquivo \*.apk)**|Cria um tipo de implantação de um arquivo de pacote de aplicativo do Android.|  
|**Pacote do aplicativo para Android no Google Play**|Cria um tipo de implantação especificando um link para o aplicativo no Google Play.|  
|**Mac OS X**|Cria um tipo de implantação para computadores Mac de um arquivo .cmmac criado com a ferramenta CMAppUtil.<br /><br /> Aplicável somente a computadores Mac que executam o cliente do Configuration Manager.|  
|**Aplicativo Web**|Cria um tipo de implantação que especifica um link para um aplicativo da web. O tipo de implantação instala um atalho para o aplicativo da web no dispositivo do usuário.<br /><br /> Se você instalou o navegador gerenciado do Microsoft Intune em dispositivos iOS ou Android, garanta que os usuários possam usar somente o navegador gerenciado para abrir o aplicativo. Use um dos seguintes formatos ao especificar um link para o aplicativo: substitua **http:** por **http-intunemam:** ou **https:** por **https-intunemam:**<br /><br /> - **http-intunemam://<caminho para o aplicativo Web\>**<br /><br /> - **https-intunemam://<caminho para o aplicativo Web\>**<br /><br /> Você pode usar os requisitos de aplicativo do Configuration Manager para garantir que os aplicativos que deseja associar ao navegador gerenciado sejam instalados apenas em dispositivos iOS e Android.<br /><br /> Para obter mais informações sobre o navegador gerenciado do Intune, consulte [Manage Internet access using managed browser policies](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md) (Gerenciar o acesso à Internet usando políticas de navegador gerenciado).|  
|**Windows Installer por meio do MDM (\*.msi)**|Esse tipo de instalador permite criar e implantar aplicativos baseados no Windows Installer em PCs com o Windows 10.<br /><br /> As seguintes considerações se aplicam quando você usa esse tipo de instalador:<br><br>- Você só pode carregar um único arquivo com a extensão .msi.<br /><br /> - O código do produto do arquivo e a versão do produto são usados para detecção de aplicativo.<br /><br /> - O comportamento de reinicialização padrão do aplicativo é usado. O Configuration Manager não controla essa reinicialização.<br /><br /> - Pacotes MSI por usuário são instalados para um único usuário.<br /><br /> - Pacotes MSI por computador são instalados para todos os usuários no dispositivo.<br /><br /> - Atualmente, os pacotes do MSI de modo dual apenas são instalados para todos os usuários no dispositivo.<br /><br /> - As atualizações de aplicativos são permitidas quando o código do produto MSI de cada versão é o mesmo|  



## <a name="next-steps"></a>Próximas etapas

Depois de criar um aplicativo no Configuration Manager, a próxima etapa é [implantá-lo](/sccm/apps/deploy-use/deploy-applications).