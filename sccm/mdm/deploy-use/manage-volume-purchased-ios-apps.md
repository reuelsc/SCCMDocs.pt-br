---
title: Manage volume-purchased iOS apps
titleSuffix: Configuration Manager
description: Implante, gerencie e monitore as licenças dos aplicativos que você comprar por meio da Apple App Store do iOS.
ms.date: 03/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f94cc80d41eb346cb1d4c2fc314d310005c7b5f2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350180"
---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Gerenciar aplicativos iOS adquiridos por volume com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*



 Na Apple App Store do iOS, você pode comprar várias licenças para um aplicativo que deseja usar na empresa. Isso ajuda a reduzir a sobrecarga administrativa de acompanhar várias cópias de aplicativos compradas.  

 O Configuration Manager facilita a implantação e o gerenciamento de aplicativos iOS que você compra por meio do programa. Você pode importar as informações de licença da App Store e controlar o número de licenças que está usando.  



## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gerenciar aplicativos adquiridos por volume para dispositivos iOS  
 Compre várias licenças para aplicativos iOS por meio do VPP (Apple Volume Purchase Program). Inicialmente, esse processo envolve configurar uma conta VPP (Apple Volume Purchase Program) no site da Apple. Em seguida, carregue o token do Apple VPP no Configuration Manager, que fornece as seguintes funcionalidades:  

-   Sincronizar informações de compra por volume com o Configuration Manager  
 
- Sincronizar aplicativos do Apple Volume Purchase Program for Business e do Apple Volume Purchase Program for Education  

- Associar vários tokens do programa de compra por volume da Apple ao Configuration Manager  

-   Os aplicativos comprados são exibidos no console do Configuration Manager  

-   Implantar e monitorar os aplicativos  

-   Controlar o número de licenças usadas de cada aplicativo   

-   O Configuration Manager pode ajudá-lo a recuperar licenças quando necessário, desinstalando aplicativos comprados por volume implantados  



## <a name="before-you-start"></a>Antes de começar  
 Para começar, você deve obter um token do Apple VPP e carregá-lo no Configuration Manager.  

-   Se você já tiver usado um token VPP com outro produto de MDM em sua conta existente do Apple VPP, será necessário gerar um novo para ser usado com o Configuration Manager.  
-   Cada token é válido por um ano.  
-   Por padrão, o Configuration Manager é sincronizado com o serviço Apple VPP duas vezes por dia, para garantir que suas licenças são sincronizadas com o Configuration Manager. Somente as alterações nas licenças são sincronizadas. Uma sincronização completa é executada uma vez a cada sete dias. Se escolher **Sincronizar** para fazer uma sincronização manual, esta ação executará sempre uma sincronização completa.  
-   Se for necessário recuperar ou restaurar o banco de dados do Configuration Manager, recomendamos a execução de uma sincronização manual logo em seguida. Esse processo garante que os dados sincronizados da licença sejam atualizados.  
-   Além disso, é necessário ter importado um certificado APNs (Apple Push Notification Service) válido da Apple. Este certificado permite gerenciar dispositivos iOS, inclusive a implantação de aplicativos. Para obter mais informações, consulte [Set up iOS hybrid device management](enroll-hybrid-ios-mac.md) (Configurar o gerenciamento de dispositivo híbrido iOS).  
-   O Configuration Manager dá suporte à adição de até 3000 tokens VPP.

Você pode implantar aplicativos licenciados para usuários e dispositivos. Dependendo da capacidade dos aplicativos para dar suporte ao licenciamento de dispositivos, uma licença apropriada será solicitada quando você implantá-la, da seguinte maneira:

|O aplicativo dá suporte ao licenciamento de dispositivos?|Tipo de coleção de implantação|Licença solicitada|
|---|---|---|
|Sim|usuário|Licença de usuário|
|Não|usuário|Licença de usuário|
|Sim|Dispositivo|Licença de dispositivo|
|Não|Dispositivo|Licença de usuário|



## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Etapa 1: obter e carregar um token de VPP da Apple  

1.  No console do Configuration Manager, escolha **Administração** > **Serviços de Nuvem** > **Tokens do Apple Volume Purchase Program**.   

3.  Na guia **Início**, no grupo **Tokens do Apple Volume Purchase Program**, escolha **Adicionar Token do Apple Volume Purchase Program**.  

4.  Na página **Geral** do assistente **Adicionar token do Apple Volume Purchase Program**, defina as seguintes configurações:   

    -   **Nome** – Insira um nome para esse token a fim de exibi-lo no console do Configuration Manager.  

    -   **Token** – escolha **Procurar** e, em seguida, o token VPP baixado no site da Apple.  

         Clique no link **Ver Conta VPP da Apple**. Se ainda não fez isso, inscreva-se no programa de compra por volume empresarial ou educacional. Depois de se inscrever, baixe o token do Apple VPP em sua conta.  

    -   **Descrição** – Opcionalmente, insira uma descrição que o ajudará a identificar esse token no console do Configuration Manager.  

    -   **Categorias atribuídas para aprimorar a pesquisa e a filtragem** – você também pode atribuir categorias para o token de VPP para facilitar a pesquisa no console do Configuration Manager.  
    -   **ID da Apple** - insira a ID de email da Apple associada ao token de VPP.
    -   **Tipo de token** - selecione o tipo de token de VPP que você deseja usar. Você pode escolher os tipos de token **Business** e **EDU**.

5.  Escolha **Avançar** e conclua o assistente.  

No nó **Tokens do Apple Volume Purchase Program**, você já pode exibir informações sobre o token do Apple VPP. Essa exibição inclui a data da última atualização, a data de expiração e a data da última sincronização.

É possível realizar uma sincronização completa dos dados mantidos pela Apple com o Configuration Manager a qualquer momento. Basta escolher **Sincronizar** na faixa de opções.  



## <a name="step-2---deploy-a-volume-purchased-app"></a>Etapa 2: implantar um aplicativo comprado por volume  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Informações de Licença para Aplicativos da Loja**.  

3.  Escolha o aplicativo que você deseja implantar e, na guia **Início**, no grupo **Criar**, escolha **Criar Aplicativo**.
O aplicativo do Configuration Manager criado contém o aplicativo Microsoft Store para Empresas. Em seguida, é possível implantar e monitorar o aplicativo, como você faria com qualquer outro aplicativo do Configuration Manager.  

    > [!IMPORTANT]  
    > É necessário escolher a finalidade da implantação **Obrigatória**. Atualmente, não há suporte para instalações disponíveis.

 Quando você implantar o aplicativo, uma licença será usada por cada usuário ou para instalações de dispositivo, cada dispositivo que instalar o aplicativo. Se você direcionar uma coleção de dispositivos com um aplicativo que oferece suporte ao licenciamento de dispositivos, uma licença de dispositivo será declarada. Se você direcionar uma coleção de dispositivos com um aplicativo sem suporte para licenciamento de dispositivos, uma licença de usuário será declarada. 

 Quando você cria um aplicativo a partir do nó **Informações de licença para aplicativos de armazenamento**, o aplicativo é associado a licenças a partir do token para o aplicativo selecionado. Por exemplo, você verá duas versões do mesmo aplicativo no nó. Esse comportamento ocorre porque cada versão do aplicativo está associada a um token do Apple VPP diferente. Em seguida, você pode criar aplicativos de cada token e implantá-los separadamente.

 Para recuperar uma licença, crie uma nova implantação para o aplicativo com a ação de implantação **Desinstalar**. Não é possível alterar a ação de implantação na implantação original. A licença é recuperada após a desinstalação do aplicativo.  



## <a name="step-3---monitor-ios-vpp-apps"></a>Etapa 3 - Monitorar aplicativos de VPP iOS  
 O nó **Informações de Licença para Aplicativos da Loja** do espaço de trabalho **Biblioteca de Software** exibe informações sobre os aplicativos iOS adquiridos por volume. As informações incluem o número total de licenças que você tem para cada aplicativo e a quantidade que foi implantada. Além disso, o modo de exibição mostra a qual token de VPP o aplicativo está associado e o tipo do token

 Também é possível monitorar o uso de licença de todos os aplicativos VPP adquiridos por meio do relatório **Aplicativos do Apple Volume Purchase Program para iOS com contagens de licença**.  

 Esse relatório mostra o nome de cada aplicativo junto com o número total de licenças adquiridas, o número de licenças disponíveis e muito mais.  

 Para obter ajuda para executar relatórios do Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  



## <a name="delete-an-apple-vpp-token"></a>Excluir um token do Apple VPP  
<!--505268-->

Use o seguinte processo para excluir um token do Configuration Manager:  

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda **Serviços de Nuvem** e selecione **Tokens do Apple Volume Purchase Program**.  

2. Selecione o token que deseja excluir.  

3. Clique na opção **Excluir** na faixa de opções.  

