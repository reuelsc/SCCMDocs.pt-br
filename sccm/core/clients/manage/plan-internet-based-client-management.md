---
title: Gerenciamento de cliente baseado na Internet | Microsoft Docs
description: Crie um plano para gerenciar clientes baseados na Internet no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: 82867e77840e14e9b8170801ea3c4a9f399c9890


---
# <a name="plan-for-internet-based-client-management-in-system-center-configuration-manager"></a>Planejar o gerenciamento de clientes baseados na Internet no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O gerenciamento de clientes baseado na Internet (às vezes chamado de IBCM) permite que você gerencie clientes do System Center Configuration Manager quando eles não estão conectados à rede da empresa, mas têm uma conexão de Internet padrão. Este arranjo tem várias vantagens, que incluem os custos reduzidos de não ter de executar VPNs (Redes Virtuais Privadas) e ser capaz de implantar atualizações de software de uma maneira oportuna.  

 Por causa dos mais altos requisitos de segurança de gerenciar computadores cliente em uma rede pública, o gerenciamento de clientes baseado na Internet requer que os clientes e servidores do sistema de site se conectem para usar certificados PKI. Isso garante que as conexões sejam autenticadas por uma autoridade independente, e que os dados de e para esses sistemas de site sejam criptografados usando protocolo SSL.  

 Use as seções a seguir para ajudá-lo a planejar o gerenciamento de clientes baseado na Internet.  

##  <a name="a-namebkmkibcmfeaturesnotsupporteda-features-that-are-not-supported-on-the-internet"></a><a name="BKMK_IBCM_FeaturesNotSupported"></a> Recursos sem suporte na Internet  
 Nem todas as funcionalidades do gerenciamento de cliente são adequadas para a Internet, portanto, não têm suporte quando os clientes são gerenciados na Internet. Os recursos sem suporte para gerenciamento na Internet normalmente contam com os Serviços de Domínio Active Directory ou não são apropriados para uma rede pública, como a descoberta de rede e o WOL (Wake-on-LAN).  

 Os seguintes recursos não têm suporte quando os clientes são gerenciados na Internet:  

-   Implantação de cliente na Internet, como a implantação por push e implantação de cliente com base em atualizações de software. Em vez disso, use a instalação manual do cliente.  

-   Atribuição automática de site.  

-   Wake on LAN.  

-   Implantação de sistema operacional. No entanto, você pode implantar sequências de tarefas que não implantam um sistema operacional, por exemplo, sequências de tarefas que executam scripts e tarefas de manutenção em clientes.  

-   Controle remoto.  

-   Implantação de software para usuários a menos que o ponto de gerenciamento baseado na Internet possa autenticar o usuário nos Serviços de Domínio Active Directory usando a autenticação do Windows (Kerberos ou NTLM). Isso é possível quando o ponto de gerenciamento baseado na Internet tem uma relação de confiança na floresta onde reside a conta do usuário.  

 Além disso, o gerenciamento de clientes baseado na Internet não oferece suporte a roaming. O roaming permite que os clientes sempre localizem os pontos de distribuição mais próximos para baixar conteúdo. Clientes que são gerenciados na Internet comunicam-se com sistemas de site por meio de seu site atribuído quando esses sistemas são configurados para usar um FQDN de Internet e as funções do sistema de site permitem conexões do cliente por meio da Internet. Clientes, de forma não determinista, selecionam um dos sistemas de áreas baseados na Internet, independentemente da largura de banda ou local físico.  

 Quando você tem um ponto de atualização de software configurado para aceitar conexões da Internet, os clientes baseados na Internet do Configuration Manager sempre são verificados em relação a esse ponto de atualização de software, para determinar quais atualizações de software são necessárias. No entanto, quando esses clientes estão na Internet, primeiro tentam baixar as atualizações de software do Microsoft Update, em vez de fazer isso de um ponto de distribuição baseado na Internet. Somente se isso falhar, eles tentarão baixar as atualizações de software necessárias de um ponto de distribuição baseado na Internet. Clientes que não estão configurados para gerenciamento de clientes baseado na Internet nunca tentam baixar atualizações de software do Microsoft Update, mas sempre usam os pontos de distribuição do Configuration Manager.  

##  <a name="a-namebkmkplanforinternetsitesystemsa-considerations-for-client-communications-from-the-internet-or-untrusted-forest"></a><a name="BKMK_PlanforInternetSiteSystems"></a> Considerações sobre a comunicação do cliente da Internet ou de uma floresta não confiável  
 As seguintes funções de sistema de site instaladas em sites primários oferecem suporte a conexões de clientes que estão em locais não confiáveis, como a Internet ou uma floresta não confiável (sites secundários não oferecem suporte a conexões de clientes em locais não confiáveis):  

-   Ponto de sites da Web do Catálogo de Aplicativos  

-   Módulo de Política do Configuration Manager  

-   Ponto de distribuição (HTTPS é exigido pelos pontos de distribuição baseados em nuvem)  

-   Ponto proxy do registro  

-   Ponto de status de fallback  

-   Ponto de gerenciamento  

-   Ponto de atualização de software  

 **Sobre sistemas de site voltados para Internet:**   
Embora não haja nenhum requisito para haver uma relação de confiança entre a floresta de um cliente e a do servidor do sistema de sites, quando a floresta que contém um sistema de sites da Internet confia na floresta que contém as contas de usuário, essa configuração dá suporte a políticas baseadas no usuário para dispositivos na Internet ao habilitar a configuração do cliente **Habilitar solicitações da política de usuário de clientes da Internet** da **Política do Cliente**.  

 Por exemplo, as configurações seguintes ilustram quando o gerenciamento de cliente baseado na Internet oferece suporte a políticas de usuário para dispositivos na Internet:  

-   O ponto de gerenciamento baseado na Internet é na rede de perímetro onde um controlador de domínio somente leitura reside, para autenticar o usuário e um firewall intermediário permite pacotes do Active Directory.  

-   A conta do usuário está na Floresta A (a intranet) e o ponto de gerenciamento baseado na Internet está na Floresta B (a rede de perímetro). A floresta B confia na Floresta A e um firewall intermediário permite pacotes de autenticação.  

-   A conta de usuário e o ponto de gerenciamento baseados na Internet estão na Floresta A (intranet). O ponto de gerenciamento é publicado na Internet usando um servidor de proxy da web (como o Forefront Threat Management Gateway).  

> [!NOTE]  
>  Se a autenticação Kerberos falhar, a autenticação NTLM será tentada automaticamente.  

 Como mostra o exemplo anterior, você pode colocar os sistemas de áreas baseados na Internet na intranet quando são publicados na Internet por meio de um servidor proxy da Web, como o ISA Server e Forefront Threat Management Gateway. Esses sistemas de site podem ser configurados para conexão do cliente por meio da Internet apenas, ou conexões de clientes da Internet e intranet. Quando você usa um servidor proxy da Web, pode configurá-lo como uma ponte de protocolo SSL com SSL (mais seguro) ou túnel SSL:  

-   **Ponte SSL para SSL:**   
    A configuração recomendada ao usar servidores proxy da Web para o gerenciamento de clientes baseado na Internet é a ponte SSL para SSL, que usa a terminação SSL com autenticação. Computadores cliente devem ser autenticados usando a autenticação do computador e os clientes herdados de dispositivos móveis são autenticados usando a autenticação do usuário. Os dispositivos móveis registrados pelo Configuration Manager não dão suporte à ponte SSL.  

     O benefício da terminação de SSL no servidor proxy da Web é que os pacotes da Internet estão sujeitos a inspeção antes de serem encaminhados à rede interna. O servidor proxy da Web autentica a conexão do cliente, termina a conexão e depois abre uma nova conexão autenticada com os sistemas de área baseados na Internet. Quando os clientes do Configuration Manager usam um servidor Web proxy, a identidade do cliente (GUID do cliente) fica protegida na carga do pacote para que o ponto de gerenciamento não considere o servidor Web proxy como o cliente. Não há suporte para ponte no Configuration Manager com HTTP para HTTPS, ou de HTTPS para HTTP.  

-   **Túnel**:   
    Se o seu servidor Web proxy não conseguir dar suporte aos requisitos da ponte SSL ou se desejar configurar o suporte da Internet para dispositivos móveis registrados pelo Configuration Manager, também haverá suporte para o túnel SSL. É uma opção menos segura, pois os pacotes de SSL da Internet são encaminhados para os sistemas de site sem terminação SSL, para que não possam ser inspecionados quanto a conteúdo malicioso. Quando você usa o túnel SSL, não existem requisitos de certificado do servidor proxy da Web.  

##  <a name="a-namebkmkplanforinternetclientsa-planning-for-internet-based-clients"></a><a name="BKMK_PlanforInternetClients"></a> Planejando clientes baseados na Internet  
 Você deve decidir se os computadores cliente gerenciados pela Internet serão configurados para gerenciamento na intranet e na internet, ou somente por gerenciamento do cliente na Internet. Você só pode configurar a opção de gerenciamento de cliente durante a instalação de um computador cliente. Se você mudar de ideia mais tarde, deverá reinstalar o cliente.  

> [!NOTE]  
>  Se você configurar um ponto de gerenciamento habilitado para Internet, os clientes que se conectarem ao ponto de gerenciamento passarão a ser habilitados para Internet na próxima vez que atualizarem sua lista de pontos de gerenciamento disponíveis.  

> [!TIP]  
>  Não é necessário restringir a configuração do gerenciamento do cliente para a Internet apenas e você também pode usá-lo na intranet.  

 Clientes configurados para gerenciamento na Internet só se comunicam com outros sistemas de site configurados para conexões de clientes da Internet. Essa configuração seria adequada para computadores que você sabe que nunca se conectam à intranet da empresa, por exemplo, computadores de pontos de venda em locais remotos. Também pode ser apropriado quando você quer restringir a comunicação do cliente apenas ao HTTPS (por exemplo, para dar suporte a firewall e políticas restritas de segurança), e ao instalar sistemas de área baseados na Internet em uma rede de perímetro e você quer gerenciar esses servidores usando o cliente do Configuration Manager.  

 Para gerenciar clientes de grupo de trabalho na Internet, você deve instalá-los como somente Internet.  

> [!NOTE]  
>  Clientes de dispositivos móveis são automaticamente configurados como Internet somente quando são configurados para usar um ponto de gerenciamento baseado na Internet.  

 Outros computadores cliente podem ser configurados para o gerenciamento de cliente na Internet e intranet. Eles podem alternar automaticamente entre o gerenciamento de cliente baseado na Internet e gerenciamento de cliente baseado na intranet quando detectam uma alteração na rede. Se esses clientes puderem encontrar e se conectar a um ponto de gerenciamento configurado para conexões de clientes na intranet, eles serão gerenciados como clientes da intranet com funcionalidade de gerenciamento completo do Configuration Manager. Se os clientes não conseguirem encontrar ou se conectar a um ponto de gerenciamento configurado para conexões de clientes na intranet, tentarão se conectar a um ponto de gerenciamento baseado na Internet e, se tiverem sucesso, serão gerenciados pelos sistemas de área baseados na Internet em seu site atribuído.  

 O benefício da comutação automática entre gerenciamento de clientes baseado na Internet e o gerenciamento de clientes da intranet é que os computadores cliente podem usar automaticamente todos os recursos do Configuration Manager sempre que estiverem conectados à intranet e ainda serem gerenciados para as funções essenciais de gerenciamento quando estiverem na Internet. Além disso, um download que começou na Internet pode perfeitamente continuar na intranet e vice-versa.  

##  <a name="a-namebkmkprerequisitsforinternetclientmgmta-prerequisites-for-internet-based-client-management"></a><a name="BKMK_PrerequisitsForInternetClientMgmt"></a> Pré-requisitos para o gerenciamento de clientes baseado na Internet  
 O gerenciamento de clientes baseados na Internet no Configuration Manager tem as seguintes dependências externas:  

-   Clientes que serão gerenciados na Internet devem ter uma conexão com a Internet.  

     O Configuration Manager usa conexões ISP (Provedor de Serviços de Internet) existentes com a Internet, que podem ser conexões permanentes ou temporárias. Dispositivos móveis de clientes devem ter uma conexão direta com a Internet, mas os computadores cliente podem ter uma conexão direta com a internet ou conectar usando um servidor proxy da Web.  

-   Sistemas de site que oferecem suporte a gerenciamento de clientes baseado na Internet devem ter conectividade com a Internet e estar em um domínio Active Directory.  

     Sistemas de áreas baseados na Internet não requerem uma relação de confiança com a floresta do Active Directory do servidor do site. No entanto, quando o ponto de gerenciamento baseado na Internet pode autenticar o usuário usando a autenticação do Windows, há suporte para as políticas do usuário. Se a autenticação do Windows falhar, somente as políticas do computador terão suporte.  

    > [!NOTE]  
    >  Para oferecer suporte às políticas de usuário, você também deve definir como **Verdadeiro** as duas configurações de **Política do Cliente** :  
    >   
    >  -   **Habilitar sondagem de política de usuário nos clientes**  
    > -   **Ativar solicitações de política de usuário de clientes da Internet**  

     Um ponto de site da Web do catálogo de aplicativos também exige a autenticação do Windows para autenticar usuários quando seu computador está na Internet. Esse requisito é independente das políticas do usuário.  

-   Você deve ter uma PKI (Infraestrutura de Chave Pública ) que pode implantar e gerenciar os certificados que os clientes precisam e que sejam gerenciados na Internet e em servidores de sistema de áreas baseado na Internet.  

     Para obter mais informações sobre certificados PKI, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](/sccm/core/plan-design/network/pki-certificate-requirements).  

-   O FQDN (Nome de Domínio Totalmente Qualificado) dos sistemas de site que oferece suporte a gerenciamento de clientes baseado na Internet deve ser registrado como entradas de host em servidores DNS públicos.  

-   Os firewalls ou os servidores proxy intermediários devem permitir a comunicação do cliente associada a sistemas de sites baseados na Internet.  

     Requisitos de comunicação do cliente:  

    -   Oferecer suporte a HTTP 1.1  

    -   Permitir tipo de conteúdo HTTP de anexo MIME de várias partes (multiparte/misto e aplicativo/octet-stream)  

    -   Permitir os seguintes verbos para o ponto de gerenciamento baseado na Internet:  

        -   HEAD  

        -   CCM_POST  

        -   BITS_POST  

        -   GET  

        -   PROPFIND  

    -   Permitir os seguintes verbos para o ponto de distribuição baseado na Internet:  

        -   HEAD  

        -   GET  

        -   PROPFIND  

    -   Permitir os seguintes verbos para o ponto de status de fallback baseado na Internet:  

        -   POST  

    -   Permitir os seguintes verbos para o ponto de sites da Web do catálogo de aplicativos baseado na Internet:  

        -   POST  

        -   GET  

    -   Permitir os seguintes cabeçalhos HTTP para o ponto de gerenciamento baseado na Internet:  

        -   Intervalo:  

        -   CCMClientID:  

        -   CCMClientIDSignature:  

        -   CCMClientTimestamp:  

        -   CCMClientTimestampsSignature:  

    -   Permitir o seguinte cabeçalho HTTP para o ponto de distribuição baseado na Internet:  

        -   Intervalo:  

     Para obter informações de configuração de suporte para esses requisitos, consulte a documentação do servidor proxy ou firewall.  

     Para requisitos de comunicação semelhantes ao usar o ponto de atualização de software para conexões de clientes da Internet, consulte a documentação do WSUS (Windows Server Update Services). Por exemplo, para o WSUS no Windows Server 2003, veja [Apêndice D: Configurações de segurança](http://go.microsoft.com/fwlink/p/?LinkId=143368), o apêndice de implantação para configurações de segurança.



<!--HONumber=Dec16_HO3-->


