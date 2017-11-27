---
title: Mudar as cargas de trabalho do Configuration Manager para o Intune
description: "Saiba como mudar as cargas de trabalho que no momento são gerenciadas pelo Configuration Manager para serem gerenciadas pelo Microsoft Intune."
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 60aff996ec598cff7572a0e88c631dc9c509e007
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Mudar as cargas de trabalho do Configuration Manager para o Intune
Em [Preparar dispositivos Windows 10 para cogerenciamento](co-management-prepare.md), você preparou dispositivos Windows 10 para o cogerenciamento. Agora, esses dispositivos ingressaram no AD e no Azure AD, e estão registrados no Intune e têm o cliente do Configuration Manager. Provavelmente ainda há dispositivos Windows 10 que ingressaram no AD e têm o cliente do Configuration Manager, mas que não ingressaram no Azure AD e não estão registrados no Intune. O procedimento a seguir fornece as etapas para habilitar o cogerenciamento e preparar o restante dos dispositivos Windows 10 (clientes do Configuration Manager sem registro no Intune) para o cogerenciamento e permite que você comece a mudar cargas de trabalho do Configuration Manager específicas para o Intune.

1. No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Cogerenciamento**.    
2. Na guia Início, no grupo Gerenciar, escolha  **Configurar cogerenciamento** para abrir o Assistente para Configuração de Cogerenciamento.    
3. Na página Assinatura, clique em **Entrar**, entre no seu locatário do Intune e, em seguida, clique em **Avançar**.   
4. Na página Habilitação, escolha **Piloto** ou **Todos** para habilitar o Registro automático do Intune e, em seguida, clique em **Avançar**. Quando você escolhe **Piloto**, somente os clientes do Configuration Manager que são membros do grupo piloto são registrados automaticamente no Intune. Isso permite que você habilite o cogerenciamento em um subconjunto de clientes para testá-lo inicialmente e distribuí-lo usando uma abordagem em fases. A linha de comando pode ser usada para implantar o cliente do Configuration Manager como um aplicativo no Intune para dispositivos já registrados no Intune. Para obter detalhes, consulte [Dispositivos Windows 10 registrados no Intune](co-management-prepare.md#windows-10-devices-enrolled-in-intune).
5. Na página Cargas de trabalho, escolha se deseja mudar as cargas de trabalho do Configuration Manager para serem gerenciadas pelo Intune Piloto ou pelo Intune e, em seguida, clique em **Avançar**. A configuração **Intune Piloto** muda a carga de trabalho associada apenas dos dispositivos do grupo piloto. A configuração **Intune** muda a carga de trabalho associada de todos os dispositivos Windows 10 cogerenciados. 
        
   > [!Important]    
   > Antes de mudar qualquer carga de trabalho, verifique se a carga de trabalho correspondente no Intune foi configurada e implantada corretamente. Isso garante que as cargas de trabalho sempre sejam gerenciadas por uma das ferramentas de gerenciamento de seus dispositivos.   
1. Na página Preparo, defina as seguintes configurações e, em seguida, clique em **Avançar**:
    - **Piloto**: o grupo piloto contém uma ou mais coleções que você seleciona. Use esse grupo como parte de sua distribuição em fases do cogerenciamento. É possível começar com uma coleção de teste pequena e, em seguida, adicionar mais coleções ao grupo piloto à medida que você distribui o cogerenciamento para mais usuários e dispositivos. Você pode alterar as coleções no grupo piloto a qualquer momento por meio das propriedades de cogerenciamento.
    - **Produção**: configurar o **Grupo de exclusão** com uma ou mais coleções. Os dispositivos que são membros de uma das coleções neste grupo são excluídos do uso do cogerenciamento. 
2. Para habilitar o cogerenciamento, conclua o assistente.  

## <a name="modify-your-co-management-settings"></a>Modificar as configurações de cogerenciamento
Depois de habilitar o cogerenciamento usando o assistente, você poderá modificar as configurações nas propriedades de cogerenciamento.  
- No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Cogerenciamento**.  
Selecione o objeto de cogerenciamento e, em seguida, na guia Início, clique em **Propriedades**. 

## <a name="monitor-co-management"></a>Monitorar o cogerenciamento
Depois de habilitar o cogerenciamento, você poderá monitorar dispositivos de cogerenciamento usando os seguintes métodos:
- **Exibição SQL e classe WMI**: você pode consultar a exibição SQL **v&#95;ClientCoManagementState** no banco de dados do site do Configuration Manager ou a classe WMI **SMS&#95;Client&#95;ComanagementState**. Com as informações na classe WMI, você pode criar coleções personalizadas no Configuration Manager para ajudar a determinar o status da implantação do cogerenciamento. Para obter detalhes, consulte [Como criar coleções](/sccm/core/clients/manage/collections/create-collections). Os campos a seguir estão disponíveis na exibição SQL e na classe WMI: 
    - **MachineId**: especifica uma ID de dispositivo exclusiva do cliente do Configuration Manager.
    - **MDMEnrolled**: especifica se o dispositivo é registrado no MDM. 
    - **Authority**: especifica a autoridade para a qual o dispositivo está registrado.
    - **ComgmtPolicyPresent**: especifica se a política de cogerenciamento do Configuration Manager existe no cliente. Se o valor de **MDMEnrolled** for **0**, o dispositivo não será cogerenciado independentemente da existência da política de cogerenciamento no cliente.

   > [!Note]    
   > Um dispositivo é cogerenciado quando os campos **MDMEnrolled** e **ComgmtPolicyPresent** têm o valor **1**.

- **Políticas de implantação**: existem duas políticas criadas em **Monitoramento** > **Implantações**, uma política para o grupo piloto e outra para produção. Essas políticas somente relatam o número de dispositivos nos quais o Configuration Manager aplicou a política. Elas não consideram quantos dispositivos estão registrados no Intune, que é um requisito para que os dispositivos possam ser cogerenciados.  

## <a name="check-compliance-for-co-managed-devices"></a>Verificar a conformidade de dispositivos cogerenciados
Os usuários podem usar o Centro de Software para verificar a conformidade de seus dispositivos Windows 10 cogerenciados independentemente se o acesso condicional é gerenciado pelo Configuration Manager ou pelo Intune. Os usuários também podem verificar a conformidade usando o aplicativo Portal da Empresa quando o acesso condicional é gerenciado pelo Intune.

## <a name="next-steps"></a>Próximas etapas
Use os seguintes recursos para ajudá-lo a gerenciar as cargas de trabalho passadas para o Intune:
- [Políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Políticas de acesso a recursos](https://docs.microsoft.com/intune/device-profiles)
- [Políticas do Windows Update para Empresas](https://docs.microsoft.com/intune/windows-update-for-business-configure)
