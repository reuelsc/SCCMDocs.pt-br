---
title: "Métodos de instalação do cliente | Microsoft Docs"
description: "Conheça os métodos de instalação do cliente para o System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
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
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 593fbd0587d54490246f48ae54f666bac6b7830d
ms.openlocfilehash: a7d5a04cf34c49246f768f9a4757c5da3b4db31a
ms.lasthandoff: 12/16/2016


---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>Métodos de instalação do cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode usar diferentes métodos para instalar o software cliente do Configuration Manager (também conhecido como ConfigMgr ou SCCM). Você pode usar um método ou uma combinação desses métodos. Neste tópico, você pode ler sobre cada método para saber qual funcionará melhor na sua organização.  

## <a name="client-push-installation"></a>Instalação do cliente por push  

 **Plataforma de cliente com suporte:** Windows  

 **Vantagens**  

-   Pode ser usada para instalar o cliente em um único computador, em uma coleção de computadores, ou para os resultados de uma consulta.  

-   Pode ser usada para instalar automaticamente o cliente em todos os computadores descobertos.  

-   Utiliza automaticamente as propriedades de instalação do cliente definidas na guia **Cliente** na caixa de diálogo **Propriedades da Instalação do Cliente por Push** .  

 **Desvantagens**  

-   Pode causar elevado tráfego na rede durante o envio por push a coleções grandes.  

-   Pode ser usada somente em computadores que foram descobertos pelo Configuration Manager.  

-   Não pode ser usada para instalar clientes em um grupo de trabalho.  

-   Uma conta de instalação de cliente por push deve ser especificada para ter direitos administrativos no computador cliente desejado.  

-   O Windows Firewall deve ser configurado em computadores cliente com exceções, de forma que a instalação de cliente por push possa ser concluída.  

-   Não é possível cancelar a instalação de cliente por push. Quando você utiliza esse método de instalação de cliente para um site, o Configuration Manager tenta instalar o cliente em todos os recursos descobertos e tenta novamente em caso de falha por até 7 dias.  

 Para obter mais informações sobre este método de instalação, consulte [Como implantar clientes em computadores Windows no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="software-update-point-based-installation"></a>Instalação baseada em ponto de atualização de software  
 **Plataforma de cliente com suporte:** Windows  

 **Vantagens:**  

-   Pode usar a infraestrutura de atualizações de software existente para gerenciar o software cliente.  

-   Poderá instalar automaticamente o software cliente em computadores novos se o Windows Server Update Services (WSUS) e as configurações da Política de Grupo nos Serviços de Domínio Active Directory estiverem configurados corretamente.  

-   Não exige que os computadores sejam descobertos para que o cliente possa ser instalado.  

-   Os computadores podem ler as propriedades de instalação de cliente publicadas nos Serviços de Domínio Active Directory .  

-   Irá reinstalar o software cliente se ele for removido.  

-   Não exige que você configure e mantenha uma conta de instalação para o computador cliente desejado.  

 **Desvantagens:**  

-   Requer uma infraestrutura de atualizações de software em funcionamento como um pré-requisito.  

-   Deve usar o mesmo servidor para a instalação de cliente e as atualizações de software, e esse servidor deve residir em um site primário.  

-   Para instalar novos clientes, configure um GPO (Objeto de Política de Grupo) nos Serviços de Domínio do Active Directory com a porta e o ponto de atualização de software ativo do cliente.  

-   Se o esquema do Active Directory não for estendido para o Configuration Manager, use as configurações de Política de Grupo para provisionar computadores com as propriedades de instalação do cliente.  

 Para obter mais informações sobre este método de instalação, consulte [Como implantar clientes em computadores Windows no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="group-policy-installation"></a>Instalação de Política de Grupo  
 **Plataforma de cliente com suporte:** Windows  

 **Vantagens:**  

-   Não exige que os computadores sejam descobertos para que o cliente possa ser instalado.  

-   Pode ser usada para novas instalações de cliente ou para atualizações.  

-   Os computadores podem ler as propriedades de instalação de cliente publicadas nos Serviços de Domínio Active Directory .  

-   Não exige que você configure e mantenha uma conta de instalação para o computador cliente desejado.  

 **Desvantagens:**  

-   Poderá causar elevado tráfego na rede se um grande número de clientes estiver sendo instalado.  

-   Se o esquema do Active Directory não for estendido para o Configuration Manager, use as configurações de Política de Grupo para adicionar propriedades de instalação de cliente aos computadores em seu site.  

 Para obter mais informações sobre este método de instalação, consulte [Como implantar clientes em computadores Windows no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="logon-script-installation"></a>Instalação de script de logon  
 **Plataforma de cliente com suporte:** Windows  

 **Vantagens:**  

-   Não exige que os computadores sejam descobertos para que o cliente possa ser instalado.  

-   Oferece suporte ao uso de propriedades de linha de comando para o CCMSetup.  

 **Desvantagens:**  

-   Poderá causar elevado tráfego na rede se um grande número de clientes estiver sendo instalado num curto período de tempo.  

-   Poderá demorar muito para se instalar em todos os computadores cliente se os usuários não fizerem frequentemente logon na rede.  

 Para obter mais informações sobre este método de instalação, consulte [Como implantar clientes em computadores Windows no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="manual-installation"></a>Instalação manual  
 **Plataforma de cliente com suporte:** Windows, UNIX/Linux, Mac OS X  

 **Vantagens:**  

-   Não exige que os computadores sejam descobertos para que o cliente possa ser instalado.  

-   Pode ser útil para fins de teste.  

-   Oferece suporte ao uso de propriedades de linha de comando para o CCMSetup.  

 **Desvantagens:**  

-   Sem automação, portanto demorada.  

 Para obter mais informações sobre como instalar manualmente o cliente em cada uma das plataformas, confira:  

-   [Como implantar clientes em computadores Windows no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

-   [Como implantar clientes para servidores UNIX e Linux no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)  

-   [Como implantar clientes em Macs no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

