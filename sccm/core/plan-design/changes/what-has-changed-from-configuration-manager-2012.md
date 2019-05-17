---
title: Alterações do Configuration Manager 2012
description: Identifique as mudanças e os novos recursos do System Center Configuration Manager com relação ao System Center 2012 Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb6071e576a12773c0aa5627dad80700db843f43
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496114"
---
# <a name="whats-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>O que mudou no System Center Configuration Manager do System Center 2012 Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O branch atual do Configuration Manager introduz alterações importantes com relação ao System Center 2012 Configuration Manager. Este artigo identifica alterações significativas e os novos recursos encontrados na versão de linha de base 1511 do System Center Configuration Manager. Para saber mais sobre as alterações introduzidas em atualizações posteriores do System Center Configuration Manager, consulte [Novidades nas versões incrementais do System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).

A versão de dezembro de 2015 do System Center Configuration Manager (versão 1511) é a versão inicial do produto atual do Configuration Manager da Microsoft. Normalmente, ela é chamada de branch atual do System Center Configuration Manager. O *branch atual* indica que esta versão oferece suporte a atualizações incrementais do produto. Também fornece uma maneira de distinguir entre esta versão e as versões anteriores do Configuration Manager.  

System Center Configuration Manager:  

- não usa um identificador de ano ou de produto no nome do produto, ao contrário das versões anteriores, como o Configuration Manager 2007 ou o System Center 2012 Configuration Manager.  

- Dá suporte a atualizações incrementais no produto, também chamadas de versões de atualização. A versão de inicial era a 1511. As seguintes versões são lançadas várias vezes no ano como atualizações de console, como a versão 1810.  

- É instalado usando uma versão de linha de base. Embora a 1511 fosse a versão de linha de base original, novas versões de linha de base também são lançadas periodicamente, como a versão 1902. As versões de linha de base podem ser usadas para instalar um novo site do System Center Configuration Manager e para atualizar de uma versão com suporte do Configuration Manager 2012.  



##  <a name="bkmk_updates"></a> Atualizações no console para o Configuration Manager  

O System Center Configuration Manager usa um método de serviço no console chamado **Atualizações e Manutenção** que facilita a localização e instalação das atualizações recomendadas.  

Algumas versões estão disponíveis apenas como atualizações para sites existentes (dentro do console do Configuration Manager) e não podem ser usadas para instalar novos sites do Configuration Manager. Por exemplo, a atualização 1810 está disponível apenas no console do Configuration Manager. Ela atualiza um site que já executa uma versão do System Center Configuration Manager.

Periodicamente, uma versão de atualização também é lançada como uma nova versão de linha de base (como a atualização 1902). Esse tipo de atualização pode ser usada para instalar uma nova hierarquia sem a necessidade de iniciar com uma versão de linha de base mais antiga (como 1802) e atualizá-la para a versão mais atual.


Para saber mais sobre o uso de atualizações, consulte [Atualizações para o Configuration Manager](/sccm/core/servers/manage/updates).  
Para saber mais sobre linhas de base, consulte [Versões de linha de base e de atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).



##  <a name="bkmk_servicepoint"></a> Nova função do sistema de sites: ponto de conexão de serviço  

O **conector do Microsoft Intune** é substituído por uma nova função de sistema de sites que habilita uma funcionalidade adicional, o **ponto de conexão de serviço**. O ponto de conexão de serviço:  

- Substitui o conector do Microsoft Intune ao integrar o Intune ao gerenciamento de dispositivo móvel local do System Center Configuration Manager.  

- É usado como um ponto de contato para os dispositivos gerenciados.  

- Carrega dados de uso sobre a implantação para o serviço de nuvem da Microsoft.  

- Disponibiliza atualizações que se aplicam à sua implantação no console do Configuration Manager.  

Essa função do sistema de sites dá suporte aos modos de operação online e offline. Para obter mais informações, consulte [Sobre o ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point).  



##  <a name="bkmk_usage"></a> Coleta de dados de uso  

O Configuration Manager coleta dados de uso sobre seus sites e sua infraestrutura. Essas informações são compiladas e enviadas ao serviço de nuvem da Microsoft pelo ponto de conexão de serviço. Elas são necessárias para permitir que o Configuration Manager baixe atualizações específicas à sua implantação do Configuration Manager. Ao configurar o ponto de conexão de serviço, é possível especificar o nível de dados coletados e se eles são enviados de forma automática (modo online) ou manual (modo offline).  

Para obter mais informações, consulte [Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  



##  <a name="bkmk_AMT"></a> Suporte para Intel AMT (Active Management Technology)  

O branch atual do Configuration Manager remove o suporte nativo para computadores baseados em AMT de dentro do console do Configuration Manager. Os computadores baseados em AMT permanecem totalmente gerenciados quando você usa o [Complemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O uso do complemento fornece acesso aos recursos mais recentes para gerenciar o AMT e, ao mesmo tempo, remove as limitações introduzidas até que o Configuration Manager possa incorporar essas mudanças.  

A remoção do AMT integrado para o Configuration Manager inclui o gerenciamento fora de banda. A função do sistema de sites do ponto de gerenciamento fora de banda não está mais disponível.  

> [!Note]   
> O gerenciamento fora de banda no System Center 2012 Configuration Manager não é afetado por essa alteração.  



##  <a name="bkmk_out"></a> Funcionalidade preterida  

Alguns recursos, como o [Suporte nativo para computadores baseados em Intel AMT (Active Management Technology)](#bkmk_AMT), foram removidos do console do Configuration Manager. Outros, como a Proteção de Acesso à Rede, foram totalmente removidos. Além disso, não há mais suporte para alguns produtos mais antigos da Microsoft como o Windows Vista, Windows Server 2008 e SQL Server 2008.  

Para ver uma lista dos recursos preteridos, consulte [Itens removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).  

Para saber mais sobre os produtos, sistemas operacionais e configurações compatíveis, consulte [Configurações com suporte](/sccm/core/plan-design/configs/supported-configurations).  



## <a name="client-deployment"></a>Implantação do cliente  

O Configuration Manager introduz um novo recurso para testar novas versões do cliente do Configuration Manager antes de atualizar o restante do site com o novo software. É possível configurar uma coleção de pré-produção na qual um novo cliente será testado como piloto. Quando estiver satisfeito com o novo software cliente em pré-produção, você poderá promover o cliente para atualizar o restante do site automaticamente com a nova versão.  

Para saber mais sobre como testar clientes, consulte [Como testar atualizações do cliente em uma coleção de pré-produção](/sccm/core/clients/manage/upgrade/test-client-upgrades).  



## <a name="os-deployment"></a>Implantação de sistema operacional  

Esteja ciente das seguintes alterações na implantação do sistema operacional:

- No Assistente para Criar Sequência de Tarefas, um novo tipo de sequência de tarefas está disponível: **Atualizar um sistema operacional do pacote de atualização**. Ele cria as etapas para atualizar os computadores do Windows 7, Windows 8 ou Windows 8.1 para o Windows 10. Para obter mais informações, confira [Atualizar o Windows para a versão mais recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).  

- Agora, o cache par do Windows PE está disponível na implantação de sistemas operacionais. Os computadores que executam uma sequência de tarefas para implantar um sistema operacional podem usar o cache par do Windows PE para obter o conteúdo de uma origem de cache par, em vez de baixar o conteúdo de um ponto de distribuição. Esse comportamento ajuda a minimizar o tráfego de WAN em cenários de filial em que não há nenhum ponto de distribuição local. Para mais informações, confira [Prepare Windows PE peer cache to reduce WAN traffic](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic) (Preparar o cache par do Windows PE para reduzir o tráfego da WAN).  

- Agora é possível exibir o estado do Windows como um serviço no ambiente. Também é possível criar planos de manutenção para formar anéis de implantação e garantir que os computadores com o branch atual do Windows 10 permaneçam atualizados após o lançamento de novos builds. Além disso, você pode exibir alertas quando os clientes com Windows 10 estiverem próximos ao fim do suporte do build. Para obter mais informações, consulte [Gerenciar o Windows como um serviço](/sccm/osd/deploy-use/manage-windows-as-a-service).  



## <a name="application-management"></a>Gerenciamento de aplicativos  

Esteja ciente das seguintes alterações no gerenciamento de aplicativos:

- O Configuration Manager permite a implantação de aplicativos UWP (Plataforma Universal do Windows) para dispositivos que executam o Windows 10 e posterior. Para saber mais, consulte [Criar aplicativos do Windows](/sccm/apps/get-started/creating-windows-applications).  

- O Centro de Software traz uma aparência nova e moderna. Aplicativos disponíveis aos usuários, que antes eram exibidos apenas no catálogo de aplicativos, agora são exibidos no Centro de Software na guia Aplicativos. Esse comportamento torna essas implantações mais detectáveis e elimina a necessidade de os usuários consultarem o catálogo de aplicativos. Além disso, você não precisa mais de um navegador habilitado para Silverlight. Para obter mais informações, consulte [Plan for and configure application management (Planejar e configurar o gerenciamento de aplicativos)](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

- O novo tipo de aplicativo Windows Installer por meio do MDM permite criar e implantar aplicativos baseados no Windows Installer em computadores registrados que executam o Windows 10. Para saber mais, consulte [Criar aplicativos do Windows](/sccm/apps/get-started/creating-windows-applications).  

- Ao criar um aplicativo para um aplicativo iOS internamente, você precisa apenas especificar o arquivo do instalador (.ipa) para o aplicativo. Não é mais necessário especificar um arquivo de lista de propriedade (.plist) correspondente. Consulte [Criar aplicativos do iOS](/sccm/apps/get-started/creating-ios-applications).  

- No Configuration Manager 2012, para especificar um link para um aplicativo na Windows Store, é possível especificar o link diretamente ou navegar até um computador remoto que tem o aplicativo instalado. No branch atual do Configuration Manager, ainda é possível inserir o link diretamente, mas agora, ao invés de acessar um computador de referência, você pode procurar o aplicativo diretamente na loja por meio do console do Configuration Manager.  



## <a name="software-updates"></a>Atualizações de software  

Esteja ciente das seguintes alterações nas atualizações de software:

- Agora, o Configuration Manager pode detectar a diferença entre métodos de gerenciamento de atualização de software em computadores. Especificamente, ele pode diferenciar entre um computador com Windows 10 que se conecta ao Windows Update para Empresas (WUfB) e um computador conectado ao WSUS. O atributo **UseWUServer** é novo e especifica se o computador é gerenciado com o WUfB. É possível usar essa configuração em uma coleção para remover esses computadores do gerenciamento de atualizações de software. Para obter mais informações, consulte [Integration with Windows Update for Business in Windows 10](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10).  

- Agora é possível agendar e executar a tarefa de limpeza do WSUS no console do Configuration Manager. Nas propriedades do **Componente de Ponto de Atualização de Software**, a tarefa de limpeza do WSUS selecionada por você será executada na próxima sincronização de atualizações de software. As atualizações expiradas do software serão definidas com o status de recusadas no servidor WSUS e o Windows Update Agent não examinará mais essas atualizações de software nos computadores. Para obter mais informações, consulte [Schedule and run the WSUS clean up task](/sccm/sum/deploy-use/software-updates-maintenance).  



## <a name="compliance-settings"></a>Configurações de conformidade  

Esteja ciente das seguintes alterações nas configurações de conformidade:

- O Configuration Manager melhora o fluxo de trabalho de criação de itens de configuração. Agora, ao criar um item de configuração e selecionar as plataformas com suporte, apenas as configurações relevantes para essa plataforma estarão disponíveis. Consulte [Introdução às configurações de conformidade](/sccm/compliance/get-started/get-started-with-compliance-settings).  

- O assistente **Criar Item de Configuração** agora facilita a escolha do tipo de item de configuração que você deseja criar. Além disso, itens de configuração novos e atualizados estão disponíveis para:  

    - Dispositivos Windows 10 gerenciados com o cliente do Configuration Manager  

    - Dispositivos Mac OS X gerenciados com o cliente do Configuration Manager  

    - Computadores desktop e de servidor com Windows gerenciados com o cliente do Configuration Manager  

    - Dispositivos Windows 8.1 e Windows 10 gerenciados sem o cliente do Configuration Manager  

    - Dispositivos Windows Phone gerenciados sem o cliente do Configuration Manager  

    - Dispositivos iOS e Mac OS X gerenciados sem o cliente do Configuration Manager  

    - Dispositivos Android e Samsung KNOX Standard gerenciados sem o cliente do Configuration Manager  
  
    Para saber mais, consulte [Como criar itens de configuração](/sccm/compliance/deploy-use/create-configuration-items).  

- Suporte para o gerenciamento de configurações em computadores Mac OS X que são registrados no Microsoft Intune ou gerenciados com o cliente do Configuration Manager. Consulte [Como criar itens de configuração para dispositivos iOS e Mac OS X gerenciados sem o cliente do Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client).  



## <a name="on-premises-mobile-device-management"></a>Gerenciamento de dispositivo móvel local  

Agora é possível gerenciar dispositivos móveis usando a infraestrutura local do Configuration Manager. Todos os dados de gerenciamento e do dispositivo são manipulados localmente e não fazem parte do Microsoft Intune nem de outros serviços de nuvem. Esse tipo de gerenciamento de dispositivos não exige software cliente. O Configuration Manager gerencia dispositivos com recursos integrados aos sistemas operacionais dos dispositivos.  

Para saber mais, confira [Gerenciar dispositivos móveis com a infraestrutura local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).
