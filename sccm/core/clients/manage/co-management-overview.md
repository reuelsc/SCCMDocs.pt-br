---
title: Cogerenciamento para dispositivos Windows 10
titleSuffix: Configuration Manager
description: Saiba como gerenciar dispositivos Windows 10 simultaneamente usando o Configuration Manager e o Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 6434ba443cb884c7fbb5d727c5db3c80d2d88aad
ms.sourcegitcommit: 12b71da551350c99c5916df3629e33e31040db15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2018
ms.locfileid: "53530924"
---
# <a name="co-management-for-windows-10-devices"></a>Cogerenciamento para dispositivos Windows 10    

Com atualizações anteriores do Windows 10, você pode associar um dispositivo com Windows 10 ao Active Directory (AD) local e ao Azure AD baseado em nuvem ao mesmo tempo (Azure AD híbrido). Do Configuration Manager versão 1710 em diante, o cogerenciamento aproveita essa melhoria. Ele permite gerenciar dispositivos Windows 10 versão 1709 simultaneamente usando o Configuration Manager e o Intune. <!-- 1350871 -->


## <a name="why-co-management"></a>Por que cogerenciamento?

Muitos clientes desejam gerenciar os dispositivos Windows 10 da mesma forma em que gerenciam os dispositivos móveis, usando uma solução baseada em nuvem simplificada e com menor custo. No entanto, fazer a transição do gerenciamento tradicional para o gerenciamento moderno pode ser um desafio.  


## <a name="what-is-co-management"></a>O que é cogerenciamento?

O cogerenciamento permite gerenciar dispositivos Windows 10 simultaneamente usando o Configuration Manager e o Intune. É uma solução que fornece uma ponte do gerenciamento tradicional para o moderno e fornece um caminho para fazer a transição usando uma abordagem em fases.


## <a name="benefits"></a>Benefícios 

Uso imediato dos seguintes recursos do Intune:  
 
- Ações remotas
    - [Redefinição de fábrica](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
    - [Apagamento seletivo](https://docs.microsoft.com/intune/apps-selective-wipe)
    - [Excluir dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
    - [Reiniciar dispositivo](https://docs.microsoft.com/intune/device-restart)
    - [Novo início](https://docs.microsoft.com/intune/device-fresh-start)  

- Orquestração com o Intune para as seguintes cargas de trabalho:
    - [Políticas de conformidade](https://docs.microsoft.com/intune/device-compliance-get-started)
    - [Políticas de acesso a recursos](https://docs.microsoft.com/intune/device-profiles)
    - [Políticas do Windows Update](https://docs.microsoft.com/intune/windows-update-for-business-configure)
    - [Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10), a partir do Configuration Manager 1802. <!-- 1357365 -->
    - [Configuração do dispositivo](https://docs.microsoft.com/intune/device-profile-create), do Configuration Manager 1806 em diante. <!-- 1357903 -->
    - [Aplicativos Clique para Executar do Office](https://docs.microsoft.com/intune/apps-add-office365), do Configuration Manager 1806 <!--1357841--> em diante
    - [Aplicativos móveis](https://docs.microsoft.com/intune/app-management), do Configuration Manager 1806 em diante como um recurso de pré-lançamento. <!--1357892-->



## <a name="how-to-configure-co-management"></a>Como configurar o cogerenciamento

 Há dois caminhos principais para usar o cogerenciamento:  

   - O Configuration Manager provisiona cogerenciamento: Você registra no Intune seus dispositivos Windows 10 ingressados no Azure AD que já são clientes do Configuration Manager.  

   - Provisionados pelo Intune: Para dispositivos que já estão registrados no Intune, você instala o cliente do Configuration Manager para atingir um estado de cogerenciamento. 


### <a name="configuration-manager"></a>Gerenciador de Configurações

 -  Atualize para o Configuration Manager versão 1710 ou posterior.


### <a name="azure-active-directory"></a>Azure Active Directory

 - Dispositivos Windows 10 devem ser associados ao Azure AD. Eles podem ser de qualquer um dos seguintes tipos:  

     - [Ingressado no Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), em que o dispositivo ingressa no seu Active Directory local e é registrado com seu Azure Active Directory.

     - Somente [ingressado no Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan). (Esse tipo é às vezes chamado de "ingressado em domínio de nuvem")<!--SCCMDocs issue 605-->

 - [Habilitar o registro automático no Windows 10](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="intune"></a>Intune

- [Como configurar a assinatura do Intune](/sccm/mdm/deploy-use/configure-intune-subscription) ou [Configurar o Intune](/intune/setup-steps)  

- [Iniciar a migração do MDM híbrido para o Intune autônomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

  > [!Note]  
  > Se você tiver um ambiente de MDM híbrido (Intune integrado ao Configuration Manager), não será possível habilitar o cogerenciamento. No entanto, você pode iniciar a migração de usuários para o Intune autônomo e, em seguida, habilitar seus dispositivos Windows 10 associados para cogerenciamento. Para obter mais informações sobre como migrar para o Intune autônomo, consulte [Iniciar a migração do MDM híbrido para o Intune autônomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  


### <a name="enable-co-management"></a>Habilitar cogerenciamento 

 > [!Important]  
 > Iniciando na versão 1802, para habilitar o cogerenciamento, sua conta de usuário administrativo no Configuration Manager deverá ser um **Administrador Completo** com **Todos** os escopos de segurança. Para obter mais informações, veja [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).<!--SCCMDoc issue 626-->  

 No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e escolha o nó **Cogerenciamento**. Clique em **Configurar cogerenciamento** na faixa de opções para abrir o **Assistente para Integração de Cogerenciamento**. 
   
1. Na página **Assinatura**, clique em **Entrar**. Entre no seu locatário do Intune e, em seguida, clique em **Avançar**.  

    > [!Tip]   
    > Verifique se a conta usada para entrar no seu locatário tem uma licença do Intune atribuída, caso contrário, ela falhará com a mensagem de erro "Usuário não reconhecido".  

2. Na página **Habilitação**, escolha sua configuração **Registro automático no Intune**. Copie a linha de comando para dispositivos já inscritos no Intune, se necessário.  

    > [!Note]  
    > Começando na versão 1806, o registro automático não é imediato para todos os clientes. Esse comportamento ajuda uma melhor escala do registro para ambientes de grande porte. O Configuration Manager torna o registro aleatório com base no número de clientes. Por exemplo, se o seu ambiente tiver 100 mil clientes, quando você habilitar essa configuração, o registro ocorrerá durante vários dias.<!--1358003-->  

3. Na página **Cargas de Trabalho**, para cada carga de trabalho, escolha qual grupo de dispositivos mover para gerenciamento com o Intune.  

4. Na página **Processo de preparo**, selecione uma coleção de dispositivos para ser a **Coleção piloto**. Verifique o **Resumo** e conclua o assistente.  


### <a name="upgrade-windows-10-client"></a>Atualizar o cliente do Windows 10

- Atualize para o [Windows 10, versão 1709 (também conhecido como a Atualização para Criadores) e posterior](/sccm/osd/deploy-use/manage-windows-as-a-service)


### <a name="configure-workloads-to-switch-to-intune"></a>Configurar cargas de trabalho para mudar para o Intune 

O artigo [Cargas de trabalho que podem ser transferidas para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) mostra como mudar cargas de trabalho específicas do Configuration Manager para o Intune. O artigo também contém instruções sobre como alterar os grupos de dispositivos para os quais as cargas de trabalho são transferidas.

#### <a name="compliance-policies"></a>Políticas de conformidade 
As políticas de conformidade definem as regras e as configurações que um dispositivo deve cumprir para ser considerado em conformidade pelas políticas de acesso condicional. Também use políticas de conformidade para monitorar e corrigir problemas de conformidade com dispositivos independentemente do acesso condicional. Para obter detalhes, consulte [Políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started).  

#### <a name="windows-update-policies"></a>Políticas do Windows Update
As políticas do Windows Update para Empresas permitem configurar políticas de adiamento para atualizações de recursos ou atualizações de qualidade do Windows 10 para dispositivos Windows 10 gerenciados diretamente pelo Windows Update para Empresas. Para obter detalhes, consulte [Configurar as políticas de adiamento do Windows Update for Business](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

#### <a name="resource-access-policies"></a>Políticas de acesso a recursos
As políticas de acesso a recursos definem as configurações de VPN, Wi-Fi, email e certificado nos dispositivos. Para obter detalhes, consulte [Implantar perfis de acesso a recursos](https://docs.microsoft.com/intune/device-profiles).

#### <a name="endpoint-protection"></a>Endpoint Protection
A partir do Configuration Manager 1802, a carga de trabalho do Endpoint Protection pode ser transferida para o Intune. Para saber mais, confira [Endpoint Protection para Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10)<!-- 1357365 --> e [Cargas de trabalho que podem ser transferidas para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).

#### <a name="device-configuration"></a>Configuração do dispositivo
Do Configuration Manager 1806 em diante, a carga de trabalho de configuração do dispositivo pode ser transferida para o Intune. Para obter mais informações, veja [Criar um perfil de dispositivo no Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create) e [Cargas de trabalho podem ser transferidas para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).  <!--1357903-->

#### <a name="office-click-to-run-apps"></a>Aplicativos Clique para Executar do Office
Do Configuration Manager 1806 em diante, a carga de trabalho do Office 365 pode ser transferida para o Intune. Para obter mais informações, veja [Cargas de trabalho podem ser transferidas para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune). <!--1357841-->

#### <a name="mobile-apps"></a>Aplicativos móveis
Do Configuration Manager versão 1806 em diante, a carga de trabalho de aplicativos móveis pode ser transferida para o Intune. Esse recurso é um recurso de pré-lançamento. Para habilitá-lo, veja [Recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Após a transição dessa carga de trabalho, todos os aplicativos disponíveis implantados do Intune estão disponíveis no Portal da Empresa. Os aplicativos que você implanta do Configuration Manager estão disponíveis no Centro de Software.<!--1357892-->


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Instalar o cliente do Configuration Manager nos dispositivos inscritos no Intune

Quando dispositivos Windows 10 são registrados no Intune, você pode instalar o cliente do Configuration Manager nos dispositivos [usando um argumento de linha de comando específico](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client) para preparar os clientes para o cogerenciamento. Em seguida, você habilitar o cogerenciamento no console do Configuration Manager para começar a mover para o Intune cargas de trabalho específicas de dispositivos Windows 10 específicos.
Para dispositivos Windows 10 que ainda não estão registrados no Intune, use o registro automático no Azure para registrar os dispositivos. Para novos dispositivos Windows 10, você pode usar o [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) para configurar a OOBE (configuração inicial pelo usuário), que inclui o registro automático de dispositivos no Intune.

Ao usar o Intune para instalar o cliente do Configuration Manager, habilite um [Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager.



## <a name="monitor-co-management"></a>Monitorar o cogerenciamento

[O painel do cogerenciamento](/sccm/core/clients/manage/co-management-dashboard) ajuda você a analisar os computadores cogerenciados no ambiente. Os gráficos podem ajudar a identificar os dispositivos que podem precisar de atenção.



## <a name="next-steps"></a>Próximas etapas

[Preparar dispositivos Windows 10 para cogerenciamento](co-management-prepare.md)
