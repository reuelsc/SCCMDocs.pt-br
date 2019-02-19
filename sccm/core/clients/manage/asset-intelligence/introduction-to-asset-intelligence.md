---
title: Introdução ao Asset Intelligence
titleSuffix: Configuration Manager
description: Use o Asset Intelligence no Configuration Manager para fazer o inventário e gerenciar o uso de licença de software em toda a empresa.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17cdfdfa90dd53f516f0dde8cd3b1130f05b9a82
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137231"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Introdução ao Asset Intelligence no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Faça o inventário e gerencie o uso de licença de software em toda a empresa usando o catálogo do Asset Intelligence. O Asset Intelligence adiciona classes de inventário de hardware para melhorar a amplitude de informações coletadas pelo Configuration Manager. Essas informações incluem os títulos de hardware e software usados em seu ambiente. Mais de 60 relatórios apresentam essas informações em um formato fácil de usar. Muitos desses relatórios vinculam-se a relatórios mais específicos. Consulte informações gerais e faça drill down de informações mais detalhadas. 

Adicione informações personalizadas ao catálogo do Asset Intelligence. Por exemplo, categorias de software personalizadas, famílias de software, rótulos de software e requisitos de hardware. Para atualizar dinamicamente o catálogo do Asset Intelligence com as informações mais atuais disponíveis, conecte-o ao Microsoft Cloud. 

Use o Asset Intelligence para ajudar a reconciliar o uso da licença de software empresarial. Importe as informações de licença de software para o banco de dados do site do Configuration Manager para exibi-las com relação a qual software está sendo usado.  



## <a name="BKMK_AssetIntelligenceCatalog"></a> Catálogo do Asset Intelligence  

O catálogo do Asset Intelligence é um conjunto de tabelas de banco de dados armazenado no banco de dados do site. Essas tabelas incluem informações de categorização e identificação para mais de 300 mil títulos e versões de software. Elas também ajudam a gerenciar os requisitos de hardware para títulos de software específicos.  

O Asset Intelligence fornece informações de licença de software para títulos de software que estão sendo usados, tanto da Microsoft como de software não Microsoft. Um conjunto predefinido de requisitos de hardware para títulos de software está disponível no catálogo do Asset Intelligence. Assim, você pode criar novas informações de requisitos de hardware definido pelo usuário para atender a requisitos personalizados. Também é possível personalizar informações no catálogo do Asset Intelligence e carregar informações de título de software para a nuvem da Microsoft para categorização.  

As atualizações do catálogo do Asset Intelligence que incluem software recém-lançado estão disponíveis para download periodicamente para executar atualizações em massa do catálogo. Ele também pode ser atualizado dinamicamente usando o ponto de sincronização do Asset Intelligence.  


### <a name="BKMK_SoftwareCategories"></a> Categorias de software  

As categorias de software do Asset Intelligence são usadas para categorizar de forma generalizada os títulos de software inventariados e como agrupamentos de alto nível de famílias de software mais específicas. Por exemplo, uma categoria de software pode ser empresas de energia, e uma família de software nessa categoria de software pode ser petróleo e gás ou hidrelétrica. Muitas categorias de software são predefinidas no catálogo do Asset Intelligence. É possível criar categorias definidas pelo usuário para definir adicionalmente o software inventariado. O estado de validação para todas as categorias de software predefinido é sempre **Validado**. As informações da categoria de software personalizado adicionadas ao catálogo do Asset Intelligence são **Definidas pelo usuário**. 

Para saber mais sobre como gerenciar categorias de software, confira [Configuring asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence) (Configuração do Asset Intelligence).  

> [!NOTE]  
> As informações de categoria de software predefinido armazenadas no catálogo do Asset Intelligence são somente leitura. Não é possível alterá-las nem excluí-las. Usuários administrativos podem adicionar, modificar ou excluir categorias de software definidas pelo usuário.  


### <a name="BKMK_SoftwareFamilies"></a> Famílias de software  

As famílias de software do Asset Intelligence são usadas para definir os títulos de software inventariados em categorias de software. Muitas famílias de software são predefinidas no catálogo do Asset Intelligence. É possível criar categorias definidas pelo usuário para definir adicionalmente o software inventariado. O estado de validação para todas as famílias de software predefinido é sempre **Validado**. As informações da família de software personalizado adicionadas ao catálogo do Asset Intelligence são **Definidas pelo usuário**. 

Para saber mais sobre como gerenciar famílias de software, confira [Configuring asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence) (Configuração do Asset Intelligence).  

> [!NOTE]  
> As informações de família de software predefinido são somente leitura e não podem ser alteradas. Usuários administrativos podem adicionar, modificar ou excluir as famílias de software definidas pelo usuário.  


### <a name="BKMK_CustomLabels"></a> Rótulos de software  

Os rótulos de software personalizado do Asset Intelligence permitem criar filtros para agrupar títulos de software e exibi-los nos relatórios do Asset Intelligence. Use rótulos de software para criar grupos de títulos de software definidos pelo usuário que compartilham um atributo comum. Por exemplo, você pode criar um rótulo de software chamado Shareware, associá-lo a títulos de shareware inventariados e executar um relatório para exibir todos os títulos de software com esse rótulo. Não há rótulos predefinidos. O estado de validação de rótulos de software é sempre **Definido pelo Usuário**. 

Para saber mais sobre como gerenciar rótulos de software, confira [Configuring asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence) (Configuração do Asset Intelligence).  


### <a name="BKMK_HardwareRequirements"></a> Requisitos de hardware  

Use as informações sobre requisitos de hardware para verificar se os computadores atendem aos requisitos de hardware para títulos de software antes que sejam afetados por implantações de software. Gerencie requisitos de hardware para títulos de software no workspace **Ativos e Conformidade** no nó **Requisitos de Hardware** no nó **Asset Intelligence**. 

Muitos requisitos de hardware são predefinidos no catálogo do Asset Intelligence. Crie novas informações de requisitos de hardware definido pelo usuário para atender a requisitos personalizados. O estado de validação para todos os requisitos de hardware predefinido é sempre **Validado**. As informações de requisitos de hardware definido pelo usuário adicionadas ao catálogo do Asset Intelligence são **Definidas pelo usuário**. 

Para saber mais sobre como gerenciar requisitos de hardware, confira [Configuring asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence) (Configuração do Asset Intelligence).  

> [!NOTE]  
> Os requisitos de hardware exibidos no console do Configuration Manager são recuperados do catálogo do Asset Intelligence. Eles não são baseados nas informações de título de software inventariado de clientes. 
> 
> As informações de requisitos de hardware não são atualizadas como parte do processo de sincronização com a Microsoft. 
> 
> É possível criar requisitos de hardware definidos pelo usuário para o software inventariado que não contém requisitos de hardware associado.  

Por padrão, as seguintes informações são exibidas para cada requisito de hardware listado:  

- **Título do software**: o título de software associado ao requisito de hardware  

- **CPU mínima (MHz)**: a velocidade mínima do processador em MHz (mega-hertz) exigida pelo título do software  

- **RAM mínima (KB)**: a RAM mínima em KB (quilobytes), exigida pelo título do software  

- **Espaço mínimo em disco (KB)**: o espaço livre mínimo em disco em KB exigido pelo título do software  

- **Tamanho mínimo do disco (KB)**: o tamanho mínimo em disco em KB exigido pelo título do software  

- **Estado de Validação**: o estado de validação para o requisito de hardware  

Os requisitos de hardware predefinido armazenados no catálogo do Asset Intelligence são somente leitura e não podem ser excluídos. Usuários administrativos podem adicionar, modificar ou excluir os requisitos de hardware definidos pelo usuário para títulos de software que não são armazenados no catálogo do Asset Intelligence.  



## <a name="BKMK_InventoriedSoftwareTitles"></a> Títulos de software inventariados  

Para exibir informações de títulos de software inventariados no console do Configuration Manager, acesse o workspace **Ativos e Conformidade**, expanda o nó **Asset Intelligence** e selecione o nó **Software inventariado**. O agente de inventário de hardware coleta as informações de software inventariado dos clientes do Configuration Manager com base em títulos de software armazenados no catálogo do Asset Intelligence.  

> [!Note]  
> O agente de inventário de hardware coleta inventário com base nas classes de relatório de inventário de hardware do Asset Intelligence habilitadas. Para saber mais sobre como habilitar as classes de relatório, confira [Configuring asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence) (Configuração do Asset Intelligence).  

Por padrão, as seguintes informações são exibidas para cada título de software inventariado:  

- **Nome**: o nome do título do software inventariado  

- **Fornecedor**: o nome do fornecedor que desenvolveu o título do software inventariado  

- **Versão**: a versão do produto do título de software inventariado  

- **Categoria**: a categoria de software atribuída no momento ao título do software inventariado  

- **Família**: a família de software atribuída no momento ao título do software inventariado  

- **Rótulo** [**1**, **2** e **3**]: Os rótulos personalizados associados ao título do software. Títulos de software inventariados podem ter até três rótulos personalizados associados a eles.  

- **Contagem**: o número de clientes do Configuration Manager que inventariaram o título do software  

- **Estado**: o estado de validação do título de software inventariado  

> [!NOTE]  
> É possível alterar as informações de categorização para o software inventariado apenas no site de nível superior na hierarquia. Essas informações incluem o nome do produto, fornecedor, categoria de software e família de software. Depois de modificar as informações de categorização de software predefinido, o estado de validação do software muda de **Validado** para **Definido pelo Usuário**.  



## <a name="AssetIntelligenceSycnronizationPoint"></a> Ponto de sincronização do Asset Intelligence  

O ponto de sincronização do Asset Intelligence é uma função do sistema de sites do Configuration Manager. Ele é usado para se conectar à nuvem da Microsoft na porta TCP 443 para gerenciar atualizações de informações do catálogo dinâmico. Instale essa função de site apenas no site de nível superior da hierarquia. Configure toda a personalização do catálogo do Asset Intelligence usando um console do Configuration Manager conectado ao site de nível superior. 

Enquanto você configura todas as atualizações no site de nível superior, as informações do catálogo são replicadas para outros sites na hierarquia. A função do site permite que você solicite a sincronização do catálogo sob demanda com a Microsoft ou agende a sincronização automática do catálogo. Além de baixar novas informações do catálogo do, o ponto de sincronização do Asset Intelligence pode carregar informações de título de software personalizado na Microsoft para categorização. A Microsoft trata todos os títulos de software carregados como informações públicas. Verifique se os títulos de software personalizados não incluem informações confidenciais ou proprietárias.  

Depois de enviar um título de software não categorizado, a Microsoft não o revisará até que haja pelo menos quatro solicitações de categorização de clientes para o mesmo título de software. Em seguida, os pesquisadores da Microsoft identificam, categorizam e disponibilizam informações de categorização de título de software a todos os clientes que estão usando o serviço online. Títulos de software que representam a maioria das solicitações por categorização recebem a prioridade mais alta para categorizar. Aplicativos de linha de negócios e de software personalizado provavelmente não recebam uma categoria. Não envie esses títulos de software à Microsoft para categorização.  

Um ponto de sincronização do Asset Intelligence é necessário para conectar-se à nuvem da Microsoft. Para saber mais sobre como instalar a função, confira [Configuring asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence) (Configuração do Asset Intelligence).  



## <a name="BKMK_AssetIntelligenceHomePage"></a> Página Inicial do Asset Intelligence  

O nó **Asset Intelligence** do workspace **Ativos e Conformidade** é a página inicial do Asset Intelligence no Configuration Manager. A página inicial apresenta uma exibição de painel de resumo das informações do catálogo do Asset Intelligence.  

> [!NOTE]  
> A página inicial do **Asset Intelligence** não é atualizada automaticamente durante sua exibição.  

A página inicial do **Asset Intelligence** inclui as seguintes seções:  

- **Sincronização de catálogo**: fornece informações sobre se o Asset Intelligence está habilitado e o status atual do ponto de sincronização do Asset Intelligence.  

    > [!NOTE]  
    > A página inicial exibe apenas esta seção quando você instala um ponto de sincronização do Asset Intelligence.  

    A seção também fornece as seguintes informações:  

    - Agendamento de sincronização  

    - Se você importou um demonstrativo de licenças do cliente   

    - A última atualização do status  

    - O tempo para a próxima atualização agendada  

    - O número de alterações depois que você instalou o ponto de sincronização do Asset Intelligence   

- **Status do software inventariado**: a contagem e o percentual de software inventariado, as categorias de software e as famílias de software identificadas pela Microsoft, identificadas por um administrador, com identificação online pendente ou não identificadas e não pendentes. As informações exibidas no formato de tabela mostram a contagem de cada um, e as informações exibidas no gráfico mostram a porcentagem de cada.  



## <a name="BKMK_AssetIntelligenceReports"></a> Relatórios do Asset Intelligence  

Os relatórios do Asset Intelligence estão localizados no console do Configuration Manager, no workspace **Monitoramento** da pasta do **Asset Intelligence**, no nó **Relatórios**. Os relatórios fornecem informações sobre hardware, gerenciamento de licenças e software. Para saber mais sobre relatórios no Configuration Manager, confira [Relatórios](/sccm/core/servers/manage/reporting).  

> [!NOTE]  
> A precisão da quantidade de títulos de software instalados e de informações de licença exibidas nos relatórios do Asset Intelligence pode variar do número real dos títulos de software instalados ou das licenças usadas no ambiente. Essa variação é causada devido às dependências complexas e limitações envolvidas no inventário das informações de licença de software para títulos de software que estão instalados em ambientes corporativos. Não use relatórios do Asset Intelligence como a origem única para determinar a conformidade da licença de software adquirido.  


### <a name="BKMK_HardwareReports"></a> Relatórios de hardware  

Os relatórios de hardware do Asset Intelligence fornecem informações sobre ativos de hardware na organização. Usando as informações de inventário de hardware, como velocidade, memória, dispositivos periféricos, os relatórios de hardware do Asset Intelligence podem apresentar informações sobre os dispositivos USB, sobre o hardware que precisa ser atualizado e até mesmo sobre os computadores que não estão prontos para uma atualização de software específica.  

> [!NOTE]  
> Alguns dados do usuário nos relatórios de hardware do Asset Intelligence são coletados do log de eventos de segurança do Windows. Para uma maior precisão do relatório, desmarque este log quando reatribuir um computador a um novo usuário.  


### <a name="BKMK_LicenseManagementReports"></a> Relatórios de gerenciamento de licença  

Os relatórios de gerenciamento de licenças do Asset Intelligence fornecem dados sobre as licenças que estão sendo usadas. O relatório **Razão de Licença** lista os aplicativos da Microsoft instalados em um formato congruente com um MLS (Demonstrativo de Licença da Microsoft). Esse formato fornece um método conveniente de fazer a correspondência das licenças adquiridas com as licenças usadas. Outros relatórios do gerenciamento de licenças fornecem informações sobre computadores que atuam como servidores que executam o KMS (Serviço de Gerenciamento de Chaves) para estatísticas de ativação do Windows.  

> [!IMPORTANT]  
> Vários dos relatórios de gerenciamento de licenças do Asset Intelligence apresentam informações sobre a função do KMS, um método de administração de licenciamento por volume. Se você não tiver implantado um servidor KMS, alguns relatórios talvez não retornarão nenhum dado.  


### <a name="BKMK_SoftwareReports"></a> Relatórios de software  

Os relatórios de software do Asset Intelligence fornecem informações sobre famílias de software, categorias e títulos de software específicos instalados em computadores na organização. Os relatórios de software apresentam informações como objetos auxiliares de navegador e software iniciado automaticamente. Esses relatórios podem ser usados para identificar adware, spyware e outros malware. Também é possível usá-los para identificar a redundância de software para ajudar a simplificar o suporte e aquisição de software.  


### <a name="BKMK_SoftwareIdTagReports"></a> Relatórios de marca de identificação de software  

Os relatórios de marca de identificação de software do Asset Intelligence fornecem informações sobre software que inclui uma marca de identificação do software em conformidade com ISO/IEC 19770-2. As marcas de identificação de software fornecem informações de autoridade usadas para identificar o software instalado. Quando você habilita a classe de relatório de inventário de hardware **SMS_SoftwareTag**, o Configuration Manager coleta informações sobre o software com marcas de identificação de software. 

Os relatórios abaixo fornecem informações sobre o software:  

- **Software 14A – Pesquisar software habilitado para marca de identificação de software**: a contagem de software instalado com uma marca de identificação de software habilitada  

- **Software 14B – Computadores com software habilitado para marca de identificação de software específico instalado**: Todos os computadores que instalaram o software com uma marca de identificação de software especificado habilitada  

- **Software 14C – Software habilitado para marca de identificação de software instalado em um computador específico**: todos os softwares instalados com uma marca de identificação de software específica habilitada em um computador específico  


### <a name="BKMK_ReportingLImitations"></a> Limitações de relatórios  

Os relatórios do Asset Intelligence podem fornecer grandes quantidades de informações sobre títulos de software instalado e licenças de software adquiridas que estão sendo usadas. Não use essas informações como a única fonte para determinar a conformidade da licença de software adquirido.  

#### <a name="BKMK_ExampleDependencies"></a> Exemplos de dependências  
A precisão da quantidade exibida nos relatórios do Asset Intelligence para títulos de software instalado e informações de licença podem variar dos valores reais usados no momento. Essa variação é causada pelas dependências complexas envolvidas no inventário das informações de licença de software para títulos de software usados em ambientes corporativos. Os exemplos abaixo mostram as dependências envolvidas ao fazer inventário do software instalado na empresa usando o Asset Intelligence que podem afetar a precisão dos relatórios do Asset Intelligence:  

- **Dependências de inventário de hardware do cliente**: Os relatórios de software instalado do Asset Intelligence se baseiam em dados coletados de clientes do Configuration Manager, estendendo o inventário de hardware para habilitar os relatórios do Asset Intelligence. Devido a essa dependência dos relatórios de inventário de hardware, os relatórios do Asset Intelligence refletirão somente os dados dos clientes que concluírem com êxito os processos de inventário de hardware com as classes de relatório WMI do Asset Intelligence necessárias habilitadas. Como os clientes do Configuration Manager executam processos de inventário de hardware em um agendamento definido pelo usuário administrativo, pode ocorrer um atraso no relatório de dados que afeta a precisão dos relatórios do Asset Intelligence. 

    Por exemplo, um título de software inventariado licenciado poderá ser desinstalado depois que o cliente concluir um ciclo de inventário de hardware bem-sucedido. Os relatórios do Asset Intelligence exibem o título de software como instalado até o próximo ciclo de relatório de inventário de hardware agendado do cliente.  

- **Dependências de pacotes de software**: Os relatórios do Asset Intelligence são baseados nos dados de título de software instalado coletados usando processos padrão de inventário de hardware do cliente do Configuration Manager. Alguns dados de título de software podem não ser coletados corretamente. Exemplos que podem causar relatórios de inteligência de ativos imprecisos:  

    - Instalações de software não compatíveis com os processos de instalação padrão  

    - Instalações de software que foram alteradas antes da instalação   

#### <a name="BKMK_LegalLimitations"></a> Limitações legais  
As informações exibidas em relatórios do Asset Intelligence estão sujeitas a muitas limitações. As informações exibidas neles não representam informações legais ou de contabilidade nem outro conselho profissional. As informações fornecidas pelos relatórios do Asset Intelligence são apenas para fins informativos. Não as use como a única fonte de informações para determinar a conformidade do uso de licenças de software.  

As limitações a seguir são exemplos do uso do Asset Intelligence que possa afetar a precisão dos relatórios:  

- **Limitações da quantidade de uso de licença da Microsoft**:  

    - a quantidade de licenças de software da Microsoft adquiridas é baseada em informações fornecidas pelos administradores. Examine-a de perto para garantir que o número correto de licenças de software seja fornecido.  

    - A quantidade relatada de licenças de software da Microsoft inclui informações somente sobre licenças de software da Microsoft adquiridas por meio de programas de licenciamento por volume. Isso não reflete informações para licenças de software adquiridas por meio de canais de varejo, OEM ou outros canais de vendas de licença de software.  

    - As licenças de software adquiridas nos últimos 45 dias podem não ser incluídas na quantidade de licenças de software Microsoft relatada, devido a requisitos e agendamentos de relatório de revendedor de software.  

    - As transferências de licença de software de fusões ou aquisições corporativas podem não ser refletidas nas quantidades de licença de software Microsoft.  

    - Termos e condições não padrão em um contrato MVLS (Licenciamento por Volume da Microsoft) podem afetar o número de licenças de software relatadas. Eles podem exigir uma análise adicional por um representante da Microsoft.  

- **Limitações da quantidade de título de software instalado**: Os clientes do Configuration Manager devem concluir com êxito os ciclos de relatórios de inventário de hardware para que os relatórios do Asset Intelligence relatem com precisão a quantidade de títulos de software instalados. Pode haver um atraso entre a instalação ou a desinstalação de um título de software licenciado após um ciclo de relatório de inventário de hardware bem-sucedido. Essa ação não pode ser refletida em relatórios do Asset Intelligence executados antes de o cliente relatar seu próximo inventário de hardware agendado.  

- **Limitações de reconciliação de licença**: A reconciliação da quantidade de títulos de software instalados em relação à quantidade de licenças de software adquiridas é calculada usando uma comparação entre a quantidade de licenças especificadas pelo administrador e a quantidade de títulos de software instalados coletados de inventários de hardware de cliente do Configuration Manager com base no agendamento definido pelo administrador. Essa comparação não representa uma conclusão final da Microsoft sobre as posições de licenças. A posição de licença real depende dos direitos específicos de software de licença e o uso título concedidos aos termos de licença.  



## <a name="BKMK_ValidationStates"></a> Estados de validação do Asset Intelligence  

Os estados de validação do Asset Intelligence representam a origem e o status atual de validação de informações do catálogo do Asset Intelligence. A tabela a seguir mostra os possíveis estados de validação do Asset Intelligence e as ações do administrador que pode causá-los.  

| Estado | Definição | Ação do administrador | Comentário |  
|---------------|--------------------|------------------------------|-----------------|  
|**Validado**|Os pesquisadores da Microsoft definiram o item de catálogo|Nenhum|Melhor estado|  
|**Definido pelo Usuário**|Os pesquisadores da Microsoft não definiram o item de catálogo|Personalizar as informações do catálogo local|Esse estado é exibido em relatórios do Asset Intelligence|  
|**Pendente**|Os pesquisadores da Microsoft não definiram o item de catálogo, mas você o enviou à Microsoft para categorização|Nenhuma ação adicional depois de solicitar a categorização|O item de catálogo continua nesse estado até que os pesquisadores da Microsoft o categorizem e você sincronize seu catálogo do Asset Intelligence|  
|**Atualizável**|Um item de catálogo definido pelo usuário foi categorizado de maneira diferente pela Microsoft durante a sincronização do catálogo.|Use a ação **Resolver Conflito** para decidir se deve usar as novas informações de categorização ou o valor definido pelo usuário anterior. Para saber mais sobre como resolver conflitos, confira [Operations for asset intelligence](/sccm/core/clients/manage/asset-intelligence/operations-for-asset-intelligence) (Operações do Asset Intelligence).|Após resolver um conflito de categorização, o item já não é validado como conflitante, a menos que as atualizações posteriores de categorização introduzam novas informações sobre o item.|  
|**Não categorizado**|O item de catálogo não foi definido pelos pesquisadores da Microsoft, o item não foi enviado para a Microsoft para categorização e o administrador não atribuiu um valor de categorização definido pelo usuário.|Solicite a categorização ou personalize as informações do catálogo local. Para saber mais, confira [Operations for asset intelligence](/sccm/core/clients/manage/asset-intelligence/operations-for-asset-intelligence) (Operações do Asset Intelligence).|Nenhum|  

> [!NOTE]  
> Os itens de catálogo enviados à Microsoft para categorização têm um estado de validação de **Pendente** em um site de administração central, mas continuam sendo exibidos com um estado de validação de **Não categorizado** nos sites primários filho.  

Para obter exemplos de quando um estado de validação pode fazer a transição de um estado para outro, confira [Example Validation State Transitions for Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence) (Exemplo de transições de estado de validação para o Asset Intelligence).  
