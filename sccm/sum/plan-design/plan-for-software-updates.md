---
title: Planejar atualizações de software
titleSuffix: Configuration Manager
description: É essencial ter um plano para a infraestrutura de ponto de atualização de software antes de usar atualizações de software em um ambiente de produção do Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.collection: M365-identity-device-management
ms.openlocfilehash: 730d99764f8ae8f8ce1b76bfd13411988c3a2e23
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138530"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>Planejar atualizações de software no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de usar atualizações de software em um ambiente de produção do Configuration Manager, é importante que você passe pelo processo de planejamento. Ter um bom plano para a infraestrutura de ponto de atualização de software é fundamental para uma implementação bem-sucedida das atualizações de software.



## <a name="capacity-planning-recommendations-for-software-updates"></a>Recomendações de planejamento de capacidade para atualizações de software  

Esta seção inclui os seguintes subtópicos:  
- [Planejamento de capacidade para o ponto de atualização de software](#BKMK_SUMCapacity)
- [Planejamento de capacidade para objetos de atualização de software](#bkmk_sum-capacity-obj)  


Use as seguintes recomendações como uma linha de base. Essa linha de base ajuda a determinar as informações para o planejamento da capacidade de atualizações de software que são apropriadas para sua organização. Os requisitos reais de capacidade podem variar em relação às recomendações listadas neste artigo, dependendo dos critérios a seguir: 
- Seu ambiente de rede específico
- O hardware que você usa para hospedar o sistema de sites do ponto de atualização de software
- O número de clientes gerenciados
- As outras funções do sistema de sites instaladas no servidor  


###  <a name="BKMK_SUMCapacity"></a> Planejamento de capacidade para o ponto de atualização de software  

O número de clientes com suporte depende da versão do WSUS (Windows Server Update Services) executada no ponto de atualização de software. Ele também depende se a função do sistema de sites do ponto de atualização de software coexiste com outra função do sistema de sites:  

-   O ponto de atualização de software pode dar suporte a até 25 mil clientes quando o WSUS é executado no servidor do ponto de atualização de software e o ponto de atualização de software coexiste com outra função do sistema de sites.  

-   O ponto de atualização de software pode dar suporte a até 150 mil clientes quando o servidor remoto atende aos requisitos do WSUS. O WSUS é usado com o Configuration Manager e você define as seguintes configurações:

    Pool de Aplicativos do IIS:
    - Aumentar o Comprimento da Fila de WsusPool para 2000
    - Aumente quatro vezes o limite de memória particular do WsusPool ou defina-o como 0 (ilimitado). Por exemplo, se o limite padrão for 1.843.200 KB aumente-o para 7.372.800. Para obter mais informações, confira esta [postagem no blog da equipe de suporte do Configuration Manager](https://blogs.technet.microsoft.com/configurationmgr/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    Para obter mais informações sobre os requisitos de hardware para o ponto de atualização de software, confira [Hardware recomendado para sistemas de sites](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems).  


### <a name="bkmk_sum-capacity-obj"></a> Planejamento de capacidade para objetos de atualização de software  

Use as seguintes informações de capacidade para planejar objetos de atualizações de software:  

#### <a name="limit-of-1000-software-updates-in-a-deployment"></a>Limite de 1000 atualizações de software em uma implantação  
Limite o número de atualizações de software a 1000 para cada implantação de atualização de software. Ao criar uma ADR (regra de implantação automática), especifique os critérios que limitam o número de atualizações de software. A ADR falha quando os critérios especificados retornam mais de 1000 atualizações de software. Verifique o status da ADR no nó **Regras de Implantação Automática** no console do Configuration Manager. Ao implantar atualizações de software manualmente, não selecione mais de 1000 atualizações para serem implantadas.  

Limite também o número de atualizações de software a 1000 em uma linha de base de configuração. Para obter mais informações, consulte [Criar linhas de base de configuração](/sccm/compliance/deploy-use/create-configuration-baselines).



##  <a name="BKMK_SUPInfrastructure"></a> Determinar a infraestrutura do ponto de atualização de software  

Esta seção inclui os seguintes subtópicos:    
- [Lista de pontos de atualização de software](#BKMK_SUPList)
- [Mudança de ponto de atualização de software](#BKMK_SUPSwitching)
- [Mudar clientes manualmente para um novo ponto de atualização de software](#BKMK_ManuallySwitchSUPs)
- [Pontos de atualização de software em uma floresta não confiável](#BKMK_SUP_CrossForest)
- [Usar um servidor WSUS existente como a origem de sincronização no site de nível superior](#BKMK_WSUSSyncSource)
- [Ponto de atualização de software em um site secundário](#BKMK_SUPSecSite)  
- [Planejar clientes baseados na Internet](#bkmk_internet-clients)  
- [Planejar o conteúdo de atualização de software](#bkmk_content)  
- [Planejar atualizações de terceiros](#bkmk_thirdparty)  


O site de administração central e todos os sites primários filho precisam ter um ponto de atualização de software. Ao planejar a infraestrutura de ponto de atualização de software, determine as seguintes dependências:
 - Onde instalar o ponto de atualização de software do site  
 - Quais sites exigem um ponto de atualização de software que aceita a comunicação de clientes baseados na Internet
 - Se você precisa de um ponto de atualização de software em sites secundários  

> [!IMPORTANT]  
>  Para obter mais informações sobre as dependências internas e externas necessárias para as atualizações de software, confira [Pré-requisitos para atualizações de software](prerequisites-for-software-updates.md).  

Adicione vários pontos de atualização de software em um site primário do Configuration Manager para fornecer tolerância a falhas. O design de failover do ponto de atualização de software é diferente do modelo aleatório puro usado no design de pontos de gerenciamento. Ao contrário do design de pontos de gerenciamento, há custos de desempenho de rede e do cliente no design de ponto de atualização de software, quando os clientes mudam para um novo ponto de atualização de software. Quando o cliente muda para um novo servidor do WSUS para verificar atualizações de software, o resultado é um aumento no tamanho do catálogo e no lado do cliente associado, e nas demandas de desempenho de rede. Portanto, o cliente preserva a afinidade com o último ponto de atualização de software que ele verificou com êxito.  

O primeiro ponto de atualização de software que você instala em um site primário é a origem da sincronização de todos os pontos de atualização de software que você adiciona ao site primário. Depois de adicionar pontos de atualização de software e iniciar a sincronização, exiba o status dos pontos de atualização de software e a origem da sincronização no nó **Status de sincronização do ponto de atualização de software** no workspace **Monitoramento**.  

Quando houver uma falha do ponto de atualização de software configurado como a origem de sincronização para o site, remova manualmente a função com falha. Em seguida, selecione um novo ponto de atualização de software a ser usado como a origem da sincronização. Para obter mais informações, confira [Remover a função do sistema de sites do ponto de atualização de software](../get-started/remove-a-software-update-point.md).  


###  <a name="BKMK_SUPList"></a> Lista de pontos de atualização de software  

O Configuration Manager fornece ao cliente uma lista de pontos de atualização de software nos seguintes cenários:  

- Um novo cliente recebe a política para habilitar atualizações de software  

- Um cliente não pode contatar seu ponto de atualização de software atribuído e precisa mudar para outro  

O cliente seleciona aleatoriamente um ponto de atualização de software na lista. Ele prioriza os pontos de atualização de software na mesma floresta. O Configuration Manager fornece aos clientes uma lista diferente dependendo do tipo de cliente:  

-   **Clientes baseados em intranet**: Recebem uma lista de pontos de atualização de software que você pode configurar para permitir conexões somente da intranet ou uma lista de pontos de atualização de software que permitem conexões do cliente na Internet e na intranet.  

-   **Clientes baseados na Internet**: Recebem uma lista de pontos de atualização de software que você pode configurar para permitir conexões somente da Internet ou uma lista de pontos de atualização de software que permitem conexões do cliente na Internet e na intranet.  


###  <a name="BKMK_SUPSwitching"></a> Mudança de ponto de atualização de software  

> [!NOTE]  
> Os clientes usam grupos de limites para encontrar um novo ponto de atualização de software. Se o ponto de atualização de software atual não estiver mais acessível, eles também usarão grupos de limites para fazer fallback e localizar um novo ponto. Adicione pontos de atualização de software individuais a grupos de limites diferentes para controlar quais servidores um cliente pode encontrar. Para obter mais informações, confira [Pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).  

Se houver vários pontos de atualização de software em um site e um deles falhar ou não ficar disponível, os clientes se conectarão a um ponto de atualização de software diferente. Com esse novo servidor, os clientes continuam a procurar as atualizações de software mais recentes. Quando um cliente é atribuído a um ponto de atualização de software pela primeira vez, ele permanece atribuído a esse ponto de atualização de software, a menos que ele não consiga verificar.  

A verificação de atualizações de software pode falhar com um número de repetição diferente e códigos de erro sem repetição. Quando há falha na verificação para repetir um código de erro, o cliente inicia o processo de repetição para verificar as atualizações de software no ponto de atualização de software. As condições de alto nível que resultam em na repetição de um código de erro geralmente ocorrem porque o servidor do WSUS está indisponível ou temporariamente sobrecarregado. Quando o cliente não consegue verificar atualizações de software, ele usa o seguinte processo:  

1.  O cliente verifica se há atualizações de software:  
    - Em seu horário agendado
    - Ao ser executado manualmente no painel de controle no cliente
    - Ao ser executado manualmente no console do Configuration Manager por meio de uma ação de notificação do cliente
    - Ao ser executado de um método do SDK do Configuration Manager  

2.  Quando a verificação falha, o cliente espera 30 minutos para repetir a verificação. Ele usa o mesmo ponto de atualização de software.  

3.  O cliente tenta novamente no mínimo quatro vezes a cada 30 minutos. Após a quarta falha e depois de esperar mais dois minutos, o cliente passa para o próximo ponto de atualização de software em sua lista.  

4.  O cliente repete esse processo com o novo ponto de atualização de software. Após uma verificação bem-sucedida, o cliente continua a conectar-se ao novo ponto de atualização de software.  

A lista a seguir fornece informações adicionais a serem consideradas para repetição de ponto de atualização de software e mudança de cenários:  

-   Se um cliente é desconectado da intranet e não consegue verificar se há atualizações de software, ele não muda para outro ponto de atualização de software. Essa falha é esperada, pois o cliente não consegue acessar a rede interna ou um ponto de atualização de software que permite conexões da intranet. O cliente do Configuration Manager determina a disponibilidade do ponto de atualização de software da intranet.  

-   Se você estiver gerenciando clientes na Internet e tiver configurado vários pontos de atualização de software para aceitar a comunicação de clientes na Internet, o processo de mudança seguirá o processo de repetição padrão já descrito.  

-   Se o processo de verificação for iniciado, mas o cliente for desligado antes da conclusão da verificação, isso não será considerado uma falha de verificação e não contará como uma das quatro repetições.  

Quando o Configuration Manager receber um dos seguintes códigos de erro do Windows Update Agent, o cliente tentará a conexão novamente:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Para pesquisar o significado de um código de erro, converta o código de erro decimal em hexadecimal e pesquise o valor hexadecimal em um site como o [Wiki Windows Update Agent – Error Codes](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx) (Windows Update Agent – Códigos de Erro). Por exemplo, o código de erro decimal 2149842970 é o hexadecimal 8024001A, o que significa WU_E_POLICY_NOT_SET Não foi definido um valor de política.  


###  <a name="BKMK_ManuallySwitchSUPs"></a> Mudar clientes manualmente para um novo ponto de atualização de software

Mude clientes do Configuration Manager para um novo ponto de atualização de software quando houver problemas com o ponto de atualização de software ativo. Essa alteração somente ocorre quando um cliente recebe vários pontos de atualização de software de um ponto de gerenciamento.

> [!IMPORTANT]    
> Quando você alternar os dispositivos para usar um novo servidor, os dispositivos usam fallback para localizar esse novo servidor. Antes de iniciar essa alteração, examine suas configurações de grupo de limites para verificar se os pontos de atualização de software estão nos grupos de limites corretos. Para obter mais informações, confira [Pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).  
>
> A mudança para um novo ponto de atualização de software aumenta o tráfego de rede. A quantidade de tráfego depende das definições de configuração do WSUS, por exemplo, as classificações e os produtos sincronizados ou uso de um banco de dados do WSUS compartilhado. Se você planeja mudar vários dispositivos, considere a possibilidade de fazer isso durante as janelas de manutenção. Esse período permitirá reduzir o impacto na rede quando os clientes verificarem o novo ponto de atualização de software.  

#### <a name="process-to-switch-software-update-points"></a>Processo de mudar de pontos de atualização de software  
Inicie essa alteração em uma coleção de dispositivos. Depois ela for disparada, os clientes procurarão outro ponto de atualização de software na próxima verificação.  

1.  No console do Configuration Manager, acesse o workspace **Ativos e Conformidade** e escolha o nó **Coleções de Dispositivos**.  

2.  Selecione a coleção de destino. Na guia **Início** da faixa de opções, no grupo **Coleção**, clique em **Notificação do Cliente** e em **Mudar para o próximo ponto de atualização de software**.  


###  <a name="BKMK_SUP_CrossForest"></a> Pontos de atualização de software em uma floresta não confiável  

Crie um ou mais pontos de atualização de software em um site para dar suporte a clientes em uma floresta não confiável. Para adicionar um ponto de atualização de software em outra floresta, primeiro instale e configure um servidor WSUS nessa floresta. Depois, inicie o assistente para adicionar um servidor do site do Configuration Manager com a função de sistema de sites do ponto de atualização de software. No assistente, defina as seguintes configurações para se conectar com êxito ao WSUS na floresta não confiável:  

-   Especifique uma **conta de instalação do sistema de sites** que possa acessar o servidor WSUS na floresta não confiável.  

-   Especifique uma **conta de conexão com o servidor WSUS** para conectar-se ao servidor WSUS.  

Por exemplo, você tem um site primário na floresta A com dois pontos de atualização de software (SUP01 e SUP02). Para o mesmo site primário, também há dois pontos de atualização de software (SUP03 e SUP04) na floresta B. Ao mudar para o próximo ponto de atualização de software, os clientes priorizam os servidores da mesma floresta.  


###  <a name="BKMK_WSUSSyncSource"></a> Usar um servidor WSUS existente como a origem de sincronização no site de nível superior  

Normalmente, o site de nível superior na sua hierarquia é configurado para sincronizar metadados de atualizações de software com o Microsoft Update. Se a política de segurança da organização não permite que o site de nível superior acesse a Internet, configure a origem da sincronização do site de nível superior para usar um servidor WSUS existente. Esse servidor WSUS não está na hierarquia do Configuration Manager. Por exemplo, há um servidor WSUS em uma rede conectada à Internet (DMZ), mas o site de nível superior está em uma rede interna sem acesso à Internet. Configure o servidor WSUS no DMZ como a origem da sincronização dos metadados de atualizações de software. Configure o servidor WSUS na DMZ para sincronizar atualizações de software com os mesmos critérios que você precisa no Configuration Manager. Caso contrário, o site de nível superior pode não sincronizar as atualizações de software que você espera. Ao instalar o ponto de atualização de software, configure uma conta de conexão com o servidor WSUS. Essa conta precisa de acesso ao servidor WSUS na DMZ. Além disso, confirme se o firewall permite tráfego para as portas apropriadas. Para obter mais informações, confira as [portas usadas pelo ponto de atualização de software para a origem da sincronização](/sccm/core/plan-design/hierarchy/ports#BKMK_PortsSUP-WSUS).  


###  <a name="BKMK_SUPSecSite"></a> Ponto de atualização de software em um site secundário  

O ponto de atualização de software é opcional em um site secundário. Instale somente um ponto de atualização de software em um site secundário. Quando um ponto de atualização de software não está instalado no site secundário, os dispositivos dentro dos limites de um site secundário usam um ponto de atualização de software em seu site primário atribuído. Geralmente se instala um ponto de atualização de software em um site secundário quando a largura de banda de rede é limitada entre os dispositivos no site secundário e os pontos de atualização de software no site primário pai. Você também pode usar essa configuração quando o ponto de atualização de software no site primário se aproxima do limite de capacidade. Depois que você instala e configura um ponto de atualização de software no site secundário com êxito, uma política para todo o site é atualizada para os clientes e eles começam a usar o novo ponto de atualização de software.  


### <a name="bkmk_internet-clients"></a> Planejar clientes baseados na Internet

Quando você precisar gerenciar dispositivos que saem da rede e usam perfil móvel na Internet, desenvolva um plano para saber como gerenciar atualizações de software nesses dispositivos. O Configuration Manager dá suporte a várias tecnologias para esse cenário. Use uma delas ou uma combinação, conforme o necessário, para atender aos requisitos da sua organização.

#### <a name="cloud-management-gateway"></a>Gateway de gerenciamento de nuvem
Crie um Gateway de Gerenciamento de Nuvem no Microsoft Azure e habilite pelo menos um ponto de atualização de software local para permitir o tráfego de clientes baseados na Internet. Conforme os clientes usam um perfil móvel na Internet, eles continuam a verificar os pontos de atualização de software. Todos os clientes baseados na Internet sempre obtêm conteúdo do serviço de nuvem do Microsoft Update. 

Para obter mais informações, confira [Planejar o Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

#### <a name="internet-based-client-management"></a>Gerenciamento de clientes baseado na Internet
Coloque um ponto de atualização de software em uma rede para a Internet e habilite-o para permitir o tráfego de clientes baseados na Internet. Conforme os clientes usam um perfil móvel na Internet, eles mudam para esse pontos de atualização de software para fazer a verificação. Todos os clientes baseados na Internet sempre obtêm conteúdo do serviço de nuvem do Microsoft Update.

Para obter mais informações sobre as vantagens e desvantagens do gerenciamento de clientes baseados na Internet, confira [Gerenciar clientes na Internet](/sccm/core/clients/manage/manage-clients-internet).

#### <a name="windows-update-for-business"></a>Windows Update for Business
O Windows Update para Empresas permite que você mantenha dispositivos Windows 10 sempre atualizados com as atualizações de recurso e de qualidade mais recentes. Esses dispositivos conectam-se diretamente ao serviço de nuvem do Windows Update. O Configuration Manager pode diferenciar entre os computadores Windows 10 que usam o WUfB e o WSUS para obter atualizações de software.

Para obter mais informações, confira [Integração com o Windows Update para Empresas](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10).


### <a name="bkmk_content"></a> Planejar o conteúdo de atualização de software

Os clientes precisam baixar os arquivos de conteúdo das atualizações de software para instalá-los. O Configuration Manager fornece várias tecnologias para dar suporte ao gerenciamento e à entrega desse conteúdo. Ou configure as implantações de atualização de software para permitir ou exigir que os clientes obtenham o conteúdo diretamente do serviço de nuvem do Microsoft Update.

#### <a name="download-and-distribute-content"></a>Baixar e distribuir conteúdo 
Por padrão, o processo de gerenciamento de atualizações de software no Configuration Manager usa os recursos internos de gerenciamento de conteúdo. Esses recursos incluem a biblioteca de conteúdo do repositório de instância única centralizado e o design distribuído da função do sistema de sites do ponto de distribuição. É possível usar esses recursos ao baixar e distribuir pacotes de implantação de atualização de software. 

Para obter mais informações, confira [Baixar atualizações de software](/sccm/sum/deploy-use/download-software-updates).

#### <a name="manage-express-installation-files-for-windows-10"></a>Gerenciar arquivos de instalação expressa para Windows 10
O Configuration Manager dá suporte ao uso de arquivos de instalação expressa para atualizações do Windows 10. Os arquivos de atualização expressa e as tecnologias de suporte, como a Otimização de Entrega, podem ajudar a reduzir o impacto na rede causado pelo download de arquivos grandes de conteúdo para os clientes. 

Para obter mais informações, confira [Otimizar a entrega de atualização do Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).

#### <a name="clients-download-content-from-the-internet"></a>Os clientes baixam o conteúdo da Internet
Quando você implantar atualizações de software para clientes, configure a implantação para que os clientes baixem o conteúdo do serviço de nuvem do Microsoft Update. Quando os clientes não conseguirem baixar o conteúdo de outra fonte de conteúdo, eles ainda poderão baixar o conteúdo da Internet. 

Começando na versão 1806, você não precisa mais criar um pacote de implantação ao implantar atualizações de software. Quando você seleciona a opção **Nenhum pacote de implantação**, os clientes ainda podem baixar o conteúdo de fontes locais, se disponível, mas normalmente eles baixam do serviço Microsoft Update.<!--1357933-->

Os clientes baseados na Internet sempre baixam o conteúdo do serviço de nuvem do Microsoft Update. Não distribua pacotes de implantação de atualização de software para um ponto de distribuição na nuvem. Você será cobrado pelo armazenamento com o ponto de distribuição na nuvem, mas os clientes não baixarão esses pacotes. 


### <a name="bkmk_thirdparty"></a> Planejar atualizações de terceiros
O Configuration Manager integra-se com o WSUS, que dá suporte nativo às atualizações de software publicadas pela Microsoft. A maioria dos clientes usa outros aplicativos de terceiros que também precisam de atualizações. Há várias opções a serem consideradas para manter os aplicativos de terceiros atualizado.

#### <a name="supersede-applications-to-update"></a>Substituir aplicativos a serem atualizados
Use uma relação de substituição com o recurso de gerenciamento de aplicativos no Configuration Manager para atualizar ou substituir os aplicativos existentes. Ao substituir um aplicativo, especifique um novo tipo de implantação para substituir o tipo de implantação do aplicativo substituído. Também decida se deseja atualizar ou desinstalar o aplicativo substituído antes que o aplicativo substituto seja instalado.

Para obter mais informações, confira [Revisar e substituir aplicativos](/sccm/apps/deploy-use/revise-and-supersede-applications).

#### <a name="third-party-software-updates"></a>Atualizações de software de terceiros
Começando na versão 1806, é possível usar o nó **Catálogos de Atualização de Software de Terceiros** no console do Configuration Manager para assinar catálogos de terceiros, publicar as atualizações em seu ponto de atualização de software e, em seguida, implantá-las nos clientes.<!--1352101-->

Para obter mais informações, confira [Atualizações de software de terceiros](/sccm/sum/deploy-use/third-party-software-updates).

#### <a name="system-center-updates-publisher"></a>System Center Updates Publisher
O SCUP (System Center Updates Publisher) é uma ferramenta autônoma que permite que os fornecedores de software independentes ou os desenvolvedores de aplicativos de linha de negócios gerenciem atualizações personalizadas. Essas atualizações incluem as que têm dependências, como drivers e pacotes de atualização.

Para obter mais informações, confira [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).



##  <a name="BKMK_SUPInstallation"></a> Planejar a instalação do ponto de atualização de software  

Esta seção inclui os seguintes subtópicos:  
- [Requisitos para o ponto de atualização de software](#BKMK_SUPSystemRequirements)
- [Planejar a instalação do WSUS](#BKMK_PlanningForWSUS)
- [Configurar firewalls](#BKMK_ConfigureFirewalls)  


Esta seção fornece informações sobre as etapas a seguir para planejar e preparar a instalação do ponto de atualização de software com êxito. Antes de criar uma função do sistema de sites para o ponto de atualização de software no Configuration Manager, há vários requisitos a serem considerados. Os requisitos específicos dependem da infraestrutura do Configuration Manager. É importante que você examine esta seção ao configurar o ponto de atualização de software para comunicar-se usando HTTPS. Os servidores habilitado para HTTPS exigem etapas adicionais para que funcionem corretamente.  

###  <a name="BKMK_SUPSystemRequirements"></a> Requisitos para o ponto de atualização de software  

Instale a função de ponto de atualização de software em um sistema de sites que atenda aos requisitos mínimos do WSUS e às configurações compatíveis com os sistemas de sites do Configuration Manager.  

-   Para obter mais informações sobre os requisitos mínimos para a função de servidor WSUS no Windows Server, confira [Examinar as considerações e os requisitos de sistema](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#BKMK_1.1).  

-   Para obter mais informações sobre as configurações com suporte para sistemas de sites do Configuration Manager, consulte [Pré-requisitos de site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


###  <a name="BKMK_PlanningForWSUS"></a> Planejar a instalação do WSUS  

Instale uma versão com suporte do WSUS em todos os servidores do sistema de sites que você configurar para a função de ponto de atualização de software. Quando você não instalar o ponto de atualização de software no servidor do site, instale o Console de Administração do WSUS no servidor do site. Esse componente permite que o servidor do site se comunique com o WSUS que é executado no ponto de atualização de software.  

Quando você usar o WSUS no Windows Server 2012 ou posteriores, configure permissões adicionais para permitir que o componente **Configuration Manager do WSUS** no Configuration Manager se conecte ao WSUS. Esse componente executa verificações de integridade periódicas. Escolha uma das opções a seguir para configurar a permissão necessária:  

-   Adicione a conta **SYSTEM** ao grupo **Administradores do WSUS**  

-   Adicione a conta **NT AUTHORITY\SYSTEM** como um usuário do SUSDB (banco de dados do WSUS). Configure uma associação mínima da função de banco de dados do webService.  
  
Para obter mais informações de como instalar o WSUS no Windows Server, confira [Instalar a função de servidor WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role).  

Quando você instalar mais de um ponto de atualização de software em um site primário, use o mesmo banco de dados do WSUS para cada ponto de atualização de software na mesma floresta do Active Directory. O compartilhamento do mesmo banco de dados melhora o desempenho quando os clientes mudam para um novo ponto de atualização de software. Para obter mais informações, confira [Usar um banco de dados do WSUS compartilhado para pontos de atualização de software](/sccm/sum/plan-design/software-updates-best-practices#bkmk_shared-susdb).  


####  <a name="BKMK_CustomWebSite"></a> Configurar o WSUS para usar um site personalizado  
Ao instalar o WSUS, você tem a opção de usar o site padrão do IIS ou criar um site do WSUS personalizado. Crie um site personalizado para o WSUS para que o IIS hospede os serviços do WSUS em um site virtual dedicado. Caso contrário, ele compartilhará o mesmo site que é usado por outros sistemas de sites ou aplicativos do Configuration Manager. Essa configuração é necessária principalmente quando você instala a função de ponto de atualização de software no servidor do site. Quando você executa o WSUS no Windows Server 2012 ou posteriores, o WSUS é configurado, por padrão, para usar a porta 8530 para HTTP e a porta 8531 para HTTPS. Especifique essas portas ao criar o ponto de atualização de software em um site.  


####  <a name="BKMK_WSUSInfrastructure"></a> Usar uma infraestrutura existente do WSUS  
Selecione um servidor WSUS que estava ativo no seu ambiente antes da instalação do Configuration Manager como um ponto de atualização de software. Quando o ponto de atualização de software for configurado, especifique as configurações de sincronização. O Configuration Manager se conecta ao servidor do WSUS que é executado no servidor do ponto de atualização de software e configura o WSUS com as mesmas configurações. 

Antes de configurar o servidor como um ponto de atualização de software, compare sua configuração de produtos e classificações com as configurações do Configuration Manager. Se você sincronizar o servidor WSUS existente antes de configurá-lo como um ponto de atualização de software e as listas de produtos e classificações forem diferentes, ele sincronizará todos os metadados de atualizações de software, independentemente das configurações definidas. Esse comportamento resulta na presença de metadados de atualizações de software inesperados no banco de dados do site. 

Você experimentará o mesmo comportamento quando adicionar produtos ou classificações diretamente no console de administração do WSUS e, logo em seguida, iniciar a sincronização. Por padrão, a cada hora o Configuration Manager conecta-se ao WSUS e redefine as configurações que foram modificadas fora do Configuration Manager. As atualizações de software que não atenderem aos produtos e às classificações que você especificar nas configurações de sincronização serão definidas como expiradas. Em seguida, elas serão removidas do banco de dados do site.  

Quando um servidor WSUS é configurado como um ponto de atualização de software, ele não pode mais ser usado como um servidor WSUS autônomo. Se você precisar de um servidor WSUS autônomo separado que não seja gerenciado pelo Configuration Manager, configure-o em um servidor diferente.  

####  <a name="BKMK_WSUSAsReplica"></a> Configurar o WSUS como um servidor de réplica  
Ao adicionar a função de ponto de atualização de software em um servidor de site primário, você não pode usar um servidor WSUS configurado como uma réplica. Quando o servidor WSUS é configurado como uma réplica, o Configuration Manager não consegue configurar o servidor WSUS e a sincronização do WSUS falha. O primeiro ponto de atualização de software instalado em um site primário é o ponto de atualização de software padrão. Pontos de atualização de software adicionais no site são configurados como réplicas do ponto de atualização de software padrão.  

####  <a name="BKMK_WSUSandSSL"></a> Decidir se o WSUS deve ser configurado para usar SSL  
Use o protocolo SSL para ajudar a proteger o ponto de atualização de software. O WSUS usa o SSL para autenticar computadores cliente e servidores de WSUS downstream para o servidor do WSUS. Além disso, o WSUS usa SSL para criptografar metadados de atualização de software. Ao optar por proteger o WSUS com SSL, prepare o servidor WSUS antes de instalar o ponto de atualização de software. Para obter mais informações, confira o artigo [Configure SSL on the WSUS server](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL) (Configurar o SSL no servidor WSUS) na documentação do WSUS. 

Ao instalar e configurar o ponto de atualização de software, selecione a opção para **Habilitar comunicações SSL para o servidor WSUS**. Caso contrário, o Configuration Manager configura o WSUS para não usar SSL. Ao habilitar o SSL em um ponto de atualização de software, configure também os pontos de atualização de software nos sites filho para usar SSL.  


###  <a name="BKMK_ConfigureFirewalls"></a> Configurar firewalls  

O ponto de atualização de software no site de administração central do Configuration Manager comunica-se com o WSUS no ponto de atualização de software. O WSUS comunica-se com a origem da sincronização para sincronizar os metadados de atualizações de software. Os pontos de atualização de software em um site filho comunicam-se com o ponto de atualização de software no site pai. Quando há mais de um ponto de atualização de software em um site primário, os pontos de atualização de software adicionais comunicam-se com o ponto de atualização de software padrão. A função padrão é o primeiro ponto de atualização de software que é instalado no site.  

Talvez você precise configurar o firewall para permitir o tráfego HTTP ou HTTPS que o WSUS usa nos seguintes cenários: 
- Entre o ponto de atualização de software e a Internet
- Entre um ponto de atualização de software e sua origem de sincronização upstream
- Entre os pontos de atualização de software adicionais  

A conexão com o Microsoft Update é sempre configurada para usar a porta 80 para HTTP e a porta 443 para HTTPS. Use uma porta personalizada para a conexão do WSUS no ponto de atualização de software em um site filho com o WSUS no ponto de atualização de software no site pai. Quando sua política de segurança não permitir a conexão, use o método de sincronização de exportação e importação. Para obter mais informações, consulte a seção [Origem da sincronização](#BKMK_SyncSource) neste artigo. Para obter mais informações sobre as portas que o WSUS usa, confira [Como determinar as configurações de porta usadas pelo WSUS no Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  


#### <a name="restrict-access-to-specific-domains"></a>Restringir o acesso a domínios específicos  
Se a sua organização não permite que portas e protocolos sejam abertos para todos os endereços no firewall entre o ponto de atualização de software ativo e a Internet, restrinja o acesso aos seguintes domínios para que o WSUS e as Atualizações Automáticas possam se comunicar com o Microsoft Update:  

-   `http://windowsupdate.microsoft.com`  

-   `http://*.windowsupdate.microsoft.com`  

-   `https://*.windowsupdate.microsoft.com`  

-   `http://*.update.microsoft.com`  

-   `https://*.update.microsoft.com`  

-   `http://*.windowsupdate.com`  

-   `http://download.windowsupdate.com`  

-   `http://download.microsoft.com`  

-   `http://*.download.windowsupdate.com`  

-   `http://test.stats.update.microsoft.com`  

-   `http://ntservicepack.microsoft.com`  

Talvez seja necessário adicionar os endereços abaixo ao firewall localizado entre os dois sistemas de sites nos seguintes casos: 
- Se os sites filho tiverem um ponto de atualização de software 
- Se houver um ponto de atualização de software remoto, baseado na Internet, ativo em um site

  **Ponto de atualização de software no site filho**  

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  



##  <a name="BKMK_SyncSettings"></a> Planejar as configurações de sincronização  

Esta seção inclui os seguintes subtópicos:  
- [Origem de sincronização](#BKMK_SyncSource)
- [Agendamento de sincronização](#BKMK_SyncSchedule)
- [Classificações de atualizações](#BKMK_UpdateClassifications)
- [Produtos](#BKMK_UpdateProducts)
- [Regras de substituição](#BKMK_SupersedenceRules)
- [Idiomas](#BKMK_UpdateLanguages)  


A sincronização de atualizações de software no Configuration Manager baixa os metadados de atualizações de software com base nos critérios que você configura. O site de nível superior na hierarquia sincroniza as atualizações de software do Microsoft Update. Você tem a opção de configurar o ponto de atualização de software no site de nível superior para ser sincronizado com um servidor do WSUS existente, que não está na hierarquia do Configuration Manager. Os sites primário filhos sincronizam metadados de atualizações de software a partir do ponto de atualização de software no site de administração central. Para instalar e configurar um ponto de atualização de software, use esta seção para planejar as configurações de sincronização.  


###  <a name="BKMK_SyncSource"></a> Origem de sincronização  

As configurações de origem de sincronização do ponto de atualização de software especificam o local para o qual o ponto de atualização de software recupera metadados de atualizações de software. Ela também especifica se o processo de sincronização cria eventos de relatório do WSUS.  

-   **Origem da sincronização**: Por padrão, o ponto de atualização de software no site de nível superior configura a origem da sincronização para o Microsoft Update. Você tem a opção de sincronizar o site de nível superior com um servidor do WSUS existente. O ponto de atualização de software em um site primário filho configura a origem de sincronização como o ponto de atualização de software no site de administração central.  

    -  O primeiro ponto de atualização de software instalado em um site primário, que é o ponto de atualização de software padrão, é sincronizado com o site de administração central. Pontos de atualização de software adicionais no site primário sincronizam com o ponto de atualização de software padrão no site primário.  

    - Quando um ponto de atualização de software estiver desconectado do Microsoft Update ou do servidor de atualização upstream, configure a origem da sincronização para não ser sincronizada com uma origem de sincronização configurada. Nesse caso, configure-a para usar a função de exportação e importação da ferramenta **WSUSUtil** para sincronizar atualizações de software. Para obter mais informações, consulte [Synchronize software updates from a disconnected software update point](../get-started/synchronize-software-updates-disconnected.md) (Sincronizar atualizações de software de um ponto de atualização de software desconectado).  

-   **Eventos de geração de relatórios do WSUS:** O Windows Update Agent em computadores cliente pode criar mensagens de eventos para geração de relatórios do WSUS. Esses eventos não são usados pelo Configuration Manager. Portanto, a opção **Não criar eventos de relatório do WSUS** é selecionada por padrão. Quando esses eventos não são criados, o único momento em que o cliente deve se conectar ao servidor WSUS é durante a avaliação da atualização de software e as verificações de conformidade. Se esses eventos forem necessários para relatórios fora do Configuration Manager, modifique essa configuração para criar eventos de relatório do WSUS.  


###  <a name="BKMK_SyncSchedule"></a> Agendamento de sincronização  

Configure o agendamento de sincronização apenas no ponto de atualização de software no site de nível superior na hierarquia do Configuration Manager. Quando você configura a agenda de sincronização, o ponto de atualização de software sincroniza-se com a origem da sincronização, na data e hora que você especificou. O agendamento personalizado permite que você sincronize as atualizações de software para otimizar o ambiente. Considere as demandas de desempenho do servidor WSUS, do servidor do site e da rede. Por exemplo, às 2h, uma vez por semana. Como alternativa, inicie a sincronização manualmente no site de nível superior usando a ação **Atualizações de Software de Sincronização** nos nós **Todas as Atualizações de Software** ou **Grupos de Atualizações de Software** no console do Configuration Manager.  

> [!TIP]  
>  Agende a sincronização das atualizações de software para ser executada em um horário apropriado para seu ambiente. Um cenário comum é definir a agenda de sincronização para ser executada logo após o lançamento da atualização de software regular da Microsoft na segunda terça-feira de cada mês. Esse dia geralmente é conhecido como *Patch Tuesday*. Se você usa o Configuration Manager para fornecer atualizações de definição e de mecanismo do Endpoint Protection e do Windows Defender, considere a possibilidade de definir o agendamento da sincronização para execução diária.  

Depois que o ponto de atualização de software é sincronizado com êxito, ele envia uma solicitação de sincronização aos sites filho. Se houver pontos de atualização de software adicionais em um site primário, ele enviará uma solicitação de sincronização para cada ponto de atualização de software. Esse processo é repetido em todos os sites na hierarquia.  


###  <a name="BKMK_UpdateClassifications"></a> Classificações de atualizações  

Cada atualização de software é definida com uma classificação de atualização que ajuda a organizar os diferentes tipos de atualização. Durante o processo de sincronização, o site sincroniza os metadados das classificações especificadas. 

O Configuration Manager dá suporte à sincronização das classificações de atualização a seguir:  

-   **Atualizações Críticas**: Uma atualização lançada em larga escala para um problema específico que corrige um bug crítico não relacionado a segurança.  

-   **Atualizações de definições**: Uma atualização de vírus ou outros arquivos de definição.  

-   **Feature Packs**: Novos recursos de produtos que são distribuídos fora de um lançamento de produto e que normalmente são incluídos no próximo lançamento do produto completo.  

-   **Atualizações de Segurança**: Uma atualização lançada em larga escala para um problema relacionado à segurança e específico do produto.  

-   **Service Packs**: Um conjunto cumulativo de hotfixes aplicados a um aplicativo ou SO. Esses hotfixes incluem atualizações de segurança, atualizações críticas e atualizações de software.  

-   **Ferramentas**: Um utilitário ou recurso que ajuda a concluir uma ou mais tarefas.  

-   **Pacotes cumulativos de atualizações**: Um conjunto cumulativo de hotfixes que são reunidos em um pacote para facilitar a implantação. Esses hotfixes incluem atualizações de segurança, atualizações críticas e atualizações de software. Um pacote cumulativo de atualizações geralmente aborda uma área específica, como segurança ou um componente do produto.  

-   **Atualizações**: Uma atualização em um aplicativo ou arquivo que está instalado no momento.  

-   **Atualizações**: Uma atualização do recurso para uma nova versão do Windows 10.  

Defina as configurações de classificação de atualização somente no site de nível superior. As configurações de classificação de atualização não são configuradas no ponto de atualização de software em sites filho, porque os metadados de atualizações de software são replicados do site de nível superior. Ao selecionar classificações de atualização, lembre-se de que quanto mais classificações você selecionar, mais tempo levará para sincronizar os metadados das atualizações de software.  

> [!WARNING]  
>  Como melhor prática, desmarque todas as classificações antes de sincronizar pela primeira vez. Após a sincronização inicial, selecione as classificações desejadas e, em seguida, execute a sincronização novamente.  


###  <a name="BKMK_UpdateProducts"></a> Produtos  

Os metadados de cada atualização de software definem um ou mais produtos aos quais a atualização se aplica. Um produto é uma edição específica de um sistema operacional ou aplicativo. Um exemplo de um produto é o Microsoft Windows 10. Uma família de produtos é o sistema operacional ou o aplicativo base do qual os produtos individuais são derivados. Um exemplo de uma família de produtos é o Microsoft Windows, do qual o Windows 10 e o Windows Server 2016 são membros. Selecione uma família de produtos ou produtos individuais dentro de uma família de produtos.  

Quando as atualizações de software forem aplicáveis a vários produtos e, pelo menos um dos produtos for selecionado para sincronização, todos os produtos aparecerão no console do Configuration Manager, mesmo que nem todos os produtos tenham sido selecionados. Por exemplo, selecione apenas o produto Windows Server 2012. Se uma atualização de software se aplicar ao Windows Server 2012 e ao Windows Server 2012 Datacenter Edition, ambos os produtos estarão no banco de dados do site.  

Configure as definições do produto somente no site de nível superior. As definições de produto não são configuradas no ponto de atualização de software para sites filho porque os metadados de atualizações de software são replicados do site de nível superior. Quanto mais produtos você selecionar, mais tempo levará para sincronizar os metadados de atualizações de software.  

> [!IMPORTANT]  
>  O Configuration Manager armazena uma lista de produtos e de famílias de produtos que você pode escolher ao instalar o ponto de atualização de software. Os produtos e as famílias de produtos que são lançados após o lançamento do Configuration Manager podem não estar disponíveis para seleção até que você conclua a sincronização. O processo de sincronização atualiza a lista de produtos e famílias de produtos disponíveis que você pode escolher. Desmarque todos os produtos antes de sincronizar as atualizações de software pela primeira vez. Após a sincronização inicial, selecione os produtos desejados e, em seguida, execute a sincronização novamente.  


###  <a name="BKMK_SupersedenceRules"></a> Regras de substituição  

Normalmente, uma atualização de software que substitui outra executa uma ou mais das seguintes ações:  

-   Melhora, aumenta ou atualiza a correção fornecida por uma ou mais atualizações lançadas anteriormente.  

-   Melhora a eficiência do pacote de arquivos de atualização substituído, que é instalado em computadores cliente quando a atualização é aprovada para instalação. Por exemplo, a atualização substituída pode conter arquivos que não são mais relevantes para a correção ou para os sistemas operacionais compatíveis com a nova atualização. Esses arquivos não são incluídos no pacote de arquivos substitutos da atualização.  

-   Atualiza versões mais recentes de um produto. Em outras palavras, atualiza as versões que não são mais aplicáveis a versões ou configurações mais antigas de um produto. As atualizações também pode substituir outras atualizações caso modificações tenham sido feitas para expandir o suporte para idiomas. Por exemplo, uma revisão posterior da atualização de um produto do Microsoft Office pode remover o suporte de um sistema operacional mais antigo, mas pode adicionar suporte para novos idiomas na versão de atualização inicial.  

Nas propriedades do ponto de atualização de software, especifique que as atualizações de software substituídas devem ser expiradas imediatamente. Essa configuração impede que elas sejam incluídas em novas implantações. Ela também sinaliza as implantações existentes para indicar que elas contêm uma ou mais atualizações de software expiradas. Ou especifique um período de tempo para que as atualizações de software substituídas expirem. Essa ação permite que você continue a implantá-las. 

Considere os seguintes cenários em que poderia ser necessário implantar uma atualização de software substituída:  

-   Uma atualização de software substituta dá suporte apenas a versões mais recentes de um sistema operacional. Alguns dos computadores cliente que executam versões anteriores do sistema operacional.  

-   Uma atualização de software substituta tem uma aplicabilidade mais restrita do que a atualização de software que ela substitui. Esse comportamento a tornaria inadequada para alguns clientes.  

-   Quando uma atualização de software substituta não é aprovada para implantação em seu ambiente de produção.  

    > [!NOTE]  
    > Antes do Configuration Manager versão 1806, quando o Configuration Manager define uma atualização de software substituída como **Expirada**, ele não define a atualização como **Recusada** no WSUS. Os clientes continuam a procurar uma atualização expirada até que a atualização seja recusada manualmente ou por meio de um script personalizado.  Após a versão 1806 do Configuration Manager, Configuration Manager também recusará as atualizações substituídas no WSUS. Para obter mais informações sobre a tarefa de limpeza do WSUS, confira [Manutenção de atualizações de software](/sccm/sum/deploy-use/software-updates-maintenance).


###  <a name="BKMK_UpdateLanguages"></a> Idiomas  

As configurações de idioma do ponto de atualização de software permitem configurar: 
- Os idiomas para os quais os detalhes de resumo (metadados de atualizações de software) são sincronizados para atualizações de software  
- Os idiomas do arquivo de atualização de software que são baixados para atualizações de software  

#### <a name="software-update-file"></a>Arquivo de atualização de software  
Configure idiomas para a configuração **Arquivo de atualização de software** nas propriedades do ponto de atualização de software. Essa configuração fornece os idiomas padrão que estão disponíveis quando você baixa atualizações de software em um site. Modifique os idiomas que são selecionados por padrão, sempre que as atualizações de software são baixadas ou implantadas. Durante o processo de download, os arquivos de atualização de software para os idiomas configurados são baixados no local de origem do pacote de implantação, se os arquivos de atualização de software estiverem disponíveis no idioma selecionado. Em seguida, eles são copiados para a biblioteca de conteúdo no servidor do site. Em seguida, eles são distribuídos aos pontos de distribuição que estão configurados para o pacote.  

Defina as configurações de idioma do arquivo de atualização de software com os idiomas usados mais usados em seu ambiente. Por exemplo, os clientes em seu site usam principalmente o inglês e o japonês para o Windows ou para aplicativos. Há alguns outros idiomas que são usados no site. Selecione apenas inglês e japonês na coluna **Arquivo de Atualização de Software** ao baixar ou implantar a atualização de software. Essa ação permite que você use as configurações padrão da página **Seleção de Idioma** dos assistentes de implantação e de download. Essa ação também impede que arquivos de atualização desnecessários sejam baixados. Defina essa configuração em cada ponto de atualização de software na hierarquia do Configuration Manager.  

#### <a name="summary-details"></a>Detalhes do resumo  
Durante o processo de sincronização, as informações detalhadas do resumo (metadados de atualizações de software) são atualizadas para as atualizações de software nos idiomas que você especificar. Os metadados fornecem informações sobre a atualização de software, por exemplo:
- Name
- Descrição
- Produtos compatíveis com a atualização
- Classificação da atualização
- ID do Artigo
- URL de download
- Regras de aplicabilidade

Defina as configurações de detalhes do resumo somente no site de nível superior. Os detalhes do resumo não são configurados no ponto de atualização de software em sites filho porque os metadados das atualizações de software são replicados do site de administração central usando a replicação baseada em arquivo. Quando você for selecionar os idiomas dos detalhes do resumo, selecione somente os idiomas necessários em seu ambiente. Quanto mais idiomas você selecionar, mais tempo levará para sincronizar os metadados de atualizações de software. O Configuration Manager exibe os metadados de atualizações de software na localidade do sistema operacional no qual o console do Configuration Manager é executado. Se as propriedades localizadas das atualizações de software não estiverem disponíveis na localidade desse sistema operacional, as informações de atualizações de software serão exibidas em inglês.  

> [!IMPORTANT]  
>  Selecione todos os idiomas de detalhes do resumo que você precisa. Quando o ponto de atualização de software no site de nível superior for sincronizado com a origem da sincronização, os idiomas selecionados para os detalhes do resumo determinarão quais metadados de atualizações de software serão recuperados. Se você modificar os idiomas de detalhes do resumo após a execução da sincronização no mínimo uma vez, os metadados de atualizações de software serão recuperados para os idiomas de detalhes do resumo modificados somente para atualizações de software novas ou atualizadas. As atualizações de software que já tiverem sido sincronizadas não serão atualizadas com os novos metadados dos idiomas modificados, a menos que haja uma alteração na atualização de software na origem da sincronização.  



##  <a name="BKMK_MaintenanceWindow"></a> Planejar uma janela de manutenção de atualizações de software  

Adicione uma janela de manutenção dedicada para a instalação das atualizações de software. Essa ação permite configurar uma janela de manutenção geral e uma janela de manutenção diferente para as atualizações de software. Quando você configura uma janela de manutenção geral e uma janela de manutenção de atualizações de software, os clientes instalam as atualizações de software somente durante a janela de manutenção de atualizações de software. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  



##  <a name="BKMK_RestartOptions"></a> Opções de reinício para clientes do Windows 10 após a instalação da atualização de software

Quando uma atualização de software que requer uma reinicialização é implantada e instalada usando o Configuration Manager, o cliente agenda uma reinicialização pendente e exibe uma caixa de diálogo de reinicialização.

Quando há uma reinicialização pendente para uma atualização de software do Configuration Manager, a opção de **Atualizar e Reiniciar** e **Atualizar e Desligar** fica disponível em computadores Windows 10 nas opções de energia do Windows. Após o uso de uma dessas opções e o reinício do computador, a caixa de diálogo de reinicialização não é mais exibida.



## <a name="next-steps"></a>Próximas etapas
Quando planejar atualizações de software, consulte [Preparar-se para o gerenciamento de atualização de software](../get-started/prepare-for-software-updates-management.md).  

Para obter mais informações de como gerenciar o Windows como serviço, confira [Conceitos básicos do Configuration Manager como serviço e do Windows como serviço](/sccm/core/understand/configuration-manager-and-windows-as-service).
