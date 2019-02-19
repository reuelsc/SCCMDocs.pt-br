---
title: Preparar os Windows Servers
titleSuffix: Configuration Manager
description: Verifique se um computador atende aos pré-requisitos para uso como um servidor do site ou um servidor de sistema de sites para o Configuration Manager.
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1e794ff161f193f76fc899ab35acb1d29afdf606
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120327"
---
# <a name="prepare-windows-servers-to-support-configuration-manager"></a>Preparar servidores Windows para dar suporte ao Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de você usar um computador Windows como servidor de sistema de sites para o Configuration Manager, o computador deve atender aos pré-requisitos para o uso pretendido como servidor de site ou servidor de sistema de sites.  

- Esses pré-requisitos geralmente incluem um ou mais recursos ou funções do Windows, habilitados usando o Gerenciador do Servidor dos computadores.  

- Já que o método para permitir que funções e recursos do Windows é diferente entre as versões dos SOs, veja a documentação da sua versão do SO para obter informações detalhadas sobre como configurar o SO que você usa.  

As informações neste artigo fornecem uma visão geral dos tipos de configurações do Windows que são necessárias para dar suporte a sistemas de sites do Configuration Manager. Para obter detalhes de configuração para funções específicas do sistema de sites, confira [Pré-requisitos de site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

##  <a name="BKMK_WinFeatures"></a> Recursos e funções do Windows  
Ao configurar funções e recursos do Windows em um computador, pode ser necessário reiniciar o computador para concluir a configuração. Portanto, é uma boa ideia identificar computadores que hospedarão funções do sistema de site específicas antes de instalar um site do Configuration Manager ou servidor de sistema de site.

### <a name="features"></a>Recursos  
Os recursos do Windows a seguir são necessários em determinados servidores de sistema de sites e devem ser configurados antes de instalar uma função de sistema de sites no computador.  

- **.NET Framework**: Incluindo  

    - ASP.NET  
    - Ativação HTTP  
    - Ativação não HTTP  
    - Serviços do WCF (Windows Communication Foundation)  

    As funções do sistema de site diferentes exigem versões diferentes do .NET Framework.  

    Já que o .NET Framework 4.0 e posteriores não são compatíveis para substituir as versões 3.5 e anteriores, quando diferentes versões são listadas como necessárias, é preciso planejar para habilitar cada versão no mesmo computador.  

- **BITS (Serviço de Transferência Inteligente em Segundo Plano)**: Os pontos de gerenciamento exigem o BITS (e as opções selecionadas automaticamente) para dar suporte à comunicação com dispositivos gerenciados.  

- **BranchCache**: Os pontos de distribuição podem ser configurados com o BranchCache para dar suporte a clientes que usam o BranchCache.  

- **Eliminação de duplicação de dados**: Os pontos de distribuição podem ser configurados com a eliminação de duplicação de dados e se beneficiar desse recurso.  

- **RDC (Compactação Diferencial Remota)**: Cada computador que hospeda um servidor do site ou um ponto de distribuição requer a RDC. A RDC é usada para gerar assinaturas de pacote e fazer comparações de assinatura.  

### <a name="roles"></a>Funções  
As seguintes funções do Windows são necessárias para dar suporte a funcionalidades específicas, como atualizações de software e implantações de SO, enquanto o IIS é necessário para as funções mais comuns do sistema de sites.  

- **Serviço de Registro de Dispositivo de Rede** (em Serviços de Certificados do Active Directory): Essa função do Windows é um pré-requisito para usar perfis de certificado no Configuration Manager.  

- **Servidor Web (IIS)**: Incluindo:  
    - Recursos comuns de HTTP  
          - Redirecionamento de HTTP  
    - Desenvolvimento de aplicativos  
          - Extensibilidade .NET  
          - ASP.NET  
          - Extensões ISAPI  
          - Filtros ISAPI  
    - Ferramentas de gerenciamento  
          - Compatibilidade de gerenciamento do IIS 6  
          - Compatibilidade de Metabase do IIS 6  
          - Compatibilidade do WMI (Instrumentação de Gerenciamento do Windows) do IIS 6  
    - Segurança  
          - Filtragem de Solicitações  
          - Autenticação do Windows  

  As seguintes funções de sistema de sites usam uma ou mais das configurações do IIS listadas:  
  - Ponto de serviços Web do Catálogo de Aplicativos  
  - Ponto de sites da Web do Catálogo de Aplicativos  
  - Ponto de distribuição  
  - Ponto de registro  
  - Ponto proxy do registro  
  - Ponto de status de fallback  
  - Ponto de gerenciamento  
  - Ponto de atualização de software  
  - Ponto de migração de estado     

  A versão mínima do IIS necessária é a versão fornecida com o SO do servidor do site.  

  Além dessas configurações do IIS, você talvez precise configurar [Filtragem de Solicitações do IIS para pontos de distribuição](#BKMK_IISFiltering).  

- **Serviços de Implantação do Windows**: Essa função é usada com a implantação do SO.  

- **Windows Server Update Services**: Essa função é necessária para atualizações de software.  


##  <a name="BKMK_IISFiltering"></a> Filtragem de solicitações do IIS para pontos de distribuição  
Por padrão, o IIS usa a filtragem de solicitações para bloquear o acesso de várias extensões de nome de arquivo e de locais de pasta por comunicação HTTP ou HTTPS. Em um ponto de distribuição, isso impede que os clientes baixem os pacotes que têm extensões ou locais de pasta bloqueados.  

Quando os arquivos de origem do pacote têm extensões bloqueadas no IIS pela sua configuração de filtragem de solicitações, é necessário configurar a filtragem de solicitações para permiti-las. Isso é feito [editando o recurso de filtragem de solicitações](https://technet.microsoft.com/library/hh831621.aspx) no Gerenciador do IIS nos computadores do ponto de distribuição.  

Além disso, as seguintes extensões de nome de arquivo são usadas pelo Configuration Manager para pacotes e aplicativos. Verifique se suas configurações da filtragem de solicitações não bloqueiam estas extensões de arquivo:  

- .PCK  
- .PKG  
- .STA  
- .TAR  

Por exemplo, arquivos de origem para uma implantação de software podem incluir uma pasta chamada **bin** ou ter um arquivo com a extensão de nome de arquivo **.mdb**.  

- Por padrão, a filtragem de solicitações do IIS bloqueia o acesso a esses elementos (**bin** é bloqueado como um segmento oculto e **.mdb** é bloqueado como uma extensão de nome de arquivo).  

- Quando você usa a configuração padrão do IIS em um ponto de distribuição, os clientes que usam BITS falham ao baixar essa implantação de software do ponto de distribuição e indicam que estão aguardando conteúdo.  

- Para permitir que os clientes baixem esse conteúdo, em cada ponto de distribuição aplicável, edite **Filtragem de Solicitações** no Gerenciador do IIS para permitir o acesso a extensões de arquivos e pastas que estão em pacotes e aplicativos que você implanta.  

> [!IMPORTANT]  
> As edições feitas no filtro de solicitações podem aumentar a superfície de ataque do computador.  
> 
> - As edições feitas no nível do servidor aplicam-se a todos os sites no servidor.   
>     - As edições feitas em sites individuais aplicam-se apenas ao site.  
> 
> A prática recomendada de segurança é executar o Configuration Manager em um servidor Web dedicado. Se precisar executar outros aplicativos no servidor Web, use um site da Web personalizado para o Configuration Manager. Para obter informações, confira [Sites para servidores de sistema de sites](/sccm/core/plan-design/network/websites-for-site-system-servers).  

## <a name="http-verbs"></a>Verbos HTTP
**Pontos de gerenciamento:** Para garantir que os clientes possam se comunicar com êxito com um ponto de gerenciamento, no servidor de ponto de gerenciamento, verifique se os seguintes verbos HTTP são permitidos:  
- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

**Pontos de distribuição:** Pontos de distribuição requerem os seguintes verbos HTTP como permitidos:
- GET
- HEAD
- PROPFIND

Para obter mais informações, confira [Configurar a solicitação de filtragem em IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs). 
