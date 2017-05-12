---
title: "Atualizações | Microsoft Docs"
description: "Saiba mais sobre um método de serviço no console chamado **Atualizações e Manutenção** que facilita a localização e a instalação das atualizações recomendadas."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
caps.latest.revision: 51
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 90775fcf2549080a43e9c1606caa79d9eb90a89c
ms.openlocfilehash: a33960fb89b71c0f8128e21a5054f5b63cfc6b17
ms.contentlocale: pt-br
ms.lasthandoff: 05/02/2017


---
# <a name="updates-for-system-center-configuration-manager"></a>Atualizações para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager usa um método de serviço no console chamado **Atualizações e Manutenção** que facilita a localização e a instalação das atualizações recomendadas para a infraestrutura do Configuration Manager. Esse método de serviço no console é complementado por atualizações fora da banda, como hotfixes, destinadas a clientes que precisam resolver problemas possivelmente específicos de seus ambientes.  

> [!TIP]
> Ao gerenciar a infraestrutura do site e da hierarquia do System Center Configuration Manager, os termos *upgrade*, *atualização* e *instalação* são usados para descrever três conceitos separados. Para saber como cada termo é usado, consulte [About upgrade, update, and install](/sccm/core/understand/upgrade-update-install) (Sobre upgrade, atualização e instalação).


 **Os tópicos a seguir podem ajudá-lo a entender como encontrar e instalar os diferentes tipos de atualizações para o System Center Configuration Manager:**  

-   [Install in-console updates for System Center Configuration Manager (Instalar atualizações no console para o System Center Configuration Manager)](../../../core/servers/manage/install-in-console-updates.md)  

-   [Usar a Ferramenta de Conexão de Serviço do System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [Usar a Ferramenta de Registro de Atualização para importar hotfixes para o System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [Usar o Instalador de Hotfix para instalar atualizações do System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


Se você usa o branch do Technical Preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview) para obter informações adicionais específicas do branch.


##  <a name="bkmk_Baselines"></a> Versões de linha de base e atualização  
 A primeira versão da ramificação atual do System Center Configuration Manager era a versão 1511, que foi a versão de linha de base. As versões mais recentes de linha de base incluem a versão 1606 e 1702:

-   Use a versão de linha de base mais recente ao instalar um novo site em uma nova hierarquia.  

-   Você deve usar uma versão de linha de base para atualizar o System Center 2012 Configuration Manager.  

-   Versões de linha de base adicionais serão lançadas periodicamente. Quando você usa a versão de linha de base mais recente para instalar uma nova hierarquia, evita a instalação de uma versão desatualizada do Configuration Manager, seguida por uma atualização de sua infraestrutura para atualizá-la.  

Depois de instalar uma versão de linha de base, versões adicionais do Configuration Manager estarão disponíveis como atualizações no console. As atualizações no console atualizam a infraestrutura para a versão mais recente do Configuration Manager.  

-   Instale as atualizações no console para atualizar a versão do site de nível superior.  

-   As atualizações instaladas no site de administração central serão instaladas automaticamente nos sites primários filhos, a não ser que sejam bloqueadas por uma janela de manutenção configurada no site primário.  

-   Você deve atualizar manualmente os sites secundários para uma nova versão de atualização usando o console.  

Ao instalar uma atualização, ela armazena os arquivos de instalação dessa versão no servidor do site em uma pasta chamada CD.Mais recente. Consulte [A pasta CD.Latest para o System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md) para obter mais informações sobre esses arquivos.  

-   Use os arquivos na pasta CD.Mais recente durante a recuperação do site e para instalar sites adicionais em uma hierarquia que não execute mais uma versão de linha de base.  

-   Você não pode usar os arquivos de instalação da CD.Mais recente para instalar o primeiro site de uma nova hierarquia ou para atualizar um site do System Center 2012 Configuration Manager.  

Algumas atualizações do Configuration Manager estão disponíveis como uma versão de atualização no console para a infraestrutura existente e como uma nova versão de linha de base.  

As seguintes versões do Configuration Manager estão disponíveis como uma linha de base e/ou uma atualização:  

|Versão |Data de disponibilidade|[Data de término do suporte](/sccm/core/servers/manage/current-branch-versions-supported) |Linha de base|Atualização no console|  
|-------------|-----------|------------|--------------|------------------------|  
|[1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)<br /><br /> 5.00.8498.1000|27/03/2017| 27/03/2018|Sim|Sim|
|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)<br /><br /> 5.00.8458.1000|18/11/2016| 18/11/2017|Não|Sim|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)<br /><br /> 5.00.8412.1000|22/07/2016| 22/07/2017|Não|Sim|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606) com o pacote cumulativo de atualizações do hotfix 1606 (KB3186654) </br></br>5.00.8412.1307 *(Observação 1)* |12/10/2016| 22/07/2017|Sim|Não|
| 1602<br /><br /> 5.00.8355.1000|11/03/2016| 11/03/2017|Não|Sim|
| 1511 <br /><br /> 5.00.8325.1000|12/08/2015| 12/08/2016|Sim|Não|  


*(Observação 1)* Esta mídia de linha de base 1606 está disponível como parte do Microsoft System Center 2016 ou do System Center Configuration Manager (Branch Atual e Branch de Manutenção em Longo Prazo 1606).

Para verificar a versão do site do Configuration Manager, no console vá para **Sobre o System Center Configuration Manager** no canto superior esquerdo do console onde é exibida a versão do novo site e do console.  

##  <a name="bkmk_inconsole"></a> Atualizações e serviços no console  
 Ao usar uma instalação pronta para produção do System Center Configuration Manager, também conhecida como o branch atual, a maioria das atualizações para instalar ficam disponíveis usando o canal Atualizações e Manutenção. Esse método identifica, baixa e disponibiliza as atualizações que se aplicam à versão atual e à configuração da sua infraestrutura e inclui apenas as atualizações que a Microsoft recomenda para todos os clientes.   
 Elas incluem:  

-   Novas versões, como a versão 1610  

-   Atualizações, que incluem novos recursos para a versão atual  

-   Hotfixes, para a sua versão do Configuration Manager e que todos os clientes devem instalar  

As atualizações no console oferecem maior estabilidade e resolvem os problemas comuns. Elas substituem os tipos de atualização das versões anteriores do produto por service packs, atualizações cumulativas e hotfixes que se aplicam a todos os clientes e à extensão do Microsoft Intune. Essas atualizações podem ser aplicadas a um ou mais dos itens a seguir:  

-   Servidores do site primário e de administração central  

-   Servidores do sistema de site e funções do sistema de site  

-   Instâncias do provedor de SMS  

-   Consoles do Configuration Manager  

-   Clientes do Configuration Manager  

O Configuration Manager descobre novas atualizações quando você sincroniza a função do sistema de sites do ponto de conexão de serviço com o centro de download e serviço de nuvem da Microsoft:  

-   Quando o ponto de conexão de serviço está no modo online, o site sincroniza-se com a Microsoft diariamente para identificar automaticamente as novas atualizações que se aplicam à infraestrutura.  Para baixar atualizações e arquivos redist para atualizações, o computador que hospeda a função do sistema de sites do ponto de conexão de serviço usa o contexto **Sistema** para acessar os seguintes locais da Internet: go.microsoft.com e Microsoft.com. Para obter informações sobre outros locais aos quais o ponto de conexão de serviço se conecta, consulte [Requisitos de acesso de Internet](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls) em [Sobre o ponto de conexão de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   Quando o ponto de conexão de serviço estiver no modo offline, use a ferramenta de conexão de serviço para sincronizar-se manualmente com a Microsoft Cloud. Para obter mais informações, consulte [Use the Service Connection Tool for System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

-   As atualizações no console substituem a necessidade de localizar e instalar atualizações, service packs e novos recursos individuais de forma independente.  

-   Você instala somente as atualizações no console que escolhe e ao instalar algumas atualizações, você pode selecionar os recursos individuais que deseja habilitar e usar. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](../../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Ao instalar uma atualização no console:  

-   Ele executa automaticamente uma verificação de pré-requisitos. Você também pode executar essa verificação antes de iniciar a instalação.  

-   Ele instala no site de administração central (se houver) e nos sites primários automaticamente. É possível controlar quando cada servidor do site primário tem permissão para atualizar sua infraestrutura usando [Service windows for site servers](../../../core/servers/manage/service-windows.md) (Períodos de serviço para servidores do site).  

-   Depois que um servidor do site é atualizado, todas as funções do sistema de site afetadas (incluindo as instâncias do Provedor de SMS) são atualizadas automaticamente. Os consoles do Configuration Manager também solicitam que o usuário do console atualize o console depois que o site instala a atualização.  

-   Se uma atualização incluir o cliente do Configuration Manager, você terá a opção de testar a atualização em pré-produção ou aplicar a atualização a todos os clientes imediatamente.  

-   Depois que um site primário é atualizado, os sites secundários não são atualizados automaticamente. Você deve iniciar a atualização de site secundário.  

> [!NOTE]  
>  A versão de produção do System Center Configuration Manager (Branch Atual), o Branch de Manutenção de Longo Prazo e o Technical Preview do System Center Configuration Manager são versões diferentes. Portanto, as atualizações que se aplicam a uma ramificação não estão disponíveis como atualizações no console para outras ramificações. Para saber mais sobre as ramificações disponíveis, confira [Qual ramificação do Configuration Manager devo usar?](/sccm/core/understand/which-branch-should-i-use)

##  <a name="bkmk_outofband"></a> Hotfixes fora da banda  
Alguns hotfixes são lançados com disponibilidade limitada para resolver problemas específicos ou são aplicáveis a todos os clientes, mas não podem ser instalados usando o método no console. Essas correções são entregues fora de banda e não são descobertas do serviço de nuvem da Microsoft.  

Geralmente, você sabe mais sobre os hotfixes fora de banda por meio dos serviços de atendimento ao cliente da Microsoft, de um artigo da base de dados de conhecimento ou do [System Center Configuration Manager Team Blog](https://blogs.technet.microsoft.com/configmgrteam) (Blog da Equipe do System Center Configuration Manager) quando procura corrigir ou solucionar um problema na implantação do Configuration Manager.  

Instale essas correções manualmente, usando um destes dois métodos:  

-   **Ferramenta de Registro de Atualização:** essa ferramenta importa o hotfix manualmente para o seu console do Configuration Manager, que você poderá usar para instalar a atualização da mesma forma que faria com as atualizações no console descobertas automaticamente. Esse método é usado para as atualizações que usam a seguinte estrutura de nome de arquivo: **.update.exe**.  O nome de arquivo completo para esse tipo de hotfix é semelhante a: **&lt;Produto\>-&lt;versão do produto\>-&lt;ID do artigo da base de dados\>-ConfigMgr.Update.exe**.  

     Para obter mais informações, consulte [Usar a Ferramenta de Registro de Atualização para importar hotfixes para o System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

-   **Instalador de hotfix:** essa ferramenta é usada para instalar manualmente um hotfix que não pode ser instalado usando o método no console. Esse método é usado para correções que usam a seguinte estrutura de nome de arquivo: **&lt;Produto\>-&lt;versão do produto\>-&lt;ID do artigo da base de dados\>-&lt;plataforma\>-&lt;idioma\>.exe**.

     Para obter mais informações, consulte [Usar o Instalador do Hotfix para instalar atualizações do System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md).

