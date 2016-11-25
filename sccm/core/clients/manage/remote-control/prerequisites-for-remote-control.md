---
title: "Pré-requisitos para o controle remoto | System Center Configuration Manager"
description: "Conheça os pré-requisitos para o controle remoto no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5e15fc7359787b40ebd138fd79dd72081dd8fb36


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
 A tabela a seguir fornece informações sobre os sistemas operacionais com suporte para o visualizador de controle remoto. Para obter informações sobre sistemas operacionais cliente com suporte, consulte [Configurações com suporte para o System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

|Sistema operacional|Suporte ao visualizador|Mais informações|  
|----------------------|--------------------|----------------------|  
|Windows XP (32 bits)|Sim|Para executar o visualizador de controle remoto neste sistema operacional, primeiro baixe e instale a [Atualização de cliente de RDC (Conexão de Área de Trabalho Remota) 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) no Centro de Download da Microsoft.|  
|Windows XP (64 bits)|Não|Nenhuma informação adicional.|  
|Windows Vista (32 bits)|Sim|Para executar o visualizador de controle remoto neste sistema operacional, primeiro baixe e instale a [Atualização de cliente de RDC (Conexão de Área de Trabalho Remota) 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) no Centro de Download da Microsoft.|  
|Windows Vista (64 bits)|Sim|Para executar o visualizador de controle remoto neste sistema operacional, primeiro baixe e instale a [Atualização de cliente de RDC (Conexão de Área de Trabalho Remota) 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) no Centro de Download da Microsoft.|  
|Windows 7 (32 bits)|Sim|Nenhuma informação adicional.|  
|Windows 7 (64 bits)|Sim|Nenhuma informação adicional.|  
|Windows Server 2003 (32 bits)|Não|Nenhuma informação adicional.|  
|Windows Server 2003 (64 bits)|Não|Nenhuma informação adicional.|  
|Windows Server 2008 (32 bits)|Não|Nenhuma informação adicional.|  
|Windows Server 2008 (64 bits)|Não|Nenhuma informação adicional.|  
|Windows Server 2008 R2 (64 bits)|Sim|Nenhuma informação adicional.|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|O controle remoto deve ser habilitado para clientes|Por padrão, o controle remoto não está habilitado quando você instala o Configuration Manager. Para obter informações sobre como habilitar e configurar o controle remoto, consulte [Configurando o controle remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services deve estar instalada antes que seja possível executar relatórios para o controle remoto. Para obter mais informações, consulte [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Permissões de segurança para gerenciar o controle remoto|Para acessar recursos da coleção e iniciar uma sessão de controle remoto do console do Configuration Manager: permissão para **Controlar AMT**, **Ler**, **Ler Recurso** e **Controlar Remotamente** para o objeto **Coleção**.<br /><br /> A função de segurança **Operador de Ferramentas Remotas** inclui essas permissões necessárias para gerenciar o controle remoto no Configuration Manager.<br /><br /> Para mais informações, consulte [Configurar administração baseada em funções para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Além disso, é necessário adicionar usuários a quem você deseja conceder permissão para usar o controle remoto e a assistência remota à lista de modos de exibição permitidos do controle remoto usando a opção **Visualizadores autorizados do Controle Remoto e da Assistência Remota** nas configurações **Ferramentas Remotas** do cliente.|  



<!--HONumber=Nov16_HO1-->


