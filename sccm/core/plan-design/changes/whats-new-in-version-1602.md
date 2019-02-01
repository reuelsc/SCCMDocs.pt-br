---
title: Novidades na versão 1602
titleSuffix: Configuration Manager
description: Veja os detalhes das alterações e os novos recursos introduzidos na versão 1602 do System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 86d36921939b611fa6647d4a0bf3af6d11f27ee7
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897620"
---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>Novidades da versão 1602 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


A atualização 1602 do System Center Configuration Manager está disponível apenas como uma atualização no console para sites instalados anteriormente que executam a versão 1511. A versão 1511 é a versão de linha de base inicial usada para instalar novos sites do Configuration Manager.  


> [!TIP]  
>  Saiba mais sobre:  
>   
>   -   [Instalação de novos sites](/sccm/core/servers/deploy/install) (usando uma versão de linha de base como a 1511)  
>   -   [Instalação de atualizações em sites](/sccm/core/servers/manage/updates) (como a atualização 1602)  

 As seções a seguir fornecem detalhes sobre as alterações e novas funcionalidades introduzidas na versão 1602 do Configuration Manager.  

## <a name="site-infrastructure"></a>Infraestrutura do site  

###  <a name="bkmk_UpgradeOS"></a> Atualização in-loco do sistema operacional dos servidores do site que executam o Windows Server 2008 R2  
 Os sites do Configuration Manager que executam a versão 1602 ou posterior dão suporte à atualização in-loco do sistema operacional dos servidores do site do Windows Server 2008 R2 para o Windows Server 2012 R2.  

> [!WARNING]  
>  Antes de atualizar para o Windows Server 2012 R2, é necessário desinstalar o WSUS 3.2 do servidor.  
>   
>  Para obter informações sobre essa etapa crítica, consulte a seção “Funcionalidade nova e alterada” em [Visão geral do Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) na documentação do Windows Server.  

 Para atualizar um servidor, use os procedimentos de atualização do Windows Server 2012 R2. Não é necessário executar uma restauração do servidor do site do Configuration Manager após a atualização. Para obter os procedimentos de atualização, consulte [Opções de atualização para o Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) na documentação do Windows Server.  

###  <a name="bkmk_AOAG"></a> Grupos de disponibilidade AlwaysOn do SQL Server  
 Use grupos de disponibilidade AlwaysOn do SQL Server para hospedar o banco de dados do site em sites primários e o site de administração central como uma solução de alta disponibilidade e recuperação de desastre.  

 Para obter detalhes, consulte [AlwaysOn do SQL Server para um banco de dados do site altamente disponível do System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>Implantação de sistema operacional  

### <a name="windows-10-servicing"></a>Serviço do Windows 10  
 Os seguintes aprimoramentos para a manutenção do Windows 10 foram adicionados na versão 1602 do Configuration Manager:  

-   Novas opções de filtro estão disponíveis para planos de manutenção que permitem filtrar por **Idioma**, **Obrigatório** e **Título**. Somente as atualizações que atendem aos critérios especificados serão adicionadas à implantação associada.  

-   Ao selecionar a classificação **Atualizações** para a sincronização das atualizações de software, um aviso é exibido. Esse aviso informa que o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para o WSUS (Windows Server Update Services) 4.0 é necessário para que seja possível sincronizar com êxito as atualizações de software e para o funcionamento correto do Serviço do Windows 10. Na mensagem de aviso, é possível acessar o artigo da base de dados de conhecimento associado.  

-   As atualizações do Windows 10 disponíveis agora são exibidas apenas no nó **Manutenção do Windows 10** \ **Todas as Atualizações do Windows 10** do console do Configuration Manager. Essas atualizações não são mais exibidas no nó **Atualizações de Software** \ **Todas as Atualizações de Software** do console.  

-   Um plano de manutenção é considerado uma implantação de alto risco, e a janela **Selecionar Coleção** exibe apenas as coleções personalizadas que atendem às definições de verificação da implantação que são configuradas nas propriedades do site. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco para o System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   Agora os usuários que iniciam um pacote de Atualização do Windows 10 recebem uma mensagem informando que seus sistemas operacionais serão atualizados.  

## <a name="application-management"></a>Gerenciamento de aplicativos  

### <a name="ios-app-configuration-policies"></a>Políticas de configuração de aplicativo iOS  
 Use políticas de configuração de aplicativo do Configuration Manager para fornecer configurações que possam ser necessárias quando o usuário executar um aplicativo iOS. Por exemplo, um aplicativo pode exigir que o usuário especifique o número da porta, idiomas, configurações de segurança ou de identidade visual (como um logotipo da empresa) personalizado. Se essas configurações forem inseridas incorretamente, isso poderá aumentar a carga do suporte técnico e também reduzir a adoção de novos aplicativos.  

 As políticas de configuração de aplicativo podem ajudar a eliminar esses problemas, permitindo que você implante essas configurações para os usuários em uma política, antes que eles executem o aplicativo. As configurações são então fornecidas automaticamente e o usuário não precisa executar nenhuma ação. Para obter detalhes, consulte [Configurar aplicativos iOS com políticas de configuração de aplicativos no System Center Configuration Manager](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  

### <a name="manage-volume-purchased-ios-apps"></a>Manage volume-purchased iOS apps  
 O Configuration Manager pode ajudá-lo a implantar e gerenciar aplicativos adquiridos por volume por meio do Apple VPP (Volume Purchase Program). O Configuration Manager importa as informações de licença da loja de aplicativos e controla quantas licenças foram utilizadas.  

 Para obter detalhes, consulte [Gerenciar aplicativos iOS adquiridos por volume com o System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).  

### <a name="automatic-creation-of-office-mobile-apps"></a>Criação automática de aplicativos móveis do Office  
 Quando você atualiza da versão 1511 para a 1602, o Configuration Manager cria automaticamente os seguintes aplicativos móveis do Microsoft Office para Android e iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (apenas iOS)  

-   Microsoft Outlook  

Você encontrará esses aplicativos no nó **Aplicativos** do console do Configuration Manager.  

 Para mais informações sobre a implantação de aplicativos, confira [Como implantar aplicativos com o System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Atualizações de software  

### <a name="manage-office-365-client-updates"></a>Gerenciar atualizações do cliente do Office 365  
 O System Center Configuration Manager tem a capacidade de gerenciar atualizações de cliente do Office 365 usando o fluxo de trabalho de gerenciamento de atualizações de software. Para obter mais informações, consulte [Gerenciar atualizações do Office 365 ProPlus com o System Center Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates).  

## <a name="compliance-settings"></a>Configurações de conformidade  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Configurações de conformidade para dispositivos que executam o Windows 10 Team  
 Foram adicionadas novas configurações ao item de configuração do **Windows 8.1 e Windows 10**. Essas configurações ajudam você a controlar os dispositivos que executam o Windows 10 Team, como um dispositivo Surface Hub.  

 Para obter detalhes, consulte [Como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 gerenciados sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Configurações do modo de quiosque para dispositivos Android Samsung KNOX Standard  
 O modo de quiosque permite bloquear um dispositivo para que somente determinados recursos funcionem. Por exemplo, você pode permitir que um dispositivo execute apenas um aplicativo gerenciado especificado ou desabilitar os botões de volume em um dispositivo. Essas configurações podem ser usadas para um modelo de demonstração de um dispositivo ou para um dispositivo dedicado a executar apenas uma função, como um dispositivo de ponto de venda. No Configuration Manager, agora é possível especificar as configurações do modo de quiosque para dispositivos Samsung KNOX Standard.  

 Para obter detalhes, consulte [Como criar itens de configuração para dispositivos Android e Samsung KNOX Standard gerenciados sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).  

## <a name="conditional-access"></a>Acesso condicional  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>Acesso condicional para PCs gerenciados pelo System Center Configuration Manager  
 Antes dessa versão, para configurar o acesso adicional em um computador, ele precisava estar registrado no Intune ou ser um computador ingressado em domínio. A partir da atualização 1602, há suporte para o acesso condicional em computadores gerenciados pelo System Center Configuration Manager. Para computadores gerenciados pelo System Center Configuration Manager, é possível restringir o acesso ao Exchange Online e ao SharePoint Online apenas a dispositivos que estão em conformidade com as políticas de conformidade definidas.  

 Para obter detalhes, consulte [Gerenciar o acesso aos serviços do O365 para PCs gerenciados pelo System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

### <a name="restricting-access-based-on-the-health-of-devices"></a>Restringindo o acesso com base na integridade dos dispositivos  
 Agora é possível restringir o acesso ao email e aos serviços do Office 365 com base na integridade dos dispositivos, conforme relatado pelo Serviço de Atestado de Integridade. Além disso, os dispositivos gerenciados pelo Intune são incluídos nos relatórios de integridade do dispositivo.  

 O console do Configuration Manager conta com uma nova regra de conformidade que permite especificar se os dispositivos devem ter o acesso permitido ou bloqueado com base em seu status de integridade. Para obter detalhes sobre o Serviço de Atestado de Integridade e como a integridade dos dispositivos é relatada no Intune, consulte [Atestado de integridade do System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Novas regras de política de conformidade  
 Novas regras de política de conformidade, como atualizações automáticas e a exigência de uma senha para desbloquear dispositivos, foram adicionadas para dar suporte a melhores requisitos de segurança.

 Para obter mais detalhes, consulte [Políticas de conformidade do dispositivo no System Center Configuration Manager](../../../protect/deploy-use/device-compliance-policies.md).  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Verificar se os dispositivos registrados e em conformidade sempre têm acesso ao Exchange no Local  
 Quando você marca a opção a seguir, os dispositivos registrados no Intune e em conformidade com as políticas de conformidade têm permissão para acessar o Exchange local: **Substituição de regra padrão – sempre permitir que os dispositivos registrados no Intune e em conformidade acessem o Exchange local:**. Essa regra está disponível na **página Geral** do **Assistente de Configuração de Política de Acesso Condicional** do Exchange no local.

 Essa regra substitui a regra padrão, o que significa que mesmo que você defina a regra padrão para bloquear o acesso ou colocar em quarentena, os dispositivos registrados e em conformidade ainda poderão acessar o Exchange no Local. Use essa configuração quando desejar que dispositivos registrados e compatíveis sempre tenham acesso ao email por meio do Exchange no local.   

 Para ver um passo a passo detalhado, consulte [Gerenciar acesso a email no System Center Configuration Manager](../../../protect/deploy-use/manage-email-access.md).  

## <a name="client-management"></a>Gerenciamento de cliente  

### <a name="client-online-status"></a>Status online do cliente  
 Um novo status para clientes está disponível para monitoramento, esteja o computador online ou não. Um computador será considerado online se estiver conectado ao seu ponto de gerenciamento atribuído. Para indicar se o computado está online, o cliente envia mensagens como ping ao ponto de gerenciamento. Se o ponto de gerenciamento não receber uma mensagem depois de 5 minutos, o cliente será considerado offline.  

 Para obter detalhes, consulte [Como monitorar clientes no System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Atualizar a política de computador e de usuário do computador no Centro de Software  
 Uma nova opção, **Política de Sincronização**, foi adicionada à página **Opções** > **Manutenção do Computador** do Centro de Software, o que faz com que o computador atualize sua política de computador e de usuário do Configuration Manager.  

### <a name="software-center-branding-changes"></a>Alterações de identidade visual do Centro de Software  
 É possível alterar a cor, o nome da organização e o ícone exibidos no Centro de Software. Essas configurações são aplicadas de acordo com as seguintes regras:  

- Se a função de servidor do site do ponto de sites da Web do Catálogo de Aplicativos não estiver instalada, o Centro de Software exibirá o nome da organização especificado na configuração do cliente **Agente de Computador** chamada **Nome da organização exibido no Centro de Software**.  

- Se a função de servidor do site do ponto de sites da Web do Catálogo de Aplicativos estiver instalada, o Centro de Software exibirá o nome da organização e a cor especificados nas propriedades da função de servidor do site do ponto de sites da Web do Catálogo de Aplicativos.  

- Se uma assinatura do Microsoft Intune estiver configurada e conectada ao ambiente do Configuration Manager, o Centro de Software exibirá o nome da organização, a cor e o logotipo da empresa especificados nas propriedades da assinatura do Intune.  

### <a name="health-attestation"></a>Atestado de integridade  
 Os administradores podem exibir o status do Atestado de Integridade do Dispositivo com Windows 10 no console do Configuration Manager. Isso está disponível para o Configuration Manager, bem como para o Configuration Manager com o Microsoft Intune. O atestado de integridade do dispositivo permite que o administrador garanta que os computadores cliente tenham as seguintes configurações confiáveis de BIOS, TPM e software de inicialização habilitadas:  

-   Antimalware de inicialização antecipada  

-   BitLocker  

-   Inicialização Segura  

-   Integridade do código  

Para obter detalhes, consulte [Atestado de integridade do System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Aprimoramentos nas configurações de antimalware do Endpoint Protection  
 A versão 1602 adiciona as seguintes novas configurações na política antimalware do Endpoint Protection para o Windows Defender:  

-   Proteção em tempo real: bloqueie aplicativos possivelmente indesejados no download, antes da instalação.  

-   Configurações de verificação: examine as unidades de rede mapeadas durante uma verificação completa.  

-   Configurações de envio automático de arquivo de exemplo:  

     O mecanismo antimalware pode solicitar que amostras de arquivo sejam enviadas à Microsoft para análise posterior. Por padrão, ele solicitará sempre antes de enviar esses exemplos. Os administradores agora podem gerenciar as configurações a seguir para configurar esse comportamento:  

    -   Avançado: habilite o envio automático de arquivo de exemplo para ajudar a Microsoft a determinar se determinados itens detectados são mal-intencionados.  

    -   Avançado: permita que os usuários modifiquem as configurações de envio automático de arquivo de exemplo.  

    Além disso, na seção “Configurações de exclusão” da política antimalware do Endpoint Protection, a configuração existente **Excluir arquivos e pastas** agora permite exclusões de dispositivo.  

Para obter detalhes, consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Gerenciamento de dispositivos móveis  

### <a name="ios-activation-lock"></a>Bloqueio de Ativação do iOS  
 O Configuration Manager pode ajudar a gerenciar o Bloqueio de Ativação do iOS, um recurso do aplicativo Buscar meu iPhone para dispositivos iOS 7.1 e posteriores. O Bloqueio de Ativação é habilitado automaticamente quando o aplicativo Buscar meu iPhone for usado em um dispositivo. Depois que ele for habilitado, a ID da Apple e a senha do usuário deverão ser inseridas antes que qualquer pessoa possa:  

-   Desligar a opção Localizar Meu iPhone.  

-   Apagar o dispositivo.  

-   Reativar o dispositivo.  

O Configuration Manager pode solicitar o status do Bloqueio de Ativação de dispositivos supervisionados e não supervisionados que executam o iOS 7.1 e posterior. Para dispositivos supervisionados, o Configuration Manager pode recuperar o código de bypass de Bloqueio de Ativação e emiti-lo diretamente para o dispositivo.  

 Para obter detalhes, consulte [Ajudar a proteger dispositivos iOS com bypass de Bloqueio de Ativação no System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock).  

### <a name="monitor-terms-and-conditions-deployments"></a>Monitorar implantações de termos e condições  
 Você pode monitorar implantações de termos e condições no console do Configuration Manager.  

 Selecione a implantação de termos e condições na lista de implantações. A área de resumo mostra as seguintes estatísticas:  

-   **Em conformidade**: os usuários que aceitaram a versão mais recente dos termos e condições.  

-   **Erro**  

-   **Fora de conformidade**: Os usuários que aceitaram uma versão dos termos e condições, mas não a versão mais recente.  

-   **Desconhecido**: os usuários que nunca aceitaram os termos e condições, incluindo aqueles que não têm um dispositivo registrado.  
