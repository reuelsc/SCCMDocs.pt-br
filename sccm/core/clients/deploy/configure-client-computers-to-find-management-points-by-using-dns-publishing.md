---
title: "Configurar clientes para localizar pontos de gerenciamento com a publicação do DNS | Microsoft Docs"
description: "Defina computadores cliente para localizar pontos de gerenciamento usando a publicação do DNS no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
caps.latest.revision: 6
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 9eadb91a575323b4c36af14962f370046ea513ce


---
# <a name="how-to-configure-client-computers-to-find-management-points-by-using-dns-publishing-in-system-center-configuration-manager"></a>Como configurar computadores cliente para localizar pontos de gerenciamento usando a publicação do DNS no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Clientes no System Center Configuration Manager devem localizar um ponto de gerenciamento para concluir a atribuição de site e como um processo contínuo para permanecer gerenciado. Os Serviços de Domínio Active Directory fornecem o método mais seguro para clientes na intranet localizarem pontos de gerenciamento. Entretanto, se os clientes não puderem usar esse método de local do serviço (por exemplo, você não estendeu o esquema do Active Directory ou os clientes não são de um grupo de trabalho), utilize a publicação de DNS como método de local do serviço alternativo preferido.  

> [!NOTE]  
>  Ao instalar o cliente para Linux e UNIX, você deve especificar um ponto de gerenciamento para usar como um ponto inicial de contato. Para obter informações sobre como instalar o cliente para Linux e UNIX, consulte [Como implantar clientes para servidores UNIX e Linux no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Antes de usar publicação DNS para pontos de gerenciamento, verifique se os servidores DNS na intranet possuem SRV RR (registros de recursos de local do serviço) e registros de recurso de host correspondentes (A ou AAA) para os pontos de gerenciamento do site. Os registros de recurso de local de serviço podem ser criados automaticamente pelo Configuration Manager ou manualmente pelo administrador de DNS que cria os registros em DNS.  

 Para obter mais informações sobre a publicação de DNS como um método de local de serviço para clientes do Configuration Manager, consulte [Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 Por padrão, os clientes procuram DNS para os pontos de gerenciamento em seu domínio DNS. No entanto, se não houver pontos de gerenciamento publicados no domínio do cliente, você deverá configurar clientes manualmente com um sufixo DNS de ponto de gerenciamento. Você pode configurar esse sufixo DNS nos clientes durante ou após a instalação do cliente:  

-   Para configurar os clientes de um sufixo de ponto de gerenciamento durante a instalação do cliente, configure as propriedades de CCMSetup Client.msi.  

-   Para configurar clientes de um sufixo de ponto de gerenciamento após a instalação do cliente, no Painel de Controle, configure **Propriedades do Configuration Manager**.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>Para configurar os clientes de um sufixo de ponto de gerenciamento durante a instalação do cliente  

-   Instale o cliente com a seguinte propriedade CCMSetup Client.msi:  

    -   **DNSSUFFIX=** *&lt;domínio de ponto de gerenciamento\>*  

         Se o site tiver mais de um ponto de gerenciamento e eles estiverem em mais de um domínio, especifique apenas um domínio. Ao conectarem-se a um ponto de gerenciamento nesse domínio, os clientes baixam uma lista de pontos de gerenciamento disponíveis, que incluirá os pontos de gerenciamento de outros domínios.  

     Para obter mais informações sobre as propriedade da linha de comando do CCMSetup, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>Para configurar os clientes de um sufixo de ponto de gerenciamento após a instalação do cliente  

1.  No Painel de Controle do computador cliente, navegue para **Configuration Manager**e clique duas vezes em **Propriedades**.  

2.  Na guia **Site** , especifique o sufixo DNS dos pontos de gerenciamento e clique em **OK**.  

     Se o site tiver mais de um ponto de gerenciamento e eles estiverem em mais de um domínio, especifique apenas um domínio. Ao conectarem-se a um ponto de gerenciamento nesse domínio, os clientes baixam uma lista de pontos de gerenciamento disponíveis, que incluirá os pontos de gerenciamento de outros domínios.



<!--HONumber=Dec16_HO3-->


