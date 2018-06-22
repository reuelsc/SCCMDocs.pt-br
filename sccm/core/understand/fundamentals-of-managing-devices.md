---
title: Conceitos básico do gerenciamento de dispositivos
titleSuffix: Configuration Manager
description: Saiba como usar o System Center Configuration Manager para gerenciar dispositivos.
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d5fe709f403676c36d77e23e3ebe40a66101a44
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32340277"
---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Conceitos básicos do gerenciamento de dispositivos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager pode gerenciar duas categorias de dispositivos:

-   Os *clientes* são dispositivos como estações de trabalho, laptops, servidores e dispositivos móveis nos quais você instala o software cliente do Configuration Manager. Algumas funções de gerenciamento, como o inventário de hardware, exigem esse software cliente.  

-   Os *dispositivos gerenciados* podem incluir *clientes*, mas normalmente consistem em um dispositivo móvel no qual o software cliente do Configuration Manager não está instalado. Nesse tipo de dispositivo, é possível gerenciar usando o Intune ou o gerenciamento de dispositivo móvel local interno do Configuration Manager.

Você também pode agrupar e identificar os dispositivos com base no usuário e não apenas no tipo de cliente.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Gerenciando dispositivos com o cliente do Configuration Manager

Há duas formas de usar o software cliente do Configuration Manager para gerenciar um dispositivo. A primeira é descobrir o dispositivo na rede e, em seguida, implantar o software cliente nesse dispositivo. A outra é instalar manualmente o software cliente em um novo computador e, em seguida, adicionar esse computador ao seu site quando ele é adicionado à rede. Para descobrir dispositivos nos quais o software cliente ainda não foi instalado, execute um ou mais dos métodos de descoberta internos. Depois que um dispositivo for descoberto, use um dos vários métodos para instalar o software cliente. Para obter mais informações sobre o uso da descoberta, consulte [Executar descoberta para o System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Depois de descobrir os dispositivos com suporte para executar o software cliente do Configuration Manager, você poderá usar um dos vários métodos para instalar o software. Depois que o software estiver instalado e o cliente for atribuído a um site primário, o dispositivo pode começar a ser gerenciado.  Os métodos de instalação comuns incluem:

 - Instalação do cliente por push.

 - Instalação baseada em atualização de software.

 - Política de grupo.

 - Instalação manual em um computador.
 - Incluindo o cliente como parte de uma imagem do sistema operacional que você implanta.  


 Depois que o cliente estiver instalado, é possível simplificar as tarefas de gerenciamento de dispositivos usando coleções. As coleções são grupos de dispositivos ou usuários que você cria para poder gerenciá-los como um grupo. Por exemplo, é possível instalar um aplicativo para dispositivo móvel em todos os dispositivos móveis registrados pelo Configuration Manager. Se esse for o caso, você poderá usar a coleção Todos os Dispositivos Móveis.  

 Para obter mais informações, consulte esses tópicos:  

-   [Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Métodos de instalação do cliente no System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Introdução às coleções no System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Configurações do cliente  
 Ao instalar o Configuration Manager pela primeira vez, todos os clientes da hierarquia são configurados usando as configurações de cliente padrão que você pode alterar. Essas configurações de cliente incluem opções como:

 -  Com que frequência os dispositivos se comunicam com o site.

 -  Se o cliente está configurado para atualizações de software e outras operações de gerenciamento.

 -  Se os usuários podem registrar seus dispositivos móveis para serem gerenciados pelo Configuration Manager.  

Você pode criar configurações personalizadas de cliente e, em seguida, atribui-las às coleções.  Os membros da coleção são configurados para ter as configurações personalizadas e você pode criar várias configurações de cliente personalizadas que são aplicadas na ordem especificada (por ordem numérica).  Se houver conflito entre elas, a configuração com o menor número substituirá as demais.  

O diagrama a seguir mostra um exemplo de como criar e aplicar configurações de cliente personalizadas.  

 ![Configurações do cliente](media/ClientSettings.gif)  

 Para saber mais sobre configurações de cliente, confira  
                [Como definir as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) e [Sobre as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Gerenciando dispositivos sem o cliente do Configuration Manager  
 O Configuration Manager dá suporte ao gerenciamento de alguns dispositivos que não instalaram o software cliente e que não são gerenciados pelo Intune. Para obter mais informações, consulte [Gerenciar dispositivos móveis com a infraestrutura local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) e [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Gerenciamento baseado em usuário  
 O Configuration Manager dá suporte a coleções de usuários do Active Directory Domain Services. Ao usar uma coleção de usuários, é possível instalar o software em todos os computadores que os membros da coleção usam. Para ter certeza de que o software implantado é instalado somente nos dispositivos especificados como um dispositivo primário do usuário, configure a afinidade de dispositivo de usuário. Um usuário pode ter um ou mais dispositivos primários.  

 Um das maneiras como os usuários podem controlar a experiência de implantação de software é usar a interface do cliente do **Centro de Software**. O **Centro de Software** é instalado automaticamente em computadores cliente e executado por meio do menu **Iniciar**. O **Centro de Software** permite que os usuários gerenciem seu próprio software e executem as tarefas a seguir:  

-   Instalar software.  

-   Agendar a instalação automática do software fora do horário comercial.  

-   Configurar quando o Configuration Manager pode instalar o software em seu dispositivo.  

-   Configurar as definições de acesso para controle remoto se o controle remoto estiver habilitado no Configuration Manager.  

-   Configurar opções de gerenciamento de energia se algum administrador configurar essa opção.  


 Um link no **Centro de Software** permite que os usuários se conectem ao **Catálogo de Aplicativos**, no qual é possível procurar, instalar e solicitar softwares. O **Catálogo de Aplicativos** também é usado para configurar as definições de preferência, apagar dispositivos móveis e, quando configurado, especificar um dispositivo primário para afinidade de dispositivo de usuário.   

 Os usuários também podem acessar o **Catálogo de Aplicativos** por meio de uma sessão de Internet ou de intranet de navegador.  
