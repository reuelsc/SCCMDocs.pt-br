---
title: Suporte para recursos do Windows | Microsoft Docs
description: "Saiba a quais recursos de rede e do Windows o System Center Configuration Manager dá suporte."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 29e4f8a70b56b772a54ee858a392533780ccbaf9


---
# <a name="support-for-windows-features-and-networks-in-system-center-configuration-manager"></a>Suporte para recursos do Windows e redes no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico identifica o suporte do System Center Configuration Manager para recursos de rede e do Windows comuns.  


##  <a name="a-namebkmkbranchcachea-branchcache"></a><a name="bkmk_branchcache"></a> BranchCache  
O Windows BranchCache é integrado no Configuration Manager. É possível definir as configurações do BranchCache em um tipo de implantação de aplicativos, na implantação de um pacote e de sequência de tarefas.  

Quando todos os requisitos do BranchCache forem atendidos, esse recurso habilita clientes em locais remotos para obter conteúdo de clientes locais que têm um cache atual do conteúdo.  

Por exemplo, quando o primeiro computador cliente habilitado para BranchCache solicitar conteúdo de um ponto de distribuição configurado como um servidor do BranchCache, o computador cliente baixará e armazenará o conteúdo em cache. Depois, esse conteúdo é disponibilizado para clientes na mesma sub-rede que solicita esse mesmo conteúdo, e os clientes também armazenam o conteúdo em cache. Dessa maneira, os clientes sucessivos na mesma sub-rede não precisam baixar o conteúdo do ponto de distribuição, e o conteúdo é distribuído entre vários clientes para transferências futuras.  

**Para dar suporte ao BranchCache com o Configuration Manager:**  

-   Adicione o recurso **Windows BranchCache** ao servidor do sistema de sites configurado como um ponto de distribuição.  

    -   Os pontos de distribuição nos servidores configurados para dar suporte ao BranchCache não exigem nenhuma configuração adicional  

    -   Não é possível adicionar o Windows BranchCache a um ponto de distribuição baseado em nuvem, mas os pontos de distribuição baseados em nuvem dão suporte para o download de conteúdo por clientes configurados para o Windows BranchCache  

**Para permitir que os clientes usem o BranchCache:**  

-   Os clientes que dão suporte ao BranchCache devem ser configurados para o modo distribuído do BranchCache  

-   A configuração do sistema operacional para as configurações do cliente BITS deve estar habilitada para dar suporte ao BranchCache  

**Há suporte para os seguintes sistemas operacionais cliente com o Windows BranchCache:**  

|Sistema operacional|Detalhes do suporte|  
|----------------------|---------------------|  
|Windows 7 com SP1|Com suporte por padrão|  
|Windows 8|Com suporte por padrão|  
|Windows 8.1|Com suporte por padrão|  
|Windows 10|Com suporte por padrão|  
|Windows Server 2008 com SP2|**Requer BITS 4.0** – é possível instalar a versão 4.0 do BITS em clientes do Configuration Manager usando atualizações de software ou distribuição de software. Para obter mais informações sobre a versão do BITS 4.0, consulte [Windows Management Framework](http://go.microsoft.com/fwlink/p/?LinkId=181979).<br /><br /> Nesse sistema operacional, não há suporte para a funcionalidade de cliente do BranchCache para distribuição de software executada da rede ou para transferências de arquivos SMB. Além disso, esse sistema operacional não pode usar a funcionalidade do BranchCache com pontos de distribuição baseados em nuvem.|  
|Windows Server 2008 R2|Com suporte por padrão|  
|Windows Server 2012|Com suporte por padrão|  
|Windows Server 2012 R2|Com suporte por padrão|  

 Para obter mais informações sobre o BranchCache, veja [BranchCache para Windows](http://go.microsoft.com/fwlink/p/?LinkId=177945) na documentação do Windows Server.  

##  <a name="a-namebkmkworkgroupsa-computers-in-workgroups"></a><a name="bkmk_Workgroups"></a> Computadores em grupos de trabalho  
O Configuration Manager dá suporte a clientes em grupos de trabalho.  

-   O Configuration Manager dá suporte à movimentação de um cliente de um grupo de trabalho para um domínio ou de um domínio para um grupo de trabalho. Para obter mais informações, consulte [How to Install Configuration Manager Clients on Workgroup Computers (Como instalar clientes do Configuration Manager em computadores do grupo de trabalho)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup) no tópico [Como implantar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

> [!NOTE]  
>  Embora haja suporte para clientes em grupos de trabalho, todos os sistemas de sites devem ser membros de um Domínio do Active Directory com suporte  


##  <a name="a-namebkmmkdatadedupa-data-deduplication"></a><a name="bkmmk_datadedup"></a> Eliminação de duplicação de dados  
O Configuration Manager dá suporte ao uso da eliminação de duplicação de dados com pontos de distribuição nos seguintes sistemas operacionais:  

-   Windows Server 2012  

-   Windows Server 2012 R2  

> [!IMPORTANT]  
>  O volume que hospeda os arquivos de origem do pacote não pode ser marcado para a eliminação de duplicação de dados. Isso ocorre, porque a eliminação de duplicação de dados usa os pontos de nova análise e o Configuration Manager não dá suporte ao uso de um local de origem do conteúdo com arquivos armazenados nos pontos de nova análise.  

Para obter mais informações, consulte [Configuration Manager Distribution Points and Windows Server 2012 Data Deduplication (Pontos de distribuição do Configuration Manager e eliminação de duplicação de dados do Windows Server 2012)](http://blogs.technet.com/b/configmgrteam/archive/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication.aspx) no blog da equipe do Configuration Manager e [Visão geral de eliminação de duplicação de dados](http://technet.microsoft.com/library/hh831602.aspx) na biblioteca do TechNet do Windows Server.  

##  <a name="a-namebkmkdaa-directaccess"></a><a name="bkmk_DA"></a> DirectAccess  
O Configuration Manager dá suporte ao recurso DirectAccess no Windows Server 2008 R2 para a comunicação entre clientes e servidores do sistema de sites.  

-   Quando todos os requisitos do DirectAccess são atendidos com este recurso, os clientes do Configuration Manager na Internet podem se comunicar com seu site atribuído como se estivessem na intranet.  

-   Para as ações iniciadas pelo servidor, como o controle remoto e a instalação por push do cliente, o computador de inicialização (como o servidor do site) deve executar o IPv6, e deve haver suporte para esse protocolo em todos os dispositivos de rede intermediários.  

O Configuration Manager não dá suporte aos seguintes com o DirectAccess:  

-   Implantação de sistemas operacionais  

-   Comunicação entre sites do Configuration Manager  

-   Comunicação entre servidores do sistema de sites do site do Configuration Manager em um site  

##  <a name="a-namebkmkdualboota-dual-boot-computers"></a><a name="bkmk_dualboot"></a> Computadores com inicialização dupla  
 O Configuration Manager não pode gerenciar mais de um sistema operacional em um único computador. Se houver mais de um sistema operacional em um computador que deve ser gerenciado, ajuste os métodos de descoberta e instalação usados para garantir que o cliente do Configuration Manager seja instalado somente no sistema operacional que deve ser gerenciado.  

##  <a name="a-namebkmkipv6a-internet-protocol-version-6"></a><a name="bkmk_IPv6"></a> Protocolo IP versão 6  
 Além do IPv4 (protocolo IP versão 4), o Configuration Manager dá suporte ao IPv6 (protocolo IP versão 6) com as seguintes exceções:  

|Função|Exceção ao suporte a IPv6|  
|--------------|-------------------------------|  
|Pontos de distribuição baseados em nuvem|O IPv4 é necessário para dar suporte ao Microsoft Azure e aos pontos de distribuição baseados em nuvem.|  
|Dispositivos móveis registrados pelo Microsoft Intune e o conector de serviço da Microsoft|O IPv4 é necessário para dar suporte aos dispositivos móveis registrados pelo Microsoft Intune e ao conector de serviço da Microsoft.|  
|Descoberta de Rede|O IPv4 é necessário ao configurar um servidor DHCP para pesquisar na Descoberta de Rede.|  
|Implantação de sistema operacional|O IPv4 é necessário para dar suporte à implantação de sistema operacional.|  
|Comunicação proxy de ativação|O IPv4 é necessário para dar suporte aos pacotes proxy de ativação do cliente.|  
|Windows CE|O IPv4 é necessário para dar suporte ao cliente do Configuration Manager em dispositivos Windows CE.|  

##  <a name="a-namebkmknata-network-address-translation"></a><a name="bkmk_NAT"></a> Conversão de endereços de rede  
 Não há suporte para a NAT (Conversão de Endereços de Rede) no Configuration Manager, a menos que o site dê suporte aos clientes na Internet e o cliente detectar que ele está conectado à Internet. Para obter mais informações sobre gerenciamento de clientes baseado na Internet, consulte [Plan for managing Internet-based clients in System Center Configuration Manager (Planejar o gerenciamento de clientes baseado na Internet no System Center Configuration Manager)](../../../core/clients/deploy/plan/plan-for-managing-internet-based-clients.md).  

##  <a name="a-namebkmkstoragea-specialized-storage-technology"></a><a name="bkmk_storage"></a> Tecnologia de armazenamento especializado  
 O Configuration Manager funciona com qualquer hardware certificado na Lista de Compatibilidade de Hardware do Windows para a versão do sistema operacional na qual o componente do Configuration Manager está instalado. As funções do servidor do site exigem sistemas de arquivos NTFS para que as permissões de diretório e arquivo possam ser definidas. Como o Configuration Manager presume que tem propriedade total de uma unidade lógica, os sistemas de sites executados em computadores separados não podem compartilhar uma partição lógica em qualquer tecnologia de armazenamento. No entanto, cada computador pode usar uma partição lógica separada na mesma partição física de um dispositivo de armazenamento compartilhado.  

 **Considerações de suporte:**  

-   **Rede de Área de Armazenamento**: há suporte para uma SAN (Rede de Área de Armazenamento) quando um servidor baseado no Windows com suporte é anexado diretamente ao volume que é hospedado pela SAN.  

-   **Single Instance Storage**: o Configuration Manager não dá suporte à configuração das pastas de pacote e assinatura do ponto de distribuição em um volume habilitado para SIS (Single Instance Storage).  

     Além disso, não há suporte para o cache de um cliente do Configuration Manager em um volume habilitado para o SIS.  

-   **Unidade de disco removível**: O Configuration Manager não dá suporte à instalação do sistema de sites ou dos clientes do Configuration Manager em uma unidade de disco removível.  



<!--HONumber=Dec16_HO3-->


