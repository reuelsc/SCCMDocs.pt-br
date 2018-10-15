---
title: Como gerenciar a Proteção de Dispositivo do Windows
titleSuffix: Configuration Manager
description: Saiba como usar o System Center Configuration Manager para gerenciar a Proteção de Dispositivo do Windows.
ms.date: 12/19/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2ccc918bf5f15798c201ed491dd3824bb20b2ebb
ms.sourcegitcommit: 3dfe3f4401651afa9dc65d14a8944ae4e4198b3e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48862559"
---
# <a name="device-guard-management-with-configuration-manager"></a>Gerenciamento de Proteção do Dispositivo com Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

## <a name="introduction"></a>Introdução
Device Guard é um grupo de recursos do Windows 10 projetado para proteger computadores contra malware e outros softwares não confiáveis. Ele impede que um código mal-intencionado seja executado, garantindo que somente o código aprovado, que você conhece, possa ser executado.

O Device Guard abrange o software e o hardware com base na funcionalidade de segurança. O Controle de Aplicativos do Windows Defender é uma camada de segurança baseada em software que impõe uma lista explícita de software que pode ser executado em um PC. Por si só, o Controle de Aplicativos não tem todos os pré-requisitos de hardware ou firmware. As políticas de Controle de Aplicativos implantadas com o Configuration Manager permitem aplicar uma política nos computadores, em coleções de destino que atendem aos requisitos mínimos de SKU e de versão do Windows descritos neste artigo. Opcionalmente, a proteção baseada em hipervisor das políticas de Controle de Aplicativos implantadas por meio do Configuration Manager pode ser ativada por meio da Diretiva de Grupo em hardware com capacidade.

Para saber mais sobre Device Guard, leia [Guia de implantação do Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

   > [!NOTE]
   > A partir do Windows 10, versão 1709, as políticas de integridade de código configuráveis ​​são conhecidas como Controle de Aplicativos do Windows Defender.

## <a name="using-device-guard-with-configuration-manager"></a>Usar o Device Guard com o Configuration Manager

Você pode usar o Configuration Manager para implantar uma política do Controle de Aplicativos do Windows Defender. Essa política permite configurar o modo no qual o Device Guard é executado em computadores em uma coleção. 

É possível configurar um dos seguintes modos:

1.  **Imposição habilitada** - somente os executáveis confiáveis podem ser executados.
2.  **Somente auditoria** - permite que todos os executáveis sejam rodados, mas registra os executáveis não confiáveis rodados no log de eventos do cliente local.

>[!TIP]
>Nesta versão do Configuration Manager, a Proteção do Dispositivo é um recurso de pré-lançamento. Para habilitá-lo, veja [Recursos de pré-lançamento no System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>O que poderá ser executado após a implantação de uma política do Controle de Aplicativos do Windows Defender?

A Proteção do dispositivo do Windows permite controlar fortemente o que pode ser executado nos PCs gerenciados. Esse recurso pode ser útil para PCs em departamentos de alta segurança, onde é vital que os softwares indesejados não possam ser executados.

Quando você implanta uma política, normalmente, os executáveis a seguir podem ser executados:

- componentes do sistema operacional Windows
- drivers do Centro de Desenvolvimento de Hardware (que têm as assinaturas do Windows Hardware Quality Labs)
- aplicativos da Windows Store
- cliente do Configuration Manager 
- Todos os softwares implantados por meio do Configuration Manager que os computadores instalarem depois que a política do Controle de Aplicativos do Windows Defender for processada. 
- Atualizações para componentes do Windows do:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Gerenciador de Configurações
    - Opcionalmente, softwares que tenham uma boa reputação de acordo com a determinação do ISG (Gráfico de Segurança Inteligente da Microsoft). O ISG inclui o Windows Defender SmartScreen e outros serviços da Microsoft. Os dispositivos precisam estar executando o Windows Defender SmartScreen e o Windows 10 versão 1709 ou superior para que esse software seja considerado confiável.

>[!IMPORTANT]
>Esses itens não incluem nenhum software que *não* seja integrado ao Windows, que seja atualizado automaticamente pela Internet ou atualizações de software de terceiros, com instalação via qualquer mecanismo de atualização mencionado anteriormente ou a partir da Internet. Somente as alterações de software implantadas pelo cliente do Configuration Manager poderão ser executadas.

## <a name="before-you-start"></a>Antes de começar

Antes de configurar ou implantar políticas de Controle de Aplicativos do Windows Defender, leia as seguintes informações:

- o Gerenciamento da Proteção do Dispositivo é um recurso de pré-lançamento do Configuration Manager e está sujeito a alterações.
- Para usar o Device Guard com o Configuration Manager, os PCs gerenciados devem ter o Windows 10 Enterprise versão 1703 ou posterior.
- Depois que uma política é processada com êxito em um computador cliente, o Configuration Manager é configurado como um Instalador Gerenciado nesse cliente. O software implantado por meio dele, após os processos de política, é automaticamente confiável. O software instalado pelo Configuration Manager antes dos processos de política do Controle de Aplicativos do Windows Defender não é automaticamente confiável.
- Os computadores clientes precisam ter conectividade com o controlador de domínio para que uma política do Controle de Aplicativos do Windows Defender seja processada com êxito.
- O agendamento da avaliação de conformidade padrão das políticas do Controle de Aplicativos que pode ser configurado durante a implantação, é diário. Se forem observados problemas no processamento da política, pode ser benéfico configurar o agendamento de avaliação de conformidade para que seja mais curto, por exemplo, a cada uma hora. Esse agendamento determina a frequência em que os clientes tentarão processar novamente uma política do Controle de Aplicativos do Windows Defender se houver falha.
- Independentemente do modo de imposição selecionado, quando uma política do Controle Aplicativos do Windows Defender está implantada, os computadores clientes não podem executar aplicativos HTML com a extensão .hta.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Como criar uma política do Controle de Aplicativos do Windows Defender
1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.
2.  No espaço de trabalho **Ativos e Conformidade**, expanda **Endpoint Protection** e clique em **Controle de Aplicativos do Windows Defender**.
3.  Na guia **Início**, no grupo **Criar**, clique em **Criar Política de Controle de Aplicativo**.
4.  Na página **Geral** do **Assistente para Criar Política de Controle de Aplicativo**, especifique estas configurações:
    - **Nome** – Insira um nome exclusivo para esta política do Controle de Aplicativos do Windows Defender. 
    - **Descrição** – opcionalmente, insira uma descrição da política que ajude a identificá-la no console do Configuration Manager.
    - **Imponha a reinicialização de dispositivos para que essa política possa ser aplicada a todos os processos** - Depois que a política for processada em um computador cliente, uma reinicialização será agendada no cliente de acordo com as **Configurações do Cliente** para **Reinicialização do Computador**.
        - Os dispositivos que executam o Windows 10 versão 1703 ou anterior sempre são reiniciados automaticamente.
        - A partir do Windows 10 versão 1709, os aplicativos atualmente em execução no dispositivo não terão a nova política de Controle de Aplicativos aplicada a eles até depois de uma reinicialização. No entanto, os aplicativos iniciados após a aplicação da política honrarão a nova política de Controle de Aplicativos. 
    - **Modo de imposição** -escolha um dos seguintes métodos de imposição para a Proteção do Dispositivo no PC cliente.
        - **Imposição habilitada** - permitir somente os executáveis confiáveis podem ser executados.
        - **Somente auditoria** - permite que todos os executáveis sejam rodados, mas registra os executáveis não confiáveis rodados no log de eventos do cliente local.
5.  Na guia **Inclusões** do assistente **Criar política de controle de aplicativo**, selecione se deseja **Autorizar software de confiança do Intelligent Security Graph**.
6. Clique em **Adicionar** se quiser adicionar confiança para arquivos ou pastas específicos em computadores. Na caixa de diálogo **Adicionar arquivo ou pasta confiável**, você pode especificar um arquivo local ou um caminho de pasta a confiar. Você também pode especificar um caminho de arquivo ou pasta em um dispositivo remoto no qual você tem permissão para se conectar. Ao adicionar uma relação de confiança para arquivos ou pastas específicas em uma política do Controle de Aplicativos do Windows Defender, você pode:
    - Solucione problemas de comportamentos do instalador gerenciado
    - Confie em aplicativos de linha de negócios que não podem ser implantados com o Configuration Manager
    - Confie em aplicativos que estão incluídos em uma imagem de implantação de sistema operacional. 
8.  Clique em **Avançar** para concluir o assistente.

>[!IMPORTANT]
>Só há suporte para a inclusão de arquivos confiáveis ou pastas em computadores cliente executando a versão 1706 ou mais recente do cliente do Configuration Manager. Se alguma regra de inclusão for incluída em uma política do Controle de Aplicativos do Windows Defender e a política for implantada em um computador cliente que esteja executando uma versão anterior no cliente do Configuration Manager, a política não será aplicada. A atualização desses clientes mais antigos resolverá o problema. As políticas que não incluem todas as regras de inclusão ainda podem ser aplicadas em versões anteriores do cliente do Configuration Manager.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Como implantar uma política do Controle de Aplicativos do Windows Defender
1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.
2.  No espaço de trabalho **Ativos e Conformidade**, expanda **Endpoint Protection** e clique em **Controle de Aplicativos do Windows Defender**.
3.  Na lista de políticas, selecione a que você deseja implantar e na guia **Início**, no grupo **Implantação**, clique em **Implantar Política de Controle de Aplicativos**.
4.  Na caixa de diálogo **Implantar política do Controle de Aplicativos**, selecione a coleção na qual deseja implantar a política. Em seguida, configure um agendamento para quando os clientes avaliarem a política. Por fim, selecione se o cliente pode avaliar a política fora de qualquer janela de manutenção configurada.
5.  Quando tiver terminado, clique em **OK** para implantar a política. 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Como monitorar uma política do Controle de Aplicativos do Windows Defender

Use as informações no artigo [Monitorar configurações de conformidade](/sccm/compliance/deploy-use/monitor-compliance-settings) para ajudá-lo a monitorar se a política implantada foi aplicada corretamente a todos os computadores.

Para monitorar o processamento de uma política do Controle de Aplicativos do Windows Defender, use o seguinte arquivo de log nos computadores clientes:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Para verificar o software específico sendo bloqueado ou auditado, confira os seguintes logs de eventos do cliente local:

1.  Para o bloqueio e a auditoria dos arquivos executáveis, use **Logs de Aplicativos e Serviços** > **Microsoft** > **Windows** > **Integridade do Código** > **Operacional**.
2.  Para o bloqueio e a auditoria do Windows Installer e arquivos de script, use **Logs de Aplicativos e Serviços** > **Microsoft** > **Windows** > **AppLocker** > **MSI e Script**.

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](https://docs.microsoft.com/windows/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-device-guard"></a>Informações de segurança e privacidade para a Proteção do Dispositivo

- Nesta versão de pré-lançamento, não implante políticas do Controle de Aplicativos do Windows Defender com o modo de imposição **Somente Auditoria** em um ambiente de produção. Esse modo destina-se a ajudá-lo a testar a funcionalidade em uma configuração de laboratório somente.
- Os dispositivos que têm uma política implantada no modo **Somente Auditoria** ou **Imposição Habilitada**, que não foram reiniciados para aplicar a política, ficarão vulneráveis à instalação de softwares não confiáveis.
Nesta situação, o software pode continuar tendo permissão para ser executado mesmo que o dispositivo reinicie ou recebe uma política no modo **Imposição Habilitada**.
- Para garantir que a política do Controle de Aplicativos do Windows Defender seja efetiva, prepare o dispositivo em um ambiente de laboratório. Em seguida, implante a política **Imposição Habilitada** e, finalmente, reinicie o dispositivo antes de conceder o dispositivo a um usuário final.
- Não implante uma política com **Imposição Habilitada**, então, implante uma política com **Somente Auditoria** no mesmo dispositivo. Essa configuração pode resultar em um software não confiável com permissão para ser executado.
- Quando você usa o Configuration Manager para habilitar o Controle de Aplicativos do Windows Defender em computadores cliente, a política não impede que os usuários com direitos de administrador local desviem das políticas do Controle de Aplicativos ou executem um software não confiável. 
- A única maneira de impedir que os usuários com direitos de administrador local desabilitem o Controle de Aplicativos é implantar uma política binária assinada. Essa implantação é possível por meio da Política de Grupo, mas não tem suporte no momento no Configuration Manager.
- A configuração do Configuration Manager como um Instalador Gerenciado nos PCs clientes usa a política AppLocker. A AppLocker é usada somente para identificar os Instaladores Gerenciados e toda a imposição acontece com o Controle de Aplicativo do Windows Defender. 




