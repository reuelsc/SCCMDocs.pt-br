---
title: "Privacidade de segurança do inventário de hardware"
titleSuffix: Configuration Manager
description: "Obtenha as informações de segurança e privacidade do inventário de hardware no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62e20d86-db6d-4a1f-b14a-905a9de31698
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: d08bae2cceada5393e58bf8ad2e4a603277f5dfc
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="security-and-privacy-for-hardware-inventory-in-system-center-configuration-manager"></a>Segurança e privacidade do inventário de hardware no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém as informações de segurança e privacidade do inventário de hardware no System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Práticas recomendadas de segurança para o inventário de hardware  
 Use as seguintes práticas recomendadas de segurança quando coletar dados de inventário de hardware de clientes:  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Assinar e criptografar dados de inventário|Quando os clientes se comunicam com pontos de gerenciamento usando HTTPS, todos os dados que eles enviam são criptografados por meio do SSL. No entanto, quando os computadores cliente usam o HTTP para se comunicarem com pontos de gerenciamento na intranet, os dados de inventário do cliente e os arquivos coletados podem ser enviados sem assinatura e sem criptografia. Certifique-se de que o site está configurado para exigir assinatura e usar criptografia. Além disso, se os clientes podem suportar o algoritmo SHA-256, selecione a opção de exigir SHA-256.|  
|Não coletar arquivos IDMIF e NOIDMIF em ambientes de alta segurança|Você pode usar a coleção de arquivos IDMIF e NOIDMIF para estender o inventário de hardware. Quando necessário, o Configuration Manager cria novas tabelas ou modifica as tabelas existentes no banco de dados do Configuration Manager para acomodar as propriedades nos arquivos IDMIF e NOIDMIF. No entanto, o Configuration Manager não valida arquivos IDMIF e NOIDMIF, esses arquivos podem ser usado para alterar as tabelas que você deseja não alteradas. Dados válidos poderão ser substituídos pelos dados inválidos. Além disso, grandes volumes de dados pode ser adicionadas e o processamento desses dados pode causar atrasos em todas as funções do Configuration Manager. Para atenuar esses riscos, configure o cliente de inventário de hardware definindo a opção **Coletar arquivos MIF** como **Nenhum**.|  

### <a name="security-issues-for-hardware-inventory"></a>Problemas de segurança para o inventário de hardware  
 A coleta de inventários expõe vulnerabilidades potenciais. Os invasores podem fazer o seguinte:  

-   Enviar dados inválidos, que serão aceitos pelo ponto de gerenciamento, mesmo quando a configuração do cliente de inventário de software estiver desabilitada e a coleção de arquivos não estiver habilitada.  

-   Enviar quantidades de dados excessivamente grandes em um único arquivo e em vários arquivos, o que pode causar uma negação de serviço.  

-   Acessar informações de inventário quando forem transferidas para o Configuration Manager.  

 Como um usuário com privilégios administrativos locais pode enviar todas as informações como dados de inventário, não considere autoritativos os dados de inventário que são coletados pelo Configuration Manager.  

 O inventário de hardware é habilitado por padrão como uma configuração do cliente.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informações sobre privacidade para o inventário de hardware  
 O inventário de hardware permite que você recupere todas as informações armazenadas no Registro e no WMI em clientes do Configuration Manager. O inventário de software permite descobrir todos os arquivos de um tipo especificado ou coletar todos os arquivos especificados de clientes. O Asset Intelligence aprimora os recursos de inventário estendendo o inventário de hardware e software e adicionando novas funcionalidades de gerenciamento de licenças.  

 O inventário de hardware é habilitado por padrão como uma configuração do cliente, e as informações do WMI coletadas são determinadas pelas opções que você selecionar. O inventário de software é habilitado por padrão, mas arquivos não são coletados por padrão. A coleta de dados do Asset Intelligence é habilitada automaticamente; mesmo assim, é possível selecionar as classes de relatório de inventário de hardware a ser habilitadas.  

 As informações de inventário não são enviadas à Microsoft. As informações de inventário são armazenadas no banco de dados do Configuration Manager. Quando os clientes usam HTTPS para se conectarem a pontos de gerenciamento, os dados de inventário que enviam para o site são criptografados durante a transferência. Se os clientes usarem HTTP para se conectar a pontos de gerenciamento, você terá a opção de habilitar a criptografia de inventário. Os dados de inventário não são armazenados em formato criptografado no banco de dados. As informações são mantidas no banco de dados até que sejam excluídas pelas tarefas de manutenção do site **Excluir Histórico de Inventário Antigo** ou **Excluir Arquivos Coletados Antigos** a cada 90 dias. Você pode configurar o intervalo de exclusão.  

 Antes de configurar o inventário de hardware, o inventário de software, a coleta de arquivos ou a coleta de dados do Asset Intelligence, considere seus requisitos de privacidade.  
