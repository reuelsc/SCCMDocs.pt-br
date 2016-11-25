---
title: Planejar o Provedor de SMS | System Center Configuration Manager
description: "Saiba mais sobre como o Provedor de SMS ajuda você a gerenciar o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bdf7b9b4ab9e9da25bf32891381f61c94ef28285


---
# <a name="plan-for-the-sms-provider-for-system-center-configuration-manager"></a>Planejar o Provedor de SMS para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para gerenciar o System Center Configuration Manager, você usar um console do Configuration Manager que se conecta a uma instância do **Provedor de SMS**. Por padrão, um provedor de SMS é instalado em um site de administração central ou site primário, quando o site é instalado.  


##  <a name="a-namebkmkplansmsprova-about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> Sobre o provedor de SMS  
 O Provedor de SMS é um provedor de WMI (Instrumentação de Gerenciamento do Windows) que atribui acesso de **leitura** e **gravação** ao banco de dados do Configuration Manager em um site:  

-   O grupo **Administradores de SMS**  fornece acesso ao provedor de SMS. O Configuration Manager cria automaticamente este grupo de segurança no servidor do site e em cada computador do Provedor de SMS.  

-   Cada site de administração central e cada site primário exigem, pelo menos, um provedor de SMS.  Você pode instalar provedores adicionais conforme necessário.  

-   Sites secundários não dão suporte para o Provedor de SMS.  


Cada console do Configuration Manager, o Gerenciador de Recursos, as ferramentas e os scripts personalizados usam um Provedor de SMS para que os usuários administrativos do Configuration Manager possam acessar as informações armazenadas no banco de dados. O Provedor de SMS não interage com os clientes do Configuration Manager. Quando um console do Configuration Manager se conecta a um site, o console do Configuration Manager solicita que o WMI no servidor do site localize uma instância do Provedor de SMS para ele usar.  

 O Provedor de SMS ajuda a reforçar a segurança do Configuration Manager. Retorna apenas informações que o usuário administrativo que está executando o console do Configuration Manager tem autorização para exibir.  

> [!IMPORTANT]  
>  Quando os computadores que contêm um Provedor de SMS de um site estão offline, os consoles do Configuration Manager não conseguem se conectar ao banco de dados desse site.  

 Para obter mais informações sobre como gerenciar o provedor de SMS, veja [Manage the SMS Provider](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) em [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md).  

 **Pré-requisitos para instalar o provedor de SMS:**  

 Para dar suporte ao provedor de SMS:  

-   o computador deve estar em um domínio que tenha uma relação de confiança bidirecional com o servidor do site e com os sistemas de site do banco de dados do site.  

-   o computador não pode ter uma função do sistema de um site diferente.  

-   o computador não pode ter um Provedor de SMS de qualquer site.  

-   o computador deve executar um sistema operacional que seja compatível com um servidor de site.  

-   O computador deve ter pelo menos 650 MB de espaço livre em disco para dar suporte aos componentes do Windows ADK (Kit de Implantação Automatizada do Windows) instalados com o Provedor de SMS. Para obter mais informações sobre o Windows ADK e o provedor de SMS, veja [Requisitos de implantação do sistema operacional para o Provedor de SMS](#BKMK_WAIKforSMSProv) neste tópico.  

##  <a name="a-namebkmklocationa-sms-provider-locations"></a><a name="bkmk_location"></a> Locais do Provedor de SMS  
 Quando você instala um site, o primeiro provedor de SMS para o site é instalado automaticamente. Você pode especificar qualquer um dos seguintes locais com suporte para o Provedor de SMS:  

-   o computador do servidor do site  

-   o computador do banco de dados do site  

-   um computador de classe de servidor que não tenha Provedor de SMS ou função de sistema de um site diferente  


Para exibir os locais de cada Provedor de SMS instalado em um local, consulte a guia **Geral** da caixa de diálogo **Propriedades** do site.  

 Cada Provedor de SMS oferece suporte a conexões simultâneas de várias solicitações. As únicas limitações a essas conexões são o número de conexões de servidores disponíveis no computador do Provedor de SMS e os recursos disponíveis no computador do Provedor de SMS para atendimento às solicitações de conexão.  

 Depois que um site é instalado, você pode executar a Instalação no servidor do site novamente para alterar a localização de um Provedor de SMS existente ou para instalar Provedores de SMS adicionais no site. Em um computador é possível instalar apenas um Provedor de SMS, e um computador não pode instalar Provedores de SMS de mais de um site.  

 Use o seguinte para identificar as vantagens e desvantagens de instalar um Provedor de SMS em cada local com suporte:  


**Servidor do site do Configuration Manager**  

-   **Vantagens:**  

    -   O Provedor de SMS não usa os recursos de sistema do computador do banco de dados do site.  

    -   Esse local pode proporcionar um desempenho melhor do que um Provedor de SMS localizado em um computador diferente do servidor do site ou no computador do banco de dados do site.  

-   **Desvantagens:**  

    -   O Provedor de SMS usa recursos de sistema e de rede que poderiam ser dedicados a operações de servidor do site.  


**SQL Server que hospeda o banco de dados do site**  

-   **Vantagens:**  

    -   O Provedor de SMS não usa recursos do sistema de site no servidor do site.  

    -   Esse local pode fornecer o melhor desempenho dos três locais, se houver recursos suficientes do servidor.  

-   **Desvantagens:**  

    -   O Provedor de SMS usa recursos de sistema e de rede que poderiam ser dedicados a operações de banco de dados do site.  

    -   Esse local não é uma opção quando o banco de dados do site está hospedado em uma instância clusterizada do SQL Server.  


**Computador diferente do servidor do site ou computador do banco de dados do site**  

-   **Vantagens:**  

    -   O Provedor de SMS não usa o servidor do site ou recursos do computador do banco de dados do site.  

    -   Esse tipo de local permite que você implante Provedores de SMS adicionais para fornecer alta disponibilidade para conexões.  

-   **Desvantagens:**  

    -   O desempenho do Provedor de SMS pode ser reduzido em razão do tráfego de rede adicional necessário para a coordenação com o servidor do site e com o computador do banco de dados do site.  

    -   Esse servidor deve estar sempre acessível ao computador do banco de dados do site e a todos os computadores com o console do Configuration Manager instalado.  

    -   Esse local pode usar recursos de sistema que seriam dedicados a outros serviços.  

##  <a name="a-namebkmksmsprovlanguagesa-about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a> Sobre idiomas do Provedor de SMS  
 O Provedor de SMS funciona independentemente do idioma de exibição do computador onde ele está instalado.  

 Quando um usuário administrativo ou um processo do Configuration Manager solicita dados usando o Provedor de SMS, o Provedor de SMS tenta retornar os dados em um formato que corresponda ao idioma do sistema operacional do computador solicitante. O Provedor de SMS não converte as informações de um idioma para outro. Em vez disso, quando os dados são retornados para exibição no console do Configuration Manager, o idioma de exibição dos dados depende da origem do objeto e do tipo de armazenamento.  

 Quando os dados de um objeto são armazenados no banco de dados, os idiomas disponíveis dependem do seguinte:  

-   Os objetos que o Configuration Manager cria são armazenados no banco de dados usando suporte para vários idiomas. O objeto é armazenado usando os idiomas configurados no local onde ele é criado quando se executa a Instalação. Esses objetos são exibidos no console do Configuration Manager no idioma de exibição do computador solicitante, quando o idioma está disponível para o objeto. Se o objeto não puder ser exibido no idioma de exibição do computador solicitante, ele será exibido no idioma padrão, que é o inglês.  

-   O objeto que um usuário administrativo cria é armazenado no banco de dados usando o idioma utilizado para se criar esse objeto. Esses objetos são exibidos no console do Configuration Manager no mesmo idioma. Eles não podem ser convertidos pelo Provedor de SMS e não possuem várias opções de idioma.  

##  <a name="a-namebkmkmultismsprova-use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a> Use vários Provedores de SMS  
 Após a instalação de um site, você pode instalar Provedores de SMS adicionais nele. Para instalar Provedores de SMS adicionais, execute a Instalação do Configuration Manager no servidor do site. Considere a instalação de Provedores de SMS adicionais quando qualquer uma das seguintes situações for verdadeira:  

-   você terá um grande número de usuários administrativos que, ao mesmo tempo, executam um console do Configuration Manager e se conectam a um site.  

-   você usará o SDK do Configuration Manager ou outros produtos que podem apresentar chamadas frequentes ao Provedor de SMS.  

-   você quer garantir alta disponibilidade para o Provedor de SMS.  


Quando vários Provedores de SMS estão instalados em um local e uma solicitação de conexão é feita, o local, de forma não determinística, atribui cada nova solicitação de conexão ao uso de um Provedor de SMS instalado. Não é possível especificar o local do Provedor de SMS a ser usado em uma sessão de conexão específica.  

> [!NOTE]  
>  Considere as vantagens e as desvantagens de cada local de Provedor de SMS e equilibre essas considerações com as informações que você não pode controlar, como quais Provedores de SMS serão usados para cada nova conexão.  

Por exemplo, quando você conecta um console do Configuration Manager pela primeira vez a um site, a conexão solicita ao WMI no servidor do site para identificar, de forma não determinística, uma instância do Provedor de SMS que o console usará. Essa instância específica do Provedor de SMS continua em uso pelo console do Configuration Manager até que a sessão do console do Configuration Manager termine. Se a sessão terminar devido ao computador do Provedor de SMS ficar indisponível na rede, quando você se conectar novamente ao console do Configuration Manager o site atribuirá, de forma não determinística, um computador do Provedor de SMS à nova sessão de conexão. É possível ser atribuído ao mesmo computador do Provedor de SMS que não está disponível. Se isso ocorrer, tente reconectar o console do Configuration Manager até que seja atribuído um computador disponível do Provedor de SMS.  

##  <a name="a-namebkmkaboutsmsadminsa-about-the-sms-admins-group"></a><a name="BKMK_AboutSMSAdmins"></a> Sobre o grupo de administradores de SMS  
 Use o grupo de administradores de SMS para fornecer acesso de usuário administrativo ao Provedor de SMS. O grupo é criado automaticamente no servidor do site quando o site é instalado, bem como em cada computador que instala um Provedor de SMS. Informações adicionais sobre o grupo de administradores de SMS:  

-   quando o computador é um servidor membro, o grupo de administradores de SMS é criado como um grupo local.  

-   quando o computador é um controlador de domínio, o grupo de administradores de SMS é criado como um grupo local de domínio.  

-   quando o Provedor de SMS é desinstalado de um computador, o grupo de administradores de SMS não é removido do computador.  


Para que um usuário possa fazer uma conexão bem-sucedida a um Provedor de SMS, sua conta de usuário deve ser um membro do grupo de administradores de SMS. Cada usuário administrativo que você configura no console do Configuration Manager é automaticamente adicionado ao grupo de administradores de SMS em cada servidor do site e a cada computador Provedor de SMS na hierarquia. Quando você exclui um usuário administrativo do console do Configuration Manager, esse usuário é removido do grupo de administradores de SMS em cada servidor do site e de cada computador do Provedor de SMS na hierarquia.  

Depois que o usuário faz uma conexão bem-sucedida com o Provedor de SMS, a administração baseada em funções determina quais recursos do Configuration Manager o usuário poderá acessar ou gerenciar.  

É possível exibir e configurar os direitos e as permissões do grupo de Administradores de SMS usando o snap-in do MMC do Controle WMI. Por padrão, a opção **Todos** tem as permissões **Executar Métodos**, **Gravação do Provedor**e **Habilitar Conta** . Quando um usuário se conecta ao Provedor de SMS, é concedido a ele acesso aos dados do banco de dados do site com base em seus direitos de segurança administrativa baseados em função definidos no console do Configuration Manager. **Habilitar conta** e **Habilitação remota** é concedido explicitamente ao grupo de administradores de SMS no namespace **Root\SMS** .  

> [!NOTE]  
>  Cada usuário administrativo que usa um console remoto do Configuration Manager requer permissões DCOM de ativação remota no computador do servidor do site e no computador Provedor de SMS. Embora você possa conceder esses direitos a qualquer usuário ou grupo, como prática recomendada, atribua-os ao grupo de administradores de SMS para simplificar a administração. Para obter mais informações, consulte a seção [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) no tópico [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) .  


##  <a name="a-namebkmksmsprovnamespacea-about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a> Sobre o namespace do Provedor de SMS  
A estrutura do Provedor de SMS é definida pelo esquema WMI. Namespaces do esquema descrevem a localização dos dados do Configuration Manager dentro do esquema Provedor de SMS. A tabela a seguir contém alguns namespaces comuns usados pelo Provedor de SMS.  

|espaço de nome|Descrição|  
|---------------|-----------------|  
|Root\SMS\site_*&lt;código do site\>*|O Provedor de SMS, que é muito utilizado pelo console do Configuration Manager, Gerenciador de Recursos, ferramentas do Configuration Manager e scripts.|  
|Root\SMS\SMS_ProviderLocation|Fornece a localização dos computadores do Provedor de SMS para um site.|  
|Root\cimv2|Local de inventário para obter informações de namespace do WMI durante o inventário de hardware e software.|  
|Root\CCM|Dados do cliente e políticas de configuração do cliente do Configuration Manager.|  
|root\CIMv2\SMS|Localização de classes de relatório de inventário que são coletadas pelo agente do cliente de inventário. Essas configurações são compiladas pelos clientes durante a avaliação de políticas do computador e são baseadas nas definições de configuração do cliente para o computador.|  

##  <a name="a-namebkmkwaikforsmsprova-operating-system-deployment-requirements-for-the-sms-provider"></a><a name="BKMK_WAIKforSMSProv"></a> Requisitos de implantação do sistema operacional para o Provedor de SMS  
O Provedor de SMS requer que a seguinte dependência externa seja instalada no computador que o executa para permitir a utilização das funções de tarefas de implantação do sistema operacional, usando o console do Configuration Manager:  

-   Kit de Avaliação e Implantação do Windows 8.1  

 Ao gerenciar implantações do sistema operacional, o Windows ADK permite que o Provedor de SMS conclua diversas tarefas, inclusive:  

-   Exibir detalhes do arquivo WIM  

-   Adicionar arquivos de driver a imagens de inicialização existentes  

-   Criar arquivos .ISO de inicialização  


A instalação do Windows ADK pode exigir até 650 MB de espaço livre em disco em cada computador que instalar o Provedor de SMS. A alta demanda de espaço em disco é necessária para que o Configuration Manager instale imagens de inicialização do Windows PE.  



<!--HONumber=Nov16_HO1-->


