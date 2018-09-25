---
title: Painel de cogerenciamento
titleSuffix: Configuraton Manager
description: Examine as informações sobre o cogerenciamento usando o painel.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3d4cbbf78639a135e9e36e3402f9920a6ef71ed
ms.sourcegitcommit: 78d2dce465e3500653b252583a6903a006784c26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46448779"
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
 - [Cogerenciamento de dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview)
 - [Preparar dispositivos Windows 10 para cogerenciamento](/sccm/core/clients/manage/co-management-prepare)

    
