---
title: Recursos preteridos | Microsoft Docs
description: "Saiba mais sobre os recursos, produtos e sistemas operacionais aos quais o System Center Configuration Manager não dá mais suporte."
ms.custom: na
ms.date: 12/29/2016
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
ms.sourcegitcommit: 16781e281676c8c1092108d16beaf7e0b16d45a7
ms.openlocfilehash: e788a3c54e3620db92f1cc3e8246e5469189a802


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

## <a name="deprecated-features"></a>Recursos preteridos  

|**Recurso**|**Substituição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|NAP (Proteção de Acesso à Rede) ‑ Encontrada no System Center 2012 Configuration Manager|10 de julho de 2015|Versão 1511|  
|Gerenciamento Fora de Banda ‑ Conforme encontrado no System Center 2012 Configuration Manager|16 de outubro de 2015|Versão 1511|
|Sequências de tarefas: <br /> – Converter Disco em Dinâmico <br /> – Instalar Ferramentas de Implantação |18 de novembro de 2016|O suporte para essas sequências de tarefas termina com a primeira atualização liberada após 1º de junho de 2017.|
|O Centro de Software tem uma aparência nova e moderna. Os aplicativos que apareciam somente no Catálogo de Aplicativos dependente do Silverlight (aplicativos disponíveis para o usuário) agora aparecem no Centro de Software, na guia **Aplicativos**. O Catálogo de Aplicativos ainda pode ser acessado usando o link na guia **Status da Instalação** do Centro de Software.<br><br>Nos próximos meses, a versão anterior do Centro de Software não estará mais disponível.<br><br>Você pode configurar clientes para usar o novo Centro de Software habilitando a configuração do cliente **Agente de Computador** > **Usar o novo Centro de Software**.<br><br>Para saber mais sobre o Software Center, consulte [Planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 de dezembro de 2016|A ser anunciado|


Detalhes adicionais dos recursos removidos na versão 1511 da liberação do System Center Configuration Manager:

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a> Gerenciamento fora da banda  
 Com o Configuration Manager, o suporte nativo para computadores baseados em AMT de dentro do console do Configuration Manager foi removido.  

-   Os computadores baseados em AMT permanecem totalmente gerenciados quando você usa o [Complemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O uso do complemento fornece acesso aos recursos mais recentes para gerenciar o AMT e, ao mesmo tempo, remove as limitações introduzidas até que o Configuration Manager possa incorporar essas mudanças.  

-   O gerenciamento fora de banda no System Center 2012 Configuration Manager não é afetado por essa alteração.  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a> Proteção de Acesso à Rede  
 O System Center Configuration Manager removeu o suporte para a Proteção de Acesso à Rede. O recurso foi preterido no Windows Server 2012 R2 e removido do Windows 10.  

 Para alternativas de proteção de acesso à rede, consulte a seção *Funcionalidade preterida* de [Visão Geral dos Serviços de Acesso e Política de Rede](https://technet.microsoft.com/library/hh831683.aspx).  


## <a name="deprecated-operating-systems"></a>Sistemas operacionais preteridos
### <a name="server-operating-systems"></a>Sistemas operacionais do servidor  

|**Sistemas operacionais**|**Substituição anunciada pela primeira vez**|**Suporte removido** |  
|-|-|-|  
|Windows Server 2008|10 de julho de 2015|O suporte termina com a primeira atualização liberada após 31 de dezembro de 2016 (veja a observação 1).|  
|Windows Server 2008 R2|10 de julho de 2015|O suporte termina com a primeira atualização liberada após 31 de dezembro de 2016 (veja a observação 2).|  

-   Observação 1: após o término do suporte, esse sistema operacional não dará mais suporte a servidores do site ou à maioria das funções do sistema de sites. No entanto, ele permanecerá com suporte para a função do sistema de sites de ponto de distribuição (incluindo ponto de distribuição pull) até o anúncio de que esse suporte será preterido ou a expiração do período de suporte estendido desse sistema operacional.  

-   Observação 2: após o término do suporte, esse sistema operacional não dará mais suporte a servidores do site ou à maioria das funções do sistema de sites. No entanto, ele permanecerá com suporte para a função de sistema de sites de ponto de migração de estado e de ponto de distribuição (incluindo pontos de distribuição pull e para PXE e multicast) até o anúncio de que esse suporte será preterido ou a expiração do período de suporte estendido desse sistema operacional. Da versão 1602 em diante, você pode atualizar in-loco o sistema operacional de um servidor do site do Windows Server 2008 R2 para o Windows Server 2012 R2.  

     Para obter mais informações sobre a atualização in-loco do sistema de operacional de servidores de site, consulte a seção [Atualização in-loco do sistema operacional dos servidores do site que executam o Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) em [O que mudou no System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



### <a name="client-operating-systems"></a>Sistemas operacionais do cliente  

 A menos que seja indicado de outra forma, cada sistema operacional com suporte como um cliente do Configuration Manager terá suporte até a data de término do suporte estendido do sistema operacional. Para obter detalhes sobre as datas de término do suporte estendido, consulte o [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle). Se o suporte do Configuration Manager para um sistema operacional terminar antes da Data de término do suporte estendido, uma data de substituição e uma data de remoção do suporte para o sistema operacional serão listadas aqui.  

|**Sistemas operacionais**|**Substituição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|Windows XP|10 de julho de 2015|Versão 1511|  
|Windows XP Embedded|10 de julho de 2015|O suporte termina com a primeira atualização liberada após 31 de dezembro de 2016.|  
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
|SQL Server 2008 R2|10 de julho de 2015|O suporte termina com a primeira atualização liberada após 31 de dezembro de 2016.|  




<!--HONumber=Dec16_HO5-->

