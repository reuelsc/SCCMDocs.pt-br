---
title: "Como gerenciar a Proteção de Dispositivo do Windows | Microsoft Docs"
description: "Saiba como usar o System Center Configuration Manager para gerenciar a Proteção de Dispositivo do Windows."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: "13"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3921748d3c99c2a35b670f3ca121dc7ab92d43bc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="device-guard-management-with-configuration-manager"></a>Gerenciamento de Proteção do Dispositivo com Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

## <a name="introduction"></a>Introdução
Device Guard é um grupo de recursos do Windows 10 projetado para proteger computadores contra malware e outros softwares não confiáveis. Ele impede que um código mal-intencionado seja executado, garantindo que somente o código aprovado, que você conhece, possa ser executado.

O Device Guard abrange o software e o hardware com base na funcionalidade de segurança. Integridade do código configurável é uma camada de segurança baseada em software que impõe uma lista explícita de software que pode ser executado em um PC. Por si só, a integridade do código configurável não tem todos os pré-requisitos de hardware ou firmware. As políticas do Device Guard implantadas com o Configuration Manager permitem uma política de integridade do código configurável nos PCs em coleções de destino que atendem aos requisitos mínimos de SKU e a versão do Windows descritos neste tópico. Opcionalmente, o hipervisor com base na proteção das políticas de integridade do código implantadas através do Configuration Manager pode ser habilitado com a Política de Grupo no hardware compatível.

Para saber mais sobre Device Guard, leia [Guia de implantação do Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

## <a name="using-device-guard-with-configuration-manager"></a>Usar o Device Guard com o Configuration Manager

Use o Configuration Manager para implantar uma política de Device Guard que permite configurar o modo de execução do Device Guard nos PCs em uma coleção. 

É possível configurar um dos seguintes modos:

1.  **Imposição habilitada** - somente os executáveis confiáveis podem ser executados.
2.  **Somente auditoria** - permite que todos os executáveis sejam rodados, mas registra os executáveis não confiáveis rodados no log de eventos do cliente local.

>[!TIP]
>Nesta versão do Configuration Manager, a Proteção do Dispositivo é um recurso de pré-lançamento. Para habilitá-lo, veja [Recursos de pré-lançamento no System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>O que pode ser executado quando você implanta uma política de Proteção do Dispositivo?

A Proteção do dispositivo do Windows permite controlar fortemente o que pode ser executado nos PCs gerenciados. Esse recurso pode ser útil para PCs em departamentos de alta segurança, onde é vital que os softwares indesejados não possam ser executados.

Quando você implanta uma política, normalmente, os executáveis a seguir podem ser executados:

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
>Esses itens não incluem nenhum software que *não* seja integrado ao Windows, que seja atualizado automaticamente pela Internet ou atualizações de software de terceiros, com instalação via qualquer mecanismo de atualização mencionado anteriormente ou a partir da Internet. Somente as alterações de software implantadas pelo cliente do Configuration Manager poderão ser executadas.

## <a name="before-you-start"></a>Antes de começar

Antes de configurar ou implantar as políticas de Proteção do Dispositivo, leia as seguintes informações:

- o Gerenciamento da Proteção do Dispositivo é um recurso de pré-lançamento do Configuration Manager e está sujeito a alterações.
- Para usar o Device Guard com o Configuration Manager, os PCs gerenciados devem ter o Windows 10 Enterprise versão 1703 ou posterior.
- Depois de uma política ser processada com êxito em um PC cliente, o Configuration Manager é configurado como um Instalador Gerenciado no cliente, e o software implantado por meio do SCCM após o processamento da política é automaticamente confiável. O software instalado pela Configuração Gerenciada antes do processamento da política de Device Guard não é automaticamente confiável.
- Os PCs cliente devem ter conectividade com o Controlador de Domínio para uma política de Proteção do Dispositivo ser processada com êxito.
- O agendamento de avaliação de conformidade padrão para as políticas de Proteção do Dispositivo, configuráveis durante a implantação, é a cada um dia. Se forem observados problemas no processamento da política, pode ser benéfico configurar o agendamento de avaliação de conformidade para que seja mais curto, por exemplo, a cada uma hora. Esse agendamento determina com que frequência os clientes tentarão processar novamente uma política de Device Guard em caso de falha.
- Independentemente do modo de imposição selecionado, quando você implanta uma política de Device Guard, os PCs cliente não poderão executar os aplicativos HTML com a extensão .hta.

## <a name="how-to-create-a-device-guard-policy"></a>Como criar uma política de Proteção do Dispositivo
1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.
2.  No espaço de trabalho **Ativos e Conformidade**, expanda **Proteção do Ponto de Extremidade**e clique em **Políticas de Proteção do Dispositivo**.
3.  Na guia **Início**, no grupo **Criar**, clique em **Criar Política de Proteção do Dispositivo**.
4.  Na página **Geral** do **Assistente para Criar Política de Device Guard**, especifique estas configurações:
    - **Nome** - insira um nome exclusivo para a política de Proteção do Dispositivo. 
    - **Descrição** – opcionalmente, insira uma descrição da política que ajude a identificá-la no console do Configuration Manager.
    - **Modo de imposição** -escolha um dos seguintes métodos de imposição para a Proteção do Dispositivo no PC cliente.
        - **Imposição habilitada** - permitir somente os executáveis confiáveis podem ser executados.
        - **Somente auditoria** - permite que todos os executáveis sejam rodados, mas registra os executáveis não confiáveis rodados no log de eventos do cliente local.
5.  Na guia **Inclusões** do **Assistente para Criar Política de Device Guard**, clique em **Adicionar** se quiser adicionar opcionalmente uma relação de confiança a arquivos ou pastas específicas nos computadores. 
6.  Na caixa de diálogo **Adicionar Arquivo ou Pasta Confiável**, especifique informações sobre o arquivo ou pasta na qual você deseja confiar. Você pode especificar um caminho de arquivo ou pasta local ou se conectar a um dispositivo remoto ao qual você tem permissão para se conectar, e especificar um caminho de arquivo ou pasta nesse dispositivo.
Quando você adiciona uma relação de confiança a arquivos específicos para pastas em uma política de Device Guard, é possível:
    - Solucione problemas de comportamentos do instalador gerenciado
    - Confie em aplicativos de linha de negócios que não podem ser implantados com o Configuration Manager
    - Confie em aplicativos que estão incluídos em uma imagem de implantação de sistema operacional. 
7.  Clique em **Avançar** e conclua o assistente.

>[!IMPORTANT]
>Só há suporte para a inclusão de arquivos confiáveis ou pastas em computadores cliente executando a versão 1706 ou mais recente do cliente do Configuration Manager. Se todas as regras de inclusão estiverem incluídas em uma política do Device Guard, e a política for implantada em um computador cliente executando uma versão anterior no cliente do Configuration Manager, a política não será aplicada. A atualização desses clientes mais antigos resolverá o problema. As políticas que não incluem todas as regras de inclusão ainda podem ser aplicadas em versões anteriores do cliente do Configuration Manager.

## <a name="how-to-deploy-a-device-guard-policy"></a>Como implantar uma política de Proteção do Dispositivo
1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.
2.  No espaço de trabalho **Ativos e Conformidade**, expanda **Proteção do Ponto de Extremidade**e clique em **Políticas de Proteção do Dispositivo**.
3.  Na lista de políticas, selecione a que você deseja implantar e na guia **Início**, no grupo **Implantação**, clique em **Implantar**.
4.  Na caixa de diálogo **Implantar Política de Device Guard**, selecione a coleção na qual você deseja implantar a política. Em seguida, configure um agendamento para quando os clientes avaliarem a política. Por fim, selecione se o cliente pode avaliar a política fora de qualquer janela de manutenção configurada.
5.  Quando tiver terminado, clique em **OK** para implantar a política. 

Depois que a política for processada em um PC cliente, uma reinicialização será agendada no cliente de acordo com as **Configurações do Cliente** para **Reinicialização do Computador**.
Até que você reinicie o PC cliente, a política não terá efeito.**

## <a name="how-to-monitor-a-device-guard-policy"></a>Como monitorar uma política de Proteção do Dispositivo

Use as informações no tópico [Monitorar configurações de conformidade](/sccm/compliance/deploy-use/monitor-compliance-settings) para ajudar você a monitorar se a política implantada foi aplicada corretamente a todos os PCs.

Para monitorar o processamento de uma política de Device Guard, use o seguinte arquivo de log em PCs cliente:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Para verificar o software específico sendo bloqueado ou auditado, confira os seguintes logs de eventos do cliente local:

1.  Para o bloqueio e a auditoria dos arquivos executáveis, use **Logs de Aplicativos e Serviços** > **Microsoft** > **Windows** > **Integridade do Código** > **Operacional**.
2.  Para o bloqueio e a auditoria do Windows Installer e arquivos de script, use **Logs de Aplicativos e Serviços** > **Microsoft** > **Windows** > **AppLocker** > **MSI e Script**.

## <a name="security-and-privacy-information-for-device-guard"></a>Informações de segurança e privacidade para a Proteção do Dispositivo

- Nesta versão de pré-lançamento, não implante as políticas de Proteção do Dispositivo com o modo de imposição **Somente Auditoria** em um ambiente de produção. Esse modo destina-se a ajudá-lo a testar a funcionalidade em uma configuração de laboratório somente.
- Os dispositivos que têm uma política implantada no modo **Somente Auditoria** ou **Imposição Habilitada**, que não foram reiniciados para aplicar a política, ficarão vulneráveis à instalação de softwares não confiáveis.
Nesta situação, o software pode continuar tendo permissão para ser executado mesmo que o dispositivo reinicie ou recebe uma política no modo **Imposição Habilitada**.
- Para garantir que a política de Device Guard seja eficaz, prepare o dispositivo em um ambiente de laboratório. Em seguida, implante a política **Imposição Habilitada** e, finalmente, reinicie o dispositivo antes de conceder o dispositivo a um usuário final.
- Não implante uma política com **Imposição Habilitada**, então, implante uma política com **Somente Auditoria** no mesmo dispositivo. Essa configuração pode resultar em um software não confiável com permissão para ser executado.
- Quando você usa o Configuration Manager para habilitar a integridade do código configurável nos PCs cliente com políticas de Proteção do Dispositivo, a política não impede que os usuários com direitos de administrador local de evitem a política de Proteção do Dispositivo ou executem um software não confiável. 
- A única maneira de impedir que os usuários com direitos de administrador local desabilitem a integridade do código configurável é implantar uma política binária assinada. Essa implantação é possível por meio da Política de Grupo, mas não tem suporte no momento no Configuration Manager.
- A configuração do Configuration Manager como um Instalador Gerenciado nos PCs clientes usa a política AppLocker. AppLocker somente é usada para identificar os Instaladores Gerenciados a toda a imposição acontece com a integridade de código configurável. 




