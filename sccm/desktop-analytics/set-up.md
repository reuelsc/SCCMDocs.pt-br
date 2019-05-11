---
title: Configurar Análise de Área de Trabalho
titleSuffix: Configuration Manager
description: Um guia de instruções para configurar e integração para análise de área de trabalho.
ms.date: 04/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b831d6f42e6a9c908b46bf21882cab58fa08483
ms.sourcegitcommit: 9af73f5c1b93f6ccaea3e6a096f75a5fecd65c2f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64559054"
---
# <a name="how-to-set-up-desktop-analytics"></a>Como configurar a análise de área de trabalho

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Use este procedimento para entrar no Analytics de área de trabalho e configurá-lo em sua assinatura. Esse procedimento é um processo único para configurar a análise de área de trabalho para sua organização.  



## <a name="initial-onboarding"></a>Migração inicial

1. Abra o portal de análise de área de trabalho no gerenciamento de dispositivo do Microsoft 365 como um usuário com **administrador da empresa** permissões. Selecione **iniciar**.  

2. Sobre o **aceite o contrato de serviço** página, examine o contrato de serviço e selecione **Accept**.  

3. Sobre o **confirmar sua assinatura** , examine a lista de necessárias licenças qualificadas. Mudar a configuração para **Yes** lado **tem uma das assinaturas com suporte ou superior**e, em seguida, selecione **próxima**.  

4. Sobre o **dar aos usuários acesso** página:

    - **Você deseja que a análise da área de trabalho para gerenciar funções de diretório para seus usuários**: Análise da área de trabalho atribui automaticamente o **proprietários do espaço de trabalho** e **colaboradores do espaço de trabalho** grupos para o **administrador de análise de área de trabalho** função. Se esses grupos já estão uma **Administrador Global**, não há nenhuma alteração.  

        Se você não selecionar essa opção, análise de área de trabalho ainda adicionará os usuários como membros dos grupos de segurança de dois. Um **Administrador Global** precisa atribuir manualmente as **administrador de análise de área de trabalho** função para os usuários.  

        Para obter mais informações sobre como atribuir permissões de função de administrador no Azure Active Directory e as permissões atribuídas às **os administradores de análise de área de trabalho**, consulte [permissões da função de administrador no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Análise da área de trabalho pré-configura dois grupos de segurança no Azure Active Directory:  

        - **Os proprietários do espaço de trabalho**: Um grupo de segurança para criar e gerenciar espaços de trabalho. Essas contas precisam de acesso de proprietário à assinatura do Azure.  

        - **Colaboradores de espaço de trabalho**: Um grupo de segurança para criar e gerenciar planos de implantação neste espaço de trabalho. Eles não precisam de qualquer acesso do Azure adicional.  

        Para adicionar um usuário a um grupo, digite seu nome ou endereço de email na **insira o nome ou endereço de email** seção grupo apropriado. Quando terminar, selecione **próxima**.

5. Na página para **definir seu espaço de trabalho**:  

    > [!Note]  
    > Conclua esta etapa como uma **proprietário do espaço de trabalho** ou **Colaborador**. Para obter mais informações, consulte [pré-requisitos](/sccm/desktop-analytics/overview#prerequisites).  

    - Para usar um espaço de trabalho para análise de área de trabalho, selecione-o e continue com a próxima etapa.  

        > [!Note]  
        > Se você já estiver usando o Windows Analytics, selecione o mesmo espaço de trabalho. Você precisará registrar novamente os dispositivos para análise de área de trabalho que você registrou anteriormente no Windows Analytics.
        >
        > Você pode ter apenas um espaço de trabalho de análise de área de trabalho por locatário do Azure AD. Dispositivos podem enviar somente dados de diagnóstico para um espaço de trabalho.  

    - Para criar um espaço de trabalho para análise de área de trabalho, selecione **adicionar espaço de trabalho**.  

        1. Insira um **nome do espaço de trabalho**.<!--do we have any guidance for this name?-->  

        2. Selecione a lista suspensa para **selecione o nome de assinatura do Azure para este espaço de trabalho**e escolha a assinatura do Azure para este espaço de trabalho.  

        3. **Criar um novo** grupo de recursos ou **usar existente**.

        4. Selecione o **região** na lista e, em seguida, selecione **Add**.  

6. Selecione um espaço de trabalho novo ou existente e, em seguida, selecione **definido como espaço de trabalho de análise de área de trabalho**.  Em seguida, selecione **Continue** na **confirmar e conceder acesso** caixa de diálogo.  

7. Na nova guia do navegador, escolha uma conta para usar para entrar. Selecione a opção para **consentir em nome de sua organização** e selecione **Accept**.  

    > [!Note]  
    > Esse consentimento é atribuir o aplicativo MALogAnalyticsReader a função de leitor do Log Analytics para o espaço de trabalho. Essa função de aplicativo é necessária pela análise de área de trabalho. Para obter mais informações, consulte [função de aplicativo MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Volta na página para **definir seu espaço de trabalho**, selecione **próxima**.  

9. Sobre o **última etapa** página, selecione **vá para a área de trabalho de análise**.

O portal do Azure mostra a área de trabalho de analítica **Home** página.


## <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para conectar o Configuration Manager com a análise de área de trabalho.
> [!div class="nextstepaction"]  
> [Conectar o Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
