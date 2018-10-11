---
title: Como analisar e converter pacotes
titleSuffix: Configuration Manager
description: Saiba como analisar e converter pacotes com o Gerenciador de Conversão de Pacotes no Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f3bf1737-827d-48fa-8bb1-f48fe71afe0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9c58e12d906606acc0015d38e543616570d61520
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297165"
---
# <a name="how-to-analyze-and-convert-packages-with-package-conversion-manager"></a>Como analisar e converter pacotes com o Gerenciador de Conversão de Pacotes

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1357861-->

Antes de converter um pacote, primeiro analise-o. Dependendo dos resultados da análise, é possível executar uma das seguintes tarefas:

- **Converta** o pacote em um aplicativo. Na lista **Pacote** no console, o estado de preparação exibe **Automático**.  

- **Corrigir e Converter** o pacote, anexar coleções e criar condições globais. Na lista **Pacote** no console, o estado de preparação exibe **Automático**.  

- Aplique**Corrigir e Converter** ao pacote. Na lista **Pacote** no console, o estado de preparação exibe **Manual**.  

- Deixe o pacote não convertido. Na lista **Pacote** no console, o estado de preparação exibe **Não Aplicável**.  



## <a name="bkmk_analyze"></a> Como analisar pacotes

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**. Expanda **Gerenciamento de Aplicativos** e selecione o nó **Pacotes**.  

2. Selecione o pacote a ser convertido. Na guia **Início** da faixa de opções, no grupo **Conversão de Pacote**, selecione **Analisar Pacote**. O Gerenciador de Conversão de Pacotes analisa o pacote.  

3. Para conferir o estado de preparação do pacote, adicione a coluna **Preparação** à lista de pacotes. O estado de preparação do pacote determina sua próxima ação:  

    - **Automático**: [como converter pacotes](#bkmk_convert)  

        Para também anexar coleções e criar condições globais com um estado de preparação **Automático**, confira [Como corrigir e converter pacotes](#bkmk_fix).  

    - **Manual**: [como corrigir e converter pacotes](#bkmk_fix)

    - **Não aplicável**: este pacote não possui um programa ou conteúdo necessário. Adicione qualquer programa ou conteúdo necessário e tente realizar a análise novamente. Ou deixe-o em um estado não convertido e continue a implantá-lo como um pacote.  



## <a name="bkmk_convert"></a> Como converter pacotes

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**. Expanda **Gerenciamento de Aplicativos** e selecione o nó **Pacotes**.  

2. Selecione o pacote para converter com um estado de preparação de **Automático**. Na guia **Início** da faixa de opções, no grupo **Conversão de Pacote**, selecione **Converter Pacote**. O assistente Converter Pacote em Aplicativo é aberto.  

3. No assistente Converter Pacote em Aplicativo, revise a lista de pacotes selecionados. Remova todos os pacotes que você não deseja converter e selecione **OK**. O Gerenciador de Conversão de Pacotes converte o pacote. A janela Conversão Concluída lista o status de conversão dos novos aplicativos.  

    > [!Note]  
    > Quando você converte um pacote, o site registra a data e a hora da conversão como a hora UTC.  

4. Siga as instruções na janela. Selecione **Exibir aplicativos** ou **Fechar**.  



## <a name="bkmk_fix"></a> Como corrigir e converter pacotes

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**. Expanda **Gerenciamento de Aplicativos** e selecione o nó **Pacotes**.  

2. Selecione um pacote com um estado de preparação de **Manual** ou **Automático**. Na guia **Início** da faixa de opções, no grupo **Conversão de Pacote**, selecione **Corrigir e Converter**.  

3. No Assistente de Conversão de Pacote, examine as informações na página **Seleção de Pacote**, observando os **Itens para Correção**. Em seguida, selecione **Avançar**.  

4. Na página **Análise de Dependência**, revise se o pacote depende de outros pacotes listados e, em seguida, selecione **Avançar**.  

    > [!Note]  
    > Se você não converteu nenhum dos pacotes dependentes listados, primeiro converta esses pacotes. Em seguida, reinicie o processo de conversão do pacote.  
    >  
    > Se uma dependência não for necessária, exclua-a ou ignore-a e continue o processo de conversão.  

5. Na página **Tipo de Implantação**, revise os tipos de implantação para o novo aplicativo. Altere suas prioridades ou exclua os tipos de implantação.  

6. Se algum dos novos tipos de implantação não tiver um método de detecção associado, a coluna **Método de Detecção** exibe um ícone de aviso. Conclua as seguintes ações:  

    1. Selecione **Editar Método de Detecção**.  

    2. Selecione **Adicionar**.  

    3. Na caixa de diálogo Regra de Detecção, especifique um **Tipo de Configuração**.  

    4. Para o tipo de configuração especificado, insira as informações adicionais necessárias para a regra de detecção.  

    5. Selecione **OK**. Se necessário, repita esse processo para adicionar vários métodos de detecção a cada tipo de implantação.  

    6. Selecione **OK**. Verifique se a coluna **Método de Detecção** exibe um ícone para confirmar um método de detecção especificado corretamente.  

7. Selecione **Avançar**.  

8. Na página **Seleção de Requisitos**, revise os tipos de implantação do novo aplicativo. Selecione um tipo de implantação e revise os requisitos desse tipo de implantação.  

    > [!Note]  
    > O assistente exibe apenas os requisitos que o Gerenciador de Conversão de Pacotes converte. Ele não converte todas as consultas WQL na coleção de dispositivos em requisitos.  

9. Adicione requisitos para um tipo de implantação selecionado, se necessário.  

10. Selecione **Avançar**.  

11. Conclua o assistente para criar o aplicativo.  

    > [!Note]  
    > Quando você converte um pacote, o site registra a data e a hora da conversão como a hora UTC.  



## <a name="bkmk_monitor"></a> Monitorar

Acesse a área de trabalho **Monitoramento** do console do Configuration Manager e selecione **Status de Conversão do Pacote**. Esse painel mostra o estado geral de análise e conversão de pacotes no site. Uma nova tarefa em segundo plano resume automaticamente os dados de análise.

> [!Tip]  
> O Gerenciador de Conversão de Pacotes integrado ao Configuration Manager não exige que você agende a análise de pacotes. Essa ação é realizada pela tarefa de resumo integrada.

![Captura de tela do exemplo Painel do Status de Conversão de Pacote](media/1357861-pcm-dashboard.png)
