---
title: Mudar as cargas de trabalho do Configuration Manager para o Intune
titleSuffix: Configuration Manager
description: Saiba como mudar as cargas de trabalho que no momento são gerenciadas pelo Configuration Manager para serem gerenciadas pelo Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/10/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: e3bd3bfda92fb877bac3ca68dbecf8b4a4078d4d
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416938"
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Mudar as cargas de trabalho do Configuration Manager para o Intune

Depois que você [preparar os dispositivos Windows 10 para cogerenciamento](/sccm/core/clients/manage/co-management-prepare), a próxima etapa será habilitar o registro automático do cliente no Intune. Em seguida, quando estiver pronto, comece a mudar cargas de trabalho específicas do Configuration Manager para o Intune. 


## <a name="setup-co-management"></a>Cogerenciamento da instalação

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e escolha o nó **Cogerenciamento**.  

2. Na guia **Página Inicial** da faixa de opções, no grupo **Gerenciar**, escolha **Configurar cogerenciamento**. Essa ação abre o Assistente de configuração de cogerenciamento.  

3. Na página de Assinatura, selecione **Entrar**. Entre no locatário do Intune e, em seguida, selecione **Avançar**.  

4. Na página Habilitação, escolha **Piloto** ou **Tudo**.  

    Essa ação habilita o registro automático do cliente no Intune. Quando você escolhe **Piloto**, somente os clientes do Configuration Manager que são membros da coleção piloto são registrados automaticamente no Intune. Com essa opção, você pode habilitar o cogerenciamento em um subconjunto de clientes para testar inicialmente o cogerenciamento e distribuí-lo usando uma abordagem em fases.  

    Use a linha de comando exibida para implantar o cliente do Configuration Manager como um aplicativo no Intune para dispositivos já registrados no Intune. Para saber mais, confira [Dispositivos Windows 10 registrados no Intune](/sccm/core/clients/manage/co-management-prepare#windows-10-devices-enrolled-in-intune).  

5. Na página Cargas de trabalho, escolha se deseja mudar as cargas de trabalho do Configuration Manager para serem gerenciadas pelo Intune. É possível habilitar o registro na página anterior sem alternar as cargas de trabalho no momento. 

    A configuração **Intune Piloto** muda a carga de trabalho associada apenas dos dispositivos da coleção piloto. A configuração **Intune** muda a carga de trabalho associada de todos os dispositivos Windows 10 cogerenciados.  

    > [!Important] 
    > Antes de mudar quaisquer cargas de trabalho, não se esqueça de configurar e implantar corretamente a carga de trabalho correspondente no Intune. As cargas de trabalho sempre devem ser gerenciadas por uma das ferramentas de gerenciamento dos dispositivos.  

6. Na página Preparo, defina as seguintes configurações:  

    - **Piloto**: o grupo piloto contém uma ou mais coleções que você seleciona. Use esse grupo como parte de sua distribuição em fases do cogerenciamento. Comece com uma coleção de teste pequena e, em seguida, adicione mais coleções ao grupo piloto à medida que você distribui o cogerenciamento para mais usuários e dispositivos. É possível alterar as coleções no grupo piloto a qualquer momento.  

    - **Produção**: Configure o **Grupo de exclusão** com uma ou mais coleções. Os dispositivos que são membros de uma das coleções neste grupo são excluídos do uso do cogerenciamento.  

7. Para habilitar o cogerenciamento, conclua o assistente.  

<!--1357377--> Começando no Configuration Manager versão 1806, quando você muda uma carga de trabalho de cogerenciamento, os dispositivos cogerenciados sincronizam automaticamente a política de MDM do Microsoft Intune. Essa sincronização também acontece quando você inicia a ação **Baixar Política do Computador** nas notificações do cliente no console do Configuration Manager. Para obter mais informações, confira [Iniciar recuperação de política do cliente usando a notificação do cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



## <a name="modify-your-co-management-settings"></a>Modificar as configurações de cogerenciamento

Depois de habilitar o cogerenciamento usando o assistente, modifique as configurações nas propriedades de cogerenciamento. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e escolha o nó **Cogerenciamento**. Selecione o objeto de cogerenciamento e, em seguida, selecione **Propriedades** na faixa de opções. 



## <a name="supported-workloads"></a>Cargas de trabalho com suporte

No momento, as cargas de trabalho estão disponíveis para você mudar do Configuration Manager para o Intune:

- **Políticas de conformidade do dispositivo**  

- **Políticas de acesso a recursos**: Para saber mais sobre essas políticas do Intune, confira [Deploy resource access profiles](https://docs.microsoft.com/intune/device-profiles) (Implantar perfis de acesso a recursos).
    - Perfil de email  
    - Perfil de Wi-Fi  
    - Perfil da VPN  
    - Perfil de certificado  

- **Políticas do Windows Update**  

- **Endpoint Protection**: Começando no Configuration Manager versão 1802, essa carga de trabalho inclui os seguintes recursos:  
    - Windows Defender Application Guard  
    - Windows Defender Firewall  
    - Windows Defender SmartScreen  
    - Criptografia do Windows  
    - Windows Defender Exploit Guard  
    - Controle de Aplicativos do Windows Defender  
    - Central de Segurança do Windows Defender  
    - Proteção Avançada contra Ameaças do Windows Defender  
    - Windows Information Protection  

- **Configuração do dispositivo**: começando no Configuration Manager versão 1806<!--1357903-->:  

    - A movimentação da carga de trabalho de configuração do dispositivo também move as cargas de trabalho **Acesso de Recurso** e **Endpoint Protection**  

    - Ainda é possível implantar as configurações do Configuration Manager em dispositivos cogerenciados mesmo que o Intune seja a autoridade de configuração do dispositivo. Essa exceção pode ser usada para definir configurações exigidas pela sua organização, mas ainda não disponíveis no Intune. Especifique essa exceção em uma [linha de base de configuração do Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Ative a opção para **Sempre aplicar essa linha de base, mesmo para clientes cogerenciados**  ao criar a linha de base, ou na guia **Geral** das propriedades de uma linha de base existente.  

- **Aplicativos Clique para Executar do Office 365**: começando no Configuration Manager versão 1806<!--1357841-->:  

    - Depois de mover a carga de trabalho, o aplicativo será exibido no **Portal da Empresa** no dispositivo  

    - As atualizações do Office podem levar cerca de 24 horas para aparecer no cliente, a menos que os dispositivos sejam reiniciados  

    - Há uma nova condição global, **Os aplicativos do Office 365 são gerenciados pelo Intune no dispositivo**. Essa condição é adicionada por padrão como um requisito dos novos aplicativos do Office 365. Ao fazer a transição dessa carga de trabalho, os clientes cogerenciados deixam de atender aos requisitos do aplicativo. Eles não instalam o Office 365 implantado por meio do Configuration Manager.  

- **Aplicativos cliente**: Começando no Configuration Manager versão 1806 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features))<!--1357892-->:  

    - Após a transição dessa carga de trabalho, todos os aplicativos disponíveis implantados do Intune estão disponíveis no Portal da Empresa  

    - Os aplicativos que você implanta do Configuration Manager estão disponíveis no Centro de Software  



## <a name="monitor-co-management"></a>Monitorar o cogerenciamento

Depois de habilitar o cogerenciamento, monitore dispositivos de cogerenciamento usando os seguintes métodos:

- [Painel de cogerenciamento](/sccm/core/clients/manage/co-management-dashboard)  

- **Exibição SQL e classe WMI**: consulte a exibição SQL **v_ClientCoManagementState** no banco de dados do site do Configuration Manager ou a classe WMI **SMS_Client_ComanagementState**. Com as informações na classe WMI, você pode criar coleções personalizadas no Configuration Manager para ajudar a determinar o status da implantação do cogerenciamento. Para obter detalhes, consulte [Como criar coleções](/sccm/core/clients/manage/collections/create-collections). Os campos a seguir estão disponíveis na exibição SQL e na classe WMI:  
  - **MachineId**: especifica uma ID de dispositivo exclusiva do cliente do Configuration Manager  
  - **MDMEnrolled**: especifica se o dispositivo é registrado no MDM  
  - **Authority**: especifica a autoridade para a qual o dispositivo está registrado  
  - **ComgmtPolicyPresent**: especifica se a política de cogerenciamento do Configuration Manager existe no cliente. Se o valor de **MDMEnrolled** for **0**, o dispositivo não será cogerenciado independentemente da existência da política de cogerenciamento no cliente.  

    > [!Note]  
    > Um dispositivo é cogerenciado quando os campos **MDMEnrolled** e **ComgmtPolicyPresent** têm o valor **1**.  

- **Políticas de implantação**: duas políticas são criadas no nó **Implantações** do workspace **Monitoramento**. Uma política para o grupo piloto e outra para produção. Essas políticas relatam somente o número de dispositivos nos quais o Configuration Manager aplicou a política. Elas não consideram quantos dispositivos estão registrados no Intune, o que é um requisito para que os dispositivos possam ser cogerenciados.  



## <a name="check-compliance-for-co-managed-devices"></a>Verificar a conformidade de dispositivos cogerenciados

Os usuários podem usar o Centro de Software para verificar a conformidade de seus dispositivos Windows 10 cogerenciados independentemente se o acesso condicional é gerenciado pelo Configuration Manager ou pelo Intune. Os usuários também podem verificar a conformidade usando o aplicativo Portal da Empresa quando o acesso condicional é gerenciado pelo Intune.



## <a name="next-steps"></a>Próximas etapas

Use os seguintes recursos para ajudá-lo a gerenciar as cargas de trabalho passadas para o Intune:
- [Políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Políticas de acesso a recursos](https://docs.microsoft.com/intune/device-profiles)
- [Políticas do Windows Update para Empresas](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Endpoint Protection para Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
