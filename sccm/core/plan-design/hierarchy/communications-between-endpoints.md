---
title: "Comunicação entre pontos de extremidade"
titleSuffix: Configuration Manager
description: Saiba mais sobre como os componentes e sistemas de sites do System Center Configuration Manager se comunicam em uma rede.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 712274456f4a48032e2ff8c1b4fc8b4b072d4536
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="communications-between-endpoints-in-system-center-configuration-manager"></a>Comunicação entre pontos de extremidade no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


##  <a name="Planning_Intra-site_Com"></a> Comunicações entre os sistemas de sites em um site  
 Quando os sistemas de sites ou componentes do Configuration Manager se comunicam pela rede com outros sistemas de sites ou componentes do Configuration Manager no site, eles utilizam um dos seguintes protocolos, dependendo de como você configura o site:  

-   Protocolo SMB  

-   HTTP  

-   HTTPS  

Com exceção da comunicação entre o servidor do site e um ponto de distribuição, as comunicações de servidor para servidor em um site podem ocorrer a qualquer momento e não usar mecanismos para controlar a largura de banda da rede. Como não é possível controlar a comunicação entre os sistemas de sites, lembre-se de instalar servidores do sistema de sites em locais que têm redes rápidas e bem conectadas.  

Para ajudá-lo a gerenciar a transferência de conteúdo do servidor do site para os pontos de distribuição:  

-   Configurar o ponto de distribuição para agendamento e controle de largura de banda da rede. Esses controles lembram as configurações usadas por endereços entre sites e muitas vezes será possível usar essa configuração em vez de instalar outro site do Configuration Manager quando a transferência de conteúdo para locais remotos da rede for sua consideração principal sobre largura de banda.  

-   Você pode instalar um ponto de distribuição como um ponto de distribuição em pré-teste. Um ponto de distribuição em pré-teste permite que você use o conteúdo que é colocado manualmente no servidor de ponto de distribuição e remove a necessidade de transferir arquivos de conteúdo pela rede.  

Para obter mais informações, consulte [Manage network bandwidth for content management](manage-network-bandwidth.md) (Gerenciar largura de banda de rede para gerenciamento de conteúdo).


##  <a name="Planning_Client_to_Site_System"></a> Comunicações de clientes para serviços e sistemas de sites  
Os clientes iniciam a comunicação com as funções do sistema de sites, o Active Directory Domain Services e os serviços online. Para habilitar essas comunicações, os firewalls devem permitir o tráfego de rede entre clientes e o ponto de extremidade de suas comunicações. Os pontos de extremidade incluem:  

-   **Ponto de sites da Web do Catálogo de Aplicativos**: dá suporte à comunicação HTTP e HTTPS

-   **Recursos baseados em nuvem**: inclui o Microsoft Azure e o Microsoft Intune  

-   **Módulo de Política do Configuration Manager (NDES)**: dá suporte à comunicação HTTP e HTTPS

-   **Pontos de distribuição**: dão suporte à comunicação HTTP e HTTPS, e o HTTPS é necessário para os pontos de distribuição baseados em nuvem  

-   **Ponto de status de fallback**: dá suporte à comunicação HTTP  

-   **Ponto de gerenciamento**: dá suporte à comunicação HTTP e HTTPS  

-   **Microsoft Update**  

-   **Pontos de atualização de software**: dão suporte à comunicação HTTP e HTTPS  

-   **Ponto de Migração de Estado**: dá suporte à comunicação HTTP e HTTPS  

-   **Vários serviços de domínio**  

Antes que um cliente possa se comunicar com uma função do sistema de sites, o cliente usa o local do serviço para localizar uma função do sistema de sites que dá suporte ao protocolo do cliente (HTTP ou HTTPS). Por padrão, os clientes usam o método mais seguro disponível para eles:  

-   Para usar HTTPS, é necessário ter uma infraestrutura de chave pública (PKI) e instalar certificados PKI em clientes e servidores. Para obter informações sobre como usar certificados, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   Quando você implanta uma função de sistema de site que usa o Internet Information Services (IIS) oferece suporte à comunicação de clientes, você deve especificar se os clientes conectam ao sistema de site usando HTTP ou HTTPS. Se você usar HTTP, também deve considerar as opções de assinatura e criptografia. Para obter mais informações, consulte [Planejar a assinatura e criptografia](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) em [Planejar a segurança no System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

Para obter mais informações sobre a localização de serviço pelos clientes, consulte [Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

Para obter detalhes sobre as portas e os protocolos usados pelos clientes quando eles se comunicam com esses pontos de extremidade, consulte [Portas usadas no System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

###  <a name="BKMK_clientspan"></a> Considerações sobre a comunicação do cliente da Internet ou de uma floresta não confiável  
As funções do sistema de sites a seguir instaladas em sites primários dão suporte a conexões de clientes que estão em locais não confiáveis, como a Internet ou uma floresta não confiável. (Sites secundários não dão suporte a conexões de cliente de locais não confiáveis):  

-   Ponto de sites da Web do catálogo de aplicativos  

-   Módulo de Política do Configuration Manager  

-   Ponto de distribuição (HTTPS é exigido pelos pontos de distribuição baseados em nuvem)  

-   Ponto proxy do registro  

-   Ponto de status de fallback  

-   Ponto de gerenciamento  

-   Ponto de atualização de software  

**Sobre os sistemas de sites para a Internet:**   
Não há nenhum requisito para haver uma relação de confiança entre a floresta do cliente e a do servidor do sistema de sites. No entanto, quando a floresta que contém um sistema de sites para a Internet confia na floresta que contém as contas de usuário, essa configuração dá suporte a políticas baseadas no usuário para dispositivos na Internet ao habilitar a configuração do cliente **Habilitar solicitações da política de usuário de clientes da Internet** da **Política do Cliente**.  

Por exemplo, as configurações seguintes ilustram quando o gerenciamento de cliente baseado na Internet oferece suporte a políticas de usuário para dispositivos na Internet:  

-   O ponto de gerenciamento baseado na Internet é na rede de perímetro onde um controlador de domínio somente leitura reside, para autenticar o usuário e um firewall intermediário permite pacotes do Active Directory.  

-   A conta do usuário está na Floresta A (a intranet) e o ponto de gerenciamento baseado na Internet está na Floresta B (a rede de perímetro). A floresta B confia na Floresta A e um firewall intermediário permite pacotes de autenticação.  

-   A conta de usuário e o ponto de gerenciamento baseados na Internet estão na Floresta A (intranet). O ponto de gerenciamento é publicado na Internet usando um servidor de proxy da web (como o Forefront Threat Management Gateway).  

> [!NOTE]  
>  Se a autenticação Kerberos falhar, a autenticação NTLM será tentada automaticamente.  

Como mostra o exemplo anterior, você pode colocar os sistemas de áreas baseados na Internet na intranet quando são publicados na Internet por meio de um servidor proxy da Web, como o ISA Server e Forefront Threat Management Gateway. Esses sistemas de sites podem ser configurados apenas para conexão de cliente pela Internet ou para conexões de cliente pela Internet e intranet. Ao usar um servidor proxy da Web, é possível configurá-lo para uma ponte do protocolo SSL para SSL (mais seguro) ou túnel SSL da seguinte maneira:  

-   **Ponte SSL para SSL:**   
    A configuração recomendada ao usar servidores proxy da Web para o gerenciamento de clientes baseado na Internet é a ponte SSL para SSL, que usa a terminação SSL com autenticação. Computadores cliente devem ser autenticados usando a autenticação do computador e os clientes herdados de dispositivos móveis são autenticados usando a autenticação do usuário. Os dispositivos móveis registrados pelo Configuration Manager não dão suporte à ponte SSL.  

     O benefício da terminação de SSL no servidor proxy da Web é que os pacotes da Internet estão sujeitos a inspeção antes de serem encaminhados à rede interna. O servidor proxy da Web autentica a conexão do cliente, termina a conexão e depois abre uma nova conexão autenticada com os sistemas de área baseados na Internet. Quando os clientes do Configuration Manager usam um servidor Web proxy, a identidade do cliente (GUID do cliente) fica protegida na carga do pacote para que o ponto de gerenciamento não considere o servidor Web proxy como o cliente. Não há suporte para ponte no Configuration Manager com HTTP para HTTPS, ou de HTTPS para HTTP.  

-   **Túnel**:   
    Se o seu servidor Web proxy não conseguir dar suporte aos requisitos da ponte SSL ou se desejar configurar o suporte da Internet para dispositivos móveis registrados pelo Configuration Manager, também haverá suporte para o túnel SSL. É uma opção menos segura, pois os pacotes de SSL da Internet são encaminhados para os sistemas de site sem terminação SSL, para que não possam ser inspecionados quanto a conteúdo malicioso. Quando você usa o túnel SSL, não existem requisitos de certificado do servidor proxy da Web.  

##  <a name="Plan_Com_X-Forest"></a> Comunicações entre florestas do Active Directory  
O System Center Configuration Manager dá suporte a sites e hierarquias que abrangem florestas do Active Directory.  

O Configuration Manager também dá suporte a computadores de domínio que não estão na mesma floresta do Active Directory que o servidor do site e a computadores de grupos de trabalho:  

-   **Para dar suporte a computadores de domínio em uma floresta que não é confiável para a floresta do seu servidor do site**, é possível:  

    -   Instalar funções de sistema de sites nessa floresta não confiável, com a opção de publicar informações do site na floresta do Active Directory  

    -   Gerenciar esses computadores como se fossem computadores de grupo de trabalho.  

  Ao instalar servidores do sistema de sites em uma floresta não confiável do Active Directory, a comunicação de cliente para servidor dos clientes da floresta é mantida na floresta e o Configuration Manager pode autenticar o computador usando o Kerberos. Ao publicar informações do site na floresta do cliente, os clientes se beneficiam da recuperação das informações do site, como uma lista de pontos de gerenciamento disponíveis da floresta do Active Directory, em vez de baixar essas informações de seu ponto de gerenciamento atribuído.  

  > [!NOTE]  
  >  Para gerenciar dispositivos na Internet, você pode instalar funções do sistema de áreas baseado na Internet em sua rede de perímetro, quando os servidores do sistema de site estiverem em uma floresta do Active Directory. Esse cenário não exige uma relação de confiança bidirecional entre a rede de perímetro e a floresta do servidor do site.  

-   **Para dar suporte a computadores em um grupo de trabalho**, você deve:  

    -   Aprovar manualmente computadores do grupo de trabalho quando eles usarem conexões de cliente HTTP com funções de sistema de sites. Isso ocorre porque o Configuration Manager não pode autenticar esses computadores usando o Kerberos.  

    -   Configurar os clientes do grupo de trabalho para usar a Conta de Acesso à Rede para que esses computadores possam recuperar conteúdo de pontos de distribuição.  

    -   Fornecer um mecanismo alternativo para os clientes do grupo de trabalho localizarem pontos de gerenciamento. É possível usar a publicação DNS, o WINS ou atribuir diretamente um ponto de gerenciamento. Isso ocorre porque esses clientes não podem recuperar informações do site dos Serviços de Domínio do Active Directory.  

    Recursos relacionados na biblioteca de conteúdo:  

    -   [Gerenciar registros conflitantes de clientes do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

    -   [Conta de acesso de rede](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

    -   [Como instalar clientes do Configuration Manager em computadores do grupo de trabalho](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

###  <a name="bkmk_span"></a> Cenários compatíveis com um site ou hierarquia que abrange vários domínios e florestas  

#### <a name="communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Comunicação entre sites em uma hierarquia que abrange florestas  
Esse cenário exige uma relação de confiança de floresta bidirecional que dá suporte à autenticação Kerberos.  Se você não tiver uma relação de confiança de floresta bidirecional que dá suporte à autenticação Kerberos, o Configuration Manager não dará suporte a um site filho na floresta remota.  

 **O Configuration Manager dá suporte à instalação de um site filho em uma floresta remota que tem a relação de confiança bidirecional necessária com a floresta do site pai**  

-   Por exemplo, é possível colocar um site secundário em uma floresta diferente de seu site pai primário, contanto que a relação de confiança necessária exista.  

> [!NOTE]  
>  Um site filho pode ser um site primário (em que o site de administração central é o site pai) ou um site secundário.  

A comunicação entre sites no Configuration Manager usa replicação de banco de dados e transferências baseadas em arquivo. Ao instalar um site, é necessário especificar uma conta com a qual o site será instalado no servidor designado. Essa conta também estabelece e mantém a comunicação entre os sites.  

Depois que o site é instalado com êxito e inicia transferências baseadas em arquivos e replicação de banco de dados, não é necessário configurar mais nada para a comunicação com o site.  

**Quando existe uma relação de confiança bidirecional na floresta, o Configuration Manager não necessita de nenhuma medida adicional de configuração.**  

Por padrão, quando você instala um novo site como filho de outro site, o Configuration Manager configura o seguinte:  

-   Uma rota de replicação baseada em arquivo entre sites em cada site que usa a conta de computador do servidor do site. O Configuration Manager adiciona a conta de computador de cada computador ao grupo **SMS_SiteToSiteConnection_&lt;sitecode\>** no computador de destino.  

-   Replicação de banco de dados entre o SQL Server em cada site.  

Também devem ser definidas as seguintes configurações:  

-   Firewalls e dispositivos de rede intermediários devem permitir os pacotes de rede de que o Configuration Manager necessita.  

-   A resolução de nomes deve funcionar entre as florestas.  

-   Para instalar um site ou de função do sistema do site, você deve especificar uma conta que tenha permissões de administrador local no computador especificado.  

#### <a name="communication-in-a-site-that-spans-forests"></a>Comunicação em um site que abrange florestas  
Esse cenário não requer uma relação de confiança de floresta bidirecional.  

**Sites primários oferecem suporte à instalação de funções do sistema de site em computadores em florestas remotas**.  

-   O Ponto de Serviços Web do Catálogo de Aplicativos é a única exceção.  Ele só tem suporte na mesma floresta que o servidor do site.  

-   Quando a função do sistema de site aceita conexões da Internet, como uma prática recomendada de segurança, instale as funções do sistema de site em um local onde o limite da floresta forneça proteção para o servidor de site (por exemplo, em uma rede de perímetro).  

**Para instalar uma função do sistema de site em um computador em uma floresta não confiável:**  

-   É necessário especificar uma **Conta de Instalação do Sistema de Site**, que é usada para instalar a função do sistema de sites. (Essa conta deve ter credenciais administrativas locais à qual se conectar.) Em seguida, instale as funções do sistema de sites no computador especificado.  

-   Você deve selecionar a opção do sistema de site **Exigir que o servidor do site inicie conexões com este sistema de site**. Isso exige que o servidor do site estabeleça conexões com o servidor do sistema de site para transferir dados. Isso impede que o computador no local não confiável inicie contato com o servidor do site que está na rede confiável. Essas conexões usam a **Conta de Instalação do Sistema de Site**.  

**Para usar uma função de sistema de sites que foi instalada em uma floresta não confiável,** os firewalls devem permitir o tráfego de rede, mesmo quando o servidor do site iniciar a transferência de dados.  

Além disso, as seguintes funções de sistema de site exigem acesso direto ao banco de dados do site. Portanto, os firewalls devem permitir o tráfego aplicável da floresta não confiável para o SQL Server do site:  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto do Endpoint Protection  

-   Ponto de registro  

-   Ponto de gerenciamento  

-   Ponto de serviço de relatório  

-   Ponto de migração de estado  

Para obter mais informações, consulte [Portas usadas no System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

**Talvez seja necessário configurar o acesso à função do sistema de sites para o banco de dados do site:**  

O ponto de gerenciamento e as funções de sistema do ponto de registro se conectam ao banco de dados do site.  

-   Por padrão, quando essas funções do sistema de sites são instaladas, o Configuration Manager configura a conta de computador do novo servidor do sistema de sites como a conta de conexão para a função do sistema de sites e, em seguida, a adiciona à função apropriada de banco de dados do SQL Server.  

-   Quando você instala essas funções do sistema de site em um domínio não confiável, deve configurar a conta de conexão da função do sistema de site para habilitá-la a obter informações do banco de dados.  

Se você configurar uma conta de usuário de domínio como uma conta de conexão para essas funções do sistema, verifique se a conta de usuário do domínio tem acesso adequado ao banco de dados do SQL Server naquele site:  

-   Ponto de gerenciamento: **Conta de Conexão do Banco de Dados do Ponto de Gerenciamento**  

-   Ponto de registro: **Conta de Conexão do Ponto de Registro**  

Ao planejar funções do sistema de site em outras florestas, considere as seguintes informações adicionais:  

-   Se você executar o Firewall do Windows, configure os perfis de firewall aplicáveis ​​para passar a comunicação entre o servidor de banco de dados do site e os computadores instalados com as funções do sistema de sites remoto. Para obter informações sobre perfis de firewall, consulte [Noções básicas dos perfis de firewall](http://go.microsoft.com/fwlink/p/?LinkId=233629).  

-   Quando o ponto de gerenciamento com base em Internet tem uma relação de confiança com a floresta que contém as contas do usuário, as políticas do usuário têm suporte. Quando não existe uma relação de confiança, somente as políticas do computador têm suporte.  

#### <a name="communication-between-clients-and-site-system-roles-when-the-clients-are-not-in-the-same-active-directory-forest-as-their-site-server"></a>Comunicação entre clientes e funções do sistema de site quando os clientes não estão na mesma floresta do Active Directory que o servidor do site.  
O Configuration Manager dá suporte aos seguintes cenários para os clientes que não estão na mesma floresta que o servidor do site:  

-   Há uma relação de confiança de floresta bidirecional entre a floresta do cliente e a floresta do servidor do site.  

-   O servidor da função do sistema de sites está localizado na mesma floresta que o cliente.  

-   O cliente está em um computador de domínio que não tem uma relação de confiança de floresta bidirecional com o servidor do site e as funções do sistema de sites não estão instaladas na floresta do cliente.  

-   O cliente está em um computador de grupo de trabalho.  

Os clientes em um computador ingressado em domínio podem usar o Active Directory Domain Services como o local do serviço quando seu site é publicado na floresta do Active Directory.  

Para publicar informações do site em outra floresta do Active Directory, você deve:  

-   Especificar a floresta e, em seguida, habilitar a publicação nessa floresta no nó **Florestas do Active Directory** do espaço de trabalho **Administração** .  

-   Configurar cada site para publicar seus dados nos Serviços de Domínio Active Directory. Essa configuração permite que os clientes nessa floresta recuperem informações do site e localizem pontos de gerenciamento. Para clientes que não podem usar o Active Directory Domain Services no local de serviço, é possível usar DNS, WINS ou o ponto de gerenciamento atribuído do cliente.  

###  <a name="bkmk_xchange"></a> Colocar o conector do Exchange Server em uma floresta remota  
Para compatibilidade com esse cenário, verifique se a resolução de nomes funciona entre as florestas (por exemplo, configure encaminhamentos de DNS) e, quando configurar o conector do Exchange Server, especifique o FQDN da intranet do Exchange Server. Para obter mais informações, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  
