---
title: Otimizar a entrega de atualização do Windows 10
titleSuffix: Configuration Manager
description: Saiba como usar o Configuration Manager para gerenciar o conteúdo de atualização e ficar atualizado com o Windows 10.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6fb655ae6094d7c764f2c3d0b84a505e9dfda3d2
ms.sourcegitcommit: 9f02f21fbd4324ee8cc1af2d56db67c9c2fce969
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52709926"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Otimizar a entrega de atualizações do Windows 10 com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para muitos clientes, um caminho bem-sucedido para ficar e manter-se atualizado com as atualizações mensais do Windows 10 começa com uma estratégia de distribuição de conteúdo válida usando o Configuration Manager. O tamanho das atualizações de qualidade mensal pode ser uma causa de preocupação para organizações de grandes porte. Há algumas tecnologias disponíveis que se destinam a ajudar a reduzir a carga de rede e a largura de banda para otimizar a distribuição de atualização. Este artigo explica essas tecnologias, as compara e fornece recomendações para ajudá-lo a tomar decisões sobre qual delas usar.  
 
O Windows 10 fornece vários tipos de atualizações. Para saber mais, confira [Tipos de atualização no Windows Update for Business](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb#update-types). Este artigo se concentra nas atualizações de *qualidade* do Windows 10 com o Configuration Manager. 


## <a name="express-update-delivery"></a>Entrega expressa de atualização

Os downloads de atualização de qualidade do Windows 10 podem ser grandes. Cada pacote contém todas as correções lançadas anteriormente para garantir consistência e simplicidade. A Microsoft conseguiu reduzir o tamanho do conteúdo de atualização do Windows 10 que cada cliente baixa com um recurso chamado expresso. A opção Expressa é usada atualmente por milhões de dispositivos que recebem atualizações diretamente do serviço Windows Update e reduz significativamente o tamanho de download. Esse benefício também está disponível para clientes cujos clientes não baixam diretamente do serviço Windows Update. 

O Configuration Manager adicionou suporte para [arquivos de instalação expressa](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates) das atualizações de qualidade do Windows 10 na versão 1702. No entanto, para obter a melhor experiência, é recomendável que você use o Configuration Manager versão 1802 ou posterior. Para obter o melhor desempenho em velocidades de download, também é recomendável que você use o Windows 10, versão 1703 ou posterior. 

> [!NOTE]  
> O conteúdo da versão expressa é consideravelmente maior do que a versão completa. Um arquivo de instalação expressa contém todas as variações possíveis para cada arquivo que ele foi projetado para atualizar. Como resultado, a quantidade necessária de espaço em disco aumenta para atualizações na origem do pacote de atualização e nos pontos de distribuição quando você habilita o suporte expresso no Configuration Manager. Embora o requisito de espaço em disco nos pontos de distribuição aumente, diminui o tamanho do conteúdo que os clientes baixam desses pontos de distribuição. Os clientes só baixam os bits de que eles necessitam (deltas), mas não a atualização inteira.



## <a name="peer-to-peer-content-distribution"></a>Distribuição de conteúdo par

Mesmo que os clientes baixem somente as partes do conteúdo de que precisam, agilize as atualizações do Windows em seu ambiente utilizando a distribuição de conteúdo de par. Aproveitar os pares como uma fonte de download para as atualizações de qualidade pode ser útil para ambientes em que os pontos de distribuição local não estão presentes em instalações remotas. Esse comportamento impede a necessidade de que todos os clientes baixem conteúdo de um ponto de distribuição remoto em um link WAN lento. Usar pares também pode ser benéfico quando os clientes fazem fallback para o serviço Windows Update. Apenas um par é necessário para baixar o conteúdo de atualização da nuvem antes de disponibilizá-lo para outros dispositivos.

O Configuration Manager dá suporte a muitas tecnologias de par, incluindo o seguinte:
- Otimização de Entrega do Windows
- Cache par do Configuration Manager
- Windows BranchCache  

As seções a seguir fornecem mais informações sobre essas tecnologias.


### <a name="windows-delivery-optimization"></a>Otimização de Entrega do Windows

[Otimização de Entrega](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) é a principal tecnologia de download e método de distribuição de par integrado ao Windows 10. Clientes do Windows 10 podem obter o conteúdo de outros dispositivos em sua rede local que baixam as mesmas atualizações. Usando as [opções do Windows disponíveis para a Otimização de Entrega](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#delivery-optimization-options), você pode configurar clientes em grupos. Esse agrupamento permite que sua organização identifique os dispositivos que são possivelmente os melhores candidatos para atender às solicitações de par. A Otimização de Entrega reduz significativamente a largura de banda geral que é usada para manter os dispositivos atualizados enquanto acelera o tempo de download.

> [!NOTE]  
> A Otimização de Entrega é uma solução gerenciada de nuvem. O acesso à Internet para o serviço de nuvem da Otimização de Entrega é um requisito para utilizar sua funcionalidade de par.  

Para obter os melhores resultados, talvez você precise configurar o [modo de download](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#download-mode) da Otimização de Entrega para **Grupo (2)** e defina *IDs de Grupo*. No modo de grupo, o emparelhamento pode cruzar sub-redes internas entre dispositivos que pertencem ao mesmo grupo, incluindo dispositivos em locais remotos. Use a [opção de ID de Grupo](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#select-the-source-of-group-ids) para criar seu próprio grupo personalizado independentemente de domínios e sites do AD DS. O modo de download de grupo é a opção recomendada para a maioria das organizações que desejam obter a melhor otimização de largura de banda com a Otimização de Entrega.

Configurar manualmente essas IDs de grupo é um desafio quando os clientes são transferidos entre diferentes redes. O Configuration Manager versão 1802 adicionou um novo recurso para simplificar o gerenciamento desse processo [integrando os grupos de limites com Otimização de Entrega](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization). Quando um cliente é ativado, ele se comunica com seu ponto de gerenciamento para obter políticas e fornece suas informações de grupo de limites e de rede. O Configuration Manager cria uma ID exclusiva para cada grupo de limites. O site usa as informações do cliente local para configurar automaticamente a ID de Grupo de Otimização de Entrega do cliente com a ID de limite do Configuration Manager. Quando o cliente passa para outro grupo de limites, ele se comunica com seu ponto de gerenciamento e é reconfigurado automaticamente com uma nova ID de grupo de limites. Com essa integração, Otimização de Entrega pode utilizar as informações do grupo de limites do Configuration Manager para localizar um par do qual deseja baixar atualizações.


### <a name="configuration-manager-peer-cache"></a>Cache par do Configuration Manager

[Cache par](/sccm/core/plan-design/hierarchy/client-peer-cache) é um recurso do Configuration Manager que permite que os clientes compartilhem com outros clientes conteúdo diretamente do cache local do Configuration Manager. O cache par não substitui o uso de outras soluções de cache par, como o Windows BranchCache. Ele funciona junto com eles para fornecer mais opções e estender as soluções tradicionais de implantação de conteúdo, como pontos de distribuição. O cache par não conta com o BranchCache. Se você não habilitar ou usar o BranchCache, o cache par ainda funcionará.

> [!NOTE]  
> Os clientes só podem baixar conteúdo de clientes de cache par que estão em seu grupo de limites atual.  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) é uma tecnologia de otimização de largura de banda no Windows. Cada cliente tem um cache e atua como uma origem alternativa para o conteúdo. Dispositivos na mesma rede podem solicitar esse conteúdo. [O Configuration Manager pode usar o BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache) para permitir que os pares obtenham conteúdo entre si, em vez de sempre terem que entrar em contato com um ponto de distribuição. Usando o BranchCache, os arquivos são armazenados em cache em cada cliente individual, e outros clientes podem recuperá-los conforme necessário. Essa abordagem distribui o cache em vez de ter um único ponto de recuperação. Esse comportamento poupa uma quantidade significativa de largura de banda, reduzindo o tempo para que os clientes recebam o conteúdo solicitado. 



## <a name="selecting-the-right-peer-caching-technology"></a>Como selecionar a tecnologia certa de cache de pares

A seleção da tecnologia certa de cache de pares para arquivos de instalação expressa varia de acordo com suas necessidades e seu ambiente. Embora o Configuration Manager dê suporte a todas as tecnologias de pares acima, você deve usar aquelas que fazem mais sentido para seu ambiente. Para a maioria dos clientes, supondo que os clientes possam atender aos requisitos da Internet para a Otimização de Entrega, o cache de pares do Windows 10 interno com Otimização de Entrega deve ser suficiente. Se os clientes não puderem atender a esses requisitos da Internet, considere o uso do recurso cache par do Configuration Manager. Se você estiver usando o BranchCache com o Configuration Manager e ele atender a todas as suas necessidades, os arquivos expressos com o BranchCache poderão ser a opção certa para você. 

### <a name="peer-cache-comparison-chart"></a>Gráfico de comparação de cache par


| Funcionalidade  | Otimização de Entrega  | Cache de pares  | BranchCache  |
|---------|---------|---------|---------|
| Com suporte entre sub-redes | Sim | Sim | Não |
| Limitação de largura de banda | Sim (Nativo) | Sim (por meio de BITS) | Sim (por meio de BITS) |
| Suporte a conteúdo parcial | Sim | Somente para o Office 365 e Atualizações Expressas | Sim |
| Tamanho do cache no controle de disco | Sim | Sim | Sim |
| Descoberta de uma fonte de pares | Automática | Manual (configuração do agente cliente) | Automática |
| Descoberta de pares | Por meio do serviço de nuvem de Otimização de Entrega (requer acesso à Internet) | Por meio do ponto de gerenciamento (com base em grupos de limites do cliente) | Multicast |
| Relatórios | Sim (usando o Windows Analytics) | Painel de fontes de dados do cliente do ConfigMgr | Painel de fontes de dados do cliente do ConfigMgr |
| Controle de uso de WAN | Sim (nativo, pode ser controlado por meio de configurações de política de grupo) | Grupos de limites | Suporte apenas para sub-rede |
| Tipos de conteúdo com suporte | - Atualizações expressas (por meio do ConfigMgr)</br> - Atualizações do Windows e de segurança</br> - Drivers</br> --Aplicativos da Windows Store</br> Aplicativos da Windows Store para Empresas | Todos os tipos de conteúdo do ConfigMgr, inclusive imagens baixadas no [Windows PE](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic) | Todos os tipos de conteúdo do ConfigMgr, exceto imagens |
| Gerenciamento por meio de ConfigMgr | Parcial (configuração do agente cliente) | Sim (configuração do agente do cliente) | Sim (configuração do agente do cliente) |



## <a name="conclusion"></a>Conclusão

A Microsoft recomenda que você otimize a entrega de atualização de qualidade do Windows 10 usando o Configuration Manager com arquivos de instalação expressa e uma tecnologia de cache de pares, conforme necessário. Essa abordagem deve aliviar os desafios associados a dispositivos Windows 10 que baixam conteúdo grande para a instalação de atualizações de qualidade. Também é recomendável manter os dispositivos Windows 10 atuais implantando atualizações de qualidade a cada mês. Essa prática reduz o delta de conteúdo de atualização de qualidade necessário por dispositivos a cada mês. Reduzir esse conteúdo delta cria downloads de tamanho menor de pontos de distribuição ou fontes de pares. 

Devido à natureza dos arquivos de instalação expressa, seu tamanho do conteúdo é consideravelmente maior do que o conteúdo do arquivo completo tradicional. Esse tamanho resulta em maiores tempos de download de atualização do serviço Windows Update para o servidor de site do Configuration Manager. A quantidade de espaço em disco necessário para os pontos de distribuição e o servidor de site também aumenta. O tempo total necessário para baixar e distribuir atualizações de qualidade pode ser mais longo. No entanto, os benefícios do lado do dispositivo devem ser perceptíveis durante o download e a instalação de atualizações de qualidade pelos dispositivos Windows 10.

Se as compensações do lado do servidor de atualizações de tamanho maior são impedirem a adoção do suporte expresso, mas os benefícios do lado do dispositivo forem essenciais para seus negócios e o ambiente, a Microsoft recomendará que você use o [Windows Update for Business](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10) com o Configuration Manager. O Windows Update for Business fornece todos os benefícios do expresso, sem a necessidade de baixar, armazenar e distribuir os arquivos de instalação expressa em todo o seu ambiente. Os clientes baixam o conteúdo diretamente do serviço Windows Update. Portanto, ainda podem usar a Otimização de Entrega.



## <a name="bkmk_faq"></a> Perguntas frequentes

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Como os downloads expressos do Windows funcionam com o Configuration Manager?

O WUA (Windows update agent) solicita o conteúdo expresso primeiro. Se ele não instalar a atualização expressa, poderá voltar para a atualização completa.  

1. O cliente do Configuration Manager instrui o WUA a baixar o conteúdo da atualização. Quando o WUA inicia um download expresso, primeiro baixa um stub (por exemplo, `Windows10.0-KB1234567-<platform>-express.cab`), que faz parte do pacote expresso.  

2. O WUA passa esse fragmento de código para o instalador de atualização do Windows, manutenção baseada em componente (CBS). O CBS usa o fragmento de código para fazer um inventário local, comparando os deltas do arquivo no dispositivo com o que é necessário para obter a versão mais recente do arquivo que está sendo oferecido.  

3. O CBS solicita que o WUA baixe os intervalos necessários de um ou mais arquivos .psf expressos.  

4. A Otimização de Entrega é coordenada com o Configuration Manager e baixa os intervalos de um ponto de distribuição local ou pares, caso disponíveis. Se a Otimização de Entrega for desabilitada, o serviço BITS (Transferência Inteligente em Segundo Plano) será usado da mesma maneira com o Configuration Manager, coordenando fontes de cache par. A Otimização de Entrega ou BITS passa os intervalos para o WUA, disponibilizando-os para o CBS aplicar e instalar.  


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Por que os arquivos expressos (.psf) são muito grandes, quando armazenados em fontes de pares do Configuration Manager na pasta ccmcache?

Os arquivos expressos (.psf) são arquivos esparsos. Para determinar o espaço real que está sendo usado no disco pelo arquivo, verifique a propriedade **Tamanho em disco** do arquivo. A propriedade Tamanho em disco deve ser consideravelmente menor do que o valor de Tamanho.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>O Configuration Manager dá suporte a arquivos de instalação expressa com atualizações de recursos do Windows 10?

Não, o Configuration Manager atualmente dá suporte apenas aos arquivos de instalação expressa com as atualizações de qualidade do Windows 10.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>Quanto espaço em disco é necessário por atualização de qualidade nos pontos de distribuição e no servidor de site?

Depende. Para cada atualização de qualidade, a versão completa e a expressa do arquivo de atualização são armazenadas nos servidores. As atualizações de qualidade do Windows 10 são cumulativas. Portanto, o tamanho desses arquivos aumenta a cada mês. Planeje no mínimo 5 GB por atualização por idioma. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>Os clientes do Configuration Manager ainda `se beneficiam de arquivos de instalação expressa ao realizar fallback para o serviço Windows Update?

Sim. Se você usar a seguinte opção de implantação de atualização de software, os clientes ainda usarão atualizações expressas e Otimização de Entrega quando realizarem fallback para o serviço de nuvem:  

**Se não houver atualizações de software disponíveis no ponto de distribuição em grupos atuais, vizinhos ou do site, baixe conteúdo do Microsoft Updates**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>Por que o conteúdo do arquivo expresso não é baixado para atualizações existentes depois que habilito o suporte a arquivos expressos? 

As alterações só entram em vigor para as novas atualizações sincronizadas e implantadas depois de habilitar o suporte.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>Há alguma maneira de ver a quantidade de conteúdo baixado de pares usando a Otimização de Entrega?
O Windows 10, versão 1703 (e posterior) inclui dois novos cmdlets do PowerShell, **Get-DeliveryOptimizationPerfSnap** e **Get-DeliveryOptimizationStatus**. Esses cmdlets oferecem mais informações sobre o uso do cache e a Otimização de Entrega. Para saber mais, confira [Cmdlets do Windows PowerShell para analisar o uso](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#windows-powershell-cmdlets-for-analyzing-usage)


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>Como os clientes se comunicam com a Otimização de Entrega na rede?
Para saber mais sobre portas de rede, requisitos de proxy e nomes de host para firewalls, confira [Perguntas frequentes para Otimização de Entrega](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).

