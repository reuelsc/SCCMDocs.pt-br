---
title: "Configure o MDM híbrido | Microsoft Docs"
description: "Configure o registro de dispositivo híbrido com o Configuration Manager e o Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 48b91e88f78752cf7c05162b701ea2ca2f401de3
ms.openlocfilehash: 85df3df19f01f8ed6f5240851c47afce01a92880

---

# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar o MDM (gerenciamento de dispositivo móvel) híbrido com o System Center Configuration Manager e com o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Antes de poder gerenciar dispositivos iOS, Windows e Android com o Configuration Manager, eles devem ser registrados com o Intune. Use as etapas a seguir para configurar o registro de dispositivo híbrido com o Configuration Manager usando o Intune. Ao concluir as etapas a seguir, você habilitará o registro de BYOD (“traga seu próprio dispositivo”) para seus usuários. Essas etapas também são pré-requisitos para [registrar dispositivos da empresa](enroll-company-owned-devices.md).

 |Etapas|Detalhes|  
 |-----------|-------------|  
 |**Etapa 1:** [criar uma coleção de MDM](#step-1-create-an-mdm-collection)|Crie uma coleção de usuários do Configuration Manager com os usuários cujos dispositivos podem ser registrados|  
 |**Etapa 2:** [requisitos de nome de domínio](#step-2-domain-name-requirements)|Confirme se o gerenciamento de usuários do Active Directory e o DNS (Serviço de Nomes de Domínio) da sua organização atendem aos requisitos de MDM|
 |**Etapa 3:** [configurar a assinatura do Intune](#step-3-configure-intune-subscription)|O serviço Intune permite gerenciar dispositivos pela Internet.|  
 |**Etapa 4:** [adicionar termos e condições](#step-4-add-terms-and-conditions)| Crie termos e condições com os quais os usuários devem concordar antes de poderem usar o aplicativo do Portal da Empresa|
 |**Etapa 5:** [criar um ponto de conexão de serviço](#step-5-create-service-connection-point)|O ponto de conexão de serviço envia as configurações e informações da implantação de software para o Configuration Manager e recupera mensagens de status e inventário dos dispositivos móveis. |  
 |**Etapa 6:** [habilitar o registro de plataforma](#step-6-enable-platform-enrollment)|O registro do MDM para dispositivos [iOS](#ios-and-mac-enrollment-setup) e [Windows](#windows-enrollment-setup) exige etapas adicionais para a comunicação entre o serviço e os dispositivos. O Android não exige nenhuma configuração adicional.|  
 |**Etapa 7:** [configurar gerenciamento adicional](#step-7-set-up-additional-management)|(Opcional) Configure o acesso condicional e itens de configuração para dispositivos registrados|
 |**Etapa 8:** [verificar a configuração do MDM](#step-8-verify-mdm-configuration)|Veja os arquivos de log para confirmar que o ponto de conexão de serviço foi criado com êxito e as contas de usuário estão sincronizando.|
 |**Etapa 9:** [Registrar dispositivos](#step-9-enroll-devices)|Diga aos usuários como registrar seus dispositivos ou comece registrando dispositivos da empresa para atender às necessidades da sua organização|

Procurando o Intune sem o Configuration Manager?
> [!div class="button"]
[Exibir documentos do Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)

## <a name="step-1-create-an-mdm-collection"></a>Etapa 1: criar uma coleção de MDM
Você precisará de uma coleção de usuários do Configuration Manager para especificar os usuários que podem registrar dispositivos no gerenciamento. Apenas coleções de usuários podem ser visadas, pois as licenças do Intune são atribuídas a usuários. Para fins de teste você pode configurar uma **regra direta** e adicionar usuários específicos que podem registrar dispositivos. No console do Configuration Manager, escolha **Ativos e Conformidade** > **Coleções de Usuários**, clique na guia **Início** > grupo **Criar** e clique em **Criar Coleção do Usuário**. Para uma distribuição mais ampla, você deve usar **Regras de consulta** para definir usuários. Para obter mais informações sobre coleções, confira [Como criar coleções](https://technet.microsoft.com/library/mt629371.aspx).

![Criar uma coleção de usuários para MDM](../media/mdm-create-user-collection.png)

## <a name="step-2-domain-name-requirements"></a>Etapa 2: requisitos de nome de domínio

Se necessário, execute as seguintes etapas para satisfazer quaisquer dependências externas para o Configuration Manager:

1. Cada usuário deve ter uma licença do Intune atribuída para registrar dispositivos. Para associar as licenças do Intune aos usuários, cada usuário deve ter um nome UPN que possa ser publicamente resolvido (por exemplo, johndoe@contoso.com) ou uma ID de logon alternativa configurada no Azure Active Directory). A configuração de uma ID de logon alternativa permite que os usuários se conectem com um endereço de email, por exemplo, mesmo se seu UPN está em um formato de NetBIOS (por exemplo, CONTOSO\johndoe).

  - Se sua empresa usa UPNs resolvíveis publicamente (ou seja, johndoe@contoso.com),, nenhuma configuração adicional é necessária.
  - Se sua empresa usa um UPN não resolvível (ou seja, CONTOSO\johndoe), você deve [configurar uma ID alternativa no Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2.  Implante e configure os Serviços de Federação do Active Directory (AD FS). (Opcional)

     Quando você configura logon único, seus usuários podem se conectar com as credenciais corporativas deles para acessar os serviços no Intune.

     Para mais informações, consulte os seguintes tópicos:
    -   [Preparar-se para o logon único](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [Planejar e implantar o AD FS 2.0 para uso com logon único](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  Implantar e configurar a sincronização de diretório.

     A sincronização de diretório permite que você popule o Intune com contas de usuário sincronizadas. As contas de usuários sincronizadas e os grupos de segurança são adicionados ao Intune. A falha ao habilitar a Sincronização de Diretório é uma causa comum de os dispositivos não poderem ser registrados na configuração do MDM do Configuration Manager com o Microsoft Intune.

     Para mais informações, consulte [Integração de diretório](http://go.microsoft.com/fwlink/?LinkID=271120) na biblioteca de documentação do Active Directory.

4.  Opcional, não recomendado: se não estiver usando os Serviços de Federação do Active Directory (AD FS), redefina as senhas dos usuários do Microsoft Online.

     Se você não estiver usando o AD FS, você deve definir uma senha online da Microsoft para cada usuário.

## <a name="step-3-configure-intune-subscription"></a>Etapa 3: configurar a assinatura do Intune
 A assinatura do Intune permite gerenciar dispositivos pela Internet. Isso inclui especificar qual coleção de usuários pode registrar dispositivos e definir informações apresentadas aos usuários. A assinatura do Intune faz o seguinte:

-   Recupera o certificado que o ponto de conexão de serviço exige para se conectar ao serviço do Intune
-   Define a coleção de usuários que permite que os usuários registrem dispositivos móveis
-   Define e configura as plataformas móveis às quais você deseja dar suporte

> [!IMPORTANT]
>  A criação de uma assinatura do Microsoft Intune no Configuration Manager colocará o ponto de conexão de serviço de seu site no “modo online”. Confira [Sobre o ponto de conexão de serviço no System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

### <a name="to-create-the-microsoft-intune-subscription"></a>Para criar a assinatura do Microsoft Intune

1.  Se ainda não tiver uma, inscreva-se para obter uma conta do Microsoft Intune em [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216).  Depois de criar sua conta do Intune, você não precisa adicionar nenhum usuário à conta do Intune ou executar configurações adicionais.

2.  No console do Configuration Manager, clique em **Administração**.

3.  No espaço de trabalho **Administração** , expanda **Serviços de Nuvem**e clique em **Assinaturas do Microsoft Intune**. Na guia **Início** , clique em **Adicionar Assinatura do Microsoft Intune**.

![Criar uma assinatura do Intune](../media/mdm-set-intune.png)

4.  Na página **Introdução** do Assistente para Criar Assinatura do Microsoft Intune, examine o texto e clique em **Próximo**.

5.  Na página **Assinatura** , clique em **Entrar** e entre usando sua conta empresarial ou de estudante. Na caixa de diálogo **Definir a autoridade de gerenciamento de dispositivos móveis**, marque a caixa de seleção para gerenciar apenas dispositivos móveis usando o Configuration Manager por meio do console do Configuration Manager. Para continuar sua assinatura, selecione essa opção.

    > [!IMPORTANT]
    >  Após selecionar o Configuration Manager como sua autoridade de gerenciamento, não será possível alterar futuramente a autoridade de gerenciamento para o Microsoft Intune.

6.  Clique nos links de privacidade para revisá-los e clique em **Próximo**.

7.  Na página **Geral** , especifique as seguintes opções e clique em **Próximo**.

  -   **Coleção**: especifique uma coleção de usuários que contém os usuários que registrarão seus dispositivos móveis.

      > [!NOTE]
      >  Se um usuário for removido da coleção, o dispositivo do usuário continuará a ser gerenciado por até 24 horas, quando o registro do usuário for removido do banco de dados de usuários.

  -   **Nome da empresa**: especifique o nome de sua empresa.

  -   **URL da documentação de privacidade**: se você publicar as informações de privacidade da sua empresa em um link acessível pela Internet, forneça um link que os usuários possam acessar pelo portal da empresa, por exemplo, http://www.contoso.com/CP_privacy.html. As informações de privacidade podem esclarecer quais informações os usuários estão compartilhando com sua empresa.

  -   **Esquema de cores do portal da empresa**: opcionalmente, troque a cor azul padrão pela cor dos portais da empresa.

  -   **Código do site do Configuration Manager**: especifica o código de um site primário para gerenciar os dispositivos móveis.

    > [!NOTE]
    >  Alterar o código do site afeta somente os novos registros e não afeta os dispositivos registrados existentes.

8.  Na página **Informações de Contato da Empresa**, especifique as informações de contato da empresa que são exibidas para os usuários em **Contatar TI** no aplicativo do Portal da Empresa. Forneça as informações de contato para a sua empresa e clique em **Próximo**.

9. Na página **Logotipo da Empresa**, você pode escolher se deseja exibir logotipos no portal da empresa e, em seguida, clicar em **Próximo**.

10. Conclua o assistente.

## <a name="step-4-add-terms-and-conditions"></a>Etapa 4: adicionar termos e condições
 Depois de configurar o gerenciamento de dispositivos móveis do Intune, é possível criar **Termos e Condições**. Use termos e condições para explicar aos usuários o que acontece quando eles registram seus dispositivos. Os usuários devem aceitar os termos e condições antes de registrar um dispositivo. No console do Configuration Manager, acesse **Ativos e Conformidade** > **Visão Geral** > **Configurações de Conformidade** > **Termos e Condições** e clique em **Criar Termos e Condições**. Confira [Termos e Condições no System Center Configuration Manager](terms-and-conditions.md).

##  <a name="step-5-create-service-connection-point"></a>Etapa 5: criar um ponto de conexão de serviço
Depois de criar a assinatura, é possível instalar a função do sistema de sites do ponto de conexão de serviço que permite que você se conecte ao serviço do Intune. Esta função do sistema de sites enviará por push as configurações e os aplicativos ao serviço do Intune.

 O ponto de conexão de serviço envia as configurações e informações da implantação de software para o Configuration Manager e recupera mensagens de status e inventário dos dispositivos móveis. O serviço Configuration Manager age como um gateway que se comunica com dispositivos móveis e armazena configurações.

> [!NOTE]
>  A função do sistema de sites do ponto de conexão de serviço só pode ser instalada em um site de administração central ou em um site primário autônomo. O ponto de conexão de serviço deve ter acesso à Internet.


### <a name="configure-the-service-connection-point-role"></a>Configurar a função do ponto de conexão de serviço

1.  No console do Configuration Manager, clique em **Administração**.

2.  No espaço de trabalho **Administração**, expanda **Sites** e clique em **Funções de Servidores e Sistema de Sites**.

3.  Adicione a função do **Ponto de conexão de serviço** a um servidor do sistema de sites novo ou existente usando a etapa associada:

    -   Novo servidor do sistema de sites: na guia **Início** , no grupo **Criar** , clique em **Criar Servidor do Sistema de Site** para iniciar o Assistente para Criar Servidor do Sistema de Site.

    -   Servidor do sistema de sites existente: clique no servidor no qual deseja instalar a função do ponto de conexão de serviço. Em seguida, na guia **Início** , no grupo **Servidor** , clique em **Adicionar Funções do Sistema de Site** para iniciar o Assistente para Adicionar Funções do Sistema de Site.

4.  Na página **Seleção de Função do Sistema** , selecione **Ponto de conexão de serviço**e clique em **Avançar**.

![Criar um ponto de conexão de serviço](../media/mdm-service-connection-point.png)

5.  Conclua o assistente.

### <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>Como o ponto de conexão de serviço é autenticado no serviço do Microsoft Intune?
 O ponto de conexão de serviço estende o Configuration Manager estabelecendo uma conexão com o serviço Intune baseado em nuvem, que gerencia dispositivos móveis pela Internet. O ponto de conexão de serviço é autenticado no serviço Intune da seguinte maneira:

1.  Ao criar uma assinatura do Intune no console do Configuration Manager, o administrador do Configuration Manager é autenticado pela conexão ao Azure Active Directory, que é redirecionada para o respectivo servidor ADFS para solicitar o nome de usuário e a senha. Em seguida, o Intune emite um certificado para o locatário.

2.  O certificado da etapa 1 é instalado na função do site do ponto de conexão de serviço e é usado para autenticar e autorizar toda a comunicação adicional com o serviço do Microsoft Intune.

## <a name="step-6-enable-platform-enrollment"></a>Etapa 6: habilitar o registro de plataforma
  Plataformas de dispositivos diferentes exigem configuração adicional para habilitar o registro de dispositivo:
  - [Configuração do registro de iOS e Mac](#ios-and-mac-enrollment-setup): obtenha um Apple MDM Push Certificate
  - [Configuração do registro do Windows](#windows-enrollment-setup): configure o DNS e habilite o registro de dispositivos de computadores Windows, Windows 10 Mobile e Windows Phone
  - Android: os dispositivos Android não exigem etapas adicionais para habilitar o registro

Depois de habilitar o gerenciamento do MDM, você poderá especificar o número de dispositivos que cada usuário pode registrar, até 15 dispositivos por usuário.

### <a name="ios-and-mac-enrollment-setup"></a>Configuração do registro de iOS e Mac
  As etapas a seguir habilitam o gerenciamento de dispositivos da Apple carregando um Apple MDM Push Certificate para o serviço Intune.

  1.  **Baixar uma solicitação de assinatura de certificado** - Um arquivo de solicitação de assinatura de certificado (.csr) é necessário para solicitar um certificado APNs da Apple.  

      1.  No console do Configuration Manager, no espaço de trabalho **Administração** , acesse **Serviços de Nuvem**> **Assinaturas do Microsoft Intune**.  

      2.  Na guia **Início** , clique em **Criar solicitação de certificado APNs**. A caixa de diálogo **Solicitar Solicitação de Assinatura de Certificado Apple Push Notification Service** é aberta.  

      3.  **Navegue** até o caminho para salvar o novo arquivo de solicitação de assinatura de certificado (.csr). Salve o arquivo (.csr) da solicitação de assinatura do certificado localmente.  

      4.  Clique em **Baixar**. O novo arquivo .csr do Microsoft Intune é baixado e salvo pelo Configuration Manager. O arquivo .csr é usado para solicitar um certificado de relação de confiança do Portal de Certificados Apple Push.  

  2.  **Solicitar um certificado APNs da Apple** O certificado APNs (Apple Push Notification Service) é usado para estabelecer uma relação de confiança entre o serviço de gerenciamento, o Intune e os dispositivos móveis iOS registrados.  

      1.  Em um navegador, vá para o [Portal de Certificados por Push da Apple](http://go.microsoft.com/fwlink/?LinkId=269844) e entre com sua ID corporativa da Apple. Essa ID da Apple deve ser usada no futuro para renovar seu certificado APNs.  

      2.  Conclua o assistente usando o arquivo (.csr) de solicitação de assinatura do certificado. Baixe o certificado APNs e salve o arquivo .pem localmente. Este arquivo de certificado APNs (.pem) é usado para estabelecer uma relação de confiança entre o servidor do Apple Push Notification e a autoridade de gerenciamento de dispositivo móvel do Intune.  

  3.  **Habilitar registro e carregar o certificado APNs** - Para habilitar o registro do iOS, carregue o certificado APNs.  

      1.  No console do Configuration Manager, no espaço de trabalho **Administração** , acesse **Serviços de Nuvem** > **Assinatura do Microsoft Intune**.  

      2.  Na guia **Início** do grupo **Assinatura** , clique em **Configurar Plataformas** > **IOS**.  

          > [!NOTE]  
          >  Não carregue o certificado APNs (Apple Push Notification Service) antes de habilitar o registro do iOS no console do Configuration Manager.  

      3.  Na caixa de diálogo **Propriedades da Assinatura do Microsoft Intune** , selecione a guia **iOS** e clique para marcar a caixa de seleção **Habilitar registro do iOS** .  

      4.  Clique em **Procurar**e vá para o arquivo de certificado APNs (.cer) baixado da Apple. O Configuration Manager exibe as informações de certificado APNs. Clique em **OK** para salvar o certificado APNs no Intune.    


Informações adicionais sobre o [registro do iOS e Mac](enroll-hybrid-ios-mac.md).

### <a name="windows-enrollment-setup"></a>Configuração do registro do Windows  
Você pode usar o Configuration Manager com o Intune para gerenciar computadores, laptops e outros dispositivos que executam o Windows como dispositivos móveis. Você também pode configurar dispositivos Windows 10 para [registrarem automaticamente quando tentarem entrar no Azure Active Directory](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/enroll-hybrid-windows#azure-active-directory-enrollment) adicionando uma conta corporativa ou de estudante no seu dispositivo.

Um alias DNS (tipo de registro CNAME) facilita o registro dos dispositivos para os usuários ao popular automaticamente o nome do servidor durante o registro do dispositivo. Em seguida, você pode habilitar o registro de dispositivos móveis de computadores Windows.  

1. No console do Configuration Manager, no espaço de trabalho **Administração**, acesse **Serviços de Nuvem** > **Assinaturas do Microsoft Intune** e faça o seguinte:  
  - **Computadores Windows:** na guia **Início**, clique em **Configurar Plataformas** e clique em **Windows**. Na guia **Geral** , selecione **Habilitar registro do Windows**.  
  - **Windows 10 Mobile e Windows Phone:** na guia **Início**, clique em **Configurar Plataformas** e clique em **Windows Phone**.  Na guia **Geral** , escolha  **Windows Phone 8.1 e Windows 10 Mobile**.

2.  Você também pode configurar o Configuration Manager para simplificar o registro usando o aplicativo do Portal da Empresa.
(Opcional) Crie um alias DNS (tipo de registro CNAME) nos registros DNS da sua empresa que redirecione as solicitações enviadas a uma URL no domínio da empresa para os servidores de serviço de nuvem da Microsoft.  Por exemplo, se o domínio da sua empresa for contoso.com, você deverá criar um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para EnterpriseEnrollment-s.manage.microsoft.com.  

|Tipo|Nome do host|Aponta para|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  

Para informações adicionais, confira [Registro do Windows](enroll-hybrid-windows.md).

### <a name="android-enrollment-setup"></a>Configuração de registro do Android
Você pode usar o Configuration Manager com o Intune para gerenciar telefones e tablets que executam o Android.
1.  No console do Configuration Manager, no espaço de trabalho **Administração** , acesse **Serviços de Nuvem** > **Assinatura do Microsoft Intune**.  

2.  Na guia **Início** do grupo **Assinatura** , clique em **Configurar Plataformas** > **Android**.  

3.  Na caixa de diálogo **Propriedades da Assinatura do Microsoft Intune** , selecione a guia **Android** e clique para marcar a caixa de seleção **Habilitar registro do Android** .

Para informações adicionais, consulte [Android](enroll-hybrid-android.md).

## <a name="step-7-set-up-additional-management"></a>Etapa 7: configurar gerenciamento adicional
(Opcional) Você pode configurar o gerenciamento adicional antes dos dispositivos serem registrados. Essas soluções de gerenciamento podem ser criadas e implantadas após a dispositivos serem registrados, embora muitas empresas prefiram implantá-las conforme os dispositivos são trazidos para o gerenciamento.

Os **Itens de configuração** permitem que você gerencie as configurações como exigir um PIN ou exigir criptografia em dispositivos registrados com base na plataforma de dispositivo:
- [Dispositivos Windows 10 e Windows 8.1](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)
- [Dispositivos Windows Phone](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client)
- [Dispositivos iOS e Mac](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)
- [Dispositivos Android e Samsung KNOX Standard](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)

Os **Aplicativos** podem ser implantados em dispositivos gerenciados:
- [Aplicativos iOS](/sccm/apps/get-started/creating-ios-applications)
- [Aplicativos Mac](/sccm/apps/get-started/creating-mac-computer-applications)
- [Aplicativos de computador Windows](/sccm/apps/get-started/creating-windows-applications)
- [Aplicativos de Windows Phone](/sccm/apps/get-started/creating-windows-phone-applications)
- [Aplicativos Android](/sccm/apps/get-started/creating-android-applications)

O **Acesso condicional** permite que você gerencie o acesso aos recursos da empresa, incluindo:  
- [Acesso ao email](/sccm/protect/deploy-use/manage-email-access)
- [Acesso ao SharePoint](/sccm/protect/deploy-use/manage-sharepoint-online-access)
- [Acesso ao Skype for Business](/sccm/protect/deploy-use/manage-skype-for-business-online-access)
- [Dynamics CRM Online](/sccm/protect/deploy-use/manage-dynamics-crm-online-access)

## <a name="step-8-verify-mdm-configuration"></a>Etapa 8: verificar a configuração do MDM

 Você pode verificar determinados componentes do gerenciamento de dispositivo examinando os seguintes arquivos de log:

-   Verifique o Cloudusersync.log para ver se as contas de usuário foram sincronizadas com êxito.

-   Verifique o Sitecomp.log para ver se o ponto de conexão de serviço foi criado com êxito.

## <a name="step-9-enroll-devices"></a>Etapa 9: Registrar dispositivos
A configuração híbrida agora está concluída. Os dispositivos podem ser registrados no Configuration Manager de várias maneiras:
- Dispositivos do usuário (BYOD): [Informar aos usuários como registrar seus dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) – As diretrizes de registro são as mesmas para dispositivos de gerenciamento híbrido e pelo Intune
- Dispositivos da empresa (COD): [Enroll company-owned devices](enroll-company-owned-devices.md) (Registrar dispositivos da empresa) fornece diretrizes sobre diferentes formas específicas da plataforma de registrar dispositivos da empresa.

## <a name="managing-intune-subscriptions-associated-with-configuration-manager"></a>Gerenciando assinaturas do Intune associadas ao Configuration Manager

Se você adicionar uma assinatura do Microsoft Intune (uma assinatura de avaliação ou uma assinatura paga) ao Configuration Manager e precisar mudar para uma assinatura diferente do Intune, será preciso excluir tanto a **Assinatura do Microsoft Intune** quanto o **Ponto de conexão de serviço** do console do Configuration Manager para poder adicionar uma nova assinatura.

### <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Como excluir uma assinatura Intune do Configuration Manager

> [!IMPORTANT]
>  Todo o conteúdo, incluindo registros do usuário, políticas e implantações de aplicativo configuradas para dispositivos gerenciados pela assinatura do Intune, serão removidos quando você excluir a assinatura.

1.  No console do Configuration Manager, clique em **Administração** > **Visão Geral** > **Serviços em Nuvem** > **Assinaturas do Microsoft Intune**.

2.  Clique com o botão direito do mouse na opção **Assinatura do Microsoft Intune** listada e clique em **Excluir**.

3.   No assistente, clique em **Remover Assinatura do Microsoft Intune do Configuration Manager**, clique em **Avançar** e, em seguida, clique em **Avançar** novamente para remover a assinatura.


### <a name="how-to-remove-the-service-connection-point-role"></a>Para remover a função do ponto de conexão de serviço

1.  Acesse **Administração** > **Visão Geral** > **Configuração do Site** > **Funções de Servidores e Sistema de Site**.

2.  Escolha o servidor que hospeda a função **Ponto de conexão de serviço**.

3.  Na lista **Funções do Sistema de Sites**, escolha **Ponto de conexão de serviço** e clique em **Remover Função** na faixa de opções. Confirme que deseja remover a função. O ponto de conexão de serviço é excluído.

Agora você pode criar um novo ponto de conexão de serviço, adicionar uma nova assinatura do Intune ao Configuration Manager e definir o Configuration Manager como a Autoridade MDM.

### <a name="how-to-change-mdm-authority-to-intune"></a>Como alterar a autoridade do MDM para o Intune

Começando na versão 1610, é possível mudar a autoridade MDM do Configuration Manager para o Intune. Informações sobre esse recurso estarão disponíveis em breve.



<!--HONumber=Dec16_HO3-->


