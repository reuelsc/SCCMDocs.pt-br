---
title: "Conceitos básicos do gerenciamento de dispositivos | System Center Configuration Manager"
description: Saiba como usar o System Center Configuration Manager para gerenciar dispositivos.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f4d39f31723711a7f5ec2b1aa39e81d3a3188029


---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Conceitos básicos do gerenciamento de dispositivos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager pode gerenciar duas categorias de dispositivos.

A primeira são os **clientes**, que são dispositivos, como estações de trabalho, laptops, servidores e dispositivos móveis que têm o software cliente do Configuration Manager instalado para que você possa gerenciá-los.   

A segunda são os **dispositivos gerenciados**, que podem incluir clientes, mas, normalmente, indicam os dispositivos móveis que não instalam o software cliente do Configuration Manager e que você gerencia usando o Microsoft Intune ou o gerenciamento de dispositivo móvel local interno do Configuration Manager.

Além de gerenciar dispositivos com ou sem o cliente do Configuration Manager, você pode usar o gerenciamento centrado no usuário para ajudar a agrupar e identificar dispositivos gerenciados.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Gerenciando dispositivos com o cliente do Configuration Manager

 O gerenciamento de clientes inclui operações como coleta de inventário de software ou hardware de dispositivos, instalação de novo software em um dispositivo ou definição de configurações que relatam ou impõem conformidade em uma configuração específica. Algumas funções de gerenciamento, como inventário de hardware, exigem que o dispositivo execute o software cliente do Configuration Manager. Outras operações, como instalação (implantação) de software em um dispositivo, são permitidas em todos os dispositivos gerenciados.  

 Para gerenciar um dispositivo usando o software cliente do Configuration Manager, você deve descobrir o dispositivo na sua rede e implantar (instalar) o software cliente nesse dispositivo ou instalar manualmente o software cliente em um novo computador e ingressar esse computador no seu site quando ele ingressar na sua rede. Para descobrir dispositivos que ainda não possuem o software cliente instalado, execute um ou mais dos métodos de detecção internos. Depois que um dispositivo for descoberto, será possível usar um dos vários métodos para instalar o software cliente. Para obter mais informações sobre o uso da descoberta, consulte [Executar descoberta para o System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Depois de descobrir dispositivos que têm suporte para executar o software cliente do Configuration Manager, você poderá usar um dos vários métodos para instalar o software. Depois que o software estiver instalado e o cliente for atribuído a um site primário, o dispositivo pode começar a ser gerenciado.  Os métodos comuns de instalação incluem instalação de cliente por push, instalação baseada em atualização de software, uso da Política de Grupo, instalação manual em um computador ou inclusão do cliente como parte da imagem de um sistema operacional que você implanta.  

 Depois que o cliente estiver instalado, é possível simplificar as tarefas de gerenciamento de dispositivos usando coleções. Coleções são grupos lógicos de dispositivos ou usuários que você cria para executar tarefas de gerenciamento em vários dispositivos que compartilham um conjunto comum de critérios. Por exemplo, é possível instalar um aplicativo para dispositivo móvel em todos os dispositivos móveis registrados pelo Configuration Manager. Se for esse o caso, será possível usar a coleção **Todos os Dispositivos Móveis** , que exclui computadores automaticamente. É possível criar suas próprias coleções para agrupar de forma lógica os dispositivos que você gerencia, de acordo com seus requisitos de negócios.  

 Para saber mais, confira os seguintes tópicos:  

-   [Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Métodos de instalação do cliente no System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Introdução às coleções no System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Configurações do cliente  
 Ao instalar o Configuration Manager pela primeira vez, todos os clientes da hierarquia são configurados usando as configurações de cliente padrão que você pode alterar. Essas configurações de cliente incluem opções como a frequência de comunicação dos dispositivos com o site, se o cliente está habilitado para atualizações de software e outras operações de gerenciamento, ou se os usuários podem registrar seus dispositivos móveis para serem gerenciados pelo Configuration Manager.  

 Se você precisar de configurações de cliente diferentes para grupos de usuários ou dispositivos, é possível criar configurações de cliente personalizadas e atribuí-las a coleções.  Os membros da coleção são configurados para ter as definições personalizadas, e você pode criar várias configurações de cliente personalizadas que são aplicadas na ordem especificada (por ordem numérica).  Se houver conflito entre elas, a configuração com o menor número substituirá as demais.  

 O diagrama a seguir mostra um exemplo de como você pode criar e aplicar configurações de cliente personalizadas.  

 ![Configurações do cliente](media/ClientSettings.gif)  

 Para saber mais sobre configurações de cliente, confira  
                [Como definir as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) e [Sobre as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Gerenciando dispositivos sem o cliente do Configuration Manager  
 O Configuration Manager dá suporte ao gerenciamento de alguns dispositivos que não instalaram o software cliente e que não são gerenciados pela interoperação com o Microsoft Intune. Para obter mais informações, consulte [Gerenciar dispositivos móveis com infraestrutura local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) e [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-centric-management"></a>Gerenciamento centrado no usuário  
 Além das coleções para dispositivos, há também coleções de usuários que contêm usuários de Serviços de Domínio Active Directory. Ao usar uma coleção do usuário, é possível instalar software em todos os computadores aos quais os membros da coleção se conectam e configurar a **afinidade de dispositivo de usuário** para que o software que você implanta seja instalado apenas nos dispositivos que são especificados como dispositivo principal dos usuários. Esses dispositivos principais são chamados de dispositivos primários. Um usuário pode ter um ou mais dispositivos primários.  

 Um das formas como os usuários podem controlar sua experiência de implantação de software é usando a interface de cliente de computador, o **Centro de Software**. O Centro de Software é instalado automaticamente em computadores cliente e acessada por meio do menu Iniciar dos usuários. O Centro de Software permite que os usuários gerenciem seu próprio software e que executem o seguinte:  

-   Instalar software  

-   Agendar a instalação automática do software fora do horário comercial  

-   Configurar quando o Configuration Manager pode instalar o software em seu dispositivo  

-   Configurar as definições de acesso para controle remoto se o controle remoto estiver habilitado no Configuration Manager  

-   Configurar opções de gerenciamento de energia se um usuário administrativo habilitá-lo  

 Um link no Centro de Software permite que os usuários se conectem ao **Catálogo de Aplicativos**, em que podem procurar, instalar e solicitar softwares. Além disso, o catálogo de aplicativos permite que os usuários configurem algumas definições de preferência, apaguem seus dispositivos móveis e (quando você permite essa configuração) especifiquem os próprios dispositivos primários para afinidade de dispositivo de usuário. (Outros métodos de configuração das informações de afinidade de dispositivo de usuário incluem importação das informações de um arquivo e geração automática de dados de uso).  

 Como o Catálogo de Aplicativos é um site hospedado no IIS, os usuários também podem acessar o Catálogo de Aplicativos diretamente de um navegador, da intranet ou da Internet.  



<!--HONumber=Nov16_HO1-->


