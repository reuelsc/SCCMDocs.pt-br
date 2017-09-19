---
title: "Criar itens de configuração para os Macs gerenciados pelo cliente – Configuration Manager | Microsoft Docs"
description: "Use o item de configuração do Mac OS X do System Center Configuration Manager para gerenciar as configurações de dispositivos Mac OS X."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
caps.latest.revision: "8"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 6910710badd0937cbdf1471e4f3f050590e2e769
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2017
---
# <a name="how-to-create-configuration-items-for-mac-os-x-devices-managed-with-the-system-center-configuration-manager-client"></a>Como criar itens de configuração para dispositivos Mac OS X gerenciados com o cliente do System Center Configuration Manager
Use o item de configuração do **Mac OS X (personalizado)** do System Center Configuration Manager para gerenciar as configurações de dispositivos Mac OS X que são gerenciados pelo cliente do Configuration Manager.  
  
 O sistema operacional Mac OS X usa arquivos de lista de propriedade (ou plist) para armazenar configurações de aplicativo. Use as configurações de conformidade para avaliar e corrigir configurações em um arquivo de lista de propriedade. Você também pode gerenciar as configurações do Mac OS X escrevendo um Script do Shell que retorna um valor que pode ser avaliado e corrigido quanto à conformidade.  
  
### <a name="to-create-a-custom-mac-os-x-configuration-item"></a>Para criar um item de configuração personalizado do Mac OS X  
  
1.  No console do Configuration Manager, clique em **Ativos e conformidade**.  
  
2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**e clique em **Itens de Configuração**.  
  
3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  
  
4.  Na página **Geral** do **Assistente para Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5.  Em **Especificar o tipo de item de configuração que deseja criar**, selecione **Mac OS X (personalizado)**.  
  
6.  Se você criar e atribuir categorias, clique em **Categorias** para ajudá-lo a pesquisar e filtrar itens de configuração no console do Configuration Manager.  
  
7.  Na página **Plataformas com Suporte** do assistente, selecione as versões específicas do Mac OS X que avaliarão o item de configuração.  
  
8.  Na página **Configurações** do assistente, você adicionará novas configurações que serão avaliadas quanto à conformidade em computadores Mac. Clique em **Novo** para abrir a caixa de diálogo **Criar Configuração** .  
  
9. Na caixa de diálogo **Criar Configuração** , digite um nome exclusivo e uma descrição para a configuração.  
  
10. Escolha o **Tipo de configuração** desejado e forneça as informações necessárias, como mostrado na seguinte tabela:  
  
    -   **Preferências do Mac OS X** -  
  
        -   **ID de Aplicativo** – Especifique a ID de aplicativo do arquivo de lista de propriedade no qual você deseja avaliar uma chave quanto à conformidade.  
  
             Por exemplo, se você quiser editar as configurações do navegador Safari, você pode usar **com.apple.Safari.plist**.  
  
        -   **Chave** – especifique o nome da chave que você deseja avaliar a conformidade em computadores Mac. Use a seguinte sintaxe: */<dicionário\>/<nomechave\>*.  
  
            > [!IMPORTANT]  
            >  O nome de chave diferencia maiúsculas de minúsculas e não será avaliado se for diferente do nome de chave no computador Mac. Além disso, você não pode editar o nome da chave depois que você o especificou. Se você precisar editar o nome da chave, exclua e recrie a configuração.  
  
    -   **Script** -  
  
        -   **Script de Descoberta** – Clique em **Adicionar Script**e insira um script do Shell para avaliar as configurações no computador Mac para fins de conformidade. Use o comando **echo** no script do Shell para retornar valores para o Configuration Manager para fins de conformidade. O Configuration Manager usa os resultados retornados em **STDOUT** para avaliar a conformidade.  
  
            > [!IMPORTANT]  
            >  Não inclua o comando **reboot** no script de descoberta. Como o script de descoberta é executado sempre que o cliente é reiniciado, isso fará com que o computador com Mac seja reiniciado de forma contínua.  
  
        -   **Script de correção (opcional)** – Opcionalmente, clique em **Adicionar Script** e insira um script de shell que é usado para corrigir quaisquer configurações não compatíveis encontradas em computadores cliente Mac.  
  
            > [!IMPORTANT]  
            >  Para garantir que você não insira uma formatação de caracteres que não pode ser interpretada pelo computador Mac, não use copiar e colar, mas digite no script.  
  
11. Escolha o **Tipo de dados** que é o formato no qual a condição retorna os dados antes que sejam usados para avaliar a configuração.  
  
    > [!NOTE]  
    >  O **ponto flutuante** tipo de dados suporta apenas 3 dígitos após o ponto decimal.  
    >   
    >  O Configuration Manager não oferece suporte ao uso do tipo de dados **Booliano** para parâmetros de script de item de configuração de Mac. Em vez disso, defina o tipo de dados como **Inteiro** e certifique-se de que o script retorna um valor inteiro.  
  
12. Clique em **OK** para salvar a configuração e fechar a caixa de diálogo **Criar Configuração** e continue para adicionar quantas configurações forem necessárias.  
  
13. Na página **Regras de Conformidade** do assistente, você especificará as condições que definem a conformidade de um item de configuração. Antes que uma configuração possa ser avaliada quanto à conformidade, ela deve ter pelo menos uma regra de conformidade. Clique em **Novo** para adicionar uma nova regra.  
  
14. Na caixa de diálogo **Criar Regra** , forneça as seguintes informações:  
  
    -   **Nome:** Digite um nome para a regra de conformidade.  
  
    -   **Descrição:** Insira uma descrição para a regra de conformidade.  
  
    -   **Configuração selecionada:** Clique em **Procurar** para abrir o **Selecionar configuração** caixa de diálogo. Selecione a configuração que você deseja definir uma regra de, ou clique em **nova configuração**. Quando tiver terminado, clique em **Selecione**.  
  
        > [!TIP]  
        >  Você também pode clicar em **propriedades** para exibir informações sobre a configuração selecionada no momento.  
  
    -   **Tipo de regra:** selecione o tipo de regra de conformidade que deseja usar:  
  
        -   **Valor:** crie uma regra que compara o valor retornado pelo item de configuração com um valor especificado.  
  
        -   **Existential** - Crie uma regra que avalia a configuração dependendo se ela existir em um dispositivo.  
  
    -   Para um tipo de regra de **Valor**, especifique as seguintes informações:  
  
        -   A configuração deve estar em conformidade com a seguinte regra – Selecione um operador e um valor que será avaliado quanto à conformidade com a configuração selecionada. Você pode usar os seguintes operadores:  
  
            -   **Igual a**  
  
            -   **Não é igual a**  
  
            -   **Maior que**  
  
            -   **Menor que**  
  
            -   **Entre**  
  
            -   **Maior ou igual a**  
  
            -   **Menor ou igual a**  
  
            -   **Um dos** - Na caixa de texto, especifique uma entrada em cada linha.  
  
            -   **Nenhum dos** - Na caixa de texto, especifique uma entrada em cada linha.  
  
        -   **Corrigir regras não compatíveis quando houver suporte** – Selecione esta opção se desejar que o Configuration Manager corrija automaticamente as regras não compatíveis.  
  
            > [!IMPORTANT]  
            >  Só é possível corrigir regras não compatíveis quando o operador de regra é definido como **É igual a**.  
  
        -   **Relatar não conformidade se esta instância de configuração não for encontrada** – O item de configuração relata a não conformidade se esta configuração não for encontrada no computador Mac.  
  
    -   **Severidade de não conformidade para relatórios** - Especifique o nível de severidade relatado em caso de falha desta regra de conformidade. Os níveis de severidade disponíveis são os seguintes:  
  
        -   **Nenhum** - os computadores que não cumprem essa regra de conformidade não relatam uma severidade de falha em relatórios do Configuration Manager.  
  
        -   **Informações** - os computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações** em relatórios do Configuration Manager.  
  
        -   **Aviso** - os computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso** em relatórios do Configuration Manager.  
  
        -   **Crítico** - os computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager.  
  
        -   **Crítico com evento** - os computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager. Esse nível de severidade também é registrado pelo computador cliente Mac.  
  
    -   Para um tipo de regra de **Existential**, especifique as seguintes informações:  
  
        -   Escolha uma destas:  
  
            -   **A configuração deve existir em dispositivos cliente**  
  
            -   **A configuração não deve existir em dispositivos cliente**  
  
        -   **Severidade de não conformidade para relatórios:** Especifique o nível de severidade relatado se a regra de conformidade falhar. Os níveis de severidade disponíveis são os seguintes:  
  
            -   **Nenhum** - os computadores que não cumprem essa regra de conformidade não relatam uma severidade de falha em relatórios do Configuration Manager.  
  
            -   **Informações** - os computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações** em relatórios do Configuration Manager.  
  
            -   **Aviso** - os computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso** em relatórios do Configuration Manager.  
  
            -   **Crítico** - os computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager.  
  
            -   **Crítico com evento** - os computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager. Esse nível de severidade também é registrado pelo computador cliente Mac.  
  
        > [!NOTE]  
        >  As opções exibidas podem variar dependendo do tipo de configuração que está sendo usado para definir uma regra.  
  
    -   Clique em **OK** para fechar a caixa de diálogo **Criar Regra** .  
  
15. Na página **Resumo** , confirme as configurações para o novo item de configuração e, em seguida, conclua o assistente.  
  
 O novo item de configuração é exibido no nó **Itens de Configuração** do espaço de trabalho **Ativos e Conformidade** .  
  
 Se quiser adicionar esse item de configuração a uma linha de base de configuração, consulte [Como criar linhas de base de configuração para as configurações de conformidade no System Center Configuration Manager](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="see-also"></a>Consulte também  
 [Itens de configuração de dispositivos gerenciados com o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)
