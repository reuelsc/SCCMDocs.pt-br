---
title: Nova versão 1610
titleSuffix: Configuration Manager
description: Veja os detalhes das alterações e os novos recursos introduzidos na versão 1610 do System Center Configuration Manager.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: a58c5c4a9543ab982ec45467eff02e134ea48965
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127551"
---
# <a name="what39s-new-in-version-1610-of-system-center-configuration-manager"></a>Novidades da versão 1610 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A atualização 1610 da ramificação atual do System Center Configuration Manager está disponível como uma atualização no console para sites instalados anteriormente que executam a versão 1511, 1602 ou 1606.


> [!TIP]  
> Para instalar um novo site, você deve usar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>  -   [Instalação de novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Instalação de atualizações em sites](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As seções a seguir fornecem detalhes sobre as alterações e novas funcionalidades introduzidas na versão 1610 do Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Monitoramento do status de instalação de atualização no console  
Começando com a versão 1610, quando você instala um pacote de atualização e monitora a instalação no console, há uma nova fase: **Pós-instalação**. Esta fase inclui o status para tarefas como reiniciar serviços essenciais e inicialização de monitoramento de replicação. (Essa fase não está disponível no console até a instalação das atualizações do site para a versão 1610.) Para obter mais informações sobre o status de instalação da atualização, consulte [Instalar atualizações no console](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).


## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir clientes da atualização automática
Você pode excluir os clientes Windows da atualização para novas versões do software cliente. Para fazer isso, você pode incluir os computadores cliente em uma coleção especificada para ser excluída da atualização. Os clientes da coleção excluída ignoram as solicitações para atualizar o software cliente.  Para obter mais informações, consulte [Excluir clientes Windows das atualizações](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Aprimoramentos para grupos de limites
A versão 1610 introduz alterações importantes para os grupos de limites e como eles funcionam com pontos de distribuição. Essas alterações podem simplificar o design da infraestrutura de conteúdo, enquanto proporcionam a você mais controle sobre como e quando os clientes realizam o fallback para pesquisar pontos de distribuição adicionais como locais de fonte de conteúdo. Isso inclui pontos de distribuição baseados em nuvem e locais.
Esses aprimoramentos substituem conceitos e comportamentos com os quais você pode estar familiarizado, como configurar pontos de distribuição para serem rápidos ou lentos. O novo modelo deve ser mais fácil de configurar e manter. Essas alterações também são bases para alterações futuras, que melhorarão outras funções do sistema de sites associadas aos grupos de limites.

Ao atualizar para a versão 1610, a atualização converte suas configurações de grupo de limites atuais de acordo com o novo modelo para que essas alterações não incomodem suas configurações de distribuição de conteúdo existentes.

Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-groups).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Cache de Pares para distribuição de conteúdo para clientes
Começando da versão 1610, o cliente **Cache de Pares** ajuda você a gerenciar a implantação de conteúdo para clientes em locais remotos. O Cache de Pares é uma solução interna do Configuration Manager para clientes compartilharem conteúdo com outros clientes diretamente do cache local.

Depois de implantar configurações do cliente que habilitam o Cache de Pares para uma coleção, os membros dessa coleção poderão atuar como uma fonte de conteúdo par para outros clientes no mesmo grupo de limites.

Você também pode usar o novo painel **Fontes de Dados do Cliente** para entender o uso de fontes de conteúdo de Cache de Pares em seu ambiente.

> [!TIP]  
> Com a versão 1610, o cache de pares e o painel de fontes de dados do cliente são recursos de pré-lançamento. Para habilitá-los, confira [Usar recursos de pré-lançamento de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

Para saber mais, veja [Cache de pares para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache) e [Painel Fontes de Dados do Cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar vários pontos de distribuição compartilhados ao mesmo tempo
Agora você pode usar a opção para **Transferir Ponto de Distribuição** para que o Configuration Manager processe em paralelo a reatribuição de até 50 pontos de distribuição compartilhados ao mesmo tempo. Antes dessa versão, os pontos de distribuição reatribuídos foram processados um de cada vez. Para mais informações, consulte [Migrar vários pontos de distribuição compartilhados ao mesmo tempo](/sccm/core/migration/planning-a-content-deployment-migration-strategy#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Gateway de gerenciamento de nuvem para o gerenciamento de clientes baseados na Internet

O gateway de gerenciamento de nuvem fornece uma maneira simples de gerenciar clientes do Configuration Manager na Internet. O serviço de gateway de gerenciamento de nuvem, que é implantado no Microsoft Azure e requer uma assinatura do Azure, conecta-se à sua infraestrutura local do Configuration Manager usando uma nova função chamada de ponto de conexão do gateway de gerenciamento de nuvem. Após ser completamente implantado e configurado, os clientes poderão se comunicar com funções locais do sistema de sites do Configuration Manager e com pontos de distribuição baseados em nuvem independentemente de estarem conectados à rede privada interna ou à Internet. Para obter mais informações e ver como o gateway de gerenciamento de nuvem se compara com o gerenciamento de clientes baseado na Internet, consulte [Gerenciar clientes na Internet](/sccm/core/clients/manage/manage-clients-internet).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Melhorias na Política de atualização de edição do Windows 10
Nesta versão, as seguintes melhorias foram feitas neste tipo de política:

- Agora é possível usar a política de atualização de edição com computadores Windows 10 que executam o cliente do Configuration Manager, além de computadores Windows 10 registrados no Microsoft Intune.
- É possível atualizar do Windows 10 Professional para qualquer uma das plataformas no assistente compatíveis com o hardware.

## <a name="manage-hardware-identifiers"></a>Gerenciar os identificadores de hardware
Agora você pode fornecer uma lista de IDs de hardware que o Configuration Manager deve ignorar para fins de registro de cliente e de inicialização PXE. Há dois problemas comuns que esse procedimento ajuda a resolver:

1. Muitos dispositivos, como o Surface Pro 3, não incluem uma porta Ethernet integrada. Um adaptador USB para Ethernet geralmente é usado para estabelecer uma conexão com fio para fins de implantação do sistema operacional. No entanto, eles costumam ser adaptadores compartilhados, devido ao custo e à usabilidade geral. Como o endereço MAC do adaptador é usado para identificar o dispositivo, reutilizar o adaptador se torna problemático sem ações de administrador adicionais entre cada implantação. Agora no Configuration Manager versão 1610, você pode excluir o endereço MAC desse adaptador para que ele possa ser facilmente reutilizado nesse cenário.
2. O esperado é que a ID do SMBIOS seja um identificador de hardware exclusivo, mas alguns dispositivos de hardware específicos são criados com IDs duplicadas. Esse problema pode não ser tão comum quanto o cenário do adaptador USB para Ethernet descrito acima, mas você pode solucioná-lo usando a lista de IDs de hardware excluídos.

Para mais detalhes, consulte [Gerenciar os identificadores de hardware duplicados](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Aprimoramentos na integração da Windows Store para Empresas com o Configuration Manager
Alterações nessa versão:
- Anteriormente, você podia implantar apenas aplicativos gratuitos da Windows Store para Empresas. Agora, o Configuration Manager também dá suporte à implantação de aplicativos licenciados online pagos (apenas para dispositivos registrados do Intune).
- Agora você pode iniciar uma sincronização imediata entre a Windows Store para Empresas e o Configuration Manager.
- Agora você pode modificar a chave secreta do cliente obtida do Azure Active Directory.
- Você pode excluir uma assinatura do repositório.

Para obter detalhes, confira [Gerenciar aplicativos da Windows Store para Empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Sincronização de política para dispositivos registrados pelo Intune
Agora você pode solicitar uma sincronização de política em um dispositivo registrado no Intune pelo console do Configuration Manager, em vez de precisar solicitar uma sincronização no aplicativo do Portal da Empresa no próprio dispositivo. As informações de estado da solicitação de sincronização ficam disponíveis como uma nova coluna as exibições do dispositivo, chamada **Estado de Sincronização Remota**. As informações também aparecem na seção de dados de descoberta na caixa de diálogo **Propriedades** de cada dispositivo móvel.
Para saber mais, veja [Sincronizar remotamente a política em dispositivos registrados no Intune pelo console do Configuration Manager](/sccm/mdm/deploy-use/sync-intune-device).


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Use as configurações de conformidade para definir configurações do Windows Defender
Agora você pode definir as configurações de cliente do Windows Defender em computadores Windows 10 registrados no Intune usando itens de configuração no console do Configuration Manager.
Para saber mais, veja a seção **Windows Defender** em [Criar itens de configuração para dispositivos Windows 8.1 e Windows 10 gerenciados sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).



## <a name="general-improvements-to-software-center"></a>Melhorias gerais ao Centro de Software
- Os usuários agora podem solicitar aplicativos do Centro de Software, bem como o Catálogo de Aplicativos.
- Melhorias para ajudar os usuários a entender qual software é novo e relevante.

## <a name="new-columns-in-device-collection-views"></a>Novas colunas nas exibições de coleção de dispositivos
Agora você pode exibir as colunas para **IMEI** e **Número de Série** (para dispositivos iOS) em exibições de coleção de dispositivos.
Para detalhes, confira [Pré-declarar dispositivos com número de série do iOS ou IMEI](https://docs.microsoft.com/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id).

## <a name="customizable-branding-for-software-center-dialogs"></a>Identidade visual personalizável para caixas de diálogo do Centro de software
A identidade visual personalizada do Centro de Software foi introduzida no Configuration Manager versão 1602. Na versão 1610, essa identidade visual foi estendida para todas as caixas de diálogo associadas para fornecer uma experiência mais consistente aos usuários do Centro de Software.

A identidade visual personalizada do Centro de Software é aplicada de acordo com as regras a seguir:

- Se a função de servidor de sites do ponto de sites da Web do Catálogo de aplicativos não estiver instalada, o Centro de software exibe o nome da organização especificado na configuração do cliente **Agente de Computador** chamada **Nome da organização exibido no Centro de Software**. Para ver instruções, consulte [How to configure client settings (Como definir as configurações do cliente)](../../clients/deploy/configure-client-settings.md).

- Se a função de servidor de sites do ponto de sites da Web do Catálogo de Aplicativos estiver instalada, o Centro de software exibe o nome da organização e a cor especificados nas propriedades da função de servidor de sites do ponto de sites da Web do Catálogo de Aplicativos. Para obter mais informações, consulte [Configuration options for Application Catalog website point (Opções de configuração do ponto de sites da Web do catálogo de aplicativos)](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#Application-Catalog-website-point).

- Se uma assinatura do Microsoft Intune estiver configurada e conectada ao ambiente do Configuration Manager, o Centro de Software exibirá o nome da organização, a cor e o logotipo da empresa especificados nas propriedades da assinatura do Intune. Para obter mais informações, consulte [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Período de cortesia para imposição de implantações de atualizações de software e aplicativos obrigatórios
Em alguns casos, talvez você queira conceder aos usuários mais tempo instalar as atualizações de software ou as implantações de aplicativo obrigatórias além das datas limite definidas. Por exemplo, isso normalmente pode ser necessário quando um computador ficou desligado por um período estendido e precisa reinstalar uma grande quantidade de implantações de atualização ou de aplicativo. Por exemplo, se um usuário final acabou de voltar de férias, eles terá que aguardar um longo período enquanto as implantações de aplicativo atrasadas são instaladas. Para ajudar a resolver esse problema, agora você pode definir um período de carência para a imposição implantando configurações de cliente do Configuration Manager para uma coleção. 

Para configurar o período de carência, execute as seguintes ações:
1. Na página **Agente de Computador** das configurações do cliente, configure a nova propriedade **Período de carência para a imposição após a data limite da implantação (horas):** com um valor entre **1** e **120** horas.
2. Em uma nova implantação de aplicativo obrigatória ou nas propriedades de uma implantação existente, na página **Agendamento**, marque a caixa de seleção **Atrase a imposição dessa implantação de acordo com as preferências do usuário, até o período de carência definido nas configurações do cliente**. Todas as implantações que têm essa caixa de seleção marcada e que são destinadas a dispositivos nos quais você também implantou as configurações do cliente usarão o período de carência imposto.

Se você configurar um período de carência para a imposição e marcar a caixa de seleção, quando o prazo da instalação do aplicativo for atingido, ele será instalado na primeira janela fora do horário comercial que o usuário configurou até esse período de carência. No entanto, o usuário ainda poderá abrir o Centro de Software e instalar o aplicativo a qualquer momento que desejar. Depois que o período de carência expirar, a imposição retorna ao comportamento normal para implantações atrasadas. Opções semelhantes foram adicionadas ao assistente de implantação de atualizações de software, ao assistente de regras de implantação automática e páginas de propriedades.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Funcionalidade aprimorada em caixas de diálogo do software necessário
Quando um usuário receber software obrigatório, na configuração **Suspender e lembrar dentro de:** ele pode selecionar na seguinte lista suspensa de valores: 
- **Mais tarde**. Especifica que as notificações são agendadas com base nas configurações de notificação definidas nas configurações do Agente Cliente.
- **Tempo fixo**. Especifica que a notificação será agendada para ser exibida novamente após o tempo selecionado (por exemplo, em 30 minutos).

![Página do Agente de Computador nas configurações do Agente Cliente](media/client-notification-settings.png)

O tempo máximo de adiamento baseia-se nos valores de notificação definidos nas configurações de Agente Cliente. Por exemplo, se a configuração **Prazo de implantação superior a 24 horas, lembrar o usuário a cada (horas)** na página Agente de Computador estiver definida como 10 horas e demorar mais de 24 horas até o prazo de implantação, o usuário verá um conjunto de opções de adiamento de até 10 horas, mas nunca superior a esse valor. Conforme o prazo se aproximar, a caixa de diálogo mostrará menos opções, consistentes com as configurações do Agente Cliente relevantes para cada componente da linha de tempo da implantação.

Além disso, para uma implantação de alto risco, como uma sequência de tarefas que implanta um sistema operacional, a experiência de notificação do usuário agora será mais invasiva. Em vez de uma notificação transitória na barra de tarefas, cada vez que o usuário for notificado de que uma manutenção de software crítica é necessária, uma caixa de diálogo como a seguinte será exibida no computador:

![Caixa de diálogo Software Exigido](media/client-toast-notification.png)


Para obter mais informações:
- [Configurações para gerenciar implantações de alto risco](../../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como definir as configurações do cliente](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Painel de atualizações de software
É possível usar o novo painel de atualizações de software para exibir o status atual de conformidade dos dispositivos em sua organização e analisar rapidamente os dados para ver quais dispositivos estão em risco. Para exibir o painel, navegue até **Monitoramento** > **Visão Geral** > **Segurança** > **Painel de Atualizações de Software**.

Para ver mais detalhes, consulte [Monitorar atualizações de software](/sccm/sum/deploy-use/monitor-software-updates).


## <a name="improvements-to-the-application-request-process"></a>Melhorias no processo de solicitação do aplicativo
Depois de ter aprovado um aplicativo para a instalação, você pode escolher negar a solicitação subsequente clicando em **Negar** no console do Configuration Manager. Anteriormente, esse botão era desabilitado após a aprovação.

Essa ação não faz com que o aplicativo seja desinstalado de todos os dispositivos. No entanto, ela interrompe os usuários de instalarem novas cópias do aplicativo do Centro de Software.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar por tamanho do conteúdo em regras de implantação automática
Agora, você pode filtrar o tamanho do conteúdo para atualizações de software em regras de implantação automática. Por exemplo, para baixar apenas atualizações de software menores que 2 MB, você pode definir o filtro **Tamanho do Conteúdo (KB)** como **< 2048**. Usar esse filtro impede que atualizações de software grandes sejam baixadas automaticamente, para dar melhor suporte à manutenção simplificada de nível inferior do Windows quando a largura de banda de rede é limitada. Para obter detalhes, consulte:
- [Configuration Manager e Serviço do Windows simplificado em sistemas operacionais de nível inferior](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)
- [Implantar atualizações de software automaticamente](/sccm/sum/deploy-use/automatically-deploy-software-updates)

Para configurar o campo **Tamanho do Conteúdo (KB)**, siga um destes procedimentos:
- Ao criar uma regra de implantação automática, no Assistente Criar regra de implantação automática, vá para a página **Atualizações de software**.
- Nas propriedades de uma regra de implantação automática existente, vá para a guia **Atualizações de software**.

## <a name="office-365-client-management-dashboard"></a>Painel de Gerenciamento de Clientes do Office 365
O painel de Gerenciamento de Clientes do Office 365 agora está disponível no console do Configuration Manager. Para exibir o painel, acesse **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Cliente do Office 365**.

O painel exibe gráficos para o seguinte:

- Número de clientes do Office 365
- Versões do cliente do Office 365
- Idiomas do cliente do Office 365
- Canais do cliente do Office 365     

Para saber mais, veja [Gerenciar atualizações do Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Etapas de sequência de tarefas para gerenciar o BIOS para a conversão de UEFI
Agora você pode personalizar uma sequência de tarefas de implantação do sistema operacional com uma nova variável, TSUEFIDrive, para que a etapa **Reiniciar o Computador** prepare uma partição FAT32 no disco rígido para a transição para UEFI. O procedimento a seguir fornece um exemplo de como você pode criar etapas de sequência de tarefas para preparar o disco rígido para a conversão de BIOS para UEFI. Para saber mais, veja [Etapas da sequência de tarefas para gerenciar a conversão de BIOS para UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Melhorias à etapa de sequência de tarefas: Prepare ConfigMgr Client for Capture  
A etapa Preparar o Cliente do ConfigMgr agora removerá completamente o cliente do Configuration Manager, em vez de apenas remover informações importantes. Quando a sequência de tarefas implanta a imagem capturada do sistema operacional, ela instala um novo cliente do Configuration Manager a cada vez. Para obter detalhes, consulte [Etapas da sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Gráficos da política de conformidade do Intune
Agora é possível obter uma exibição rápida da conformidade geral dos dispositivos e os principais motivos de não conformidade usando novos gráficos no workspace **Monitoramento** no console do Configuration Manager. Você pode clicar em uma seção no gráfico para detalhar uma lista de dispositivos nessa categoria. Para obter detalhes, consulte [Monitorar a política de conformidade](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Integração do Lookout para implementações híbridas para proteger dispositivos Android e iOS
A Microsoft está em integração com a solução de proteção de ameaças móveis do Lookout para proteger dispositivos móveis Android e iOS ao detectar malware, aplicativos de risco e muito mais, em dispositivos. A solução do Lookout ajuda a determinar o nível de ameaça, que é configurável. Você pode criar uma regra de política de conformidade no System Center Configuration Manager para determinar a conformidade do dispositivo com base na avaliação de risco feita pelo Lookout. Usando políticas de acesso condicional, você pode permitir ou bloquear o acesso aos recursos da empresa com base no status de conformidade do dispositivo. Para saber mais sobre a integração e como ela funciona, consulte [Gerenciar o acesso com base no dispositivo, na rede e no risco do aplicativo](/sccm/protect/deploy-use/manage-access-based-on-device-network-app-risk).

Os usuários de dispositivos iOS incompatíveis serão solicitados a se registrar. Eles serão solicitados a instalar o aplicativo Lookout for Work em seus dispositivos, ativar o aplicativo e corrigir ameaças relatadas no aplicativo Lookout for Work para obter acesso aos dados da empresa. Saiba como [Configurar e implantar aplicativos Lookout for Work](/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps).



## <a name="new-compliance-settings-for-configuration-items"></a>Novas configurações de conformidade para itens de configuração
Há várias novas configurações que você pode usar em seus itens de configuração para várias plataformas de dispositivo. Essas são configurações que anteriormente estavam no Microsoft Intune em uma configuração autônoma e agora estão disponíveis quando você usa o Intune com o Configuration Manager.
Para mais detalhes, consulte [Itens de configuração para dispositivos gerenciados sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/configuration-items-for-devices-managed-without-the-client).

### <a name="new-settings-for-android-devices"></a>Novas configurações para dispositivos Android
#### <a name="password-settings"></a>Configurações de senha
- **Lembrar histórico de senha**
- **Permitir desbloqueio por impressão digital**

#### <a name="security-settings"></a>Configurações de segurança
- **Exigir criptografia em cartões de memória**
- **Permitir captura de tela**
- **Permitir envio de dados diagnósticos**

#### <a name="browser-settings"></a>Configurações do navegador
- **Permitir navegador da Web**
- **Permitir preenchimento automático**
- **Permitir bloqueador de pop-up**
- **Permitir cookies**
- **Permitir script ativo**

#### <a name="app-settings"></a>Configurações do aplicativo
- **Permitir Google Play Store**

#### <a name="device-capability-settings"></a>Configurações de funcionalidade do dispositivo
- **Permitir armazenamento removível**
- **Permitir compartilhamento de Internet por Wi-Fi**
- **Permitir geolocalização**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir roaming de voz**
- **Permitir roaming de dados**
- **Permitir mensagens SMS/MMS**
- **Permitir assistência de voz**
- **Permitir discagem por voz**
- **Permitir copiar e colar**

### <a name="new-settings-for-ios-devices"></a>Novas configurações para dispositivos iOS
#### <a name="password-settings"></a>Configurações de senha
- **Número de caracteres complexos necessários na senha**
- **Permitir senha simples**
- **Minutos de inatividade antes de a senha ser necessária**
- **Lembrar histórico de senha**

### <a name="new-settings-for-mac-os-x-devices"></a>Novas configurações para dispositivos Mac OS X
#### <a name="password-settings"></a>Configurações de senha
- **Número de caracteres complexos necessários na senha**
- **Permitir senha simples**
- **Lembrar histórico de senha**
- **Minutos de inatividade antes que o protetor de tela seja ativado**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Novas configurações para dispositivos Windows 10 Desktop e Mobile
#### <a name="password-settings"></a>Configurações de senha
- **Número mínimo de conjuntos de caracteres**
- **Lembrar histórico de senha**
- **Exigir uma senha quando o dispositivo volta do estado ocioso**

#### <a name="security-settings"></a>Configurações de segurança
- **Exigir criptografia no dispositivo móvel**
- **Permitir cancelamento de registro manual**

#### <a name="device-capability-settings"></a>Configurações de funcionalidade do dispositivo
- **Permitir VPN por celular**
- **Permitir roaming de VPN no celular**
- **Permitir a redefinição do telefone**
- **Permitir conexão USB**
- **Permitir Cortana**
- **Permitir notificações da central de ações**

### <a name="new-settings-for-windows-10-team-devices"></a>Novas configurações para os dispositivos do Windows 10 Team
#### <a name="device-settings"></a>Configurações do dispositivo
- **Habilitar Azure Operational Insights**
- **Habilitar projeção sem fio Miracast**
- **Escolher as informações da reunião exibidas na tela de boas-vindas**
- **URL da imagem de tela de fundo da tela de bloqueio**

### <a name="new-settings-for-windows-81-devices"></a>Novas configurações para dispositivos Windows 8.1
#### <a name="applicability-settings"></a>Configurações de aplicabilidade
- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Configurações de senha
- **Tipo de senha necessária**
- **Número mínimo de conjuntos de caracteres**
- **Tamanho mínimo da senha**
- **Número de falhas de entrada repetidas permitidas antes que o dispositivo seja apagado**
- **Minutos de inatividade antes que a tela seja desligada**
- **Expiração da senha (dias)**
- **Lembrar histórico de senha**
- **Evitar a reutilização de senhas anteriores**
- **Permitir PIN e senha com imagem**

#### <a name="browser-settings"></a>Configurações do navegador
- **Permitir detecção automática da rede intranet**

### <a name="new-settings-for-windows-phone-81-devices"></a>Novas configurações para dispositivos Windows Phone 8.1
#### <a name="applicability-settings"></a>Configurações de aplicabilidade
- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Configurações de senha
- **Número mínimo de conjuntos de caracteres**
- **Permitir senha simples**
- **Lembrar histórico de senha**

#### <a name="device-capability-settings"></a>Configurações de funcionalidade do dispositivo
- **Permitir conexão automática a pontos de acesso Wi-Fi gratuitos**
