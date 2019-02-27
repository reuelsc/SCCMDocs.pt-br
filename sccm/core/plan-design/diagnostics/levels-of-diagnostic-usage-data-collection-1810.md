---
title: Dados de diagnóstico e uso para 1810
titleSuffix: Configuration Manager
description: Conheça os níveis de dados de diagnóstico e uso coletados na versão 1810.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bce9e299-7b3a-4f51-8863-a322877daa2c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 52c13109710fc35dcd2853f76188ac42269a8058
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120054"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1810"></a>Níveis de coleta de dados de uso de diagnóstico para a versão 1810

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager versão 1810 coleta três níveis de dados de diagnóstico e de uso: **Básico**, **Avançado** e **Completo**. Por padrão, esse recurso é definido no nível Avançado. As seções a seguir fornecem mais detalhes sobre os dados coletados em cada nível.

Alterações de versões anteriores são indicadas com ***[Novo]*** ou ***[Atualizado]***, ***[Removido]*** ou ***[Movido]***.


> [!IMPORTANT]
>  O Configuration Manager não coleta códigos do site, nomes de site, endereços IP, nomes de usuário, nomes de computador, endereços físicos nem endereços de email nos níveis Básico ou Avançado. Qualquer coleta dessas informações no nível Completo não é proposital. Ela é potencialmente incluída nas informações de diagnóstico avançado, como arquivos de log ou instantâneos de memória. A Microsoft não usa essas informações para identificá-lo, contatá-lo nem para desenvolver anúncios.



##  <a name="bkmk_change"></a> Como alterar o nível

Para alterar o nível de coleção de dados, você precisa de permissões para **Modificar** na classe de objeto **Site**. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**. Selecione **Configurações da Hierarquia** na faixa de opções e, em seguida, escolha o nível de dados nas configurações de diagnóstico e de dados.  



##  <a name="bkmk_level1"></a> Nível 1 — Básico
O nível básico inclui dados sobre sua hierarquia. É necessário para ajudar a melhorar sua experiência de instalação ou de atualização. Esses dados também ajudam a determinar as atualizações do Configuration Manager que são aplicáveis à sua hierarquia.

Para o Configuration Manager versão 1810, esse nível inclui os seguintes dados:

- Estatísticas sobre as conexões de console do Configuration Manager: versão do sistema operacional, idioma, SKU e arquitetura, memória do sistema, número de processadores lógicos, ID do site de conexão, versões do .NET instaladas e pacotes de idiomas do console

- Contagens básicas de tipo de implantação e de aplicativo: total de aplicativos, total de aplicativos com vários tipos de implantação, total de aplicativos com dependências, total de aplicativos substituídos e contagem de tecnologias de implantação em uso

- Dados básicos da hierarquia de sites do Configuration Manager: lista de sites, tipo, versão, status, contagem de clientes e fuso horário

- ***[Atualizado]***  Configuração básica do banco de dados: processadores, tamanho da memória, configurações de memória, configuração de banco de dados do Configuration Manager, tamanho do banco de dados do Configuration Manager, configuração de cluster, configuração de exibições distribuídas e versão de controle de alterações  

- Estatísticas básicas de descoberta: contagem de descobertas, tamanho mínimo/máximo/médio de grupos e quando o site está em execução completamente com os Serviços do Azure Active Directory

- Informações básicas do Endpoint Protection sobre versões de cliente de antimalware

- Contagens básicas de imagens de implantação de sistema operacional

- Informações básicas do servidor do sistema de sites: funções do sistema de sites usadas, status da Internet e do SSL, sistema operacional, processadores, máquina virtual ou física e uso da alta disponibilidade do servidor do site

- Esquema de banco de dados do Configuration Manager (hash de todas as definições de objeto)

- Nível configurado para dados de uso e diagnóstico, modo online ou offline e configuração de atualização rápida

- Contagem de idiomas e localidades do cliente

- Contagem de versões de cliente do Configuration Manager, versões de sistema operacional e versões do Office

- Contagem de sistemas operacionais em dispositivos gerenciados e políticas definidas pelo Exchange Connector

- ***[Atualizado]***  Contagem de dispositivos do Windows 10 por branch, build e floresta exclusiva do Active Directory  

- Contagem de clientes do Windows 10 que usam o Windows Update para Empresas  

- Métricas de desempenho do banco de dados: informações de processamento de replicação, principais procedimentos armazenados do SQL Server por processador e uso de disco

- Tipos de ponto de distribuição e de ponto de gerenciamento e informações básicas de configuração: protegido, pré-teste, PXE, multicast, estado de SSL, pontos de distribuição pull e de pares, habilitado para MDM e habilitado para SSL

- Lista com hash de extensões para páginas de propriedades do console de administração e assistentes

- Informações de Instalação:  

    - Build, tipo de instalação, pacotes de idiomas e recursos habilitados   

    - Uso pré-lançamento, tipo de mídia de instalação, tipo de ramificação  

    - Data de validade do Software Assurance  

    - Status e erros de implantação do pacote de atualização, andamento do download e erros de pré-requisitos  

    - Uso do anel rápido de atualização  

    - Versão do script pós-atualização  

- Versão do SQL, nível do service pack, edição, ID de ordenação e conjunto de caracteres  

- Estatísticas de diagnóstico e dados de uso: quando executar, tempo de execução, erros  

- Se a descoberta de rede está habilitada ou desabilitada  

- Contagem de clientes que ingressaram no Azure Active Directory  

- Contagem de implantações em fases criadas por tipo  

- Contagem de clientes de interoperabilidade estendida  

- Lista com hash de propriedades de inventário de hardware com mais de 255 caracteres  

- Contagem de clientes por método de registro de cogerenciamento  

- Estatísticas de erro do registro de cogerenciamento  

- Contagem de clientes por idade do sistema operacional Windows para o intervalo de três meses mais próximo  

- ***[Atualizado]***  10 principais nomes de processadores usados em clientes e servidores  

- Contagem e taxas de processamento de objetos chave do Configuration Manager: DDR (registros de dados de descoberta), mensagens de estado, mensagens de status, inventário de hardware, inventário de software e contagem total de arquivos em caixas de entrada  

- Informações de desempenho de processador e disco do servidor do site  

- Informações de uso de memória e tempo de atividade para processos do servidor do site do Configuration Manager  

- Contagem de falhas para processos do servidor do site do Configuration Manager e ID de assinatura do Watson se disponível  

- ***[Novo]***  Lista com hash de principais consultas SQL por contagem de bloqueio e de uso de memória  

- ***[Movido, atualizado]***  Estatísticas agregadas de cogerenciamento: número de clientes já registrados, número de clientes registrados, número de clientes com registro pendente, clientes que recebem a política, estados da carga de trabalho, tamanhos da coleção de piloto/exclusão e registro erros  



##  <a name="bkmk_level2"></a> Nível 2 - Avançado

O nível Avançado é o padrão após a conclusão da instalação. Esse nível inclui dados coletados no nível básico e dados específicos do recurso. Ele mostra a frequência e a duração de uso de recursos diferentes. Também inclui dados de configurações do cliente do Configuration Manager: nome do componente, estado e algumas configurações como intervalos de sondagem. Informações sobre atualizações de software são básicas sobre uso, nenhum dado em relação à conformidade de atualizações.

A Microsoft recomenda esse nível porque fornece o mínimo de dados para fazer aperfeiçoamentos de produtos e serviços. Esse nível não coleta nomes de objeto (sites, usuários, computadores ou objetos), detalhes de objetos relacionados à segurança ou vulnerabilidades, como contagens de sistemas que exigem atualizações de software.

Para o Configuration Manager versão 1810, esse nível inclui os seguintes dados:

### <a name="application-management"></a>Gerenciamento de aplicativos  

- Requisitos de aplicativo: a contagem de condições internas é referenciada por tecnologia de implantação  

- Substituição de aplicativo, profundidade máxima da cadeia  

- Estatísticas de aprovação de aplicativo e frequência de uso  

- Estatísticas de tamanho do conteúdo do aplicativo  

- Informações de implantação do aplicativo: uso de instalação versus desinstalação, necessidade de aprovação, habilitação/desabilitação da interação do usuário, dependência, substituição e contagem de uso do recurso de comportamento da instalação  

- Estatísticas de tamanho e complexidade da política de aplicativo  

- Estatísticas de solicitação de aplicativo disponíveis  

- Informações básicas de configuração para pacotes e programas: opções de implantação e sinalizadores de programas  

- Informações básicas de uso/direcionamento para tipos de implantação: usuário versus dispositivo direcionado, obrigatório versus disponível e aplicativos universais  

- Contagem de ambientes do App-V e propriedades de implantação  

- Contagem de aplicabilidade de aplicativo por sistema operacional  

- Contagem de aplicativos referenciado em uma sequência de tarefas  

- Contagem de marcas distintas do catálogo de aplicativos  

- Contagem de aplicativos do Office 365 criados usando o painel  

- Contagem de pacotes por tipo  

- Contagem de implantações de pacote/programa  

- Contagem de licenças de aplicativos do Windows 10 licenciadas  

- Contagem de tipos de implantação do Windows Installer pelas configurações de conteúdo de desinstalação  

- Contagem de aplicativos da Microsoft Store para Empresas e estatísticas de sincronização: tipos de aplicativos resumidos, status de aplicativos licenciados e número de aplicativos licenciados online e offline  

- Tipo e duração da janela de manutenção  

- Número mínimo/máximo/médio de implantações de aplicativo por usuário/dispositivo por período  

- Códigos de erro mais comuns de instalação de aplicativo por tecnologia de implantação  

- Contagens e opções de configuração do MSI  

- Estatísticas na interação do usuário final com notificação para implantações de software necessárias  

- Uso do Acesso a Dados Universal, como foi criado  

- Estatísticas agregadas de afinidade de dispositivo de usuário  

- Máximo e média de usuários primários por dispositivo  

- Uso de condição global de aplicativo por tipo  

- Configuração de personalização do Centro de Software  

- Contagens e prontidão do Gerenciador de Conversões de Pacotes  

- Contagem de métodos de detecção de aplicativo por tipo  

- Contagem de erros de imposição do aplicativo  

- Propriedades do instalador MSI  

- Estatísticas de solicitações de instalação do usuário  

- ***[Novo]***  Estatísticas agregadas sobre o uso do recurso de aprovação de email  

- ***[Novo]***  Contagem, tamanho do conteúdo, contagem de serviços e contagem de ação personalizada de MSIs no catálogo de aplicativos  


### <a name="client"></a>Cliente  

- Versão do cliente do AMT (Active Management Technology)  

- Idade do BIOS em anos  

- Contagem de dispositivos com a Inicialização Segura habilitada  

- Contagem de dispositivos por estado do TPM  

- Atualização automática do cliente: configuração de implantação, incluindo piloto do cliente e uso de exclusão (cliente de interoperabilidade estendida)  

- Configuração de tamanho do cache do cliente  

- Erros de download da implantação do cliente  

- Estatísticas de integridade do cliente e resumo de principais problemas por versão do cliente  

- Status da ação de operação de notificação do cliente: quantas vezes cada uma é executada, número máximo de clientes direcionados e taxa média de êxito  

- Contagem de instalações do cliente de cada tipo de local de origem  

- Contagem de falhas de instalação do cliente  

- Contagem de dispositivos virtualizados pelo Hyper-V ou Azure  

- Contagem de ações do Centro de Software  

- Contagem de dispositivos habilitados para UEFI  

- Métodos de implantação usados para o cliente e contagem de clientes por método de implantação  

- Lista/contagem de agentes cliente habilitados  

- Idade do sistema operacional em meses  

- Número de classes de inventário de hardware, regras de inventário de software e regras de coleta de arquivos  

- Estatísticas de atestado de integridade do dispositivo: os erros de código mais comuns, número de servidores locais e contagens de dispositivos em vários estados  

- Contagem de dispositivos por navegador padrão  

- Contagem de certificados de autenticação de servidor gerados pelo Configuration Manager  

- Contagem de dispositivos do Microsoft Surface por modelo  


### <a name="cloud-services"></a>Cloud Services  

- Estatísticas de descoberta do Azure Active Directory  

- Estatísticas de uso e de configuração do Gateway de Gerenciamento de Nuvem: contagens de regiões e ambientes e estatísticas de autenticação/autorização  

- Contagem de aplicativos e serviços do Azure Active Directory conectados ao Configuration Manager  

- Contagem de coleções sincronizadas com o Azure Log Analytics  

- Contagem de Conectores do Upgrade Analytics  

- Se o conector de nuvem do Azure Log Analytics estiver habilitado ou não  

- Contagem de pontos de distribuição de pull com um ponto de distribuição na nuvem como localização de origem  


### <a name="cmpivot"></a>CMPivot

- Estatísticas de uso do CMPivot  

- ***[Novo]***  Contagem de consultas de CMPivot salvas  

- ***[Novo]***  Total de consultas por tipo de entidade  


### <a name="co-management"></a>Cogerenciamento  

- Estatísticas históricas e de agendamento de registro  

- Contagem de clientes qualificados para o cogerenciamento  

- Locatário associado do Microsoft Intune  


### <a name="collections"></a>Coleções  

- Uso de ID de coleção (com IDs suficientes)  

- Estatísticas de avaliação da coleção: tempo de consulta, contagens de atribuídos versus não atribuídos, contagens por tipo, substituição de ID e uso de regra  

- Coleções sem uma implantação  


### <a name="compliance-settings"></a>Configurações de conformidade  

- Informações básicas de linha de base de configuração: contagem, número de implantações e número de referências  

- Estatísticas de erro de política de conformidade  

- Contagem de itens de configuração por tipo  

- Contagem de implantações que referenciam configurações internas, incluindo a configuração de correção  

- Contagem de regras e implantações criadas para configurações personalizadas, incluindo a configuração de correção  

- Contagem de protocolos SCEP, VPN, Wi-Fi, certificados (.pfx) e modelos de política de conformidade implantados  

- Contagem de implantações de certificado SCEP, VPN, Wi-Fi, certificado (.pfx) e política de conformidade por plataforma  

- Política do Windows Hello para Empresas (criada, implantada)  

- Contagem de políticas de navegador Microsoft Edge implantadas  


### <a name="content"></a>Conteúdo  

- Estatísticas de grupos de limites: contagem de quantos estavam rápidos, contagem de quantos estavam lentos, contagem por grupo e relações de fallback  

- Informações de grupos de limites: contagem de limites e de sistemas de sites atribuídos a cada grupo de limites  

- Relações de grupos de limites e configuração de fallback  

- Estatísticas de download do conteúdo do cliente  

- Contagem de limites por tipo  

- Contagem de clientes de cache pares, estatísticas de uso e estatísticas de download parcial  

- Informações de configuração do Gerenciador de Distribuição: threads, intervalo de repetição, número de repetições e configurações de pontos de distribuição pull  

- Informações de configuração dos pontos de distribuição: uso do cache de branch e monitoramento do ponto de distribuição  

- Informações dos grupos de pontos de distribuição: contagem de pacotes e pontos de distribuição atribuídos a cada grupo de pontos de distribuição  

- Tipo de biblioteca de conteúdo local ou remota  

- ***[Novo]***  Contagem de grupos de limite por configuração  


### <a name="endpoint-protection"></a>Endpoint Protection  

- Políticas de ATP (Proteção Avançada contra Ameaças) do Windows Defender: contagem de políticas e se as políticas foram implantadas  

- Contagem de alertas configurados para o recurso Endpoint Protection  

- Contagem de coleções selecionadas para serem exibidas no painel do Endpoint Protection  

- Contagem de políticas, implantações e clientes direcionados do Windows Defender Exploit Guard  

- Erros de implantação do Endpoint Protection, contagem de códigos de erro de implantação da política do Endpoint Protection  

- Uso da política do Firewall do Windows e antimalware do Endpoint Protection (número de políticas exclusivas atribuídas ao grupo). Esses dados não incluem informações sobre as configurações incluídas na política.  


### <a name="migration"></a>Migração  

- Contagem de objetos migrados (uso do assistente de migração)  


### <a name="mobile-device-management-mdm"></a>MDM (gerenciamento de dispositivo móvel)  

- Contagem de ações de dispositivo móvel emitidas: comandos de bloquear, redefinição de PIN, apagar, desativar e sincronizar agora  

- Contagem de políticas de dispositivo móvel  

- Contagem de dispositivos móveis do Configuration Manager e de gerenciamentos do Microsoft Intune e como você os registrou (em massa, baseado no usuário)  

- Contagem de usuários que têm vários dispositivos móveis registrados  

- Agendamento de sondagem de dispositivo móvel e estatísticas de duração de check-in de dispositivos móveis  


### <a name="microsoft-intune-troubleshooting"></a>Solução de problemas do Microsoft Intune  

- Contagem e tamanho das ações de dispositivo (apagar, desativar, bloquear), dados de uso e mensagens de dados replicadas para o Microsoft Intune  

- Contagem e tamanho de estado, status, inventário, RDR, DDR, UDX, estado de Locatário, POL, LOG, Cert, CRP, Ressincronização, CFD, RDO, BEX, ISM e mensagens de conformidade baixadas do Microsoft Intune  

- Estatísticas de sincronização de usuário completa e delta para o Microsoft Intune  


### <a name="on-premises-mobile-device-management-mdm"></a>MDM (Gerenciamento de dispositivos móveis) local  

- Contagem de perfis e pacotes de registro em massa do Windows 10  

- Estatísticas de êxito/falha de implantação para implantações locais de aplicativo de MDM  


### <a name="os-deployment"></a>Implantação de sistema operacional  

- Contagem de imagens de inicialização, drivers, pacotes de driver, pontos de distribuição habilitados para multicast, pontos de distribuição habilitados para PXE e sequências de tarefas  

- Contagem de imagens de inicialização por versão de cliente do Configuration Manager  

- Contagem de imagens de inicialização por versão do Windows PE  

- Contagem de políticas de atualização de edição  

- Contagem de identificadores de hardware excluídos do PXE  

- Contagem de implantações de sistema operacional por versão de sistema operacional  

- Contagem de atualizações de sistema operacional ao longo do tempo  

- Contagem de implantações de sequência de tarefas usando a opção de baixar conteúdo previamente  

- Contagens de uso da etapa de sequência de tarefas  

- Versão do Windows ADK instalada  

- Contagem de tarefas de manutenção de imagem  

- ***[Novo]***  Contagem de computadores importados  


### <a name="site-updates"></a>Atualizações do site  

- Versões de hotfixes do Configuration Manager instalados  


### <a name="software-updates"></a>Atualizações de software  

- Deltas disponíveis e de data limite usados nas regras de implantação automática  

- Número médio e máximo de atribuições por atualização  

- Avaliação da atualização de cliente e agendamentos de verificação  

- Classificações sincronizadas pelo ponto de atualização de software  

- Estatísticas de aplicação de patch de cluster  

- Configuração de atualizações expressas do Windows 10  

- Configurações usadas para planos ativos de manutenção do Windows 10  

- Contagem de atualizações do Office 365 implantadas  

- Contagem de drivers do Microsoft Surface sincronizados  

- Contagem de grupos de atualização e atribuições  

- Contagem de pacotes de atualização e o número mínimo/máximo/médio de pontos de distribuição direcionados com pacotes  

- Contagem de atualizações criadas e implantadas com o System Center Update Publisher  

- Contagem de políticas do Windows Update para Empresas criadas e implantadas  

- Estatísticas agregadas das configurações do Windows Update para Empresas  

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

- Contagem de assinaturas e uso de catálogo de atualização de software de terceiros  

- Contagem de atualizações de software implantadas com e sem conteúdo  

- ***[Novo]*** Estatísticas agregadas sobre o número de atualizações UUP necessárias, implantadas, expiradas, substituídas e baixadas  

- ***[Novo]*** Uso de categorias de produto UUP  

- ***[Novo]***  Contagem de clientes que implantaram pelo menos uma atualização de qualidade UUP ou atualização de recurso UUP  

- ***[Novo]***  Códigos de erro UUP superiores e contagem de dispositivos afetados  


### <a name="sqlperformance-data"></a>Dados de desempenho/SQL  

- Configuração e duração do resumo do site  

- Contagem das maiores tabelas de banco de dados  

- Estatísticas operacionais de descoberta (contagem de objetos encontrados)  

- Tipos de descoberta, habilitação e agendamento (completo, incremental)  

- Uso, status de integridade e informações de réplica do SQL AlwaysOn  

- Período de retenção, estado de limpeza automática e problemas de desempenho do controle de alterações do SQL  

- Período de retenção do controle de alterações do SQL  

- Estatísticas de desempenho de mensagem de estado e status, incluindo tipos de mensagens mais comuns e mais caras  

- ***[Novo]***  Estatísticas de tráfego de ponto de gerenciamento (total de bytes enviados e recebidos pelo ponto de extremidade)  

- ***[Novo]***  Medidas do contador de desempenho do ponto de gerenciamento  


### <a name="miscellaneous"></a>Diversos  

- Configuração do ponto de serviço do data warehouse, incluindo agendamento de sincronização e tempo médio  

- Contagem de scripts e estatísticas de execução  

- Contagem de sites com WOL (Wake On LAN)  

- Estatísticas de desempenho e de uso de relatório  

- Estatísticas de uso da implantação em fases  

- Contagens e o progresso de item de insights de gerenciamento  

- Contagem de falhas para processos exclusivos não do Configuration Manager no servidor do site e ID da assinatura do Watson se disponível  



##  <a name="bkmk_level3"></a> Nível 3 - Completo

O nível Completo inclui todos os dados nos níveis Básico e Avançado. Também inclui informações adicionais sobre o Endpoint Protection, o percentual de conformidade da atualização e as informações de atualização de software. Esse nível também pode incluir informações de diagnóstico avançadas, como arquivos do sistema e instantâneos de memória. Esses dados avançados podem incluir informações pessoais existem na memória ou em arquivos de log no momento da captura.

Para o Configuration Manager versão 1810, esse nível inclui os seguintes dados:

- Informações de agendamento de avaliação da regra de implantação automática  

- Resumo de integridade do ATP  

- Avaliação de coleta e estatísticas de atualização  

- Estatísticas de política de conformidade em relação a conformidade e erros  

- Configurações de conformidade: Detalhes de configuração do modelo de SCEP, VPN, Wi-Fi e de política de conformidade  

- Pacote de configuração do DCM para uso do Configuration Manager  

- Erros detalhados de instalação de implantação de cliente  

- Resumo de integridade do Endpoint Protection: incluindo contagem de clientes protegidos, em risco, desconhecidos e não compatíveis  

- Configuração da política do Endpoint Protection  

- Lista de processos configurados com comportamento da instalação para aplicativos  

- Número mínimo/máximo/médio de horas desde a última verificação de atualização de software  

- Número mínimo/máximo/médio de clientes inativos em coleções de implantação de atualização de software  

- Número mínimo/máximo/médio de atualizações de software por pacote  

- Estatísticas de implantação de código de produto MSI  

- Conformidade geral de implantações de atualização de software  

- Contagem de grupos que têm atualizações de software expiradas  

- Contagens e códigos de erro de implantação da atualização de software  

- Informações de implantação de atualização de software: percentual de implantações direcionadas com o cliente versus hora UTC, obrigatório versus opcional versus silencioso e supressão de reinicialização  

- Produtos de atualização de software sincronizados por ponto de atualização de software  

- Percentuais de êxito de verificação da atualização de software  

- As 50 principais CPUs no ambiente  

- Tipo de políticas de acesso condicional (bloquear ou colocar em quarentena) do EAS (Exchange Active Sync) para dispositivos gerenciados pelo Microsoft Intune  

- Detalhes de aplicativos da Microsoft Store para Empresas: lista sem agregação de aplicativos sincronizados, incluindo AppID, estado online ou offline e contagens totais de licenças compradas  

- ***[Novo]***  Contagem de clientes cujo push foi efetuado com opção de não permitir fallback para NTLM  
