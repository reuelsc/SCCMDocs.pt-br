---
title: Gerenciar aplicativos iOS adquiridos por volume | Microsoft Docs
description: "Implante, gerencie e monitore licenças de aplicativos adquiridos por meio da loja de aplicativos iOS."
ms.custom: na
ms.date: 05/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: c6a6137fa978e1ea28aefea2aea4e29ba661efd6
ms.openlocfilehash: 55f1204b088a7b636a90561f20aa41c7de72bc05
ms.contentlocale: pt-br
ms.lasthandoff: 05/04/2017

---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Gerenciar aplicativos iOS adquiridos por volume com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*



 A loja de aplicativos iOS permite que você compre várias licenças para um aplicativo que deseja executar em sua empresa. Isso ajuda a reduzir a sobrecarga administrativa de acompanhar várias cópias de aplicativos adquiridas.  

 O System Center Configuration Manager ajuda você a implantar e gerenciar aplicativos iOS adquiridos por meio do programa, importando as informações de licença da loja de aplicativos e acompanhando o número de licenças utilizadas.  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gerenciar aplicativos adquiridos por volume para dispositivos iOS  
 Compre várias licenças para aplicativos iOS por meio do VPP (Apple Volume Purchase Program). Isso envolve a configuração de uma conta do Apple VPP no site da Apple e upload do token Apple VPP no Configuration Manager, o que fornece as seguintes funcionalidades:  

-   Sincronize as informações de compra por volume com o Configuration Manager. 
 
- Os aplicativos de sincronização do Apple Volume Purchase Program for Business e o Apple Volume Purchase Program for Education.

- Associe vários tokens de programa de compra por volume da Apple ao seu Configuration Manager.

-   Os aplicativos adquiridos são exibidos no console do Configuration Manager.  

-   É possível implantar aplicativos, monitorá-los e acompanhar o número de licenças para cada aplicativo utilizado.  

-   O Configuration Manager pode ajudá-lo a recuperar licenças quando necessário, desinstalando aplicativos adquiridos por volume implantados.  

## <a name="before-you-start"></a>Antes de começar  
 Antes de começar, você precisará obter um token Apple VPP e carregá-lo no Configuration Manager.  

-   Se você já tiver usado um token VPP com outro produto de MDM em sua conta existente do Apple VPP, será necessário gerar um novo para ser usado com o Configuration Manager.  
-   Cada token é válido por um ano.  
-   Por padrão, o Configuration Manager é sincronizado com o serviço Apple VPP duas vezes por dia, para garantir que suas licenças são sincronizadas com o Configuration Manager.  
      Somente as alterações nas licenças são sincronizadas. Porém, uma vez a cada sete dias, uma sincronização completa será executada.  
      Ao escolher **Sincronização** para fazer uma sincronização manual, essa opção sempre fará com que uma sincronização completa seja executada.  
-   Se você precisar recuperar ou restaurar o banco de dados do Configuration Manager, recomendamos a execução de uma sincronização manual logo em seguida, para garantir que os dados de licença sincronizados estarão atualizados.  
-   Além disso, é necessário ter importado um certificado APNs (Apple Push Notification Service) válido da Apple para permitir o gerenciamento de dispositivos iOS, incluindo a implantação de aplicativos. Para obter mais informações, consulte [Set up iOS hybrid device management](enroll-hybrid-ios-mac.md) (Configurar o gerenciamento de dispositivo híbrido iOS).  

Começando com o System Center Configuration Manager versão 1702, agora você pode implantar aplicativos licenciados a dispositivos, além dos usuários. Dependendo da capacidade dos aplicativos para dar suporte ao licenciamento de dispositivos, uma licença apropriada será solicitada quando você implantá-la, da seguinte maneira:

|||||
|-|-|-|-|
|Versão do Configuration Manager|O aplicativo dá suporte ao licenciamento de dispositivos?|Tipo de coleção de implantação|Licença solicitada|
|Anterior à versão 1702|Sim|usuário|Licença de usuário|
|Anterior à versão 1702|Não|usuário|Licença de usuário|
|Anterior à versão 1702|Sim|Dispositivo|Licença de usuário|
|Anterior à versão 1702|Não|Dispositivo|Licença de usuário|
|Versão 1702 e posterior|Sim|usuário|Licença de usuário|
|Versão 1702 e posterior|Não|usuário|Licença de usuário|
|Versão 1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
|Versão 1702 e posterior|Não|Dispositivo|Licença de usuário|

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Etapa 1: obter e carregar um token de VPP da Apple  

1.  No console do Configuration Manager, escolha **Administração** > **Serviços de Nuvem** > **Tokens do Apple Volume Purchase Program**.   

3.  Na guia **Início**, no grupo **Tokens do Apple Volume Purchase Program**, escolha **Adicionar Token do Apple Volume Purchase Program**.  

4.  Na página **Geral** do assistente **Adicionar token do Apple Volume Purchase Program**, configure o seguinte:   

    -   **Nome** – insira um nome para esse token, uma vez que ele será exibido no console do Configuration Manager.  

    -   **Token** – escolha **Procurar** e, em seguida, o token VPP baixado no site da Apple.  

         Escolha o link **Ver Conta do Apple VPP** e, se ainda não tiver feito isso, inscreva-se no programa de compra por volume empresarial ou educacional. Depois de se inscrever, baixe o token Apple VPP de sua conta.  

    -   **Descrição** – opcionalmente, insira uma descrição que ajudará você a identificar esse token de VPP no console do Configuration Manager.  

    -   **Categorias atribuídas para aprimorar a pesquisa e a filtragem** – você também pode atribuir categorias para o token de VPP para facilitar a pesquisa no console do Configuration Manager.  
    -   **ID da Apple** - insira a ID de email da Apple associada ao token de VPP.
    -   **Tipo de token** - selecione o tipo de token de VPP que você deseja usar. Você pode escolher os tipos de token **Business** e **EDU**.

5.  Escolha **Avançar** e conclua o assistente.  

No nó **Tokens do Apple Volume Purchase Program**, é possível exibir informações sobre o token Apple VPP, incluindo quando foi a última atualização, quando ele expirará e quando ele foi sincronizado pela última vez.

É totalmente possível sincronizar os dados mantidos pela Apple com o Configuration Manager a qualquer momento, escolhendo **Sincronização** na guia **Início** no grupo **Sincronização**.  

## <a name="step-2---deploy-a-volume-purchased-app"></a>Etapa 2: implantar um aplicativo comprado por volume  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Informações de Licença para Aplicativos da Loja**.  

3.  Escolha o aplicativo que você deseja implantar e, na guia **Início**, no grupo **Criar**, escolha **Criar Aplicativo**.
O aplicativo do Configuration Manager criado contém o aplicativo da Windows Store para Empresas. Em seguida, é possível implantar e monitorar o aplicativo, como você faria com qualquer outro aplicativo do Configuration Manager.

    > [!IMPORTANT]  
    > É necessário escolher a finalidade da implantação **Obrigatória**. Atualmente, não há suporte para instalações disponíveis.

 Quando você implantar o aplicativo, uma licença será usada por cada usuário ou para instalações de dispositivo, cada dispositivo que instalar o aplicativo.  Se você direcionar uma coleção de dispositivos com um aplicativo que oferece suporte ao licenciamento de dispositivos, uma licença de dispositivo será declarada.  Se você direcionar uma coleção de dispositivos com um aplicativo que não oferece suporte ao licenciamento de dispositivos, uma licença de usuário será declarada. 

 Quando você cria um aplicativo a partir do nó **Informações de licença para aplicativos de armazenamento**, o aplicativo é associado a licenças a partir do token para o aplicativo selecionado.  Por exemplo, você verá duas versões do mesmo aplicativo no nó. Isso ocorre porque cada versão do aplicativo está associada com um token de VPP da Apple diferente.  Em seguida, você pode criar aplicativos a partir de cada token e implantá-los separadamente.

 Para recuperar uma licença, crie uma nova implantação para o aplicativo com a ação de implantação **Desinstalar**. Não é possível alterar a ação de implantação na implantação original. A licença será recuperada após a desinstalação do aplicativo.  

## <a name="step-3---monitor-ios-vpp-apps"></a>Etapa 3 - Monitorar aplicativos de VPP iOS  
 O nó **Informações de Licença para Aplicativos da Loja** do espaço de trabalho **Biblioteca de Software** exibe informações sobre os aplicativos iOS adquiridos por volume. As informações incluem o número total de licenças que você tem para cada aplicativo e a quantidade que foi implantada. Além disso, o modo de exibição mostra a qual token de VPP o aplicativo está associado e o tipo do token

 Também é possível monitorar o uso de licença de todos os aplicativos VPP adquiridos por meio do relatório **Aplicativos do Apple Volume Purchase Program para iOS com contagens de licença**.  

 Esse relatório mostra o nome de cada aplicativo junto com o número total de licenças adquiridas, o número de licenças disponíveis e muito mais.  

 Para obter ajuda para executar relatórios do Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

