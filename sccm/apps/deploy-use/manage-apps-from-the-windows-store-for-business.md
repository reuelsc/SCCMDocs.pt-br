---
title: Gerenciar aplicativos da Microsoft Store para Empresas
titleSuffix: Configuration Manager
description: Gerenciar e implantar aplicativos da Microsoft Store para Empresas usando o System Center Configuration Manager.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: "11"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 0400262c6d00a83a3da10cb0a60072552dd14360
ms.sourcegitcommit: 1dd051d8548a19b724bb8f9e6a2278a4901ed916
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2017
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-system-center-configuration-manager"></a>Gerenciar aplicativos da Microsoft Store para Empresas com o System Center Configuration Manager
Na [Microsoft Store para Empresas](https://www.microsoft.com/business-store), é possível encontrar e adquirir aplicativos Windows para sua organização, individualmente ou por volume. Ao conectar a loja ao Configuration Manager, é possível sincronizara lista de aplicativos adquiridos com o Configuration Manager. Em seguida, é possível exibir esses aplicativos no console do Configuration Manager e implantá-los como você implantaria qualquer outro aplicativo.


## <a name="online-and-offline-apps"></a>Aplicativos online e offline

A Microsoft Store para Empresas é compatível com dois tipos de aplicativo:

- **Online** – este tipo de licença exige que usuários e dispositivos se conectem à loja para obter um aplicativo e sua licença. Dispositivos Windows 10 devem ser ingressados em um domínio do Azure Active Directory.
- **Offline** – permite que você armazene em cache aplicativos e licenças para implantar diretamente em sua rede local, sem se conectar à loja ou ter uma conexão com a Internet.

[Leia mais](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) sobre a Microsoft Store para Empresas.

O Configuration Manager é compatível com o gerenciamento de aplicativos da Microsoft Store para Empresas em dispositivos Windows 10 que executam o cliente do Configuration Manager e a dispositivos Windows 10 registrados no Microsoft Intune (conhecido como configuração híbrida). O Configuration Manager oferece os seguintes recursos para aplicativos online e offline.

> [!IMPORTANT]
> Para usar essa funcionalidade, dispositivos Windows 10 devem estar executando a versão de novembro de 2015 (1511) ou posterior.


|Funcionalidade|Aplicativos offline|Aplicativos online|
|------------|------------|------------|
|Sincronizar dados do aplicativo com o Configuration Manager<br>(a sincronização ocorre a cada 24 horas)|Sim|Sim|
|Criar aplicativos do Configuration Manager de aplicativos da loja|Sim|Sim|
|Suporte para aplicativos gratuitos da loja|Sim|Sim|
|Suporte para aplicativos pagos da loja|Não|Sim|
|Suporte para implantações obrigatórias em coleções de usuários ou dispositivos|Sim|Sim|
|Suporte para implantações disponíveis em coleções de usuários ou dispositivos|Sim|Sim|
|Suporte a aplicativos de linha de negócios da loja|Sim|Sim|

Para implantar aplicativos licenciados online em PCs com Windows 10 com o cliente do Configuration Manager, ele deverá estar executando a Atualização do Windows 10 para Criadores ou posterior.

## <a name="deploying-online-apps-using-the-microsoft-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Implantando aplicativos online usando a Microsoft Store para Empresas com PCs que executam o cliente do Configuration Manager
Antes de implantar aplicativos da Microsoft Store para Empresas em PCs que executam o cliente completo do Configuration Manager, considere os seguintes pontos:

- Para a funcionalidade completa, os PCs devem estar executando a Atualização do Windows 10 para Criadores, ou posterior.
- Os PCs devem estar ingressados no espaço de trabalho do Azure Active Directory e estar no mesmo locatário do AAD em que registrou a Microsoft Store para Empresas como uma ferramenta de gerenciamento.
- Quando o logon dos PCs tiver sido feito com a conta de administrador interno, eles não poderão acessar os aplicativos da Microsoft Store para Empresas.
- Os PCs devem ter uma conexão de Internet dinâmica com a Microsoft Store para Empresas.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Observações para PCs que executam versões anteriores do Windows 10
Em computadores que executam uma versão do Windows 10 anterior à Atualização para Criadores (com o cliente do Configuration Manager), a seguinte funcionalidade aplica-se:


- Quando a instalação for imposta pelo usuário que estiver instalando o aplicativo, pelo aplicativo que estiver atingindo seu prazo de instalação ou pela publicação da reavaliação de instalação para as implantações necessárias:
    - O aplicativo é "imposto" ao iniciar o aplicativo da Microsoft Store para Empresas. 
    - O usuário final deverá concluir a instalação pela loja antes que o aplicativo seja instalado
    - O status do aplicativo no console do Configuration Manager relatará falha com o erro "O aplicativo da Microsoft Store foi aberto no PC cliente e está aguardando o usuário concluir a instalação."
- No próximo ciclo de avaliação do aplicativo:
    - Se o aplicativo tiver sido instalado pelo usuário final da loja, o aplicativo relatará o status **Sucesso**. 
    - Se o usuário final não tiver tentado instalar o aplicativo pela loja:
        - As implantações necessárias tentarão inicializar a loja e impor novamente a instalação do aplicativo.
        - As implantações disponíveis não serão impostas novamente.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Outras observações para PCs que executam versões anteriores do Windows 10:

- Não é possível implantar aplicativos de linha de negócios da Microsoft Store para Empresas
- Quando você implanta aplicativos pagos pela loja, os usuários finais devem fazer logon na loja e comprar os aplicativos por sua conta.
- Se você tiver implantado uma Política de Grupo desabilitando o acesso à versão de consumidor da Microsoft Store, as implantações da Microsoft Store para Empresas não funcionarão, mesmo se ela estiver habilitada.


## <a name="set-up-microsoft-store-for-business-synchronization"></a>Configurar a sincronização da Microsoft Store para Empresas

### <a name="for-configuration-manager-versions-prior-to-1706"></a>Para versões do Configuration Manager anteriores à 1706

**No Azure Active Directory, registre o Configuration Manager como uma ferramenta de gerenciamento de "Aplicativo Web e/ou API da Web". Esta ação lhe dá uma ID de cliente que será necessária mais tarde.**
1. No nó Active Directory de [https://manage.windowsazure.com](https://manage.windowsazure.com), selecione seu Azure Active Directory e clique em **Aplicativos** > **Adicionar**.
2.  Clique em **Adicionar um aplicativo que minha organização esteja desenvolvendo**.
3.  Insira um nome para o aplicativo, selecione **Aplicativo Web** e/ou **API da Web** e clique na seta **Avançar**.
4.  Insira a mesma URL para **URL de Entrada** e **URI da ID do Aplicativo**. A URL pode ser qualquer uma e não precisa ser resolvida para um endereço real. Por exemplo, você pode inserir *https://seudomínio/sccm*.
5.  Conclua o assistente.

**No Azure Active Directory, crie uma chave de cliente para a ferramenta de gerenciamento registrada**
1.  Realce o aplicativo criado e clique em **Configurar**.
2.  Em **Chaves**, escolha uma duração na lista e clique em **Salvar**. Essa ação cria uma nova chave do cliente. Não saia dessa página até que você tenha carregado com êxito a Microsoft Store para Empresas no Configuration Manager.

**Na Microsoft Store para Empresas, configure o Configuration Manager como a ferramenta de gerenciamento da loja**
1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e se conecte, se solicitado.
2.  Aceite os termos de uso, se solicitado.
3.  Em **Ferramentas de Gerenciamento**, clique em **Adicionar uma ferramenta de gerenciamento**.
4.  Em **Pesquisar a ferramenta por nome**, digite o nome do aplicativo que você criou anteriormente no AAD e clique em **Adicionar**.
5.  Clique em **Ativar** ao lado do aplicativo importado.
6.  Na página **Gerenciar > Informações da Conta**, selecione **Exibir Aplicativos Licenciados Offline** se quiser permitir que aplicativos licenciados offline sejam comprados.

**Adicionar a conta da loja ao Configuration Manager**

1. Verifique se você comprou pelo menos um aplicativo da Microsoft Store para Empresas. No espaço de trabalho **Administração** do console do Configuration Manager, expanda **Serviços de Nuvem** e clique em **Microsoft Store para Empresas**.
2.  Na guia **Início**, no grupo **Microsoft Store para Empresas**, clique em **Adicionar conta da Microsoft Store para Empresas**. 
3.  Adicione a ID de locatário, a id de cliente e a chave de cliente do Azure Active Directory e conclua o assistente.
4. Quando terminar, será possível ver a conta configurada na lista **Microsoft Store para Empresas** no console do Configuration Manager.

### <a name="for-configuration-manager-version-1706-and-later"></a>Para a versão do Configuration Manager anterior à 1706

1. No console, vá para **Administração** > **Visão geral** > **Gerenciamento de serviços de nuvem** > **Azure** > **Serviços do Azure** e, em seguida, escolha **Configurar serviços do Azure** para iniciar o **Assistente de serviços do Azure**.
2. Na página de **Serviços do Azure**, selecione o serviço que deseja configurar e, em seguida, clique em **Próxima**.
3. Na página **Geral**, forneça um nome amigável para o Nome do serviço do Azure e uma descrição opcional e clique **Próxima**.
4. Na página do **Aplicativo**, especifique seu ambiente do Azure e, em seguida, clique em **Procurar** para abrir a janela do **Aplicativo de Servidor**.
5. Na janela do **aplicativo de servidor**, selecione o aplicativo de servidor que você deseja usar e depois clique em **OK**. Aplicativos de servidor são os aplicativos Web do Azure que contêm as configurações da sua conta do Azure, incluindo sua ID de locatário, ID de cliente e uma chave secreta para clientes. Se você não tiver um aplicativo de servidor disponível, use um dos seguintes:
    - **Criar**: Para criar um novo aplicativo de servidor, clique em **Criar**. Forneça um nome amigável para o aplicativo e o locatário. Em seguida, depois que você entrar no Azure, o Configuration Manager cria o aplicativo Web do Azure para você, incluindo a ID do cliente e a chave secreta para uso com o aplicativo Web. Posteriormente, você pode exibi-las no portal do Azure.
    - **Importar**: Para usar um aplicativo Web que já existe em sua assinatura do Azure, clique em **Importar**. Forneça um nome amigável para o aplicativo e o locatário e especifique a ID de locatário, ID do cliente e a chave secreta para o aplicativo Web do Azure que você deseja que o Configuration Manager use. Depois que você **verificar** as informações, clique em **OK** para continuar. 
6. Examine a página de **informações** e conclua quaisquer etapas adicionais e configurações, conforme indicado. Essas configurações são necessárias para usar o serviço com o Configuration Manager. Por exemplo, para configurar a Microsoft Store para Empresas:
    - No Azure, você deve registrar o Configuration Manager como um aplicativo Web ou API Web e registrar a ID do cliente. Você também pode especificar uma chave de cliente para uso pela ferramenta de gerenciamento (que é o Configuration Manager).
    - No console da Microsoft Store para Empresas, é necessário configurar o Configuration Manager como a ferramenta de gerenciamento de repositório, habilitar o suporte para aplicativos licenciados offline e, em seguida, adquirir pelo menos um aplicativo. 
7. Quando estiver pronto para continuar, clique em **Próximo**.
8. Na página **Configurações de aplicativo**, conclua as configurações de catálogo e idioma do aplicativo para este serviço e, em seguida, clique em **Próxima**.
9. Depois que o assistente for concluído, o console do Configuration Manager mostrará que você configurou a **Microsoft Store para Empresas** como um **Tipo de Serviço de nuvem**.




## <a name="create-and-deploy-a-configuration-manager-application-from-a-microsoft-store-for-business-app"></a>Crie e implante um aplicativo do Configuration Manager por meio de um aplicativo da Microsoft Store para Empresas.
1.  No espaço de trabalho **Biblioteca de Software** do console do Configuration Manager, expanda **Gerenciamento de Aplicativos** e clique em **Informações sobre Licença para Aplicativos da Loja**.
2.  Escolha o aplicativo que deseja implantar e, na guia **Início**, no grupo **Criar**, clique em **Criar Aplicativo**.
É criado um aplicativo do Configuration Manager contendo o aplicativo da Microsoft Store para Empresas. Em seguida, é possível implantar e monitorar o aplicativo, como você faria com qualquer outro aplicativo do Configuration Manager.

> [!IMPORTANT]
> Para dispositivos registrados no Intune, os aplicativos implantados ficam disponíveis somente para o usuário que registrou o dispositivo originalmente. Nenhum outro usuário pode acessar o aplicativo.

## <a name="next-steps"></a>Próximas etapas

No espaço de trabalho **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e clique em **Informações sobre Licença para Aplicativos da Loja**.

Para cada aplicativo da loja que gerencia, você pode ver as informações sobre o aplicativo, incluindo seu nome, a plataforma, quantas licenças do aplicativo que você possui e o número de licenças que estão disponíveis.

Depois de implantar aplicativos online, observe que as atualizações dese aplicativo virão diretamente da Microsoft Store.

Ao implantar aplicativos offline nos dispositivos Windows 10 com cliente do Configuration Manager (principalmente em ambientes multiusuário, como salas de aula), desabilite a Microsoft Store e/ou as atualizações de aplicativos por meio da Microsoft Store (por exemplo, usando a [política de grupo](https://docs.microsoft.com/en-us/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy)) para que os usuários não possam atualizar aplicativos externos a implantações do Configuration Manager. Além disso, depois que o administrador da Microsoft Store para Empresas adquirir o aplicativo (isto é, tornando-o disponível no estado offline para sincronização com o Configuration Manager), não o publique para usuários para eles poderem instalar ou atualizar online. Isso garantirá que todos os usuários receberão apenas atualizados do aplicativo por meio do Configuration Manager. 
