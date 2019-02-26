---
title: Tutorial&#58; caminho de cogerenciamento 1
titleSuffix: Configuration Manager
description: Configure o cogerenciamento com o Microsoft Intune quando você já gerencia dispositivos Windows 10 com o Configuration Manager.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: brenduns
ms.author: brenduns
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1aecb2c33c874717f1da979f1316d1b46b785071
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754539"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Tutorial: Habilitar o cogerenciamento para clientes existentes do Configuration Manager
Com o cogerenciamento, você pode manter seus processos bem estabelecidos para usar o Configuration Manager para gerenciar PCs em sua organização. Ao mesmo tempo, você está investindo em nuvem por meio do uso do Intune para segurança e provisionamento modernos.  

Neste tutorial, você configurar cogerenciamento de dispositivos Windows 10 que já estão registrados no Configuration Manager. Este tutorial começa com a premissa de que você já usa o Configuration Manager para gerenciar seus dispositivos Windows 10.

Use este tutorial quando:  

- Você tem um local do Active Directory que você pode se conectar ao Azure Active Directory (Azure AD) em uma configuração híbrida do Azure AD
- Você tem clientes do Configuration Manager existente que você deseja anexar a nuvem


**Neste tutorial, você irá:**  
> [!div class="checklist"]  
> * Examine os pré-requisitos para o Azure e seu ambiente local  
> * Configurar o Azure AD híbrido  
> * Configurar agentes de cliente do Configuration Manager para se registrar com o Azure AD  
> * Configurar o Intune para registro automático de dispositivos  
> * Atribuir licenças do Intune aos usuários  
> * Habilitar o cogerenciamento no Configuration Manager  


## <a name="prerequisites"></a>Pré-requisitos  

### <a name="azure-services-and-environment"></a>Ambiente e os serviços do azure
- Assinatura do Azure ([avaliação gratuita](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Assinatura do Microsoft Intune
  > [!TIP]  
  > Uma Enterprise Mobility + Security (EMS) assinatura inclui o Azure Active Directory Premium e o Microsoft Intune. Assinatura do EMS ([avaliação gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Se não estiver presente em seu ambiente, durante este tutorial, você vai:
- Atribuir usuários uma licença do *Intune* e para *Azure Active Directory Premium*
- Configure [do Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) entre seu Active Directory no local e o Azure Active Directory (AD) do locatário


### <a name="on-premises-infrastructure"></a>Infraestrutura local
- Um [versão com suporte](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions) da ramificação atual do System Center Configuration Manager
- O [autoridade de MDM](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) deve ser definida para o Intune  


### <a name="permissions"></a>Permissões
Ao longo deste tutorial, use as seguintes permissões para concluir tarefas:  
- Uma conta que seja um *administrador global* no Azure  
- Uma conta que seja um *administrador de domínio* na sua infraestrutura local  
- Uma conta que seja um *administrador completo* para *todos os* escopos no Configuration Manager   

## <a name="set-up-hybrid-azure-ad"></a>Configurar o Azure AD híbrido
Quando você configura um híbrido do Azure AD, você realmente estiver configurando a integração de um local do AD com o Azure AD usando o Azure AD Connect e o Active Directory Federated Services (ADFS). Com uma configuração bem-sucedida, seus funcionários podem perfeitamente entrar usando suas instalações de sistemas externos credenciais do AD.

> [!IMPORTANT]  
> Este tutorial fornece detalhes sobre um processo básico para configurar híbrido do Azure AD para um domínio gerenciado. É recomendável que você esteja familiarizado com o processo e não depender neste tutorial como seu guia para compreender e implantar o Azure AD híbrido.
>
> Para obter mais informações sobre o Azure AD híbrido, inicie com os seguintes artigos na documentação do Azure Active Directory:
> - [Planejar sua implementação de junção do Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> -  [Planejar sua implementação de junção do Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> -  [Controlar a junção do Azure AD híbrido de seus dispositivos](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> -  [Configurar o ingresso no Azure AD híbrido para domínios federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  


### <a name="set-up-azure-ad-connect"></a>Configurar o Azure AD Connect  
Azure AD híbrido requer a configuração do Azure AD Connect para manter contas de computador no seu local do Active Directory (AD) e o objeto de dispositivo no Azure AD em sincronia.

Começando com a versão 1.1.819.0, Azure AD Connect fornece um Assistente para configurar o ingresso no Azure AD híbrido. Uso do assistente simplifica o processo de configuração.  

Para configurar o Azure AD Connect, você precisa de credenciais de um administrador global para seu locatário do Azure AD.  

> [!TIP]  
> O procedimento a seguir não devem ser considerado autoritativo para a configuração do Azure AD Connect, mas é fornecido aqui para ajudar a simplificar a configuração de cogerenciamento entre o Intune e Configuration Manager. Para o conteúdo autoritativo sobre isso e procedimentos relacionados para o conjunto de backup do Azure AD, consulte [configurar ingresso no AD do Azure híbrido para domínios gerenciados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) na documentação do Azure AD.  


#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Configurar um ingresso no Azure AD híbrido usando o Azure AD Connect

1. Obtenha e instale o [a versão mais recente do Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 ou superior).  
2. Inicie o Azure AD Connect e, em seguida, selecione **configurar**.
3. Sobre o **tarefas adicionais** página, selecione **configurar opções do dispositivo**e, em seguida, selecione **próxima**.
4. Sobre o **visão geral** página, selecione **próxima**.
5. Sobre o **conectar ao Azure AD** página, insira as credenciais de um administrador global para seu locatário do AD do Azure.
6. Sobre o **opções do dispositivo** página, selecione **junção do Azure AD híbrido de configurar**e, em seguida, selecione **próxima**.
7. Sobre o **SCP** página, para cada floresta local você deseja que o Azure AD Connect para configurar o ponto de conexão de serviço (SCP), execute as seguintes etapas e, em seguida, selecione **próxima**:  
   1. Selecione a floresta.  
   2. Selecione o serviço de autenticação.  Se você tiver um domínio federado, selecione o servidor do AD FS, a menos que sua organização tem exclusivamente os clientes do Windows 10 e você tiver configurado a sincronização do computador/dispositivo ou sua organização está usando [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Clique em **adicionar** para inserir as credenciais de administrador corporativo.  
8. Sobre o **sistemas operacionais de dispositivos** página, selecione os sistemas operacionais usados pelos dispositivos no ambiente do Active Directory e, em seguida, selecione **próxima**.  

   Você pode selecionar a opção para dar suporte a dispositivos de domínio de nível inferior do Windows, mas tenha em mente que o gerenciamento de dispositivos co só tem suporte para Windows 10.

9. Se você tiver um domínio gerenciado, ignore esta etapa.  

   Sobre o **configuração de Federação** página, insira as credenciais do administrador do AD FS e, em seguida, selecione **próxima**.
10. Sobre o **pronto para configurar** página, selecione **configurar**.
11. Sobre o **concluir a configuração** página, selecione **sair**.

Se você tiver problemas com o Azure AD híbrido join para domínio dispositivos ingressados no Windows, consulte [junção do Azure AD híbrido de solução de problemas para dispositivos atuais do Windows](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).


## <a name="configure-client-settings-to-direct-clients-register-with-azure-ad"></a>Definir configurações do cliente para direcionar os clientes registram no Azure AD  
Use as configurações do cliente para configurar os clientes do Configuration Manager para registrar automaticamente com o Azure AD.  

1. Abra o **console do Configuration Manager** > **administração** > **visão geral** > **as configurações do cliente** e, em seguida, edite o **configurações do cliente padrão**.  

2. Selecione **serviços de nuvem**.  

3. Sobre o **configurações padrão** , defina **registrar automaticamente novos dispositivos de ingressados no domínio do Windows 10 com o Azure Active Directory** para = **Sim**.  

4. Selecione **OK** para salvar esta configuração.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Configurar o registro automático de dispositivos ao Intune   
Em seguida, vamos definir o registro automático de dispositivos com o Intune. Com o registro automático, dispositivos que você gerencia com o Configuration Manager automaticamente registrar com o Intune.

O registro automático também permite que os usuários registrem seus dispositivos Windows 10 ao Intune. Os dispositivos registrados quando um usuário adiciona sua conta de trabalho para seus dispositivos pessoais, ou quando um dispositivo corporativo é associado ao Azure Active Directory.  

1. Entrar para o [portal do Azure](https://portal.azure.com/) e selecione **Azure Active Directory** > **mobilidade (MDM e MAM)** > **Microsoft Intune** .  

2. Configure **escopo do usuário MDM**. Especifique um dos seguintes procedimentos para configurar os dispositivos dos quais usuários são gerenciados pelo Microsoft Intune e aceite os padrões para os valores da URL.  

   - **Alguns** - selecione o **grupos** automaticamente que podem registrar seus dispositivos Windows 10  

   - **Todos os** -todos os usuários podem registrar automaticamente seus dispositivos Windows 10 quando definidos como **None**, registro automático de gerenciamento de dispositivo móvel (MDM) está desabilitado

   > [!IMPORTANT]  
   > Se os dois **escopo do usuário MAM** e o registro automático do MDM (**escopo do usuário MDM**) estão habilitadas para um grupo, somente MAM será habilitado. Somente MAM Mobile Application Management () é adicionado para usuários nesse grupo quando eles dispositivo pessoal de junção de local de trabalho. Dispositivos não são automaticamente registrados no MDM.  

3. Selecione **salvar** para concluir a configuração do registro automático.  

4. Retorne ao **mobilidade (MDM e MAM)** e, em seguida, selecione **registro do Microsoft Intune**.  

5. Para o escopo de usuário do MDM, selecione **todos os**e então **salvar**.  


## <a name="assign-intune-licenses-to-users"></a>Atribuir licenças do Intune aos usuários   
Uma ação geralmente subestimada, mas crítica é atribuir uma licença do Intune a cada usuário que irá usar um dispositivo é cogerenciado.  

Para atribuir licenças a grupos de usuários, use o Azure Active Directory.  

1. Entrar para o [portal do Azure](https://portal.azure.com/) com uma conta de administrador. Para gerenciar licenças, a conta deve ser um administrador de conta de usuário ou função de administrador global.  

2. Selecione **todos os serviços** no painel de navegação esquerdo e selecione **Azure Active Directory**.  

3. Sobre o **Azure Active Directory** painel, selecione **licenças** para abrir um painel onde você pode ver e gerenciar todos os produtos licenciados no locatário.  

4. Sob **todos os produtos**, selecione a opção de produto que inclui a licença do Intune e, em seguida, selecione **atribuir** na parte superior do painel.  

   Por exemplo, você pode selecionar **Enterprise Mobility + Security E5** se isso é como obter o Intune.  

5. Sobre o **atribuir licença** painel, clique em **usuários e grupos** para abrir o **usuários e grupos** painel. Selecione os grupos e usuários individuais aos quais você deseja atribuírem uma licença.  Em seguida, clique em **selecionar** na parte inferior do painel para confirmar a seleção.  

6. Sobre o **atribuir licença** painel, clique em **opções de atribuição** para exibir todos os planos de serviço incluídos no produto que você selecionou anteriormente. Se você tiver selecionado um único produto, como o Intune, somente esse produto é mostrado.  
   - Definir **Microsoft Intune** à **em**.  
   - Atribuir a cada usuário uma licença do **Azure Active Directory Premium**.  

   Quando as licenças aplicáveis são atribuídas, selecione **Okey**.  

7. Ao concluir a atribuição, o **atribuir licença** painel, clique em **atribuir** na parte inferior do painel.

8. Uma notificação é exibida no canto superior direito que mostra o status e o resultado do processo. Se a atribuição para o grupo não pôde ser concluída (por exemplo, devido a licenças já existentes no grupo), clique na notificação para exibir detalhes da falha.

Para obter mais informações sobre como atribuir licenças do Intune aos usuários, consulte [atribuir licenças](https://docs.microsoft.com/intune/licenses-assign).


## <a name="enable-co-management-in-configuration-manager"></a>Habilitar o cogerenciamento no Configuration Manager
Com híbrido do Azure AD configurado, as configurações de cliente do Configuration Manager em vigor e licenças de produto atribuídas a usuários, você está pronto para mudar a opção e habilitar o cogerenciamento de seus dispositivos Windows 10.  

> [!TIP]  
>  Na etapa seis do procedimento a seguir, você atribuirá uma coleção como uma *grupo piloto* para o cogerenciamento. Este é um grupo que contém um número pequeno de clientes para testar as configurações de cogerenciamento. É recomendável que você crie uma coleção adequada antes de iniciar o procedimento. Em seguida, você pode selecionar essa coleção sem concluir o procedimento para fazer isso.  

1. No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Cogerenciamento**.

2. Na guia página inicial, no grupo gerenciar, selecione **configurar o cogerenciamento** para abrir o Assistente de configuração de cogerenciamento.

3. Na página de assinatura, selecione **entrar** e entrar no seu locatário do Intune e, em seguida, selecione **próxima**.

4. Na página habilitação, do *registro automático do Intune* lista suspensa, selecione uma das seguintes opções:  

   - **Piloto**  - *(recomendado)* membros da coleção que você especificar são automaticamente registrados no Intune e, em seguida, podem ser gerenciados em conjunto. Especifique a coleção piloto na *preparo* página desse assistente. Essa opção permite que você teste o cogerenciamento em um subconjunto de clientes. Em seguida, você pode distribuir cogerenciamento para clientes adicionais usando uma abordagem em fases.  

   - **Todos os** -habilitar o cogerenciamento para todos os clientes.  

5. Na página cargas de trabalho, você pode mudar cargas de trabalho da **Configuration Manager** a um dos seguintes e, em seguida, quando estiver pronto para continuar, selecione **próxima**.  

   - **Criar um piloto do Intune** -alterna uma carga de trabalho apenas para os dispositivos no grupo piloto. Você atribuirá uma coleção como o grupo piloto na próxima página do assistente.  

   - **Intune** -muda a carga de trabalho associada para todos os dispositivos Windows 10 cogerenciados.  

   Você não precisa mudar as cargas de trabalho no momento em que você habilitar o cogerenciamento. Você pode visitar novamente esta configuração no console do Gerenciador de configuração mais tarde, após a configuração de cogerenciamento.  

   Antes de mudar uma carga de trabalho, verifique se a carga de trabalho correspondente no Intune é configurada e implantada. Fazer então mantém as cargas de trabalho gerenciados.  

6. Na página preparo, especifique uma coleção a ser usado para o **coleção piloto**e, em seguida, clique em **próxima**. A coleção que você especifica é usada como parte de sua distribuição em fases do cogerenciamento. Você pode alterar as coleções no grupo piloto a qualquer momento por meio das propriedades de cogerenciamento.  

7. Na página de resumo, selecione **próxima**e então **fechar** para concluir o assistente.  


## <a name="next-steps"></a>Próximas etapas
- Verificar o status dos dispositivos gerenciados em conjunto com o [painel de cogerenciamento](/sccm/comanage/how-to-monitor)
- Comece obtendo [valor imediato](quickstarts.md#immediate-value) do cogerenciamento
- Use [acesso condicional](quickstart-conditional-access.md) e regras de conformidade do Intune para gerenciar o acesso do usuário aos recursos corporativos
