---
title: Painel de cogerenciamento
titleSuffix: System Center Configuration Manager
description: Examine as informações sobre o cogerenciamento usando o painel.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
caps.latest.revision: 1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 380ca748921a806a0e5edf608a62e8a44edf4d84
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2018
---
# <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Painel de cogerenciamento no System Center Configuration Manager
*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A partir da versão 1802, você pode exibir um painel com informações sobre o cogerenciamento. O painel ajuda você a analisar os computadores cogerenciados no ambiente. Os grafos podem ajudar a identificar os dispositivos que podem precisar de atenção.<!--1356648-->

## <a name="open-the-co-management-dashboard"></a>Abrir o painel de cogerenciamento
Para abrir o painel de cogerenciamento, use as seguintes etapas: 

1. Abra o console do gerenciador de configurações. 
2. Clique no nó **Monitoramento**. 
3. Para carregar o painel, clique em **Cogerenciamento**.

## <a name="reviewing-information-in-the-co-management-dashboard"></a>Examinando as informações no painel de cogerenciamento

O painel de cogerenciamento mostra quatro grafos para o ambiente. 

- **Dispositivos cogerenciados** – fornece o percentual dos dispositivos cogerenciados no ambiente.

    ![Grafo de dispositivos cogerenciados](media\co-management-dashboard\Percent-Co-managed-graph.PNG)

- **Distribuição de sistemas operacionais cliente** – mostra o número de dispositivos cliente por sistema operacional e versão. Os seguintes agrupamentos são usados: </br>
    - Windows 7 e 8.x
    - Windows 10 inferior a 1709
    - Windows 10 1709 e posterior

         > [!NOTE] 
         > O Windows 10, versão 1709 e posterior, é um pré-requisito para o cogerenciamento.

     Focalizar uma seção do grafo fornecerá o percentual de dispositivos no agrupamento de sistema operacional selecionado.

     ![Grafo de distribuição de sistemas operacionais cliente](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)

- **Status de cogerenciamento** – a divisão de êxito ou falha do dispositivo nas seguintes categorias:
    - Sucesso, Ingressado no Azure AD híbrido
    - Sucesso, Ingressado no Azure AD
    - Falha: falha no registro automático
    
     Focalizar uma seção do grafo fornecerá o percentual de dispositivos na categoria. 

     ![Grafo de status para o cogerenciamento](media\co-management-dashboard\Co-management-status-graph.PNG)

     Clicar em uma seção do grafo levará você para uma lista de dispositivos da categoria.
 
     ![Lista de dispositivos com falha de registro](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


- **Transição de carga de trabalho** – exibe um gráfico de barras com o número de dispositivos transferidos para o Microsoft Intune para as quatro cargas de trabalho disponíveis:
    - Políticas de conformidade
    - Acesso de Recurso
    - Windows Update for Business
    - Endpoint Protection

     Focalizar uma seção do gráfico fornecerá o número de dispositivos que fizeram a transição para a carga de trabalho. 
     ![Grafo de barras de transição de carga de trabalho](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o cogerenciamento, consulte:
 - [Cogerenciamento de dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview.md)
 - [Preparar dispositivos Windows 10 para cogerenciamento](/sccm/core/clients/manage/co-management-prepare.md)

    
