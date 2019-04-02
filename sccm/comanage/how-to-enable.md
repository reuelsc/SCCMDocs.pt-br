---
title: Habilitar cogerenciamento
titleSuffix: Configuration Manager
description: Habilite o cogerenciamento no Configuration Manager para obter os benefícios imediatos rapidamente.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8fac7ac5-96a3-4ec1-85cb-623b26bf5b1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 37dce37551627394da2630fa591a3c803ae8343f
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754572"
---
# <a name="how-to-enable-co-management-in-configuration-manager"></a>Como habilitar o cogerenciamento no Configuration Manager

Ao habilitar o cogerenciamento, você pode obter benefícios imediatos. Quando estiver pronto, você poderá iniciar a transição de cargas de trabalho conforme necessário em seu ambiente.

Verifique se os pré-requisitos de cogerenciamento estão configurados antes de iniciar esse processo. Para obter mais informações, veja [Pré-requisitos](/sccm/comanage/overview#prerequisites).



## <a name="process"></a>Processar

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e escolha o nó **Cogerenciamento**. Clique em **Configurar cogerenciamento** na faixa de opções para abrir o **Assistente para Integração de Cogerenciamento**.  

2. Na página **Assinatura** do assistente, selecione **Entrar**. Entre no locatário do Intune e, em seguida, selecione **Avançar**.  

3. Na página **Habilitação**, escolha sua configuração **Registro automático no Intune**, **Piloto** ou **Todos**.   

    Essa ação habilita o registro automático do cliente no Intune para clientes existentes do Configuration Manager. Quando você escolhe **Piloto**, somente os clientes do Configuration Manager que são membros da coleção piloto são registrados automaticamente no Intune. Com essa opção, você pode habilitar o cogerenciamento em um subconjunto de clientes para testar inicialmente o cogerenciamento e distribuí-lo usando uma abordagem em fases.  

    > [!Note]  
    > Começando na versão 1806, o registro automático não é imediato para todos os clientes. Esse comportamento ajuda uma melhor escala do registro para ambientes de grande porte. O Configuration Manager torna o registro aleatório com base no número de clientes. Por exemplo, se o seu ambiente tem 100 mil clientes, quando você habilitar essa configuração, o registro ocorre durante vários dias.<!--1358003-->  

    Se você tem dispositivos baseados na Internet já registrados no Intune, copie a linha de comando nesta página. Você pode usar essa linha de comando para instalar o cliente do Configuration Manager como um aplicativo no Intune.

4. Na página **Cargas de Trabalho**, para cada carga de trabalho, escolha qual grupo de dispositivos mover para gerenciamento com o Intune. Para saber mais, confira [Cargas de trabalho](/sccm/comanage/workloads).  

    Se você quer habilitar o cogerenciamento, não precisa mudar as cargas de trabalho agora. Você poderá mudá-las mais tarde. Para saber mais, confira [Como mudar cargas de trabalho](/sccm/comanage/how-to-switch-workloads).  

    A configuração **Intune Piloto** muda a carga de trabalho associada apenas dos dispositivos da coleção piloto. A configuração **Intune** muda a carga de trabalho associada de todos os dispositivos Windows 10 cogerenciados.  

    > [!Important] 
    > Antes de mudar cargas de trabalho, não se esqueça de configurar e implantar corretamente a carga de trabalho correspondente no Intune. As cargas de trabalho sempre devem ser gerenciadas por uma das ferramentas de gerenciamento dos dispositivos.  

5. Na página **Preparo**, defina as seguintes configurações:  

    - **Piloto**: o grupo piloto contém uma ou mais coleções que você seleciona. Use esse grupo como parte de sua distribuição em fases do cogerenciamento. Comece com uma coleção de teste pequena e, em seguida, adicione mais coleções ao grupo piloto à medida que você distribui o cogerenciamento para mais usuários e dispositivos. É possível alterar as coleções no grupo piloto a qualquer momento.  

    - **Produção**: Configure o **Grupo de exclusão** com uma ou mais coleções. Os dispositivos que são membros de uma das coleções neste grupo são excluídos do uso do cogerenciamento.  

6. Para habilitar o cogerenciamento, conclua o assistente.  



## <a name="next-steps"></a>Próximas etapas

Agora que você habilitou o cogerenciamento, examine os seguintes artigos para conhecer os benefícios imediatos que você pode obter em seu ambiente:

- [Acesso condicional](/sccm/comanage/quickstart-conditional-access)  

- [Ações remotas do Intune](/sccm/comanage/quickstart-remote-actions)  

- [Integridade do cliente](/sccm/comanage/quickstart-client-health)  
