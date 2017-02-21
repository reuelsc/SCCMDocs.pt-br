---
title: "Opções de função do sistema de sites | Microsoft Docs"
description: "Consulte este artigo para obter detalhes sobre funções do sistema de sites do Configuration Manager que não são necessariamente autoexplicativas."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fff93794afdfa9f890b1f06d6c330d8cffc5796c
ms.openlocfilehash: b4db5d86cc0ed020ed176feb2e8f1f9dc51a2280

---
# <a name="configuration-options-for-site-system-roles-for-system-center-configuration-manager"></a>Configurar opções para funções do sistema de sites para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A maioria das opções de configuração de funções do sistema de sites do System Center Configuration Manager é autoexplicativa ou é explicada nas caixas de diálogo ou no assistente quando você as configura. As seções a seguir explicam as funções do sistema de sites cujas configurações precisam de informações adicionais.  

##  <a name="a-namebkmkapplicationcatalogwebsitea-application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a> Ponto de sites da Web do Catálogo de Aplicativos  
 Para saber mais sobre como configurar o ponto de sites da Web do Catálogo de Aplicativos para o Catálogo de Aplicativos, veja [Planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **Conexões de clientes**  

 Selecione **HTTPS** para conectar usando a configuração mais segura e determinar se os clientes se conectam da Internet. Essa opção requer um certificado PKI no servidor para autenticação de servidor para clientes e criptografia de dados sobre SSL (Secure Socket Layer). Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver um exemplo de implantação do certificado do servidor e obter informações sobre como configurá-lo no IIS (Serviços de Informações da Internet), veja a seção *Implantação do certificado de servidor Web para sistemas de sites que executam o IIS* no tópico [Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

 **Adicionar o site da Web do catálogo de aplicativos à zona sites confiáveis**  

 Esta mensagem exibe o valor nas configurações do cliente padrão se a configuração do cliente **Adicionar o site da Web do catálogo de aplicativos à zona sites confiáveis** estiver definida como **Verdadeiro** ou **Falso** no momento. Se você definiu essa configuração usando as configurações do cliente personalizado, deve verificar esse valor por conta própria.  

 Se esse sistema de site estiver configurado para um FQDN (nome de domínio totalmente qualificado) e o site da Web não estiver na zona de sites confiáveis no Internet Explorer, os usuários deverão fornecer credenciais ao se conectarem ao Catálogo de Aplicativos.  

 **Nome da organização**  

 Digite o nome que os usuários veem no Catálogo de Aplicativos. Essas informações de identidade visual ajudam os usuários a identificar este site da Web como uma fonte confiável.  

##  <a name="a-namebkmkapplicationcatalogwebservicea-application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a> Ponto de serviços Web do Catálogo de Aplicativos  
 Para saber mais sobre como configurar o ponto de serviço Web do Catálogo de Aplicativos para o Catálogo de Aplicativos, veja [Planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **HTTPS**  

 Selecione **HTTPS** para autenticar os pontos de sites da Web do Catálogo de Aplicativos para este ponto de serviço Web do catálogo de aplicativos.  Essa opção requer um certificado PKI nos servidores que executam o ponto de sites da Web do Catálogo de Aplicativos para autenticação do servidor e criptografia de dados sobre SSL. Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver um exemplo de implantação do certificado do servidor e obter informações sobre como configurá-lo no IIS, veja a seção *Implantação do certificado de servidor Web para sistemas de sites que executam o IIS* em [Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="a-namebkmkcertificateregistrationpointa-certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a> Ponto de registro de certificado  
 Para saber mais sobre como configurar o ponto de registro de certificado, veja [Introdução aos perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

##  <a name="a-namebkmkdistributionpointa-distribution-point"></a><a name="BKMK_Distribution_Point"></a> Ponto de distribuição  
 Para saber mais sobre como definir o ponto de distribuição para implantação de conteúdo, veja [Gerenciar conteúdo e infraestrutura de conteúdo do System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Para saber mais sobre como definir o ponto de distribuição para implantações PXE, veja [Use o PXE para implantar o Windows pela rede com o System Center Configuration Manager](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Para saber mais sobre como definir o ponto de distribuição para implantações multicast, veja [Usar o multicast para implantar o Windows pela rede com o System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 **Instalar e configurar o IIS se exigido pelo Configuration Manager**  
 Selecione esta opção para que o Configuration Manager instale e configure o IIS no sistema de sites, se ainda não estiver instalado. O IIS deve ser instalado em todos os pontos de distribuição, e você deve selecionar essa configuração para continuar no assistente.  

 **Conta de instalação do sistema de sites**  
 Para pontos de distribuição instalados em um servidor do site, há suporte apenas para a conta do computador do servidor do site para uso como a Conta de Instalação de Sistema de Site.  

 **Criar um certificado autoassinado ou importar um certificado de cliente PKI**  
 Este certificado tem duas finalidades:  

1.  autentica o ponto de distribuição em um ponto de gerenciamento antes que o ponto de distribuição envie mensagens de status.  

2.  Quando a opção **Habilitar suporte a PXE para clientes** é selecionada, o certificado é enviado para computadores que executam uma inicialização PXE, para que eles possam se conectar a um ponto de gerenciamento durante a implantação do sistema operacional.  

Quando todos os pontos de gerenciamento do site estiverem configurados para HTTP, crie um certificado autoassinado. Quando os pontos de gerenciamento estiverem configurados para HTTPS, importe um certificado de cliente PKI.  

Para importar o certificado, navegue até um arquivo PKCS #12 (Public-Key Cryptography Standards #12) que contenha um certificado PKI com os seguintes requisitos para o Configuration Manager:  

-   O uso pretendido deve incluir a autenticação do cliente.  

-   A chave privada deve poder ser exportada.  

Não há nenhum requisito específico para o nome da entidade do certificado nem para o SAN (Nome Alternativo da Entidade), e você pode usar o mesmo certificado para vários pontos de distribuição.  

Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Para ver um exemplo de implantação deste certificado, consulte a seção *Implantando o certificado de cliente para pontos de distribuição* em [Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: Autoridade de Certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

**Habilitar este ponto de distribuição para conteúdo pré-configurado**  
Marque esta caixa de seleção para habilitar o ponto de distribuição para conteúdo pré-testado. Quando essa caixa de seleção estiver marcada, você pode configurar o comportamento de distribuição ao distribuir conteúdo. Você pode escolher sempre pré-testar o conteúdo no ponto de distribuição, pré-testar o conteúdo inicial para o pacote, mas usar o processo normal de distribuição de conteúdo quando houver atualizações ou sempre usar o processo normal de distribuição de conteúdo para o conteúdo no pacote.  

**Grupos de limites**  
 Você pode associar grupos de limites a um ponto de distribuição. Durante a implantação do conteúdo, os clientes devem estar em um grupo de limites associado ao ponto de distribuição para usá-lo como um local de origem para conteúdo.
 - **Nas versões anteriores à 1610**, você pode marcar a caixa de seleção **Permitir local de origem de fallback para conteúdo** para permitir que clientes fora desses grupos de limites façam fallback e usem o ponto de distribuição como um local de origem para conteúdo quando nenhum outro ponto de distribuição estiver disponível.
 - **Começando da versão 1610**, não é mais possível configurar a opção **Permitir local de origem de fallback para conteúdo**.  Em vez disso, você configura relações entre grupos de limites que determinam quando um cliente pode começar a pesquisar localizações de fontes de conteúdo válidas em grupos de limites adicionais.

##  <a name="a-namebkmkenrollmentpointa-enrollment-point"></a><a name="BKMK_Enrollment_Point"></a> Ponto de registro  
Pontos de registro são usados para instalar computadores Mac e registrar os dispositivos gerenciados com o gerenciamento de dispositivos móveis locais. Para obter mais informações, consulte:  

-   [Como implantar clientes em Macs no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

-   [Como os usuários registram dispositivos com o Gerenciamento de Dispositivo Móvel local no System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

**Conexões permitidas**  
 A configuração HTTPS é selecionada automaticamente e requer um certificado PKI no servidor para autenticação do servidor para o ponto de proxy do registro, autenticação de servidor para ponto de serviço fora da banda, e criptografia de dados sobre SSL. Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver um exemplo de implantação do certificado do servidor e obter informações sobre como configurá-lo no IIS, veja a seção *Implantação do certificado de servidor Web para sistemas de sites que executam o IIS* em [Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="a-namebkmkenrollmentproxypointa-enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a> Ponto proxy do registro  
Para saber mais sobre como configurar um ponto de proxy do registro para dispositivos móveis, veja [Como os usuários registram dispositivos com o Gerenciamento de Dispositivo Móvel local no System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

**Conexões de clientes**  
 A configuração HTTPS é selecionada automaticamente e requer um certificado PKI no servidor para autenticação do servidor para dispositivos móveis e computadores Mac registrados pelo Configuration Manager e para criptografia de dados sobre protocolo SSL. Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para ver um exemplo de implantação do certificado do servidor e obter informações sobre como configurá-lo no IIS, veja a seção *Implantação do certificado de servidor Web para sistemas de sites que executam o IIS* em [Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="a-namebkmkfallbackstatuspointa-fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a> Ponto de status de fallback  
**Número de mensagens de estado** e **Intervalo de limitação (em segundos)**  
Embora as configurações padrão para essas opções (10.000 mensagens de estado e 3.600 segundos para o intervalo de limitação) sejam suficientes para a maioria das circunstâncias, talvez seja preciso alterá-las quando ambas das seguintes condições forem verdadeiras:  

-   O ponto de status de fallback aceita conexões somente da intranet.  

-   Você usa o ponto de status de fallback durante uma implantação do cliente para muitos computadores.  

Neste cenário, um fluxo contínuo de mensagens de estado pode criar uma lista de pendências que causa alto uso da CPU no servidor de sites por um período prolongado. Além disso, talvez você não veja informações atualizadas sobre a implantação do cliente no console do Configuration Manager e nos relatórios de implantação do cliente.  

Essas configurações do ponto de status de fallback foram projetadas para serem definidas para mensagens de estado geradas durante a implantação do cliente. As configurações não foram projetadas para serem definidas para problemas de comunicação do cliente, como quando clientes na Internet não conseguem se conectar ao ponto de gerenciamento baseado na Internet. Como o ponto de status de fallback não pode aplicar essas configurações somente às mensagens de estado geradas durante a implantação do cliente, não defina essas configurações quando o ponto de status de fallback aceitar conexões da Internet.  

Cada computador que instala o cliente do System Center 2012 Configuration Manager com êxito envia as quatro mensagens de estado a seguir para o ponto de status de fallback:  

-   Implantação do cliente iniciada  

-   Implantação do cliente com êxito  

-   Atribuição do cliente iniciada  

-   Atribuição do cliente com êxito  

Os computadores que não podem ser instalados, nem atribuir o cliente do Configuration Manager enviam mensagens de estado adicionais.  

Por exemplo, se você implantar o cliente do Configuration Manager em 20.000 computadores, a implantação poderá criar 80.000 mensagens de estado enviadas ao ponto de status de fallback. Como a configuração de limitação padrão permite o envio de 10.000 mensagens de estado ao ponto de status de fallback a cada 3,600 segundos (1 hora), as mensagens de estado podem ficar acumuladas no ponto de status de fallback. Você também deve considerar a largura de banda de rede disponível entre o ponto de status de fallback e o servidor de sites, e a potência de processamento do servidor de sites para processar muitas mensagens de estado.  

Para ajudar a evitar esses problemas, considere aumentar o número de mensagens de estado e diminuir o intervalo de limitação.  

Redefina os valores de limitação para o ponto de status de fallback se alguma das seguintes condições for verdadeira:  

-   Você calcular que os valores de limitação atuais são maiores do que o necessário para processar mensagens de estado do ponto de status de fallback.  

-   Você achar que as configurações de limitação atuais criam alto uso da CPU no servidor do site.  

Não altere as definições das configurações de limitação do ponto de status de fallback a menos que você entenda as consequências. Por exemplo, quando você aumenta as configurações de limitação para alto, o uso de CPU no servidor do site pode aumentar para alto, o que reduz a velocidade de todas as operações do site.  



<!--HONumber=Feb17_HO2-->


