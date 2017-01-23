---
title: "Gerenciar atualizações do Office 365 ProPlus | Microsoft Docs"
description: "O Configuration Manager sincroniza a atualização de clientes do Office 365 do catálogo do WSUS para o servidor do site para disponibilizar as atualizações para implantar em clientes."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/04/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 46c8004afee4b18d5c7a2fcc5dac0f7d0d1f823c
ms.openlocfilehash: fb2fc409c2f734816e4f3bf93d61a748d957ebf0

---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>Gerenciar atualizações do Office 365 ProPlus com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A partir do Configuration Manager versão 1602, ele tem a capacidade de gerenciar atualizações de clientes do Office 365 usando o fluxo de trabalho do gerenciamento de atualizações de software. Quando a Microsoft publica uma nova atualização de cliente do Office 365 na Rede de Distribuição de Conteúdo do Office (CDN), a Microsoft também publica um pacote de atualização para o Windows Server Update Services (WSUS). Após o Configuration Manager sincronizar a atualização de clientes do Office 365 do catálogo do WSUS para o servidor do site, a atualização ficará disponível para implantar em clientes.

## <a name="office-365-client-management-dashboard"></a>Painel de gerenciamento de clientes do Office 365  
Começando do Configuration Manager versão 1610, o painel Gerenciamento de Clientes do Office 365 está disponível no console do Configuration Manager. Para exibir o painel, acesse **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Cliente do Office 365**.

<!--- >[!NOTE]
>In the **What's New** workspace in the Configuration Manager console, the new dashboard is incorrectly named **Office 365 Servicing dashboard**. --->

O painel exibe gráficos para o seguinte:

- Número de clientes do Office 365
- Versões do cliente do Office 365
- Idiomas do cliente do Office 365
- Canais do cliente do Office 365     
Para mais informações, confira [Visão geral dos canais de atualização do Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

Na parte superior do painel, use a configuração suspensa **Coleção** para filtrar os dados do painel por membros de uma coleção específica.

<!---
 On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).
--->

## <a name="deploy-office-365-updates-with-configuration-manager"></a>Implantar atualizações do Office 365 com o Configuration Manager
Use as etapas a seguir para implantar atualizações do Office 365 com o Configuration Manager:

1.  [Verifique os requisitos](https://technet.microsoft.com/library/mt628083.aspx) para usar o Configuration Manager para gerenciar atualizações de clientes do Office 365 na seção **Requisitos para usar o Configuration Manager para gerenciar atualizações de clientes do Office 365** do tópico.  

2.  [Configure os pontos de atualização de software](../get-started/configure-classifications-and-products.md) para sincronizar as atualizações de clientes do Office 365. Defina as **atualizações** para a classificação e selecione o **cliente do Office 365**. Talvez seja necessário sincronizar atualizações de software pelo menos uma vez antes que o produto cliente do Office 365 esteja disponível para sua escolha. É necessário sincronizar as atualizações de software depois de configurar os pontos de atualização de software para usar a classificação **Atualizações**.  

3.  Permita que os clientes do Office 365 recebam atualizações do Configuration Manager. É possível fazer isso usando configurações de cliente do Configuration Manager ou usar a política de grupo. Use um dos seguintes métodos para habilitar o cliente:  
    - Método 1: a partir do Configuration Manager versão 1606, é possível usar a configuração do cliente do Configuration Manager para gerenciar o agente cliente do Office 365. Depois de definir essa configuração e implantar as atualizações do Office 365, o agente cliente do Configuration Manager se comunica com o agente cliente do Office 365 para baixar atualizações do Office 365 de um ponto de distribuição e instalá-las. O Configuration Manager faz um inventário das configurações de cliente do Office 365 ProPlus.
      1.  No console do Configuration Manager, escolha **Administração** > **Visão Geral** > **Configurações do Cliente**.  

      2.  Abra as configurações do dispositivo apropriado para habilitar o agente cliente. Para obter mais informações sobre configurações do cliente padrão e personalizadas, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Clique em **Atualizações de Software** e selecione **Sim** para a configuração **Habilitar o gerenciamento do Agente Cliente do Office 365**.  

    - Método 2: [Permitir que os clientes do Office 365 recebam atualizações](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) do Configuration Manager usando a Ferramenta de Implantação do Office ou a Política de Grupo.  

4. [Implante as atualizações do Office 365](deploy-software-updates.md) nos clientes.  

<!--  ## Add other languages for Office 365 update downloads
Beginning in Configuration Manager version 1610, you can add support for Configuration Manager to download updates for any languages supported by Office 365 regardless of whether they are supported in Configuration Manager.

### To add support to download updates for additional languages
Use the following procedure on the central administration site, or stand-alone primary site, where the software update point site system role is installed.
1. From a command prompt, type *wbemtest* as an administrative user to open the Windows Management Instrumentation Tester.
2. Click **Connect**, and then type *root\sms\site_<siteCode>*.
3. Click **Query**, and then run the following query:
   *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*
4. Double-click the object with the site code for the central administration site or stand-alone primary site.

5. Browse the properties for View Embedded.
3). Find the SMS_EmbeddedProperty instance with the PropertyName of "AdditionalUpdateLanguagesForO365"
4). Set Value2 to be additional languages, e.g.:  pt-pt,af-za,nn-no, and save
5). Right click to download an O365 update, choose languages from UI
6). Verify that the language packs got downloaded including the UI specified ones plus the SDK specified ones. Admin can check the content package share specified to verify this.
-->

<!-- ## Change the update channel after you enable Office 365 clients to receive updates from Configuration Manager
To change the update channel after you enable Office 365 clients to receive updates from Configuration Manager, you must distribute a registry key value change to Office 365 clients using group policy. Change the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** registry key to use one of the following values:

- Current Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Deferred Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- First Release for Current Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- First Release for Deferred Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf
-->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->



<!--HONumber=Jan17_HO1-->


