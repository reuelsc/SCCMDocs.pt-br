---
title: Recursos preteridos | Microsoft Docs
description: "Saiba mais sobre os recursos, produtos e sistemas operacionais aos quais o System Center Configuration Manager não dá mais suporte."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 57b9ab13bda0bb5fa5139e52a4c55ef9524e4097
ms.lasthandoff: 03/27/2017


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Recursos removidos e preteridos do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico descreve os recursos, os produtos e os sistemas operacionais que foram removidos do suporte do System Center Configuration Manager ou que serão removidos em uma atualização futura (preteridos). Trata-se de um aviso antecipado das futuras alterações que poderão afetar o uso do Configuration Manager.  

Essas informações estão sujeitas a alterações em versões futuras e podem não incluir todos os recursos, os produtos ou os sistemas operacionais preteridos.  

## <a name="how-to-use-this-information"></a>Como usar essas informações  
Quando um recurso ou sistema operacional é listado em primeiro como preterido, o suporte para usá-lo com o Configuration Manager está programado para ser removido em uma versão futura do Configuration Manager. Essas informações são fornecidas para ajudar você no planejamento de alternativas no uso desse recurso ou sistema operacional. Quando ocorrer a liberação da primeira versão do Configuration Manager na qual o suporte será removido, os detalhes deste tópico serão atualizados para indicar essa versão específica.  

Quando o suporte de um recurso ou sistema operacional for removido, o sistema operacional ou o recurso permanecerá com suporte ao usar uma versão anterior do Configuration Manager, desde que essa versão do Configuration Manager permaneça com suporte. No entanto, quando você usa uma versão do Configuration Manager lançada após a data ou versão indicada, essa versão do Configuration Manager não dá suporte.

Por exemplo, se um recurso fosse agendado para ter o suporte removido na primeira atualização liberada após setembro de 2016, o suporte para esse recurso não seria mais incluído na atualização 1610, a qual seria liberada em outubro de 2016.
-  Com a atualização 1610, o recurso não teria mais suporte.
-  Este tópico seria atualizado para indicar que o suporte havia sido removido com a versão 1610.
No entanto, se continuar a usar uma versão anterior que ofereça suporte ao recurso, como a versão 1602 ou 1606, você poderá usar esse recurso até que a versão que você usa fique sem suporte.

Para obter mais informações, consulte:
 - O site do [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle).
 - [Suporte para versões do branch atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).




## <a name="deprecated-operating-systems"></a>Sistemas operacionais preteridos
### <a name="server-operating-systems"></a>Sistemas operacionais do servidor  

|**Sistemas operacionais**|**Substituição anunciada pela primeira vez**|**Suporte removido** |  
|-|-|-|  
|Windows Server 2008|10 de julho de 2015|Versão 1511 </br></br>O suporte como um sistema de sites foi removido. (Consulte a observação 1).|  
|Windows Server 2008 R2|10 de julho de 2015| Versão 1702 (veja a observação 2)|  

-   Observação 1: não há suporte para esse sistema operacional para servidores do site ou funções do sistema de sites, com exceção do ponto de distribuição e do ponto de distribuição pull. Você pode continuar a usar esse sistema operacional como um ponto de distribuição até que a substituição desse suporte seja anunciada ou o período de suporte estendido do sistema operacional expire. Para obter mais informações, consulte [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (A instalação do CB e do LTSB do System Center Configuration Manager falha no Windows Server 2008).

-   Observação 2: a partir da versão 1702, esse sistema operacional não oferece suporte para servidores do site ou a maioria das funções de sistema de site; no entanto, as versões anteriores 1702 continuam a dar suporte ao seu uso. Este sistema operacional ainda terá suporte para a função de sistema de sites de ponto de migração de estado e de ponto de distribuição (incluindo pontos de distribuição pull e para PXE e multicast) até o anúncio de que esse suporte será preterido ou a expiração do período de suporte estendido desse sistema operacional. Da versão 1602 em diante, você pode atualizar in-loco o sistema operacional de um servidor do site do Windows Server 2008 R2 para o Windows Server 2012 R2.  

     Para obter mais informações sobre a atualização in-loco do sistema de operacional de servidores de site, consulte a seção [Atualização in-loco do sistema operacional dos servidores do site que executam o Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) em [O que mudou no System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



### <a name="client-operating-systems"></a>Sistemas operacionais do cliente  

 A menos que seja indicado de outra forma, cada sistema operacional com suporte como um cliente do Configuration Manager terá suporte até a data de término do suporte estendido do sistema operacional. Para obter detalhes sobre as datas de término do suporte estendido, consulte o [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle). Se o suporte do Configuration Manager para um sistema operacional terminar antes da Data de término do suporte estendido, uma data de substituição e uma data de remoção do suporte para o sistema operacional serão listadas aqui.  

|**Sistemas operacionais**|**Substituição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|Windows XP|10 de julho de 2015|Versão 1511|  
|Windows XP Embedded|10 de julho de 2015|Versão 1702|  
|Windows Server 2003|10 de julho de 2015|Versão 1511|  
|Windows Server 2003 R2|10 de julho de 2015|Versão 1511|  
|Windows Vista|10 de julho de 2015|Versão 1511|  
|Mac OS X 10.6 a 10.8|10 de julho de 2015|Versão 1511|  
|Windows Mobile 6.0 a 6.5|10 de julho de 2015|Versão 1511|  
|Nokia Symbian Belle|10 de julho de 2015|Versão 1511|  
|Windows CE 5.0 a 6.0|10 de julho de 2015|Versão 1511|  


## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Suporte preterido para versões do SQL Server como um banco de dados do site  

|**Versões do SQL Server**|**Substituição anunciada pela primeira vez**|**Suporte removido**|   
|-|-|-|  
|SQL Server 2008|10 de julho de 2015|Versão 1511|  
|SQL Server 2008 R2|10 de julho de 2015|Versão 1702|  

Se você precisa atualizar sua versão do SQL Server, recomendamos os seguintes métodos, do mais fácil para o mais complexo.
1. [Atualização do SQL Server no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).
2. Instale uma nova versão do SQL Server em um computador novo e, em seguida, [use a opção de mover o banco de dados](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) da instalação do Configuration Manager para apontar o servidor do site para o novo SQL Server.
3. Use [backup e recuperação](/sccm/protect/understand/backup-and-recovery).


## <a name="deprecated-features"></a>Recursos preteridos  

|**Recurso**|**Substituição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|NAP (Proteção de Acesso à Rede) ‑ Encontrada no System Center 2012 Configuration Manager|10 de julho de 2015|Versão 1511|  
|Gerenciamento Fora de Banda ‑ Conforme encontrado no System Center 2012 Configuration Manager|16 de outubro de 2015|Versão 1511|
|Sequências de tarefas: <br /> - OSDPreserveDriveLetter  <br /><br /> Durante uma implantação de sistema operacional, por padrão, a Instalação do Windows agora determina a melhor letra da unidade a ser usada (geralmente, C:). Se desejar especificar o uso de uma unidade diferente, mude o local na etapa da sequência de tarefas Aplicar Sistema Operacional. Vá para a configuração **Selecione o local onde deseja aplicar este sistema operacional**, selecione **Letra da unidade lógica específica** e escolha a unidade que deseja usar. |20 de junho de 2016 |Versão 1606 |
|Sequências de tarefas: <br /> – Converter Disco em Dinâmico <br /> – Instalar Ferramentas de Implantação |18 de novembro de 2016|O suporte para essas sequências de tarefas termina com a primeira atualização liberada após 1º de junho de 2017.|
|O Centro de Software tem uma aparência nova e moderna. Os aplicativos que apareciam somente no Catálogo de Aplicativos dependente do Silverlight (aplicativos disponíveis para o usuário) agora aparecem no Centro de Software, na guia **Aplicativos**. O Catálogo de Aplicativos ainda pode ser acessado usando o link na guia **Status da Instalação** do Centro de Software.<br><br>Nos próximos meses, a versão anterior do Centro de Software não estará mais disponível.<br><br>Você pode configurar clientes para usar o novo Centro de Software habilitando a configuração do cliente **Agente de Computador** > **Usar o novo Centro de Software**.<br><br>Para saber mais sobre o Software Center, consulte [Planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 de dezembro de 2016|A ser anunciado|
|Gerenciamento de VHDs (discos de rígidos virtuais) com o Configuration Manager. </br></br>Isso inclui a remoção de opções para criar um novo VHD ou gerenciar um VHD usando uma sequência de tarefas, e a remoção do nó de discos rígidos virtuais no console do Configuration Manager. </br></br>Após a remoção desse suporte, os VHDs existentes não serão excluídos, mas deixarão de ser acessíveis de um console do Configuration Manager.  |6 de janeiro de 2017 |O suporte para VHDs termina com a primeira atualização liberada após 1º de junho de 2017.|
|Ferramenta de avaliação de atualização do System Center Configuration Manager. </br></br>A Ferramenta de Avaliação de Atualização depende do System Center Configuration Manager e do Application Compatibility Toolkit (ACT) 6.x. A versão final do ACT foi entregue no Windows 10 v1511 ADK. Como não haverá atualizações adicionais para o ACT, o suporte para a Ferramenta de Avaliação de Atualização será descontinuado. </br></br>A Ferramenta de Avaliação de Atualização foi substituída pelo recurso [Preparação para atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics). O aviso de substituição foi adicionado à [página de download para UAT](https://www.microsoft.com/download/details.aspx?id=37145) em 12/09/2016. |12/09/2016  | 11 de julho de 2017 |  


<br></br>
Detalhes adicionais dos recursos removidos na versão 1511 da liberação do System Center Configuration Manager:

###  <a name="bkmk_amt"></a> Gerenciamento fora da banda  
 Com o Configuration Manager, o suporte nativo para computadores baseados em AMT de dentro do console do Configuration Manager foi removido.  

-   Os computadores baseados em AMT permanecem totalmente gerenciados quando você usa o [Complemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O uso do complemento fornece acesso aos recursos mais recentes para gerenciar o AMT e, ao mesmo tempo, remove as limitações introduzidas até que o Configuration Manager possa incorporar essas mudanças.  

-   O gerenciamento fora de banda no System Center 2012 Configuration Manager não é afetado por essa alteração.  

###  <a name="bkmk_nap"></a> Proteção de Acesso à Rede  
 O System Center Configuration Manager removeu o suporte para a Proteção de Acesso à Rede. O recurso foi preterido no Windows Server 2012 R2 e removido do Windows 10.  

 Para alternativas de proteção de acesso à rede, consulte a seção *Funcionalidade preterida* de [Visão Geral dos Serviços de Acesso e Política de Rede](https://technet.microsoft.com/library/hh831683.aspx).

