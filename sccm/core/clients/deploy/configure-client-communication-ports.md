---
title: "Configurar portas de comunicação do cliente | Microsoft Docs"
description: "Defina as portas de comunicação do cliente no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstack
ms.author: robstackmsft
manager: angrobe
ms.openlocfilehash: 63e033fdb436930ac5f37e7408ca9292bc444560
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-communication-ports-in-system-center-configuration-manager"></a>Como configurar portas de comunicação do cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É possível alterar os números das portas de solicitação que os clientes do System Center Configuration Manager utilizam para se comunicarem com os sistemas de site que usam HTTP e HTTPS. Embora seja provável que o HTTP ou o HTTPS já estejam configurados para firewalls, a notificação de cliente que utiliza o HTTP ou o HTTPS requer mais uso da CPU e da memória do computador do ponto de gerenciamento do que o uso de um número de porta personalizado. Você também pode especificar o número da porta do site a ser usado caso você ative clientes usando os pacotes de ativação tradicionais.  

 Ao especificar portas de solicitação HTTP e HTTPS, você poderá especificar um número de porta padrão e um número de porta alternativo. Os clientes automaticamente experimentam a porta alternativa depois de falha de comunicação com a porta padrão. Você pode especificar configurações para comunicações de dados HTTP e HTTPS.  

 Os valores padrão para as portas de solicitação do cliente são **80** para tráfego HTTP e **443** para tráfego HTTPS. Altere-os somente se não desejar usar esses valores padrão. Um cenário típico de uso de portas personalizadas é quando você usa um site no IIS, em vez de usar o site padrão. Se você alterar os números da porta padrão para o site padrão no IIS e outros aplicativos também usarem o site da Web padrão, eles provavelmente falharão.  

> [!IMPORTANT]  
>  Não altere os números de porta no Configuration Manager sem entender as consequências. Exemplos:  
>   
>  -   Se você alterar os números de porta para os serviços de solicitação do cliente como uma configuração de site e os clientes existentes não estiverem reconfigurados para usar os novos números de porta, esses clientes se tornarão não gerenciados.  
> -   Antes de definir um número de porta não padrão, certifique-se de que os firewalls e todos os dispositivos de rede intermediária possam dar suporte a essa configuração e reconfigurá-los quando necessário. Se você gerenciar clientes na Internet e alterar o número da porta HTTPS padrão 443, os roteadores e firewalls da Internet poderão bloquear essa comunicação.  

 Para verificar se os clientes não se tornaram não gerenciados após a alteração dos números das portas de solicitação, os clientes deverão ser configurados para usar os novos números de portas de solicitação. Ao alterar as portas de solicitação em um site primário, quaisquer sites secundários vinculados herdarão automaticamente a mesma configuração de porta. Use o procedimento neste tópico para configurar as portas de solicitação no site primário.  

> [!NOTE]  
>  Para saber mais sobre como configurar as portas de solicitação para clientes em computadores com Linux e UNIX, consulte [Configurar portas de solicitação do cliente para Linux e UNIX](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations).  

 Quando o site do Configuration Manager for publicado no Active Directory Domain Services, as configurações de porta de site dos clientes (novos e existentes) que puderem acessar essas informações serão automaticamente definidas, e nenhuma outra ação será necessária. Os clientes que não podem acessar essas informações publicadas nos Serviços de Domínio do Active Directory incluem clientes de grupo de trabalho, clientes de outra floresta do Active Directory, clientes que são configurados somente para Internet e clientes que estão na Internet no momento. Se você alterar os números de porta padrão após a instalação desses clientes, reinstale-os e instale novos clientes usando um dos seguintes métodos:  

-   Reinstale os clientes usando o Assistente de Instalação por Push de Cliente. A instalação do cliente por push define automaticamente os clientes com a configuração da porta do site atual. Para saber mais sobre como usar o Assistente de Instalação por Push de Cliente, consulte [Como instalar clientes do Configuration Manager usando push de cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

-   Reinstale os clientes usando as propriedades de instalação CCMSetup.exe e client.msi de CCMHTTPPORT e CCMHTTPSPORT. Para obter mais informações sobre essas propriedades, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

-   Reinstale os clientes usando um método que pesquise propriedades de instalação do cliente do Configuration Manager nos Serviços de Domínio Active Directory. Para obter mais informações, consulte [Sobre as propriedades de instalação de cliente publicadas nos Serviços de Domínio do Active Directory no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 Para reconfigurar os números de porta nos clientes existentes, você também pode usar o script PORTSWITCH.VBS fornecido com a mídia de instalação na pasta SMSSETUP\Tools\PortConfiguration.  

> [!IMPORTANT]  
>  Em clientes existentes e novos que estão na Internet no momento, é necessário configurar os números de porta não padrão usando as propriedades client.msi do CCMSetup.exe do CCMHTTPPORT e do CCMHTTPSPORT.  

 Após alterar as portas de solicitação no site, os novos clientes instalados por meio do método de instalação de cliente por push em todo site serão automaticamente configurados com os números de portas atuais para o site.  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>Para configurar os números de porta de comunicação do cliente para um site  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**, clique em **Sites**e selecione o site primário a ser configurado.  

3.  Na guia **Início** , clique em **Propriedades**e na guia **Portas** .  

4.  Selecione qualquer item e clique no ícone Propriedades para exibir a caixa de diálogo **Detalhes de Porta** .  

5.  Na caixa de diálogo **Detalhes de Porta** , especifique o número da porta e a descrição para o item e clique em **OK**.  

6.  Selecione **Usar site personalizado** , se for usar o nome do site personalizado **SMSWeb** para sistemas de site que executam o IIS.  

7.  Clique em **OK** para fechar a caixa de diálogo de propriedades do site.  

 Repita esse procedimento para todos os sites primários da hierarquia.
