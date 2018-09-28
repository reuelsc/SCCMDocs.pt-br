---
title: Dados de diagnóstico para 1706
titleSuffix: Configuration Manager
description: Saiba mais sobre os níveis de dados de diagnóstico e de uso que o System Center Configuration Manager versão 1706 coleta.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ee4fb0-7790-45a6-906e-6e55627d4079
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8ed8aed38f20adb3558b61dd32a36f88fbac3b00
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893501"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1706-of-system-center-configuration-manager"></a>Níveis da coleta de dados de diagnóstico e de uso da versão 1706 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager versão 1706 coleta três níveis de dados de diagnóstico e de uso: **Básico**, **Avançado** e **Completo**. Por padrão, esse recurso é definido no nível Avançado. As seções a seguir fornecem detalhes adicionais sobre os dados coletados por cada nível.

Alterações de versões anteriores são indicadas com ***[Novo]*** ou ***[Atualizado]***, ***[Removido]*** ou ***[Movido]***.


> [!IMPORTANT]
>  O Configuration Manager não coleta códigos do site, nomes de site, endereços IP, nomes de usuário, nomes de computador, endereços físicos nem endereços de email nos níveis Básico ou Avançado. Qualquer coleta dessas informações no nível Completo não é proposital, ou seja, é potencialmente incluída nas informações de diagnóstico avançado como arquivos de log ou instantâneos de memória. A Microsoft não usará essas informações para identificá-lo, contatá-lo nem para desenvolver publicidade.



##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que têm um escopo administrativo baseado em função que inclui permissões **Modificar** na classe de objeto **Site** podem alterar o nível dos dados coletados nas configurações de Dados de Diagnóstico e de Uso no console do Configuration Manager.

Você altera o nível da coleta de dados no console navegando até **Administração** > **Visão Geral** > **Configuração de Site** > **Sites**. Abra **Configurações da Hierarquia** e, em seguida, selecione o nível de dados que você deseja usar.  



##  <a name="bkmk_level1"></a> Nível 1 — Básico
O nível Básico inclui dados sobre sua hierarquia, dados necessários para ajudar a melhorar sua experiência de instalação ou de atualização e dados que ajudam a determinar as atualizações do Configuration Manager aplicáveis à sua hierarquia.

Para o System Center Configuration Manager versão 1706, esse nível inclui o seguinte:

- Console de administração:
   - Estatísticas sobre as conexões do console (versão de sistema operacional, idioma, SKU e arquitetura, memória do sistema, número de processadores lógicos, ID do site de conexão, versões do .NET instaladas e pacotes de idiomas do console)

- Contagens básicas de tipo de implantação e de aplicativo (total de aplicativos, total de aplicativos com vários tipos de implantação, total de aplicativos com dependências, total de aplicativos substituídos e contagem de tecnologias de implantação em uso)

- Dados básicos da hierarquia de sites do Configuration Manager (lista, tipo, versão, status, contagem de clientes e fuso horário de sites)

- Configuração básica do banco de dados (processadores, configuração de cluster e configuração de exibições distribuídas)

- Estatísticas básicas de descoberta (contagem de descoberta e tamanho de grupo mínimo/máximo/médio) incluindo quando o site está em execução completamente com os serviços de Azure Active Directory.

- Informações básicas do Endpoint Protection (versões de cliente de antimalware)

- Contagens básicas de OSD (implantação de sistema operacional) (imagens)

- ***[Atualizado]*** Informações básicas de servidor do sistema de sites (funções do sistema de sites usadas, status de Internet e SSL, sistema operacional, processadores, máquina virtual ou física e uso da alta disponibilidade do servidor de sites)

- Esquema de banco de dados do Configuration Manager (hash de todas as definições de objeto)

- Nível de telemetria configurado, modo (online ou offline) e configuração de atualização rápida

- Contagem de idiomas e localidades do cliente

- Contagem de versões de cliente do Configuration Manager e de versões do sistema operacional

- Contagem de sistemas operacionais em dispositivos gerenciados e políticas definidas pelo Exchange Connector

- Contagem de dispositivos com Windows 10 por ramificação e compilação

- Métricas de desempenho do banco de dados (informações de processamento de replicação, principais procedimentos armazenados do SQL Server por processador e uso de disco)

- Tipos de ponto de distribuição e de ponto de gerenciamento e informações básicas de configuração (protegidas, pré-teste, PXE, multicast, estado de SSL, pontos de distribuição de recepção e de pares, habilitado para MDM, habilitado para SSL, etc.)

- ***[Novo]***  Lista com hash de extensões para páginas de propriedade do console de administração e assistentes

- Informações de Instalação:
     - Build, tipo de instalação, pacotes de idiomas e recursos habilitados   

     - Uso pré-lançamento, tipo de mídia de instalação, tipo de ramificação

     - Data de validade do Software Assurance      

     - Status e erros de implantação do pacote de atualização, andamento do download e erros de pré-requisitos     

     - Uso do anel rápido de atualização

     - Versão do script pós-atualização

- Versão do SQL, nível do service pack, edição, ID de agrupamento e conjunto de caracteres     
- Estatísticas de telemetria (quando executar, tempo de execução, erros)

- Uso da Descoberta de Rede (habilitada ou desabilitada)




##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível Avançado é o padrão após a conclusão da instalação. Esse nível inclui dados coletados no nível Básico, dados específicos ao recurso (frequência e duração de uso), configurações de cliente do Configuration Manager (nome do componente, estado e algumas configurações como intervalos de sondagem) e informações básicas sobre atualizações de software.

Esse nível é recomendado porque fornece à Microsoft o mínimo de dados necessários para fazer melhorias úteis em versões futuras de produtos e serviços. Esse nível não coleta nomes de objeto (sites, usuários, computadores ou objetos), detalhes de objetos relacionados à segurança ou vulnerabilidades, como contagens de sistemas que exigem atualizações de software.

Para o System Center Configuration Manager versão 1706, esse nível inclui o seguinte:

- **Gerenciamento de aplicativos:**  

   - Requisitos de aplicativo (a contagem de condições internas é referenciada por tecnologia de implantação)

   - Substituição de aplicativo, profundidade máxima da cadeia

   - Estatísticas de aprovação de aplicativo e frequência de uso

   - ***[Novo]***  Estatísticas de tamanho do conteúdo do aplicativo

   - Informações de implantação de aplicativo (uso de instalação versus desinstalação, exigência de aprovação, habilitação/desabilitação da interação do usuário, dependência, substituição e uso do recurso de contagem do comportamento de instalação)  

   - Estatísticas de tamanho e complexidade da política de aplicativo

   - Estatísticas de solicitação de aplicativo disponíveis

   - Informações básicas de configuração para pacotes e programas (opções de implantação e os sinalizadores de programas)

   - Informações básicas de uso/direcionamento para os tipos de implantação usados na organização (usuário versus dispositivo direcionado, obrigatório versus disponível e aplicativos universais)

   - Estatísticas de grupos de limites (quantos são rápidos, quantos são lentos e contagem por grupo)

   - Contagem de ambientes do App-V e propriedades de implantação

   - Contagem de aplicabilidade de aplicativo por sistema operacional  

   - Contagem de aplicativos que são referenciados por uma sequência de tarefas

   - ***[Novo]*** Contagem de marcas distintas para o catálogo de aplicativos

   - ***[Novo]*** Contagem de aplicativos do Office 365 criados usando o painel

   - Contagem de pacotes por tipo  

   - Contagem de implantações de pacote/programa  

   - Contagem de licenças de aplicativos do Windows 10 licenciadas  

   - ***[Novo]*** Contagem de tipos de implantação do Windows Installer pelas configurações de conteúdo de desinstalação

   - Contagem de aplicativos Windows Store para Empresas e estatísticas de sincronização (incluindo tipos de aplicativos resumidos, status de aplicativos licenciados e número de aplicativos licenciados online e offline)  

   - Tipo e duração da janela de manutenção  

   - Número mínimo/máximo/médio de implantações de aplicativo por usuário/dispositivo por período

   - Códigos de erro mais comuns de instalação de aplicativo por tecnologia de implantação

   - Contagens e opções de configuração do MSI

   - Estatísticas na interação do usuário final com notificação para implantações de software necessárias   

   - Uso, como foi criado o UDA (Acesso a Dados Universal)




- **Cliente:**  

   - Versão do cliente do AMT (Active Management Technology)

   - Idade do BIOS em anos
   
   - ***[Novo]***  Contagem de dispositivos com a Inicialização Segura habilitada
   
   - ***[Novo]***  Contagem de dispositivos por estado de TPM

   - Atualização automática do cliente: configuração de implantação, incluindo piloto do cliente e uso de exclusão (cliente de interoperabilidade estendida)

   - Configuração de tamanho do cache do cliente

   - Erros de download da implantação do cliente

   - Estatísticas de integridade do cliente e resumo dos principais problemas

   - Status da ação de operação de notificação do cliente (quantas vezes cada uma é executada, número máximo de clientes de destino e taxa média de êxito)
   - Contagem de instalações do cliente de cada tipo de local de origem  

   - Contagem de falhas de instalação do cliente  

   - Contagem de dispositivos virtualizados pelo Hyper-V ou Azure  

   - Contagem de ações do Centro de Software   

   - Contagem de dispositivos habilitados para UEFI

   - Métodos de implantação usados para o cliente e contagem de clientes por método de implantação

   - Lista/contagem de agentes cliente habilitados  

   - Idade do sistema operacional em meses

   - Número de classes de inventário de hardware, regras de inventário de software e regras de coleta de arquivos

   - Estatísticas de atestado de integridade de dispositivo, incluindo os erros de código mais comuns, número de servidores locais e contagens de dispositivos em vários estados.



- **Serviços de Nuvem:**

  - ***[Novo]*** Estatísticas de descoberta do Azure Active Directory

  - ***[Atualização]*** Estatísticas de uso e de configuração do Gateway de Gerenciamento de Nuvem, incluindo contagens de regiões e ambientes, e estatísticas de autenticação/autorização

  - ***[Novo]*** Contagem de aplicativos e serviços do Azure Active Directory conectados ao Configuration Manager

  - Contagem de clientes associados aos serviços do Azure Active Directory

  - Contagem de coleções sincronizadas com o Azure Log Analytics

  - Contagem de Conectores do Upgrade Analytics

  - Se o conector de nuvem do Azure Log Analytics estiver habilitado ou não





- **Coleções:**

    - Uso de ID de coleção (com IDs suficientes)

    - Estatísticas de avaliação da coleção (tempo de consulta, contagens de atribuídos versus não atribuídos, contagens por tipo, substituição de ID e uso de regra)

    - Coleções sem uma implantação




- **Configurações de conformidade:**  

    - Informações de linha de base de configuração básica (contagem, número de implantações e número de referências)

    - ***[Novo]*** Estatísticas de erro da política de conformidade

    - Contagem de itens de configuração por tipo  

    - Contagem de implantações que fazem referência às configurações internas (a configuração de correção agora é capturada)  

    - Contagem de regras e implantações criadas para configurações personalizadas (a configuração de correção agora é capturada)  
    -  Contagem de protocolo SCEP, VPN, WiFi, certificado (.pfx) e modelos de Política de Conformidade implantados

    - Contagem implantações de certificados SCEP, VPN, Wi-Fi, certificado (.pfx) e de Política de Conformidade por plataforma

    - Política do Passport for Work (criada, implantada)



- **Conteúdo:**  

    - Informações de grupo de limites (contagem de limites e de sistemas de sites atribuídos a cada grupo de limites)  

    - Relações de grupos de limites e configuração de fallback

    - Estatísticas de download do conteúdo do cliente

    - Contagem de limites por tipo  

    - ***[Atualizado]*** Contagem de clientes de cache de pares, estatísticas de uso e estatísticas de download parcial

    - Informações de configuração do Gerenciador de Distribuição (threads, intervalo de repetição, número de repetições e configurações de pontos de distribuição de recepção)  

    - Informações de configuração de pontos de distribuição (uso do cache de ramificação e monitoramento do ponto de distribuição)

    - Informações de grupo de pontos de distribuição (contagem de pacotes e pontos de distribuição atribuídos a cada grupo de pontos de distribuição)  



- **Endpoint Protection:**  

   - Políticas ATP (Proteção Avançada contra Ameaças) (contagem de políticas e se as políticas são implantadas)

   - Contagem de alertas configurados para o recurso Endpoint Protection  

   - Contagem de coleções selecionadas para serem exibidas no painel do Endpoint Protection  

   - Erros de implantação do Endpoint Protection (contagem de códigos de erro de implantação da política do Endpoint Protection)  

   - Uso da política do Firewall do Windows e antimalware do Endpoint Protection (número de políticas exclusivas atribuídas ao grupo)<br /><br /> Isso não inclui informações sobre as configurações incluídas na política.  



- **Migração:**

  - Contagem de objetos migrados (uso do assistente de migração)



- **MDM (Gerenciamento de dispositivo móvel):**  

    - Contagem de ações de dispositivo móvel emitidas: comandos de bloquear, redefinição de PIN, apagar, desativar e sincronizar agora

    - Contagem de políticas de dispositivo móvel  

    - Contagem de dispositivos móveis gerenciados pelo Configuration Manager e pelo Microsoft Intune e como eles foram registrados (em massa, baseado no usuário)  

    - Contagem de usuários que têm vários dispositivos móveis registrados  

    - Agendamento de sondagem de dispositivo móvel e estatísticas de duração de check-in de dispositivos móveis  




- **Solução de problemas do Microsoft Intune:**

    - Contagem e tamanho das ações de dispositivo (apagar, desativar, bloquear), telemetria e mensagens de dados replicadas para o Microsoft Intune

    - Contagem e tamanho de estado, status, inventário, RDR, DDR, UDX, estado de Locatário, POL, LOG, Cert, CRP, Ressincronização, CFD, RDO, BEX, ISM e mensagens de conformidade baixadas do Microsoft Intune

    - Estatísticas de sincronização de usuário completa e delta para o Microsoft Intune



- **MDM (Gerenciamento de dispositivo móvel) local:**  

    - Contagem de perfis e pacotes de registro em massa do Windows 10  

    - Estatísticas de êxito/falha de implantação para implantações locais de aplicativo de MDM  




- **Implantação de sistema operacional:**  

    - Contagem de imagens de inicialização, drivers, pacotes de driver, pontos de distribuição habilitados para multicast, pontos de distribuição habilitados para PXE e sequências de tarefas  

    - ***[Novo]*** Contagem de imagens de inicialização pela versão do cliente do Configuration Manager

    - ***[Novo]*** Contagem de imagens de inicialização pela versão do Windows PE

    - Contagem de políticas de atualização de edição

    - ***[Novo]*** Contagem de identificadores de hardware excluídos do PXE

    - ***[Novo]*** Contagem de implantações de sequência de tarefas usando a opção para baixar o conteúdo previamente

    - Contagens de uso da etapa de sequência de tarefas

    - ***[Novo]*** Versão do Windows ADK instalada


- **Atualizações do site:**

    - Versões de hotfixes do Configuration Manager instalados



- **Atualizações de software:**  

    - Deltas disponíveis e de data limite usados nas regras de implantação automática  

    - Número médio e máximo de atribuições por atualização  

    - Avaliação da atualização de cliente e agendamentos de verificação  

    - Classificações sincronizadas pelo Ponto de Atualização de Software

    - Estatísticas de aplicação de patch de cluster  

    - Configuração de atualizações expressas do Windows 10

    - Configurações usadas para planos ativos de manutenção do Windows 10  

    - Contagem de atualizações do Office 365 implantadas  

    - ***[Novo]*** Contagem de drivers do Microsoft Surface sincronizados

    - Contagem de grupos de atualização e atribuições  

    - Contagem de pacotes de atualização e o número mínimo/máximo/médio de pontos de distribuição direcionados com pacotes  

    - Contagem de atualizações criadas e implantadas com o System Center Update Publisher  

    - Contagem de clientes do Windows 10 que usam o Windows Update para Empresas  

    - ***[Novo]*** Contagem do Windows Update para políticas de negócios criadas e implantadas

    - Número de regras de implantação automática vinculadas à sincronização  

    - Número de regras de implantação automática que criam ou adicionam atualizações a um grupo existente  

    - Número de regras de implantação automática que têm várias implantações  
    - Número de grupos de atualização e número mínimo/máximo/médio de atualizações por grupo  

    - Número de atualizações e percentual de atualizações implantadas, expiradas, substituídas, baixadas e que contêm EULAs  

    - Estatísticas de balanceamento de carga do ponto de atualização de software

    - Agendamento de sincronização do ponto de atualização de software  

    - Número total/médio de coleções que têm implantações de atualização de software e número máximo/médio de atualizações implantadas  

    - Códigos de erro de verificação de atualização e contagem de computadores  

    - Versões de conteúdo do painel do Windows 10  



- **Dados de desempenho/SQL:**  

    - ***[Novo]***  Configuração e duração do resumo do site

    - Contagem das maiores tabelas de banco de dados  

    - Estatísticas operacionais de descoberta (contagem de objetos encontrados)

    - Tipos de descoberta, habilitação e agendamento (completo, incremental)

    - Uso, status de integridade e informações de réplica do SQL AlwaysOn

    - Período de retenção, estado de limpeza automática e problemas de desempenho do controle de alterações do SQL

    - Período de retenção do controle de alterações do SQL

    - Estatísticas de desempenho de mensagem de estado e status, incluindo tipos de mensagens mais comuns e mais caras



- **Diversos**

    - Configuração do ponto de serviço do Data Warehouse incluindo agenda de sincronização e tempo médio

    - ***[Novo]*** Contagem de scripts e estatísticas de execução

    - Contagem de sites com WOL (Wake On LAN)

    - Estatísticas de desempenho e de uso de relatório  



##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível Completo inclui todos os dados nos níveis Básico e Avançado. Também inclui informações adicionais sobre o Endpoint Protection, o percentual de conformidade da atualização e as informações de atualização de software.  Esse nível também pode incluir informações de diagnóstico avançado, como arquivos do sistema e instantâneos de memória, que podem incluir informações pessoais que existiam na memória ou nos arquivos de log no momento da captura.

Para o System Center Configuration Manager versão 1706, esse nível inclui o seguinte:

- Informações de agendamento de avaliação da regra de implantação automática

- Resumo de Integridade do ATP

- Avaliação de coleta e estatísticas de atualização

- ***[Novo]*** Estatísticas de política de conformidade sobre conformidade e erros

- Configurações de conformidade: detalhes de configuração de: protocolo SCEP, VPN, Wi-Fi e de modelo de Política de Conformidade. Contagem de grupos que têm atualizações de software expiradas

- Pacote de configuração do DCM para uso do System Center Configuration Manager

- Erros detalhados de instalação de implantação de cliente

- Resumo de integridade do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e sem suporte)

- Configuração da política do Endpoint Protection

- Lista de processos configurados com comportamento da instalação para aplicativos

- Número mínimo/máximo/médio de horas desde a última verificação de atualização de software

- Número mínimo/máximo/médio de clientes inativos em coleções de implantação de atualização de software

- Número mínimo/máximo/médio de atualizações de software por pacote

- Código do produto MSI (aplicativos comuns que os clientes implantam)

- Conformidade geral de implantações de atualização de software

- Contagens e códigos de erro de implantação da atualização de software

- Informações de implantação de atualização de software (percentual de implantações direcionadas com o cliente versus hora UTC, obrigatório versus opcional versus silencioso e supressão de reinicialização)

- Produtos de atualização de software sincronizados pelo Ponto de Atualização de Software

- Percentuais de êxito de verificação da atualização de software

- As 50 principais CPUs no ambiente

- Tipo de políticas de Acesso Condicional EAS (bloqueio ou quarentena) para dispositivos que o Intune gerencia

- Detalhes de aplicativos da Windows Store para Empresas (lista sem agregação de aplicativos sincronizados, incluindo AppID, estado online ou offline e contagem total de licenças compradas)
