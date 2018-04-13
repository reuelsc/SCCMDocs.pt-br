---
title: Métodos de instalação de cliente
titleSuffix: Configuration Manager
description: Saiba mais sobre os métodos de instalação do cliente do Configuration Manager.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
caps.latest.revision: 9
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38f7d428149f4a4ac2b0bcb604031eca60a0fae5
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2018
---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>Métodos de instalação do cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode usar diferentes métodos para instalar o software cliente do Configuration Manager. Use um método ou uma combinação de métodos. Este artigo descreve cada método, para que você saiba qual deles funciona melhor para sua organização.  

## <a name="client-push-installation"></a>Instalação do cliente por push  

**Plataforma de cliente compatível**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Pode ser usada para instalar o cliente em um único computador, em uma coleção de computadores, ou para os resultados de uma consulta.  

-   Pode ser usada para instalar automaticamente o cliente em todos os computadores descobertos.  

-   Utiliza automaticamente as propriedades de instalação do cliente definidas na guia **Cliente** na caixa de diálogo **Propriedades da Instalação do Cliente por Push** .  

#### <a name="disadvantages"></a>Desvantagens  

-   Pode causar elevado tráfego na rede durante o envio por push a coleções grandes.  

-   Pode ser usada somente em computadores que foram descobertos pelo Configuration Manager.  

-   Não pode ser usada para instalar clientes em um grupo de trabalho.  

-   Uma conta de instalação de cliente por push deve ser especificada para ter direitos administrativos no computador cliente desejado.  

-   O Firewall do Windows deve ser configurado com exceções nos computadores cliente.   

-   Não é possível cancelar a instalação do cliente por push. O Configuration Manager tenta instalar o cliente em todos os recursos descobertos. Ele tenta as falhas novamente por até sete dias.  

Para obter mais informações, consulte [Como instalar clientes com o push do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).  



## <a name="software-update-point-based-installation"></a>Instalação baseada em ponto de atualização de software  

**Plataforma de cliente compatível**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Pode usar a infraestrutura de atualizações de software existente para gerenciar o software cliente.  

-   Se o WSUS (Windows Server Update Services) e as configurações de política de grupo no Active Directory Domain Services forem definidas corretamente, ele poderá instalar automaticamente o software cliente em novos computadores.  

-   Não exige que os computadores sejam descobertos antes que o cliente possa ser instalado.  

-   Os computadores podem ler as propriedades de instalação de cliente publicadas nos Serviços de Domínio Active Directory .  

-   Se o cliente for removido, esse método o reinstalará.  

-   Não exige que você configure e mantenha uma conta de instalação para o computador cliente desejado.  

#### <a name="disadvantages"></a>Desvantagens  

-   Requer uma infraestrutura de atualizações de software em funcionamento como um pré-requisito.  

-   Deve usar o mesmo servidor para a instalação do cliente e as atualizações de software. Esse servidor deve residir em um site primário.  

-   Para instalar novos clientes, configure um objeto de política de grupo no Active Directory Domain Services com a porta e o ponto de atualização de software ativo do cliente.  

-   Se o esquema do Active Directory não for estendido para o Configuration Manager, use as configurações de política de grupo para provisionar computadores com as propriedades de instalação do cliente.  

Para obter mais informações, consulte [Como instalar clientes com a instalação baseada em atualização de software](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP).  



## <a name="group-policy-installation"></a>Instalação da política de grupo  

**Plataforma de cliente compatível**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Não exige que os computadores sejam descobertos antes que o cliente possa ser instalado.  

-   Pode ser usada para novas instalações de cliente ou para atualizações.  

-   Os computadores podem ler as propriedades de instalação de cliente publicadas nos Serviços de Domínio Active Directory .  

-   Não exige que você configure e mantenha uma conta de instalação para o computador cliente desejado.  

#### <a name="disadvantages"></a>Desvantagens  

-   A instalação de um grande número de clientes poderá causar um elevado tráfego de rede.  

-   Se o esquema do Active Directory não for estendido para o Configuration Manager, use as configurações de política de grupo para adicionar as propriedades de instalação do cliente aos computadores do site.  

Para obter mais informações, consulte [Como instalar clientes com a política de grupo](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientGP).  



## <a name="logon-script-installation"></a>Instalação de script de logon  

**Plataforma de cliente compatível**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Não exige que os computadores sejam descobertos antes que o cliente possa ser instalado.  

-   Oferece suporte ao uso de propriedades de linha de comando para o CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

-   A instalação de um grande número de clientes em um período curto poderá causar um elevado tráfego de rede.  

-   Se os usuários não fizerem logon na rede frequentemente, poderá levar muito tempo para a instalação em todos os computadores cliente.  

Para obter mais informações, consulte [Como instalar clientes com scripts de logon](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientLogonScript).  



## <a name="manual-installation"></a>Instalação manual  

**Plataforma de cliente compatíveis:** Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Vantagens  

-   Não exige que os computadores sejam descobertos antes que o cliente possa ser instalado.  

-   Pode ser útil para fins de teste.  

-   Oferece suporte ao uso de propriedades de linha de comando para o CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

-   Sem automação, portanto demorada.  

Para obter mais informações sobre como instalar manualmente o cliente em cada uma das plataformas, consulte os seguintes artigos:  

-   [Como implantar clientes em computadores com Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)  

-   [Como implantar clientes em servidores UNIX e Linux](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)  

-   [Como implantar clientes em Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  



## <a name="microsoft-intune-mdm-installation"></a>Instalação do Microsoft Intune MDM

**Plataforma de cliente compatíveis**: Windows 10

#### <a name="advantages"></a>Vantagens  

-   Não exige que os computadores sejam descobertos antes que o cliente possa ser instalado.  

-   Não exige que você configure e mantenha uma conta de instalação para o computador cliente desejado.  

-   Pode usar a autenticação moderna com o Azure Active Directory.  

-   Pode instalar e atribuir computadores na Internet.  

-   Pode automatizar com o Windows AutoPilot e o Microsoft Intune para o cogerenciamento.  

#### <a name="disadvantages"></a>Desvantagens  

-   Exige tecnologias adicionais fora do Configuration Manager.  

-   Exige que o dispositivo tenha acesso à Internet, mesmo se não for baseado na Internet.  

Para obter mais informações, consulte os seguintes artigos:  

-   [Como instalar clientes em dispositivos Windows gerenciados pelo Intune MDM](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#bkmk_mdm)  

-   [Instalar e atribuir clientes do Windows 10 do Configuration Manager usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

