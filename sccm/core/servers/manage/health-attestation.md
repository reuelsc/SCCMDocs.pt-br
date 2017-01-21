---
title: Atestado de integridade | Microsoft Docs
description: "Saiba mais sobre a funcionalidade de Atestado de Integridade do Dispositivo visualizável no console do Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: 17
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 937a168f79168b3e3a3a578513814abb2b368d9f


---
# <a name="health-attestation-for-system-center-configuration-manager"></a>Atestado de integridade do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A partir do branch atual o System Center Configuration Manager versão 1602, os administradores podem ver o status do [Atestado de Integridade de Dispositivo do Windows 10](https://technet.microsoft.com/library/mt592023.aspx) no console do Configuration Manager.  Essa funcionalidade está disponível para recursos locais e computadores gerenciados pelo Configuration Manager e dispositivos móveis gerenciados com o Microsoft Intune. Os administradores podem especificar se o relatório é gerado pela infraestrutura local ou na nuvem. Isso permite que PCs cliente sem acesso à Internet habilitem e monitorem dispositivos usando o atestado de integridade. O atestado de integridade do dispositivo permite que o administrador garanta que os computadores cliente tenham as seguintes configurações confiáveis de BIOS, TPM e software de inicialização habilitadas:  

-   Antimalware de início antecipado - o ELAM (Antimalware de início antecipado) protege seu computador quando ele é iniciado e antes da inicialização de drivers de terceiros. [Como ativar o ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  

-   BitLocker - a Criptografia de Unidade BitLocker do Windows é um software que permite a criptografia de todos os dados armazenados no volume do sistema operacional Windows.  [Como ativar o Bitlocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  

-   Inicialização segura - a Inicialização Segura é um padrão de segurança desenvolvido por membros do mercado de PCs para certificar-se de que seu PC seja iniciado usando apenas o software de confiança do fabricante do PC. [Saiba mais sobre a Inicialização Segura](https://technet.microsoft.com/library/hh824987.aspx)  

-   Integridade do código - a Integridade do Código é um recurso que melhora a segurança do sistema operacional validando a integridade de um driver ou arquivo do sistema sempre que ele é carregado na memória. [Saiba mais sobre a Integridade do Código](https://technet.microsoft.com/library/dd348642.aspx)  



##  <a name="device-health-attestation"></a>Atestado de integridade do dispositivo  
 O Atestado de Integridade do Dispositivo do Configuration Manager exibe o seguinte:  

-   **Status do Atestado de Integridade** – mostra a proporção de dispositivos nos estados de conformidade, não conformidade, erro e desconhecido  

-   **Dispositivos reportando Atestado de Integridade** – mostra o percentual de dispositivos que informam um status do Atestado de Integridade  

-   **Dispositivos Não Compatíveis por Tipo de Cliente** – mostra a proporção de dispositivos móveis e computadores não compatíveis  

-   **Principais Configurações de Atestado de Integridade Ausentes** – mostra o número de dispositivos que não apresentam a configuração de atestado de integridade, listados por configuração  

 **Requisitos:**  

-   Dispositivos cliente executando o Win10  

-   Windows Server 2016 Technical Preview 5 com [Atestado de Integridade do Dispositivo habilitado](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)

-    TPM 2 habilitada  

-   Desbloquear a comunicação entre o agente cliente do Configuration Manager e o serviço de Atestado de Integridade em has.spserv.microsoft.com (porta 443)

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Como habilitar a comunicação do serviço de Atestado de Integridade em computadores cliente do Configuration Manager  

1.  No console do Configuration Manager, escolha **Administração** > **Visão Geral** > **Configurações do Cliente**.  Selecione a guia de configurações do **Agente de Computador** .  

2.  Na caixa de diálogo **Configurações Padrão** , selecione **Agente de Computador** e role a tela para baixo até **Habilitar comunicação com o Serviço de Atestado de Integridade**  

3.  Defina **Habilitar comunicação com o Serviço de Atestado de Integridade** como **Sim**e clique em **OK**.  

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Como habilitar a comunicação local do serviço de Atestado de Integridade em computadores cliente do Configuration Manager


1. No console do Configuration Manager, navegue para **Administração** > **Visão Geral** > **Configurações do cliente**e defina **Usar Serviço de Atestado de Integridade local** como **Sim**.


2. Especifique a **URL do Serviço de Atestado de Integridade local**e clique em **OK**.

## <a name="how-to-view-health-attestation"></a>Como exibir o Atestado de Integridade  


1.  Para ver a exibição do atestado de integridade do dispositivo no console do Configuration Manager, acesse o espaço de trabalho **Monitoramento** , clique no nó **Segurança** e clique em **Atestado de Integridade**.  

2.  O Atestado de Integridade do dispositivo é exibido  

 O status do Atestado de Integridade do dispositivo cliente pode ser usado para definir regras de acesso condicional nas políticas de conformidade para dispositivos gerenciados pelo Configuration Manager com o Microsoft Intune. Para obter detalhes, confira [Gerenciar políticas de conformidade do dispositivo no System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  



<!--HONumber=Dec16_HO3-->


