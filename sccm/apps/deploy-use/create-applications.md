---
title: Criar aplicativos | Microsoft Docs
description: "Criar e implantar aplicativos e tipos de implantação com o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 4d048d4f9ab01b28e6c21a38cca4d82c85030618
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="create-applications-with-system-center-configuration-manager"></a>Criar aplicativos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um aplicativo do System Center Configuration Manager tem os arquivos e as informações que são necessários para implantar o software em um dispositivo. Um aplicativo tem um ou mais tipos de implantação que abrangem os arquivos de instalação e as informações que são necessários para instalar o software. Um tipo de implantação também tem regras que especificam quando e como o software é implantado.  

 Você pode criar aplicativos com os seguintes métodos:  

-   Crie automaticamente os aplicativos e tipos de implantação, lendo os arquivos de instalação do aplicativo.  

-   Crie manualmente o aplicativo e adicione tipos de implantação posteriormente.  

-   Importe um aplicativo de um arquivo.  

> [!NOTE]  
>  [Criar aplicativos para dispositivos móveis ](../../mdm/deploy-use/create-applications.md) fornece informações detalhadas sobre a criação de aplicativos para Android, Windows Phone e iOS.  

Use as seguintes etapas para criar aplicativos e tipos de implantação do Configuration Manager.  

## <a name="start-the-create-application-wizard"></a>Iniciar o assistente para criar aplicativo  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Aplicativo**.  

## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>Especifique se deseja detectar automaticamente ou definir manualmente as informações do aplicativo  

-   Detecte automaticamente as informações do aplicativo para criar um aplicativo simples com um único tipo de implantação, como um arquivo do Windows Installer sem dependências ou requisitos. Criado o aplicativo com esse procedimento, você pode editá-lo conforme necessário para adicionar ou alterar os tipos de implantação e adicionar métodos de detecção, dependências ou requisitos.  

-   Especifique manualmente as informações do aplicativo para criar aplicativos mais complexos e com vários tipos de implantação, dependências, métodos de detecção ou requisitos.  

### <a name="automatically-detect-application-information"></a>Detectar automaticamente as informações do aplicativo  

1.  Na página **Geral** do Assistente para Criar Aplicativo, selecione **Detectar automaticamente informações sobre este aplicativo em arquivos de instalação**.  

2.  Na lista suspensa **Tipo** , selecione o tipo de arquivo de instalação do aplicativo que deseja usar para detectar as informações do aplicativo. Para obter informações sobre os tipos de instalação disponíveis, consulte [Tipos de implantação com suporte do Configuration Manager](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) neste tópico.  

3.  Na caixa **Local**, especifique o caminho UNC (no formato *\\\\servidor\\compartilhamento\\\nome do arquivo*) ou o link do repositório para o arquivo de instalação do aplicativo que você deseja usar para detectar informações do aplicativo. Como alternativa, clique em **Procurar** para localizar o arquivo de instalação.  

    > [!IMPORTANT]  
    >  Quando você seleciona **Windows Installer (arquivo \*.msi)** como um tipo de aplicativo, todos os arquivos da pasta especificada serão importados com o aplicativo e enviados aos pontos de distribuição. Verifique se a pasta especificada contém apenas os arquivos necessários instalar o aplicativo. O Configuration Manager foi testado para dar suporte a até 20.000 arquivos de aplicativo no pacote do aplicativo. Se o aplicativo tiver mais arquivos, considere a criação de vários aplicativos com um número menor de arquivos.  

    >  Você deve ter acesso ao caminho UNC que contém o aplicativo e a todas as subpastas que contêm o conteúdo do aplicativo.  

4.  Na página **Importar Informações** do Assistente para Criar Aplicativo, examine as informações que foram importadas e, em seguida, escolha **Avançar**. Caso seja necessário, escolha **Anterior** para voltar e corrigir quaisquer erros.  

5.  Na página **Informações Gerais** do Assistente para Criar Aplicativo, especifique as seguintes informações:  

    > [!NOTE]  
    >  Algumas dessas informações já podem estar fornecidas se foram obtidas automaticamente dos arquivos de instalação do aplicativo. Além disso, as opções exibidas podem ser diferentes dependendo do tipo de aplicativo que você criar.  

    -   Informações gerais sobre o aplicativo, como nome do aplicativo, comentários, versão e uma referência opcional para ajudá-lo a localizar o aplicativo no console do Configuration Manager.  

    -   **Programa de instalação** – especifique o programa de instalação e as propriedades necessárias para instalar o tipo de implantação do aplicativo.  

        > [!TIP]  
        >  Se o programa de instalação não aparecer, escolha **Procurar** e procure local do programa de instalação.  

    -   **Comportamento da instalação** – especifique se o tipo de implantação do aplicativo será instalado somente para o usuário conectado no momento ou para todos os usuários. Você também poderá especificar se o tipo de implantação será instalado para todos os usuários se for implantado em um dispositivo ou somente para um usuário específico se for implantado para um usuário.  

    -   **Usar uma conexão VPN automática (se estiver configurada)** – se houver um perfil VPN implantado no dispositivo no qual o aplicativo será iniciado, inicie a conexão VPN quando o aplicativo for iniciado (somente Windows 8.1 e Windows Phone 8.1).  

         Em dispositivos Windows Phone 8.1, não há suporte para conexões VPN automáticas se mais de um perfil VPN tiver sido implantado no dispositivo.  

         Para obter mais informações sobre perfis VPN, consulte [perfis VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Escolha **Avançar**, examine as informações do aplicativo na página **Resumo** e, em seguida, conclua o Assistente para Criar Aplicativo.  

O novo aplicativo aparece no nó **Aplicativos** no console do Configuration Manager e você concluiu o processo de criação de aplicativo. Se quiser adicionar mais tipos de implantação ao aplicativo, consulte [Criar tipos de implantação para o aplicativo](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) neste tópico.  

### <a name="manually-specify-application-information"></a>Especificar manualmente as informações do aplicativo  

1.  Na página **Geral** do Assistente para Criar Aplicativo, selecione **Especificar manualmente as informações do aplicativo** e escolha **Avançar**.  

2.  Especifica informações gerais sobre o aplicativo, como nome do aplicativo, comentários, versão e uma referência opcional para ajudá-lo a localizar o aplicativo no console do Configuration Manager.  

3.  Na página **Catálogo de Aplicativos** do Assistente para Criar Aplicativo, especifique as seguintes informações:  

    -   **Idioma Selecionado** – na lista suspensa, selecione a versão de idioma do aplicativo que deseja configurar. Escolha **Adicionar/Remover** para configurar mais idiomas para esse aplicativo.  

    -   **Nome do aplicativo localizado** – especifique o nome do aplicativo no idioma que você selecionou na lista suspensa **Idioma selecionado**.  

        > [!IMPORTANT]  
        >  Você deve especificar um nome de aplicativo localizado para cada versão do idioma configurado.  

    -   **Categorias de usuário** – escolha **Editar** para especificar as categorias de aplicativo no idioma que você selecionou na lista suspensa **Idioma Selecionado**. Os usuários do Centro de Software podem usar essas categorias selecionadas para ajudar a filtrar e classificar os aplicativos disponíveis.  

    -   **Documentação do usuário** – escolha **Procurar** para especificar a URL ou o caminho UNC e o nome do arquivo que os usuários do Centro de Software podem ler para obter mais informações sobre este aplicativo.  

    -   **Texto do link** – especifique o texto que será exibido no lugar da URL do aplicativo.  

    -   **URL de Privacidade do Aplicativo** – especifique uma URL que vincule à política de privacidade do aplicativo.  

    -   **Descrição localizada** – insira uma descrição para este aplicativo no idioma que você selecionou na lista suspensa **Idioma Selecionado**.  

    -   **Palavras-chave** – insira uma lista de palavras-chave no idioma que você selecionou na lista suspensa **Idioma Selecionado**. Essas palavras-chave ajudarão os usuários na pesquisa do aplicativo no Centro de Software.  

    -   **Ícone** – escolha **Procurar** para selecionar um ícone para esse aplicativo entre os ícones disponíveis. Se você não especificar um ícone, um ícone padrão será usado para esse aplicativo.  

    -   **Exibir como um aplicativo em destaque e realçá-lo no portal da empresa** – selecione essa opção para exibir o aplicativo em destaque no portal da empresa.  

4.  Na página **Tipos de Implantação** do Assistente para Criar Aplicativo, escolha **Adicionar** para criar um novo tipo de implantação.  

 Para obter mais informações, consulte [Criar tipos de implantação para o aplicativo](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application).  

5.  Escolha **Avançar**, examine as informações do aplicativo na página **Resumo** e, em seguida, conclua o Assistente para Criar Aplicativo.  

O novo aplicativo aparece no nó **Aplicativos** do console do Configuration Manager.  

##  <a name="create-deployment-types-for-the-application"></a>Criar tipos de implantação para o aplicativo  
 Se você selecionar **Identificar automaticamente as informações sobre esse tipo de implantação nos arquivos de instalação** na página **Geral** do Assistente para Criar Tipo de Implantação, talvez não seja necessário concluir algumas das etapas nos procedimentos a seguir.  

## <a name="start-the-create-deployment-type-wizard"></a>Iniciar o assistente para criar tipo de implantação  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Selecione um aplicativo e, em seguida, na guia **Início**, no grupo **Aplicativo**, escolha **Criar Tipo de Implantação**.  

> [!TIP]  
>  Você também pode iniciar o Assistente para Criar Tipo de Implantação no Assistente para Criar Aplicativo e na guia **Tipos de Implantação** da caixa de diálogo **Propriedades** do *<nome do aplicativo\>*.  

## <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-set-up-the-information"></a>Especifique se deseja detectar automaticamente as informações do tipo de implantação ou configurar as informações manualmente  
 Use um dos procedimentos a seguir para detectar automaticamente ou definir manualmente as informações do tipo de implantação.  

### <a name="automatically-detect-deployment-type-information"></a>Detectar automaticamente as informações do tipo de implantação  

1.  Na página **Geral** do Assistente para Criar Tipo de Implantação, selecione **Identificar automaticamente as informações sobre esse tipo de implantação nos arquivos de instalação**.  

2.  Na caixa **Tipo**, selecione o tipo de arquivo de instalação de aplicativo que deseja usar para detectar as informações do tipo de implantação.  

3.  No caixa **Local**, especifique o caminho UNC (no formato *\\\\servidor\\compartilhamento\\nome do arquivo*) ou especifique o link do repositório para os arquivos de instalação do aplicativo e o conteúdo que deseja usar para detectar as informações do tipo de implantação. Você também pode escolher **Procurar** para localizar o arquivo de instalação.  

    > [!NOTE]  
    >  Você deve ter acesso ao caminho UNC que contém o aplicativo e a todas as subpastas que contêm o conteúdo do aplicativo.  

4.  Na página **Importar Informações** do Assistente para Criar Tipo de Implantação, examine as informações que foram importadas e escolha **Avançar**. Você também pode escolher **Anterior** para voltar e corrigir quaisquer erros.  

5.  Na página **Informações Gerais** do Assistente para Criar Tipo de Implantação, especifique as seguintes informações:  

    > [!NOTE]  
    >  Algumas das informações do tipo de implantação podem já estar presentes se elas tiverem sido lidas dos arquivos de instalação do aplicativo. Além disso, as opções exibidas podem diferir, dependendo do tipo de implantação que você está criando.  

    -   Informações gerais sobre o tipo de implantação, como nome, comentários do administrador e idiomas disponíveis.  

    -   **Programa de instalação** – especifique o programa de instalação e quaisquer propriedades necessárias para instalar o tipo de implantação.  

    -   **Comportamento da instalação** – especifique se deseja instalar o tipo de implantação para o usuário atual ou para todos os usuários. É possível especificar o tipo de implantação a ser instalado para todos os usuários se ele estiver implantado em um dispositivo ou para um usuário somente se ele estiver implantado para um usuário.  

    -   **Usar uma conexão VPN automática (se estiver configurada)** – se houver um perfil VPN implantado no dispositivo no qual o aplicativo será iniciado, inicie a conexão VPN quando o aplicativo for iniciado (somente Windows 8.1 e Windows Phone 8.1). Se vários perfis VPN foram implantados em um dispositivo Windows 8.1, o primeiro perfil VPN implantado será usado por padrão.  

         Em dispositivos Windows Phone 8.1, não há suporte para conexões VPN automáticas se mais de um perfil VPN tiver sido implantado no dispositivo.  

         Para obter mais informações sobre perfis VPN, consulte [Perfis VPN no System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

6.  Escolha **Avançar** e continue para [Especificar as opções de conteúdo para o tipo de implantação](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

### <a name="manually-set-up-the-deployment-type-information"></a>Configurar manualmente as informações do tipo de implantação  

1.  Na página **Geral** do Assistente para Criar Tipo de Implantação, selecione **Especificar manualmente as informações do tipo de implantação**.  

2.  Na caixa **Tipo**, escolha o tipo de arquivo de instalação do aplicativo que deseja usar para detectar as informações do tipo de implantação. Você pode escolher os mesmos tipos de instalação que usaria para detectar automaticamente as informações do tipo de implantação e também pode especificar um script para instalar o tipo de implantação.  

3.  Na página **Informações Gerais** do Assistente para Criar Tipo de Implantação, especifique o nome do tipo de implantação, uma descrição opcional e os idiomas que deseja disponibilizar para esse tipo de implantação e escolha **Avançar**.  

4.  Continuar para [Especificar as opções de conteúdo para o tipo de implantação](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

##  <a name="specify-content-options-for-the-deployment-type"></a>Especificar as opções de conteúdo para o tipo de implantação  

1.  Na página **Conteúdo** do Assistente para Criar Tipo de Implantação, especifique as seguintes informações:  

    -   **Local do conteúdo** – especifique o local do conteúdo para esse tipo de implantação ou selecione **Procurar** para escolher a pasta de conteúdo do tipo de implantação.  

        > [!IMPORTANT]  
        >  A Conta do Sistema do computador do servidor do site deve ter permissões ao local do conteúdo que você especifica.  

    -   **Desinstalar as configurações do conteúdo**--Especifique uma das seguintes opções:
        - **Mesmo que o conteúdo de instalação**--Selecione esta opção se o conteúdo de instalação e desinstalação forem os mesmos. Esse é o comportamento padrão.
        - **Sem conteúdo de instalação**--Selecione esta opção se o seu aplicativo não precisar de conteúdo para desinstalação.
        - **Diferente do conteúdo da instalação**--Selecione esta opção se o conteúdo de desinstalação for diferente do conteúdo de instalação.

4. Se você tiver selecionado **Diferente do conteúdo de instalação**, procure, ou insira, o local do conteúdo do aplicativo que será usado para desinstalar o aplicativo.
5. Clique em **OK** para fechar a caixa de diálogo Propriedades do tipo de implantação.

    -   **Manter o conteúdo no cache do cliente** – selecione essa opção para especificar se o conteúdo deve ser mantido no cache do computador cliente por tempo indeterminado, mesmo após sua execução. Embora essa opção seja útil em algumas implantações, como do software baseado no Windows Installer que precisa de uma cópia de origem local disponível para aplicar atualizações, ela reduz o espaço em cache disponível. Selecionar essa opção pode causar uma falha em uma implantação grande posteriormente se o cache não tiver espaço suficiente.  

    -   **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede** – selecione essa opção para reduzir a carga na rede, permitindo que os clientes baixem conteúdo de outros clientes locais na rede que já tenham baixado e armazenado o conteúdo em cache. Essa opção utiliza a tecnologia Windows BranchCache.  

    -   **Programa de instalação** – especifique o nome do programa de instalação e todos os parâmetros de instalação necessários ou escolha **Procurar** para localizar o arquivo de instalação.  

    -   **Instalação inicia em** – opcionalmente, especifique a pasta que contém o programa de instalação para o tipo de implantação. Essa pasta pode ser um caminho absoluto no cliente ou um caminho para a pasta do ponto de distribuição que contém os arquivos de instalação.  

    -   **Desinstalar programa** – opcionalmente, especifique o nome do programa de desinstalação e todos os parâmetros necessários ou escolha **Procurar** para localizá-lo.  

    -   **Desinstalação inicia em** – opcionalmente, especifique a pasta que contém o programa de desinstalação para o tipo de implantação. Essa pasta pode ser um caminho absoluto no cliente ou um caminho relativo à pasta do ponto de distribuição que contém o pacote.  

    -   **Executar programa de instalação e desinstalação como um processo de 32 bits em clientes de 64 bits** – use o arquivo de 32 bits e os locais do Registro em computadores baseados em Windows para executar o programa de instalação para o tipo de implantação.  

2.  Escolha **Próxima**.  

## <a name="set-up-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>Configurar métodos de detecção para indicar a presença do tipo de implantação (somente computadores Windows)  
 Este procedimento configura um método de detecção que indica se o tipo de implantação já está instalado.  

1.  Na página **Método de Detecção** do Assistente para Criar Tipo de Implantação, selecione **Configurar regras para detectar a presença desse tipo de implantação** e escolha **Adicionar Cláusula**.  

    > [!NOTE]  
    >  Você também pode selecionar **Usar um script personalizado para detectar a presença desse tipo de implantação**. Para obter mais informações, consulte [Usar um script personalizado para verificar a presença de um tipo de implantação](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type).  

2.  Na caixa de diálogo **Regra de Detecção**, na lista suspensa **Tipo de configuração**, selecione o método que você quer usar para detectar a presença do tipo de implantação. Você pode escolher entre os seguintes métodos disponíveis:  

    -   **Sistema de Arquivos** – use esse método para detectar se um arquivo ou uma pasta especificada existe em um dispositivo cliente, indicando que o aplicativo está instalado.  

        > [!NOTE]  
        >  O tipo de configuração **Sistema de arquivos** não dá suporte à especificação de um caminho UNC para um compartilhamento de rede no campo Caminho. Você só pode especificar um caminho local no dispositivo do cliente.  
        >   
        >  Para marcar locais de arquivo de 32 bits para o arquivo ou a pasta especificada, primeiro selecione a opção **Esse arquivo ou pasta está associada a um aplicativo de 32 bits em sistemas de 64 bits**. Se o arquivo ou pasta não for encontrado, os locais de 64 bits serão pesquisados.  

    -   **Registro** – use esse método para detectar se uma chave do Registro ou um valor do Registro especificado existe em um dispositivo cliente, indicando assim que o aplicativo está instalado.  

        > [!NOTE]  
        >  Para marcar locais do Registro de 32 bits para a chave do Registro especificada, primeiro selecione a opção **Essa chave do Registro está associada a um aplicativo de 32 bits em sistemas de 64 bits**. Se a chave do Registro não for encontrada, os locais de 64 bits serão pesquisados.  

    -   **Windows Installer** – use esse método para detectar se um arquivo do Windows Installer especificado existe em um dispositivo cliente, indicando assim que o aplicativo está instalado.  

3.  Especificar detalhes sobre o item que você quer usar para detectar se esse tipo de implantação está instalado. Por exemplo, você pode usar um arquivo, uma pasta, uma chave do Registro ou um valor de Registro, ou um código de produto do Windows Installer.  

4.  Especificar detalhes sobre o valor que você quer avaliar em relação ao item que usa para detectar se esse tipo de implantação está instalado. Por exemplo, se você usar um arquivo para verificar se o tipo de implantação está instalado, selecione **A configuração do sistema de arquivos deve existir no sistema de destino para indicar a presença deste aplicativo**.  

5.  Escolha **Avançar** para fechar a caixa de diálogo **Regra de Detecção**.  

###  <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a>Use um script personalizado para verificar a presença de um tipo de implantação  

1.  Na página **Método de Detecção** do Assistente para Criar Tipo de Implantação, selecione a caixa **Usar um script personalizado para detectar a presença desse tipo de implantação** e, em seguida, escolha **Editar**.  

2.  Na caixa de diálogo **Editor de Scripts**, na lista suspensa **Tipo de script** selecione a linguagem de script que você quer usar para detectar o tipo de implantação.  

3.  Na caixa **Conteúdo de script**, insira o script que deseja usar. Você também pode colar o conteúdo de um script existente nesse campo ou escolher **Abrir** para procurar um script salvo existente. O Configuration Manager verifica os resultados do script lendo os valores que são gravados no fluxo de saída STDOUT (Saída Padrão), no fluxo de saída STDERR (Erro Padrão) e no código de saída do script. Se o código de saída for um valor diferente de zero, então o script terá falhado e o status de detecção do aplicativo será desconhecido. Se o código de saída for zero e STDOUT tiver dados, o status de detecção do aplicativo será Instalado.  

 Use a tabela a seguir para saber como usar a saída de um script para verificar se um aplicativo está instalado.  

|Código de saída do script|Detalhes|
|--------------------------------|-----------------|
|0|**Dados lidos de STDOUT** – vazio<br /><br /> **Dados lidos de STDERR** – vazio<br /><br /> **Resultado do script** – êxito<br /><br /> **Estado de detecção do aplicativo** – não instalado|  
|0|**Dados lidos de STDOUT** – vazio<br /><br /> **Dados lidos de STDERR** – não vazio<br /><br /> **Resultado do script** – falha<br /><br /> **Estado de detecção do aplicativo** – desconhecido|  
|0|**Dados lidos de STDOUT** – não vazio<br /><br /> **Dados lidos de STDERR** – vazio<br /><br /> **Resultado do script** – êxito<br /><br /> **Estado de detecção do aplicativo** – instalado|  
|0|**Dados lidos de STDOUT** – não vazio<br /><br /> **Dados lidos de STDERR** – não vazio<br /><br /> **Resultado do script** – êxito<br /><br /> **Estado de detecção do aplicativo** – instalado|  
|Valor diferente de zero|**Dados lidos de STDOUT** – vazio<br /><br /> **Dados lidos de STDERR** – vazio<br /><br /> **Resultado do script** – falha<br /><br /> **Estado de detecção do aplicativo** – desconhecido|  
|Valor diferente de zero|**Dados lidos de STDOUT** – vazio<br /><br /> **Dados lidos de STDERR** – não vazio<br /><br /> **Resultado do script** – falha<br /><br /> **Estado de detecção do aplicativo** – desconhecido|  
|Valor diferente de zero|**Dados lidos de STDOUT** – não vazio<br /><br /> **Dados lidos de STDERR** – vazio<br /><br /> **Resultado do script** – falha<br /><br /> **Estado de detecção do aplicativo** – desconhecido|  
|Valor diferente de zero|**Dados lidos de STDOUT** – não vazio<br /><br /> **Dados lidos de STDERR** – não vazio<br /><br /> **Resultado do script** – falha<br /><br /> **Estado de detecção do aplicativo** – desconhecido|  

A tabela a seguir apresenta scripts de exemplo do Microsoft VB (Visual Basic) que você pode usar para gravar seus próprios scripts de detecção de aplicativo.  

|Script de exemplo do Visual Basic|Descrição|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|O script retorna um código de saída que não é zero, o que indica que ele não foi executado com êxito. Nesse caso, o estado de detecção do aplicativo é desconhecido.|  
|**WScript.StdErr.Write "Falha de script"**<br /><br /> **WScript.Quit(0)**|O script retorna um código de saída zero, mas o valor de STDERR não está vazio, o que indica que o script não foi executado com êxito. Nesse caso, o estado de detecção do aplicativo é desconhecido.|  
|**WScript.Quit(0)**|O script retorna um código de saída igual a zero, o que indica que ele foi executado com êxito. No entanto, o valor para STDOUT está vazio, que indica que o aplicativo não está instalado.|  
|**WScript.StdOut.Write "O aplicativo está instalado"**<br /><br /> **WScript.Quit(0)**|O script retorna um código de saída igual a zero, o que indica que ele foi executado com êxito. O valor para STDOUT não está vazio, o que indica que o aplicativo está instalado.|  
|**WScript.StdOut.Write "O aplicativo está instalado"**<br /><br /> **WScript.StdErr.Write "Concluído"**<br /><br /> **WScript.Quit(0)**|O script retorna um código de saída igual a zero, o que indica que ele foi executado com êxito. Os valores para STDOUT e STDERR não está vazios, o que indica que o aplicativo está instalado.|  

 > [!NOTE]  
 >  O tamanho máximo que você pode usar para um script é 32 quilobytes (KB).  

4.  Escolha **OK** para fechar a caixa de diálogo **Editor de Scripts**.  

## <a name="specify-user-experience-options-for-the-deployment-type"></a>Especificar opções de experiência do usuário para o tipo de implantação  
 Essas configurações especificam como o aplicativo será instalado nos dispositivos e o que o usuário verá.  

1.  Na página **Experiência do Usuário** do Assistente para Criar Tipo de Implantação, especifique as seguintes informações:  

    -   **Comportamento da instalação** – na lista suspensa, selecione uma das seguintes opções:  

        -   **Instalar para o Usuário** – o aplicativo é instalado somente para o usuário para o qual ele será implantado.  

        -   **Instalar para o Sistema** – o aplicativo é instalado apenas uma vez e fica disponível para todos os usuários.  

        -   **Instalar para o sistema se o recurso for dispositivo, caso contrário, instalar como usuário** – se o aplicativo for implantado em um dispositivo, ele será instalado para todos os usuários. Se o aplicativo for implantado para um usuário, então ele será instalado somente para esse usuário.  

    -   **Requisito de logon** – especifique os requisitos de logon para esse tipo de implantação entre as seguintes opções:  

        -   **Somente quando um usuário tiver efetuado logon**  

        -   **Se um usuário tiver ou não efetuado logon**  

        -   **Somente quando nenhum usuário tiver efetuado logon**  

        > [!NOTE]  
        >  Essa opção assume o padrão de **Somente quando um usuário tiver efetuado logon**, e não poderá ser alterada se você selecionou **Instalar para o usuário** na lista suspensa **Comportamento da instalação** .  

    -   **Visibilidade do programa de instalação** – especifique o modo no qual o tipo de implantação será executado em dispositivos clientes. As seguintes opções estão disponíveis:  

        -   **Maximizado** – o tipo de implantação é executado maximizado em dispositivos clientes. Os usuários verão todas as atividades da instalação.  

        -   **Normal** – o tipo de implantação é executado no modo normal com base nos padrões do sistema e do programa. Este é o modo padrão.  

        -   **Minimizado** – o tipo de implantação é executado minimizado em dispositivos clientes. Os usuários podem ver a atividade de instalação na área de notificação ou na barra de tarefas.  

        -   **Oculto** – o tipo de implantação é executado oculto em dispositivos clientes e os usuários não verão nenhuma atividade de instalação.  

    -   **Permitir que os usuários exibam e interajam com o programa de instalação** – especifique se um usuário pode interagir com a instalação do tipo de implantação para configurar as opções de instalação.  

        > [!NOTE]  
        >  Essa opção é habilitada por padrão, se você selecionou a opção **Instalar para o usuário** na lista suspensa **Comportamento da instalação** .  

    -   **Tempo de execução máximo permitido (minutos)** – especifique o tempo máximo em que o programa deverá ser executado no computador cliente. Essa configuração pode ser definida como um número inteiro maior que zero. A configuração padrão é 120 minutos.  

         Esse valor é usado para:  

        -   Monitore os resultados do tipo de implantação.  

        -   Verifique se um tipo de implantação será instalado quando houver janelas de manutenção definidas em dispositivos clientes. Quando uma janela de manutenção está ativa, um programa será iniciado somente se houver tempo suficiente disponível na janela de manutenção para acomodar a configuração **Tempo de Execução Máximo Permitido** .  

        > [!IMPORTANT]  
        >  Um conflito poderá ocorrer se o **Tempo de execução máximo permitido** for maior do que a janela de manutenção agendada. Se o tempo de execução máximo for definido pelo usuário para um período que exceda o tamanho de qualquer janela de manutenção disponível, esse tipo de implantação não será executado.  

2.  **Tempo estimado para instalação (minutos)** – especifique o tempo estimado para a instalação do tipo de implantação. Isso é exibido aos usuários do Centro de Software.  

## <a name="specify-requirements-for-the-deployment-type"></a>Especificar os requisitos para o tipo de implantação  

1.  Na página **Requisitos** do Assistente para Criar Tipo de Implantação, escolha **Adicionar** para abrir a caixa de diálogo **Criar Requisito** e adicione um novo requisito.  

    > [!NOTE]  
    >  Você também pode adicionar novos requisitos na guia **Requisitos** da caixa de diálogo **Propriedades** do *<nome do tipo de implantação\>*.  

2.  Na lista suspensa **Categoria**, selecione se esse requisito é para um dispositivo ou um usuário, ou selecione **Personalizar** para usar uma condição global criada anteriormente. Ao selecionar **Personalizar**, você também pode escolher **Criar** para criar uma nova condição global. Para obter mais informações sobre condições globais, consulte [Como criar condições globais no Configuration Manager](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  Todos os requisitos da categoria **Usuário** e da condição **Dispositivo Primário** serão ignorados se você implantar o aplicativo em uma coleção de dispositivos.  
    >   
    >  Se você tiver criado um pacote do Windows e um programa ou sequência de tarefas que tenha o Windows 10 como um requisito usando o System Center 2012 R2 Configuration Manager SP1 e, em seguida, atualizar para o System Center Configuration Manager, os requisitos para o Windows 10 poderão ser removidos. Para corrigir esse problema, especifique os requisitos novamente. Observe que, embora o requisito tenha sido removido da exibição de requisitos, ele ainda é processado corretamente nos dispositivos.  

3.  Na lista suspensa **Condição** , selecione a condição que você deseja usar para avaliar se o usuário ou o dispositivo atende aos requisitos de instalação. O conteúdo desta lista varia dependendo da categoria selecionada.  

4.  Na lista suspensa **Operador** , escolha o operador que será usado para comparar a condição selecionada ao valor especificado para avaliar se o usuário ou o dispositivo atende aos requisitos de instalação. Os operadores disponíveis variam dependendo da condição selecionada.  

    > [!IMPORTANT]  
    >  Os requisitos disponíveis variam dependendo do tipo de dispositivo que o tipo de implantação usa.  

5.  Na caixa **Valor**, especifique os valores que serão usados com a condição e o operador selecionados para avaliar se o usuário ou o dispositivo atende aos requisitos de instalação. Os valores disponíveis irão variar dependendo da condição selecionada e do operador selecionado.  

6.  Escolha **OK** para salvar o requisito e feche a caixa de diálogo **Criar Requisito**.  

## <a name="specify-dependencies-for-the-deployment-type"></a>Especificar as dependências para o tipo de implantação  
 As dependências definem um ou mais tipos de implantação de outro aplicativo que deve ser instalado antes um tipo de implantação ser instalado. Você pode configurar os tipos de implantação dependentes para instalar automaticamente antes que um tipo de implantação seja instalado.  

> [!IMPORTANT]  
>  Em alguns casos, um tipo de implantação é dependente de um tipo de implantação que também tem dependências. O número máximo de dependências com suporte na cadeia é cinco.  

1.  Na página **Dependências** do Assistente para Criar Tipo de Implantação, escolha **Adicionar** se desejar especificar os tipos de implantação que devem ser instalados antes da instalação desse tipo de implantação.  

    > [!IMPORTANT]  
    >  Você também pode adicionar novas dependências na guia **Dependências** da caixa de diálogo **Propriedades** do *<nome do tipo de implantação\>*.  

2.  Na caixa de diálogo **Adicionar Dependência**, escolha **Adicionar**.  

3.  Na caixa de diálogo **Especificar Aplicativo Necessário** , selecione um aplicativo existente e um dos tipos de implantação de aplicativos para usar como uma dependência.  

    > [!TIP]  
    >  Você pode escolher **Exibir** para exibir as propriedades do tipo de aplicativo ou de implantação selecionado.  

4.  Escolha **OK** para fechar a caixa de diálogo **Especificar aplicativo necessário**.  

5.  Se você deseja que um aplicativo dependente seja instalado automaticamente, selecione **Instalação Automática** ao lado do aplicativo dependente.  

    > [!NOTE]  
    >  Um aplicativo dependente não precisa ser implantado para ser instalado automaticamente.  

6.  Na caixa de diálogo **Adicionar Dependência**, em **Nome do grupo de dependências**, insira um nome para indicar esse grupo de dependências de aplicativo.  

7.  Opcionalmente, use os botões **Aumentar Prioridade** e **Diminuir Prioridade** para alterar a ordem em que cada dependência é avaliada.  

8.  Escolha **OK** para fechar a caixa de diálogo **Adicionar Dependência**.  

## <a name="confirm-the-deployment-type-settings-and-finish-the-wizard"></a>Confirme as configurações de tipo de implantação e conclua o assistente  

1.  Na página **Resumo** do Assistente para Criar Tipo de Implantação, examine as ações que o assistente executará. Escolha **Avançar** para criar o tipo de implantação ou escolha **Anterior** para voltar e alterar as configurações do tipo de implantação.  

2.  Após a conclusão da página **Andamento** do assistente, examine as ações executadas por ele e escolha **Fechar** para concluí-lo.  

3.  Se você tiver iniciado o Assistente para Criar Tipo de Implantação no Assistente para Criar Aplicativo, você retornará à página **Tipos de Implantação** do Assistente para Criar Aplicativo.  

## <a name="set-up-additional-options-for-deployment-types-that-contain-virtual-applications"></a>Configurar opções adicionais para tipos de implantação que contêm aplicativos virtuais  
 Use os procedimentos a seguir para configurar opções adicionais para tipos de implantação que contêm aplicativos virtuais.  

### <a name="set-up-content-options-for-application-virtualization-app-v-deployment-types"></a>Configurar opções de conteúdo para tipos de implantação do App-V (Application Virtualization)  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Aplicativos**.  

2.  Na lista **Aplicativos**, selecione um aplicativo que tenha um tipo de implantação do App-V. Em seguida, na guia **Início**, no grupo **Propriedades**, escolha **Propriedades**.  

3.  Na caixa de diálogo **Propriedades** do *<Nome do Aplicativo\>*, na guia **Tipos de Implantação**, selecione um tipo de implantação do App-V e escolha **Editar**.  

4.  Na caixa de diálogo **Propriedades** do *<Nome do Tipo de Implantação\>*, na guia **Conteúdo**, configure as seguintes opções, se necessário:  

    -   **Manter o conteúdo no cache do cliente** – selecione essa opção para garantir que o conteúdo desse tipo de implantação não seja excluído do cache do cliente Configuration Manager.  

    -   **Carregar conteúdo no cache do App-V antes de iniciar** – selecione essa opção para garantir que todo o conteúdo do aplicativo virtual seja carregado no cache do App-V antes que o aplicativo seja iniciado. Essa opção também garante que o conteúdo do aplicativo não seja fixado no cache e possa ser excluído se necessário.  

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

4.  Na página **Geral** do **Assistente para Importar Aplicativo**, escolha **Procurar** e especifique um caminho UNC para o arquivo .zip que contém o aplicativo que deseja importar.  

5.  Na página **Conteúdo do Arquivo**, selecione a ação a ser tomada se o aplicativo que você está tentando importar for uma duplicata de um aplicativo existente. Você pode criar um novo aplicativo ou ignorar o duplicado e adicionar uma nova revisão do aplicativo existente.  

6.  Na página **Resumo**, examine as ações a serem executadas e conclua o assistente.  

 O novo aplicativo aparece no nó **Aplicativos**.  

> [!TIP]  
>  O cmdlet do Windows PowerShell **Import-CMApplication** tem a mesma função que esse procedimento. Para obter mais informações, consulte [Import-CMApplication](https://technet.microsoft.com/library/jj821738.aspx) na Referência do Cmdlet do Microsoft System Center 2012 Configuration Manager SP1.  

##  <a name="deployment-types-supported-by-configuration-manager"></a>Tipos de implantação com suporte do Configuration Manager  

|Nome do tipo de implantação|Mais informações|  
|--------------------------|----------------------|  
|**Windows Installer (arquivo \*.msi)**|Cria um tipo de implantação por meio de um arquivo do Windows Installer.|  
|**Pacote do aplicativo do Windows (\*.appx, \*.appxbundle)**|Cria um tipo de implantação para o Windows 8, Windows RT ou posterior por meio de um arquivo de pacote de aplicativos do Windows ou de um pacote de lote de aplicativo do Windows.|  
|**Pacote do aplicativo do Windows (na Windows Store)**|Cria um tipo de implantação do Windows 8, Windows RT ou posterior especificando um link para o aplicativo na Windows Store ou procurando o armazenamento para selecionar o aplicativo de que você precisa.<br /><br /> Se deseja implantar o aplicativo como um link para a Windows Store, verifique se a configuração da Política de Grupo **Desligar o aplicativo da Loja** está definida como **Desabilitada** ou **Não configurada**. Se essa configuração estiver habilitada, os clientes não poderão se conectar à Windows Store para baixar e instalar aplicativos.<br /><br /> Os tipos de implantação do Windows 8 que usam um link para um repositório são sempre avaliados antes de outros tipos de implantação, independentemente de sua prioridade.|  
|**Instalador de Script**|Cria um tipo de implantação que especifica um script que é executado em dispositivos clientes para instalar o conteúdo ou executar uma ação.|  
|**Microsoft Application Virtualization 4**|Cria um tipo de implantação por meio de um manifesto do Microsoft Application Virtualization 4|  
|**Microsoft Application Virtualization 5**|Cria um tipo de implantação de um arquivo de pacote do Microsoft Application Virtualization 5.|  
|**Pacote do aplicativo do Windows Phone (arquivo \*.xap)**|Cria um tipo de implantação de um arquivo de pacote do aplicativo do Windows Phone.|  
|**Pacote do aplicativo do Windows Phone (na Loja do Windows Phone)**|Cria um tipo de implantação especificando um link para o aplicativo na Loja do Windows Phone.|  
|**Gabinete do Windows Mobile**|Cria um tipo de implantação para dispositivos Windows Mobile por meio de um arquivo CAB (Gabinete do Windows Mobile).|  
|**Pacote de aplicativo para iOS (\*arquivo .ipa)**|Cria um tipo de implantação de um arquivo de pacote de aplicativo do iOS.|  
|**Pacote de aplicativo para iOS da App Store**|Cria um tipo de implantação especificando um link para o aplicativo do iOS na Loja de Aplicativos.|  
|**Pacote do aplicativo para Android (arquivo \*.apk)**|Cria um tipo de implantação de um arquivo de pacote de aplicativo do Android.|  
|**Pacote do aplicativo para Android no Google Play**|Cria um tipo de implantação especificando um link para o aplicativo no Google Play.|  
|**Mac OS X**|Cria um tipo de implantação para computadores Mac de um arquivo .cmmac criado com a ferramenta CMAppUtil.<br /><br /> Aplica-se somente a computadores Mac que executam o cliente Configuration Manager.|  
|**Aplicativo Web**|Cria um tipo de implantação que especifica um link para um aplicativo da web. O tipo de implantação instala um atalho para o aplicativo da web no dispositivo do usuário.<br /><br /> Se tiver instalado o navegador gerenciado pelo Intune em dispositivos iOS ou Android que você gerencia, você poderá garantir que os usuários poderão usar somente o navegador gerenciado para abrir o aplicativo. Para fazer isso, use um dos seguintes formatos ao especificar um link para o aplicativo, substituindo **http:** por **http-intunemam:** ou **https:** por **https-intunemam:**<br /><br /> - **http-intunemam://<caminho para o aplicativo Web\>**<br /><br /> - **https-intunemam://<caminho para o aplicativo Web\>**<br /><br /> Você pode usar os requisitos de aplicativo do Configuration Manager para garantir que os aplicativos que deseja associar ao navegador gerenciado sejam instalados apenas em dispositivos iOS e Android.<br /><br /> Para obter mais informações sobre o navegador gerenciado do Intune, consulte [Manage Internet access using managed browser policies](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md) (Gerenciar o acesso à Internet usando políticas de navegador gerenciado).|  
|**Windows Installer por meio do MDM (\*.msi)**|Esse tipo de instalador permite criar e implantar aplicativos baseados no Windows Installer em PCs com o Windows 10.<br /><br /> As seguintes considerações se aplicam quando você usa esse tipo de instalador:<br><br>- Você só pode carregar um único arquivo com a extensão .msi.<br /><br /> - O código do produto do arquivo e a versão do produto são usados para detecção de aplicativo.<br /><br /> - O comportamento de reinicialização padrão do aplicativo será usado. O Configuration Manager não controla isto.<br /><br /> - Serão instalados pacotes do MSI por usuário para um único usuário.<br /><br /> - Serão instalados pacotes do MSI por computador para todos os usuários no dispositivo.<br /><br /> - Atualmente, os pacotes do MSI de modo dual apenas são instalados para todos os usuários no dispositivo.<br /><br /> - As atualizações de aplicativos são permitidas quando o código do produto MSI de cada versão é o mesmo|  
