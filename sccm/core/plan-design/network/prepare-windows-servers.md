---
title: Preparar os Windows Servers
titleSuffix: Configuration Manager
description: "Verifique se um computador atende aos pré-requisitos para uso como um servidor do site ou um servidor de sistema de sites para o System Center Configuration Manager."
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: a55322868d45cf1d2b3004e21d641ca5299aa957
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="prepare-windows-servers-to-support-system-center-configuration-manager"></a>Preparar Servidores Windows para dar suporte ao System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de você usar um computador Windows como servidor de sistema de sites para o System Center Configuration Manager, o computador deve atender aos pré-requisitos para o uso pretendido como servidor de site ou servidor de sistema de sites.  

-   Esses pré-requisitos geralmente incluem um ou mais recursos ou funções do Windows, habilitados usando o Gerenciador do Servidor dos computadores.  

-   Como o método para permitir que funções e recursos do Windows é diferente entre os sistemas operacionais, confira a documentação do sistema operacional para obter informações detalhadas sobre como configurar o sistema operacional que você usa.  

As informações neste artigo fornecem uma visão geral dos tipos de configurações do Windows que são necessárias para dar suporte a sistemas de sites do Configuration Manager. Para obter detalhes de configuração para funções específicas do sistema de sites, confira [Pré-requisitos de site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

##  <a name="BKMK_WinFeatures"></a> Recursos e funções do Windows  
 Ao configurar funções e recursos do Windows em um computador, pode ser necessário reiniciar o computador para concluir a configuração. Portanto, é uma boa ideia identificar computadores que hospedarão funções do sistema de site específicas antes de instalar um site do Configuration Manager ou servidor de sistema de site.
### <a name="features"></a>Recursos  
 Os recursos do Windows a seguir são necessários em determinados servidores de sistema de sites e devem ser configurados antes de instalar uma função de sistema de sites no computador.  

-   **.NET Framework**: incluindo  

    -   ASP.NET  
    -   Ativação HTTP  
    -   Ativação não HTTP  
    -   Serviços do WCF (Windows Communication Foundation)  

    As funções do sistema de site diferentes exigem versões diferentes do .NET Framework.  

    Como o .NET Framework 4.0 e posteriores não são compatíveis para substituir as versões 3.5 e anteriores, quando diferentes versões são listadas como necessárias, é preciso planejar para habilitar cada versão no mesmo computador.  

-   **BITS (Serviço de Transferência Inteligente em Segundo Plano)**: os pontos de gerenciamento exigem o BITS (e as opções selecionadas automaticamente) para permitir a comunicação com dispositivos gerenciados.  

-   **BranchCache**: os pontos de distribuição podem ser configurados com o BranchCache para dar suporte a clientes que usam o BranchCache.  

-   **Eliminação de Duplicação de Dados**: os pontos de distribuição podem ser configurados com a eliminação de duplicação de dados e se beneficiar desse recurso.  

-   **RDC (Compactação Diferencial Remota)**: cada computador que hospeda um servidor de sites ou ponto de distribuição requer RDC.   
    A RDC é usada para gerar assinaturas de pacote e fazer comparações de assinatura.  

### <a name="roles"></a>Funções  
 as seguintes funções do Windows são necessárias para dar suporte a funcionalidades específicas, como atualizações de software e implantações de sistema operacional, enquanto o IIS é necessário para as funções mais comuns do sistema de sites.  

 -   **Serviço de Registro de Dispositivo de Rede** (em Serviços de Certificados do Active Directory): essa função do Windows é um pré-requisito para usar os Perfis de Certificado no Configuration Manager.  

 -   **Servidor Web (IIS)**: incluindo:  
    -   Recursos HTTP Comuns >  
        -   Redirecionamento de HTTP  
    -   Desenvolvimento de Aplicativos >  
        -   Extensibilidade .NET  
        -   ASP.NET  
        -   Extensões ISAPI  
        -   Filtros ISAPI  
    -   Ferramentas de Gerenciamento >  
        -   Compatibilidade de gerenciamento do IIS 6  
        -   Compatibilidade de Metabase do IIS 6  
        -   Compatibilidade do WMI (Instrumentação de Gerenciamento do Windows) do IIS 6  
    -   Segurança >  
        -   Filtragem de Solicitações  
        -   Autenticação do Windows  

 As seguintes funções de sistema de sites usam uma ou mais das configurações do IIS listadas:  
    -   Ponto de serviços Web do Catálogo de Aplicativos  
    -   Ponto de sites da Web do catálogo de aplicativos  
    -   Ponto de distribuição  
    -   Ponto de registro  
    -   Ponto proxy do registro  
    -   Ponto de status de fallback  
    -   Ponto de gerenciamento  
    -   Ponto de atualização de software  
    -   Ponto de migração de estado     

    A versão mínima do IIS necessária é a versão fornecida com o sistema operacional do servidor do site.  

    Além dessas configurações do IIS, você talvez precise configurar [Filtragem de Solicitações do IIS para pontos de distribuição](#BKMK_IISFiltering).  

-   **Serviços de Implantação do Windows**: essa função é usada com a Implantação de Sistema Operacional.  
-   **Windows Server Update Services**: essa função é necessária quando você implanta atualizações de software.  

##  <a name="BKMK_IISFiltering"></a> Filtragem de Solicitações do IIS para pontos de distribuição  
 Por padrão, o IIS usa a Filtragem de Solicitações para bloquear o acesso de várias extensões de nome de arquivo e de locais de pasta por comunicação HTTP ou HTTPS. Em um ponto de distribuição, isso impede que os clientes baixem os pacotes que têm extensões ou locais de pasta bloqueados.  

 Quando os arquivos de origem do pacote têm extensões bloqueadas no IIS pela sua configuração de Filtragem de Solicitações, é necessário configurar a Filtragem de Solicitações para permiti-las. Isso é feito [editando o recurso Filtragem de Solicitações](https://technet.microsoft.com/library/hh831621.aspx) no Gerenciador do IIS nos computadores do ponto de distribuição.  

 Além disso, as seguintes extensões de nome de arquivo são usadas pelo Configuration Manager para pacotes e aplicativos. Verifique se suas configurações da Filtragem de Solicitações não bloqueiam estas extensões de arquivo:  

-   .PCK  
-   .PKG  
-   .STA  
-   .TAR  

Por exemplo, arquivos de origem para uma implantação de software podem incluir uma pasta chamada **bin** ou ter um arquivo com a extensão de nome de arquivo **.mdb**.  

-   Por padrão, a Filtragem de Solicitações do IIS bloqueia o acesso a esses elementos (**bin** é bloqueado como um segmento oculto e **.mdb** é bloqueado como uma extensão de nome de arquivo).  

-   Quando você usa a configuração padrão do IIS em um ponto de distribuição, os clientes que usam BITS falham ao baixar essa implantação de software do ponto de distribuição e indicam que estão aguardando conteúdo.  

-   Para permitir que os clientes baixem esse conteúdo, em cada ponto de distribuição aplicável, edite **Filtragem de Solicitações** no Gerenciador do IIS para permitir o acesso a extensões de arquivos e pastas que estão em pacotes e aplicativos que você implanta.  

> [!IMPORTANT]  
>  As edições feitas no Filtro de Solicitações podem aumentar a superfície de ataque do computador.  
>   
>  -   As edições feitas no nível do servidor aplicam-se a todos os sites no servidor.  
> -   As edições feitas em sites individuais aplicam-se apenas ao site.  
>   
>  A prática recomendada de segurança é executar o Configuration Manager em um servidor Web dedicado. Se precisar executar outros aplicativos no servidor Web, use um site da Web personalizado para o Configuration Manager. Para obter informações, consulte [Sites para servidores de sistema de sites no System Center Configuration Manager](../../../core/plan-design/network/websites-for-site-system-servers.md).  

## <a name="http-verbs"></a>Verbos HTTP
**Pontos de gerenciamento:** para garantir que os clientes possam se comunicar com êxito com um ponto de gerenciamento, no servidor de ponto de gerenciamento, verifique se os seguintes verbos HTTP são permitidos:  
 - GET
 - POST
 - CCM_POST
 - HEAD
 - PROPFIND

**Pontos de distribuição:** pontos de distribuição requerem os seguintes verbos HTTP como permitidos:
 - GET
 - HEAD
 - PROPFIND

Para saber mais sobre como configurar a filtragem de solicitações, confira [Configurar filtragem de solicitações no IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs) no TechNet ou a documentação semelhante que se aplica à versão do Windows Server que hospeda o ponto de gerenciamento.
