---
title: "Requisitos de infraestrutura para implantação do sistema operacional"
titleSuffix: Configuration Manager
description: "Verifique se você conhece as dependências externas e dependências de produto antes de usar o System Center 2012 Configuration Manager para a implantação de sistema operacional."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
caps.latest.revision: "24"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 0b90cb20707340bec6fc7d5ddbab6f39d78e10bf
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="infrastructure-requirements-for-operating-system-deployment-in-system-center-configuration-manager"></a>Requisitos de infraestrutura para implantação do sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A implantação de sistema operacional no System Center 2012 Configuration Manager tem dependências externas e dependências dentro do produto. Use as seções a seguir para ajudá-lo a preparar uma implantação do sistema operacional.  

##  <a name="BKMK_ExternalDependencies"></a> Dependências externas ao Configuration Manager  
 A seguir, há informações sobre ferramentas externas, kits de instalação e sistemas operacionais necessários para implantar sistemas operacionais no Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK para Windows 10  
 O Windows ADK é um conjunto de ferramentas e de documentação que oferece suporte à configuração e implantação dos sistemas operacionais Windows. O Configuration Manager usa o Windows ADK para automatizar as instalações do Windows, capturar imagens do Windows, migrar perfis e dados de usuários, entre outros.  

 Os recursos a seguir do Windows ADK devem ser instalados no servidor do site de nível superior da hierarquia, no servidor de cada site primário da hierarquia e no servidor de sistema do site do Provedor de SMS:  

-   USMT (Ferramenta de Migração do Usuário) <sup>1</sup>  

-   Windows Deployment Tools  

-   Ambiente de Pré-Instalação do Windows (Windows PE)

Para obter uma lista das versões do Windows 10 ADK que você pode usar com diferentes versões do Configuration Manager, consulte [Support For Windows 10 as a client (Suporte para o Windows 10 como cliente)](https://docs.microsoft.com/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

 <sup>1</sup> USMT não é obrigatória no servidor do sistema de site do Provedor de SMS.  

> [!NOTE]  
>  É necessário instalar manualmente o Windows ADK em cada computador que hospedará um site de administração central ou um servidor do site primário antes de instalar o site do Configuration Manager.  

 Para obter mais informações, consulte:  

-   [Cenários do Windows ADK para Windows 10 para Profissionais de TI](https://technet.microsoft.com/library/mt280162\(v=vs.85\).aspx)  

-   [Baixar o Windows ADK para Windows 10](https://msdn.microsoft.com/windows/hardware/dn913721.aspx#adkwin10)  

-   [Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>USMT (Ferramenta de Migração do Usuário)  
 O Configuration Manager usa um pacote de USMT que contém arquivos de origem da USMT 10 para capturar e restaurar o estado do usuário como parte da implantação do seu sistema operacional. A Instalação do Configuration Manager no site de nível superior cria automaticamente o pacote da USMT. A USMT 10 pode capturar o estado do usuário do Windows 7, Windows 8, Windows 8.1 e Windows 10. A USMT 10 é distribuída no Windows ADK (Kit de Avaliação e Implantação do Windows) para Windows 10.  

 Para obter mais informações, consulte:  

-   [Cenários comuns de migração da USMT 10](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)  

-   [Gerenciar o estado do usuário](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 O Windows PE é usado em imagens de inicialização para iniciar um computador. É um sistema operacional Windows com serviços limitados usado durante a pré-instalação e implantação dos sistemas operacionais Windows. Veja a seguir a versão do Configuration Manager e a versão com suporte do Windows ADK, a versão do Windows PE na qual se baseia a imagem de inicialização que pode ser personalizada no console do Configuration Manager e as versões do Windows PE nas quais se baseia a imagem de inicialização que pode ser personalizada com o DISM e, em seguida, adicione a imagem à versão especificada do Configuration Manager.  

#### <a name="configuration-manager-version-1511"></a>Configuration Manager versão 1511  
 Veja a seguir a versão com suporte do Windows ADK, a versão do Windows PE na qual se baseia a imagem de inicialização que pode ser personalizada no console do Configuration Manager e as versões do Windows PE nas quais se baseia a imagem de inicialização que pode ser personalizada usando o DISM e, em seguida, adicione a imagem ao Configuration Manager.  

-   **Versão do Windows ADK**  

     Windows ADK para Windows 10  

-   **Versões do Windows PE para imagens de inicialização personalizáveis no console do Configuration Manager**  

     Windows PE 10  

-   **Versões do Windows PE com suporte para imagens de inicialização não personalizáveis no console do Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> Só será possível adicionar uma imagem de inicialização ao Configuration Manager quando ela se basear no Windows PE 3.1. Instale o Suplemento do Windows AIK para Windows 7 SP1 a fim de atualizar o Windows AIK para Windows 7 (baseado no Windows PE 3) com o Suplemento do Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Você pode baixar o Suplemento do Windows AIK para Windows 7 SP1 do [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Por exemplo, quando você tiver o Configuration Manager, será possível personalizar as imagens de inicialização do Windows ADK para Windows 10 (baseado no Windows PE 10) no console do Configuration Manager. No entanto, embora haja suporte para imagens de inicialização baseadas no Windows PE 5, você deverá personalizá-las em outro computador e usar a versão do DISM instalada com o Windows ADK para Windows 8. Em seguida, é possível adicionar a imagem de inicialização ao console do Configuration Manager. Para obter mais informações sobre as etapas para personalizar uma imagem de inicialização (adicionar componentes e drivers opcionais), habilitar o suporte de comandos para a imagem de inicialização, adicionar a imagem de inicialização ao console do Configuration Manager e atualizar os pontos de distribuição com ela, consulte [Personalizar imagens de inicialização](../get-started/customize-boot-images.md). Para obter mais informações sobre imagens de inicialização, consulte [Gerenciar imagens de inicialização](../get-started/manage-boot-images.md).  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
Você precisa instalar os seguintes hotfixes do WSUS 4.0:
  - [Hotfix 3095113](https://support.microsoft.com/kb/3095113) é necessário para a manutenção do Windows 10, que utiliza a infraestrutura de atualizações de software para obter as atualizações de recursos do Windows 10. Quando você tem o WSUS 3.2, deve usar sequências de tarefas para atualizar o Windows 10. Para obter mais informações, consulte [Gerenciar o Windows como um serviço](../deploy-use/manage-windows-as-a-service.md).  
  - O [Hotfix 3159706](https://support.microsoft.com/kb/3159706) é necessário para usar o serviço do Windows 10 para atualizar os computadores para a Atualização de Aniversário do Windows 10, bem como para versões posteriores. Há etapas manuais descritas no artigo de suporte que você precisa seguir para instalar esse hotfix. Para obter mais informações, consulte [Gerenciar o Windows como um serviço](../deploy-use/manage-windows-as-a-service.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>IIS (Serviços de Informações da Internet) nos servidores do sistema de sites  
 O IIS é necessário no ponto de distribuição, ponto de migração de estado e ponto de gerenciamento. Para obter mais informações sobre esse requisito, consulte [Pré-requisitos do site e do sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-deployment-services-wds"></a>WDS (Serviços de Implantação do Windows)  
 O WDS é necessário para as implantações do PXE, ao usar o multicast para otimizar a largura de banda em implantações e para a instalação offline de imagens. Caso o provedor esteja instalado em um servidor remoto, você deve instalar o WDS no servidor do site e no provedor remoto. Para obter mais informações, consulte [Serviços de implantação do Windows](#BKMK_WDS) , neste tópico.  

### <a name="dynamic-host-configuration-protocol-dhcp"></a>Protocolo DHCP  
 O DHCP é necessário para as implantações do PXE. É necessário ter um servidor DHCP em funcionamento com um host ativo para implantar os sistemas operacionais usando o PXE. Para obter mais informações sobre implantações de PXE, veja [Usar PXE para implantar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Sistemas operacionais e configurações de disco rígido com suporte  
 Para obter mais informações sobre versões do sistema operacional e configurações de disco rígido com suporte do Configuration Manager ao implantar sistemas operacionais, consulte [Sistemas operacionais com suporte](#BKMK_SupportedOS) e [Configurações de disco com suporte](#BKMK_SupportedDiskConfig).  

### <a name="windows-device-drivers"></a>Drivers de dispositivos Windows  
 Os drivers de dispositivos Windows podem ser usados ao instalar o sistema operacional no computador de destino e ao executar o Windows PE usando uma imagem de inicialização. Para obter mais informações sobre drivers de dispositivo, consulte [Gerenciar drivers](../get-started/manage-drivers.md).  

##  <a name="BKMK_InternalDependencies"></a> Dependências do Configuration Manager  
 A seguir, há informações sobre os pré-requisitos de implantação de sistema operacional do Configuration Manager.  

### <a name="operating-system-image"></a>Imagem do sistema operacional  
 As imagens do sistema operacional no Configuration Manager são armazenadas em arquivos de formato WIM (Windows Imaging) e representam uma coleção compactada de arquivos e pastas de referência necessários para instalar e configurar com êxito um sistema operacional em um computador. Para obter mais informações, consulte [Gerenciar imagens do sistema operacional](../get-started/manage-operating-system-images.md).  

### <a name="driver-catalog"></a>Catálogo de drivers  
 Para implantar o driver de dispositivo, é necessário importá-lo, habilitá-lo e disponibilizá-lo em um ponto de distribuição que o cliente do Configuration Manager possa acessar. Para obter mais informações sobre o catálogo de drivers, consulte [Gerenciar drivers](../get-started/manage-drivers.md).  

### <a name="management-point"></a>Ponto de gerenciamento  
 Os pontos de gerenciamento transferem informações entre os computadores cliente e o site do Configuration Manager. O cliente usa o ponto de gerenciamento para executar toda sequência de tarefas necessárias para a conclusão da implantação do sistema operacional.  

 Para obter mais informações sobre sequências de tarefas, consulte [Considerações sobre o planejamento para automatizar tarefas](planning-considerations-for-automating-tasks.md).  

### <a name="distribution-point"></a>Ponto de distribuição  
 Os pontos de distribuição são usados na maioria das implantações para armazenar os dados usados para implantar um sistema operacional, como a imagem do sistema operacional e os pacotes de drivers de dispositivos. As sequências de tarefas normalmente recuperam dados de um ponto de distribuição para implantar o sistema operacional.  

 Para obter mais informações sobre como instalar pontos de distribuição e gerenciar conteúdo, consulte [Gerenciar conteúdo e infraestrutura de conteúdo](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="pxe-enabled-distribution-point"></a>Ponto de distribuição habilitado para PXE  
 Para realizar as implantações iniciadas por PXE, é necessário configurar um ponto de distribuição para aceitar as solicitações PXE de clientes. Para obter mais informações sobre como configurar o ponto de distribuição, consulte [Configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).  

### <a name="multicast-enabled-distribution-point"></a>Ponto de distribuição habilitado para multicast  
 Para otimizar as imagens do sistema operacional usando multicast, configure um ponto de distribuição que ofereça suporte a multicast. Para obter mais informações sobre como configurar o ponto de distribuição, consulte [Configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).   

### <a name="state-migration-point"></a>Ponto de migração de estado  
 Ao capturar e restaurar os dados do estado do usuário para implantações lado a lado e de atualização, é necessário configurar um ponto de migração de estado para armazenar os dados de estado do usuário em outro computador.  

 Para obter mais informações sobre como configurar o ponto de migração de estado, consulte [Ponto de migração de estado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

 Para obter informações sobre como capturar e restaurar o estado do usuário, consulte [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

### <a name="service-connection-point"></a>Ponto de Conexão de Serviço  
 Ao usar o WaaS (Windows como um Serviço) para implantar a ramificação atual do Windows 10, o ponto de conexão do serviço deve estar instalado. Para obter mais informações, consulte [Gerenciar o Windows como um serviço](../deploy-use/manage-windows-as-a-service.md).  

### <a name="reporting-services-point"></a>Ponto do Reporting Services  
 Para usar os relatórios do Configuration Manager para implantações de sistema operacional, é necessário instalar e configurar um ponto do Reporting Services. Para obter mais informações, consulte [Relatórios](../../core/servers/manage/reporting.md).  

### <a name="security-permissions-for-operating-system-deployments"></a>Permissões de segurança para implantações de sistema operacional  
 A função de segurança do **Gerenciador de Implantação de Sistema Operacional** é uma função interna que não pode ser alterada. No entanto, é possível copiar a função, fazer alterações e salvar essas alterações como uma nova função de segurança personalizada. Aqui estão algumas das permissões que se aplicam diretamente às implantações de sistema operacional:  

-   **Pacote de Imagem de Inicialização**: Criar, Excluir, Modificar, Modificar Pasta, Mover Objeto, Ler, Definir Escopo de Segurança  

-   **Drivers do dispositivo**: Criar, Excluir, Modificar, Modificar Pasta, Modificar Relatório, Mover Objeto, Ler, Executar Relatório  

-   **Pacote de drivers**: Criar, Excluir, Modificar, Modificar Pasta, Mover Objeto, Ler, Definir Escopo de Segurança  

-   **Imagem do sistema operacional**: Criar, Excluir, Modificar, Modificar Pasta, Mover Objeto, Ler, Definir Escopo de Segurança  

-   **Pacote de instalação do sistema operacional**: Criar, Excluir, Modificar, Modificar Pasta, Mover Objeto, Ler, Definir Escopo de Segurança  

-   **Pacote de sequência de tarefas**: Criar, Criar Mídia de Sequência de Tarefas, Excluir, Modificar, Modificar Pasta, Modificar Relatório, Mover Objeto, Ler, Executar Relatório, Definir Escopo de Segurança  

 Para obter mais informações sobre funções de segurança personalizadas, consulte [Criar funções de segurança personalizadas](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  

### <a name="security-scopes-for-operating-system-deployments"></a>Escopos de segurança para implantações de sistema operacional  
 Use os escopos de segurança para fornecer aos usuários administrativos o acesso a objetos protegíveis usados nas implantações de sistema operacional, como imagens de sistema operacional e de inicialização, pacotes de drivers e pacotes de sequência de tarefas. Para obter mais informações, consulte [Escopos de segurança](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  

##  <a name="BKMK_WDS"></a> Serviços de Implantação do Windows  
 O WDS (Serviços de Implantação do Windows) deve ser instalado no mesmo servidor que os pontos de distribuição configurados para dar suporte a PXE ou multicast. O WDS está incluído no sistema operacional do servidor. Para implantações do PXE, o WDS é o serviço que executa a inicialização do PXE. Quando o ponto de distribuição está instalado e habilitado para PXE, o Configuration Manager instala um provedor no WDS que usa as funções de inicialização do PXE do WDS.  

> [!NOTE]  
>  Se o servidor requerer reinicialização, a instalação do WDS poderá falhar. 

 Outras configurações do WDS que devem ser consideradas incluem o seguinte:  

-   A instalação do WDS no servidor exige que o administrador seja membro do grupo local de administradores.  

-   O servidor do WDS deve ser membro de um domínio Active Directory ou de um controlador de domínio para o domínio Active Directory. Todas as configurações de domínio e de floresta do Windows têm suporte para o WDS.  

-   Caso o provedor esteja instalado em um servidor remoto, você deve instalar o WDS no servidor do site e no provedor remoto.  

###  <a name="BKMK_WDSandDHCP"></a> Considerações sobre quando você tem o WDS e DHCP no mesmo servidor  
 Considere os seguintes problemas de configuração se você planeja co-hospedar o ponto de distribuição em um servidor executando DHCP.  

-   Você deve ter um servidor DHCP funcionando com um escopo ativo. Os Serviços de Implantação do Windows utilizam PXE, o que requer um servidor DHCP.  

-   O DHCP e os Serviços de Implantação do Windows exigem o número da porta 67. Se você co-hospedar os Serviços de Implantação do Windows e o DHCP, será possível mover o DHCP ou o ponto de distribuição que está configurado para PXE para um servidor separado. Ou, você pode usar o procedimento a seguir para configurar o servidor dos Serviços de Implantação do Windows para escutar em uma porta diferente.  

    #### <a name="to-configure-the-windows-deployment-services-server-to-listen-on-a-different-port"></a>Para configurar o servidor dos Serviços de Implantação do Windows para escutar em uma porta diferente  

    1.  Modifique a seguinte chave do Registro:  

         **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE**  

    2.  Defina o valor do Registro como: **UseDHCPPorts = 0**  

    3.  Para que a nova configuração entre em vigor, execute o seguinte comando no servidor:  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   Um servidor DNS é necessário para executar os Serviços de Implantação do Windows.  

-   As seguintes portas UDP devem ser abertas no servidor dos Serviços de Implantação do Windows.  

    -   Porta 67 (DHCP)  

    -   Porta 69 (TFTP)  

    -   Porta 4011 (PXE)  

    > [!NOTE]  
    >  Além disso, se a autorização de DHCP for necessária no servidor, a porta 68 do cliente DHCP precisará estar aberta no servidor.  

##  <a name="BKMK_SupportedOS"></a> Sistemas operacionais com suporte  
 Todos os sistemas operacionais Windows listados como sistemas operacionais cliente com suporte em [Sistemas operacionais com suporte para clientes e dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) têm suporte para implantações de sistema operacional.  

##  <a name="BKMK_SupportedDiskConfig"></a> Configurações de disco compatíveis  
 As combinações de configurações de disco rígido nos computadores de referência e destino que têm suporte para a implantação de sistema operacional do Configuration Manager são mostradas na tabela a seguir.  

|Configuração de disco rígido do computador de referência|Configuração de disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco básico|  
|Volume simples em um disco dinâmico|Volume simples em um disco dinâmico|  

 O Configuration Manager dá suporte à captura de uma imagem de sistema operacional somente de computadores configurados com volumes simples. Não há suporte para as seguintes configurações de disco rígido:  

-   Volumes estendidos  

-   Volumes distribuídos (RAID 0)  

-   Volumes espelhados (RAID 1)  

-   Volumes de paridade (RAID 5)  

 A tabela a seguir mostra uma configuração de disco rígido adicional em computadores de referência e de destino que não tem suporte com a implantação de sistema operacional do Configuration Manager.  

|Configuração de disco rígido do computador de referência|Configuração de disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco dinâmico|  

## <a name="next-steps"></a>Próximas etapas
[Preparar para implantação de sistema operacional](../get-started/prepare-for-operating-system-deployment.md)
