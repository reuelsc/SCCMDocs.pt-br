---
title: Suporte para recursos do Windows
titleSuffix: Configuration Manager
description: Saiba a quais recursos de rede e do Windows o System Center Configuration Manager dá suporte.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c1b4dbb6986b5e617ae7a8eb2a0264ce799e87ca
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="support-for-windows-features-and-networks-in-system-center-configuration-manager"></a>Suporte para recursos do Windows e redes no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo identifica o suporte do Configuration Manager para recursos de rede e recursos comuns do Windows.  


##  <a name="bkmk_branchcache"></a> BranchCache  
Use o Windows BranchCache com o Configuration Manager ao habilitá-lo nos pontos de distribuição e configure os clientes para usá-lo no modo de cache distribuído.

É possível definir as configurações do BranchCache em um tipo de implantação de aplicativos, na implantação de um pacote e de sequência de tarefas.  

Quando todos os requisitos do BranchCache são atendidos, esse recurso permite que os clientes em locais remotos obtenham o conteúdo de clientes locais que têm um cache atual do conteúdo.  

Por exemplo, quando o primeiro cliente habilitado para BranchCache solicita o conteúdo de um ponto de distribuição configurado como um servidor do BranchCache, o cliente baixa e armazena o conteúdo em cache. Esse conteúdo é então disponibilizado para os clientes na mesma sub-rede que o solicitou.

Esses clientes também armazenam o conteúdo em cache. Os outros clientes na mesma sub-rede não precisam baixar o conteúdo do ponto de distribuição. O conteúdo é distribuído entre vários clientes para transferências futuras.  

### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Requisitos de suporte do BranchCache com o Configuration Manager
-   **Configurar pontos de distribuição**: adicione o recurso **Windows BranchCache** ao servidor do sistema de sites configurado como um ponto de distribuição.    
    -   Os pontos de distribuição nos servidores configurados para dar suporte ao BranchCache não exigem nenhuma configuração adicional.   
    -   Não é possível adicionar o Windows BranchCache a um ponto de distribuição baseado em nuvem. Os pontos de distribuição baseados em nuvem dão suporte ao download de conteúdo por clientes configurados para o Windows BranchCache.  

-   **Configurar clientes**:    
    -   Os clientes que oferecem suporte ao BranchCache devem ser configurados para o modo de cache distribuído do BranchCache.  
    -   A configuração do sistema operacional para as configurações do cliente BITS deve estar habilitada para dar suporte ao BranchCache.   <br /> <br />

    Para obter informações, consulte [Configurar clientes para o BranchCache](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache) na documentação do Windows.


### <a name="configuration-manager-supported-os-versions-with-windows-branchcache"></a>Versões de sistema operacional compatíveis com o Configuration Manager no Windows BranchCache

|Sistema operacional|Detalhes do suporte|  
|----------------------|---------------------|  
|Windows 7 com SP1|Com suporte por padrão|  
|Windows 8|Com suporte por padrão|  
|Windows 8.1|Com suporte por padrão|  
|Windows 10|Com suporte por padrão|  
|Windows Server 2008 com SP2|**Exige o BITS 4.0**: é possível instalar a versão BITS 4.0 em clientes do Configuration Manager usando as atualizações de software ou a distribuição de software. Para obter mais informações, consulte [Windows Management Framework](https://support.microsoft.com/help/968929/windows-management-framework-windows-powershell-2-0-winrm-2-0-and-bits).<br /><br /> Nesse sistema operacional, não há suporte para a funcionalidade de cliente do BranchCache para distribuição de software executada na rede ou para transferências de arquivos SMB. Além disso, esse sistema operacional não pode usar a funcionalidade do BranchCache com pontos de distribuição baseados em nuvem.|  
|Windows Server 2008 R2|Com suporte por padrão|  
|Windows Server 2012|Com suporte por padrão|  
|Windows Server 2012 R2|Com suporte por padrão|  
|Windows Server 2016|Com suporte por padrão|  

 Para obter mais informações, consulte [BranchCache para Windows](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) na documentação do Windows Server.  



##  <a name="bkmk_Workgroups"></a> Computadores em grupos de trabalho  
O Configuration Manager dá suporte a clientes em grupos de trabalho.  

-   O Configuration Manager dá suporte à movimentação de um cliente de um grupo de trabalho para um domínio ou de um domínio para um grupo de trabalho. Para obter mais informações, consulte [Como instalar clientes do Configuration Manager em computadores do grupo de trabalho](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup) no tópico [Como implantar clientes em computadores Windows](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

> [!NOTE]  
>  Embora haja suporte para clientes em grupos de trabalho, todos os sistemas de sites devem ser membros de um Domínio do Active Directory com suporte.  



##  <a name="bkmmk_datadedup"></a> Eliminação de duplicação de dados  
O Configuration Manager dá suporte ao uso da eliminação de duplicação de dados com pontos de distribuição nos seguintes sistemas operacionais:  

-   Windows Server 2016
-   Windows Server 2012 R2  
-   Windows Server 2012  


> [!IMPORTANT]  
>  O volume que hospeda os arquivos de origem do pacote não pode ser marcado para a eliminação de duplicação de dados. Essa limitação existe porque a eliminação de duplicação de dados usa pontos de nova análise. O Configuration Manager não dá suporte ao uso de um local de fonte de conteúdo com arquivos armazenados em pontos de nova análise.  

Para obter mais informações, consulte [Pontos de distribuição do Configuration Manager e eliminação de duplicação de dados do Windows Server 2012](https://cloudblogs.microsoft.com/enterprisemobility/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication/) no blog da equipe do Configuration Manager e [Visão geral de eliminação de duplicação de dados](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview) na documentação do Windows Server.  



##  <a name="bkmk_DA"></a> DirectAccess  
O Configuration Manager é compatível com o recurso DirectAccess para a comunicação entre clientes e sistemas de servidor do site.  

-   Quando todos os requisitos do DirectAccess são atendidos, ele permite que os clientes do Configuration Manager na Internet se comuniquem com seu site atribuído como se estivessem na intranet.  

-   Para ações iniciadas pelo servidor, como o controle remoto e a instalação do cliente por push, o computador de inicialização deve executar o IPv6. Esse protocolo deve ter suporte em todos os dispositivos de rede intermediários.  

O Configuration Manager não dá suporte às seguintes funcionalidades no DirectAccess:  

-   A implantação de sistemas operacionais  

-   Comunicação entre sites do Configuration Manager  

-   Comunicação entre servidores do sistema de sites do site do Configuration Manager em um site  



##  <a name="bkmk_dualboot"></a> Computadores com inicialização dupla  
 O Configuration Manager não pode gerenciar mais de um sistema operacional em um único computador. Se houver mais de um sistema operacional em um computador a ser gerenciado, ajuste os métodos de descoberta e instalação de cliente do site para garantir que o cliente do Configuration Manager seja instalado somente no sistema operacional que precisa ser gerenciado.  



##  <a name="bkmk_IPv6"></a> Protocolo IP versão 6  
 Além do IPv4 (protocolo IP versão 4), o Configuration Manager dá suporte ao IPv6 (protocolo IP versão 6) com as seguintes exceções:  

|Função| Exceção ao suporte a IPv6|  
|--------------|-------------------------------|  
|Pontos de distribuição baseados em nuvem|O IPv4 é necessário para dar suporte ao Microsoft Azure e aos pontos de distribuição baseados em nuvem.|  
|Gateway de gerenciamento de nuvem|O IPv4 é necessário para dar suporte ao Microsoft Azure e ao gateway de gerenciamento de nuvem.|  
|Dispositivos móveis registrados pelo Microsoft Intune e o conector de serviço da Microsoft|O IPv4 é necessário para dar suporte aos dispositivos móveis registrados pelo Microsoft Intune e ao conector de serviço da Microsoft.|  
|Descoberta de Rede|O IPv4 é necessário ao configurar um servidor DHCP para pesquisar na Descoberta de Rede.|  
|Implantação de sistema operacional|O IPv4 é necessário para dar suporte à implantação de sistema operacional. |  
|Comunicação proxy de ativação|O IPv4 é necessário para dar suporte aos pacotes proxy de ativação do cliente.|  
|Windows CE|O IPv4 é necessário para dar suporte ao cliente do Configuration Manager em dispositivos Windows CE.|  



##  <a name="bkmk_NAT"></a> Conversão de endereços de rede  
 Não há suporte para a NAT (Conversão de Endereços de Rede) no Configuration Manager, a menos que o site dê suporte aos clientes na Internet e o cliente detecte que ele está conectado à Internet. Para obter mais informações sobre o gerenciamento de clientes baseado na Internet, consulte [Planejar o gerenciamento de clientes baseado na Internet](../../../core/clients/deploy/plan/plan-for-managing-internet-based-clients.md).  



##  <a name="bkmk_storage"></a> Tecnologia de armazenamento especializado  
 O Configuration Manager funciona com qualquer hardware certificado na Lista de Compatibilidade de Hardware do Windows para a versão do sistema operacional na qual o componente do Configuration Manager está instalado.

As funções de servidor do site exigem o NTFS, de modo que o Configuration Manager possa definir permissões de arquivo e diretório. O Configuration Manager pressupõe que ele tenha propriedade total sobre uma unidade lógica. Os sistemas de sites executados em computadores separados não podem compartilhar uma partição lógica em qualquer tecnologia de armazenamento. No entanto, cada computador pode usar uma partição lógica separada na mesma partição física de um dispositivo de armazenamento compartilhado.  

 ### <a name="support-considerations"></a>Considerações sobre suporte

-   **Rede de Área de Armazenamento**: há suporte para uma SAN (Rede de Área de Armazenamento) quando um servidor baseado no Windows com suporte é anexado diretamente ao volume que é hospedado pela SAN.  

-   **Single Instance Storage**: o Configuration Manager não dá suporte à configuração das pastas de pacote e assinatura do ponto de distribuição em um volume habilitado para SIS (Single Instance Storage).  

     Além disso, não há suporte para o cache de um cliente do Configuration Manager em um volume habilitado para o SIS.  

-   **Unidade de disco removível**: o Configuration Manager não dá suporte à instalação do sistema de sites ou dos clientes do Configuration Manager em uma unidade de disco removível.  
