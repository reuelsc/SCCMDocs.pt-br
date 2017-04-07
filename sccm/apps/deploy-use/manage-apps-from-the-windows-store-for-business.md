---
title: Gerenciar aplicativos da Windows Store para Empresas | Microsoft Docs
description: Gerenciar e implantar aplicativos da Windows Store para Empresas usando o System Center Configuration Manager.
ms.custom: na
ms.date: 3/29/2017
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
ms.sourcegitcommit: 6accec2d356861b273b25ba2b6338d9684a46ff6
ms.openlocfilehash: f2d9da1c584f78e27e84b7f55e7ffe4dd052a27c
ms.lasthandoff: 03/29/2017

---

# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Gerenciar aplicativos da Windows Store para Empresas com o System Center Configuration Manager
Na [Windows Store para Empresas](https://www.microsoft.com/business-store), é possível encontrar e adquirir aplicativos Windows para sua organização, individualmente ou por volume. Conectando a loja ao Configuration Manager, você pode sincronizar a lista de aplicativos que comprou com o Configuration Manager, vê-los no console do Configuration Manager e implantá-los como faria com qualquer outro aplicativo.


## <a name="online-and-offline-apps"></a>Aplicativos online e offline

A Windows Store para Empresas dá suporte a dois tipos de aplicativo:

- **Online** – este tipo de licença exige que usuários e dispositivos se conectem à loja para obter um aplicativo e sua licença. Dispositivos Windows 10 devem ser ingressados em um domínio do Azure Active Directory.
- **Offline** – as organizações podem armazenar em cache aplicativos e licenças para implantá-los diretamente em sua rede local, sem se conectar à loja ou ter uma conexão com a Internet.

[Leia mais](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview?f=255&MSPPError=-2147217396) sobre o Windows Store para Empresas.

O Configuration Manager dá suporte ao gerenciamento de aplicativos da Windows Store para Empresas em dispositivos Windows 10 que executam o cliente do Configuration Manager e a dispositivos Windows 10 registrados no Microsoft Intune (conhecido como configuração híbrida). O Configuration Manager oferece os seguintes recursos para aplicativos online e offline.

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

## <a name="deploying-online-apps-using-the-windows-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Implantando aplicativos online usando a Windows Store para Empresas com PCs que executam o cliente do Configuration Manager
Antes de implantar aplicativos da Windows Store para Empresas em PCs que executam o cliente do Configuration Manager completo, considere o seguinte:

- Para a funcionalidade completa, os PCs devem estar executando a Atualização do Windows 10 para Criadores, ou posterior.
- Os PCs devem estar associados ao espaço de trabalho do Azure Active Directory e estar no mesmo locatário do AAD onde você registrou a Windows Store para Empresas como uma ferramenta de gerenciamento.
- Quando os PCs estão conectados com a conta de administrador interna, eles não podem acessar os aplicativos na Windows Store para Empresas.
- Os PCs devem ter uma conexão de Internet em tempo real para a Windows Store para Empresa.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Observações para PCs que executam versões anteriores do Windows 10
Em computadores que executam uma versão do Windows 10 anterior à Atualização para Criadores (com o cliente do Configuration Manager), a seguinte funcionalidade aplica-se:


- Quando a instalação for imposta pelo usuário que está instalando o aplicativo ou o aplicativo atingir seu prazo de instalação ou postar reavaliação de instalação para as implantações necessárias:
    - O aplicativo será "imposto" iniciando o aplicativo da Windows Store para Empresas. 
    - O usuário final deverá concluir a instalação pela loja antes que ele seja realmente instalado
    - O status do aplicativo no console do Configuration Manager relatará falha com o erro "O aplicativo da Windows Store foi aberto no computador cliente e está aguardando o usuário concluir a instalação".
- No próximo ciclo de avaliação do aplicativo:
    - Se o aplicativo tiver sido instalado pelo usuário final pela loja, o aplicativo relatará o status **Sucesso**. 
    - Se o usuário final não tiver tentado instalar o aplicativo pela loja:
        - As implantações necessárias tentarão iniciar a loja e impor novamente a instalação do aplicativo.
        - As implantações disponíveis não serão impostas novamente.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Outras observações para PCs que executam versões anteriores do Windows 10:

- Você pode implantar aplicativos personalizados de linha de negócios da Windows Store para Empresas
- Quando você implanta aplicativos pagos pela loja, os usuários finais serão solicitados a fazer logon na loja e comprar o aplicativo por sua conta.
- Se você tiver implantado uma Política de grupo desabilitando o acesso para a versão de cliente da Windows Store, as implantações da Windows Store para Empresas não funcionará, mesmo se estiver habilitada.


## <a name="set-up-windows-store-for-business-synchronization"></a>Configurar a sincronização da Windows Store para Empresas

**No Azure Active Directory, registre o Configuration Manager como uma ferramenta de gerenciamento de "Aplicativo Web e/ou API da Web". Isso lhe fornecerá uma ID de cliente de que você precisará mais tarde.**
1. No nó Active Directory de [https://manage.windowsazure.com](https://manage.windowsazure.com), selecione seu Azure Active Directory e clique em **Aplicativos** > **Adicionar**.
2.  Clique em **Adicionar um aplicativo que minha organização esteja desenvolvendo**.
3.  Insira um nome para o aplicativo, selecione **Aplicativo Web** e/ou **API da Web** e clique na seta **Avançar**.
4.  Insira a mesma URL para **URL de Entrada** e **URI da ID do Aplicativo**. A URL pode ser qualquer uma e não precisa ser resolvida para um endereço real. Por exemplo, você pode inserir *https://seudomínio/sccm*.
5.  Conclua o assistente.

**No Azure Active Directory, crie uma chave de cliente para a ferramenta de gerenciamento registrada**
1.  Realce o aplicativo que você acabou de criar e clique em **Configurar**.
2.  Em **Chaves**, escolha uma duração na lista e clique em **Salvar**. Isso criará uma nova chave de cliente. Não saia dessa página até que você tenha carregado com êxito a Windows Store para Empresas no Configuration Manager.

**Na Windows Store para Empresas, configure o Configuration Manager como a ferramenta de gerenciamento da loja.**
1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e se conecte, se solicitado.
2.  Aceite os termos de uso, se solicitado.
3.  Em **Ferramentas de Gerenciamento**, clique em **Adicionar uma ferramenta de gerenciamento**.
4.  Em **Pesquisar a ferramenta por nome**, digite o nome do aplicativo que você criou anteriormente no AAD e clique em **Adicionar**.
5.  Clique em **Ativar** ao lado do aplicativo que você acabou de importar.
6.  Na página **Gerenciar > Informações da Conta**, selecione **Exibir Aplicativos Licenciados Offline** se quiser permitir que aplicativos licenciados offline sejam comprados.

**Adicionar a conta da loja ao Configuration Manager**

1. Verifique se você comprou pelo menos um aplicativo da Windows Store para Empresas. No espaço de trabalho **Administração** do console do Configuration Manager, expanda **Serviços de Nuvem** e clique em **Windows Store para Empresas**.
2.  Na guia **Início**, no grupo **Windows Store para Empresas**, clique em **Adicionar Conta da Windows Store para Empresas**. 
3.  Adicione a ID de locatário, a id de cliente e a chave de cliente do Azure Active Directory e conclua o assistente.
4. Quando terminar, você verá a conta configurada na lista **Windows Store para Empresas** no console do Configuration Manager.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Criar e implantar um aplicativo do Configuration Manager por meio de um aplicativo da Windows Store para Empresas.
1.  No espaço de trabalho **Biblioteca de Software** do console do Configuration Manager, expanda **Gerenciamento de Aplicativos** e clique em **Informações sobre Licença para Aplicativos da Loja**.
2.  Escolha o aplicativo que deseja implantar e, na guia **Início**, no grupo **Criar**, clique em **Criar Aplicativo**.
É criado um aplicativo do Configuration Manager contendo o aplicativo da Windows Store para Empresas. Em seguida, é possível implantar e monitorar o aplicativo, como você faria com qualquer outro aplicativo do Configuration Manager.
> [!IMPORTANT]
> Para dispositivos registrados no Intune, os aplicativos implantados ficam disponíveis somente para o usuário que registrou o dispositivo originalmente. Nenhum outro usuário pode acessar o aplicativo.

## <a name="monitor-windows-store-for-business-apps"></a>Monitorar aplicativos da Windows Store para Empresas

No espaço de trabalho **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e clique em **Informações sobre Licença para Aplicativos da Loja**.

Para cada aplicativo da loja que gerencia, você pode ver as informações sobre o aplicativo, incluindo seu nome, a plataforma, quantas licenças do aplicativo que você possui e o número de licenças que estão disponíveis.

