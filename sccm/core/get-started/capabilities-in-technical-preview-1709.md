---
title: Technical Preview 1709
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis na Technical Preview versão 1709 do System Center Configuration Manager.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 74ffd06f8b9786d627dc7fd9cecb15215228313d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1709-for-system-center-configuration-manager"></a>Recursos na Technical Preview 1709 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos que estão disponíveis na Technical Preview do System Center Configuration Manager, versão 1709. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão da visualização técnica, veja [Visualização Técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de uma visualização técnica, como atualizar entre versões e como fornecer comentários sobre os recursos em uma visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos nesse Technical Preview:**
-   **A atualização para a versão prévia 1709 falha quando há um servidor do site no modo passivo**. Quando você executar a versão prévia 1706, 1707 ou 1708 e houver um [servidor do site primário no modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), você deverá desinstalar o servidor do site de modo passivo para que seja possível atualizar seu site da versão prévia com êxito para a versão 1709. Quando seu site estiver executando a versão 1709, você poderá reinstalar o servidor do site de modo passivo.

  Para desinstalar o servidor do site no modo passivo:
  1. No console, acesse **Administração** > **Visão geral** > **Configuração do Site** > **Servidores e Funções do Sistema de Sites** e selecione o servidor de site no modo passivo.
  2. No painel **Funções do Sistema de Site**, clique com o botão direito na função **Servidor do Site** e, em seguida, escolha **Remover Função**.
  3. Clique com o botão direito no servidor do site de modo passivo e, em seguida, escolha **Excluir**.
  4. Após a desinstalação do servidor do site, no servidor do site primário ativo, reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Melhoria da experiência do perfil de VPN no Console do Configuration Manager
<!-- 1313282 -->
Com esta versão, as páginas de assistente e de propriedades do perfil de VPN foram atualizadas para exibir as configurações apropriadas para a plataforma selecionada. Especificamente:

- Cada plataforma tem seu próprio fluxo de trabalho, o que significa que os novos perfis de VPN contêm apenas a configuração com suporte na plataforma.
- As páginas **Plataformas com Suporte** agora são exibidas após a página **Geral**.  Agora você escolhe a plataforma antes de configurar os valores das propriedades.
- Quando a plataforma está definida como **Android**, **Android for Work** ou **Windows Phone 8.1**, a página **Plataformas com Suporte** não é necessária e não é exibida.
- O fluxo de trabalho baseado no cliente do Configuration Manager foi combinado com os fluxos de trabalho do Windows 10 baseados no cliente do dispositivo móvel híbrido (MDM). Eles dão suporte às mesmas configurações.
- O fluxo de trabalho de cada plataforma inclui apenas as configurações apropriadas para esse fluxo de trabalho.  Por exemplo, o fluxo de trabalho do Android contém as configurações apropriadas para Android e as configurações apropriadas para iOS ou Windows 10 Mobile não aparecem mais no fluxo de trabalho do Android.
- Para dispositivos Windows 8.1, as configurações gerenciadas pelo Configuration Manager estão claramente marcadas.
- A página VPN automática ficou obsoleta e foi removida.

Essas alterações aplicam-se aos novos perfis de VPN.  

Para minimizar o risco de compatibilidade, os perfis de VPN existentes não foram alterados.  Quando você edita um perfil existente, as configurações são exibidas como quando o perfil foi criado.  

### <a name="try-it-out"></a>Experimente!

Crie um novo perfil de VPN usando o processo normal. Observe que a primeira página de opções do assistente de perfil de VPN foi alterada.

1.  Acesse **Ativos e Conformidade** > **Visão Geral** > **Configurações de Conformidade** > **Acesso aos Recursos da Empresa** > **Perfis de VPN** e, em seguida, escolha **Criar Perfil de VPN**.
2.  Insira um nome na página **Geral** e escolha uma das opções a seguir em **Especificar o tipo de perfil de VPN que você deseja criar**:

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS e macOS  
    - Android  
    - Android for Work  

3.  Se você escolher **Windows 8.1**, também haverá a opção de **Criar novo perfil** ou **Importar do arquivo**.
4.  Finalize o assistente para concluir a criação do perfil.

Conforme você selecionar diferentes plataformas, observe que serão exibidas apenas as configurações relevantes para a plataforma selecionada.

## <a name="co-management-for-windows-10-devices"></a>Cogerenciamento para dispositivos Windows 10    
<!-- 1350871 -->
Muitos clientes desejam gerenciar os dispositivos Windows 10 da mesma forma em que gerenciam os dispositivos móveis, usando uma solução baseada em nuvem simplificada e com menor custo. No entanto, fazer a transição do gerenciamento tradicional para o gerenciamento moderno pode ser um desafio. A partir do Windows 10, versão 1607 (também conhecido como a Atualização de Aniversário), você pode associar um dispositivo com Windows 10 ao Active Directory (AD) local e ao Azure AD baseado em nuvem ao mesmo tempo (Azure AD híbrido). O cogerenciamento aproveita essa melhoria e permite que você gerencie dispositivos com Windows 10 simultaneamente por meio do Configuration Manager e o Intune. É uma solução que fornece uma ponte do gerenciamento tradicional para o moderno e fornece um caminho para fazer a transição usando uma abordagem em fases. 

### <a name="prerequisites"></a>Pré-requisitos
Você deve ter os seguintes pré-requisitos em vigor antes de habilitar o cogerenciamento. Há pré-requisitos gerais e pré-requisitos diferentes para clientes existentes do Configuration Manager e para dispositivos que não são clientes.

### <a name="known-issues"></a>Problemas conhecidos
Depois de criar uma política de cogerenciamento, você não poderá editar a política. Para alterar a política, exclua-a e, em seguida, recrie-a com as configurações necessárias. 

#### <a name="general-prerequisites"></a>Pré-requisitos gerais
Estes são os pré-requisitos gerais para habilitar o cogerenciamento:  

- Technical Preview do Configuration Manager versão 1709
- Azure AD 
- Licença do EMS ou do Intune para todos os usuários
- Assinatura do Intune &#40;autoridade do MDM no Intune definida para **Intune**&#41;

   > [!Note]  
   > Se você tiver um ambiente de MDM híbrido (Intune integrado ao Configuration Manager), não será possível habilitar o cogerenciamento. Se você estiver interessado em migrar para o Intune autônomo, consulte [Start migrating from hybrid MDM to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) (Iniciar a migração do MDM híbrido para o Intune autônomo).

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Pré-requisitos adicionais para os clientes existentes do Configuration Manager
- Windows 10, versão 1709 (Fall Creators Update) e posterior
- Ingressado no Azure AD híbrido (ingressado no AD e no Azure AD)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Pré-requisitos adicionais para novos dispositivos Windows 10
- Windows 10, versão 1709 (Fall Creators Update) e posterior
- [Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager

### <a name="workloads-you-can-switch-to-intune"></a>Cargas de trabalho que você pode mudar para o Intune
Depois que você habilitar o cogerenciamento, o Configuration Manager continuará a gerenciar todas as cargas de trabalho. Quando você decidir que está pronto, poderá fazer com que o Intune comece a gerenciar as cargas de trabalho disponíveis. Nesta versão, o Intune pode gerenciar as cargas de trabalho as seguir.   

#### <a name="compliance-policies"></a>Políticas de conformidade
As políticas de conformidade definem as regras e configurações que um dispositivo deve obedecer para ser considerado em conformidade pelas políticas de acesso condicional. Você também pode usar as políticas de conformidade para monitorar e corrigir problemas com dispositivos, independentemente do acesso condicional. Para obter detalhes, consulte [Políticas de conformidade do dispositivo](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/device-compliance-policies).  

#### <a name="windows-update-for-business-policies"></a>Políticas do Windows Update para Empresas
As políticas do Windows Update para Empresas permitem configurar políticas de adiamento para atualizações de recursos ou atualizações de qualidade do Windows 10 para dispositivos Windows 10 gerenciados diretamente pelo Windows Update para Empresas. Para obter detalhes, consulte [Configurar as políticas de adiamento do Windows Update for Business](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Ações remotas disponíveis no Intune no Azure para dispositivos cogerenciados
Quando um dispositivo Windows 10 está habilitado para cogerenciamento, você tem as seguintes ações remotas disponíveis por meio do Intune no Azure:  
- [Redefinição de fábrica](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [Apagamento seletivo](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Excluir dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Reiniciar dispositivo](https://docs.microsoft.com/intune/device-restart)
- [Novo início](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Preparar o Intune para o cogerenciamento
Antes de mudar as cargas de trabalho do Configuration Manager para o Intune, crie os perfis e as políticas que você precisa no Intune para garantir que os dispositivos continuem protegidos.
Você pode criar objetos no Intune com base nos objetos que você tem no Configuration Manager. Ou, se sua estratégia atual se baseia em gerenciamento herdado ou tradicional, convém fazer uma pausa para repensar quais políticas e perfis são necessários para o gerenciamento moderno. Use os recursos a seguir para criar os perfis e as políticas.    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Políticas do Windows Update para Empresas](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [Perfis de configuração do dispositivo](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Visão geral de arquitetura para cogerenciamento
O diagrama a seguir fornece uma visão geral da arquitetura de cogerenciamento e como ela se encaixa nas infraestruturas existentes do Configuration e do Intune.

![Diagrama de arquitetura de cogerenciamento](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Cenários para habilitar o cogerenciamento  
Você pode habilitar o cogerenciamento tanto para dispositivos Windows 10 registrados no Microsoft Intune quanto para clientes Windows 10 existentes do Configuration Manager. Ambos os cenários resultam em dispositivos Windows 10 gerenciados simultaneamente pelo Configuration Manager e pelo Intune, e também ingressados no AD e no Azure AD.  

#### <a name="devices-enrolled-in-intune"></a>Dispositivos registrados no Intune  
Quando dispositivos Windows 10 são registrados no Intune, você pode instalar o cliente do Configuration Manager nos dispositivos (usando um argumento de linha de comando específico) para preparar os clientes para o cogerenciamento. Em seguida, você habilitar o cogerenciamento no console do Configuration Manager para começar a mover para o Intune cargas de trabalho específicas de dispositivos Windows 10 específicos.  

Para dispositivos Windows 10 que ainda não estão registrados no Intune, você pode usar o registro automático no Azure para registrar os dispositivos. Para novos dispositivos Windows 10, você pode usar o Windows AutoPilot para definir a OOBE (configuração inicial pelo usuário), que inclui o registro automático que registra os dispositivos no Intune.  

#### <a name="configuration-manager-clients"></a>Clientes do Configuration Manager
Quando houver dispositivos Windows 10 que sejam clientes do Configuration Manager, você poderá registrar esses dispositivos e habilitar o cogerenciamento no console do Configuration Manager. O Configuration Manager dispara o registro automático no Intune com base nas informações de locatário do Azure AD.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Preparar dispositivos Windows 10 para o cogerenciamento
Você pode habilitar o cogerenciamento em dispositivos Windows 10 que foram ingressados no AD e no Azure AD e registrados no Intune e em um cliente no Configuration Manager. Para novos dispositivos Windows 10 e dispositivos que já estão registrados no Intune, instale o cliente do Configuration Manager antes que eles possam ser cogerenciados. Para dispositivos Windows 10 que já são clientes do Configuration Manager, você pode registrar os dispositivos no Intune e habilitar o cogerenciamento no console do Configuration Manager.

#### <a name="command-line-to-install-configuration-manager-client"></a>Linha de comando para instalar o cliente do Configuration Manager
Crie um aplicativo no Intune para dispositivos Windows 10 que ainda não são clientes do Configuration Manager. Ao criar o aplicativo nas próximas seções, use a seguinte linha de comando:

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*URL do ponto de extremidade de autenticação mútua do gateway de gerenciamento de nuvem*&#62;/ CCMHOSTNAME=&#60;*URL do ponto de extremidade de autenticação mútua do gateway de gerenciamento de nuvem*&#62; SMSSiteCode=&#60;*Código do site*&#62; SMSMP=https:&#47;/&#60;*FQDN do MP*&#62; AADTENANTID=&#60;*ID do locatário do AAD*&#62; AADTENANTNAME=&#60;*Nome do locatário*&#62; AADCLIENTAPPID=&#60;*AppID do servidor para integração com o AAD*&#62; AADRESOURCEURI=https:&#47;/&#60;*ID do recurso*&#62;”

Por exemplo, se você tiver os valores a seguir:

- **URL do ponto de extremidade de autenticação mútua do gateway de gerenciamento de nuvem**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Use o valor **MutualAuthPath** na exibição de SQL **vProxy_Roles** para o valor da **URL do ponto de extremidade de autenticação mútua do gateway de gerenciamento de nuvem**.

- **FQDN do MP (ponto de gerenciamento)**: sccmmp.corp.contoso.com    
- **Código do site**: PS1    
- **ID do locatário do Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Nome do locatário do Azure AD**: contoso    
- **ID do aplicativo cliente do Azure AD**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI da ID do recurso do AAD**: ConfigMgrServer    

  > [!Note]    
  > Use o valor **IdentifierUri** encontrado na exibição de SQL **vSMS_AAD_Application_Ex** para o valor do **URI da ID do recurso do AAD**.

Você usaria a seguinte linha de comando:

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer”

> [!Tip]
>Você pode encontrar os parâmetros de linha de comando para o seu site usando as seguintes etapas:     
> 1. No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Cogerenciamento**.  
> 2. Na guia Início, no grupo Gerenciar, escolha **Configurar o cogerenciamento** para abrir o Assistente para Integração de Cogerenciamento.    
> 3. Na página Assinatura, clique em **Entrar**, entre no seu locatário do Intune e, em seguida, clique em **Avançar**.    
> 4. Na página Habilitação, clique em **Copiar** na seção **Dispositivos registrados no Intune** para copiar a linha de comando para a área de transferência e, em seguida, salve a linha de comando, que será usada no procedimento para criar o aplicativo.  
> 5. Clique em **Cancelar** para sair do assistente.

#### <a name="new-windows-10-devices"></a>Novos dispositivos Windows 10
Para novos dispositivos Windows 10, você pode usar o serviço AutoPilot para definir a configuração inicial pelo usuário, que inclui ingressar o dispositivo no AD e no Azure AD, bem como registrar o dispositivo no Intune. Em seguida, crie um aplicativo no Intune para implantar o cliente do Configuration Manager.  
1. Habilite o AutoPilot para os novos dispositivos Windows 10. Para obter detalhes, consulte [Visão geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Configure o registro automático no Azure AD para que seus dispositivos sejam registrados automaticamente no Intune. Para obter detalhes, consulte  [Registrar os dispositivos Windows no Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Crie um aplicativo no Intune com o pacote do cliente do Configuration Manager e implante o aplicativo nos dispositivos Windows 10 que você deseja cogerenciar. Use a [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) ao percorrer as etapas para [instalar clientes da Internet usando o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivos Windows 10 não registrados no Intune nem em um cliente do Configuration Manager
Para dispositivos Windows 10 que não estão registrados no Intune e não têm o cliente do Configuration Manager, você pode usar o registro automático para registrar o dispositivo no Intune. Em seguida, crie um aplicativo no Intune para implantar o cliente do Configuration Manager.
1. Configure o registro automático no Azure AD para que seus dispositivos sejam registrados automaticamente no Intune. Para obter detalhes, consulte  [Registrar os dispositivos Windows no Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Crie um aplicativo no Intune com o pacote do cliente do Configuration Manager e implante o aplicativo nos dispositivos Windows 10 que você deseja cogerenciar. Use a [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) ao percorrer as etapas para [instalar clientes da Internet usando o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).

#### <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivos Windows 10 registrados no Intune
Para dispositivos Windows 10 que já estão registrados no Intune, crie um aplicativo no Intune para implantar o cliente do Configuration Manager. Use a [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) ao percorrer as etapas para [instalar clientes da Internet usando o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Mudar as cargas de trabalho do Configuration Manager para o Intune
Na seção anterior, você preparou os dispositivos Windows 10 para o cogerenciamento. Agora, esses dispositivos ingressaram no AD e no Azure AD, e estão registrados no Intune e têm o cliente do Configuration Manager. Provavelmente ainda há dispositivos Windows 10 que ingressaram no AD e têm o cliente do Configuration Manager, mas que não ingressaram no Azure AD e não estão registrados no Intune. O procedimento a seguir fornece as etapas para habilitar o cogerenciamento e preparar o restante dos dispositivos Windows 10 (clientes do Configuration Manager sem registro no Intune) para o cogerenciamento e permite que você comece a mudar cargas de trabalho do Configuration Manager específicas para o Intune.

1. No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Cogerenciamento**.    
2. Na guia Início, no grupo Gerenciar, escolha **Configurar o cogerenciamento** para abrir o Assistente para Integração de Cogerenciamento.    
3. Na página Assinatura, clique em **Entrar**, entre no seu locatário do Intune e, em seguida, clique em **Avançar**.   
4. Na página Preparo, defina as seguintes configurações e, em seguida, clique em **Avançar**:
    - **Grupo piloto**: o grupo piloto contém uma ou mais coleções para você selecionar. Use esse grupo como parte de sua distribuição em fases do cogerenciamento. É possível começar com uma coleção de teste pequena e, em seguida, adicionar mais coleções ao grupo piloto à medida que você distribui o cogerenciamento para mais usuários e dispositivos. Você pode alterar as coleções no grupo piloto a qualquer momento por meio das propriedades de cogerenciamento.
    - **Produção**: quando você seleciona essa configuração, todos os dispositivos Windows 10 com suporte são habilitados para o cogerenciamento. Configure o **Grupo de exclusão** com uma ou mais coleções. Os dispositivos que são membros de uma das coleções neste grupo são excluídos do uso do cogerenciamento. 
5. Na página Habilitação, escolha **Piloto** ou **Todos** (dependendo das configurações que você configurou na página Preparo) para habilitar o registro automático do Intune e, em seguida, clique em **Avançar**. Quando você escolhe **Piloto**, somente os clientes do Configuration Manager que são membros do grupo piloto são registrados automaticamente no Intune. Isso permite que você habilite o cogerenciamento em um subconjunto de clientes para testá-lo inicialmente e distribuí-lo usando uma abordagem em fases. 
6. Na página Cargas de trabalho, escolha se deseja mudar as cargas de trabalho do Configuration Manager para serem gerenciadas pelo Intune e, em seguida, clique em **Avançar**. Use os controles deslizantes para mudar a carga de trabalho para o grupo piloto ou para todos os clientes Windows 10 (dependendo das configurações que você configurou na página Preparo). 
7. Para habilitar o cogerenciamento, conclua o assistente.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Consulte também
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview). 
