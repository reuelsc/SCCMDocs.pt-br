---
title: "Dados de diagnóstico para 1511 | Microsoft Docs"
description: "Saiba mais sobre os níveis de dados de diagnóstico e de uso que o System Center Configuration Manager versão 1511 coleta."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: fa3c2f9c9bdc1f095b450babd675db4a160992d9

---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1511-of-system-center-configuration-manager"></a>Níveis da coleta de dados de diagnóstico e de uso da versão 1511 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager versão 1511 coleta três níveis de dados de diagnóstico e de uso: **Básico**, **Avançado** e **Completo**. Por padrão, esse recurso é definido no nível Avançado. As seções a seguir fornecem mais detalhes de quais dados são coletados por cada nível.  

> [!IMPORTANT]  
>  O Configuration Manager não coleta códigos do site ou nomes de sites, endereços IP, nomes de usuário ou computador, endereços físicos ou de email nos níveis Básico ou Avançado. Qualquer coleta dessas informações no nível Completo não é proposital (potencialmente incluídas nas informações de diagnóstico avançadas, como arquivos de log ou instantâneos de memória) e elas não serão usadas pela Microsoft para identificá-lo ou contatá-lo nem para fins de publicidade.  

##  <a name="a-namebkmkchangea-how-to-change-the-level"></a><a name="bkmk_change"></a> Como alterar o nível  
 Os administradores com um escopo administrativo baseado em funções que inclui as permissões **Modificar** na classe de objeto **Site** podem alterar o nível dos dados coletados nas configurações Dados de Diagnóstico e de Uso no console do Configuration Manager.

 Para fazer isso, no console, acesse a guia Backstage (a guia superior esquerda com a seta suspensa), selecione **Dados de Uso** e o nível de dados que você deseja usar.  


##  <a name="a-namebkmklevel1a-level-1---basic"></a><a name="bkmk_level1"></a> Nível 1 — Básico  
 O nível Básico inclui dados sobre sua hierarquia e é necessário para ajudar a aperfeiçoar sua experiência de instalação ou de atualização, bem como para ajudar a determinar quais atualizações do Configuration Manager são aplicáveis à sua hierarquia.  

 A partir da versão 1511 do System Center Configuration Manager, este nível inclui o seguinte:  


-   Informações de configuração (compilação, tipo de instalação, pacotes de idiomas, recursos habilitados pelo usuário, status de implantação e erros do pacote de atualização)  

-   Métricas de desempenho do banco de dados (informações de processamento de replicação, principais procedimentos armazenados do SQL Server por processador e uso de disco)  

-   Configuração básica de banco de dados (processadores, configuração de cluster, configuração de exibições distribuídas)  

-   Esquema de banco de dados do Configuration Manager (hash de todas as definições de objeto)  

-   Contagem de versões de cliente do Configuration Manager e de versões do sistema operacional  

-   Contagem e sistema operacional de dispositivos gerenciados e políticas definidas pelo Exchange Connector  

-   Contagem de idiomas e localidade do cliente  

-   Contagem de dispositivos com Windows 10 por ramificação e compilação  

-   Dados básicos de hierarquia de site do Configuration Manager (lista de sites, tipo, versão, status, contagem de clientes e fuso horário)  

-   Informações básicas de servidor do sistema de sites (funções do sistema de sites usadas, status de Internet e SSL, sistema operacional, processadores, máquina virtual ou física)  

-   Estatísticas básicas de descoberta de usuário (contagem de descoberta de usuário, tamanhos mínimo/máximo/médio de grupo)  

-   Informações básicas do endpoint protection (versões de cliente de antimalware)  

-   Contagens básicas de tipo de implantação e aplicativo (total de aplicativos, total de aplicativos com vários tipos de implantação, total de aplicativos com dependências, total de aplicativos substituídos, contagem de tecnologias de implantação em uso)  

-   Contagens básicas de OSD (imagens)  

-   Tipos de ponto de distribuição e de ponto de gerenciamento e informações de configuração básica (protegidas, em pré-teste, PXE, multicast, estado de SSL, pontos de distribuição de recepção/ponto a ponto, habilitado para MDM, habilitado para SSL, etc.)  

-   Estatísticas de telemetria (quando executar, tempo de execução, erros)  

##  <a name="a-namebkmklevel2a-level-2---enhanced"></a><a name="bkmk_level2"></a> Nível 2 - Avançado  
O nível Avançado é o padrão após a instalação. Esse nível inclui dados coletados no nível Básico, bem como dados específicos do recurso (frequência e duração de uso), configurações do cliente do Configuration Manager (nome do componente, seu estado e algumas configurações como intervalos de sondagem), bem como informações básicas sobre atualizações de software.  

Esse nível é recomendado porque fornece à Microsoft o mínimo de dados necessários para fazer aperfeiçoamentos úteis em versões futuras de produtos e serviços. Esse nível não coleta nomes de objeto (sites, usuários, computadores ou objetos), detalhes de objetos relacionados à segurança ou vulnerabilidades, como contagens de sistemas que exigem atualizações de software.  

A partir da versão 1511 do System Center Configuration Manager, este nível inclui o seguinte:  

-   **Gerenciamento de aplicativos:**  

    -   Informações básicas de uso/direcionamento para os tipos de implantação usados na organização (usuário vs. dispositivo afetado, obrigatório vs. disponível)  

    -   Informações de implantação de aplicativo (instalação/desinstalação, exigência de aprovação, habilitação/desabilitação da interação do usuário)  

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

    -   Informações do grupo de pontos de distribuição (contagem de pacotes e de pontos de distribuição atribuídos a cada grupo de pontos de distribuição)  

    -   Informações de configuração do ponto de distribuição (uso do cache de ramificação, monitoramento do ponto de distribuição)  

    -   Informações de configuração do Gerenciador de Distribuição (threads, intervalo de repetição, número de repetições, configurações de ponto de distribuição de recepção)  

-   **Endpoint Protection:**  

    -   Antimalware do Endpoint Protection e uso de política do Firewall do Windows (número de políticas exclusivas atribuídas ao grupo; isso não inclui quaisquer informações sobre as configurações incluídas na política)  

    -   Erros de implantação do Endpoint Protection (contagem de códigos de erro de implantação da política do Endpoint Protection)  

    -   Contagem de coleções selecionadas que aparecerá no painel do endpoint protection  

    -   Contagem de alertas configurados para o recurso endpoint protection  

-   **MAM (Gerenciamento de aplicativos móveis):**  

    -   Contagem de aplicativos de linha de negócios e do Office habilitados para MAM e política por sistema operacional  

    -   Contagem de implantações de aplicativo/política de MAM  

    -   Contagem de regras criadas de acordo com a configuração de MAM  

-   **MDM (Gerenciamento de dispositivo móvel):**  

    -   Contagem de ações de comandos (bloquear, fixar, repousar, apagar e desativar) de dispositivo móvel emitidos  

    -   Contagem de dispositivos móveis gerenciados pelo Configuration Manager e pelo Microsoft Intune e como eles foram registrados (em massa ou com base no usuário)  

    -   Agendamento e estatísticas de sondagem de dispositivo móvel e duração de check-in de dispositivos móveis  

    -   Contagem de políticas de dispositivo móvel  

    -   Contagem de usuários com vários dispositivos móveis registrados  

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

    -   Contagem de pacotes de atualização e o número mínimo/máximo/médio de pontos de distribuição afetados com pacotes  

    -   Número de grupos de atualização e número mínimo/máximo/médio de atualizações por grupo  

    -   Número de atualizações e percentual de atualizações implantadas, vencidas, substituídas, baixadas e que contêm EULAs  

    -   Códigos de erro de verificação de atualização e contagem de computadores  

    -   Avaliação da atualização de cliente e agendamentos de verificação  

    -   Agendamento de sincronização do ponto de atualização de software  

    -   Número de regras de implantação automática com várias implantações  

    -   Configurações usadas para planos de serviço ativos do Windows 10  

    -   Versões de conteúdo do painel do Windows 10  

    -   Contagem de clientes do Windows 10 que estão usando o Windows Update para Empresas  

    -   Estatísticas de aplicação de patch de cluster  

    -   Contagem de atualizações do Office 365 implantadas  

-   **Dados de desempenho/SQL:**  

    -   Contagem das maiores tabelas de banco de dados  

    -   Informações de réplica do SQL Always-On  

    -   Contagem de coleções por tipo  

##  <a name="a-namebkmklevel3a-level-3---full"></a><a name="bkmk_level3"></a> Nível 3 - Completo  
O nível Completo inclui todos os dados em Básico e Avançado. Também inclui informações adicionais sobre o Endpoint Protection, o percentual de conformidade da atualização e as informações de atualização de software.  Esse nível também pode incluir informações de diagnóstico avançadas, como arquivos do sistema e instantâneos da memória que podem incluir informações pessoais que existiam na memória ou nos arquivos de log no momento da captura.  

A partir da versão 1511 do System Center Configuration Manager, este nível inclui o seguinte:  

-   Avaliação de coleta e estatísticas de atualização  

-   Resumo de integridade do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e sem suporte)  

-   Configuração da política do Endpoint Protection  

-   Informações de implantação de atualização de software (percentual de implantações afetadas com o cliente vs. Hora UTC, necessário vs. opcional vs. silencioso, supressão de reinicialização)  

-   Conformidade geral de implantações de atualização de software  

-   Informações de agendamento de avaliação da regra de implantação automática  

-   Número de clientes com a política de proteção de acesso à rede  

-   Contagens e códigos de erro de implantação da atualização de software  

-   Número mínimo/máximo/médio de clientes inativos em coleções de implantação de atualização de software  

-   Contagem de grupos com atualizações de software vencidas  

-   Número mínimo/máximo/médio de atualizações de software por pacote  

-   Percentuais de êxito de verificação da atualização de software  

-   Número mínimo/máximo/médio de horas desde a última verificação de atualização de software  



<!--HONumber=Dec16_HO3-->


