---
title: "configurar classificações e produtos para sincronizar"
titleSuffix: Configuration Manager
description: "Siga estas etapas para configurar classificações e produtos para sincronizar no console do Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: f36ff74b794e57b51742c40d10bd25a9cb4a13a5
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
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
    > - **Atualizações críticas**: especifica uma atualização lançada em larga escala para um problema específico que aborda um bug crítico não relacionado à segurança.  
    > - **Atualizações de definições**: especifica uma atualização para vírus ou outros arquivos de definição.  
    > - **Feature Packs**: especifica novos recursos de produtos que são distribuídos fora de um lançamento de produto e que normalmente são incluídos no próximo lançamento do produto completo.  
    > - **Atualizações de segurança**: especifica uma atualização lançada em larga escala para um problema de um produto em específico relacionado à segurança.  
    > - **Service Packs**: especifica um conjunto cumulativo de hotfixes que são aplicados a um aplicativo. Estes hotfixes podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim por diante.  
    > - **Ferramentas**: especifica um utilitário ou um recurso que ajuda a concluir uma ou mais tarefas.  
    > - **Pacotes cumulativos de atualizações**: especifica um conjunto cumulativo de hotfixes que são reunidos para facilitar a implantação. Esses hotfixes podem incluir atualizações de segurança, atualizações críticas, atualizações e assim por diante. Um pacote cumulativo de atualizações geralmente aborda uma área específica, como segurança ou um componente do produto.  
    > - **Atualizações**: especifica uma atualização para um aplicativo ou arquivo que está atualmente instalado.  
    > - **Upgrade**: especifica uma atualização para os recursos e funcionalidades do Windows 10. Seus sites e pontos de atualização de software devem executar o WSUS 4.0 com o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para obter a classificação de **Upgrade**.    
    >       

    > [!NOTE]    
    > A partir do Configuration Manager versão 1706, você pode marcar a caixa de seleção **Incluir drivers e atualizações de firmware do Microsoft Surface** para sincronizar os drivers do Microsoft Surface. Todos os pontos de atualização de software devem executar o Windows Server 2016 para sincronizar com êxito os drivers do Surface. Se você habilitar um ponto de atualização de software em um computador que executa o Windows Server 2012 depois de habilitar os drivers do Surface, os resultados da verificação das atualizações de driver não serão precisos. Isso resulta na exibição de dados de conformidade incorretos no console do Configuration Manager e nos relatórios do Configuration Manager.  
    > 
    > A caixa de seleção **Incluir drivers e atualizações de firmware do Microsoft Surface** está sempre disponível no Configuration Manager versão 1710. No entanto, esse é um recurso de pré-lançamento do Configuration Manager versão 1706 e você precisa ativá-lo para que fique disponível. Os recursos de pré-lançamento são recursos que estão na Ramificação atual para testes iniciais em um ambiente de produção. Esses recursos têm suporte total, mas ainda estão em desenvolvimento ativo e podem receber alterações até que saiam da categoria de pré-lançamento. Para obter mais informações, consulte [Usar recursos de pré-lançamento de atualizações](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

5.  Na guia **Produtos** , especifique os produtos para os quais você deseja sincronizar atualizações de software e clique em **Fechar**.  

    > [!NOTE]  
    >  Os metadados de cada atualização de software definem os produtos aos quais a atualização é aplicável. Um produto é uma edição específica de um aplicativo ou sistema operacional, como o Windows Server 2012. Uma família de produtos é o sistema operacional base ou o aplicativo do qual os produtos individuais são derivados. Um exemplo de uma família de produtos é o Windows, do qual o Windows Server 2012 é membro. Você pode especificar uma família de produtos ou produtos individuais dentro de uma família de produtos. Quanto mais produtos você selecionar, maior será o tempo para sincronizar as atualizações de software.  
    >   
    >  Quando as atualizações de software forem aplicáveis a vários produtos e pelo menos um dos produtos for selecionado para sincronização, todos os produtos aparecerão no console do Configuration Manager, mesmo que nem todos os produtos tenham sido selecionados. Por exemplo, se você selecionar somente o Windows Server 2012 e uma atualização de software for aplicável ao Windows 8 e ao Windows Server 2012, ambos os produtos serão exibidos no console do Configuration Manager.  

    > [!IMPORTANT]  
    >  O Configuration Manager armazena uma lista de produtos e famílias de produtos que você pode escolher ao instalar o ponto de atualização de software pela primeira vez. Os produtos e as famílias de produtos que forem lançados após o lançamento do Configuration Manager podem não estar disponíveis para seleção até que você conclua a sincronização das atualizações de software, o que atualizará a lista de produtos e famílias de produtos disponíveis para você escolher.  

## <a name="next-steps"></a>Próximas etapas
Inicie a sincronização de atualizações de software para recuperar atualizações de software com base nos novos critérios. Para ver mais detalhes, consulte [Sincronizar atualizações de software](synchronize-software-updates.md).
