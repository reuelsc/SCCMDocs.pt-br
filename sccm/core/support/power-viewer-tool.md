---
title: Ferramenta Power Viewer
titleSuffix: Configuration Manager
description: Use a Ferramenta Power Viewer para exibir o status do recurso de gerenciamento de energia em um cliente do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 09b1cf553aaa5fd75dbf0f7500246263a9bed7a6
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500827"
---
# <a name="power-viewer-tool"></a>Ferramenta Power Viewer

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A ferramenta Power Viewer é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). Use-o para exibir o status do recurso de gerenciamento de energia em um cliente do Configuration Manager.

Execute o **PowerVwr.exe** como administrador. Quando a ferramenta inicializa, ela exibe os recursos de energia e as configurações de energia do computador local na guia **Configuração de Energia**. 

Para exibir os dados de gerenciamento de energia de um computador remoto:  

1. Vá para o menu **Arquivo** e clique em **Conectar**. 

2. Insira o nome do **Computador** e um **Nome de usuário** e **Senha** se necessário. 

Há três guias no Power Viewer:  

- **Configuração de Energia**: exiba as funcionalidades de energia e as configurações do computador de destino.  

- **Atividade Diária**: exiba os gráficos de atividade diária do cliente, que incluem as seguintes informações:  

    - **Computador ligado**: o status de energia do computador em um dia. O modo de suspensão é considerado como desligado.  

    - **Monitorar ligado**: status ligado ou desligado do monitor em um dia.  

    - **Usuário Ativo**: informações de atividade do usuário em um dia.  

- **Eventos de Energia**: exiba todos os eventos de energia diários. O cliente resume esses eventos à meia-noite. Esse resumo gera dados para o gráfico de atividade diária.  
