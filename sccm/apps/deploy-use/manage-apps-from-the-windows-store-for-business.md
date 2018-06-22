---
title: Gerenciar aplicativos da Microsoft Store para Empresas
titleSuffix: Configuration Manager
description: Gerenciar e implantar aplicativos da Microsoft Store para Empresas usando o System Center Configuration Manager.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4999784140ece9df49a28063e8660566f7206df0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336112"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-system-center-configuration-manager"></a>Gerenciar aplicativos da Microsoft Store para Empresas com o System Center Configuration Manager
Na [Microsoft Store para Empresas](https://www.microsoft.com/business-store), é possível encontrar e adquirir aplicativos Windows para sua organização, individualmente ou por volume. Ao conectar a loja ao Configuration Manager, é possível sincronizara lista de aplicativos adquiridos com o Configuration Manager. Em seguida, é possível exibir esses aplicativos no console do Configuration Manager e implantá-los como você implantaria qualquer outro aplicativo.


## <a name="online-and-offline-apps"></a>Aplicativos online e offline

A Microsoft Store para Empresas é compatível com dois tipos de aplicativo:

- **Online** – este tipo de licença exige que usuários e dispositivos se conectem à loja para obter um aplicativo e sua licença. Dispositivos Windows 10 devem ser ingressados em um domínio do Azure Active Directory.
- **Offline** – permite armazenar aplicativos e licenças em cache para implantá-los diretamente na rede local. Os dispositivos não precisam se conectar à loja nem ter uma conexão à Internet.

[Leia mais](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) sobre a Microsoft Store para Empresas.

O Configuration Manager dá suporte ao gerenciamento de aplicativos da Microsoft Store para Empresas em dispositivos Windows 10 com o cliente do Configuration Manager, bem como dispositivos Windows 10 registrados no Microsoft Intune. O Configuration Manager oferece os seguintes recursos para aplicativos online e offline.

> [!IMPORTANT]
> Para usar a Microsoft Store para Empresas, os dispositivos Windows 10 devem executar a versão de novembro de 2015 (1511) ou posterior.


|Funcionalidade|Aplicativos offline|Aplicativos online|
|------------|------------|------------|
|Sincronizar dados do aplicativo com o Configuration Manager<br>(a sincronização ocorre a cada 24 horas)|Sim|Sim|
|Criar aplicativos do Configuration Manager de aplicativos da loja|Sim|Sim|
|Suporte para aplicativos gratuitos da loja|Sim|Sim|
|Suporte para aplicativos pagos da loja|Não|Sim<sup>1</sup>|
|Suporte para implantações obrigatórias em coleções de usuários ou dispositivos|Sim|Sim|
|Suporte para implantações disponíveis em coleções de usuários ou dispositivos|Sim|Sim|
|Suporte a aplicativos de linha de negócios da loja|Sim|Sim|

<sup>1</sup>Para implantar aplicativos licenciados online em computadores Windows 10 com o cliente do Configuration Manager, eles devem executar a Atualização do Windows 10 para Criadores ou posterior.

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Implantando aplicativos online usando a Microsoft Store para Empresas com PCs que executam o cliente do Configuration Manager
Antes de implantar aplicativos da Microsoft Store para Empresas em PCs que executam o cliente completo do Configuration Manager, considere os seguintes pontos:

- Para a funcionalidade completa, os PCs devem estar executando a Atualização do Windows 10 para Criadores, ou posterior.
- Os computadores devem estar ingressados no Azure Active Directory no mesmo locatário em que você registrou a Microsoft Store para Empresas como uma ferramenta de gerenciamento.
- Quando o logon dos PCs tiver sido feito com a conta de administrador interno, eles não poderão acessar os aplicativos da Microsoft Store para Empresas.
- Os PCs devem ter uma conexão de Internet dinâmica com a Microsoft Store para Empresas.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Observações para PCs que executam versões anteriores do Windows 10
Em computadores que executam uma versão do Windows 10 anterior à Atualização para Criadores (com o cliente do Configuration Manager), a seguinte funcionalidade aplica-se:


- Ao impor a instalação pelo usuário que estiver instalando o aplicativo, o aplicativo que estiver atingindo sua data limite de instalação ou pela reavaliação de pós-instalação para as implantações necessárias:
    - O aplicativo é “imposto” com a inicialização do aplicativo da Microsoft Store para Empresas. 
    - O usuário final deverá concluir a instalação pela loja antes que o aplicativo seja instalado
    - No console do Configuration Manager, o status do aplicativo relata uma falha com o seguinte erro: “O aplicativo da Microsoft Store foi aberto no computador cliente e está aguardando o usuário concluir a instalação”.
- No próximo ciclo de avaliação do aplicativo:
    - Se o aplicativo tiver sido instalado pelo usuário final da loja, o aplicativo relatará o status **Sucesso**. 
    - Se o usuário final não tiver tentado instalar o aplicativo pela loja:
        - As implantações necessárias tentarão inicializar a loja e impor novamente a instalação do aplicativo.
        - As implantações disponíveis não serão impostas novamente.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Outras observações para PCs que executam versões anteriores do Windows 10:

- Não é possível implantar aplicativos de linha de negócios da Microsoft Store para Empresas
- Quando você implanta aplicativos pagos pela loja, os usuários finais devem fazer logon na loja e comprar os aplicativos por sua conta.
- Se você implantar uma política de grupo para desabilitar o acesso à versão de consumidor da Microsoft Store, as implantações da Microsoft Store para Empresas não funcionarão, mesmo se ela estiver habilitada.


## <a name="set-up-microsoft-store-for-business-synchronization"></a>Configurar a sincronização da Microsoft Store para Empresas
A sincronização da lista de aplicativos adquiridos por sua organização permite que você veja esses aplicativos no console do Configuration Manager.

<!-- Remove below after 1802... -->
### <a name="for-configuration-manager-versions-prior-to-1706"></a>Para versões do Configuration Manager anteriores à 1706

**No Azure Active Directory, registre o Configuration Manager como uma ferramenta de gerenciamento de “Aplicativo Web e/ou API Web”. Esta ação lhe dá uma ID de cliente que será necessária mais tarde.**
1. No nó do Active Directory do [https://manage.windowsazure.com](https://manage.windowsazure.com), selecione Azure Active Directory, clique em **Aplicativos** > **Adicionar**.
2.  Clique em **Adicionar um aplicativo que minha organização esteja desenvolvendo**.
3.  Insira um nome para o aplicativo, selecione **Aplicativo Web** e/ou **API da Web** e clique na seta **Avançar**.
4.  Insira a mesma URL para **URL de Entrada** e **URI da ID do Aplicativo**. A URL pode ser qualquer uma e não precisa ser resolvida para um endereço real. Por exemplo, você pode inserir *https://yourdomain/sccm*.
5.  Conclua o assistente.

**No Azure Active Directory, crie uma chave de cliente para a ferramenta de gerenciamento registrada**
1.  Realce o aplicativo criado e clique em **Configurar**.
2.  Em **Chaves**, escolha uma duração na lista e clique em **Salvar**. Essa ação cria uma nova chave do cliente. Não saia dessa página até que você tenha carregado com êxito a Microsoft Store para Empresas no Configuration Manager.

**Na Microsoft Store para Empresas, configure o Configuration Manager como a ferramenta de gerenciamento da loja**
1.  Abra [https://businessstore.microsoft.com/managementtools](https://businessstore.microsoft.com/managementtools) e entre, se solicitado.
2.  Aceite os termos de uso, se solicitado.
3.  Em **Ferramentas de Gerenciamento**, clique em **Adicionar uma ferramenta de gerenciamento**.
4.  Em **Pesquisar a ferramenta por nome**, digite o nome do aplicativo que você criou anteriormente no AAD e clique em **Adicionar**.
5.  Clique em **Ativar** ao lado do aplicativo importado.
6.  Na página **Gerenciar > Informações da Conta**, selecione **Exibir Aplicativos Licenciados Offline** se quiser permitir que aplicativos licenciados offline sejam comprados.

**Adicionar a conta da loja ao Configuration Manager**

1. Verifique se você comprou pelo menos um aplicativo da Microsoft Store para Empresas. No espaço de trabalho **Administração** do console do Configuration Manager, expanda **Serviços de Nuvem** e clique em **Microsoft Store para Empresas**.
2.  Na guia **Início**, no grupo **Microsoft Store para Empresas**, clique em **Adicionar conta da Microsoft Store para Empresas**. 
3.  Adicione a ID de locatário, a ID de cliente e a chave de cliente do Azure Active Directory e, em seguida, conclua o assistente.
4. Quando terminar, você poderá ver a conta na **Microsoft Store para Empresas** no console do Configuration Manager.

### <a name="for-configuration-manager-version-1706-and-later"></a>Para a versão do Configuration Manager anterior à 1706
<!-- ...remove above after 1802 -->

1. No console, acesse **Administração** > **Serviços de Nuvem** > **Serviços do Azure** e, em seguida, escolha **Configurar Serviços do Azure** para iniciar o **Assistente de Serviços do Azure**.
2. Na página de **Serviços do Azure**, selecione o serviço que deseja configurar e, em seguida, clique em **Próxima**.
3. Na página **Geral**, forneça um nome amigável para o Nome do serviço do Azure e uma descrição opcional e clique **Próxima**.
4. Na página do **Aplicativo**, especifique seu ambiente do Azure e, em seguida, clique em **Procurar** para abrir a janela do **Aplicativo de Servidor**.
5. Na janela do **aplicativo de servidor**, selecione o aplicativo de servidor que você deseja usar e depois clique em **OK**. Os aplicativos de servidor são os aplicativos Web do Azure que contêm as configurações de sua conta do Azure, incluindo a ID de locatário, ID de cliente e uma chave secreta para clientes. Se você não tiver um aplicativo de servidor disponível, use uma das seguintes ações:
    - **Criar**: Para criar um novo aplicativo de servidor, clique em **Criar**. Forneça um nome amigável para o aplicativo e o locatário. Em seguida, depois que você entrar no Azure, o Configuration Manager criará o aplicativo Web no Azure para você, incluindo a ID do cliente e a chave secreta para uso com o aplicativo Web. Posteriormente, você poderá exibir esses valores no portal do Azure.
    - **Importar**: Para usar um aplicativo Web que já existe em sua assinatura do Azure, clique em **Importar**. Forneça um nome amigável para o aplicativo e o locatário. Em seguida, especifique a ID de locatário, ID do cliente e a chave secreta para o aplicativo Web do Azure que você deseja que o Configuration Manager use. Depois que você **verificar** as informações, clique em **OK** para continuar. 
6. Examine a página de **informações** e conclua quaisquer etapas adicionais e configurações, conforme indicado. Essas configurações são necessárias para usar o serviço com o Configuration Manager. Por exemplo, para configurar a Microsoft Store para Empresas:
    - No Azure, é necessário registrar o Configuration Manager como um aplicativo Web ou uma API Web e registrar a ID do cliente. Você também pode especificar uma chave de cliente para uso pela ferramenta de gerenciamento (que é o Configuration Manager).
    - No portal da Microsoft Store para Empresas, é necessário configurar o Configuration Manager como a ferramenta de gerenciamento de repositórios, habilitar o suporte para aplicativos licenciados offline e, em seguida, adquirir pelo menos um aplicativo. 
7. Quando estiver pronto para continuar, clique em **Próximo**.
8. Na página **Configurações de aplicativo**, conclua as configurações de catálogo e idioma do aplicativo para este serviço e, em seguida, clique em **Próxima**.
9. Depois que o assistente for concluído, o console do Configuration Manager mostrará que você configurou a **Microsoft Store para Empresas** como um **Tipo de Serviço de nuvem**.




## <a name="create-and-deploy-a-configuration-manager-application-from-a-microsoft-store-for-business-app"></a>Criar e implantar um aplicativo do Configuration Manager por meio de um aplicativo da Microsoft Store para Empresas
Após a sincronização, crie e implante os aplicativos da loja, assim como você faria com qualquer outro aplicativo.

1.  No espaço de trabalho **Biblioteca de Software** do console do Configuration Manager, expanda **Gerenciamento de Aplicativos** e clique em **Informações sobre Licença para Aplicativos da Loja**.
2.  Escolha o aplicativo que deseja implantar e, na guia **Início**, no grupo **Criar**, clique em **Criar Aplicativo**.
É criado um aplicativo do Configuration Manager contendo o aplicativo da Microsoft Store para Empresas. Em seguida, é possível implantar e monitorar o aplicativo, como você faria com qualquer outro aplicativo do Configuration Manager.

> [!IMPORTANT]
> Para dispositivos registrados no Microsoft Intune, os aplicativos implantados ficam disponíveis somente para o usuário que registrou o dispositivo originalmente. Nenhum outro usuário pode acessar o aplicativo.

## <a name="next-steps"></a>Próximas etapas

No espaço de trabalho **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e clique em **Informações sobre Licença para Aplicativos da Loja**.

Para cada aplicativo gerenciado da loja, é possível exibir informações sobre o aplicativo. Essas informações incluem o nome do aplicativo, a plataforma, o número de licenças para o aplicativo que você possui e o número de licenças disponíveis.

Depois de implantar aplicativos online, as atualizações desse aplicativo serão obtidas diretamente da Microsoft Store. Além disso, o Configuration Manager não verifica a conformidade da versão de aplicativos online, até que o Windows relate o aplicativo como instalado.  

Ao implantar aplicativos offline em dispositivos Windows 10 com o cliente do Configuration Manager, não permita que os usuários atualizem aplicativos externos para implantações do Configuration Manager. O controle de atualizações em aplicativos offline é especialmente importante em ambientes de vários usuários, como salas de aula. Uma opção é desabilitar a Microsoft Store usando uma [política de grupo](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy). 

Depois que o administrador da Microsoft Store para Empresas adquirir um aplicativo offline, não publique o aplicativo para os usuários por meio da loja. Essa configuração garante que os usuários não possam instalar nem atualizar online. Os usuários receberão somente atualizações de aplicativo offline por meio do Configuration Manager. 
