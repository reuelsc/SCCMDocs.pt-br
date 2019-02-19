---
title: Atestado de integridade
titleSuffix: Configuration Manager
description: Saiba mais sobre a funcionalidade de Atestado de Integridade do Dispositivo visualizável no console do Configuration Manager.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 116c12d86c097222844e76dde877b674ca7498b9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127109"
---
# <a name="health-attestation-for-system-center-configuration-manager"></a>Atestado de integridade do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os administradores podem exibir o status do [Atestado de Integridade do Dispositivo do Windows 10](https://technet.microsoft.com/library/mt592023.aspx) no console do Configuration Manager.  O atestado de integridade do dispositivo permite que o administrador garanta que os computadores cliente tenham as seguintes configurações confiáveis de BIOS, TPM e software de inicialização habilitadas:  

-   Antimalware de início antecipado - o ELAM (Antimalware de início antecipado) protege seu computador quando ele é iniciado e antes da inicialização de drivers de terceiros. [Como ativar o ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker - a Criptografia de Unidade BitLocker do Windows é um software que permite a criptografia de todos os dados armazenados no volume do sistema operacional Windows.  [Como ativar o BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Inicialização segura - a Inicialização Segura é um padrão de segurança desenvolvido por membros do mercado de PCs para certificar-se de que seu PC seja iniciado usando apenas o software de confiança do fabricante do PC. [Saiba mais sobre a Inicialização Segura](https://technet.microsoft.com/library/hh824987.aspx)  
-   Integridade do código - a Integridade do Código é um recurso que melhora a segurança do sistema operacional validando a integridade de um driver ou arquivo do sistema sempre que ele é carregado na memória. [Saiba mais sobre a Integridade do Código](https://technet.microsoft.com/library/dd348642.aspx)  

Essa funcionalidade está disponível para recursos locais e computadores gerenciados pelo Configuration Manager e dispositivos móveis gerenciados com o Microsoft Intune. Os administradores podem especificar se o relatório é gerado pela infraestrutura local ou na nuvem. O monitoramento do atestado de integridade do dispositivo no local permite que o administrador monitore os computadores de cliente sem acesso à Internet.

## <a name="enable-health-attestation"></a>Habilitar atestado de integridade

 **Requisitos:**  

-   Dispositivos clientes que executam o Windows 10 versão 1607 ou o Windows Server 2016 versão 1607 com o [Atestado de Integridade do Dispositivo habilitado](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation).
-   Dispositivos habilitados para TPM 1.2 ou TPM 2.
-   Ao usar o gerenciamento de nuvem, a comunicação entre o agente cliente do Configuration Manager e o ponto de gerenciamento com o serviço de Atestado de Integridade *has.spserv.microsoft.com* (porta 443) (gerenciamento de nuvem). Quando local, o cliente deve ser capaz de comunicar-se com o ponto de gerenciamento habilitado para Atestado de Integridade do Dispositivo.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Como habilitar a comunicação do serviço de Atestado de Integridade em computadores cliente do Configuration Manager

Use este procedimento para habilitar o monitoramento do atestado de integridade do dispositivo para dispositivos que se conectam à Internet.

1.  No console do Configuration Manager, escolha **Administração** > **Visão Geral** > **Configurações do Cliente**.  Selecione a guia de configurações do **Agente de Computador** .  
2.  Na caixa de diálogo **Configurações Padrão** , selecione **Agente de Computador** e role a tela para baixo até **Habilitar comunicação com o Serviço de Atestado de Integridade**  
3.  Defina **Habilitar comunicação com o Serviço de Atestado de Integridade** como **Sim**e clique em **OK**.  
4. Direcione para as coleções de dispositivos que devem relatar a integridade do dispositivo.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Como habilitar a comunicação local do serviço de Atestado de Integridade em computadores cliente do Configuration Manager
Use este procedimento para habilitar o monitoramento do atestado de integridade do dispositivo para dispositivos locais que não se conectam à Internet.

A partir do Configuration Manager 1702, a URL do serviço de atestado de integridade do dispositivo no local pode ser configurada no ponto de gerenciamento para oferecer suporte a dispositivos de cliente sem acesso à Internet.

1. No console do Configuration Manager, navegue até **Administração** > **Visão Geral** > **Configuração de Site** > **Sites**.
2. Clique com o botão direito no site primário ou secundário com o ponto de gerenciamento que oferece suporte a clientes de atestado de integridade do dispositivo no local e selecione **Configurar componentes do site** > **Ponto de Gerenciamento**. A página **Propriedades de componente do ponto de gerenciamento** é aberta.
3. Na guia **Opções Avançadas**, selecione **Adicionar** e especifique uma URL válida de serviço de atestado de integridade do dispositivo no local. Você pode adicionar várias URLs. Se forem especificadas várias URLs no local, os clientes receberão o conjunto completo e escolherão qual usar aleatoriamente.
4.  No console do Configuration Manager, escolha **Administração** > **Visão Geral** > **Configurações do Cliente**.  Selecione a guia de configurações do **Agente de Computador** .  
5.  Role para baixo até **Habilitar a comunicação com o serviço de atestado de integridade** e definido como **Sim**.
7.  Clique na opção **Usar serviço de Atestado de Integridade local** e defina-a como **Sim**.
8. Direcione para as coleções de dispositivos que devem relatar a integridade do dispositivo com as configurações de agente do cliente para habilitar o relatório de atestado de integridade do dispositivo.

Você também pode **Editar** ou **Remover** as URLs de serviço de atestado de integridade do dispositivo.

> [!NOTE]
> Se você usou o atestado de integridade do dispositivo antes de atualizar para o Configuration Manager 1702, as URLs no local especificadas nas configurações de agente do cliente são preenchidas previamente nas propriedades do ponto de gerenciamento durante a atualização. Os clientes no local continuarão a usar a URL especificada nas configurações do agente do cliente até que sejam atualizados. Eles mudarão para uma das URLs especificadas no ponto de gerenciamento.

## <a name="monitor-device-health-attestation"></a>Monitorar o atestado de integridade do dispositivo

1.  Para ver a exibição do atestado de integridade do dispositivo no console do Configuration Manager, acesse o workspace **Monitoramento**, clique no nó **Segurança** e clique em **Atestado de Integridade**.  
2.  O Atestado de Integridade do dispositivo é exibido  

O Atestado de Integridade do Dispositivo do Configuration Manager exibe o seguinte:  

-   **Status do Atestado de Integridade** – mostra a proporção de dispositivos nos estados de conformidade, não conformidade, erro e desconhecido  
-   **Dispositivos reportando Atestado de Integridade** – mostra o percentual de dispositivos que informam um status do Atestado de Integridade  
-   **Dispositivos Não Compatíveis por Tipo de Cliente** – mostra a proporção de dispositivos móveis e computadores não compatíveis  
-   **Principais Configurações de Atestado de Integridade Ausentes** – mostra o número de dispositivos que não apresentam a configuração de atestado de integridade, listados por configuração

O status do Atestado de Integridade do Dispositivo cliente pode ser usado para definir regras de acesso condicional nas políticas de conformidade para dispositivos gerenciados pelo Configuration Manager com o Microsoft Intune. Para obter detalhes, confira [Gerenciar políticas de conformidade do dispositivo no System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  
