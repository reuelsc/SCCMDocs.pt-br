---
title: Gerenciar o acesso a email
titleSuffix: Configuration Manager
description: Saiba como usar o acesso condicional do Configuration Manager para gerenciar o acesso ao email do Exchange.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f976b63b4580b5df9c6e609ff6b361538860c41c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137636"
---
# <a name="manage-email-access-in-configuration-manager"></a>Gerenciar acesso a email no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o Configuration Manager o acesso condicional para gerenciar o acesso ao email do Exchange com base nas condições especificadas.  

Você pode gerenciar o acesso a:  

- Microsoft Exchange Local  

- Microsoft Exchange Online  

- Exchange Online dedicado  

Você pode controlar o acesso ao Exchange Online e Exchange Local do cliente de email internos nas seguintes plataformas:  

- Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior  

- iOS 9.0 e posterior  

- Windows Phone 8.1 e posterior  

- Aplicativo de email no Windows 8.1 e posterior  

Os aplicativos de área de trabalho do Office podem acessar o Exchange Online em computadores que executam:  

- Área de trabalho do Office 2013 e posterior com [autenticação moderna](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) habilitada.  

- Windows 7.0 ou Windows 8.1  

> [!NOTE]  
> PCs devem estar ingressados no domínio ou ser compatíveis com as políticas definidas no Intune.  


## <a name="device-requirements"></a>Requisitos do dispositivo
Se você configurar o acesso condicional, antes que um usuário possa se conectar ao seu email, o dispositivo que ele usa deve:  

- Estar registrado no Intune ou em um PC ingressado no domínio.  

- Registre o dispositivo no Azure Active Directory (isso ocorrerá automaticamente quando o dispositivo for registrado com o Intune (somente para o Exchange Online). Além disso, a ID do cliente do Exchange ActiveSync deve estar registrada no Azure Active Directory (não se aplica a dispositivos Windows e Windows Phone conectados ao Exchange local).  

    Para um PC integrado ao domínio, você deve configurá-lo para se registrar automaticamente ao Active Directory do Azure. O **acesso condicional para PCs** seção o [gerenciar o acesso aos serviços](../../protect/deploy-use/manage-access-to-services.md) artigo lista o conjunto completo de requisitos para habilitar o acesso condicional para PCs.  

- Ser compatível com todas as políticas de conformidade do Configuration Manager implantadas nesse dispositivo  

    Se uma condição de acesso condicional não for atendida, o usuário receberá uma das seguintes mensagens ao fazer logon:  

- Se o dispositivo não estiver registrado no Intune ou não estiver registrado no Azure Active Directory, será exibida uma mensagem com instruções sobre como instalar o aplicativo de portal da empresa, registrar o dispositivo e (para dispositivos Android e iOS), ativar o email, que associa o ID do dispositivo Exchange ActiveSync com o registro de dispositivo no Azure Active Directory.  

- Se o dispositivo não for compatível, será exibida uma mensagem que direciona o usuário para o portal da web do Intune no qual ele podem encontrar informações sobre o problema e como corrigi-lo.  

#### <a name="for-mobile-devices"></a>Para dispositivos móveis

Você pode restringir o acesso ao **OWA (Outlook Web Access)** no Exchange Online quando o acesso é feito por meio de um navegador em dispositivos **iOS** e **Android** . O acesso será permitido somente de navegadores com suporte em dispositivos compatíveis:  

- Safari (iOS)  
- Chrome (Android)  
- Navegador gerenciado (iOS e Android)  

Navegadores sem suporte serão bloqueados. Não há suporte para os aplicativos do OWA para iOS e Android. Eles devem ser bloqueados por meio de regras de declarações do ADFS:  

- Configure as regras de declarações do ADFS para bloquear protocolos de autenticação não moderna. Instruções detalhadas são fornecidas no cenário 3 para [bloquear todo o acesso ao O365, exceto aplicativos baseados em navegador](https://technet.microsoft.com/library/dn592182.aspx).  

#### <a name="for-pcs"></a>Para PCs

- Se o requisito de política de acesso condicional for permitir qualquer dispositivo **ingressado no domínio** ou **em conformidade**, será exibida uma mensagem com instruções sobre como registrá-lo. Se o PC não atender a nenhum dos requisitos, será solicitado que o usuário registre o dispositivo no Intune.  

- Se o requisito de política de acesso condicional for configurado para permitir apenas dispositivos Windows ingressados no domínio, o dispositivo será bloqueado e será exibida uma mensagem para o usuário entrar em contato com o administrador de TI.  

Você pode bloquear o acesso ao email do Exchange a partir do cliente de email Exchange ActiveSync interno aos dispositivos das seguintes plataformas:  

- Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior  

- iOS 9.0 e posterior  

- Windows Phone 8.1 e posterior  

- O aplicativo **Mail** no Windows 8.1 e posterior  

O aplicativo Outlook para iOS e Android, e o Outlook para desktop 2013 e acima é compatível apenas com o Exchange Online.  

O **conector do Exchange Local** entre o Configuration Manager e o Exchange é necessário para que o acesso condicional funcione.  

É possível configurar uma política de acesso condicional para o Exchange Local no console do Configuration Manager. Ao configurar uma política de acesso condicional para o Exchange Online, é possível começar o processo no console do Configuration Manager, que inicia o console do Intune no qual você pode concluir o processo.  



## <a name="configure-conditional-access"></a>Configurar o acesso condicional

### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>Etapa 1: Avaliar o efeito da política de acesso condicional  

Depois de configurar o **conector do Exchange no local**, você pode usar o Configuration Manager **lista de dispositivos por estado de acesso condicional** relatório para identificar os dispositivos que serão impedidos de acessar o Exchange após você configurar a política de acesso condicional. Este relatório também exige:  

- Uma assinatura do Intune  

- O ponto de conexão do serviço deve ser configurado e implantado  

Nos parâmetros do relatório, selecione o grupo do Intune que deseja avaliar e, se necessário, as plataformas de dispositivo às quais a política se aplicará.  

Para obter mais informações sobre como executar relatórios, consulte [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting).  

Depois de executar o relatório, examine essas quatro colunas para determinar se um usuário será bloqueado:  

- **Canal de gerenciamento**: O dispositivo é gerenciado pelo Intune, Exchange ActiveSync ou ambos.  

- **Registrado no AAD**: O dispositivo está registrado com o Azure Active Directory (conhecido como ingresso no local).  

- **Em conformidade**: O dispositivo está em conformidade com as políticas de conformidade implantadas.  

- **EAS ativado**: dispositivos iOS e Android precisam ter sua ID do Exchange ActiveSync associada com o registro do dispositivo no Azure Active Directory. Isso acontece quando o usuário clica no link **Ativar Email** no email de quarentena.  

    > [!NOTE]  
    > Dispositivos Windows Phone sempre exibem um valor nesta coluna.  

Os dispositivos que fazem parte de um grupo de destino serão impedidos de acessar o Exchange, a menos que os valores na coluna correspondam aos valores listados na seguinte tabela:  

|Canal de gerenciamento|Registrado no AAD|compatível|EAS ativado|Ação resultante|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**Gerenciado pelo Microsoft Intune e pelo Exchange ActiveSync**|Sim|Sim|**Sim** ou **Não** é exibido|Acesso ao email permitido|  
|Qualquer outro valor|Não|Não|Nenhum valor é exibido|Acesso ao email bloqueado|  

Você pode exportar o conteúdo do relatório e usar a coluna **Endereço de email** para ajudar a informar os usuários de que eles serão bloqueados.  


### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>Etapa 2: Configurar grupos de usuários ou coleções para a política de acesso condicional  

Direcione as políticas de acesso condicional a diferentes grupos ou coleções de usuários de acordo com os tipos de política. Esses grupos contêm os usuários que serão afetados ou que ficarão isentos da política. Quando um usuário é afetado por uma política, cada dispositivo que ele usa deve ser compatível para que possa acessar o email.  

- **Para a política do Exchange Online**: para grupos de usuários de segurança do Active Directory do Azure. Você pode configurar esses grupos no **Centro de administração do Office 365**ou no **Portal de conta do Intune**.  

- **Para a política do Exchange no local**: em coleções de usuários do Configuration Manager. É possível configurá-las no workspace **Ativos e Conformidade**.  

Você pode especificar dois tipos de grupo em cada política:  

- **Grupos de destino**: Grupos de usuários ou coleções para o qual a política é aplicada.  

- **Grupos isentos**: Grupos de usuários ou coleções que estão isentas da política (opcional)  

Se um usuário estiver nas duas, ele ficará isento da política.  

Somente os grupos ou coleções que são destinados pela política de acesso condicional são avaliados para o acesso ao Exchange.  


### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>Etapa 3: Configurar e implantar uma política de conformidade  

Certifique-se de que você criou e implantou uma política de conformidade para todos os dispositivos aos quais a política de acesso condicional do Exchange será direcionada.  

Para obter detalhes sobre como configurar a política de conformidade, consulte [Gerenciar políticas de conformidade do dispositivo](device-compliance-policies.md).  

> [!IMPORTANT]  
> Se você ainda não tiver implantado uma política de conformidade e, em seguida, habilita uma política de acesso condicional do Exchange, todos os dispositivos direcionados terão acesso.  


### <a name="step-4-configure-the-conditional-access-policy"></a>Etapa 4: Configurar a política de acesso condicional  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>Para p Exchange Online (e locatários no novo ambiente do Exchange Online dedicado)

> [!NOTE]  
> Você também pode criar a política de acesso condicional no console de gerenciamento do Azure AD. O console de gerenciamento do Azure AD permite que você crie políticas de acesso condicional no dispositivo do Intune (chamada de política de acesso condicional baseada em dispositivos no Azure AD), além de outras políticas de acesso condicional, como a autenticação multifator. Você também pode definir políticas de acesso condicional para aplicativos corporativos de terceiros com suporte pelo Azure AD, como o Salesforce e o Box. Para obter mais detalhes, consulte [How To: Exigir que os dispositivos gerenciados para acesso de aplicativo de nuvem com acesso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

As políticas de acesso condicional usam o seguinte fluxo para o Exchange Online para decidir se devem permitir ou bloquear os dispositivos.  

![Fluxo de acesso condicional](media/ConditionalAccess8-1.png)  

Para acessar o email, o dispositivo deve:  

- Registrar com o Intune  

- PCs devem ser ingressado no domínio ou ser registrados e compatíveis com as políticas definidas no Intune  

- Registre o dispositivo no Azure AD. Isso ocorre automaticamente quando o dispositivo é registrado com o Intune. Para PCs ingressados no domínio, você deve configurá-lo para [registrar o dispositivo automaticamente](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-manual-steps) com o Azure AD.  

- Ter ativado o email, que associa a ID do Exchange ActiveSync do dispositivo ao registro do dispositivo no Azure Active Directory (aplica-se somente a dispositivos iOS e Android).  

- Estar em conformidade com todas as políticas de conformidade implantadas  

O estado do dispositivo é armazenado no Azure Active Directory, que concede ou bloqueia o acesso ao email, com base nas condições avaliadas.  

Se uma condição não for atendida, o usuário é apresentado com uma das seguintes mensagens ao entrar:  

- Se o dispositivo não está registrado ou registrado no Azure AD, é exibida uma mensagem com instruções sobre como instalar o aplicativo de portal da empresa e registrá-lo  

- Se o dispositivo não for compatível, será exibida uma mensagem que direciona o usuário para o site de Portal da empresa Intune ou o aplicativo de Portal da empresa no qual ele podem encontrar informações sobre o problema e como corrigi-lo.  

- Para um PC:  

    - Se a política estiver definida para exigir ingresso no domínio e o computador não estiver ingressado no domínio, é exibida uma mensagem para contatar o administrador de TI.  

    - Se a política estiver definida para exigir ingresso no domínio ou conformidade e o computador não atender a nenhum dos dois requisitos, será exibida uma mensagem com instruções sobre como instalar o aplicativo de portal da empresa e registrá-lo.  

A mensagem é exibida no dispositivo para usuários e locatários do Exchange Online no novo ambiente dedicado do Exchange Online, e é entregue à caixa de entrada de email dos usuários para dispositivos Exchange locais e dispositivos herdados do Exchange Online dedicado.  

> [!NOTE]  
> As regras de acesso condicional do Configuration Manager substituem, permitem, bloqueiam e colocam em quarentena regras que são definidas no console de administração do Exchange Online.  
> 
> A política de acesso condicional deve ser configurada no console do Intune. As etapas a seguir começam pelo acesso do console do Intune por meio do Configuration Manager. Se solicitado, entre usando as mesmas credenciais que foram usadas para configurar o ponto de conexão de serviço entre o Intune e Configuration Manager.  

##### <a name="to-enable-the-exchange-online-policy"></a>Para habilitar a política do Exchange Online  

1. No console do Configuration Manager, selecione **ativos e conformidade**.  

2. Expandir **as configurações de conformidade**, expanda **acesso condicional**e, em seguida, selecione **Exchange Online**.  

3. Sobre o **Home** guia da **Links** grupo, selecione **configurar política de acesso condicional no Console do Intune**. Talvez seja necessário fornecer o nome de usuário e a senha da conta usada para conectar o Configuration Manager a qualquer administrador global do serviço do Intune. O console de administração do Intune é aberto.  

4. No portal do Microsoft Intune, selecione **diretiva** > **acesso condicional** > **política do Exchange Online**.  

    ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5. Na página **Política do Exchange Online** , selecione **Habilitar política de acesso condicional para o Exchange Online**. Se você marcar essa opção, o dispositivo deverá ser compatível. Se isso não estiver selecionado, em seguida, o acesso condicional não será aplicado.  

    > [!NOTE]  
    > Se você ainda não tiver implantado uma política de conformidade e habilitar a política do Exchange Online, todos os dispositivos de destino serão relatados como compatíveis.  
   >   
   >  Independentemente do estado de conformidade, todos os usuários aos quais a política se destina precisarão registrar seus dispositivos no Intune.  

6. Sob **acesso a aplicativos**, para o Outlook e outros aplicativos que usam autenticação moderna, que você pode optar por restringir o acesso apenas aos dispositivos que estão em conformidade para cada plataforma. Os dispositivos Windows devem estar ingressados no domínio ou então devem estar em conformidade e estar registrados no Intune.  

    > [!TIP]  
    > **Autenticação moderna** traz a entrada baseada no ADAL (Active Directory Authentication Library) para clientes Office.  
    > 
    > - A autenticação com base em ADAL permite que os clientes Office participem de autenticação baseada em navegador (também conhecida como autenticação passiva). Para autenticar, o usuário é direcionado a uma página da Web de entrada.  
    > - Esse novo método de entrada permite novos cenários, como acesso condicional, com base em **conformidade do dispositivo** e se a **autenticação multifator** foi executada.  
    > 
    >  Para obter mais informações, consulte [Como a autenticação moderna funciona para aplicativos de cliente do Office 2013 e Office 2016](https://docs.microsoft.com/office365/enterprise/modern-auth-for-office-2013-and-2016).  

    Usando o Exchange Online com o Configuration Manager e o Intune, você pode gerenciar dispositivos móveis com acesso condicional e computadores desktop. PCs devem ser ingressado no domínio ou ser registrados no Intune e compatíveis. Você pode definir os seguintes requisitos:  

    - **Os dispositivos devem estar ingressados no domínio ou ser compatíveis.** PCs devem estar ingressados no domínio ou em conformidade com as políticas. Se um PC não atender a esses requisitos, o usuário é solicitado a registrar o dispositivo com o Intune.  

    - **Os dispositivos devem estar ingressados no domínio.** Os PCs devem estar ingressado no domínio para acessar o Exchange Online. Se um PC não estiver ingressado no domínio, o acesso ao email será bloqueado e o usuário é solicitado a entrar em contato com o administrador de TI.  

    - **Os dispositivos devem ser compatíveis.** Os PCs devem ser compatíveis e estar registrados no Intune. Se um PC não estiver registrado, é exibida uma mensagem com instruções sobre como registrar.  

7. Sob **Outlook web access (OWA)**, você pode optar por permitir o acesso ao Exchange Online somente por meio de navegadores com suporte: Safari (iOS) e Chrome (Android). O acesso de outros navegadores será bloqueado. As mesmas restrições de plataforma selecionadas para Acesso do aplicativo para o Outlook também se aplicarão aqui.  

    - Em dispositivos **Android** , os usuários devem habilitar o acesso do navegador. Para fazer essa ação, o usuário deve habilitar a opção "Habilitar acesso do navegador" no dispositivo registrado da seguinte maneira:  

        1. Inicie o **aplicativo do Portal da Empresa**.  

        2. Vá para a página **Configurações** por meio dos três pontos (...) ou do botão de menu do hardware.  

        3. Pressione o botão **Habilitar o Acesso do Navegador** .  

        4. No navegador Chrome, saia do Office 365 e reinicie o Chrome.  

    - Na **iOS e Android** plataformas, para identificar o dispositivo que é usado para acessar o serviço, o Azure AD emitirá um certificado TLS para o dispositivo. O dispositivo exibe o certificado com um prompt ao usuário para selecionar o certificado conforme visto nas capturas de tela abaixo. O usuário deve selecionar esse certificado antes que eles podem continuar a usar o navegador.  

        - **iOS**  

        ![captura de tela do prompt do certificado em um ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)  

        - **Android**  

        ![captura de tela do prompt do certificado em um dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)  

8. Para**aplicativos de email do Exchange ActiveSync**, você poderá optar por bloquear o acesso de email ao Exchange Online se o dispositivo não for compatível e selecionar se deseja permitir ou bloquear o acesso ao email quando o Intune não puder gerenciar o dispositivo.  

9. Em **Grupos de destino**, selecione os grupos de segurança de usuários do Active Directory aos quais a política será aplicada.  

    > [!NOTE]  
    > Para usuários que estão nos grupos de destino, as políticas do Intune irá substituir regras do Exchange e políticas.  
    > 
    > Só serão impostas pelo Exchange as regras de permissão, bloqueio e quarentena e as políticas do Exchange se:  
    > 
    > - O usuário não estiver licenciado para o Intune.  
    > - O usuário está licenciado para o Intune, mas o usuário não pertence a nenhum grupo de segurança direcionado na política de acesso condicional.  

10. Em **Grupos isentos**, selecione os grupos de segurança de usuários do Active Directory que serão isentos desta política. Se um usuário estiver em ambos os grupos de destino e isentos, eles serão isentos da política e terão acesso a seus emails.  

11. Ao terminar, clique em **Salvar**.  


Examine as seguintes observações sobre esta política:  

- Você não precisa implantar a política de acesso condicional; ele entra em vigor imediatamente.  

- Depois que um usuário cria uma conta de email, o dispositivo é bloqueado imediatamente.  

- Se um usuário bloqueado registrar o dispositivo no Intune (ou solucionar a incompatibilidade), o acesso ao email será desbloqueado em 2 minutos.  

- Se o usuário cancelar o registro de seu dispositivo, o email será bloqueado após cerca de 6 horas.  


### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>Para o Exchange local (e locatários no ambiente herdado do Exchange Online dedicado)  
O seguinte fluxo é usado pelas políticas de acesso condicional para o Exchange local e locatários no ambiente herdado do Exchange Online dedicado para decidir entre permitir ou bloquear dispositivos.  

![ConditionalAccess8&#45;2](media/ConditionalAccess8-2.png)  

#### <a name="to-enable-the-exchange-on-premises-policy"></a>Para habilitar a política do Exchange no Local  

1. No console do Configuration Manager, selecione **ativos e conformidade**.  

2. Expandir **as configurações de conformidade**, expanda **acesso condicional**e, em seguida, selecione **Exchange no local**.  

3. No **Home** guia, o **Exchange local** grupo, selecione **configurar política de acesso condicional**.  

4. No **gerais** página do **configurar o Assistente de política de acesso condicional**, especifique se deseja substituir a regra padrão do Exchange Active Sync. Selecione esta opção se você quiser registrados e tenham sempre acesso ao email, mesmo quando a regra padrão é definida como quarentena ou bloquear os dispositivos em conformidade de acesso.  

    > [!NOTE]  
    > Há um problema com a substituição padrão para dispositivos Android. Se a regra de acesso padrão do Exchange Server estiver definida como **Bloquear** , e a política de acesso condicional do Exchange estiver habilitada com a opção de substituição de regra padrão, os dispositivos Android dos usuários de destino não poderão ser desbloqueados, mesmo depois que os dispositivos estiverem registrados e compatíveis com o Intune. Para solucionar esse problema, defina a regra de acesso padrão do Exchange como **Quarentena**. O dispositivo não obterá acesso ao Exchange por padrão, e o administrador pode obter um relatório do Exchange server na lista de dispositivos que estão sendo colocados em quarentena.  

    Se você ainda não a instalação uma conta de email de notificação ao configurar o conector do Exchange, você verá um aviso nessa página e o **próxima** botão está desabilitado.  Antes de prosseguir, primeiro você deve definir as configurações de email de notificação no Exchange Connector e depois voltar para o **Assistente de Configuração de Política de Acesso Condicional** para concluir o processo.  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

5. Na página **Coleções de Destino** , adicione uma ou mais coleções de usuários. Para acessar o Exchange, os usuários nessas coleções devem registrar seus dispositivos no Intune e também ser compatíveis com as políticas de conformidade implantadas.  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

6. Na página **Coleções Isentas** , adicione todas as coleções de usuário que deseja isentar da política de acesso condicional. Os usuários nesses grupos, não precisam registrar seus dispositivos com o Intune e precisa estar em conformidade com as políticas de conformidade implantadas para acessar o Exchange.  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

    Se um usuário aparecer nas listas de destino e isenta, ele ficará isento da política de acesso condicional.  

7. Na página **Editar Notificação do Usuário**, configure o email enviado aos usuários pelo Intune com instruções de como desbloquear seus dispositivos (além do email enviado pelo Exchange).  

    Você pode editar a mensagem padrão e usar marcas HTML para formatar como o texto é exibido. Você também pode enviar um email com antecedência para seus funcionários, notificando sobre as alterações futuras e fornecendo instruções sobre como registrar seus dispositivos.  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    > Como o email de notificação do Intune que contém instruções de correção é entregue à caixa de correio do Exchange do usuário, se o dispositivo do usuário for bloqueado antes dele receber a mensagem de email, ele pode usar um dispositivo desbloqueado ou outro método para acessar o Exchange e exibir a mensagem.  
    > 
    > Para o Exchange enviar o email de notificação, configure a conta que será usada para enviar o email de notificação. Faça isso ao configurar as propriedades do conector do Exchange Server.  
    >   
    > Para saber mais, confira [Gerenciar dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  

8. Sobre o **resumo** página, examine as configurações e conclua o assistente.  


Examine as seguintes observações sobre esta política:  

- Você não precisa implantar a política de acesso condicional; ela entra em vigor imediatamente.  

- Depois que um usuário configura um perfil do Exchange ActiveSync, pode levar um a três horas para o dispositivo ser bloqueado (se ele não é gerenciado pelo Intune).  

- Se um usuário bloqueado, em seguida, registra o dispositivo com o Intune (ou solucionar a incompatibilidade), o acesso ao email será desbloqueado em até dois minutos.  

- Se o usuário cancelar-registro do Intune, poderá levar um a três horas para o dispositivo ser bloqueado.  


## <a name="see-also"></a>Consulte também  

[Gerenciar o acesso a serviços](/sccm/protect/deploy-use/manage-access-to-services)
