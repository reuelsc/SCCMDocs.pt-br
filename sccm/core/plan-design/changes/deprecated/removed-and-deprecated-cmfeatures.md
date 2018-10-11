---
title: Recursos preteridos
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos que não são mais compatíveis com o Configuration Manager.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dbebfa1ef5d4851cfd6bbc118c2d7bab30f0b01f
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893443"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Recursos removidos e preteridos do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo lista os recursos que foram preteridos ou removidos do suporte do Configuration Manager. Recursos preteridos serão removidos em uma atualização futura. Essas futuras alterações poderão afetar o uso do Configuration Manager.  

Essas informações estão sujeitas a alterações em versões futuras. Elas podem não incluir cada recurso preterido do Configuration Manager.



## <a name="deprecated-features"></a>Recursos preteridos  

|Recurso|Substituição anunciada pela primeira vez|Suporte&nbsp;removido|  
|-----------|---|--------------|  
|Gerenciamento híbrido de dispositivos móveis. Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->|14 de agosto de 2018|1º de setembro de 2019|
|Não há mais suporte para a **experiência do usuário do Silverlight** para o ponto do site do Catálogo de Aplicativos. Os usuários devem usar o novo Centro de Software. Observação: ainda há suporte para as funções de ponto de site do Catálogo de Aplicativos e de ponto de serviço Web. Em alguns cenários, o novo Centro de Software comunica-se com o ponto de site do Catálogo de Aplicativos. Para saber mais, veja [Configurar Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).<!--1358309-->|11 de agosto de 2017| Versão 1806|
|A versão anterior do Centro de Software.<br><br>Para saber mais sobre o novo Centro de Software, veja [Planejar e configurar o gerenciamento de aplicativos](/sccm/apps/plan-design/plan-for-and-configure-application-management##bkmk_userex).|13 de dezembro de 2016|Versão 1802|
|Gerenciamento de VHDs (discos de rígidos virtuais) com o Configuration Manager. </br></br>Essa reprovação inclui a remoção de opções para criar um novo VHD ou gerenciar um VHD usando uma sequência de tarefas, e a remoção do nó de discos rígidos virtuais no console do Configuration Manager. </br></br>VHDs existentes não são excluídos, mas não são mais acessíveis de dentro do console do Configuration Manager.  |6 de janeiro de 2017 |Versão 1710|
|Sequências de tarefas: <br /> – Converter Disco em Dinâmico <br /> – Instalar Ferramentas de Implantação |18 de novembro de 2016|Versão 1710|
|Ferramenta de avaliação de atualização do System Center Configuration Manager. </br></br>A Ferramenta de Avaliação de Atualização depende do System Center Configuration Manager e do Application Compatibility Toolkit (ACT) 6.x. A versão final do ACT foi entregue no Windows 10 v1511 ADK. Como não há atualizações adicionais para o ACT, o suporte para a Ferramenta de Avaliação de Atualização será descontinuado. </br></br>A Ferramenta de Avaliação de Atualização foi substituída pelo recurso [Preparação para atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics). O aviso de substituição foi adicionado à [página de download para UAT](https://www.microsoft.com/download/details.aspx?id=37145) em 12 de setembro de 2016. | 12 de setembro 2016  | 11 de julho de 2017 |
|Pontos de atualização de software com um cluster de NLB (balanceamento de carga de rede) | 27 de fevereiro de 2016 | Versão 1702 | 
|Sequências de tarefas: <br /> - OSDPreserveDriveLetter  <br /><br /> Durante uma implantação de sistema operacional, por padrão, a Instalação do Windows agora determina a melhor letra da unidade a ser usada (geralmente, C:). Se desejar especificar o uso de uma unidade diferente, mude o local na etapa da sequência de tarefas Aplicar Sistema Operacional. Acesse a configuração **Selecione o local onde deseja aplicar este sistema operacional**. Selecione **Letra da unidade lógica específica** e escolha a unidade que você deseja usar. |20 de junho de 2016 |Versão 1606 |
|NAP (Proteção de Acesso à Rede) ‑ Encontrada no System Center 2012 Configuration Manager|10 de julho de 2015|Versão 1511|  
|Gerenciamento Fora de Banda ‑ Conforme encontrado no System Center 2012 Configuration Manager|16 de outubro de 2015|Versão 1511|



## <a name="features-removed-in-version-1511"></a>Recursos removidos na versão 1511
As seções a seguir incluem detalhes adicionais para recursos removidos com a versão 1511:

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
 - [Ciclo de vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle)
 - [Suporte para versões do branch atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).
