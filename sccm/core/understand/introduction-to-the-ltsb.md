---
title: "Introdução ao Branch de Manutenção em Longo Prazo | Microsoft Docs"
description: "Saiba mais sobre o Branch de Manutenção em Longo Prazo do System Center Configuration Manager."
ms.custom: na
ms.date: 1/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a86546eb513a2ef6f95013178b141fb1833ea8ab
ms.openlocfilehash: fa4d7dd2e1edbbc0b136ebfc27560f20ab63c12e


---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Introdução ao Branch de Manutenção em Longo Prazo do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch de Manutenção em Longo Prazo)*

Use este tópico para aprender mais sobre o LTSB (Branch de Manutenção em Longo Prazo) do Configuration Manager e entender a documentação deste branch.


O LTSB é um branch distinto do Configuration Manager baseado na versão 1606 do Branch Atual. Em comparação com o Branch Atual, o LTSB tem [funcionalidade reduzida](#features-that-are-not-available-in-the-ltsb-of-configuration-manager). Ele é projetado para clientes que [permitiram que seu SA (Software Assurance) ou seus direitos de assinatura equivalente prescrevessem](/sccm/core/understand/learn-more-editions#software-assurance-and-the-ltsb).

**Visão geral do licenciamento:**   
Os clientes com SA (Software Assurance) ativo para as licenças do System Center Configuration Manager ou com direitos de assinatura equivalentes a partir de 1º de outubro de 2016 têm direito de usar a versão 1606, de outubro de 2016, do System Center Configuration Manager. Clientes que adquiriram direitos do System Center Configuration Manager em ou após 1º de outubro de 2016 encontrarão duas opções licenciadas durante a instalação: o Branch Atual e o LTSB (Branch de Manutenção em Longo Prazo).

**Especificações de licenciamento:**  
[Os termos e condições completos dos produtos que você compra por meio dos programas de licenciamento por volume da Microsoft podem ser encontrados aqui](http://go.microsoft.com/fwlink/?LinkId=800052).

Clientes que têm direitos perpétuos do System Center Configuration Manager ou que permitirem que o SA ou a assinatura expire após 1º de outubro podem instalar a versão do LTSB do System Center Configuration Manager que for atual no momento em que a licença expirar.
- Para informações sobre o Software Assurance e os requisitos de licença para o System Center Configuration Manager, confira [System Center Configuration Manager licensing and branches](learn-more-editions.md) (Branches e licenciamento do System Center Configuration Manager).
-   Para informações sobre as diferenças entre os diferentes branches, confira [Qual branch do Configuration Manager devo usar](which-branch-should-i-use.md).

Para instalar um novo site ou atualizar de um site do System Center 2012 Configuration Manager com suporte para o LTSB, você deve usar a mídia de linha de base da versão 1606. Essa mídia de linha de base está disponível em DVD como parte da versão do Microsoft System Center 2016 ou do System Center Configuration Manager (Branch Atual e Branch de Manutenção em Longo Prazo 1606). A mídia de linha de base que pode instalar o LTSB também pode ser usada para instalar a versão 1606 do Branch Atual do Configuration Manager. Para saber mais sobre a mídia de linha de base, confira [Baseline and update versions](/sccm/core/servers/manage/updates#baseline-and-update-versions) (Versões de linha de base e atualização).

Para obter informações sobre como instalar um site do LTSB, confira [Instalação e atualização para o Branch de Manutenção em Longo Prazo](install-the-ltsb.md). Confira a [documentação do System Center 2016](https:\technet.microsoft.com\system-center-docs\System-Center-2016) para encontrar informações sobre como obter o System Center 2016.

> [!IMPORTANT]
> Todos os sites em uma hierarquia devem executar o mesmo branch. Não há suporte para ter uma hierarquia com uma combinação do LTSB e do Branch Atual em sites diferentes.
>
> Da mesma forma, quando você usar a recuperação, precisará restaurar o site ou o banco de dados do site para seu branch original. Não é possível recuperar um banco de dados do site do Branch Atual para uma instalação do LTSB ou vice-versa.


## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Recursos que não estão disponíveis no LTSB do Configuration Manager
Em comparação com o Branch Atual, o LTSB tem as seguintes limitações de suporte:

- Não recebe atualizações para novos recursos
- Não dá suporte à adição de uma Assinatura do Microsoft Intune, o que impede o uso do:
  - Intune em uma configuração de MDM (Gerenciamento de Dispositivo Móvel) híbrido
  - MDM local
-   Não dá suporte ao uso do Painel de Serviço do Windows 10, Planos de Serviço e não dá suporte ao CB (Branch Atual) e ao CBB (Branch Atual para Negócios) do Windows 10
- Não dá suporte a versões futuras do Windows 10 LTSB e do Windows Server
-   Não dá suporte ao Asset Intelligence
-   Não dá suporte aos pontos de distribuição baseados em nuvem
-   Não dá suporte ao Suporte para o Exchange Online como um Exchange Connector
-   Não dá suporte a nenhum recurso de pré-lançamento


Embora o suporte para esses recursos não esteja incluído no LTSB, alguns recursos permanecem visíveis no console do Configuration Manager, mas não podem ser selecionados ou usados.

Além disso, os novos sistemas operacionais que são adicionados como com suporte pelo Branch Atual não terão suporte pelo LTSB.

## <a name="documentation-for-the-ltsb"></a>Documentação para o LTSB
Como o LTSB é baseado no Current Branch versão 1606, a documentação usada para o LTSB é a [documentação online que se aplica ao Branch Atual](https://docs.microsoft.com/sccm/), com as advertências e limitações que são específicas para o LTSB conforme identificado nos tópicos a seguir:  

-   [Introdução ao Branch de Manutenção em Longo Prazo](introduction-to-the-ltsb.md): (esse tópico).

-   [Qual branch do Configuration Manager devo usar](which-branch-should-i-use.md): informações sobre os diferentes branches do System Center Configuration Manager para que você possa se certificar de instalar o melhor branch para suas necessidades.

-   [Instalar o Branch de Manutenção em Longo Prazo](install-the-ltsb.md): como instalar um novo site do LTSB ou atualizar um site do System Center 2012 Configuration Manager para o LTSB.

-   [Atualizar o Branch de Manutenção em Longo Prazo para o Branch Atual](convert-to-current-branch.md): como converter sua instalação do LTSB para uma instalação do Branch Atual.

-   [Licenciamento e branches do System Center Configuration Manager](learn-more-editions.md): informações sobre o Software Assurance e o requisito de licença relacionados para o System Center Configuration Manager.
-   [Configurações com suporte para o Branch de Manutenção em Longo Prazo](supported-configurations-for-ltsb.md): as versões e os requisitos de sistema operacional e produtos dependentes como o SQL Server que você pode usar com o LTSB.


Para ajudá-lo a distinguir a qual branch a documentação específica se aplica, use o seguinte guia:  
-   Tópicos com um cabeçalho de *Aplica-se a: Branch Atual* se aplicam ao Branch Atual e ao Branch de Manutenção em Longo Prazo (embora partes do tópico possam se aplicar apenas a uma versão mais nova do Branch Atual).

-   Para identificar partes de um tópico que não se aplicam ao LTSB, os recursos e as alterações que foram introduzidos após a versão 1606 do Branch Atual são identificados com um texto como *A partir da versão 1610*. Como eles foram introduzidos após a versão 1606 do Branch Atual, eles não estão disponíveis com o LTSB.

### <a name="similarities-between-the-current-branch-and-the-ltsb"></a>Semelhanças entre o Branch Atual e o LTSB
Como o LTSB é baseado na versão 1606 do Branch Atual (com algumas exceções, como a integração do Intune e os recursos relacionados à nuvem), a maioria das tarefas de implantação de planejamento, configuração e gerenciamento dos dois branches é idêntica.

Por exemplo, o LTSB dá suporte ao mesmo número de sites, tipos de site, clientes e infraestrutura geral que o Branch Atual. Portanto, você pode usar as diretrizes encontradas nos tópicos sobre design e planejamento de hierarquia e site para o Branch Atual. Da mesma forma, para recursos com suporte pelos dois branches, como Atualizações de Software ou Implantação de Sistema Operacional, use as diretrizes encontradas nas seções da documentação do Branch Atual com as advertências sobre não ter acesso às alterações introduzidas após a versão 1606 do Branch Atual.


## <a name="how-to-identify-your-branch-and-version"></a>Como identificar seu branch e sua versão
Ao exibir as informações da versão de um site do Configuration Manager, também confirma o branch.

Para verificar a versão do site, no console, acesse **Sobre o System Center Configuration Manager** no canto superior esquerdo do console em que a **Versão do site** é exibida como **5.0.8412.1000**.

Para confirmar o branch do seu site (como LTSB ou Branch Atual), no console, acesse **Administração** > **Configuração do Site** > **Sites** e abra **Configurações da Hierarquia**.  Se houver uma opção para converter para o Branch Atual e ela estiver ativa, o site executará a versão LTSB. Quando o site executa o Branch Atual, essa opção fica esmaecida.

Para obter informações sobre as diferentes versões do Configuration Manager, consulte “Versões de linha de base e atualização” no tópico [Atualizações para o Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="exceptions-for-using-the-ltsb"></a>Exceções para o uso do LTSB
### <a name="updates-and-servicing-of-the-ltsb"></a>Atualizações e manutenção do LTSB
Somente as atualizações de segurança críticas são disponibilizadas como atualizações no console no LTSB.

As informações sobre as atualizações regulares para as versões subsequentes do Branch Atual estão visíveis nesse console, mas não estão disponíveis no LTSB. Elas não são baixadas e não podem ser instaladas.

Para dar suporte às atualizações no console para as correções de segurança críticas, um site do LTSB requer o uso do [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point). É possível configurar essa função de sistema de sites no modo offline ou online, como é feito para o Branch Atual. O LTSB coleta e envia os mesmos dados de telemetria e uso que o Branch Atual.

O LTSB dá suporte ao uso da ferramenta de Registro de Atualização e Instalador de Hotfix, como documentado para o Branch Atual.

Para obter informações gerais sobre atualizações e manutenção, confira [Updates for System Center Configuration Manager](/sccm/core/servers/manage/updates) (Atualizações para o System Center Configuration Manager).

### <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Alterações para a expansão de site e para a pasta CD.Latest
Quando você executa o LTSB e está expandindo um site primário autônomo instalando um novo site de administração central, deve usar a Instalação e os arquivos de origem da mídia de linha de base da versão 1606.  Para o Branch Atual, você executa a Instalação e usa os arquivos de origem da pasta CD.Latest.

Embora você não execute a Instalação para a expansão do site da pasta CD.Latest, você continua a usar a pasta CD.Latest para a recuperação de site e para instalar um novo site primário filho quando seu primeiro site do LTSB era um site de administração central.

Para mais informações, confira [Expandir um site primário autônomo](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site) em [Usar o Assistente de Instalação para instalar sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).
Para mais informações sobre a pasta CD.Latest, confira [The CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder) (A pasta CD.Latest).



<!--HONumber=Jan17_HO2-->


