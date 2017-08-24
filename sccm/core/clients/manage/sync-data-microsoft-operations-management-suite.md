---
title: "Sincronização de dados | Microsoft Docs | Microsoft Operations Management Suite "
description: Sincronizar dados do System Center Configuration Manager com o Microsoft Operations Management Suite.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: "9"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 608a9893011c6500d5d4cd2f756a124db66b1858
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
#  <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Sincronizar dados do Configuration Manager com o Microsoft Operations Management Suite

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o **Assistente para Serviços do Azure** para configurar sua conexão do Configuration Manager para o serviço de nuvem do Operations Management Suite (OMS). A partir da versão 1706, o assistente substitui os fluxos de trabalho anteriores para configurar essa conexão. Para versões anteriores, confira [Sincronizar dados do Configuration Manager com o Microsoft Operations Management Suite (1702 e anterior)](#Sync-data-from-Configuration-Manager-to-the-Microsoft-Operations-Management-Suite-(1702-and-earlier)).

-   O assistente é usado para configurar os serviços de nuvem para o Configuration Manager, como o OMS, o Windows Store for Business (WSfB) e o Azure Active Directory (Azure AD).  

-   O Configuration Manager conecta-se ao OMS para recursos como [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) ou [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).

## <a name="prerequisites-for-the-oms-connector"></a>Pré-requisitos para o Conector do OMS
Os pré-requisitos para configurar uma conexão para o OMS são os mesmos dos [documentados para a versão Branch Atual 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Essa informação é repetida aqui:  

-   Antes de instalar o conector do OMS no Configuration Manager, você deverá fornecer ao Configuration Manager as permissões para OMS. Especificamente, você deverá conceder *acesso de colaborador* ao *grupo de recursos* do Azure que contém o espaço de trabalho do OMS Log Analytics. Os procedimentos para fazer isso estão documentados no conteúdo do Log Analytics. Consulte [Fornecer o Configuration Manager com permissões para OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) na documentação do OMS.

-   O conector do OMS deve ser instalado no computador que hospeda um [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) no [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

-   Você deve instalar um Agente de Monitoramento da Microsoft para o OMS instalado no ponto de conexão de serviço junto com o conector do OMS. O agente e o conector do OMS devem ser configurados para usar o mesmo **espaço de trabalho do OMS**. Para instalar o agente, veja [Baixar e instalar o agente](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) na documentação do OMS.
-   Depois de instalar o conector e o agente, você deverá configurar o OMS para usar dados do Configuration Manager. Para fazer isso, no Portal do OMS, veja [Importar as coleções do Configuration Manager](/azure/log-analytics/log-analytics-sccm#import-collections).

## <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Use o Assistente para Serviços do Azure para configurar a conexão para OMS

1.  No console, acesse **Administração** > **Visão geral** > **Serviços de Nuvem** > **Serviços do Azure** e, em seguida, escolha **Configurar Serviços do Azure**, na guia **Início** da faixa de opções, para iniciar o **Assistente de Serviços do Azure**.

2.  Na página **Serviços do Azure**, selecione o serviço de nuvem do Operation Management Suite. Forneça um nome amigável para o **Nome do serviço do Azure** e uma descrição opcional e clique **Próxima**.

3.  Na página **Aplicativo**, especifique seu Ambiente do Azure (a visualização técnica oferece suporte somente à nuvem pública). Em seguida, clique em **Procurar** para abrir a janela do Aplicativo do Servidor.

4.  Selecione um aplicativo Web:

    -   **Importar**: Para usar um aplicativo Web que já existe em sua assinatura do Azure, clique em **Importar**. Forneça um nome amigável para o aplicativo e o locatário e especifique a ID de locatário, ID do cliente e a chave secreta para o aplicativo Web do Azure que você deseja que o Configuration Manager use. Depois que você **verificar** as informações, clique em **OK** para continuar.   

    > [!NOTE]   
    > Quando você configura o OMS com essa visualização, o OMS oferece suporte somente à função *import* função para um aplicativo Web. Não há suporte para a criação de um novo aplicativo Web. Da mesma forma, não é possível reutilizar um aplicativo existente para o OMS.

5.  Se você concluiu todos os outros procedimentos com êxito, as informações na tela **Configuração de Conexão de OMS** aparecerão automaticamente nesta página. As informações para as configurações de conexão devem aparecer para sua **Assinatura do Azure**, **Grupo de recursos do Azure** e **Espaço de trabalho do Operations Management Suite**.

6.  O assistente conecta-se ao serviço do OMS usando as informações que você inseriu. Selecione as coleções de dispositivos que você deseja sincronizar com o OMS e, em seguida, clique em **Adicionar**.

7.  Verifique suas configurações de conexão na tela **Resumo** e, em seguida, selecione **Avançar**. A tela **Andamento** mostra o status da conexão e, em seguida, clique em **Concluir**.

8.  Após concluir o assistente, o console do Configuration Manager mostra que você configurou o **Operations Management Suite** como um **Tipo de Serviço de Nuvem**.

## <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite-1702-and-earlier"></a>Sincronizar dados do Configuration Manager com o Microsoft Operations Management Suite (1702 e anterior)


*Aplica-se a: System Center Configuration Manager (1702 e versões anteriores)*

É possível usar o Conector do Microsoft OMS (Operations Management Suite) para sincronizar dados como suas coleções do System Center Configuration Manager com o OMS Log Analytics no Microsoft Azure. Isso torna dados de sua implantação do Configuration Manager visíveis no OMS.
> [!TIP]
> O Conector do OMS é um recurso de pré-lançamento. Para saber mais, confira [Usar recursos de pré-lançamento de atualizações](/sccm/core/servers/manage/pre-release-features).

A partir da versão 1702, você pode usar o conector do OMS para se conectar a um espaço de trabalho do OMS que está na nuvem do Microsoft Azure Government. Isso exige a modificação de um arquivo de configuração antes de instalar o conector do OMS. Veja [Usar o conector do OMS com a nuvem Azure Governamental](#fairfaxconfig) neste tópico.

### <a name="prerequisites"></a>Pré-requisitos
- Antes de instalar o conector do OMS no Configuration Manager, você deverá fornecer ao Configuration Manager as permissões para OMS. Especificamente, você deverá conceder *acesso de colaborador* ao *grupo de recursos* do Azure que contém o espaço de trabalho do OMS Log Analytics. Os procedimentos para fazer isso estão documentados no conteúdo do Log Analytics. Consulte [Fornecer o Configuration Manager com permissões para OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) na documentação do OMS.

- O conector do OMS deve ser instalado no computador que hospeda um [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) no [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

  Se você conectou o OMS a um site primário autônomo e planeja adicionar um site de administração central ao seu ambiente, deverá excluir a conexão atual e reconfigurar o conector no novo site de administração central.

- Você deve instalar um Agente de Monitoramento da Microsoft para o OMS instalado no ponto de conexão de serviço junto com o conector do OMS.  O agente e o conector do OMS devem ser configurados para usar o mesmo **espaço de trabalho do OMS**. Para instalar o agente, veja [Baixar e instalar o agente](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) na documentação do OMS.

- Depois de instalar o conector e o agente, você deverá configurar o OMS para usar dados do Configuration Manager.  Para fazer isso, no Portal do OMS, veja [Importar as coleções do Configuration Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).



### <a name="install-the-oms-connector"></a>Instalar o Conector do OMS  
1. No console do Configuration Manager, configure sua [hierarquia para usar recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features) e, em seguida, habilitar o uso do Conector do OMS.  

2. Em seguida, vá até **Administração** > **Serviços de nuvem** > **Conector do OMS**. Na faixa de opções, clique em "Criar conexão com o Operations Management Suite". Isso abre o **Assistente de Conexão com o Operation Management Suite**. Selecione **Avançar**.  


3.  Na página **Geral**, confirme que você tem as seguintes informações e selecione **Avançar**.  
  - Registrou o Configuration Manager como uma ferramenta de gerenciamento "Aplicativo Web e/ou API Web" e que você tem a [ID de cliente desse registro](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).  
  - Criou uma chave de cliente para a ferramenta de gerenciamento registrada no Azure Active Directory.  

  - No Portal de gerenciamento do Azure, forneceu o aplicativo Web registrado com permissão para acessar o OMS, conforme descrito em [Fornecer o Configuration Manager com permissões para OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).  

4.  Na página **Azure Active Directory**, defina as configurações de conexão do OMS, fornecendo seu **Locatário**, sua **ID do cliente** e sua **Chave secreta do cliente** e, em seguida, selecione **Avançar**.  

5.  Na página **Configuração de Conexão do OMS**, forneça as suas configurações de conexão preenchendo sua **assinatura do Azure**, **grupo de recursos do Azure** e **espaço de trabalho do Operations Management Suite**.  O espaço de trabalho deve coincidir com o espaço de trabalho que está configurado para o Agente de Gerenciamento da Microsoft que está instalado no ponto de conexão de serviço.  

6.  Verifique suas configurações de conexão na página **Resumo** e, em seguida, selecione **Avançar**. A página **Andamento** mostrará o status da conexão e, em seguida, clique em **Concluir**.

Depois de vincular o Configuration Manager ao OMS, será possível adicionar ou remover coleções e exibir as propriedades da conexão do OMS.

### <a name="verify-the-oms-connector-properties"></a>Verifique as propriedades do conector do OMS
1.  No console do Configuration Manager, vá até **Administração** > **Serviços de Nuvem** e, em seguida, selecione **Conector do OMS** para abrir a página **Conexão do OMS ****.
2.  Nessa página, há duas guias:
  - **Azure Active Directory:**   
    Esta guia mostra **Locatário**, **ID do Cliente**, **Expiração da Chave Secreta do Cliente** e permite que você verifique se sua chave secreta do cliente expirou.

  - **Propriedades de Conexão do OMS:**  
    Esta guia mostra sua **Assinatura do Azure**, **grupo de recursos do Azure**, **Espaço de Trabalho do Operations Management Suite** e uma lista de **Coleções de dispositivos para os quais o Operations Management Suite pode obter dados**. Use os botões **Adicionar** e **Remover** para modificar quais coleções são permitidas.

### <a name="fairfaxconfig"> </a> Usar o conector do OMS com a nuvem Azure Governamental


1.  Em qualquer computador que tenha o console do Configuration Manager instalado, edite o seguinte arquivo de configuração para apontar para a nuvem governamental: ***&lt;CM install path>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Edições:**

    Altere o valor do nome da configuração *FairFaxArmResourceID* para que seja igual a “https://management.usgovcloudapi.net/”

   - **Original:** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Editado:**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Altere o valor para o nome da configuração *FairFaxAuthorityResource* para que seja igual a "https://login.microsoftonline.com/"

  - **Original:**&lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **Editado:**&lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.com/&lt;/value>

2.  Depois de salvar o arquivo com as duas alterações, reinicie o console do Configuration Manager no mesmo computador e, em seguida, use esse console para instalar o conector do OMS. Para instalar o conector, use as informações em [Sincronizar dados do Configuration Manager para o Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) e selecione o **Espaço de trabalho do Operations Management Suite** que está na nuvem Microsoft Azure Governamental.

3.  Após instalar o conector do OMS, a conexão com a nuvem Governamental estará disponível quando você usar um console que se conecta ao site.
