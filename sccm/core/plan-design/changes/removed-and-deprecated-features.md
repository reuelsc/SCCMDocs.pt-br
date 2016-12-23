---
title: Recursos preteridos | Microsoft Docs
description: "Saiba mais sobre os recursos, produtos e sistemas operacionais aos quais o System Center Configuration Manager não dá mais suporte."
ms.custom: na
ms.date: 12/05/2016
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
ms.sourcegitcommit: ffebee1e85008611a9841dc849bea735d15a88c6
ms.openlocfilehash: 888b6de9fd2b70e8b4f58e32cca7cf5e615d1dca


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Recursos removidos e preteridos do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico descreve os recursos, produtos e sistemas operacionais que foram removidos do suporte do System Center Configuration Manager ou que serão removidos em uma atualização futura (Preteridos). Isso serve para fornecer um aviso antecipado sobre futuras alterações que podem afetar o uso do Configuration Manager.  

 Essas informações estão sujeitas a alterações em versões futuras e podem não incluir cada recurso preterido, produto ou sistema operacional.  

## <a name="how-to-use-this-information"></a>Como usar essas informações  
Quando um recurso ou sistema operacional é listado em primeiro como preterido, o suporte para usá-lo com o Configuration Manager está programado para ser removido em uma versão futura do Configuration Manager. Essas informações são fornecidas para ajudá-lo no planejamento de alternativas para usar esse recurso ou sistema operacional.  Quando a primeira versão do Configuration Manager na qual o suporte foi removido for lançada, os detalhes deste tópico serão atualizados para indicar essa versão específica.  

Quando o suporte é removido de um recurso ou sistema operacional, o sistema operacional ou o recurso permanece com suporte quando você usa uma versão anterior do Configuration Manager, enquanto essa versão do Configuration Manager permanecer no suporte. No entanto, quando você usa uma versão do Configuration Manager lançada após a data ou versão indicada, essa versão do Configuration Manager não dá suporte.

**Por exemplo:** se um recurso foi agendado para ter seu suporte removido com a primeira atualização liberada após setembro de 2016, significa que o suporte para esse recurso não seria mais incluído na atualização 1610, lançada em outubro de 2016.
-  Com a atualização 1610, o recurso não teria mais suporte.
-  Este conteúdo será atualizado para indicar que o suporte foi removido com a versão 1610.
No entanto, se continuar a usar uma versão anterior que ofereça suporte ao recurso, como a versão 1602 ou 1606, você poderá usar esse recurso até que a versão que você usa fique sem suporte.

Para obter mais informações, consulte:
 - O site do [Ciclo de vida de suporte da Microsoft](https://support.microsoft.com/lifecycle)
 - [Suporte para versões atuais de branch do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)

**Recursos preteridos:**  


|**Recurso**|**Substituição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|NAP (Proteção de Acesso à Rede) ‑ Encontrada no System Center 2012 Configuration Manager|10/7/2015|Versão 1511|  
|Gerenciamento Fora de Banda ‑ Conforme encontrado no System Center 2012 Configuration Manager|16/10/2015|Versão 1511|
|Sequências de tarefas: <br /> – Converter Disco em Dinâmico <br /> – Instalar Ferramentas de Implantação |11/18/2016|O suporte para essas sequências de tarefas termina com a primeira atualização liberada após 1º de junho de 2017|
|O novo Software Center tem uma aparência nova e moderna, e os aplicativos que antes só eram exibidos no Catálogo de Aplicativos dependente do Silverlight (aplicativos disponíveis para o usuário) agora aparecem no Software Center sob a guia **Aplicativos**. O Catálogo de Aplicativos ainda pode ser acessado usando o link sob a guia **Status da Instalação** do Centro de Software.<br><br>Nos próximos meses, removeremos a versão anterior do Software Center e ela não estará mais disponível para uso.<br><br>É possível configurar clientes para usar o novo Centro de Software habilitando a configuração do cliente **Agente de Computador** > **Usar o novo Centro de Software**.<br><br>Para saber mais sobre o Software Center, consulte [Planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13/12/2016|A ser anunciado| 

 **Sistemas operacionais de servidor preteridos:**  

 |**Sistemas operacionais**|**Substituição anunciada pela primeira vez**|**Suporte removido** |  
|-|-|-|  
|Windows Server 2008|10/7/2015|O suporte termina com a primeira atualização liberada após 31/12/2016 *Veja a observação 1*|  
|Windows Server 2008 R2|10/7/2015|O suporte termina com a primeira atualização liberada após 31/12/2016 *Veja a observação 2*|  

-   *Observação 1*: após o término do suporte, esse sistema operacional não terá mais suporte a servidores do site ou à maioria das funções do sistema de sites. No entanto, ele permanecerá com suporte para a função do sistema de sites do ponto de distribuição (incluindo ponto de distribuição de recepção) até que a desaprovação desse suporte seja anunciada ou o período de suporte estendido deste sistema operacional expire.  

-   *Observação 2*: após o término do suporte, esse sistema operacional não terá mais suporte a servidores do site ou à maioria das funções do sistema de sites. No entanto, ele permanecerá com suporte para a função de sistema de sites de ponto de migração de estado e ponto de distribuição (incluindo pontos de distribuição de recepção, e para PXE e multi-cast) até que esse suporte seja preterido ou o período de suporte estendido deste sistema operacional expire.  A partir da versão 1602, você pode atualizar in-loco o sistema operacional de um servidor do site do Windows Server 2008 R2 para o Windows Server 2012 R2.  

     Para obter mais informações sobre a atualização in-loco do sistema de operacional de servidores de site, consulte a seção [Atualização in-loco do sistema operacional dos servidores do site que executam o Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) em [O que mudou no System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



 **Sistemas operacionais de cliente preteridos:**  

 A menos que seja indicado de outra forma, cada sistema operacional com suporte como um cliente do Configuration Manager terá suporte até a Data de término do suporte estendido do sistema operacional, conforme detalhado no [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle).  Se o suporte do Configuration Manager para um sistema operacional terminar antes da Data de término do suporte estendido, uma data de substituição e uma data de remoção do suporte para o sistema operacional serão listadas aqui.  

|**Sistemas operacionais**|**Substituição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|Windows XP|10/7/2015|Versão 1511|  
|Windows XP Embedded|10/7/2015|O suporte termina com a primeira atualização liberada após 31/12/2016|  
|Windows Server 2003|10/7/2015|Versão 1511|  
|Windows Server 2003 R2|10/7/2015|Versão 1511|  
|Windows Vista|10/7/2015|Versão 1511|  
|Mac OS X 10.6 a 10.8|10/7/2015|Versão 1511|  
|Windows Mobile 6.0 a 6.5|10/7/2015|Versão 1511|  
|Nokia Symbian Belle|10/7/2015|Versão 1511|  
|Windows CE 5.0 a 6.0|10/7/2015|Versão 1511|  


 **Suporte preterido para versões do SQL Server como um banco de dados do site:**  

|**Versões do SQL Server**|**Substituição anunciada pela primeira vez**|**Suporte removido**|   
|-|-|-|  
|SQL Server 2008|10/7/2015|Versão 1511|  
|SQL Server 2008 R2|10/7/2015|O suporte termina com a primeira atualização liberada após 31/12/2016|  

## <a name="features-removed-in-system-center-configuration-manager"></a>Recursos removidos do System Center Configuration Manager  
 A partir da versão inicial do System Center Configuration Manager, os seguintes recursos foram removidos:

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a> Gerenciamento fora da banda  
 Com o Configuration Manager, o suporte nativo para computadores baseados em AMT de dentro do console do Configuration Manager foi removido.  

-   Os computadores baseados em AMT permanecem totalmente gerenciados, quando você usa o [Complemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)  

-   O uso do Complemento fornece acesso aos recursos mais recentes para gerenciar o AMT, ao mesmo tempo que remove as limitações introduzidas até que o Configuration Manager possa incorporar essas alterações  

-   O Gerenciamento fora de banda no System Center 2012 Configuration Manager não é afetado por essa alteração  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a> Proteção de Acesso à Rede  
 O System Center Configuration Manager removeu o suporte para a Proteção de Acesso à Rede. O recurso foi preterido no Windows Server 2012 R2 e removido do Windows 10.  

 Para alternativas de proteção de acesso à rede, consulte a seção **Funcionalidade preterida** de [Visão Geral dos Serviços de Acesso e Política de Rede](https://technet.microsoft.com/library/hh831683.aspx).  



<!--HONumber=Dec16_HO3-->


