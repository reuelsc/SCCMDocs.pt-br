---
title: "Introdução ao gerenciamento de aplicativos | System Center Configuration Manager"
description: "Descubra as informações básicas de que você precisará para gerenciar e implantar aplicativos do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
caps.latest.revision: 18
author: robstackmsft
ms.author: robstack
manager: angrobe
experimental: true
experiment_id: rob-table-161101
translationtype: Human Translation
ms.sourcegitcommit: aa985dcb947803f7bc6d770f80a89a2fe6750681
ms.openlocfilehash: bec4d6d7008d5eabc7219dc7aaa1198c6e68a4df


---
# <a name="introduction-to-application-management-in-system-center-configuration-manager"></a>Introdução ao gerenciamento de aplicativos no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Neste tópico, você aprenderá as noções básicas que você precisa saber antes de começar a trabalhar com os aplicativos do System Center Configuration Manager.  

> [!TIP]  
>  Se você já está familiarizado com a maneira de gerenciar aplicativos no Configuration Manager, fique à vontade para ignorar este tópico e passar diretamente para a criação de um aplicativo de exemplo. Consulte [Criar e implantar um aplicativo com o System Center Configuration Manager](../../apps/get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>O que é um aplicativo?  
 Embora “aplicativo” seja um termo amplamente usado em computação, no Configuration Manager, isso significa algo diferente. Pense em um aplicativo como uma caixa. Essa caixa contém um ou mais conjuntos de arquivos de instalação para um pacote de software (conhecido como um **tipo de implantação**), além de instruções sobre como implantar o software.  

 Quando o aplicativo é implantado em dispositivos, os **requisitos** decidem qual tipo de implantação está instalada no dispositivo.  

 Claro, há muito mais coisas que você pode fazer com um aplicativo e você saberá mais sobre elas ao ler este guia. A lista a seguir apresenta alguns conceitos que você precisará saber antes de começar a se aprofundar. Você não precisará de todos eles em todos os aplicativos que criar:  



- **Requisitos** Nas versões anteriores do Configuration Manager, geralmente você criava uma coleção que continha os dispositivos nos quais desejava implantar um aplicativo. Embora você ainda possa fazer isso, os requisitos reduzem essa necessidade ao permitir que você especifique critérios muito mais granulares de acordo com os quais um aplicativo será instalado.<br> Por exemplo, você pode especificar que um aplicativo pode instalar somente em dispositivos que executam o Windows 10. Em seguida, você pode implantar o aplicativo em todos os seus dispositivos, mas ele será instalado somente em dispositivos que executam o Windows 10.<br> O cliente do Configuration Manager avalia os requisitos para determinar se um aplicativo e qualquer de seus tipos de implantação serão instalados. Em seguida, ele determina o tipo de implantação correto pelo qual instalar um aplicativo. A cada sete dias, por padrão, as regras de requisitos são reavaliadas para garantir a conformidade de acordo com a configuração do cliente **Agendar a reavaliação de implantações**.<br> Para obter detalhes, consulte [Create and deploy an application (Criar e implantar um aplicativo)](../../apps/get-started/create-and-deploy-an-application.md). 


- **Condições globais** Embora os requisitos sejam usados com um tipo de implantação específico em um único aplicativo, você também pode criar condições globais que são uma biblioteca de requisitos predefinidos que você pode usar com qualquer aplicativo e qualquer tipo de implantação.<br> O Configuration Manager contém um conjunto de condições globais internas e você também pode criar os seus próprios conjuntos.<br> Para obter detalhes, consulte [Create global conditions (Criar condições globais)](../../apps/deploy-use/create-global-conditions.md).


- A **Implantação simulada** avalia os requisitos, método de detecção e dependências de um aplicativo e relata os resultados sem realmente instalar o aplicativo.<br> Para obter detalhes, consulte [Simulate application deployments (Simular implantações de aplicativos)](../../apps/deploy-use/simulate-application-deployments.md). 


- **Ação de implantação** especifica se você deseja instalar ou desinstalar (quando há suporte) o aplicativo que você está implantando.<br> Para obter detalhes, consulte [Deploy applications (Implantar aplicativos)](../../apps/deploy-use/deploy-applications.md).  


- **Finalidade da implantação** especifica se o aplicativo de implantação será **Necessário** ou **Disponível**.<br>
**Necessário** significa que o aplicativo é implantado automaticamente de acordo com o agendamento configurado. No entanto, o usuário poderá acompanhar o status da implantação do aplicativo, se não estiver oculto, e instalar o aplicativo antes da data limite usando o Centro de Software.<br> **Disponível** significa que se o aplicativo for implantado em um usuário, o usuário verá o aplicativo publicado no Centro de Software e poderá instalá-lo sob demanda.<br> Para obter detalhes, consulte [Deploy applications (Implantar aplicativos)](../../apps/deploy-use/deploy-applications.md).


- **Revisões** Quando você faz revisões em um aplicativo ou em um tipo de implantação contido em um aplicativo, o Configuration Manager cria uma nova revisão do aplicativo. Você pode exibir o histórico de revisão de cada aplicativo, exibir suas propriedades, restaurar uma revisão anterior de um aplicativo ou excluir uma revisão antiga.<br> Para obter detalhes, consulte [Update and retire applications (Atualizar e desativar aplicativos)](../../apps/deploy-use/update-and-retire-applications.md).


- **Método de detecção** métodos de detecção são usados para descobrir se um aplicativo implantado já está instalado. Se o método de detecção indica que o aplicativo está instalado, o Configuration Manager não tenta instalá-lo novamente.<br> Para obter detalhes, consulte [Create applications (Criar aplicativos)](../../apps/deploy-use/create-applications.md). 


- **Dependências** As dependências definem um ou mais tipos de implantação de outro aplicativo que deve ser instalado antes da instalação de um tipo de implantação. Você pode configurar os tipos de implantação dependentes para instalar automaticamente antes que um tipo de implantação seja instalado.<br> Para obter detalhes, consulte [Create applications (Criar aplicativos)](../../apps/deploy-use/create-applications.md).  


- **Substituição** o Configuration Manager permite que você atualize ou substitua os aplicativos existentes usando uma relação de substituição. Ao substituir um aplicativo, é possível especificar um novo tipo de implantação para substituir o tipo de implantação do aplicativo substituído e também configurar para atualizar ou desinstalar o aplicativo substituído antes do aplicativo substituto ser instalado.<br> Para obter detalhes, consulte [Create applications (Criar aplicativos)](../../apps/deploy-use/create-applications.md).


- **Gerenciamento voltado ao usuário** Os aplicativos do Configuration Manager dão suporte ao gerenciamento voltado ao usuário, o que permite associar usuários específicos a dispositivos específicos. Em vez de ter de lembrar o nome do dispositivo de um usuário, você pode implantar aplicativos para o usuário e para o dispositivo. Essa funcionalidade pode ajudá-lo a garantir que os aplicativos mais importantes estejam sempre disponíveis em cada dispositivo acessado por um usuário específico. Se um usuário adquire um novo computador, você pode instalar automaticamente os aplicativos do usuário no dispositivo antes que ele faça logon.<br> Para obter detalhes, consulte [Vincular usuários e dispositivos com a afinidade de dispositivo de usuário](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

## <a name="what-application-types-can-you-deploy"></a>Quais tipos de aplicativos posso implantar?  
 O Configuration Manager permite que você implante os seguintes tipos de aplicativos:  

- Windows Installer (arquivo *.msi)
- Pacote do aplicativo do Windows (*.appx, \*.appxbundle)
- Pacote de aplicativo Windows (na Windows Store)
- Microsoft Application Virtualization 4
- Microsoft Application Virtualization 5
- Gabinete do Windows Mobile
- Mac OS X  


Além disso, quando você gerencia dispositivos por meio do gerenciamento de dispositivo local do Microsoft Intune ou do Configuration Manager, é possível gerenciar mais estes tipos de aplicativos:

- Pacote de aplicativos do Windows Phone (arquivo *.xap)
- Pacote de aplicativo para iOS (arquivo *.ipa)
- Pacote de aplicativo para Android (arquivo *.apk)
- Pacote do aplicativo para Android no Google Play
- Pacote de aplicativo do Windows Phone (na Windows Store)
- Windows Installer por meio do MDM
- Aplicativo da Web



## <a name="state-based-applications"></a>Aplicativos baseados em estado  
 Os aplicativos do Configuration Manager usam monitoramento baseado em estado, o que permite a você controlar o estado da última implantação de aplicativo para usuários e dispositivos. Essas mensagens de estado exibem informações sobre dispositivos individuais. Por exemplo, se um aplicativo for implantado em um conjunto de usuários, será possível exibir o estado de conformidade e a finalidade da implantação no console do Configuration Manager. É possível monitorar a implantação de todo o software usando o espaço de trabalho **Monitoramento** no console do Configuration Manager. Implantações de software incluem atualizações de software, configurações de conformidade, aplicativos, sequências de tarefas e pacotes e programas. Para obter mais informações, consulte [Monitor applications (Monitorar aplicativos)](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Implantações de aplicativos são regularmente reavaliadas pelo Configuration Manager. Por exemplo:  

-   Um aplicativo implantado será desinstalado pelo usuário final. No próximo ciclo de avaliação, o Configuration Manager detectará que o aplicativo não está presente e o reinstalará.  

-   Um aplicativo não foi instalado em um dispositivo porque ele não conseguiu atender aos requisitos. Mais adiante, uma alteração é feita ao dispositivo e agora ele atende aos requisitos. O Configuration Manager detecta esta alteração e o aplicativo é instalado.  

 Você pode configurar o intervalo de reavaliação de implantações de aplicativos usando a configuração do cliente **Agendar a reavaliação de implantações** . Para obter mais informações, consulte [Sobre as configurações do cliente](../../core/clients/deploy/about-client-settings.md).  

## <a name="get-started-creating-an-application"></a>Introdução à criação de um aplicativo  
 Se deseja começar imediatamente e iniciar a criação de um aplicativo, você encontrará um passo a passo para criar um aplicativo simples no tópico [Create and deploy an application (Criar e implantar um aplicativo)](../../apps/get-started/create-and-deploy-an-application.md).  

 Se você está familiarizado com as noções básicas e deseja obter mais informações de referência sobre todas as opções disponíveis, comece por [Create applications (Criar aplicativos)](/sccm/apps/deploy-use/create-applications).  

## <a name="software-center-and-the-application-catalog"></a>Centro de Software e o Catálogo de Aplicativos  
 Nas versões anteriores do Configuration Manager, o Centro de Software foi usado para instalar e agendar instalações de software, definir configurações de controle remoto e definir configurações de gerenciamento de energia. Os usuários podem se conectar ao Catálogo de Aplicativos para procurar e solicitar software, definir algumas configurações de preferência e apagar remotamente seus dispositivos móveis.  

 Embora essas configurações ainda estejam disponíveis no System Center Configuration Manager, agora há uma nova versão do Centro de Software disponível que permite procurar aplicativos sem a necessidade de usar o Catálogo de Aplicativos, que requer um navegador da Web habilitado para Silverlight. No entanto, as funções do sistema de sites do ponto de sites da Web e do ponto de serviço Web do catálogo de aplicativos ainda são necessárias para que os aplicativos disponíveis para o usuário sejam exibidos no Centro de Software.  

 Para obter mais informações, consulte [Plan for and configure application management (Planejar e configurar o gerenciamento de aplicativos)](../../apps/plan-design/plan-for-and-configure-application-management.md).  

## <a name="using-configuration-manager-packages-and-programs"></a>Usando pacotes e programas no Configuration Manager  
 O Configuration Manager continua dando suporte a pacotes e programas usados nas versões anteriores do produto. Uma implantação que usa pacotes e programas pode ser mais adequada do que uma implantação que usa um aplicativo quando você implanta um dos seguintes:  

-   Scripts que não instalam um aplicativo em um computador, como um script para desfragmentar a unidade de disco do computador  

-   Scripts “únicos” que não precisam ser monitorados continuamente  

-   Scripts que são executados em um agendamento recorrente e que não usam a avaliação global  

 Para obter mais informações, consulte [Pacotes e programas](../../apps/deploy-use/packages-and-programs.md).  




<!--HONumber=Dec16_HO3-->


