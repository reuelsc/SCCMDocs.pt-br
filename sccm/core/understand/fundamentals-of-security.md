---
title: "Conceitos básicos de segurança | Microsoft Docs"
description: "Saiba mais sobre as camadas de segurança no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: b4d12eaadaf0324515f6ae595a737f576bd5076c


---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>Conceitos básicos de segurança do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A segurança do System Center Configuration Manager é composta por diversas camadas. A primeira camada é fornecida pelos recursos do segurança do Windows para o sistema operacional e para a rede, e inclui:  

-   Compartilhamento de arquivos para transferi-los entre os componentes do Configuration Manager  

-   Listas de controle de acesso (ACLs) para ajudar a proteger arquivos e chaves do Registro  

-   IPsec para proteger as comunicações  

-   Política de grupo para configurar a política de segurança  

-   Permissões DCOM para aplicativos distribuídos, como o console do Configuration Manager  

-   Serviços de Domínio do Active Directory para armazenar entidades de segurança  

-   Segurança da conta do Windows, incluindo alguns grupos que são criados durante a Instalação do Configuration Manager  

Componentes de segurança adicionais, como firewalls e detecção de intrusões, ajudam a fornecer uma melhor defesa para todo o ambiente. Os certificados emitidos pelas implementações padrão de PKI do setor ajudam a fornecer autenticação, assinatura e criptografia.  

Além da segurança fornecida pela infraestrutura de servidor e de rede do Windows, o Configuration Manager controla o acesso ao console do Configuration Manager e a seus recursos de várias maneiras. Por padrão, apenas os Administradores locais têm direitos sobre esses arquivos e chaves do Registro necessárias para executar o console do Configuration Manager em computadores em que ele está instalado.  

A próxima camada de segurança é baseada no acesso pela WMI (Instrumentação de Gerenciamento do Windows), especificamente o **Provedor de SMS**. O Provedor de SMS é um componente do Configuration Manager que concede acesso a um usuário para consulta de informações no banco de dados do site. Por padrão, o acesso ao provedor é restrito a membros do grupo local **Administradores de SMS** . Em um primeiro momento, esse grupo contém apenas o usuário que instalou o Configuration Manager. Para conceder outras permissões de contas do repositório do Common Information Model (CIM) e o Provedor de SMS, adicione outras contas ao grupo Administradores de SMS.  

A camada final de segurança é baseada em permissões para objetos do banco de dados do site. Por padrão, a conta Sistema Local e a conta de usuário usada na instalação do Configuration Manager podem administrar todos os objetos no banco de dados do site. É possível conceder e restringir as permissões para usuários administrativos adicionais no console do Configuration Manager usando uma **administração baseada em funções**.  

O restante deste tópico aborda aspectos de segurança relacionados ao Configuration Manager.  

## <a name="role-based-administration"></a>Administração baseada em funções  
 O Configuration Manager usa a administração baseada em funções para ajudar a proteger objetos, como coleções, implantações e sites. Este modelo de administração centralizado define e gerencia configurações de acesso segurança de toda a hierarquia para todos os sites e as configurações do site. As funções de segurança são atribuídas a usuários administrativos e permissões de grupo para diferentes tipos de objeto do Configuration Manager, como as permissões para criar ou alterar as configurações do cliente. Os escopos de segurança agrupam instâncias específicas de objetos pelas quais um usuário administrativo é responsável por gerenciar, como um aplicativo que instala o Microsoft Office 2010. A combinação de funções de segurança, escopos de segurança e coleções define quais objetos um usuário administrativo pode exibir e gerenciar. O Configuration Manager instala algumas funções de segurança padrão para tarefas típicas de gerenciamento. No entanto, você pode criar suas próprias funções de segurança para oferecer suporte às necessidades específicas dos negócios.  

 Para mais informações, consulte [Configurar administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)  

## <a name="securing-client-endpoints"></a>Protegendo os pontos de extremidade do cliente  
 A comunicação do cliente com as funções de sistema de site é protegida usando certificados autoatribuídos ou certificados PKI (infraestrutura de chave pública). Os computadores cliente que o Configuration Manager detecta estarem em clientes de dispositivos móveis e Internet devem usar certificados PKI. Dessa maneira, os pontos de extremidade podem ser protegidos usando HTTPS. As funções de sistema de site que os clientes se conectam podem ser configuradas para a comunicação de cliente HTTP ou HTTPS. Os computadores cliente sempre se comunicam usando o método mais seguro disponível e somente voltam a usar o menos seguro de HTTP na intranet se você possuir funções de sistema de site que permitem comunicação HTTP.  

 Para obter mais informações, consulte [Referência técnica para controles de criptografia para o System Center Configuration Manager](../../protect/deploy-use/cryptographic-controls-technical-reference.md)  

## <a name="configuration-manager-accounts-and-groups"></a>Contas e grupos do Gerenciador de Configurações  
 O Configuration Manager usa a conta **Sistema Local** para a maioria das operações do site. No entanto, algumas tarefas de gerenciamento podem exigir a criação e manutenção de contas adicionais. Diversos grupos padrão e funções do SQL Server são criados durante a instalação. No entanto, talvez você precise adicionar manualmente as contas de usuário ou o computador para essas funções e grupos padrão.  

 Para obter mais informações, consulte [Contas usadas no System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## <a name="privacy"></a>Privacidade  
 Embora os produtos de gerenciamento corporativo ofereçam várias vantagens, pois podem gerenciar de maneira efetiva vários clientes, você também deve estar atento a como esse software pode afetar a privacidade dos usuários em sua organização. O System Center Configuration Manager inclui várias ferramentas para coletar dados e monitorar dispositivos, algumas das quais poderiam gerar problemas de privacidade.  

 Por exemplo, ao instalar o cliente do Configuration Manager, muitas configurações de gerenciamento são habilitadas por padrão. Isso resulta no software cliente enviando informações para o site do Configuration Manager. As informações do cliente são armazenadas no banco de dados do Configuration Manager e não são enviadas à Microsoft. Antes de implementar o System Center Configuration Manager, considere seus requisitos de privacidade.  



<!--HONumber=Dec16_HO3-->


