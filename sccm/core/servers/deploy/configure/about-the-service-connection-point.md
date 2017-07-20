---
title: "Ponto de conexão de serviço | Microsoft Docs"
description: "Saiba mais sobre essa função do sistema de sites do Configuration Manager, bem como entenda e planeje seus diversos usos."
ms.custom: na
ms.date: 6/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: 18
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 0ec241d07f51b80b84d65676ef1207b31a9a9983
ms.openlocfilehash: e3d41dc1bb732e887d722f39ee86deaf0aae3240
ms.contentlocale: pt-br
ms.lasthandoff: 06/28/2017


---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>Sobre o ponto de conexão de serviço no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O ponto de conexão de serviço do System Center Configuration Manager é uma função do sistema de sites que atende a várias funções importantes para a hierarquia. Antes de configurar o ponto de conexão de serviço, entenda e planeje os usos que podem afetar como você configurará essa função de sistema de sites:  

-   **Gerencie dispositivos móveis com o Microsoft Intune**: esta função substitui o conector do Windows Intune usado por versões anteriores do Configuration Manager e pode ser configurada com os detalhes da sua assinatura do Intune. Consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune (MDM (Gerenciamento de dispositivo móvel) híbrido com o System Center Configuration Manager e Microsoft Intune)](../../../../mdm/understand/hybrid-mobile-device-management.md).  

-   **Gerenciar dispositivos móveis com o MDM local**: esta função dá suporte a dispositivos locais gerenciados que não se conectam à Internet. Consulte [Gerenciar dispositivos móveis com a infraestrutura local no System Center Configuration Manager](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

-   **Carregar dados de uso da sua infraestrutura do Configuration Manager**: você pode controlar a quantidade ou o nível dos detalhes que carrega. Os dados carregados nos ajuda a:  

    -   Identificar e solucionar problemas proativamente  

    -   Melhorar nossos produtos e serviços  

    -   Identificar atualizações para o Configuration Manager que se aplicam à versão do Configuration Manager usada  

  Para saber mais sobre os dados coletados em cada nível e como alterar o nível de coleta após a instalação da função, veja [Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data) e siga o link da versão do Configuration Manager que você usa.  

  Para obter mais informações, consulte [Configurações e níveis de dados de uso](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

-   **Baixar as atualizações que se aplicam à sua infraestrutura do Configuration Manager**: somente atualizações relevantes para sua infraestrutura ficam disponíveis, com base nos dados de uso carregados.  

- **Cada hierarquia dá suporte a uma única instância dessa função:**  

 -   A função do sistema de sites só pode ser instalada no site de nível superior da hierarquia (um site de administração central ou site primário autônomo).  

  -   Se expandir um site primário autônomo para uma hierarquia maior, você deve desinstalar essa função do site primário e, em seguida, pode instalá-lo no site de administração central.  


##  <a name="bkmk_modes"></a> Modos de operação  
 O ponto de conexão de serviço oferece suporte a dois modos de operação:  

-   No **modo online**, o ponto de conexão de serviço verifica atualizações automaticamente, a cada 24 horas, e baixa novas atualizações disponíveis para sua infraestrutura e versão do produto atuais, disponibilizando-as no console do Configuration Manager.  

-   No **modo offline**, o ponto de conexão de serviço não se conecta ao serviço de nuvem da Microsoft e você deve [Usar a ferramenta de conexão de serviço do System Center Configuration Manager](../../../../core/servers/manage/use-the-service-connection-tool.md) manualmente para importar as atualizações disponíveis.  

Quando você alterar o modo entre online ou offline depois de ter instalado o ponto de conexão de serviço, será preciso reiniciar o thread SMS_DMP_DOWNLOADER do serviço SMS_Executive do Configuration Manager antes que essa alteração entre em vigor. Para fazer isso, use o Configuration Manager Service Manager para reiniciar apenas o thread SMS_DMP_DOWNLOADER do serviço SMS_Executive. Também é possível reiniciar o serviço SMS_Executive do Configuration Manager (que reinicia a maioria dos componentes do site) ou aguardar até que uma tarefa agendada, como um backup do site, interrompa e posteriormente reinicie o SMS_Executive para você.  

Para usar o Configuration Manager Service Manager, no console, navegue para **Monitoramento** > **Status do Sistema** > **Status do Componente**, clique em **Iniciar** e escolha **Configuration Manager Service Manager**. No Service Manager:  

-   No painel de navegação, expanda o site e **Componentes**, depois escolha o componente que você deseja reiniciar.  

-   No painel de detalhes, clique com o botão direito do mouse no componente e escolha **Consulta**.  

-   Depois que o status do componente for confirmado, clique com o botão direito do mouse no componente novamente e escolha **Parar**.  

-   **Consulte** o componente novamente para confirmar que ele foi interrompido e, em seguida, clique com o botão direito do mouse no componente mais uma vez e escolha **Iniciar**.  

> [!IMPORTANT]  
>  O processo que adiciona uma assinatura do Microsoft Intune ao ponto de conexão de serviço configura automaticamente a função do sistema de sites como online. O ponto de conexão de serviço não dá suporte ao modo offline quando configurado com uma assinatura do Intune.  

**Quando a função é instalada em um computador remoto do servidor do site:**  

-   A conta de computador do servidor do site deve ser um administrador local no computador que hospeda uma conexão de serviço remoto.

-   Você deve configurar o servidor do sistema de sites que hospeda a função com uma Conta de instalação do sistema de sites.  

-   A conta de instalação do sistema de sites é usada pelo gerenciador de distribuição no servidor de sites para transferir atualizações do ponto de conexão de serviço.

##  <a name="bkmk_urls"></a> Requisitos de acesso à Internet  
Para habilitar a operação, o computador que hospeda o ponto de conexão de serviço e quaisquer firewalls entre o computador e a Internet deve passar as comunicações pela **porta TCP 443** e **porta TCP 443** nos seguintes locais da Internet. O ponto de conexão de serviço também dá suporte ao uso de um proxy da Web (com ou sem autenticação) para acessar esses locais.  Se você precisar configurar uma conta de proxy da web, consulte: [Suporte do servidor proxy no System Center Configuration Manager](/sccm/core/plan-design/network/proxy-server-support).

**Atualizações e manutenção**  

-   *.akamaiedge.net  

-   *.akamaitechnologies.com 

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   download.windowsupdate.com

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *manage.microsoft.com  
-   https://bspmts.mp.microsoft.com/V
-   https://login.microsoftonline.com/{TenantID}


**Serviço do Windows 10**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  

## <a name="install-the-service-connection-point"></a>Instalar o ponto de conexão de serviço
Quando você executa **Instalação** para instalar o site de nível superior de uma hierarquia, você tem a opção de instalar o ponto de conexão de serviço.

Após a execução da configuração, ou se você estiver reinstalando a função do sistema de sites, use o assistente **Adicionar Funções do Sistema de Site** ou o assistente **Criar Servidor do Sistema de Site** para instalar o sistema de site em um servidor no site de nível superior da hierarquia, isto é, o site de administração central ou um site primário autônomo. Ambos os assistentes estão localizados na guia **Início** no console em **Administração** > **Configuração do Site** > **Funções de Servidores e Sistema de Site**.

## <a name="log-files-used-by-the-service-connection-point"></a>Os arquivos de log usados pelo ponto de conexão de serviço
Para exibir informações sobre carregamentos para a Microsoft, veja o **Dmpuploader.log** no computador que executa o ponto de conexão de serviço.  Para downloads, incluindo o progresso do download de atualizações, veja **Dmpdownloader.log**. Para obter a lista completa de logs relacionados ao ponto de conexão de serviço, veja [Ponto de conexão de serviço](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) no tópico de arquivos de log do Configuration Manager.

Você também pode usar os fluxogramas a seguir para entender o fluxo de processo e as principais entradas de log para downloads de atualização e replicação de atualizações para outros sites:
 - [Fluxograma — baixar atualizações](/sccm/core/servers/manage/download-updates-flowchart)
 - [Fluxograma — atualizar replicação](/sccm/core/servers/manage/update-replication-flowchart)

