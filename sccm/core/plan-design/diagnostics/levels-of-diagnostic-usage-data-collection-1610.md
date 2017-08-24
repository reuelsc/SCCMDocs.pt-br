---
title: "Dados de diagnóstico para 1610 | System Center Configuration Manager"
description: "Saiba mais sobre os níveis de dados de diagnóstico e de uso coletados pelo System Center Configuration Manager versão 1610."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb20eb90-bcc0-41de-bfea-638ea470c0dd
caps.latest.revision: "4"
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
ms.openlocfilehash: ba1e53fdc895690bb958c12d59f82a26067ecad3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1610-of-system-center-configuration-manager"></a>Níveis da coleta de dados de diagnóstico e de uso da versão 1610 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager versão 1610 coleta três níveis de dados de diagnóstico e de uso: **Básico**, **Avançado** e **Completo**. Por padrão, esse recurso é definido no nível Avançado. As seções a seguir fornecem detalhes adicionais sobre os dados coletados por cada nível.

Alterações de versões anteriores são indicadas com ***[Novo]*** ou ***[Atualizado]***, ***[Removido]*** ou ***[Movido]***.


> [!IMPORTANT]
>  O Configuration Manager não coleta códigos do site, nomes de site, endereços IP, nomes de usuário, nomes de computador, endereços físicos nem endereços de email nos níveis Básico ou Avançado. Qualquer coleta dessas informações no nível Completo não é proposital, ou seja, é potencialmente incluída nas informações de diagnóstico avançado como arquivos de log ou instantâneos de memória. A Microsoft não usará essas informações para identificá-lo, contatá-lo nem para desenvolver publicidade.

##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que têm um escopo administrativo baseado em função que inclui permissões **Modificar** na classe de objeto **Site** podem alterar o nível dos dados coletados nas configurações de Dados de Diagnóstico e de Uso no console do Configuration Manager.

Começando com a versão 1610, você altera o nível da coleta de dados no console navegando até **Administração** > **Visão Geral** > **Configuração de Site** > **Sites**. Abra **Configurações da Hierarquia** e, em seguida, selecione o nível de dados que você deseja usar.  

##  <a name="bkmk_level1"></a> Nível 1 — Básico
 O nível Básico inclui dados sobre sua hierarquia, dados necessários para ajudar a melhorar sua experiência de instalação ou de atualização e dados que ajudam a determinar as atualizações do Configuration Manager aplicáveis à sua hierarquia.

 Para o System Center Configuration Manager versão 1610, esse nível inclui o seguinte:


-   Informações de Instalação:
      - Build, tipo de instalação, pacotes de idiomas e recursos habilitados  

      - Status e erros de implantação do pacote de atualização, andamento do download e erros de pré-requisitos    

      - Versão do script pós-atualização

      - Uso do anel rápido de atualização

    - ***[Novo]*** Uso pré-lançamento, tipo de mídia de instalação, tipo de branch

    - ***[Novo]*** Data de validade do Software Assurance

- Métricas de desempenho do banco de dados (informações de processamento de replicação, principais procedimentos armazenados do SQL Server por processador e uso de disco)

- Configuração básica do banco de dados (processadores, configuração de cluster e configuração de exibições distribuídas)

- Esquema de banco de dados do Configuration Manager (hash de todas as definições de objeto)

- Contagem de versões de cliente do Configuration Manager e de versões do sistema operacional

- Contagem de sistemas operacionais em dispositivos gerenciados e políticas definidas pelo Exchange Connector

- Contagem de idiomas e localidades do cliente

- Contagem de dispositivos com Windows 10 por ramificação e compilação

- Dados básicos da hierarquia de sites do Configuration Manager (lista, tipo, versão, status, contagem de clientes e fuso horário de sites)

- Informações básicas do servidor do sistema de sites (funções do sistema de sites usadas, status de Internet e SSL, sistema operacional, processadores e máquina virtual ou física)

- Estatísticas de descoberta de usuário básicas (contagem de descoberta de usuário e tamanhos de grupo mínimo/máximo/médio)

- Informações básicas do Endpoint Protection (versões de cliente de antimalware)

- Contagens básicas de tipo de implantação e de aplicativo (total de aplicativos, total de aplicativos com vários tipos de implantação, total de aplicativos com dependências, total de aplicativos substituídos e contagem de tecnologias de implantação em uso)

- Contagens básicas de OSD (implantação de sistema operacional) (imagens)

- Tipos de ponto de distribuição e de ponto de gerenciamento e informações básicas de configuração (protegidas, pré-teste, PXE, multicast, estado de SSL, pontos de distribuição de recepção e de pares, habilitado para MDM, habilitado para SSL, etc.)

- Estatísticas de telemetria (quando executar, tempo de execução, erros)

- Nível de telemetria configurado, modo (online ou offline) e configuração de atualização rápida

- Uso da Descoberta de Rede (habilitada ou desabilitada)
- Console de administração:

     - Estatísticas sobre as conexões do console (versão de sistema operacional, idioma, SKU e arquitetura, memória do sistema, número de processadores lógicos, ID do site de conexão, versões do .NET instaladas e pacotes de idiomas do console)    

- Versão do SQL, nível do service pack, edição, ID de agrupamento e conjunto de caracteres


##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível Avançado é o padrão após a conclusão da instalação. Esse nível inclui dados coletados no nível Básico, dados específicos ao recurso (frequência e duração de uso), configurações de cliente do Configuration Manager (nome do componente, estado e algumas configurações como intervalos de sondagem) e informações básicas sobre atualizações de software.

Esse nível é recomendado porque fornece à Microsoft o mínimo de dados necessários para fazer melhorias úteis em versões futuras de produtos e serviços. Esse nível não coleta nomes de objeto (sites, usuários, computadores ou objetos), detalhes de objetos relacionados à segurança ou vulnerabilidades, como contagens de sistemas que exigem atualizações de software.

Para o System Center Configuration Manager versão 1610, esse nível inclui o seguinte:

-   **Gerenciamento de aplicativos:**  

    -    Informações básicas de uso/direcionamento para os tipos de implantação usados na organização (usuário versus dispositivo direcionado, obrigatório versus disponível e aplicativos universais)  

    -   Informações de implantação de aplicativo (instalação/desinstalação, exigência de aprovação, habilitação/desabilitação da interação do usuário, dependência e substituição)  

    -   Estatísticas de solicitação de aplicativo disponíveis  

    -   Contagem de pacotes por tipo  

    -   Contagem de aplicabilidade de aplicativo por sistema operacional  

    -   Contagem de implantações de pacote/programa  

    -   Contagem de ambientes do App-V e propriedades de implantação  

    -   Contagem de licenças de aplicativos do Windows 10 licenciadas  

    -   Número mínimo/máximo/médio de implantações de aplicativo por usuário/dispositivo por período

    -   Tipo e duração da janela de manutenção  

    -  Estatísticas de tamanho e complexidade da política de aplicativo

    - ***[Atualizado]*** Contagem de aplicativos Windows Store para Empresas e estatísticas de sincronização (incluindo tipos de aplicativos resumidos, status de aplicativos licenciados e número de aplicativos licenciados online e offline)  

    - Estatísticas de grupos de limites (quantos são rápidos, quantos são lentos e contagem por grupo)

    - Contagens e opções de configuração do MSI

    - Requisitos de aplicativo (a contagem de condições internas é referenciada por tecnologia de implantação)

    - Substituição de aplicativo, profundidade máxima da cadeia

    - Uso, como foi criado o UDA (Acesso a Dados Universal)

    - ***[Novo]*** Estatísticas de aprovação de aplicativo e frequência de uso



-   **Cliente:**  

    -   Lista/contagem de agentes cliente habilitados  

    -   Contagem de instalações do cliente de cada tipo de local de origem  

    -   Contagem de falhas de instalação do cliente  

    -  ***[Atualizado]*** Atualização automática do cliente: configuração de implantação, incluindo piloto do cliente e uso de exclusão (cliente de interoperabilidade estendida)

    -  Estatísticas de integridade do cliente e resumo dos principais problemas

    - Idade do BIOS em anos

    - Idade do sistema operacional em meses

    - Contagem de ações do Centro de Software

    - Versão do cliente do AMT (Active Management Technology)

    - Erros de download da implantação do cliente

    - Status da ação de operação de notificação do cliente (quantas vezes cada uma é executada, número máximo de clientes de destino e taxa média de êxito)

    - Métodos de implantação usados para o cliente e contagem de clientes por método de implantação

    - Configuração de tamanho do cache do cliente

    - ***[Novo]*** Número de classes de inventário de hardware, regras de inventário de software e regras de coleta de arquivos




- **Serviços de Nuvem:**

  - Contagem de coleções sincronizados com o Operations Management Suite

  -  Se o conector de nuvem do Operations Management Suite está habilitado

  - ***[Novo]*** Estatísticas de uso e de configuração do Gateway de Gerenciamento de Nuvem

  - ***[Novo]*** Contagem de Conectores do Upgrade Analytics




- **Coleções:**

    -  Estatísticas de avaliação da coleção (tempo de consulta, contagens de atribuídos versus não atribuídos, contagens por tipo, substituição de ID e uso de regra)

    - Coleções sem uma implantação

    - Uso de ID de coleção (com IDs suficientes)



-   **Configurações de conformidade:**  

    -   Contagem de itens de configuração por tipo  

    -   Informações de linha de base de configuração básica (contagem, número de implantações e número de referências)  

    -   Contagem de implantações que fazem referência às configurações internas (a configuração de correção agora é capturada)  

    -   Contagem de regras e implantações criadas para configurações personalizadas (a configuração de correção agora é capturada)  
    -   Contagem de protocolo SCEP, VPN, WiFi, certificado (.pfx) e modelos de Política de Conformidade implantados

    -  Contagem implantações de certificados SCEP, VPN, Wi-Fi, certificado (.pfx) e de Política de Conformidade por plataforma

    - Política do Passport for Work (criada, implantada)



-   **Conteúdo:**  

    -   Contagem de limites por tipo  

    -   Informações de grupo de limites (contagem de limites e de sistemas de sites atribuídos a cada grupo de limites)  

    - ***[Novo]*** Relações de grupos de limites e configuração de fallback

    -   Informações de grupo de pontos de distribuição (contagem de pacotes e pontos de distribuição atribuídos a cada grupo de pontos de distribuição)  

    -   Informações de configuração de pontos de distribuição (uso do cache de ramificação e monitoramento do ponto de distribuição)  

    -   Informações de configuração do Gerenciador de Distribuição (threads, intervalo de repetição, número de repetições e configurações de pontos de distribuição de recepção)  

    - ***[Novo]*** Contagem de clientes em cache de pares e estatísticas de uso

    - ***[Novo]*** Estatísticas de download do conteúdo do cliente


-   **Endpoint Protection:**  

    -   Uso da política do Firewall do Windows e antimalware do Endpoint Protection (número de políticas exclusivas atribuídas ao grupo)<br /><br /> Isso não inclui informações sobre as configurações incluídas na política.  

    -   Erros de implantação do Endpoint Protection (contagem de códigos de erro de implantação da política do Endpoint Protection)  

    -   Contagem de coleções selecionadas para serem exibidas no painel do Endpoint Protection  

    -   Contagem de alertas configurados para o recurso Endpoint Protection  

    -   Políticas ATP (Proteção Avançada contra Ameaças) (contagem de políticas e se as políticas são implantadas)


- **Migração:**

  -   Contagem de objetos migrados (uso do assistente de migração)



-   **MDM (Gerenciamento de dispositivo móvel):**  

    -   ***[Atualizado]*** Contagem de ações de dispositivo móvel emitidas: comandos de bloquear, redefinição de PIN, apagar, desativar e sincronizar agora  

    -   Contagem de dispositivos móveis gerenciados pelo Configuration Manager e pelo Microsoft Intune e como eles foram registrados (em massa, baseado no usuário)  

    -   Agendamento de sondagem de dispositivo móvel e estatísticas de duração de check-in de dispositivos móveis  

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

    -   Contagens de uso da etapa de sequência de tarefas

    - ***[Novo]*** Contagem de políticas de atualização de edição



-   **Atualizações do site:**

    - Versões de hotfixes do Configuration Manager instalados




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

    -   Classificações sincronizadas pelo Ponto de Atualização de Software

    -   Estatísticas de balanceamento de carga do ponto de atualização de software

    -  ***[Novo]*** Configuração de atualizações expressas do Windows 10




-   **Dados de desempenho/SQL:**  

    -   Contagem das maiores tabelas de banco de dados  

    -   ***[Atualizado]*** Uso, status de integridade e informações de réplica do SQL AlwaysOn

    -  Período de retenção do controle de alterações do SQL

    - Tipos de descoberta, habilitação e agendamento (completo, incremental)

    - Estatísticas operacionais de descoberta (contagem de objetos encontrados)

    - Período de retenção, estado de limpeza automática e problemas de desempenho do controle de alterações do SQL



- **Diversos**

    - Contagem de sites com WOL (Wake On LAN)

    - ***[Novo]*** Estatísticas de desempenho e de uso de relatório  



##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível Completo inclui todos os dados nos níveis Básico e Avançado. Também inclui informações adicionais sobre o Endpoint Protection, o percentual de conformidade da atualização e as informações de atualização de software.  Esse nível também pode incluir informações de diagnóstico avançado, como arquivos do sistema e instantâneos de memória, que podem incluir informações pessoais que existiam na memória ou nos arquivos de log no momento da captura.

Para o System Center Configuration Manager versão 1610, esse nível inclui o seguinte:

-   Avaliação de coleta e estatísticas de atualização

-   Resumo de integridade do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e sem suporte)

-   Configuração da política do Endpoint Protection

-   Informações de implantação de atualização de software (percentual de implantações direcionadas com o cliente versus hora UTC, obrigatório versus opcional versus silencioso e supressão de reinicialização)

-   Conformidade geral de implantações de atualização de software

-   Informações de agendamento de avaliação da regra de implantação automática

-   Contagens e códigos de erro de implantação da atualização de software

-   Número mínimo/máximo/médio de clientes inativos em coleções de implantação de atualização de software

-   Contagem de grupos que têm atualizações de software expiradas

-   Número mínimo/máximo/médio de atualizações de software por pacote

-   Percentuais de êxito de verificação da atualização de software

-   Número mínimo/máximo/médio de horas desde a última verificação de atualização de software

-    Produtos de atualização de software sincronizados pelo Ponto de Atualização de Software
-    Configurações de conformidade: detalhes de configuração de: modelo de protocolo SCEP, VPN, Wi-Fi e de Política de Conformidade

-    Tipo de políticas de Acesso Condicional EAS (bloqueio ou quarentena) para dispositivos que o Intune gerencia

-   As 50 principais CPUs no ambiente

-   Pacote de configuração do DCM para uso do System Center Configuration Manager

-   Código do produto MSI (aplicativos comuns que os clientes implantam)

-   Resumo de Integridade do ATP

-   Erros detalhados de instalação de implantação de cliente

- ***[Novo]*** Detalhes de aplicativos da Windows Store para Empresas (lista sem agregação de aplicativos sincronizados, incluindo AppID, estado online ou offline e contagem total de licenças compradas)
