---
title: Gerenciar catálogos de atualização
titleSuffix: Configuration Manager
description: Gerenciar catálogos de atualizações de software para o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3bc66350205ac09a09ca5543adf022b00e2b027f
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896669"
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Gerenciar catálogos de atualizações de software no Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Use **Catálogos****Workspace** para gerenciar catálogos de atualizações de software. Isso inclui a adição de novos catálogos, o gerenciamento de assinaturas de catálogo existentes e a importação de informações sobre as atualizações de um catálogo no repositório do Updates Publisher.

Os catálogos de atualizações de software contêm informações sobre as atualizações relacionadas que são criadas por organizações diferentes da Microsoft. Outras organizações incluem sua própria organização e fornecedores de software de terceiros que registraram seus catálogos com a Microsoft. Catálogos registrados de fornecedores de software são chamados *catálogos de parceiros*. Os catálogos que você cria, e que não estão registrados com a Microsoft, são chamados de catálogos de*usuário*.

## <a name="add-software-update-catalogs"></a>Adicionar catálogos de atualizações de software
Você deve adicionar um catálogo de atualizações ao Updates Publisher antes de poder gerenciar as atualizações que ele contém. Quando você adiciona um catálogo, o Updates Publisher:
-   Cria uma assinatura para esse catálogo, para que possa verificar se há atualizações para esse catálogo.
-   Adiciona o catálogo a uma lista na janela **Meus Catálogos de Atualizações de Software** do **Workspace de Catálogos**.  

Confira informações sobre cada catálogo assinado no console. As informações incluem a URL ou local de download, o nome da empresa ou organização que criou o catálogo e quando ele foi importado ou modificado pela última vez.

O Updates Publisher pode verificar automaticamente as assinaturas em busca de alterações sempre que for iniciado. Isso é configurado como uma [Opção avançada](/sccm/sum/tools/updates-publisher-options#advanced). Quando configurado, o Updates Publisher consulta as informações de URL ou local de download da assinatura e envia um alerta quando houver alterações no catálogo que foram feitas desde a última vez que você o importou no repositório.

Para verificar manualmente uma atualização do catálogo, selecione o catálogo na lista **Meus Catálogos de Atualização de Software** e, em seguida, escolha **Atualizar** na faixa de opções.

Além de adicionar catálogos e exibir informações sobre os catálogos assinados, você pode:
-  **Editar** informações de catálogos de *usuário*.
-  **Excluir** (remover) um catálogo do Updates Publisher.
-  **Importar** atualizações de um catálogo no repositório do Updates Publisher. Quando você importa as atualizações, importa todas as atualizações contidas nesse catálogo. Em seguida, você pode exibir as atualizações no workspace de Atualizações, onde pode selecionar e publicar atualizações em seu servidor de atualização.

> [!NOTE]   
> A exclusão de um catálogo do Updates Publisher resulta na remoção das atualizações no catálogo de seu repositório. Isso não afeta as atualizações que você publicou em seu servidor de atualização. Para remover as atualizações de seu servidor de atualização que não estão mais em seu repositório, confira [Expirar atualizações de software sem referência](/sccm/sum/tools/updates-publisher-options#expire-unreferenced-software-updates).

## <a name="manage-update-catalogs"></a>Gerenciar catálogos de atualização
Veja a lista de catálogos que você importou na janela **Meus Catálogos de Atualizações de Software** do **Workspace de Catálogos**. Nesse workspace, você pode:

-   **Adicionar um catálogo de parceiros:** use um dos seguintes para localizar novos catálogos de parceiros:

    -   No console, acesse **Workspace de Atualizações** > **Visão geral**. Na janela **Introdução**, escolha **Adicionar Catálogos de Atualizações de Software de Parceiros**.

    -   No console, acesse **Workspace de Catálogos** > **Meus Catálogos**. Em seguida, na faixa de opções, escolha **Adicionar Catálogos**.

-   **Adicionar um catálogo de usuários:** No console, acesse **Workspace de Catálogos** > **Meus Catálogos**. Em seguida, na faixa de opções, escolha **Adicionar Catálogos**. Além do local do arquivo .cab, você deve especificar um Editor, Nome e Descrição para identificar o catálogo.


-   **Verificar se há atualizações dos catálogos:** Selecione um ou mais catálogos e, em seguida, selecione **Atualizar** na faixa de opções.

-   **Editar um catálogo de usuários:** Selecione um catálogo de *usuários* e, em seguida, **Editar** na faixa de opções. Depois, você pode modificar as propriedades definidas pelo usuário.

-   **Excluir catálogos:** selecione um ou mais catálogos e, em seguida, escolha **Remover** na faixa de opções. Isso remove o catálogo, sua assinatura e as atualizações desses catálogos de seu repositório do Updates Publisher.

-   **Adicionar atualizações de um catálogo ao seu repositório**: escolha **Importar** na faixa de opções para iniciar o assistente **Importar catálogo**. Para saber mais, veja [Importar atualizações](#import-updates)

## <a name="import-updates"></a>Importar atualizações
Quando você importa um catálogo, o Gerenciador de Atualizações adiciona as atualizações desse catálogo ao repositório do Updates Publisher. Após a importação das atualizações, você poderá publicá-las em seu servidor de atualização para disponibilizá-las para dispositivos gerenciados.

### <a name="to-import-updates"></a>Para importar atualizações
1. Para iniciar o assistente para **Importar Catálogo**, escolha **Importar** na faixa de opções em um dos seguintes workspaces:

   -   Workspace de Catálogos

   -   Workspace de Atualizações

2. Na página **Tipo de Importação**, selecione um ou mais catálogos que você adicionou ao Updates Publisher, ou especifique um caminho para um catálogo que você ainda não adicionou como uma assinatura. Escolha **Avançar** para exibir a tela de resumo e, quando estiver pronto, escolha **Avançar** para iniciar a importação.

3. Na janela **Aviso de Segurança – Validação de Catálogo**, examine o certificado do catálogo e, quando estiver pronto, escolha **Aceitar** para importar as atualizações.

   > [!CAUTION]
   > Aceite atualizações somente de editores confiáveis. As atualizações de software de editores que não são confiáveis pode danificar os computadores dos clientes ao verificar se há atualizações.
   > 
   >  Se você não confiar em um editor, remova esse editor da lista de editores confiáveis. Para saber mais sobre a aceitação de catálogos, clique em **Conte-me Mais** na caixa de diálogo **Aviso de Segurança – Validação de Catálogo**.

   Se você optar por sempre aceitar catálogos de um editor, esse editor será adicionado à [lista de editores confiáveis](/sccm/sum/tools/updates-publisher-options#trusted-publishers). Você pode revisar e editar essa lista como uma opção do Updates Publisher.

4. A importação ignora a importação de uma atualização quando a atualização já estiver no repositório e uma das seguintes opções for verdadeira:

   -   A atualização não sofreu alterações desde a última vez em que foi importada.

   -   A atualização foi editada e tem um novo hash digital. A edição de uma atualização impede que uma nova atualização substitua a original, pois isso substituiria as alterações que você pode ter implantado.

5. Na página **Confirmação**, revise os resultados da importação.

6. Clique em **Fechar** para concluir o assistente. Agora você pode exibir as atualizações para esse catálogo no Workspace de Atualizações.

## <a name="next-steps"></a>Próximas etapas
Depois de importar atualizações, as ações comuns incluem:
-   [Gerenciar atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher) para agrupar, atribuir e implantá-las em seu servidor de atualização.
-   [Criar regras de aplicabilidade](/sccm/sum/tools/updates-publisher-applicability-rules) para ajudar a determinar quando as atualizações são implantadas no servidor de atualização.
