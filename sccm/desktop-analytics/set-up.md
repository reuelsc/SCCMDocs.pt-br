---
title: Configurar Análise de Área de Trabalho
titleSuffix: Configuration Manager
description: Um guia de instruções para configurar e integração para análise de área de trabalho.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9bd3a9efcbc76647ae39eb1a104b401b112d15fb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754512"
---
# <a name="how-to-set-up-desktop-analytics"></a>Como configurar a análise de área de trabalho 

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Use este procedimento para entrar no Analytics de área de trabalho e configurá-lo em sua assinatura. Esse procedimento é um processo único para configurar a análise de área de trabalho para sua organização.  



## <a name="initial-onboarding"></a>Migração inicial

1. Abra o [portal de análise de área de trabalho](https://aka.ms/m365aprod) no gerenciamento de dispositivo do Microsoft 365 como um usuário com **administrador de empresa** permissões. Selecione **iniciar**.  

2. Sobre o **aceite o contrato de serviço** página, examine o contrato de serviço e selecione **Accept**.  

3. Sobre o **confirmar sua assinatura** , examine a lista de necessárias licenças qualificadas. Mudar a configuração para **Yes** lado **tem uma das assinaturas com suporte ou superior**e, em seguida, selecione **próxima**.  

4. Sobre o **dar acesso de usuários e aplicativos** página, análise de área de trabalho pré-configura dois grupos de segurança no Azure Active Directory:  

    - **Os proprietários do espaço de trabalho**: Criar e gerenciar espaços de trabalho. Essas contas precisam de acesso de proprietário à assinatura do Azure.  

    - **Colaboradores de espaço de trabalho**: Criar e gerenciar planos de implantação neste espaço de trabalho. Eles não precisam de qualquer acesso do Azure adicional.  
  
   Para adicionar um usuário a um grupo, digite seu nome ou endereço de email na **insira o nome ou endereço de email** seção grupo apropriado. Quando terminar, selecione **próxima**. 

5. Na página para **definir seu espaço de trabalho**:  

    - Para usar um espaço de trabalho para análise de área de trabalho, selecione-o e continue com a próxima etapa.  

        > [!Note]  
        > Se você já estiver usando o Windows Analytics, selecione o mesmo espaço de trabalho. Você precisará registrar novamente os dispositivos para análise de área de trabalho que você registrou anteriormente no Windows Analytics. 
        > 
        > Você pode ter apenas um espaço de trabalho de análise de área de trabalho por locatário do Azure AD. Dispositivos podem enviar somente dados de diagnóstico para um espaço de trabalho.   

    - Para criar um espaço de trabalho para análise de área de trabalho, selecione **adicionar espaço de trabalho**.  

        1. Insira um **nome do espaço de trabalho**.<!--do we have any guidance for this name?-->  

        2. Selecione a lista suspensa para **selecione o nome de assinatura do Azure para este espaço de trabalho**e escolha a assinatura do Azure para este espaço de trabalho.  

        3. Selecione o **região** na lista e, em seguida, selecione **Add**.  

6. Selecione um espaço de trabalho novo ou existente e, em seguida, selecione **definido como espaço de trabalho de análise de área de trabalho**.  Em seguida, selecione **Continue** na **confirmar e conceder acesso** caixa de diálogo.  

7. Na nova guia do navegador, escolha uma conta para usar para entrar. Selecione a opção para **consentir em nome de sua organização** e selecione **Accept**.  

    > [!Note]  
    > Esse consentimento é atribuir o aplicativo MALogAnalyticsReader a função de leitor do Log Analytics para o espaço de trabalho. Essa função de aplicativo é necessária pela análise de área de trabalho. Para obter mais informações, consulte [função de aplicativo MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Volta na página para **definir seu espaço de trabalho**, selecione **próxima**.  

9. Sobre o **última etapa** página, selecione **vá para a área de trabalho de análise**. 

O portal do Azure mostra a área de trabalho de analítica **Home** página.



## <a name="create-app-for-configuration-manager"></a>Criar aplicativo para o Configuration Manager

Crie um aplicativo no Azure AD para o Configuration Manager.

1. No [portal do Azure](http://portal.azure.com), acesse **Azure Active Directory**e selecione **registros do aplicativo**. Em seguida, selecione **novo registro de aplicativo**.  

2. No **criar** painel, defina as seguintes configurações:  

    - **Nome**: um nome exclusivo que identifica o aplicativo, por exemplo: `Desktop-Analytics-Connection`  

    - **Tipo de aplicativo**: **Aplicativo Web / API**  

    - **URL de logon**: esse valor não é usado pelo Configuration Manager, mas exigido pelo Azure AD. Insira uma URL exclusiva e é válida, por exemplo: `https://configmgrapp`  
  
   Selecione **Criar**.  

3. Selecione o aplicativo e observe os **ID do aplicativo**. Esse valor é um GUID que é usado para configurar a conexão do Configuration Manager.  

4. Selecione **as configurações** sobre o aplicativo e, em seguida, selecione **chaves**. No **senhas** , digite um **descrição da chave**, especifique uma expiração **duração**e, em seguida, selecione **salvar**. Cópia de **valor** da chave, que é usado para configurar a conexão do Configuration Manager. 

    > [!Important]  
    > Isso é a única oportunidade para copiar o valor da chave. Se você não copiá-lo agora, você precisará criar outra chave.  
    > 
    > Salve o valor da chave em um local seguro.  

5. No aplicativo **as configurações** painel, selecione **permissões necessárias**.  

    1. Sobre o **permissões necessárias** painel, selecione **Add**.  

    2. No **adicionar acesso à API** painel **selecionar uma API**.  

    3. Pesquise o **Microsserviço do Configuration Manager** API. Selecione-o e, em seguida, escolha **selecionar**.  

    4. Sobre o **habilitar acesso** painel, selecione ambas as permissões de aplicativo: **Gravar dados de coleção de CM** e **ler dados de coleção de CM**. Em seguida, escolha **selecionar**.  

    5. Sobre o **adicionar acesso à API** painel, selecione **feito**.  

6. Sobre o **permissões necessárias** página, selecione **conceder permissões**. Selecione **Sim**.  

7. Copie a ID de locatário do AD do Azure. Esse valor é um GUID que é usado para configurar a conexão do Configuration Manager. Selecione **Azure Active Directory** no menu principal e, em seguida, selecione **propriedades**. Cópia de **ID de diretório** valor.  



## <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para conectar o Configuration Manager com a análise de área de trabalho.
> [!div class="nextstepaction"]  
> [Conectar o Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
