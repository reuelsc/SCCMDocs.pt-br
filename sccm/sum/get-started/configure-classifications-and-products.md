---

title: "Configurar classificações e produtos para sincronizar | System Center Configuration Manager"
description: "Siga estas etapas para configurar classificações e produtos para sincronizar no console do Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 46cf461c92348e1a90533518355f2b5982ae5770



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
    > - **Upgrade**: especifica uma atualização para os recursos e funcionalidades do Windows 10.  
    >   
    >      Seus sites e pontos de atualização de software devem executar o WSUS 4.0 com o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para obter a classificação de **Upgrade**.  

5.  Na guia **Produtos** , especifique os produtos para os quais você deseja sincronizar atualizações de software e clique em **Fechar**.  

    > [!NOTE]  
    >  Os metadados de cada atualização de software definem os produtos aos quais a atualização é aplicável. Um produto é uma edição específica de um aplicativo ou sistema operacional, como o Windows Server 2012. Uma família de produtos é o sistema operacional base ou o aplicativo do qual os produtos individuais são derivados. Um exemplo de uma família de produtos é o Windows, do qual o Windows Server 2012 é membro. Você pode especificar uma família de produtos ou produtos individuais dentro de uma família de produtos. Quanto mais produtos você selecionar, mais tempo irá demorar a sincronizar as atualizações de software.  
    >   
    >  Quando as atualizações de software são aplicáveis a vários produtos, e no mínimo um dos produtos é selecionado para sincronização, todos os produtos aparecerão no console do Configuration Manager, mesmo se alguns produtos não forem selecionados. Por exemplo, se o Windows Server 2012 for o único sistema operacional que você selecionou, e se uma atualização de software se aplicar ao Windows 8 e ao Windows Server 2012, ambos os produtos serão exibidos no console do Configuration Manager.  

    > [!IMPORTANT]  
    >  O Configuration Manager armazena uma lista de produtos e famílias de produtos que você pode escolher ao instalar o ponto de atualização de software pela primeira vez. Os produtos e as famílias de produtos que forem lançados após o lançamento do Configuration Manager podem não estar disponíveis para seleção até que você conclua a sincronização das atualizações de software, o que atualizará a lista de produtos e famílias de produtos disponíveis para você escolher.  


## <a name="next-steps"></a>Próximas etapas
Inicie a sincronização de atualizações de software para recuperar atualizações de software com base nos novos critérios. Para ver mais detalhes, consulte [Sincronizar atualizações de software](synchronize-software-updates.md).



<!--HONumber=Nov16_HO1-->


