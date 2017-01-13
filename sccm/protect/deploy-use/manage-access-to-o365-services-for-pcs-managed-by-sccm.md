---
title: "Gerenciar o acesso aos serviços do O365 para computadores gerenciados | Microsoft Docs"
description: Saiba como configurar o acesso condicional para computadores gerenciados pelo System Center Configuration Manager.
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccdb424a-b603-4ccc-af36-558924248022
caps.latest.revision: 15
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: da5fcd65d7af8d73aa23f4a7d96cd8fc6e48f9dc


---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Gerenciar o acesso aos serviços O365 para PCs gerenciados pelo System Center Configuration Manager.

*Aplica-se a: System Center Configuration Manager (Branch Atual)*



 A partir da versão 1602 do Configuration Manager, é possível configurar o acesso condicional para computadores gerenciados pelo System Center Configuration Manager.  

> [!IMPORTANT]  
>  Esse é um recurso de pré-lançamento disponível nas atualizações 1602, 1606 e 1610. Os recursos de pré-lançamento foram incluídos no produto para testes iniciais em um ambiente de produção, mas não devem ser considerados prontos para produção. Para obter mais informações, consulte [Usar recursos de pré-lançamento de atualizações](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).
> - Depois de instalar a atualização 1602, o tipo de recurso é exibido como liberado apesar de ser pré-lançamento.
> - Se você atualiza da 1602 para a 1606, o tipo de recurso é exibido como liberado apesar de continuar sendo pré-lançamento.
> - Se você atualiza da versão 1511 diretamente para a 1606, o tipo de recurso é exibido como pré-lançamento.

 Se você estiver procurando informações sobre como configurar o acesso condicional para dispositivos registrados e gerenciados pelo Intune, ou para PCs que ingressaram no domínio e não são avaliados com relação à conformidade, consulte [Gerenciar o acesso a serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md).  


## <a name="supported-services"></a>Serviços com suporte  

-   Exchange Online  

-   SharePoint Online  

## <a name="supported-pcs"></a>PCs com suporte  

-   Windows 7  

-   Windows 8.1  

-   O Windows 10 ainda não tem suporte total.  Se você tentar definir o acesso condicional para PCs com Windows 10, talvez encontre alguns problemas.  Consulte [Problemas conhecidos](#bkmk_KnownIssues) para obter mais detalhes.  

## <a name="configure-conditional-access"></a>Configurar o acesso condicional  
 Para configurar o acesso condicional, primeiro você precisa criar uma política de conformidade e configurar a política de acesso condicional. Ao configurar as políticas de acesso condicional para PCs, você pode exigir que os PCs estejam em conformidade com a política de conformidade a fim de acessar os serviços do Exchange Online e do SharePoint Online.  

### <a name="prerequisites"></a>Pré-requisitos  

-   Sincronização do ADFS e uma assinatura de O365. A assinatura de O365 serve para configurar o Exchange Online e o SharePoint Online.  

-   Uma assinatura do Microsoft Intune. A assinatura do Microsoft Intune deve ser configurada no console do Configuration Manager. Isso ainda exige que você esteja em uma implantação híbrida.  

 Os PCs devem atender aos seguintes requisitos:  

-   [Pré-requisitos](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) para registro automático do dispositivo com o Azure Active Directory  

     Você pode registrar os PCs com o Azure AD por meio da política de conformidade.  

    -   Para PCs com Windows 8.1 e Windows 10, você pode usar uma Política de Grupo do Active Directory para configurar os dispositivos a fim de registrar automaticamente no Azure AD.  

    -   o   Para PCs com Windows 7, você deve implantar o pacote do software de registro de dispositivo para seu PC com Windows 7 por meio do System Center Configuration Manager. O tópico [Registro de dispositivo automático com o Azure Active Directory para dispositivos ingressados no domínio do Windows](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) traz mais detalhes.  

-   É necessário usar o Office 2013 ou Office 2016 com a autenticação moderna [habilitada](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a).  

 As etapas descritas abaixo se aplicam ao Exchange Online e ao SharePoint Online  

### <a name="step-1-configure-compliance-policy"></a>Etapa 1. Configurar a política de conformidade  
 No Console do Configuration Manager, crie uma política de conformidade com as regras a seguir:  

-   Requer registro no Azure Active Directory: essa regra verifica se o dispositivo do usuário é o local de trabalho associado ao Azure AD; se não, o dispositivo será registrado automaticamente no Azure AD. O registro automático só tem suporte no Windows 8.1. Para PCs com Windows 7, implante um MSI para realizar o registro automático. Para obter mais detalhes, consulte [Registro de dispositivo automático com o Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)  

-   **Todas as atualizações necessárias instaladas com um prazo superior a determinado número de dias:** essa regra verifica se o dispositivo do usuário tem todas as atualizações necessárias (especificadas na regra Atualizações automáticas necessárias) dentro do prazo e período de carência especificado por você e instala automaticamente quaisquer atualizações necessárias.  

-   **Exigir criptografia de unidade de disco BitLocker:** essa é uma verificação para ver se a unidade principal (por exemplo, C:\\) no dispositivo é criptografada pelo BitLocker. Se a criptografia Bitlocker não estiver habilitada no dispositivo primário, o acesso aos serviços de email e do SharePoint será bloqueado.  

-   **Exigir Antimalware:** essa é uma verificação para ver se o software antimalware (somente System Center Endpoint Protection ou Windows Defender) está habilitado e em execução. Se não estiver habilitado, o acesso aos serviços de email e do SharePoint estará bloqueado.  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Etapa 2. Avaliar o efeito do acesso condicional  
 Execute o Relatório de conformidade de acesso condicional. Ele pode ser encontrado na seção Monitoramento em Relatórios > Gerenciamento de Conformidade e Configurações. Isso exibe o status de conformidade para todos os dispositivos.  Dispositivos reportados como não compatíveis serão impedidos de acessar o Exchange Online e o SharePoint Online.  

 ![CA&#95;compliance&#95;report](../media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Configurar grupos de segurança do Active Directory  
 Você direciona políticas de acesso condicional a grupos de usuários de acordo com os tipos de política. Esses grupos contêm os usuários que serão afetados ou que ficarão isentos da política. Quando um usuário é afetado por uma política, cada dispositivo que ele usa deve ser compatível para que possa acessar o serviço.  

 Grupos de usuário de segurança do Active Directory Esses grupos de usuário devem ser sincronizados com o Azure Active Directory. Você também pode configurar esses grupos no Centro de administração do Office 365 ou no Portal de conta do Intune.  

 É possível especificar dois tipos de grupo em cada política. :  

-   **Grupos de destino** – grupos de usuários aos quais a política é aplicada. O mesmo grupo deve ser usado para as políticas de conformidade e de acesso condicional.  

-   **Grupos isentos** – Grupos de usuários isentos da política (opcional)  
    Se um usuário estiver nas duas, ele ficará isento da política.  

     Somente os grupos que são afetados pela política de acesso condicional são avaliados.  

### <a name="step-3--create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Etapa 3.  Criar uma política de acesso condicional para o Exchange Online e o SharePoint Online.  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  Para criar uma política para o Exchange Online, selecione **Habilitar política de acesso condicional para o Exchange Online**.  

     Para criar uma política para o SharePoint Online, selecione **Habilitar política de acesso condicional para o Exchange Online**.  

3.  Na guia **Início** , no grupo **Links** , clique em **Configurar Política de Acesso Condicional no Console do Intune**. Talvez seja necessário fornecer o nome de usuário e a senha da conta usada para conectar o Configuration Manager ao Intune.  

     O console de administração do Intune será aberto.  

4.  Para o Exchange Online, no console de administração do Microsoft Intune, clique em **Política > Acesso Condicional > Política do Exchange Online**.  

     Para o SharePoint Online, no console de administração do Microsoft Intune, clique em **Política > Acesso Condicional > Política do SharePoint Online**.  

5.  Defina o requisito de PC com Windows com a opção**Dispositivos devem ser compatíveis**.  

6.  Em **Grupos de Destino**, clique em **Modificar** para selecionar os grupos de segurança do Active Directory do Azure aos quais a política será aplicada.  

    > [!NOTE]  
    >  O mesmo grupo de usuários de segurança deve ser usado para implantar a política de conformidade e o Grupo de Destino para a política de acesso condicional.  

     Opcionalmente, em **Grupos isentos**, clique em **Modificar** para selecionar os grupos de segurança do Active Directory do Azure que são isentos dessa política.  

7.  Clique em **Salvar** para criar e salvar a política  

 Usuários finais bloqueados por falta de conformidade verão informações de conformidade no Centro de Software do System Center Configuration Manager e iniciarão uma nova avaliação de política quando problemas de conformidade forem corrigidos.  

##  <a name="a-namebkmkknownissuesa-known-issues"></a><a name="bkmk_KnownIssues"></a> Problemas conhecidos  
 Talvez você veja os seguintes problemas ao usar esse recurso:  

-   Nesta atualização 1602, a conformidade de cinco dias não é imposta. Mesmo se a verificação de conformidade no dispositivo do usuário final tiver ocorrido há mais de cinco dias, os usuários ainda poderão acessar o Office 365 e o SharePoint online.  

-   Quando um dispositivo não for compatível com a política de conformidade, o motivo não será exibido automaticamente. O usuário final deve acessar o novo Centro de Software para descobrir o motivo da não conformidade. O motivo é exibido na seção de Conformidade do dispositivo do Centro de Software.  

-   Os usuários do Windows 10 podem ver várias falhas de acesso ao tentar acessar recursos do O365 e/ou do SharePoint Online. Observe que o acesso condicional não tem suporte total para o Windows 10.  

### <a name="see-also"></a>Consulte também  
 [Proteger a infraestrutura de dados e do site com o System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)



<!--HONumber=Dec16_HO3-->


