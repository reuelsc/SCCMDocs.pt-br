---
title: Atribuir clientes a um site
titleSuffix: Configuration Manager
description: Atribuir clientes a um site no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15467e83be28e884acb14309bdbb57768d7f19f0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-assign-clients-to-a-site-in-system-center-configuration-manager"></a>Como atribuir clientes a um site no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Após um cliente do System Center Configuration Manager ser instalado, ele deve ingressar em um site primário do Configuration Manager antes de você poder gerenciá-lo. O site ao qual o cliente se associa é conhecido como seu *site atribuído*. Clientes não podem ser atribuídos a um site de administração central ou a um site secundário.  

O processo de atribuição ocorre depois que o cliente foi instalado com sucesso e determina qual site gerencia o computador cliente. Você pode atribuir diretamente o cliente a um site ou pode usar a atribuição automática de site na qual o cliente encontra automaticamente um site apropriado com base em seu local de rede atual ou um em site de fallback configurado para a hierarquia.

Quando você instala o cliente do dispositivo móvel durante o registro do Configuration Manager, o dispositivo sempre é atribuído automaticamente a um site. Ao instalar o cliente em um computador, você pode escolher se deseja ou não atribuí-lo a um site. No entanto, quando o cliente está instalado, mas não atribuído, permanece sem gerenciamento até que a atribuição do site seja bem-sucedida.  
 

> [!NOTE]  
>  Sempre atribua clientes a sites que executam a mesma versão do Configuration Manager. Evite atribuir um cliente do Configuration Manager de uma versão mais recente a um site de uma versão mais antiga.   Se necessário, atualize o site primário para a mesma versão do Configuration Manager que você está usando para os clientes.  

Depois que o cliente é atribuído a um site, ele permanece atribuído a esse site, mesmo se mudar de endereço IP e ir para outro site. Somente um administrador pode atribuir o cliente a outro site ou remover a atribuição do cliente manualmente.  

> [!WARNING]  
>  Uma exceção a um cliente que permanece atribuído a um site é se você atribuir o cliente em um dispositivo Windows Embedded quando os filtros de gravação estão habilitados. Se você não desabilitar primeiro os filtros de gravação antes de atribuir o cliente, o status de atribuição de site do cliente voltará ao seu estado original quando o dispositivo for reiniciado da próxima vez.  
>   
>  Por exemplo, se o cliente estiver configurado para atribuição automática de site, ele será reatribuído na inicialização e poderá ser atribuído a um site diferente. Se o cliente não estiver configurado para atribuição automática de site, mas precisar de uma atribuição de site manual, reatribua manualmente o cliente após a inicialização para poder gerenciar esse cliente novamente usando o Configuration Manager.  
>   
>  Para evitar esse comportamento, desabilite os filtros de gravação antes de atribuir o cliente em dispositivos inseridos e depois habilite os filtros de gravação após ter verificado se a atribuição do site foi bem-sucedida.  

Se a atribuição do cliente falhar, o software cliente permanecerá instalado, mas não será gerenciado. Um cliente é considerado não gerenciado quando é instalado, mas não atribuído a um site, ou é atribuído a um site, mas não pode se comunicar com um ponto de gerenciamento.  

##  <a name="using-manual-site-assignment-for-computers"></a>Usando atribuição manual de site para computadores  
 Você pode atribuir manualmente os computadores cliente a um site usando os dois métodos a seguir:  

-   Use uma propriedade de instalação de cliente que especifica o código do site.  

-   No painel de controle, em **Configuration Manager**, especifique o código do site.  

> [!NOTE]  
>  Se você atribuir manualmente um computador cliente a um código do site do Configuration Manager que não existe, a atribuição do site falhará.   

##  <a name="BKMK_AutomaticAssignment"></a> Usando atribuição manual de site para computadores  
 A atribuição automática do site pode ocorrer durante a implementação do cliente, ou quando você clica em **Localizar Site** na guia **Avançado** nas **Propriedades do Configuration Manager** no Painel de Controle. O cliente do Configuration Manager compara seu próprio local de rede com os limites configurados na hierarquia do Configuration Manager. Quando o local de rede do cliente está dentro de um grupo de limites habilitado para atribuição de site, ou a hierarquia está configurada para um local de fallback, o cliente é automaticamente atribuído a esse site sem que você tenha que especificar um código de site.  

 Você pode configurar limites usando um ou mais destes procedimentos:  

-   Sub-rede IP  

-   Site do Active Directory  

-   Prefixo IP v6  

-   Intervalo de Endereços IP  

> [!NOTE]  
>  Se um cliente do Configuration Manager tiver vários adaptadores de rede e, portanto, tiver vários endereços IP, o endereço IP usado para uma atribuição de site de cliente de avaliação será atribuído aleatoriamente.  

 Para obter informações sobre como configurar grupos de limites para atribuição de site e como configurar um site de fallback para atribuição automática de site, consulte [Definir limites de site e grupos de limites para o System Center Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

 Clientes do Configuration Manager que usam a tentativa de atribuição automática de site para encontrar grupos de limites de sites publicados no Active Directory Domain Services. Se isso falhar (por exemplo, o esquema do Active Directory não for estendido para o Configuration Manager, ou os clientes forem computadores do grupo de trabalho), os clientes poderão obter informações do grupo de limites em um ponto de gerenciamento.  

 Você pode especificar um ponto de gerenciamento para os computadores cliente usarem quando são instalados, ou os clientes podem localizar um ponto de gerenciamento usando publicação DNS ou WINS.  

 Se o cliente não conseguir encontrar um site associado a um grupo de limites que contém seu local de rede, e a hierarquia não tiver um site de fallback, o cliente tentará novamente a cada 10 minutos até ter um site atribuído.  

 Os computadores cliente do Configuration Manager não poderão ser atribuídos automaticamente a um site se qualquer uma das condições a seguir se aplicar, devendo então ser atribuídos manualmente:  

-   Eles estão, no momento, atribuídos a um site.  

-   Eles estão na Internet ou configurados como clientes somente Internet.  

-   Seu local de rede não está em um dos grupos de limites configurados na hierarquia do Configuration Manager e não existe site de fallback para a hierarquia.  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>Concluindo a atribuição do site pela verificação da compatibilidade do site  
 Depois que um cliente encontra seu site atribuído, a versão e o sistema operacional do cliente são verificados para garantir que um site do Configuration Manager possa gerenciá-lo. Por exemplo, o Configuration Manager não pode gerenciar clientes do Configuration Manager 2007, clientes do System Center 2012 Configuration Manager ou clientes que executam o Windows 2000.  

 A atribuição do site falhará se você atribuir um cliente que executa o Windows 2000 a um site do Configuration Manager. Ao atribuir um cliente do Configuration Manager 2007 ou do System Center 2012 Configuration Manager a um site do Configuration Manager (branch atual), a atribuição de site deverá ser realizada com êxito para dar suporte à atualização de cliente automática. No entanto, até que os clientes de geração mais antiga sejam atualizados para um cliente do Configuration Manager (branch atual), o Configuration Manager não poderá gerenciar esse cliente usando configurações, aplicativos ou atualizações de software do cliente.  

> [!NOTE]  
>  Para dar suporte à atribuição de site de um cliente do Configuration Manager 2007 ou do System Center 2012 Configuration Manager a um site do Configuration Manager (branch atual), você precisará configurar a atualização automática do cliente para a hierarquia. Para obter mais informações, consulte [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

O Configuration Manager também verifica se você atribuiu o cliente do Configuration Manager (branch atual) a um site que dê suporte a ele. Os cenários a seguir podem ocorrer durante a migração de versões anteriores do Configuration Manager.  

-   Cenário: você usou a atribuição de site automática e os limites se sobrepõem com aqueles definidos em uma versão anterior do Configuration Manager.  

     Nesse caso, o cliente tenta automaticamente encontrar um site do Configuration Manager (branch atual).  

     O cliente verifica primeiro Active Directory Domain Services e, se encontrar um site publicado do Configuration Manager (branch atual), a atribuição de site será bem-sucedida. Se ela falhar, (por exemplo, o site do Configuration Manager não foi publicado ou o computador está em um cliente de grupo de trabalho), o cliente verificará as informações do site no seu ponto de gerenciamento atribuído.  

    > [!NOTE]  
    >  Você pode atribuir um ponto de gerenciamento ao cliente durante a instalação do cliente usando a propriedade **SMSMP=&lt;nome_do_servidor>** do Client.msi.  

     Se esses dois métodos falharem, a atribuição do site falhará e você deverá atribuir manualmente o cliente.  

-   Cenário: você atribuiu o cliente do Configuration Manager (branch atual) usando um código do site específico em vez da atribuição automática de site e, erroneamente, especificou um código do site para uma versão do Configuration Manager anterior ao System Center 2012 R2 Configuration Manager.  

     Nesse caso, a atribuição de site falha e você deve reatribuir manualmente o cliente a um site do Configuration Manager (branch atual).  

 A verificação de compatibilidade de site requer uma das seguintes condições:  

-   O cliente pode acessar informações do site publicadas nos Serviços de Domínio Active Directory.  

-   O cliente pode se comunicar com um ponto de gerenciamento no site.  

 Se a verificação de compatibilidade do site não for bem-sucedida, a atribuição do site falhará e o cliente permanecerá sem gerenciamento até que a verificação de compatibilidade do site seja executada novamente com êxito.  

 A exceção a realizar a verificação de compatibilidade do site ocorre quando um cliente é configurado para um ponto de gerenciamento baseado na Internet. Nesse cenário, nenhuma verificação de compatibilidade do site é realizada. Se você estiver atribuindo clientes a um site que contém sistemas baseados na Internet e especificar um ponto de gerenciamento baseado na Internet, verifique se está atribuindo o cliente ao site correto. Se você, por engano, atribuir o cliente a um site do Configuration Manager 2007, um site do System Center 2012 Configuration Manager ou um site do Configuration Manager que não tem funções de sistema de sites baseadas na Internet, o cliente não será gerenciado.  

##  <a name="locating-management-points"></a>Localizando pontos de gerenciamento  
 Depois que um cliente é atribuído com êxito a um site, ele localiza um ponto de gerenciamento no site.  

 Computadores cliente baixam uma lista de pontos de gerenciamento com os quais eles podem se conectar ao site. Isso acontece sempre que o cliente é reiniciado, a cada 25 horas ou quando cliente detecta uma mudança na rede como, por exemplo, quando o computador desconecta e reconecta na rede ou recebe um novo endereço IP. A lista inclui pontos de gerenciamento na intranet e se eles aceitam conexões de clientes em HTTP ou HTTPS. Quando o computador cliente está na Internet e o cliente ainda não tem uma lista de pontos de gerenciamento, ele se conecta ao ponto de gerenciamento especificado baseado na Internet para obter uma lista de pontos de gerenciamento. Quando o cliente tem uma lista de pontos de gerenciamento para seu site atribuído, ele seleciona um para se conectar:  

-   Quando o cliente está na intranet e tem um certificado PKI válido que pode usar, ele escolhe pontos de gerenciamento HTTPS em detrimento dos pontos de gerenciamento HTTP. Em seguida, ele localiza o ponto de gerenciamento mais próximo, com base em sua associação na floresta.  

-   Quando o cliente está na Internet, ele escolhe aleatoriamente um dos pontos de gerenciamento baseados na Internet.  

Clientes de dispositivos móveis registrados pelo Configuration Manager só se conectam a um ponto de gerenciamento em seu site atribuído e nunca se conectam a pontos de gerenciamento de sites secundários. Esses clientes sempre se conectam em HTTPS e o ponto de gerenciamento deve ser configurado para aceitar conexões de clientes pela Internet. Quando há mais de um ponto de gerenciamento para clientes de dispositivos móveis no site primário, o Configuration Manager escolhe aleatoriamente um desses pontos de gerenciamento durante a atribuição e o cliente do dispositivo móvel continua usando o mesmo ponto de gerenciamento.  

Quando o cliente baixa uma política de cliente de um ponto de gerenciamento no site, ele é, então, um cliente gerenciado.  

##  <a name="downloading-site-settings"></a>Baixando configurações do site  
 Depois de uma atribuição de site bem-sucedida e de o cliente ter encontrado um ponto de gerenciamento, um computador cliente que usa os Serviços de Domínio Active Directory para verificação de compatibilidade baixa as configurações de site relacionadas ao cliente para o seu site atribuído. Essas configurações incluem critérios de seleção de certificado do cliente, se uma lista de revogação de certificado deve ser usada e os números de porta da solicitação do cliente. O cliente continua a verificar essas configurações em uma base periódica.  

 Quando os computadores cliente não podem obter as configurações dos Serviços de Domínio Active Directory, eles as baixam do ponto de gerenciamento. Computadores cliente também podem obter as configurações do site quando são instalados por push, ou você pode especificá-las manualmente usando CCMSetup.exe e as propriedades de instalação do cliente. Para obter mais informações sobre as propriedades de instalação do cliente, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="downloading-client-settings"></a>Baixando as configurações do cliente  
 Todos os clientes baixam a política de configurações de cliente padrão e quaisquer outras políticas personalizadas aplicáveis. O Centro de Software conta com essas políticas de configuração do cliente para computadores Windows e notificará os usuários de que o Centro de Software não pode ser executado com sucesso até que essas informações de configuração sejam baixadas. Dependendo das configurações do cliente, o download inicial das configurações do cliente pode levar um tempo, e algumas tarefas de gerenciamento do cliente não podem ser executadas até que o processo seja concluído.  

##  <a name="verifying-site-assignment"></a>Verificando a atribuição de site  
 Você pode verificar se a atribuição de site foi bem-sucedida usando um dos seguintes métodos:  

-   Para clientes em computadores Windows, use o Configuration Manager no Painel de Controle e verifique se o código do site é exibido corretamente na guia **Site**.  

-   Para computadores cliente, no nó espaço de trabalho **Ativos e Conformidade** > **Dispositivos**, verifique se o computador exibe **Sim** para a coluna **Cliente** e o código do site primário correto para a coluna **Código do Site**.  

-   Para clientes de dispositivo móvel, no espaço de trabalho **Ativos e Conformidade** , use a coleção **Todos os Dispositivos Móveis** para verificar se dispositivo móvel exibe **Sim** para a coluna **Cliente** e o código do site primário correto para a coluna **Código do Site** .  

-   Use os relatórios de atribuição do cliente e o registro do dispositivo móvel.  

-   Para computadores cliente, use o arquivo LocationServices.log no cliente.  

##  <a name="roaming-to-other-sites"></a>Roaming para outros sites  
 Quando computadores cliente na intranet são atribuídos a um site primário, mas mudam de local da rede, de forma que fiquem em um grupo de limite configurado para outro site, eles foram movidos para outro site. Quando esse site é um site secundário de seu site atribuído, os clientes podem usar um ponto de gerenciamento no secundário para baixar a política do cliente e carregar dados do cliente, o que evita enviar esses dados por uma rede possivelmente lenta. Entretanto, se esses clientes se movem para limites para outro site primário ou um secundário que não seja um site filho do site atribuído, os clientes sempre usam um ponto de gerenciamento em seu site atribuído para baixar a política do cliente e carregar dados para seu site.  

 Esses computadores cliente que se movem para outros sites (todos os sites primários e todos os sites secundários) podem sempre usar pontos de gerenciamento em outros sites para solicitações de local de conteúdo. Pontos de gerenciamento no site atual podem proporcionar aos clientes uma lista de pontos de distribuição que possuem conteúdo que os clientes precisam.  

 Para computadores cliente configurados para gerenciamento de clientes somente da Internet e para dispositivos móveis e computadores Mac registrados pelo Configuration Manager, esses clientes se comunicam somente com pontos de gerenciamento em seu site atribuído. Esses clientes nunca se comunicam com pontos de gerenciamento em sites secundários ou com pontos de gerenciamento em outros sites primários.  
