---
title: Atualizar instalações de avaliação
titleSuffix: Configuration Manager
description: Saiba como atualizar uma instalação de avaliação para uma instalação completa do System Center Configuration Manager.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1b5e527fbed544447052556041db3de3c5b06ffd
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65497668"
---
# <a name="upgrade-an-evaluation-installation-of-system-center-configuration-manager-to-a-full-installation"></a>Atualizar uma instalação de avaliação para uma instalação completa do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Se você tiver instalado o System Center Configuration Manager como uma versão de avaliação, após 180 dias o console do Configuration Manager se tornará somente leitura até você ativar o produto na página **Manutenção do site** em Configurações. A qualquer momento antes ou depois do período de 180 dias, você tem a opção de atualizar para uma instalação de avaliação para uma instalação completa.  

> [!NOTE]  
>  Ao conectar um console do Configuration Manager a uma instalação de avaliação do Configuration Manager, a barra de título do console mostra o número de dias que restam antes de expirar a instalação de avaliação. O número de dias não é atualizado automaticamente; é atualizado somente quando você faz uma nova conexão a um site.  

 Você pode atualizar os seguintes sites que executam uma instalação de avaliação:  

-   Site de administração central  
-   Site primário  

Como os sites secundários não são tratados como instalações de avaliação, você não precisa modificar um site secundário depois que seu site pai primário é atualizado para uma instalação completa.  

Pré-requisitos para atualizar de uma versão de avaliação para uma versão licenciada:  

-   Você deve ter um produto válido a ser usado durante a atualização.  
-   Sua conta deve ter permissões de **administrador** para o computador no qual o site está instalado.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Para atualizar uma versão de avaliação do Configuration Manager para uma versão licenciada  

1.  No servidor de sites, localize **Setup.exe** (instalação do Configuration Manager) na pasta de instalação do Configuration Manager (**%caminho%\BIN\X64**). Você deve executar a cópia da instalação que está localizada no servidor do site na pasta do Configuration Manager, uma vez que não há opções de manutenção do site disponíveis quando você executa a instalação da mídia de instalação.  
2.  Na página **Antes de Começar** escolha **Avançar**.  
3.  Na página **Guia de introdução**, selecione **Realizar a manutenção do site ou redefinir o site** e clique em **Avançar**.  
4.  Na página **Manutenção do site**, selecione **Atualizar a edição de avaliação para uma edição licenciada**, insira uma chave do produto válida e clique em **Avançar**.  
5.  Na página **Termos de Licença de Software Microsoft**, leia e aceite os termos de licença e clique em **Avançar**.  
6.  Na página **Configuração**, clique em **Fechar** para concluir o assistente.  

    > [!NOTE]  
    >  A barra de título do console do Configuration Manager que permanece conectado ao site que está sendo atualizado pode indicar que o site ainda é uma versão de avaliação até que você reconecte o console ao site.  
