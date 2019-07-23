---
title: Configurar Análise de Área de Trabalho
titleSuffix: Configuration Manager
description: Um guia de instruções para configurar e realizar a integração com o desktop Analytics.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d2a098c560305429e4bba65c95a65f3b0d2e8c45
ms.sourcegitcommit: 315fbb9c44773b3b1796ae398568cb61bd07092e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2019
ms.locfileid: "68374426"
---
# <a name="how-to-set-up-desktop-analytics"></a>Como configurar o desktop Analytics

> [!Note]  
> Essas informações se relacionam a um serviço de visualização que pode ser substancialmente modificado antes de ser lançada comercialmente. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Use este procedimento para entrar no desktop Analytics e configurá-lo em sua assinatura. Esse procedimento é um processo único para configurar a análise de desktops para sua organização.  


> [!Important]  
> Para obter informações sobre os pré-requisitos gerais para análise de desktop com Configuration Manager, consulte [pré-requisitos](/sccm/desktop-analytics/overview#prerequisites).  

## <a name="initial-onboarding"></a>Integração inicial

1. Abra o [portal do desktop Analytics](https://aka.ms/desktopanalytics) no gerenciamento de dispositivos Microsoft 365 como um usuário com a função de **administrador global** . Selecione **Iniciar**. Como alternativa, no console do Configuration Manager, vá para o espaço de trabalho **biblioteca de software** , selecione o nó de **manutenção do desktop Analytics** e selecione **planejar**implantações.

2. Na página **aceitar contrato de serviço** , examine o contrato de serviço e selecione **aceitar**.  

3. Na página **confirmar sua assinatura** , examine a lista de licenças de qualificação necessárias. Alterne a configuração para **Sim** ao lado de **você tiver uma das assinaturas com suporte ou mais recentes**e, em seguida, selecione **Avançar**.  

4. Na página **fornecer acesso aos usuários** :

    - **Permitir que o desktop Analytics gerencie funções de diretório em seu nome**: O desktop Analytics atribui automaticamente os **proprietários do espaço de trabalho** à função de administrador do **Desktop Analytics** . Se esses grupos já forem um **administrador global**, não haverá alteração.

        Se você não selecionar essa opção, o desktop Analytics ainda adicionará os usuários como membros do grupo de segurança. Um **administrador global** precisa atribuir manualmente a função de **administrador do desktop Analytics** para os usuários.   

        Para obter mais informações sobre como atribuir permissões de função de administrador no Azure Active Directory e as permissões atribuídas aos **Administradores do desktop Analytics**, consulte [permissões de função de administrador no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - A análise de desktops configura o grupo de segurança **proprietários do espaço de trabalho** no Azure Active Directory para criar e gerenciar espaços de trabalho e planos de implantação. 

        Para adicionar um usuário ao grupo, digite seu nome ou endereço de email na seção **Inserir nome ou endereço de email** . Quando terminar, selecione **Avançar**.

5. Na página para **configurar seu espaço de trabalho**:  

    - Para usar um espaço de trabalho existente para análise de desktop, selecione-o e continue com a próxima etapa.  

        > [!Note]  
        > Se você já estiver usando o Windows Analytics, selecione esse mesmo espaço de trabalho. Você precisa registrar novamente os dispositivos no desktop Analytics que você registrou anteriormente no Windows Analytics.
        >
        > Você só pode ter um espaço de trabalho do desktop Analytics por locatário do Azure AD. Os dispositivos só podem enviar dados de diagnóstico para um espaço de trabalho.  

    - Para criar um espaço de trabalho para análise de desktop, selecione **adicionar espaço de trabalho**.  

        1. Insira um **nome de espaço de trabalho**.<!--do we have any guidance for this name?-->  

        2. Selecione a lista suspensa para **selecionar o nome da assinatura do Azure para este espaço de trabalho**e escolha a assinatura do Azure para este espaço de trabalho.  

        3. **Criar novo** Grupo de recursos ou **use existente**.

        4. Selecione a **região** na lista e, em seguida, selecione **Adicionar**.  

6. Selecione um espaço de trabalho novo ou existente e, em seguida, selecione **definir como espaço de trabalho do desktop Analytics**.  Em seguida, selecione **continuar** na caixa de diálogo **confirmar e conceder acesso** .  

7. Na guia novo navegador, escolha uma conta a ser usada para entrar. Selecione a opção para **consentir em nome da sua organização** e selecione **aceitar**.  

    > [!Note]  
    > Esse consentimento é atribuir ao aplicativo MALogAnalyticsReader a função leitor de Log Analytics para o espaço de trabalho. Essa função de aplicativo é necessária para o desktop Analytics. Para obter mais informações, consulte [função de aplicativo MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. De volta à página para **configurar seu espaço de trabalho**, selecione **Avançar**.  

9. Na página **últimas etapas** , selecione **ir para o desktop Analytics**.

A portal do Azure mostra a **Home** Page da análise de desktop.


## <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para se conectar Configuration Manager com a análise de desktops.
> [!div class="nextstepaction"]  
> [Conectar Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
