---
title: Novidades no 1606 | System Center Configuration Manager
description: "Veja os detalhes das alterações e os novos recursos introduzidos na versão 1606 do System Center Configuration Manager."
ms.custom: na
ms.date: 10/09/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
caps.latest.revision: 40
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: 8de28e112a2d7faf1d8aca9b7214498e9a65f919

---
# <a name="what39s-new-in-version-1606-of-system-center-configuration-manager"></a>Novidades da versão 1606 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A atualização 1606 do System Center Configuration Manager é uma atualização que está disponível como uma atualização no console para sites instalados anteriormente que executam a versão 1511 ou 1602. A versão 1511 é a versão de linha de base inicial usada para instalar novos sites do Configuration Manager.
> [!TIP]  
>  Saiba mais sobre:  
>   
>  -   [Instalação de novos sites](/sccm/core/servers/deploy/install) (usando uma versão de linha de base como a 1511)  
>  -   [Instalação de atualizações em sites](/sccm/core/servers/manage/updates) (como a atualização 1602 ou 1606)  

 As seções a seguir fornecem detalhes sobre as alterações e novas funcionalidades introduzidas na versão 1606 do Configuration Manager.  



## <a name="a-nameupdatesandservicingaupdates-and-servicing"></a><a name="updatesandservicing"></a>Atualizações e manutenção

### <a name="changes-for-the-updates-and-servicing-node"></a>Alterações no nó Atualizações e Manutenção
Estas são as alterações para Atualizações e Manutenção no console do Configuration Manager:
> [!NOTE]
> Essas alterações não estarão disponíveis até que você instale a versão 1606.

- **Alteração de nome de nó:**

    No espaço de trabalho **Monitoramento**, o nó **Status de Manutenção do Site** foi renomeado para **Status de Serviço e Atualizações**.
- **Mais status da instalação:**

    Quando você exibe o status da instalação da atualização para um site, agora o console mostra detalhes separados para as seguintes ações:
    - **Baixar** (isso se aplica somente ao site de nível superior em que a função do sistema de sites do ponto de conexão de serviço está instalado)
    - **Replicação**
    - **Verificação de pré-requisitos**
    - **Instalação**

  Além disso, agora há informações mais detalhadas para cada etapa, incluindo qual arquivo de log você pode exibir para obter mais informações.  
-   **Nova opção para repetir as falhas de pré-requisito:**

    Nos espaços de trabalho **Administração** e **Monitoramento**, o nó **Atualizações e Manutenção** inclui um novo botão na Faixa de opções chamado **	Ignorar avisos de pré-requisito**.

    Ao instalar atualizações sem usar a opção de Ignorar avisos de pré-requisito (de dentro do Assistente de Atualizações), e a instalação da atualização for interrompida com um estado de **Prereq warning (Aviso de pré-requisito)**, você poderá selecionar **Ignorar avisos de pré-requisito** na faixa de opções para disparar uma continuação automática da instalação da atualização que ignora os avisos de pré-requisito.  



- **Exibição mais clara das atualizações:**

    Ao ver o nó **Atualizações e Manutenção**, agora você pode visualizar apenas as atualizações instaladas mais recentemente e quaisquer atualizações que estejam disponíveis para instalação. Para exibir atualizações instaladas anteriormente, clique no novo botão **Histórico**, que aparece na faixa de opções.  

-   **Opção renomeada para pré-produção:**

    No nó Atualizações e Manutenção, o botão chamado **Client options (Opções do cliente)** agora foi renomeado para **Promover o Cliente de Pré-produção**.


###  <a name="pre-release-features"></a>Recursos de pré-lançamento
A partir da 1606, você deverá dar consentimento para usar Recursos de pré-lançamento no System Center Configuration Manager antes de selecionar e habilitar seu uso. Para obter mais informações, consulte [Usar recursos de pré-lançamento de atualizações](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="new-distribution-point-update-behavior"></a>Novo comportamento de atualização de ponto de distribuição
A atualização 1606 introduz alterações para melhorar a disponibilidade de pontos de distribuição ao instalar atualizações futuras.

Após a atualização 1606 ser instalada, quando você instalar uma nova atualização no site que requer a reinstalação automática das funções de sistema de sites do ponto de distribuição por pull e padrão, todos os pontos de distribuição não ficam mais offline para atualizar ao mesmo tempo. Em vez disso, o servidor do site usa as configurações de distribuição de conteúdo do site para distribuir a atualização para um subconjunto de pontos de distribuição por vez. O resultado é que apenas alguns pontos de distribuição ficam offline para instalar a atualização. Isso permite que pontos de distribuição que ainda não começaram a ser atualizados ou que concluíram a atualização permaneçam online e forneçam conteúdo aos clientes.



## <a name="a-nameaccessibilitya-accessibility"></a><a name="accessibility"></a> Acessibilidade
A partir da versão 1606, para navegar entre os diferentes nós de um espaço de trabalho, você pode inserir a primeira letra do nome do nó. Cada tecla pressionada move o cursor para o próximo nó que começa com a letra dessa tecla e, ao usar um leitor de tela, o leitor lê o nome do nó. Para mais informações sobre opções de acessibilidade, confira [Accessibility features in System Center Configuration Manager](../../../core/understand/accessibility-features.md) (Recursos de acessibilidade no System Center Configuration Manager).

## <a name="a-nameadministrationaadministration"></a><a name="administration"></a>Administração
Estas são as alterações para a Administração no console do Configuration Manager:
### <a name="oms-connector"></a>Conector do OMS

Agora você pode conectar o Configuration Manager como coleções do System Center Configuration Manager ao [OMS (Microsoft Operations Management Suite)](https://azure.microsoft.com/en-us/documentation/articles/operations-management-suite-overview/). Isso torna dados como coleções da implantação do Configuration Manager visíveis no OMS. Saiba mais sobre a [sincronização de dados do Configuration Manager com o Microsoft Operations Management Suite aqui](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md).

O conector do OMS é um recurso de pré-lançamento. Para habilitá-lo, confira [Use pre-release features from updates](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease) (Usar recursos de pré-lançamento de atualizações).

### <a name="support-for-cache-size-in-client-settings"></a>Suporte para o tamanho do cache nas Configurações do Cliente

Agora você pode configurar o tamanho da pasta de cache em computadores cliente com as Configurações do Cliente no console do Configuration Manager. Anteriormente, você poderia definir o tamanho do cache do cliente apenas ao instalar ou reinstalar o software cliente (usando a propriedade SMSCACHESIZE). Agora você pode especificar o tamanho do cache como uma configuração de cliente (padrão ou personalizada) e, então, aplicar essas configurações com a próxima atualização de política no cliente sem a necessidade de reinstalar o cliente. Para mais informações, consulte [Configurar o cache do cliente para clientes do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Gerenciamento de dispositivo móvel local

### <a name="support-for-multiple-device-management-points"></a>Suporte para vários ponto de gerenciamento de dispositivos

O MDM (Gerenciamento de Dispositivo Móvel) local agora dá suporte a uma nova funcionalidade na Atualização de Aniversário do Windows 10 que configura automaticamente um dispositivo registrado para ter mais de um ponto de gerenciamento de dispositivos disponível para uso. Essa funcionalidade permite que o dispositivo realize o fallback para outro ponto de gerenciamento de dispositivos quando o que ele usa normalmente não estiver disponível. Essa funcionalidade funciona apenas para computadores e dispositivos com a Atualização de Aniversário do Windows 10 instalada.


## <a name="application-management"></a>Gerenciamento de aplicativos

### <a name="manage-apps-from-the-windows-store-for-business"></a>Gerenciar aplicativos da Windows Store para Empresas

Na [Windows Store para Empresas](https://www.microsoft.com/business-store), é possível encontrar e adquirir aplicativos Windows para sua organização, individualmente ou por volume. Conectando a loja ao Configuration Manager, você pode sincronizar a lista de aplicativos que comprou com o Configuration Manager, vê-los no console do Configuration Manager e implantá-los como faria com qualquer outro aplicativo.

Para obter detalhes, confira [Gerenciar aplicativos da Windows Store para Empresas com o System Center Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Gerenciar aplicativos iOS adquiridos por volume

O fluxo de trabalho para gerenciar aplicativos iOS adquiridos por volume e implantar esses aplicativos com o Configuration Manager foi aprimorado.

Para obter detalhes, consulte [Gerenciar aplicativos iOS adquiridos por volume com o System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).

### <a name="software-center-user-interface"></a>Interface do usuário do Centro de Software

A interface do Centro de Software foi otimizada para facilitar a experiência de navegar do usuário final.
*  As guias **Status da Instalação** e **Software Instalado** foram combinadas em uma única guia **Status da Instalação**.
*  **Atualizações**, **Sistemas Operacionais** e **Aplicativos** foram separados em três guias separadas.
* Agora é possível selecionar várias atualizações de uma vez ou é possível instalar todas as atualizações de uma vez clicando no botão **Instalar Tudo**.

### <a name="content-status-links"></a>Links de status do conteúdo
Ao exibir as propriedades de um aplicativo ou pacote, agora há um link que leva você até o status desse objeto.

## <a name="software-updates"></a>Atualizações de software

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Configuração do cliente para gerenciar o agente cliente do Office 365
Agora você pode usar uma configuração de cliente do Configuration Manager para gerenciar o agente cliente do Office 365. Depois de definir essa configuração e implantar as atualizações do Office 365, o agente cliente do Configuration Manager se comunica com o agente cliente do Office 365 para baixar atualizações do Office 365 de um ponto de distribuição e instalá-las.

Para obter detalhes, confira [Manage Office 365 ProPlus updates with Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md) (Gerenciar atualizações do Office 365 ProPlus com o Configuration Manager).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Mudar manualmente clientes para um novo ponto de atualização de software
Agora você pode habilitar a opção para clientes do Configuration Manager mudarem para um novo ponto de atualização de software quando houver problemas com o ponto de atualização de software ativo. Uma vez habilitada, os clientes procurarão outro ponto de atualização de software na próxima verificação.

Para obter detalhes, confira [Plan for software updates in Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs) (Planejar atualizações de software no Configuration Manager).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Opções de reinício para clientes do Windows 10 após a instalação da atualização de software
Quando uma atualização de software que requer reinicialização é implantada usando o Configuration Manager e é instalada em um computador, uma reinicialização pendente é agendada e uma caixa de diálogo de reinicialização é exibida. A partir da versão 1606 do Configuration Manager, as opções **Atualizar e Reiniciar**e **Atualizar e Desligar** estão disponíveis em computadores Windows 10, nas opções de energia do Windows, sempre que houver uma reinicialização pendente para uma atualização de software do Configuration Manager. Depois de usar uma dessas opções, a caixa de diálogo de reinicialização não será exibida após o computador reiniciar.

Para obter detalhes, confira [Plan for software updates in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions) (Planejar atualizações de software no System Center Configuration Manager).

## <a name="operating-system-deployment"></a>Implantação de sistema operacional

### <a name="improvements-to-the-install-software-updates-task-sequence-step"></a>Melhorias na etapa da sequência de tarefas de Instalar Atualizações de Software
Há uma nova configuração, **Avaliar as atualizações de software dos resultados da varredura em cache**, que oferece a opção de realizar uma varredura completa para atualizações de software em vez de usar os resultados de varredura armazenados em cache. Para obter detalhes, confira [Etapas da sequência de tarefas no System Center Configuration Manager](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

Além disso, uma nova variável de sequência de tarefas, **SMSTSSoftwareUpdateScanTimeout**, está disponível para oferecer a capacidade de controlar o tempo limite para a varredura de atualizações de software durante a etapa de sequência de tarefas de Instalar atualizações de software. O valor padrão é 30 minutos. Para obter detalhes, confira [Task sequence built-in variables in System Center Configuration Manager](../../../osd/understand/task-sequence-built-in-variables.md) (Variáveis internas de sequência de tarefas no System Center Configuration Manager).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>A variável de sequência de tarefas OSDPreserveDriveLetter foi preterida
A partir da versão 1606 do Configuration Manager, a variável de sequência de tarefas OSDPreserveDriveLetter foi preterida. A partir da versão 1606 do Configuration Manager, a Instalação do Windows determina a melhor letra da unidade a ser usada (normalmente C:) durante uma implantação de sistema operacional, por padrão.

Para obter detalhes, confira [Task sequence built-in variables in System Center Configuration Manager](../../../osd/understand/task-sequence-built-in-variables.md) (Variáveis internas de sequência de tarefas no System Center Configuration Manager).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Personalizar o tamanho da janela do RamDisk TFTP para pontos de distribuição habilitados para PXE
Agora você pode personalizar o tamanho da janela do RamDisk para pontos de distribuição habilitados para PXE. Se você tiver personalizado sua rede, isso poderá fazer com que o download da imagem de inicialização falhe com um erro de tempo limite devido ao tamanho da janela ser muito grande. A personalização do tamanho da janela do RamDisk TFTP permite otimizar o tráfego TFTP ao usar o PXE para atender aos seus requisitos de rede específicos.

Para obter detalhes, confira [Prepare site system roles for operating system deployments with System Center Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP) (Preparar as funções do sistema de sites para implantações de sistema operacional com o System Center Configuration Manager).

## <a name="compliance-settings"></a>Configurações de conformidade

### <a name="smart-lock-setting-for-android-devices"></a>Configuração do SmartLock para dispositivos Android
Uma nova configuração, **Permitir Smart Lock e outros agentes de confiança**, foi adicionada ao item de configuração do Android e Samsung KNOX.

Essa configuração permite controlar o recurso Smart Lock em dispositivos Android compatíveis. Essa capacidade do telefone, às vezes conhecida como agentes de confiança, permite desabilitar ou ignorar a senha da tela de bloqueio do dispositivo se o dispositivo estiver em um local confiável, como quando ele está conectado a um dispositivo Bluetooth específico, ou quando ele está perto de uma marca NFC. Você pode usar essa configuração para impedir que usuários finais configurem o Smart Lock.

Para obter detalhes, consulte [Como criar itens de configuração para dispositivos Android e Samsung KNOX gerenciados sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).

## <a name="device-configuration-and-protection"></a>Configuração e proteção do dispositivo

### <a name="product-name-changes"></a>Alterações do nome do produto

* O Microsoft Passport for Work agora é conhecido como **Windows Hello para Empresas**.
* A proteção de dados corporativos agora é conhecida como **Proteção de Informações do Windows**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Implantação do Windows Hello para Empresas (Passport for Work)

Agora você pode implantar as políticas do Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio gerenciados pelo cliente do Configuration Manager.

O console do Configuration Manager foi atualizado para refletir essas alterações.

### <a name="ios-activation-lock"></a>Bloqueio de Ativação do iOS
O Configuration Manager pode ajudar a gerenciar o Bloqueio de Ativação do iOS, um recurso do aplicativo Buscar meu iPhone para dispositivos iOS 7.1 e posteriores. Depois que o Bloqueio de Ativação for habilitado, a ID da Apple e a senha do usuário deverão ser inseridas antes que qualquer pessoa possa:
* Desligar o Buscar meu iPhone
* Apagar o dispositivo
* Reativar o dispositivo

O Configuration Manager pode ajudar a gerenciar o Bloqueio de Ativação de duas maneiras:

1. habilitar o Bloqueio de Ativação em dispositivos supervisionados.
2. ignorar o Bloqueio de Ativação em dispositivos supervisionados.

Para obter detalhes, confira [Manage iOS Activation Lock with System Center Configuration Manager](../../../mdm/deploy-use/manage-ios-activation-lock.md) (Gerenciar o Bloqueio de Ativação do iOS com o System Center Configuration Manager)


### <a name="windows-defender-advanced-threat-protection"></a>Proteção Avançada contra Ameaças do Windows Defender

O Endpoint Protection pode ajudar a gerenciar e monitorar a ATP (Proteção Avançada contra Ameaças) do Windows Defender. A ATP do Windows Defender é um novo serviço que ajudará as empresas a detectar, investigar e responder a ataques avançados em suas redes. Políticas do Configuration Manager podem ajudar a carregar e monitorar o Windows 10, versão 1607 (build 14328) ou posterior gerenciado.

Para obter detalhes, confira [Windows Defender Advanced Threat Protection](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md) (Proteção Avançada contra Ameaças do Windows Defender).

### <a name="device-categories"></a>Categorias de dispositivos
Você pode criar categorias de dispositivos, que podem ser usadas para colocar automaticamente os dispositivos em coleções de dispositivos ao usar o Configuration Manager com o Microsoft Intune. Os usuários devem, então, escolher uma categoria de dispositivo ao registrar um dispositivo no Intune. Além disso, você pode alterar a categoria de um dispositivo do console do Configuration Manager.

Para obter detalhes, confira [Como categorizar automaticamente os dispositivos em coleções com o System Center Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com número de série do iOS ou IMEI

Você pode identificar os dispositivos corporativos importando seus números IMEI (identidade internacional de equipamento móvel) ou números de série do iOS. Você pode carregar um arquivo .csv (valores separados por vírgula) que contém os números IMEI do dispositivo ou inserir manualmente as informações sobre o dispositivo. As informações importadas definirão a **Propriedade** dos dispositivos que registram como "**Corporativo**" nas listas de dispositivos. Uma licença do Intune ainda é necessária para cada usuário que acessa o serviço.

Para detalhes, confira [Pré-declarar dispositivos com número de série do iOS ou IMEI](../../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).

### <a name="on-premises-health-attestation-service-communication"></a>Comunicação de serviço de Atestado de Integridade local

Agora você pode habilitar o monitoramento de serviços de Atestado de Integridade para computadores com Windows 10 usando apenas a infraestrutura local para que computadores sem acesso à Internet possam relatar o DHA (Atestado de Integridade do Dispositivo).

Para obter detalhes, consulte [Atestado de integridade do System Center Configuration Manager](../../../core/servers/manage/health-attestation.md#How-to-enable-Health-Attestation-service-communication-on-Configuration-Manager-client-computers).  

## <a name="remote-control"></a>Controle remoto
Conceda os seus usuários finais a oportunidade de aceitar ou negar transferências de arquivo antes de transferir conteúdo da área de transferência compartilhada em uma seção de controle remoto. Os usuários finais precisarão apenas conceder a permissão uma vez por sessão e o visualizador não terá a capacidade de conceder a si mesmo a permissão para prosseguir com a transferência de arquivos. Você pode encontrar essa nova configuração no espaço de trabalho **Administração**, em seguida, navegar para **Configurações do Cliente**, em seguida abrir o painel **Ferramentas Remotas** em **Configurações Padrão**.



<!--HONumber=Nov16_HO1-->


