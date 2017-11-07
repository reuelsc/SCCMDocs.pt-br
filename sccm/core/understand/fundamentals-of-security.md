---
title: "Conceitos básicos de segurança"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as camadas de segurança no System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b13371e7ea16c5614b0742bd4f4241bd84de105d
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>Conceitos básicos de segurança do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A segurança do System Center Configuration Manager é composta por diversas camadas. A primeira camada é fornecida pelos recursos do segurança do Windows para o sistema operacional e para a rede e inclui:  

-   Compartilhamento de arquivos para transferi-los entre os componentes do Configuration Manager.  

-   Listas de Controle de Acesso (ACLs) para ajudar a proteger arquivos e chaves do Registro.  

-   IPsec (Protocolo IPsec) para ajudar a proteger as comunicações.  

-   Política de Grupo para definir a política de segurança.  

-   Permissões de DCOM (Distributed Component Object Model) para aplicativos distribuídos, como o console do Configuration Manager.  

-   Active Directory Domain Services para armazenar entidades de segurança.  

-   Segurança da conta do Windows, incluindo alguns grupos que são criados durante a instalação do Configuration Manager.  

Além disso, componentes de segurança adicionais, como firewalls e detecção de intrusões, ajudam a fornecer defesa para todo o ambiente. Os certificados emitidos pelas implementações de PKI (infraestrutura de chave pública) padrão do setor ajudam a fornecer autenticação, assinatura e criptografia.  

Além da segurança fornecida pela infraestrutura de servidor e de rede do Windows, o Configuration Manager controla o acesso ao console do Configuration Manager e a seus recursos de várias maneiras. Por padrão, apenas os administradores locais têm direitos sobre esses arquivos e chaves do Registro que são necessários para executar o console do Configuration Manager em computadores em que ele está instalado.  

A próxima camada de segurança é baseada no acesso pela WMI (Instrumentação de Gerenciamento do Windows), especificamente o Provedor de SMS. O Provedor de SMS é um componente do Configuration Manager que concede acesso a um usuário para consulta de informações no banco de dados do site. Por padrão, o acesso ao provedor é restrito a membros do grupo local Administradores de SMS. Em um primeiro momento, esse grupo contém apenas o usuário que instalou o Configuration Manager. Para conceder outras permissões de contas do repositório do Common Information Model (CIM) e o Provedor de SMS, adicione outras contas ao grupo Administradores de SMS.  

A camada final de segurança é baseada em permissões para objetos do banco de dados do site. Por padrão, a conta Sistema Local e a conta de usuário usada na instalação do Configuration Manager podem administrar todos os objetos no banco de dados do site. É possível conceder e restringir as permissões para usuários administrativos adicionais no console do Configuration Manager usando a administração baseada em funções.  



## <a name="role-based-administration"></a>Administração baseada em funções  
 O Configuration Manager usa a administração baseada em funções para ajudar a proteger objetos, como coleções, implantações e sites. Este modelo de administração centralizado define e gerencia configurações de acesso segurança de toda a hierarquia para todos os sites e as configurações do site. As funções de segurança são atribuídas a usuários administrativos e permissões de grupo. As permissões são conectadas a diferentes tipos de objeto do Configuration Manager, como as permissões que são usadas para criar ou alterar configurações de cliente. A segurança analisa as instâncias de grupo específicas dos objetos que um usuário administrativo é responsável por gerenciar, como um aplicativo que instala o Microsoft Office. A combinação de funções de segurança, escopos de segurança e coleções define os objetos que um usuário administrativo pode exibir e gerenciar. O Configuration Manager instala algumas funções de segurança padrão para tarefas típicas de gerenciamento. Mas você pode criar suas próprias funções de segurança para oferecer suporte às necessidades específicas do seu negócio.  

 Para mais informações, consulte [Configurar administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="securing-client-endpoints"></a>Protegendo os pontos de extremidade do cliente  
 A comunicação do cliente com as funções do sistema de sites é protegida usando certificados autoassinados ou certificados PKI. Você precisará usar um certificado PKI para computadores cliente que o Configuration Manager detecta que estão na Internet e para clientes de dispositivos móveis. O certificado PKI usa HTTPS para proteger os pontos de extremidade de cliente. As funções de sistema de site que os clientes se conectam podem ser configuradas para a comunicação de cliente HTTP ou HTTPS. Os computadores cliente sempre se comunicam usando o método mais seguro disponível. Os computadores cliente somente voltam a usar o método de comunicação menos seguro de HTTP na intranet se você tiver funções do sistema de sites que permitem comunicação HTTP.  

 Para obter mais informações, consulte [Referência técnica para controles de criptografia para o System Center Configuration Manager](../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

## <a name="configuration-manager-accounts-and-groups"></a>Contas e grupos do Gerenciador de Configurações  
 O Configuration Manager usa a conta Sistema Local para a maioria das operações do site. Algumas tarefas de gerenciamento podem exigir que você crie e mantenha contas adicionais. Diversos grupos padrão e funções do SQL Server são criados durante a instalação. Talvez você precise adicionar manualmente as contas de usuário ou o computador para os grupos padrão e para as funções do SQL Server.  

 Para obter mais informações, consulte [Contas usadas no System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## <a name="privacy"></a>Privacidade  
 Embora os produtos de gerenciamento corporativo ofereçam várias vantagens, pois podem gerenciar de maneira efetiva vários clientes, você também deve estar atento a como esse software pode afetar a privacidade dos usuários em sua organização. O System Center Configuration Manager inclui várias ferramentas para coletar dados e monitorar dispositivos. Algumas ferramentas podem gerar problemas de privacidade.  

 Por exemplo, ao instalar o cliente do Configuration Manager, muitas configurações de gerenciamento são habilitadas por padrão. Isso faz com que o software cliente envie informações para o site do Configuration Manager. As informações de cliente são armazenadas no banco de dados do Configuration Manager e não são enviadas à Microsoft. Antes de implementar o System Center Configuration Manager, considere seus requisitos de privacidade.  
