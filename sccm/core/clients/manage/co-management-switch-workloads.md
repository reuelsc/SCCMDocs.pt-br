---
title: Mudar as cargas de trabalho do Configuration Manager para o Intune
titleSuffix: Configuraton Manager
description: Saiba como mudar as cargas de trabalho que no momento são gerenciadas pelo Configuration Manager para serem gerenciadas pelo Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: c1f5f96c4178068ced727cfe96b1c6fe8b60a0fc
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383992"
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Mudar as cargas de trabalho do Configuration Manager para o Intune
Em [Preparar dispositivos Windows 10 para cogerenciamento](co-management-prepare.md), você preparou dispositivos Windows 10 para o cogerenciamento. Esses dispositivos ingressaram no Azure AD, são registrados no Intune e têm o cliente do Configuration Manager. Provavelmente ainda há dispositivos Windows 10 que ingressaram no AD e têm o cliente do Configuration Manager, mas que não ingressaram no Azure AD e não estão registrados no Intune. O procedimento a seguir fornece as etapas para habilitar o cogerenciamento e preparar o restante dos dispositivos Windows 10 (clientes do Configuration Manager sem registro no Intune) para o cogerenciamento e permite que você comece a mudar cargas de trabalho do Configuration Manager específicas para o Intune.


## <a name="switch-configuration-manager-workloads-to-intune"></a>Mudar as cargas de trabalho do Configuration Manager para o Intune

1. No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Cogerenciamento**.    
2. Na guia Início, no grupo Gerenciar, escolha  **Configurar cogerenciamento** para abrir o Assistente para Configuração de Cogerenciamento.    
3. Na página Assinatura, clique em **Entrar**, entre no seu locatário do Intune e, em seguida, clique em **Avançar**.   
4. Na página Habilitação, escolha **Piloto** ou **Todos** para habilitar o Registro automático do Intune e, em seguida, clique em **Avançar**. Quando você escolhe **Piloto**, somente os clientes do Configuration Manager que são membros do grupo piloto são registrados automaticamente no Intune. Com essa opção, você pode habilitar o cogerenciamento em um subconjunto de clientes para testar inicialmente o cogerenciamento e distribuí-lo usando uma abordagem em fases. A linha de comando pode ser usada para implantar o cliente do Configuration Manager como um aplicativo no Intune para dispositivos já registrados no Intune. Para obter detalhes, consulte [Dispositivos Windows 10 registrados no Intune](co-management-prepare.md#windows-10-devices-enrolled-in-intune).
5. Na página Cargas de trabalho, escolha se deseja mudar as cargas de trabalho do Configuration Manager para serem gerenciadas pelo Intune Piloto ou pelo Intune e, em seguida, clique em **Avançar**. A configuração **Intune Piloto** muda a carga de trabalho associada apenas dos dispositivos do grupo piloto. A configuração **Intune** muda a carga de trabalho associada de todos os dispositivos Windows 10 cogerenciados. 
        
   > [!Important]    
   > Antes de mudar qualquer carga de trabalho, verifique se a carga de trabalho correspondente no Intune foi configurada e implantada corretamente. Isso garante que as cargas de trabalho sempre sejam gerenciadas por uma das ferramentas de gerenciamento dos dispositivos.   
1. Na página Preparo, defina as seguintes configurações e, em seguida, clique em **Avançar**:
    - **Piloto**: o grupo piloto contém uma ou mais coleções que você seleciona. Use esse grupo como parte de sua distribuição em fases do cogerenciamento. É possível começar com uma coleção de teste pequena e, em seguida, adicionar mais coleções ao grupo piloto à medida que você distribui o cogerenciamento para mais usuários e dispositivos. Você pode alterar as coleções no grupo piloto a qualquer momento por meio das propriedades de cogerenciamento.
    - **Produção**: configurar o **Grupo de exclusão** com uma ou mais coleções. Os dispositivos que são membros de uma das coleções neste grupo são excluídos do uso do cogerenciamento. 
2. Para habilitar o cogerenciamento, conclua o assistente.  

<!--1357377--> Começando no Configuration Manager versão 1806, quando você muda uma carga de trabalho de cogerenciamento, os dispositivos cogerenciados sincronizam automaticamente a política de MDM do Microsoft Intune. Essa sincronização também acontece quando você inicia a ação **Baixar Política do Computador** nas Notificações do Cliente no console do Configuration Manager. Para obter mais informações, confira [Iniciar recuperação de política do cliente usando a notificação do cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).

## <a name="modify-your-co-management-settings"></a>Modificar as configurações de cogerenciamento
Depois de habilitar o cogerenciamento usando o assistente, você poderá modificar as configurações nas propriedades de cogerenciamento.  
- No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Cogerenciamento**.  
Selecione o objeto de cogerenciamento e, em seguida, na guia Início, clique em **Propriedades**. 

## <a name="workloads-able-to-be-transitioned-to-intune"></a>As cargas de trabalho podem ser transferidas para o Intune
Algumas cargas de trabalho estão disponíveis para serem transferidas para o Intune. A seguinte lista será atualizada conforme as cargas de trabalho ficarem disponíveis para a transição:
1. Políticas de conformidade do dispositivo
2. Políticas de acesso a recursos: as políticas de acesso a recursos definem as configurações de VPN, Wi-Fi, email e certificado nos dispositivos. Para saber mais, confira [Implantar perfis de acesso a recursos](https://docs.microsoft.com/intune/device-profiles).
      - Perfil de email
      - Perfil de Wi-Fi
      - Perfil da VPN
      - Perfil de certificado
3. Políticas do Windows Update
4. Endpoint Protection (a partir do Configuration Manager versão 1802)
      - Windows Defender Application Guard
      - Windows Defender Firewall
      - Windows Defender SmartScreen
      - Criptografia do Windows
      - Windows Defender Exploit Guard
      - Controle de Aplicativos do Windows Defender
      - Central de Segurança do Windows Defender
      - Proteção Avançada contra Ameaças do Windows Defender
      - Windows Information Protection

5. Configuração do dispositivo (começando no Configuration Manager versão 1806) <!--1357903-->
       - Começando na versão 1806, a movimentação da carga de trabalho de configuração do dispositivo também move as cargas de trabalho **Acesso de Recurso** e **Endpoint Protection**.
       - Começando na versão 1806, ainda é possível implantar as configurações do Configuration Manager em dispositivos cogerenciados mesmo que o Intune seja a autoridade de configuração do dispositivo. Essa exceção pode ser usada para definir configurações exigidas pela sua organização, mas ainda não disponíveis no Intune. Especifique essa exceção em uma [linha de base de configuração do Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines.md). Ative a opção para **Sempre aplicar essa linha de base, mesmo para clientes cogerenciados**  ao criar a linha de base, ou na guia **Geral** das propriedades de uma linha de base existente.
6. Aplicativos Clique para Executar do Office 365 (começando no Configuration Manager versão 1806) <!--1357841-->
       - Depois de mover a carga de trabalho, o aplicativo aparece no **Portal da Empresa** no dispositivo.
       - As atualizações do Office podem levar cerca de 24 horas para aparecer no cliente, a menos que os dispositivos sejam reiniciados. 
       - Há uma nova condição global **Os aplicativos do Office 365 são gerenciados pelo Intune no dispositivo**. Essa condição é adicionada por padrão como um requisito dos novos aplicativos do Office 365. Ao fazer a transição dessa carga de trabalho, os clientes cogerenciados deixam de atender aos requisitos do aplicativo, portanto, não instalam o Office 365 implantado por meio do Configuration Manager.
7. Aplicativos móveis (começando no Configuration Manager versão 1806 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features)) <!--1357892-->
      - Após a transição dessa carga de trabalho, todos os aplicativos disponíveis implantados do Intune estão disponíveis no Portal da Empresa. 
      -  Os aplicativos que você implanta do Configuration Manager estão disponíveis no Centro de Software.

## <a name="monitor-co-management"></a>Monitorar o cogerenciamento
Depois de habilitar o cogerenciamento, você poderá monitorar dispositivos de cogerenciamento usando os seguintes métodos:

- [Painel de cogerenciamento](/sccm/core/clients/manage/co-management-dashboard)
- **Exibição SQL e classe WMI**: você pode consultar a exibição SQL **v&#95;ClientCoManagementState** no banco de dados do site do Configuration Manager ou a classe WMI **SMS&#95;Client&#95;ComanagementState**. Com as informações na classe WMI, você pode criar coleções personalizadas no Configuration Manager para ajudar a determinar o status da implantação do cogerenciamento. Para obter detalhes, consulte [Como criar coleções](/sccm/core/clients/manage/collections/create-collections). Os campos a seguir estão disponíveis na exibição SQL e na classe WMI: 
    - **MachineId**: especifica uma ID de dispositivo exclusiva do cliente do Configuration Manager.
    - **MDMEnrolled**: especifica se o dispositivo é registrado no MDM. 
    - **Authority**: especifica a autoridade para a qual o dispositivo está registrado.
    - **ComgmtPolicyPresent**: especifica se a política de cogerenciamento do Configuration Manager existe no cliente. Se o valor de **MDMEnrolled** for **0**, o dispositivo não é cogerenciado independentemente da existência da política de cogerenciamento no cliente.

   > [!Note]    
   > Um dispositivo é cogerenciado quando os campos **MDMEnrolled** e **ComgmtPolicyPresent** têm o valor **1**.

- **Políticas de implantação**: duas políticas são criadas em **Monitoramento** > **Implantações**, uma para o grupo piloto e outra para produção. Essas políticas relatam somente o número de dispositivos nos quais o Configuration Manager aplicou a política. Elas não consideram quantos dispositivos estão registrados no Intune, o que é um requisito para que os dispositivos possam ser cogerenciados.  

## <a name="check-compliance-for-co-managed-devices"></a>Verificar a conformidade de dispositivos cogerenciados
Os usuários podem usar o Centro de Software para verificar a conformidade de seus dispositivos Windows 10 cogerenciados independentemente se o acesso condicional é gerenciado pelo Configuration Manager ou pelo Intune. Os usuários também podem verificar a conformidade usando o aplicativo Portal da Empresa quando o acesso condicional é gerenciado pelo Intune.

## <a name="next-steps"></a>Próximas etapas
Use os seguintes recursos para ajudá-lo a gerenciar as cargas de trabalho passadas para o Intune:
- [Políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Políticas de acesso a recursos](https://docs.microsoft.com/intune/device-profiles)
- [Políticas do Windows Update para Empresas](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Endpoint Protection para Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
