---
title: Sobre upgrade, atualização e instalação
titleSuffix: Configuration Manager
description: Aprenda a diferença entre os termos Instalação, Atualização e Upgrade ao gerenciar a infraestrutura do Configuration Manager.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 263ec638afa62cee4f8fce86a9f7b9e35b37f0bb
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676035"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Sobre upgrade, atualização e instalação para infraestrutura de site e hierarquia

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Ao gerenciar a infraestrutura do site e da hierarquia do System Center Configuration Manager, os termos *upgrade*, *atualização* e *instalação* são usados para descrever três conceitos separados.

## <a name="upgrade"></a>Atualização
O *upgrade*, ou *upgrade in-loco*, é usado ao converter seu site ou hierarquia do Configuration Manager 2012 em um que execute o System Center Configuration Manager.
Ao fazer o upgrade do System Center 2012 Configuration Manager para o System Center Configuration Manager, você continuar usando os mesmos servidores para hospedar seus sites e servidores de site e mantém seus dados e configurações existentes do Configuration Manager.  Isso é diferente de uma [Migração](/sccm/core/migration/migrate-data-between-hierarchies), que é uma maneira de manter suas configurações e dados sobre dispositivos gerenciados usando novos sites do System Center Configuration Manager instalados em um novo hardware.

Para saber mais detalhes, confira [Atualização para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).



## <a name="update"></a>Atualização
A *atualização* é usada para instalar atualizações no console do System Center Configuration Manager e para atualizações fora de banda, que são atualizações que não podem ser entregues de dentro do console do Configuration Manager. As atualizações no console podem modificar a versão de seu site de Branch Atual (ou site de Technical Preview) para execute uma versão posterior. Por exemplo, se o seu site executar a versão 1806, você poderá instalar uma atualização para a versão 1810. As atualizações também podem instalar correções para um problema conhecido sem modificar a versão do site.      

Normalmente, as atualizações adicionam novos recursos, melhorias de qualidade e correções de segurança à implantação existente. Se você usar a ramificação Technical Preview, uma atualização poderá instalar uma versão mais recente do Technical Preview.
- Escolha quando instalar a atualização no console, começando pelo site de nível superior de sua hierarquia.
- Você pode instalar qualquer atualização disponível no console. Por exemplo, se seu site executar a versão 1802, e as versões 1806 e 1810 forem oferecidas, considere a instalação da versão 1810, pois cada versão inclui os recursos disponibilizados nas versões anteriores.
- Após a conclusão da instalação de uma nova atualização em seu site de nível superior, os sites primários filhos começarão automaticamente o processo de atualização. No entanto, você pode configurar [Períodos de manutenção](/sccm/core/servers/manage/service-windows) para controlar o cronograma das atualizações.
- Os sites secundários não instalam automaticamente as atualizações. Em vez disso, inicie manualmente a atualização de dentro do console do Configuration Manager.

Para saber mais, confira [Atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates) e [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).



## <a name="install"></a>Instalar o
A *instalação* é usada ao criar uma nova hierarquia do Configuration Manager a partir do zero, ou para adicionar outros sites em uma hierarquia existente.  

Quando você instala um novo site primário ou site de administração central, o local do setup.exe e seus arquivos de origem relacionados que você usa depende do cenário de instalação.

Para saber mais, confira [Preparar a instalação de sites](/sccm/core/servers/deploy/install/prepare-to-install-sites).
