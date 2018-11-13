---
title: Planejar a segurança
titleSuffix: Configuration Manager
description: Veja as práticas recomendadas de segurança e informações sobre segurança no Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e03c2b53044225eeb790d70474868e337a4cc997
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411452"
---
# <a name="plan-for-security-in-configuration-manager"></a>Planejar a segurança no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo descreve os conceitos a serem consideradas ao planejar a segurança com a implementação do Configuration Manager. Ele inclui as seguintes seções:  

- [Planejar certificados (autoassinados e PKI)](#BKMK_PlanningForCertificates)  
    - [Certificados CNG (Criptografia: Próxima Geração)](#bkmk_plan-cng)  
    - [HTTP aprimorado](#bkmk_plan-ehttp)  
    - [Certificados para CMG e CDP](#bkmk_plan-cmgcdp)  
    - [O certificado de autenticação (autoassinado) do servidor do site](#bkmk_plansitesign)  
    - [Revogação de certificado PKI](#BKMK_PlanningForCRLs)  
    - [Certificados de raiz confiável PKI e os emissores de certificados](#BKMK_PlanningForRootCAs)  
    - [Seleção de certificado de cliente PKI](#BKMK_PlanningForClientCertificateSelection)  
    - [Uma estratégia de transição para certificados PKI e gerenciamento de clientes baseados na Internet](#BKMK_PlanningForPKITransition)  

- [Planejar-se para a chave de raiz confiável](#BKMK_PlanningForRTK)  

- [Planejar-se para a assinatura e criptografia](#BKMK_PlanningForSigningEncryption)  

- [Planejar-se para a administração baseada em funções](#BKMK_PlanningForRBA)  

- [Planejar-se para o Azure Active Directory](#bkmk_planazuread)  



##  <a name="BKMK_PlanningForCertificates"></a> Planejar certificados (autoassinados e PKI)  

 O Configuration Manager usa uma combinação de certificados autoassinados e certificados PKI (infraestrutura de chave pública).  

 Use certificados PKI sempre que possível. Para obter mais informações, veja [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements). Quando o Configuration Manager solicita os certificados PKI durante o registro de dispositivos móveis, você precisa usar o Active Directory Domain Services e uma autoridade de certificação corporativa. Para todos os outros certificados PKI, implante e gerencie-os independentemente do Configuration Manager. 

 Certificados PKI são solicitados quando computadores cliente conectam-se a sistemas de site baseados na Internet. Alguns cenários com o gateway de gerenciamento de nuvem e o ponto de distribuição de nuvem também exigem certificados PKI. Para obter mais informações, veja [Gerenciar clientes na Internet](/sccm/core/clients/manage/manage-clients-internet).

 Quando você usa uma PKI, também pode usar IPsec para ajudar a proteger a comunicação de servidor para servidor entre sistemas de sites em um site, entre sites e para outras transferências de dados entre computadores. A implementação do IPsec é independente do Configuration Manager.  

 Quando certificados PKI não estiverem disponíveis, o Configuration Manager gerará certificados autoassinados automaticamente. Alguns certificados no Configuration Manager são sempre autoassinados. Na maioria dos casos, o Configuration Manager gerencia automaticamente os certificados autoassinados e você não precisa tomar medidas adicionais. Um exemplo é o certificado de assinatura do servidor do site. Esse certificado é sempre autoassinado. Ele garante que as políticas que os clientes baixam do ponto de gerenciamento tenham sido enviadas do servidor do site e que não tenham sido violadas.  


### <a name="bkmk_plan-cng"></a> Certificados CNG (Criptografia: Próxima Geração)  

 O Configuration Manager dá suporte a certificados CNG (Criptografia: Próxima Geração). Os clientes do Configuration Manager podem usar o certificado de autenticação de cliente de PKI com chave privada no KSP (provedor de armazenamento de chaves) da CNG. Com o suporte do KSP, os clientes do Configuration Manager dão suporte para chave de privada baseada em hardware, como TPM KSP para certificados de autenticação de cliente de PKI. Para obter mais informações, consulte [Visão geral dos certificados CNG](/sccm/core/plan-design/network/cng-certificates-overview).


### <a name="bkmk_plan-ehttp"></a> HTTP aprimorado  

 Usar comunicação HTTPS é recomendado para todos os caminhos de comunicação do Configuration Manager, mas é um desafio para alguns clientes devido à sobrecarga de gerenciamento de certificados PKI. A introdução da integração do Azure AD (Azure Active Directory) reduz alguns, mas não todos os requisitos de certificado. Da versão 1806 em diante, você pode habilitar o site para usar **HTTP aprimorado**. Essa configuração dá suporte a HTTPS em sistemas de sites usando uma combinação de certificados autoassinados e o Azure AD. Não requer PKI. Para obter mais informações, confira [HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http).  


### <a name="bkmk_plan-cmgcdp"></a> Certificados para CMG e CDP

Gerenciar clientes na Internet por meio do CMG (gateway de gerenciamento de nuvem) e do CDP (ponto de distribuição de nuvem) requer o uso de certificados. O número e o tipo de certificados variam de acordo com seus cenários específicos. Para obter mais informações, consulte os seguintes artigos:
- [Certificados para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)  
- [Certificados para o ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_certs)  


### <a name="bkmk_plansitesign"></a> Planejar o certificado de autenticação (autoassinado) do servidor do site  

 Os clientes podem obter com segurança uma cópia do certificado de autenticação do servidor do site do Active Directory Domain Services e da instalação do cliente por push. Se os clientes não puderem obter uma cópia desse certificado por um desses mecanismos, instale-o quando você instalar o cliente. Esse processo será especialmente importante se a primeira comunicação do cliente com o site for com um ponto de gerenciamento baseado na Internet. Uma vez que esse servidor está conectado a uma rede não confiável, ele está mais vulnerável a ataques. Se você não seguir essa etapa adicional, os clientes baixarão automaticamente uma cópia do certificado de autenticação do servidor do site do ponto de gerenciamento.  

 Os clientes com segurança não podem obter uma cópia do certificado do servidor do site nos seguintes cenários:  

 - Você não instala o cliente por push e:  

    - Você não estendeu o esquema do Active Directory para o Configuration Manager.  

    - Você não publicou o site do cliente no Active Directory Domain Services.  

    - O cliente é de uma floresta ou de um grupo de trabalho não confiável.  

 - Você está usando o gerenciamento de clientes baseados na Internet e instala o cliente quando ele está na Internet.  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Para instalar clientes com uma cópia do certificado de autenticação do servidor do site  

1.  Localize o certificado de autenticação do servidor do site no servidor do site principal. O certificado é armazenado no repositório de certificados **SMS** do Windows. Ele tem o nome da Entidade **Servidor do Site** e o nome amigável **Certificado de Assinatura do Servidor do Site**.  

2.  Exporte o certificado sem a chave privada, armazene o arquivo com segurança e acesse-o apenas de um canal protegido.  

3.  Instale o cliente usando a propriedade Client.msi a seguir: `SMSSIGNCERT=<full path and file name>`  


###  <a name="BKMK_PlanningForCRLs"></a> Planejar a revogação de certificados PKI  

Quando você usa certificados PKI com o Configuration Manager, planeje usar uma CRL (lista de certificados revogados). Dispositivos usam a CRL para verificar o certificado no computador que está se conectando. CRL é um arquivo que uma AC (autoridade de certificação) cria e assina. Ele tem uma lista de certificados que a AC emitiu, mas revogou. Quando um administrador de certificado Revoga os certificados, sua impressão digital é adicionada à CRL. Por exemplo, se houver suspeita ou confirmação de comprometimento de um certificado emitido.

> [!IMPORTANT]  
>  Como a localização da CRL é adicionada ao certificado quando ele é emitido por uma AC, planeje a CRL antes de implantar os certificados PKI que o Configuration Manager usa.  

O IIS sempre verifica a CRL quanto a certificados de cliente e você não pode alterar essa configuração no Configuration Manager. Por padrão, os clientes do Configuration Manager sempre verificam a CRL para os sistemas de sites. Desabilite essa configuração especificando uma propriedade do site e especificando uma propriedade CCMSetup.  

Computadores que usam a verificação de revogação de certificados, mas não conseguem localizar a CRL, comportam-se como se todos os certificados na cadeia de certificação estivessem revogados. Esse comportamento ocorre porque eles não conseguem verificar se os certificados estão na lista. Nesse cenário, todas as conexões que requerem certificados e usam uma CRL falham.  

Verificar a CRL sempre que um certificado é usado oferece mais segurança contra o uso de um certificado revogado. No entanto, introduz um atraso de conexão e processamento adicional no cliente. Sua organização pode exigir a verificação de segurança adicional para os clientes na Internet ou em uma rede não confiável.  

Consulte seus administradores PKI antes de decidir se os clientes do Configuration Manager devem verificar a CRL. Em seguida, considere manter essa opção habilitada no Configuration Manager quando as duas condições a seguir forem verdadeiras:  

-   sua infraestrutura de PKI dá suporte a uma CRL e é publicada em um local em que todos os clientes do Configuration Manager podem localizá-la. Esses clientes podem incluir dispositivos na Internet e aqueles em florestas não confiáveis.  

-   O requisito de verificar a CRL para cada conexão a um sistema de sites configurado para usar um certificado PKI é maior do que os seguintes requisitos:  
    - Conexões mais rápidas  
    - Processamento eficiente no cliente  
    - O risco de os clientes não conseguirem se conectar a servidores caso não consigam localizar a CRL  


###  <a name="BKMK_PlanningForRootCAs"></a> Planejar certificados PKI de raiz confiável e a lista de emissores de certificados  

Se os sistemas de site do IIS usam certificados de cliente PKI para autenticação do cliente via HTTP ou para autenticação do cliente e criptografia via HTTPS, você deve importar certificados de AC raiz como uma propriedade do site. Aqui estão os dois cenários:  

-   Você implanta sistemas operacionais usando o Configuration Manager e os pontos de gerenciamento aceitam somente conexões de cliente HTTPS.  

-   Você usa certificados de cliente PKI que não são encadeados a um certificado raiz em que os pontos de gerenciamento confiam.  

    > [!NOTE]  
    >  Ao emitir certificados PKI de clientes da mesma hierarquia de CA que emite os certificados do servidor que você usa para pontos de gerenciamento, você não precisa especificar esse Certificado de Autoridade de Certificação raiz. No entanto, se você usar várias hierarquias de CA e não tiver certeza se elas têm confiança entre si, importe a AC raiz para a hierarquia de CA dos clientes.  

Se você precisar importar certificados de AC raiz para o Configuration Manager, exporte-os da AC emissora ou do computador cliente. Se você exportar o certificado da AC emissora que também é a AC raiz, lembre-se de não exportar a chave privada. Armazene o arquivo de certificado exportado em um local seguro para impedir a violação. Você precisa ter acesso ao arquivo ao configurar o site. Se você acessar o arquivo pela rede, verifique se a comunicação está protegida contra violação usando IPsec.  

Se algum Certificado de AC raiz que você importa for renovado, você deverá importar o certificado renovado.  

Esses certificados de AC raiz importados e o certificado de AC raiz de cada ponto de gerenciamento criam a lista de emissores de certificado que os computadores do Configuration Manager usam das seguintes maneiras:  

-   Quando clientes se conectam a pontos de gerenciamento, o ponto de gerenciamento verifica se o certificado do cliente está encadeado a um certificado de raiz confiável na lista de emissores de certificado do site. Caso não se encadeie, o certificado será rejeitado e ocorrerá falha na conexão PKI.  

-   Quando clientes selecionam um certificado PKI e têm uma lista de emissores do certificado, eles selecionam um certificado que se encadeie a um certificado de raiz confiável na lista de emissores do certificado. Se não houver nenhuma correspondência, o cliente não selecionará um certificado PKI. Para obter mais informações, confira [Planejar a seleção de certificado de cliente PKI](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="BKMK_PlanningForClientCertificateSelection"></a> Planejar a seleção de certificados PKI de cliente  

 Se os sistemas de sites do IIS usarem certificados PKI de cliente para autenticação via HTTP ou para autenticação do cliente e criptografia via HTTPS, planeje como os clientes Windows selecionarão o certificado a ser usado para o Configuration Manager.  

> [!NOTE]  
>  Alguns dispositivos não dão suporte a um método de seleção de certificado. Em vez disso, eles selecionam automaticamente o primeiro certificado que atende aos requisitos de certificado. Por exemplo, clientes em computadores Mac e dispositivos móveis não dão suporte a um método de seleção de certificado.  

Em muitos casos, a configuração e o comportamento padrão são suficientes. O cliente do Configuration Manager em computadores Windows filtra vários certificados usando esses critérios, nessa ordem:  

1.  A lista de emissores do certificado: o certificado está encadeado a uma AC raiz confiável pelo ponto de gerenciamento.  

2.  O certificado está no repositório de certificados padrão **Pessoal**.  

3.  O certificado é válido, não revogado e não expirou. A verificação de validade também verifica se a chave privada está acessível.  

4.  O certificado tem uma funcionalidade de autenticação do cliente ou é emitido para o nome do computador.  

5.  O certificado tem o período de validade mais longo.  

Configure clientes para usarem a lista de emissores do certificado por meio dos seguintes mecanismos:  

-   Publique-o com informações de site do Configuration Manager para o Active Directory Domain Services.  

-   Instale clientes por push.  

-   Os clientes baixam o certificado do ponto de gerenciamento depois de terem sido atribuídos com êxito ao site.  

-   Especifique-o durante a instalação do cliente, como uma propriedade CCMSetup client.msi de CCMCERTISSUERS.  

Clientes que não têm a lista de emissores do certificado quando forem instalados pela primeira vez e ainda não estiverem atribuídos ao site ignoram essa verificação. Quando os clientes tiverem a lista de emissores de certificado e não tiverem um certificado de PKI encadeado a um certificado raiz confiável na lista de emissores de certificados, a seleção de certificado falhará. Os clientes não continuam com os outros critérios de seleção de certificado.  

Na maioria dos casos, o cliente do Configuration Manager identifica corretamente um certificado PKI único e apropriado. No entanto, quando esse comportamento não for o caso, em vez de selecionar o certificado baseado na funcionalidade de autenticação do cliente, você pode configurar dois métodos de seleção alternativos:  

-   Uma correspondência parcial de cadeia de caracteres no nome da entidade do certificado do cliente. Esse método é uma correspondência que não diferencia maiúsculas de minúsculas. É apropriado se você está usando o FQDN (nome de domínio totalmente qualificado) de um computador no campo da entidade e deseja que a seleção do certificado seja baseada no sufixo do domínio, por exemplo, **contoso.com**. Entretanto, você pode usar esse método de seleção para identificar alguma cadeia de caracteres sequencial no nome da entidade do certificado que diferencia o certificado dos outros no repositório de certificados do cliente.  

    > [!NOTE]  
    >  Você não pode usar a correspondência parcial de cadeia de caracteres com o SAN (nome alternativo da entidade) como uma configuração do site. Embora você possa especificar uma correspondência parcial de cadeia de caracteres para o SAN usando CCMSetup, ela será substituída pelas propriedades do site nos seguintes cenários:  
    >   
    >  -   Clientes recuperam informações do site que são publicadas no Active Directory Domain Services.  
    > -   Clientes são instalados por push.  
    >   
    >  Use uma correspondência parcial de cadeia de caracteres na SAN somente ao instalar clientes manualmente e quando eles não recuperarem informações de site do Active Directory Domain Services. Por exemplo, essas condições só se aplicam a clientes da Internet.  

-   Uma correspondência nos valores de atributo de nome da entidade do certificado do cliente ou valores de atributo da SAN (nome alternativo da entidade). Esse método é uma correspondência que diferencia maiúsculas de minúsculas. Será apropriado se você estiver usando um nome diferenciado X500 ou OIDs (identificadores de objeto) equivalentes em conformidade com a RFC 3280 e se desejar que a seleção do certificado seja baseada em valores de atributos. Você só pode especificar os atributos e seus valores necessários para identificar ou validar com exclusividade o certificado e diferenciá-lo de outros no armazenamento de certificados.  

A tabela a seguir mostra os valores de atributo a que o Configuration Manager dá suporte como critérios de seleção de certificados do cliente.  

|Atributo OID|Atributo de nome diferenciado|Definição de atributo|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Componente do domínio|  
|1.2.840.113549.1.9.1|E ou email|Endereço de email|  
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

Se mais de um certificado apropriado for localizado após a aplicação dos critérios de seleção, você poderá substituir a configuração padrão para selecionar o certificado que tem o período de validade mais longo e, em vez disso, especificar que nenhum certificado foi selecionado. Nesse cenário, o cliente não será capaz de se comunicar com sistemas de site IIS com um certificado PKI. O cliente envia uma mensagem de erro ao seu ponto de status de fallback atribuído para alertá-lo sobre a falha na seleção do certificado para que você possa alterar ou aperfeiçoar seus critérios de seleção. O comportamento do cliente, então, depende se a falha da conexão foi em HTTPS ou HTTP:  

-   Se a conexão com falha for via HTTPS: o cliente tentará se conectar via HTTP e usará o certificado autoassinado do cliente.  

-   Se a conexão com falha for via HTTP: o cliente tentará se conectar novamente via HTTP usando o certificado autoassinado do cliente.  

Para ajudar a identificar um certificado PKI único de cliente, você também pode especificar um repositório personalizado, diferente do padrão **Pessoal** no repositório do **Computador**. No entanto, você deve criar esse repositório independentemente do Configuration Manager. Você deve ser capaz de implantar certificados neste repositório personalizado e renová-los antes que o período de validade expire.  

Para obter mais informações, confira [Definir as configurações para certificados PKI do cliente](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureClientPKI).  


###  <a name="BKMK_PlanningForPKITransition"></a> Planejar uma estratégia de transição para certificados PKI e gerenciamento de clientes baseados na Internet  

As opções de configuração flexíveis do Configuration Manager permitem que você faça a transição gradual dos clientes e do site para usar certificados PKI e ajudar a proteger os pontos de extremidade do cliente. Os certificados PKI fornecem maior segurança e permitem gerenciar os clientes da Internet.  

Devido ao grande número de escolhas e opções de configuração no Configuration Manager, não há uma maneira única de fazer a transição de um site de forma que todos os clientes usem conexões HTTPS. No entanto, você pode seguir estas etapas como orientação:  

1.  Instale o site do Configuration Manager e configure-o de modo que os sistemas de sites aceitem conexões de clientes via HTTPS e HTTP.  

2.  Configure a guia **Comunicação do Computador Cliente** nas propriedades do site para que as **Configurações do Sistema de Sites** sejam **HTTP ou HTTPS**, e selecione **Usar certificado de cliente PKI (funcionalidade de autenticação de cliente) quando disponível**.  Para obter mais informações, confira [Definir as configurações para certificados PKI do cliente](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureClientPKI).  

3.  Coordene uma distribuição de PKI para certificados de cliente. Para um exemplo de implantação, confira [Implantar o certificado do cliente para computadores Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).  

4.  Instale clientes usando o método de instalação por push do cliente. Para obter mais informações, confira [Como instalar clientes do Configuration Manager por push](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).  

5.  Monitore a implantação e o status do cliente usando os relatórios e as informações no console do Configuration Manager.  

6.  Controle quantos clientes estão usando um certificado PKI de cliente visualizando a coluna **Certificado do Cliente** no workspace **Ativos e Conformidade**, nó **Dispositivos**.  

     Você também pode implantar a Ferramenta de Avaliação de Prontidão do Configuration Manager HTTPS (**cmHttpsReadiness.exe**) nos computadores. Em seguida, use os relatórios para exibir o número de computadores que podem usar um certificado PKI de cliente com o Configuration Manager.  

    > [!NOTE]  
    >  Quando você instala o cliente do Configuration Manager, ele instala a ferramenta **CMHttpsReadiness.exe** na pasta `%windir%\CCM`. As opções de linha de comando a seguir estão disponíveis quando você executa esta ferramenta:  
    >   
    > - `/Store:<name>`: essa opção é igual à propriedade client.msi **CCMCERTSTORE**  
    > - `/Issuers:<list>`: essa opção é igual à propriedade client.msi **CCMCERTISSUERS**    
    > - `/Criteria:<criteria>`: essa opção é igual à propriedade client.msi **CCMCERTSEL**    
    > - `/SelectFirstCert`: essa opção é igual à propriedade client.msi **CCMFIRSTCERT**    
    >   
    >  Para obter mais informações, veja [Sobre propriedades de instalação do cliente](/sccm/core/clients/deploy/about-client-installation-properties).  

7.  Quando estiver confiante de que um número suficiente de clientes está usando com sucesso o certificado PKI de cliente para autenticação via HTTP, siga essas etapas:  

    1.  Implante um certificado do servidor Web de PKI em um servidor membro que execute um ponto de gerenciamento adicional para o site e configure o certificado no IIS. Para obter mais informações, confira [Implantar o certificado do servidor Web para sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  

    2.  Instale a função de ponto de gerenciamento no servidor e configure a opção **Conexões de Cliente** nas propriedades do ponto de gerenciamento de **HTTPS**.  

8.  Monitore e verifique se os clientes que têm um certificado PKI usam o novo ponto de gerenciamento ao usar o HTTPS. Você pode usar o registro em log do IIS ou contadores de desempenho para verificar.  

9. Reconfigure as outras funções de sistema de site para usar conexões de cliente HTTPS. Se você quiser gerenciar clientes na Internet, verifique se os sistemas de site têm um FQDN de Internet. Configure pontos de gerenciamento individuais e pontos de distribuição para aceitar conexões de clientes da Internet.  

    > [!IMPORTANT]  
    >  Antes de configurar as funções do sistema de sites para aceitar conexões da Internet, examine as informações de planejamento e os pré-requisitos para gerenciamento de clientes baseados na Internet. Para obter mais informações, veja [Comunicações entre pontos de extremidade](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

10. Estenda a distribuição de certificado PKI de clientes e sistemas de sites que executam o IIS. Configure as funções do sistema de site para conexões de cliente HTTPS e conexões de Internet conforme necessário.  

11. Para maior segurança: quando estiver seguro de que todos os clientes estão usando um certificado PKI de cliente para autenticação e criptografia, altere as propriedades do site para usar somente HTTPS.  

 Esse plano primeiro apresenta certificados PKI para autenticação somente via HTTP e, em seguida, para autenticação e criptografia via HTTPS. Quando você segue esse plano para introduzir gradualmente esses certificados, pode reduzir o risco de os clientes se tornarem não gerenciados. Você também se beneficia da maior segurança à qual o Configuration Manager dá suporte.  

##  <a name="BKMK_PlanningForRTK"></a> Planejar a chave de raiz confiável  

 A chave de raiz confiável do Configuration Manager fornece um mecanismo para os clientes do Configuration Manager verificarem se os sistemas de sites pertencem à sua hierarquia. Cada servidor de site gera uma chave de troca de site para se comunicar com outros sites. A chave de troca do site de nível superior na hierarquia é chamada de chave de raiz confiável.  

 A função da chave raiz confiável no Configuration Manager é semelhante a um certificado raiz em uma infraestrutura de chave pública. Qualquer item assinado pela chave privada da chave de raiz confiável tem confiança mais abaixo na hierarquia. Os clientes armazenam uma cópia da chave de raiz confiável do site na **root\ccm\locationservices** namespace WMI. 

 Por exemplo, o site emite um certificado para o ponto de gerenciamento, que ele assina com a chave privada da chave de raiz confiável. O site compartilha com os clientes a chave pública de sua chave de raiz confiável. Então os clientes podem diferenciar entre os pontos de gerenciamento que estão em sua hierarquia e os pontos de gerenciamento que não estão em sua hierarquia.   

 Os clientes recuperam automaticamente a cópia pública da chave de raiz confiável usando dois mecanismos:  

 - Você estende o esquema do Active Directory para Configuration Manager e publica o site no Active Directory Domain Services. Em seguida, os clientes recuperam informações do site de um servidor de catálogo global. Para obter mais informações, consulte [Preparar o Active Directory para publicação de sites](/sccm/core/plan-design/network/extend-the-active-directory-schema).  

 - Quando você instala clientes usando o método de instalação do cliente por push. Para saber mais, confira [Instalação no cliente por push](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation).  

 Se os clientes não puderem recuperar a chave de raiz confiável usando um desses mecanismos, eles confiarão na chave de raiz confiável fornecida pelo primeiro ponto de gerenciamento com o qual se comunicarem. Neste cenário, um cliente pode ser direcionado erroneamente para um ponto de gerenciamento de um invasor, em que receberia a política do ponto de gerenciamento não autorizado. Esta ação requer um invasor sofisticado. Esse ataque é limitado ao curto tempo antes de o cliente recuperar a chave raiz confiável de um ponto de gerenciamento válido. Para reduzir esse risco de um invasor direcionar clientes para um ponto de gerenciamento invasor, pré-provisione os clientes com a chave de raiz confiável.  

 Use os seguintes procedimentos para pré-provisionar e verificar a chave de raiz confiável para um cliente do Configuration Manager:  

 - [Pré-provisionar um cliente com a chave de raiz confiável usando um arquivo](#bkmk_trk-provision-file)  

 - [Pré-provisionar um cliente com a chave de raiz confiável sem usar um arquivo](#bkmk_trk-provision-nofile)  

 - [Verificar a chave de raiz confiável em um cliente](#bkmk_trk-verify)  

 - [Remover ou substituir a chave de raiz confiável](#bkmk_trk-reset)  

 > [!NOTE]  
 > Se os clientes puderem obter a chave de raiz confiável do Active Directory Domain Services ou o cliente por push, você não precisará provisioná-la previamente. 
 > 
 > Quando os clientes usam comunicação HTTPS em pontos de gerenciamento, você não precisa pré-provisionar a chave raiz confiável. Eles estabelecem confiança pelos certificados PKI.  


### <a name="bkmk_trk-provision-file"></a> Pré-provisionar um cliente com a chave de raiz confiável usando um arquivo  

1.  No servidor do site, abra o arquivo a seguir em um editor de texto: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Localize a entrada **SMSPublicRootKey=**. Copie a chave por meio dessa linha e feche o arquivo sem quaisquer alterações.  

3.  Crie um novo arquivo de texto e cole as informações da chave que você copiou do arquivo mobileclient.tcf.  

4.  Salve o arquivo em uma localização em que todos os computadores possam acessá-lo, mas em que o arquivo esteja protegido contra violação.  

5.  Instale o cliente usando qualquer método de instalação que aceite propriedades client.msi. Especifique a propriedade a seguir: `SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    >  Quando você especifica a chave raiz confiável durante a instalação do cliente, especifique também o código do site. Use a propriedade de client.msi a seguir: `SMSSITECODE=<site code>`   


### <a name="bkmk_trk-provision-nofile"></a> Pré-provisionar um cliente com a chave de raiz confiável sem usar um arquivo  

1.  No servidor do site, abra o arquivo a seguir em um editor de texto: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Localize a entrada **SMSPublicRootKey=**. Copie a chave por meio dessa linha e feche o arquivo sem quaisquer alterações.  

3.  Instale o cliente usando qualquer método de instalação que aceite propriedades client.msi. Especifique a propriedade client.msi a seguir: `SMSPublicRootKey=<key>` em que `<key>` é a cadeia de caracteres que você copiou de mobileclient.tcf.  

    > [!IMPORTANT]  
    >  Quando você especifica a chave raiz confiável durante a instalação do cliente, especifique também o código do site. Use a propriedade de client.msi a seguir: `SMSSITECODE=<site code>`   


### <a name="bkmk_trk-verify"></a> Verificar a chave de raiz confiável em um cliente  

1. Abra um console do Windows PowerShell como administrador.  

2. Execute o seguinte comando:  

``` PowerShell
 (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
```

A cadeia de caracteres retornada é a chave de raiz confiável. Verifique se corresponde ao valor **SMSPublicRootKey** no arquivo mobileclient.tcf no servidor do site.  


### <a name="bkmk_trk-reset"></a> Remover ou substituir a chave de raiz confiável  

 Remova a chave raiz de confiável de um cliente usando a propriedade do client.msi **RESETKEYINFORMATION=TRUE**. 

 Para substituir a chave de raiz confiável, reinstale o cliente juntamente com a nova chave de raiz confiável. Por exemplo, use o push de cliente ou especifique a propriedade client.msi **SMSPublicRootKey**.  

 Para obter mais informações sobre essas propriedades de instalação, confira [Sobre os parâmetros e as propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).



##  <a name="BKMK_PlanningForSigningEncryption"></a> Planejar assinatura e criptografia  
 
 Quando você usa certificados PKI para todas as comunicações do cliente, não precisa planejar a assinatura nem a criptografia para ajudar a proteger o cliente na comunicação de dados. Se você configurar qualquer sistema de sites que execute IIS para permitir conexões de cliente HTTP, decida como ajudar a proteger a comunicação do cliente com o site.  

 Para ajudar a proteger os dados que os clientes enviam aos pontos de gerenciamento, é possível exigir que os clientes assinem os dados. Você também pode exigir o algoritmo SHA-256 para assinatura. Essa configuração é mais segura, mas não exige o SHA-256, a menos que todos os clientes deem suporte a ele. Muitos sistemas operacionais dão suporte nativo a esse algoritmo, mas os sistemas operacionais mais antigos podem exigir uma atualização ou hotfix. 

 Embora a assinatura ajude a proteger os dados contra violação, a criptografia ajuda a proteger os dados contra a divulgação de informações. Você pode habilitar a criptografia de 3DES para dados de inventário e mensagens de estado que os clientes enviam para pontos de gerenciamento no site. Você não precisa instalar nenhuma atualização nos clientes para dar suporte a essa opção. Os clientes e os pontos de gerenciamento exigem o uso de CPU adicional para criptografia e descriptografia.  

 Para obter mais informação sobre como definir as configurações para assinatura e criptografia, confira [Configurar assinatura e criptografia](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureSigningEncryption).  



##  <a name="BKMK_PlanningForRBA"></a> Planejar a administração baseada em funções  

 Para obter mais informações, consulte [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).  



## <a name="bkmk_planazuread"></a> Planejar-se para o Azure Active Directory

 O Configuration Manager integra-se ao Azure AD (Azure Active Directory) para habilitar o site e os clientes a usar autenticação moderna. Integrar seu site com o Azure AD dá suporte aos seguintes cenários do Configuration Manager:

**Cliente**  

- [Gerenciar clientes na Internet via gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

- [Gerenciar dispositivos ingressados no domínio de nuvem](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

- [Cogerenciamento](/sccm/core/clients/manage/co-management-overview)  

- [Implantar aplicativos disponíveis para o usuário](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)  

- [Aplicativos online da Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

- Reduzia os requisitos de infraestrutura. Por exemplo, [Centro de Software usando o ponto de gerenciamento](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex), em vez do catálogo de aplicativos  

- [Gerenciar aplicativos do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates)  


**Servidor**  

- [Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness)  

- [Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics)  

- [Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics)  

- [Hub de Comunidade](/sccm/core/get-started/capabilities-in-technical-preview-1807#bkmk_hub)  

- [Ponto de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- [Descoberta de usuário](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  


 Para obter mais informações sobre como conectar seu site ao Azure AD, confira [Configurar serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).


 Para obter mais informações sobre o Azure AD, confira [Documentação do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).



## <a name="see-also"></a>Consulte também
- [Segurança e privacidade para clientes do Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configurar a segurança](/sccm/core/plan-design/security/configure-security)  

- [Comunicação entre pontos de extremidade](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Referência técnica de controles de criptografia](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  

- [Requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements)  

