---
title: "Introdução ao Asset Intelligence"
titleSuffix: Configuration Manager
description: "Obtenha uma introdução ao Asset Intelligence no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 349f5998c0d5e96a626e901ae99fee76541d1b4e
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="introduction-to-asset-intelligence-in-system-center-configuration-manager"></a>Introdução ao Asset Intelligence no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Asset Intelligence no System Center Configuration Manager permite inventariar e gerenciar o uso de licença de software em toda a empresa usando o catálogo do Asset Intelligence. Muitas classes WMI (Instrumentação de Gerenciamento do Windows) de inventário de hardware melhoram a gama das informações coletadas sobre títulos de hardware e software que estão sendo usados. Mais de 60 relatórios apresentam estas informações em um formato fácil de usar. Muitos desses relatórios contêm links para relatórios mais específicos nos quais você pode executar consultas para obter informações gerais e fazer uma busca detalhada das informações. Você pode adicionar informações personalizadas ao catálogo do Asset Intelligence, como categorias de software personalizado, famílias de software, rótulos de software e requisitos de hardware. Você também pode se conectar ao System Center Online para atualizar dinamicamente o catálogo do Asset Intelligence com as informações mais atuais disponíveis. Os clientes da Microsoft poderão reconciliar o uso de licença de software corporativo com licenças de software adquiridas que estão sendo usadas por meio da importação de informações de licença de software para o banco de dados do site do Configuration Manager.  

##  <a name="BKMK_AssetIntelligenceCatalog"></a> Catálogo do Asset Intelligence  

 O catálogo do Asset Intelligence no Configuration Manager é um conjunto de tabelas de banco de dados armazenadas no banco de dados do site que contém informações de categorização e identificação de mais de 300.000 títulos de software e versões. Essas tabelas de banco de dados também são usadas para gerenciar os requisitos de hardware para títulos de software específicos.  

 O catálogo do Asset Intelligence fornece informações de licença de software para títulos de software que estão sendo usados, tanto da Microsoft como de software não Microsoft. Um conjunto predefinido de requisitos de hardware para títulos de software está disponível no catálogo do Asset Intelligence. Assim, você pode criar novas informações de requisitos de hardware definido pelo usuário para atender a requisitos personalizados. Além disso, você pode personalizar as informações no catálogo do Asset Intelligence e carregar informações do título de software no System Center Online para categorização.  

 As atualizações do catálogo do Asset Intelligence que contêm software recém-lançado estão disponíveis para download periodicamente para executar atualizações em massa do catálogo. Ou então, o catálogo pode ser atualizado dinamicamente usando a função do sistema de sites do ponto de sincronização do Asset Intelligence.  

###  <a name="BKMK_SoftwareCategories"></a> Categorias de software  
 As categorias de software do Asset Intelligence são usadas para categorizar de forma generalizada os títulos de software inventariados e também são usadas como agrupamentos de alto nível de famílias de software mais específicas. Por exemplo, uma categoria de software pode ser empresas de energia, e uma família de software nessa categoria de software pode ser petróleo e gás ou hidrelétrica. Muitas categorias de software são predefinidas no catálogo do Asset Intelligence, e é possível criar categorias definidas pelo usuário para definir com mais detalhes o software inventariado. O estado de validação para todas as categorias de software predefinido é sempre **Validado**, enquanto as informações de categorias de software personalizado adicionadas ao catálogo do Asset Intelligence são **Definidas pelo Usuário**. Para obter mais informações sobre como gerenciar categorias de software, consulte [Configuração do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  As informações de categoria de software predefinido armazenadas no catálogo do Asset Intelligence são somente leitura e não podem ser alteradas ou excluídas. Usuários administrativos podem adicionar, modificar ou excluir categorias de software definidas pelo usuário.  

###  <a name="BKMK_SoftwareFamilies"></a> Famílias de software  
 As famílias de software do Asset Intelligence são usadas para definir os títulos de software inventariados em categorias de software. Muitas famílias de software são predefinidas no catálogo do Asset Intelligence, e é possível criar categorias definidas pelo usuário para definir com mais detalhes o software inventariado. O estado de validação para todas as famílias de software predefinido é sempre **Validado**, enquanto as informações de famílias de software personalizado adicionadas ao catálogo do Asset Intelligence são **Definidas pelo Usuário**. Para obter mais informações sobre como gerenciar famílias de software, consulte [Configuração do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  As informações de família de software predefinido são somente leitura e não podem ser alteradas. Usuários administrativos podem adicionar, modificar ou excluir as famílias de software definidas pelo usuário.  

###  <a name="BKMK_CustomLabels"></a> Rótulos de software  
 Os rótulos de software personalizado do Asset Intelligence permitem criar filtros que você pode usar para agrupar títulos de software e exibi-los usando os relatórios do Asset Intelligence. Você pode usar rótulos de software para criar grupos de títulos de software definidos pelo usuário que compartilham um atributo comum. Por exemplo, você pode criar um rótulo de software chamado Shareware, associar esse rótulo de software a títulos de shareware inventariados e executar um relatório para exibir todos os títulos de software com o rótulo de software Shareware associado. Os rótulos de software não são predefinidos. O estado de validação de rótulos de software é sempre **Definido pelo Usuário**. Para obter mais informações sobre como gerenciar rótulos de software, consulte [Configuração do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

###  <a name="BKMK_HardwareRequirements"></a> Requisitos de hardware  
 É possível usar as informações sobre requisitos de hardware para verificar se os computadores atendem aos requisitos de hardware para títulos de software antes que sejam afetados por implantações de software. Você pode gerenciar requisitos de hardware para títulos de software no espaço de trabalho **Ativos e Conformidade** do nó **Requisitos de Hardware** , no nó **Asset Intelligence** . Vários requisitos de hardware são predefinidos no catálogo do Asset Intelligence. Assim, você pode criar novas informações de requisitos de hardware definido pelo usuário para atender a requisitos personalizados. O estado de validação para todos os requisitos de hardware predefinidos é sempre **Validado**, enquanto as informações de requisitos de hardware adicionadas ao catálogo do Asset Intelligence são **Definidas pelo Usuário**. Para obter mais informações sobre como gerenciar requisitos de software, consulte [Configuração do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  Os requisitos de hardware exibidos no console do Configuration Manager são recuperados do catálogo do Asset Intelligence e não são baseados em informações de título de software inventariados de clientes do System Center 2012 Configuration Manager. As informações de requisitos de hardware não são atualizadas como parte do processo de sincronização com o System Center Online. Você pode criar requisitos de hardware definidos pelo usuário para o software inventariado que não contém requisitos de hardware associado.  

 Por padrão, as seguintes informações são exibidas para cada requisito de hardware listado:  

-   **Título de Software**: especifica o título de software associado ao requisito de hardware.  

-   **CPU Mínima (MHz)**: especifica a velocidade mínima do processador, em MHz (mega-hertz), requerida pelo título de software.  

-   **RAM Mínima (KB)**: especifica a RAM mínima, em KB (quilobytes), requerida pelo título de software.  

-   **Espaço em Disco Mínimo (KB)**: especifica o espaço mínimo livre em disco, em KB, necessário para o título de software.  

-   **Tamanho Mínimo de Disco (KB)**: especifica o tamanho mínimo de disco, em KB, requerido pelo título de software.  

-   **Estado de Validação**: especifica o estado de validação para os requisitos de hardware.  

 Os requisitos de hardware predefinido armazenados no catálogo do Asset Intelligence são somente leitura e não podem ser excluídos.  Usuários administrativos podem adicionar, modificar ou excluir os requisitos de hardware definidos pelo usuário para títulos de software que não são armazenados no catálogo do Asset Intelligence.  

##  <a name="BKMK_InventoriedSoftwareTitles"></a> Títulos de software inventariados  
 Você pode exibir informações de título de software inventariado no espaço de trabalho **Ativos e Conformidade** do nó **Software Inventariado** , no nó **Asset Intelligence** . O Agente Cliente de Inventário de Hardware coleta as informações de software inventariado dos clientes do Configuration Manager com base em títulos de software armazenados no catálogo do Asset Intelligence.  

> [!WARNING]  
>  O Agente Cliente de Inventário de Hardware coleta inventário de acordo com as classes de relatório de inventário de hardware do Asset Intelligence habilitadas. Para obter mais informações sobre como habilitar as classes de relatórios, consulte [Configuração do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Por padrão, as seguintes informações são exibidas para cada título de software inventariado:  

-   **Nome**: especifica o nome do título de software inventariado.  

-   **Fornecedor**: especifica o nome do fornecedor que desenvolveu o título de software inventariado.  

-   **Versão**: especifica a versão do produto do título de software inventariado.  

-   **Categoria**: especifica a categoria de software que está atribuída no momento ao título de software inventariado.  

-   **Família**: especifica a família de software que está atribuída no momento ao título de software inventariado.  

-   **Rótulo** [**1**, **2**e **3**]: especifica os rótulos personalizados associados ao título de software. Títulos de software inventariados podem ter até três rótulos personalizados associados a eles.  

-   **Contagem**: especifica o número de clientes do Configuration Manager que inventariaram o título de software.  

-   **Estado**: especifica o estado de validação do título de software inventariado.  

> [!NOTE]  
>  Você pode alterar as informações de categorização (nome do produto, fornecedor, categoria de software e família de software) para o software inventariado apenas no site de nível superior na hierarquia. Depois de modificar as informações de categorização de software predefinido, o estado de validação do software muda de **Validado** para **Definido pelo Usuário**.  

##  <a name="AssetIntelligenceSycnronizationPoint"></a> Ponto de sincronização do Asset Intelligence  
 O ponto de sincronização do Asset Intelligence é uma função do sistema de sites do Configuration Manager usada para a conexão ao System Center Online (usando a porta TCP 443) a fim de gerenciar atualizações dinâmicas de informações do catálogo do Asset Intelligence. Essa função do site pode ser instalada somente no site de nível superior da hierarquia. É necessário configurar todas as personalizações do catálogo do Asset Intelligence usando um console do Configuration Manager conectado ao site de nível superior. Embora todas as atualizações precisem ser configuradas no site de nível superior, as informações do catálogo do Asset Intelligence são replicadas para outros sites na hierarquia. A função do site do ponto de sincronização do Asset Intelligence permite que você solicite a sincronização do catálogo sob demanda com o System Center Online ou agende a sincronização automática do catálogo. Além de baixar novas informações do catálogo do Asset Intelligence, o ponto de sincronização do Asset Intelligence pode carregar informações de título de software personalizado no System Center Online para categorização. A Microsoft trata todos os títulos de software carregados no System Center Online para categorização como informações públicas. Portanto, você deve garantir que os títulos de software personalizado não contêm informações confidenciais ou proprietárias.  

> [!NOTE]  
>  Depois que um título de software não categorizado é enviado e houver, pelo menos, quatro solicitações de categorização de clientes pelo mesmo título de software, os pesquisadores do System Center Online identificam, categorizam e disponibilizam as informações de categorização de título de software para todos os clientes que estão usando o serviço online. Títulos de software que representam a maioria das solicitações por categorização recebem a prioridade mais alta para categorizar. É pouco provável que software personalizado e aplicativos de linha de negócios recebam uma categoria; por isso, como uma prática recomendada, você não deve enviar esses títulos de software à Microsoft para categorização.  

> [!NOTE]  
>  Uma função do sistema de sites do ponto de sincronização do Asset Intelligence é necessária para conectar-se ao System Center Online. Para obter informações sobre como instalar um ponto de sincronização do Asset Intelligence, consulte [Configuração do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

##  <a name="BKMK_AssetIntelligenceHomePage"></a> Home page do Asset Intelligence  
 O nó **Asset Intelligence** do espaço de trabalho **Ativos e Conformidade** é a home page do Asset Intelligence no Configuration Manager. A home page do **Asset Intelligence** exibe uma exibição de painel de resumo das informações do catálogo do Asset Intelligence.  

> [!NOTE]  
>  A home page do **Asset Intelligence** não será atualizada automaticamente durante sua exibição.  

 A home page do **Asset Intelligence** contém as seguintes seções:  

-   **Sincronização do Catálogo**: fornece informações sobre se o Asset Intelligence está habilitado e o status atual do ponto de sincronização do Asset Intelligence. A seção também fornece o agendamento de sincronização, se o demonstrativo de licença do cliente foi importado, a última atualização de status e a hora da próxima atualização agendada, bem como o número de alterações ocorridas depois que o sistema de sites do ponto de sincronização do Asset Intelligence foi instalado.  

    > [!NOTE]  
    >  A seção de sincronização do catálogo do Asset Intelligence da home page do **Asset Intelligence** é exibida somente se uma função do sistema de sites do ponto de sincronização do Asset Intelligence tiver sido instalada.  

-   **Status de Software Inventariado**: fornece a contagem e o percentual de software inventariado, categorias de software e famílias de software que são identificadas pela Microsoft, identificados por um administrador, com identificação online pendente ou não identificados e não pendentes. As informações exibidas em formato de tabela mostram a contagem para cada um, e as informações exibidas no gráfico mostram o percentual de cada um.  

##  <a name="BKMK_AssetIntelligenceReports"></a> Relatórios do Asset Intelligence  
 Os relatórios do Asset Intelligence estão localizados no console do Configuration Manager, no espaço de trabalho **Monitoramento** da pasta do Asset Intelligence, no nó **Relatórios**. Os relatórios fornecem informações sobre hardware, gerenciamento de licenças e software. Para obter mais informações sobre os relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  A precisão da quantidade de títulos de software instalados e de informações de licença exibidas nos relatórios do Asset Intelligence pode variar do número real dos títulos de software instalados ou das licenças usadas no ambiente. Essa variação é causada devido às dependências complexas e limitações envolvidas no inventário das informações de licença de software para títulos de software que estão instalados em ambientes corporativos. Não use relatórios do Asset Intelligence como a única origem para determinar a conformidade das licenças de software adquiridas.  

###  <a name="BKMK_HardwareReports"></a> Relatórios de hardware do Asset Intelligence  
 Os relatórios de hardware do Asset Intelligence fornecem informações sobre ativos de hardware na organização. Usando as informações de inventário de hardware, como velocidade, memória, dispositivos periféricos e muito mais, os relatórios de hardware do Asset Intelligence podem apresentar informações sobre os dispositivos USB, sobre o hardware que precisa ser atualizado e até mesmo sobre os computadores que não estão prontos para uma atualização de software específica.  

> [!NOTE]  
>  Alguns dados do usuário nos relatórios de hardware do Asset Intelligence são coletados do Log de Eventos de Segurança do Sistema. Para uma maior precisão do relatório, recomendamos que você desmarque este log quando reatribuir um computador a um novo usuário.  

###  <a name="BKMK_LicenseManagementReports"></a> Relatórios de gerenciamento de licenças do Asset Intelligence  
 Os relatórios de gerenciamento de licenças do Asset Intelligence fornecem dados sobre as licenças que estão sendo usadas. O relatório de Razão de Licença lista os aplicativos da Microsoft instalados em um formato congruente com um MLS (Demonstrativo de Licença da Microsoft). Isso fornece um método conveniente de fazer a correspondência das licenças adquiridas com as licenças usadas. Outros relatórios do Gerenciamento de Licenças fornecem informações sobre computadores que atuam como servidores que executam o KMS (Serviço de Gerenciamento de Chaves) para estatísticas de ativação do sistema operacional.  

> [!IMPORTANT]  
>  Vários dos relatórios de Gerenciamento de licenças do Asset Intelligence apresentam informações sobre a função do KMS, um método de administração de licenciamento por volume. Se um servidor KMS não tiver sido implementado, alguns relatórios podem não retornar nenhum dado. Para obter mais informações sobre o KMS, procure por KMS no [Microsoft TechNet](http://go.microsoft.com/fwlink/?linkid=3225).  

###  <a name="BKMK_SoftwareReports"></a> Relatórios de software do Asset Intelligence  
 Os relatórios de software do Asset Intelligence fornecem informações sobre famílias de software, categorias e títulos de software específicos que estão instalados em computadores na organização. Os relatórios do software apresentam informações sobre objetos auxiliares de navegador, software que é iniciado automaticamente e muito mais. Esses relatórios podem ser usados para identificar o adware, spyware e outros tipos de malware e identificar a redundância de software para ajudar a simplificar a compra de software e o suporte.  

###  <a name="BKMK_SoftwareIdTagReports"></a> Relatórios de marca de identificação de software do Asset Intelligence  
 Os relatórios de marca de identificação de software do Asset Intelligence fornecem informações sobre software que contém uma marca de identificação de software que está em conformidade com a ISO/IEC 19770-2. As marcas de identificação de software fornecem informações autoritativa usadas para identificar o software instalado. Quando você habilita a classe de relatório de inventário de hardware SMS_SoftwareTag, o Configuration Manager coleta informações sobre o software com marcas de identificação de software. Os relatórios abaixo fornecem informações sobre o software:  

-   **Software 14A – Pesquisar software habilitado para marca de identificação de software**: este relatório fornece a contagem de software instalado com uma marca de identificação de software habilitada.  

-   **Software 14B – Computadores com software habilitado para marca de identificação de software específica instalado**: este relatório lista todos os computadores que instalaram software com uma marca de identificação de software específica habilitada.  

-   **Software 14C – Software habilitado para marca de identificação de software instalado em um computador específico**: este relatório lista todos os programas instalados com uma marca de identificação de software específica habilitada em um computador específico.  

###  <a name="BKMK_ReportingLImitations"></a> Limitações de relatórios do Asset Intelligence  
 Os relatórios do Asset Intelligence podem fornecer grandes quantidades de informações sobre os títulos de software instalados e as licenças de software adquiridas que estão sendo usados. No entanto, você não deve usar essas informações como a única fonte para determinar a conformidade de licença de software adquirida.  

####  <a name="BKMK_ExampleDependencies"></a> Exemplos de dependências  
 A precisão da quantidade exibida nos relatórios do Asset Intelligence para títulos de software instalados e informações de licença pode variar das quantidades reais usadas no momento. Essa variação é causada pelas dependências complexas envolvidas no inventário das informações de licença de software para títulos de software usados em ambientes corporativos. Os exemplos abaixo mostram as dependências envolvidas no inventário do software instalado na empresa usando Asset Intelligence que podem afetar a precisão dos relatórios do Asset Intelligence:  

 **Dependências de inventário de hardware do cliente**  
 Os relatórios de software instalado do Asset Intelligence se baseiam em dados coletados de clientes do Configuration Manager, estendendo o inventário de hardware para habilitar os relatórios do Asset Intelligence. Devido a essa dependência dos relatórios de inventário de hardware, os relatórios do Asset Intelligence refletem somente os dados dos clientes do Configuration Manager que concluírem com êxito os processos de inventário de hardware com as classes de relatório WMI do Asset Intelligence necessárias habilitadas. Além disso, como os clientes do Configuration Manager executam processos de inventário de hardware em um agendamento definido pelo usuário administrativo, pode ocorrer um atraso no relatório de dados que afetará a precisão dos relatórios do Asset Intelligence. Por exemplo, um título de software inventariado licenciado poderá ser desinstalado depois que o cliente concluir um ciclo de inventário de hardware bem-sucedido. No entanto, o título do software é exibido como instalado nos relatórios do Asset Intelligence até o próximo ciclo de relatórios do inventário de hardware agendado do cliente.  

 **Dependências de pacotes de software**  
 Como os relatórios do Asset Intelligence se baseiam em dados de títulos de software instalados que são coletados usando processos padrão de inventário de hardware do cliente do Configuration Manager, alguns dados do título de software podem não ser coletados corretamente. Por exemplo, as instalações de software que não seguirem os processos de instalação ou as instalações de software padrão que foram alterados antes da instalação podem gerar relatórios imprecisos do Asset Intelligence.  

####  <a name="BKMK_LegalLimitations"></a> Limitações legais  
 As informações exibidas nos relatórios do Asset Intelligence estão sujeitas a muitas limitações e as informações exibidas neles não representam assessoria jurídica, contábil ou qualquer outro tipo de assessoria profissional. As informações fornecidas pelos relatórios do Asset Intelligence servem apenas para fins informativos e não devem ser usadas como a única fonte de informação para determinar a conformidade do uso de licença de software.  

 Estes são exemplos de limitações envolvidas no inventário do software instalado e do uso de licença na empresa usando Asset Intelligence que podem afetar a precisão dos relatórios do Asset Intelligence:  

 **Limitações da quantidade de uso de licença da Microsoft**  
 -   A quantidade de licenças de software Microsoft adquiridas se baseia em informações fornecidas por administradores e deve ser examinada atentamente para garantir que o número correto de licenças de software seja fornecido.  

-   A quantidade relatada de licenças de software Microsoft contém informações somente sobre licenças de software Microsoft adquiridas por meio de programas de licenciamento por volume e não reflete as informações de licenças de software adquiridas por varejo, OEM ou outros canais de vendas de licença de software.  

-   As licenças de software adquiridas nos últimos 45 dias podem não ser incluídas na quantidade de licenças de software Microsoft relatada, devido a requisitos e agendamentos de relatório de revendedor de software.  

-   As transferências de licença de software de fusões ou aquisições corporativas podem não ser refletidas nas quantidades de licença de software Microsoft.  

-   Termos e condições não padrão em um contrato MVLS (Licenciamento por Volume da Microsoft) podem afetar o número de licenças de software relatadas e, portanto, podem exigir uma análise adicional por um representante da Microsoft.  

 **Limitações da quantidade de título de software instalada**  
 Os clientes do Configuration Manager devem concluir com êxito os ciclos de relatórios de inventário de hardware para que os relatórios do Asset Intelligence relatem com precisão a quantidade de títulos de software instalados. Além disso, pode haver um atraso entre a instalação ou desinstalação de um título de software licenciado após um ciclo de relatório de inventário de hardware bem-sucedido que não é refletido nos relatórios do Asset Intelligence executados antes de o cliente relatar seu próximo inventário de hardware agendado.  

 **Limitações de reconciliação de licença**  
 A reconciliação da quantidade de títulos de software instalados em relação à quantidade de licenças de software adquiridas é calculada usando uma comparação entre a quantidade de licenças especificadas pelo administrador e a quantidade de títulos de software instalados coletados de inventários de hardware de cliente do Configuration Manager com base no agendamento definido pelo administrador. Essa comparação não representa uma conclusão final da Microsoft sobre as posições de licenças. A posição real da licença depende da licença do título de software específico e dos direitos de uso concedidos pelos termos de licença.  

##  <a name="BKMK_ValidationStates"></a> Estados de validação do Asset Intelligence  
 Os estados de validação do Asset Intelligence representam a origem e o status atual de validação das informações do catálogo do Asset Intelligence. A tabela a seguir mostra os possíveis estados de validação do Asset Intelligence e as ações do administrador que podem afetá-los.  

|**Estado**|**Definição**|**Ação do administrador**|**Comentário**|  
|---------------|--------------------|------------------------------|-----------------|  
|**Validado**|O item de catálogo foi definido pelos pesquisadores do System Center Online.|nenhuma.|O melhor estado.|  
|**Definidas pelo Usuário**|O item de catálogo não foi definido pelos pesquisadores do System Center Online.|As informações do catálogo local foram personalizadas.|Esse estado é exibido nos relatórios do Asset Intelligence.|  
|**Pendente**|O item de catálogo não foi definido pelos pesquisadores do System Center Online, mas foi enviado para o System Center Online para categorização.|Categorização solicitada do System Center Online.|O item de catálogo permanece nesse estado até que os pesquisadores do System Center Online o categorizem, e o catálogo do Asset Intelligence é sincronizado.|  
|**Atualizável**|Um item de catálogo definido pelo usuário foi categorizado de modo diferente pelo System Center Online durante uma sincronização de catálogo posterior.|O catálogo do Asset Intelligence local foi personalizado para categorizar um item como definido pelo usuário.|Você pode usar a ação Resolver Conflito para decidir se deve usar as novas informações de categorização ou o valor definido pelo usuário anterior. Para obter mais informações sobre como resolver conflitos, consulte [Operações do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  
|**Não categorizado**|O item de catálogo não foi definido pelos pesquisadores do System Center Online e não foi enviado ao System Center Online para categorização, e o administrador não atribuiu um valor de categorização definido pelo usuário.|nenhuma.|Solicite a categorização ou personalize as informações do catálogo local.<br /><br /> Para obter mais informações sobre como solicitar categorização, consulte [Operações do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).<br /><br /> Para obter mais informações sobre como alterar a categoria do título de software, consulte [Operações do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  

> [!NOTE]  
>  Os itens de catálogo enviados ao System Center Online para categorização têm um estado de validação de **Pendente** em um site de administração central, mas continuam sendo exibidos com um estado de validação de **Não categorizado** nos sites primários filho.  

> [!NOTE]  
>  Depois que um conflito de categorização é resolvido, o item já não é validado como conflitante, a menos que as atualizações posteriores de categorização introduzam novas informações sobre o item.  

 Para obter exemplos de quando um estado de validação pode fazer a transição de um estado para outro, consulte [Exemplos de transições de estado de validação do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence.md).  
