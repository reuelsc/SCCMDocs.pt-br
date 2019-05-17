---
title: Referência da instalação
titleSuffix: Configuration Manager
description: Examine essa referência para ajudar você a se preparar para instalar um site ou hierarquia do Configuration Manager.
ms.date: 4/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f602bc42d007fa5780f4a8bc3971aa0ad41abfb9
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501312"
---
# <a name="reference-for-system-center-configuration-manager-setup"></a>Referência da instalação do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A Instalação do System Center Configuration Manager fornece links para vários tópicos, que estão detalhados nas seções a seguir. As informações nas seções a seguir podem ajudá-lo a preparar a instalação de um site ou hierarquia do Configuration Manager e a preparar para algumas das decisões que é necessário tomar durante a instalação.  


##  <a name="bkmk_start"></a> Antes de começar  
Antes de instalar novos sites do Configuration Manager, não deixe de ler as informações a seguir, que podem ajudar a preparar o terreno para um projeto de implantação bem-sucedido:  

-   [Conceitos básicos do System Center Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Planejar a infraestrutura do System Center Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Preparar para instalar sites do System Center Configuration Manager](prepare-to-install-sites.md)  

##  <a name="bkmk_assess"></a> Avaliar a preparação do servidor  
Antes de iniciar a instalação de um novo site, certifique-se de que o servidor de sites e os servidores de sistema de sites remoto que você planeja usar para o site (como o servidor que hospeda o banco de dados do site) atendem a todas as configurações de pré-requisitos. Os seguintes tópicos da biblioteca de documentação podem ajudar:  

-   [Configurações com suporte para o System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Verificador de Pré-requisitos](prerequisite-checker.md)  

##  <a name="bkmk_Addclients"></a> Clientes para sistemas operacionais adicionais  
É possível baixar o software cliente do Configuration Manager no Centro de Download da Microsoft para os seguintes sistemas operacionais:  

-   Mac (Apple)  
-   UNIX  
-   Linux  

Use os seguintes links para baixar clientes com a versão do Configuration Manager que você usa:  

-   Veja [Microsoft System Center Configuration Manager – Clientes para Sistemas Operacionais Adicionais](http://www.microsoft.com/download/details.aspx?id=47719)  

##  <a name="bkmk_usage"></a> Configurações e níveis de dados de uso  
Ao instalar seu primeiro site do System Center Configuration Manager, ele instala e configura automaticamente uma nova função do sistema de sites, o **ponto de conexão de serviço**, no servidor de sites. O ponto de conexão de serviço possui as seguintes configurações padrão:  

-   Modo **online** (também há suporte para o modo offline)  
-   Nível de coleção de dados **avançado** (há suporte para dois outros níveis de coleção de dados: Básico e Completo)  

Quando esta função estiver online, a Microsoft pode coletar automaticamente informações de diagnóstico e de uso pela Internet. Informações coletadas nos ajudam a:  

-   Identificar e solucionar problemas  
-   Melhorar nossos produtos e serviços  
-   Identificar atualizações para o Gerenciador de Configurações que se aplicam à versão do Gerenciador de Configurações que você usa  

### <a name="levels-of-data-collection"></a>Níveis de coleta de dados  
Os três níveis de coleção de dados são:

-   **Básico** inclui dados sobre a instalação e atualização, como o número de sites e quais recursos do Configuration Manager estão habilitados. Nenhuma informação de identificação pessoal será transmitida.  

-   **Avançado** inclui os dados da configuração Básica, dados de transmissão sobre a hierarquia, como cada recurso é usado (frequência e duração) e informações de diagnóstico avançadas, como o estado de memória do servidor quando ocorre uma falha de sistema ou do aplicativo. Nenhum dado de identificação pessoal será transmitido.  

-   **Completo** inclui os dados das configurações Básica e Avançada e também envia informações de diagnóstico avançadas, como arquivos de sistema e instantâneos de memória. Essa opção pode incluir informações de identificação pessoal, mas elas não serão usadas para identificá-lo ou contatá-lo, nem para enviar publicidade para você.  

Para saber mais, incluindo a divulgação dos detalhes coletados por cada nível, veja [Dados de diagnóstico e de uso para o System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Para exibir a política de privacidade online do System Center Configuration Manager, vá para [http://go.microsoft.com/fwlink/?LinkID=626527](http://go.microsoft.com/fwlink/?LinkID=626527).
