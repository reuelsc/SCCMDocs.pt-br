---
title: Painel de cogerenciamento
titleSuffix: Configuration Manager
description: Use o painel de cogerenciamento para examinar as informações sobre dispositivos cogerenciados.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ad76140285df1c0125fcd2efab0f4794ed4881bf
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52455930"
---
# <a name="co-management-dashboard-in-configuration-manager"></a>Painel de cogerenciamento no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Iniciando na versão 1802, exiba um painel com informações sobre cogerenciamento. O painel ajuda você a analisar os computadores cogerenciados no ambiente. Os grafos podem ajudar a identificar os dispositivos que podem precisar de atenção.<!--1356648-->

No console do Configuration Manager, vá até o workspace **Monitoramento** e selecione o nó **Cogerenciamento**.

Da versão 1810 em diante, o painel de cogerenciamento foi aprimorado com informações mais detalhadas. <!--1358980-->



## <a name="dashboard-tiles"></a>Blocos de painel 

O painel de cogerenciamento mostra blocos diferentes, dependendo da versão do site. 


### <a name="co-managed-devices"></a>Dispositivos cogerenciado

*Aplica-se às versões 1802 e 1806*

Mostra o percentual de dispositivos cogerenciados no seu ambiente.
 ![Bloco de dispositivos cogerenciados](media\co-management-dashboard\Percent-Co-managed-graph.PNG)


### <a name="client-os-distribution"></a>Distribuição do sistema operacional cliente

*Aplica-se a todas as versões* 

Mostra o número de dispositivos do cliente por sistema operacional por versão. Este usa os seguintes agrupamentos:  
- Windows 7 e 8.x  
- Windows 10 inferior a 1709  
- Windows 10 1709 e posterior  

    > [!Tip]  
    > O Windows 10, versão 1709 e posterior, é um pré-requisito para o cogerenciamento.  

Focalize uma seção do gráfico para mostrar o percentual de dispositivos nesse grupo de sistema operacional.
 ![Bloco de distribuição do sistema operacional cliente](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)


### <a name="co-management-status-donut"></a>Status de cogerenciamento (rosca)

*Aplica-se às versões 1802 e 1806*

Mostra a divisão de êxito ou falha do dispositivo nas seguintes categorias:
- Sucesso, Ingressado no Azure AD híbrido  
- Sucesso, Ingressado no Azure AD  
- Falha: falha no registro automático  

Focalize uma seção do gráfico para mostrar o percentual de dispositivos nessa categoria. 
 ![Bloco de status de cogerenciamento (rosca)](media\co-management-dashboard\Co-management-status-graph.PNG)

Selecione uma seção do grafo para exibir a lista de dispositivos para essa categoria.
 ![Lista de dispositivos com falha de registro](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


### <a name="co-management-status-funnel"></a>Status de cogerenciamento (funil)

*Aplica-se à versão 1810 e posteriores*

Um gráfico de funil que mostra o número de dispositivos com os seguintes estados do processo de registro:  
- Dispositivos qualificados  
- Agendado  
- Registro iniciado  
- Inscrito  

![Bloco de status de cogerenciamento (funil)](media\co-management-dashboard\1358980-status-funnel.png)


### <a name="co-management-enrollment-status"></a>Status do registro de cogerenciamento

*Aplica-se à versão 1810 e posteriores*

Mostra a divisão de status do dispositivo nas seguintes categorias:
- Sucesso, ingressado no Azure AD híbrido  
- Sucesso, ingressado no Azure AD  
- Inscrição, ingressado no Azure AD híbrido  
- Falha, ingressado no Azure AD híbrido  
- Falha, ingressado no Azure AD  
- Entrada do usuário pendente  

Selecione um estado no bloco para detalhar uma lista de dispositivos nesse estado.  

![Bloco de status do registro de cogerenciamento](media\co-management-dashboard\1358980-enrollment-status.png)


### <a name="enrollment-errors"></a>Erros de registro

*Aplica-se à versão 1810 e posteriores*

Uma tabela que mostra a contagem de erros de registro de dispositivos.  


### <a name="workload-transition"></a>Transição da carga de trabalho

*Aplica-se a todas as versões*

Exibe um gráfico de barras com o número de dispositivos transferidos para o Microsoft Intune para as cargas de trabalho disponíveis. (A lista de cargas de trabalho varia de acordo com a versão do Configuration Manager. Para obter mais informações, confira [Cargas de trabalho que podem ser transferidas para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune).)

Focalize uma seção do gráfico para mostrar o número de dispositivos que fizeram a transição para a carga de trabalho. 
 ![Grafo de barras de transição de carga de trabalho](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o cogerenciamento, consulte:
 - [Cogerenciamento de dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview)
 - [Preparar dispositivos Windows 10 para cogerenciamento](/sccm/core/clients/manage/co-management-prepare)

    
