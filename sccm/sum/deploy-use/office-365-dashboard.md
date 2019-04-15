---
title: Painel de Gerenciamento de Clientes do Office 365
titleSuffix: Configuration Manager
description: Examinar as informações de clientes do Office 365 usando o painel de Gerenciamento de Clientes do Office 365
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/10/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.collection: M365-identity-device-management
ms.openlocfilehash: aff55aee5b2eaa584a6161452b4a232fab07412a
ms.sourcegitcommit: 1328b5bcf4e52fe459cb212f936038c69886693b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 04/10/2019
ms.locfileid: "59477049"
---
# <a name="office-365-client-management-dashboard"></a>Painel de Gerenciamento de Clientes do Office 365

A partir da versão 1802 do Configuration Manager, é possível examinar as informações de clientes do Office 365 no painel do Gerenciamento de Clientes do Office 365. O painel de gerenciamento de clientes do Office 365 exibe uma lista de dispositivos relevantes quando as seções de gráfico são selecionadas. <!--1357281 -->

## <a name="prerequisites"></a>Pré-requisitos

Os dados que são exibidos no painel de Gerenciamento de Clientes do Office 365 vêm de inventário de hardware. Habilite o inventário de hardware e selecione a classe de inventário de hardware **Configurações do Office 365 ProPlus** para que os dados sejam exibidos no painel.
 
1. Habilite inventário de hardware se ele ainda não estiver habilitado. Para mais detalhes, consulte [Configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).
2. No console do Configuration Manager, acesse **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  
3. Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  
4. No **configurações do cliente padrão** caixa de diálogo, clique em **inventário de Hardware**.  
5. No **configurações do dispositivo** clique em **Definir Classes**.  
6. Na caixa de diálogo **Classes de Inventário de Hardware**, selecione **Configurações do Office 365 ProPlus**.  
7. Clique em **OK** para salvar suas alterações e fechar o **Classes de inventário de Hardware** caixa de diálogo. 

O painel de Gerenciamento de Clientes do Office 365 começará a exibir dados à medida que o inventário de hardware for relatado.

## <a name="viewing-the-office-365-client-management-dashboard"></a>Visualização do painel de Gerenciamento de Clientes do Office 365

Para exibir o painel de Gerenciamento de Clientes do Office 365, no console do Configuration Manager, vá até **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Clientes do Office 365**. Na parte superior do painel, use a configuração suspensa **Coleção** para filtrar os dados do painel por membros de uma coleção específica. A partir do Configuration Manager versão 1802, o painel de gerenciamento de clientes do Office 365 exibe uma lista de dispositivos relevantes quando seções de gráfico são selecionadas.

O painel de Gerenciamento de Clientes do Office 365 fornece gráficos com as seguintes informações:

- Número de clientes do Office 365
- Versões do cliente do Office 365
- Idiomas do cliente do Office 365
- Canais de clientes do Office 365 Confira mais informações em [Visão geral dos canais de atualização do Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="bkmk_o365_readiness"></a> Integração para a preparação do Office 365 ProPlus
<!--3735402-->
A partir da versão 1902 do Configuration Manager, é possível usar o painel para identificar os dispositivos com alta confiança que estejam prontos para atualizar para o Office 365 ProPlus. Essa integração fornece informações sobre quaisquer possíveis problemas de compatibilidade com suplementos do Office e macros usadas em seu ambiente. Em seguida, use o Configuration Manager para implantar o Office em dispositivos prontos.

O painel de gerenciamento de clientes do Office 365 inclui um novo bloco, **Office 365 ProPlus Upgrade Readiness**. Esse bloco é um gráfico de barras de dispositivos nos seguintes estados:
- Não avaliado
- Pronto para atualizar
- Precisa de revisão

Selecione um estado para obter mais detalhes em uma lista de dispositivos. Este relatório de preparação mostra mais detalhes sobre os dispositivos. Ele inclui as colunas para o estado de compatibilidade de macros e suplementos do Office.

### <a name="prerequisites-for-office-365-proplus-readiness-integration"></a>Pré-requisitos para a integração da preparação do Office 365 ProPlus

- Habilitar inventário de hardware em configurações do cliente. Confira mais informações, na seção [Pré-requisitos](#prerequisites).  

- O dispositivo precisa de conectividade com a CDN (rede de distribuição de conteúdo) do Office para baixar um arquivo de preparação do suplemento. Para obter mais informações, veja [Redes de distribuição de conteúdo](https://docs.microsoft.com/office365/enterprise/content-delivery-networks). Se o dispositivo não pode baixar esse arquivo, o estado de suplementos é *Precisa de revisão*.  

    > [!Note]  
    > Nenhum dado é enviado à Microsoft para esse recurso.  

### <a name="bkmk_ort"></a> Preparação de macro detalhada

Por padrão, o agente de verificação examina a lista de arquivos MRU (usada mais recentemente) em cada dispositivo. Ele conta os arquivos nessa lista compatíveis com macros. Esses arquivos incluem os seguintes tipos:
- Formatos de arquivo do Office habilitados para macro, tais como pastas de trabalho do Excel habilitadas para macro (.xlsm) ou documento do Word habilitado para macro (.docm)  
- Formatos Office mais antigos que não indicam se há conteúdo de macro. Por exemplo, uma pasta de trabalho do Excel 97-2003 (.xls).

Se você precisar de uma avaliação mais detalhada, implante o **Readiness Toolkit for Office**. Essa ferramenta analisa o código dentro de um arquivo de macro. Ele verifica se há possíveis problemas de compatibilidade. Por exemplo, o arquivo usa uma função que foi alterada em uma versão mais recente do Office. Após executar o Readiness Toolkit for Office, o Configuration Manager pode usar seus resultados. Esses dados adicionais aprimoram o cálculo de preparação do dispositivo. Para obter mais informações, consulte [usar o Readiness Toolkit para avaliar a compatibilidade do aplicativo do Office 365 ProPlus](http://aka.ms/readinesstoolkit).

## <a name="next-steps"></a>Próximas etapas

[Gerenciar o Office 365 ProPlus com o Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates)