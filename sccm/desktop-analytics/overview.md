---
title: Análise de Área de Trabalho
titleSuffix: Configuration Manager
description: Uma visão geral do serviço de análise de desktop integrado com o Configuration Manager.
ms.date: 07/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fd86e5bd939ecd356a6cf290958a766266248645
ms.sourcegitcommit: 75f48834b98ea6a238d39f24e04c127b2959d913
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2019
ms.locfileid: "68604481"
---
# <a name="what-is-desktop-analytics"></a>O que é o desktop Analytics?

> [!Note]  
> Essas informações se relacionam a um serviço de visualização que pode ser substancialmente modificado antes de ser lançada comercialmente. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

O desktop Analytics é um serviço baseado em nuvem que se integra ao Configuration Manager. O serviço fornece informações e inteligência para você tomar decisões mais informadas sobre a prontidão de atualização de seus clientes Windows. Ele combina dados de sua organização com dados agregados de milhões de dispositivos conectados aos serviços de nuvem da Microsoft.

Use a análise de desktop com Configuration Manager para:  

- Criar um inventário de aplicativos em execução na sua organização  

- Avaliar a compatibilidade de aplicativos com as atualizações de recursos mais recentes do Windows 10  

- Identificar problemas de compatibilidade e receber sugestões de mitigação com base em informações de dados habilitadas para nuvem  

- Criar grupos-piloto que representam todo o aplicativo e o estado do driver em um conjunto mínimo de dispositivos  

- Implantar o Windows 10 em dispositivos de piloto e de produção gerenciados  

![Captura de tela da análise de desktop home page no portal do Azure](media/portal-home.png)

> [!Note]  
> A análise de desktops é uma sucessora do Windows Analytics. O serviço *análise do Windows* inclui Upgrade Readiness, Conformidade de Atualizações e integridade do dispositivo.
>
> Todos esses recursos são combinados no serviço de *análise de desktop* . A análise de desktops também é mais rigorosamente integrada ao Configuration Manager.



## <a name="benefits"></a>Benefícios

Muitos clientes têm desafios para se obter e se manter atualizado com o Windows 10. O principal desafio é testar aplicativos. Esse processo é normalmente manual. É demorado para os administradores de ti e os proprietários de aplicativos analisarem continuamente os aplicativos existentes. Em seguida, corrija todos os problemas que surgirem.

A análise de desktops oferece os seguintes benefícios:

- **Inventário de dispositivo e software**: Inventário de fatores principais, como aplicativos e versões do Windows.  

- **Identificação do piloto**: Identificação do menor conjunto de dispositivos que fornece a maior cobertura de fatores. Ele se concentra nos fatores que são mais importantes para um piloto de atualizações e upgrades do Windows. Garantir que o piloto seja mais bem-sucedido permite que você prossiga com mais rapidez e confiança para implantações amplas em produção.  

- **Identificação do problema**: Usando dados agregados do mercado junto com os dados do seu ambiente, o serviço prevê possíveis problemas para obter e se manter atualizado com o Windows. Em seguida, ele sugere possíveis mitigações.  

- **Integração do Configuration Manager**: A nuvem de serviço-habilita sua infraestrutura local existente. Use esses dados e a análise para implantar e gerenciar o Windows em seus dispositivos.  



## <a name="prerequisites"></a>Pré-requisitos

Para usar a análise de desktop, verifique se seu ambiente atende aos seguintes pré-requisitos.


### <a name="technical"></a>Technical

- Uma assinatura ativa do Azure, com permissões de [administrador global](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator) . Não há suporte para [contas da Microsoft](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) .  

    > [!Important]  
    > Atualmente, a análise de desktops é oferecida como um serviço do Office 365 e requer uma assinatura do Office 365 em seu locatário do Azure AD. Isso pode não ser um requisito no futuro.

    - Permissões de proprietário ou **colaborador** do **espaço de trabalho** para **configurar seu espaço de trabalho**e as seguintes funções:  

      - Função de [**administrador do desktop Analytics**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) .

      - [**Log Analytics colaborador**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) e [**administrador de acesso do usuário**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) no grupo de recursos para usar um espaço de trabalho existente ou criar um novo espaço de trabalho em um grupo de recursos existente.

      - Permissões de [**proprietário**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner), ou [**colaborador**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) e [**administrador de acesso de usuário**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) na assinatura para criar um espaço de trabalho em um novo grupo de recursos.  

- Configuration Manager, versão 1902 com pacote cumulativo de atualizações (4500571) ou posterior. Para obter mais informações, consulte [Update Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    - Função de [**administrador completo**](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_Planroles) no Configuration Manager  

    > [!Note]  
    > O desktop Analytics dá suporte a uma ID comercial por locatário Azure Active Directory (Azure AD) e hierarquia de Configuration Manager. Se você tiver várias hierarquias em seu ambiente, use IDs comerciais e locatários do Azure AD diferentes.<!-- 4958160 -->

- Dispositivos que executam o Windows 7, Windows 8.1 ou Windows 10  

    - Instale as atualizações mais recentes. Para obter mais informações, consulte [Atualizar dispositivos](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Os dispositivos também precisam ter o cliente Configuration Manager, versão 1902 com pacote cumulativo de atualizações (4500571) ou posterior. Para obter mais informações, consulte [Update Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    > [!Note]  
    > O desktop Analytics não dá suporte a atualizações para o LTSC (canal de manutenção de longo prazo) do Windows 10. Para obter mais informações, consulte [visão geral do Windows como um serviço](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > O desktop Analytics foi projetado para dar melhor suporte ao cenário de atualização in-loco. Se você precisar fazer grandes alterações, como de 32 a a arquitetura de 64 bits, use um cenário de geração de imagens. As informações de análise de desktop ainda são valiosas nesses cenários de implantação de sistema operacional clássicos, mas você pode ignorar as diretrizes específicas de atualização in-loco. Para obter mais informações, consulte [cenários para implantar sistemas operacionais corporativos com Configuration Manager](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems).

- Dados de diagnóstico do Windows. Para obter mais informações, confira os seguintes artigos:  

    - [Níveis de dados de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [Privacidade do desktop Analytics](/sccm/desktop-analytics/privacy)  

- Conectividade de rede de dispositivos para a nuvem pública da Microsoft. Para obter mais informações, consulte [como habilitar o compartilhamento de dados](/sccm/desktop-analytics/enable-data-sharing)  


### <a name="licensing-and-costs"></a>Licenciamento e custos

A análise de desktops requer uma das seguintes assinaturas de licença:

- Windows 10 Enterprise E3 ou e5; ou Microsoft 365 F1, E3 ou e5  

- Educação do Windows 10 a3 ou a5; ou Microsoft 365 a3 ou a5  

- Windows VDA E3 ou e5  

Além do custo das assinaturas de licença, não há nenhum custo adicional para usar a análise de desktops. No Log Analytics do Azure, a análise de desktops é "classificada como zero". Essa classificação significa que ela é excluída dos limites e dos custos de dados, independentemente do tipo de preço do Azure Log Analytics escolhido. Para obter mais informações sobre os tipos de preço do Azure Log Analytics, consulte [log Analytics de preços](https://azure.microsoft.com/pricing/details/monitor/).

- Se você usar a camada gratuita, que tem um limite na quantidade de dados coletados por dia, os dados de análise da área de trabalho não são considerados nesse limite. Você pode coletar todos os dados de análise de desktop de seus dispositivos e ainda ter o limite completo disponível para coletar dados adicionais de outras fontes.

- Se você usar uma camada paga que cobra por GB de dados coletados, não será cobrado pelos dados de análise de desktop. Você pode coletar todos os dados de análise de desktop de seus dispositivos e não incorrer em nenhum custo.

> [!Note]  
> Diferentes planos de Log Analytics do Azure têm períodos de retenção de dados diferentes. A análise de desktops herda a política de retenção de dados do espaço de trabalho. Se o seu espaço de trabalho estiver no plano gratuito, a análise de desktops manterá os últimos 30 dias de "instantâneos diários" que são coletados no espaço de trabalho.


## <a name="next-steps"></a>Próximas etapas

O tutorial a seguir fornece um guia passo a passo para a introdução ao desktop Analytics e Configuration Manager:  

- [Implantar o Windows 10 para o piloto](/sccm/desktop-analytics/tutorial-windows10)  
