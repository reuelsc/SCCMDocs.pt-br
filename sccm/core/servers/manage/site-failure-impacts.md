---
title: Impactos de falha do site
titleSuffix: Configuration Manager
description: Compreenda os efeitos de várias falhas em um site do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eebd1aaf72cbd7932a919c0a8ffdef6d6af8389f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132009"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Impactos de falha do site no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O servidor do site e qualquer um dos outros sistemas de sites podem falhar e causar uma perda dos serviços que eles oferecem regularmente. Se você instalar diversos sistemas de sites no mesmo computador e esse computador falhar, todos os serviços fornecidos regularmente pelos sistemas de sites deixarão de estar disponíveis.

Parte do processo de planejamento deve incluir reconhecer o impacto sobre o serviço que você fornece à sua organização. Como cada sistema de sites incluído no site fornece uma funcionalidade diferente, o impacto de uma falha no site é diferente conforme a função do sistema de sites que falhou. 

Use [opções de alta disponibilidade](/sccm/core/servers/deploy/configure/high-availability-options) para ajudar a atenuar a falha de qualquer sistema individual. Também planeje e pratique uma estratégia de [backup e recuperação](/sccm/core/servers/manage/backup-and-recovery) para reduzir a quantidade de tempo em que o serviço não está disponível.

As seções a seguir descrevem o impacto quando o sistema de site especificado não está operacional:


### <a name="site-server"></a>Servidor do site

- Nenhuma administração de site é possível. Você não pode conectar o console ao site.  

- O ponto de gerenciamento coleta informações do cliente e as armazena em cache até que o servidor do site esteja online novamente.  

- Os usuários podem executar as implantações existentes e os clientes podem baixar o conteúdo dos pontos de distribuição.  


### <a name="site-database"></a>Banco de dados do site

- Nenhuma administração de site é possível.  

- Se o cliente do Configuration Manager já tiver uma atribuição de política com as novas políticas e se o ponto de gerenciamento tiver armazenado em cache o corpo da política, o cliente poderá fazer uma solicitação de corpo de política e receber a resposta do corpo de política. No entanto, o site não pode atender a nenhuma nova solicitação de atribuição de política.  

- Os clientes poderão executar implantações somente se já tiverem recebido a política e os arquivos de origem associados já estiverem em cache localmente no cliente.  


### <a name="management-point"></a>Ponto de gerenciamento

- Embora você possa criar novas implantações, os clientes não as receberão até que um ponto de gerenciamento esteja online.  

- Os clientes ainda coletam informações de inventário, medição de software e status. Eles armazenam dados localmente até que o ponto de gerenciamento esteja disponível.  

- Os clientes poderão executar implantações somente se já tiverem recebido a política e os arquivos de origem associados já estiverem em cache localmente no cliente.  


### <a name="distribution-point"></a>Ponto de distribuição

- Clientes do Configuration Manager poderão executar implantações somente se os arquivos de origem associados já tiverem sido baixados localmente ou estiverem disponíveis em uma fonte de par.

