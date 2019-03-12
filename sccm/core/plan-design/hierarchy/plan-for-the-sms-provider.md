---
title: Planejar o provedor de SMS
titleSuffix: Configuration Manager
description: Saiba sobre a função do sistema de site do Provedor de SMS no Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aec16c4b55afd8c4baf7486794e07f29fa84aebf
ms.sourcegitcommit: 223549003829fce7c6dc63959ee71e8b88542417
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56951827"
---
# <a name="plan-for-the-sms-provider"></a>Planejar o provedor de SMS 

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para gerenciar o Configuration Manager, você usa um console do Configuration Manager que se conecta a uma instância do **Provedor de SMS**. Por padrão, um provedor de SMS é instalado no servidor de sites ao instalar em um site de administração central ou site primário. 



##  <a name="BKMK_PlanSMSProv"></a> Sobre o provedor de SMS  

O Provedor de SMS é um provedor de WMI (Instrumentação de Gerenciamento do Windows) que atribui acesso de **leitura** e **gravação** ao banco de dados do Configuration Manager em um site.  

- Cada site de administração central e cada site primário exigem, pelo menos, um provedor de SMS. Você pode instalar provedores adicionais conforme necessário.  

- O grupo **Administradores de SMS** fornece acesso ao provedor de SMS. O Configuration Manager cria automaticamente este grupo de segurança no servidor de sites e em cada computador em que for instalada uma instância do Provedor de SMS. Para obter mais informações, confira [Administradores de SMS](/sccm/core/plan-design/hierarchy/accounts#sms-admins).  

- Sites secundários não dão suporte à função do Provedor de SMS.  

Usuários administrativos do Configuration Manager usam um provedor de SMS para acessar as informações armazenadas no banco de dados. Para fazer isso, os administradores podem usar o console do Configuration Manager, o Gerenciador de Recursos, ferramentas e scripts personalizados. O Provedor de SMS não interage com os clientes do Configuration Manager. Quando um console do Configuration Manager se conecta a um site, ele consulta o WMI no servidor do site localize uma instância do Provedor de SMS para ele usar.  

O Provedor de SMS ajuda a reforçar a segurança do Configuration Manager. Ele retorna somente as informações que o usuário do console está autorizado a exibir.  

> [!IMPORTANT]  
>  Quando cada instância do provedor de SMS para um site está offline, os consoles do Configuration Manager não podem se conectar ao site.  

 Para obter mais informações sobre como gerenciar o Provedor de SMS, confira [Gerenciar o Provedor de SMS](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider).  



## <a name="installation-prerequisites"></a>Pré-requisitos de instalação  

 Para dar suporte ao Provedor de SMS, o servidor de destino deve atender aos seguintes pré-requisitos:  

-   No mesmo domínio que o servidor do site e os sistemas de site do banco de dados do site  

-   Não é possível ter uma função de sistema de site de um site diferente  

-   Não pode já ter um Provedor de SMS de qualquer site  

-   Executar uma versão de sistema operacional com suporte  

-   Pelo menos 650 MB de espaço livre em disco para oferecer suporte os componentes do Windows ADK. Para obter mais informações sobre o Windows ADK e o provedor de SMS, confira [Requisitos de implantação de sistema operacional](#BKMK_WAIKforSMSProv).  



##  <a name="bkmk_location"></a> Locais  

Ao instalar um site, o primeiro provedor de SMS para o site é instalado automaticamente. Você pode especificar qualquer um dos seguintes locais com suporte para o Provedor de SMS:  

-   Servidor do site  

-   O servidor de banco de dados do site  

-   Outro servidor, que cumpre os [pré-requisitos de instalação](#installation-prerequisites)  


Para exibir os locais de cada provedor de SMS de um site: 

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2. Selecione o site desejado na lista e, em seguida, escolha **Propriedades** na faixa de opções.  

3. Na guia **Geral** do site **Propriedades**, exiba o campo **Localização do provedor de SMS**.    


Cada Provedor de SMS oferece suporte a conexões simultâneas de várias solicitações. As únicas limitações a essas conexões são o número de conexões de servidor disponíveis para Windows e os recursos disponíveis no servidor para atender às solicitações de conexão.  

Depois de instalar um site, você pode executar novamente a instalação do Configuration Manager no servidor do site. Use a instalação para alterar a localização de um provedor de SMS existente ou instalar provedores de SMS adicionais nesse site. Instale somente um Provedor de SMS em um computador. Um computador não pode hospedar um provedor de SMS de mais de um site.  


### <a name="choosing-a-location"></a>Escolher uma localização 

As seguintes seções descrevem as vantagens e as desvantagens de instalar um Provedor de SMS em cada localização com suporte:  

#### <a name="configuration-manager-site-server"></a>Servidor do site do Configuration Manager

- **Vantagens:**  

    -   O Provedor de SMS não usa os recursos de sistema do computador do banco de dados do site.  

    -   Esse local pode proporcionar um desempenho melhor do que um Provedor de SMS localizado em um computador diferente do servidor do site ou no computador do banco de dados do site.  

- **Desvantagens:**  

    -   O Provedor de SMS usa recursos de sistema e de rede que poderiam ser dedicados a operações de servidor do site.  


#### <a name="sql-server-that-hosts-the-site-database"></a>SQL Server que hospeda o banco de dados do site

- **Vantagens:**  

    -   O Provedor de SMS não usa recursos do sistema no servidor do site.  

    -   Esse local pode fornecer o melhor desempenho dos três locais, se houver recursos suficientes do servidor.  

- **Desvantagens:**  

    -   O Provedor de SMS usa recursos de sistema e de rede que poderiam ser dedicados a operações de banco de dados do site.  

    -   Não é possível usar esse local quando o banco de dados do site está hospedado em uma instância clusterizada do SQL Server.  


#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>Computador diferente do servidor do site ou servidor de banco de dados do site

- **Vantagens:**  

    -   O Provedor de SMS não usa o servidor do site nem recursos do sistema do banco de dados do site.  

    -   Esse tipo de local permite que você implante Provedores de SMS adicionais para fornecer alta disponibilidade para conexões.  

- **Desvantagens:**  

    -   O desempenho do provedor de SMS pode ser reduzido. Esse comportamento é devido à atividade de rede adicional necessária para coordenar com o servidor do site e o computador do banco de dados do site.  

    -   Esse servidor deve estar sempre acessível ao servidor de banco de dados do site e a todos os computadores com o console do Configuration Manager instalado.  

    -   Esse local pode usar recursos de sistema que seriam dedicados a outros serviços.  



## <a name="bkmk_auth"></a> Autenticação
<!--1357013-->

Da versão 1810 em diante, você pode especificar o nível mínimo de autenticação para os administradores acessarem sites do Configuration Manager. Esse recurso faz com que os administradores entrem no Windows com o nível necessário. Isso se aplica a todos os componentes que acessam o Provedor de SMS. Por exemplo, o console do Configuration Manager, os métodos do SDK e os cmdlets do Windows PowerShell. 


### <a name="configure-authentication"></a>Configurar a autenticação

Para definir essa configuração, primeiro entre no Windows com o nível de autenticação pretendido. 

> [!Important]  
> Essa configuração é uma configuração de toda a hierarquia. Antes de alterar essa configuração, verifique se todos os administradores do Configuration Manager podem entrar no Windows com o nível de autenticação necessário. 

Para definir essa configuração, use as seguintes etapas:

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2. Clique em **Configurações da Hierarquia** na faixa de opções.  

3. Mude para a guia **Autenticação**. Selecione o [nível de autenticação](#authentication-levels) desejado e, em seguida, selecione **OK**.  

    - Somente quando necessário, selecione **Adicionar** para excluir usuários ou grupos específicos. Para obter mais informações, confira [Exclusões](#exclusions).  


### <a name="authentication-levels"></a>Níveis de autenticação

Os seguintes níveis estão disponíveis:

- **Autenticação do Windows**: Exige autenticação com credenciais de domínio do Active Directory. Essa configuração é o comportamento anterior e a configuração padrão atual. Quando você atualiza o site, não há alteração no nível de autenticação.  

- **Autenticação de certificado**: Exige autenticação com um certificado válido emitido por uma autoridade de certificação PKI confiável. Você não configura esse certificado no Configuration Manager. O Configuration Manager exige que o administrador esteja conectado ao Windows usando a PKI.  

- **Autenticação do Windows Hello para Empresas**: Exige autenticação com autenticação forte de dois fatores que esteja vinculada a um dispositivo e use biometria ou um PIN. Para obter mais informações, confira [Windows Hello para Empresas](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).   


### <a name="exclusions"></a>Exclusões

Na guia **Autenticação** das Configurações da Hierarquia, você também pode excluir determinados usuários ou grupos. Use essa opção com moderação. Por exemplo, quando usuários específicos exigem acesso ao console do Configuration Manager, mas não podem autenticar no Windows no nível necessário. Também pode ser necessário para automação ou serviços executados no contexto de uma conta do sistema.



##  <a name="BKMK_SMSProvLanguages"></a> Sobre idiomas do Provedor de SMS  

O Provedor de SMS funciona de modo independente do idioma de exibição do servidor em que ele está instalado.  

Quando um usuário administrativo ou um processo do Configuration Manager solicita dados usando o Provedor de SMS, ele tenta retornar esses dados em um formato que corresponde ao idioma do sistema operacional do computador solicitante.

A maneira como ele tenta combinar o idioma é indireta. O Provedor de SMS não converte as informações de um idioma para outro. Quando ele retorna dados para exibição no console do Configuration Manager, o idioma de exibição dos dados depende da origem do objeto e do tipo de armazenamento.  

Quando o Configuration Manager armazena dados para um objeto no banco de dados, os idiomas disponíveis dependem dos seguintes fatores:  

-   O Configuration Manager armazena objetos que ele cria usando suporte para vários idiomas. Ele armazena o objeto no banco de dados do site usando os idiomas que você configura para o site ao executar a instalação. O console do Configuration Manager exibe esses objetos no idioma de exibição do computador solicitante, quando o idioma está disponível para o objeto. Se o console não puder exibir o objeto no idioma de exibição do computador solicitante, ele exibirá o objeto no idioma padrão, que é o inglês.  

-   O Configuration Manager armazena objetos que um usuário administrativo cria usando o idioma utilizado para criar o objeto. Esses objetos são exibidos no console do Configuration Manager no mesmo idioma. O Provedor de SMS não pode convertê-los e eles não têm várias opções de idioma.  



##  <a name="BKMK_MultiSMSProv"></a> Use vários Provedores de SMS  

 Após a instalação de um site, você pode instalar Provedores de SMS adicionais nele. Para instalar Provedores de SMS adicionais, execute a instalação do Configuration Manager no servidor do site. 

Considere a instalação de Provedores de SMS adicionais quando qualquer uma das seguintes situações for verdadeira:  

- Muitos usuários administrativos precisam usar o console do Configuration Manager e se conectar a um site ao mesmo tempo.  

- Você usará o SDK do Configuration Manager ou outros produtos que podem apresentar chamadas frequentes ao Provedor de SMS.  

- Você tem um requisito empresarial de alta disponibilidade do Provedor de SMS.  

Quando você instala vários Provedores de SMS em um site e uma solicitação de conexão é feita, o site atribui aleatoriamente cada nova solicitação de conexão para usar um Provedor de SMS instalado. Não é possível especificar o Provedor de SMS a ser usado com uma sessão de conexão específica.  

> [!NOTE]  
>  Considere as vantagens e desvantagens de cada local de provedor de SMS. Para obter mais informações, confira [Locais](#bkmk_location). Equilibre essas considerações com as informações que você não pode controlar, que são os provedores de SMS usados para cada nova conexão.  

Ao conectar um console do Configuration Manager pela primeira vez em um site, a conexão consulta WMI no servidor do site. Essa consulta identifica uma instância do Provedor de SMS que usa o console. Essa instância específica do Provedor de SMS continua em uso pelo console até que a sessão do console termine. Se a sessão terminar porque o servidor do provedor de SMS não está disponível na rede, quando você reconectar o console ao site, ele repetirá a consulta inicial. É possível que o site atribua a mesma instância do provedor de SMS que não está disponível. Se este comportamento ocorrer, tente reconectar o console até que o site retorne um provedor de SMS disponível.  



##  <a name="BKMK_SMSProvNamespace"></a> Sobre o namespace do Provedor de SMS  

O esquema WMI do Configuration Manager define a estrutura do provedor de SMS. Namespaces do esquema descrevem a localização dos dados do Configuration Manager dentro do esquema Provedor de SMS. A tabela a seguir contém alguns dos namespaces comuns usados pelo Provedor de SMS:  

|espaço de nome|Descrição|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|O Provedor de SMS, que é muito utilizado pelo console do Configuration Manager, Gerenciador de Recursos, ferramentas do Configuration Manager e scripts.|  
|`Root\SMS\SMS_ProviderLocation`|A localização dos computadores do Provedor de SMS para um site.|  
|`Root\CIMv2`|O local de inventário para obter informações de namespace do WMI durante o inventário de hardware e software.|  
|`Root\CCM`|Dados do cliente e políticas de configuração do cliente do Configuration Manager.|  
|`Root\CIMv2\SMS`|A localização das classes de relatório de inventário coletadas pelo agente cliente de inventário. Os clientes compilam essas configurações durante a avaliação de política de computador. Essas configurações se baseiam na configuração de definições do cliente para o computador.|  



##  <a name="BKMK_WAIKforSMSProv"></a> Requisitos de implantação do sistema operacional

O computador no qual você instala uma instância do Provedor de SMS requer uma versão com suporte do Windows ADK.  

Para obter mais informações sobre esse requisito, confira [Requisitos de infraestrutura para implantação de sistema operacional](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10) e [Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).  

Ao gerenciar implantações do sistema operacional, o Windows ADK permite que o Provedor de SMS conclua diversas tarefas, inclusive:  

-   Exibir detalhes do arquivo WIM  

-   Adicionar arquivos de driver a imagens de inicialização existentes  

-   Criar arquivos ISO de inicialização  


A instalação do Windows ADK pode exigir até 650 MB de espaço livre em disco em cada computador que instalar o Provedor de SMS. A alta demanda de espaço em disco é necessária para que o Configuration Manager instale imagens de inicialização do Windows PE.  
