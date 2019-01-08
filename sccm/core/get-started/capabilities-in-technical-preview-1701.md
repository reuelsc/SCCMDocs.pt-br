---
title: Recursos no Technical Preview 1701
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1701.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: b2a01d8ccc76315edbdf0e14085381463ec7ed7b
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424503"
---
# <a name="capabilities-in-technical-preview-1701-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1701 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*



Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1701. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Aprimoramentos de grupos de limites para os pontos de atualização de software
A partir dessa visualização, você agora pode usar grupos de limites para associar os clientes com pontos de atualização de software. Isso faz parte do trabalho contínuo para expandir as alterações de grupos de limites para gerenciar funções de sistema de site adicionais.  As alterações de grupos de limites foram introduzidas no Technical Preview 1609 e no Branch Atual, na versão 1610.  

Com essa visualização, você deve usar o novo comportamento de grupo de limite para gerenciar quais pontos de atualização de software um cliente pode usar, semelhante a como gerenciar qual ponto de distribuição um cliente pode usar:  

- Configure os grupos de limites para associar um ou mais servidores que hospedam um ponto de atualização de software.
- Os clientes que buscam um novo ponto de atualização de software tentarão usar um associado a seu grupo de limite atual.
- Quando o cliente não conseguir acessar seu ponto de atualização de software atual e não conseguir localizar um de seus grupos de limite atual, o cliente usará o comportamento de Fallback para expandir o pool disponível de pontos de atualização de software que pode ser usado.    

Para obter mais informações sobre grupos de limites, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) no conteúdo do Branch Atual.

No entanto, com essa visualização, grupos de limites para pontos de atualização de software são apenas parcialmente implementados. Você pode adicionar pontos de atualização de software e configurar grupos de limites vizinhos que contêm pontos de atualização de software, mas o tempo de fallback para pontos de atualização de software ainda não tem suporte e os clientes aguardarão duas horas antes de iniciar o fallback.

O seguinte descreve o comportamento de pontos de atualização de software com essa visualização técnica:  

- **Novos clientes usam grupos de limites para selecionar pontos de atualização de software**. Um cliente instalado após a instalação da versão 1701selecione um ponto de atualização de software dos associados ao grupo de limite do cliente.

  Isso substitui o comportamento anterior em que os clientes selecionavam um ponto de atualização de software aleatoriamente de uma lista dos que compartilham a floresta de clientes.   

- **Clientes instalados anteriormente continuam a usar seu atual ponto de atualização de software até fazerem fallback para localizar um novo.**
  Clientes que foram instalados anteriormente e que já têm um ponto de atualização de software continuarão a usar o ponto de atualização de software até fazerem fallback. Isso inclui pontos de atualização de software que não estão associados ao grupo de limite atual do cliente. Eles não tentam localizar e usar imediatamente um ponto de atualização de software do grupo de limite atual.

  Um cliente que já tem um ponto de atualização de software começa a usar esse novo comportamento de grupo de limite somente após o cliente não conseguir acessar seu ponto de atualização de software atual e iniciar um fallback.
  Esse atraso para alternar para o novo comportamento é intencional. Isso ocorre porque uma alteração do ponto de atualização de software pode resultar em um grande uso de largura de banda de rede à medida que o cliente sincroniza dados com o novo ponto de atualização de software. O atraso na transição pode ajudar a evitar a saturação de sua rede se todos os clientes mudarem para os novos pontos de atualização de software ao mesmo tempo.

- **Configurações de tempo de fallback:** Configurações para quando os clientes iniciarem fallback para pesquisar um novo ponto de atualização de software a clientes não são compatíveis com este Technical Preview. Isso inclui configurações para **Tempos de fallback (em minutos)** e **Nunca realizar fallback**, que você pode configurar para relacionamentos de grupo de limite diferentes.

  Em vez disso, os clientes mantêm seu comportamento atual no qual um cliente tenta se conectar ao seu ponto de atualização de software atual por duas horas antes de começar o fallback, para localizar um novo ponto de atualização de software que pode ser usado.

  Quando um cliente usa o fallback, ele usará as configurações de grupo de limite para realizar fallback para criar um pool de pontos de atualização de software disponíveis. Esse pool inclui todos os pontos de atualização de software do *grupo de limite atual* e dos *grupos de limite vizinho* do cliente e do *grupo de limite padrão do site* do cliente.

- **Configure o grupo de limite do site padrão:**  
  Considere adicionar um ponto de atualização de software para *Default-Site-Boundary-Group&lt;sitecode>*. Isso garante que os clientes que não são membros de outro grupo de limite possam realizar fallback para localizar um ponto de atualização de software.


Para gerenciar pontos de atualização de software para grupos de limite, use os [procedimentos da documentação do Branch Atual](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#procedures-for-boundary-groups), mas se lembre de que os tempos de fallback que você deve configurar ainda não são usados para pontos de atualização de software.


## <a name="hardware-inventory-collects-uefi-information"></a>O inventário de hardware coleta informações de UEFI
Uma nova classe de inventário de hardware (**SMS_Firmware**) e a propriedade (**UEFI**) estão disponíveis para ajudá-lo a determinar se um computador é iniciado no modo UEFI. Quando um computador é iniciado no modo UEFI, a propriedade **UEFI** é definida como **TRUE**. Isso é habilitado no inventário de hardware por padrão. Para obter mais informações sobre o inventário de hardware, consulte [Como configurar o inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="improvements-to-operating-system-deployment"></a>Melhorias na implantação do sistema operacional
Fizemos as seguintes melhorias para a implantação de sistema operacional, muitas das quais foram resultado dos comentários dos usuários.
- [**Suporte para mais aplicativos para a etapa da sequência de tarefas Instalar Aplicativos**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): Aumentamos o número máximo de aplicativos que você pode instalar para 99 na etapa de sequência de tarefas **Instalar Aplicativos**. O número máximo anterior era de 9 aplicativos.
- [**Selecionar vários aplicativos na etapa de sequência de tarefas Instalar Aplicativo**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step): Ao adicionar aplicativos à etapa da sequência de tarefas Instalar Aplicativo no editor de sequência de tarefas, agora você pode selecionar vários aplicativos no painel **Selecionar o aplicativo a instalar**.
- [**Expirar mídia autônoma**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): Quando você cria mídia autônoma, há novas opções para definir datas de início e vencimento opcionais na mídia. Essas configurações estão desabilitadas por padrão. As datas são comparadas com a hora do sistema no computador antes de a mídia autônoma ser executada. Quando a hora do sistema for anterior à hora de início ou posterior à hora de expiração, a mídia autônoma não será iniciada. Essas opções também estão disponíveis usando o cmdlet New-CMStandaloneMedia PowerShell.
- [**Suporte para conteúdo adicional na mídia autônoma**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): Agora há suporte para conteúdo adicional na mídia autônoma. Você pode selecionar pacotes adicionais, pacotes de driver e aplicativos para obter preparação na mídia junto com outros conteúdos referenciados na sequência de tarefas. Anteriormente, somente o conteúdo referenciado na sequência de tarefas era preparado na mídia autônoma.
- [**Tempo limite configurável para a etapa de sequência de tarefas do Driver de Aplicação Automática**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): Novas variáveis de sequência de tarefas estão agora disponíveis para configurar o valor de tempo limite na etapa de sequência de tarefas do Driver de aplicação automática ao fazer solicitações do catálogo HTTP. As seguintes variáveis e valores padrão (em segundos) estão disponíveis:
   - SMSTSDriverRequestResolveTimeOut Default: 60
   - SMSTSDriverRequestConnectTimeOut Default: 60
   - SMSTSDriverRequestSendTimeOut Default: 60
   - SMSTSDriverRequestReceiveTimeOut Default: 480
- [**A ID do pacote exibida nas etapas da sequência de tarefas**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste): Qualquer etapa de sequência da tarefa que faz referência a um pacote, pacote de driver, imagem do sistema operacional, imagem de inicialização ou pacote de atualização do sistema operacional agora exibirá a ID do pacote do objeto referenciado. Quando uma etapa de sequência de tarefas fizer referência a um aplicativo, ela exibirá a ID do objeto.
- **Windows 10 ADK controlado pela versão de build**: O Windows 10 ADK agora é controlado pela versão de build para garantir uma experiência com mais suporte ao personalizar imagens de inicialização do Windows 10. Por exemplo, se o site usa o Windows ADK para Windows 10, versão 1607, somente as imagens de inicialização com a versão 10.0.14393 poderão ser personalizadas no console. Para obter detalhes sobre como personalizar as versões WinPE, consulte [Personalizar imagens de inicialização](/sccm/osd/get-started/customize-boot-images).
- **O caminho de origem de imagem de inicialização padrão não pode ser alterado**: As imagens de inicialização padrão são gerenciadas pelo Configuration Manager e o caminho de origem da imagem de inicialização padrão não pode mais ser alterado no console do Configuration Manager ou ao usar o SDK do Configuration Manager. Você pode continuar a configurar um caminho de origem personalizado para imagens de inicialização personalizadas.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Hospede as atualizações de software nos pontos de distribuição baseados em nuvem
A partir da versão de visualização, você pode usar um ponto de distribuição baseado em nuvem para hospedar um pacote de atualização de software. No entanto, como você pode configurar clientes para baixar atualizações de software diretamente do Microsoft Update, considere que pode haver custos adicionais da implantação de um pacote de atualização de software para um ponto de distribuição baseado em nuvem.

Para obter informações sobre como usar pontos de distribuição baseados em nuvem, consulte [Usar um ponto de distribuição baseado em nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) no conteúdo do Branch Atual do Configuration Manager.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Validar dados de atestado de integridade do dispositivo por meio de pontos de gerenciamento

A partir dessa versão de visualização, você pode configurar pontos de gerenciamento para validar dados de relatório de atestado de integridade para serviços de atestado de integridade locais ou na nuvem. Uma nova guia **Opções Avançadas** na caixa de diálogo **Propriedades do Componente de Ponto de Gerenciamento** permite a você **Adicionar**, **Editar** ou **Remover** a **URL de serviço do atestado de integridade do dispositivo local**. Você também pode especificar **Configurações Personalizadas do Dispositivo** para o agente cliente para **Usar serviço de Atestado de Integridade local**.  Definir **Sim** para essa configuração permitirá a criação de relatórios para o ponto de gerenciamento local em vez do serviço baseado em nuvem.

### <a name="try-it-out"></a>Experimente

- **Habilitar atestado de integridade de dispositivo local em um ponto de gerenciamento**<br>  No console do Configuration Manager, acesse o ponto de gerenciamento e abra **Propriedades do Componente do Ponto de Gerenciamento** e, em seguida, clique na guia **Opções Avançadas**. Clique em **Adicionar** e especifique a URL local (por exemplo, https://10.10.10.10) para **URLs de serviço de atestado de integridade do dispositivo local**.
- **Habilitar relatórios de atestado de integridade do ponto de gerenciamento local para o agente cliente**<br>No console do Configuration Manager, selecione **Administração** > **Configurações do Cliente** e clique duas vezes ou crie uma nova **Configuração Personalizada de Dispositivo**. Selecione **Agente do Computador** e defina **Usar Serviço de Atestado Integridade Local** como **Sim**. Se **Habilitar comunicação com o serviço de atestado de integridade do dispositivo** estiver definido como **Sim** e **Usar atestado de integridade local** estiver definido como **Não**, o ponto de gerenciamento usará o serviço de atestado de integridade do dispositivo baseado em nuvem.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Usar o conector do OMS para nuvem Microsoft Azure Governamental
Com esse technical preview, agora você pode usar o conector do OMS (Microsoft Operations Management Suite) para se conectar a um workspace do OMS que está na nuvem Microsoft Azure Governamental.  

Para fazer isso, modifique um arquivo de configuração para apontar para a nuvem Governamental e, em seguida, instale o conector do OMS.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Instalar um conector do OMS na nuvem Microsoft Azure Governamental
1. Em qualquer computador que tenha o console do Configuration Manager instalado, edite o seguinte arquivo de configuração para apontar para a nuvem governamental:  ***&lt;caminho de instalação do CM>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

   **Edições:**

   Altere o valor do nome da configuração *FairFaxArmResourceID* para que seja igual a “<https://management.usgovcloudapi.net/”>

   - **Original:** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
     &lt;value>&lt;/value>   
     &lt;/setting>

   - **Editado:**     
     &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value><https://management.usgovcloudapi.net/&lt;/value>>  
     &lt;/setting>

   Altere o valor do nome da configuração *FairFaxAuthorityResource* para que seja igual a "<https://login.microsoftonline.com/>"

   - **Original:**&lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value>&lt;/value>

   - **Editado:**&lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value><https://login.microsoftonline.com/&lt;/value>>

2. Depois de salvar o arquivo com as duas alterações, reinicie o console do Configuration Manager no mesmo computador e, em seguida, use esse console para instalar o conector do OMS. Para instalar o conector, use as informações em [Sincronizar dados do Configuration Manager para o Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) e selecione o **Workspace do Operations Management Suite** que está na nuvem Microsoft Azure Governamental.

3. Após instalar o conector do OMS, a conexão com a nuvem Governamental estará disponível quando você usar um console que se conecta ao site.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>As versões do Android e iOS não precisam mais ser direcionadas nos assistentes de criação do MDM híbrido

Começando nesta visualização técnica para MDM (gerenciamento de dispositivo móvel) híbrido, você não precisa mais direcionar a versões específicas do Android e do iOS ao criar novas políticas e perfis de dispositivos gerenciados pelo Intune. Em vez disso, escolha um dos seguintes tipos de dispositivo:

- Android
- Samsung KNOX Standard 4.0 e superior
- iPhone
- iPad

Essa alteração afeta os assistentes de criação dos seguintes itens:

- Itens de configuração
- Políticas de conformidade
- Perfis de certificado
- Perfis de email
- Perfis de VPN
- Perfis de Wi-Fi

Com essa alteração, as implantações híbridas podem fornecer suporte com mais rapidez para novas versões do Android e do iOS sem precisar de uma nova versão ou extensão do Configuration Manager. Assim que uma nova versão passar a ter suporte no Intune autônomo, os usuários poderão atualizar seus dispositivos móveis para essa versão.

Para evitar problemas ao atualizar de versões anteriores do Configuration Manager, as versões dos sistemas operacionais móveis ainda estarão disponíveis nas páginas de propriedades desses itens. Se você ainda precisar direcionar a uma versão específica, crie o novo item e especifique a versão de destino na página de propriedades do item recém-criado.
