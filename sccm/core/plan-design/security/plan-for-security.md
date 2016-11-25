---
title: "Planejar a segurança no System Center Configuration Manager"
description: "Veja as práticas recomendadas de segurança e informações sobre segurança no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
caps.latest.revision: 6
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f38d7275a39d16f9e6cf90334a46668fcc860bc1


---
# <a name="plan-for-security-in-system-center-configuration-manager"></a>Planejar a segurança no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações neste tópico para ajudá-lo a planejar a segurança no System Center Configuration Manager.  

   Para obter mais informações sobre como o Configuration Manager utiliza certificados e controles de criptografia, consulte [Referência técnica para controles de criptografia usados no System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  


##  <a name="a-namebkmkplanningforcertificatesa-planning-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> Planejando certificados (autoassinados e PKI)  
 O Configuration Manager usa uma combinação de certificados autoassinados e certificados PKI (infraestrutura de chave pública).  

 Como prática recomendada de segurança, use certificados PKI sempre que possível. Para obter mais informações sobre os requisitos de certificados PKI, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md). Quando o Configuration Manager solicita os certificados PKI, como durante o registro de dispositivos móveis e o provisionamento AMT, você precisa usar o Active Directory Domain Services e uma autoridade de certificação corporativa. Para todos os outros certificados PKI, implante e gerencie-os independentemente do Configuration Manager.  

 Os certificados PKI também são solicitados quando computadores cliente se conectam a sistemas de áreas baseados na Internet, e recomenda-se usá-los quando os clientes se conectam a sistemas de site que executam o IIS (Serviços de Informações da Internet). Para obter mais informações sobre a comunicação do cliente, consulte [Como configurar portas de comunicação do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

 Quando você usa uma PKI, também pode usar IPsec para ajudar a proteger a comunicação de servidor para servidor entre sistemas de site em um site e entre sites, e para qualquer cenário quando você transferir dados entre computadores. Você deve configurar e implementar o IPsec independentemente do Configuration Manager.  

 O Configuration Manager pode gerar automaticamente certificados autoassinados quando certificados PKI não estiverem disponíveis, e alguns certificados no Configuration Manager sempre são autoassinados. Na maioria dos casos, o Configuration Manager gerencia automaticamente os certificados autoassinados e você não precisa tomar medidas adicionais. Uma possível exceção é o certificado de autenticação do servidor do site. O certificado de autenticação do servidor do site é sempre autoassinado e assegura que as políticas do cliente que os clientes baixam do ponto de gerenciamento foram enviadas do servidor do site e não foram violadas.  

### <a name="planning-for-the-site-server-signing-certificate-self-signed"></a>Planejando o certificado de autenticação (autoassinado) do servidor do site  
 Os clientes podem obter com segurança uma cópia do certificado de autenticação do servidor do site dos Serviços de Domínio Active Directory e da instalação do cliente por push. Se os clientes não conseguirem obter uma cópia do certificado de autenticação do servidor do site usando um desses mecanismos, como prática recomendada de segurança, instale uma cópia do certificado de autenticação do servidor do site ao instalar o cliente. Isso é especialmente importante se a primeira comunicação do cliente com o site for da Internet, pois o ponto de gerenciamento está conectado a uma rede não confiável e, portanto, vulnerável a ataques. Se você não seguir essa etapa adicional, os clientes baixarão automaticamente uma cópia do certificado de autenticação do servidor do site do ponto de gerenciamento.  

 Os cenários nos quais os clientes não conseguem obter com segurança uma cópia do certificado do servidor do site incluem o seguinte:  

-   Você não instala o cliente usando o push de cliente, e nenhuma das condições a seguir é verdadeira:  

    -   o esquema do Active Directory não foi estendido para o Configuration Manager.  

    -   o site do cliente não foi publicado no Active Directory Domain Services.  

    -   O cliente é de uma floresta ou de um grupo de trabalho não confiável.  

-   Você instala o cliente quando ele está na Internet.  

Use o procedimento a seguir para instalar clientes junto com uma cópia do certificado de autenticação do servidor do site.  

##### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Para instalar clientes com uma cópia do certificado de autenticação do servidor do site  

1.  Localize o certificado de autenticação do servidor do site no servidor do site principal do cliente. O certificado é armazenado no repositório de certificados **SMS** e tem como nome da Entidade **Servidor do Site** e como nome amigável **Certificado de Autenticação do Servidor do Site**.  

2.  Exporte o certificado sem a chave privada, armazene o arquivo com segurança e acesso-o somente de um canal protegido (por exemplo, usando assinatura SMB ou IPsec).  

3.  Instale o cliente usando a propriedade Client.msi **SMSSIGNCERT=***&lt;Caminho completo e nome do arquivo\>* com CCMSetup.exe.  

###  <a name="a-namebkmkplanningforcrlsa-planning-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> Planejando a revogação de certificados PKI  
Quando usar certificados PKI com o Configuration Manager, planeje como e se os clientes e servidores usarão uma CRL (lista de certificados revogados) para verificar o certificado no computador que está se conectando. A CRL é um arquivo criado e assinado por uma CA (autoridade de certificação) e contém uma lista de certificados emitidos, mas revogados. Os certificados podem ser revogados por um administrador da CA, por exemplo, se um certificado emitido for conhecido ou tiver suspeita estar comprometido.  

> [!IMPORTANT]  
>  Como o local da CRL é adicionado ao certificado quando ele é emitido por uma AC, planeje a CRL antes de implantar os certificados PKI que o Configuration Manager usará.  

Por padrão, o IIS sempre verifica a CRL quanto a certificados de cliente, e você não pode alterar essa configuração no Configuration Manager. Por padrão, os clientes do Configuration Manager sempre verificam a CRL quanto a sistemas de sites. No entanto, você pode desabilitar essa configuração especificando uma propriedade do site e uma propriedade CCMSetup. Ao gerenciar computadores Intel AMT fora de banda, você também pode habilitar a verificação da CRL para o ponto de serviço fora de banda e para computadores que executam o console de gerenciamento fora de banda.  

Se os computadores usam a verificação de revogação de certificados, mas não podem localizar a CRL, eles se comportam como se todos os certificados na cadeia de certificados fossem revogados, pois sua ausência da lista não pode ser verificada. Nesse cenário, todas as conexões que requerem certificados e usam uma CRL falham.  

A verificação da CRL sempre que um certificado é usado oferece mais segurança contra o uso de um certificado revogado, mas gera atraso de conexão e processamento adicional no cliente. É mais provável que você solicite essa verificação de segurança adicional quando os clientes estão na Internet ou em uma rede não confiável.  

Consulte seus administradores de PKI antes de decidir se os clientes do Configuration Manager devem verificar a CRL e considere manter essa opção habilitada no Configuration Manager quando as duas condições a seguir forem verdadeiras:  

-   sua infraestrutura de PKI dá suporte a uma CRL e é publicada onde todos os clientes do Configuration Manager podem localizá-la. Lembre-se que isso poderá incluir clientes na Internet se você estiver usando gerenciamento de clientes baseado na Internet e clientes em florestas não confiáveis.  

-   O requisito para verificar a CRL para cada conexão a um sistema de site configurado para usar um certificado PKI é maior do que o requisito para conexões mais rápidas e eficientes que são processadas no cliente, e também é maior do que o risco de os clientes não conseguirem se conectar a servidores se eles não puderem localizar a CRL.  

###  <a name="a-namebkmkplanningforrootcasa-planning-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> Planejando certificados PKI de raiz confiável e a lista de emissores de certificados  
Se os sistemas de site do IIS usam certificados de cliente PKI para autenticação do cliente via HTTP ou para autenticação do cliente e criptografia via HTTPS, você deve importar certificados de CA raiz como uma propriedade do site. Os dois cenários são os seguintes:  

-   Você implanta sistemas operacionais usando o Configuration Manager e os pontos de gerenciamento aceitam somente conexões de cliente HTTPS.  

-   Você usa certificados de cliente PKI que não se encadeiam a um certificado de autoridade de certificação raiz que é confiável por pontos de gerenciamento.  

    > [!NOTE]  
    >  Ao emitir certificados PKI de clientes da mesma hierarquia de CA que emite os certificados do servidor que você usa para pontos de gerenciamento, você não precisa especificar esse certificado de CA raiz. No entanto, se você usar várias hierarquias de AC e não tiver certeza se elas têm confiança entre si, importe a AC raiz para a hierarquia de autoridade de certificação dos clientes.  

Se você precisar importar certificados de AC raiz para o Configuration Manager, exporte-os da AC emissora ou do computador cliente. Se você exportar o certificado da CA emissora que também é a CA raiz, verifique se a chave privada não foi exportada. Armazene o arquivo de certificado exportado em um local seguro para impedir a violação. Você deve ser capaz de acessar o arquivo ao configurar o site; assim, se você acessar o arquivo pela rede, verifique se a comunicação está protegida contra violação usando a assinatura SMB ou IPsec.  

Se algum dos certificados de CA raiz que você importa for renovado, você deverá importar os certificados renovados.  

Esses certificados de AC raiz importados e o certificado de AC raiz de cada ponto de gerenciamento criam a lista de emissores de certificado que os computadores do Configuration Manager usam das seguintes maneiras:  

-   Quando clientes se conectam a pontos de gerenciamento, o ponto de gerenciamento verifica se o certificado do cliente se encadeia a um certificado de raiz confiável na lista de emissores de certificado do site. Caso não se encadeie, o certificado será rejeitado e ocorrerá falha na conexão PKI.  

-   Quando clientes selecionam um certificado PKI, se eles tiverem uma lista de emissores do certificado, eles selecionam um certificado que se encadeie a um certificado de raiz confiável na lista de emissores do certificado. Se não houver nenhuma correspondência, o cliente não selecionará um certificado PKI. Para obter mais informações sobre o processo de certificado de cliente, consulte a seção [Planning for PKI client certificate selection](#BKMK_PlanningForClientCertificateSelection) neste tópico.  

Independentemente da configuração do site, você também pode precisar importar um certificado de CA raiz ao registrar dispositivos móveis ou computadores Mac e ao provisionar computadores Intel AMT para redes sem fio.  

###  <a name="a-namebkmkplanningforclientcertificateselectiona-planning-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> Planning for PKI client certificate selection  
 Se os sistemas de sites do IIS usarem certificados de cliente PKI para autenticação via HTTP ou para autenticação do cliente e criptografia via HTTPS, planeje como os clientes Windows selecionarão o certificado a ser usado para o Configuration Manager.  

> [!NOTE]  
>  Nem todos os dispositivos oferecem suporte ao método de seleção de certificado, mas, em vez disso, selecionam automaticamente o primeiro certificado que preencha os requisitos do certificado. Por exemplo, clientes em computadores Mac e dispositivos móveis não oferecem suporte a um método de seleção de certificado.  

Em muitos casos, a configuração padrão e o comportamento serão suficientes. O cliente do Configuration Manager em computadores Windows filtra vários certificados usando os seguintes critérios:  

1.  A lista de emissores do certificado: o certificado está encadeado a uma AC raiz confiável pelo ponto de gerenciamento.  

2.  O certificado está no repositório de certificados padrão **Pessoal**.  

3.  O certificado é válido, não revogado e não expirou. A verificação de validade inclui verificar se a chave privada é acessível e se o certificado não foi criado usando um modelo de certificado versão 3, que não é compatível com o Configuration Manager.  

4.  O certificado tem um recurso de autenticação do cliente ou é emitido para o nome do computador.  

5.  O certificado tem o período de validade mais longo.  

Os clientes podem ser configurados para usar a lista de emissores do certificado por meio dos seguintes mecanismos:  

-   Ele é publicado como informações de site do Configuration Manager para o Active Directory Domain Services.  

-   Os clientes são instalados usando a instalação por push.  

-   Os clientes baixam o certificado do ponto de gerenciamento, depois que eles são atribuídos com êxito ao site.  

-   Ele é especificado durante a instalação do cliente, como uma propriedade CCMSetup client.msi de CCMCERTISSUERS.  

Se os clientes não tiverem a lista de emissores do certificado quando forem instalados pela primeira vez e ainda não estiverem atribuídos ao site, eles irão ignorar essa verificação. Quando eles tiverem a lista de emissores do certificado e não tiverem um certificado PKI que se encadeie a um certificado de raiz confiável na lista de emissores do certificado, ocorrerá falha na seleção do certificado, e os clientes não continuarão com os outros critérios de seleção do certificado.  

Na maioria dos casos, o cliente do Configuration Manager identifica corretamente um certificado PKI único e apropriado a ser usado. No entanto, quando esse não for o caso, em vez de selecionar o certificado baseado no recurso de autenticação do cliente, você pode configurar dois métodos de seleção alternativos:  

-   Uma correspondência parcial de cadeia de caracteres no nome da entidade do certificado do cliente. Essa é uma correspondência que não diferencia maiúscula de minúsculas e é apropriada se você está usando o FQDN (nome de domínio totalmente qualificado) de um computador no campo da entidade e deseja que a seleção do certificado seja baseada no sufixo do domínio, por exemplo, **contoso.com**. Entretanto, você pode usar esse método de seleção para identificar alguma cadeia de caracteres sequencial no nome da entidade do certificado que diferencia o certificado dos outros no repositório de certificados do cliente.  

    > [!NOTE]  
    >  Você não pode usar a correspondência parcial de cadeia de caracteres com o SAN (Nome de Alternativo da Entidade) como uma configuração do site. Embora você possa especificar uma correspondência parcial de cadeia de caracteres para o SAN usando CCMSetup, ela será substituída pelas propriedades do site nos seguintes cenários:  
    >   
    >  -   Clientes recuperam informações do site que são publicadas nos Serviços de Domínio Active Directory.  
    > -   Clientes são instalados por push.  
    >   
    >  Use uma correspondência parcial de cadeia de caracteres na SAN somente ao instalar clientes manualmente e quando eles não recuperarem informações de site dos Serviços de Domínio Active Directory. Por exemplo, essas condições só se aplicam a clientes da Internet.  

-   Uma correspondência nos valores de atributo de nome da Entidade do certificado do cliente ou valores de atributo da SAN (Nome Alternativo da Entidade). Essa é uma correspondência com diferenciação de maiúsculas e minúsculas que é apropriada se você estiver usando um nome diferenciado X500 ou OIDs (Identificadores de Objeto) equivalentes em conformidade com a RFC 3280, e se desejar que a seleção do certificado seja baseada em valores de atributos. Você só pode especificar os atributos e seus valores necessários para identificar ou validar com exclusividade o certificado e diferenciá-lo de outros no armazenamento de certificados.  

A tabela a seguir mostra os valores de atributo a que o Configuration Manager dá suporte como critérios de seleção de certificados do cliente.  

|Atributo OID|Atributo de nome diferenciado|Definição de atributo|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Componente do domínio|  
|1.2.840.113549.1.9.1|E ou email|Endereço de e-mail|  
|2.5.4.3|CN|Nome comum|  
|2.5.4.4|SN|Nome da entidade|  
|2.5.4.5|SERIALNUMBER|Número de série|  
|2.5.4.6|C|Código do país|  
|2.5.4.7|L|Localidade|  
|2.5.4.8|S ou ST|Nome do estado ou província|  
|2.5.4.9|RUA|Endereço|  
|2.5.4.10|O|Nome da organização|  
|2.5.4.11|OU|Unidade organizacional|  
|2.5.4.12|T ou Título|Título|  
|2.5.4.42|G ou GN ou GivenName|Nome|  
|2.5.4.43|I ou Iniciais|Iniciais|  
|2.5.29.17|(nenhum valor)|Nome alternativo da entidade|  

Se mais de um certificado apropriado for localizado após a aplicação dos critérios de seleção, você poderá substituir a configuração padrão para selecionar o certificado com o período de validade mais longo e, em vez disso, especificar que nenhum certificado foi selecionado. Neste cenário, o cliente não será capaz de se comunicar com sistemas de site IIS usando um certificado PKI. O cliente envia uma mensagem de erro ao seu ponto de status de fallback atribuído para alertá-lo sobre a falha na seleção do certificado para que você possa modificar ou aperfeiçoar seus critérios de seleção. O comportamento do cliente, então, depende se a falha da conexão foi em HTTPS ou HTTP:  

-   Se a conexão com falha for via HTTPS: o cliente tentará fazer uma conexão via HTTP e usa seu certificado autoassinado.  

-   Se a conexão com falha for via HTTP: o cliente tentará fazer outra conexão via HTTP usando seu certificado autoassinado.  

Para ajudar a identificar um certificado PKI único de cliente, você também pode especificar um repositório personalizado, diferente do padrão **Pessoal** no repositório do **Computador** . No entanto, você precisa criar esse repositório independentemente do Configuration Manager e precisa implantar certificados neste repositório personalizado e renová-los antes que o prazo de validade expire.  

Para obter informações sobre como definir as configurações para certificados de cliente, consulte a seção [Definir configurações para certificados PKI de clientes](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) no tópico [Configurar a segurança no System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

###  <a name="a-namebkmkplanningforpkitransitiona-planning-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> Planejando uma estratégia de transição para certificados PKI e gerenciamento de clientes baseados na Internet  
As opções de configuração flexíveis do Configuration Manager permitem que você faça a transição gradual dos clientes e do site para usar certificados PKI e ajudar a proteger os pontos de extremidade do cliente. Certificados PKI fornecem maior segurança e permitem que os clientes sejam gerenciados quando estão na Internet.  

Devido ao grande número de escolhas e opções de configuração no Configuration Manager, não há uma maneira única de fazer a transição de um site de forma que todos os clientes usem conexões HTTPS. No entanto, você pode seguir estas etapas como orientação:  

1.  Instale o site do Configuration Manager e configure-o de modo que os sistemas de sites aceitem conexões de clientes via HTTPS e HTTP.  

2.  Configure a guia **Comunicação do Computador Cliente** nas propriedades do site para que as **Configurações do Sistema de Site** sejam **HTTP ou HTTPS**, e marque a caixa de seleção **Usar certificado de cliente PKI (Recurso de Autenticação de Cliente) quando disponível** . Defina outras configurações necessárias nesta guia. Para obter mais informações, consulte a seção [Definir configurações para certificados PKI de clientes](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) no tópico [Configurar a segurança no System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

3.  Coordene uma distribuição de PKI para certificados de cliente. Para ver um exemplo de implantação, consulte a seção *Implantando o certificado de cliente em computadores Windows* no tópico [Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: Autoridade de Certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

4.  Instale clientes usando o método de instalação por push do cliente. Para obter mais informações, consulte a seção [Como instalar clientes do Configuration Manager usando o push do cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush) no tópico [Como implantar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

5.  Monitore a implantação e o status do cliente usando os relatórios e as informações no console do Configuration Manager.  

6.  Controle quantos clientes estão usando um certificado PKI de cliente visualizando a coluna **Certificado do Cliente** no espaço de trabalho **Ativos e Conformidade** , nó **Dispositivos** .  

     Você também pode implantar a Ferramenta de avaliação de prontidão do HTTPS do Configuration Manager (**cmHttpsReadiness.exe**) em computadores e usar os relatórios para ver quantos computadores podem usar um certificado PKI de cliente com o Configuration Manager.  

    > [!NOTE]  
    >  Quando o cliente do Configuration Manager é instalado em computadores cliente, a ferramenta **cmHttpsReadiness.exe** é instalada na pasta *%windir%***\CCM**. Quando você executa essa ferramenta em clientes, pode especificar as seguintes opções:  
    >   
    >  -   /Store:&lt;name\>  
    > -   /Issuers:&lt;list\>  
    > -   /Criteria:&lt;criteria\>  
    > -   /SelectFirstCert  
    >   
    >  Essas opções mapeiam para as propriedades de Client.msi **CCMCERTSTORE**, **CCMCERTISSUERS**, **CCMCERTSEL**e **CCMFIRSTCERT** , respectivamente. Para obter mais informações sobre essas opções, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

7.  Quando estiver confiante de que um número suficiente de clientes está usando com sucesso o certificado PKI de cliente para autenticação em HTTP, faça o seguinte:  

    1.  Implante um certificado PKI de servidor Web em um servidor membro que irá executar um ponto de gerenciamento adicional para o site, e configure o certificado no IIS. Para obter mais informações, consulte a seção *Implantando o certificado do servidor Web para sistemas de sites que executam IIS* no tópico [Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: Autoridade de Certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

    2.  Instale a função de ponto de gerenciamento no servidor e configure a opção **Conexões de Cliente** nas propriedades do ponto de gerenciamento de **HTTPS**.  

8.  Monitore e verifique se os clientes que têm um certificado PKI usam o novo ponto de gerenciamento ao usar o HTTPS. Você pode usar o registro em log do IIS ou contadores de desempenho para verificar isso.  

9. Reconfigure as outras funções de sistema de site para usar conexões de cliente HTTPS. Se você quiser gerenciar clientes na Internet, verifique se os sistemas do site têm um FQDN de Internet e configure pontos de gerenciamento individuais e pontos de distribuição para aceitar conexões de clientes da Internet.  

    > [!IMPORTANT]  
    >  Para configurar as funções do sistema de site para aceitar conexões da Internet, verifique as informações de planejamento e os pré-requisitos para gerenciamento de clientes baseados na Internet. Para obter mais informações, consulte [Comunicação entre pontos de extremidade no System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

10. Estenda a distribuição de certificado PKI a clientes e sistemas de site que executam IIS, e configure as funções do sistema de site para conexões de cliente HTTPS e conexões de Internet, conforme necessário.  

11. Para maior segurança: quando estiver seguro de que todos os clientes estão usando um certificado PKI de cliente para autenticação e criptografia, altere as propriedades do site para usar somente HTTPS.  

 Quando você segue este plano para introduzir gradualmente certificados PKI, primeiro para autenticação somente por HTTP, e depois para autenticação e criptografia HTTPS, reduz o risco dos clientes ficarem sem gerenciamento. Além disso, você será beneficiado com a maior segurança a que o Configuration Manager dá suporte.  

##  <a name="a-namebkmkplanningforrtka-planning-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> Planejando a chave de raiz confiável  
A chave de raiz confiável do Configuration Manager fornece um mecanismo para os clientes do Configuration Manager verificarem se os sistemas de sites pertencem à sua hierarquia. Cada servidor de site gera uma chave de troca de site para se comunicar com outros sites. A chave de troca do site de nível superior na hierarquia é chamada de chave de raiz confiável.  

A função da chave de raiz confiável no Configuration Manager se assemelha a um certificado raiz em uma infraestrutura de chave pública no sentido de que qualquer coisa assinada pela chave privada da chave de raiz confiável tem confiança abaixo na hierarquia. Por exemplo, ao assinar o certificado do ponto de gerenciamento com a chave privada do par de chaves de raiz confiável e ao disponibilizar uma cópia da chave pública do par de chaves de raiz confiável para os clientes, eles podem diferenciar entre os pontos de gerenciamento que estão em sua hierarquia e os que não estão. Os clientes usam WMI para armazenar uma cópia da chave raiz confiável no namespace **root\ccm\locationservices**.  

Clientes podem recuperar automaticamente a cópia pública da chave de raiz confiável usando dois mecanismos:  

-   O esquema do Active Directory é estendido para o Configuration Manager, o site é publicado no Active Directory Domain Services e os clientes podem recuperar informações do site por meio de um servidor de catálogo global.  

-   Os clientes são instalados usando a instalação por push.  

Se os clientes não puderem recuperar a chave de raiz confiável usando um desses mecanismos, eles confiarão na chave de raiz confiável fornecida pelo primeiro ponto de gerenciamento com o qual se comunicarem. Neste cenário, um cliente pode ser direcionado erroneamente para um ponto de gerenciamento de um invasor, em que receberia a política do ponto de gerenciamento não autorizado. Isso seria, provavelmente, a ação de um invasor sofisticado e só poderia ocorrer em um tempo limitado antes de o cliente recuperar a chave de raiz confiável de um ponto de gerenciamento válido. No entanto, para reduzir esse risco de um invasor direcionar clientes para um ponto de gerenciamento não autorizado, você pode pré-provisionar os clientes usando a chave de raiz confiável.  

Use os seguintes procedimentos para pré-provisionar e verificar a chave de raiz confiável para um cliente do Configuration Manager:  

-   Pré-provisionar um cliente usando a chave de raiz confiável com um arquivo.  

-   Pré-provisionar um cliente usando a chave de raiz confiável sem um arquivo.  

-   Verificar a chave de raiz confiável em um cliente.  

> [!NOTE]  
>  Não é necessário pré-provisionar cliente usando a chave de raiz confiável se ele puder obtê-la dos Serviços de Domínio Active Directory ou se estiverem instaladas usando push de cliente. Além disso, não é necessário pré-provisionar clientes quando eles usam a comunicação HTTPS em pontos de gerenciamento, porque a confiança é estabelecida usando certificados PKI.  

É possível remover a chave raiz confiável de um cliente usando a propriedade **RESETKEYINFORMATION = TRUE** do Client.msi com o CCMSetup.exe. Para substituir a chave raiz confiável, reinstale o cliente juntamente com a nova chave raiz confiável, por exemplo, usando o push de cliente ou especificando a propriedade **SMSPublicRootKey** do Client.msi por meio do CCMSetup.exe.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a>Para pré-provisionar um cliente com a chave de raiz confiável usando um arquivo  

1.  Em um editor de texto, abra o arquivo *&lt;Diretório do Configuration Manager\>***\bin\mobileclient.tcf**.  

2.  Localize a entrada **SMSPublicRootKey=**, copie a chave por meio dessa linha e feche o arquivo sem quaisquer alterações.  

3.  Crie um novo arquivo de texto e cole as informações da chave que você copiou do arquivo mobileclient.tcf.  

4.  Salve o arquivo e coloque-o em algum lugar onde todos os computadores possam acessá-lo, mas o arquivo é protegido para evitar violação.  

5.  Instale o cliente usando qualquer método de instalação que aceitar propriedades de Client.msi e especifique a propriedade de Client.msi **SMSROOTKEYPATH=***&lt;Caminho completo e nome do arquivo\>*.  

    > [!IMPORTANT]  
    >  Ao especificar a chave de raiz confiável para segurança adicional durante a instalação do cliente, você também precisa especificar o código do site, usando a propriedade **SMSSITECODE=&lt;código do site\>** do Client.msi.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a>Para pré-provisionar um cliente com a chave de raiz confiável sem usar um arquivo  

1.  Em um editor de texto, abra o arquivo *&lt;Diretório do Configuration Manager\>***\bin\mobileclient.tcf**.  

2.  Localize a entrada SMSPublicRootKey=, anote a chave dessa linha ou copie-a na área de transferência, e feche o arquivo sem quaisquer alterações.  

3.  Instale o cliente usando qualquer método de instalação que aceitar as propriedades de Client.msi e especifique a propriedade de Client.msi **SMSPublicRootKey=***&lt;chave\>*, em que *&lt;chave\>* é a cadeia de caracteres que você copiou de mobileclient.tcf.  

    > [!IMPORTANT]  
    >  Ao especificar a chave de raiz confiável para segurança adicional durante a instalação do cliente, você também precisa especificar o código do site, usando a propriedade **SMSSITECODE=&lt;código do site\>** do Client.msi.  

#### <a name="to-verify-the-trusted-root-key-on-a-client"></a>Para verificar a chave de raiz confiável em um cliente  

1.  No menu **Iniciar** , clique em **Executar**e digite **Wbemtest**.  

2.  Na caixa de diálogo **Testador de Instrumentação de Gerenciamento do Windows** , clique em **Conectar**.  

3.  Na caixa de diálogo **Conectar** , na caixa **Namespace** , digite **root\ccm\locationservices**e clique em **Conectar**.  

4.  Na caixa de diálogo **Testador de Instrumentação de Gerenciamento do Windows** , na seção **IWbemServices** , clique em **Enumerar Classes**.  

5.  Na caixa de diálogo **Informações de Superclasse** , selecione **Recursivo**e clique em **OK**.  

6.  Na janela **Resultado da Consulta** , role para o final da lista e clique duas vezes em **TrustedRootKey ()**.  

7.  Na caixa de diálogo **Editor de objeto para TrustedRootKey** , clique em **Instâncias**.  

8.  Na nova janela **Resultado da Consulta** que exibe as instâncias de **TrustedRootKey**, clique duas vezes em **TrustedRootKey=@**  

9. Na caixa de diálogo **Editor de objeto de TrustedRootKey=@**, na seção **Propriedades**, role para baixo até **TrustedRootKey CIM_STRING**. A cadeia de caracteres na coluna da direita é a chave de raiz confiável. Verifique se ela corresponde ao valor **SMSPublicRootKey** no arquivo *&lt;Diretório do Configuration Manager\>***\bin\mobileclient.tcf**.  

##  <a name="a-namebkmkplanningforsigningencryptiona-planning-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> Planejando para assinatura e criptografia  
 Quando você usa certificados PKI para todas as comunicações do cliente, não precisa planejar assinatura e criptografia para ajudar a proteger o cliente nas comunicação de dados. No entanto, se você configurar qualquer sistema de site que execute IIS para permitir conexões de cliente HTTP, deverá decidir como ajudar a proteger a comunicação do cliente com o site.  

 Para ajudar a proteger os dados que os clientes enviam aos pontos de gerenciamento, é possível requerer que eles sejam assinados. Além disso, você pode requerer que todos os dados assinados de clientes que usam HTTP utilizem o algoritmo SHA-256. Embora esta seja uma configuração mais segura, não habilite esta opção, a menos que todos os clientes deem suporte ao SHA-256. Muitos sistemas operacionais dão suporte nativo ao SHA-256, mas os sistemas operacionais mais antigos podem exigir uma atualização ou hotfix. Por exemplo, computadores que executam Windows Server 2003 SP2 devem instalar um hotfix que é referido no [KB artigo 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  

 Enquanto a assinatura ajuda a proteger os dados contra violação, a criptografia ajuda a proteger os dados contra a divulgação de informações. Você pode habilitar a criptografia de 3DES para dados de inventário e mensagens de estado que os clientes enviam para pontos de gerenciamento no site. Não é necessário instalar nenhuma atualização em clientes para oferecerem suporte para essa opção, mas considere o uso adicional de CPU necessário nos clientes e o ponto de gerenciamento para executar criptografia e decriptografia.  

 Para obter informações sobre como definir as configurações de assinatura e criptografia, consulte a seção [Configurar assinatura e criptografia](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) no tópico [Configurar a segurança no System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

##  <a name="a-namebkmkplanningforrbaa-planning-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> Planejando a administração baseada em funções  
 Para obter essas informações, consulte [Fundamentos da administração baseada em funções no System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  



<!--HONumber=Nov16_HO1-->


