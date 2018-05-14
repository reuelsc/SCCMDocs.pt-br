---
title: Atualizações e serviços
titleSuffix: Configuration Manager
description: Saiba mais sobre um método de serviço no console chamado Atualizações e Manutenção que facilita a localização e a instalação das atualizações recomendadas.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9c2a9d7c754e7a1a02527c4c985d1b9db6bc7d14
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="updates-for-system-center-configuration-manager"></a>Atualizações para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager usa um método de serviço no console chamado **Atualizações e Manutenção**. Esse método no console facilita a localização e instalação de atualizações recomendadas para sua infraestrutura do Configuration Manager. O serviço no console é complementado por atualizações fora da banda, como hotfixes, destinadas a clientes que precisam resolver problemas possivelmente específicos de seus ambientes.  

> [!TIP]  
> Os termos *upgrade*, *atualizar* e *instalar* são usados para descrever três conceitos separados no Configuration Manager. Para mais informações sobre como cada termo é usado, veja [Sobre upgrade, atualização e instalação](/sccm/core/understand/upgrade-update-install).


 **Os tópicos a seguir podem ajudá-lo a entender como encontrar e instalar os diferentes tipos de atualizações para o Configuration Manager:**  

-   [Instalar de atualizações no console](../../../core/servers/manage/install-in-console-updates.md)  

-   [Usar a ferramenta de conexão de serviço](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [Usar a ferramenta de registro de atualização para importar hotfixes](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [Usar o instalador do hotfix para instalar atualizações](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


Para saber mais sobre o branch de technical preview, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).



##  <a name="bkmk_Baselines"></a> Versões de linha de base e atualização  

Use a versão de linha de base mais recente ao instalar um novo site em uma nova hierarquia. 
- Use também uma versão de linha de base para atualizar o System Center 2012 Configuration Manager.  

- Depois de atualizar para o branch atual do Configuration Manager, não use versões de linha de base para se manter atualizado. Em vez disso, use somente [atualizações no console](/sccm/core/servers/manage/install-in-console-updates) para atualizar para a versão mais recente.  

- Versões de linha de base adicionais são lançadas periodicamente. Ao usar a versão de linha de base mais recente para instalar uma nova hierarquia, você evita a instalação de uma versão desatualizada ou sem suporte do Configuration Manager, seguida por uma atualização adicional de sua infraestrutura para atualizá-la.  

Depois de instalar uma versão de linha de base, versões adicionais do Configuration Manager estarão disponíveis como atualizações no console. As atualizações no console atualizam a infraestrutura para a versão mais recente do Configuration Manager.  

-   Instale as atualizações no console para atualizar a versão do site de nível superior.  

-   Atualizações instaladas automaticamente no site de administração central em sites primários filho. Controle esse intervalo usando uma janela de manutenção no site primário.  

-   Atualize manualmente os sites secundários para uma nova versão de atualização usando o console.  

Ao instalar uma atualização, ela armazena os arquivos de instalação dessa versão no servidor do site em uma pasta chamada **CD.Latest**. Para mais informações sobre esses arquivos, confira [A pasta CD.Latest](../../../core/servers/manage/the-cd.latest-folder.md).  

-   Use os arquivos na pasta CD.Latest durante a recuperação de site. Além disso, quando sua hierarquia não executar mais uma versão de linha de base, use esses arquivos para instalar sites adicionais.  

-   Você não pode usar os arquivos de instalação do CD.Latest para instalar o primeiro site de uma nova hierarquia ou para atualizar um site do System Center 2012 Configuration Manager.  

Algumas atualizações do Configuration Manager estão disponíveis como uma versão de atualização no console para a infraestrutura existente e como uma nova versão de linha de base.  

As seguintes versões do Configuration Manager estão disponíveis como uma linha de base e/ou uma atualização:  

|Version |Data de disponibilidade|[Data de término do suporte](/sccm/core/servers/manage/current-branch-versions-supported) |Linha de base|Atualização no console|  
|-------------|-----------|------------|--------------|------------------------|  
|[1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)<br /><br /> 5.00.8634.1000|22 de março de 2018|22 de setembro de 2019|Sim|Sim|
|[1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)<br /><br /> 5.00.8577.1000|20 de novembro de 2017|20 de maio de 2019|Não|Sim|
|[1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)<br /><br /> 5.00.8540.1000|31 de julho de 2017|31 de julho de 2018|Não|Sim|
|[1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)<br /><br /> 5.00.8498.1000|27 de março de 2017| 27 de março de 2018|Sim|Sim|
|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)<br /><br /> 5.00.8458.1000|18 de novembro de 2016| 18 de novembro de 2017|Não|Sim|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)<br /><br /> 5.00.8412.1000|22 de julho de 2016| 22 de julho de 2017|Não|Sim|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606) com o pacote cumulativo de atualizações do hotfix 1606 (KB3186654) </br></br>5.00.8412.1307 *(Observação 1)* |12 de outubro de 2016| 12 de outubro de 2017|Sim|Não|
| 1602<br /><br /> 5.00.8355.1000|11 de março de 2016| 11 de março de 2017|Não|Sim|
| 1511 <br /><br /> 5.00.8325.1000|8 de dezembro de 2015| 8 de dezembro de 2016|Sim|Não|  


*(Observação 1)*  A mídia de linha de base 1802 está disponível como parte das seguintes versões no VLSC [(Centro de Serviços de Licença por Volume)](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx):
- System Center Config Mgr (branch atual)
- System Center 2016 Datacenter
- System Center 2016 Standard. Por exemplo, pesquisar VLSC para `System Center Config Mgr (current branch)`. Localize a mídia de linha de base 1802 na lista de arquivos e baixe essa versão.

Para verificar a versão do site do Configuration Manager, no console, vá para **Sobre o System Center Configuration Manager** no canto superior esquerdo do console. Essa caixa de diálogo exibe a versão do site e do console.  

 > [!Note]  
 > Iniciando na versão 1802, a versão do console agora é ligeiramente diferente da versão do site. A versão secundária do console agora corresponde à versão de lançamento do Configuration Manager. Por exemplo, no Configuration Manager versão 1802, a versão inicial é 5.0.8634.1000 e a versão inicial do console é 5.**1802**.1082.1700. Os números de build (1082) e de revisão (1700) podem ser alterados com hotfixes futuros para a versão 1802.



##  <a name="bkmk_inconsole"></a> Atualizações e serviços no console  
 Ao usar uma instalação pronta para produção do branch atual do Configuration Manager, a maioria das atualizações ficam disponíveis usando o canal **Atualizações e Manutenção**. Esse método identifica, baixa e disponibiliza as atualizações que se aplicam à versão atual e à configuração da sua infraestrutura. Ele inclui apenas as atualizações que a Microsoft recomenda para todos os clientes.   

 As atualizações incluídas são:  

-   Novas versões, como a versão 1702, 1706, 1710 ou 1802.  

-   Atualizações que incluem novos recursos para a versão atual.

-   Hotfixes para a sua versão do Configuration Manager e que todos os clientes devem instalar.

As atualizações no console oferecem maior estabilidade e resolvem os problemas comuns. Elas substituem os tipos de atualização das versões anteriores do produto por service packs, atualizações cumulativas e hotfixes que se aplicam a todos os clientes e à extensão do Microsoft Intune. 

As atualizações no console podem ser aplicadas a um ou mais dos sistemas a seguir:  

-   Servidores do site primário e de administração central  

-   Servidores do sistema de site e funções do sistema de site  

-   Instâncias do provedor de SMS  

-   Consoles do Configuration Manager  

-   Clientes do Configuration Manager  

O Configuration Manager descobre novas atualizações para você. Sincronize o ponto de conexão de serviço do Configuration Manager com o serviço de nuvem da Microsoft, observando os seguintes comportamentos:  

-   Quando o ponto de conexão de serviço está no modo online, o site sincroniza com a Microsoft diariamente. Ele identifica automaticamente novas atualizações que se aplicam à sua infraestrutura. Para baixar atualizações e arquivos redistribuíveis, o computador que hospeda a função do sistema de sites do ponto de conexão de serviço usa o contexto **Sistema** para acessar os seguintes locais da Internet: go.microsoft.com e download.microsoft.com. Para saber mais sobre as localizações adicionais usadas pelo ponto de conexão de serviço, confira [Requisitos de acesso à Internet](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls).  

-   Quando o ponto de conexão de serviço estiver no modo offline, use a ferramenta de conexão de serviço para sincronizar-se manualmente com a nuvem da Microsoft. Para obter mais informações, veja [Usar a ferramenta de conexão de serviço](../../../core/servers/manage/use-the-service-connection-tool.md).  

-   As atualizações no console substituem a necessidade de localizar e instalar atualizações, service packs e novos recursos individuais de forma independente.  

-   Instale somente as atualizações no console que você escolher. Ao instalar algumas atualizações, você pode selecionar recursos individuais para habilitar e usar. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](../../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Quando você instala uma atualização no console, ocorre o seguinte processo:  

-   Ele executa automaticamente uma verificação de pré-requisitos. Você também pode executar manualmente essa verificação antes de iniciar a instalação.  

-   Ela instala no site de nível superior no seu ambiente. Esse é o site de administração central, se você tiver um. Em uma hierarquia, a atualização instala automaticamente em sites primários. Controle quando cada servidor do site primário tem permissão para atualizar usando [Períodos de serviço para servidores do site](../../../core/servers/manage/service-windows.md).  

-   Depois que um servidor do site é atualizado, todas as funções do sistema de site afetadas são atualizadas automaticamente. Essas funções incluem instâncias do provedor de SMS. Após o site instalar a atualização, os consoles do Configuration Manager também solicitam que o usuário do console atualize o console.  

-   Se uma atualização incluir o cliente do Configuration Manager, você terá a opção de testar a atualização em pré-produção ou aplicar a atualização a todos os clientes imediatamente.  

-   Depois que um site primário é atualizado, os sites secundários não são atualizados automaticamente. Em vez disso, você deve iniciar manualmente a atualização de site secundário.  

> [!NOTE]  
>  O branch atual do Configuration Manager, o branch de manutenção em longo prazo e o branch de technical preview são versões diferentes. Portanto, as atualizações que se aplicam a um branch não estão disponíveis como atualizações no console para outros branches. Para saber mais sobre as ramificações disponíveis, confira [Qual ramificação do Configuration Manager devo usar?](/sccm/core/understand/which-branch-should-i-use)



##  <a name="bkmk_outofband"></a> Hotfixes fora da banda  
Alguns hotfixes são lançados com disponibilidade limitada para resolver problemas específicos. Outros hotfixes são aplicáveis a todos os clientes, mas não é possível instalar usando o método no console. Essas correções são entregues fora de banda e não são descobertas do serviço de nuvem da Microsoft.  

Geralmente, quando para corrigir ou solucionar um problema na implantação do Configuration Manager, há mais informações sobre os hotfixes fora de banda por meio dos serviços de atendimento ao cliente da Microsoft, um artigo da base de dados de conhecimento de suporte da Microsoft ou do [Blog da Equipe do System Center Configuration Manager](https://blogs.technet.microsoft.com/configmgrteam). 

Instale essas correções manualmente, usando um dos seguintes dois métodos:  

-   **Ferramenta de registro de atualização**: essa ferramenta importa o hotfix manualmente no console do Configuration Manager. Em seguida, instale a atualização como você faria nas atualizações no console que são descobertas automaticamente.  

    - Esse método é usado para hotfixes que usam a seguinte estrutura de nome de arquivo:  
         `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`    

    - Para mais informações, veja [Usar a ferramenta de registro de atualização para importar hotfixes](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

-   **Instalador de hotfix**: use essa ferramenta para instalar manualmente um hotfix que não pode ser instalado usando o método no console.  

    - Esse método é usado para correções que usam a seguinte estrutura de nome de arquivo:   
         `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

    - Para obter mais informações, veja [Usar o instalador do hotfix para instalar atualizações](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md).  
