---
title: Planejar a implantação do cliente em computadores Linux e UNIX
titleSuffix: Configuration Manager
description: Planejar a implantação do cliente em computadores Linux e UNIX no Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cfa2a2412744046ca1a16aad2721fcb9efcff38e
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58524142"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-configuration-manager"></a>Planejar a implantação do cliente em computadores Linux e UNIX no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

> [!Important]  
> A partir da versão 1902, o Configuration Manager não dá suporte a clientes Linux ou UNIX. 
> 
> Considere o Gerenciamento do Microsoft Azure para gerenciar servidores Linux. As soluções do Azure têm amplo suporte para Linux que, na maioria dos casos, supera a funcionalidade do Configuration Manager, incluindo o gerenciamento de patches de ponta a ponta para o Linux.

Você pode instalar o cliente do Configuration Manager em computadores que executam o Linux ou o UNIX. Esse cliente é projetado para servidores que funcionam como um computador de grupo de trabalho, e o cliente não oferece suporte à interação com usuários conectados. Após você instalar o software cliente e o cliente estabelecer a comunicação com o site do Configuration Manager, você gerenciará o cliente usando o console e relatórios do Configuration Manager.  

> [!NOTE]
>  O cliente do Configuration Manager para computadores Linux e UNIX não dá suporte aos seguintes recursos de gerenciamento:  
> 
> - Instalação do cliente por push  
>   -   Implantação de sistema operacional  
>   -   Implantação de aplicativos; em vez disso, distribua software usando pacotes e programas.  
>   -   Inventário de software  
>   -   Atualizações de software  
>   -   Configurações de conformidade  
>   -   Controle remoto  
>   -   Gerenciamento de Energia  
>   -   Correção e verificação de cliente do status do cliente  
>   -   Gerenciamento de clientes baseado na Internet  

 Para obter informações sobre as distribuições do Linux e UNIX com suporte e o hardware necessário para dar suporte ao cliente para Linux e UNIX, consulte a seção [Recommended hardware for System Center Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md) (Hardware recomendado para o System Center Configuration Manager).  

 Use as informações neste artigo para ajudá-lo a planejar a implantação do cliente do Configuration Manager para Linux e UNIX.  

##  <a name="BKMK_ClientDeployPrereqforLnU"></a> Pré-requisitos para implantação do cliente em servidores Linux e UNIX  
 Use as informações a seguir para determinar os pré-requisitos, para que você deve ter êxito em vigor instalar o cliente para Linux e UNIX.  

###  <a name="BKMK_ClientDeployExternalforLnU"></a> Dependências externas ao Configuration Manager:  
 As tabelas a seguir descrevem os sistemas operacionais UNIX e Linux necessários, bem como as dependências de pacotes.  

 **Red Hat Enterprise Linux Server versão 5.1 (Tikanga)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas C padrão|2.5-12|  
|Openssl|Bibliotecas OpenSSL; Protocolo de Comunicações de Rede Seguras|0.9.8b-8.3.el5|  
|PAM|Módulos de Autenticação Conectáveis|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server versão 6**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas C padrão|2.12-1.7|  
|Openssl|Bibliotecas OpenSSL; Protocolo de Comunicações de Rede Seguras|1.0.0-4|  
|PAM|Módulos de Autenticação Conectáveis|1.1.1-4|  

 **Red Hat Enterprise Linux Server versão 7**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas C padrão|2.17|  
|Openssl|Bibliotecas OpenSSL; Protocolo de Comunicações de Rede Seguras|1.0.1|  
|PAM|Módulos de Autenticação Conectáveis|1.1.1-4|  

 **Solaris 10 SPARC**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Patch do sistema operacional necessários|Vazamento de memória do PAM|117463-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Math & Microtasking Libraries (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|Openssl|SUNopenssl-librararies (Usr)<br /><br /> O Sun fornece as bibliotecas OpenSSL para Solaris 10 SPARC. Elas estão incluídas no sistema operacional.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Módulos de Autenticação Conectáveis<br /><br /> SUNWcsr, Core Solaris, (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Patch do sistema operacional necessários|Vazamento de memória do PAM|117464-04|  
|SUNWlibC|Sun Workshop compiladores agrupados libC (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Principais Solaris, (bibliotecas compartilhadas) (i386)|11.10.0, REV=2005.01.21.16.34|  
|SUNWcslr|Bibliotecas do Solaris principal (raiz) (i386)|11.10.0, REV=2005.01.21.16.34|  
|Openssl|Bibliotecas de SUNWopenssl; Bibliotecas OpenSSL (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Módulos de Autenticação Conectáveis<br /><br /> Pacotes SUNWcsr Core Solaris, (Root)(i386)|11.10.0, REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0,REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc-2,4-31,30|Biblioteca compartilhada padrão C|2,4-31,30|  
|Openssl|Bibliotecas OpenSSL; Protocolo de Comunicações de Rede Seguras|0.9.8a-18.15|  
|PAM|Módulos de Autenticação Conectáveis|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Biblioteca compartilhada padrão C|2.9-13.2|  
|PAM|Módulos de Autenticação Conectáveis|pam-1.0.2-20.1|  

 **Universal Linux (pacote Debian) Debian, Ubuntu Server**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|libc6|Biblioteca compartilhada padrão C|2.3.6|  
|Openssl|Bibliotecas OpenSSL; Protocolo de Comunicações de Rede Seguras|0.9.8 ou 1.0|  
|PAM|Módulos de Autenticação Conectáveis|0.79-3|  

 **Universal Linux (pacote RPM) CentOS, Oracle Linux**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Biblioteca compartilhada padrão C|2.5-12|  
|Openssl|Bibliotecas OpenSSL; Protocolo de Comunicações de Rede Seguras|0.9.8 ou 1.0|  
|PAM|Módulos de Autenticação Conectáveis|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Versão do SO|Versão do sistema operacional|AIX 6.1: qualquer Nível de Tecnologia e Service Pack|  
|xlC.rte|Tempo de execução XL C/C++|9.0.0.5|  
|OpenSSL/openssl.base|Bibliotecas OpenSSL; Protocolo de Comunicações de Rede Seguras|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Versão do SO|Versão do sistema operacional|AIX 7.1: qualquer Nível de Tecnologia e Service Pack|  
|xlC.rte|Tempo de execução XL C/C++||  
|OpenSSL/openssl.base|Bibliotecas OpenSSL; Protocolo de Comunicações de Rede Seguras||  


 **HP-UX 11i v3 IA64**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|Ambiente operacional HP-UX Foundation|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Bibliotecas específicas de desenvolvimento IA|B.11.31|  
|SysMgmtMin|Ferramentas de Implantação de Softwares Mínimos|B.11.31.0709|  
|SysMgmtMin.openssl|Bibliotecas OpenSSL; Protocolo de Comunicações de Rede Seguras|A.00.09.08d.002|  
|PAM|Módulos de Autenticação Conectáveis|No HP-UX, o PAM faz parte dos componentes centrais do sistema operacional. Não há outras dependências.|  

 **Dependências do Configuration Manager:** a tabela a seguir lista as funções do sistema de sites compatíveis com clientes Linux e UNIX. Para obter mais informações sobre essas funções de sistema de sites, consulte [Adicionar as funções do sistema de sites para os clientes do System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Sistemas de site do Configuration Manager|Mais informações|  
|---------------------------------------|----------------------|  
|Ponto de gerenciamento|Embora não seja necessário um ponto de gerenciamento para instalar um cliente do Configuration Manager no Linux e no UNIX, será necessário ter um ponto de gerenciamento para transferir as informações entre os computadores cliente e os servidores do Configuration Manager. Sem um ponto de gerenciamento, você não pode gerenciar computadores cliente.|  
|Ponto de distribuição|Não é necessário o ponto de distribuição para instalar um cliente do Configuration Manager no Linux e no UNIX. No entanto, a função de sistema de site é necessária se você implantar o software em servidores Linux e UNIX.<br /><br /> Uma vez que o cliente do Configuration Manager para Linux e UNIX não oferece suporte a comunicações que utilizam o SMB, os pontos de distribuição que você usar com o cliente devem dar suporte à comunicação HTTP ou HTTPS.|  
|Ponto de status de fallback|O ponto de status de fallback não é necessário para instalar um cliente do Configuration Manager no Linux e no UNIX. No entanto, o ponto de status de fallback habilita os computadores no site do Configuration Manager a enviar mensagens de estado quando eles não podem se comunicar com um ponto de gerenciamento. Cliente também pode enviar seu status de instalação para o ponto de status de fallback.|  

 **Requisitos de firewall**: verifique se os firewalls não bloqueiam as comunicações entre as portas que você especificar como portas de solicitação do cliente. O cliente para Linux e UNIX se comunica diretamente com os pontos de gerenciamento, pontos de distribuição e pontos de status de fallback.  

 Para obter informações sobre portas de solicitação e de comunicação do cliente, consulte  [Configurar o cliente para Linux e UNIX para localizar pontos de gerenciamento](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="BKMK_PlanningforCommunicationsforLnU"></a> Planejamento da comunicação entre florestas com relações de confiança para servidores Linux e UNIX  
 Os servidores Linux e UNIX que você gerenciada com o Configuration Manager funcionam como clientes de grupo de trabalho e requerem configurações semelhantes às de clientes baseados no Windows que estão em um grupo de trabalho. Para saber mais sobre as comunicações entre computadores em grupos de trabalho, confira as informações a respeito das [comunicações entre florestas do Active Directory](/sccm/core/plan-design/hierarchy/communications-between-endpoints#Plan_Com_X-Forest).  

###  <a name="BKMK_ServiceLocationforLnU"></a> Local do serviço pelo cliente para Linux e UNIX  
 A tarefa de localizar um servidor de sistema de site que fornece o serviço aos clientes é conhecida como serviço local. Ao contrário de um cliente baseado em Windows, o cliente para Linux e UNIX não usa o Active Directory para local do serviço. Além disso, o cliente do Configuration Manager para Linux e UNIX não dá suporte a uma propriedade de cliente que especifica o sufixo de domínio de um ponto de gerenciamento. Em vez disso, o cliente aprende sobre servidores de sistema de site adicionais que fornecem serviços aos clientes de um ponto de gerenciamento conhecidos que você atribuir ao instalar o software cliente.  

 Para saber mais, confira as informações sobre o [local de serviço e como os clientes determinam seu ponto de gerenciamento atribuído](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#BKMK_Plan_Service_Location).  

##  <a name="BKMK_SecurityforLnU"></a> Planejamento de segurança e certificados para servidores Linux e UNIX  
 Para ter uma comunicação segura e autenticada com sites do Configuration Manager, o cliente do Configuration Manager para Linux e UNIX usa o mesmo modelo de comunicação que o cliente do Configuration Manager para Windows.  

 Quando instala o cliente Linux e UNIX, você pode atribuir ao cliente um certificado PKI que permite a ele usar HTTPS para se comunicar com sites do Configuration Manager. Se você não atribuir um certificado PKI, o cliente criará um certificado autoassinado e se comunicará somente via HTTP.  

 Os clientes que recebem um certificado PKI ao instalar usam HTTPS para se comunicar com pontos de gerenciamento. Quando um cliente não consegue localizar um ponto de gerenciamento que oferece suporte a HTTPS, ele voltará para usar HTTP com o certificado PKI fornecido.  

 Quando um cliente Linux ou UNIX usa um certificado PKI, você não precisa aprová-los. Quando um cliente usar um certificado autoassinado, examine as configurações de hierarquia para aprovação do cliente no console do Configuration Manager. Se o método de aprovação do cliente não é **Aprovar automaticamente todos os computadores (não recomendados)**, você deve aprovar manualmente o cliente.  

 Para saber mais sobre como aprovar computadores manualmente, confira as informações sobre como [gerenciar clientes no nó de dispositivos](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode).  

 Para saber mais como usar certificados no Configuration Manager, confira os [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

###  <a name="BKMK_AboutCertsforLnU"></a> Sobre certificados para uso por servidores Linux e UNIX  
 O cliente do Configuration Manager para Linux e UNIX usa um certificado autoassinado ou um certificado PKI X.509, assim como clientes baseados em Windows. Não há nenhuma alteração nos requisitos de PKI para sistemas de sites do Configuration Manager quando você gerencia clientes Linux e UNIX.  

 Os certificados que você usa para clientes Linux e UNIX que se comunicam com sistemas de sites do Configuration Manager devem estar em um formato PKCS nº 12 (Padrão de certificado de chave pública) e é necessário saber a senha para que você possa especificá-la para o cliente ao especificar o certificado PKI.  

 O cliente do Configuration Manager para Linux e UNIX dá suporte a um único certificado PKI e não oferece suporte a vários certificados. Portanto, os critérios de seleção de certificado que você configura para um site do Configuration Manager não se aplicam.  

###  <a name="BKMK_ConfigCertsforLnU"></a> Configuração de certificados para servidores Linux e UNIX  
 Para configurar um cliente do Configuration Manager para servidores Linux e UNIX para usar comunicações HTTPS, você deve configurar o cliente para usar um certificado PKI no momento em que você instalar o cliente. Não é possível provisionar um certificado antes da instalação do software cliente.  

 Ao instalar um cliente que usa um certificado PKI, use o parâmetro de linha de comando `-UsePKICert` para especificar o local e o nome do arquivo PKCS#12 que contém o certificado PKI. Além disso, é preciso usar o parâmetro de linha de comando `-certpw` para especificar a senha do certificado.  

 Se você não especificar `-UsePKICert`, o cliente irá gerar um certificado autoassinado e tentará se comunicar com os servidores do sistema de site usando apenas HTTP.  

##  <a name="BKMK_NoSHA-256"></a> Versões que não dão suporte a SHA-256  
 Os seguintes sistemas operacionais Linux e UNIX que têm suporte como clientes no Configuration Manager foram lançados com versões do OpenSSL que não dão suporte a SHA-256:  

-   Solaris Versão 10 (SPARC/x86)  


 Para gerenciar esses sistemas operacionais com o Configuration Manager, é necessário instalar o cliente do Configuration Manager para Linux e UNIX com a opção de linha de comando que instrui o cliente a ignorar a validação de SHA-256. Os clientes do Configuration Manager que são executados nessas versões de sistema operacional operam em um modo menos seguro que os clientes que dão suporte a SHA-256. Este modo menos seguro de operação tem o seguinte comportamento:  

-   Os clientes não validam a assinatura do servidor de site associada à política que eles solicitam a um ponto de gerenciamento.  

-   Os clientes não validam o hash para pacotes que eles baixam do ponto de distribuição.  

> [!IMPORTANT]  
>  A opção `ignoreSHA256validation` permite que você execute o cliente para computadores Linux e UNIX em um modo menos seguro. Isso é destinado ao uso em plataformas mais antigas que não inclui suporte para SHA-256. Isso é uma substituição de segurança e não é recomendado pela Microsoft, mas há suporte para uso em um ambiente de datacenter segura e confiável.  

 Quando o cliente do Configuration Manager para Linux e UNIX é instalado, o script de instalação verifica a versão do sistema operacional. Por padrão, se a versão do sistema operacional for identificada como tendo sido lançada sem uma versão do OpenSSL que dá suporte a SHA-256, a instalação do cliente do Configuration Manager falhará.  

 Para instalar o cliente do Configuration Manager em sistemas operacionais Linux e UNIX que não foram lançados com uma versão do OpenSSL que dê suporte a SHA-256, você precisará usar a opção de linha de comando de instalação `ignoreSHA256validation`. Quando você usar essa opção de linha de comando em um sistema operacional Linux ou UNIX aplicável, o cliente do Configuration Manager ignorará a validação de SHA-256 e, após a instalação, o cliente não usará o SHA-256 para assinar os dados que envia a sistemas de sites usando HTTP. Para obter informações sobre como configurar clientes Linux e UNIX para usar certificados, confira o [planejamento de segurança e certificados para servidores Linux e UNIX](#BKMK_SecurityforLnU). Confira mais informações sobre a necessidade de SHA-256 em [Configurar assinatura e criptografia](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureSigningEncryption).  

> [!NOTE]  
>  A opção de linha de comando `ignoreSHA256validation` é ignorada em computadores que executam uma versão do Linux e UNIX lançada com versões do OpenSSL que dão suporte a SHA-256.  
