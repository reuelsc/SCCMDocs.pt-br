---
title: "Gerenciar atualizações do Office 365 ProPlus | Microsoft Docs"
description: "O Configuration Manager sincroniza a atualização de clientes do Office 365 do catálogo do WSUS para o servidor do site para disponibilizar as atualizações para implantar em clientes."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 05/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.translationtype: Human Translation
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: 744bcb603a02bc7d237ffb3a7f925037b94a23ba
ms.contentlocale: pt-br
ms.lasthandoff: 06/01/2017

---

# <a name="manage-office-365-proplus-with-configuration-manager"></a>Gerenciar o Office 365 ProPlus com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager sincroniza as atualizações de cliente do Office 365 e as disponibiliza para implantar para os clientes com o Office 365 instalado. A partir do Configuration Manager versão 1610, você pode examinar as informações de cliente do Office 365 no painel do Gerenciamento de clientes do Office 365.

A partir do Configuration Manager versão 1602, ele tem a capacidade de gerenciar atualizações de clientes do Office 365 usando o fluxo de trabalho do gerenciamento de atualizações de software. Quando a Microsoft publica uma nova atualização de cliente do Office 365 na Rede de Distribuição de Conteúdo do Office (CDN), a Microsoft também publica um pacote de atualização para o Windows Server Update Services (WSUS). Após o Configuration Manager sincronizar a atualização de clientes do Office 365 do catálogo do WSUS para o servidor do site, a atualização ficará disponível para implantar em clientes.

A partir da versão 1702, você pode iniciar o Instalador do Office 365 no painel de Gerenciamento de clientes do Office 365 para facilitar a experiência inicial de instalação do aplicativo do Office 365. O assistente permite que você defina as configurações de instalação do Office 365, baixe arquivos das redes de distribuição de conteúdo (CDNs) do Office, e crie e implante um aplicativo de script com o conteúdo.

## <a name="office-365-client-management-dashboard"></a>Painel de gerenciamento de clientes do Office 365  
Começando do Configuration Manager versão 1610, o painel Gerenciamento de Clientes do Office 365 está disponível no console do Configuration Manager. Para exibir o painel, acesse **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Cliente do Office 365**.

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

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Dados de exibição no painel de gerenciamento de clientes do Office 365
Os dados que são exibidos no painel de gerenciamento de clientes do Office 365 vêm de inventário de hardware. O inventário de hardware deve estar habilitado e você deve selecionar a classe de inventário de hardware **Configurações do Office 365 ProPlus** antes de os dados serem exibidos no painel de controle.
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Como exibir dados no painel de gerenciamento de clientes do Office 365
1. Habilite o inventário de hardware se ele ainda não estiver habilitado. Para mais detalhes, consulte [Configurar inventário de hardware](\sccm\core\clients\manage\configure-hardware-inventory).
2. No console do Configuration Manager, acesse **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  
3. Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  
4. No **configurações do cliente padrão** caixa de diálogo, clique em **inventário de Hardware**.  
5. No **configurações do dispositivo** clique em **Definir Classes**.  
6. Na caixa de diálogo **Classes de Inventário de Hardware**, selecione **Configurações do Office 365 ProPlus**.  
7.  Clique em **OK** para salvar suas alterações e fechar o **Classes de inventário de Hardware** caixa de diálogo.  
O painel de gerenciamento de clientes do Office 365 começará a exibir dados à medida que o inventário de hardware for relatado.

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

> [!Important]
> Quando você tiver um cliente do Office 365 com mais de um idioma e baixar atualizações para menos idiomas, as atualizações não serão instaladas. Por exemplo, digamos que você tenha um cliente do Office 365 com en-us e de-de. No servidor do site, você baixa e implanta apenas conteúdo de en-us para uma atualização correspondente do Office 365. Quando o usuário inicia a instalação desta atualização do Centro de Software, a atualização travará durante o download do conteúdo. Você deve baixar e implantar as atualizações nos mesmos idiomas que os clientes do Office 365.  


## <a name="add-other-languages-for-office-365-update-downloads"></a>Adicionar outros idiomas a downloads de atualização do Office 365
A partir do Configuration Manager versão 1610, você pode adicionar suporte do Configuration Manager para baixar atualizações de quaisquer idiomas compatíveis com o Office 365, independentemente de serem compatíveis com o Configuration Manager.
> [!IMPORTANT]  
> A configuração de idiomas de atualização adicionais do Office 365 é aplicada a todo o site. Depois de adicionar os idiomas usando o procedimento a seguir, todas as atualizações do Office 365 serão baixadas nesses idiomas, bem como os idiomas que você selecionar na página Seleção de idioma nos assistentes Baixar atualizações de software ou Implantar atualizações de software.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Para adicionar suporte para baixar atualizações para outros idiomas
Use o procedimento a seguir no site de administração central ou no site primário autônomo, em que está instalada a função do sistema de site do ponto de atualização do software.
1. Em um prompt de comando, digite *wbemtest* como administrador para abrir o Testador de Instrumentação de Gerenciamento do Windows.
2. Clique em **Conectar**e, em seguida, digite *root\sms\site_&lt;siteCode&gt;*.
3. Clique em **Consulta** e, em seguida, execute a seguinte consulta: *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Consulta WMI](..\media\1-wmiquery.png)
4. No painel de resultados, clique duas vezes no objeto com o código de site para o site de administração central ou o site primário autônomo.
5. Selecione a propriedade **Acessórios**, clique em **Editar propriedade** e, em seguida, clique em **Exibir incorporado**.
![Editor de propriedades](..\media\2-propeditor.png)
6. Começando no primeiro resultado de consulta, abra cada objeto até encontrar aquele com **AdditionalUpdateLanguagesForO365** na propriedade **PropertyName**.
7. Selecione **Value2** e clique em **Editar propriedade**.  
![Editar a propriedade Value2](..\media\3-queryresult.png)
8. Adicione mais idiomas à propriedade **Value2** e clique em **Salvar propriedade**.  
Por exemplo, pt-pt (para português - Portugal), af-za (para africâner - África do Sul), nn-no (para Norueguês (Nynorsk) - Noruega), etc.  
![Adicionar idiomas no Editor de propriedades](..\media\4-props.png)  
9. Clique em **Fechar**, em **Fechar**, em **Salvar propriedade**, em **Salvar objeto** (se você clicar em **Fechar** aqui, os valores serão descartados), em **Fechar** e, em seguida, em **Sair** para sair do Testador de Instrumentação de Gerenciamento do Windows.
10. No console do Configuration Manager, vá para **Biblioteca de software** > **Visão geral** > **Gerenciamento de clientes do Office 365** > **Atualizações do Office 365**.
11. Agora, ao baixar as atualizações do Office 365, elas serão baixadas no idioma selecionado no assistente e nos idiomas que você configurou neste procedimento. Para verificar as atualizações baixadas nesses idiomas, vá para a origem do pacote para a atualização e procure por arquivos com o código de idioma no nome do arquivo.  
![Nomes de arquivos com idiomas adicionais](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Alterar o canal de atualização após habilitar os clientes do Office 365 para receber atualizações do Configuration Manager
Para alterar o canal de atualização após habilitar os clientes do Office 365 para receber atualizações do Configuration Manager, você pode usar a política de grupo para distribuir uma alteração de valor da chave do registro para os clientes do Office 365. Altere a chave do registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** para usar um dos seguintes valores:

- Canal atual:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Canal adiado:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- Primeira versão do canal atual:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- Primeira versão do canal adiado:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf

## <a name="deploy-office-365-apps"></a>Implantar aplicativos do Office 365  
A partir da versão 1702, você pode iniciar o Instalador do Office 365 no painel de Gerenciamento de clientes do Office 365 para facilitar a experiência inicial de instalação do aplicativo do Office 365. O assistente permite que você defina as configurações de instalação do Office 365, baixe arquivos das redes de distribuição de conteúdo (CDNs) do Office, e crie e implante um aplicativo de script para os arquivos.

Isso é especialmente útil porque as atualizações do Office 365 não são aplicáveis para clientes sem o Office 365 instalado. Antes da versão 1702, para instalar os aplicativos do Office 365 pela primeira vez em clientes, você precisava baixar manualmente a Ferramenta de Implantação do Office 365 (ODT) e os arquivos originais de instalação do Office 365, incluindo todos os pacotes de idiomas de que você precisava, e gerar o Configuration.xml que especificava a versão correta do Office e o canal. Em seguida, precisava criar e implantar um pacote herdado ou um aplicativo de script para os clientes para instalar os aplicativos do Office 365.

> [!NOTE]
> - O computador que executa o Instalador do Office 365 deve ter acesso à Internet.  
> - O usuário que executa o Instalador do Office 365 deve ter acesso de **leitura** e **gravação** ao compartilhamento de local de conteúdo que é fornecido no assistente.
> - Se você receber um erro 404 download, copie os seguintes arquivos para a pasta %temp% do usuário:
>    - [releasehistory.xml](http://officecdn.microsoft.com.edgesuite.net/wsus/releasehistory.cab)
>    - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  
> - Depois de criar e implantar os aplicativos do Office 365 usando o Instalador do Office 365, o Configuration Manager não gerenciará as atualizações do Office por padrão. Para permitir que os clientes do Office 365 recebam atualizações do Configuration Manager, veja [Implantar atualizações do Office 365 com o Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>Para implantar aplicativos do Office 365 a clientes a partir do Painel de Gerenciamento de Clientes do Office 365
1. No console do Configuration Manager, navegue até **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Cliente do Office 365**.
2. Clique em **Office 365 Installer (Instalador do Office 365)** no painel superior direito. O Assistente de Instalação de Cliente do Office 365 é aberto.
3. Na página **Configurações de Aplicativo**, forneça um nome e uma descrição para o aplicativo, insira o local de download para os arquivos e clique em **Avançar**. Observe que o local deve ser especificado no formato &#92;&#92;*servidor*&#92;*compartilhamento*.
4. Na página **Import Client Settings (Importar Configurações do Cliente)**, escolha se deseja importar as configurações do cliente do Office 365 de um arquivo de configuração XML existente ou especificar as configurações manualmente e clique em **Avançar**.  

    Quando você tiver um arquivo de configuração existente, insira o local do arquivo e vá para a etapa 7. Observe que o local deve ser especificado no formato &#92;&#92;*servidor*&#92;*compartilhamento*&#92;*nome do arquivo*.XML.
    > [!IMPORTANT]    
    > O arquivo de configuração XML deve conter apenas [idiomas com suporte pelo cliente do Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx).

5. Na página **Client Products (Produtos do Cliente)**, selecione o pacote do Office 365 usado, selecione os aplicativos que deseja incluir, selecione quaisquer produtos Office adicionais que devem ser incluídos e clique em **Avançar**.
6. Na página **Configurações do Cliente**, escolha as configurações a serem incluídas e clique em **Avançar**.
7. Na página **Implantação**, escolha se deseja implantar o aplicativo e clique em **Avançar**.  
Se você optar por não implantar o pacote no assistente, vá para a etapa 9.
8. Configure o restante das páginas do assistente como você faria para uma implantação de aplicativo típica. Para obter detalhes, consulte [Create and deploy an application (Criar e implantar um aplicativo)](/sccm/apps/get-started/create-and-deploy-an-application).
9. Conclua o assistente.
10. Você pode implantar ou editar o aplicativo exatamente como faria com qualquer outro aplicativo no Configuration Manager de **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Aplicativos** > **Aplicativos**.   

> [!IMPORTANT]
> O aplicativo do Office 365 que você cria e implanta usando o Assistente para aplicativo do Office 365 no Configuration Manager não é gerenciado automaticamente pelo Configuration Manager até que você habilite a configuração de agente de cliente de atualização **Habilitar o gerenciamento do agente do cliente do Office 365**. Para obter detalhes, veja [Sobre configurações do cliente](/sccm/core/clients/deploy/about-client-settings).

>[!NOTE]
>Depois de implantar aplicativos do Office 365, você pode criar regras de implantação automática para manter os aplicativos. Para criar uma regra de implantação automática para aplicativos do Office 365, clique em **Criar um ADR** no painel de gerenciamento de cliente do Office 365 e selecione **Cliente do Office 365** quando escolher o produto. Para mais informações, confira [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates) (Implantar atualizações de software automaticamente).

<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->

