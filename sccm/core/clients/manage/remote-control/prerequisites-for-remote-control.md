---
title: "Pré-requisitos de controle remoto | Microsoft Docs"
description: "Conheça os pré-requisitos para o controle remoto no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 12c602ddfa237768af497324440091e17e597ae9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-remote-control-in-system-center-configuration-manager"></a>Pré-requisitos para o controle remoto no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O controle remoto no System Center Configuration Manager tem dependências externas e dependências dentro do produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Driver de placa de vídeo do computador|Verifique se o driver de vídeo mais recente está instalado nos computadores cliente para garantir o desempenho ideal do controle remoto.|  

 Dispositivos que executam o Windows Embedded, Windows Embedded for Point of Service (POS) e Windows Fundamentals for Legacy PCs não dão suporte ao visualizador do controle remoto, mas dão suporte ao cliente do controle remoto.  

 O controle remoto do Configuration Manager não pode ser usado para administrar remotamente os computadores cliente que executam o Servidor de Gerenciamento do Sistema 2003 ou o Configuration Manager 2007.  

> [!NOTE]  
>  Nenhum serviço do Windows é necessário como uma dependência externa para o controle remoto.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Sistemas operacionais com suporte para o visualizador de controle remoto  
O visualizador de controle remoto tem suporte em todos os sistemas operacionais compatíveis com o console do Configuration Manager. Para saber mais, confira [Configurações com suporte para consoles do System Center Configuration Manager](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|O controle remoto deve ser habilitado para clientes|Por padrão, o controle remoto não está habilitado quando você instala o Configuration Manager. Para obter informações sobre como habilitar e configurar o controle remoto, consulte [Configurando o controle remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services deve estar instalada antes que seja possível executar relatórios para o controle remoto. Para obter mais informações, consulte [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Permissões de segurança para gerenciar o controle remoto|Para acessar recursos da coleção e iniciar uma sessão de controle remoto do console do Configuration Manager: permissão para **Ler**, **Ler Recurso** e **Controlar Remotamente** para o objeto **Coleção**.<br /><br /> A função de segurança **Operador de Ferramentas Remotas** inclui essas permissões necessárias para gerenciar o controle remoto no Configuration Manager.<br /><br /> Para mais informações, consulte [Configurar administração baseada em funções para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Além disso, os visualizadores autorizados devem receber a permissão para usar o controle remoto por meio da adição desses usuários à lista **Visualizadores permitidos de Controle Remoto e Assistência Remota** nas configurações do cliente das **Ferramentas Remotas**.
