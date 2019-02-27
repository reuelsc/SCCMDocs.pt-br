---
title: Planejar para o gerenciamento de aplicativo
titleSuffix: Configuration Manager
description: Implemente e configure as dependências necessárias para implantar aplicativos no Configuration Manager.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 62d750a6ff711afc06ddbcec9b9ad98ecfab758e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124148"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Planejar e configurar o gerenciamento de aplicativos no Configuration Manager

*Aplica-se a: System Center Configuration Manager (branch atual)*

Use as informações descritas neste artigo como auxílio para implantar as dependências necessárias para implantar aplicativos no Configuration Manager.  



## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  


### <a name="internet-information-services-iis"></a>Serviços de Informações da Internet (IIS)

O IIS é necessário nos servidores que executam as seguintes funções do sistema de sites: 
- Ponto de sites da Web do Catálogo de Aplicativos  
- Ponto de serviços Web do Catálogo de Aplicativos  
- Ponto de gerenciamento  
- Ponto de distribuição  

Para obter mais informações sobre esse requisito, consulte [Pré-requisitos do site e do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Certificados em aplicativos com assinatura de código para dispositivos móveis

Quando você assinar o código de aplicativos para implantá-los nos dispositivos móveis, não use um certificado que tenha sido gerado usando um modelo de Versão 3 (**Windows Server 2008, Enterprise Edition**). Esse modelo de certificado cria um certificado não compatível com aplicativos do Configuration Manager para dispositivos móveis.

Se você usa os Serviços de Certificados do Active Directory para assinar o código de aplicativos para aplicativos de dispositivo móvel, não use um modelo de certificado de Versão 3.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Auditoria de eventos de entrada para afinidade de dispositivo de usuário  

Se você quiser criar automaticamente afinidades de dispositivo de usuário, configure clientes para fazer auditoria de eventos de entrada.

Para determinar afinidades automáticas de dispositivo do usuário, o cliente do Configuration Manager lê os eventos de entrada do tipo **sucesso** do log de eventos de segurança do Windows. Habilite esses eventos com as duas políticas de auditoria seguintes:
- **Eventos de logon de conta de auditoria**
- **Eventos de logon de auditoria**

Para criar automaticamente relacionamentos entre usuários e dispositivos, verifique se essas duas configurações estão habilitadas em computadores cliente. Você pode usar a política de grupo do Windows para definir essas configurações.

Para saber mais sobre afinidade de dispositivo de usuário, veja [Vincular usuários e dispositivos com a afinidade de dispositivo de usuário](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  



## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager   


### <a name="management-point"></a>Ponto de gerenciamento

Os clientes entram em contato com um ponto de gerenciamento para baixar a política do cliente, para localizar conteúdo e para se conectar ao catálogo de aplicativos. Se os clientes não podem acessar um ponto de gerenciamento, não podem usar o Catálogo de Aplicativos.

> [!Note]  
> A partir da versão 1806, as funções do catálogo de aplicativos não são mais necessárias para exibir aplicativos disponíveis ao usuário no Centro de Software. Para saber mais, veja [Configurar Centro de Software](#bkmk_userex).<!--1358309-->  
  

### <a name="distribution-point"></a>Ponto de distribuição

Antes de implantar aplicativos nos clientes, você precisará ter pelo menos um ponto de distribuição na hierarquia. Por padrão, o servidor do site possui uma função de site de ponto de distribuição habilitada durante uma instalação padrão. O número e a localização dos pontos de distribuição variam de acordo com os requisitos específicos de seu ambiente. 

Para obter mais informações sobre como instalar pontos de distribuição e gerenciar conteúdo, consulte [Gerenciar conteúdo e infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  


### <a name="reporting-services-point"></a>Ponto do Reporting Services

Para usar os relatórios no Configuration Manager para gerenciamento de aplicativos, primeiro instale e configure um ponto do Reporting Services.

Para obter mais informações, confira [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting) (Relatórios no Configuration Manager).  


### <a name="client-settings"></a>Configurações do cliente

Muitas configurações de cliente controlam como o cliente instala aplicativos e a experiência do usuário no dispositivo. Essas configurações do cliente incluem os seguintes grupos:
- Agente de Computador  
- Reinicialização do computador  
- Centro de software  
- Implantação de software  
- Afinidade de dispositivo e de usuário  

Para obter mais informações, consulte os seguintes artigos:
- [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings)  
- [Como definir as configurações do cliente](/sccm/core/clients/deploy/configure-client-settings)  


### <a name="security-permissions-for-application-management"></a>Permissões de segurança para gerenciamento de aplicativos

- A função de segurança **Autor de Aplicativos** inclui as permissões necessárias para criar, alterar e desativar aplicativos.  

- A função de segurança **Gerenciador de Implantação de Aplicativos** inclui as permissões necessárias para implantar aplicativos.  

- A função de segurança do **Administrador de Aplicativos** tem todas as permissões de ambas as funções de segurança: **Autor de Aplicativos** e **Gerenciador de Implantação de Aplicativos**.  

Para obter mais informações, confira [Configurar a administração baseada em função](/sccm/core/servers/deploy/configure/configure-role-based-administration).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>Cliente App-V 4.6 SP1 ou posterior para executar aplicativos virtuais

Para criar aplicativos virtuais no Configuration Manager, instale o App-V 4.6 SP1 ou posterior nos dispositivos.

Antes de implantar os aplicativos virtuais, também atualize o cliente do App-V com o hotfix descrito no [artigo de suporte 2645225 da Microsoft](https://support.microsoft.com/help/2645225).  


### <a name="discovered-user-accounts-for-application-catalog"></a>Contas de usuário descobertas para Catálogo de Aplicativos

O Configuration Manager deve primeiro descobrir as contas de usuários antes que os usuários possam exibir e solicitar aplicativos do Catálogo de Aplicativos. Para mais informações, consulte [Executar descoberta](/sccm/core/servers/deploy/configure/run-discovery).  


### <a name="application-catalog-web-service-point"></a>Ponto de serviços Web do Catálogo de Aplicativos

O ponto de serviços Web do Catálogo de Aplicativos é uma função de sistema de site que fornece informações sobre softwares disponíveis da sua biblioteca de software para os sites da Web do catálogo de aplicativos que os usuários acessam.

Para saber mais sobre como configurar esta função do sistema de sites, veja [Configurar Centro de Software](#bkmk_userex).  

> [!Note]  
> A partir da versão 1806, as funções de ponto de serviço de site do catálogo de aplicativos e ponto de serviço Web não são mais *necessária*, mas ainda são *compatíveis*.<!--1358309-->  
> 
> Não há mais suporte para a **experiência do usuário do Silverlight** para o ponto do site do Catálogo de Aplicativos. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="application-catalog-website-point"></a>Ponto de sites da Web do Catálogo de Aplicativos

O ponto de sites da Web do catálogo de aplicativos é uma função de sistema de site que fornece aos usuários uma lista de softwares disponíveis.
Para saber mais sobre como configurar esta função do sistema de sites, veja [Configurar Centro de Software](#bkmk_userex).

> [!Note]  
> A partir da versão 1806, a função de ponto de site do catálogo de aplicativos não são mais *necessária*, mas ainda são *compatíveis*.<!--1358309-->  
> 
> Não há mais suporte para a **experiência do usuário do Silverlight** para o ponto do site do Catálogo de Aplicativos. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  



## <a name="bkmk_userex"></a> Configurar Centro de Software  

Os usuários alteram configurações, procuram e instalam aplicativos do Centro de Software. Quando você instala o cliente do Configuration Manager em um dispositivo do Windows, ele automaticamente instala o Centro de Software. O novo Centro de Software tem uma aparência moderna. Os aplicativos que só eram exibidos no Catálogo de Aplicativos dependente do Silverlight (aplicativos disponíveis para o usuário) agora aparecem no Centro de Software sob a guia **Aplicativos**. Para saber mais sobre os outros recursos do Centro de Software, veja o [Guia do usuário do Centro de Software](/sccm/core/understand/software-center).  

Analise as melhorias a seguir ao Centro de Software: 

#### <a name="starting-in-version-1802"></a>A partir da versão 1802

- A configuração do cliente **Usar o novo Centro de Software** no grupo **Agente de computador** está habilitada por padrão. A versão anterior do Centro de Software não tem mais suporte. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

- Os usuários podem procurar e instalar aplicativos disponíveis para usuários em dispositivos ingressados no Azure Active Directory (Azure AD). Para obter mais informações, consulte [Implantar aplicativos disponíveis para o usuário em dispositivos ingressados no Azure AD](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).  

#### <a name="starting-in-version-1806"></a>A partir da versão 1806

- Especifique a visibilidade do link do site do Catálogo de Aplicativos na guia **Status da Instalação** no Centro de Software. Para saber mais, veja [Configurações de cliente do Centro de Software](/sccm/core/clients/deploy/about-client-settings#software-center).  

- As funções do catálogo de aplicativos não são mais necessárias para exibir aplicativos disponíveis para o usuário no Centro de Software. Essa alteração ajuda a reduzir a infraestrutura de servidor necessária para fornecer aplicativos aos usuários. O Centro de Software agora depende do ponto de gerenciamento para obter essas informações, o que ajuda ambientes maiores a serem melhor dimensionados por meio de suas atribuições a [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).<!--1358309-->  

    > [!Note]  
    > Se você estiver usando o catálogo de aplicativos e atualizar o Configuration Manager para a versão 1806, ele continuará a funcionar. As funções de ponto de site do catálogo de aplicativos e ponto de serviço Web não são mais *necessárias*, mas ainda são *compatíveis*. Não há mais suporte para a **experiência do usuário do Silverlight** para o *ponto do site* do Catálogo de Aplicativos. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). 
    > 
    > Comece planejando a remoção das funções de catálogo do aplicativo de sua infraestrutura no futuro. Aproveite as melhorias do Centro de Software para usar o ponto de gerenciamento e simplifique seu ambiente do Configuration Manager.  

Use a tabela a seguir para ajudar a reconhecer os requisitos do Centro de Software, dependendo da versão específica do Configuration Manager:

| Tipo de dispositivo | Versão do site | Infraestrutura | 
|-----------------|--------------|----------------|
| Dispositivo ingressado no Azure AD</br>(ou "ingressado no domínio de nuvem") | 1802 ou 1806 | Ponto de gerenciamento para todas as implantações de aplicativo | 
| [Dispositivo híbrido que tenha ingressado no Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) na Internet | 1802 ou 1806 | Gateway de gerenciamento de nuvem e ponto de gerenciamento para todas as implantações de aplicativo |
| Dispositivo ingressado no domínio do Active Directory no local | 1802 | Catálogo de aplicativos necessário para os aplicativos disponíveis para o usuário por meio do Centro de Software |
| Dispositivo ingressado no domínio do Active Directory no local | 1806 | Ponto de gerenciamento para todas as implantações de aplicativo |


> [!Important]  
> Para aproveitar os novos recursos do Configuration Manager, primeiro atualize os clientes para a versão mais recente. Embora a nova funcionalidade seja exibida no console do Configuration Manager quando você atualiza o site e o console, o cenário completo só funcionará quando a versão do cliente também for a mais recente.



## <a name="branding-software-center"></a>Centro de Software de identidade visual

Altere a aparência do Centro de Software para atender aos requisitos e identidade visual da sua organização. Essa configuração ajuda os usuários a confiar no Centro de Software. 

O Configuration Manager aplica a identidade visual personalizada para o Centro de Software de acordo com as seguintes prioridades:  

- Se você ainda não instalou o catálogo de aplicativos (recomendado):  

    1. Configurações do cliente do **Centro de Software**. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. Configurações do cliente **Nome da organização** no grupo **Agente de computador**. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- Se você tiver instalado o catálogo de aplicativos:  

    1. Configurações do cliente do **Centro de Software**. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. Se você conectar uma assinatura do Microsoft Intune ao Configuration Manager, o Centro de Software exibirá o *nome da organização*, a *cor* e o *logotipo da empresa* especificados nas propriedades de assinatura do Intune. Para obter mais informações, consulte [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).  

    3. O *nome da organização* e a *cor* que você especificar nas propriedades de ponto de site do Catálogo de Aplicativos. Para obter mais informações, consulte [Configuration options for Application Catalog website point (Opções de configuração do ponto de sites da Web do catálogo de aplicativos)](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).  

    4. Configurações do cliente **Nome da organização** no grupo **Agente de computador**. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

#### <a name="configure-software-center-branding"></a>Configurar identidade visual do Centro de Software
<!-- 1351224 --> Personalize a aparência do Centro de Software adicionando os elementos de identidade visual da sua organização e especificando a visibilidade das guias. 

Para obter mais informações, consulte os seguintes artigos:
- Configurações do grupo de cliente do [Centro de Software](/sccm/core/clients/deploy/about-client-settings#software-center)  
- [Como definir as configurações do cliente](/sccm/core/clients/deploy/configure-client-settings)  



## <a name="bkmk_appcat"></a> Instalar e configurar o Catálogo de Aplicativos  

> [!Note]  
> A partir da versão 1806, as funções de ponto de site do catálogo de aplicativos e ponto de serviço Web não são mais *necessária*, mas ainda são *compatíveis*. Para saber mais, veja [Configurar Centro de Software](#bkmk_userex).  
> 
> Não há mais suporte para a **experiência do usuário do Silverlight** para o *ponto do site* do Catálogo de Aplicativos. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

> [!IMPORTANT]  
>  Antes de realizar essas etapas, verifique se todas as dependências estão em vigor. Para saber mais, veja as seguintes seções neste artigo:
> - [Dependências externas ao Configuration Manager](#dependencies-external-to-configuration-manager)  
> - [Dependências do Configuration Manager](#configuration-manager-dependencies)


### <a name="step-1-web-server-certificate-for-https"></a>Etapa 1: Certificado do servidor Web para HTTPS

Se você usar conexões HTTPS, implante um certificado do servidor Web nos servidores do sistema de site no ponto de sites da Web do Catálogo de Aplicativos e ponto de serviços Web do catálogo de aplicativos. 

Se você quiser que os clientes usem o Catálogo de Aplicativos da Internet, implante um certificado do servidor Web para pelo menos um ponto de gerenciamento. Configure-o para conexões do cliente por meio da Internet.

Para saber mais sobre os requisitos de certificado PKI, consulte [Requisitos do certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Etapa 2: Certificado de autenticação de cliente para HTTPS

Se você usar um certificado PKI de cliente para conexões a pontos de gerenciamento, implante um certificado de autenticação de cliente nos computadores cliente. Apesar de os clientes não usarem um certificado PKI de cliente para se conectarem ao Catálogo de Aplicativos, eles precisam se conectar ao ponto de gerenciamento para poderem usar o Catálogo de Aplicativos. 

Implante um certificado de autenticação de cliente em computadores cliente nos seguintes cenários:
- Todos os pontos de gerenciamento na intranet aceitam apenas conexões de clientes HTTPS.
- Os clientes se conectam ao Catálogo de Aplicativos pela Internet.

Para saber mais sobre os requisitos de certificado PKI, consulte [Requisitos do certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Etapa 3: Instalar e configurar as funções do Catálogo de Aplicativos

Instale o ponto de serviço Web de Catálogo de Aplicativos e as funções de site do catálogo de aplicativos no mesmo site. Não é necessário instalá-las no mesmo servidor ou na mesma floresta do Active Directory. No entanto, o ponto de serviço Web do catálogo de aplicativos deve estar na mesma floresta que o banco de dados do site.

Para saber mais sobre o posicionamento de servidores, veja [Planejamento para servidores de sistema de sites e funções de sistema de sites](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).

> [!NOTE]  
> Instale o Catálogo de Aplicativos em um site primário. Você não consegue instalá-lo em um site secundário ou site de administração central.  

Instale o catálogo de aplicativos em um novo servidor do sistema de site ou um servidor existente no site. Para saber mais sobre o procedimento geral, veja [Instalar funções do sistema de site](/sccm/core/servers/deploy/configure/install-site-system-roles). No assistente para adicionar uma função de sistema de site ou criar um servidor de sistema de site, selecione as seguintes funções da lista:  
- **Ponto de serviços Web do catálogo de aplicativos**  
- **Ponto de site da Web do catálogo de aplicativos**  

> [!TIP]  
>  Se você deseja que computadores cliente usem o Catálogo de Aplicativos pela Internet, especifique o FQDN (nome de domínio totalmente qualificado) de Internet.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Verificar a instalação dessas funções de sistema de site  

- Mensagens de status: use os componentes **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Por exemplo, a ID do status **1015** para **SMS_PORTALWEB_CONTROL_MANAGER** confirma se o Gerenciador do Componente de Site instalou com êxito o ponto de sites da Web do Catálogo de Aplicativos.  

- Arquivos de log: pesquise por **SMSAWEBSVCSetup.log** e **SMSPORTALWEBSetup.log**.  

    Para obter mais informações, pesquise os arquivos de log **awebsvcMSI.log** e **portlwebMSI.log**.  


### <a name="step-4-configure-client-settings"></a>Etapa 4: Definir as configurações do cliente

Se você desejar que todos os usuários tenham a mesma configuração, defina as configurações padrão. Caso contrário, defina as configurações do cliente personalizadas para coleções específicas.

Para obter mais informações, consulte os seguintes artigos:
- [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings)  
    - Agente de Computador  
    - Reinicialização do computador  
    - Centro de software  
    - Implantação de software  
    - Afinidade de dispositivo e de usuário  
- [Como definir as configurações do cliente](/sccm/core/clients/deploy/configure-client-settings)  

O cliente do Configuration Manager definirá dispositivos com essas configurações quando baixar a política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [Como gerenciar clientes](/sccm/core/clients/manage/manage-clients).


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Etapa 5: Verifique se o Catálogo de Aplicativos está operacional

Use os procedimentos a seguir para verificar se o catálogo de aplicativos está operacional. 

> [!NOTE]  
>  A experiência de usuário do Catálogo de Aplicativos exige o Microsoft Silverlight. Se você usar o Catálogo de Aplicativos diretamente de um navegador, verifique primeiramente se o Microsoft Silverlight está instalado no computador.  

> [!TIP]  
>  Os pré-requisitos ausentes correspondem aos motivos mais comuns do mau funcionamento do Catálogo de Aplicativos após a instalação. Confirme se os pré-requisitos de função para as funções do sistema de site do Catálogo de Aplicativos. Para obter mais informações, consulte [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) (Pré-requisitos de site e sistema de sites).  

Em um navegador, digite o endereço do site do Catálogo de Aplicativos. Confirme se a página da Web exibe as três guias: **Catálogo de Aplicativos**, **Minhas Solicitações de Aplicativos** e **Meus Dispositivos**.  

Use o endereço apropriado para o Catálogo de Aplicativos na lista a seguir, em que &lt;servidor&gt; é o nome do computador, FQDN da intranet ou FQDN da Internet:  

- Conexões de cliente HTTPS e configurações padrão de função do sistema de sites: **https://&lt;servidor&gt;/CMApplicationCatalog**  

- Conexões de cliente HTTP e configurações padrão de função do sistema de sites: **http://&lt;servidor&gt;/CMApplicationCatalog**  

- Conexões de cliente HTTPS e configurações personalizadas de função do sistema de sites: **https://&lt;servidor&gt;:&lt;porta&gt;/&lt;nome do aplicativo Web&gt;**  

- Conexões de cliente HTTP e configurações personalizadas de função do sistema de sites: **http://&lt;servidor&gt;:&lt;porta&gt;/&lt;nome do aplicativo Web&gt;**  

> [!NOTE]  
>  Se você tiver entrado no dispositivo com uma conta de administrador de domínio, o cliente do Configuration Manager não exibirá mensagens de notificação. Por exemplo, mensagens indicando que novos softwares estão disponíveis.  

