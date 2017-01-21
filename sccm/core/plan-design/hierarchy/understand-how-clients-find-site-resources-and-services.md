---
title: Encontre recursos de site | Microsoft Docs
description: "Entenda como e quando os clientes do System Center Configuration Manager usam o local do serviço para encontrar recursos do site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: b006896091901fab7b141f99f4c95eb22ea61b82


---
# <a name="understand-how-clients-find-site-resources-and-services-for-system-center-configuration-manager"></a>Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os clientes do System Center Configuration Manager usam um processo chamado **local do serviço** para localizar servidores de sistema de sites com os quais eles podem se comunicar e que fornecem serviços que os clientes são direcionados a usar.   Noções básicas sobre como e quando os clientes usam local do serviço para localizar recursos de site podem ajudá-lo a configurar seus sites para dar suporte a operações do cliente com sucesso.   Essas configurações podem exigir que o site interaja com configurações de rede e de domínio, como o AD DS (Serviços de Domínio do Active Directory) e o DNS, ou que você configure alternativas mais complexas.  

 Exemplos de funções de sistema de site que fornecem serviços incluem o servidor do sistema de sites principal para clientes, o ponto de gerenciamento e servidores de sistema de sites adicionais com o qual o cliente pode se comunicar, como pontos de distribuição e pontos de atualização de software.  



##  <a name="a-namebkmkfunda-fundamentals-of-service-location"></a><a name="bkmk_fund"></a> Fundamentals of service location  
 Um cliente avalia seu local de rede atual, a preferência de protocolo de comunicação e o site atribuído ao usar o local do serviço para localizar um ponto de gerenciamento com o qual ela possa se comunicar.  

 **Um cliente se comunica com um ponto de gerenciamento para:**  
-   Baixar informações sobre outros pontos de gerenciamento para o site para que eles possam criar uma lista de MP de ciclos de local de serviço futuros  
-   Carregar os detalhes de configuração, como inventário e status  
-   Baixar a política que define as configurações no cliente e poder informar ao cliente de software que ele pode ou deve instalar e outras tarefas relacionadas.  
-   Solicitar informações sobre funções de sistema de sites adicionais que fornecem serviços para cujo uso o cliente foi configurado, como pontos de distribuição de software que ele pode instalar ou um ponto de atualização de software do qual obter atualizações.  

**Um cliente do Configuration Manager faz uma solicitação de local do serviço:**  
-   A cada 25 horas de operação contínua  
-   Quando o cliente detecta uma mudança de sua configuração de rede ou local  
-   Quando o serviço **ccmexec.exe** é iniciado no computador (o serviço de cliente de núcleo)  
-   Quando o cliente deve localizar uma função de sistema de sites que fornece um serviço necessário  

**Ao tentar encontrar servidores que hospedam as funções do sistema de sites**, o cliente usa o local do serviço para localizar uma função do sistema de sites que dá suporte ao protocolo do cliente (HTTP ou HTTPS). Por padrão, os clientes usam o método mais seguro disponível para eles:  

-   Para usar HTTPS, é necessário ter uma infraestrutura de chave pública (PKI) e instalar certificados PKI em clientes e servidores. Para obter informações sobre como usar certificados, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   Quando você implanta uma função de sistema de site que usa o Internet Information Services (IIS) oferece suporte à comunicação de clientes, você deve especificar se os clientes conectam ao sistema de site usando HTTP ou HTTPS. Se você usar HTTP, também deve considerar as opções de assinatura e criptografia. Para obter mais informações, consulte [Planning for Signing and Encryption (Planejando assinatura e criptografia)](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) no tópico [Planejar a segurança no System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="a-namebkmkplanservicelocationa-service-location-and-how-clients-determine-their-assigned-management-point"></a><a name="BKMK_Plan_Service_Location"></a> Local do serviço e como os clientes determinam seu ponto de gerenciamento atribuído  
Quando um cliente atribui inicialmente a um site primário, ele seleciona um ponto de gerenciamento padrão para o site. (Sites primários dão suporte a vários pontos de gerenciamento, e cada cliente independente identifica um ponto de gerenciamento como seu ponto de gerenciamento padrão.)  Esse ponto de gerenciamento padrão então se torna aquele que os clientes atribuíram ao ponto de gerenciamento. (Você também pode usar comandos de instalação do cliente para definir o ponto de gerenciamento atribuído para um cliente no momento em que ele instala.)  

-   Os clientes selecionam um ponto de gerenciamento para se comunicarem com base no local de rede atual e nas configurações de grupo de limite. Embora tenha um ponto de gerenciamento atribuído, esse não pode ser o ponto de gerenciamento que o cliente usa.  

    > [!NOTE]  
    >  Um cliente sempre usa o ponto de gerenciamento atribuído para mensagens de registro e determinadas mensagens de política, mesmo quando outras comunicações são enviadas para um proxy ou um ponto de gerenciamento local.  

-   Você pode usar pontos de gerenciamento preferenciais. Um ponto de gerenciamento preferencial é um ponto de gerenciamento associado a um grupo de limites como o servidor do sistema de sites, semelhante ao modo como os pontos de distribuição ou pontos de migração de estado são associados a um grupo de limites. Se você habilitar pontos de gerenciamento preferenciais para a hierarquia, quando um cliente usar um ponto de gerenciamento do seu site atribuído, ele tentará usar um ponto de gerenciamento preferencial antes de usar outros pontos de gerenciamento de seu site atribuído.  

-   Você também pode usar as informações no seguinte blog do TechNet.com para configurar a afinidade do ponto de gerenciamento. A afinidade do ponto de gerenciamento substitui o comportamento padrão para pontos de gerenciamento atribuídos e permite que o cliente use um ou mais pontos de gerenciamento específicos: [afinidade do ponto de gerenciamento](http://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx).  

Cada vez que um cliente precisa fazer contato com um ponto de gerenciamento, ele verifica uma lista de pontos de gerenciamento conhecidos (conhecida como o **lista de MP**) a qual é localmente armazenada no WMI. O cliente cria uma lista de MP inicial quando é instalado e atualiza periodicamente a lista com detalhes sobre cada ponto de gerenciamento na hierarquia.  

Quando o cliente não consegue localizar um ponto de gerenciamento válido na sua lista de MP, ele pesquisa as seguintes origens de local de serviço, em ordem, até encontrar um ponto de gerenciamento que pode ser usado:  

1.  Ponto de gerenciamento  
2.  Serviços de Domínio do Active Directory  
3.  DNS  
4.  WINS  

Depois que um cliente localiza e entra em contato com sucesso com um ponto de gerenciamento de uma dessas origens, ele baixa a lista atual de pontos de gerenciamento que estão disponíveis na hierarquia e atualiza sua lista de MP local. Isso se aplica igualmente a clientes que estão associados ao domínio e os que não estão.  

Por exemplo, quando um cliente do Configuration Manager na Internet se conecta a um ponto de gerenciamento baseado na Internet, o ponto de gerenciamento envia para esse cliente uma lista de pontos de gerenciamento disponíveis baseados na Internet no site. Da mesma forma, os clientes que ingressaram no domínio ou em grupos de trabalho também recebem a lista de pontos de gerenciamento que eles podem usar.  
-   Um cliente que não está configurado para a Internet não receberia somente pontos de gerenciamento da Internet.  
-   Clientes de grupo de trabalho configurados para a Internet comunicam-se apenas com pontos de gerenciamento da Internet.  

##  <a name="a-namebkmkmplista-the-mp-list"></a><a name="BKMK_MPList"></a> A lista de MP  
A lista de MP é a origem preferencial para o local de origem do serviço para um cliente, pois é uma lista priorizada de pontos de gerenciamento que o cliente já identificou. Essa lista é classificada por cada cliente com base em seu local de rede no momento em que o cliente atualizou a lista, armazenando-a localmente no cliente no WMI.  

### <a name="building-the-initial-mp-list"></a>Criando a lista inicial de MP  
Durante a instalação do cliente, as regras a seguir são usadas para criar os a **lista MP**inicial do cliente:  

-   A lista inicial inclui pontos de gerenciamento especificados durante a instalação do cliente (quando você usa o **SMSMP**= ou as opções **/MP** ).  
-   O cliente consulta o Active Directory Domain Services (AD DS) em busca de pontos de gerenciamento publicados. Para ser identificado no AD DS, o ponto de gerenciamento deve ser proveniente do site atribuído do cliente e ser da mesma versão do produto do cliente.  
-   Se nenhum ponto de gerenciamento foi especificado durante a instalação do cliente e o esquema do Active Directory não foi estendido, o cliente verifica DNS e WINS em busca de pontos de gerenciamento publicados.  
-   Ao criar a lista inicial, as informações sobre alguns pontos de gerenciamento na hierarquia podem não ser conhecidas.  

### <a name="organizing-the-management-point-list"></a>Organizando a lista de pontos de gerenciamento  
Os clientes organizam sua lista de pontos de gerenciamento usando as seguintes classificações:  

-   **Proxy**: um ponto de gerenciamento de proxy é um ponto de gerenciamento em um site secundário.  
-   **Local**: qualquer ponto de gerenciamento associado ao local de rede atual do cliente conforme definido pelos limites do site.  
    -   Quando um cliente pertence a mais de um grupo de limites, a lista de pontos de gerenciamento local é determinada pela união de todos os limites que incluem o local de rede atual do cliente.  
    -   Normalmente, os pontos de gerenciamento **Local** são um subconjunto de pontos de gerenciamento **Atribuído** , a menos que o cliente esteja em um local de rede associado a outro site com os pontos de manutenção de seus grupos de limites.   


-   **Atribuído**: qualquer ponto de gerenciamento que é um sistema de sites para o site atribuído do cliente.  

     Você pode usar pontos de gerenciamento preferenciais. Os pontos de gerenciamento preferenciais são pontos de gerenciamento do site atribuído de um cliente associados a um grupo de limites que o cliente usa para encontrar servidores do sistema de sites.  

     Os pontos de gerenciamento em um site que não estão associados a um grupo de limites ou que não estão em um grupo de limites associado ao local de rede atual de um cliente não são considerados preferenciais e serão usados quando o cliente não conseguir identificar um ponto de gerenciamento preferencial disponível.  

### <a name="selecting-a-management-point-to-use"></a>Selecionando um ponto de gerenciamento para usar  
Para comunicações típicas, um cliente tenta usar um ponto de gerenciamento por meio das classificações na seguinte ordem, com base no local de rede do cliente:  

1.  Proxy  
2.  Local  
3.  Atribuído  

No entanto, o cliente sempre usa o ponto de gerenciamento atribuído para mensagens de registro e determinadas mensagens de política, mesmo quando outras comunicações são enviadas para um proxy ou um ponto de gerenciamento local.  

Dentro de cada classificação (proxy, local ou atribuído), os clientes tentarão usar um ponto de gerenciamento com base nas preferências, na seguinte ordem:  

1.  Compatível com HTTPS em uma floresta confiável ou local (quando o cliente está configurado para comunicação HTTPS)  
2.  Compatível com HTTPS fora de uma floresta confiável ou local (quando o cliente está configurado para comunicação HTTPS)  
3.  Compatível com HTTP em uma floresta confiável ou local  
4.  Compatível com HTTP fora de uma floresta confiável ou local  

Do conjunto de pontos de gerenciamento classificadas pelas preferências, os clientes tentam usar o primeiro ponto de gerenciamento na lista:  

-   Essa lista classificada de pontos de gerenciamento é aleatória e não pode ser ordenada.  
-   A ordem da lista pode mudar cada vez que o cliente atualizar sua lista de pontos de gerenciamento.  

Quando um cliente não puder estabelecer contato com o primeiro ponto de gerenciamento, ele tenta cada ponto de gerenciamento sucessivo em sua lista, tentando cada ponto de gerenciamento preferencial na classificação antes de tentar os pontos de gerenciamento não preferenciais. Se um cliente não puder se comunicar com êxito com nenhum ponto de gerenciamento na classificação, ele tentará contatar um ponto de gerenciamento preferido da próxima classificação, e assim por diante, até o cliente encontrar um ponto de gerenciamento para usar.  

Depois de estabelecer comunicação com um ponto de gerenciamento, os clientes continuam a usar o mesmo ponto de gerenciamento até:  

-   Após 25 horas, o cliente seleciona aleatoriamente um novo ponto de gerenciamento para usar.  
-   O cliente não é capaz de se comunicar com o ponto de gerenciamento após 5 tentativas por um período de 10 minutos, quando então o cliente seleciona um novo ponto de gerenciamento para usar.  

##  <a name="a-namebkmkada-active-directory"></a><a name="bkmk_ad"></a> Active Directory  
Clientes que ingressaram no domínio podem usar os o Active Directory Domain Services (AD DS) para o local do serviço. Isso requer que sites [publiquem dados para o Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

Os clientes podem usar os o Active Directory Domain Services para o local do serviço quando todas as seguintes condições forem verdadeiras:  

-   O [esquema do Active Directory foi estendido](https://technet.microsoft.com/library/mt345589.aspx) ou foi estendido para o System Center 2012 Configuration Manager.  
-   A floresta do [Active Directory é configurada para publicação](http://technet.microsoft.com/library/hh696542.aspx)e os sites do Configuration Manager estão configurados para publicação.  
-   O computador cliente for um membro de um domínio do Active Directory e puder acessar um servidor de catálogo global.  

Se um cliente não conseguir localizar um ponto de gerenciamento para usar a localização de serviço do AD DS, em seguida, ele tentará usar DNS. Clientes que ingressaram no domínio podem usar o AD DS para o local do serviço. Isso requer que sites [publiquem dados para o Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

##  <a name="a-namebkmkdnsa-dns"></a><a name="bkmk_dns"></a> DNS  
Clientes na intranet podem usar o DNS para o local do serviço. Isso exige que pelo menos um site em uma hierarquia publique informações sobre pontos de gerenciamento no DNS.  

Considere usar o DNS para o local do serviço quando qualquer uma das seguintes condições forem verdadeiras:
-   O esquema do Active Directory Domain Services não tiver sido estendido para dar suporte ao Configuration Manager.
-   Os clientes da intranet estiverem localizados em uma floresta que não esteja habilitada para publicar no Configuration Manager.  
-   Você possui clientes em computadores do grupo de trabalho, os quais não estão configurados para gerenciamento de cliente somente pela Internet. (Um cliente de grupo de trabalho configurado para a Internet somente se comunicará com pontos de gerenciamento da Internet e não usará o DNS para o local do serviço.)  
-   Você pode [configurar clientes para localizar pontos de gerenciamento do DNS](http://technet.microsoft.com/library/gg682055).  

Quando um site publica registros de localização de serviço para pontos de gerenciamento no DNS:  

-   A publicação é aplicável somente a pontos de gerenciamento que aceitam conexões de clientes da intranet.  
-   A publicação adiciona um registro de recurso de local de serviço (SRV RR) na zona DNS do computador do ponto de gerenciamento. Deve haver uma entrada correspondente do host no DNS para o computador.  

Por padrão, clientes ingressados no domínio pesquisam DNS em busca de registros de ponto de gerenciamento do domínio local do cliente. Você pode configurar uma propriedade de cliente que especifica um sufixo de domínio para um domínio que tem informações de ponto de gerenciamento publicadas no DNS.  

Para obter mais informações sobre como configurar a propriedade de sufixo DNS do cliente, consulte [Como configurar computadores cliente para localizar pontos de gerenciamento usando a publicação do DNS no System Center Configuration Manager](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Se um cliente não conseguir localizar um ponto de gerenciamento para usar a localização de serviço do DNS, em seguida, ele tentará usar WINS.  

### <a name="publish-management-points-to-dns"></a>Publicar pontos de gerenciamento no DNS  
Para publicar pontos de gerenciamento no DNS, as seguintes condições devem ser verdadeiras:  

-   Seus servidores DNS suportarem registros de recursos de localização de serviço, usando no mínimo uma versão 8.1.2 do BIND.  
-   Os FQDNs da intranet especificados para os pontos de gerenciamento no Configuration Manager tiverem entradas de host (por exemplo, registros A) no DNS.  

> [!IMPORTANT]  
>  A publicação de DNS do Configuration Manager não dão suporte a um namespace não contíguo. Se você tiver um namespace separado, você poderá publicar manualmente pontos de gerenciamento no DNS ou usar um dos outros métodos alternativos de localização de serviço documentados nesta seção.  

**Quando os seus servidores DNS dão suporte a atualizações automáticas**, é possível configurar o Configuration Manager para publicar automaticamente pontos de gerenciamento na intranet no DNS ou é possível publicar manualmente esses registros no DNS. Quando pontos de gerenciamento são publicados no DNS, seus números de portas e FQDNs da intranet são publicados no registro de localização de serviço (SRV). Você pode configurar a publicação de DNS em um site nos sites de propriedades do componente do ponto de gerenciamento. Para obter mais informações, consulte [Site components for System Center Configuration Manager (Componentes do site para o System Center Configuration Manager)](../../../core/servers/deploy/configure/site-components.md).  

**Quando a Zona DNS é definida como "Somente seguro" para Atualizações Dinâmicas**, somente o primeiro ponto de gerenciamento para publicação no DNS pode fazer isso com êxito com as permissões padrão.
- Se apenas um ponto de gerenciamento puder publicar e modificar com êxito seu registro DNS, contanto que o servidor desse ponto de gerenciamento permaneça íntegro, os clientes poderão obter a lista completa de MP desse ponto de gerenciamento e, em seguida, localizar o ponto de gerenciamento preferencial.


**Quando seus servidores DNS não suportarem atualizações automáticas, mas suportarem registros de localização de serviços**, você poderá publicar manualmente pontos de gerenciamento no DNS. Para fazer isso, é necessário especificar manualmente o registro de recurso de localização de serviço (SRV RR) no DNS.  

O Configuration Manager dá suporte à RFC 2782 para registros de local do serviço, que têm o seguinte formato: *_Service._Proto.Name TTL Class SRV Priority Weight Port Target*  

Para publicar um ponto de gerenciamento no Configuration Manager, especifique os seguintes valores:  

-   **_Service**: Insira **_mssms_mp***_&lt;códigodosite\>*, em que *&lt;códigodosite\>* é o código do site do ponto de gerenciamento.  
-   **._Proto**: especifique **._tcp**.  
-   **.Name**: insira o sufixo DNS do ponto de gerenciamento, por exemplo **contoso.com**.  
-   **TTL**: insira **14400**, que é de quatro horas.  
-   **Classe**: especifique **IN** (em conformidade com a RFC 1035).  
-   **Prioridade**: esse campo não é usado pelo Configuration Manager.
-   **Peso**: esse campo não é usado pelo Configuration Manager.  
-   **Porta**: insira o número da porta que o ponto de gerenciamento usa, por exemplo **80** para HTTP e **443** para HTTPS.  

    > [!NOTE]  
    >  A porta do registro SRV deve corresponder à porta de comunicação usada pelo ponto de gerenciamento. Por padrão, ela é **80** para comunicação HTTP e **443** para comunicações HTTPS.  

-   **Destino**: insira o FQDN da intranet especificado para o sistema de site que é configurado com a função do site do ponto de gerenciamento.  

Se você estiver usando o DNS do Windows Server, você poderá usar o procedimento a seguir para inserir esse registro DNS nos pontos de gerenciamento da intranet. Se você estiver usando uma implementação diferente para DNS, use as informações desta seção sobre os valores dos campos e consulte a documentação de DNS para adaptar esse procedimento.  

##### <a name="to-configure-automatic-publishing"></a>Para configurar a publicação automática:  

1.  No console do Configuration Manager, expanda **Administração** > **Configuração de Site** > **Sites**.  

2.  Selecione seu site e clique em **Configurar Componentes do Site**.  

3.  Selecione **Ponto de Gerenciamento**.  

4.  Selecione os pontos de gerenciamento que você deseja publicar. (Esta seleção se aplica à publicação no AD DS e DNS).  

5.  Marque a caixa de seleção para publicar no DNS:  

    -   Essa caixa de diálogo permite selecionar quais pontos de gerenciamento publicar e publicá-los no DNS.  

    -   Essa caixa de diálogo não configura a publicação para o AD DS.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Para publicar manualmente os pontos de gerenciamento no DNS do Windows Server  

1.  No console do Configuration Manager, especifique os FQDNs dos sistemas de site da intranet.  

2.  No console de gerenciamento do DNS, selecione a zona DNS para o computador do ponto de gerenciamento.  

3.  Verifique se há um registro de host (A ou AAAA) para o FQDN do sistema de site da intranet. Se esse registro não existir, crie-o.  

4.  Usando a opção **Outros Novos Registros** , clique em **Local do Serviço (SRV)** na caixa de diálogo **Tipo de Registro de Recurso** , clique em **Criar Registro**, digite as seguintes informações e clique em **Concluído**:  

    -   **Domínio**: se necessário, digite o sufixo DNS do ponto de gerenciamento, por exemplo **contoso.com**.  
    -   **Serviço**: Digite **_mssms_mp***_&lt;códigodosite\>*, em que *&lt;códigodosite\>* é o código do site do ponto de gerenciamento.  
    -   **Protocolo**: tipo **_tcp**.  
    -   **Prioridade**: esse campo não é usado pelo Configuration Manager.  
    -   **Peso**: esse campo não é usado pelo Configuration Manager.  
    -   **Porta**: insira o número da porta que o ponto de gerenciamento usa, por exemplo **80** para HTTP e **443** para HTTPS.  

        > [!NOTE]  
        >  A porta do registro SRV deve corresponder à porta de comunicação usada pelo ponto de gerenciamento. Por padrão, ela é **80** para comunicação HTTP e **443** para comunicações HTTPS.  

    -   **Host que oferece este serviço**: insira o nome de domínio totalmente qualificado da intranet especificado para o sistema de site que é configurado com a função do site do ponto de gerenciamento.  

Repita essas etapas para cada ponto de gerenciamento da intranet que você desejar publicar no DNS.  

##  <a name="a-namebkmkwinsa-wins"></a><a name="bkmk_wins"></a> WINS  
Quando outros mecanismos de localização de serviço falharem, os clientes poderão encontrar um ponto de gerenciamento inicial verificando o WINS.  

Por padrão, um site primário publica para o WINS, o primeiro ponto de gerenciamento no site que está configurado para HTTP e o primeiro ponto de gerenciamento configurado para HTTPS.  

Se você não quiser que os clientes encontrem um ponto de gerenciamento HTTP em WINS, configure-os com a propriedade CCMSetup.exe Client.msi **SMSDIRECTORYLOOKUP=NOWINS**.  



<!--HONumber=Dec16_HO3-->


