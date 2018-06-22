---
title: Recursos no Technical Preview 1605
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1605.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 05d87b253f2387dd8428f4b9fadea3fe5f3a48e8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342521"
---
# <a name="capabilities-in-technical-preview-1605-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1605 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1605. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.  

 **Problemas conhecidos nesse Technical Preview:**  

-   Com o Technical Preview 1605, se você atualizar as propriedades de um ponto de gerenciamento após ele ser instalado, poderá ver um erro de console que força o fechamento do console.  Se isso acontecer, você poderá desinstalar o ponto de gerenciamento e, em seguida, reinstalar o ponto de gerenciamento usando as configurações desejadas. Como alternativa, você pode modificar o ponto de gerenciamento antes de instalar o Technical Preview 1605.  

-   Quando você usa a o recurso da Windows Store para Empresas com o Technical Preview 1604 e, em seguida, atualiza para o Technical Preview 1605, não é mais possível exibir os dados de integração. Todos os outros recursos continuam a funcionar. Se você tiver integrado com o Technical Preview 1604, poderá continuar integrado após instalar o Technical Preview 1605 e não precisará executar nenhuma ação adicional.  

 **Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

##  <a name="BKMK_PerAppVPN"></a> VPN por aplicativo para dispositivos com Windows 10  
 Para dispositivos Windows 10 gerenciados usando o Configuration Manager com o Intune, você pode adicionar uma lista de aplicativos que abrem automaticamente uma conexão VPN que você configurou por meio do console de administração do Configuration Manager. Você tem a opção de restringir o tráfego VPN para esses aplicativos, ou você pode continuar a permitir todo o tráfego pela conexão VPN.  

 **Requisitos**:  

-   Configuration Manager com Intune  

-   Um perfil de VPN do Windows 10 que foi implantado em pelo menos um dispositivo  

##  <a name="BKMK_InstallSU"></a> Melhorias na sequência de tarefas de Instalar Atualizações de Software  
 As seguintes melhorias foram feitas na sequência de tarefas de Instalar Atualizações de Software:  

-   Uma nova variável de sequência de tarefas, SMSTSSoftwareUpdateScanTimeout, está disponível para oferecer a capacidade de controlar o tempo limite na varredura de atualizações de software durante a etapa de sequência de tarefas de Instalar atualizações de software. O valor padrão é 30 minutos.  

-   Houve aprimoramentos para registro em log. O arquivo smsts.log conterá novas entradas de log que fazem referência a outros arquivos de log que ajudarão você a solucionar problemas durante o processo de instalação de atualizações.  

##  <a name="BKMK_PrepareConfigMgrClient"></a> Melhorias na etapa de sequência de tarefas Preparar o Cliente do ConfigMgr para Captura  
 A etapa Preparar o Cliente do ConfigMgr agora removerá completamente o cliente do Configuration Manager, em vez de apenas remover informações importantes. Quando a sequência de tarefas implantar a imagem capturada do sistema operacional, ela instalará um novo cliente do Configuration Manager sempre.  

##  <a name="BKMK_Grace"></a> Período de cortesia para implantações de aplicativos obrigatórios  
 Em alguns casos, talvez você queira conceder aos usuários mais tempo instalar as implantações de aplicativo obrigatórias além dos prazos configurados. Por exemplo, se um usuário final acabou de voltar de férias, eles terá que aguardar um longo período enquanto as implantações de aplicativo atrasadas são instaladas. No entanto, eles ainda podem instalar o aplicativo imediatamente a qualquer momento que desejarem.  

 Para ajudar a resolver esse problema, agora você pode definir um **período de carência** implantando configurações de cliente do Configuration Manager para uma coleção.  

 Para configurar o período de carência, execute as seguintes ações:  

1.  Na página **Agente de Computador** das configurações do cliente, configure a nova propriedade **Período de carência para a imposição após a data limite da implantação (horas):** com um valor entre **1** e **120** horas.  

2.  Em uma nova implantação de aplicativo ou nas propriedades de uma implantação existente, na página **Agendamento**, marque a caixa de seleção **Delay enforcement of this deployment according to user preferences (Atrasar a imposição dessa implantação de acordo com as preferências do usuário)** até o período de carência definido nas configurações do cliente.  

     Todas as implantações que têm essa caixa de seleção marcada e que são destinadas a dispositivos nos quais você também implantou as configurações do cliente usarão o período de carência.  

 Nesta versão, o período de carência configurado não é usado por dispositivos de cliente. Se você configurar um período de carência e marcar a caixa de seleção, o aplicativo será instalado na primeira janela fora do horário comercial que o usuário configurou após o prazo.  

 Opções semelhantes foram adicionadas ao assistente de implantação de atualizações de software, ao assistente de regras de implantação automática e páginas de propriedades. No entanto, elas não estão implementadas no momento nesse technical preview.  

##  <a name="BKMK_Remote"></a> Nova experiência para ações de dispositivo remoto  
 A experiência para executar as ações de dispositivo remoto do console do Configuration Manager foi aprimorada.  
Ações comuns, como **Desativar/Apagar**, **Redefinir Senha**, **Bloqueio Remoto** e **Ignorar Bloqueio de Ativação** agora podem ser encontradas no menu **Ações do Dispositivo Remoto** acessado pelo espaço de trabalho **Ativos e Conformidade**.  

 ![Captura de tela de novas ações de dispositivo remoto](media/New-Remote-Device-Actions.png)  

 Você pode encontrar o status de cada uma dessas operações nos seguintes locais:  

-   No painel de detalhes quando você seleciona um dispositivo do nó **Dispositivos**.  

-   Na página **Propriedades** de um dispositivo.  

-   Na página principal do nó **Dispositivos** (nem todas as colunas podem estar visíveis por padrão).  

 Para mais informações sobre o bypass do Bloqueio de Ativação do iOS, confira [Ajudar a proteger dispositivos iOS com bypass de Bloqueio de Ativação para o Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock), em especial a seção **Problemas atuais conhecidos com o bypass do Bloqueio de Ativação no Configuration Manager Technical Preview**.  

##  <a name="BKMK_WSFB"></a> Aplicativos da Windows Store para Empresas  
 Na [Windows Store para Empresas](https://www.microsoft.com/business-store), é possível encontrar e adquirir aplicativos para sua organização, individualmente ou por volume. Ao conectar a loja ao Configuration Manager, é possível gerenciar aplicativos adquiridos por volume no console do Configuration Manager, por exemplo:  

-   É possível sincronizar a lista de aplicativos adquiridos com o Configuration Manager  

-   Os aplicativos que são sincronizados aparecem no console do Configuration Manager e você pode implantá-los como qualquer outro aplicativo  

-   A cada 24 horas, o Configuration Manager baixa informações de licenciamento de aplicativo da loja e você pode examiná-las no console do Configuration Manager  

 Na versão de technical preview 1604, você pode sincronizar e exibir aplicativos da Windows Store para Empresas no console do Configuration Manager. Nesta versão, adicionamos a capacidade de criar e implantar aplicativos do Configuration Manager de aplicativos da loja sincronizados.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Configurar a sincronização da Windows Store para Empresas  

1.  No Azure Active Directory, registre o Configuration Manager como uma ferramenta de gerenciamento de "Aplicativo Web e/ou API da Web". Isso fornecerá uma ID de cliente que você precisará mais tarde.  

    1.  No nó do Active Directory do [https://manage.windowsazure.com](https://manage.windowsazure.com), selecione Azure Active Directory, clique em **Aplicativos** > **Adicionar**.  

    2.  Clique em **Adicionar um aplicativo que minha organização esteja desenvolvendo**.  

    3.  Insira um nome para o aplicativo, selecione **Aplicativo Web** e/ou **API da Web** e clique na seta **Avançar**.  

    4.  Insira a mesma URL para **URL de Entrada** e **URI da ID do Aplicativo**. A URL pode ser qualquer uma e não precisa ser resolvida para um endereço real. Por exemplo, você pode inserir **https://&lt;seudomínio>/sccm**.  

    5.  Conclua o assistente.  

2.  No Azure Active Directory, crie uma chave de cliente para a ferramenta de gerenciamento registrada.  

    1.  Realce o aplicativo que você acabou de criar e clique em **Configurar**.  

    2.  Em **Chaves**, escolha uma duração na lista e clique em **Salvar**. Isso criará uma nova chave de cliente. Não saia dessa página até que você tenha carregado com êxito a Windows Store para Empresas no Configuration Manager.  

3.  Na Windows Store para Empresas, configure o Configuration Manager como a ferramenta de gerenciamento da loja.  

    1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools) e entre, se solicitado.  

    2.  Aceite os termos de uso, se necessário.  

    3.  Em **Ferramentas de Gerenciamento**, clique em **Adicionar uma ferramenta de gerenciamento**.  

    4.  Em **Pesquisar a ferramenta por nome**, digite o nome do aplicativo que você criou anteriormente no AAD e clique em **Adicionar**.  

    5.  Clique em **Ativar** ao lado do aplicativo que você acabou de importar.  

    6.  No assistente **Exibir Aplicativos Licenciados Offline**, clique em **Sim** se quiser permitir que aplicativos licenciados offline sejam comprados.  

4.  Compre pelo menos um aplicativo da Windows Store para Empresas.  

5.  No espaço de trabalho **Administração** do console do Configuration Manager, expanda **Serviços de Nuvem** e clique em **Windows Store para Empresas**.  

6.  Na guia **Início**, no grupo **Criar**, clique em **Adicionar Conta da Windows Store para Empresas**.  

7.  Adicione a ID de locatário, a id de cliente e a chave de cliente do Azure Active Directory e conclua o assistente.  

8.  Quando terminar, você verá a conta configurada na lista **Contas da Windows Store para Empresas** no console do Configuration Manager.  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir a tarefa a seguir e conte-nos como foi usando o formulário de comentários na página [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) (Programa de comentários do Configuration Manager) no site do Microsoft Connect:  

 Crie e implante um aplicativo do Configuration Manager por meio de um aplicativo licenciado offline da Windows Store para Empresas.  

1.  No espaço de trabalho **Biblioteca de Software** do console do Configuration Manager, expanda **Gerenciamento de Aplicativos** e clique em **Informações sobre Licença para Aplicativos da Loja**.  

2.  Escolha o aplicativo que deseja implantar e, na guia **Início**, no grupo **Criar**, clique em **Criar Aplicativo**.  

 É criado um aplicativo do Configuration Manager contendo o aplicativo da Windows Store para Empresas. Em seguida, é possível implantar e monitorar o aplicativo, como você faria com qualquer outro aplicativo do Configuration Manager.  

> [!IMPORTANT]  
>  Quando você cria um aplicativo do Configuration Manager com um único tipo de implantação de um aplicativo licenciado offline, ele pode ser implantado em dispositivos que são gerenciados pelo MDM e também gerenciados com o cliente do Configuration Manager. Se você tentar implantar um aplicativo com vários tipos de implantação, a instalação falhará.  
>   
>  No momento, não é possível implantar aplicativos licenciados online com o Configuration Manager.  

##  <a name="BKMK_VPP2"></a> Melhorias gerais para aplicativos adquiridos por volume  

-   Nessa versão, os aplicativos adquiridos por volume da Windows Store para Empresas e da iOS App Store foram consolidados na mesma exibição, **Informações sobre Licença para Aplicativos da Loja**.  

-   Para aplicativos do iOS adquiridos por volume, a guia Apple Volume Purchase Program foi removida da caixa de diálogo **Pacote de aplicativo para Navegador do iOS** no Assistente para Criar Aplicativo. Para criar um aplicativo adquirido por volume para iOS, use essas etapas:  

    1.  1.  No espaço de trabalho **Biblioteca de Software** do console do Configuration Manager, expanda **Gerenciamento de Aplicativos** e clique em **Informações sobre Licença para Aplicativos da Loja**.  

    2.  2.  Escolha o aplicativo que deseja implantar e, na guia **Início**, no grupo **Criar**, clique em **Criar Aplicativo**.  

-   O local usado para obter e carregar um token de VPP da Apple para aplicativos adquiridos por volume no console do Configuration Manager mudou. Agora você pode fazer isso no espaço de trabalho **Administração** no nó **Serviços de Nuvem** > **Tokens do Apple Volume Purchase Program**.  

##  <a name="BKMK_VPP"></a> EDP (Proteção de dados empresariais)  
 Você pode criar itens de configuração que permitem implantar suas políticas de EDP (proteção de dados empresariais), incluindo permitindo que você escolha seus aplicativos protegidos, seu nível de proteção EDP e como encontrar dados empresariais na rede. Para obter mais informações sobre a EDP, consulte os seguintes tópicos:  

-   [Protect your enterprise data using enterprise data protection (EDP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-edp) (Proteger os dados empresariais usando a EDP (proteção de dados empresariais))  

-   [Create and deploy an enterprise data protection (EDP) policy using System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-edp-policy-using-sccm) (Criar e implantar uma política de EDP (proteção de dados empresariais) usando o System Center Configuration Manager)  

##  <a name="BKMK_End"></a> Os usuários finais podem instalar aplicativos do Portal da Empresa  
 O MDM local foi introduzido na versão 1511 do System Center Configuration Manager. Nas versões anteriores, você podia implantar aplicativos em dispositivos Windows 10 gerenciados por MDM com uma finalidade da implantação de instalação **Obrigatória** para todos os dispositivos gerenciados por MDM locais.  

 Nesta versão, agora você pode implantar aplicativos com uma finalidade da implantação **Disponível** para usuários de computadores Windows 10 gerenciados por MDM locais e agora os próprios usuários podem instalar esses aplicativos do Portal da Empresa.
Nesse technical preview, se o Portal da Empresa estiver aberto por mais de 15 minutos, o usuário final verá uma mensagem de erro. Para contornar o problema, reinicie o Portal da Empresa.  

### <a name="before-you-start"></a>Antes de começar  

#### <a name="server-prerequisites"></a>Pré-requisitos do servidor  

-   .NET 4.5 ou superior (exige reinicialização)  

-   PowerShell 3.0 para o script de configuração (exige reinicialização)  

#### <a name="client-prerequisites"></a>Pré-requisitos do cliente  

-   Windows 10 Desktop 1511 (compilação do SO build 10586.218) ou posterior  

#### <a name="general-prerequisites"></a>Pré-requisitos gerais  

-   Certifique-se de ter concluído as [Etapas de preparação para o gerenciamento de dispositivo móvel local](https://technet.microsoft.com/library/mt613153.aspx) e [registrado seus dispositivos](https://technet.microsoft.com/library/mt627870.aspx).  

-   Para obter a melhor experiência de instalação de aplicativo ao usar o Portal da empresa, certifique-se de que o Configuration Manager tenha uma conexão ativa com o Microsoft Intune.  

-   Se você escolher a opção de registro em massa, configure a afinidade de dispositivo de usuário para o dispositivo registrado antes de experimentar esse cenário.  

### <a name="configuration-steps"></a>Etapas de configuração  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Instalar as funções o Catálogo de Aplicativos e habilitar o suporte do Gerenciamento de Dispositivo Móvel  

1.  Adicionar as funções do site da web e do serviço Web do Catálogo de Aplicativos  

    1.  Selecione **HTTPS mode (Modo HTTPS)** e a opção **Permitir que dispositivos móveis usem este ponto de serviços Web do catálogo de aplicativos**.  

    2.  Limitações neste Technical Preview:  

        -   Você deve desinstalar quaisquer funções do Catálogo de Aplicativos existente antes de selecionar a opção para permitir que os dispositivos móveis se conectem.  

        -   Certifique-se de que haja apenas um conjunto de funções do Catálogo de Aplicativos e que as funções estejam colocalizadas no mesmo sistema de sites com as funções do ponto de registro e do ponto proxy de registro.  

2.  Verifique se os seguintes componentes estão operacionais do nó Status do Componente no console do Configuration Manager:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Configurar limites  
 Configure os limites necessários para os pontos de distribuição apenas da intranet.  

> [!NOTE]  
>  Apenas os limites de intervalo IPv4 têm suporte no momento para o gerenciamento de dispositivo móvel.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Implantar a configuração e o aplicativo do Portal da Empresa  

1.  Use o script de configuração incluído com o technical preview para preparar a implantação e a configuração do Portal da Empresa:  

    1.  Abra uma janela de comando com privilégios elevados do PowerShell.  

    2.  Execute **set-executionPolicy RemoteSigned**  

    3.  Na pasta **&lt;diretório de instalação do SCCM\>\cd.latest\SMSSETUP\TOOLS\MDM**, execute **.\ConfigurationScript.ps1**  

     O script de configuração faz o seguinte:  

    1.  Cria um aplicativo do Configuration Manager com um tipo de implantação de pacote do aplicativo Windows usando **CompanyPortalOnPremisesMDM.appx** na mesma pasta.  

    2.  Cria um item de configuração e uma linha de base de configuração que configura o Portal da Empresa.  

    3.  Implanta a linha de base de configuração e o aplicativo e adiciona o aplicativo a todos os pontos de distribuição.  

    > [!NOTE]  
    >  Se as funções do Catálogo de Aplicativos não estiverem colocalizadas com o site primário, realize as seguintes ações:  
    >   
    >  -   No espaço de trabalho **Ativos e Conformidade**, localize o item de configuração **OnPremMDM Portal Configuration CI – server urls (CI de configuração do portal do MDM – URLs de servidor)**  
    > -   Altere o valor de **Regras de Conformidade** para o nome de domínio totalmente qualificado do sistema de sites em que as funções do Catálogo de Aplicativos estão localizadas.  

2.  Depois que o aplicativo do Portal da Empresa e sua configuração forem implantados, verifique se a linha de base de configuração e o aplicativo são compatíveis para o dispositivo determinado usando a seção **Implantações** do console do Configuration Manager. O Portal da Empresa será exibido como **Portal da Empresa (Technical Preview)** no menu Iniciar no dispositivo.  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as tarefas a seguir e conte-nos como foi usando o formulário de comentários na página [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) (Programa de comentários do Configuration Manager) no site do Microsoft Connect:  

1.  Implante vários aplicativos com os tipos de implantação com suporte para uma coleção de usuário com uma finalidade da implantação **Disponível**. Para esse technical preview, os aplicativos que requerem a aprovação do administrador não terão suporte e não serão exibidos no Portal da Empresa.  

2.  Os usuários podem então procurar e instalar os aplicativos do Portal da Empresa.  

     Depois de abrir o Portal da Empresa, você verá uma caixa de diálogo de autenticação chamada **System Center Configuration Manager**. Especifique as credenciais do Active Directory do usuário (na forma de user@domain ou domínio\usuário) para fazer logon.  

##  <a name="BKMK_SW1"></a> Novas guias para Atualizações e Sistemas operacionais no Centro de Software  
 Nessa versão, as seguintes alterações foram feitas para melhorar o layout do aplicativo do Centro de Software:  

-   A guia **Aplicativos** foi dividida em três guias separadas para **Atualizações**, **Sistemas operacionais** (que anteriormente eram encontradas na lista **Filtros**) e **Aplicativos**.  

##  <a name="BKMK_ServerGroups"></a> Manutenção de um grupo de servidores  
 O Technical Preview do System Center Configuration Manager, versão 1511, incluía a habilidade de criar uma coleção em que todos os dispositivos na coleção compõem um grupo de servidores. Em seguida, você pode definir as configurações do grupo de servidores a serem usadas ao implantar as atualizações de software no grupo de servidores, controlar o percentual de computadores atualizados a qualquer momento e configurar scripts do PowerShell de pré-implantação e pós-implantação para executar ações personalizadas.  

 O Technical Preview do System Center Configuration Manager, versão 1605, adiciona a capacidade de atualizar os computadores em um grupo de servidores em uma ordem especificada que você define, adiciona o monitoramento aprimorado para exibir o status dos computadores no grupo de servidores e fornece a capacidade de limpar os bloqueios de implantação que é útil quando os clientes falharam em instalar as atualizações de software e estão impedindo que outros clientes instalem suas atualizações de software.  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as tarefas a seguir e conte-nos como foi usando o formulário de comentários na página [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) (Programa de comentários do Configuration Manager) no site do Microsoft Connect:  

-   Posso criar uma coleção que representa um grupo de servidores. Para este teste, é possível configurar suas regras de associação de coleta para ter dois computadores nesta coleção.   

-   Posso especificar que os computadores no grupo de servidores instalem as atualizações de software em uma ordem específica com base nas configurações do grupo de servidores para a coleção. Use os scripts de exemplo no procedimento para especificar os scripts de pré e pós-implantação.  

-   Posso implantar uma atualização de software para essa coleção. Examine os arquivos start.txt e end.txt (criados por meio dos scripts de exemplo) em C:\temp e verifique as horas de início e término da implantação nos computadores no grupo de servidores. Examine o arquivo UpdatesDeployment.log para obter mais informações.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Para criar uma coleção para um grupo de servidores  

1.  [Crie uma coleção de dispositivos](https://technet.microsoft.com/library/gg712295.aspx) que contém os computadores do grupo de servidores.  

2.  No espaço de trabalho **Ativos e Conformidade**, clique em **Coleções de Dispositivos**, clique com o botão direito do mouse na coleção que contém os computadores do grupo de servidores e clique em **Propriedades**.  

3.  Na guia **Geral**, selecione **Todos os dispositivos fazem parte do mesmo grupo de servidores** e clique em **Configurações**.  

4.  Na página **Configurações do Grupo de Servidor**, especifique uma das seguintes configurações:  

    -   **Allow a percentage of machines to be updated at the same time (Permitir que um percentual de computadores seja atualizado ao mesmo tempo)**: especifica que somente um determinado percentual dos clientes serão atualizados a qualquer dado momento. Se, por exemplo, a coleção tiver 10 clientes e for configurada para atualizar 30% dos clientes ao mesmo tempo, apenas três clientes instalarão atualizações de software a qualquer momento.  

    -   **Allow a number of machines to be updated at the same time (Permitir que um número de computadores seja atualizado ao mesmo tempo)**: especifica que somente um determinado número dos clientes será atualizado a qualquer dado momento.  

    -   **Especifique a sequência de manutenção**: especifica que os clientes na coleção serão atualizados um de cada vez na sequência que você configurar. Um cliente instalará atualizações de software apenas depois que o cliente que está à sua frente na lista terminar de instalar atualizações de software.  

5.  Especifique se deseja usar um script de pré-implantação (drenagem de nó) ou pós-implantação (retomada de nó).  

    > [!TIP]  
    >  Veja abaixo exemplos que você pode usar em testes de scripts de pré-implantação e pós-implantação que gravam a hora atual em um arquivo de texto:  
    >   
    >  **Pré-implantação**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Pós-implantação**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Para implantar atualizações de software no grupo de servidores e monitorar o status  

1.  [Implante atualizações de software](https://technet.microsoft.com/library/gg712304.aspx) na coleção do grupo de servidores.  

2.  [Monitore a implantação de atualização de software](https://technet.microsoft.com/library/gg712304.aspx). Além das exibições de monitoramento padrão para a implantação de atualizações de software, a descrição de um novo estado é exibida quando um cliente está esperando sua vez de instalar as atualizações de software. **Aguardando o bloqueio** é exibido para o novo estado.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>Para limpar os bloqueios de implantação para computadores em um grupo de servidores  

1.  No espaço de trabalho **Ativos e Conformidade**, clique em **Coleções de Dispositivos** e clique na coleção para limpar os bloqueios de implantação.  

2.  Na guia **Início**, no grupo **Implantação**, clique em **Limpar Bloqueios de Implantação de Grupo de Servidores**. Quando os clientes não conseguem instalar as atualizações de software e impedem que outros clientes instale suas atualizações de software, os bloqueios de implantação podem ser removidos manualmente.  

##  <a name="BKMK_ATP"></a> Suporte para o serviço Proteção Avançada contra Ameaças do Windows Defender  
 A ATP (Proteção Avançada contra Ameaças) do Windows Defender é um novo serviço que ajudará as empresas a detectar, investigar e responder a ataques avançados em suas redes. Saiba mais sobre a [ATP do Windows Defender](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). O Configuration Manager pode ajudá-lo a integrar e monitorar os dispositivos de cliente da Edição de Aniversário do Windows 10 gerenciados.  

### <a name="try-it-now"></a>Experimente agora!  
 Tente concluir as tarefas a seguir e conte-nos como foi usando o formulário de comentários na página [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) (Programa de comentários do Configuration Manager) no site do Microsoft Connect:  

-   Integrar os dispositivos para o serviço online da ATP (Proteção Avançada contra Ameaças) do Windows Defender  

-   Monitorar a implantação da ATP do Windows Defender em dispositivos gerenciados  

 **Pré-requisitos**  

-   Assinatura do serviço online de Proteção Avançada contra Ameaças do Windows Defender  

-   Clientes que executam a Edição de Aniversário do Windows 10 (build 14328 e superior)  

-   Criar um arquivo de configuração de integração  

    ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Como criar um arquivo de configuração de integração  

    1.  Faça logon no serviço online da ATP do Windows Defender  

    2.  Clique no item de menu **Integração de Cliente**  

    3.  Selecione **System Center Configuration Manager** e clique em **Baixar pacote**.  

    4.  Baixe o arquivo compactado (.zip) e extraia o conteúdo.  


##### <a name="onboard-devices-for-windows-defender-atp"></a>Dispositivos integrados para a ATP do Windows Defender  

1.  No console do Configuration Manager, navegue para **Ativos e Conformidade** > **Visão Geral** > **Endpoint Protection** > **Políticas do Windows Defender ATP** e clique em **Criar uma política do Windows Defender ATP**. O Assistente de Política da ATP do Windows Defender é aberto.  

2.  Digite o **Nome** e a **Descrição** para a política da ATP do Windows Defender e selecione **Integração**. Clique em Avançar.  

3.  **Procure** o arquivo de Configuração fornecido pelo locatário do serviço de nuvem da ATP do Windows Defender da sua organização. Clique em **Avançar**.  

4.  Especifique os arquivos de exemplo que são coletados e compartilhados por meio dos dispositivos gerenciados para análise.  

    -   **Nenhum** – Nenhum arquivo de exemplo é coletado para análise  

    -   **Arquivos Executáveis Portáteis** – Arquivos como arquivos de programa (.exe), arquivos de link de biblioteca dinâmica (.dll), arquivos de fonte e arquivos semelhantes que podem ser explorados em ciberataques são coletados e compartilhados para análise  

     Clique em **Avançar**.  

5.  Examine o resumo e conclua o assistente.  

6.  Agora você pode implantar a política da ATP do Windows Defender em computadores cliente gerenciados clicando em **Implantar**.  

##### <a name="monitor-windows-defender-atp"></a>Monitorar a ATP do Windows Defender  

1.  No console do Configuration Manager, navegue para **Monitoramento** > **Visão Geral** > **Segurança** e clique em **Windows Defender ATP**.  

2.  Examine o painel da Proteção Avançada contra Ameaças do Windows Defender.  

    -   **Status da Implantação do Agente do Windows Defender** – O número e o percentual de computadores cliente gerenciados qualificados com a política da ATP do Windows Defender ativa e integrada  

    -   **Integridade do Agente do Windows Defender ATP** – Percentual de computadores cliente que relatam o status para o agente da ATP do Windows Defender  

        -   **Íntegro** – Funcionando corretamente  

        -   **Inativo** – Nenhum dado enviado ao serviço durante o período  

        -   **Estado do agente** – O serviço do sistema para o agente do Windows não está em execução  

        -   **Não integrado** – A política foi aplicada, mas o agente não informou sua integração  

##  <a name="BKMK_DHA"></a> Atestado de integridade do dispositivo local  
 O atestado de integridade para dispositivos Windows 10 agora podem ser configurados para comunicação usando a infraestrutura local. Os administradores podem especificar se o relatório é gerado pelos recursos locais ou na nuvem. Se local for escolhido para o relatório de atestado de integridade, uma URL poderá ser especificada para o serviço. Isso permite que os computadores cliente sem acesso à Internet habilitem e gerenciem dispositivos usando o atestado de integridade.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Habilitar atestado de integridade para dispositivos no local  
 Na 1605, corrigimos alguns bugs descobertos no Technical Preview 1604.  Para testar, configure o Serviço de Atesto de Integridade local usando as configurações do agente cliente.  

1.  No console do Configuration Manager, navegue para **Administração** > **Visão Geral** > **Configurações do cliente** e defina **Usar o serviço de atestado de integridade local** como **Sim**.  

2.  Especifique a **URL do Serviço de Atestado de Integridade local**e clique em **OK**.  

##  <a name="BKMK_RestartOptions"></a> Novas opções de reinício para clientes do Windows 10 após a instalação da atualização de software  
 Quando uma atualização de software que requer reinicialização é implantada usando o Configuration Manager e é instalada em um computador, uma reinicialização pendente é agendada e uma caixa de diálogo de reinicialização é exibida. No momento, para o Windows 8 e acima, se você desligar ou reiniciar o computador usando as opções de energia do Windows (em vez da caixa de diálogo de reinicialização), a caixa de diálogo de reinicialização permanecerá depois da reinicialização do computador e ainda será necessário reiniciá-lo no prazo configurado. Nesse technical Preview, as opções **Atualizar e Reiniciar** e **Atualizar e Desligar** estarão disponíveis em computadores Windows 10, nas opções de energia do Windows, sempre que houver uma reinicialização pendente para uma atualização de software do Configuration Manager. Depois de usar uma dessas opções, a caixa de diálogo de reinicialização não será exibida após o computador reiniciar.  

##  <a name="BKMK_IMEI"></a> Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI  
 Agora é possível identificar os dispositivos corporativos importando seus números IMEI (identidade da estação internacional do equipamento móvel). Você pode carregar um arquivo .csv (valores separados por vírgula) que contém os números IMEI do dispositivo ou inserir manualmente as informações sobre o dispositivo.  Você também pode importar os números de série para dispositivos iOS.  As informações importadas definirão a propriedade dos dispositivos que são registrados como “Corporativos”.  Uma licença do Intune ainda é necessária para cada usuário que acessa o serviço.  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as tarefas a seguir e conte-nos como foi usando o formulário de comentários na página [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) (Programa de comentários do Configuration Manager) no site do Microsoft Connect:  

-   Importe um conjunto de números IMEI em um arquivo .csv. Cada linha pode conter o número IMEI seguido por um campo de detalhes.  

-   Importe manualmente os números IMEI do console do Configuration Manager.  

-   Importe um conjunto de números de série do iOS em um arquivo .csv. Novamente, cada linha contém um número seguido por todos os detalhes para o dispositivo.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI  

1.  No console do Configuration Manager, vá para **Ativos e Conformidade** > **Visão geral** > **Todos os Dispositivos de Propriedade Corporativa** > **Pre-declared Devices (Dispositivos Pré-declarados)** e clique em **Create Pre-declared Devices (Criar Dispositivos Pré-declarados)**. O assistente de Dispositivos Pré-declarados é aberto.  

2.  Especifique como você deseja adicionar as informações do dispositivo:  

    -   **Carregar um arquivo CSV contendo detalhes e números IMEI** – para carregar uma lista de números, consulte a Etapa 3.  

    -   **Adicionar detalhes e números IMEI manualmente** – para inserir manualmente as informações, digite o número IMEI ou o número de série do iOS e os detalhes dos dispositivos e prossiga para a Etapa 4.  

3.  Para arquivos carregados, navegue até o arquivo .csv que contém informações para pré-declarar dispositivos corporativos. O arquivo deve ter o seguinte formato, exceto a linha superior (fornecida apenas para fins de orientação):  

    |**Nº do IMEI**|**Nº de série do iOS**|**Sistema operacional**|**Detalhes**|
    |---|---|---|---|
    |123456789012345||WINDOWS|Dispositivo Windows de propriedade da empresa|
    |123456789012|A0BCD0EFGH0J|IOS|Dispositivos iOS de propriedade da empresa|
    |123456789012346||ANDROID|Dispositivo Android de propriedade da empresa|

     **Colunas:**  

    -   Coluna 1: Número IMEI – é necessário um número de série do iOS ou um número IMEI para cada linha  

    -   Coluna 2: Número de série do iOS – apenas os números de série do iOS podem ser pré-declarados. Use o número IMEI para outras plataformas de dispositivo  

    -   Coluna 3: Sistema operacional do dispositivo (maiúsculas/minúsculas necessárias):  

        -   IOS – todos os dispositivos iOS  

        -   WINDOWS – inclui Windows Phone e Windows 10 Mobile e computadores Windows  

        -   ANDROID – Todos os dispositivos Android  

    -   Coluna 4: detalhes – informações de dispositivo adicionais exibidas no console do Configuration Manager  

     Clique em **Avançar**.  

4.  Examine os resultados da importação do arquivo. Os números de série ou IMEI importados anteriormente terão seus detalhes atualizados com novos detalhes.  Clique em **Avançar** para continuar ou em **Voltar** para preservar os detalhes atualizados e conclua o assistente.  
