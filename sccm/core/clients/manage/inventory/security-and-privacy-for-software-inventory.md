---
title: Privacidade de segurança do inventário de software
titleSuffix: Configuration Manager
description: Obtenha as informações de segurança e privacidade do inventário de software no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5fef3c1892c015fcec42197c9af373506d8e426a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-software-inventory-in-system-center-configuration-manager"></a>Segurança e privacidade do inventário de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém as informações de segurança e privacidade do inventário de software no System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Práticas recomendadas de segurança para inventário de software  
 Use as seguintes práticas recomendadas de segurança ao coletar dados de inventário de software de clientes:  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Assinar e criptografar dados de inventário|Quando os clientes se comunicam com pontos de gerenciamento usando HTTPS, todos os dados que eles enviam são criptografados por meio do SSL. No entanto, quando os computadores cliente usam o HTTP para se comunicarem com pontos de gerenciamento na intranet, os dados de inventário do cliente e os arquivos coletados podem ser enviados sem assinatura e sem criptografia. Certifique-se de que o site está configurado para exigir assinatura e usar criptografia. Além disso, se for possível que os clientes deem suporte para o algoritmo SHA-256, selecione a opção que exige o SHA-256.|  
|Não use a coleta de arquivos para coletar arquivos críticos ou informações confidenciais|O inventário de software do Configuration Manager usa todos os direitos da conta LocalSystem, que tem a capacidade de coletar cópias de arquivos de sistema críticos, como o Registro ou o banco de dados de contas de segurança. Quando esses arquivos estão disponíveis no servidor do site, alguém com os direitos de Ler Recursos ou direitos NTFS para o local do arquivo armazenado poderia analisar seu conteúdo e possivelmente distinguir detalhes importantes sobre o cliente a fim de comprometer a segurança.|  
|Restringir direitos administrativos locais nos computadores cliente|Um usuário com direitos administrativos locais pode enviar dados inválidos como informações de inventário.|  

### <a name="security-issues-for-software-inventory"></a>Problemas de segurança para o inventário de software  
 A coleta de inventários expõe vulnerabilidades potenciais. Os invasores podem fazer o seguinte:  

-   Enviar dados inválidos, que serão aceitos pelo ponto de gerenciamento, mesmo quando a configuração do cliente de inventário de software estiver desabilitada e a coleção de arquivos não estiver habilitada.  

-   Enviar quantidades de dados excessivamente grandes em um único arquivo e em vários arquivos, o que pode causar uma negação de serviço.  

-   Acessar informações de inventário quando forem transferidas para o Configuration Manager.  

 Se os usuários souberem que podem criar um arquivo oculto chamado **Skpswi.dat** e colocá-lo na raiz de um disco rígido do cliente para excluí-lo do inventário de software, você não poderá coletar dados de inventário de software desse computador.  

 Como um usuário com privilégios administrativos locais pode enviar todas as informações como dados de inventário, não considere autoritativos os dados de inventário que são coletados pelo Configuration Manager.  

 O inventário de software é habilitado por padrão como uma configuração do cliente.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informações sobre privacidade para o inventário de software  
 O inventário de hardware permite que você recupere todas as informações armazenadas no Registro e no WMI em clientes do Configuration Manager. O inventário de software permite descobrir todos os arquivos de um tipo especificado ou coletar todos os arquivos especificados de clientes. O Asset Intelligence aprimora os recursos de inventário estendendo o inventário de hardware e software e adicionando novas funcionalidades de gerenciamento de licenças.  

 O inventário de hardware é habilitado por padrão como uma configuração do cliente, e as informações do WMI coletadas são determinadas pelas opções que você selecionar. O inventário de software é habilitado por padrão, mas arquivos não são coletados por padrão. A coleta de dados do Asset Intelligence é habilitada automaticamente; mesmo assim, é possível selecionar as classes de relatório de inventário de hardware a ser habilitadas.  

 As informações de inventário não são enviadas à Microsoft. As informações de inventário são armazenadas no banco de dados do Configuration Manager. Quando os clientes usam HTTPS para se conectarem a pontos de gerenciamento, os dados de inventário que enviam para o site são criptografados durante a transferência. Se os clientes usarem HTTP para se conectar a pontos de gerenciamento, você terá a opção de habilitar a criptografia de inventário. Os dados de inventário não são armazenados em formato criptografado no banco de dados. As informações são mantidas no banco de dados até que sejam excluídas pelas tarefas de manutenção do site **Excluir Histórico de Inventário Antigo** ou **Excluir Arquivos Coletados Antigos** a cada 90 dias. Você pode configurar o intervalo de exclusão.  

 Antes de configurar o inventário de hardware, o inventário de software, a coleta de arquivos ou a coleta de dados do Asset Intelligence, considere seus requisitos de privacidade.  
