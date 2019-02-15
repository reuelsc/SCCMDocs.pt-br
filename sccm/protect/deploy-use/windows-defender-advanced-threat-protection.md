---
title: Proteção Avançada contra Ameaças do Windows Defender
titleSuffix: Configuration Manager
description: Saiba como gerenciar e monitorar a Proteção Avançada contra Ameaças do Windows Defender, um novo serviço que ajuda as empresas a responder a ataques avançados.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf48b4602245750071ad60e2f42cb9afa66c40aa
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123552"
---
# <a name="windows-defender-advanced-threat-protection"></a>Proteção Avançada contra Ameaças do Windows Defender

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Começando com a versão 1606 do Configuration Manager (branch atual), o Endpoint Protection pode ajudar a gerenciar e monitorar o [Windows Defender ATP (Proteção Avançada contra Ameaças)](http://aka.ms/technet-wdatp). O Windows Defender ATP ajuda as empresas a detectar, investigar e responder a ataques avançados em suas redes.  As políticas do Configuration Manager ou do Microsoft Intune podem ajudá-lo a carregar e monitorar o Windows 10, versão 1607 (build 14328) ou posterior gerenciado.

O Windows Defender ATP é um serviço na [Central de Segurança do Windows Defender](https://securitycenter.windows.com). Adicionando e implantando um arquivo de configuração de integração do cliente, o Configuration Manager pode monitorar o status da implantação e a integridade de agente do Windows Defender ATP. O Windows Defender ATP é compatível com computadores executando o cliente do Configuration Manager ou gerenciados pelo Microsoft Intune, mas computadores Intune híbridos gerenciados por MDM não são compatíveis.

 **Pré-requisitos**  

-   Assinatura do serviço online de Proteção Avançada contra Ameaças do Windows Defender  
-   Computadores clientes que executam o Windows 10, versão 1607 e posterior  
-   Os computadores clientes que executam a versão 1610 do Configuration Manager ou agente cliente posterior ou gerenciados pelo Microsoft Intune

## <a name="how-to-create-an-onboarding-configuration-file"></a>Como criar um arquivo de configuração de integração  

 1.  Faça logon no [serviço online da ATP do Windows Defender](https://securitycenter.windows.com/)   

 2.  Clique no item de menu **Gerenciamento de pontos de extremidade**.  

 3.  Selecione **System Center Configuration Manager (branch atual) versão 1606** e clique em **Baixar pacote**.  

 4.  Baixe o arquivo compactado (.zip) e extraia o conteúdo.

> [!IMPORTANT]
> O arquivo de configuração do Windows Defender ATP contém informações confidenciais que devem ser mantidas seguras.

## <a name="onboard-devices-for-windows-defender-atp"></a>Dispositivos integrados para a ATP do Windows Defender  

1. No console do Configuration Manager, navegue para **Ativos e Conformidade** > **Visão Geral** > **Endpoint Protection** > **Políticas do Windows Defender ATP** e clique em **Criar uma política do Windows Defender ATP**. O Assistente de Política da ATP do Windows Defender é aberto.  

2. Digite o **Nome** e a **Descrição** para a política da ATP do Windows Defender e selecione **Integração**. Clique em **Avançar**.  

3. **Procure** o arquivo de Configuração fornecido pelo locatário do serviço de nuvem da ATP do Windows Defender da sua organização. Clique em **Avançar**.  

4. Especifique os arquivos de exemplo que são coletados e compartilhados por meio dos dispositivos gerenciados para análise.  

   - **Nenhum**   

   - **Todos os tipos de arquivo**  

     Clique em **Avançar**.  

5. Examine o resumo e conclua o assistente.  

6. Agora você pode implantar a política da ATP do Windows Defender em computadores cliente gerenciados clicando em **Implantar**.  

## <a name="monitor-windows-defender-atp"></a>Monitorar a ATP do Windows Defender  

1.  No console do Configuration Manager, navegue para **Monitoramento** > **Visão Geral** > **Segurança** e clique em **Windows Defender ATP**.  

2.  Examine o painel da Proteção Avançada contra Ameaças do Windows Defender.  

    -   **Status da Implantação do Agente do Windows Defender** – O número e o percentual de computadores cliente gerenciados qualificados com a política da ATP do Windows Defender ativa e integrada  

    -   **Integridade do Agente do Windows Defender ATP** – Percentual de computadores cliente que relatam o status para o agente da ATP do Windows Defender  

        -   **Íntegro** – Funcionando corretamente  

        -   **Inativo** – Nenhum dado enviado ao serviço durante o período  

        -   **Estado do agente** – O serviço do sistema para o agente do Windows não está em execução  

        -   **Não integrado** ‑ A política foi aplicada, mas o agente não informou sua integração  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>Como criar e implantar um arquivo de configuração de remoção  

1.  Faça logon no [serviço online da ATP do Windows Defender](https://securitycenter.windows.com/)   

2.  Clique no item de menu **Gerenciamento de pontos de extremidade**.  

3.  Selecione **System Center Configuration Manager (branch atual) versão 1606** e clique em **Remoção de ponto de extremidade**.  

4.  Baixe o arquivo compactado (.zip) e extraia o conteúdo. Os arquivos de remoção são válidos por 30 dias.

5.  No console do Configuration Manager, navegue para **Ativos e Conformidade** > **Visão Geral** > **Endpoint Protection** > **Políticas do Windows Defender ATP** e clique em **Criar uma política do Windows Defender ATP**. O Assistente de Política da ATP do Windows Defender é aberto.  

6.  Digite o **Nome** e a **Descrição** para a política da ATP do Windows Defender e selecione **Remoção**. Clique em **Avançar**.  

7.  **Procure** o arquivo de Configuração fornecido pelo locatário do serviço de nuvem da ATP do Windows Defender da sua organização. Clique em **Avançar**.  

8.  Examine o resumo e conclua o assistente.  

9.  Agora você pode implantar a política da ATP do Windows Defender em computadores cliente gerenciados clicando em **Implantar**.  

> [!IMPORTANT]
> Os arquivos de configuração do Windows Defender ATP contém informações confidenciais que devem ser mantidas seguras.

[Proteção Avançada contra Ameaças do Windows Defender](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Solucionar problemas de integração da Proteção Avançada contra Ameaças do Windows Defender](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)
