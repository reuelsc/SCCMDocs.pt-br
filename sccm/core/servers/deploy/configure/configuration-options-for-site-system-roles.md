---
title: Opções de função do sistema de sites
titleSuffix: Configuration Manager
description: Consulte este artigo para obter detalhes sobre funções do sistema de sites do Configuration Manager que não são necessariamente autoexplicativas.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 379fa3637d1634caf4797b1f1b7029e3531158cc
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893518"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Configurar opções para funções do sistema de sites no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A maioria das opções de configuração de funções do sistema de sites do Configuration Manager é autoexplicativa ou é explicada nas caixas de diálogo ou no assistente quando você as configura. As seções a seguir explicam as funções do sistema de sites cujas configurações precisam de informações adicionais.  



##  <a name="BKMK_ApplicationCatalog_Website"></a> Ponto de sites da Web do Catálogo de Aplicativos  

> [!Note]  
> A partir da versão 1806, o ponto de site do catálogo de aplicativos não será mais *necessário*, mas ainda será *compatível*. Para saber mais, veja [Configurar Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  
> 
> Não há mais suporte para a **experiência do usuário do Silverlight** para o ponto do site do Catálogo de Aplicativos. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

 Para saber mais sobre como configurar o ponto de sites da Web do Catálogo de Aplicativos, veja [Planejar e configurar o gerenciamento de aplicativos](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### <a name="client-connections"></a>Conexões de clientes
 Selecione **HTTPS** para conectar usando a configuração mais segura e determinar se os clientes se conectam da Internet. Essa opção requer um certificado PKI no servidor para autenticação de servidor para clientes e criptografia de dados sobre SSL (Secure Socket Layer). Para obter mais informações, veja [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para obter um exemplo de implantação do certificado do servidor e informações sobre como configurá-lo no IIS (Serviços de Informações da Internet), veja [Implantando o certificado do servidor Web para sistemas de sites que executam IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  

 #### <a name="add-application-catalog-website-to-trusted-sites-zone"></a>Adicionar o site da Web do catálogo de aplicativos à zona sites confiáveis  
 Esta mensagem exibe o valor nas configurações do cliente padrão se a configuração do cliente **Adicionar o site da Web do catálogo de aplicativos à zona sites confiáveis** estiver definida como **Verdadeiro** ou **Falso** no momento. Se você definiu essa configuração usando as configurações do cliente personalizado, habilite essa configuração.  

 Se esse sistema de site estiver configurado para um FQDN (nome de domínio totalmente qualificado) e o site da Web não estiver na zona de sites confiáveis no Internet Explorer, os usuários deverão fornecer credenciais ao se conectarem ao Catálogo de Aplicativos.  

 #### <a name="organization-name"></a>Nome da organização  

 Digite o nome que os usuários veem no Catálogo de Aplicativos. Essas informações de identidade visual ajudam os usuários a identificar este site da Web como uma fonte confiável.  



##  <a name="BKMK_ApplicationCatalog_WebService"></a> Ponto de serviços Web do Catálogo de Aplicativos  

> [!Note]  
> A partir da versão 1806, o ponto de serviço de site do catálogo de aplicativos e ponto de serviço Web não são mais *necessária*, mas ainda são *compatíveis*. Para saber mais, veja [Configurar Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  

 Para saber mais sobre como configurar o ponto de serviço da Web do Catálogo de Aplicativos, veja [Planejar e configurar o gerenciamento de aplicativos](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### <a name="https"></a>HTTPS

 Selecione **HTTPS** para autenticar os pontos de sites da Web do Catálogo de Aplicativos para este ponto de serviço Web do catálogo de aplicativos. Essa opção requer um certificado PKI nos servidores que executam o ponto de sites da Web do Catálogo de Aplicativos para autenticação do servidor e criptografia de dados sobre SSL. Para obter mais informações, veja [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para obter um exemplo de implantação do certificado do servidor e informações sobre como configurá-lo no IIS (Serviços de Informações da Internet), veja [Implantando o certificado do servidor Web para sistemas de sites que executam IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_CertificateRegistrationPoint"></a> Ponto de registro de certificado  

 Para saber mais sobre como configurar o ponto de registro de certificado, veja [Introdução aos perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  



##  <a name="BKMK_Distribution_Point"></a> Ponto de distribuição  

 Para saber mais sobre como definir o ponto de distribuição para implantação de conteúdo, veja [Gerenciar conteúdo e infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

 Para saber mais sobre como definir o ponto de distribuição para implantações PXE, veja [Use o PXE para implantar o Windows pela rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  

 Para saber mais sobre como definir o ponto de distribuição para implantações multicast, veja [Use o multicast para implantar o Windows pela rede](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).  

 #### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Instalar e configurar o IIS se exigido pelo Configuration Manager
 Selecione esta opção para que o Configuration Manager instale e configure o IIS no sistema de sites, se ainda não estiver instalado. O IIS deve ser instalado em todos os pontos de distribuição, e você deve selecionar essa configuração para continuar no assistente.  

 #### <a name="site-system-installation-account"></a>Conta de instalação do sistema de site
 Para pontos de distribuição instalados em um servidor do site, há suporte apenas para a conta do computador do servidor do site para uso como a Conta de Instalação de Sistema de Site. Para saber mais, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account).  

 #### <a name="create-a-self-signed-certificate-or-import-a-pki-client-certificate"></a>Criar um certificado autoassinado ou importar um certificado de cliente PKI
 Este certificado tem duas finalidades:  

1.  autentica o ponto de distribuição em um ponto de gerenciamento antes que o ponto de distribuição envie mensagens de status.  

2.  Quando **Habilitar suporte a PXE para clientes** estiver selecionado, o certificado será enviado para os computadores para boot de PXE. Eles usam esse certificado para se conectar a um ponto de gerenciamento durante a implantação do sistema operacional.  

Quando todos os pontos de gerenciamento do site estiverem configurados para HTTP, crie um certificado autoassinado. Quando os pontos de gerenciamento estiverem configurados para HTTPS, importe um certificado de cliente PKI.  

Para importar o certificado, navegue até um arquivo PKCS #12 (Public-Key Cryptography Standards #12) que contenha um certificado PKI com os seguintes requisitos para o Configuration Manager:  

-   O uso pretendido deve incluir a autenticação do cliente.  

-   A chave privada deve poder ser exportada.  

Não há nenhum requisito específico para a entidade do certificado ou o SAN (nome alternativo da entidade). Você pode usar o mesmo certificado para vários pontos de distribuição.  

Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos do certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements). 

Para ver um exemplo de implantação desse certificado, confira a seção [Implantando o certificado do cliente para pontos de distribuição](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

#### <a name="enable-this-distribution-point-for-prestaged-content"></a>Habilitar este ponto de distribuição para conteúdo pré-configurado
Marque esta caixa de seleção para habilitar o ponto de distribuição para conteúdo pré-configurado. Quando você habilita essa opção, você pode configurar o comportamento de distribuição ao distribuir conteúdo. Você pode escolher sempre pré-testar o conteúdo no ponto de distribuição, pré-testar o conteúdo inicial para o pacote, mas usar o processo normal de distribuição de conteúdo quando houver atualizações ou sempre usar o processo normal de distribuição de conteúdo para o conteúdo no pacote. Para obter mais informações, confira [Conteúdo pré-teste](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  

#### <a name="boundary-groups"></a>Grupos de limites
 Você pode associar grupos de limites a um ponto de distribuição. Durante a implantação do conteúdo, os clientes devem estar em um grupo de limites associado ao ponto de distribuição para usá-lo como um local de origem para conteúdo. Você configura relações entre grupos de limites que determinam quando um cliente pode começar a pesquisar localizações de fontes de conteúdo válidas em grupos de limites adicionais. Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).



##  <a name="BKMK_Enrollment_Point"></a> Ponto de registro  

Pontos de registro são usados para instalar computadores macOS e registrar os dispositivos gerenciados com o gerenciamento de dispositivos móveis locais. Para obter mais informações, consulte os seguintes artigos:  

-   [Como implantar clientes em Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  

-   [Como os usuários registram dispositivos com o MDM local](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm)  

#### <a name="allowed-connections"></a>Conexões permitidas
 A configuração HTTPS é selecionada automaticamente e requer um certificado PKI no servidor para autenticação do servidor para o ponto de proxy do registro, autenticação de servidor para ponto de serviço fora da banda, e criptografia de dados sobre SSL. Para obter mais informações, veja [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para obter um exemplo de implantação do certificado do servidor e informações sobre como configurá-lo no IIS, veja [Implantando o certificado do servidor Web para sistemas de sites que executam IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Enrollment_Proxy_Point"></a> Ponto proxy do registro  

Para saber mais sobre como configurar um ponto de proxy do registro para dispositivos móveis, veja [Como os usuários registram dispositivos com o MDM local](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm).  

#### <a name="client-connections"></a>Conexões de clientes
 A configuração de HTTPS é selecionada automaticamente. Isso requer os seguintes certificados de PKI no servidor: 
- Para autenticação de servidor para dispositivos móveis e computadores Mac registrados com o Configuration Manager 
- Para criptografia de dados sobre protocolo SSL

Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos do certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para obter um exemplo de implantação do certificado do servidor e informações sobre como configurá-lo no IIS, veja [Implantando o certificado do servidor Web para sistemas de sites que executam IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Fallback_Status_Point"></a> Ponto de status de fallback  

#### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Número de mensagens de estado e Intervalo de limitação (em segundos)
As configurações padrão para essas opções são 10.000 mensagens de estado e 3.600 segundos para o intervalo de limitação. Embora essas configurações sejam suficientes para a maioria das circunstâncias, talvez você precise alterá-las quando ambas as seguintes condições forem verdadeiras:  

-   O ponto de status de fallback aceita conexões somente da intranet.  

-   Você usa o ponto de status de fallback durante uma implantação do cliente para muitos computadores.  

Neste cenário, um fluxo contínuo de mensagens de estado pode criar uma lista de pendências que causa alto uso de processador no servidor de sites por um período prolongado. Além disso, talvez você não veja informações atualizadas sobre a implantação do cliente no console do Configuration Manager e nos relatórios de implantação do cliente.  

Essas configurações do ponto de status de fallback foram projetadas para serem definidas para mensagens de estado geradas durante a implantação do cliente. As configurações não foram projetadas para serem definidas para problemas de comunicação do cliente, como quando clientes na Internet não conseguem se conectar ao ponto de gerenciamento baseado na Internet. Como o ponto de status de fallback não pode aplicar essas configurações somente às mensagens de estado geradas durante a implantação do cliente, não defina essas configurações quando o ponto de status de fallback aceitar conexões da Internet.  

Cada computador que instala o cliente do Configuration Manager com êxito envia as quatro mensagens de estado a seguir para o ponto de status de fallback:  

-   Implantação do cliente iniciada  

-   Implantação do cliente com êxito  

-   Atribuição do cliente iniciada  

-   Atribuição do cliente com êxito  

Os computadores que não podem ser instalados, nem atribuir o cliente do Configuration Manager enviam mensagens de estado adicionais.  

Por exemplo, se você implantar o cliente do Configuration Manager em 20.000 computadores, a implantação poderá criar 80.000 mensagens de estado enviadas ao ponto de status de fallback. Como a configuração de limitação padrão permite o envio de 10.000 mensagens de estado ao ponto de status de fallback a cada 3,600 segundos (1 hora), as mensagens de estado podem ficar acumuladas no ponto de status de fallback. Considere também a largura de banda de rede disponível entre o ponto de status de fallback e o servidor de sites, e a potência de processamento do servidor de sites para processar muitas mensagens de estado.  

Para ajudar a evitar esses problemas, considere aumentar o número de mensagens de estado e diminuir o intervalo de limitação.  

Redefina os valores de limitação para o ponto de status de fallback se alguma das seguintes condições for verdadeira:  

-   Você calcular que os valores de limitação atuais são maiores do que o necessário para processar mensagens de estado do ponto de status de fallback.  

-   Você achar que as configurações de limitação atuais criam alto uso do processador no servidor do site.  

Não altere as definições das configurações de limitação do ponto de status de fallback a menos que você reconheça as consequências. Por exemplo, quando você aumenta as configurações de limitação para alto, o uso de processador no servidor do site pode aumentar para alto, o que reduz a velocidade de todas as operações do site.  
