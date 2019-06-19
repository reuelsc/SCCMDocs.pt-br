---
title: Tutorial&#58;Habilitar o cogerenciamento de clientes existentes do Configuration Manager
titleSuffix: Configuration Manager
description: Configure o cogerenciamento com o Microsoft Intune quando você já gerenciar dispositivos Windows 10 com o Configuration Manager.
ms.date: 06/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b19f54d60ed0594be4a51b5abcef69304a27ece
ms.sourcegitcommit: 0bd336e11c9a7f2de05656496a1bc747c5630452
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66834757"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Tutorial: Habilitar o cogerenciamento de clientes existentes do Configuration Manager
Com o cogerenciamento, você pode manter os seus processos bem estabelecidos para usar o Configuration Manager a fim de gerenciar PCs em sua organização. Ao mesmo tempo, você está investindo na nuvem com o uso do Intune para provisionamento moderno e de segurança.  

Neste tutorial, você configurará o cogerenciamento de dispositivos Windows 10 que já estão registrados no Configuration Manager. Este tutorial começa com a premissa de que você já usa o Configuration Manager para gerenciar seus dispositivos Windows 10.

Use este tutorial quando:  

- Você tiver um Active Directory local o qual você possa conectar ao Azure AD (Azure Active Directory) em uma configuração híbrida do Azure AD. 

  Se você não puder implantar um Azure AD (Active Directory) híbrido que una o AD local ao Azure AD, recomendamos seguir nosso tutorial complementar, [Habilitar o cogerenciamento para novos dispositivos Windows 10 baseados na internet](/sccm/comanage/tutorial-co-manage-new-devices). 
- Você tem clientes do Configuration Manager os quais deseja anexar à nuvem.


**Neste tutorial, você vai:**  
> [!div class="checklist"]  
> * Examinar os pré-requisitos para o Azure e seu ambiente local  
> * Configurar o Azure AD híbrido  
> * Configurar agentes de cliente do Configuration Manager para se registrar com o Azure AD  
> * Configurar o Intune para o registro automático de dispositivos  
> * Atribuir licenças do Intune aos usuários  
> * Habilitar o cogerenciamento no Configuration Manager  


## <a name="prerequisites"></a>Pré-requisitos  

### <a name="azure-services-and-environment"></a>Ambiente e serviços do Azure
- Assinatura do Azure ([avaliação gratuita](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Assinatura do Microsoft Intune
  > [!TIP]  
  > Uma Assinatura EMS (Enterprise Mobility + Security) inclui o Azure Active Directory Premium e o Microsoft Intune. Assinatura EMS ([avaliação gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Se isso ainda não estiver presente em seu ambiente, durante este tutorial, você vai:
- Atribuir aos usuários uma licença do *Intune* e do *Azure Active Directory Premium*
- Configurar o [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) entre o Active Directory local e seu locatário do Azure AD (Azure Active Directory)


### <a name="on-premises-infrastructure"></a>Infraestrutura local
- Uma [versão compatível](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions) do branch atual do System Center Configuration Manager
- A [Autoridade de MDM](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) deve ser definida para o Intune  


### <a name="permissions"></a>Permissões
Ao longo deste tutorial, use as seguintes permissões para concluir tarefas:  
- Uma conta que seja um *administrador global* no Azure  
- Uma conta que seja um *administrador de domínio* na sua infraestrutura local  
- Uma conta que seja um *administrador completo* para *todos* os escopos no Configuration Manager   

## <a name="set-up-hybrid-azure-ad"></a>Configurar o Azure AD híbrido
Quando você configura um Azure AD híbrido, está de fato configurando a integração de um AD local com o Azure AD usando o Azure AD Connect e o ADFS (Active Directory Federated Services). Com uma configuração bem-sucedida, seus funcionários podem entrar sem problemas em sistemas externos usando as credenciais do AD local.

> [!IMPORTANT]  
> Este tutorial fornece detalhes sobre um processo básico para configurar um Azure AD híbrido para um domínio gerenciado. Recomendamos que a familiaridade prévia com o processo e não depender deste tutorial como guia para compreender e implantar o Azure AD híbrido.
>
> Para saber mais sobre o Azure AD híbrido, comece com os seguintes artigos na documentação do Azure Active Directory:
> - [Planejar sua implementação de ingresso no Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> -  [Planejar sua implementação de ingresso no Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> -  [Controlar o ingresso do Azure AD híbrido de seus dispositivos](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> -  [Configurar o ingresso no Azure AD híbrido para domínios federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  


### <a name="set-up-azure-ad-connect"></a>Configurar o Azure AD Connect  
O Azure AD híbrido exige a configuração do Azure AD Connect para manter em sincronia as contas de computador em seu AD (Active Directory) local e o objeto de dispositivo no Azure AD.

A partir da versão 1.1.819.0, o Azure AD Connect fornece um assistente para configurar o ingresso no Azure AD híbrido. O uso do assistente simplifica o processo de configuração.  

Para configurar o Azure AD Connect, você precisa de credenciais de um administrador global para seu locatário do Azure AD.  

> [!TIP]  
> O procedimento a seguir não deve ser considerado autoritativo para configuração do Azure AD Connect, mas é fornecido aqui para ajudar a simplificar a configuração de cogerenciamento entre o Intune e o Configuration Manager. Para conferir o conteúdo autoritativo sobre isso e os procedimentos relacionados para a configuração do Azure AD, consulte [Configurar ingresso no Azure AD híbrido para domínios gerenciados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) na documentação do Azure AD.  


#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Configurar ingresso no Azure AD híbrido usando o Azure AD Connect

1. Obtenha e instale [a versão mais recente do Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 ou superior).  
2. Inicie o Azure AD Connect e, em seguida, selecione **Configurar**.
3. Na página **Tarefas adicionais**, selecione **Configurar opções do dispositivo** e, em seguida, selecione **Avançar**.
4. Na página **Visão geral**, selecione **Avançar**.
5. Na página **Conectar ao Azure AD**, insira as credenciais de um administrador global para seu locatário do Azure AD.
6. Na página **Opções do dispositivo**, selecione **Configurar ingresso no Azure AD Híbrido** e, em seguida, selecione **Avançar**.
7. Na página **Sistemas operacionais de dispositivos**, selecione os sistemas operacionais usados pelos dispositivos no ambiente do Active Directory e, depois, selecione **Avançar**.  

   Você pode selecionar a opção para dar suporte a dispositivos ingressados em domínio de nível inferior do Windows, mas lembre-se de que o cogerenciamento de dispositivos só tem suporte para Windows 10.
8. Na página **SCP**, para cada floresta local na qual você quer que o Azure AD Connect configure o SCP (ponto de conexão de serviço), execute as seguintes etapas e, em seguida, selecione **Avançar**:  
   1. Selecione a floresta.  
   2. Selecione o serviço de autenticação.  Se você tiver um domínio federado, selecione o servidor do AD FS, a menos que sua organização tenha exclusivamente clientes do Windows 10 e você tenha configurado a sincronização do computador/dispositivo, ou sua organização esteja usando [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Clique em **Adicionar** para inserir as credenciais de administrador corporativo.  
9. Se você tiver um domínio gerenciado, ignore esta etapa.  

   Na página **Configuração de federação**, insira as credenciais do administrador do AD FS e, depois, selecione **Avançar**.
10. Na página **Pronto para configurar**, selecione **Configurar**.
11. Na página **Configuração completa**, selecione **Sair**.

Se você tiver problemas com a conclusão da ingressão do Azure AD híbrido para dispositivos Windows ingressados no domínio, consulte [Solução de problemas de ingressão do Azure AD híbrido para dispositivos atuais Windows](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).


## <a name="configure-client-settings-to-direct-clients-register-with-azure-ad"></a>Definir configurações do cliente para orientar os clientes a registrar usando o Azure AD  
Use as Configurações do Cliente para configurar os clientes do Configuration Manager para registro com o Azure AD.  

1. Abra o **console do Configuration Manager** > **Administração** > **Visão Geral** > **Configurações do Cliente** e edite as **Configurações do Cliente Padrão**.  

2. Selecione **Serviços de Nuvem**.  

3. Na página **Configurações Padrão**, defina **Registrar automaticamente os novos dispositivos ingressados em domínio do Windows 10 com o Azure Active Directory** como **Sim**.  

4. Selecione **OK** para salvar esta configuração.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Configurar o registro automático de dispositivos ao Intune   
Em seguida, definiremos o registro automático de dispositivos com o Intune. Com o registro automático, os dispositivos que você gerencia com o Configuration Manager são registrados automaticamente com o Intune.

O registro automático também permite que os usuários registrem seus dispositivos Windows 10 ao Intune. Os dispositivos são registrados quando um usuário adiciona uma conta de trabalho aos seus dispositivos pessoais, ou quando um dispositivo corporativo é associado ao Azure Active Directory.  

1. Entre no [portal do Azure](https://portal.azure.com/) e selecione **Azure Active Directory** > **Mobilidade (MDM e MAM)**  > **Microsoft Intune**.  

2. Configure o **escopo do usuário MDM**. Especifique um dos seguintes procedimentos para configurar os dispositivos dos usuários gerenciados pelo Microsoft Intune e aceite os padrões para os valores da URL.  

   - **Alguns** - selecione os **Grupos** que podem registrar automaticamente seus dispositivos Windows 10  

   - **Todos** - todos os usuários podem registrar automaticamente seus dispositivos com Windows 10 quando definidos como **Nenhum**, o registro automático de MDM (gerenciamento de dispositivo móvel) está desabilitado

   > [!IMPORTANT]  
   > Se **escopo do usuário MAM** e o registro automático do MDM (**escopo do usuário MDM**) estiverem habilitadas para um grupo, somente MAM será habilitado. Somente MAM (Gerenciamento de Aplicativo Móvel) é adicionado para usuários nesse grupo quando eles ingressam um dispositivo pessoal no local de trabalho. Os dispositivos não são registrados automaticamente no MDM.  

3. Selecione **Salvar** para concluir a configuração do registro automático.  

4. Retorne a **Mobilidade (MDM e MAM)** e selecione **Registro do Microsoft Intune**.  

5. Para o escopo de usuário do MDM, selecione **Todos** e depois **Salvar**.  


## <a name="assign-intune-licenses-to-users"></a>Atribuir licenças do Intune aos usuários   
Uma ação frequentemente negligenciada, porém, crítica, é atribuir uma licença do Intune a cada usuário que usará um dispositivo cogerenciado.  

Para atribuir licenças a grupos de usuários, use o Azure Active Directory.  

1. Entre no [portal do Azure](https://portal.azure.com/) com uma conta de Administrador. Para gerenciar licenças, a conta deve ter uma função Administrador global ou administrador da conta do usuário.  

2. Selecione **Todos os serviços** no painel de navegação esquerdo e selecione **Azure Active Directory**.  

3. No painel **Azure Active Directory**, selecione **Licenças** para abrir um painel no qual é possível ver e gerenciar todos os produtos licenciáveis no locatário.  

4. Em **Todos os produtos**, selecione a sua opção de produto que inclui a licença do Intune e selecione **Atribuir** na parte superior do painel.  

   Por exemplo, você pode selecionar **Enterprise Mobility + Security E5**, se é como você obtém o Intune.  

5. No painel **Atribuir licença**, clique em **Usuários e grupos** para abrir o painel **Usuários e grupos**. Selecione os grupos e usuários individuais a quem deseja atribuir uma licença.  Em seguida, clique em **Selecionar** na parte inferior do painel para confirmar a seleção.  

6. No painel **Atribuir licença**, clique em **Opções de atribuição** para exibir todos os planos de serviço incluídos no produto selecionado anteriormente. Se você tiver selecionado um único produto, como o Intune, somente esse produto será mostrado.  
   - Defina **Microsoft Intune** como **Ativado**.  
   - Atribua a cada usuário uma licença para o **Azure Active Directory Premium**.  

   Quando as licenças aplicáveis forem atribuídas, selecione **OK**.  

7. Para concluir a atribuição, no painel **Atribuir licença**, clique em **Atribuir** na parte inferior do painel.

8. Uma notificação é exibida no canto superior direito que mostra o status e o resultado do processo. Se a atribuição ao grupo não puder ser concluída (por exemplo, devido a licenças preexistentes no grupo), clique na notificação para ver os detalhes da falha.

Para saber mais sobre como atribuir licenças do Intune aos usuários, confira [Atribuir licenças](https://docs.microsoft.com/intune/licenses-assign).


## <a name="enable-co-management-in-configuration-manager"></a>Habilitar o cogerenciamento no Configuration Manager
Com o Azure AD híbrido configurado, as configurações de cliente do Configuration Manager em vigor, e as licenças de produto atribuídas a usuários, você está pronto para mudar a opção e habilitar o cogerenciamento de seus dispositivos Windows 10.  

> [!TIP]  
>  Na etapa seis do procedimento a seguir, você atribuirá uma coleção como uma *Grupo piloto* para o cogerenciamento. Esse é um grupo que contém um número pequeno de clientes para testar as suas configurações de cogerenciamento. É recomendável criar uma coleção adequada antes de iniciar o procedimento. Em seguida, você pode selecionar essa coleção sem sair do procedimento para isso.  

1. No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Cogerenciamento**.

2. Na guia Início, no grupo Gerenciar, selecione **Configurar cogerenciamento** para abrir o Assistente para Configuração de Cogerenciamento.

3. Na página Assinatura, selecione **Entrar**, entre no seu locatário do Intune e selecione **Avançar**.

4. Na página Habilitação, na lista suspensa *Registro automático no Intune*, selecione uma das seguintes opções:  

   - **Piloto**  -  *(recomendado)* membros da coleção que você especifica são automaticamente inscritos no Intune e podem ser cogerenciados. Especifique a coleção piloto na página *Preparo* desse assistente. Essa opção permite testar o cogerenciamento em um subconjunto de clientes. Em seguida, você pode distribuir o cogerenciamento para clientes adicionais usando uma abordagem em fases.  

   - **Todos** – o cogerenciamento é habilitado para todos os clientes.  

5. Na página Cargas de Trabalho, é possível alternar cargas de trabalho no **Configuration Manager** para uma das seguintes e, quando estiver pronto para continuar, selecionar **Avançar**.  

   - **Piloto Intune** - alterna uma carga de trabalho apenas para os dispositivos no grupo Piloto. Você atribuirá uma coleção como o grupo Piloto na próxima página do assistente.  

   - **Intune** - alterna a carga de trabalho associada para todos os dispositivos Windows 10 cogerenciados.  

   Não é necessário alternar quaisquer cargas de trabalho no momento em que você habilita o cogerenciamento. É possível revisitar essa configuração no console do Configuration Manager posteriormente, depois que o cogerenciamento é configurado.  

   Antes de alternar uma carga de trabalho, certifique-se de que a carga de trabalho correspondente no Intune esteja configurada e implantada. Fazer isso mantém as cargas de trabalho gerenciadas.  

6. Na página Preparo, especifique uma coleção a ser usada para a **Coleção Piloto** e clique em **Avançar**. A coleção que você especifica é usada como parte da distribuição em fases do cogerenciamento. Você pode alterar as coleções no grupo piloto a qualquer momento por meio das propriedades de cogerenciamento.  

7. Na página Resumo, selecione **Avançar** e, em seguida, **Fechar** para concluir o Assistente.  


## <a name="next-steps"></a>Próximas etapas
- Verificar o status de dispositivos cogerenciados com o [painel de cogerenciamento](/sccm/comanage/how-to-monitor)
- Começar a obter o [valor imediato](quickstarts.md#immediate-value) do cogerenciamento
- Usar o [acesso condicional](quickstart-conditional-access.md) e regras de conformidade do Intune para gerenciar o acesso do usuário aos recursos corporativos
