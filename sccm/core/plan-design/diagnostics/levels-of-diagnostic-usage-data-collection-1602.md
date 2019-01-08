---
title: Dados de diagnóstico para 1602
titleSuffix: Configuration Manager
description: Saiba mais sobre os níveis de dados de diagnóstico e de uso que o System Center Configuration Manager versão 1602 coleta.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1210a1ca-78c7-4d17-81cf-ac1bc5c5cf3e
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: cac4e555ece110ede0ccddb59d947a6068ef38ff
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423313"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1602-of-system-center-configuration-manager"></a>Níveis da coleta de dados de diagnóstico e de uso da versão 1602 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager versão 1602 coleta três níveis de dados de diagnóstico e de uso: **Básico**, **Avançado** e **Completo**. Por padrão, esse recurso é definido no nível Avançado. As seções a seguir fornecem detalhes adicionais sobre os dados coletados por cada nível.

Alterações de versões anteriores são indicadas com ***[Novo]*** ou ***[Atualizado]***.

> [!IMPORTANT]
>  O Configuration Manager não coleta códigos do site, nomes de site, endereços IP, nomes de usuário, nomes de computador, endereços físicos nem endereços de email nos níveis Básico ou Avançado. Qualquer coleta dessas informações no nível Completo não é proposital, ou seja, é potencialmente incluída nas informações de diagnóstico avançado como arquivos de log ou instantâneos de memória. A Microsoft não usará essas informações para identificá-lo, contatá-lo nem para desenvolver publicidade.

##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que têm um escopo administrativo baseado em função que inclui permissões **Modificar** na classe de objeto **Site** podem alterar o nível dos dados coletados nas configurações de Dados de Diagnóstico e de Uso no console do Configuration Manager.


  Para fazer isso, no console, acesse a guia Backstage (a guia superior esquerda com a seta suspensa), selecione **Dados de Uso** e, em seguida, selecione o nível de dados que você deseja usar.  

##  <a name="bkmk_level1"></a> Nível 1 — Básico
 O nível Básico inclui dados sobre sua hierarquia, dados necessários para ajudar a melhorar sua experiência de instalação ou de atualização e dados que ajudam a determinar as atualizações do Configuration Manager aplicáveis à sua hierarquia.

 A partir da versão 1602 do System Center Configuration Manager, este nível inclui o seguinte:


- Informações de Instalação:
  - Build, tipo de instalação, pacotes de idiomas e recursos habilitados  

  - ***[Atualizado]*** Foi atualizado o status e erros de implantação de pacote, andamento do download e erros de pré-requisitos     

  - ***[Novo]*** Versão do script pós-atualização

  - ***[Novo]*** Uso do anel rápido de atualização

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

- ***[Novo]*** Nível de telemetria configurado, modo (online ou offline) e configuração de atualização rápida

- ***[Novo]*** Uso de Descoberta de Rede (habilitado ou desabilitado)
- ***[Novo]*** Console de Administração:

    -  Estatísticas sobre as conexões do console (versão de sistema operacional, idioma, SKU e arquitetura, memória do sistema, número de processadores lógicos, ID do site de conexão, versão do .NET instalada e pacotes de idiomas do console)

##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível Avançado é o padrão após a conclusão da instalação. Esse nível inclui dados coletados no nível Básico, dados específicos ao recurso (frequência e duração de uso), configurações de cliente do Configuration Manager (nome do componente, estado e algumas configurações como intervalos de sondagem), bem como informações básicas sobre atualizações de software.

Esse nível é recomendado porque fornece à Microsoft o mínimo de dados necessários para fazer melhorias úteis em versões futuras de produtos e serviços. Esse nível não coleta nomes de objeto (sites, usuários, computador ou objetos), detalhes sobre objetos relacionados à segurança ou vulnerabilidades como contagens de sistemas que exigem atualizações de software.

A partir da versão 1602 do System Center Configuration Manager, este nível inclui o seguinte:

- **Gerenciamento de aplicativos:**

  -   ***[Atualizado]*** Informações básicas de uso/direcionamento para os tipos de implantação usados na organização (usuário versus dispositivo direcionado, obrigatório versus disponível e aplicativos universais)  

  -  ***[Atualizado]*** Informações de implantação de aplicativo (instalação/desinstalação, exigência de aprovação, habilitação/desabilitação da interação do usuário, dependência e substituição)  

  -   Estatísticas de solicitação de aplicativo disponíveis  

  -   Contagem de pacotes por tipo  

  -   Contagem de aplicabilidade de aplicativo por sistema operacional  

  -   Contagem de implantações de pacote/programa  

  -   Contagem de ambientes do App-V e propriedades de implantação  

  -   Contagem de licenças de aplicativos do Windows 10 licenciadas  

  -   ***[Atualizado]*** Número mínimo/máximo/médio de implantações de aplicativo por usuário/dispositivo por período

  -   Tipo e duração da janela de manutenção  

  -  ***[Novo]*** Estatísticas de tamanho e complexidade da política de aplicativo

- **Cliente:**

  -   Lista/contagem de agentes cliente habilitados

  -   Contagem de instalações do cliente de cada tipo de local de origem

  -   Contagem de falhas de instalação do cliente

- **Configurações de conformidade:**

  -   Contagem de itens de configuração por tipo

  -   Informações de linha de base de configuração básica (contagem, número de implantações e número de referências)

  -   Contagem de implantações que fazem referência a configurações internas (o valor da configuração não é capturado)

  -   Contagem de regras e implantações criadas para as configurações personalizadas

  -   ***[Atualizado]*** Contagem de protocolo SCEP, VPN, WiFi, certificado (.pfx) e modelos de Política de Conformidade implantados   

  -  ***[Novo]*** Contagem de protocolo SCEP, VPN, WiFi, certificado (.pfx) e modelos de Política de Conformidade implantados por plataforma

- **Conteúdo:**

  -   Contagem de limites por tipo

  -   Informações de grupo de limites (contagem de limites e de sistemas de sites atribuídos a cada grupo de limites)

  -   Informações de grupo de pontos de distribuição (contagem de pacotes e pontos de distribuição atribuídos a cada grupo de pontos de distribuição)

  -   Informações de configuração de pontos de distribuição (uso do cache de ramificação e monitoramento do ponto de distribuição)

  -   Informações de configuração do Gerenciador de Distribuição (threads, intervalo de repetição, número de repetições e configurações de pontos de distribuição de recepção)

- **Endpoint Protection:**

  -   Uso da política do Firewall do Windows e antimalware do Endpoint Protection (número de políticas exclusivas atribuídas ao grupo)<br /><br />Isso não inclui informações sobre as configurações incluídas na política.

  -   Erros de implantação do Endpoint Protection (contagem de códigos de erro de implantação da política do Endpoint Protection)

  -   Contagem de coleções selecionadas para serem exibidas no painel do Endpoint Protection

  -   Contagem de alertas configurados para o recurso Endpoint Protection

- **MAM (Gerenciamento de aplicativos móveis):**

  -   Contagem de aplicativos do Office habilitados para MAM, aplicativos de linha de negócios e políticas por sistema operacional

  -   Contagem de implantações de aplicativo/política de MAM

  -   Contagem de regras criadas de acordo com a configuração de MAM

- **MDM (Gerenciamento de dispositivo móvel):**

  -   Contagem de ações de dispositivo móvel emitidas: comandos bloquear, redefinição de PIN, apagar e desativar

  -   Contagem de dispositivos móveis gerenciados pelo Configuration Manager e pelo Microsoft Intune e como eles foram registrados (em massa ou baseado no usuário)

  -   Agendamento de sondagem de dispositivo móvel e estatísticas de duração de check-in de dispositivos móveis

  -   Contagem de políticas de dispositivo móvel

  -   Contagem de usuários que têm vários dispositivos móveis registrados

- **Solução de problemas do Microsoft Intune:**

  -   Contagem e tamanho de estado, status, inventário, RDR, DDR, UDX, estado de Locatário, POL, LOG, Cert, CRP, Ressincronização, CFD, RDO, BEX, ISM e mensagens de conformidade baixadas do Microsoft Intune

  -   Contagem e tamanho das ações de dispositivo (apagar, desativar, bloquear), telemetria e mensagens de dados replicadas para o Microsoft Intune

  -   Estatísticas de sincronização de usuário completa e delta para o Microsoft Intune

- **MDM (Gerenciamento de dispositivo móvel) local:**

  -   Estatísticas de êxito/falha de implantação para implantações locais de aplicativo de MDM

  -   Contagem de perfis e pacotes de registro em massa do Windows 10

- **Implantação de sistema operacional:**

  -   Contagem de imagens de inicialização, drivers, pacotes de driver, pontos de distribuição habilitados para multicast, pontos de distribuição habilitados para PXE e sequências de tarefas

- **Atualizações de software:**

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

  -   ***[Novo]*** Classificações sincronizadas pelo Ponto de Atualização de Software

- **Dados de desempenho/SQL:**

  -   Contagem das maiores tabelas de banco de dados

  -   Informações de réplica do SQL Always-On

  -   Contagem de coleções por tipo

  -   ***[Atualizado]*** Estatísticas de avaliação de coleção (tempo de consulta, contagens de atribuído versus não atribuídos, contagens por tipo, ID de substituição e uso de regra)

  - ***[Novo]*** Período de retenção do controle de alterações do SQL Server

- ***[Novo] Atualizações do site:***

  - ***[Novo]*** Versões dos hotfixes do Configuration Manager instalados

##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível Completo inclui todos os dados nos níveis Básico e Avançado. Também inclui informações adicionais sobre o Endpoint Protection, o percentual de conformidade da atualização e as informações de atualização de software. Esse nível também pode incluir informações de diagnóstico avançado, como arquivos do sistema e instantâneos de memória, que podem incluir informações pessoais que existiam na memória ou nos arquivos de log no momento da captura.

A partir da versão 1602 do System Center Configuration Manager, este nível inclui o seguinte:

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

-   ***[Novo]*** Produtos de atualização de software sincronizados pelo Ponto de Atualização de Software
-   ***[Novo]*** Configurações de conformidade: detalhes de configuração de protocolo SCEP, VPN, Wi-Fi e de modelo de política de conformidade

-   ***[Novo]*** Tipo de políticas de acesso condicional EAS (bloqueio ou quarentena) para dispositivos gerenciados pelo Intune
