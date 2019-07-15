---
title: 'Criar itens de configuração para Macs gerenciados pelo cliente '
titleSuffix: Configuration Manager
description: Use o item de configuração do Mac OS X do System Center Configuration Manager para gerenciar as configurações de dispositivos Mac OS X.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 346848bf3cd8b69b3bcecb479fb82250943dfd49
ms.sourcegitcommit: de3c86077bbf91b793e94e1f60814df18da11bab
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726165"
---
# <a name="create-configuration-items-for-mac-os-x-devices"></a>Criar itens de configuração para dispositivos Mac OS X
Use o item de configuração do **Mac OS X (personalizado)** do System Center Configuration Manager para gerenciar as configurações de dispositivos Mac OS X gerenciados pelo cliente do Configuration Manager.  
  
O sistema operacional Mac OS X usa arquivos de lista de propriedade (.plist) para armazenar configurações de aplicativo. Use as configurações de conformidade para avaliar e corrigir configurações em um arquivo de lista de propriedade. Você também pode gerenciar as configurações do Mac OS X escrevendo um script do shell que retorna um valor que pode ser avaliado e corrigido quanto à conformidade.  
  
## <a name="create-a-custom-mac-os-x-configuration-item"></a>Criar um item de configuração personalizado do Mac OS X  
  
1. No console do Configuration Manager, selecione **Ativos e Conformidade**.  
  
2. No espaço de trabalho **Ativos e Conformidade**, expanda **Configurações de Conformidade** e selecione **Itens de Configuração**.  
  
3. Na guia **Início**, no grupo **Criar**, selecione **Criar Item de Configuração**.  
  
4. Na página **Geral** do assistente para **Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5. Em **Especificar o tipo de item de configuração que deseja criar**, selecione **Mac OS X (personalizado)**.  
  
6. Se você quiser criar e atribuir categorias para ajudar a pesquisar e filtrar itens de configuração no console do Configuration Manager, selecione **Categorias**.  
  
7. Na página **Plataformas com Suporte** do assistente, selecione as versões específicas do Mac OS X que avaliarão o item de configuração.  
  
8. Na página **Configurações** do assistente, adicione novas configurações que serão avaliadas quanto à conformidade em computadores Mac. Selecione **Novo** para abrir a caixa de diálogo **Criar Configuração**.  
  
9. Na caixa de diálogo **Criar Configuração** , digite um nome exclusivo e uma descrição para a configuração.  
  
10. Escolha o **tipo de configuração** desejado e, em seguida, forneça as informações necessárias:  
  
    -   **Preferências do Mac OS X**  
  
        -   **ID de Aplicativo**: especifique a ID do aplicativo do arquivo de lista de propriedade do qual você deseja avaliar a conformidade de uma chave.  
  
             Por exemplo, se você quiser editar as configurações do navegador Safari, você pode usar **com.apple.Safari.plist**.  
  
        -   **Chave**: especifique o nome da chave cuja conformidade você deseja avaliar em computadores Mac. Use a seguinte sintaxe: */<dicionário\>/<nomechave\>*.  
  
            > [!IMPORTANT]  
            >  O nome de chave diferencia maiúsculas de minúsculas e não será avaliado se for diferente do nome de chave no computador Mac. Além disso, você não pode editar o nome da chave depois que especificá-la. Se você precisar editar o nome da chave, exclua e recrie a configuração.  
  
    -   **script**  
  
        -   **Script de Descoberta**: selecione **Adicionar Script** e insira um script do shell para avaliar a conformidade das configurações no computador Mac. Use o comando **echo** no script do Shell para retornar valores para o Configuration Manager para fins de conformidade. O Configuration Manager usa os resultados retornados em **STDOUT** para avaliar a conformidade.  
  
            > [!IMPORTANT]  
            >  Não inclua o comando **reboot** no script de descoberta. Como o script de descoberta é executado sempre que o cliente é reiniciado, isso fará com que o computador Mac seja reiniciado de forma contínua.  
  
        -   **Script de correção (opcional)**: opcionalmente, selecione **Adicionar Script** e insira um script de shell que é usado para corrigir quaisquer configurações não compatíveis encontradas em computadores cliente Mac.  
  
            > [!IMPORTANT]  
            >  Para garantir que você não introduza os caracteres de formatação que o computador Mac não pode interpretar, não use copiar e colar. Em vez disso, digite o script.  
  
11. Escolha o **Tipo de dados** que é o formato no qual a condição retorna os dados antes que sejam usados para avaliar a configuração.  
  
    > [!NOTE]  
    >  O **ponto flutuante** tipo de dados suporta apenas 3 dígitos após o ponto decimal.  
    >   
    >  O Configuration Manager não dá suporte ao uso do tipo de dados **Booliano** para parâmetros de script de item de configuração de Mac. Em vez disso, defina o tipo de dados como **Inteiro** e certifique-se de que o script retorna um valor inteiro.  
  
12. Selecione **OK** para salvar a configuração e fechar a caixa de diálogo **Criar Configuração**. Continue a adicionar quantas configurações forem necessárias.  
  
13. Na página **Regras de Conformidade** do assistente, especifique as condições que definem a conformidade de um item de configuração. Antes que uma configuração possa ser avaliada quanto à conformidade, ela deve ter pelo menos uma regra de conformidade. Selecione **Novo** para adicionar uma nova regra.  
  
14. Na caixa de diálogo **Criar Regra** , forneça as seguintes informações:  
  
    -   **Nome**: insira um nome para a regra de conformidade.  
  
    -   **Descrição:** insira uma descrição para a regra de conformidade.  
  
    -   **Configuração selecionada:** selecione **Procurar** para abrir a caixa de diálogo **Selecionar Configuração**. Selecione a configuração para a qual você deseja definir uma regra, ou selecione **Nova Configuração**. Ao terminar, escolha **Selecionar**.  
  
        > [!TIP]  
        >  Você também pode selecionar **Propriedades** para exibir informações sobre a configuração selecionada no momento.  
  
    -   **Tipo de regra**: Selecione o tipo de regra de conformidade que você deseja usar:  
  
        -   **Valor**: crie uma regra que compara o valor retornado pelo item de configuração com um valor especificado.  
  
        -   **Existential**: crie uma regra que avalia a configuração, caso ela exista em um dispositivo.  
  
    -   Para um tipo de regra de **Valor**, especifique as seguintes informações:  
  
        -   **A configuração deve estar em conformidade com a seguinte regra**: selecione um operador e um valor que será avaliado quanto à conformidade com a configuração selecionada. Você pode usar os seguintes operadores:  
  
            -   **Igual a**  
  
            -   **Não é igual a**  
  
            -   **Maior que**  
  
            -   **Menor que**  
  
            -   **Entre**  
  
            -   **Maior ou igual a**  
  
            -   **Menor ou igual a**  
  
            -   **Um dos**: na caixa de texto, especifique uma entrada em cada linha.  
  
            -   **Nenhum dos**: na caixa de texto, especifique uma entrada em cada linha.  
  
        -   **Corrigir regras não compatíveis quando houver suporte**: selecione esta opção se desejar que o Configuration Manager corrija automaticamente as regras não compatíveis.  
  
            > [!IMPORTANT]  
            >  Só é possível corrigir regras não compatíveis quando o operador de regra é definido como **É igual a**.  
  
        -   **Relatar não conformidade se esta instância de configuração não for encontrada**: o item de configuração relata a não conformidade se esta configuração não for encontrada no computador Mac.  
  
        -   **Gravidade de não conformidade para relatórios**: especifique o nível de gravidade relatado em caso de falha desta regra de conformidade. Os níveis de severidade disponíveis são:  
  
            -   **Nenhum**: computadores que não cumprem essa regra de conformidade não relatam uma gravidade de falha em relatórios do Configuration Manager.  
  
            -   **Informações**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações** em relatórios do Configuration Manager.  
  
            -   **Aviso**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso** em relatórios do Configuration Manager.  
  
            -   **Crítico**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager.  
  
            -   **Crítico com evento**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager. O computador cliente Mac também registra esse nível de severidade.  
  
    -   Para um tipo de regra de **Existential**, especifique as seguintes informações:  
  
        -   Escolha:  
  
            -   **A configuração deve existir em dispositivos cliente**  
  
            -   **A configuração não deve existir em dispositivos cliente**  
  
        -   **Gravidade de não conformidade para relatórios**: especifique o nível de gravidade relatado em caso de falha desta regra de conformidade. Os níveis de severidade disponíveis são:  
  
            -   **Nenhum**: computadores que não cumprem essa regra de conformidade não relatam uma gravidade de falha em relatórios do Configuration Manager.  
  
            -   **Informações**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações** em relatórios do Configuration Manager.  
  
            -   **Aviso**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso** em relatórios do Configuration Manager.  
  
            -   **Crítico**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager.  
  
            -   **Crítico com evento**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager. O computador cliente Mac também registra esse nível de severidade.  
  
        > [!NOTE]  
        >  As opções exibidas podem variar dependendo do tipo de configuração que está sendo usado para definir uma regra.  
  
15. Selecione **OK** para fechar a caixa de diálogo **Criar Regra**.  
  
16. Sobre o **resumo** , confirme as configurações para o novo item de configuração. Em seguida, conclua o assistente.  
  
Exiba o novo item de configuração no nó **Itens de Configuração** do espaço de trabalho **Ativos e Conformidade**.  
  
Se quiser adicionar esse item de configuração a uma linha de base de configuração, consulte [Como criar linhas de base de configuração para as configurações de conformidade no System Center Configuration Manager](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="next-steps"></a>Próximas etapas

 [Itens de configuração de dispositivos gerenciados com o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items.md)
