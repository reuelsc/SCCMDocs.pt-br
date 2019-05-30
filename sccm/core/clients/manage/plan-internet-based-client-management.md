---
title: Gerenciamento de clientes baseado na Internet
titleSuffix: Configuration Manager
description: Crie um plano para o gerenciamento de clientes baseado na Internet no System Center Configuration Manager.
ms.date: 05/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: afcc3c2d70e1f6d94e7239a0be78c00294108c76
ms.sourcegitcommit: 18ad7686d194d8cc9136a761b8153a1ead1cdc6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66176693"
---
# <a name="plan-for-internet-based-client-management-in-system-center-configuration-manager"></a>Planejar o gerenciamento de clientes baseado na Internet no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O gerenciamento de clientes baseado na Internet (às vezes chamado de IBCM) permite que você gerencie clientes do System Center Configuration Manager quando eles não estão conectados à rede da empresa, mas têm uma conexão padrão com a Internet. Este arranjo tem várias vantagens, que incluem os custos reduzidos de não ter de executar VPNs (Redes Virtuais Privadas) e ser capaz de implantar atualizações de software de uma maneira oportuna.  

 Devido aos mais altos requisitos de segurança do gerenciamento de computadores cliente em uma rede pública, o gerenciamento de clientes baseado na Internet exige que os clientes e os servidores do sistema de sites se conectem para usar certificados PKI. Isso garante que as conexões sejam autenticadas por uma autoridade independente, e que os dados de e para esses sistemas de site sejam criptografados usando protocolo SSL.  

 Use as seções a seguir para ajudá-lo a planejar o gerenciamento de clientes baseado na Internet.  

##  <a name="features-that-are-not-supported-on-the-internet"></a>Recursos não compatíveis na Internet  
 Nem todos os recursos do gerenciamento de clientes são adequados para a Internet; portanto, eles não são compatíveis quando os clientes são gerenciados na Internet. Os recursos não compatíveis para o gerenciamento na Internet normalmente dependem do Active Directory Domain Services ou não são apropriados para uma rede pública, como descoberta de rede e WOL (Wake On LAN).  

 Os seguintes recursos não são compatíveis quando os clientes são gerenciados na Internet:  

- Implantação de cliente na Internet, como a implantação de cliente baseada na atualização de software e de cliente por push. Em vez disso, use a instalação manual do cliente.  

- Atribuição automática de site.  

- Wake on LAN.  

- Implantação de sistema operacional. No entanto, você pode implantar sequências de tarefas que não implantam um sistema operacional, por exemplo, sequências de tarefas que executam scripts e tarefas de manutenção em clientes.  

- Controle remoto.  

- Implantação de software para usuários, a menos que o ponto de gerenciamento baseado na Internet possa autenticar o usuário no Active Directory Domain Services usando a autenticação do Windows (Kerberos ou NTLM). Isso é possível quando o ponto de gerenciamento baseado na Internet tem uma relação de confiança na floresta em que reside a conta do usuário.  

  Além disso, o gerenciamento de clientes baseado na Internet não dá suporte ao roaming. O roaming permite que os clientes sempre localizem os pontos de distribuição mais próximos para baixar conteúdo. Os clientes que são gerenciados na Internet se comunicam com os sistemas de sites por meio de seu site atribuído quando esses sistemas de sites são configurados para usar um FQDN da Internet e as funções do sistema de sites permitem conexões do cliente pela Internet. Os clientes selecionam de forma não determinística um dos sistemas de sites baseados na Internet, independentemente de largura de banda ou localização física.  

  Quando você tem um ponto de atualização de software configurado para aceitar conexões da Internet, os clientes baseados na Internet do Configuration Manager sempre são examinados em relação a esse ponto de atualização de software, para determinar quais atualizações de software são necessárias. No entanto, quando esses clientes estão na Internet, primeiro eles tentam baixar as atualizações de software do Microsoft Update, em vez de fazer isso de um ponto de distribuição baseado na Internet. Somente se isso falhar, eles tentarão baixar as atualizações de software necessárias de um ponto de distribuição baseado na Internet. Os clientes que não estão configurados para o gerenciamento de clientes baseado na Internet nunca tentam baixar as atualizações de software do Microsoft Update, mas sempre usam os pontos de distribuição do Configuration Manager.  
 
> [!Tip]  
> O cliente do Configuration Manager determina automaticamente se ele está na intranet ou na Internet. Se o cliente pode contatar um controlador de domínio ou um ponto de gerenciamento local, ele define seu tipo de conexão como Atualmente intranet. Caso contrário, ele alterna para Atualmente Internet, e o cliente usa os pontos de gerenciamento, os pontos de atualização de software e os pontos de distribuição atribuídos ao site para comunicação.

##  <a name="considerations-for-client-communications-from-the-internet-or-untrusted-forest"></a>Considerações sobre a comunicação do cliente da Internet ou de uma floresta não confiável  
 As seguintes funções do sistema de sites instaladas em sites primários dão suporte a conexões de clientes que estão em localizações não confiáveis, como a Internet ou uma floresta não confiável (os sites secundários não dão suporte a conexões de clientes em localizações não confiáveis):  

- Ponto de sites da Web do Catálogo de Aplicativos  

- Módulo de Política do Configuration Manager  

- Ponto de distribuição (HTTPS é exigido pelos pontos de distribuição baseados em nuvem)  

- Ponto proxy do registro  

- Ponto de status de fallback  

- Ponto de gerenciamento  

- Ponto de atualização de software  

  **Sobre sistemas de site voltados para Internet:**    
  Embora não haja nenhum requisito para haver uma relação de confiança entre a floresta de um cliente e a do servidor do sistema de sites, quando a floresta que contém um sistema de sites para a Internet confia na floresta que contém as contas de usuário, essa configuração é compatível com políticas baseadas no usuário para dispositivos na Internet ao habilitar a configuração do cliente **Habilitar solicitações da política de usuário de clientes da Internet** da **Política do Cliente**.  

  Por exemplo, as configurações seguintes ilustram quando o gerenciamento de cliente baseado na Internet dá suporte a políticas de usuário para dispositivos na Internet:  

- O ponto de gerenciamento baseado na Internet é na rede de perímetro em que um controlador de domínio somente leitura reside, para autenticar o usuário e um firewall intermediário permite pacotes do Active Directory.  

- A conta do usuário está na Floresta A (a intranet) e o ponto de gerenciamento baseado na Internet está na Floresta B (a rede de perímetro). A floresta B confia na Floresta A e um firewall intermediário permite pacotes de autenticação.  

- A conta de usuário e o ponto de gerenciamento baseados na Internet estão na Floresta A (intranet). O ponto de gerenciamento é publicado na Internet usando um servidor proxy da Web (como o Forefront Threat Management Gateway).  

> [!NOTE]  
>  Se a autenticação Kerberos falhar, a autenticação NTLM será tentada automaticamente.  

 Como mostra o exemplo anterior, você poderá colocar os sistemas de sites baseados na Internet na intranet quando eles forem publicados na Internet usando um servidor proxy Web, como o ISA Server e o Forefront Threat Management Gateway. Esses sistemas de sites podem ser configurados para a conexão do cliente somente na Internet ou para conexões de clientes na Internet e na intranet. Quando você usa um servidor proxy da Web, pode configurá-lo como uma ponte de protocolo SSL com SSL (mais seguro) ou túnel SSL:  

-   **Ponte SSL para SSL:**    
    A configuração recomendada ao usar servidores proxy da Web para o gerenciamento de clientes baseado na Internet é a ponte SSL para SSL, que usa a terminação SSL com autenticação. Computadores cliente devem ser autenticados usando a autenticação do computador e os clientes herdados de dispositivos móveis são autenticados usando a autenticação do usuário. Os dispositivos móveis registrados pelo Configuration Manager não dão suporte à ponte SSL.  

     O benefício da terminação SSL no servidor Web proxy é que os pacotes da Internet estão sujeitos à inspeção antes de serem encaminhados à rede interna. O servidor proxy Web autentica a conexão do cliente, termina a conexão e depois abre uma nova conexão autenticada com os sistemas de área baseados na Internet. Quando os clientes do Configuration Manager usam um servidor Web proxy, a identidade do cliente (GUID do cliente) fica protegida na carga do pacote para que o ponto de gerenciamento não considere o servidor Web proxy como o cliente. Não há suporte para ponte no Configuration Manager com HTTP para HTTPS, ou de HTTPS para HTTP.  
     
    > [!Note]  
    > O Configuration Manager não oferece suporte à definição de configurações de ponte SSL de terceiros. Por exemplo, Citrix Netscaler ou F5 BIG-IP. Trabalhe com seu fornecedor de dispositivos para configurá-los para uso com o Configuration Manager.  

-   **Túnel**:   
    Se o servidor Web proxy não puder dar suporte aos requisitos da ponte SSL ou se você desejar configurar o suporte da Internet para dispositivos móveis registrados pelo Configuration Manager, também haverá suporte para o túnel SSL. É uma opção menos segura, pois os pacotes SSL da Internet são encaminhados para os sistemas de sites sem terminação SSL, não podendo, portanto, ser inspecionados quanto a conteúdo malicioso. Quando você usa o túnel SSL, não existem requisitos de certificado do servidor proxy da Web.  

##  <a name="planning-for-internet-based-clients"></a>Como planejar clientes baseados na Internet  
 Você precisa decidir se os computadores cliente que serão gerenciados pela Internet serão configurados para o gerenciamento na intranet e na Internet ou para o gerenciamento de clientes somente na Internet. Você só pode configurar a opção de gerenciamento de cliente durante a instalação de um computador cliente. Se você mudar de ideia mais tarde, deverá reinstalar o cliente.  

> [!NOTE]  
>  Se você configurar um ponto de gerenciamento habilitado para Internet, os clientes que se conectarem ao ponto de gerenciamento passarão a ser habilitados para Internet na próxima vez que atualizarem sua lista de pontos de gerenciamento disponíveis.  

> [!TIP]  
>  Você não precisa restringir a configuração do gerenciamento de clientes somente na Internet à Internet e também pode usá-la na intranet.  

 Os clientes configurados para o gerenciamento de clientes somente na Internet só se comunicam com os sistemas de sites configurados para conexões de clientes na Internet. Essa configuração seria adequada para computadores que você sabe que nunca se conectam à intranet da empresa, por exemplo, computadores de pontos de venda em locais remotos. Também pode ser apropriado quando você deseja restringir a comunicação do cliente apenas ao HTTPS (por exemplo, para dar suporte a políticas de segurança restrita e firewall) e ao instalar sistemas de sites baseados na Internet em uma rede de perímetro e você deseja gerenciar esses servidores usando o cliente do Configuration Manager.  

 Quando desejar gerenciar clientes de grupo de trabalho na Internet, você precisará instalá-los como somente Internet.  

> [!NOTE]  
>  Os clientes de dispositivos móveis são automaticamente configurados como somente Internet quando são configurados para usar um ponto de gerenciamento baseado na Internet.  

 Outros computadores cliente podem ser configurados para o gerenciamento de clientes na Internet e na intranet. Eles poderão alternar automaticamente entre o gerenciamento de clientes baseado na Internet e o gerenciamento de clientes baseado na intranet quando detectarem uma alteração na rede. Se esses clientes puderem encontrar e se conectar a um ponto de gerenciamento configurado para conexões de clientes na intranet, eles serão gerenciados como clientes da intranet com funcionalidade de gerenciamento completo do Configuration Manager. Se os clientes não puderem encontrar um ponto de gerenciamento ou não puderem se conectar a um ponto de gerenciamento configurado para conexões de clientes na intranet, eles tentarão se conectar a um ponto de gerenciamento baseado na Internet e, se tiverem sucesso, serão gerenciados pelos sistemas de sites baseados na Internet em seu site atribuído.  

 O benefício da alternância automática entre o gerenciamento de clientes baseado na Internet e o gerenciamento de clientes da intranet é que os computadores cliente poderão usar automaticamente todos os recursos do Configuration Manager sempre que estiverem conectados à intranet e ainda poderão ser gerenciados para as funções essenciais de gerenciamento quando estiverem na Internet. Além disso, um download iniciado na Internet pode ser retomado sem interrupção na intranet e vice-versa.  

##  <a name="prerequisites-for-internet-based-client-management"></a>Pré-requisitos para o gerenciamento de clientes baseado na Internet  
 O gerenciamento de clientes baseados na Internet no Configuration Manager tem as seguintes dependências externas:  

- Os clientes que serão gerenciados na Internet precisam ter uma conexão com a Internet.  

   O Configuration Manager usa as conexões existentes de ISP (provedor de serviços de Internet) com a Internet, que podem ser conexões permanentes ou temporárias. Os dispositivos móveis de clientes precisam ter uma conexão direta com a Internet, mas os computadores cliente podem ter uma conexão direta com a Internet ou conectar-se usando um servidor Web proxy.  

- Os sistemas de sites que dão suporte ao gerenciamento de clientes baseado na Internet precisam ter conectividade com a Internet e estar em um domínio do Active Directory.  

   Os sistemas de sites baseados na Internet não exigem uma relação de confiança com a floresta do Active Directory do servidor do site. No entanto, quando o ponto de gerenciamento baseado na Internet pode autenticar o usuário usando a autenticação do Windows, há suporte para políticas de usuário. Se a autenticação do Windows falhar, somente as políticas do computador terão suporte.  

  > [!NOTE]
  >  Para oferecer suporte às políticas de usuário, você também deve definir como **Verdadeiro** as duas configurações de **Política do Cliente** :  
  > 
  > - **Habilitar sondagem de política de usuário nos clientes**  
  >   -   **Ativar solicitações de política de usuário de clientes da Internet**  

   Um ponto de sites da Web do Catálogo de Aplicativos baseado na Internet também exige a autenticação do Windows para autenticar usuários quando seu computador está na Internet. Esse requisito é independente das políticas do usuário.  

- É necessário ter uma PKI (infraestrutura de chave pública) de suporte que possa implantar e gerenciar os certificados exigidos pelos clientes e que sejam gerenciados na Internet e em servidores do sistema de sites baseado na Internet.  

   Para obter mais informações sobre certificados PKI, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](/sccm/core/plan-design/network/pki-certificate-requirements).  

- O FQDN (nome de domínio totalmente qualificado) da Internet dos sistemas de sites que dão suporte ao gerenciamento de clientes baseado na Internet precisa ser registrado como entradas de host em servidores DNS públicos.  

- Os firewalls ou os servidores proxy intermediários precisam permitir a comunicação do cliente associada aos sistemas de sites baseados na Internet.  

   Requisitos de comunicação do cliente:  

  - Oferecer suporte a HTTP 1.1  

  - Permitir tipo de conteúdo HTTP de anexo MIME de várias partes (multiparte/misto e aplicativo/octet-stream)  

  - Permitir os seguintes verbos para o ponto de gerenciamento baseado na Internet:  

    -   HEAD  

    -   CCM_POST  

    -   BITS_POST  

    -   GET  

    -   PROPFIND  

  - Permitir os seguintes verbos para o ponto de distribuição baseado na Internet:  

    -   HEAD  

    -   GET  

    -   PROPFIND  

  - Permitir os seguintes verbos para o ponto de status de fallback baseado na Internet:  

    -   POST  

  - Permitir os seguintes verbos para o ponto de sites da Web do Catálogo de Aplicativos baseado na Internet:  

    -   POST  

    -   GET  

  - Permitir os seguintes cabeçalhos HTTP para o ponto de gerenciamento baseado na Internet:  

    -   Intervalo:  

    -   CCMClientID:  

    -   CCMClientIDSignature:  

    -   CCMClientTimestamp:  

    -   CCMClientTimestampsSignature:  

  - Permitir o seguinte cabeçalho HTTP para o ponto de distribuição baseado na Internet:  

    -   Intervalo:  

    Para obter informações de configuração de suporte para esses requisitos, consulte a documentação do servidor proxy ou firewall.  

    Para obter os requisitos de comunicação semelhantes ao usar o ponto de atualização de software para conexões de clientes na Internet, confira a documentação do WSUS (Windows Server Update Services). Por exemplo, para o WSUS no Windows Server 2003, confira o [Apêndice D: Configurações de segurança](http://go.microsoft.com/fwlink/p/?LinkId=143368), o apêndice de implantação das configurações de segurança.
