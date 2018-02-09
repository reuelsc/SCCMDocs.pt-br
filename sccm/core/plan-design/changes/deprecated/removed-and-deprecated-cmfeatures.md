---
title: Preterido para recursos do Configuration Manager
titleSuffix: Configuration Manager
description: "Saiba mais sobre os recursos que não são mais compatíveis com o System Center Configuration Manager."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: d49e0f839106af652f7b49227b6c4f8c957347d9
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Recursos removidos e preteridos do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo descreve os recursos que foram removidos do suporte do System Center Configuration Manager ou que serão removidos em uma atualização futura (preteridos). O artigo oferece um aviso antecipado das futuras alterações que poderão afetar o uso do Configuration Manager.  

Essas informações estão sujeitas a alterações em versões futuras e podem não incluir cada recurso preterido do Configuration Manager.

## <a name="deprecated-features"></a>Recursos preteridos  

|**Recurso**|**Substituição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|Com a chegada da nova experiência do Centro de Software na versão 1511, os aplicativos que só eram exibidos no Catálogo de Aplicativos (aplicativos disponíveis para o usuário) agora aparecem no Centro de Software. </br></br>Com a inclusão dessa funcionalidade principal do Catálogo de Aplicativos no Centro de Software, a experiência de Catálogo de Aplicativos baseada na Web não estará mais disponível nos próximos meses.|11 de agosto de 2017| O suporte para a experiência de usuário do site do Catálogo de Aplicativos termina com a primeira atualização liberada após 1º de junho de 2018|
|O Centro de Software traz uma aparência nova e moderna. Nos próximos meses, a versão anterior do Centro de Software não estará mais disponível.<br><br>Você pode configurar clientes para usar o novo Centro de Software habilitando a configuração do cliente **Agente de Computador** > **Usar o novo Centro de Software**.<br><br>Para saber mais sobre o Software Center, consulte [Planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 de dezembro de 2016|O suporte para a versão anterior do Centro de Software terminará com a primeira atualização lançada após 1 de janeiro de 2018.|
|Gerenciamento de VHDs (discos de rígidos virtuais) com o Configuration Manager. </br></br>Isso inclui a remoção de opções para criar um novo VHD ou gerenciar um VHD usando uma sequência de tarefas, e a remoção do nó de discos rígidos virtuais no console do Configuration Manager. </br></br>Após a remoção desse suporte, os VHDs existentes não serão excluídos, mas deixarão de ser acessíveis de um console do Configuration Manager.  |6 de janeiro de 2017 |Versão 1710|
|Sequências de tarefas: <br /> – Converter Disco em Dinâmico <br /> – Instalar Ferramentas de Implantação |18 de novembro de 2016|Versão 1710|
|Ferramenta de avaliação de atualização do System Center Configuration Manager. </br></br>A Ferramenta de Avaliação de Atualização depende do System Center Configuration Manager e do Application Compatibility Toolkit (ACT) 6.x. A versão final do ACT foi entregue no Windows 10 v1511 ADK. Como não haverá atualizações adicionais para o ACT, o suporte para a Ferramenta de Avaliação de Atualização será descontinuado. </br></br>A Ferramenta de Avaliação de Atualização foi substituída pelo recurso [Preparação para atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics). O aviso de substituição foi adicionado à [página de download para UAT](https://www.microsoft.com/download/details.aspx?id=37145) em 12 de setembro de 2016. | 12 de setembro 2016  | 11 de julho de 2017 |
|Sequências de tarefas: <br /> - OSDPreserveDriveLetter  <br /><br /> Durante uma implantação de sistema operacional, por padrão, a Instalação do Windows agora determina a melhor letra da unidade a ser usada (geralmente, C:). Se desejar especificar o uso de uma unidade diferente, mude o local na etapa da sequência de tarefas Aplicar Sistema Operacional. Acesse a configuração **Selecione o local onde deseja aplicar este sistema operacional**. Selecione **Letra da unidade lógica específica** e escolha a unidade que você deseja usar. |20 de junho de 2016 |Versão 1606 |
|NAP (Proteção de Acesso à Rede) ‑ Encontrada no System Center 2012 Configuration Manager|10 de julho de 2015|Versão 1511|  
|Gerenciamento Fora de Banda ‑ Conforme encontrado no System Center 2012 Configuration Manager|16 de outubro de 2015|Versão 1511|



<br></br>
Detalhes adicionais dos recursos removidos na versão 1511 da liberação do System Center Configuration Manager:

###  <a name="bkmk_amt"></a> Gerenciamento fora da banda  
 Com o Configuration Manager, o suporte nativo para computadores baseados em AMT de dentro do console do Configuration Manager foi removido.  

-   Os computadores baseados em AMT permanecem totalmente gerenciados quando você usa o [Complemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O uso do complemento fornece acesso aos recursos mais recentes para gerenciar o AMT e, ao mesmo tempo, remove as limitações introduzidas até que o Configuration Manager possa incorporar essas mudanças.  

-   O gerenciamento fora de banda no System Center 2012 Configuration Manager não é afetado por essa alteração.  

###  <a name="bkmk_nap"></a> Proteção de Acesso à Rede  
 O System Center Configuration Manager removeu o suporte para a Proteção de Acesso à Rede. O recurso foi preterido no Windows Server 2012 R2 e removido do Windows 10.  

 Para alternativas de proteção de acesso à rede, consulte a seção *Funcionalidade preterida* de [Visão Geral dos Serviços de Acesso e Política de Rede](https://technet.microsoft.com/library/hh831683.aspx).

## <a name="more-information"></a>Mais informações
Para obter mais informações, consulte:
 - [Removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - O site do [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle).
 - [Suporte para versões do branch atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).
