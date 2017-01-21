---
title: Gerenciar aplicativos da Windows Store para Empresas | Microsoft Docs
description: Gerenciar e implantar aplicativos da Windows Store para Empresas usando o System Center Configuration Manager.
ms.custom: na
ms.date: 11/19/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3847a85c11d7b72b84095ba9add563bdf5c49a75
ms.openlocfilehash: 605cdd01d767dda3467198f5e6539448f9b559f6

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Gerenciar aplicativos da Windows Store para Empresas com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Na [Windows Store para Empresas](https://www.microsoft.com/business-store), é possível encontrar e comprar aplicativos Windows para sua organização, individualmente ou por volume. Ao conectar o repositório ao Configuration Manager, é possível sincronizar a lista de aplicativos comprados com o Configuration Manager, exibi-los no console do Configuration Manager e implantá-los da mesma forma como você implantaria qualquer outro aplicativo.


## <a name="online-and-offline-apps"></a>Aplicativos online e offline

A Windows Store para Empresas dá suporte a dois tipos de aplicativo:

- **Online** – esse tipo de licença exige que os usuários e dispositivos se conectem ao repositório para obter um aplicativo e sua licença. Dispositivos Windows 10 devem ser ingressados em um domínio do Azure Active Directory.
- **Offline** – as organizações podem armazenar aplicativos e licenças em cache para implantá-los diretamente em suas redes locais, sem se conectar à loja ou ter uma conexão com a Internet.

Leia mais sobre o [Windows Store para Empresas](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview).

O Configuration Manager dá suporte ao gerenciamento de aplicativos da Windows Store para Empresas em dispositivos Windows 10 que executam o cliente do Configuration Manager e em dispositivos Windows 10 registrados no Microsoft Intune (configuração híbrida). O Configuration Manager oferece os seguintes recursos para aplicativos online e offline.

> [!IMPORTANT]
> Para usar essas funcionalidades, os dispositivos Windows 10 devem executar a versão de novembro de 2015 (1511) ou posterior.

|Funcionalidade|Aplicativos offline|Aplicativos online|
|------------|------------|------------|
|Sincronizar dados do aplicativo com o Configuration Manager<br>(A sincronização ocorre a cada 24 horas ou é possível iniciar uma sincronização imediata.)|Sim|Sim|
|Criar aplicativos do Configuration Manager de aplicativos da loja|Sim|Sim|
|Suporte para aplicativos gratuitos da loja|Sim|Sim<sup>1</sup>|
|Suporte para aplicativos pagos da loja|Não|Sim<sup>1</sup>|
|Suporte para implantações obrigatórias em coleções de usuários ou dispositivos|Sim|Sim<sup>1</sup>|
|Suporte para implantações disponíveis em coleções de usuários ou dispositivos|Sim<sup>2</sup>|Não|

<sup>1</sup>O suporte é válido somente para dispositivos gerenciados pelo Intune. Nada o impede de criar um aplicativo online no console do Configuration Manager e implantá-lo em um dispositivo gerenciado pelo cliente do Configuration Manager, mas a implantação não funcionará. Os usuários serão direcionados para a página relevante da loja de aplicativos para instalar o aplicativo manualmente.

<sup>2</sup>O suporte é válido somente para dispositivos gerenciados pelo cliente do Configuration Manager.

<!--- ## Activate the Windows Store for Business capability
Because this is a pre-release feature, before you can connect Configuration Manager to the Windows Store for Business, you must take the following steps:

**Give your consent to use pre-release features**
1. In the **Administration** workspace of the Configuration Manager console, choose **Site Configuration** > **Sites**.
2. Select the top-level site in your hierarchy, then, open **Hierarchy Settings**.
3. In the **Hierarchy Settings Properties** dialog box, check the box, **Consent to use Pre-Release** features.
4. Choose **OK**.

**Activate the Windows Store for Business capability**
1. In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Features**.
2. Select **Windows Store for Business Integration**, and then in the **Home** tab, in the **Features** group, choose **Turn on**.
3. Close and re-open the Configuration Manager console.
4. You'll now see the node **Windows Store for Business** in the **Administration** workspace under **Cloud Services**. --->

## <a name="set-up-windows-store-for-business-synchronization"></a>Configurar a sincronização da Windows Store para Empresas

> [!IMPORTANT]
> Ao configurar uma conexão entre o Configuration Manager e a Windows Store para Empresas, é necessário fornecer uma pasta em que o conteúdo do aplicativo sincronizado do repositório será mantido.
Para garantir que essa pasta é segura e que seu conteúdo pode ser implantado em dispositivos, verifique se as seguintes permissões existem:
-   O computador no qual você instala a função do sistema de sites do ponto de conexão de serviço (o site de nível superior na hierarquia) deve ter permissões de leitura e gravação na pasta especificada durante o uso da conta **Computer$**.
-   O autor do aplicativo deve ter permissões de leitura da pasta especificada.
-   A conta **Computer$** de cada computador que hospeda uma instância do Provedor de SMS deve poder usar a pasta especificada.


No Azure Active Directory, registre o Configuration Manager como uma ferramenta de gerenciamento de API Web ou de aplicativo Web. Isso fornecerá uma ID de cliente que você precisará mais tarde.
1. No nó [https://manage.windowsazure.com](https://manage.windowsazure.com) do Active Directory, selecione o Azure Active Directory e escolha **Aplicativos** > **Adicionar**.
2.  Escolha **Adicionar um aplicativo que minha organização está desenvolvendo**.
3.  Insira um nome para o aplicativo, selecione **Aplicativo Web** e/ou **API Web** e escolha **Avançar**.
4.  Insira a mesma URL para **URL de Entrada** e **URI da ID do Aplicativo**. A URL pode ser qualquer uma e não precisa ser resolvida para um endereço real. Por exemplo, você pode inserir *https://seudomínio/sccm*.
5.  Conclua o assistente.

No Azure Active Directory, crie uma chave de cliente para a ferramenta de gerenciamento registrada.
1.  Realce o aplicativo que você acabou de criar e escolha **Configurar**.
2.  Em **Chaves**, selecione uma duração na lista e escolha **Salvar**. Isso criará uma nova chave de cliente. Não saia desta página antes de carregar com êxito a Windows Store para Empresas no Configuration Manager.

Na Windows Store para Empresas, configure o Configuration Manager como a ferramenta de gerenciamento do repositório.
1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e se conecte, se solicitado.
2.  Aceite os termos de uso, se solicitado.
3.  Em **Ferramentas de Gerenciamento**, escolha **Adicionar uma ferramenta de gerenciamento**.
4.  Em **Pesquisar a ferramenta por nome**, digite o nome do aplicativo que você criou anteriormente no Azure Active Directory e escolha **Adicionar**.
5.  Escolha **Ativar** ao lado do aplicativo que você acabou de importar.
6.  Na página **Gerenciar > Informações da Conta**, selecione **Exibir Aplicativos Licenciados Offline** se desejar permitir a compra de aplicativos licenciados offline.

Adicione a conta do repositório ao Configuration Manager.

1. Verifique se você comprou pelo menos um aplicativo da Windows Store para Empresas. No espaço de trabalho **Administração** do console do Configuration Manager, expanda **Serviços de Nuvem** e escolha **Windows Store para Empresas**.
2.  Na guia **Início**, no grupo **Windows Store para Empresas**, escolha **Adicionar Conta da Windows Store para Empresas**.
3.  Adicione sua ID de locatário, ID do cliente e chave de segredo do cliente do Azure Active Directory e conclua o assistente.
4. Quando terminar, você verá a conta configurada na lista **Windows Store para Empresas** no console do Configuration Manager.

Altere os idiomas do aplicativo que serão mostrados no Catálogo de Aplicativos para os usuários baixarem.

1.  No espaço de trabalho **Administração** do console do Configuration Manager, escolha **Serviços de Nuvem** > **Atualizações e Manutenção** > **Windows Store para Empresas**.
2.  Selecione sua conta da Windows Store para Empresas e escolha **Propriedades**.
3.  Selecione a guia **Idioma**.
4.  Adicione ou remova os idiomas que serão mostrados no Catálogo de Aplicativos. Selecione o idioma padrão do catálogo de aplicativos que será disponibilizado para os usuários.

>[!IMPORTANT]
>Nesta versão, se você alterar os idiomas que serão sincronizados, será necessário reiniciar o serviço SMS Executive no servidor do site antes que as configurações de idioma entrem em vigor.


Modifique a chave de segredo do cliente do Azure Active Directory.

1.  No espaço de trabalho **Administração** do console do Configuration Manager, escolha **Serviços de Nuvem** > **Atualizações e Manutenção** > **Windows Store para Empresas**.
2.  Selecione sua conta da Windows Store para Empresas e escolha **Propriedades**.
3.  Na caixa de diálogo **Propriedades da Conta da Windows Store para Empresas**, insira uma nova chave no campo **Chave de segredo do cliente** e escolha **Verificar**. Após a verificação, escolha **Aplicar** e feche a caixa de diálogo.

## <a name="synch-apps-from-the-store-with-configuration-manager"></a>Sincronizar aplicativos da loja com o Configuration Manager

A sincronização ocorre a cada 24 horas ou é possível iniciar uma sincronização imediata usando este procedimento:

1. No espaço de trabalho **Administração** do console do Configuration Manager, escolha **Serviços de Nuvem** > **Atualizações e Manutenção** > **Windows Store para Empresas**.
3.  Na guia **Início**, no grupo **Sincronização**, escolha **Sincronizar Agora**.
4.  O aplicativo que você comprou será exibido no nó **Informações de Licença para Aplicativos da Loja** do espaço de trabalho **Gerenciamento de Aplicativos**.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Criar e implantar um aplicativo do Configuration Manager por meio de um aplicativo da Windows Store para Empresas

Este procedimento pressupõe que você tenha adquirido, no mínimo, um aplicativo gratuito ou comprado pelo menos um aplicativo licenciado online pago na Windows Store para Empresas.

1.  No espaço de trabalho **Biblioteca de Software** do console do Configuration Manager, expanda **Gerenciamento de Aplicativos** e escolha **Informações de Licença para Aplicativos da Loja**.
2.  Escolha o aplicativo que você deseja implantar e, na guia **Início**, no grupo **Criar**, escolha **Criar Aplicativo**.
É criado um aplicativo do Configuration Manager contendo o aplicativo da Windows Store para Empresas. Em seguida, é possível implantar e monitorar o aplicativo, como você faria com qualquer outro aplicativo do Configuration Manager.

> [!IMPORTANT]
> Para dispositivos registrados no Intune, os aplicativos implantados ficam disponíveis somente para o usuário que registrou o dispositivo originalmente. Nenhum outro usuário poderá usar o aplicativo.

## <a name="monitor-windows-store-for-business-apps"></a>Monitorar aplicativos da Windows Store para Empresas

No espaço de trabalho **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e escolha **Informações de Licença para Aplicativos da Loja**.

Para cada aplicativo da loja que você gerenciar, é possível exibir informações sobre o aplicativo, incluindo nome, plataforma, número de licenças do aplicativo que você tem e número de licenças disponíveis.



<!--HONumber=Dec16_HO3-->


