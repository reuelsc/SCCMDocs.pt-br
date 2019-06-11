---
title: Novidades na versão 1902
titleSuffix: Configuration Manager
description: Obtenha os detalhes sobre as alterações e as novas funcionalidades incluídas na versão 1902 do Branch Atual do Configuration Manager.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6b2468dc5f4cf7a9e1a715b3ec8e8a1d912a12b0
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66354884"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Novidades da versão 1902 do Branch Atual do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A atualização 1902 do Branch Atual do Configuration Manager está disponível como uma atualização no console. Aplique essa atualização em sites que executam a versão 1802, 1806 ou 1810. <!-- baseline only statement:-->Ao instalar um novo site, ela também está disponível como uma versão de linha de base. Este artigo resume as alterações e os novos recursos no Configuration Manager, versão 1902.  

Sempre examine a lista de verificação mais recente para instalar essa atualização. Confira mais informações em [Lista de verificação para a instalação da atualização 1902](/sccm/core/servers/manage/checklist-for-installing-update-1902). Depois de atualizar um site, examine também a [Lista de verificação pós-atualização](/sccm/core/servers/manage/checklist-for-installing-update-1902#post-update-checklist).

Para aproveitar ao máximo os novos recursos do Configuration Manager, depois de atualizar o site, atualize também os clientes para a versão mais recente. Embora a nova funcionalidade seja exibida no console do Configuration Manager quando você atualiza o site e o console, o cenário completo só funcionará quando a versão do cliente também for a mais recente.

> [!Note]  
> Atualmente, esse artigo lista todos os recursos importantes nesta versão. No entanto, nem todas as seções ainda se vinculam ao conteúdo atualizado com informações adicionais sobre os novos recursos. Continue verificando esta página regularmente para ver se há atualizações. As alterações são indicadas com a marcação ***[Atualizado]***. Essa observação será removida quando o conteúdo for finalizado.  

> [!Tip]  
> Para ser notificado quando esta página for atualizada, copie e cole a seguinte URL em seu leitor de feeds de RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`



## <a name="bkmk_deprecated"></a> Sistemas operacionais e recursos preteridos

Saiba mais sobre alterações de suporte antes que elas sejam implementadas em [itens removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

- A implementação para o compartilhamento de conteúdo do Azure foi alterada. Use um gateway de gerenciamento de nuvem habilitado para conteúdo ativando a opção **Permitir que o CMG funcione como um ponto de distribuição de nuvem e forneça conteúdo do armazenamento do Azure**. Você não poderá criar um ponto de distribuição de nuvem tradicional no futuro.

A versão 1902 descarta o suporte para os seguintes produtos:  

- Linux e UNIX como cliente. A reprovação foi anunciada com a [versão 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802#deprecation-announcement-for-linux-and-unix-client-support). Considere o Gerenciamento do Microsoft Azure para gerenciar servidores Linux. As soluções do Azure têm amplo suporte para Linux que, na maioria dos casos, supera a funcionalidade do Configuration Manager, incluindo o gerenciamento de patches de ponta a ponta para o Linux.



## <a name="bkmk_infra"></a> Infraestrutura do site

### <a name="client-health-dashboard"></a>Painel de integridade do cliente
<!--3599209-->
Você implanta as atualizações de software e outros aplicativos para ajudar a proteger seu ambiente, mas essas implantações alcançam apenas os clientes íntegros. Os clientes não íntegros do Configuration Manager prejudicam a conformidade geral. A determinação da integridade do cliente pode ser um desafio dependendo do denominador: que número total de dispositivos deve estar no seu escopo de gerenciamento? Por exemplo, se você descobrir todos os sistemas do Active Directory, mesmo que alguns desses registros sejam de computadores desativados, esse processo aumentará o denominador. 

Agora você pode exibir um painel com informações sobre a integridade dos clientes do Configuration Manager em seu ambiente. Exiba a integridade do cliente, a integridade do cenário e erros comuns. Filtre a exibição por vários atributos para ver possíveis problemas pelas versões do sistema operacional e do cliente. 

No console do Configuration Manager, acesse o workspace **Monitoramento**. Expanda **Status do cliente** e selecione o nó **Painel de integridade do cliente**. 

![Captura de tela do painel de integridade do cliente](media/3599209-client-health-dashboard.png)

<!-- For more information, see [How to monitor clients](/sccm/core/clients/manage/monitor-clients). -->


### <a name="new-management-insight-rules"></a>Novas regras de insight de gerenciamento
O recurso de insights de gerenciamento tem as seguintes regras novas:

- Várias regras com recomendações sobre como gerenciar coleções. Use esses insights para simplificar o gerenciamento e melhorar o desempenho. Examine essas novas regras no grupo **Coleções**.<!--3555752-->  

- Regra de **Atualização de clientes para uma versão com suporte para o Windows 10** no grupo **Gerenciamento Simplificado**. Esta regra relata os clientes que estão executando uma versão do Windows 10 que não têm mais suporte. Ela também inclui os clientes com uma versão do Windows 10 que esteja perto do fim do serviço (três meses).<!--3897268-->  

<!-- For more information, see [Management insights](/sccm/core/servers/manage/management-insights). -->


### <a name="improvement-to-enhanced-http"></a>Melhoria no HTTP aprimorado

<!--3798957-->

***[Atualizado]*** Agora, você pode habilitar o HTTP aprimorado por site primário ou para o site de administração central.

Nas propriedades do site de administração central, selecione a opção para **Usar certificados gerados pelo Configuration Manager para sistemas de site HTTP**. Essa configuração só se aplica às funções do sistema de site no site de administração central. Não é uma configuração global para a hierarquia.

Para saber mais, confira [HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http).


### <a name="improvement-to-setup-prerequisites"></a>Melhorias nos pré-requisitos de instalação
Quando você instala a versão 1902 ou faz a atualização para essa versão, a instalação do Configuration Manager agora inclui as verificações de pré-requisitos a seguir:

- **Reinicialização do sistema pendente no SQL Server remoto**: essa verificação de pré-requisito é semelhante à regra de **Reinicialização pendente do sistema**, mas ela verifica o SQL Server remoto. Para saber mais, confira a [Lista de verificações de pré-requisitos](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#pending-system-restart-on-the-remote-sql-server). <!--SCCMDocs-pr issue 3377-->  



## <a name="bkmk_cloud"></a> Gerenciamento conectado à nuvem

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>Interromper o serviço de nuvem quando ele exceder o limite
<!--3735092-->
Agora, o Configuration Manager pode parar um serviço CMG (Gateway de Gerenciamento de Nuvem) quando a transferência de dados total ultrapassar o limite. O CMG sempre teve alertas para disparar notificações quando o uso atingia níveis de aviso ou críticos. Para ajudar a reduzir os custos inesperados do Azure devido a um aumento do uso, esta nova opção desabilita o serviço de nuvem. 

[Configurar os alertas de tráfego de saída](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#set-up-outbound-traffic-alerts) no CMG e, então, habilitar a opção para **Interromper esse serviço quando ele exceder o limite crítico**.  

<!-- For more information, see [Set up outbound traffic alerts](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#set-up-outbound-traffic-alerts). -->


### <a name="use-azure-resource-manager-for-cloud-services"></a>Usar o Azure Resource Manager para os serviços de nuvem
<!--3605704-->
A partir da versão 1810, a implantação de serviço clássico no Azure é preterida para uso no Configuration Manager. Essa versão é a última compatível com a criação dessas implantações do Azure. 

As implantações existentes continuam a funcionar. A partir dessa versão do Branch Atual, o Azure Resource Manager é o único mecanismo de implantação para novas instâncias do ponto de distribuição de nuvem e do Gateway de Gerenciamento de Nuvem.

<!-- For more information, see [Azure Resource Manager for the cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).   -->


### <a name="add-cloud-management-gateway-to-boundary-groups"></a>Adicionar o Gateway de Gerenciamento de Nuvem a grupos de limites
<!--3640932-->
Já é possível associar um gateway de gerenciamento de nuvem (CMG) a um grupo de limites. Essa configuração permite que os clientes façam fallback ou voltem ao CMG padrão para comunicações de cliente de acordo com os relacionamentos de grupos de limite. Esse comportamento é especialmente útil em cenários de VPN e de branch do Office. É possível direcionar o tráfego do cliente para longe de links WAN caros e lentos e, em vez disso, usar os links de internet mais rápidos do Microsoft Azure.

<!-- For more information, see [Plan for the CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). -->



## <a name="bkmk_real"></a> Gerenciamento em tempo real

### <a name="run-cmpivot-from-the-central-administration-site"></a>Executar o CMPivot no site de administração central
<!--3610960-->
***[Atualizado]*** O Configuration Manager agora dá suporte à execução do CMPivot por meio do site de administração central em uma hierarquia. O site primário ainda gerencia a comunicação com o cliente. Quando o CMPivot é executado do site de administração central, ele se comunica com o site primário pelo canal de assinatura de mensagem de alta velocidade. Essa comunicação não depende da replicação padrão do SQL entre sites.

Para obter mais informações, confira [CMPivot para dados em tempo real](/sccm/core/servers/manage/cmpivot#bkmk_cmpivot1902).


### <a name="edit-or-copy-powershell-scripts"></a>Editar ou copiar scripts do PowerShell
<!--3705507-->
Agora é possível **Editar** ou **Copiar** um script existente do PowerShell usado com o recurso Executar Scripts. Em vez de recriar um script que você precisa alterar, agora pode editá-lo diretamente. As duas ações usam a mesma experiência do assistente de quando você cria um novo script. Quando você edita ou copia um script, o Configuration Manager não persiste o estado de aprovação. 

<!-- For more information, see [Run Scripts](/sccm/apps/deploy-use/create-deploy-scripts). -->



## <a name="bkmk_content"></a> Gerenciamento de conteúdo

### <a name="distribution-point-maintenance-mode"></a>Modo de manutenção do ponto de distribuição

<!--3555754-->

***[Atualizado]*** Agora, você pode definir um ponto de distribuição no modo de manutenção. Habilite o modo de manutenção quando você estiver instalando atualizações de software ou fazendo alterações de hardware no servidor.

Enquanto o ponto de distribuição está no modo de manutenção, ele tem os seguintes comportamentos:

- o site não distribui nenhum conteúdo para ele.  

- os pontos de gerenciamento não retornam o local desse ponto de distribuição aos clientes.

- quando você atualiza o site, um ponto de distribuição no modo de manutenção ainda é atualizado.

- as propriedades do ponto de distribuição são somente leitura. Por exemplo, você não pode alterar o certificado ou adicionar grupos de limites.  

- qualquer tarefa agendada, como validação de conteúdo, ainda é executada no mesmo agendamento.

Para saber mais sobre este recurso, confira o tópico [Modo de manutenção](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_maint).

Para saber mais sobre como automatizar este processo com o SDK do Configuration Manager, confira [Método SetDPMaintenanceMode na classe SMS_DistributionPointInfo](/sccm/develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo).



## <a name="bkmk_client"></a> Gerenciamento de cliente

### <a name="client-provisioning-mode-timeout"></a>Tempo limite do modo de provisionamento do cliente

<!--3197824-->
***[Atualizado]*** A sequência de tarefas define um carimbo de data/hora quando coloca o cliente no modo de provisionamento. Um cliente no modo de provisionamento verifica a duração de tempo a cada 60 minutos desde o carimbo de data/hora. Se o cliente estiver no modo de provisionamento a mais de 48 horas, ele sairá automaticamente do modo de provisionamento e reiniciará seu processo.

Para saber mais, confira o tópico [Modo de provisionamento](/sccm/osd/understand/provisioning-mode).

### <a name="view-first-screen-only-during-remote-control"></a>Exibir a primeira tela somente durante o controle remoto
<!--3231732-->
***[Atualizado]*** Ao se conectar a um cliente com dois ou mais monitores, pode ser difícil visualizar todos eles no visualizador de controle remoto do Configuration Manager. O operador de ferramentas remotas pode agora escolher entre visualizar **Todas as telas** ou apenas a **Primeira tela**.

Para obter mais informações, consulte [Como administrar remotamente um computador de cliente do Windows](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer). 


### <a name="specify-a-custom-port-for-peer-wakeup"></a>Especificar uma porta personalizada para ativação de par
<!--3605925-->
***[Atualizado]***  Agora você pode especificar um número da porta personalizado para o proxy de ativação. Nas configurações do cliente, no grupo **Gerenciamento de energia**, defina a configuração para **Número de porta Wake On LAN (UDP)** .  

Para saber mais, confira [Como configurar o Wake On LAN](/sccm/core/clients/deploy/configure-wake-on-lan).



<!-- ## <a name="bkmk_comgmt"></a> Co-management -->




<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->



## <a name="bkmk_app"></a> Gerenciamento de aplicativos

### <a name="improvements-to-application-approvals-via-email"></a>Melhorias nas aprovações de aplicativo por email

<!--3594063-->
***[Atualizado]*** Esta versão apresenta melhorias ao recurso para receber notificações por email das solicitações de aplicativos. Os usuários sempre puderam adicionar um comentário à solicitação no Centro de Software. Este comentário é exibido na solicitação do aplicativo no console do Configuration Manager. Agora esse comentário também é exibido no email. Incluir este comentário no email ajuda os aprovadores a tomarem uma decisão melhor para aprovar ou negar a solicitação.

Para saber mais, confira o tópico [Notificações por email](/sccm/apps/deploy-use/app-approval#bkmk_email-approve).


### <a name="improvements-to-package-conversion-manager"></a>Melhorias no Package Conversion Manager
<!-- SCCMDocs-pr issue #3357 -->
Esta versão inclui as seguintes melhorias ao [Package Conversion Manager](/sccm/apps/pcm/package-conversion-manager):
- A análise de pacote agendada é executada a cada 7 dias por padrão
- Cmdlets do PowerShell para analisar e converter pacotes
- Melhorias e correções de bug gerais



## <a name="bkmk_osd"></a> Implantação do sistema operacional


### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>Status do andamento durante a sequência de tarefas de atualização in-loco
<!--3747129-->
Agora você pode ver uma barra de progresso mais detalhada durante uma sequência de tarefas de atualização in-loco do Windows 10. Essa barra mostra o andamento da instalação do Windows, que normalmente é silenciosa durante a sequência de tarefas. Os usuários agora têm alguma visibilidade sobre o andamento subjacente. Isso ajuda em caso de preocupações de que o processo de atualização esteja suspenso por causa da falta de indicação de andamento.  

![Exemplo de andamento da sequência de tarefas com o progresso da atualização do Windows](media/3747129-installation-progress.png)

Esse recurso funciona com qualquer versão do Windows 10 com suporte e somente com a sequência de tarefas de atualização in-loco. 


### <a name="improvements-to-task-sequence-media-creation"></a>Melhorias na criação de mídia de sequência de tarefas

<!--3556027, fka 1359388-->
***[Atualizado]*** Esta versão inclui várias melhorias para ajudá-lo a criar e gerenciar de maneira melhor a mídia de sequência de tarefas. Para saber mais, confira os seguintes artigos sobre tipos de mídia específicos:

- [Criar mídia autônoma](/sccm/osd/deploy-use/create-stand-alone-media)
- [Criar mídia pré-configurada](/sccm/osd/deploy-use/create-prestaged-media)
- [Criar mídia inicializável](/sccm/osd/deploy-use/create-bootable-media)
- [Criar mídia de captura](/sccm/osd/deploy-use/create-capture-media)

#### <a name="specify-temporary-storage"></a>Especificar armazenamento temporário

Agora, quando você cria a mídia de sequência de tarefas, personalize a localização que seu site usa para armazenamento temporário de dados. Esse processo pode exigir muito espaço de unidade temporária. Essa alteração oferece maior flexibilidade para escolher em que local armazenar esses arquivos temporários.

No **Assistente Criar Mídia de Sequência de Tarefas**, especifique uma localização para a **Pasta de preparo**. Por padrão, essa localização é semelhante ao seguinte caminho: `%UserProfile%\AppData\Local\Temp`.

#### <a name="add-a-label-to-the-media"></a>Adicione um rótulo à mídia

Agora você pode adicionar um rótulo à mídia de sequência de tarefas. Esse rótulo ajuda a identificar melhor a mídia depois de criá-la. No **Assistente Criar Mídia de Sequência de Tarefas**, especifique um **Rótulo de mídia**.

#### <a name="include-autoruninf-file-on-media"></a>Incluir arquivo autorun.inf na mídia

<!-- 4090666 -->
Quando você cria a mídia de sequência de tarefas, o Configuration Manager não adiciona um arquivo autorun.inf. Normalmente, esse arquivo é bloqueado por produtos antimalware. Você ainda pode incluir o arquivo se necessário para seu cenário.


### <a name="import-a-single-index-of-an-os-image"></a>Importar um índice único de uma imagem do sistema operacional

<!--3719699-->
***[Atualizado]*** Ao importar um arquivo de imagem (WIM) do Windows para o Configuration Manager, você já pode especificar a importação automática de um único índice, em vez de todos os índices de imagem no arquivo. Essa opção oferece os seguintes benefícios:

- arquivo de imagem menor  
- serviço offline mais rápido  
- Otimizar o serviço de imagens, para um arquivo de imagem menor após o serviço offline

Ao importar uma imagem de um sistema operacional, selecione a opção **Extrair um índice de imagem específico do arquivo WIM especificado**. Em seguida, selecione o índice de imagem na lista.  

Para saber mais, confira o tópico [Adicionar uma imagem do sistema operacional](/sccm/osd/get-started/manage-operating-system-images#BKMK_AddOSImages).


### <a name="optimized-image-servicing"></a>Serviço de imagens otimizado

<!--3555951-->
***[Atualizado]*** Quando você aplica as atualizações de software a uma imagem do sistema operacional, há uma nova opção para otimizar a saída, removendo as atualizações substituídas. A otimização do serviço offline só se aplica a imagens com um único índice.

Ao criar um agendamento para atualizar um sistema operacional, selecione a opção **Remover atualizações substituídas depois que a imagem for atualizada**.

Para saber mais, confira o item sobre como [aplicar atualizações de software a uma imagem](/sccm/osd/get-started/manage-operating-system-images#bkmk_resetbase).


### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>Melhorias na etapa da sequência de tarefas Executar Script do PowerShell

<!--3556028, fka 1359389-->
***[Atualizado]*** Agora a etapa de sequência de tarefas **Executar Script do PowerShell** inclui as seguintes melhorias:  

- Você pode agora inserir diretamente o código do Windows PowerShell nessa etapa. Essa alteração permite que você execute comandos do PowerShell durante uma sequência de tarefas sem primeiro criar e distribuir o pacote com o script.

- Quando você escolhe a opção **Inserir um script do PowerShell**, selecione **Editar Script**. A nova janela de script do PowerShell fornece as seguintes ações:  

    - Editar o script diretamente  

    - Abrir um script existente de um arquivo  

    - Navegar até um script existente aprovado no Configuration Manager

- Salvar a saída do script para uma variável de sequência de tarefas personalizada  

- Para incluir os parâmetros do script no log de sequência de tarefas, defina a variável de sequência de tarefas **OSDLogPowerShellParameters** para **TRUE**. Por padrão, os parâmetros não estão no log.  

- Outras melhorias que fornecem funcionalidade semelhante como a etapa [Executar linha de comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine). Por exemplo, especifique as credenciais de usuário alternativas ou um tempo limite.

> [!Important]  
> Para aproveitar esse novo recurso do Configuration Manager, depois de atualizar o site, atualize também os clientes com a versão mais recente. Embora a nova funcionalidade seja exibida no console do Configuration Manager quando você atualiza o site e o console, o cenário completo só funcionará quando a versão do cliente também for a mais recente.

Para saber mais, confira [Executar scripts do PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript).


### <a name="other-improvements-to-os-deployment"></a>Outras melhorias à implantação do sistema operacional

<!--3633146,3641475,3654172,3734270-->
***[Atualizado]*** Esta versão inclui as seguintes melhorias na implantação do sistema operacional:

- Há uma nova ação padrão para **Exibição** nas sequências de tarefas. <!--3633146-->  

- A janela de diálogo de erro de sequência de tarefas agora exibe mais informações. Ele mostra o nome da etapa da sequência de tarefas com falha. <!--3641475-->  

- Quando você define a variável da sequência de tarefas **OSDDoNotLogCommand** como true, agora ela também oculta a linha de comando da etapa Executar linha de comando no arquivo de log. Anteriormente ela apenas mascarava o nome do programa da etapa Instalar pacote no smsts.log.<!--3654172-->  

- Quando você habilita um respondente do PXE em um ponto de distribuição sem o serviço de implantação do Windows, agora isso pode ser feito no mesmo servidor que o serviço DHCP. <!--3734270--> Para saber mais, leia o tópico [Configurar pelo menos um ponto de distribuição para aceitar solicitações PXE](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network#BKMK_Configure).



## <a name="bkmk_userxp"></a> Centro de software

### <a name="replace-toast-notifications-with-dialog-window"></a>Substituir as notificações do sistema por uma janela de diálogo

<!--3555947-->
***[Atualizado]*** Às vezes os usuários não veem a notificação do sistema do Windows sobre uma reinicialização ou implantação necessária. Assim, eles não veem a experiência de adiar o lembrete. Esse comportamento pode levar a uma experiência ruim para o usuário quando o cliente alcança um prazo final.

Agora quando as implantações precisam ser reinicializadas ou são necessárias alterações de software, você tem a opção de usar uma janela de diálogo mais intrusiva.

Para saber mais, confira [Plano para o Centro de Software](/sccm/apps/plan-design/plan-for-software-center#bkmk_impact)


### <a name="configure-user-device-affinity-in-software-center"></a>Configurar a afinidade de dispositivo do usuário no Centro de Software
<!--3485366-->
Com as [melhorias na infraestrutura do Centro de Software](/sccm/core/plan-design/changes/whats-new-in-version-1806#software-center-infrastructure-improvements), a partir da versão 1806, as funções de servidor do site de catálogo de aplicativos não são mais necessárias na maioria dos cenários. Alguns clientes ainda se basearam no catálogo de aplicativos para permitir que os usuários definam seus dispositivos primários para a afinidade de dispositivo de usuário. 

Agora os usuários podem definir seus dispositivos primários no Centro de Software. Essa ação torna-os um usuário primário do dispositivo no Configuration Manager.

<!-- For more information, see [Link users and devices with user device affinity](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity). -->


### <a name="configure-default-views-in-software-center"></a>Configurar as exibições padrão no Centro de Software
<!--3612112-->
Esta versão do Configuration Manager faz maior iteração em como você pode personalizar o Centro de Software:
 
- Definir o layout padrão de aplicativos, como blocos ou uma lista  

    - Se um usuário alterar essa configuração, o Centro de Software persistirá a preferência do usuário no futuro  

- Configurar o filtro de aplicativo padrão para todos ou apenas para aplicativos necessários  

    - O Centro de Software sempre usa a sua configuração padrão. Os usuários podem alterar esse filtro, mas o Centro de Software não persistirá as preferências deles.    

Especifique essas configurações no grupo **Centro de Software** das configurações do cliente.

<!-- For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#software-center). -->



## <a name="bkmk_sum"></a> Atualizações de software

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>Especificar a prioridade das atualizações de recurso nos serviços do Windows 10
<!--3734525-->
***[Atualizado]*** Ajuste a prioridade em que os clientes instalam uma atualização de recurso pelo [serviço do Windows 10](/sccm/osd/deploy-use/manage-windows-as-a-service). Por padrão, agora os clientes instalam atualizações de recurso com uma prioridade de processamento mais alta. 

Use as configurações do cliente para configurar esta opção. No grupo **Atualizações de Software**, defina a seguinte configuração: **Especifique a prioridade de thread para as atualizações de recurso**.

Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#software-updates). 



## <a name="bkmk_o365"></a> Gerenciamento do Office

### <a name="redirect-windows-known-folders-to-onedrive"></a>Redirecionar as pastas conhecidas do Windows para o OneDrive
<!--3556021-->
***[Atualizado]*** Use o Configuration Manager para mover pastas conhecidas do Windows para o OneDrive for Business. Essas pastas incluem a Área de Trabalho, Documentos e Imagens. Para simplificar suas atualizações do Windows 10, implante essas configurações para clientes do Windows 7 antes de implantar uma sequência de tarefas. 

Confira mais informações sobre este recurso do OneDrive for Business em [Redirecionar e mover pastas conhecidas do Windows para o OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders).

Primeiro, [encontre a ID do locatário do Office 365](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id). Em seguida, implante a versão do cliente de sincronização do OneDrive 18.111.0603.0004 ou posterior. Confira mais informações em [Implantar aplicativos do OneDrive usando o System Center Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

Para criar e implantar um perfil no OneDrive for Business, no console do Configuration Manager, acesse o workspace **Ativos e Conformidade**. Expanda as **Configurações de Conformidade** e selecione o nó **Perfis do OneDrive for Business**.  

Para ver mais informações, consulte a seção Redirecionar as pastas conhecidas do Windows para o OneDrive no artigo [Perfis do OneDrive for Business](/sccm/compliance/deploy-use/onedrive-profile).


### <a name="integration-for-office-365-proplus-readiness"></a>Integração para a preparação do Office 365 ProPlus
<!--3735402-->
***[Atualizado]*** Use o Configuration Manager para identificar os dispositivos com alta confiança que estão prontos para atualizar para o Office 365 ProPlus. A integração fornece percepções sobre quaisquer possíveis problemas de compatibilidade com suplementos do Office e macros usadas em seu ambiente. Em seguida, use o Configuration Manager para implantar o Office em dispositivos prontos. 

O painel de gerenciamento de cliente do Office 365 inclui agora um novo bloco, **Office 365 ProPlus Upgrade Readiness**.

Para saber mais informações, veja o [Painel de gerenciamento de clientes do Office 365](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness)


### <a name="additional-languages-for-office-365-updates"></a>Idiomas adicionais para atualizações do Office 365
<!--3555955-->
O Configuration Manager agora dá suporte a todos os idiomas compatíveis com as atualizações de cliente do Office 365. O fluxo de trabalho de atualização agora separa os 38 idiomas do **Windows Update** dos diversos idiomas da **Atualização de Cliente do Office 365**. 

Para obter mais informações, veja [Gerenciar atualizações do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#bkmk_o365_lang)


### <a name="office-products-on-lifecycle-dashboard"></a>Produtos do Office no painel de ciclo de vida
<!--3556026-->
***[Atualizado]*** O painel de ciclo de vida do produto agora inclui informações sobre as versões instaladas do Office 2003 até o Office 2016. Os dados aparecem depois que o site executa a tarefa de resumo de ciclo de vida, que ocorre a cada 24 horas.

Para saber mais, veja [Usar o painel de Ciclo de Vida do Produto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard).



<!-- ## <a name="bkmk_inv"></a> Inventory -->



## <a name="bkmk_pod"></a> Implantações em fases

### <a name="dedicated-monitoring-for-phased-deployments"></a>Monitoramento dedicado para implantações em fases
<!--3555949-->
***[Atualizado]*** As implantações em fases agora têm seu próprio nó de monitoramento dedicado. Esse nó facilita a identificação das implantações em fases que você criou e a navegação até a exibição de monitoramento da implantação em fases. No console do Configuration Manager, acesse o workspace **Monitoramento** e selecione o nó **Implantações em fases**. Ele mostra a lista de implantações em fases.

Para saber mais, veja [Exibição de monitoramento da implantações em fases](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_monitor). 


### <a name="improvement-to-phased-deployment-success-criteria"></a>Melhoria dos critérios de sucesso da implantação em fases
<!--3555946-->
***[Atualizado]*** Especifica critérios adicionais para o sucesso de uma fase em uma implantação em fases. Em vez de apenas um percentual, esse critério agora também pode ser o número de dispositivos implantados com êxito. Essa opção é útil quando o tamanho da coleção é variável, e você tem um número específico de dispositivos para mostrar o êxito antes de passar para a próxima fase. 

Crie uma implantação em fases para uma sequência de tarefas, uma atualização de software ou um aplicativo. Em seguida, na página Configurações do assistente, selecione a opção a seguir como critérios para o sucesso da primeira fase: **Número de dispositivos implantados com êxito**.

Saiba mais em [Criar implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).



## <a name="bkmk_admin"></a> Console do Configuration Manager

### <a name="bkmk_console"></a> Melhorias no console do Configuration Manager
<!--3594151-->
Com base nos comentários do cliente no MMS (Midwest Management Summit) Desert Edition 2018, esta versão inclui as seguintes melhorias no console do Configuration Manager:
- Maximiza a janela de registro de navegação para métodos de detecção de aplicativo
- Ir para a coleção de uma implantação de aplicativo
- Remover o conteúdo do status de monitoramento
- Exibições organizadas por valores inteiros no nó **Implantações** do workspace **Monitoramento**
- Mover o aviso para um grande número de resultados

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="configuration-manager-console-notifications"></a>Notificações do console do Configuration Manager
<!--3556016, fka 1318035-->
Para mantê-lo mais bem informado para que você possa tomar a ação apropriada, o console do Configuration Manager agora o notifica dos seguintes eventos:
- Quando uma atualização está disponível para o Configuration Manager em si
- Quando ocorrem eventos de ciclo de vida e manutenção no ambiente

Essa notificação é uma barra na parte superior da janela do console abaixo da faixa de opções. Ela substitui a experiência anterior quando atualizações do Configuration Manager estão disponíveis. Essas notificações no console ainda exibem informações críticas, mas não interferem no trabalho no console. Você não pode descartar notificações críticas. O console exibe todas as notificações em uma nova área de notificação da barra de título. 

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="confirmation-of-console-feedback"></a>Confirmação de comentários do console
<!--3556010-->
***[Atualizado]*** Quando você envia [comentários](/sccm/core/understand/find-help#product-feedback) no console do Configuration Manager, agora ele mostra uma mensagem de confirmação. Essa mensagem inclui uma **ID dos comentários**, que você pode fornecer à Microsoft como um identificador de acompanhamento.

Para obter mais informações, consulte [Comentários sobre o produto](/sccm/core/understand/find-help#bkmk_feedbackid).


### <a name="view-recently-connected-consoles"></a>Exibir consoles conectados recentemente 
<!--3699367-->
***[Atualizado]*** Agora você pode exibir as conexões mais recentes do console do Configuration Manager. O modo de exibição inclui conexões ativas e aqueles consoles que se conectaram recentemente. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Segurança** e escolha o nó **Conexões do Console**.

Para obter mais informações, veja [Usando o console do Configuration Manager](/sccm/core/servers/manage/admin-console#bkmk_viewconnected).


### <a name="in-console-documentation-dashboard"></a>Painel de documentação no console
<!--3556019, fka 1357546-->
Há um novo nó **Documentação** no novo workspace **Comunidade**. Esse nó inclui informações atualizadas sobre a documentação e os artigos de suporte do Configuration Manager.

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="search-device-views-using-mac-address"></a>Pesquisar exibições de dispositivo usando o endereço MAC
<!--3600878-->
Agora você pode pesquisar um endereço MAC em uma exibição de dispositivo do console do Configuration Manager. Essa propriedade é útil para os administradores de implantação do sistema operacional durante a solução de problemas de implantações baseadas no PXE. Ao exibir uma lista de dispositivos, adicione a coluna **Endereço MAC** à exibição. Use o campo de pesquisa para adicionar os critérios de pesquisa de **Endereço MAC**. 


### <a name="use-net-47-for-improved-console-accessibility"></a>Usar o .NET 4.7 para melhorar a acessibilidade do console
<!-- SCCMDocs-pr issue #3228 -->
Para melhorar os recursos de acessibilidade do console do Configuration Manager, atualize o .NET para versão 4.7 ou posterior no computador que executa o console. 

Para obter mais informações, confira [Recursos de acessibilidade no Configuration Manager](/sccm/core/understand/accessibility-features).


### <a name="changes-to-console-setup-process"></a>Alterações no processo de instalação do console

<!-- 3612513 -->
***[Atualizado]*** Há novos componentes necessários ao instalar o console do Configuration Manager. Se você criar um pacote para a instalação do console em outros computadores, verifique se que o pacote inclui os seguintes arquivos:

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

Ao instalar ou atualizar um servidor do site, ele copia os arquivos de instalação e os pacotes de idioma compatíveis com o site na subpasta **Tools\ConsoleSetup**. Para obter mais informações, veja [Instalar o console do Configuration Manager](/sccm/core/servers/deploy/install/install-consoles).



<!-- ## <a name="bkmk_opmdm"></a> On-premises MDM -->




## <a name="other-updates"></a>Outras atualizações

Além de novos recursos, este lançamento inclui outras alterações, como correções de bugs. Para obter mais informações, confira [Resumo das alterações no Branch Atual do Configuration Manager, versão 1902](https://support.microsoft.com/help/4498910).

Para saber mais sobre as alterações nos cmdlets do Windows PowerShell para o Configuration Manager, confira as [notas sobre a versão 1902 do PowerShell](https://docs.microsoft.com/powershell/sccm/1902-release-notes?view=sccm-ps).

<!-- 
The following update rollup (4486457) is available in the console starting on 25 January 2019: [Update rollup for Configuration Manager current branch, version 1902](https://support.microsoft.com/help/4486457).


### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |
 
-->



## <a name="next-steps"></a>Próximas etapas

Quando estiver tudo pronto para instalar esta versão, confira as informações sobre a [instalação de atualizações do Configuration Manager](/sccm/core/servers/manage/updates) e a [lista de verificação para a instalação da atualização 1902](/sccm/core/servers/manage/checklist-for-installing-update-1902).

> [!TIP]  
> Para instalar um novo site, use uma versão de linha de base do Configuration Manager.  
>
>  Saiba mais sobre:    
>   - [Instalação de novos sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Para problemas conhecidos e significativos, veja [Notas de versão](/sccm/core/servers/deploy/install/release-notes).

Depois de atualizar um site, examine também a [Lista de verificação pós-atualização](/sccm/core/servers/manage/checklist-for-installing-update-1902#post-update-checklist).
