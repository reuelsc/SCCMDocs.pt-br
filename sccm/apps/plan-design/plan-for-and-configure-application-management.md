---
title: Planejar e configurar o gerenciamento de aplicativos
titleSuffix: Configuration Manager
description: "Implemente e configure as dependências necessárias para implantar aplicativos no System Center Configuration Manager."
ms.custom: na
ms.date: 11/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
caps.latest.revision: "13"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: cd06d3ee2ea14c9ff1b9cf09980c2b25a5263db9
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>Planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações descritas neste artigo como auxílio para implantar as dependências necessárias para implantar aplicativos no System Center Configuration Manager.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Dependência|Mais informações|  
|------------------|----------------------|  
|O IIS (Serviços de Informações da Internet) é necessário nos servidores do sistema de sites que executam o ponto de sites da Web e o ponto de serviço Web do Catálogo de Aplicativos, o ponto de gerenciamento e o ponto de distribuição.|Para obter mais informações sobre este requisito, veja [Configurações com suporte](../../core/plan-design/configs/supported-configurations.md).|  
|Dispositivos móveis registrados pelo Configuration Manager|Quando você assinar o código de aplicativos para implantá-los nos dispositivos móveis, não use um certificado que tenha sido gerado usando um modelo de Versão 3 (**Windows Server 2008, Enterprise Edition**). Esse modelo de certificado cria um certificado não compatível com aplicativos do Configuration Manager para dispositivos móveis.<br /><br /> Se você usa os Serviços de Certificados do Active Directory para assinar o código de aplicativos para aplicativos de dispositivo móvel, não use um modelo de certificado de Versão 3.|  
|Clientes deverão ser configurados para fazer auditoria de eventos de entrada, se você quiser criar automaticamente afinidades de dispositivo de usuário.|O cliente do Configuration Manager lê os eventos de logon do tipo **sucesso** do log de eventos de segurança do computador para determinar afinidades de dispositivo de usuário automático.  Esses eventos são habilitados pelas duas políticas de auditoria seguintes:<br>**Eventos de logon de conta de auditoria**<br>**Eventos de logon de auditoria**<br>Para criar automaticamente relacionamentos entre usuários e dispositivos, verifique se essas duas configurações estão habilitadas em computadores cliente. Você pode usar a política de grupo do Windows para definir essas configurações.|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager   

|Dependência|Mais informações|  
|------------------|----------------------|  
|Ponto de gerenciamento|Os clientes entram em contato com um ponto de gerenciamento para baixar a política do cliente, para localizar conteúdo e para se conectar ao catálogo de aplicativos.<br /><br /> Se os clientes não podem acessar um ponto de gerenciamento, não podem usar o Catálogo de Aplicativos.|  
|Ponto de distribuição|Para os aplicativos serem implantados nos clientes, tenha pelo menos um ponto de distribuição na hierarquia. Por padrão, o servidor do site possui uma função de site de ponto de distribuição habilitada durante uma instalação padrão. O número e a localização dos pontos de distribuição variam de acordo com os requisitos específicos de sua empresa.<br /><br /> Para obter mais informações sobre como instalar pontos de distribuição e gerenciar conteúdo, consulte [Gerenciar conteúdo e infraestrutura de conteúdo](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Configurações do cliente|Muitas configurações do cliente controlam como os aplicativos são instalados no cliente e a experiência do usuário no cliente. Essas configurações do cliente incluem:<br /><br /><ul><li>Agente de Computador</li><li>Reinicialização do computador</li><li>Implantação de software</li><li>Afinidade de dispositivo e de usuário</li></ul> Para mais informações sobre essas configurações do cliente, consulte [Sobre as configurações do cliente](../../core/clients/deploy/about-client-settings.md).<br /><br /> Para saber mais sobre como definir as configurações do cliente, consulte [Como definir as configurações do cliente](../../core/clients/deploy/configure-client-settings.md).|  
|Contas de usuário descobertas para Catálogo de Aplicativos |O Configuration Manager deve primeiro descobrir as contas de usuários antes que os usuários possam exibir e solicitar aplicativos do Catálogo de Aplicativos. Para mais informações, consulte [Executar descoberta](/sccm/core/servers/deploy/configure/run-discovery).|  
|Cliente App-V 4.6 SP1 ou posterior para executar aplicativos virtuais|Para criar aplicativos virtuais no Configuration Manager, os computadores cliente devem ter o cliente App-V 4.6 SP1 ou posterior instalado.<br /><br /> É necessário atualizar o cliente App-V com o hotfix descrito na Base de Dados de Conhecimento, [artigo 2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) antes de implantar aplicativos virtuais.|  
|Ponto de serviços Web do Catálogo de Aplicativos|O ponto de serviços Web do catálogo de aplicativos é uma função de sistema de site que fornece informações sobre softwares disponíveis da Biblioteca de Software para os sites da Web do catálogo de aplicativos.<br /><br /> Para saber mais sobre como configurar esta função do sistema de sites, veja [Configurar o Centro de Software e o Catálogo de Aplicativos (apenas para computadores Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) neste artigo.|  
|Ponto de sites da Web do catálogo de aplicativos|O ponto de sites da Web do catálogo de aplicativos é uma função de sistema de site que fornece aos usuários uma lista de softwares disponíveis.<br /><br /> Para saber mais sobre como configurar esta função do sistema de sites, veja [Configurar o Centro de Software e o Catálogo de Aplicativos (apenas para computadores Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) neste artigo.|  
|Ponto do Reporting Services|Para usar os relatórios no Configuration Manager para gerenciamento de aplicativos, primeiro instale e configure um ponto do Reporting Services.<br /><br /> Para obter mais informações, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).|  
|Permissões de segurança para gerenciamento de aplicativos|Você deve ter as seguintes permissões de segurança para gerenciar aplicativos:<br /><br /> A função de segurança **Autor de Aplicativos** inclui as permissões listadas anteriormente que são necessárias para criar, alterar e desativar aplicativos no Configuration Manager.<br /><br /> **Para implantar aplicativos:**<br /><br /> A função de segurança **Gerenciador de Implantação de Aplicativos** inclui as permissões listadas anteriormente que são necessárias para implantar aplicativos no Configuration Manager.<br /><br /> A função de segurança do **Administrador de Aplicativos** tem todas as permissões de ambas as funções de segurança: **Autor de Aplicativos** e **Gerenciador de Implantação de Aplicativos**.<br /><br /> Para mais informações, consulte [Configurar administração baseada em funções](../../core/servers/deploy/configure/configure-role-based-administration.md).|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>Configurar o Centro de Software e o Catálogo de Aplicativos (somente computadores com Windows)  

 No System Center Configuration Manager, agora você tem duas opções para que os usuários alterem configurações, procurem e instalem aplicativos:  

-   **O novo Centro de Software**: o novo Centro de Software tem uma aparência moderna. Os aplicativos que só eram exibidos no Catálogo de Aplicativos dependente do Silverlight (aplicativos disponíveis para o usuário) agora aparecem no Centro de Software sob a guia **Aplicativos**. O Catálogo de Aplicativos ainda pode ser acessado usando o link na guia **Status da Instalação** do Centro de Software.  

     É possível configurar clientes para usar o novo Centro de Software habilitando a configuração do cliente **Agente de Computador** > **Usar o novo Centro de Software**.  

    > [!IMPORTANT]  
    >  Embora não seja mais necessário conectar-se ao Catálogo de Aplicativos, você ainda deve configurar o ponto de sites da Web e o ponto de serviço Web do Catálogo de Aplicativos, conforme detalhado na próxima seção.  

-   **O Centro de Software e o Catálogo de Aplicativos anteriores**: por padrão, os usuários continuam se conectando à versão anterior do Centro de Software e conectando-se ao Catálogo de Aplicativos (navegador da Web habilitado para Silverlight necessário) para procurar os aplicativos disponíveis.  

 Qualquer que seja a versão que você optar por usar, o Centro de Software é instalado automaticamente durante a instalação do cliente do Configuration Manager em computadores com Windows.  

    > [!TIP]  
    >  A versão do Centro de Software vista pelos usuários baseia-se nas configurações do cliente do Configuration Manager. Isso fornece a flexibilidade para controlar a versão que é usada com base nas configurações personalizadas do cliente que são implantadas em uma coleção. 

    > [!IMPORTANT]
    > Nos próximos meses, removeremos a versão anterior do Software Center e ela não estará mais disponível.
    > É possível configurar clientes para usar o novo Centro de Software habilitando a configuração do cliente **Agente de Computador** > **Usar o novo Centro de Software**. 

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>Etapas para instalar e configurar o Catálogo de Aplicativos e o Centro de Software  

> [!IMPORTANT]  
>  Antes de executar essas etapas, verifique se você atendeu a todos os pré-requisitos listados anteriormente.  

|Etapas|Detalhes|Mais informações|  
|-----------|-------------|----------------------|  
|**Etapa 1:** se você usar conexões HTTPS, verifique primeiro se você implantou um certificado do servidor Web nos servidores do sistema de sites.|Implante um certificado do servidor Web nos servidores do sistema de site que executarão o ponto de sites da Web do catálogo de aplicativos e ponto de serviços Web do catálogo de aplicativos.<br /><br /> Além disso, se você desejar que clientes usem o Catálogo de Aplicativos pela Internet, implante um certificado do servidor Web em ao menos um servidor do sistema de site do ponto de gerenciamento e configure-o para conexões de clientes pela Internet.|Para saber mais sobre os requisitos de certificado PKI, consulte [Requisitos do certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Etapa 2:** se você usar um certificado PKI de cliente para conexões a pontos de gerenciamento, implante um certificado de autenticação de cliente nos computadores cliente.|Apesar de os clientes não usarem um certificado PKI de cliente para se conectarem ao Catálogo de Aplicativos, eles precisam se conectar ao ponto de gerenciamento para poderem usar o Catálogo de Aplicativos. Você deve implantar um certificado de autenticação de cliente em computadores cliente nos seguintes cenários:<br /><br /><ul><li>Todos os pontos de gerenciamento na intranet aceitam apenas conexões de clientes HTTPS.</li><li>Os clientes se conectam ao Catálogo de Aplicativos pela Internet.</li></ul>|Para saber mais sobre os requisitos de certificado PKI, consulte [Requisitos do certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Etapa 3:** Instale e configure o ponto de serviços Web do catálogo de aplicativos e o site do catálogo de aplicativos.|Você deve instalar as duas funções do sistema de site no mesmo site. Não é necessário instalá-las no mesmo servidor do sistema de site ou na mesma floresta do Active Directory. No entanto, o ponto de serviço Web do catálogo de aplicativos deve estar na mesma floresta que o banco de dados do site.|Para obter mais informações sobre o posicionamento de funções do sistema de sites, consulte [Planejamento para servidores de sistema de sites e funções de sistema de sites](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).<br /><br /> Para configurar o ponto de serviço Web e o ponto de sites da Web do Catálogo de Aplicativos, veja **Etapa 3: Instalar e configurar as funções do sistema de sites do Catálogo de Aplicativos**.|  
|**Etapa 4:** Definir as configurações do cliente para o Catálogo de Aplicativos e o Centro de Software.|Defina as configurações do cliente padrão se você desejar que todos os usuários tenham a mesma configuração. Caso contrário, defina as configurações do cliente personalizadas para coleções específicas.|Para mais informações sobre configurações do cliente, consulte [Sobre as configurações do cliente](../../core/clients/deploy/about-client-settings.md).<br /><br /> Para saber mais sobre como definir estas configurações do cliente, veja **Etapa 4: Definir as configurações do cliente para o Catálogo de Aplicativos e o Centro de Software**.|  
|**Etapa 5:** Verificar se o Catálogo de Aplicativos está funcionando.|Você pode usar o Catálogo de Aplicativos diretamente de um navegador ou do Centro de Software.|Veja **Etapa 5: Verificar se o Catálogo de Aplicativos está funcionando**.|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>Procedimentos complementares para instalar e configurar o catálogo de aplicativos e o Centro de Software  
 Use as seguintes informações quando as etapas descritas na tabela anterior exigirem procedimentos complementares.  

###  <a name="step-3-install-and-configure-the-application-catalog-site-system-roles"></a>Etapa 3: instalar e configurar as funções do sistema de site do catálogo de aplicativos  
 Esses procedimentos configuram as funções do sistema de site para o catálogo de aplicativos. Escolha um dos dois procedimentos a seguir dependendo se você instalará um novo servidor do sistema de sites ou se usará um servidor do sistema de sites existente:  

> [!NOTE]  
>  O catálogo de aplicativos não pode ser instalado em um site secundário ou um site de administração central.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>Para instalar e configurar os sistemas de site do catálogo de aplicativos: Novo servidor do sistema de site  

1.  No console do Configuration Manager, escolha **Administração** > **Configuração do Site** > **Funções de Servidores e Sistema de Site**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Servidor do Sistema de Site**.  

4.  Na página **Geral**, especifique as configurações gerais para o sistema de site e, em seguida, escolha **Próximo**.  

    > [!TIP]  
    >  Se você deseja que computadores cliente usem o Catálogo de Aplicativos pela Internet, especifique o FQDN (nome de domínio totalmente qualificado) de Internet.  

5.  Na página **Seleção de Função do Sistema**, selecione **Ponto de serviço Web do Catálogo de Aplicativos** e **Ponto de sites da Web do Catálogo de Aplicativos** na lista de funções disponíveis e escolha **Próximo**.  

6.  Conclua as etapas restantes.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>Para instalar e configurar os sistemas de site do catálogo de aplicativos: Servidor do sistema de site existente  

1.  No console do Configuration Manager, escolha **Administração** > **Configuração do Site** > **Funções de Servidores e Sistema de Site** e selecione o servidor a ser usado para o Catálogo de Aplicativos.  

3.  Na guia **Início**, no grupo **Servidor**, clique em **Adicionar funções do sistema de sites**.  

4.  Na página **Geral**, especifique as configurações gerais para o sistema de site e, em seguida, escolha **Próximo**.  

    > [!TIP]  
    >  Se você deseja que computadores cliente usem o Catálogo de Aplicativos pela Internet, especifique o FQDN (nome de domínio totalmente qualificado) de Internet.  

5.  Na página **Seleção de Função do Sistema**, selecione **Ponto de serviço Web do Catálogo de Aplicativos** e **Ponto de sites da Web do Catálogo de Aplicativos** na lista de funções disponíveis e escolha **Próximo**.  

6.  Conclua as etapas restantes.  

7. Verifique a instalação dessas funções do sistema de site usando as mensagens de status e analisando os arquivos de log:  

    Mensagens de status: Use os componentes **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Por exemplo, a ID do status **1015** para **SMS_PORTALWEB_CONTROL_MANAGER** confirma se o Gerenciador do Componente de Site instalou com êxito o ponto de sites da Web do Catálogo de Aplicativos.  

    Arquivos de log: Procure **SMSAWEBSVCSetup.log** e **SMSPORTALWEBSetup.log**.  

    Para obter mais informações, pesquise os arquivos de log **awebsvcMSI.log** e **portlwebMSI.log**.  

###  <a name="step-4-configure-the-client-settings-for-the-application-catalog-and-software-center"></a>Etapa 4: definir as configurações do cliente para o Catálogo de Aplicativos e o Centro de Software  
 Esse procedimento define as configurações do cliente padrão para o Catálogo de Aplicativos e o Centro de Software que se aplicam a todos os dispositivos na hierarquia. Se você deseja que essas configurações se apliquem a somente alguns dispositivos, é possível criar uma configuração personalizada do cliente e implantá-la em uma coleção que tem os dispositivos com as configurações específicas. Para saber mais sobre como criar uma configuração de dispositivo personalizada, veja a seção [Como criar e implantar configurações personalizadas do cliente](../../core/clients/deploy/configure-client-settings.md#create-and-deploy-custom-client-settings) em [Definindo as configurações de gerenciamento de cliente no Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  

3.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

4.  Analise e defina as configurações relacionadas a notificações de usuário, catálogo de aplicativos e Centro de Software. Por exemplo:  

    1.  Grupo**Agente de Computador** :  

        -   **Ponto de sites do Catálogo de Aplicativos padrão**.  

        -   **Adicionar sites do Catálogo de Aplicativos padrão à zona de sites confiáveis do Internet Explorer**.  

        -   **Nome da organização exibido no Centro de Software**.  

            > [!TIP]  
            >  Para especificar o nome da organização exibido no Catálogo de Aplicativos e configurar o tema do site, use a guia **Personalização** nas propriedades de sites da Web do Catálogo de Aplicativos.  

        -   **Usar o novo Centro de Software**. Defina como **Sim** se quiser usar o novo Centro de Software, que permite aos usuários procurar e instalar aplicativos disponíveis sem a necessidade de acessar o Catálogo de Aplicativos (que exige um navegador da Web habilitado para Silverlight).  

        -   **Permissões de instalação**.  

        -   **Mostrar notificações para novas implantações**.  

    2.  Grupo**Gerenciamento de Energia** :  

        -   **Permitir que os usuários excluam seu dispositivo do gerenciamento de energia**.  

    3.  Grupo**Ferramentas Remotas** :  

        -   **Os usuários podem alterar as configurações de política ou notificação no Centro de Software**.  

    4.  Grupo**Afinidade de Usuário e Dispositivo** :  

        -   **Permitir que os usuários definam seus dispositivos primários**.  

    > [!NOTE]  
    >  Para obter mais informações sobre as configurações do cliente, consulte [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

5.  Escolha **OK** para fechar a caixa de diálogo **Configurações do Cliente Padrão**.  

Os computadores cliente serão definidos com essas configurações durante o próximo download da política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [Como gerenciar clientes](../../core/clients/manage/manage-clients.md).

#### <a name="to-customize-software-center-branding"></a>Para personalizar a identidade visual do Centro de Software

A identidade visual personalizada do Centro de Software é aplicada de acordo com as regras a seguir:

1. Se a função de servidor do site ponto de sites da Web do Catálogo de Aplicativos não estiver instalada, o Centro de Software exibirá o nome da organização especificado na configuração do cliente **Nome da organização** do **Agente de Computador** exibido no Centro de Software. Para ver instruções, consulte [How to configure client settings (Como definir as configurações do cliente)](https://docs.microsoft.com/sccm/core/clients/deploy/configure-client-settings).
2. Se a função de servidor do site ponto de sites da Web do catálogo de aplicativos estiver instalada, o Centro de Software exibirá o nome da organização a e cor especificados nas propriedades da função de servidor do site ponto de sites da Web do catálogo de aplicativos. Para obter mais informações, consulte [Configuration options for Application Catalog website point (Opções de configuração do ponto de sites da Web do catálogo de aplicativos)](https://docs.microsoft.com/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).
3. Se uma assinatura do Microsoft Intune estiver configurada e conectada ao Configuration Manager, o Centro de Software exibirá o nome da organização, a cor e o logotipo da empresa especificados nas propriedades de assinatura do Intune. Para obter mais informações, consulte [Configuring the Microsoft Intune subscription](https://docs.microsoft.com/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).

#### <a name="to-manually-set-software-center-branding"></a>Para definir manualmente a identidade visual do Centro de Software
<!-- 1351224 -->
Com a versão 1710, você pode adicionar elementos de identidade visual da empresa e especificar a visibilidade das guias no Centro de Software manualmente. Você pode adicionar o nome específico da empresa do Centro de Software, definir um tema de cores de configuração do Centro de Software, definir um logotipo da empresa e definir as guias visíveis para os dispositivos cliente.

1. No console do **Configuration Manager**, escolha **Administração** > **Configurações do Cliente**. Clique na instância de configuração de cliente desejada.
2. Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.
3. Na caixa de diálogo **Configurações Padrão**, escolha **Centro de Software**.
4. Selecione **Sim** para **Selecionar novas configurações para especificar as informações da empresa** para habilitar as configurações de personalização do Centro de Software.
5. Digite o **Nome da empresa**.
6. Selecione o **Esquema de Cores do Centro de Software**.
7. Clique em **Procurar** para buscar seu logotipo do Centro de Software. O logotipo deve ser um JPEG ou PNG de 400 x 100 pixels com tamanho máximo de 750 KB.
8. Selecione **SIM** para tornar as guias visíveis no Centro de Software para dispositivos cliente. Pelo menos uma guia deve ser visível:

    -  Habilitar a guia Aplicativos
    -  Habilitar o guia Atualizações
    -  Habilitar a guia Sistemas Operacionais
    -  Habilitar a guia Status de Instalação
    -  Habilitar a guia Conformidade do dispositivo
    -  Habilitar a guia Opções

> [!IMPORTANT]  
>  A identidade visual do Centro de Software é sincronizada com o serviço Intune a cada 14 dias. Portanto, pode ocorrer um atraso antes que as alterações feitas no Intune sejam exibidas no Configuration Manager.

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Etapa 5: Verificar se o Catálogo de Aplicativos está funcionando  
 Use os procedimentos a seguir para verificar se o catálogo de aplicativos está operacional. Você pode usar o Catálogo de Aplicativos diretamente de um navegador ou do Centro de Software.  

> [!NOTE]  
>  O catálogo de aplicativos requer o Microsoft Silverlight, que é instalado automaticamente como um pré-requisito de cliente do Configuration Manager. Se você usa o catálogo de aplicativos diretamente de um navegador usando um computador que não tem o cliente do Configuration Manager instalado, verifique primeiramente se o Microsoft Silverlight está instalado no computador.  

> [!TIP]  
>  Os pré-requisitos ausentes correspondem aos motivos mais comuns do mau funcionamento do Catálogo de Aplicativos após a instalação. Confirme se os pré-requisitos de função do sistema de site para as funções do sistema de site do catálogo de aplicativos. Você pode fazer isso usando o artigo [Configurações com suporte](../../core/plan-design/configs/supported-configurations.md).  

> [!NOTE]  
>  Se você entrar usando uma conta de Administrador de domínio, as mensagens de notificação do cliente do Configuration Manager (por exemplo, mensagens indicando que novos softwares estão disponíveis) não serão exibidas.  

### <a name="to-use-the-application-catalog-directly-from-a-browser"></a>Para usar o Catálogo de Aplicativos diretamente de um navegador  

-   No navegador, digite o endereço do site da Web do Catálogo de Aplicativos e confirme se a página da Web exibe estas três guias: **Catálogo de Aplicativos**, **Minhas Solicitações de Aplicativos**e **Meus Dispositivos**.  

     Selecione e use o endereço apropriado na lista a seguir para o Catálogo de Aplicativos, em que &lt;servidor&gt; é o nome do computador, FQDN da intranet ou FQDN da Internet:  

    -   Conexões de cliente HTTPS e configurações padrão de função do sistema de sites: **https://&lt;servidor&gt;/CMApplicationCatalog**  

    -   Conexões de cliente HTTP e configurações padrão de função do sistema de sites: **http://&lt;servidor&gt;/CMApplicationCatalog**  

    -   Conexões de cliente HTTPS e configurações personalizadas de função do sistema de sites: **https://&lt;servidor&gt;:&lt;porta&gt;/&lt;nome do aplicativo Web&gt;**  

    -   Conexões de cliente HTTP e configurações personalizadas de função do sistema de sites: **http://&lt;servidor&gt;:&lt;porta&gt;/&lt;nome do aplicativo Web&gt;**  

### <a name="to-use-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>Para usar o Catálogo de Aplicativos do Centro de Software (não se aplica à nova versão do Centro de Software)  

1.  Em um computador cliente, selecione **Iniciar** > **Todos os Programas** > **Microsoft System Center 2012** > **Configuration Manager** > **Centro de Software**.  

2.  Se você configurou anteriormente um nome organizacional para o Software Center como uma configuração de cliente, confirme se isso é exibido conforme especificado.  

3.  Selecione **Encontrar aplicativos adicionais no Catálogo de Aplicativos** e confirme se a página exibe estas três guias: **Catálogo de Aplicativos**, **Minhas Solicitações de Aplicativos**e **Meus Dispositivos**.  

> [!WARNING]  
>  Após a instalação das funções do sistema de site do Catálogo de Aplicativos, você não verá imediatamente o Catálogo de Aplicativos ao clicar no link **Encontrar aplicativos adicionais no Catálogo de Aplicativos** do Centro de Software. O catálogo de aplicativos ficará disponível no Software Center quando o cliente fizer seus próximos downloads de sua política de cliente ou até 25 horas após a instalação das funções do sistema de site do catálogo de aplicativos.  
