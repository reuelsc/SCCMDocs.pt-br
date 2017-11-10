---
title: Configurar sua assinatura com Lookout
titleSuffix: Configuration Manager
description: "Este tópico fornece detalhes sobre como configurar a proteção contra ameaças de dispositivo do Lookout."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
caps.latest.revision: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 142926bc41a79adc8d8300e413022fb0e3566c5a
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="set-up-your-subscription-for--lookout-device-threat-protection"></a>Configure sua assinatura para a proteção contra ameaças de dispositivo do Lookout

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para preparar a sua assinatura para o serviço de proteção contra ameaça ao dispositivo do Lookout, o suporte do Lookout (enterprisesupport@lookout.com) precisa das seguintes informações sobre sua assinatura do Azure AD (Active Directory). Seu locatário do Lookout Mobility Endpoint Security será associado à sua assinatura do Azure AD para integrar o Lookout ao Intune. 

* **ID de Locatário do Azure AD**
* **ID do Objeto de Grupo do Azure AD** para acesso **completo** ao console do Lookout
* **ID do Objeto de Grupo do Azure AD** para acesso **restrito** ao console do Lookout (opcional)

> [!IMPORTANT]
> Um locatário existente do Lookout Mobile Endpoint Security que ainda não está associado ao seu locatário do Azure AD não pode ser usado para a integração ao Azure AD e ao Intune. Contate o suporte do Lookout para criar um novo locatário do Lookout Mobile Endpoint Security. Use o novo locatário para carregar os usuários do Azure AD.

Use a seção a seguir para coletar as informações necessárias para fornecer à equipe de suporte do Lookout.  

## <a name="get-your-azure-ad-information"></a>Obter suas informações do Azure AD
### <a name="azure-ad-tenant-id"></a>ID de locatário do Azure AD
Entre no [Portal de Gerenciamento do Azure AD](https://manage.windowsazure.com) e selecione sua assinatura. 

![captura de tela da página do Azure AD mostrando o nome do locatário](media/aad_tenant_name.png) Quando você escolhe o nome de sua assinatura, a URL resultante inclui a ID da assinatura.  Se você tiver problemas ao localizar a ID da assinatura, consulte este [artigo do Suporte da Microsoft](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b?ui=en-US&rs=en-US&ad=US) para obter dicas sobre como localizar a ID da assinatura.   
### <a name="azure-ad-group-id"></a>ID de Grupo do Azure AD
O console do Lookout dá suporte a dois níveis de acesso:  
* **Acesso completo:** o administrador do Azure AD pode criar um grupo de usuários que terá acesso completo e, opcionalmente, criar um grupo de usuários que terá acesso restrito.  Somente os usuários nesses grupos poderão fazer logon no **console do Lookout**.
* **Acesso restrito:** os usuários neste grupo não terão acesso a várias configurações e módulos relacionados ao registro do console do Lookout e terão acesso somente leitura ao módulo de **Política de segurança** do console do Lookout.  

Para obter mais detalhes sobre as permissões, leia [este artigo](https://personal.support.lookout.com/hc/en-us/articles/114094105653) no site do Lookout.

A **ID de Objeto do Grupo** está na página **Propriedades** do grupo no **console de gerenciamento do Azure AD**.

![captura de tela da página de propriedades com o campo GroupID realçado](media/aad_group_object_id.png)

Depois de obter essas informações, contate o suporte do Lookout (email: enterprisesupport@lookout.com).

O suporte do Lookout funcionará com seu contato principal para integrar sua assinatura e criar sua conta do Lookout Enterprise, usando as informações coletadas.


## <a name="configure-your-subscription-with-lookout-device-threat-protection"></a>Configure sua assinatura com a proteção contra ameaças de dispositivo do Lookout
### <a name="step-1-set-up-your-device-threat-protection"></a>Etapa1: configure a proteção contra ameaças de dispositivo
Depois que o suporte do Lookout criar sua conta do Lookout Enterprise, você poderá entrar no console do Lookout.   Um email do Lookout Enterprise é enviado para o contato principal da sua empresa com um link para a URL de logon: https://aad.lookout.com/les?action=consent

Você deve usar uma conta de usuário com a função de Administrador Global do Azure AD quando fizer logon pela primeira vez no console do Lookout, pois o Lookout requer que essas informações registrem seu locatário do Azure AD.   A entrada subsequente não exigirá que o usuário tenha esse nível de privilégio do Azure AD.  Neste primeiro logon, é exibida uma página de consentimento. Escolha **Aceitar** para concluir o registro.

![captura de tela da página de primeiro logon do console do Lookout](media/lookout-initial-login.png)

Depois de aceita e consentir, você será redirecionado para o Console do Lookout. Logons subsequentes após o registro inicial podem ser feitos usando a URL: https://aad.lookout.com

Consulte o [artigo de solução de problemas]() se você se deparar com problemas de logon.

As próximas etapas descrevem as tarefas que você deve fazer para concluir a configuração do Lookout dentro do [Console do Lookout](https://aad.lookout.com).

### <a name="step-2-configure-the-intune-connector"></a>Etapa 2: configurar o conector do Intune

1.  No console do Lookout, do módulo **Sistema**, escolha a guia **Conectores** e selecione **Intune**.

  ![captura de tela do console do Lookout com a guia Conectores aberta e opção a Intune realçada](media/lookout-setup-intune-connector.png)

2.  Na opção de configurações de conexão, configure a frequência de pulsação em minutos.  O conector do Intune agora está pronto.  

  ![captura de tela da guia configurações de conexão mostrando a frequência de pulsação configurada](media/lookout-connection-settings.png)

### <a name="step-3-configure-enrollment-groups"></a>Etapa 3: configurar grupos de registro
Na opção **Gerenciamento de Registro**, defina um conjunto de usuários cujos dispositivos devem ser registrados com o Lookout. A prática recomendada é iniciar com um pequeno grupo de usuários de teste e se familiarizar com como a integração funciona.  Quando estiver satisfeito com os resultados do teste, você poderá estender o registro para grupos de usuários adicionais.

Para começar com grupos de registros, primeiro defina um grupo de segurança do Azure AD que seria um bom primeiro conjunto de usuários para registrar na proteção contra ameaças de dispositivo do Lookout. Após o grupo ser criado no Azure AD, no Console do Lookout, acesse a opção **Gerenciamento de Registro** e adicione os **Nomes de Exibição** do grupo de segurança do Azure AD para registro.

Quando um usuário está em um grupo de registro, qualquer um dos seus dispositivos identificados e com suporte no Azure AD são registrados e qualificados para ativação na proteção contra ameaças de dispositivo do Lookout.  Na primeira vez que o aplicativo Lookout for Work for aberto no dispositivo com suporte, o dispositivo será ativado no Lookout.

![captura de tela da página de registro do conector do Intune](media/lookout-enrollment.png)

A prática recomendada é usar o padrão (5 minutos) para o incremento de tempo para verificar novos dispositivos.

>[!IMPORTANT]
> O nome de exibição diferencia maiúsculas de minúsculas.  Use o **Nome de Exibição** mostrado na página **Propriedades** do grupo de segurança no Portal do Azure. Observe na imagem abaixo que na página **Propriedades** do grupo de segurança, o nome de exibição é mostrado em letras minúsculas concatenadas.  No entanto, o título é exibido em letras minúsculas e não deve ser usado para entrar no console do Lookout.
>![captura de tela do Portal do Azure, serviço Azure Active Directory, página Propriedades](media/aad-group-display-name.png)

A versão atual tem as seguintes limitações:  
* Não há nenhuma validação para os nomes de exibição do grupo.  Certifique-se de usar o valor no campo **NOME DE EXIBIÇÃO** mostrado no Portal do Azure para o grupo de segurança do Azure AD.
* Atualmente não há suporte para a criação de grupos dentro de grupos.  Grupos de segurança do Azure AD especificados podem conter apenas usuários e grupos não aninhados.


### <a name="step-4-configure-state-sync"></a>Etapa 4: configurar a sincronização de estado
Na opção **Estado de Sincronização**, especifique o tipo de dados que deve ser enviado para o Intune.  No momento, você deve habilitar o status do dispositivo e o status de ameaça em ordem para a integração do Intune do Lookout funcionar corretamente.  Essas regras são habilitadas por padrão.
### <a name="step-5-configure-error-report-email-recipient-information"></a>Etapa 5: configurar informações de destinatário do email de relatório de erro
Na opção **Gerenciamento de Erro**, insira o endereço de email que deve receber os relatórios de erros.

![captura de tela da página de gerenciamento de erro do conector do Intune](media/lookout-connector-error-notifications.png)

### <a name="step-6-configure-enrollment-settings"></a>Etapa 6. Definir configurações de registro
No módulo **Sistema**, na página **Conectores**, especifique o número de dias antes que um dispositivo seja considerado como desconectado.  Dispositivos desconectados são considerados incompatíveis e serão impedidos de acessar seus aplicativos da empresa com base nas políticas de acesso condicional do SCCM. Você pode especificar valores entre 1 e 90 dias.

![](media/lookout-console-enrollment-settings.png)

### <a name="step-7-configure-email-notifications"></a>Etapa 7: configurar notificações por email
Se você deseja receber alertas por email sobre ameaças, entre no [console do Lookout](https://aad.lookout.com) com a conta de usuário que deve receber as notificações. Na guia **Preferências** do módulo **Sistema**, escolha as notificações desejadas e defina como **ON**. Salve suas alterações.

![captura de tela da página de preferências com a conta de usuário exibida](media/lookout-email-notifications.png) Se não desejar mais receber notificações por email, defina as notificações como **OFF** e salve suas alterações.
### <a name="step-8-configure-threat-classification"></a>Etapa 8: configurar a classificação de risco
A proteção contra ameaças de dispositivo do Lookout classifica ameaças a dispositivos móveis de vários tipos. As [classificações de ameaças do Lookout](http://personal.support.lookout.com/hc/en-us/articles/114094130693) têm níveis de risco padrão associados a elas. Eles podem ser alterados a qualquer momento para adequação com os requisitos da sua empresa.

![captura de tela da página de política mostrando ameaças e classificações](media/lookout-threat-classification.png)

>[!IMPORTANT]
> Os níveis de risco especificados aqui são um aspecto importante da proteção contra ameaças de dispositivo porque a integração do Intune calcula a conformidade do dispositivo de acordo com esses níveis de risco no tempo de execução. Em outras palavras, o administrador do Intune define uma regra na política para identificar um dispositivo como não compatível se o dispositivo tem uma ameaça ativa com um nível mínimo de: alto, médio ou baixo. A política de classificação de ameaças na proteção contra ameaças de dispositivo do Lookout direciona diretamente o cálculo de conformidade do dispositivo no Intune.

## <a name="watching-enrollment"></a>Observando o registro
Quando a instalação estiver concluída, a proteção contra ameaças de dispositivo do Lookout começará a sondar o Azure AD quanto a dispositivos que correspondam aos grupos de registro especificados.  Você pode encontrar informações sobre os dispositivos registrados no módulo Dispositivos.  O status inicial dos dispositivos é mostrado como pendente.  O status do dispositivo será alterado quando o aplicativo Lookout for Work estiver instalado, aberto e ativado no dispositivo.  Para obter detalhes sobre como obter o Lookout for Work no dispositivo, consulte o tópico [Configurar e implantar aplicativos Lookout for Work](configure-and-deploy-lookout-for-work-apps.md).
## <a name="next-steps"></a>Próximas etapas
[Habilitar conexão do Lookout MTP no Intune](enable-lookout-connection-in-intune.md)
