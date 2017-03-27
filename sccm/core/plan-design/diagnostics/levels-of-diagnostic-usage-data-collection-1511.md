---
title: "Dados de diagnóstico para 1511 | Microsoft Docs"
description: "Saiba mais sobre os níveis de dados de diagnóstico e de uso que o System Center Configuration Manager versão 1511 coleta."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e614ae1-47d2-4a93-ba0a-89dc50d1e266
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 34a4c3d0d641c4ab03e068c6dad78300057861bd
ms.openlocfilehash: 4c7717e4f5a20c5c8d20fef21d0c67172b3198bd
ms.lasthandoff: 03/16/2017

---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1511-of-system-center-configuration-manager"></a>Níveis da coleta de dados de diagnóstico e de uso da versão 1511 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager versão 1511 coleta três níveis de dados de diagnóstico e de uso: **Básico**, **Avançado** e **Completo**. Por padrão, esse recurso é definido no nível Avançado. As seções a seguir fornecem detalhes adicionais sobre os dados coletados por cada nível.  

> [!IMPORTANT]  
>  O Configuration Manager não coleta códigos do site, nomes de site, endereços IP, nomes de usuário, nomes de computador, endereços físicos nem endereços de email nos níveis Básico ou Avançado. Qualquer coleta dessas informações no nível Completo não é proposital, ou seja, é potencialmente incluída nas informações de diagnóstico avançado como arquivos de log ou instantâneos de memória. A Microsoft não usará essas informações para identificá-lo, contatá-lo nem para desenvolver publicidade.  

##  <a name="bkmk_change"></a> Como alterar o nível  
 Os administradores que têm um escopo administrativo baseado em função que inclui permissões **Modificar** na classe de objeto **Site** podem alterar o nível dos dados coletados nas configurações de Dados de Diagnóstico e de Uso no console do Configuration Manager.

 Para fazer isso, no console, acesse a guia Backstage (a guia superior esquerda com a seta suspensa), selecione **Dados de Uso** e, em seguida, selecione o nível de dados que você deseja usar.  


##  <a name="bkmk_level1"></a> Nível 1 — Básico  
 O nível Básico inclui dados sobre sua hierarquia, dados necessários para ajudar a melhorar sua experiência de instalação ou de atualização e dados que ajudam a determinar as atualizações do Configuration Manager aplicáveis à sua hierarquia.  

 A partir da versão 1511 do System Center Configuration Manager, este nível inclui o seguinte:  


-   Informações de configuração
    - Build, tipo de instalação, pacotes de idiomas e recursos habilitados

    - Status e erros de implantação de pacote de atualização  

-   Métricas de desempenho do banco de dados (informações de processamento de replicação, principais procedimentos armazenados do SQL Server por processador e uso de disco)  

-   Configuração básica do banco de dados (processadores, configuração de cluster e configuração de exibições distribuídas)  

-   Esquema de banco de dados do Configuration Manager (hash de todas as definições de objeto)  

-   Contagem de versões de cliente do Configuration Manager e de versões do sistema operacional  

-   Contagem de sistemas operacionais em dispositivos gerenciados e políticas definidas pelo Exchange Connector  

-   Contagem de idiomas e localidades do cliente

-   Contagem de dispositivos com Windows 10 por ramificação e compilação  

-   Dados básicos da hierarquia de sites do Configuration Manager (lista, tipo, versão, status, contagem de clientes e fuso horário de sites)  

-   Informações básicas do servidor do sistema de sites (funções do sistema de sites usadas, status de Internet e SSL, sistema operacional, processadores e máquina virtual ou física)  

-   Estatísticas de descoberta de usuário básicas (contagem de descoberta de usuário e tamanhos de grupo mínimo/máximo/médio)  

-   Informações básicas do Endpoint Protection (versões de cliente de antimalware)  

-   Contagens básicas de tipo de implantação e de aplicativo (total de aplicativos, total de aplicativos com vários tipos de implantação, total de aplicativos com dependências, total de aplicativos substituídos e contagem de tecnologias de implantação em uso)  

-   Contagens básicas de OSD (implantação de sistema operacional) (imagens)  

-   Tipos de ponto de distribuição e de ponto de gerenciamento e informações básicas de configuração (protegidas, pré-teste, PXE, multicast, estado de SSL, pontos de distribuição de recepção e de pares, habilitado para MDM, habilitado para SSL, etc.)  

-   Estatísticas de telemetria (quando executar, tempo de execução e erros)  

##  <a name="bkmk_level2"></a> Nível 2 - Avançado  
O nível Avançado é o padrão após a conclusão da instalação. Esse nível inclui dados coletados no nível Básico, dados específicos ao recurso (frequência e duração de uso), configurações do cliente do Configuration Manager (nome do componente, estado e algumas configurações como intervalos de sondagem), bem como informações básicas sobre atualizações de software.  

Esse nível é recomendado porque fornece à Microsoft o mínimo de dados necessários para fazer melhorias úteis em versões futuras de produtos e serviços. Esse nível não coleta nomes de objeto (sites, usuários, computadores ou objetos), detalhes sobre objetos relacionados à segurança ou vulnerabilidades como contagens de sistemas que exigem atualizações de software.  

A partir da versão 1511 do System Center Configuration Manager, este nível inclui o seguinte:  

-   **Gerenciamento de aplicativos:**  

    -   Informações básicas de uso/direcionamento para os tipos de implantação usados na organização (usuário versus dispositivo direcionado e obrigatório versus disponível)  

    -   Informações de implantação de aplicativo (instalação/desinstalação, exigência de aprovação e habilitação/desabilitação da interação do usuário)  

    -   Estatísticas de solicitação de aplicativo disponíveis  

    -   Contagem de pacotes por tipo  

    -   Contagem de aplicabilidade de aplicativo por sistema operacional  

    -   Contagem de implantações de pacote/programa  

    -   Contagem de ambientes do App-V e propriedades de implantação  

    -   Contagem de licenças de aplicativos do Windows 10 licenciadas  

    -   Número mínimo/máximo/médio de implantações de aplicativo por usuário/dispositivo  

    -   Tipo e duração da janela de manutenção  

-   **Cliente:**  

    -   Lista/contagem de agentes cliente habilitados  

    -   Contagem de instalações do cliente de cada tipo de local de origem  

    -   Contagem de falhas de instalação do cliente  

-   **Configurações de conformidade:**  

    -   Contagem de itens de configuração por tipo  

    -   Informações de linha de base de configuração básica (contagem, número de implantações e número de referências)  

    -   Contagem de implantações que fazem referência a configurações internas (o valor da configuração não é capturado)  

    -   Contagem de regras e implantações criadas para as configurações personalizadas  

    -   Contagem de modelos de protocolo SCEP implantados  

-   **Conteúdo:**  

    -   Contagem de limites por tipo  

    -   Informações de grupo de limites (contagem de limites e de sistemas de sites atribuídos a cada grupo de limites)  

    -   Informações de grupo de pontos de distribuição (contagem de pacotes e pontos de distribuição atribuídos a cada grupo de pontos de distribuição)  

    -   Informações de configuração de pontos de distribuição (uso do cache de ramificação e monitoramento do ponto de distribuição)  

    -   Informações de configuração do Gerenciador de Distribuição (threads, intervalo de repetição, número de repetições e configurações de pontos de distribuição de recepção)  

-   **Endpoint Protection:**  

    -   Uso da política do Firewall do Windows e antimalware do Endpoint Protection (número de políticas exclusivas atribuídas ao grupo)<br /><br />Isso não inclui informações sobre as configurações incluídas na política.  

    -   Erros de implantação do Endpoint Protection (contagem de códigos de erro de implantação da política do Endpoint Protection)  

    -   Contagem de coleções selecionadas a serem exibidas no painel do Endpoint Protection  

    -   Contagem de alertas configurados para o recurso Endpoint Protection  

-   **MAM (Gerenciamento de aplicativos móveis):**  

    -   Contagem de aplicativos do Office habilitados para MAM, aplicativos de linha de negócios e políticas por sistema operacional  

    -   Contagem de implantações de aplicativo/política de MAM  

    -   Contagem de regras criadas de acordo com a configuração de MAM  

-   **MDM (Gerenciamento de dispositivo móvel):**  

    -   Contagem de ações de dispositivo móvel emitidas: comandos bloquear, redefinição de PIN, apagar e desativar

    -   Contagem de dispositivos móveis gerenciados pelo Configuration Manager e pelo Microsoft Intune e como eles foram registrados (em massa ou baseado no usuário)  

    -   Agendamento e estatísticas de sondagem de dispositivo móvel e duração de check-in de dispositivos móveis  

    -   Contagem de políticas de dispositivo móvel  

    -   Contagem de usuários que têm vários dispositivos móveis registrados  

-   **Solução de problemas do Microsoft Intune:**  

    -   Contagem e tamanho de estado, status, inventário, RDR, DDR, UDX, estado de Locatário, POL, LOG, Cert, CRP, Ressincronização, CFD, RDO, BEX, ISM e mensagens de conformidade baixadas do Microsoft Intune  

    -   Contagem e tamanho das ações de dispositivo (apagar, desativar, bloquear), telemetria e mensagens de dados replicadas para o Microsoft Intune  

    -   Estatísticas de sincronização de usuário completa e delta para o Microsoft Intune  

-   **MDM (Gerenciamento de dispositivo móvel) local:**  

    -   Estatísticas de êxito/falha de implantação para implantações locais de aplicativo de MDM  

    -   Contagem de perfis e pacotes de registro em massa do Windows 10  

-   **Implantação de sistema operacional:**  

    -   Contagem de imagens de inicialização, drivers, pacotes de driver, pontos de distribuição habilitados para multicast, pontos de distribuição habilitados para PXE e sequências de tarefas  

-   **Atualizações de software:**  

    -   Número total/médio de coleções que têm implantações de atualização de software e número máximo/médio de atualizações implantadas  

    -   Número de regras de implantação automática vinculadas à sincronização  

    -   Número de regras de implantação automática que criam ou adicionam atualizações a um grupo existente  

    -   Deltas disponíveis e de data limite usados nas regras de implantação automática  

    -   Número médio e máximo de atribuições por atualização  

    -   Contagem de atualizações criadas e implantadas com o System Center Update Publisher  

    -   Contagem de grupos de atualização e atribuições  

    -   Contagem de pacotes de atualização e o número mínimo/máximo/médio de pontos de distribuição direcionados com pacotes  

    -   Número de grupos de atualização e número mínimo/máximo/médio de atualizações por grupo  

    -   Número de atualizações e percentual de atualizações implantadas, expiradas, substituídas, baixadas e que contêm EULAs  

    -   Códigos de erro de verificação de atualização e contagem de computadores  

    -   Avaliação da atualização de cliente e agendamentos de verificação  

    -   Agendamento de sincronização do ponto de atualização de software  

    -   Número de regras de implantação automática que têm várias implantações  

    -   Configurações usadas para planos ativos de manutenção do Windows 10  

    -   Versões de conteúdo do painel do Windows 10  

    -   Contagem de clientes do Windows 10 que usam o Windows Update para Empresas  

    -   Estatísticas de aplicação de patch de cluster  

    -   Contagem de atualizações do Office 365 implantadas  

-   **Dados de desempenho/SQL:**  

    -   Contagem das maiores tabelas de banco de dados  

    -   Informações de réplica do SQL Always-On  

    -   Contagem de coleções por tipo  

##  <a name="bkmk_level3"></a> Nível 3 - Completo  
O nível Completo inclui todos os dados nos níveis Básico e Avançado. Também inclui informações adicionais sobre o Endpoint Protection, o percentual de conformidade da atualização e as informações de atualização de software. Esse nível também pode incluir informações de diagnóstico avançado, como arquivos do sistema e instantâneos de memória, que podem incluir informações pessoais que existiam na memória ou nos arquivos de log no momento da captura.  

A partir da versão 1511 do System Center Configuration Manager, este nível inclui o seguinte:  

-   Avaliação de coleta e estatísticas de atualização  

-   Resumo de integridade do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e sem suporte)  

-   Configuração da política do Endpoint Protection  

-   Informações de implantação de atualização de software (percentual de implantações direcionadas com o cliente versus hora UTC, obrigatório versus opcional versus silencioso e supressão de reinicialização)  

-   Conformidade geral de implantações de atualização de software  

-   Informações de agendamento de avaliação da regra de implantação automática  

-   Número de clientes que têm políticas de proteção de acesso à rede  

-   Contagens e códigos de erro de implantação da atualização de software  

-   Número mínimo/máximo/médio de clientes inativos em coleções de implantação de atualização de software  

-   Contagem de grupos que têm atualizações de software expiradas  

-   Número mínimo/máximo/médio de atualizações de software por pacote  

-   Percentuais de êxito de verificação da atualização de software  

-   Número mínimo/máximo/médio de horas desde a última verificação de atualização de software  

