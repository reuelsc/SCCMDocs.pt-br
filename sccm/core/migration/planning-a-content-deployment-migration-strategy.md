---
title: "Migrar o conteúdo"
titleSuffix: Configuration Manager
description: "Use pontos de distribuição para gerenciar o conteúdo ao migrar dados para uma hierarquia de destino do System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
caps.latest.revision: "8"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 7332ff4bf0ad10bd18e42485fb548eee70deaf04
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2018
---
# <a name="plan-a-content-deployment-migration-strategy-in-system-center-configuration-manager"></a>Planejar uma estratégia de migração de implantação de conteúdo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Enquanto você migrar dados ativamente para uma hierarquia de destino do System Center Configuration Manager, os clientes do Configuration Manager nas hierarquias de origem e de destino podem manter o acesso ao conteúdo implantado na hierarquia de origem. Também é possível usar a migração para atualizar ou transferir os pontos de distribuição da hierarquia de origem para tornarem-se pontos de distribuição na hierarquia de destino. Quando você compartilha e atualiza ou reatribui os pontos de distribuição, essa estratégia pode ajudá-lo a evitar ter de reimplantar conteúdo em novos servidores na hierarquia de destino para os clientes que você migrar.  

Embora você possa recriar e distribuir conteúdo na hierarquia de destino, também é possível usar as seguintes opções para gerenciar esse conteúdo:  

-   Compartilhar pontos de distribuição na hierarquia de origem com clientes na hierarquia de destino.  

-   Atualizar pontos de distribuição autônomos do Configuration Manager 2007 ou sites secundários do Configuration Manager 2007 na hierarquia de origem para tornarem-se pontos de distribuição na hierarquia de destino.  

-   Reatribua os pontos de distribuição de uma hierarquia de origem do System Center Configuration Manager ou a um site na hierarquia de destino.  

Use as seções a seguir como auxílio para planejar a implantação de conteúdo durante a migração:  

-   [Compartilhar pontos de distribuição entre hierarquias de origem e destino](#About_Shared_DPs_in_Migration)  

-   [Planejar para atualizar pontos de distribuição compartilhados do Configuration Manager 2007](#Planning_to_Upgrade_DPs)  

    -   [Processo de atualização do ponto de distribuição](#BKIMK_UpgradeProcess)  

    -   [Planejar para atualizar sites secundários do Configuration Manager 2007](#BKMK_UpgradeSS)  

-   [Planejar para transferir pontos de distribuição do System Center Configuration Manager](#BKMK_ReassignDistPoint)  

    -   [Processo de reatribuição de pontos de distribuição](#BKMK_ReassignProcess)  

-   [Propriedade do conteúdo durante a migração de conteúdo](#About_Migrating_Content)  

##  <a name="About_Shared_DPs_in_Migration"></a> Compartilhar pontos de distribuição entre hierarquias de origem e destino  
Durante a migração, é possível compartilhar pontos de distribuição de uma hierarquia de origem com a hierarquia de destino. É possível usar pontos de distribuição compartilhados para tornar o conteúdo migrado de uma hierarquia de origem imediatamente disponível para clientes na hierarquia de destino sem ter de recrear esse conteúdo, e depois distribuí-lo para novos pontos de distribuição na hierarquia de destino. Quando clientes na hierarquia de destino solicitam conteúdo implantado em pontos de distribuição compartilhados, os pontos de distribuição compartilhados podem ser oferecidos aos clientes como locais de conteúdo válidos.  

 Além de ser um local de conteúdo válido para clientes na hierarquia de destino enquanto a migração da hierarquia de origem permanece ativa, é possível atualizar ou transferir um ponto de distribuição para a hierarquia de destino. Você pode atualizar pontos de distribuição compartilhados do Configuration Manager 2007 e reatribuir pontos de distribuição compartilhados do System Center 2012 Configuration Manager. Quando você atualiza ou reatribui um ponto de distribuição compartilhado, o ponto de distribuição é removido da hierarquia de origem e torna-se um ponto de distribuição na hierarquia de destino. Depois de atualizar ou reatribuir um ponto de distribuição compartilhado, é possível continuar a usar o ponto de distribuição na hierarquia de destino após a conclusão da migração da hierarquia de origem. Para saber mais sobre como atualizar um ponto de distribuição compartilhado, consulte [Planejar para atualizar pontos de distribuição compartilhados do Configuration Manager 2007](#Planning_to_Upgrade_DPs). Para saber mais sobre como transferir um ponto de distribuição compartilhado, consulte [Planejar para transferir pontos de distribuição do System Center Configuration Manager](#BKMK_ReassignDistPoint).  

 Você pode optar por compartilhar pontos de distribuição de qualquer site de origem da hierarquia de origem. Quando você compartilha pontos de distribuição para um site de origem, sites secundários filho são compartilhados em cada ponto de distribuição qualificado nesse site primário e em cada um dos sites primários. Para qualificar-se para ser um ponto de distribuição compartilhado, o servidor de sistema de site que hospeda o ponto de distribuição deve ser configurado com um FQDN (nome de domínio totalmente qualificado). Os pontos de distribuição configurados com um nome NetBIOS são desconsiderados.  

> [!TIP]  
>  O Configuration Manager 2007 não requer a configuração de um FQDN para servidores do sistema de sites.  

Use as seguintes informações como auxílio para o planejamento de pontos de distribuição compartilhados:  

-   Os pontos de distribuição que você compartilhar deverão atender aos pré-requisitos para pontos de distribuição compartilhados. Para mais informações sobre esses pré-requisitos, veja [Configurações necessárias para a migração](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) em [Pré-requisitos da migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

-   A ação de compartilhar pontos de distribuição é uma configuração que abrange todo o site que compartilha todos os pontos de distribuição qualificados em um site de origem e em qualquer site secundário filho direto. Não é possível selecionar pontos de distribuição individuais para compartilhar quando se habilita o compartilhamento de pontos de distribuição.  

-   Os clientes na hierarquia de destino podem receber informações do local do conteúdo para pacotes que são distribuídos em pontos de distribuição compartilhados da hierarquia de origem. No caso de pontos de distribuição de uma hierarquia de origem do Configuration Manager 2007, isso inclui pontos de distribuição secundários, em compartilhamentos de servidores e padrão.  

    > [!WARNING]  
    >  Se você alterar a hierarquia de origem, os pontos de distribuição compartilhados da hierarquia de origem não estarão mais disponíveis e não poderão ser oferecidos como locais de conteúdo para clientes na hierarquia de destino. Se você reconfigurar a migração para usar a hierarquia de origem, os pontos de distribuição compartilhados anteriormente serão restaurados como servidores de locais de conteúdo válidos.  

-   Quando você migra um pacote hospedado em um ponto de distribuição compartilhado, a versão do pacote deve permanecer a mesma nas hierarquias de origem e destino. Quando uma versão do pacote não é a mesma nas hierarquias de origem e destino, os clientes na hierarquia de destino não podem recuperar o conteúdo do ponto de distribuição compartilhado. Portanto, se você atualizar um pacote na hierarquia de origem, deverá migrar novamente os dados do pacote para que os clientes da hierarquia de destino possam recuperar esse conteúdo de um ponto de distribuição compartilhado.  

    > [!NOTE]  
    >  Quando você exibe detalhes de um pacote hospedado em um ponto de distribuição compartilhado, o número de pacotes exibidos como **Pacotes Migrados Hospedados** na guia **Pontos de Distribuição Compartilhados** nos sites de origem não é atualizado até a conclusão do próximo ciclo de coleta de dados.  

-   É possível exibir os pontos de distribuição compartilhados e suas propriedades no nó **Hierarquia de Origem** do espaço de trabalho **Administração** no console do Configuration Manager que se conecta à hierarquia de destino.  

-   Não é possível usar um ponto de distribuição compartilhado de uma hierarquia de origem do Configuration Manager 2007 para hospedar pacotes do Microsoft Application Virtualization (App-V). Os pacotes do App-V devem ser migrados e convertidos para uso pelos clientes na hierarquia de destino. No entanto, é possível usar um ponto de distribuição compartilhado de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager para hospedar pacotes do App-V para clientes em uma hierarquia de destino.  

-   Quando você compartilha um ponto de distribuição protegido de uma hierarquia de origem do Configuration Manager 2007, a hierarquia de destino cria um grupo de limites que inclui os locais de rede protegidos desse pronto de distribuição. Não é possível alterar esse grupo de limites na hierarquia de destino. No entanto, se você alterar as informações de limites protegidos do ponto de distribuição na hierarquia de origem do Configuration Manager 2007, essa alteração será refletida na hierarquia de destino após a conclusão do próximo ciclo de coleta de dados.  

    > [!NOTE]  
    >  Os sites do System Center 2012 Configuration Manager e do System Center Configuration Manager usam o conceito de pontos de distribuição preferidos em vez de pontos de distribuição protegidos. Essa condição só se aplica aos pontos de distribuição compartilhados de sites de origem do Configuration Manager 2007.  

Os pontos de distribuição qualificados não ficam visíveis no console do Configuration Manager antes que você compartilhe pontos de distribuição de um site de origem. Depois de compartilhar pontos de distribuição, somente os pontos de distribuição compartilhados com êxito são listados.  

Depois de compartilhar pontos de distribuição, é possível alterar a configuração de qualquer ponto de distribuição compartilhado na hierarquia de origem. As alterações feitas na configuração de um ponto de distribuição são refletidas na hierarquia de destino após o próximo ciclo de coleta de dados. Os pontos de distribuição atualizados para qualificação para compartilhamento são compartilhados automaticamente, enquanto aos que não se qualificam mais param de compartilhar pontos de distribuição. Por exemplo, é possível ter um ponto de distribuição que não é configurado com um FQDN de intranet e não foi compartilhado inicialmente com a hierarquia de destino. Depois de configurar o FQDN para esse ponto de distribuição, o próximo ciclo de coleta de dados identifica essa configuração e o ponto de distribuição é compartilhado com a hierarquia de destino.  

##  <a name="Planning_to_Upgrade_DPs"></a> Planejar para atualizar pontos de distribuição compartilhados do Configuration Manager 2007  
Ao migrar de uma hierarquia de origem do Configuration Manager 2007, é possível atualizar um ponto de distribuição compartilhado para transformá-lo em um ponto de distribuição do System Center Configuration Manager. É possível atualizar pontos de distribuição em sites primários e secundários. O processo de atualização remove o ponto de distribuição da hierarquia do Configuration Manager 2007 e o transforma em um servidor de sistema de sites na hierarquia de destino. Esse processo também copia o conteúdo existente que está no ponto de distribuição para um novo local no computador do ponto de distribuição. Em seguida, o processo de atualização modifica a cópia do conteúdo para criar a instância única para usar com a implantação de conteúdo na hierarquia de destino. Portanto, ao atualizar um ponto de distribuição, você não precisa redistribuir o conteúdo migrado hospedado no ponto de distribuição do Configuration Manager 2007.  

Depois que o Configuration Manager converter o conteúdo para o Single Instance Store, exclui o conteúdo de origem original no computador do ponto de distribuição para liberar espaço em disco. O Configuration Manager não usa o local original do conteúdo de origem.  

Nem todos os pontos de distribuição do Configuration Manager 2007 que você pode compartilhar são qualificados para a atualização para o System Center Configuration Manager. Para ser qualificado para atualização, um ponto de distribuição do Configuration Manager 2007 deve atender às condições para atualização. Essas condições incluem o servidor do sistema de sites em que o ponto de distribuição está instalado e o tipo de ponto de distribuição instalado do Configuration Manager 2007. Por exemplo, não é possível atualizar qualquer tipo de ponto de distribuição instalado no computador do servidor do site em um site primário, mas é possível atualizar um ponto de distribuição padrão instalado no computador do servidor do site em um site secundário.  

> [!NOTE]  
>  É possível atualizar somente os pontos de distribuição compartilhados do Configuration Manager 2007 que estão em um computador que executa uma versão de sistema operacional com suporte para pontos de distribuição na hierarquia de destino. Por exemplo, embora seja possível compartilhar um ponto de distribuição do Configuration Manager 2007 que esteja em um computador que executa o Windows Vista, não é possível atualizar esse ponto de distribuição compartilhado, pois não há suporte do System Center Configuration Manager para o sistema operacional para uso como um ponto de distribuição.  

A tabela a seguir lista os locais com suporte para cada tipo de ponto de distribuição do Configuration Manager 2007 que pode ser atualizado.  

|Tipo de ponto de distribuição|Ponto de distribuição em um computador de sistema de site diferente do servidor do site|Ponto de distribuição em um computador de sistema de site diferente do servidor do site e que hospeda outras funções de sistema de site|Ponto de distribuição em um servidor do site secundário|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|Ponto de distribuição padrão|Sim|Não|Sim|  
|Ponto de distribuição em compartilhamentos do servidor<sup>1</sup>|Sim|Não|Não|  
|Ponto de distribuição secundário|Sim|Não|Não|  

 <sup>1</sup> O System Center Configuration Manager não dá suporte aos compartilhamentos de servidor para sistemas de sites, mas dá suporte à atualização de um ponto de distribuição do Configuration Manager 2007 que está em um compartilhamento de servidor. Ao atualizar um ponto de distribuição do Configuration Manager 2007 que está em um compartilhamento do servidor, o tipo de ponto de distribuição é automaticamente convertido em um servidor, e você deve selecionar a unidade no computador do ponto de distribuição que armazenará o repositório de conteúdo de instância única.  

> [!WARNING]  
>  Antes de atualizar um ponto de distribuição secundário, desinstale o software cliente do Configuration Manager 2007. Ao atualizar um ponto de distribuição secundário que tem o software cliente do Configuration Manager 2007 instalado, o conteúdo implantado anteriormente é removido do computador, e ocorre falha na atualização do ponto de distribuição.  

Para identificar os pontos de distribuição qualificados para atualização no console do Configuration Manager no nó **Hierarquia de Origem**, selecione um site de origem e a guia **Pontos de Distribuição Compartilhados**. Os pontos de distribuição qualificados são exibidos com **Sim** na coluna **Qualificado para Atualização** .  

Ao atualizar um ponto de distribuição instalado em um servidor de site secundário do Configuration Manager 2007, o site secundário é desinstalado da hierarquia de origem. Embora este cenário seja chamado de uma atualização de site secundária, ele se aplica somente à função de sistema de site do ponto de distribuição. Como resultado, o site secundário não é atualizado e, em vez disso, é desinstalado. Isso deixa um ponto de distribuição da hierarquia de destino no computador que era o servidor do site secundário. Se você pretende atualizar o ponto de distribuição em um site secundário, consulte [Planejar para atualizar sites secundários do Configuration Manager 2007](#BKMK_UpgradeSS) neste tópico.  

###  <a name="BKIMK_UpgradeProcess"></a> Processo de atualização do ponto de distribuição  
Você pode usar o console do Configuration Manager para atualizar os pontos de distribuição do Configuration Manager 2007 que você compartilhou com a hierarquia de destino. Quando você atualiza um ponto de distribuição compartilhado, o ponto de distribuição é desinstalado do site do Configuration Manager 2007. Em seguida, ele é instalado como um ponto de distribuição que é anexado a um site primário ou secundário que você especifica na hierarquia de destino. O processo de atualização cria uma cópia do conteúdo migrado que é armazenado no ponto de distribuição e converte essa cópia em um single instance content store. Quando o Configuration Manager converte um pacote para o repositório de conteúdo de instância única, ele exclui esse pacote do compartilhamento SMSPKG no computador do ponto de distribuição a menos que o pacote tenha um ou mais anúncios que estão definidos para **Executar programa do ponto de distribuição**.  

Para atualizar o ponto de distribuição, o Configuration Manager usa a **Conta de Acesso do Site de Origem** que está configurada para coletar dados do Provedor de SMS do site de origem. Embora essa conta requeira apenas permissão de **Leitura** de objetos do site para coletar dados do site de origem, ela também deve ter as permissões **Excluir** e **Modificar** para a classe **Site** para remover com êxito o ponto de distribuição do site do Configuration Manager 2007 durante a atualização.  

> [!NOTE]  
>  O Configuration Manager pode converter o conteúdo para o single instance store em apenas um ponto de distribuição por vez. Quando você configura várias atualizações de pontos de distribuição, eles são enfileirados para a atualização e processados ​​um de cada vez.  

Para atualizar um ponto de distribuição compartilhado, verifique se todo o conteúdo implantado no ponto de distribuição é migrado. O conteúdo que você não migrar antes de atualizar o ponto de distribuição não estará disponível na hierarquia de destino após a atualização. Quando você atualiza um ponto de distribuição, o conteúdo dos pacotes migrados é convertido em um formato compatível com o single instance store da hierarquia de destino.  

Para atualizar um ponto de distribuição por meio do console do Configuration Manager, o servidor do sistema de sites do Configuration Manager 2007 deve atender às seguintes condições:  

-   A configuração do ponto de distribuição e o local devem ser qualificados para atualização.  

-   O computador do ponto de distribuição deve ter espaço em disco suficiente para que o conteúdo seja convertido do formato de armazenamento de conteúdo do Configuration Manager 2007 em um formato single instance store. Essa conversão necessita de espaço disponível em disco livre igual ao tamanho do maior pacote armazenado no ponto de distribuição.  

-   O computador do ponto de distribuição deve executar uma versão do sistema operacional que tenha suporte como um ponto de distribuição na hierarquia de destino.  

    > [!NOTE]  
    >  Quando o Configuration Manager verifica a elegibilidade de um ponto de distribuição para atualização, ele não valida a versão do sistema operacional do computador do ponto de distribuição.  

Para atualizar um ponto de distribuição, no espaço de trabalho **Administração**, expanda **Migração**, expanda o nó **Hierarquia de Origem** e, em seguida, selecione o site que contém o ponto de distribuição que você deseja atualizar. Em seguida, no painel de detalhes, na guia **Pontos de Distribuição Compartilhados** , selecione o ponto de distribuição que você quer atualizar.  

Você pode verificar se o ponto de distribuição está pronto para atualização exibindo o status na coluna **Qualificado para Reatribuição** .  Em seguida, na faixa de opções do console do Configuration Manager, na guia **Pontos de Distribuição**, no grupo **Ponto de Distribuição**, selecione **Transferir**. Isso abre um assistente que você usa para concluir a atualização do ponto de distribuição.  

Ao atualizar um ponto de distribuição compartilhado, você deve atribuir o ponto de distribuição a um site primário ou secundário de sua escolha na hierarquia de destino. Depois que o ponto de distribuição é atualizado, você o gerencia como um ponto de distribuição na hierarquia do destino da mesma maneira que qualquer outro ponto de distribuição.  

Você pode monitorar o progresso de uma atualização de ponto de distribuição no console do Configuration Manager selecionando o nó **Migração do Ponto de Distribuição** no nó **Migração** do espaço de trabalho **Administração**. Você também pode exibir informações no **Migmctrl.log** , no servidor do site de administração central da hierarquia de destino, ou no **distmgr.log** no servidor do site na hierarquia de destino que controla o ponto de distribuição atualizado.  

> [!NOTE]  
>  Quando você atualiza um ponto de distribuição na hierarquia de destino, a função do sistema de sites do ponto de distribuição é removida do site de origem do Configuration Manager 2007. No entanto, os pacotes enviados para o ponto de distribuição não são atualizados na hierarquia do Configuration Manager 2007. No console do Configuration Manager 2007, os pacotes que haviam sido enviados para o ponto de distribuição continuam a listar o computador do sistema de sites como um ponto de distribuição com um **Tipo** **Desconhecido**. Atualizações subsequentes do pacote no Configuration Manager 2007 resultam em erros de relatórios do Gerenciador de Distribuição no distmgr.log desse site quando o site tenta atualizar o pacote no sistema de sites desconhecido.  

Se você decidir não atualizar um ponto de distribuição compartilhado, ainda poderá instalar um ponto de distribuição da hierarquia de destino em um antigo ponto de distribuição do Configuration Manager 2007. Para instalar o novo ponto de distribuição, você deve primeiro desinstalar todas as funções do sistema de sites do Configuration Manager 2007 do computador do ponto de distribuição. Isso incluirá o site do Configuration Manager 2007 se ele for o computador do servidor do site. Quando você desinstala um ponto de distribuição do Configuration Manager 2007, o conteúdo implantado no ponto de distribuição não é excluído do computador.  

###  <a name="BKMK_UpgradeSS"></a> Planejar para atualizar sites secundários do Configuration Manager 2007  
 Quando você usa a migração para atualizar um ponto de distribuição compartilhado hospedado em um servidor de site secundário do Configuration Manager 2007, o Configuration Manager atualiza a função do sistema de sites do ponto de distribuição para ser um ponto de distribuição na hierarquia de destino. Ele também desinstala o site secundário da hierarquia de origem. O resultado é um ponto de distribuição do System Center Configuration Manager, mas nenhum site secundário.  

 Para que um ponto de distribuição no computador servidor do site seja qualificado para atualização, o Configuration Manager deve ser capaz de desinstalar o site secundário e cada uma das funções do sistema de sites nesse computador. Geralmente, um ponto de distribuição compartilhado em um servidor compartilhado do Configuration Manager 2007 é qualificado para atualização. No entanto, quando um compartilhamento de servidor existe no servidor do site secundário, o site secundário e quaisquer pontos de distribuição compartilhados naquele computador não são elegíveis para atualização. Isso porque o compartilhamento do servidor é tratado como um objeto adicional do sistema de sites, quando o processo tenta desinstalar o site secundário e esse processo não pode desinstalar esse objeto. Nesse cenário, você pode ativar um ponto de distribuição padrão no servidor do site secundário e depois redistribuir o conteúdo a esse ponto de distribuição padrão. Esse processo não usa largura de banda de rede e, quando concluído, você pode desinstalar o ponto de distribuição no compartilhamento do servidor, remover o compartilhamento do servidor e depois atualizar o ponto de distribuição e o site secundário.  

 Para atualizar um ponto de distribuição compartilhado, examine a configuração do ponto de distribuição no Configuration Manager 2007 para evitar a atualização de um ponto de distribuição em um site secundário que você ainda queira usar com o Configuration Manager 2007. Essa é uma boa prática, porque depois de atualizar um ponto de distribuição compartilhado que está em um servidor de site secundário, o servidor do sistema do sites é retirado da hierarquia do Configuration Manager 2007 e não fica mais disponível para uso com essa hierarquia. Quando o site secundário é removido, quaisquer pontos de distribuição restantes nesse site secundário ficam órfãos. Isso significa que eles se tornam não gerenciados do Configuration Manager 2007 e não são mais compartilhados ou qualificados para atualização.  

> [!WARNING]  
>  Quando você exibe pontos de distribuição compartilhados no console do Configuration Manager, não há nenhuma indicação visível de que um ponto de distribuição compartilhado está em um servidor do sistema de sites remoto ou no servidor do site secundário.  

 Quando existe um site secundário em um local de rede remoto que é usado principalmente para controlar a implantação de conteúdo nesse local remoto, considere atualizar sites secundários que têm um ponto de distribuição compartilhado. Como é possível configurar o controle de largura de banda para quando você distribui o conteúdo para um ponto de distribuição do System Center Configuration Manager, muitas vezes você pode atualizar um site secundário para um ponto de distribuição, configurar o ponto de distribuição para controles de largura de banda e evitar a instalação de um site secundário nesse local de rede na hierarquia de destino.  

 O processo para atualizar um ponto de distribuição compartilhado em um servidor de site secundário é o mesmo que qualquer outra atualização do ponto de distribuição compartilhado. O conteúdo é copiado e convertido para o single instance store em uso pela hierarquia de destino. No entanto, quando você atualiza um ponto de distribuição compartilhado que está em um servidor de site secundário, o processo de atualização também desinstala o ponto de gerenciamento, se estiver presente e, em seguida, desinstala o site secundário do servidor. O resultado é que o site secundário é removido da hierarquia do Configuration Manager 2007. Para desinstalar o site secundário, o Configuration Manager usa a conta que é configurada para coletar dados do site de origem.  

 Durante a atualização, existe um atraso entre quando o site secundário do Configuration Manager 2007 é desinstalado e quando a instalação do ponto de distribuição na hierarquia de destino começa. O ciclo de coleta de dados determina esse atraso de até quatro horas. O atraso tem por objetivo proporcionar tempo para o site secundário ser desinstalado antes que a nova instalação do ponto de distribuição comece.  

 Para saber mais sobre como atualizar um ponto de distribuição compartilhado, consulte [Planejar para atualizar pontos de distribuição compartilhados do Configuration Manager 2007](#Planning_to_Upgrade_DPs).  

##  <a name="BKMK_ReassignDistPoint"></a> Planejar para transferir pontos de distribuição do System Center Configuration Manager  
 Ao migrar de uma versão com suporte do System Center 2012 Configuration Manager para uma hierarquia da mesma versão, você pode reatribuir um ponto de distribuição compartilhado da hierarquia de origem a um site na hierarquia de destino. Isso é semelhante ao conceito de atualizar um ponto de distribuição do Configuration Manager 2007 para se tornar um ponto de distribuição na hierarquia de destino. É possível transferir pontos de distribuição de sites primários e secundários. A ação de transferir um ponto de distribuição remove o ponto de distribuição da hierarquia de origem e torna o computador e seu ponto de distribuição um servidor de sistema de sites do site que você selecionou na hierarquia de destino.  

 Quando você reatribui um ponto de distribuição, não é necessário redistribuir conteúdo migrado que estava hospedado no ponto de distribuição do site de origem. Além disso, ao contrário da atualização de um ponto de distribuição do Configuration Manager 2007, a reatribuição de um ponto de distribuição não requer espaço em disco adicional no computador do ponto de distribuição. Isso ocorre porque, a partir do System Center 2012 Configuration Manager, os pontos de distribuição usam o formato single instance store para conteúdo. O conteúdo no computador do ponto de distribuição não precisa ser convertido quando o ponto de distribuição é transferido entre hierarquias.  

 Para que um ponto de distribuição do System Center 2012 Configuration Manager seja qualificado para reatribuição, ele deve atender aos seguintes critérios:  

-   Um ponto de distribuição compartilhado deve ser instalado em um computador diferente do servidor do site.  

-   Um ponto de distribuição compartilhado não pode ser co-localizado com funções adicionais do sistema de site.  

Para identificar os pontos de distribuição qualificados para reatribuição no console do Configuration Manager no nó **Hierarquia de Origem**, selecione um site de origem e a guia **Pontos de Distribuição Compartilhados**. Os pontos de distribuição qualificados exibem **Sim** na coluna **Qualificado para Transferência** (essa coluna se chamava **Qualificado para Atualização** antes do System Center 2012 R2 Configuration Manager).  

###  <a name="BKMK_ReassignProcess"></a> Processo de reatribuição de pontos de distribuição  
 Você pode usar o console do Configuration Manager para reatribuir pontos de distribuição que você compartilhou de uma hierarquia de origem ativa. Quando você transfere um ponto de distribuição compartilhado, o ponto de distribuição é desinstalado do site de origem e instalado como um ponto de distribuição anexado a um site primário ou secundário que você especifica na hierarquia de destino.  

 Para transferir o ponto de distribuição, a hierarquia de destino usa a Conta de Acesso do Site de Origem configurada para coletar dados do Provedor de SMS do site de origem. Para obter informações sobre as permissões necessárias e pré-requisitos adicionais, confira [Prerequisites for migration in System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md) (Pré-requisitos para migração no System Center Configuration Manager).  

## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar vários pontos de distribuição compartilhados ao mesmo tempo
A partir da versão 1610, você pode usar **Transferir Ponto de Distribuição** para que Configuration Manager processe em paralelo a transferência de até 50 pontos de distribuição compartilhados ao mesmo tempo. Isso inclui pontos de distribuição compartilhados de sites de origem com suporte que executam:  
- Configuration Manager 2007
- System Center 2012 Configuration Manager
- System Center 2012 R2 Configuration Manager
- System Center Configuration Manager (Branch Atual)

Quando você transfere os pontos de distribuição, cada ponto de distribuição deve estar qualificado para ser atualizado ou transferido. O nome da ação e do processo envolvidos (atualizar ou transferir) depende de qual versão do Configuration Manager o site de origem executa. Os resultados finais para as duas ações são os mesmos: o ponto de distribuição é atribuído a um de seus sites do Branch Atual com seu conteúdo no local.

Antes da versão 1610, o Configuration Manager podia processar apenas um ponto de distribuição por vez. Agora, você pode transferir quantos pontos de distribuição desejar com as seguintes ressalvas:  
- Embora você não possa selecionar vários pontos de distribuição para serem transferidos, quando tiver colocado mais de um em fila, o Configuration Manager os processará em paralelo em vez de esperar completar um antes de iniciar o próximo.  
- Por padrão, são processados até 50 pontos de distribuição em paralelo de uma vez. Após a conclusão da transferência do primeiro ponto de distribuição, o Configuration Manager começará a processar o 51º e assim por diante.  
- Quando você usa o SDK do Configuration Manager, pode alterar a **SharedDPImportThreadLimit** para ajustar o número de pontos de distribuição transferidos que o Configuration Manager pode processar em paralelo.


##  <a name="About_Migrating_Content"></a> Atribuir propriedade do conteúdo durante a migração de conteúdo  
 Ao migrar conteúdo para implantações, você deverá atribuir o objeto do conteúdo a um site na hierarquia de destino. Esse site, então, torna-se o proprietário desse conteúdo na hierarquia de destino. Embora o site de nível superior da hierarquia de destino seja o site que migra os metadados de conteúdo, é o site atribuído que usa os arquivos de origem originais de conteúdo em toda a rede.  

 Para minimizar a largura de banda de rede usada quando você migra conteúdo, considere transferir a propriedade do conteúdo para um site na hierarquia de destino que está fechada na rede para o local de conteúdo na hierarquia de origem. Como as informações de conteúdo na hierarquia de destino são compartilhadas globalmente, elas estarão disponíveis em todos os sites.  

 Embora as informações de conteúdo sejam compartilhadas com todos os sites usando a replicação de banco de dados, qualquer conteúdo que você atribui a um site primário e depois implanta nos pontos de distribuição em outros sites primários é transferido por meio da replicação baseada em arquivo. Essa transferência é roteada através do site de administração central e, em seguida, para o site primário adicional. É possível reduzir a transferência de dados por meio de redes de baixa largura de banda ao centralizar pacotes que você pretende distribuir para vários sites primários antes ou durante a migração quando você atribui um site como o proprietário do conteúdo.
