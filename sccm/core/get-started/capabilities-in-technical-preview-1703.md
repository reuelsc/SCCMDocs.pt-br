---
title: Funcionalidades no Technical Preview 1703 do Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1703."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3eb48942c1259d2aa1b3c200fad73b39b11c0b8c
ms.openlocfilehash: d497bd5a2971315eecdc0900f735ab2cd8b2e7bc
ms.lasthandoff: 03/30/2017

---
# <a name="capabilities-in-technical-preview-1703-for-system-center-configuration-manager"></a>Funcionalidades do Technical Preview 1703 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1703. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implantar aplicativos iOS adquiridos por volume em coleções de dispositivos

Agora você pode implantar aplicativos licenciados para dispositivos, bem como os usuários. Dependendo da capacidade dos aplicativos para dar suporte ao licenciamento de dispositivos, uma licença apropriada será solicitada quando você implantá-la, da seguinte maneira:

|||||
|-|-|-|-|
|Versão do Configuration Manager|O aplicativo dá suporte ao licenciamento de dispositivos?|Tipo de coleção de implantação|Licença solicitada|
|Anterior à versão 1702|Sim|usuário|Licença de usuário|
|Anterior à versão 1702|Não|usuário|Licença de usuário|
|Anterior à versão 1702|Sim|Dispositivo|Licença de usuário|
|Anterior à versão 1702|Não|Dispositivo|Licença de usuário|
|1702 e posterior|Sim|usuário|Licença de usuário|
|1702 e posterior|Não|usuário|Licença de usuário|
|1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
|1702 e posterior|Não|Dispositivo|Licença de usuário|

Para saber mais sobre aplicativos do iOS adquiridos por volume, veja [Gerenciar aplicativos iOS adquiridos por volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

## <a name="direct-links-to-applications-in-software-center"></a>Links diretos para aplicativos no Centro de Software

Agora você pode fornecer aos usuários finais um link direto para um aplicativo no Centro de Software. Isso significa que eles não precisam mais abrir o Centro de Software e pesquisar por um aplicativo antes de poder instalá-lo. Isso está disponível apenas para os aplicativos do Configuration Manager, não para os pacotes e programas ou sequências de tarefas.

### <a name="try-it-out"></a>Experimente                 

Use o seguinte formato de URL para abrir o Centro de Software para um aplicativo específico:

**Softwarecenter:SoftwareId=*Application Identifier***

### <a name="how-to-get-the-application-identifier-of-an-application"></a>Como obter o identificador do aplicativo de um aplicativo.

1.    No console do Configuration Manager, clique em **Biblioteca de Software**.
2.    No espaço de trabalho Biblioteca de Software, expanda **Gerenciamento de Aplicativos** e clique em **Aplicativos**.
3.    Na exibição dos **aplicativos**, clique com o botão direito do mouse em um dos cabeçalhos de coluna e, em seguida, na lista, selecione **ID exclusiva do IC**. Você verá que a ID exclusiva de cada aplicativo agora é mostrada na lista.
4.    Observe a **ID exclusiva do IC** do aplicativo para o qual você deseja fornecer um link, por exemplo: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5.    Em seguida, remova qualquer texto após o aplicativo GUID, neste caso **/2**. Isso deixa você com o identificador do aplicativo.
6.    Por fim, para concluir a construção do link, preceda-o com **Softwarecenter:SoftwareID =**. Usando o exemplo acima, o link final será: **Softwarecenter:SoftwareId = ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Usando este link, os usuários finais podem abrir o Centro de Software diretamente para o aplicativo especificado.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Certificados PFX para computadores cliente Windows do Configuration Manager

Agora você pode implantar perfis de certificado PFX importados para computadores cliente do Configuration Manager com o Windows 10.

### <a name="try-it-out"></a>Experimente

Use as instruções em [Como criar perfis de certificado PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) para importar um arquivo PFX, implantar o perfil e, em seguida, verifique se o certificado foi instalado para o usuário de destino.



## <a name="configure-azure-services-wizard"></a>Assistente de Configuração de Serviços do Azure
O Technical preview 1703 introduz o assistente de **configuração de serviços do Azure**. Esse assistente fornece uma experiência de configuração comum que substitui os fluxos de trabalho individuais para configurar os serviços de nuvem usados com o Configuration Manager. Isso é feito usando um **aplicativo Web do Azure** para fornecer os detalhes de assinatura e de configuração que você insere cada vez que configura um novo componente do Configuration Manager ou serviço com o Azure.

Com technical preview 1703, apenas a Windows Store para Empresas (WSfB) é configurada usando esse assistente.  Outros serviços de nuvem são configurados por meio de seus fluxos de trabalho separados.

-    Use as informações deste tópico de visualização para substituir as etapas de configuração encontradas na seção [Configurar sincronização da Windows Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#set-up-windows-store-for-business-synchronization) do tópico do Branch Atual [Gerenciar aplicativos da Windows Store para Empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

-    Para obter mais informações sobre os aplicativos Web, consulte [Autenticação e autorização no serviço de aplicativo do Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) e [Visão geral de aplicativos Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### <a name="prerequisites-and-planning"></a>Pré-requisitos e planejamento
Ao configurar uma conexão entre o Configuration Manager e a Windows Store para Empresas, é necessário fornecer uma pasta em que o conteúdo do aplicativo sincronizado do repositório será mantido. Para garantir que essa pasta é segura e que seu conteúdo pode ser implantado em dispositivos, verifique se as seguintes permissões existem:
-    O computador no qual você instala a função do sistema de sites do ponto de conexão de serviço (o site de nível superior na hierarquia) deve ter permissões de leitura e gravação na pasta especificada durante o uso da conta **Computer$**.  

-    O autor do aplicativo deve ter permissões de leitura da pasta especificada.  

-    A conta **Computer$** de cada computador que hospeda uma instância do Provedor de SMS deve poder usar a pasta especificada.

No Azure Active Directory, registre o Configuration Manager como uma ferramenta de gerenciamento de API Web ou de aplicativo Web. Isso lhe fornecerá uma ID de cliente de que você precisará mais tarde.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Use o assistente para configurar o serviço de nuvem WSfB

1. No console, vá para **Administração** > **Visão geral** > **Gerenciamento de serviços de nuvem** > **Azure** > **Serviços do Azure** e, em seguida, escolha **Configurar serviços do Azure** para iniciar o **Assistente de serviços do Azure**.

2. Na página de **Serviços do Azure**, selecione o serviço que deseja configurar e, em seguida, clique em **Próxima**. Com essa visualização, somente WSfB pode ser configurado.

3. Na página **Geral**, forneça um nome amigável para o **Nome do serviço do Azure** e uma descrição opcional e clique **Próxima**.

4. Na página do **aplicativo**, especifique seu ambiente do Azure e, em seguida, clique em **Procurar** para abrir a janela do aplicativo de servidor.

5. Na janela do **aplicativo de servidor**, selecione o aplicativo de servidor que você deseja usar e depois clique em **OK**.
Aplicativos de servidor são os aplicativos Web do Azure que contêm as configurações da sua conta do Azure, incluindo sua ID de locatário, ID de cliente e uma chave secreta para clientes. Se você não tiver um aplicativo de servidor disponível, use um dos seguintes:
  -    **Criar**: Para criar um novo aplicativo de servidor, clique em **Criar**. Forneça um nome amigável para o aplicativo e o locatário. Em seguida, depois que você entrar no Azure, o Configuration Manager cria o aplicativo Web do Azure para você, incluindo a ID do cliente e a chave secreta para uso com o aplicativo Web. Posteriormente, você pode exibi-las no portal do Azure.
  -    **Importar**: Para usar um aplicativo Web que já existe em sua assinatura do Azure, clique em **Importar**. Forneça um nome amigável para o aplicativo e o locatário e especifique a ID de locatário, ID do cliente e a chave secreta para o aplicativo Web do Azure que você deseja que o Configuration Manager use. Depois que você **verificar** as informações, clique em **OK** para continuar.  </br></br>

6. Examine a página de **informações** e conclua quaisquer etapas adicionais e configurações, conforme indicado. Essas configurações são necessárias para usar o serviço com o Configuration Manager.
Por exemplo, para configurar WSfB:

  1. No Azure, você deve registrar o Configuration Manager como um aplicativo Web ou API Web e registrar a ID do cliente. Você também pode especificar uma chave de cliente para uso pela ferramenta de gerenciamento (que é o Configuration Manager).

  2.    No console do WSfB, você deve configurar o Configuration Manager como a ferramenta de gerenciamento de repositório, habilitar o suporte para aplicativos licenciados offline e, em seguida, pelo menos um aplicativo de compra.   </br>

  Quando estiver pronto para continuar, clique em **Próximo**.

7. Na página **Configurações de aplicativo**, conclua as configurações de catálogo e idioma do aplicativo para este serviço e, em seguida, clique em **Próxima**.
8. Após concluir o assistente, o console do Configuration Manager mostra que você configurou **Windows Store para Empresas** como um **tipo de serviço de nuvem**.

Agora você pode usar o restante do [conteúdo do Branch atual](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) para gerenciar aplicativos de WSfB para sincronizar, criar e implantar e monitorar aplicativos da Windows Store para Empresas.

### <a name="modify-a-cloud-service-configuration"></a>Modificar uma configuração de serviço de nuvem
Você pode exibir e editar as propriedades de um serviço de nuvem para modificar a configuração.

No console, vá para **Administração** > **Visão geral** > **Gerenciamento de serviços de nuvem** > **Azure** > **Serviços do Azure** e, em seguida, escolha **Configurar serviços do Azure**, selecione um serviço de nuvem e, em seguida, escolha **Propriedades**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Converter de BIOS para UEFI durante uma atualização in-loco
A Atualização do Windows 10 para Criadores apresenta uma ferramenta de conversão simples que automatiza o processo para reparticionar o disco rígido para hardware habilitado para UEFI e integra a ferramenta de conversão ao processo de atualização in-loco do Windows 7 para o Windows 10. Quando você combina essa ferramenta com a sequência de tarefas de atualização do sistema operacional e a ferramenta de OEM que converte o firmware do BIOS para UEFI, pode converter os computadores de BIOS para UEFI durante uma atualização in-loco para a Atualização do Windows 10 para Criadores. Para obter detalhes, consulte [Etapas de sequência de tarefas para gerenciar o BIOS para a conversão para UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

## <a name="collapsible-task-sequence-groups"></a>Grupos de sequências de tarefas recolhíveis
Esta versão apresenta a capacidade de expandir e recolher grupos de sequência de tarefas. Você pode expandir ou recolher grupos individuais ou expandir ou recolher todos os grupos de uma só vez.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Configurações do cliente para configurar o Windows Analytics para Preparação para Atualização
Começando com esta versão, você pode usar as configurações do dispositivo cliente para simplificar a configuração de Análise do Windows quando você usa [preparação para atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics) com o Configuration Manager. A Análise do Windows coleta e relata dados de telemetria sobre seus clientes do Configuration Manager para seu espaço de trabalho do Operations Manager Suite (OMS). Os dados de telemetria coletados podem ajudá-lo a priorizar as decisões sobre atualizações do Windows para os dispositivos gerenciados.

Os dados de telemetria que o Configuration Manager coleta estão na forma dos arquivos de log do Rastreamento de Eventos para Windows (ETW). Esses arquivos de log são enviados para o site do Configuration Manager quando o cliente envia o inventário de hardware. Esses arquivos são transferidos para seu espaço de trabalho do OMS. Os arquivos de log e seus dados são removidos do site do Configuration Manager após transferir os logs do OMS.

Para obter informações sobre as configurações de telemetria do Windows, consulte [Configure a telemetria do Windows em sua organização](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).

### <a name="prerequisites"></a>Pré-requisitos
- Você deve ter configurado o seu site para usar Log Analytics de prontidão de atualização do OMS. Para obter informações, consulte [atualização Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) na biblioteca de conteúdo para a ramificação atual.
- Clientes devem usar o inventário de hardware para enviar os dados de telemetria.

### <a name="configure-windows-analytics-client-settings"></a>Definir configurações de cliente de análise do Windows
Para configurar a análise do Windows, no console do Configuration Manager, vá para **Administração** > **Configurações do cliente**, clique duas vezes em **Configurações do cliente-padrão** e, em seguida, selecione **Análise do Windows**.  

Configure, então, o seguinte:
- **ID comercial**  
A ID comercial mapeia informações de dispositivos que você gerencia para seu espaço de trabalho do OMS. Se você já configurou uma ID comercial para uso com a preparação de atualização para uso com o Configuration Manager, use essa ID. Se você ainda não tiver uma ID comercial, consulte [Gerar a chave da ID comercial]( https://technet.microsoft.com /itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

- Defina um **nível de telemetria para dispositivos com Windows 10**   
Para obter informações sobre o que é coletado por cada nível de telemetria do Windows 10, consulte [Níveis de telemetria]( https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels) na documentação online do Windows.

- Escolha **aceitar a coleta de dados comerciais em dispositivos com Windows 7, 8 e 8.1**   
Para obter informações sobre dados coletados desses sistemas operacionais quando você aceita, baixe o arquivo pdf [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Campos e eventos de telemetria de avaliação do Windows 7, Windows 8 e Windows 8.1) da Microsoft.

- **Configurar coleta de dados do Internet Explorer**

