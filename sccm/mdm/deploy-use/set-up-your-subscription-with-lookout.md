---
title: Configurar sua assinatura do Lookout
titleSuffix: Configuration Manager
description: Saiba como configurar a defesa contra ameaças móveis do Lookout.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f914cba7eee44f340bf5b696aca1854128aeb8b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141299"
---
# <a name="set-up-your-subscription-for-lookout-mobile-threat-defense"></a>Configurar sua assinatura para a defesa contra ameaças móveis do Lookout

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As etapas a seguir são necessárias para configurar a assinatura da defesa contra ameaças móveis do Lookout:

| #        |Etapa  |
| ------------- |-------------|
| 1 | [Coletar informações do Azure AD](#collect-azure-ad-information) |
| 2 | [Configurar sua assinatura](#configure-your-subscription) |
| 3 | [Configurar grupos de registro](#configure-enrollment-groups) |
| 4 | [Configurar a sincronização de estado](#configure-state-sync) |
| 5 | [Configurar informações de destinatário de email do relatório de erros](#configure-error-report-email-recipient-information) |
| 6 | [Definir configurações de registro](#configure-enrollment-settings) |
| 7 | [Configurar notificações por email](#configure-email-notifications) |
| 8 | [Configurar a classificação de ameaças](#configure-threat-classification) |
| 9 | [Observando o registro](#watching-enrollment) |


> [!IMPORTANT]  
> Um locatário de segurança de ponto de extremidade móvel do Lookout existente que ainda não esteja associado ao seu locatário do Azure AD não poderá ser usado para a integração com o Azure AD e o Intune. Contate o suporte do Lookout para criar um novo locatário do Lookout Mobile Endpoint Security. Use o novo locatário para carregar os usuários do Azure AD.




## <a name="collect-azure-ad-information"></a>Coletar informações do Azure AD
Seu locatário do Lookout Mobility Endpoint Security será associado à sua assinatura do Azure AD para integrar o Lookout ao Intune. Para habilitar sua assinatura do serviço de defesa contra ameaças móveis do Lookout, o suporte do Lookout (enterprisesupport@lookout.com) precisa das seguintes informações:

- **ID de Locatário do Azure AD**
- **ID do Objeto de Grupo do Azure AD** para acesso *completo* ao console do Lookout
- **ID do Objeto de Grupo do Azure AD** para acesso *restrito* ao console do Lookout (opcional)

Use as etapas a seguir para coletar as informações que você precisa fornecer à equipe de suporte do Lookout.

1. Entre no [portal do Azure](https://portal.azure.com) e selecione sua assinatura. 

2. Quando você escolher o nome da sua assinatura, a URL resultante incluirá a ID da assinatura. Se você tiver problemas ao localizar a ID da assinatura, consulte este [artigo do Suporte da Microsoft](https://support.office.com/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b) para obter dicas sobre como localizar a ID da assinatura.

3. Encontre sua ID do Grupo do Azure AD.  
     > [!NOTE]   
     > A **ID de Objeto do Grupo** está na página **Propriedades** do grupo na folha Azure AD do portal do Azure.  

   O console do Lookout permite dois níveis de acesso:  

   - **Acesso completo:** O administrador do AD do Azure pode criar um grupo de usuários que têm acesso completo e, opcionalmente, crie um grupo para usuários que terão acesso restrito. Somente os usuários nesses grupos podem entrar no **console do Lookout**.
   - **Acesso restrito:** Os usuários neste grupo terão não acessar a várias configurações e módulos relacionados ao registro do console do Lookout, e ter acesso somente leitura para o **política de segurança** módulo do console do Lookout.  

     > [!TIP]  
     > Para obter mais informações sobre as permissões, confira [este artigo de suporte do Lookout](https://personal.support.lookout.com/hc/articles/114094105653).


4. Depois de obter essas informações, contate o suporte do Lookout (email: enterprisesupport@lookout.com). O suporte do Lookout funcionará com seu contato principal para integrar sua assinatura e criar sua conta do Lookout Enterprise, usando as informações coletadas.



## <a name="configure-your-subscription"></a>Configurar sua assinatura

1. Depois que o suporte do Lookout criar sua conta Corporativa do Lookout, um email do Lookout será enviado para o contato principal da sua empresa com um link para a [URL de logon](https://aad.lookout.com/les?action=consent).

2. O primeiro logon no console do Lookout precisa ser feito com uma conta de usuário com a função Administrador Global do Azure AD para registrar seu locatário do Azure AD. As próximas entradas não exigirão esse nível de privilégio do Azure AD. Uma página de consentimento é exibida. Escolha **Aceitar** para concluir o registro. Depois de aceitar e autorizar, você será redirecionado para o Console do Lookout.

   ![captura de tela da página do primeiro logon no console do Lookout](media/lookout-initial-login.png)

3. No [Console do Lookout](https://aad.lookout.com), no módulo **Sistema**, escolha a guia **Conectores** e selecione **Intune**.

   ![captura de tela do console do Lookout com a guia Conectores aberta e opção a Intune realçada](media/lookout-setup-intune-connector.png)

4. Acesse **Conectores** > **Configurações de Conexão** e especifique a **Frequência de Pulsação** em minutos.

   ![captura de tela da guia configurações de conexão mostrando a frequência de pulsação configurada](media/lookout-connection-settings.png)



## <a name="configure-enrollment-groups"></a>Configurar grupos de registro
1. Como prática recomendada, crie um grupo de segurança do Azure AD no [Portal do Azure](https://portal.azure.com) contendo um pequeno número de usuários para testar a integração do Lookout.

    > [!NOTE]  
    > Todos os dispositivos de usuários compatíveis com o Lookout e registrados pelo Intune em um grupo de registro no Azure AD que forem identificados e compatíveis serão registrados e qualificados para ativação no console do Lookout MTD.

2. No [Console do Lookout](https://aad.lookout.com), no módulo **Sistema**, escolha a guia **Conectores** e selecione **Gerenciamento de Registro** para definir um conjunto de usuários cujos dispositivos devem ser registrados no Lookout. Adicione o **Nome de Exibição** do grupo de segurança do Azure AD para registro.

    ![captura de tela da página de registro do conector do Intune](media/lookout-enrollment.png)

    >[!IMPORTANT]  
    > O **Nome de Exibição** diferencia maiúsculas de minúsculas, conforme é mostrado nas **Propriedades** do grupo de segurança no portal do Azure. Conforme é mostrado na imagem abaixo, o **Nome de Exibição** do grupo de segurança apresenta letras minúsculas concatenadas, enquanto o título apresenta todas as letras minúsculas. No console do Lookout, faça a correspondência de maiúsculas e minúsculas no **Nome de Exibição** do grupo de segurança.
    >![captura de tela do Portal do Azure, serviço Azure Active Directory, página Propriedades](media/aad-group-display-name.png)

    >[!NOTE]  
    >A prática recomendada é usar o padrão de 5 minutos para que o incremento de tempo verifique se há novos dispositivos. Limitações atuais, **Lookout não é possível validar nomes de exibição de grupo:** Verifique se o **nome de exibição** campo no portal do Azure corresponde exatamente o grupo de segurança do Azure AD. **Não há suporte para a criação de grupos aninhados:**  Segurança do Azure AD grupos usados no Lookout devem conter somente usuários. Eles não podem conter outros grupos.

3.  Depois que um grupo for adicionado, na próxima vez que um usuário abrir o aplicativo Lookout for Work em seu dispositivo com suporte, o dispositivo estará ativado no Lookout.

4.  Quando estiver satisfeito com os resultados, estenda o registro para grupos de usuários adicionais.



## <a name="configure-state-sync"></a>Configurar a sincronização de estado
Na opção **Estado de Sincronização**, especifique o tipo de dados que deve ser enviado para o Intune. O status do dispositivo e o status da ameaça são necessários para que a integração do Lookout com o Intune funcione corretamente. Essas configurações são habilitadas por padrão.



## <a name="configure-error-report-email-recipient-information"></a>Configurar informações de destinatário de email do relatório de erros
Na opção **Gerenciamento de Erro**, insira o endereço de email que deve receber os relatórios de erros.

![captura de tela da página de gerenciamento de erro do conector do Intune](media/lookout-connector-error-notifications.png)



## <a name="configure-enrollment-settings"></a>Definir configurações de registro
No módulo **Sistema**, na página **Conectores**, especifique o número de dias antes que um dispositivo seja considerado como desconectado. Os dispositivos desconectados são considerados não compatíveis e serão impedidos de acessar os aplicativos da empresa com base nas políticas de acesso condicional do SCCM. Você pode especificar valores entre 1 e 90 dias.

![Configurações de registro do Lookout](media/lookout-console-enrollment-settings.png)



## <a name="configure-email-notifications"></a>Configurar notificações por email
Se você deseja receber alertas por email sobre ameaças, entre no [console do Lookout](https://aad.lookout.com) com a conta de usuário que deve receber as notificações. Na guia **Preferências** do módulo **Sistema**, escolha os níveis de ameaças que devem emitir notificações e defina-os como **HABILITADO**. Salve suas alterações.

![captura de tela da página de preferências com a conta de usuário exibida](media/lookout-email-notifications.png) Se você não desejar mais receber notificações por email, defina as notificações como DESABILITADO e salve suas alterações.



## <a name="configure-threat-classification"></a>Configurar a classificação de ameaças
A defesa contra ameaças móveis do Lookout classifica ameaças móveis de vários tipos. As [classificações de ameaças do Lookout](http://personal.support.lookout.com/hc/articles/114094130693) têm níveis de risco padrão associados a elas. Essas configurações podem ser alteradas a qualquer momento para atender aos requisitos da empresa.

![captura de tela da página de política mostrando ameaças e classificações](media/lookout-threat-classification.png)

>[!IMPORTANT]  
> Os níveis de risco são um aspecto importante da defesa contra ameaças móveis. A integração do Intune calcula a conformidade do dispositivo de acordo com esses níveis de risco em tempo de execução. O administrador do Intune define uma regra na política para identificar um dispositivo como não compatível, se ele tiver uma ameaça ativa com um nível mínimo igual a **Alto**, **Médio** ou **Baixo**. A política de classificação de ameaças da defesa contra ameaças móveis do Lookout gera diretamente o cálculo de conformidade do dispositivo no Intune.



## <a name="watching-enrollment"></a>Observando o registro
Quando a instalação estiver concluída, a defesa contra ameaças móveis do Lookout começará a sondar o Azure AD em busca de dispositivos que correspondam aos grupos de registro especificados. Você pode encontrar informações sobre os dispositivos registrados no módulo Dispositivos. O status inicial dos dispositivos é mostrado como pendente. O status do dispositivo será alterado quando o aplicativo Lookout for Work estiver instalado, aberto e ativado no dispositivo. Para obter mais informações de como obter por push o aplicativo Lookout for Work no dispositivo, confira o tópico [Configurar e implantar aplicativos Lookout for Work](configure-and-deploy-lookout-for-work-apps.md).


## <a name="next-steps"></a>Próximas etapas
[Habilitar conexão do Lookout MTP no Intune](enable-lookout-connection-in-intune.md)
