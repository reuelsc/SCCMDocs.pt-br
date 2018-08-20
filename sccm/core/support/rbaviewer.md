---
title: Ferramenta de administração baseada em funções
titleSuffix: Configuration Manager
description: Use a Ferramenta de Auditoria e a Administração Baseada em Funções de para modelar e auditar funções e escopos de segurança no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 19e0e61681e26a2fc666f67909864ba09b68691d
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386407"
---
# <a name="role-based-administration-and-auditing-tool"></a>Ferramenta de Administração e Auditoria Baseada em Funções

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A Ferramenta de Administração e Auditoria Baseada em Funções é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). Use essa ferramenta para as seguintes tarefas:

- Modelar funções de segurança com permissões específicas  

- Auditar os escopos de segurança e as funções de segurança que os outros usuários têm



## <a name="requirements"></a>requisitos

- Execute-a no mesmo computador que o console do Configuration Manager  

- Você tem a função de **Administrador Completo**, **Analista Somente Leitura** ou **Administrador de Segurança**  

- Atribuir a sua conta a **todos** os escopo de segurança e todas as coleções  

- (*Opcional*) Para analisar a segurança de pasta de relatório, você deve ter acesso ao SQL  

- (*Opcional*) Para analisar o relatório de detalhamento, execute essa ferramenta no servidor do sistema de site com a função de ponto de relatório



## <a name="procedures"></a>Procedimentos


### <a name="model-permissions-for-a-new-role"></a>Permissões de modelo para uma nova função

Use o procedimento a seguir para permissões de modelo para uma nova função que você deseja criar: 

1. Execute o **RBAViewer.exe**.  

2. Selecione as funções de segurança de base que você deseja criar ou comece com um conjunto de permissões vazio. Selecione as permissões necessárias.  

3. Clique em **Analisar** para ver a interface do usuário que essa função personalizada verá.  

    > [!Note]  
    > Para ver se há uma função de segurança existente que atenda às suas necessidades, mude para a guia **Similaridade**.  

4. Clique em **Exportar** para salvar a função como um arquivo XML. Em seguida, importe-a para o console do Configuration Manager. Para obter mais informações, consulte [Criar funções de segurança personalizadas](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole).


### <a name="audit-existing-security-scopes"></a>Escopos de segurança existentes de auditoria

Use o procedimento a seguir para fazer a auditoria de todos os usuários administrativos, coleções e escopos de segurança existentes no Configuration Manager:

1. Execute o **RBAViewer.exe**.  

2. Selecione o botão **Auditar RBA** na barra de ferramentas.  

    1. Para exibir as relações limitadas por coleção em um modo de exibição de árvore, mude para a guia **Resumo da Coleção**.  

    2. Para exibir objetos atribuídos a uma função de segurança, mude para a guia **Resumo de Escopo**.  


### <a name="audit-a-specific-user"></a>Auditar um usuário específico

Use o procedimento a seguir para auditar a configuração de administração baseada em funções para um usuário específico:

1. Execute o **RBAViewer.exe**.  

2. Selecione o botão **Executar como** na barra de ferramentas.  

3. Insira o nome de usuário específico para verificar as permissões para a conta.  

4. A ferramenta exibe as funções de segurança atribuídas ao usuário ou grupo de segurança ao qual o usuário pertence. Ele também exibe os objetos que esse usuário pode ver e as ações que ele pode realizar no console.  



## <a name="see-also"></a>Consulte também

- [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration)
- [Configurar administração baseada em funções](/sccm/core/servers/deploy/configure/configure-role-based-administration)