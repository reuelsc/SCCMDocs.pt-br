---
title: "Referência da instalação | Microsoft Docs"
description: "Examine essa referência para ajudar você a se preparar para instalar um site ou hierarquia do Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: a1f13fcde27baf7d0245682292134f08c4f9f8e6


---
# <a name="reference-for-system-center-configuration-manager-setup"></a>Referência da instalação do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A Instalação do System Center Configuration Manager fornece links para vários tópicos, em que são detalhados nas seções a seguir. As informações nas seções a seguir podem ajudá-lo a preparar a instalação de um site ou hierarquia do Configuration Manager e a prepará-lo para algumas das decisões que é necessário tomar durante a instalação:  

-   [Antes de começar](#bkmk_start)  

-   [Avaliar a preparação do servidor](#bkmk_assess)  

-   [Clientes para sistemas operacionais adicionais](#bkmk_Addclients)  

-   [Dados de diagnóstico e de uso para o System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

##  <a name="a-namebkmkstarta-before-you-begin"></a><a name="bkmk_start"></a> Antes de começar  
 Antes de instalar novos sites do Configuration Manager, não deixe de ler as informações a seguir, que podem ajudar a preparar o terreno para um projeto de implantação bem-sucedido:  

-   [Conceitos básicos do System Center Configuration Manager](../../../../core/understand/fundamentals.md)  

-   [Planejar a infraestrutura do System Center Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md)  

-   [Preparar para instalar sites do System Center Configuration Manager](prepare-to-install-sites.md)  

##  <a name="a-namebkmkassessa-assess-server-readiness"></a><a name="bkmk_assess"></a> Avaliar a preparação do servidor  
 Antes de iniciar a instalação de um novo site, certifique-se de que o servidor do site e os servidores de sistema de sites remoto que você planeja usar para o site (como o servidor que hospeda o banco de dados do site) atendem a todas as configurações de pré-requisito. Os seguintes tópicos da biblioteca de documentação podem ajudar:  

-   [Configurações com suporte para o System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  

-   [Verificador de Pré-requisitos](https://technet.microsoft.com/library/mt590813.aspx#bkmk_PreqChk)  

##  <a name="a-namebkmkaddclientsa-clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> Clientes para sistemas operacionais adicionais  
 É possível baixar o software cliente do Configuration Manager no Centro de Download da Microsoft para os seguintes sistemas operacionais:  

-   Mac (Apple)  

-   UNIX  

-   Linux  

**Use os seguintes links para baixar clientes com a versão do Configuration Manager utilizada:**  

-   [System Center Configuration Manager (branch atual)](http://www.microsoft.com/download/details.aspx?id=47719)  

-   [System Center 2012 R2 Configuration Manager SP1 e System Center 2012 Configuration Manager SP2](http://go.microsoft.com/fwlink/?LinkID=626550)  

-   [System Center 2012 R2 Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=316448)  

-   [System Center 2012 Configuration Manager SP1](http://www.microsoft.com/en-pk/download/details.aspx?id=36212)  

##  <a name="a-namebkmkusagea-usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Configurações e níveis de dados de uso  
Ao instalar seu primeiro site do System Center Configuration Manager, ele instala e configura automaticamente uma nova função do sistema de sites no servidor do site, o **ponto de conexão de serviço**, com as seguintes configurações padrão:  

-   Modo**online** (também há suporte para o modo offline)  

-   Um nível de coleção de dados de **Avançado** (há suporte para dois outros níveis de coleção de dados, Básico e Completo)  

Quando esta função estiver online, ela permite que a Microsoft colete automaticamente diagnóstico e informações de uso pela Internet. Informações coletadas nos ajudam a:  

-   Identificar e solucionar problemas  

-   Melhorar nossos produtos e serviços  

-   Identificar atualizações para o Gerenciador de Configurações que se aplicam à versão do Gerenciador de Configurações que você usa  

Os três níveis de coleção de dados incluem:  

-   **Básica** inclui dados sobre a instalação e atualização, como o número de sites e quais recursos do Configuration Manager estão habilitados. Nenhuma informação de identificação pessoal será transmitida.  

-   **Avançada** inclui os dados na configuração Básica, bem como dados de transmissão sobre a hierarquia, como cada recurso é usado (frequência e duração) e informações de diagnóstico avançadas, como o estado de memória do servidor quando ocorre uma falha de sistema ou do aplicativo. Nenhum dado de identificação pessoal será transmitido.  

-   **Completa** inclui os dados nas configurações Básica e Avançada e também envia informações de diagnóstico avançadas, como arquivos de sistema e instantâneos de memória. Essa opção pode incluir informações de identificação pessoal, mas elas não serão usadas para identificar ou contatá-lo nem para enviar publicidade para você.  

Para obter mais informações, incluindo a divulgação dos detalhes coletados por cada nível, veja [Dados de diagnóstico e de uso para o System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

[Política de Privacidade do System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527)



<!--HONumber=Dec16_HO3-->


