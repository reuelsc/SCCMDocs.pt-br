---
title: Nova versão 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Veja os detalhes das alterações e dos novos recursos introduzidos na versão 1710 do System Center Configuration Manager.
ms.date: 1/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c1609f162460d525a146289e70426783cd126912
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123414"
---
# <a name="what39s-new-in-version-1710-of-system-center-configuration-manager"></a>Novidades da versão 1710 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A atualização 1710 do branch atual do System Center Configuration Manager está disponível como uma atualização no console para os sites já instalados que executam a versão 1610, 1702 ou 1706.

Além de novos recursos, este lançamento inclui outras alterações, como correções de bugs. Para saber mais, confira [Resumo das alterações no Branch Atual do System Center Configuration Manager, versão 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran).

As atualizações adicionais a seguir também já estão disponíveis neste lançamento:
- [Pacote cumulativo de atualizações para o Branch Atual do System Center Configuration Manager, versão 1710](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Pacote cumulativo de atualizações 2 para o Branch Atual do System Center Configuration Manager, versão 1710](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Para instalar um novo site, você deve usar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>   - [Instalação de novos sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Instalação de atualizações em sites](/sccm/core/servers/manage/updates)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As seções a seguir fornecem detalhes sobre as alterações e novos recursos introduzidos na versão 1710 do Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura do site

### <a name="updates-for-peer-cache-----sms500850---"></a>Atualizações do Cache Par  <!-- sms500850 -->
A partir desta versão, o Cache Par deixou de ser um recurso de pré-lançamento.  Nenhuma outra alteração do Cache Par foi introduzida nesta versão. Para obter mais informações, consulte [Cache par para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Suporte ao ponto de distribuição de nuvem na nuvem do Azure Governamental   <!-- sms491428 -->
Agora você pode usar [pontos de distribuição baseados em nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) na nuvem do Azure governamental.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Revisão de unidade padrão de inventário <!-- sms503697 -->
Como os dispositivos agora incluem discos rígidos com tamanhos em escalas de GB (gigabytes), TB (terabytes) e maiores, esta versão altera a unidade padrão (SMS_Units) usada em várias exibições de MB (megabytes) para GB. Por exemplo, o valor de v_gs_LogicalDisk.FreeSpace agora relata unidades em GB.


<!-- ## Migration  -->


## <a name="client-management"></a>Gerenciamento de cliente

### <a name="co-management-for-windows-10-devices"></a>Cogerenciamento para dispositivos Windows 10    
<!-- 1350871 --> Em atualizações anteriores do Windows 10, você pode associar um dispositivo com Windows 10 ao Active Directory (AD) local e ao Azure AD baseado em nuvem ao mesmo tempo (Azure AD híbrido). A partir do Configuration Manager versão 1710, o cogerenciamento usufrui dessa melhoria e permite gerenciar dispositivos Windows 10, versão 1709 (também conhecido como Fall Creators Update) simultaneamente usando o Configuration Manager e o Intune. É uma solução que fornece uma ponte do gerenciamento tradicional para o moderno e fornece um caminho para fazer a transição usando uma abordagem em fases. Para obter detalhes, confira [Cogerenciamento para dispositivos com Windows 10](/sccm/comanage/overview).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Reinicie os computadores do console do Configuration Manager <!-- 1356283 -->
A partir desta versão, você pode usar o console do Configuration Manager para identificar os dispositivos cliente que exigem uma reinicialização e, em seguida, usar uma ação de notificação do cliente para reiniciá-los.

Consulte [Como gerenciar clientes no System Center Configuration Manager](/sccm/core/clients/manage/manage-clients#restart-clients)


<!-- ## Compliance settings -->


## <a name="application-management"></a>Gerenciamento de aplicativos
### <a name="improvements-for-run-scripts------1236459---"></a>Melhorias no recurso Executar Scripts   <!-- 1236459 -->
Esta versão oferece várias melhorias para o recurso **Executar Scripts**, permitindo implantar os scripts do PowerShell para serem executados nos dispositivos gerenciados. Esse recurso foi introduzido na versão 1706.

As melhorias incluem:
- Usar Escopos de Segurança para ajudar a controlar quem pode usar o recurso Executar Scripts
- Monitoramento em tempo real dos scripts que você executa
- Os parâmetros do script são exibidos no Assistente para Criar Script, na validação do suporte e são identificados como obrigatórios ou opcionais.

Para obter mais informações de como usar o recurso Executar Scripts, consulte [Criar e executar scripts](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Novas configurações de política de gerenciamento de aplicativo móvel
<!-- 1324760 --> As configurações a seguir foram adicionadas nas configurações de política de gerenciamento de aplicativos móveis:
- **Desabilitar sincronização de contatos**: impede que o aplicativo salve dados no aplicativo Contatos nativo do dispositivo.
- **Desabilitar impressão**: impede que o aplicativo imprima dados corporativos ou de estudante.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>O Centro de Software não distorce mais os ícones maiores do que 250 x 250  
<!-- 1356194 -->

Com esta versão, o Centro de Software não distorcerá mais os ícones maiores do que 250 x 250. O Centro de Software fazia esses ícones parecerem desfocados. Agora, você pode definir um ícone com dimensões de pixel de até 512 x 512, e ele será exibido sem distorção.

Para adicionar um ícone para seu aplicativo no Centro de Software, consulte [Criar aplicativos](/sccm/apps/deploy-use/create-applications).

## <a name="operating-system-deployment"></a>Implantação de sistema operacional
 > [!TIP]   
 > <!-- 1354281 --> Do Windows 10 versão 1709 (também conhecido como Fall Creators Update) em diante, a mídia do Windows inclui várias edições. Ao configurar uma sequência de tarefas para usar um pacote de atualização do sistema operacional ou imagem do sistema operacional, selecione uma [edição com suporte para uso no Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicionar sequências de tarefas filho a uma sequência de tarefas
<!-- 1261338 -->

Você pode adicionar uma nova etapa de sequência de tarefas que executa outra sequência de tarefas e cria uma relação pai/filho entre as sequências de tarefas. Isso permite que você crie sequências de tarefas mais modulares que podem ser usadas novamente.  

Para saber mais sobre a sequência de tarefas filha, consulte [Sequência de tarefas filha](/sccm/osd/understand/task-sequence-steps#child-task-sequence).

## <a name="software-center-customization"></a>Personalização do Centro de Software
<!-- 1351224 --> Você pode adicionar elementos de identidade visual empresarial e especificar a visibilidade das guias no Centro de Software. Você pode adicionar o nome específico da empresa do Centro de Software, definir um tema de cores de configuração do Centro de Software, definir um logotipo da empresa e definir as guias visíveis para os dispositivos cliente.

Para obter mais informações, consulte [Planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager](/sccm/apps/plan-design/plan-for-and-configure-application-management).

## <a name="software-updates"></a>Atualizações de software

### <a name="surface-driver-updates-----1098490---"></a>Atualizações de driver do Surface  <!-- 1098490 -->
A partir desta versão, o gerenciamento de atualizações de driver do Surface deixou de ser um recurso de pré-lançamento.  


## <a name="reporting"></a>Relatórios

### <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limitar telemetria avançada do Windows 10 para enviar apenas dados relevantes para a integridade do dispositivo do Windows Analytics
<!-- 1356148 -->

Agora é possível definir o nível de coleta de dados de telemetria do Windows 10 como **Avançado (Limitado)**. Essa configuração permite que você obtenha informações acionáveis sobre dispositivos em seu ambiente sem que os dispositivos reportem todos os dados no nível de telemetria **Avançado** com Windows 10 versão 1709 ou posterior.

Para obter mais informações, consulte [Como definir as configurações do cliente no System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Gerenciamento de dispositivos móveis

### <a name="actions-for-non-compliance"></a>Ações de não conformidade 
<!--1321366 -->    
Agora é possível configurar uma sequência de ações ordenadas por tempo aplicadas aos dispositivos que estão fora de conformidade. Por exemplo, é possível notificar os usuários sobre dispositivos que não estão em conformidade por email ou marcá-los como não em conformidade. Para obter detalhes, consulte [Set up actions for non-compliance](/sccm/mdm/deploy-use/actions-for-noncompliance) (Configurar ações de não conformidade).

### <a name="windows-10-arm64-device-support"></a>Suporte a dispositivos Windows 10 ARM64
<!-- 1355000 -->

Os cenários híbridos de MDM (gerenciamento de dispositivo móvel) terão suporte em dispositivos ARM64 executando o Windows 10 quando esses dispositivos ficarem disponíveis.

Esses cenários incluem:

- [Registrar dispositivos](../../../mdm/deploy-use/enroll-hybrid-windows.md)
- [Executar ações de apagamento remoto completo e seletivo](../../../mdm/deploy-use/wipe-lock-reset-devices.md)
- [Gerenciar configurações por meio de itens de configuração e linhas de base](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Gerenciar a política de conformidade](../../../mdm/deploy-use/device-compliance-policies.md) e o [acesso condicional](../../../protect/deploy-use/manage-access-to-services.md)
- Gerencie o acesso aos recursos da empresa por meio de:
   - [Perfis de certificado](../../../mdm/deploy-use/create-pfx-certificate-profiles.md)
   - [Perfis de VPN](../../../mdm/deploy-use/create-vpn-profiles.md)
   - [Perfis de Wi-Fi](../../../mdm/deploy-use/create-wifi-profiles.md)
   - [Perfis de email](../../../mdm/deploy-use/create-exchange-activesync-profiles.md)
- [Configurar a política do Windows Hello para Empresas](../../../mdm/deploy-use/windows-hello-for-business-settings.md)
- [Gerenciar aplicativos](../../../mdm/deploy-use/management-tasks-applications.md)

> [!NOTE]
> A implantação de aplicativos .appxbundle criados para várias arquiteturas pode não funcionar nestes dispositivos. Este cenário não é compatível no momento.

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Melhoria da experiência do perfil de VPN no Console do Configuration Manager 
<!-- 1318232 -->

Nesta versão, as páginas de assistente e de propriedades do perfil de VPN foram atualizadas para exibir as configurações apropriadas para a plataforma selecionada:


- Cada plataforma tem seu próprio fluxo de trabalho, o que significa que os novos perfis de VPN contêm apenas a configuração com suporte na plataforma.
- A página **Plataformas com Suporte** agora é exibida após a página **Geral**.  Agora você escolhe a plataforma antes de configurar os valores das propriedades.
- Quando a plataforma está definida como **Android**, **Android for Work** ou **Windows Phone 8.1**, a página **Plataformas com Suporte** não é necessária e não é exibida.
- O fluxo de trabalho baseado no cliente do Configuration Manager foi combinado com os fluxos de trabalho do Windows 10 baseados no cliente do dispositivo móvel híbrido (MDM). Eles dão suporte às mesmas configurações.
- O fluxo de trabalho de cada plataforma inclui apenas as configurações apropriadas para esse fluxo de trabalho.  Por exemplo, o fluxo de trabalho do Android contém as configurações apropriadas para Android e as configurações apropriadas para iOS ou Windows 10 Mobile não aparecem mais no fluxo de trabalho do Android.
- A página VPN automática ficou obsoleta e foi removida.

Essas alterações aplicam-se aos novos perfis de VPN.  

Para minimizar o risco de compatibilidade, os perfis de VPN existentes não foram alterados.  Quando você edita um perfil existente, as configurações são exibidas como quando o perfil foi criado.  

Para obter mais informações, consulte [Perfis de VPN em dispositivos móveis no System Center Configuration Manager](../../../mdm/deploy-use/create-vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Suporte limitado para certificados CNG (Cryptography Next Generation)<!-- 1356191 -->

O Configuration Manager tem suporte limitado para certificados CNG (Cryptography Next Generation). Os clientes do Configuration Manager podem usar o certificado de autenticação de cliente de PKI com chave privada no KSP (provedor de armazenamento de chaves) da CNG. Com o suporte do KSP, os clientes do Configuration Manager dão suporte para chave de privada baseada em hardware, como TPM KSP para certificados de autenticação de cliente de PKI.

Para obter mais informações, consulte [Visão geral dos certificados CNG](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Proteger dispositivos

### <a name="create-and-deploy-exploit-guard-policies"></a>Criar e implantar políticas do Exploit Guard
<!-- 1355468 -->

Você pode [criar e implantar políticas](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) que gerenciarão os quatro componentes do Windows Defender Exploit Guard, incluindo redução da superfície de ataque, acesso controlado a pastas, proteção de exploração e proteção de rede.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Criar e implantar políticas do Windows Defender Application Guard
<!-- 1351960 -->

Você pode [criar e implantar políticas do Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy) usando a proteção de ponto de extremidade do Configuration Manager.

### <a name="device-guard-policy-changes"></a>Alterações de política do Device Guard
<!-- 1355092 --> As três alterações a seguir foram feitas em relação às políticas do Device Guard:

- Políticas do Device Guard que foram renomeadas para políticas de Controle de Aplicativo do Windows Defender. Então, por exemplo, o **Assistente para Criar política do Device Guard** foi nomeado para **Assistente para Criar política de controle de aplicativo do Windows Defender**.
- Os dispositivos que usam o Fall Creators Update da versão 1709 do Windows não exigem uma reinicialização para aplicar as políticas do Windows Defender Application Control. Reiniciar ainda é o padrão, mas você pode [desligar as reinicializações](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
- Você pode [definir os dispositivos para executar automaticamente softwares](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) que são confiáveis segundo o Gráfico de Segurança Inteligente.





## <a name="next-steps"></a>Próximas etapas
Quando estiver pronto para instalar esta versão, consulte [Atualizações para o Configuration Manager](/sccm/core/servers/manage/updates).
