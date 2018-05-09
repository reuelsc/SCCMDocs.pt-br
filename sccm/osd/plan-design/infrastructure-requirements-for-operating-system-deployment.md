---
title: Requisitos de infraestrutura para implantação de sistema operacional
titleSuffix: Configuration Manager
description: Conheça as dependências externas e do produto e os requisitos para implantação de sistema operacional
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6407344676230c12c66abb02c1394032e102e4b8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="infrastructure-requirements-for-os-deployment-in-system-center-configuration-manager"></a>Requisitos de infraestrutura para implantação de sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A implantação de sistema operacional no Configuration Manager tem dependências externas e dependências no produto. Use este artigo para ajudá-lo a preparar a infraestrutura para a implantação de sistema operacional.  



##  <a name="BKMK_ExternalDependencies"></a> Dependências externas ao Configuration Manager  
 Esta seção fornece informações sobre ferramentas externas, kits de instalação e versões de sistema operacional necessários para implantar sistemas operacionais no Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK para Windows 10  
 O Windows ADK (Kit de Avaliação e Implantação) é um conjunto de ferramentas e documentação que dá suporte à configuração e implantação do Windows. O Configuration Manager usa o Windows ADK para automatizar ações como instalação do Windows, captura de imagens e migração de dados e perfis de usuário.  

 Os seguintes recursos do Windows ADK devem ser instalados no servidor do site de nível superior da hierarquia, no servidor de cada site primário da hierarquia e no servidor do sistema de sites do Provedor de SMS:  

-   USMT (Ferramenta de Migração do Usuário) <sup>1</sup>  

-   Windows Deployment Tools  

-   Ambiente de Pré-Instalação do Windows (Windows PE)

Para obter uma lista das versões do Windows 10 ADK que podem ser usadas com diferentes versões do Configuration Manager, consulte [Suporte para o Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

 <sup>1</sup> A USMT não é obrigatória no servidor do sistema de sites do Provedor de SMS.  

> [!NOTE]  
>  É necessário instalar manualmente o Windows ADK em cada servidor do site antes de instalar o site do Configuration Manager.  

 Para obter mais informações, consulte:  

-   [Cenários do Windows ADK para Windows 10 para Profissionais de TI](/windows/deployment/windows-adk-scenarios-for-it-pros)  

-   [Baixar o Windows ADK para Windows 10](/windows-hardware/get-started/adk-install)  

-   [Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>USMT (Ferramenta de Migração do Usuário)  
 O Configuration Manager usa um pacote da USMT que inclui os arquivos de origem da USMT 10 para captura e restauração do estado do usuário como parte da implantação de sistema operacional. A instalação do Configuration Manager no site de nível superior cria automaticamente o pacote da USMT. A USMT 10 captura o estado do usuário do Windows 7, Windows 8, Windows 8.1 e Windows 10.  

 Para obter mais informações, consulte:  

-   [Cenários comuns de migração da USMT 10](/windows/deployment/usmt/usmt-common-migration-scenarios)  

-   [Gerenciar o estado do usuário](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 O Windows PE é usado em imagens de inicialização para iniciar um computador. É uma versão do Windows com serviços limitados usada durante a pré-instalação e implantação do Windows. A seguinte lista inclui as versões compatíveis do Windows ADK para o Configuration Manager, o branch atual:  

-   **Versão do Windows ADK**  

     Windows ADK para Windows 10. Para obter mais informações, consulte [Suporte para o Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

-   **Versões do Windows PE para imagens de inicialização personalizáveis no console do Configuration Manager**  

     Windows PE 10  

-   **Versões do Windows PE com suporte para imagens de inicialização não personalizáveis no console do Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> Só será possível adicionar uma imagem de inicialização ao Configuration Manager quando ela se basear no Windows PE 3.1. Instale o Suplemento do Windows AIK para Windows 7 SP1 a fim de atualizar o Windows AIK para Windows 7 (baseado no Windows PE 3) com o Suplemento do Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Você pode baixar o Suplemento do Windows AIK para Windows 7 SP1 do [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

     Por exemplo, quando você tiver o Configuration Manager, será possível personalizar as imagens de inicialização do Windows ADK para Windows 10 (baseado no Windows PE 10) no console do Configuration Manager. No entanto, embora haja suporte para imagens de inicialização baseadas no Windows PE 5, você deverá personalizá-las em outro computador e usar a versão do DISM instalada com o Windows ADK para Windows 8. Em seguida, é possível adicionar a imagem de inicialização ao console do Configuration Manager. Para obter mais informações sobre as etapas para personalizar uma imagem de inicialização (adicionar componentes e drivers opcionais), habilitar o suporte de comandos para a imagem de inicialização, adicionar a imagem de inicialização ao console do Configuration Manager e atualizar os pontos de distribuição com ela, consulte [Personalizar imagens de inicialização](../get-started/customize-boot-images.md). Para obter mais informações sobre imagens de inicialização, consulte [Gerenciar imagens de inicialização](../get-started/manage-boot-images.md).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
 O WSUS é obrigatório para o ponto de atualização de software, que é necessário para instalar atualizações de software durante a implantação de sistema operacional. Para obter mais informações, consulte [Instalar e configurar um ponto de atualização de software](/sccm/sum/get-started/install-a-software-update-point).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>IIS (Serviços de Informações da Internet) nos servidores do sistema de sites  
 O IIS é obrigatório no ponto de distribuição, no ponto de migração de estado e no ponto de gerenciamento. Para obter mais informações, consulte [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Pré-requisitos de site e sistema de sites).  


### <a name="windows-deployment-services-wds"></a>WDS (Serviços de Implantação do Windows)  
 O WDS é necessário para as implantações do PXE e ao usar o multicast para otimizar a largura de banda em implantações. Para obter mais informações, consulte [Serviços de Implantação do Windows](#BKMK_WDS) neste artigo.  


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Protocolo DHCP  
 O DHCP é necessário para as implantações do PXE. É necessário ter um servidor DHCP em funcionamento com um host ativo para implantar os sistemas operacionais usando o PXE. Para obter mais informações sobre implantações de PXE, veja [Usar PXE para implantar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Sistemas operacionais e configurações de disco rígido com suporte  
 Para obter mais informações sobre as versões do sistema operacional e as configurações de disco rígido compatíveis com o Configuration Manager ao implantar sistemas operacionais, consulte [Sistemas operacionais compatíveis](#BKMK_SupportedOS) e [Configurações de disco compatíveis](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Drivers de dispositivos Windows  
 Os drivers de dispositivo do Windows podem ser usados durante a instalação do sistema operacional no computador de destino. Eles também são usados durante a execução do Windows PE em uma imagem de inicialização. Para mais informações, consulte [Manage drivers (Gerenciar drivers)](../get-started/manage-drivers.md).  



##  <a name="BKMK_InternalDependencies"></a> Dependências do Configuration Manager  
 Esta seção fornece informações sobre os pré-requisitos de implantação de sistema operacional do Configuration Manager.  


### <a name="os-image"></a>Imagem do sistema operacional  
 As imagens do sistema operacional no Configuration Manager são armazenadas no formato de arquivo WIM (Windows Imaging). Elas representam uma coleção compactada de pastas e arquivos de referência. Essas imagens são necessárias para a instalação e configuração bem-sucedidas de um sistema operacional em um computador. Para obter mais informações, consulte [Gerenciar imagens do sistema operacional](../get-started/manage-operating-system-images.md).  


### <a name="driver-catalog"></a>Catálogo de drivers  
 Para implantar o driver de dispositivo, é necessário importá-lo, habilitá-lo e disponibilizá-lo em um ponto de distribuição que o cliente do Configuration Manager possa acessar. Para obter mais informações sobre o catálogo de drivers, consulte [Gerenciar drivers](../get-started/manage-drivers.md).  


### <a name="management-point"></a>Ponto de gerenciamento  
 Os pontos de gerenciamento transferem informações entre clientes e o site do Configuration Manager. O cliente usa um ponto de gerenciamento para executar a sequência de tarefas para concluir a implantação de sistema operacional. Para obter mais informações sobre sequências de tarefas, consulte [Considerações sobre o planejamento para automatizar tarefas](planning-considerations-for-automating-tasks.md).  


### <a name="distribution-point"></a>Ponto de distribuição  
 Os pontos de distribuição são usados na maioria das implantações para armazenar os dados usados para implantar um sistema operacional, como os pacotes de driver ou imagem. As sequências de tarefas normalmente recuperam os dados de um ponto de distribuição para implantar o sistema operacional. Para obter mais informações sobre como instalar pontos de distribuição e gerenciar conteúdo, consulte [Gerenciar conteúdo e infraestrutura de conteúdo](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="pxe-enabled-distribution-point"></a>Ponto de distribuição habilitado para PXE  
 Para realizar as implantações iniciadas por PXE, é necessário configurar um ponto de distribuição para aceitar as solicitações PXE de clientes. Para obter mais informações, consulte [Configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).


### <a name="multicast-enabled-distribution-point"></a>Ponto de distribuição habilitado para multicast  
 Para otimizar as implantações de sistema operacional usando o multicast, configure um ponto de distribuição para dar suporte ao multicast. Para obter mais informações, consulte [Configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).   


### <a name="state-migration-point"></a>Ponto de migração de estado  
 Ao capturar e restaurar os dados do estado do usuário para implantações lado a lado e de atualização, é necessário configurar um ponto de migração de estado para armazenar os dados de estado do usuário em outro computador.  

 Para obter mais informações sobre como configurar o ponto de migração de estado, consulte [Ponto de migração de estado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

 Para obter informações sobre como capturar e restaurar o estado do usuário, consulte [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  


### <a name="reporting-services-point"></a>Ponto do Reporting Services  
 Para usar os relatórios do Configuration Manager para implantações de sistema operacional, é necessário instalar e configurar um ponto do Reporting Services. Para obter mais informações, consulte [Relatórios](../../core/servers/manage/reporting.md).  


### <a name="security-permissions-for-os-deployments"></a>Permissões de segurança para implantações de sistema operacional  
 A função de segurança **Gerenciador de Implantação de Sistema Operacional** é uma função interna que não pode ser alterada. No entanto, é possível copiar a função, fazer alterações e salvar essas alterações como uma nova função de segurança personalizada. Estas são algumas das permissões que se aplicam diretamente às implantações de sistema operacional:  

-   **Pacote de Imagem de Inicialização**: Criar, Excluir, Modificar, Modificar Pasta, Mover Objeto, Ler, Definir Escopo de Segurança  

-   **Drivers do dispositivo**: Criar, Excluir, Modificar, Modificar Pasta, Modificar Relatório, Mover Objeto, Ler, Executar Relatório  

-   **Pacote de drivers**: Criar, Excluir, Modificar, Modificar Pasta, Mover Objeto, Ler, Definir Escopo de Segurança  

-   **Imagem do sistema operacional**: Criar, Excluir, Modificar, Modificar Pasta, Mover Objeto, Ler, Definir Escopo de Segurança  

-   **Pacote de instalação do sistema operacional**: Criar, Excluir, Modificar, Modificar Pasta, Mover Objeto, Ler, Definir Escopo de Segurança  

-   **Pacote de sequência de tarefas**: Criar, Criar Mídia de Sequência de Tarefas, Excluir, Modificar, Modificar Pasta, Modificar Relatório, Mover Objeto, Ler, Executar Relatório, Definir Escopo de Segurança  

 Para obter mais informações, consulte [Criar funções de segurança personalizadas](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>Escopos de segurança para implantações de sistema operacional  
 Use os escopos de segurança para fornecer aos usuários administrativos o acesso aos objetos protegíveis usados nas implantações de sistema operacional, como imagens do sistema operacional e de inicialização, pacotes de driver e pacotes de sequência de tarefas. Para obter mais informações, consulte [Escopos de segurança](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="BKMK_WDS"></a> Serviços de Implantação do Windows  
 O WDS (Serviços de Implantação do Windows) deve ser instalado no mesmo servidor que os pontos de distribuição configurados para dar suporte a PXE ou multicast. O WDS está incluído no sistema operacional do servidor. Para implantações do PXE, o WDS é o serviço que executa a inicialização do PXE. Quando o ponto de distribuição está instalado e habilitado para PXE, o Configuration Manager instala um provedor no WDS que usa as funções de inicialização do PXE do WDS.  

> [!NOTE]  
>  Se o servidor requerer reinicialização, a instalação do WDS poderá falhar. 


### <a name="wds-requirements"></a>Requisitos do WDS  

-   A instalação do WDS no servidor exige que o administrador seja membro do grupo local de Administradores.  

-   O servidor do WDS deve ser membro de um domínio Active Directory ou de um controlador de domínio para o domínio Active Directory. Todas as configurações de domínio e de floresta do Windows têm suporte para o WDS.  

-   Caso o provedor esteja instalado em um servidor remoto, você deve instalar o WDS no servidor do site e no provedor remoto.  


###  <a name="BKMK_WDSandDHCP"></a> Considerações sobre quando você tem o WDS e DHCP no mesmo servidor  
 Considere os seguintes problemas de configuração se você planeja co-hospedar o ponto de distribuição em um servidor executando DHCP.  

-   Você deve ter um servidor DHCP funcionando com um escopo ativo. O WDS usa o PXE, que exige um servidor DHCP.  

-   O DHCP e o WDS exigem o número da porta 67. Se você co-hospedar o WDS e o DHCP, poderá mover o DHCP ou o ponto de distribuição configurado para PXE para um servidor separado. Se preferir, use o procedimento a seguir para configurar o servidor do WDS para escutar em outra porta.  

    #### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>Para configurar o servidor do WDS para escutar em outra porta  

    1.  Modifique a seguinte chave do Registro:  

         `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

    2.  Defina o valor do Registro **UseDHCPPorts** como **0**.  

    3.  Para que a nova configuração entre em vigor, execute o seguinte comando no servidor:  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   Um servidor DNS é necessário para executar o WDS.  

-   As portas UDP a seguir devem ser abertas no servidor do WDS.  

    -   Porta 67 (DHCP)  

    -   Porta 69 (TFTP)  

    -   Porta 4011 (PXE)  

    > [!NOTE]  
    >  Se a autorização do DHCP for obrigatória no servidor, a porta 68 do cliente DHCP precisará estar aberta no servidor.  



##  <a name="BKMK_SupportedOS"></a> sistemas operacionais com suporte  
 Todos os sistemas operacionais Windows listados como clientes compatíveis em [Sistemas operacionais compatíveis para clientes e dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) são compatíveis com a implantação de sistema operacional.  



##  <a name="BKMK_SupportedDiskConfig"></a> Configurações de disco compatíveis  
 As combinações de configurações de disco rígido nos computadores de referência e destino compatíveis com a implantação de sistema operacional do Configuration Manager são mostradas na seguinte tabela:  

|Configuração de disco rígido do computador de referência|Configuração de disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco básico|  
|Volume simples em um disco dinâmico|Volume simples em um disco dinâmico|  

 O Configuration Manager permite a captura de uma imagem do sistema operacional somente em computadores configurados com volumes simples. Não há suporte para as seguintes configurações de disco rígido:  

-   Volumes estendidos  

-   Volumes distribuídos (RAID 0)  

-   Volumes espelhados (RAID 1)  

-   Volumes de paridade (RAID 5)  

 A tabela a seguir mostra uma configuração de disco rígido adicional nos computadores de referência e destino que não são compatíveis com a implantação de sistema operacional do Configuration Manager.  

|Configuração de disco rígido do computador de referência|Configuração de disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco dinâmico|  



## <a name="next-steps"></a>Próximas etapas
- [Preparar as funções do sistema de sites para implantações de sistema operacional](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments)
- [Preparar a implantação de sistema operacional](../get-started/prepare-for-operating-system-deployment.md)
