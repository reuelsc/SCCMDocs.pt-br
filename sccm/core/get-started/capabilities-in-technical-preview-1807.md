---
title: Visualização técnica 1807
titleSuffix: Configuration Manager
description: Saiba mais sobre os novos recursos disponíveis no branch de visualização técnica versão 1807 do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c443f561392f95d875a681319ebb9db4ff3fb66b
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898470"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Funcionalidades na visualização técnica da versão 1807 do Configuration Manager 

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis na visualização técnica do Configuration Manager, versão 1807. Instale esta versão para atualizar e adicionar novos recursos ao seu site da visualização técnica. 

Examine o artigo da [visualização técnica](/sccm/core/get-started/technical-preview) antes de instalar essa atualização. Este artigo familiariza você com os requisitos gerais e as limitações do uso de um technical preview, como atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>Problemas conhecidos 

### <a name="ki_o365"></a> Problemas com as atualizações de software do Office 365
<!--521365--> Se você gerenciar as atualizações do Office 365 usando o branch de visualização técnica das versões 1806 e 1806.2, elas poderão falhar na instalação nos clientes. 

#### <a name="workaround"></a>Solução alternativa
- Exclua pacotes de implantação e grupos de atualização de software existente para o Office 365.  

- A partir de 31 de julho de 2018, sincronize as atualizações de software do Office 365 e implante somente as atualizações mais recentes.  



</br>

**As seções a seguir descrevem os novos recursos para experimentar nesta versão:**  


## <a name="bkmk_hub"></a> Hub da comunidade
<!--1357766-->

O Hub da comunidade é um local centralizado para o compartilhamento de objetos úteis do Configuration Manager com outras pessoas. Confira o novo workspace **Comunidade** no console do Configuration Manager e escolha o nó **Hub**. Use o Hub da comunidade para fazer o download dos seguintes tipos de objetos do Configuration Manager: 
- Scripts
- Itens de configuração

![Console do Configuration Manager, Workspace da comunidade, Nó do hub](media/1357766-hub.png)

Para ver mais detalhes sobre um item disponível, clique nele no hub. Na página de detalhes, clique em **Fazer o download** para adquirir o item. Quando você faz o download de um item no hub, ele é automaticamente adicionado ao seu site. 

![Console do Configuration Manager, Workspace da comunidade, Nó do hub, página de detalhes](media/1357766-hub-details.png)

O workspace da **comunidade** também inclui os seguintes nós:

- **Documentação**: exibe a [biblioteca de documentação](https://docs.microsoft.com/sccm/) do Configuration Manager  

- **Comentários**: exibe o [site UserVoice](https://configurationmanager.uservoice.com/) do Configuration Manager  


### <a name="prerequisites"></a>Pré-requisitos

- Usar o console do Configuration Manager no SO do cliente.  

    - Como alternativa, mas não recomendado: em um sistema operacional do servidor, desabilite a opção [Internet Explorer: configuração de segurança aprimorada](https://go.microsoft.com/fwlink/?LinkId=253461).  

- O computador do console exige acesso à Internet e conectividade aos seguintes sites:  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>Problema conhecido

Contribuir com itens para o hub não está disponível nesta versão. 



## <a name="bkmk_osd"></a> Especificar a unidade para manutenção offline de imagem do sistema operacional  
<!--1358924-->

Com base em seus [comentários do UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive), agora especifique a unidade que o Configuration Manager usará durante a manutenção offline de imagens do sistema operacional. Esse processo pode consumir uma grande quantidade de espaço em disco com arquivos temporários, portanto, essa opção oferece flexibilidade na escolha da unidade que será usada. 


### <a name="try-it-out"></a>Experimente!

Tente concluir as tarefas. Em seguida, envie [Comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) com sua opinião sobre o recurso.

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**. Na faixa de opções, clique em **Configurar Componentes do Site** e escolha **Ponto de Atualização de Software**.  

2. Alterne para a guia **Manutenção Offline** e especifique a opção para **Uma unidade local a ser usada pela manutenção offline de imagens**.  

Por padrão, essa configuração é **Automática**. Com esse valor, o Configuration Manager escolhe a unidade na qual ele é instalado. 

Durante a manutenção offline, o Configuration Manager armazena arquivos temporariamente em uma pasta, `<drive>:\ConfigMgr_OfflineImageServicing`. Ele também cria imagens do sistema operacional nessa pasta. 

Examine o arquivo de log **OfflineServicingMgr.log**. 



## <a name="bkmk_comgmt"></a> Atividade de sincronização de dispositivo cogerenciado do Intune
<!--1358565-->

Exiba no console do Configuration Manager se um dispositivo cogerenciado está ativo com o Microsoft Intune. Esse estado se baseia nos dados do [Intune Data Warehouse](https://docs.microsoft.com/intune/reports-nav-create-intune-reports). O painel **Status do Cliente** no console do Configuration Manager exibe **Clientes inativos usando o Intune**. Essa nova categoria destina-se a dispositivos cogerenciados que estão inativos no Configuration Manager, mas foram sincronizados com o serviço do Intune na semana passada.


### <a name="try-it-out"></a>Experimente!

Tente concluir as tarefas. Em seguida, envie [Comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) com sua opinião sobre o recurso.

Se você já tiver configurado seu site para cogerenciamento: 

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e escolha o nó **Cogerenciamento**. Na faixa de opções, clique em **Propriedades**.  

2. Alterne para a guia **Relatório**. Clique em **Entrar** e autentique. Em seguida, clique em **Atualizar** para habilitar permissões de leitura para o Intune Data Warehouse.  

3. Após o site ser sincronizado com o Intune, vá para o workspace **Monitoramento** e escolha o nó **Status do Cliente**. Na seção **Status Geral do Cliente**, confira a linha de **Clientes inativos que usam o Intune**.  

Para saber mais sobre a ativação do cogerenciamento, confira [Cogerenciamento para dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview).



## <a name="bkmk_app-repair"></a> Reparar aplicativos
<!--1357866-->

Com base nos [Comentários do UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application), agora você pode especificar uma linha de comando de reparo para os tipos de implantação do Windows Installer e do Instalador de Script. 


### <a name="try-it-out"></a>Experimente!

Tente concluir as tarefas. Em seguida, envie [Comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) com sua opinião sobre o recurso.

1. No console do Configuration Manager, abra as propriedades de um tipo de implantação do Windows Installer ou Instalador de Script.  

2. Alterne para a guia **Programas**. Especifique o comando **Programa de reparo**.  

3. Implante o aplicativo. Na guia **Configuração de Implantação** da implantação, habilite a opção para **Permitir que os usuários finais tentem reparar este aplicativo**.  


### <a name="known-issue"></a>Problema conhecido

O novo botão no Centro de Software para que os usuários possam **Reparar** o aplicativo não é visível nesta versão.  



## <a name="bkmk_email-approve"></a> Aprovar solicitações de aplicativo por email
<!--1321550-->

Configure notificações por email para solicitações de aprovação do aplicativo. Quando um usuário solicitar um aplicativo, você receberá um email. Clique nos links no email para aprovar ou negar a solicitação sem precisar usar o console do Configuration Manager.


### <a name="prerequisites"></a>Pré-requisitos

#### <a name="to-send-email-notifications"></a>Para enviar notificações por email
- Habilite o [recurso opcional](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Aprovar solicitações de aplicativo para usuários por dispositivo**.  

- Configure [notificações por email para alertas](/sccm/core/servers/manage/use-alerts-and-the-status-system#to-configure-email-notification-for-alerts).  

#### <a name="to-approve-or-deny-requests-from-email"></a>Para aprovar ou negar solicitações de email
Se você não configurar esses pré-requisitos, o site enviará uma notificação por email com as solicitações de aplicativo sem links para aprovar ou negar a solicitação.  

- Nas propriedades do site **Habilitar o ponto de extremidade REST para todas as funções de provedor neste site e permitir o tráfego de gateway de gerenciamento de nuvem do Configuration Manager**. Para saber mais, confira [Acesso a dados do ponto de extremidade OData](/sccm/core/get-started/capabilities-in-technical-preview-1612#odata-endpoint-data-access).  

    - Reiniciar o serviço SMS_EXEC depois de habilitar o ponto de extremidade REST

- [Gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)  

- Integrar o site aos [serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para **Gerenciamento de nuvem**  

    - Habilitar a [Descoberta de usuários do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Defina manualmente as seguintes configurações para este aplicativo nativo no Azure AD:  

        - **URI de redirecionamento**: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`. Use o FQDN (Nome do Domínio Totalmente Qualificado) do serviço do CMG (Gateway de Gerenciamento de Nuvem), por exemplo, GraniteFalls.Contoso.com.   

        - **Manifesto**: defina **oauth2AllowImplicitFlow** como true: `"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>Experimente!

Tente concluir as tarefas. Em seguida, envie [Comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) com sua opinião sobre o recurso.

1. No console do Configuration Manager, implante um aplicativo como disponível para uma coleção de usuários. Na página **Configurações de Implantação**, habilite-a para aprovação. Em seguida, insira um endereço de email *único* para receber a notificação.  

     > [!Note]  
     > Qualquer pessoa na organização do Azure AD que receber o email poderá aprovar a solicitação. Não encaminhe o email para outras pessoas, a menos que você queira que elas realizem alguma ação.  

2. Como usuário, solicite o aplicativo no Centro de Software.  

3. Você receberá uma notificação por email semelhante ao exemplo a seguir:  

![Exemplo de notificação por email para aprovação do aplicativo](media/1321550-email.png)

> [!Note]  
> O link para aprovar ou negar é para ser usado uma única vez. Por exemplo, você pode configurar um alias de grupo para receber notificações. Sara aprova a solicitação. E Vinícius já não pode negar a solicitação.  



## <a name="bkmk_script"></a> Melhoria na saída do script
<!--1236459-->

Agora você pode visualizar a saída detalhada do script em formato JSON bruto ou estruturado. Essa formatação facilita a leitura e a análise da saída. Se o script retornar um texto formatado em JSON válido, exiba a saída detalhada como **Saída JSON** ou **Saída Raw**. Caso contrário, a única opção será **Saída do Script**. 

#### <a name="example-script-output-is-valid-json"></a>Exemplo: A saída do script é um JSON válido
Comando: `$PSVersionTable.PSVersion`  

Saída:  
```
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>Exemplo: Saída do script não é um JSON válido
Comando: `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

Saída:  
```
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>Experimente!

Tente concluir as tarefas. Em seguida, envie [Comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) com sua opinião sobre o recurso.

1. No console do Configuration Manager, acesse o workspace **Ativos e Conformidade** e escolha o nó **Coleções de Dispositivos**. Clique com o botão direito do mouse em uma coleção e escolha **Executar Script**. Para saber mais sobre a criação e execução de scripts, confira [Criar e executar scripts do PowerShell do console do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).  

2. Execute um script na coleção de destino.  

3. Na página **Monitoramento de Status de Script** do assistente Executar Script, marque a guia **Resumo** na parte inferior. Altere as duas listas suspensas na parte superior para **Saída do Script** e **Tabela de Dados**. Em seguida, clique duas vezes na linha de resultados para abrir a caixa de diálogo **Saída Detalhada**.  

4. Na página **Monitoramento de Status de Script** do assistente Executar Script, marque a guia **Executar Detalhes** na parte inferior. Clique duas vezes na linha de resultados para abrir a caixa de diálogo Saída Detalhada desse dispositivo.  



## <a name="bkmk_3pupdate"></a> Melhoria nas atualizações de software de terceiros
<!--1358714-->

Agora você já pode modificar as propriedades de catálogos personalizados.

Para saber mais, confira [Suporte a catálogos personalizados de atualizações de software de terceiros](/sccm/core/get-started/capabilities-in-technical-preview-1806-2#bkmk_3pupdate).



## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como instalar ou atualizar o branch da visualização técnica, confira [Visualização técnica](/sccm/core/get-started/technical-preview).    

Para saber mais sobre os diferentes branches do Configuration Manager, confira [Qual branch do Configuration Manager devo usar?](/sccm/core/understand/which-branch-should-i-use)