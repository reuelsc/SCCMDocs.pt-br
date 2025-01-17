---
title: Ponto de Conexão de Serviço
titleSuffix: Configuration Manager
description: Saiba mais sobre essa função do sistema de sites do Configuration Manager, bem como entenda e planeje seus diversos usos.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: af65085590d8b02d6b3a020668566a334de42f13
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285561"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Sobre o ponto de conexão de serviço no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O ponto de conexão de serviço é uma função de sistema de sites que atende a várias funções importantes para a hierarquia. Antes de configurar o ponto de conexão de serviço, entenda e planeje as possibilidades de uso. O planejamento do uso pode afetar a maneira como você configura essa função do sistema de sites:  

- **Gerenciar dispositivos móveis com o Microsoft Intune**: Essa função substitui o conector do Windows Intune usado por versões anteriores do Configuration Manager e pode ser configurada com os detalhes da sua assinatura do Intune. Para obter mais informações, veja [MDM (gerenciamento de dispositivo móvel) híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).  

- **Gerenciar dispositivos móveis com o MSM local:** Essa função oferece suporte a dispositivos locais que você gerencia e que não se conectam à Internet. Para saber mais, confira [Gerenciar dispositivos móveis com a infraestrutura local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  

- **Carregar dados de uso por meio da infraestrutura do Configuration Manager**: Você pode controlar a quantidade ou nível dos detalhes que carrega. Os dados carregados ajudam a:  

    - Identificar e solucionar problemas proativamente  

    - Melhorar nossos produtos e serviços  

    - Identificar atualizações para o Configuration Manager que se aplicam à versão do Configuration Manager usada  

    Para obter mais informações sobre os dados coletados em cada nível e como alterar o nível de coleta após a instalação da função, confira [Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data). Depois, siga o link da versão do Configuration Manager que você usa.  

    Para obter mais informações, consulte [Configurações e níveis de dados de uso](/sccm/core/servers/deploy/install/setup-reference#bkmk_usage).  

- **Baixar as atualizações que se aplicam à infraestrutura do Configuration Manager**: Somente atualizações relevantes para sua infraestrutura ficam disponíveis, com base nos dados de uso carregados.  

- **Cada hierarquia dá suporte a uma única instância dessa função**:  

    - A função do sistema de sites só pode ser instalada no site de nível superior da hierarquia (um site de administração central ou site primário autônomo).  

    - Se expandir um site primário autônomo para uma hierarquia maior, você deve desinstalar essa função do site primário e, em seguida, pode instalá-lo no site de administração central.  


##  <a name="bkmk_modes"></a> Modos de operação  
O ponto de conexão de serviço oferece suporte a dois modos de operação:  

- No **modo online**, o ponto de conexão de serviço verifica se há atualizações automaticamente a cada 24 horas. Ele baixa as atualizações disponíveis para sua infraestrutura e versão do produto atuais, disponibilizando-as no console do Configuration Manager.  

- No **modo offline**, o ponto de conexão de serviço não se conecta ao serviço de nuvem da Microsoft. Para importar manualmente as atualizações disponíveis, use a [ferramenta de conexão de serviço](/sccm/core/servers/manage/use-the-service-connection-tool).  

Se você alterar entre os modos online ou offline depois de ter instalado o ponto de conexão de serviço, será preciso reiniciar o thread SMS_DMP_DOWNLOADER do serviço SMS_Executive do Configuration Manager antes que essa alteração entre em vigor. Use o Configuration Manager Service Manager para reiniciar apenas o thread SMS_DMP_DOWNLOADER do serviço SMS_Executive. Também é possível reiniciar o serviço SMS_Executive do Configuration Manager, o que reinicia a maioria dos componentes do site. Como alternativa, aguarde uma tarefa agendada, como um backup do site, que interromperá e reiniciará o serviço SMS_Executive para você.  

Para usar o Configuration Manager Service Manager, no console, navegue para **Monitoramento** > **Status do Sistema** > **Status do Componente**, clique em **Iniciar** e escolha **Configuration Manager Service Manager**. No Service Manager:  

- No painel de navegação, expanda o site e **Componentes**, depois escolha o componente que você deseja reiniciar.  

- No painel de detalhes, clique com o botão direito do mouse no componente e escolha **Consulta**.  

- Depois que o status do componente for confirmado, clique com o botão direito do mouse no componente novamente e escolha **Parar**.  

- **Consulte** o componente novamente para confirmar se ele está parado. Clique com o botão direito do mouse no componente mais uma vez e, em seguida, escolha **Iniciar**.  

> [!IMPORTANT]  
> O processo que adiciona uma assinatura do Microsoft Intune ao ponto de conexão de serviço configura automaticamente a função do sistema de sites como online. O ponto de conexão de serviço não dá suporte ao modo offline quando configurado com uma assinatura do Intune.  

**Quando a função é instalada em um computador remoto do servidor do site:**  

- A conta de computador do servidor do site deve ser um administrador local no computador que hospeda uma conexão de serviço remoto.

- Você deve configurar o servidor do sistema de sites que hospeda a função com uma conta de instalação do sistema de sites.  

- A conta de instalação do sistema de sites é usada pelo gerenciador de distribuição no servidor de sites para transferir atualizações do ponto de conexão de serviço.


## <a name="bkmk_urls"></a> Requisitos de acesso à Internet  

Se sua organização restringe a comunicação de rede com a Internet usando um dispositivo de firewall ou proxy, você precisará permitir que o ponto de conexão de serviço acesse os pontos de extremidade da Internet.

Para saber mais, confira [Requisitos de acesso à Internet](/sccm/core/plan-design/network/internet-endpoints#bkmk_scp).


## <a name="install-the-service-connection-point"></a>Instalar o ponto de conexão de serviço
Quando você executa **Instalação** para instalar o site de nível superior de uma hierarquia, você tem a opção de instalar o ponto de conexão de serviço.

Após a execução da configuração, ou se você estiver reinstalando a função do sistema de sites, use o assistente **Adicionar Funções do Sistema de Site** ou o assistente **Criar Servidor do Sistema de Site** para instalar o sistema de site em um servidor no site de nível superior da hierarquia, isto é, o site de administração central ou um site primário autônomo. Ambos os assistentes estão localizados na guia **Início** no console em **Administração** > **Configuração do Site** > **Funções de Servidores e Sistema de Site**.



## <a name="log-files-used-by-the-service-connection-point"></a>Os arquivos de log usados pelo ponto de conexão de serviço
Para exibir informações sobre carregamentos para a Microsoft, veja o **Dmpuploader.log** no computador que executa o ponto de conexão de serviço.  Para downloads, incluindo o progresso do download de atualizações, veja **Dmpdownloader.log**. Para obter a lista completa de logs relacionados ao ponto de conexão de serviço, veja [Ponto de conexão de serviço](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) no artigo de arquivos de log do Configuration Manager.

Você também pode usar os fluxogramas a seguir para entender o fluxo de processo e as principais entradas de log para downloads de atualização e replicação de atualizações para outros sites:
- [Fluxograma — baixar atualizações](/sccm/core/servers/manage/download-updates-flowchart)
- [Fluxograma — atualizar replicação](/sccm/core/servers/manage/update-replication-flowchart)
