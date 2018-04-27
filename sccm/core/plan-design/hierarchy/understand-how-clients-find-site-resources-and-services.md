---
title: Localizar recursos de site
titleSuffix: Configuration Manager
description: Saiba como e quando os clientes do System Center Configuration Manager usam o local do serviço para encontrar recursos do site.
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
caps.latest.revision: 10
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 76d9d486bf0c07da3d81596b1b065fe6532b29fe
ms.sourcegitcommit: e4ca9fb1fad2caaf61bb46e0a12f4d6b96f15513
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="learn-how-clients-find-site-resources-and-services-for-system-center-configuration-manager"></a>Saiba como os clientes encontram serviços e recursos do site para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os clientes do System Center Configuration Manager usam um processo chamado *local do serviço* para localizar servidores de sistema de sites com os quais eles podem se comunicar e que fornecem serviços que os clientes são direcionados a usar. Noções básicas sobre como e quando os clientes usam local do serviço para localizar recursos de site podem ajudá-lo a configurar seus sites para dar suporte a tarefas do cliente com sucesso. Essas configurações podem exigir que o site interaja com configurações de rede e de domínio, como o AD DS (Active Directory Domain Services) e o DNS. Ou podem exigir que você configure alternativas mais complexas.  

 Entre os exemplos de funções do sistema de site que fornecem serviços estão:

 - O servidor do sistema de site principal para clientes.
 - O ponto de gerenciamento.
 - Outros servidores do sistema de site com os quais o cliente pode se comunicar, como pontos de atualização de software e pontos de distribuição.  



##  <a name="bkmk_fund"></a> Fundamentals of service location  
 Um cliente avalia seu local de rede atual, a preferência de protocolo de comunicação e o site atribuído ao usar o local do serviço para localizar um ponto de gerenciamento com o qual ela possa se comunicar.  

 **Um cliente se comunica com um ponto de gerenciamento para:**  
-   Baixar informações sobre outros pontos de gerenciamento para o site, para que possa criar uma lista de pontos de gerenciamento conhecidos (conhecida como *lista MP*) para ciclos de local de serviço futuros.  
-   Carregar os detalhes de configuração, como inventário e status.  
-   Baixar uma política que define as configurações no cliente e poder informar ao cliente de software que ele pode ou deve instalar e outras tarefas relacionadas.  
-   Solicitar informações sobre outras funções do sistema de site que fornecem serviços para os quais o cliente foi configurado para usar. Os exemplos incluem pontos de distribuição para software os quais o cliente pode instalar, ou um ponto de atualização de software para obtenção de atualizações.  

**Um cliente do Configuration Manager faz uma solicitação de local do serviço:**  
-   A cada 25 horas de operação contínua.  
-   Quando o cliente detecta uma mudança de sua configuração de rede ou local.  
-   Quando o serviço **ccmexec.exe** é iniciado no computador (o serviço de cliente de núcleo).  
-   Quando o cliente deve localizar uma função de sistema de sites que fornece um serviço necessário.  

**Quando um cliente tenta encontrar servidores que hospedam as funções do sistema de sites**, ele usa o local do serviço para localizar uma função do sistema de sites que dá suporte ao protocolo do cliente (HTTP ou HTTPS). Por padrão, os clientes usam o método mais seguro disponível para eles. Considere o seguinte:  

-   Para usar HTTPS, é necessário ter uma infraestrutura de chave pública (PKI) e instalar certificados PKI em clientes e servidores. Para obter informações sobre como usar certificados, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   Quando você implanta uma função de sistema de site que usa o Internet Information Services (IIS) oferece suporte à comunicação de clientes, você deve especificar se os clientes conectam ao sistema de site usando HTTP ou HTTPS. Se você usar HTTP, também deve considerar as opções de assinatura e criptografia. Para saber mais, consulte [Planejar assinatura e criptografia](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) em [Planejar a segurança no System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="BKMK_Plan_Service_Location"></a> Local do serviço e como os clientes determinam seu ponto de gerenciamento atribuído  
Quando um cliente é atribuído inicialmente a um site primário, ele seleciona um ponto de gerenciamento padrão para o site. Sites primários dão suporte a vários pontos de gerenciamento, e cada cliente independente identifica um ponto de gerenciamento como seu ponto de gerenciamento padrão. Esse ponto de gerenciamento padrão então se torna o ponto de gerenciamento atribuído desse cliente. (Você também pode usar comandos de instalação do cliente para definir o ponto de gerenciamento atribuído para um cliente no momento da instalação).  

Um cliente seleciona um ponto de gerenciamento para se comunicarem com base no local de rede atual e nas configurações de grupo de limite. Embora tenha um ponto de gerenciamento atribuído, esse não pode ser o ponto de gerenciamento que o cliente usa.  

   > [!NOTE]  
   >  Um cliente sempre usa o ponto de gerenciamento atribuído para mensagens de registro e determinadas mensagens de política, mesmo quando outras comunicações são enviadas para um proxy ou um ponto de gerenciamento local.

Você pode usar pontos de gerenciamento preferenciais. Os pontos de gerenciamento preferenciais são pontos de gerenciamento do site atribuído de um cliente associados a um grupo de limites que o cliente usa para encontrar servidores do sistema de sites. A associação do ponto de gerenciamento preferencial a um grupo de limites, como o servidor do sistema de sites, é semelhante ao modo como os pontos de distribuição ou pontos de migração de estado são associados a um grupo de limites. Se você habilitar pontos de gerenciamento preferenciais para a hierarquia, quando um cliente usar um ponto de gerenciamento do seu site atribuído, ele tentará usar um ponto de gerenciamento preferencial antes de usar outros pontos de gerenciamento de seu site atribuído.  

Você também pode usar as informações no blog [afinidade do ponto de gerenciamento](http://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx) no TechNet.com para configurar a afinidade do ponto de gerenciamento. A afinidade do ponto de gerenciamento substitui o comportamento padrão para pontos de gerenciamento atribuídos e permite que o cliente use um ou mais pontos de gerenciamento específicos.  

Cada vez que um cliente precisa fazer contato com um ponto de gerenciamento, ele verifica uma lista de MP, armazenada localmente no WMI (Windows Management Instrumentation). O cliente cria uma lista de MP inicial durante a instalação. Em seguida, o cliente atualiza periodicamente a lista com detalhes sobre cada ponto de gerenciamento na hierarquia.  

Quando o cliente não consegue localizar um ponto de gerenciamento válido na sua lista de MP, ele pesquisa as seguintes origens de local de serviço, em ordem, até encontrar um ponto de gerenciamento que pode ser usado:  

1.  Ponto de gerenciamento  
2.  AD DS  
3.  DNS  
4.  WINS  

Depois que um cliente localiza e entra em contato com um ponto de gerenciamento com êxito, ele baixa a lista atual de pontos de gerenciamento que estão disponíveis na hierarquia e atualiza a lista de MP local. Isso se aplica igualmente a clientes que estão associados ao domínio e os que não estão.  

Por exemplo, quando um cliente do Configuration Manager na Internet se conecta a um ponto de gerenciamento baseado na Internet, o ponto de gerenciamento envia para esse cliente uma lista de pontos de gerenciamento disponíveis baseados na Internet no site. Da mesma forma, os clientes que ingressaram no domínio ou em grupos de trabalho também recebem a lista de pontos de gerenciamento que eles podem usar.  

Um cliente que não está configurado para a Internet não recebe pontos de gerenciamento voltados apenas para a Internet. Clientes de grupo de trabalho configurados para a Internet comunicam-se apenas com pontos de gerenciamento voltados para a Internet.  

##  <a name="BKMK_MPList"></a> A lista de MP  
A lista de MP é a origem preferencial para o local de origem do serviço para um cliente, pois é uma lista priorizada de pontos de gerenciamento que o cliente já identificou. Essa lista é classificada por cada cliente com base em seu local de rede no momento em que o cliente atualizou a lista, armazenando-a localmente no cliente no WMI.  

### <a name="building-the-initial-mp-list"></a>Criar a lista de MP inicial  
Durante a instalação do cliente, as regras a seguir são usadas para criar os a lista MP inicial do cliente:  

-   A lista inicial inclui pontos de gerenciamento especificados durante a instalação do cliente (quando você usa o **SMSMP**= ou a opção **/MP**).  
-   O cliente consulta o AD DS em busca de pontos de gerenciamento publicados. Para ser identificado no AD DS, o ponto de gerenciamento deve ser proveniente do site atribuído do cliente e deve ser da mesma versão do produto do cliente.  
-   Se nenhum ponto de gerenciamento foi especificado durante a instalação do cliente e o esquema do Active Directory não foi estendido, o cliente verifica DNS e WINS em busca de pontos de gerenciamento publicados.  
-   Quando o cliente cria a lista inicial, talvez as informações sobre alguns pontos de gerenciamento na hierarquia não sejam conhecidas.  

### <a name="organizing-the-mp-list"></a>Organização da lista de MP  
Os clientes organizam sua lista de pontos de gerenciamento usando as seguintes classificações:  

-   **Proxy**: um ponto de gerenciamento em um site secundário.  
-   **Local**: qualquer ponto de gerenciamento associado ao local de rede atual do cliente conforme definido pelos limites do site. Observe as seguintes informações sobre limites:
    -   Quando um cliente pertence a mais de um grupo de limites, a lista de pontos de gerenciamento local é determinada pela união de todos os limites que incluem o local de rede atual do cliente.  
    -   Normalmente, os pontos de gerenciamento locais são um subconjunto de pontos de gerenciamento atribuído, a menos que o cliente esteja em um local de rede associado a outro site com os pontos de manutenção de seus grupos de limites.   


-   **Atribuído**: qualquer ponto de gerenciamento que é um sistema de sites para o site atribuído do cliente.  

Você pode usar pontos de gerenciamento preferenciais. Os pontos de gerenciamento em um site que não estão associados a um grupo de limites ou que não estão em um grupo de limites associado ao local de rede atual de um cliente não são considerados preferenciais. Eles serão usados quando o cliente não conseguir identificar um ponto de gerenciamento preferencial disponível.  

### <a name="selecting-a-management-point-to-use"></a>Selecionando um ponto de gerenciamento para usar  
Para comunicações típicas, um cliente tenta usar um ponto de gerenciamento por meio das classificações na seguinte ordem, com base no local de rede do cliente:  

1.  Proxy  
2.  Local  
3.  Atribuído  

No entanto, o cliente sempre usa o ponto de gerenciamento atribuído para mensagens de registro e determinadas mensagens de política, mesmo quando outras comunicações são enviadas para um proxy ou um ponto de gerenciamento local.  

Dentro de cada classificação (proxy, local ou atribuído), o cliente tenta usar um ponto de gerenciamento com base nas preferências, na seguinte ordem:  

1.  Compatível com HTTPS em uma floresta confiável ou local (quando o cliente está configurado para comunicação HTTPS)  
2.  Compatível com HTTPS fora de uma floresta confiável ou local (quando o cliente está configurado para comunicação HTTPS)  
3.  Compatível com HTTP em uma floresta confiável ou local  
4.  Compatível com HTTP não em uma floresta confiável ou local  

Do conjunto de pontos de gerenciamento classificadas pelas preferências, o cliente tenta usar o primeiro ponto de gerenciamento na lista. Essa lista classificada de pontos de gerenciamento é aleatória e não pode ser ordenada. A ordem da lista pode mudar cada vez que o cliente atualizar sua lista de MP.  

Quando um cliente não consegue estabelecer contato com o primeiro ponto de gerenciamento, ele tenta cada ponto de gerenciamento sucessivo em sua lista. Ele tenta cada ponto de gerenciamento preferencial na classificação antes de tentar os pontos de gerenciamento não preferenciais. Se um cliente não puder se comunicar com êxito com nenhum ponto de gerenciamento na classificação, ele tentará contatar um ponto de gerenciamento preferido da próxima classificação, e assim por diante, até o cliente encontrar um ponto de gerenciamento para usar.  

Depois de estabelecer comunicação com um ponto de gerenciamento, um cliente continuam a usar o mesmo ponto de gerenciamento até:  

-   25 horas decorridas.  
-   O cliente não ser capaz de se comunicar com o ponto de gerenciamento por cinco tentativas durante um período de 10 minutos.

Depois, o cliente seleciona aleatoriamente um novo ponto de gerenciamento para usar.  

##  <a name="bkmk_ad"></a> Active Directory  
Clientes que ingressaram no domínio podem usar o AD DS para o local do serviço. Isso requer que sites [publiquem dados para o Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

Um cliente poderá usar AD DS para o local do serviço quando todas as condições a seguir forem verdadeiras:  

-   O [esquema do Active Directory foi estendido](https://technet.microsoft.com/library/mt345589.aspx) ou foi estendido para o System Center 2012 Configuration Manager.  
-   A floresta do [Active Directory é configurada para publicação](http://technet.microsoft.com/library/hh696542.aspx)e os sites do Configuration Manager estão configurados para publicação.  
-   O computador cliente for um membro de um domínio do Active Directory e puder acessar um servidor de catálogo global.  

Se um cliente não conseguir localizar um ponto de gerenciamento para usar para a localização do serviço do AD DS, ele tentará usar DNS.  

##  <a name="bkmk_dns"></a> DNS  
Clientes na intranet podem usar o DNS para o local do serviço. Isso exige que pelo menos um site em uma hierarquia publique informações sobre pontos de gerenciamento no DNS.  

Considere usar o DNS para o local do serviço quando qualquer uma das seguintes condições forem verdadeiras:
-   O esquema do AD DS não foi estendido para dar suporte ao Configuration Manager.
-   Os clientes da intranet estiverem localizados em uma floresta que não esteja habilitada para publicar no Configuration Manager.  
-   Você possui clientes em computadores do grupo de trabalho, os quais não estão configurados para gerenciamento de cliente somente pela Internet. (Um cliente de grupo de trabalho configurado para a Internet somente se comunicará com pontos de gerenciamento da Internet e não usará o DNS para o local do serviço).  
-   Você pode [configurar clientes para localizar pontos de gerenciamento do DNS](http://technet.microsoft.com/library/gg682055).  

Quando um site publica registros de localização de serviço para pontos de gerenciamento no DNS:  

-   A publicação é aplicável somente a pontos de gerenciamento que aceitam conexões de clientes da intranet.  
-   A publicação adiciona um registro de recurso de local de serviço (SRV RR) na zona DNS do computador do ponto de gerenciamento. Deve haver uma entrada correspondente do host no DNS para o computador.  

Por padrão, clientes ingressados no domínio pesquisam DNS em busca de registros de ponto de gerenciamento do domínio local do cliente. Você pode configurar uma propriedade de cliente que especifica um sufixo de domínio para um domínio que tem informações de ponto de gerenciamento publicadas no DNS.  

Para obter mais informações sobre como configurar a propriedade de sufixo DNS do cliente, consulte [Como configurar computadores cliente para localizar pontos de gerenciamento usando a publicação do DNS no System Center Configuration Manager](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Se um cliente não conseguir localizar um ponto de gerenciamento para usar para localização de serviço do DNS, ele tentará usar WINS.  

### <a name="publish-management-points-to-dns"></a>Publicar pontos de gerenciamento no DNS  
Para publicar pontos de gerenciamento no DNS, as seguintes condições devem ser verdadeiras:  

-   Seus servidores DNS suportarem registros de recursos de localização de serviço, usando no mínimo uma versão 8.1.2 do BIND.  
-   Os FQDNs da intranet especificados para os pontos de gerenciamento no Configuration Manager tiverem entradas de host (por exemplo, registros A) no DNS.  

> [!IMPORTANT]  
>  A publicação de DNS do Configuration Manager não dão suporte a um namespace não contíguo. Se você tiver um namespace separado, você poderá publicar manualmente pontos de gerenciamento no DNS ou usar um dos outros métodos de localização de serviço documentados nesta seção.  

**Quando os seus servidores DNS dão suporte a atualizações automáticas**, é possível configurar o Configuration Manager para publicar automaticamente pontos de gerenciamento na intranet no DNS ou é possível publicar manualmente esses registros no DNS. Quando pontos de gerenciamento são publicados no DNS, seus números de portas e FQDNs da intranet são publicados no registro de localização de serviço (SRV). Você pode configurar a publicação de DNS em um site nos sites de propriedades do componente do ponto de gerenciamento. Para obter mais informações, consulte [Site components for System Center Configuration Manager (Componentes do site para o System Center Configuration Manager)](../../../core/servers/deploy/configure/site-components.md).  

**Quando a zona DNS for definida como "Somente seguro" para atualizações dinâmicas**, somente o primeiro ponto de gerenciamento para publicação no DNS pode fazer isso com êxito com as permissões padrão.

Se apenas um ponto de gerenciamento puder publicar e alterar com êxito seu registro DNS, e o servidor desse ponto de gerenciamento estiver íntegro, os clientes poderão obter a lista completa de MP desse ponto de gerenciamento e, em seguida, localizar o ponto de gerenciamento preferencial.


**Quando seus servidores DNS não suportarem atualizações automáticas, mas suportarem registros de localização de serviços**, você poderá publicar manualmente pontos de gerenciamento no DNS. Para fazer isso, é necessário especificar manualmente o registro de recurso de localização de serviço (SRV RR) no DNS.  

O Configuration Manager dá suporte à RFC 2782 para registros de local do serviço. Esses registros têm o seguinte formato:   *_Service._Proto.Name TTL Class SRV Priority Weight Port Target*  

Para publicar um ponto de gerenciamento no Configuration Manager, especifique os seguintes valores:  

-   **_Service**: insira **_mssms_mp**_&lt;sitecode\>, em que &lt;sitecode\> é o código do site do ponto de gerenciamento.  
-   **._Proto**: especifique **._tcp**.  
-   **.Name**: insira o sufixo DNS do ponto de gerenciamento, por exemplo **contoso.com**.  
-   **TTL**: insira **14400**, que é de quatro horas.  
-   **Classe**: especifique **IN** (em conformidade com a RFC 1035).  
-   **Prioridade**: o Configuration Manager não usa esse campo.
-   **Peso**: o Configuration Manager não usa esse campo.  
-   **Porta**: insira o número da porta que o ponto de gerenciamento usa, por exemplo **80** para HTTP e **443** para HTTPS.  

    > [!NOTE]  
    >  A porta do registro SRV deve corresponder à porta de comunicação usada pelo ponto de gerenciamento. Por padrão, ela é **80** para comunicação HTTP e **443** para comunicação HTTPS.  

-   **Destino**: insira o FQDN da intranet especificado para o sistema de site que é configurado com a função do site do ponto de gerenciamento.  

Se você estiver usando o DNS do Windows Server, você poderá usar o procedimento a seguir para inserir esse registro DNS nos pontos de gerenciamento da intranet. Se você estiver usando uma implementação diferente para DNS, use as informações desta seção sobre os valores dos campos e consulte a documentação de DNS para adaptar esse procedimento.  

##### <a name="to-configure-automatic-publishing"></a>Para configurar a publicação automática:  

1.  No console do Configuration Manager, expanda **Administração** > **Configuração de Site** > **Sites**.  

2.  Selecione seu site e escolha **Configurar Componentes do Site**.  

3.  Escolha **Ponto de Gerenciamento**.  

4.  Selecione os pontos de gerenciamento que você deseja publicar. (Esta seleção se aplica à publicação no AD DS e DNS).  

5.  Marque a caixa para publicar no DNS. Esta caixa:  

    -   Permite que você selecione quais pontos de gerenciamento publicar no DNS.  

    -   Não configura a publicação para o AD DS.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Para publicar manualmente os pontos de gerenciamento no DNS do Windows Server  

1.  No console do Configuration Manager, especifique os FQDNs dos sistemas de site da intranet.  

2.  No console de gerenciamento do DNS, selecione a zona DNS para o computador do ponto de gerenciamento.  

3.  Verifique se há um registro de host (A ou AAAA) para o FQDN do sistema de site da intranet. Se esse registro não existir, crie-o.  

4.  Usando a opção **Outros Novos Registros**, escolha **Local do Serviço (SRV)** na caixa de diálogo **Tipo de Registro de Recurso**, escolha **Criar Registro**, digite as seguintes informações e escolha **Concluído**:  

    -   **Domínio**: se necessário, digite o sufixo DNS do ponto de gerenciamento, por exemplo **contoso.com**.  
    -   **Service**: digite **_mssms_mp**_&lt;sitecode\>, em que &lt;sitecode\> é o código do site do ponto de gerenciamento.  
    -   **Protocolo**: tipo **_tcp**.  
    -   **Prioridade**: o Configuration Manager não usa esse campo.  
    -   **Peso**: o Configuration Manager não usa esse campo.  
    -   **Porta**: insira o número da porta que o ponto de gerenciamento usa, por exemplo **80** para HTTP e **443** para HTTPS.  

        > [!NOTE]  
        >  A porta do registro SRV deve corresponder à porta de comunicação usada pelo ponto de gerenciamento. Por padrão, ela é **80** para comunicação HTTP e **443** para comunicação HTTPS.  

    -   **Host que oferece esse serviço**: insira o FQDN da intranet especificado para o sistema de site que é configurado com a função do site do ponto de gerenciamento.  

Repita essas etapas para cada ponto de gerenciamento da intranet que você desejar publicar no DNS.  

##  <a name="bkmk_wins"></a> WINS  
Quando outros mecanismos de localização de serviço falharem, os clientes poderão encontrar um ponto de gerenciamento inicial verificando o WINS.  

Por padrão, um site primário publica para o WINS, o primeiro ponto de gerenciamento no site que está configurado para HTTP e o primeiro ponto de gerenciamento configurado para HTTPS.  

Se você não quiser que os clientes encontrem um ponto de gerenciamento HTTP em WINS, configure-os com a propriedade CCMSetup.exe Client.msi **SMSDIRECTORYLOOKUP=NOWINS**.  
