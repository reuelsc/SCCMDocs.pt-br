---
title: "Gerenciar o acesso à Internet usando políticas de navegador gerenciado | Microsoft Docs"
description: "Implante o Intune Managed Browser para gerenciar e restringir o acesso à Internet."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e25e00c-c9a8-473f-bcb7-ea989f6ca3c5
caps.latest.revision: 6
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 7c8d38ad6bdfece5432d4886f60ff98b8d3bd342
ms.lasthandoff: 03/06/2017


---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>Gerenciar o acesso à Internet usando políticas de navegador gerenciado com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

No System Center Configuration Manager, é possível implantar o Intune Managed Browser (um aplicativo de navegação na Web) e associá-lo a uma política de navegador gerenciado. A política de navegador gerenciado configura uma lista de sites permitidos ou bloqueados que restringe os sites que os usuários do navegador gerenciado podem acessar.  

 Como esse aplicativo é um aplicativo gerenciado, também é possível aplicar políticas de gerenciamento de aplicativo móvel a ele, como o controle do uso de recortar, copiar e colar. Isso impede capturas de tela e também garante que os links para conteúdo sejam abertos somente em outros aplicativos gerenciados. Para ver os detalhes [Proteger aplicativos usando políticas de gerenciamento de aplicativos móveis](protect-apps-using-mam-policies.md).  

> [!IMPORTANT]  
>  Se os usuários instalarem o navegador gerenciado, eles não serão gerenciados por nenhuma das políticas que você especificar. Para garantir que o navegador seja gerenciado pelo Configuration Manager, eles deverão desinstalar o aplicativo antes de você implantá-lo como um aplicativo gerenciado.  

 Você pode criar políticas de navegador gerenciado para os seguintes tipos de dispositivo:  

-   Dispositivos que executam o Android 4 e posterior.  

-   Dispositivos que executam o iOS 7 e posterior.  

> [!NOTE]  
>  Para obter mais informações sobre o aplicativo Intune Managed Browser e para baixá-lo, confira [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) para o iOS e [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) para o Android.  

## <a name="create-a-managed-browser-policy"></a>Criar uma política de navegador gerenciado  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Políticas de Gerenciamento de Aplicativos**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Política de Gerenciamento de Aplicativos**.  

4.  Na página **Geral**, insira o nome e a descrição da política e escolha **Avançar**.  

5.  Na página **Tipo de Política**, selecione a plataforma e, em seguida, **Navegador Gerenciado** como o tipo de política e escolha **Avançar**.  

     Na página **Managed Browser** , selecione uma das seguintes opções:  

    -   **Permitir que o navegador gerenciado abra apenas as URLs listadas abaixo** – especifique uma lista de URLs que podem ser abertas pelo navegador gerenciado.  

    -   **Impedir que o navegador gerenciado abra as URLs listadas abaixo** – especifique uma lista de URLs que não poderão ser abertas pelo navegador gerenciado.  

    > [!NOTE]  
    >  Você não pode incluir URLs permitidos e bloqueados na mesma política de navegador gerenciado.  

     Para saber mais sobre os formatos de URL que podem ser especificados, consulte o formato de URL para obter as URLs permitidas e bloqueadas neste artigo.  

    > [!NOTE]  
    >  O tipo de política Geral permite alterar a funcionalidade dos aplicativos implantados para ajudar a alinhá-los com as políticas de conformidade e segurança de sua empresa. Por exemplo, é possível restringir as operações de recortar, copiar e colar em um aplicativo restrito. Para saber mais sobre o tipo de política Geral, consulte [Proteger aplicativos usando políticas de gerenciamento de aplicativo móvel](protect-apps-using-mam-policies.md).  

6.  Conclua o assistente.  

A nova política é exibida no nó **Políticas de Gerenciamento de Aplicativos** no espaço de trabalho **Biblioteca de Software** .  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>Crie uma implantação de software para o aplicativo de navegador gerenciado  
 Depois de criar a política de navegador gerenciado, é possível criar um tipo de implantação de software para o aplicativo de navegador gerenciado. É necessário associar uma política geral e uma política de navegador gerenciado para o aplicativo de navegador gerenciado.  

 Para mais informações, consulte [Criar aplicativos](create-applications.md).  

## <a name="security-and-privacy-for-the-managed-browser"></a>Segurança e privacidade para o navegador gerenciado  

-   Em dispositivos iOS, os sites que têm certificados expirados ou não confiáveis não podem ser abertos.  

-   As configurações feitas pelos usuários para o navegador interno em seus dispositivos não são usadas pelo navegador gerenciado. O navegador gerenciado não tem acesso a essas configurações.  

-   Se você configurar as opções **Solicitar PIN simples para acesso** ou **Solicitar credenciais corporativas para acesso** em uma política de gerenciamento de aplicativo móvel associada ao navegador gerenciado, um usuário poderá clicar na Ajuda na página de autenticação e, em seguida, acessar qualquer site – mesmo um que tenha sido adicionado a uma lista de sites bloqueados na política de navegador gerenciado.  

-   O navegador gerenciado pode bloquear o acesso a sites apenas quando eles são acessados diretamente. Ele não pode bloquear o acesso quando serviços intermediários (como um serviço de tradução) são usados para acessar o site.  

## <a name="reference-information"></a>Informações de referência  

###  <a name="url-format-for-allowed-and-blocked-urls"></a>Formato de URL para URLs permitidas e bloqueadas  

Use as informações a seguir para saber mais sobre os formatos permitidos e caracteres curinga que você pode usar ao especificar URLs para as listas permitidas e bloqueadas.  

-   Você pode usar o símbolo de caractere curinga '**\***' de acordo com as regras na lista de padrões permitidos abaixo.  

-   Certifique-se de prefixar todas as URLs com **http** ou **https** ao inseri-las na lista.  

-   Você pode especificar os números de porta no endereço. Se você não especificar um número de porta, os valores usados serão:  

    -   Porta 80 para https  

    -   Porta 443 para https  

     Não há suporte para o uso de curingas no número da porta, como **http://www.contoso.com:\*** e **http://www.contoso.com: /\***  

-   Use a tabela a seguir para aprender sobre os padrões permitidos que você pode usar para especificar URLs:  

    |URL|Corresponde a|Não corresponde a|  
    |---------|-------------|--------------------|  
    |http://www.contoso.com<br /><br /> Corresponde a uma única página|www.contoso.com|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> contoso.com/|  
    |http://contoso.com<br /><br /> Corresponde a uma única página|contoso.com/|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com|  
    |http://www.contoso.com/*<br /><br /> Corresponde a todas as URLs iniciadas por www.contoso.com|www.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com/videos/tvshows|host.contoso.com<br /><br /> host.contoso.com/images|  
    |http://*.contoso.com/\*<br /><br /> Corresponde a todos os subdomínios em contoso.com|developer.contoso.com/resources<br /><br /> news.contoso.com/images<br /><br /> news.contoso.com/videos|contoso.host.com|  
    |http://www.contoso.com/images<br /><br /> Corresponde a uma única pasta|www.contoso.com/images|www.contoso.com/images/dogs|  
    |http://www.contoso.com:80<br /><br /> Corresponde a uma única página, usando um número de porta|http://www.contoso.com:80||  
    |https://www.contoso.com<br /><br /> Corresponde a uma única página segura|https://www.contoso.com|http://www.contoso.com|  
    |http://www.contoso.com/images/*<br /><br /> Corresponde a uma única pasta e todas as subpastas|www.contoso.com/images/dogs<br /><br /> www.contoso.com/images/cats|www.contoso.com/videos|  

-   Seguem exemplos de algumas das entradas que você não pode especificar:  

    -   *.com  

    -   *.contoso/\*  

    -   www.contoso.com/*images  

    -   www.contoso.com/*images\*pigs  

    -   www.contoso.com/page*  

    -   Endereços IP  

    -   https://*  

    -   http://*  

    -   http://www.contoso.com:*  

    -   http://www.contoso.com: / *  

> [!NOTE]  
>  *.microsoft.com sempre é permitido.  

### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>Como os conflitos entre a lista de permissões e bloqueios são resolvidos  
 Se várias políticas de navegador gerenciado forem implantadas em um dispositivo e houver conflitos entre as configurações, o modo (permitir ou bloquear) e as listas de URLs são avaliados quanto aos conflitos. Em caso de conflitos, o comportamento a seguir se aplica:  

-   Se os modos de cada política forem os mesmos, mas as listas de URLs forem diferentes, as URLs não serão impostas no dispositivo.  

-   Se os modos de cada política forem diferentes, mas as listas de URLs forem as mesmas, as URLs não serão impostas no dispositivo.  

-   Se um dispositivo estiver recebendo políticas de navegador gerenciado pela primeira vez e houver conflito entre duas políticas, as URLs não serão impostas ao dispositivo. Use o nó **Conflitos de Política** do espaço de trabalho **Política** para ver os conflitos.  

-   Se um dispositivo já tiver recebido uma política de navegador gerenciado e uma segunda política for implantada com configurações conflitantes, as configurações originais permanecerão no dispositivo. Use o nó **Conflitos de Política** do espaço de trabalho **Política** para ver os conflitos.  

