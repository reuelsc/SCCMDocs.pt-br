---
title: Planejar funções do sistema de sites
titleSuffix: Configuration Manager"
description: Considere os servidores e as funções do sistema de sites ao planejar sua hierarquia do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c6ae8b6fb99016bfc0a39c328cb0d52269897917
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128027"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Planejar servidores de sistema de sites e funções do sistema de sites no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Cada site do Configuration Manager que você instala inclui um servidor do site que é um **servidor do sistema de sites**. O site também pode incluir servidores adicionais do sistema de sites em computadores que são remotos do servidor do site. Servidores de sistemas de sites (o servidor do site ou um servidor do sistema de sites remoto) dão suporte a **funções de sistema de sites**.  


##  <a name="bkmk_siteservers"></a> Servidores de sistema de sites  

Quando você instala uma função do sistema de sites em um computador, esse computador torna-se um servidor do sistema de sites. Em cada site, você instala um ou mais servidores adicionais do sistema de sites. Você não precisa instalar mais servidores do sistema de sites e pode optar por executar todas as funções do sistema de sites diretamente no computador servidor do site. Cada servidor de sistema de site dá suporte a uma ou mais funções de sistema de site. Servidores adicionais podem expandir as funcionalidades e a capacidade de um site compartilhando a carga de processamento que as funções do sistema de sites colocam em um servidor.  

Ao considerar a adição de um servidor de sistema de site, verifique se o servidor atende aos pré-requisitos para o uso pretendido. Adicione-o também em um local de rede com largura de banda suficiente para comunicar-se com os pontos de extremidade esperados. Esses pontos de extremidade incluem o servidor do site, recursos de domínio, um local baseado em nuvem, servidores do sistema de sites e clientes.  



##  <a name="bkmk_planroles"></a> Site system roles  

Instale funções do sistema de sites em um servidor para fornecer recursos adicionais ao site. Os exemplos incluem:  

-   Pontos de gerenciamento adicionais para que o site possa dar suporte a mais dispositivos, até chegar à capacidade com suporte pelos sites.  

-   Pontos de distribuição adicionais para expandir a infraestrutura de conteúdo, melhorando o desempenho das distribuições de conteúdo a usuários e dispositivos.  

-   Uma ou mais funções do sistema de site de recursos específicos. Por exemplo, um ponto de atualização de software permite gerenciar as atualizações de software de dispositivos gerenciados. Um ponto do Reporting Services permite executar relatórios para monitorar, entender e compartilhar informações sobre seu ambiente.  


Diferentes sites do Configuration Manager podem dar suporte a conjuntos diferentes de funções do sistema de sites. O conjunto de funções do sistema de sites com suporte depende do tipo do site. (Os tipos de sites incluem um site de administração central, sites primários ou sites secundários.) A topologia da sua hierarquia pode limitar o posicionamento de algumas funções em determinados tipos de site. Por exemplo, o ponto de conexão de serviço só tem suporte no site de nível superior da hierarquia. O site de nível superior pode ser um site de administração central ou um site primário autônomo. Não há suporte para essa função em um site primário filho ou em sites secundários.  

Depois de instalar um site, você pode mover o local de algumas funções de sistema de site do local padrão no servidor de site para outro servidor. Por exemplo, as funções de ponto de gerenciamento ou de ponto de distribuição são instaladas por padrão em um servidor de site primário ou secundário. Instale também instâncias adicionais de algumas funções do sistema de sites para expandir as funcionalidades do site e para atender às suas necessidades de negócios. Algumas funções são obrigatórias, enquanto outras são opcionais.  

#### <a name="configuration-manager-site-server"></a>Servidor do site do Configuration Manager
Essa função identifica o servidor em que a instalação do Configuration Manager é executada para instalar um site ou o servidor no qual você instala um site secundário. Você só poderá mover ou desinstalar essa função depois que o site for desinstalado.  

#### <a name="configuration-manager-site-system"></a>Sistemas de site do Configuration Manager
Essa função é atribuída a qualquer computador em que você instala um site ou uma função do sistema de sites. Você só poderá mover ou desinstalar essa função depois de remover a última função do sistema de sites do computador.  

#### <a name="configuration-manager-component-site-system-role"></a>Função do sistema de sites do componente do Configuration Manager
Essa função identifica um sistema de sites que executa uma instância do serviço **SMS Executive**. Ele é necessário para dar suporte a outras funções, como pontos de gerenciamento. Você só poderá mover ou desinstalar essa função depois de remover a última função do sistema de sites aplicável do computador.  

#### <a name="configuration-manager-site-database-server"></a>Servidor de banco de dados do site do Configuration Manager
O site atribui essa função para servidores do sistema de sites que mantêm uma instância do banco de dados do site. Apenas mova essa função para um novo servidor executando a instalação para modificar o site para usar uma instância diferente do SQL Server para hospedar o banco de dados do site.  

#### <a name="sms-provider"></a>Provedor de SMS
O site atribui essa função para cada computador que hospeda uma instância do provedor de SMS. O provedor é a interface entre um console do Configuration Manager e o banco de dados do site. Por padrão, essa função é instalada automaticamente no servidor do site de um site de administração central e de sites primários. Instale instâncias adicionais em cada site para fornecer acesso a mais usuários administrativos ou para redundância.  

Para instalar provedores adicionais, execute a instalação do Configuration Manager para [Gerenciar o provedor de SMS](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider). Em seguida, instale provedores adicionais em computadores adicionais. Instale apenas uma instância do provedor de SMS em um computador. Esse computador precisa estar no mesmo domínio que o servidor do site.  

#### <a name="application-catalog-web-service-point"></a>Ponto de serviços Web do Catálogo de Aplicativos
Uma função do sistema de sites que fornece informações sobre software para o site do Catálogo de Aplicativos da biblioteca de software. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

#### <a name="application-catalog-website-point"></a>Ponto de sites da Web do Catálogo de Aplicativos
Uma função do sistema de site que fornece aos usuários uma lista de softwares disponíveis no Catálogo de Aplicativos. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

Quando o Catálogo de Aplicativos dá suporte a computadores cliente na Internet, para melhorar segurança, instale os pontos de sites da Web do catálogo de aplicativos em uma rede de perímetro. Em seguida, instale o ponto de serviços Web do catálogo de aplicativos na intranet.  

#### <a name="asset-intelligence-synchronization-point"></a>Ponto de sincronização do Asset Intelligence
Uma função de sistema de site que se conecta à Microsoft para baixar informações de catálogo do Asset Intelligence. Essa função também carrega títulos não categorizados, para que a Microsoft possa considerá-los para inclusão futura no catálogo. Uma hierarquia dá suporte a apenas uma única instância dessa função no site de nível superior da sua hierarquia. Se você expandir um site primário autônomo em uma hierarquia maior, desinstale essa função do site primário. Em seguida, instale-a no site de administração central. 

Para obter mais informações, confira [Asset Intelligence no Configuration Manager](/sccm/core/clients/manage/asset-intelligence/introduction-to-asset-intelligence).  

#### <a name="certificate-registration-point"></a>Ponto de registro de certificado
Uma função do sistema de sites que se comunica com um servidor que executa o NDES (Serviço de Registro de Dispositivo de Rede). Essa função gerencia solicitações de certificado de dispositivo que usam SCEP (Simple Certificate Enrollment Protocol). Essa função tem suporte apenas em sites primários e no site de administração central.

Embora um ponto de registro de certificado único possa fornecer funcionalidade a uma hierarquia inteira, para ajudar no balanceamento de carga das solicitações de certificado, convém instalar várias instâncias dessa função em um site e em vários sites na mesma hierarquia. Esse design ajuda com o balanceamento de carga. Quando houver várias instâncias em uma hierarquia, os clientes serão atribuídos aleatoriamente a um dos pontos de registro de certificado.  

Cada ponto de registro de certificado requer acesso a uma instância separada do NDES. Você não pode configurar dois ou mais pontos de registro de certificado para usar a mesma instância do NDES. Além disso, não instale o ponto de registro de certificado no mesmo servidor que executa o NDES.  

#### <a name="cloud-management-gateway-connection-point"></a>Ponto de conexão do gateway de gerenciamento de nuvem
Uma função de sistema de site para se comunicar com o [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

#### <a name="data-warehouse-service-point"></a>Ponto de serviço de data warehouse
Use o ponto de serviço de data warehouse para armazenar e relatar dados históricos de longo prazo em seu ambiente do Configuration Manager. Para obter mais informações, confira [Data warehouse](/sccm/core/servers/manage/data-warehouse).  

#### <a name="distribution-point"></a>Ponto de distribuição
Uma função do sistema de sites que contém os arquivos de origem para os clientes baixarem, por exemplo: 
- Conteúdo de aplicativo
- Pacotes de software
- Atualizações de software
- Imagens do sistema operacional
- Imagens de inicialização  

Por padrão, essa função é instalada no servidor do site quando você instala um novo site primário ou secundário. Essa função não é permitida em um site de administração central. Instale várias instâncias dessa função em um site com suporte e em vários sites na mesma hierarquia. Para obter mais informações, confira [Conceitos básicos do gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management), e [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure) (Gerenciar conteúdo e infraestrutura de conteúdo).  

#### <a name="endpoint-protection-point"></a>Ponto do Endpoint Protection
Função do sistema de site que o Configuration Manager usa para aceitar os termos de licença do Endpoint Protection e configurar a associação padrão para o Cloud Protection Service. Uma hierarquia dá suporte apenas a uma única instância dessa função, que precisa estar no site de nível superior. Se você expandir um site primário autônomo em uma hierarquia maior, desinstale essa função do site primário e, em seguida, instale-o no site de administração central. Para obter mais informações, confira [Endpoint Protection no Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).  

#### <a name="enrollment-point"></a>Ponto de registro
Uma função do sistema de sites que usa certificados PKI para que o Configuration Manager registre computadores macOS e dispositivos móveis. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

Se um usuário registrar dispositivos móveis usando o Configuration Manager e sua conta do Active Directory estiver em uma floresta não confiável para o servidor de site, instale um ponto de registro na floresta do usuário. Assim, o Configuration Manager poderá autenticar o usuário.  

#### <a name="enrollment-proxy-point"></a>Ponto proxy do registro
Um função do sistema de sites que gerencia as solicitações de registro do Configuration Manager realizadas por dispositivos móveis e computadores macOS. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

Para dar suporte a dispositivos móveis na Internet, instale um ponto proxy do registro em uma rede de perímetro e outro na intranet.   

#### <a name="exchange-server-connector"></a>Conector do Exchange Server
Para obter informações sobre essa função, confira [Gerenciar dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  

#### <a name="fallback-status-point"></a>Ponto de status de fallback
Uma função do sistema de sites que ajuda você a monitorar a instalação do cliente. Ele identifica os clientes que não são gerenciados porque eles não podem se comunicar com seu ponto de gerenciamento. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site e em vários sites na mesma hierarquia.     

#### <a name="management-point"></a>Ponto de gerenciamento
Uma função do sistema de sites que fornece informações de localização de serviço e de política aos clientes. Ela também recebe dados de configuração dos clientes.  

Por padrão, essa função é instalada no servidor do site quando você instala um novo site primário ou secundário. Sites primários dão suporte a várias instâncias dessa função. Os sites secundários permitem um único ponto de gerenciamento. Também conhecida como ponto de gerenciamento de proxy, essa função em um site secundário fornece um ponto de contato local para que os clientes obtenham as políticas do usuário e do computador.  

Configure os pontos de gerenciamento para dar suporte a HTTP ou HTTPS. Eles também podem dar suporte a dispositivos móveis gerenciados com o MDM (gerenciamento de dispositivo móvel) local do Configuration Manager. Para ajudar a reduzir a carga de processamento colocada no servidor de banco de dados do site pelos pontos de gerenciamento conforme eles atendem às solicitações dos clientes, use [Réplicas de banco de dados para pontos de gerenciamento](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  

#### <a name="reporting-services-point"></a>Ponto do Reporting Services
Uma função do sistema de site que se integra ao SQL Server Reporting Services para criar e gerenciar relatórios do Configuration Manager. Essa função tem suporte em sites primários e no site de administração central, e você pode instalar várias instâncias dela em um site compatível. Para obter mais informações, consulte [Planejando relatórios](/sccm/core/servers/manage/planning-for-reporting).  

#### <a name="service-connection-point"></a>Ponto de Conexão de Serviço
Uma função do sistema de sites que carrega dados de uso do seu site e é necessária para fazer as atualizações do Configuration Manager disponíveis no console. Essa função também ajuda a gerenciar dispositivos móveis com o Microsoft Intune e o MDM local. Uma hierarquia dá suporte apenas a uma única instância dessa função, que precisa estar no site de nível superior da hierarquia. Se você expandir um site primário autônomo em uma hierarquia maior, desinstale essa função do site primário e, em seguida, instale-o no site de administração central. Para obter mais informações, consulte [Sobre o ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point).  

#### <a name="software-update-point"></a>Ponto de atualização de software
Uma função do sistema de site que se integra ao WSUS (Windows Server Update Services) para fornecer atualizações de software a clientes do Configuration Manager. Essa função tem suporte em todos os sites:  

-   Instale esse sistema de sites no site de administração central para sincronização com o WSUS.  

-   Configure cada instância da função em sites primários filho para sincronizar com o site de administração central.  

-   Quando a transferência de dados pela rede estiver lenta, considere a instalação de um ponto de atualização de software em sites secundários.  

Para obter mais informações, confira [Planejar atualizações de software](/sccm/sum/plan-design/plan-for-software-updates).  

#### <a name="state-migration-point"></a>Ponto de migração de estado
Quando você migra um computador para um novo sistema operacional, essa função do sistema de sites armazena dados de estado do usuário. Essa função tem suporte em sites primários e secundários. Instale várias instâncias dessa função em um site e em vários sites na mesma hierarquia. Para obter mais informações de como armazenar o estado do usuário ao implantar um sistema operacional, confira [Gerenciar o estado do usuário](/sccm/osd/get-started/manage-user-state).  



## <a name="next-steps"></a>Próximas etapas

Algumas funções do sistema de sites do Configuration Manager requerem conexão com a Internet. Se seu ambiente exigir tráfego da Internet para usar um servidor proxy, configure as funções desse sistema de sites para usar o proxy. Para obter mais informações, confira [Suporte ao servidor proxy](/sccm/core/plan-design/network/proxy-server-support).  
