---
title: Segurança e privacidade do CMG
description: Saiba mais sobre as diretrizes e recomendações de segurança e privacidade com o gateway de gerenciamento de nuvem.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.openlocfilehash: d07c30d6a1e4fd1314b6e69ac157577ae0163696
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Segurança e privacidade do gateway de gerenciamento de nuvem

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo inclui informações de segurança e privacidade para o CMG (gateway de gerenciamento de nuvem) do Configuration Manager. Para obter mais informações, consulte [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

## <a name="cmg-security-details"></a>Detalhes de segurança do CMG
- O CMG aceita e gerencia as conexões nos pontos de conexão do CMG. Ele usa a autenticação SSL mútua usando certificados e IDs de conexão.
- O CMG aceita e encaminha as solicitações de cliente usando os seguintes métodos:
    - Pré-autentica as conexões usando o SSL mútuo com o Azure AD ou o certificado de autenticação de cliente baseado em PKI. 
      - O IIS em instâncias de VM do CMG verifica o caminho do certificado com base nos certificados raiz confiáveis carregados no CMG.
      - O IIS na instância de VM também verifica a revogação de certificado de cliente, se estiver habilitado. Para obter mais informações, consulte [Publicar a lista de certificados revogados](#bkmk_crl).
    - A lista de certificados confiáveis verifica a raiz do certificado de autenticação de cliente. Ele também executa a mesma validação como o ponto de gerenciamento para o cliente. Para obter mais informações, consulte [Examinar as entradas da lista de certificados confiáveis do site](#bkmk_ctl).
    - Valida e filtra as solicitações de cliente (URLs) para verificar se um ponto de conexão do CMG pode atender à solicitação.  
    - Verifica o tamanho do conteúdo para cada ponto de extremidade de publicação.
    - Usa o comportamento round robin para balancear a carga dos pontos de conexão do CMG no mesmo site.
- O ponto de conexão do CMG usa os seguintes métodos:
    - Cria conexões HTTPS/TCP consistentes para todas as instâncias de VM do CMG. Ele verifica e mantém essas conexões a cada minuto.
    - Usa a autenticação SSL mútua com o CMG usando certificados.
    - Encaminha as solicitações do cliente com base em mapeamentos de URL.
    - Relata o status de conexão para mostrar o status da integridade do serviço no console.
    - Relata o tráfego por ponto de extremidade a cada cinco minutos.

### <a name="configuration-manager-client-facing-roles"></a>Funções voltadas para o cliente do Configuration Manager
O ponto de gerenciamento e o ponto de atualização de software no IIS hospedam pontos de extremidade no IIS para atender às solicitações de cliente. O CMG não expõe todos os pontos de extremidade internos. Cada ponto de extremidade publicado no CMG tem um mapeamento de URL.
  - A URL externa é aquela usada pelo cliente para se comunicar com o CMG.
  - A URL interna é o ponto de conexão de CMG usado para encaminhar solicitações para o servidor interno.

#### <a name="url-mapping-example"></a>Exemplo de mapeamento de URL
Quando você habilita o tráfego do CMG em um ponto de gerenciamento, o Configuration Manager cria um conjunto interno de mapeamentos de URL para cada servidor de ponto de gerenciamento. Por exemplo: ccm_system, ccm_incoming e sms_mp. A URL externa para o ponto de extremidade de ccm_system do ponto de gerenciamento pode ser semelhante a esta:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
A URL é exclusiva para cada ponto de gerenciamento. Em seguida, o cliente do Configuration Manager coloca o nome do ponto de gerenciamento habilitado para CMG em sua lista de pontos de gerenciamento da Internet. Esse nome é semelhante a este:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
O site carrega automaticamente todas as URLs externas publicadas no CMG. Esse comportamento permite que o CMG faça a filtragem de URL. Todos os mapeamentos de URL são replicados para o ponto de conexão do CMG. Em seguida, ele encaminha a comunicação para os servidores internos, de acordo com a URL externa da solicitação do cliente.



## <a name="security-guidance-for-cmg"></a>Diretrizes de segurança para o CMG


<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>Publicar a lista de certificados revogados

Publique a CRL (lista de certificados revogados) da PKI para acesso pelos clientes baseados na Internet. Ao implantar um CMG usando a PKI, configure o serviço para **verificar a revogação de certificados do cliente** na guia Configurações. Essa configuração define o serviço para que ele use uma CRL (lista de certificados revogados) publicados. Para obter mais informações, consulte [Planejar a revogação de certificados PKI](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).



<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Examinar as entradas na lista de certificados confiáveis do site
<!--503739-->
Cada site do Configuration Manager inclui uma lista de autoridades de certificação confiáveis, a CTL (lista de certificados confiáveis). Exiba e modifique a lista acessando o espaço de trabalho Administração, expanda Configuração do Site e selecione Sites. Selecione um site e clique em Propriedades na faixa de opções. Alterne para a guia Comunicação do Computador Cliente e, em seguida, clique em **Definir** em Autoridades de Certificação Confiáveis.
 
Use uma CTL mais restritiva para um site com um CMG que usa a autenticação de cliente PKI. Caso contrário, os clientes com certificados de autenticação de cliente emitidos por qualquer raiz confiável já existente no ponto de gerenciamento serão automaticamente aceitos para o registro de cliente.

Esse subconjunto fornece aos administradores mais controle sobre a segurança. A CTL restringe o servidor a aceitar somente os certificados de cliente emitidos por autoridades de certificação na CTL. Por exemplo, o Windows é fornecido com diversos certificados de Autoridade de Certificação de terceiros conhecidos, como VeriSign e Thawte. Por padrão, o computador que executa o IIS confia nos certificados vinculados a essas ACs conhecidas. Sem configurar o IIS com uma CTL, qualquer computador que tem um certificado de cliente emitido por essas ACs será aceito como um cliente válido do Configuration Manager. Se você configurar o IIS com uma CTL que não inclui essas ACs, as conexões de cliente serão recusadas, caso o certificado seja vinculado a essas ACs. 


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>Próximas etapas

- [Plano para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Perguntas frequentes sobre o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Certificados para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
