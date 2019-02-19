---
title: Qual branch devo usar
titleSuffix: Configuration Manager
description: Aprenda as diferenças entre os branches do System Center Configuration Manager disponíveis.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0bb478eb875e97d8e3088e50daab8538113b40c5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139578"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Qual branch do Configuration Manager devo usar?

*Aplica-se a: System Center Configuration Manager (Branch Atual, 	Branch de Manutenção de Longo Prazo e Technical Preview)*


Há três branches disponíveis do System Center Configuration Manager: branch atual, branch de manutenção em longo prazo e branch technical preview. Use este tópico para ajudar a escolher o branch correto para você.

> [!TIP]  
> Todos os sites em uma hierarquia devem executar o mesmo branch. Não há suporte para ter uma hierarquia com branches diferentes em sites diferentes.


## <a name="current-branch"></a>Branch atual
Esse branch é licenciado para uso em um ambiente de produção. Use esse branch para obter os últimos recursos e funcionalidades. Se você tiver uma das seguintes licenças, poderá usar este branch:  
- System Center Datacenter
- System Center Standard
- System Center Configuration Manager
- Direitos de assinatura equivalente  

Para obter mais informações sobre as opções do licenciamento do Software Assurance, veja [Licenciamento e branches do System Center Configuration Manager](learn-more-editions.md) e [Perguntas frequentes sobre o licenciamento e os branches do Configuration Manager](/sccm/core/understand/product-and-licensing-faq).

A Microsoft planeja lançar atualizações para o branch atual do System Center Configuration Manager algumas vezes por ano. Para versões do Configuration Manager lançadas antes da 1710, o suporte é de 12 meses. A partir da versão 1710, cada versão de atualização permanece com suporte por 18 meses a partir da data de lançamento de GA (disponibilidade geral). O suporte técnico é fornecido durante todo o período suporte. No entanto, nossa estrutura de suporte é dinâmica, evoluindo em duas fases de manutenção distintas que dependem da disponibilidade da última versão do branch atual. Para saber mais, examine o tópico chamado [Suporte para versões do branch atual do System Center Configuration Manager](https://docs.microsoft.com/sccm/core/servers/manage/current-branch-versions-supported). As atualizações para as versões mais novas estão disponíveis como atualizações no console.

Para instalar o Branch Atual como um novo site, use a [mídia de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions). Use também a mídia de linha de base para atualizar do System Center 2012 Configuration Manager com Service Pack 2 ou o System Center 2012 R2 Configuration Manager com Service Pack 1. O acesso a esta mídia depende de como sua organização licenciou o System Center Configuration Manager. 

Você também pode usar a mídia de linha de base para instalar um novo site de uma edição de avaliação do branch atual. A edição de avaliação não requer uma licença. Você pode usar a edição de avaliação de 180 dias. Ela dá suporte à atualização para uma edição licenciada do branch atual. Para instalar apenas uma edição de avaliação, é possível obtê-la no [Centro de Avaliação do TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

> [!NOTE]
> Use a mídia de linha de base para instalar sites para uma nova hierarquia do Configuration Manager. Se você instalou uma versão de linha de base anteriormente, use as atualizações no console para atualizar seus sites para uma nova versão.  
> 
> Sites que são atualizados usando atualizações no console resultam em sites iguais ao novo site instalado usando a mídia de linha de base.
> 
> Para obter mais informações, consulte [Atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).  


### <a name="features-of-the-current-branch"></a>Recursos do branch atual
- Recebe [atualizações no console](/sccm/core/servers/manage/install-in-console-updates) que disponibilizam novos recursos para uso.
- Recebe atualizações no console que fornecem correções de segurança e qualidade para os recursos existentes.
- Dá suporte a atualizações fora da banda quando necessário. Para mais informações, veja [Usar a ferramenta de registro de atualização](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) ou [Usar o instalador do hotfix](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Integra-se com o Microsoft Intune e outros serviços baseados em nuvem.
- Dá suporte à [migração de dados](/sccm/core/migration/migrate-data-between-hierarchies) de e para outras instalações do Configuration Manager.
- Dá suporte à atualização de versões anteriores do Configuration Manager.
- Dá suporte à instalação como uma edição de avaliação, por meio da qual você pode atualizar para uma instalação totalmente licenciada posteriormente.

A versão inicial do Branch Atual foi a versão 1511. Atualizações subsequentes incluem as versões 1602, 1606 e assim por diante. Cada versão permanece no suporte por um ano e a Microsoft recomenda que você atualize para a versão mais nova logo após seu lançamento. Você pode esperar por até um ano antes de atualizar para uma versão mais nova e também pode ignorar uma atualização para instalar a versão mais nova disponível. Como cada versão é cumulativa, se você pular uma atualização e instalar a versão mais recente, ainda terá acesso a todos os recursos e aprimoramentos de versões anteriores.

Para mais informações, confira [Suporte para versões do branch atual](/sccm/core/servers/manage/current-branch-versions-supported).


### <a name="update-options"></a>Opções de atualização
- Com o Software Assurance ativo, você pode instalar atualizações no console para versões do branch atual.  
- Não há nenhuma opção para converter o branch atual em um technical preview. Os branches de technical preview são instalações separadas que não exigem uma licença.
- Não há nenhuma opção para converter seu branch atual para o LTSB (Branch de Manutenção em Longo Prazo). Você deve desinstalar o branch atual e, em seguida, desinstalar o LTSB como uma nova instalação.



##  <a name="long-term-servicing-branch"></a>Branch de manutenção em longo prazo 
Esse é um branch licenciado para uso na produção para clientes do Configuration Manager que estão usando o branch atual e que permitiram que seu SA (Software Assurance) do Configuration Manager ou seus direitos de assinatura equivalente expirassem após 1º de outubro de 2016. Para obter mais informações sobre as opções do licenciamento do Software Assurance, veja [Licenciamento e branches do System Center Configuration Manager](learn-more-editions.md) e [Perguntas frequentes sobre o licenciamento e os branches do Configuration Manager](/sccm/core/understand/product-and-licensing-faq).

O LTSB baseia-se na versão 1606. Esse branch não recebe atualizações no console que oferecem novas funcionalidades ou atualiza funcionalidades existentes. No entanto, correções de segurança críticas são fornecidas. Para instalar o LTSB, você deverá usar a [mídia de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions) da versão 1606 que você obtém como o System Center 2016. Versões de linha de base posteriores não dão suporte à instalação do LTSB.

Para instalar o LTSB como um novo site ou uma atualização de um site com suporte do Configuration Manager 2012, use a versão 1606 da [mídia de linha de base](/sccm/core/servers/manage/updates#baseline-and-update-versions), que você pode obter com o System Center 2016. Você pode usar a mídia de linha de base para instalar um novo site que executa a versão 1606 do branch atual ou um novo site que executa o branch de manutenção em longo prazo.

> [!TIP]  
> Para saber sobre o System Center 2016, consulte a [Documentação do System Center 2016](https://docs.microsoft.com/system-center/index). Esta documentação também identifica como obter o System Center 2016, que exige um contrato de licença da Microsoft ou direitos semelhantes.  
>  
> Para localizar o System Center Configuration Manager versão 1606 no VLSC (Centro de Serviços de Licenciamento por Volume), acesse a guia **Downloads e Chaves** do [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), pesquise `System Center 2016` e selecione **System Center 2016 Datacenter** ou **System Center 2016 Standard**.  
>  
> Você também pode obter uma edição de avaliação do System Center 2016 do [Centro de Avaliação do TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).  


### <a name="features-of-the-ltsb"></a>Recursos do LTSB
-   Recebe atualizações no console que fornecem correções de segurança críticas.
- Fornece uma opção de instalação quando o contrato de SA ou direitos equivalentes para o Configuration Manager tiverem expirado.
- Dá suporte à atualização (conversão) para o branch atual quando você tem um contrato de SA atual ou direitos equivalentes para o Configuration Manager.


### <a name="limitations"></a>Limitações  
O LTSB se baseia na versão 1606 do branch atual e tem as seguintes limitações:
- O LTSB tem suporte por 10 anos de atualizações de segurança críticas após sua disponibilidade geral (outubro de 2016), após o qual o suporte para esse branch expira. Para mais informações sobre o ciclo de vida de suporte, confira [Política de Ciclo de Vida da Microsoft](https://support.microsoft.com/lifecycle).
- Dá suporte a uma lista de definições limitada dos sistemas operacionais do servidor e do cliente e tecnologias relacionadas, como as versões do SQL Server. Para mais informações sobre o que tem suporte com esse branch, confira [Configurações com suporte para o branch de manutenção em longo prazo](supported-configurations-for-ltsb.md).
- Não recebe atualizações para novos recursos
- Não dá suporte para as seguintes funcionalidades: 
   - Adição de uma assinatura do Microsoft Intune, que impede o uso de:
     -  Intune em uma configuração de MDM híbrida
     - MDM local
   -    O painel de serviço, planos de serviço ou canal semestral do Windows 10
   - Versões futuras do Windows 10 LTSB e do Windows Server
   -    Asset Intelligence
   -    Pontos de distribuição baseados em nuvem
   -    Exchange Online como um Exchange Connector
   -    Qualquer recurso de pré-lançamento


### <a name="update-options"></a>Opções de atualização
- Você pode converter sua instalação do LTSB para uma instalação de branch atual. A conversão para o Branch Atual tem suporte antes ou depois do suporte ao LTSB expirar.

  Para converter, você deve ter um contrato de Software Assurance ativo com a Microsoft. Para mais informações, consulte os links a seguir:
  - [Atualizar o Branch de Manutenção em Longo Prazo para o Branch Atual](convert-to-current-branch.md)
  - [Licenciamento e branches do System Center Configuration Manager](learn-more-editions.md)
  - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#baseline-and-update-versions) 
- Não há nenhuma opção para converter o LTSB em um branch de technical preview. Os branches de technical preview são instalações separadas que não exigem uma licença.
-   Você não pode atualizar uma edição de avaliação do branch atual para uma instalação do LTSB.



## <a name="technical-preview-branch"></a>Branch de technical preview
O branch de technical preview é destinado ao uso em um ambiente de laboratório. Saiba mais sobre e experimente os recursos mais recentes que estão sendo desenvolvidos para o Configuration Manager. Não tem suporte em um ambiente de produção e não requer que você tenha um contrato de licença do Software Assurance.

Para instalar um novo site que executa o branch de technical preview, use a [mídia de linha de base do branch de technical preview](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview) mais recente. Depois de instalar o branch de technical preview, há novas versões disponíveis como atualizações no console todo mês.


### <a name="features-of-the-technical-preview-branch"></a>Recursos do branch de technical preview
-  Com base nas versões de linha de base recente do branch atual
-  Recebe atualizações no console que atualizam sua instalação para a versão mais recente do branch de technical preview
-  Inclui novos recursos que estão sendo desenvolvidos e para os quais a Microsoft gostaria de receber seus comentários
-  Recebe atualizações que se aplicam apenas ao branch de technical preview


### <a name="limitations"></a>Limitações
-  [O suporte é limitado](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), incluindo apenas um único site primário e até 10 clientes.  
-  Não pode ser atualizado para o branch atual ou o LTSB.
-  Não dá suporte para os seguintes comportamentos:
   - Uso da migração para importar ou exportar dados para outra instalação do Configuration Manager
   - Atualização de versões anteriores do Configuration Manager
   - Instalação como uma edição de avaliação

Recursos que são introduzidos pela primeira vez em um branch de technical preview geralmente são adicionados ao branch atual em uma atualização posterior. Cada nova versão do branch de technical preview inclui os recursos dos branches de technical preview anteriores, mesmo após esses recursos terem sido adicionados ao branch atual.

Para mais informações, confira [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).


### <a name="update-options"></a>Opções de atualização
-   Você pode instalar qualquer atualização no console para uma nova versão do branch de technical preview.
-   Não há nenhuma opção para converter um branch de technical preview para o branch atual ou LTSB.



## <a name="identify-your-version-and-branch"></a>Identificar a versão e o branch

### <a name="version"></a>Version   
Para verificar a versão do site, no console, acesse **Sobre o System Center Configuration Manager** no canto superior esquerdo do console. Essa caixa de diálogo exibe a **versão do site**. Veja [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines) para obter uma lista de versões do site.

### <a name="branch"></a>Branch
Para confirmar o branch do seu site, no console, vá para **Administração** > **Configuração do Site** > **Sites** e abra **Configurações da Hierarquia**. Se houver uma opção para converter para o branch atual e ela estiver ativa, o site executará a versão de LTSB. Quando o site executa o branch atual, essa opção fica esmaecida.

Para saber mais sobre as diferentes versões do Configuration Manager, veja [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines).
