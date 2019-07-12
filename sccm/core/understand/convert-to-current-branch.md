---
title: 'Atualizar a ramificação de manutenção de longo prazo para a ramificação atual '
titleSuffix: Configuration Manager
description: Saiba como converter um site do Branch de Manutenção em Longo Prazo em um site do Branch Atual.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 20b50fcd54513ccd780a7da173766fb177bf5da7
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676122"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Atualizar a ramificação de manutenção de longo prazo para a ramificação atual

*Aplica-se a: System Center Configuration Manager (branch de manutenção em longo prazo)*

Use este tópico para saber como atualizar (converter) um site e uma hierarquia que executa o LTSB (Branch de Manutenção em Longo Prazo) do Configuration Manager para o Branch Atual.

Quando você tiver um contrato do Software Assurance (ou direitos de licenciamento semelhantes) que concede a você direitos de uso do Branch Atual, será possível converter a sua instalação do LTSB no Branch Atual.  Essa é uma conversão unidirecional, pois não há suporte para converter um site da Ramificação Atual para LTSB.

Se você tiver vários sites, só precisará converter o site da camada superior da sua hierarquia. Depois que o site da camada superior for convertido:
- Os sites primários filho serão convertidos automaticamente.
- Será necessário atualizar manualmente os sites secundários de dentro do console do Configuration Manager.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Executar a configuração para converter a Ramificação de Manutenção de Longo Prazo
No site de camada superior da sua hierarquia, é possível executar a instalação do Configuration Manager na mídia de linha de base de qualificação e selecionar **Manutenção do site**.  Em seguida, quando a página de licenciamento aparecer, selecione a opção para a Ramificação Atual e conclua o assistente.

Quando o seu site for convertido para a Ramificação Atual, os recursos anteriormente indisponíveis estarão disponíveis para uso.

> [!NOTE]  
> A mídia de linha de base de qualificação é uma mídia que tem uma versão igual ou posterior à da sua instalação LTSB.

Por exemplo, como o LTSB se baseia na versão 1606, você não pode usar a mídia 1511 de linha de base para converter no Branch Atual. Em vez disso, execute a instalação com a mesma mídia de linha de base versão 1606 usada para instalar o site LTSB e escolha a opção de licenciamento para a Ramificação Atual.  Como alternativa, se uma linha de base mais recente da Ramificação Atual tiver sido lançada, é possível executar a instalação dessa mídia de linha de base.

Para ver uma lista de versões de linha de base, consulte **Versões de linha de base e atualização** em [Updates for Configuration Manager (Atualizações para o Configuration Manager)](/sccm/core/servers/manage/updates).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Usar o console do Configuration Manager para converter a ramificação de manutenção de longo prazo
Se seu site executar o LTSB, será possível usar a opção a seguir no console do Configuration Manager para converter no Branch Atual:

 1. No console, vá para **Administração** > **Configuração do Site** > **Sites** e abra **Configurações da Hierarquia**.  

 2. Em **Configurações da Hierarquia**, mude para a guia **Licenciamento**. Selecione a opção **Converter para o Branch Atual** e, em seguida, clique em **Aplicar**.  

Quando o seu site for convertido para a Ramificação Atual, os recursos anteriormente indisponíveis estarão disponíveis para uso.
