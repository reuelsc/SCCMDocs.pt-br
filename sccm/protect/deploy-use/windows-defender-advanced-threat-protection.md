---
title: "Proteção Avançada contra Ameaças do Windows Defender | System Center Configuration Manager"
description: "Saiba como gerenciar e monitorar a Proteção Avançada contra Ameaças do Windows Defender, um novo serviço que ajuda as empresas a responder a ataques avançados."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: a4ad2d93ecd994fff00dab33084a734252cac651

---
# <a name="windows-defender-advanced-threat-protection"></a>Proteção Avançada contra Ameaças do Windows Defender

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A partir da versão 1606 do Configuration Manager (ramificação atual), o Endpoint Protection pode ajudar a gerenciar e monitorar a ATP (Proteção Avançada contra Ameaças) do Windows Defender. A ATP do Windows Defender é um novo serviço que ajudará as empresas a detectar, investigar e responder a ataques avançados em suas redes.  Saiba mais sobre a [ATP do Windows Defender](http://aka.ms/technet-wdatp). Políticas do Configuration Manager podem ajudar a carregar e monitorar o Windows 10, versão 1607 (build 14328) ou posterior gerenciado.

O Windows Defender ATP é um serviço da [Central de Segurança do Windows](https://securitycenter.windows.com). Adicionando e implantando um arquivo de configuração de integração do cliente, o Configuration Manager pode monitorar o status da implantação e a integridade de agente do Windows Defender ATP. Somente há suporte para o Windows Defender ATP em computadores que executam o cliente do Configuration Manager. Não há suporte para o gerenciamento de dispositivo móvel local nem para computadores gerenciados por MDM híbrido com Intune.

 **Pré-requisitos**  

-   Assinatura do serviço online de Proteção Avançada contra Ameaças do Windows Defender  

-   Clientes que executam o Windows 10, versão 1607 e posterior  

## <a name="how-to-create-an-onboarding-configuration-file"></a>Como criar um arquivo de configuração de integração  

 1.  Faça logon no [serviço online da ATP do Windows Defender](https://securitycenter.windows.com/)   

 2.  Clique no item de menu **Integração de Cliente**.  

 3.  Selecione **System Center Configuration Manager** e clique em **Baixar pacote**.  

 4.  Baixe o arquivo compactado (.zip) e extraia o conteúdo.

> [!IMPORTANT]
> O arquivo de configuração do Windows Defender ATP contém informações confidenciais que devem ser mantidas seguras.

## <a name="onboard-devices-for-windows-defender-atp"></a>Dispositivos integrados para a ATP do Windows Defender  

1.  No console do Configuration Manager, navegue para **Ativos e Conformidade** > **Visão Geral** > **Endpoint Protection** > **Políticas do Windows Defender ATP** e clique em **Criar uma política do Windows Defender ATP**. O Assistente de Política da ATP do Windows Defender é aberto.  

2.  Digite o **Nome** e a **Descrição** para a política da ATP do Windows Defender e selecione **Integração**. Clique em **Avançar**.  

3.  **Procure** o arquivo de Configuração fornecido pelo locatário do serviço de nuvem da ATP do Windows Defender da sua organização. Clique em **Avançar**.  

4.  Especifique os arquivos de exemplo que são coletados e compartilhados por meio dos dispositivos gerenciados para análise.  

    -   **Nenhum**   

    -   **Todos os tipos de arquivo**  

     Clique em **Avançar**.  

5.  Examine o resumo e conclua o assistente.  

6.  Agora você pode implantar a política da ATP do Windows Defender em computadores cliente gerenciados clicando em **Implantar**.  

## <a name="monitor-windows-defender-atp"></a>Monitorar a ATP do Windows Defender  

1.  No console do Configuration Manager, navegue para **Monitoramento** > **Visão Geral** > **Segurança** e clique em **Windows Defender ATP**.  

2.  Examine o painel da Proteção Avançada contra Ameaças do Windows Defender.  

    -   **Status da Implantação do Agente do Windows Defender** – O número e o percentual de computadores cliente gerenciados qualificados com a política da ATP do Windows Defender ativa e integrada  

    -   **Integridade do Agente do Windows Defender ATP** – Percentual de computadores cliente que relatam o status para o agente da ATP do Windows Defender  

        -   **Íntegro** – Funcionando corretamente  

        -   **Inativo** – Nenhum dado enviado ao serviço durante o período  

        -   **Estado do agente** – O serviço do sistema para o agente do Windows não está em execução  

        -   **Não integrado** ‑ A política foi aplicada, mas o agente não informou sua integração  



<!--HONumber=Nov16_HO1-->


