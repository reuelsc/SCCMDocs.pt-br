---
title: Planejar o gateway de gerenciamento de nuvem | Microsoft Docs
description: 
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: d3e658714c30a1eba64f94e248d5e11095ca1dcb
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2017
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planejar o gateway de gerenciamento de nuvem no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Começando da versão 1610, o gateway de gerenciamento de nuvem fornece uma maneira simples de gerenciar clientes do Configuration Manager na Internet. O serviço de gateway de gerenciamento de nuvem é implantado no Microsoft Azure e requer uma assinatura do Azure. Ele se conecta à sua infraestrutura local do Configuration Manager usando uma nova função chamada ponto de conexão do gateway de gerenciamento de nuvem. Após ser implantado e configurado, os clientes poderão acessar funções locais do sistema de sites do Configuration Manager independentemente se eles estão na rede privada interna ou na Internet.

> [!TIP]  
> A partir da versão 1610, o gateway de gerenciamento de nuvem é um recurso de pré-lançamento. Para habilitá-lo, confira [Use pre-release features from updates](/sccm/core/servers/manage/pre-release-features) (Usar recursos de pré-lançamento de atualizações).

Use o console do Configuration Manager para implantar o serviço no Azure, adicione a função de ponto de conexão do gateway de gerenciamento de nuvem e configure as funções do sistema de sites para permitir o tráfego do gateway de gerenciamento de nuvem. No momento, o gateway de gerenciamento de nuvem dá suporte apenas às funções de ponto de gerenciamento e de ponto de atualização de software.

Os certificados de cliente e os certificados SSL são necessários para autenticar computadores e criptografar comunicações entre diferentes camadas do serviço. Normalmente, os computadores cliente recebem um certificado do cliente por meio da aplicação de política de grupo. Para criptografar o tráfego entre clientes e o servidor do sistema de sites hospedando as funções, você precisa criar um certificado SSL personalizado por meio da AC. Você também precisa configurar um certificado de gerenciamento no Azure que permita que o Configuration Manager implante o serviço de gateway de gerenciamento de nuvem.

## <a name="requirements-for-cloud-management-gateway"></a>Requisitos para o gateway de gerenciamento de nuvem

-   Computadores cliente e o servidor do sistema de sites que está executando o ponto de conexão do gateway de gerenciamento de nuvem.

-   Certificados SSL personalizados da AC interna – Usado para criptografar a comunicação de computadores cliente e autenticar a identidade do serviço de gateway de gerenciamento de nuvem.

-   Assinatura do Azure para serviços de nuvem.

-   Certificado de gerenciamento do Azure – usado para autenticar o Configuration Manager com o Azure.

## <a name="specifications-for-cloud-management-gateway"></a>Especificações para o gateway de gerenciamento de nuvem

- Cada instância do gateway de gerenciamento de nuvem oferece suporte a 4.000 clientes.
- É recomendável que você crie pelo menos duas instâncias do gateway de gerenciamento de nuvem para aumentar a disponibilidade.
- O gateway de gerenciamento de nuvem dá suporte apenas às funções de ponto de gerenciamento e de ponto de atualização de software.
-   No momento, os seguintes recursos não têm suporte no Configuration Manager para o gateway de gerenciamento de nuvem:

    -   Implantação do cliente
    -   Atribuição automática de site
    -   Políticas de usuário
    -   Catálogo de aplicativos (incluindo solicitações de aprovação de software)
    -   OSD (implantação de sistema operacional) completa
    -   Console do Configuration Manager
    -   Ferramentas remotas
    -   Site de relatórios
    -   Wake on LAN
    -   Clientes Mac, Linux e UNIX
    -   Azure Resource Manager
    -   Cache de pares
    -   Gerenciamento de dispositivo móvel local

## <a name="cost-of-cloud-management-gateway"></a>Custo do gateway de gerenciamento de nuvem

>[!IMPORTANT]
>As informações de custo fornecidas abaixo são apenas para fins de estimativa. Seu ambiente pode ter outras variáveis que afetam o custo geral do uso do gateway de gerenciamento de nuvem.

O gateway de gerenciamento de nuvem usa a seguinte funcionalidade do Microsoft Azure, que resulta em encargos para a conta de assinatura do Azure:

-   Máquina virtual

    -   O gateway de gerenciamento de nuvem atualmente requer uma máquina virtual Standard\_A2. Ao criar o serviço, você pode selecionar quantas VMs para dar suporte ao serviço (uma é o padrão).

    -   Apenas para fins de estimativa, estime que uma única máquina virtual Standard\_A2 do Azure pode dar suporte a aproximadamente 2.000 clientes baseados na Internet simultâneos.

    -   Consulte a [Calculadora de preços do Azure](https://azure.microsoft.com/en-us/pricing/calculator/) para ajudar a determinar os possíveis custos.

      >[!NOTE]
      >Os custos de máquina virtual variam de acordo com a região.

-   Transferência de dados de saída

    -   Há cobrança para dados saindo do serviço. Consulte os [Detalhes de preços de largura de banda do Azure](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para ajudar a determinar os possíveis custos.

    -   Apenas para fins de estimativa, estime aproximadamente 100 MB por cliente por mês para clientes baseados na Internet realizando atualizações de política a cada hora.

    >[!NOTE]
    > Executar outras ações com suporte por meio do gateway de gerenciamento de nuvem (por exemplo, implantar atualizações de software ou aplicativos) aumentará a quantidade de transferência de dados de saída do Azure.

-   Armazenamento de conteúdo

    -   Os clientes baseados na Internet gerenciados com o gateway de gerenciamento de nuvem obterão o conteúdo da atualização de software do Windows Update sem custo.

    -   Qualquer outro conteúdo necessário (por exemplo, aplicativos) deve ser distribuído para um ponto de distribuição baseado em nuvem. No momento, o gateway de gerenciamento de nuvem dá suporte apenas ao Ponto de Distribuição na Nuvem para enviar conteúdo para clientes.

    - Consulte o custo do uso de uma [distribuição baseada em nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution) para obter mais detalhes.

## <a name="frequently-asked-questions-about-the-cloud-management-gateway-cmg"></a>Perguntas frequentes sobre o CMG (Gateway de gerenciamento de nuvem)

### <a name="why-use-the-cloud-management-gateway"></a>Por que usar o gateway de gerenciamento de nuvem?

Use esta função para simplificar o gerenciamento de clientes baseado na Internet em três etapas no console do Configuration Manager.

1. Implante o CMG no Azure usando o assistente [Criar Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway).
2. Configure a função de sistema de site [ponto de conexão do gateway de gerenciamento de nuvem](/sccm/core/servers/deploy/configure/install-site-system-roles).
3. [Configure funções para o tráfego de gateway de gerenciamento na nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic), como o ponto de gerenciamento e o ponto de atualização de software.

### <a name="how-does-the-cloud-management-gateway-work"></a>Como funciona o gateway de gerenciamento de nuvem?

- O ponto de conexão do gateway de gerenciamento de nuvem permite uma conexão consistente e de alto desempenho da Internet para o gateway de gerenciamento de nuvem.
- O Configuration Manager publica configurações no CMG, incluindo informações de conexão e configurações de segurança.
- O CMG autentica e encaminha as solicitações de cliente do Configuration Manager para o ponto de conexão do gateway de gerenciamento de nuvem. Essas solicitações são encaminhadas para funções na rede corporativa de acordo com mapeamentos de URL.

### <a name="how-is-the-cloud-management-gateway-deployed"></a>Como o gateway de gerenciamento de nuvem é implantado?

O componente do gerenciador de serviço de nuvem no ponto de conexão de serviço lida com todas as tarefas de implantação de CMG. Além disso, ele monitora e reporta informações de integridade e de registro em log do serviço do Azure AD.

#### <a name="certificate-requirements"></a>Requisitos de certificado

Você precisará dos seguintes certificados para proteger o CMG:

- **Certificado de gerenciamento** – pode ser qualquer certificado, incluindo certificados autoassinados. Use um certificado público carregado no Azure AD ou um [PFX com chave privada](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) importado no Configuration Manager a fim de autenticar com o Azure AD.
- **Certificado de serviço Web** – recomendamos que você use um certificado de autoridade de certificação público para ganhar a confiança nativa dos clientes. O CName precisa ser criado na registar de DNS público. Não há suporte para certificados curinga.
- **Carregamento de certificados Raiz/SubCA no CMG** – o CMG precisa realizar uma validação completa da cadeia em certificados PKI do cliente. Se você usar uma autoridade de certificação corporativa para emissão de certificados PKI do cliente, e a autoridade de certificação raiz ou subordinada dele não estiver disponível na internet, você deverá carregá-lo no CMG.

#### <a name="deployment-process"></a>Processo de implantação

A implantação é dividida em duas fases:

- Implantar o serviço de nuvem
    - Carregue seu arquivo de [Esquema de Definição de Serviço do Azure](https://msdn.microsoft.com/library/azure/ee758711.aspx) (csdef)
    - Carregue seu arquivo de [Esquema de Configuração de Serviço do Azure](https://msdn.microsoft.com/library/azure/ee758710.aspx) (cscfg).
- Configurar o componente CMG em seu servidor do Azure AD, e configurar pontos de extremidade, manipuladores HTTP e serviços no ISS (Serviços de Informações da Internet)

Se você alterar a configuração do CMG, uma implantação de configuração será iniciada para o CMG.

### <a name="how-does-the-cloud-management-gateway-help-ensure-security"></a>Como o gateway de gerenciamento de nuvem ajuda a garantir a segurança?

O CMG ajuda a garantir a segurança das seguintes maneiras:

- Aceita e gerencia conexões de pontos de conexão CMG, incluindo a autenticação mútua de SSL usando certificados internos e IDs de conexão.
- Aceita e encaminha as solicitações de cliente
    - Pré-autentica as conexões usando SSL mútua no certificado PKI do cliente.
    - A lista de certificados confiáveis verifica a raiz do certificado PKI do cliente. Especifique essa configuração nas configurações de comunicação do cliente nas propriedades do site. Também executa a mesma validação como ponto de gerenciamento para o cliente.
    - Valida URLs recebidas
    - Filtra as URLs recebidas para verificar se algum ponto de conexão de CMG pode atender à solicitação da URL.  
    - Verifica a seleção de tamanho de conteúdo para cada ponto de extremidade de publicação.
    - Usa 'round-robin' para balancear a carga entre os pontos de conexão de CMG do mesmo site.

- Protege o ponto de conexão de CMG
    - Compila conexões HTTP/TCP consistentes para todas as instâncias virtuais do CMG em conexão. Verifica e mantém conexões a cada minuto.
    - Autentica mutuamente a autenticação SSL com CMG usando certificados internos.
    - Encaminha solicitações HTTP com base nos mapeamentos de URL.
    - Reporta o status de conexão para mostrar o status de integridade do serviço de administração.
    - Reporta o tráfego de ponto de extremidade por ponto de extremidade a cada cinco minutos.

- Protege as funções voltadas para o cliente do Configuration Manager do ponto de extremidade de publicação, como o ponto de gerenciamento, e pontos de extremidade host do ponto de atualização de software em solicitações do IIS para o cliente do serviço. Cada ponto de extremidade publicado no CMG tem um mapeamento de URL.
A URL externa é aquela usada pelo cliente para se comunicar com o CMG.
A URL interna é o ponto de conexão de CMG usado para encaminhar solicitações para o servidor interno.

#### <a name="example"></a>Exemplo:
Quando você habilita o tráfego CMG em um ponto de gerenciamento, o Configuration Manager cria internamente um conjunto de mapeamentos de URL para cada servidor de ponto de gerenciamento, como ccm_system, ccm_incoming e sms_mp.
A URL externa do ponto de extremidade do ponto de gerenciamento ccm_system pode parecer com **https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System**.
A URL é exclusiva para cada ponto de gerenciamento. Depois, o cliente do Configuration Manager coloca o nome de MP habilitado para CMG como **<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>** em sua lista de pontos de gerenciamento da internet.
Todas as URLs externas publicadas são carregadas automaticamente no CMG, assim o CMG é capaz de fazer a filtragem de URL. Todo o mapeamento de URL é replicado no ponto de conexão de CMG, para que ele possa encaminhar para servidores internos de acordo com a URL externa de solicitação do cliente.

### <a name="what-ports-are-used-by-the-cloud-management-gateway"></a>Quais portas são usadas pelo gateway de gerenciamento de nuvem?

- Nenhuma porta de entrada é necessária na rede local. A implantação de CMG criará automaticamente um grupo no CMG.
- Além da 443, algumas portas de saída são exigidas pelo ponto de conexão do CMG.

|||||
|-|-|-|-|
|Fluxo de dados|Servidor|Portas do servidor|Cliente|
|Implantação de CMG|Azure|443|Ponto de conexão de serviço do Configuration Manager|
|Compilar canal de CMG|CMG|Instância da VM: 1 Porta: 443<br>Instância da VM: N (N>=2 e N<16) Portas: 10124~N 10140~N|Ponto de conexão de CMG|
|Cliente para CMG|CMG|443|Cliente|
|Função de conector de CMG com o site (atualmente os pontos de gerenciamento e os pontos de atualização de software)|Função de site|Protocolo/portas configuradas na função de site|Ponto de conexão de CMG|

### <a name="how-can-you-improve-performance-of-the-cloud-management-gateway"></a>Como você pode melhorar o desempenho do gateway de gerenciamento de nuvem?

- Se for possível, configure o CMG, o ponto de conexão do CMG e o servidor de site do Configuration Manager na mesma região de rede a fim de reduzir a latência.
- Atualmente, a conexão entre o cliente do Configuration Manager e o CMG não tem reconhecimento de região.
- Para obter alta disponibilidade, recomendamos pelo menos duas instâncias virtuais do CMG e dois pontos de conexão de CMG por site
- Você pode dimensionar o CMG para oferecer suporte a mais clientes adicionando mais instâncias de VM. A carga delas é balanceada pelo Balanceador de carga do Azure AD.
- Crie mais pontos de conexão de CMG para distribuir a carga entre eles. O CMG fará 'round-robin' do tráfego para seus pontos de conexão de CMG.
- O número de clientes com suporte por instância de VM do CMG é de 6 mil na versão 1702. Quando o canal do CMG estiver com muita carga, a solicitação ainda será tratada, mas pode demorar mais tempo do que o normal.

### <a name="how-can-you-monitor-the-cloud-management-gateway"></a>Como você pode monitorar o gateway de gerenciamento de nuvem?

Para solução de problemas de implantação, use **CloudMgr.log** e **CMGSetup.log**.
Para solução de problemas de integridade de serviço, use **CMGService.log** e **SMS_CLOUD_PROXYCONNECTOR.log**.
Para solução de problemas de tráfego de clientes, use **CMGHttpHandler.log**, **CMGService.log** e **SMS_CLOUD_PROXYCONNECTOR.log**.

Para obter uma lista com todos os arquivos de log relacionadas ao CMG, veja [Arquivos de log no Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)

## <a name="next-steps"></a>Próximas etapas

[Configurar o gateway de gerenciamento de nuvem](setup-cloud-management-gateway.md)
