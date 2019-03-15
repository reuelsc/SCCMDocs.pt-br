---
title: Gerenciar o acesso aos serviços do O365
titleSuffix: Configuration Manager
description: Saiba como configurar o acesso condicional aos serviços do Office 365 para computadores gerenciados pelo System Center Configuration Manager.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 74a28863b2e30566b07890d57e927703d77247f6
ms.sourcegitcommit: ec4411fe30770f90128cf6cbd181047db90040cb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57881700"
---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Gerenciar o acesso aos serviços O365 para PCs gerenciados pelo System Center Configuration Manager.

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1191496-->
Configure o acesso condicional aos serviços do Office 365 para computadores gerenciados pelo Configuration Manager.  

> [!Important]  
> Incluindo o MDM híbrido no local são de acesso condicional [recursos preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  
> 
> Se você usar o acesso condicional em dispositivos gerenciados com o cliente do Configuration Manager, para certificar-se de que eles ainda estão protegidos, primeiro habilite o acesso condicional no Intune para os dispositivos antes de migrar. Habilitar o cogerenciamento no Configuration Manager, mover a carga de trabalho de política de conformidade para o Intune e, em seguida, concluir a migração do Intune híbrido para Intune autônomo. Para obter mais informações, consulte [acesso condicional com o cogerenciamento](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access). 


Para obter informações sobre como configurar o acesso condicional para dispositivos registrados e gerenciados pelo Microsoft Intune, consulte [Gerenciar o acesso a serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md). Esse artigo também aborda os dispositivos ingressados em domínio e não são avaliados quanto à conformidade.

> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


## <a name="supported-services"></a>Serviços com suporte  

-   Exchange Online
-   SharePoint Online

## <a name="supported-pcs"></a>PCs com suporte  

-   Windows 7
-   Windows 8.1
-   Windows 10

## <a name="supported-windows-servers"></a>Servidores Windows com Suporte

-   Windows Server 2008 R2
-   Windows Server 2012
-   Windows Server 2012 R2
-   Windows Server 2016

    > [!IMPORTANT]
    > Para Servidores Windows que possam ter vários usuários conectados ao mesmo tempo, implante as mesmas políticas de acesso condicional para todos esses usuários.

## <a name="configure-conditional-access"></a>Configurar o acesso condicional  
 Para configurar o acesso condicional, primeiro é necessário criar uma política de conformidade e configurar a política de acesso condicional. Ao configurar as políticas de acesso condicional para computadores, você pode exigir que os computadores estejam em conformidade a fim de acessar os serviços do Exchange Online e SharePoint Online.  

### <a name="prerequisites"></a>Pré-requisitos  

- Sincronização do ADFS e uma assinatura de O365. A assinatura de O365 serve para configurar o Exchange Online e o SharePoint Online.  

- Uma assinatura do Microsoft Intune. A assinatura do Microsoft Intune deve ser configurada no console do Configuration Manager. A assinatura do Intune é usada para transmitir o estado de conformidade do dispositivo para o Azure Active Directory e para o licenciamento do usuário.  

  Os PCs devem atender aos seguintes requisitos:  

- [Pré-requisitos](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) para registro automático do dispositivo com o Azure Active Directory  

   Você pode registrar os PCs com o Azure AD por meio da política de conformidade.  

  -   Para PCs com Windows 8.1 e Windows 10, você pode usar uma Política de Grupo do Active Directory para configurar os dispositivos a fim de registrar automaticamente no Azure AD.  

  -   o   Para PCs com Windows 7, você deve implantar o pacote do software de registro de dispositivo para seu PC com Windows 7 por meio do System Center Configuration Manager. O artigo [Registro de dispositivo automático com o Azure Active Directory para dispositivos ingressados no domínio do Windows](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) traz mais detalhes.  

- É necessário usar o Office 2013 ou Office 2016 com a autenticação moderna [habilitada](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a).  

  As etapas a seguir se aplicam ao Exchange Online e SharePoint Online  

### <a name="step-1-configure-compliance-policy"></a>Etapa 1. Configurar a política de conformidade  
 No Console do Configuration Manager, crie uma política de conformidade com as regras a seguir:  

-   **Requer registro no Azure Active Directory:** Esta regra verifica se o dispositivo do usuário é o local de trabalho associado ao Azure AD e se não, o dispositivo é registrado automaticamente no Azure AD. O registro automático só tem suporte no Windows 8.1. Para PCs com Windows 7, implante um MSI para realizar o registro automático. Para obter mais informações, consulte [Registro de dispositivo automático com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  

-   **Todas as atualizações necessárias instaladas com uma data limite superior a um determinado número de dias:** Especifique o valor para o período de cortesia do prazo de implantação para as atualizações necessárias no dispositivo do usuário. Adicionar esta regra também instala automaticamente quaisquer atualizações necessárias. Especifique as atualizações necessárias na regra **Atualizações automáticas necessárias**.   

-   **Exigir a Criptografia de Unidade de Disco BitLocker:** Essa regra verifica se a unidade principal (por exemplo, c\\) no dispositivo é criptografada pelo BitLocker. Se a criptografia não está habilitada no dispositivo primário, o acesso ao email e SharePoint services o BitLocker estiver bloqueado.  

-   **Exigir antimalware:** Esta regra verifica se o System Center Endpoint Protection ou o Windows Defender está habilitado e em execução. Se não estiver habilitado, o acesso aos serviços de email e do SharePoint estará bloqueado.  

-   **Relatado como Íntegro pelo serviço de atestado de integridade:** Essa condição inclui quatro sub-regras para verificar a conformidade do dispositivo no serviço de atestado de integridade do dispositivo. Para obter mais informações, consulte [Atestado de integridade](/sccm/core/servers/manage/health-attestation). 

    - **Exigir que o BitLocker esteja habilitado no dispositivo**
    - **Exigir que a Inicialização Segura esteja habilitada no dispositivo** 
    - **Exigir que a Integridade de Código esteja habilitada no dispositivo**
    - **Exigir que o Antimalware de Início Antecipado esteja habilitado no dispositivo**  

    >[!Tip]  
    > Os critérios de acesso condicional para o atestado de integridade do dispositivo foram introduzidos na versão 1710 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1802, esse recurso deixa de ser um recurso de pré-lançamento.<!--1235616-->  

    > [!Note]  
    > O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Etapa 2. Avaliar o efeito do acesso condicional  
 Execute o **Relatório de Conformidade de Acesso Condicional**. Ele pode ser encontrado no workspace **Monitoramento** em **Relatórios** > **Gerenciamento de conformidade e configurações**. Esse relatório exibe o status de conformidade para todos os dispositivos. Dispositivos relatados como fora de conformidade são impedidos de acessar o Exchange Online e o SharePoint Online.  

 ![Console do Configuration Manager, espaço de trabalho de monitoramento, relatórios, relatórios, conformidade e gerenciamento de configurações: Relatório de conformidade de acesso condicional](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Configurar grupos de segurança do Active Directory  
 Você direciona políticas de acesso condicional a grupos de usuários de acordo com os tipos de política. Esses grupos contêm os usuários que são afetados ou que ficam isentos da política. Quando uma política afeta um usuário, cada dispositivo usado por ele deve estar em conformidade para que possa acessar o serviço.  

 Grupos de usuário de segurança do Active Directory Esses grupos de usuário devem ser sincronizados com o Azure Active Directory. Você também pode configurar esses grupos no Centro de administração do Microsoft 365 ou portal de conta do Intune.  

 É possível especificar dois tipos de grupo em cada política. :  

-   **Grupos de destino** – grupos de usuários aos quais a política é aplicada. O mesmo grupo deve ser usado para as políticas de conformidade e de acesso condicional.  

-   **Grupos isentos** – grupos de usuários isentos da política (opcional).  
    Se um usuário estiver nas duas, ele ficará isento da política.  

     Somente os grupos que são afetados pela política de acesso condicional são avaliados.  

### <a name="step-3-create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Etapa 3. Criar uma política de acesso condicional para o Exchange Online e o SharePoint Online.  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  Para criar uma política para o Exchange Online, selecione **Habilitar política de acesso condicional para o Exchange Online**.  

     Para criar uma política para o SharePoint Online, selecione **Habilitar política de acesso condicional para o Exchange Online**.  

3.  Na guia **Início** , no grupo **Links** , clique em **Configurar Política de Acesso Condicional no Console do Intune**. Talvez seja necessário fornecer o nome de usuário e a senha da conta usada para conectar o Configuration Manager ao Intune.  

     O console de administração do Intune é aberto.  

4.  Para o Exchange Online, no console de administração do Microsoft Intune, clique em **Política > Acesso Condicional > Política do Exchange Online**.  

     Para o SharePoint Online, no console de administração do Microsoft Intune, clique em **Política > Acesso Condicional > Política do SharePoint Online**.  

5.  Defina o requisito de PC com Windows com a opção**Dispositivos devem ser compatíveis**.  

6.  Em **Grupos Direcionados**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory aos quais a política se aplica.  

    > [!NOTE]  
    >  O mesmo grupo de usuários de segurança deve ser usado para implantar a política de conformidade e o Grupo de Destino para a política de acesso condicional.  

     Opcionalmente, em **Grupos isentos**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory que são isentos dessa política.  

7.  Clique em **Salvar** para criar e salvar a política  

Os usuários exibem as informações de conformidade no Centro de Software. Quando estiver bloqueado devido à não conformidade, inicie uma nova avaliação de política após a correção dos problemas de conformidade.  


## <a name="see-also"></a>Consulte também

- [Protect data and site infrastructure with System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)
- [Fluxograma de solução de problemas de acesso condicional para o Configuration Manager](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0)
