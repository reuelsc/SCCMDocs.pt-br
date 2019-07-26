---
title: Hardware recomendado
titleSuffix: Configuration Manager
description: Obtenha recomendações de hardware para ajudar você a dimensionar o ambiente do System Center Configuration Manager, além de uma implantação básica.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cbad2440f9309e712fb00da2739ed5302866ff63
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68339470"
---
# <a name="recommended-hardware-for-system-center-configuration-manager"></a>Hardware recomendado para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As recomendações a seguir são diretrizes para ajudar a dimensionar seu ambiente do System Center Configuration Manager para dar suporte a mais de uma implantação muito básica de sites, sistemas de sites e clientes. Elas não têm a finalidade de abordar todos os sites e configurações de hierarquia possíveis.  

Use as informações nas seções a seguir como um guia para ajudar a planejar o hardware que pode atender aos volumes de processamento de clientes e sites que usam os recursos do Configuration Manager disponíveis com as configurações padrão.  



##  <a name="bkmk_ScaleSieSystems"></a> Sistemas de sites  
Esta seção fornece as configurações de hardware recomendadas para sistemas de sites do Configuration Manager para implantações que dão suporte ao número máximo de clientes e usam todos os recursos do Configuration Manager ou a maior parte deles. Implantações que dão suporte a menos que o número máximo de clientes e que não usam todos os recursos disponíveis podem exigir menos recursos do computador. Em geral, os fatores principais que limitam o desempenho geral do sistema incluem, na ordem:  

1.  Desempenho da E/S de disco  

2.  Memória disponível  

3.  CPU  

Para obter um melhor desempenho, use as configurações de RAID 10 para todas as unidades de dados e rede Ethernet de 1 Gbps.  

###  <a name="bkmk_ScaleSiteServer"></a> Servidores do site  

|Configuração do site|CPU (núcleos)|Memória (GB)|Alocação de memória para o SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Servidor do site primário autônomo com uma função de site do banco de dados no mesmo servidor<sup>1</sup>|16|96|80|  
|Servidor de site primário autônomo com um banco de dados do site remoto|8|16|-|  
|Servidor de banco de dados remoto para um site primário autônomo|16|72|90|  
|Servidor do site de administração central com uma função de site do banco de dados no mesmo servidor<sup>1</sup>|20|128|80|  
|Servidor de site de administração central com um banco de dados do site remoto|8|16|-|  
|Servidor de banco de dados remoto para um site de administração central|16|96|90|  
|Site primário filho com a função de site do banco de dados no mesmo servidor|16|96|80|  
|Servidor de site primário filho com um banco de dados do site remoto|8|16|-|  
|Servidor de banco de dados remoto para um site primário filho|16|72|90|  
|Servidor do site secundário|8|16|-|  

<sup>1</sup> Quando o servidor do site e do SQL Server estão instalados no mesmo computador, a implantação dá suporte a um máximo de [números de tamanho e escala](/sccm/core/plan-design/configs/size-and-scale-numbers) para sites e clientes. Porém, essa configuração pode limitar as [opções de alta disponibilidade para o System Center Configuration Manager](/sccm/protect/understand/high-availability-options), como ao usar um cluster do SQL Server. Além disso, por causa dos requisitos de E/S mais elevados necessários para dar suporte tanto ao SQL Server quanto ao servidor do site do Configuration Manager ao executar ambos no mesmo computador, será recomendável considerar o uso de uma configuração com um computador remoto do SQL Server se você tiver uma implantação maior.  

###  <a name="bkmk_RemoteSiteSystem"></a> Servidores do sistema de sites remoto  
As diretrizes a seguir são para computadores que contêm uma função de sistema de sites único. Você planeja fazer ajustes ao instalar várias funções de sistema de site no mesmo computador.  

|Função do sistema de site|CPU (núcleos)|Memória (GB)|Espaço em disco (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Ponto de gerenciamento|4|8|50|  
|Ponto de distribuição|2|8|Conforme exigido pelo sistema operacional e para armazenar o conteúdo que você implantar|  
|Catálogo de aplicativos, com o serviço Web e o site da Web no computador do sistema de site|4|16|50|  
|Ponto de atualização de software<sup>1</sup>|8|16|Conforme exigido pelo sistema operacional e para armazenar as atualizações que você implantar|  
|Todas as outras funções do sistema de site|4|8|50|  

<sup>1</sup> O computador que hospeda um ponto de atualização de software exige as seguintes configurações para pools de aplicativos do IIS:  

- Aumentar o **Comprimento da Fila de WsusPool** para **2000**.  

- Aumente o **limite da Memória Particular do WsusPool** em quatro vezes ou defina-o como **0** (ilimitado).  

###  <a name="bkmk_DiskSpace"></a> Espaço em disco para sistemas de sites  
A configuração e a alocação de disco contribuem para o desempenho de Configuration Manager. Como cada ambiente do Configuration Manager é diferente, os valores que você implementa podem variar com a seguinte diretriz.  

Para obter o melhor desempenho, coloque cada objeto em um volume RAID separado e dedicado. Para todos os volumes de dados (Configuration Manager e seus arquivos de banco de dados), use RAID 10 para obter o melhor desempenho.  

|Uso de dados|Espaço mínimo em disco|25.000 clientes|50.000 clientes|100.000 clientes|150.000 clientes|700.000 clientes (site de administração central)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Sistema operacional|Consulte as diretrizes para o sistema operacional.|Consulte as diretrizes para o sistema operacional.|Consulte as diretrizes para o sistema operacional.|Consulte as diretrizes para o sistema operacional.|Consulte as diretrizes para o sistema operacional.|Consulte as diretrizes para o sistema operacional.|  
|Arquivos de log e aplicativo do Configuration Manager|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Arquivo .mdf do banco de dados do site|75 GB para cada 25.000 clientes|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Arquivo .ldf do banco de dados do site|25 GB para cada 25.000 clientes|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Arquivos do banco de dados temporário (. mdf e. ldf)|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|  
|Conteúdo (compartilhamentos de ponto de distribuição)|Conforme o necessário<sup>1</sup>|Conforme o necessário<sup>1</sup>|Conforme o necessário<sup>1</sup>|Conforme o necessário<sup>1</sup>|Conforme o necessário<sup>1</sup>|Conforme o necessário<sup>1</sup>|  

<sup>1</sup> As diretrizes de espaço em disco não incluem o espaço necessário para o conteúdo localizado na biblioteca de conteúdo no servidor do site ou pontos de distribuição. Para obter informações sobre o planejamento da biblioteca de conteúdo, consulte [A biblioteca de conteúdo](../../../core/plan-design/hierarchy/the-content-library.md).  

Além das orientações acima, considere as seguintes diretrizes ao planejar requisitos de espaço em disco:  

- Cada cliente requer aproximadamente 5 MB de espaço.  

- Quando planejar o tamanho do banco de dados temporário de um site primário, planeje um tamanho combinado que seja de 25% a 30% do arquivo .mdf do banco de dados do site. O tamanho real pode ser significativamente menor ou maior, isso depende do desempenho do servidor do site e do volume de dados de entrada durante períodos de tempo curtos e longos.  

  > [!NOTE]  
  >  Quando tiver 50.000 ou mais clientes em um site, planeje usar quatro ou mais arquivos .mdf do banco de dados temporário.  

- O tamanho do banco de dados Temp de um site de administração central normalmente é muito menor do que o de um site primário.  

- O banco de dados do site secundário tem as seguintes limitações de tamanho:  

  - SQL Server 2012 Express: 10 GB  

  - SQL Server 2014 Express: 10 GB  

##  <a name="bkmk_ScaleClient"></a> Clientes  
Esta seção fornece as configurações de hardware recomendadas para computadores gerenciados usando o software cliente do Configuration Manager.  

### <a name="client-for-windows-computers"></a>Cliente para computadores Windows  
Estes são os requisitos mínimos para computadores baseados no Windows que você gerencia usando o Configuration Manager, incluindo sistemas operacionais inseridos:  

- **Processador e memória:** Confira os requisitos de RAM e do processador do sistema operacional do computador.  

- **Espaço em disco:** 500 MB de espaço em disco disponível, com 5 GB recomendados para o cache do cliente do Configuration Manager. Menos espaço em disco será necessário se você usar as configurações personalizadas para instalar o cliente do Configuration Manager:  

  - Use a propriedade de linha de comando /skipprereq do CCMSetup para evitar a instalação de arquivos não solicitados pelo cliente. Por exemplo, execute `CCMSetup.exe /skipprereq:silverlight.exe` se o cliente não usar o Catálogo de Aplicativos. A partir do Configuration Manager 1802, o Silverlight deixa de ser instalado automaticamente.  

  - Use a propriedade SMSCACHESIZE do Client.msi para definir um arquivo de cache que seja menor do que o padrão de 5.120 MB. O tamanho mínimo é 1 MB. Por exemplo, o `CCMSetup.exe SMSCachesize=2` cria um cache que é de 2 MB de tamanho.  

  Para obter mais informações sobre essas configurações de instalação do cliente, consulte [Sobre as propriedades de instalação do cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

  > [!TIP]  
  >  Instalar o cliente com espaço em disco mínimo é útil para dispositivos com Windows Embedded que normalmente têm tamanhos menores de disco que computadores com Windows padrão.  



 Veja abaixo os requisitos de hardware mínimos adicionais para a funcionalidade opcional no Configuration Manager.  

- **Implantação de sistema operacional:** 384 GB de RAM  

- **Centro de Software:** processador de 500 MHz  

- **Controle Remoto:** Pentium 4 Hyper-Threaded 3 GHz (núcleo único) ou CPU comparável, com pelo menos 1 GB de RAM para uma experiência ideal  

### <a name="client-for-linux-and-unix"></a>Cliente para Linux e UNIX  
Estes são os requisitos mínimos para servidores Linux e UNIX que você gerencia com o Configuration Manager.  

|Requisito|Detalhes|  
|-----------------|-------------|  
|Processador e memória|Consulte os requisitos de RAM e processador para o sistema operacional do computador.|  
|Espaço em disco|500 MB de espaço em disco disponível, com 5 GB recomendados para o cache do cliente do Configuration Manager.|  
|Conectividade de rede|Os computadores cliente do Configuration Manager devem ter conectividade de rede com os sistemas de sites do Configuration Manager para habilitar o gerenciamento.|  

##  <a name="bkmk_ScaleConsole"></a> Console do Configuration Manager  
Os requisitos na tabela a seguir se aplicam a cada computador que executa o console do Configuration Manager.  

**Configuração mínima de hardware:**  

- CPU Intel i3 ou comparável  

- 2 GB de RAM  

- 2 GB de espaço em disco  

|Configuração de DPI|Resolução mínima|  
|-----------------|------------------------|  
|96/100%|1024 x 768|  
|120/125%|1280 x 960|  
|144/150%|1600 x 1200|  
|196/200%|2500 x 1600|  

**Suporte para o PowerShell:**  

Quando você instala o suporte para o PowerShell em um computador que executa o console do Configuration Manager, é possível executar os cmdlets do PowerShell nesse computador para gerenciar o Configuration Manager.

- Há suporte para PowerShell 3.0 ou posterior

Além do PowerShell, há suporte para o Windows Management Framework (WMF) versão 3.0 ou posterior.   


##  <a name="bkmk_ScaleLab"></a> Implantações de laboratório  
Use as recomendações mínimas de hardware a seguir para implantações de laboratório e teste do Configuration Manager. Essas recomendações se aplicam a todos os tipos de site, até 100 clientes:  

|Função|CPU (núcleos)|Memória (GB)|Espaço em disco (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Servidor de banco de dados e site|2 - 4|8 – 12|100|  
|Servidor do sistema de site|1 - 4|2 - 4|50|  
|Cliente|1 - 2|1 - 3|30|  
