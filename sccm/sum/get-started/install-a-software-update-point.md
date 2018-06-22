---
title: instalar e configurar um ponto de atualização de software
titleSuffix: Configuration Manager
description: Os sites primários requerem um ponto de atualização de software no site de administração central para a avaliação de conformidade das atualizações de software e para implantar atualizações de software em clientes.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 05/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 3b2bb1f6866bb5266f20fb94451bfbfd2ce675bb
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353072"
---
# <a name="install-and-configure-a-software-update-point"></a>instalar e configurar um ponto de atualização de software  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


> [!IMPORTANT]  
>  Antes de instalar a função de SUP (ponto de atualização de software), é necessário verificar se o servidor atende às dependências necessárias e determina a infraestrutura do ponto de atualização de software no site. Para obter mais informações sobre como planejar as atualizações de software e determinar a infraestrutura do ponto de atualização de software, consulte [Planejar atualizações de software](../plan-design/plan-for-software-updates.md).  

 O ponto de atualização de software é necessário no site de administração central e nos sites primários para habilitar a avaliação de conformidade das atualizações de software e implantar atualizações de software em clientes. O ponto de atualização de software é opcional em sites secundários. A função de sistema de site do ponto de atualização de software deve ser criada em um servidor que tenha o WSUS instalado. O ponto de atualização de software interage com os serviços do WSUS para configurar os parâmetros de atualização de software e solicitar a sincronização dos metadados das atualizações de software. Quando houver uma hierarquia do Configuration Manager, instale e configure o ponto de atualização de software no site de administração central primeiro, depois nos sites primários filho e, opcionalmente, nos sites secundários. Quando houver um site primário autônomo, e não um site de administração central, instale e configure o ponto de atualização de software no site primário primeiro e, opcionalmente, nos sites secundários. Algumas configurações estão disponíveis somente quando você configura o ponto de atualização de software no site de nível superior. Há diferentes opções que devem ser consideradas dependendo de onde o ponto de atualização de software é instalado.  

> [!IMPORTANT]  
>  É possível instalar mais de um ponto de atualização de software em um site. O primeiro ponto de atualização de software que você instala é configurado como a origem da sincronização, que sincroniza as atualizações do Microsoft Update ou da origem de sincronização upstream. Os outros pontos de atualização de software no site são configurados como réplicas do primeiro ponto de atualização de software. Portanto, algumas configurações não estarão disponíveis depois de instalar e configurar o ponto de atualização de software inicial.  

> [!IMPORTANT]  
>  Não há suporte para instalar a função do sistema de site do ponto de atualização de software em um servidor que tenha sido configurado e usado como um servidor do WSUS autônomo ou usando um ponto de atualização de software para gerenciar diretamente os clientes do WSUS. Os servidores do WSUS existentes têm suporte apenas como origens da sincronização upstream para o ponto de atualização de software ativo. Veja [Sincronizar por meio de um local de fonte de dados upstream](#BKMK_wsussync)

 Você pode adicionar a função do sistema de site do ponto de atualização de software a um servidor do sistema de site existente ou criar um novo. Na página **Seleção de Função do Sistema** do **Assistente para Criar Servidor do Sistema de Site** ou do **Assistente para Adicionar Funções do Sistema de Site, dependendo se você adicionar a função do sistema de site a um servidor do site novo ou existente, selecione **Ponto de atualização de software** e configure os parâmetros de atualização de software no assistente. As configurações são diferentes dependendo da versão do Configuration Manager que você usa. Para obter mais informações sobre como instalar funções do sistema de sites, veja [Instalar funções do sistema de sites](../../core/servers/deploy/configure/install-site-system-roles.md).  

 Use as seções a seguir para obter informações sobre as configurações do ponto de atualização de software em um site.  

## <a name="proxy-server-settings"></a>Configurações do servidor proxy  
 É possível configurar os parâmetros do servidor proxy em diferentes páginas do **Assistente para Criar Servidor do Sistema de Sites** ou do **Assistente para Adicionar Funções do Sistema de Sites** dependendo da versão do Configuration Manager que você usa.  

-   Você deve configurar o servidor proxy e especificar quando usar esse servidor para atualizações de software. Defina as seguintes configurações:  

    -   Defina as configurações do servidor proxy na página **Proxy** do assistente ou na guia **Proxy** em Propriedades do Sistema de Site. As configurações do servidor proxy são específicas do sistema de site, o que significa que todas as funções do sistema de site usam as configurações de servidor proxy que você especificar.  

    -   Especifique se é para usar o servidor proxy quando o Configuration Manager sincroniza as atualizações de software e baixa conteúdo usando uma regra de implantação automática. Defina as configurações do servidor proxy do ponto de atualização do software na página **Configurações de Proxy e Conta** do assistente ou na guia **Configurações de Proxy e Conta** em Propriedades do Ponto de Atualização de Software.  

        > [!NOTE]  
        >  A configuração **Usar um proxy ao baixar conteúdo usando regras de implantação automática** está disponível, mas não é usada para um ponto de atualização de software em um site secundário. Somente o ponto de atualização de software no site de administração central e no site primário baixa conteúdo da página do Microsoft Update.  

> [!IMPORTANT]  
>  Por padrão, a conta **Sistema Local** do servidor em que uma regra de implantação automática foi criada é usada para conectar à Internet e baixar atualizações de software quando as regras de implantação automática forem executadas. Quando essa conta não tem acesso à Internet, as atualizações de software não são baixadas e a seguinte entrada é registrada em ruleengine.log: **Falha ao baixar a atualização da Internet. Erro = 12007**. Configure as credenciais para conectar ao servidor proxy quando a conta Sistema Local não tem acesso à Internet.  


## <a name="wsus-settings"></a>Configurações do WSUS  
 É necessário definir as configurações do WSUS em diferentes páginas do **Assistente para Criar Servidor do Sistema de Sites** ou do **Assistente para Adicionar Funções do Sistema de Sites** dependendo da versão do Configuration Manager que você usa e, em alguns casos, somente nas propriedades do ponto de atualização de software, também conhecidas como Propriedades do Componente de Ponto de Atualização de Software. Use as informações das seções a seguir para configurar o WSUS.  

### <a name="BKMK_wsusport"></a> Configurações de porta do WSUS  
 Você deve configurar os parâmetros da porta do WSUS na página Ponto de Atualização de Software do assistente ou nas propriedades do ponto de atualização de software. Use o procedimento a seguir para determinar as configurações de porta usadas pelo WSUS.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>Para determinar as configurações de porta usadas no IIS  

 1.  No servidor WSUS, abra o Gerenciador do IIS (Serviços de Informações da Internet).  

 2.  Expanda **Sites**, clique com o botão direito do mouse no site do servidor WSUS e clique em **Editar Ligações**. No diálogo Ligações do Site, os valores de porta HTTP e HTTPS são exibidos na coluna **Porta** .


### <a name="configure-ssl-communications-to-wsus"></a>Configurar as comunicações SSL para o WSUS  
 É possível configurar a comunicação SSL na página **Geral** do assistente ou na guia **Geral** das propriedades do ponto de atualização de software.  

 Para obter mais informações sobre como usar o SSL, veja [Decide whether to configure WSUS to use SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL).  

### <a name="wsus-server-connection-account"></a>Conta de conexão do servidor do WSUS  
 Você pode configurar uma conta para ser usada pelo servidor do site quando ele se conecta ao WSUS executado no ponto de atualização de software. Quando você não configura essa conta, o Configuration Manager usa a conta de computador do servidor do site para se conectar ao WSUS. Configure a Conta de Conexão do Servidor do WSUS na página **Configurações de Proxy e Conta** do assistente ou na guia **Configurações de Proxy e Conta** nas Propriedades do Ponto de atualização de software.  É possível configurar a conta em diferentes locais do assistente dependendo da versão do Configuration Manager que você usa.  

 Para obter mais informações sobre contas do Configuration Manager, consulte [Contas usadas no System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## <a name="synchronization-source"></a>Origem de sincronização  
 Você pode configurar a origem da sincronização upstream para a sincronização de atualizações de software na página **Origem da Sincronização** do assistente ou na guia **Configurações de Sincronização** em Propriedades do Componente de Ponto de Atualização de Software. As opções de origem da sincronização variam dependendo do site.  

 Use a tabela a seguir para obter as opções disponíveis ao configurar o ponto de atualização de software em um site.  

|Site|Opções de origem da sincronização disponíveis|  
|----------|----------------------------------------------|  
|-   Site de administração central<br />-   Site primário autônomo|-   Sincronizar do site Microsoft Update<br />-   Sincronizar por meio de um local de fonte de dados upstream<br />-   Não sincronizar do Microsoft Update ou da fonte de dados upstream|  
|-   Pontos de atualização de software adicionais em um site<br />-   Site primário filho<br />-   Site secundário|-   Sincronizar por meio de um local de fonte de dados upstream|  

 A lista a seguir fornece mais informações sobre cada opção que você pode usar como origem da sincronização:  

-   **Sincronizar do Microsoft Update**: use essa configuração para sincronizar metadados de atualizações de software do Microsoft Update. O site de administração central deve ter acesso à Internet; caso contrário, a sincronização falhará. Essa configuração está disponível apenas quando você configura o ponto de atualização de software no site de nível superior.  

    > [!NOTE]  
    >  Quando há um firewall entre o ponto de atualização de software e a Internet, o firewall pode precisar configurar o firewall para aceitar as portas HTTP e HTTPS usadas para o site do WSUS. Você também pode restringir o acesso no firewall a domínios limitados. Para obter mais informações sobre como planejar um firewall que dá suporte a atualizações de software, veja [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   **<a name="BKMK_wsussync"></a>Sincronizar a partir de um local de fonte de dados upstream**: use essa configuração para sincronizar os metadados das atualizações de software da origem de sincronização upstream. Os sites primários filhos e os sites secundários são automaticamente configurados para usar o URL do site pai para essa configuração. Você tem a opção de sincronizar as atualizações de software em um servidor do WSUS existente. Especifique um URL, como https://WSUSServer:8531, em que 8531 é a porta usada para se conectar ao servidor WSUS.  

-   **Não sincronizar do Microsoft Update ou da fonte de dados upstream**: use essa configuração para sincronizar manualmente as atualizações de software quando o ponto de atualização de software no site de nível superior estiver desconectado da Internet. Para obter mais informações, consulte [Synchronize software updates from a disconnected software update point](synchronize-software-updates-disconnected.md) (Sincronizar atualizações de software de um ponto de atualização de software desconectado).  

> [!NOTE]  
>  Quando há um firewall entre o ponto de atualização de software e a Internet, o firewall pode precisar configurar o firewall para aceitar as portas HTTP e HTTPS usadas para o site do WSUS. Você também pode restringir o acesso no firewall a domínios limitados. Para obter mais informações sobre como planejar um firewall que dá suporte a atualizações de software, veja [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

 Você também pode configurar se deseja criar eventos de relatório do WSUS na página **Origem de Sincronização** do assistente ou na guia **Configurações de Sincronização** nas propriedades do Componente do Ponto de Atualização de Software. O Configuration Manager não usa esses eventos; portanto, normalmente você escolherá a configuração padrão **Não criar eventos de relatório do WSUS**.  

## <a name="synchronization-schedule"></a>Agendamento de sincronização  
 Configure a agenda de sincronização na página **Agenda de Sincronização** do assistente ou em Propriedades do Componente de Ponto de Atualização de Software. Essa configuração é definida somente no ponto de atualização de software no site de nível superior.  

 Ao habilitar a agenda, você poderá configurar um agendamento de sincronização simples e recorrente ou personalizado. Quando você configura um agendamento simples, o horário de início é baseado na hora local do computador que executa o console do Configuration Manager no momento em que a agenda é criada. Quando você configura a hora de início para um agendamento personalizado, ela é baseada no horário local do computador que executa o console do Configuration Manager.  

> [!TIP]  
>  Agende a sincronização de atualizações de software para ser executada em um período apropriado ao seu ambiente. Um cenário típico é definir a agenda de sincronização de atualizações de software para ser executada logo após o lançamento da atualização de segurança regular da Microsoft na segunda terça-feira de cada mês, que é normalmente conhecida como Patch Tuesday. Outro cenário típico é definir a agenda de sincronização de atualizações de software para ser executada diariamente quando você usar as atualizações de software para fornecer atualizações de mecanismos e definições do Endpoint Protection.  

> [!NOTE]  
>  Ao optar por não permitir a sincronização de atualizações de software em uma agenda, você poderá sincronizar manualmente as atualizações de software nos nós **Todas as Atualizações de Software** ou **Grupos de Atualização de Software** , no espaço de trabalho Biblioteca de Software. Para mais informações, consulte [Sincronizar atualizações de software](synchronize-software-updates.md).  

## <a name="supersedence-rules"></a>Regras de substituição  
 Configure as definições de substituição na página **Regras de Substituição** do assistente ou na guia **Regras de Substituição** em Propriedades do Componente de Ponto de Atualização de Software. Você pode configurar as regras de substituições somente no site de nível superior.  

 Nesta página, você pode determinar que as atualizações de software substituídas sejam imediatamente expiradas, o que as impedirá de serem incluídas em novas implantações e sinalizará as implantações existentes para indicar que as atualizações de software substituídas contêm uma ou mais atualizações de software expiradas. Ou, você pode especificar um período de tempo até que as atualizações de software substituídas se expirem, o que permitirá que você continue a implantá-las. Para obter mais informações, consulte [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  A página **Regras de Substituição** do assistente está disponível apenas quando você configura o primeiro ponto de atualização de software no site. Essa página não é exibida quando você instala pontos de atualização de software adicionais.  

## <a name="classifications"></a>Classificações  
 Configure as definições de classificação na página **Classificações** do assistente ou na guia **Classificações** em Propriedades do Componente de Ponto de Atualização de Software. Para obter mais informações sobre classificações de atualização de software, veja [Update classifications](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  A página **Classificações** do assistente está disponível apenas quando você configura o primeiro ponto de atualização de software no site. Essa página não é exibida quando você instala pontos de atualização de software adicionais.  

> [!TIP]  
>  Ao instalar pela primeira vez o ponto de atualização de software no site de nível superior, desmarque todas as classificações de atualizações de software. Após a sincronização inicial das atualizações de software, configure as classificações de uma lista atualizada e reinicie a sincronização. Essa configuração é definida somente no ponto de atualização de software no site de nível superior.  

## <a name="products"></a>Produtos  
 Configure as definições de produto na página **Produtos** do assistente ou na guia **Produtos** em Propriedades do Componente de Ponto de Atualização de Software.  

> [!NOTE]  
>  A página **Produtos** do assistente está disponível apenas quando você configura o primeiro ponto de atualização de software no site. Essa página não é exibida quando você instala pontos de atualização de software adicionais.  

> [!TIP]  
>  Ao instalar pela primeira vez o ponto de atualização de software no site de nível superior, desmarque todos os produtos. Após a sincronização inicial das atualizações de software, configure os produtos de uma lista atualizada e reinicie a sincronização. Essa configuração é definida somente no ponto de atualização de software no site de nível superior.  

## <a name="languages"></a>Idiomas  
 Configure as definições de idioma na página **Idiomas** do assistente ou na guia **Idiomas** em Propriedades do Componente de Ponto de Atualização de Software. Especifique os idiomas para os quais você quer sincronizar os arquivos de atualização de software e detalhes do resumo. A configuração do **Arquivo de Atualização de Software** é configurada em cada ponto de atualização de software da hierarquia do Configuration Manager. As configurações **Detalhes do Resumo** são definidas somente no ponto de atualização de software de nível superior. Para obter mais informações, consulte [Languages](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  A página **Idiomas** do assistente está disponível apenas quando você instala o ponto de atualização de software no site de administração central. Você pode configurar os idiomas do Arquivo de Atualização de Software em sites filhos na guia **Idiomas** em Propriedades do Componente de Ponto de Atualização de Software.  

## <a name="third-party-updates"></a>Atualizações de terceiros
A partir do Configuration Manager versão 1802, você pode habilitar atualizações de terceiros para clientes do Configuration Manager. Quando você habilitar as atualizações de software nas propriedades de componente de SUP, o SUP baixará o certificado de autenticação usado pelo WSUS para atualizações de terceiros. Essa opção não está disponível durante a instalação do ponto de atualização de software e deve ser configurada depois que o SUP for instalado. Para habilitar as configurações do cliente para atualizações de terceiros, consulte o [Sobre configurações do cliente](/sccm/core/clients/deploy/about-client-settings#Enable-third-party-software-updates) artigo.

## <a name="next-steps"></a>Próximas etapas
Você instalou o ponto de atualização de software iniciando no site de mais alto na hierarquia do Configuration Manager. Repita os procedimentos deste artigo para instalar o ponto de atualização de software em sites filho.

Depois de instalar os pontos de atualização de software, vá para [sincronizar atualizações de software](synchronize-software-updates.md).
