---
title: Configurar classificações e produtos
titleSuffix: Configuration Manager
description: Siga estas etapas para configurar as classificações e os produtos de atualização de software a serem sincronizados no console do Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/15/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.collection: M365-identity-device-management
ms.openlocfilehash: f1d984598288434aa1e81c6bd2c51a315edfa551
ms.sourcegitcommit: fd16fc2b681608fd6def5bad2cedffbcd1f2423a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/18/2019
ms.locfileid: "56405685"
---
#  <a name="configure-classifications-and-products-to-synchronize"></a>configurar classificações e produtos para sincronizar  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


> [!NOTE]  
>  Use o procedimento desta seção somente no site de nível superior.  

 Os metadados de atualizações de software são recuperados durante o processo de sincronização no Configuration Manager com base nas configurações que você especificar nas propriedades do componente de Ponto de Atualização de Software. Depois de sincronizar as atualizações de software pela primeira vez ou quando novos produtos e classificações forem lançados, você deverá ir para as propriedades para selecionar os novos itens. Use o procedimento a seguir para configurar as classificações e os produtos para sincronizar.  

#### <a name="to-configure-classifications-and-products-to-synchronize"></a>Para configurar classificações e produtos para sincronizar  

1.  No console do **Configuration Manager**, navegue até **Administração** > **Configuração de Site** > **Sites**.

2. Selecione o site de administração central ou um site primário autônomo.  

3.  Na guia **Início** , no grupo **Configurações** , clique em **Configurar Componentes do Site**e **Ponto de Atualização de Software**.

4.  Na guia **Classificações** , especifique as classificações de atualização de software para as quais você deseja sincronizar atualizações de software.  

    > [!NOTE]  
    >  Cada atualização de software é definida com uma classificação de atualização que ajuda a organizar os diferentes tipos de atualização. Durante o processo de sincronização, os metadados de atualizações de software para as classificações especificadas são sincronizados. O Configuration Manager fornece a capacidade de sincronizar atualizações de software com as seguintes classificações de atualização:  
    >   
    > - **Atualizações Críticas**: especifica uma correção lançada em larga escala para um problema específico que corrige um bug crítico não relacionado a segurança.  
    > - **Atualizações de definições**: especifica uma atualização de software frequente e lançada em larga escala que contém adições ao banco de dados de definição de um produto.  
    > - **Feature Packs**: especifica novas funcionalidades de produtos distribuídas pela primeira vez fora de um lançamento de produto e que normalmente são incluídas no próximo lançamento do produto completo.  
    > - **Atualizações de Segurança**: especifica uma correção lançada em larga escala para uma vulnerabilidade relacionada à segurança específica do produto.  
    > - **Service Packs**: especifica um conjunto cumulativo e testado de todos os hotfixes, atualizações de segurança, atualizações críticas e atualizações aplicadas a um produto. Além disso, os service packs podem conter correções adicionais para problemas encontrados internamente desde o lançamento do produto.  
    > - **Ferramentas**: Especificam um utilitário ou um recurso que ajuda a concluir uma ou mais tarefas.  
    > - **Pacotes cumulativos de atualizações**: especifica um conjunto cumulativo e testado de hotfixes, atualizações de segurança, atualizações críticas e atualizações combinadas para facilitar a implantação. Um pacote cumulativo de atualizações geralmente aborda uma área específica, como segurança ou um componente do produto.  
    > - **Atualizações**: especifica uma correção lançada em larga escala para um problema específico. Uma atualização corrige um bug não crítico não relacionado à segurança.  
    > - **Atualização**: especifica uma atualização para os recursos e funcionalidades do Windows 10. Seus sites e pontos de atualização de software devem executar o WSUS 4.0 com o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para obter a classificação de **Upgrade**.    
    >       

    > [!NOTE]    
    > Começando com o Configuration Manager versão 1706, você pode marcar a caixa de seleção **Incluir atualizações de drivers e de firmware do Microsoft Surface** para sincronizar os drivers do Microsoft Surface.<!--1098490--> Todos os pontos de atualização de software devem executar o Windows Server 2016 para sincronizar com êxito os drivers do Surface. Se você habilitar um ponto de atualização de software em um computador que executa o Windows Server 2012 depois de habilitar os drivers do Surface, os resultados da verificação das atualizações de driver não serão precisos. Isso resulta na exibição de dados de conformidade incorretos no console do Configuration Manager e nos relatórios do Configuration Manager.  
    >  
    > Esse recurso foi introduzido pela primeira vez na versão 1706 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1710, esse recurso deixou de ser um recurso de pré-lançamento.  
    >  
    > O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, veja [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

5.  Na guia **Produtos** , especifique os produtos para os quais você deseja sincronizar atualizações de software e clique em **Fechar**.  

    > [!NOTE]  
    >  Os metadados de cada atualização de software definem os produtos aos quais a atualização é aplicável. Um produto é uma edição específica de um aplicativo ou sistema operacional, como o Windows Server 2012. Uma família de produtos é o sistema operacional base ou o aplicativo do qual os produtos individuais são derivados. Um exemplo de uma família de produtos é o Windows, do qual o Windows Server 2012 é membro. Você pode especificar uma família de produtos ou produtos individuais dentro de uma família de produtos. Quanto mais produtos você selecionar, maior será o tempo para sincronizar as atualizações de software.  
    >   
    >  Quando as atualizações de software forem aplicáveis a vários produtos e pelo menos um dos produtos for selecionado para sincronização, todos os produtos aparecerão no console do Configuration Manager, mesmo que nem todos os produtos tenham sido selecionados. Por exemplo, se você selecionar somente o Windows Server 2012 e uma atualização de software for aplicável ao Windows 8 e ao Windows Server 2012, ambos os produtos serão exibidos no console do Configuration Manager.  

    > [!IMPORTANT]  
    >  O Configuration Manager armazena uma lista de produtos e famílias de produtos que você pode escolher ao instalar o ponto de atualização de software pela primeira vez. Os produtos e as famílias de produtos que forem lançados após o lançamento do Configuration Manager podem não estar disponíveis para seleção até que você conclua a sincronização das atualizações de software, o que atualizará a lista de produtos e famílias de produtos disponíveis para você escolher.  

## <a name="next-steps"></a>Próximas etapas
Inicie a sincronização de atualizações de software para recuperar atualizações de software com base nos novos critérios. Para ver mais detalhes, consulte [Sincronizar atualizações de software](synchronize-software-updates.md).
