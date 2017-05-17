---
title: "Como gerenciar a Proteção de Dispositivo do Windows | Microsoft Docs"
description: "Saiba como usar o System Center Configuration Manager para gerenciar a Proteção de Dispositivo do Windows."
ms.custom: na
ms.date: 04/14/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 49599f529bb409f40caf9057989762e759f1c0ac
ms.openlocfilehash: 113dddb2939fedf24e8d489ff4443bd5e3e72c65
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---


# <a name="device-guard-management-with-configuration-manager"></a>Gerenciamento de Proteção do Dispositivo com Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

## <a name="introduction"></a>Introdução
A Proteção de Dispositivo do Windows é um grupo de recursos do Windows 10 projetado para proteger computadores contra malware e outros softwares não confiáveis. Ele impede que um código mal-intencionado seja executado, garantindo que somente o código aprovado, que você conhece, possa ser executado.

A Proteção de Dispositivo abrange o software e o hardware com base na funcionalidade de segurança. Integridade do código configurável é uma camada de segurança baseada em software que impõe uma lista explícita de software que pode ser executado em um PC. Por si só, a integridade do código configurável não tem todos os pré-requisitos de hardware ou firmware. As políticas de Proteção do dispositivo implantadas com o Configuration Manager permitem uma política de integridade do código configurável nos PCs em coleções de destino que atendem aos requisitos de SKU e a versão mínima do Windows descritos abaixo. Opcionalmente, o hipervisor com base na proteção das políticas de integridade do código implantadas através do Configuration Manager pode ser habilitado com a Política de Grupo no hardware compatível.

Para saber mais sobre a Proteção do Dispositivo, leia [Guia de implantação da Proteção do Dispositivo](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

Você pode usar o Configuration Manager para implantar uma política de Proteção do Dispositivo que permite configurar o modo como a Proteção será executada nos PCs em uma coleção. 

É possível configurar um dos seguintes modos:

1.    **Imposição habilitada** - somente os executáveis confiáveis podem ser executados.
2.    **Somente auditoria** - permite que todos os executáveis sejam rodados, mas registra os executáveis não confiáveis rodados no log de eventos do cliente local.

>[!TIP]
>Nesta versão do Configuration Manager, a Proteção do Dispositivo é um recurso de pré-lançamento. Para habilitá-lo, veja [Recursos de pré-lançamento no System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

### <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>O que pode ser executado quando você implanta uma política de Proteção do Dispositivo?

A Proteção do dispositivo do Windows permite controlar fortemente o que pode ser executado nos PCs gerenciados. Isso pode ser particularmente útil para os PCs em departamentos de alta segurança, onde é vital que os softwares indesejados não tenham permissão para ser executados.

Quando você implanta uma política, normalmente, os executáveis a seguir poderão ser executados:

- componentes do sistema operacional Windows
- drivers do Centro de Desenvolvimento de Hardware (que têm as assinaturas do Windows Hardware Quality Labs)
- aplicativos da Windows Store
- cliente do Configuration Manager 
- todo software implantado com o Configuration Manager que os PCs instalam depois da política de Proteção ser processada. 
- Atualizações para componentes do Windows do:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Gerenciador de Configurações

>[!IMPORTANT]
>Não inclui nenhum software que **não** seja integrado no Windows que atualiza automaticamente a partir da Internet ou de atualizações de software de terceiros, com instalação via qualquer mecanismo de atualização mencionado acima ou a partir da Internet. Somente as alterações de software implantadas no cliente do Configuration Manager poderão ser executadas.

## <a name="before-you-start"></a>Antes de começar

Antes de configurar ou implantar as políticas de Proteção do Dispositivo, leia as seguintes informações:

- o Gerenciamento da Proteção do Dispositivo é um recurso de pré-lançamento do Configuration Manager e está sujeito a alterações.
- Para usar a Proteção do Dispositivo, os PCs gerenciados devem estar executando o Windows 10 Enterprise com a Atualização para Criadores ou posterior.
- Depois de uma política ser processada com êxito em um PC cliente, o Configuration Manager é configurado como um Instalador Gerenciado no cliente e o software implantado por meio do SCCM depois da política ser processada é automaticamente confiável. O software instalado pela Configuração Gerenciada antes da política de Proteção do Dispositivo ser processada não é automaticamente confiável.
- Nesta versão de pré-lançamento, depois do PC cliente receber uma implantação de uma política de Proteção do Dispositivo, ele ficará aleatório durante o processamento dessa política em um período de duas horas. 
- Os PCs cliente devem ter conectividade com o Controlador de Domínio para uma política de Proteção do Dispositivo ser processada com êxito.
- O agendamento de avaliação de conformidade padrão para as políticas de Proteção do Dispositivo, configuráveis durante a implantação, é a cada um dia. Se forem observados problemas no processamento da política, pode ser benéfico configurar o agendamento de avaliação de conformidade para que seja mais curto, por exemplo, a cada uma hora. Esse agendamento determina com que frequência os clientes tentarão novamente processar uma política de Proteção do Dispositivo em caso de falha.
- Independentemente do modo de imposição selecionado, quando você implantar uma política de Proteção do Dispositivo, os PCs cliente não poderão executar os aplicativos HTML com a extensão .hta.

## <a name="how-to-create-a-device-guard-policy"></a>Como criar uma política de Proteção do Dispositivo
1.    No console do Configuration Manager, clique em **Ativos e Conformidade**.
2.    No espaço de trabalho **Ativos e Conformidade**, expanda **Proteção do Ponto de Extremidade**e clique em **Políticas de Proteção do Dispositivo**.
3.    Na guia **Início**, no grupo **Criar**, clique em **Criar Política de Proteção do Dispositivo**.
4.    Na página **Geral** do **Assistente da Política de Proteção do Dispositivo**, especifique o seguinte:
    - **Nome** - insira um nome exclusivo para a política de Proteção do Dispositivo. 
    - **Descrição** - opcionalmente, insira uma descrição da política que ajudará a identificá-la no console do Configuration Manager.
    - **Modo de imposição** -escolha um dos seguintes métodos de imposição para a Proteção do Dispositivo no PC cliente.
        - **Imposição habilitada** - permitir somente os executáveis confiáveis podem ser executados.
        - **Somente auditoria** - permite que todos os executáveis sejam rodados, mas registra os executáveis não confiáveis rodados no log de eventos do cliente local.
5.    Clique em **Avançar** e conclua o assistente.

## <a name="how-to-deploy-a-device-guard-policy"></a>Como implantar uma política de Proteção do Dispositivo
1.    No console do Configuration Manager, clique em **Ativos e Conformidade**.
2.    No espaço de trabalho **Ativos e Conformidade**, expanda **Proteção do Ponto de Extremidade**e clique em **Políticas de Proteção do Dispositivo**.
3.    Na lista de políticas, selecione a que você deseja implantar e na guia **Início**, no grupo **Implantação**, clique em **Implantar**.
4.    Na caixa de diálogo **Implantar Política de Proteção do Dispositivo**, selecione a coleção na qual você deseja implantar a política, configure uma agenda para quando os clientes avaliarão a política e, por fim, selecione se o cliente pode avaliar a política fora de qualquer janela de manutenção configurada.
5.    Quando tiver terminado, clique em **OK** para implantar a política. 

Depois que a política for processada em um PC cliente, uma reinicialização será agendada no cliente de acordo com as **Configurações do Cliente** para **Reiniciar Computador**.
**Até que você reinicie o PC cliente, a política não terá efeito.**

## <a name="how-to-monitor-a-device-guard-policy"></a>Como monitorar uma política de Proteção do Dispositivo

Use as informações no tópico [Monitorar configurações de conformidade](/sccm/compliance/deploy-use/monitor-compliance-settings) para ajudá-lo a monitorar a política implantada para garantir que ela tenha sido aplicada em todos os PCs corretamente.

Use o seguinte arquivo de log nos PCs cliente para monitorar o processamento de uma política de Proteção do Dispositivo:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Para verificar o software específico sendo bloqueado ou auditado, consulte os seguintes logs de eventos do cliente local. No Visualizador de Eventos, os logs relevantes são:

1.    Para o bloqueio e a auditoria dos arquivos executáveis, use **Logs de Aplicativos e Serviços** > **Microsoft** > **Windows** > **Integridade do Código** > **Operacional**.
2.    Para o bloqueio e a auditoria do Windows Installer e arquivos de script, use **Logs de Aplicativos e Serviços** > **Microsoft** > **Windows** > **AppLocker** > **MSI e Script**.

## <a name="security-and-privacy-information-for-device-guard"></a>Informações de segurança e privacidade para a Proteção do Dispositivo

- Nesta versão de pré-lançamento, não implante as políticas de Proteção do Dispositivo com o modo de imposição **Somente Auditoria** em um ambiente de produção. Esse modo destina-se a ajudá-lo a testar a funcionalidade em uma configuração de laboratório somente.
- Os dispositivos que têm uma política implantada para eles no modo **Somente Auditoria** ou dispositivos que têm uma política implantada para eles no modo **Imposição Habilitada**, que ainda não foram reiniciados para aplicar a política, são vulneráveis aos softwares não confiáveis sendo instalados.
Nesta situação, o software pode continuar tendo permissão para ser executado mesmo que o dispositivo reinicie ou recebe uma política no modo **Imposição Habilitada**.
- Para garantir que a política de Proteção do Dispositivo seja eficiente, prepare o dispositivo em um ambiente de laboratório, implante a política **Imposição Habilitada** e reinicie o dispositivo antes de concedê-lo a um usuário final.
- Não implante uma política com **Imposição Habilitada**, então, implante uma política com **Somente Auditoria** no mesmo dispositivo. Isso pode resultar em um software não confiável com permissão para ser executado.
- Quando você usa o Configuration Manager para habilitar a integridade do código configurável nos PCs cliente com políticas de Proteção do Dispositivo, a política **não** impede que os usuários com direitos de administrador local de evitem a política de Proteção do Dispositivo ou executem um software não confiável. 
- A única maneira de impedir que os usuários com direitos de administrador local desabilitem a integridade do código configurável é implantar uma política binária assinada, que é possível por meio da Política de Grupo, mas atualmente não tem suporte no Configuration Manager.
- A configuração do Configuration Manager como um Instalador Gerenciado nos PCs clientes usa a política AppLocker. AppLocker somente é usada para identificar os Instaladores Gerenciados a toda a imposição acontece com a integridade de código configurável. 





