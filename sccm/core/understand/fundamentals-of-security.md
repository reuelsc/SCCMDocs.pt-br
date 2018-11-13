---
title: Conceitos básicos de segurança
titleSuffix: Configuration Manager
description: Saiba mais sobre as camadas de segurança no Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 45b65e5ff35f93bb79418f00795aecab5cc208b9
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411197"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Conceitos básicos de segurança do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo resume os seguintes componentes de segurança fundamentais de qualquer ambiente do Configuration Manager:
- [Camadas de segurança](#bkmk_layers)
- [Administração baseada em funções](#bkmk_rba)
- [Protegendo os pontos de extremidade do cliente](#bkmk_endpoints)
- [Contas e grupos do Configuration Manager](#bkmk_accounts)
- [Privacidade](#bkmk_privacy)

## <a name="bkmk_layers"></a> Camadas de segurança

A segurança do Configuration Manager é composta pelas seguintes camadas: 
- [Segurança de rede e Sistema Operacional Windows](#bkmk_layer-windows)
- [Infraestrutura de rede: firewalls, detecção de intrusões, PKI (infraestrutura de chave pública)](#bkmk_layer-network)
- [Controles de segurança do Configuration Manager](#bkmk_layer-cm)
- [Provedor de SMS](#bkmk_layer-provider)
- [Permissões de banco de dados do site](#bkmk_layer-db)

#### <a name="bkmk_layer-windows"></a> Segurança de rede e Sistema Operacional Windows
A primeira camada é fornecida pelos recursos do segurança do Windows para o sistema operacional e para a rede. Essa camada inclui os seguintes componentes:  

-   Compartilhamento de arquivos para transferi-los entre os componentes do Configuration Manager  

-   Listas de controle de acesso (ACLs) para ajudar a proteger arquivos e chaves do Registro  

-   Protocolo IPsec para ajudar a proteger as comunicações  

-   Política de Grupo para definir a política de segurança  

-   Permissões de DCOM (Distributed Component Object Model) para aplicativos distribuídos, como o console do Configuration Manager  

-   Serviços de Domínio do Active Directory para armazenar entidades de segurança  

-   Segurança da conta do Windows, incluindo alguns grupos criados pelo Configuration Manager durante a instalação  

#### <a name="bkmk_layer-network"></a> Infraestrutura de rede

Componentes de segurança adicionais, como firewalls e detecção de intrusões, ajudam a fornecer defesa para todo o ambiente. Os certificados emitidos pelas implementações de PKI (infraestrutura de chave pública) padrão do setor ajudam a fornecer autenticação, assinatura e criptografia.  

#### <a name="bkmk_layer-cm"></a> Controles de segurança do Configuration Manager

Além da segurança fornecida pela infraestrutura de servidor e de rede do Windows, o Configuration Manager controla o acesso ao seu console e a seus recursos de várias maneiras. Por padrão, apenas os administradores locais têm direitos sobre esses arquivos e chaves do Registro que o console do Configuration Manager exige em computadores em que você o instala.  

#### <a name="bkmk_layer-provider"></a> Provedor de SMS

A próxima camada de segurança é baseada no acesso pela WMI (Instrumentação de Gerenciamento do Windows), especificamente o Provedor de SMS. O Provedor de SMS é um componente do Configuration Manager que concede acesso a um usuário para consulta de informações no banco de dados do site. Por padrão, o acesso ao provedor é restrito a membros do grupo local Administradores de SMS. Em um primeiro momento, esse grupo contém apenas o usuário que instalou o Configuration Manager. Para conceder outras permissões de contas do repositório do Common Information Model (CIM) e o Provedor de SMS, adicione outras contas ao grupo Administradores de SMS.  

Para obter mais informações, veja [Planejar para o provedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

#### <a name="bkmk_layer-db"></a> Permissões de banco de dados do site

A camada final de segurança é baseada em permissões para objetos do banco de dados do site. Por padrão, a conta Sistema Local e a conta de usuário usada na instalação do Configuration Manager podem administrar todos os objetos no banco de dados do site. Conceda e restrinja permissões para usuários administrativos adicionais no console do Configuration Manager usando a administração baseada em funções.  



## <a name="bkmk_rba"></a> Administração baseada em funções  

 O Configuration Manager usa a administração baseada em funções para ajudar a proteger objetos, como coleções, implantações e sites. Este modelo de administração centralizado define e gerencia configurações de acesso segurança de toda a hierarquia para todos os sites e as configurações do site. 

 Um administrador atribui *funções de segurança* a usuários administrativos e permissões de grupo. As permissões são conectadas a diferentes tipos de objeto do Configuration Manager, por exemplo, para criar ou alterar configurações de cliente. 

 A *segurança analisa* as instâncias de grupo específicas dos objetos que um usuário administrativo é responsável por gerenciar, como um aplicativo que instala o Microsoft Office. 

 A combinação de funções de segurança, escopos de segurança e coleções define os objetos que um usuário administrativo pode exibir e gerenciar. O Configuration Manager instala algumas funções de segurança padrão para tarefas típicas de gerenciamento. Crie suas próprias funções de segurança para oferecer suporte às suas necessidades empresariais específicas.  

 Para obter mais informações, confira [Configurar a administração baseada em função](/sccm/core/servers/deploy/configure/configure-role-based-administration).  



## <a name="bkmk_endpoints"></a> Protegendo os pontos de extremidade do cliente  

 O Configuration Manager protege a comunicação de cliente para funções do sistema de site usando o autoassinados ou certificados PKI ou tokens do Azure AD (Azure Active Directory). Alguns cenários exigem o uso de certificados PKI. Por exemplo, [gerenciamento de clientes baseados na Internet](/sccm/core/clients/manage/plan-internet-based-client-management) e para [clientes de dispositivos móveis](/sccm/mdm/plan-design/plan-on-premises-mdm).  

 Você pode configurar as funções de sistema de site às quais os clientes se conectam para a comunicação de cliente HTTP ou HTTPS. Os computadores cliente sempre se comunicam usando o método mais seguro disponível. Os computadores cliente somente voltarão a usar o método de comunicação menos seguro se você tiver funções do sistema de sites que permitirem comunicação HTTP.  

 Para obter mais informações, confira [Planejar para ter segurança](/sccm/core/plan-design/security/plan-for-security).



## <a name="bkmk_accounts"></a> Contas e grupos do Configuration Manager  

 O Configuration Manager usa a conta Sistema Local para a maioria das operações do site. Algumas tarefas de gerenciamento podem exigir que você crie e mantenha contas adicionais. O Configuration Manager cria diversos grupos padrão e funções do SQL Server durante a instalação. Talvez você precise adicionar manualmente as contas de usuário ou o computador para os grupos padrão e para as funções do SQL Server.  

 Para obter mais informações, confira [Contas usadas no Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).  



## <a name="bkmk_privacy"></a> Privacidade  

 Antes de implementar o Configuration Manager, considere seus requisitos de privacidade. Embora os produtos de gerenciamento empresarial ofereçam várias vantagens, pois podem gerenciar de maneira efetiva vários clientes, este software pode afetar a privacidade dos usuários em sua organização. O Configuration Manager inclui várias ferramentas para coletar dados e monitorar dispositivos. Algumas ferramentas podem gerar problemas de privacidade em sua organização.  

 Por exemplo, ao instalar o cliente do Configuration Manager, ele habilita muitas configurações de gerenciamento por padrão. Essa configuração faz com que o software cliente envie informações para o site do Configuration Manager. O site armazena informações de cliente no banco de dados do site. As informações do cliente não são enviadas diretamente para a Microsoft. Para obter mais informações, consulte [Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).



## <a name="see-also"></a>Consulte também

- [Planejar a segurança](/sccm/core/plan-design/security/plan-for-security)  

- [Segurança e privacidade para clientes do Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configurar a segurança](/sccm/core/plan-design/security/configure-security)   

- [Comunicação entre pontos de extremidade](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Referência técnica de controles de criptografia](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  
