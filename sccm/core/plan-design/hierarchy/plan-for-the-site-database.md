---
title: Planejar o banco de dados do site | Microsoft Docs
description: "Considere o banco de dados do site e a função do servidor de banco de dados do site ao planejar sua hierarquia do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 012d5b313487640faeebe5b49064c74d41a7edb9


---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>Planejar o banco de dados do site para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O servidor de banco de dados do site é um computador que executa uma versão com suporte do Microsoft SQL Server que armazena informações para sites do Configuration Manager. Cada site em uma hierarquia do Configuration Manager contém um banco de dados e um servidor de site que são atribuídos à função de servidor de banco de dados do site.  

-   Para sites de administração central e sites primários, você pode instalar o SQL Server no servidor do site ou em um computador que não seja o servidor do site  

-   Para sites secundários, você pode usar o SQL Server Express em vez de uma instalação completa do SQL Server; no entanto, o servidor de banco de dados deve ser executado no servidor do site secundário.  

Se você usar um computador servidor remoto de banco de dados, certifique-se de que a conexão de rede é uma intervenção de alta disponibilidade e grande largura de banda. Isso ocorre porque o servidor do site e algumas funções do sistema de site devem se comunicar constantemente com o SQL Server que hospeda o banco de dados do site.  


**Ao selecionar um local do servidor de banco de dados remoto, considere o seguinte:**  

-   A quantidade de largura de banda necessária para a comunicação com o servidor de banco de dados depende de uma combinação de muitas configurações diferentes de site e cliente, portanto, a largura de banda real necessária não pode ser adequadamente prevista.  

-   Cada computador que executa o Provedor de SMS e que se conecta ao banco de dados do site aumenta os requisitos de largura de banda da rede.  

-   O computador que executa o SQL Server deve estar localizado em um domínio com uma relação de confiança bidirecional com o servidor do site e todos os computadores que executam o Provedor de SMS.  

-   Não é possível usar um SQL Server clusterizado para o servidor do banco de dados do site quando o banco de dados do site está colocalizado com o servidor do site.  


Geralmente, um servidor do sistema de sites dá suporte a funções de um único site do Configuration Manager; no entanto, você pode usar diferentes instâncias do SQL Server, em servidores clusterizados ou não, executando o SQL Server, para hospedar um banco de dados de diferentes sites do Configuration Manager. Para dar suporte a bancos de dados de diferentes sites, é necessário configurar cada instância do SQL Server para usar portas de comunicação exclusivas.  


**As seguintes configurações do SQL Server podem ser usadas para hospedar o banco de dados do site:**  

-   A instância padrão do SQL Server  

-   Uma instância nomeada em um único computador com o SQL Server  

-   Uma instância nomeada em uma instância clusterizada do SQL Server  

-   Um grupo de disponibilidade AlwaysOn do SQL Server (a partir da versão 1602)


**Pré-requisitos para o Banco de Dados do Site:**  

-   Para hospedar o banco de dados do site, o SQL Server deve atender aos requisitos detalhados na seção [Suporte a versões do SQL Server para o System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  



<!--HONumber=Dec16_HO3-->


