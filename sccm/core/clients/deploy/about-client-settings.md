---
title: "Configurações do cliente"
titleSuffix: Configuration Manager
description: "Escolha as configurações do cliente usando o console de administração no System Center Configuration Manager."
ms.custom: na
ms.date: 01/05/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: "15"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 230d608c9ebc8126d7d8e18f7211875a2155bb7b
ms.sourcegitcommit: ac9268e31440ffe91b133c2ba8405d885248d404
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Sobre as configurações do cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Gerencie todas as configurações de cliente no console do Configuration Manager por meio do nó **Configurações de Cliente** no espaço de trabalho **Administração**. O Configuration Manager é fornecido com um conjunto de configurações padrão. Quando você altera as configurações padrão do cliente, essas configurações são aplicadas a todos os clientes na hierarquia. Também defina configurações de cliente personalizadas, que substituem as configurações de cliente padrão ao atribuí-las a coleções. Para obter mais informações, consulte [Como definir as configurações de cliente](../../../core/clients/deploy/configure-client-settings.md).  
 

## <a name="background-intelligent-transfer-service"></a>Serviço de Transferência Inteligente em Segundo Plano  

-   **Limitar a largura de banda de rede máxima para transferências em segundo plano do BITS**   </br>
   Quando essa opção é **Sim**, os clientes usam a limitação da largura de banda do BITS. Para definir as outras configurações nesse grupo, é necessário habilitar essa configuração. 

-   **Hora de início do período de limitação**   </br>
   Especifique a hora de início local para o período de limitação do BITS.  

-   **Hora de término do período de limitação**   </br>
   Especifique a hora de início final para o período de limitação do BITS. Se for o mesmo que a **Hora de início do período de limitação**, a limitação do BITS sempre estará habilitada.  

-   **Taxa de transferência máxima durante o período de limitação (Kbps)** </br>
    Especifica a taxa de transferência máxima que pode ser usada pelos clientes durante a janela.  

-   **Permitir downloads de BITS fora do período de limitação**   </br>
   Permita que os clientes usem configurações de BITS separadas fora da janela especificada.  

-   **Taxa de transferência máxima fora do período de limitação (Kbps)**   </br>
   Especifique a taxa de transferência máxima usada pelos clientes fora da janela de limitação do BITS.  



## <a name="client-cache-settings"></a>Configurações de cache do cliente

- **Configurar o BranchCache** </br>
  Use essa configuração para configurar o computador cliente para o [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Para permitir o armazenamento em cache do BranchCache no cliente, defina **Habilitar o BranchCache** como **Sim**.

    - **Habilitar o BranchCache** </br>
    Habilite o BranchCache nos computadores cliente.

    - **Tamanho máximo do cache do BranchCache (percentual do disco)** </br>
    O percentual do disco que é permitido que o BranchCache use. 

- **Configurar o tamanho do cache do cliente** </br>
  O cache do cliente do Configuration Manager em computadores Windows armazena arquivos temporários usados para instalar aplicativos e programas. Se for definido como **Não**, o tamanho padrão será 5.120 MB.</br>
    Escolha **Sim** e, em seguida, especifique:
    - **Tamanho máximo de cache (MB)**
    - **Tamanho máximo do cache (percentual do disco)** </br>
    O tamanho do cache do cliente expande até o tamanho máximo em MB (megabytes) ou o percentual do disco, *o que for menor*. 

- **Habilitar cliente do Configuration Manager em um SO completo para compartilhar conteúdo** </br>
    Habilite o [cache par](/sccm/core/plan-design/hierarchy/client-peer-cache) para clientes do Configuration Manager. Escolha **Sim** e, em seguida, especifique as informações da porta pela qual o cliente se comunica com o computador par. 
    - **Porta para difusão de rede inicial** (padrão 8004)
    - **Porta para download de conteúdo do par** (padrão 8003) </br>
    O Configuration Manager configura automaticamente as regras do Firewall do Windows para permitir esse tráfego. Se você usar um firewall diferente, deverá configurar manualmente as regras para permitir esse tráfego.




## <a name="client-policy"></a>Política do cliente  

-   **Intervalo de sondagem da política do cliente (minutos)**  </br>
     Especifica a frequência com que os seguintes clientes do Configuration Manager baixam a política do cliente:  
      -   Computadores Windows (por exemplo, desktops, servidores, laptops)  
      -   Dispositivos móveis registrados pelo Configuration Manager  
      -   Computadores Mac  
      -   Computadores que executam o Linux ou UNIX  

-   **Habilitar política de usuário em clientes**   </br>
   Quando você define essa opção como **Sim** e usa a [descoberta de usuário](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), os clientes recebem aplicativos e programas direcionados ao usuário conectado.  

    O Catálogo de Aplicativos recebe a lista de softwares disponíveis para usuários do servidor do site. Assim, essa configuração não precisa ser **Sim** para que os usuários vejam e solicitem aplicativos do Catálogo de Aplicativos. Se essa configuração for **Não**, os seguintes comportamentos não funcionarão quando os usuários usarem o Catálogo de Aplicativos:  

      -   Os usuários não podem instalar os aplicativos que veem no Catálogo de Aplicativos.  

      -   Os usuários não veem as notificações sobre suas solicitações de aprovação de aplicativo. Em vez disso, eles devem atualizar o catálogo de aplicativos e verificar o status de aprovação.  

      -   Os usuários não recebem as revisões e atualizações para aplicativos publicadas no Catálogo de Aplicativos. O usuários veem as alterações nas informações do aplicativo no Catálogo de Aplicativos.  

      -   Se você remover uma implantação de aplicativo depois que o cliente instalar o aplicativo por meio do Catálogo de Aplicativos, os clientes continuarão verificando se o aplicativo está instalado por até dois dias.  

    Além disso, quando essa configuração for **Não**, os usuários não receberão os aplicativos obrigatórios implantados em usuários. Os usuários também não recebem outras tarefas de gerenciamento em políticas de usuário.  

    Essa configuração se aplica aos usuários quando o computador está na intranet e Internet. Ela deverá ser **Sim** se você desejar habilitar políticas de usuário pela Internet.  

-   **Ativar solicitações de política de usuário de clientes da Internet**   </br>
   Defina essa configuração como **Sim** para que os usuários recebam a política de usuário em computadores baseados na Internet. Os seguintes requisitos também devem se aplicar:  

      -   O cliente e o site são configurados para o gerenciamento de clientes baseado na Internet

      -   A configuração **Habilitar política de usuário em clientes** é **Sim**  

      -   O ponto de gerenciamento baseado na Internet autentica com êxito o usuário usando a autenticação do Windows (Kerberos ou NTLM)  

       Se você definir essa opção como **Não** ou se um dos requisitos anteriores não forem atendidos, um computador na Internet receberá somente as políticas do computador. Nesse cenário, os usuários ainda podem ver, solicitar e instalar aplicativos de um catálogo de aplicativos baseados na Internet. Se essa configuração for **Não**, mas **Habilitar política de usuário em clientes** for **Sim**, os usuários não receberão as políticas de usuário até que o computador esteja conectado à intranet.  

       Para obter mais informações sobre como gerenciar clientes na Internet, consulte [Considerações sobre a comunicação do cliente pela Internet ou por uma floresta não confiável](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

      > [!NOTE]  
      >  As solicitações de aprovação de aplicativo dos usuários não exigem autenticação de usuário nem políticas de usuário.  


## <a name="cloud-services"></a>Cloud Services

-   **Permitir acesso ao ponto de distribuição na nuvem** </br>
    Defina essa configuração como **Sim** para que os clientes obtenham o conteúdo de um ponto de distribuição na nuvem. Essa configuração não exige que o dispositivo seja baseado na Internet.

-    **Registrar automaticamente novos dispositivos ingressados em domínio do Windows 10 com o Azure Active Directory** </br> Quando você configura o Azure Active Directory para dar suporte à junção híbrida, o Configuration Manager configura dispositivos Windows 10 para essa funcionalidade. Para obter mais informações, consulte [Como configurar dispositivos híbridos ingressados no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

-   **Habilitar clientes a usarem um gateway de gerenciamento de nuvem** </br>
    Por padrão, todos os clientes de roaming na Internet usam qualquer [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) disponível. Um exemplo de quando definir essa configuração como **Não** é para definir o escopo do uso do serviço, como durante um projeto piloto ou para economizar custos.



##  <a name="compliance-settings"></a>Configurações de conformidade  

-   **Habilitar a avaliação de conformidade nos clientes** </br>
    Defina essa configuração como **Sim** para definir as outras configurações nesse grupo.
 
-   **Agendar a avaliação da conformidade**   </br>
     Clique em **Agendamento** para criar o agendamento padrão para as implantações de linha de base de configuração. Esse valor é configurável para cada linha de base na caixa de diálogo **Implantar Linha de Base de Configuração**.  

-   **Habilitar perfis e dados do usuário**   </br>
     Escolha **Sim** se deseja implantar itens de configuração de [perfis e dados de usuário](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md).



## <a name="computer-agent"></a>Agente de Computador  
-   Notificações do usuário para implantações necessárias </br>
    Para obter mais informações sobre as três seguintes configurações, consulte [Notificações do usuário para implantações obrigatórias](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments):
    -   **Data limite de implantação superior a 24 horas, lembrar o usuário a cada (horas)**
    -   **Data limite de implantação inferior a 24 horas, lembrar o usuário a cada (horas)**  </br>
    -   **Data limite de implantação inferior a 1 hora, lembrar o usuário a cada (minutos)**  </br>

-   **Ponto de sites da Web do Catálogo de Aplicativos padrão**   </br>
     O Configuration Manager usa essa configuração para conectar usuários ao Catálogo de Aplicativos do Centro de Software. Clique em **Definir Site** para especificar um servidor que hospeda o ponto de sites da Web do Catálogo de Aplicativos. Insira seu nome NetBIOS ou FQDN, especifique a detecção automática ou uma URL para implantações personalizadas. Na maioria dos casos, a detecção automática é a melhor opção porque oferece os seguintes benefícios:  

    -   Se o site tiver um ponto de sites da Web do Catálogo de Aplicativos, os clientes receberão automaticamente um ponto de sites da Web do Catálogo de Aplicativos em seus sites.  

    -   O cliente prefere pontos de sites da Web do Catálogo de Aplicativos habilitados para HTTPS na intranet em servidores somente HTTP. Essa funcionalidade ajuda a proteger contra um servidor não autorizado.

    -   O ponto de gerenciamento fornece um ponto de sites da Web do Catálogo de Aplicativos baseado na Internet a clientes baseados na Internet. O ponto de gerenciamento fornece um ponto de sites da Web do Catálogo de Aplicativos baseado na intranet a clientes baseados na intranet.  

     A detecção automática não garante que os clientes receberão o ponto de sites da Web do Catálogo de Aplicativos mais próximo. Você pode decidir por não usar a **Detecção automática** pelos seguintes motivos:  

     -   Você deseja configurar manualmente o servidor mais próximo para clientes ou garantir que eles não se conectem a um servidor em uma conexão de rede lenta.  

     -   Você deseja controlar quais clientes se conectam a qual servidor. Essa configuração pode ser por motivos comerciais, de desempenho ou teste.  

     -   Você não quer esperar até 25 horas ou uma alteração de rede para que os clientes usem outro ponto de sites da Web do Catálogo de Aplicativos.  

     Se você especificar o ponto de sites da Web do catálogo de aplicativos em vez de usa a detecção automática, especifique o nome NetBIOS em vez do FQDN da intranet. Essa configuração reduz a probabilidade de que o navegador da Web solicite aos usuários as credenciais quando ele acessar um Catálogo de Aplicativos baseado na intranet. Para usar o nome NetBIOS, as seguintes condições devem ser aplicáveis:  

     -   O nome NetBIOS é especificado nas propriedades do ponto de sites da Web do catálogo de aplicativos.  

     -   Você usa o WINS ou todos os clientes estão no mesmo domínio do ponto de sites da Web do catálogo de aplicativos.  

     -   Configure o ponto de sites da Web do Catálogo de Aplicativos para conexões do cliente HTTP ou configure o servidor para HTTPS e o certificado do servidor Web contém o nome NetBIOS.  

     Geralmente, os usuários apresentam credenciais quando a URL contém um FQDN, mas não quando a URL é um nome NetBIOS. Espere que os usuários sempre sejam solicitados quando eles se conectam à Internet, pois essa conexão deve usar o FQDN de Internet. Ao usar um cliente baseado na Internet e o navegador da Web solicita aos usuários as credenciais, verifique se o ponto de Sites da Web do Catálogo de Aplicativos pode se conectar a um controlador de domínio para a conta do usuário. Essa configuração permite que o usuário seja autenticado usando o Kerberos.  

    > [!NOTE]  
    >  Como funciona a detecção automática:  
    >   
    >  O cliente faz uma solicitação de local de serviço para um ponto de gerenciamento. Se houver um ponto de sites da Web do catálogo de aplicativos no mesmo site do cliente, o servidor é fornecido ao cliente como o servidor do catálogo de aplicativos a ser usado. Quando mais de um ponto de sites da Web do catálogo de aplicativos está disponível no site, um servidor habilitado para HTTPS tem prioridade sobre um servidor não habilitado para HTTPS. Depois dessa filtragem, todos os clientes recebem um dos servidores para usar como o Catálogo de Aplicativos. O Configuration Manager não faz o balanceamento de carga entre vários servidores. Quando o site do cliente não contém um ponto de sites da Web do catálogo de aplicativos, o ponto de gerenciamento retorna de forma não determinística um ponto de sites da Web do catálogo de aplicativos da hierarquia.  
    >   
    >  Para clientes baseados na intranet, se você configurar o ponto de sites da Web do Catálogo de Aplicativos com um nome NetBIOS para a URL do Catálogo de Aplicativos, o ponto de gerenciamento dará aos clientes esse nome NetBIOS em vez do FQDN da intranet. Para clientes baseados na Internet, o ponto de gerenciamento só fornece o FQDN da Internet ao cliente.  
    >   
    >  O cliente faz a solicitação de local de serviço a cada 25 horas ou sempre que detecta uma alteração de rede. Por exemplo, se o cliente sair da intranet e acessar a Internet e localizar um ponto de gerenciamento baseado na Internet, o ponto de gerenciamento baseado na Internet fornecerá servidores do ponto de sites da Web do Catálogo de Aplicativos baseados na Internet para os clientes.  

-   **Adicionar sites da Web do Catálogo de Aplicativos padrão à zona de sites confiáveis do Internet Explorer**   </br>
     Se essa opção for **Sim**, o cliente adicionará automaticamente a URL padrão atual do site do Catálogo de Aplicativos à zona de sites confiáveis do Internet Explorer.  

     Essa definição garante que a configuração do Internet Explorer para Modo Protegido não está habilitada. Se o Modo Protegido estiver habilitado, o cliente do Configuration Manager poderá não conseguir instalar aplicativos do Catálogo de Aplicativos. Por padrão, a zona de sites confiáveis oferece suporte ao logon de usuário para o catálogo de aplicativos, o que requer autenticação do Windows.  

     Se você deixar essa opção como **Não**, o cliente do Configuration Manager poderá não conseguir instalar aplicativos por meio do Catálogo de Aplicativos. Um método alternativo é definir essas configurações do Internet Explorer em outra zona para a URL do Catálogo de Aplicativos usada pelos clientes.  

    > [!NOTE]  
    >  Sempre que o Configuration Manager adiciona um Catálogo de Aplicativos padrão à zona de sites confiáveis, ele remove as URLs do Catálogo de Aplicativos adicionadas anteriormente.  
    >   
    >  Se a URL já estiver especificada em uma das zonas de segurança, o Configuration Manager não poderá adicionar a URL. Nesse cenário, você deve remover a URL da outra zona ou definir manualmente as configurações necessárias do Internet Explorer.  

-   **Permitir que os aplicativos Silverlight sejam executados no modo de confiança elevada**   </br>
     Essa configuração deve ser **Sim** para que os usuários usem o Catálogo de Aplicativos.  

     Se você alterar essa configuração, ela terá efeito quando o usuário carregar o navegador da próxima vez ou atualizar a janela do navegador aberta no momento.  

     Para obter mais informações sobre essa configuração, consulte [Certificados para o Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicativos](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

-   **Nome da organização exibido no Centro de Software**   </br>
     Digite o nome que os usuários veem no Centro de Software. Essa informação de identidade visual ajuda os usuários a identificarem este aplicativo como uma fonte confiável.  

-   **Usar o novo Centro de Software**   </br>
     Se você definir essa configuração de cliente como **Sim**, todos os computadores cliente usarão o novo Centro de Software. O Centro de Software mostra os aplicativos disponíveis para o usuário que estavam acessíveis anteriormente apenas no Catálogo de Aplicativos. O Catálogo de Aplicativos exige o Silverlight, que não é um pré-requisito para o novo Centro de Software.   

     As funções do sistema de sites do ponto de sites da Web do catálogo de aplicativos e do ponto de serviços Web do catálogo de aplicativos ainda são necessárias para que os aplicativos disponíveis para o usuário sejam exibidos no Centro de Software.  

     Para obter mais informações, consulte [Plan for and configure application management (Planejar e configurar o gerenciamento de aplicativos)](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Habilitar comunicação com o Serviço de Atestado de Integridade**  </br>
    Defina essa configuração como **Sim** para que os dispositivos Windows 10 usem o [Atestado de integridade](/sccm/core/servers/manage/health-attestation). Quando você habilitar essa configuração, a configuração a seguir também estará disponível para configuração.

    -   **Usar o Serviço de Atestado de Integridade local** </br>
        Defina essa configuração como **Sim** para que os dispositivos usem um serviço local. Defina essa configuração como **Não** para que os dispositivos usem o serviço baseado em nuvem da Microsoft.  

-   **Permissões de instalação**   </br>
    > [!WARNING]  
    >  Essa configuração aplica-se o Centro de Software e ao Catálogo de Aplicativos. Essa configuração não tem nenhum efeito quando os usuários usam o Portal da Empresa.  

     Configure como os usuários podem iniciar a instalação de software, as atualizações de software e as sequências de tarefas:  

    -   **Todos os Usuários**: os usuários com qualquer permissão, exceto Convidado  

    -   **Somente Administradores**: os usuários devem ser membros do grupo local de Administradores  

    -   **Somente Administradores e usuários primários**: os usuários devem ser membros do grupo local de Administradores ou um usuário primário no computador  

    -   **Nenhum Usuário**: nenhum usuário conectado a um computador cliente pode iniciar a instalação de software, as atualizações de software e as sequências de tarefas. Implantações obrigatórias para o computador são sempre instaladas na data limite. Os usuários não podem iniciar a instalação do software usando o Catálogo de Aplicativos ou o Centro de Software.  

-   **Suspender a entrada de PIN do BitLocker na reinicialização**  </br>
     Se os computadores exigirem a entrada de PIN do BitLocker, essa opção ignorará o requisito de inserção de um PIN quando o computador for reiniciado após uma instalação de software.  

    -   **Sempre**: o Configuration Manager suspende temporariamente o BitLocker após a instalação do software que exige uma reinicialização e a iniciou. Essa configuração se aplica somente a uma reinicialização do computador iniciada pelo Configuration Manager. Essa configuração não suspende o requisito de inserção de PIN do BitLocker quando o usuário reinicia o computador. O requisito de entrada de PIN do BitLocker é retomado após a inicialização do Windows.

    -   **Nunca**: o Configuration Manager não suspende o BitLocker na próxima inicialização do computador, após ter instalado o software que exige a reinicialização. Nesse cenário, a instalação do software não pode terminar até que o usuário insira o PIN para concluir o processo de inicialização padrão e carregar o Windows.

-   **O software adicional gerencia a implantação de aplicativos e as atualizações de software**  </br>
     Habilite essa opção somente se uma das seguintes condições forem aplicáveis:  

    -   Você usa uma solução de fornecedor que requer que essa configuração seja habilitada.  

    -   Você usa o SDK (Software Development Kit) do Configuration Manager para gerenciar notificações do agente cliente e a instalação de atualizações de aplicativos e software.  

    > [!WARNING]  
    >  Se você escolher essa opção quando nenhuma dessas condições for aplicável, o cliente não instalará as atualizações de software e os aplicativos obrigatórios. Essa configuração não impede que os usuários instalem aplicativos por meio do Catálogo de Aplicativos nem a instalação de pacotes, programas e sequências de tarefas.  

-   **Política de execução do PowerShell**  </br>
     Configurar como os clientes do Configuration Manager podem executar scripts do Windows PowerShell. Esses scripts são muitas vezes usados para detecção e configuração de itens em configurações de conformidade. Eles também podem ser enviados em uma implantação como um script padrão.  

    -   **Ignorar**: o cliente do Configuration Manager ignora a configuração do Windows PowerShell no computador cliente para que os scripts não assinados possam ser executados.  

    -   **Restrito**: o cliente do Configuration Manager usa a configuração atual do Windows PowerShell no computador cliente. Essa configuração determina se é possível executar scripts não assinados.  

    -   **Tudo Assinado**: o cliente do Configuration Manager executará scripts apenas se forem assinados por um fornecedor confiável. Essa restrição aplica-se, independentemente da configuração atual do Windows PowerShell no computador cliente.  

     Essa opção exige no mínimo a versão do Windows PowerShell 2.0. O padrão é todos **Tudo Assinado**.  

    > [!TIP]  
    >  Se os scripts não assinados não forem executados devido a essa configuração do cliente, o Configuration Manager relatará esse erro das seguintes maneiras:  
    >   
    > -   O espaço de trabalho **Monitoramento** no console exibe a ID de erro de status de implantação **0x87D00327** e a descrição **O script não está assinado**  
    > -   Os relatórios exibem o tipo de erro **Erro de Descoberta** e, em seguida, o código de erro **0x87D00327** e a descrição **O script não está assinado** ou o código de erro **0x87D00320** e a descrição **O host de script ainda não foi instalado**. Um relatório de exemplo é **Detalhes de erros de itens de configuração em uma linha de base de configuração para um ativo**.  
    > -   O arquivo **DcmWmiProvider.log** exibe a mensagem **O script não está assinado (erro: 87D00327; fonte: CCM)**.  

-   **Mostrar notificações para novas implantações**  </br>
     Escolha **Sim** para exibir uma notificação para implantações disponíveis em menos de uma semana.  Essa mensagem é exibida sempre que o agente cliente é iniciado.

-   **Desabilitar data limite aleatória**  </br>
     Após a data limite da implantação, essa configuração determina se o cliente usa um atraso de ativação de até duas horas para instalar as atualizações de software obrigatórias. Por padrão, o atraso de ativação está desabilitado.  

     Para cenários de VDI (Virtual Desktop Infrastructure), esse atraso ajuda a distribuir o processamento da CPU e a transferência de dados para um computador host com várias máquinas virtuais. Mesmo que você não use VDI, se muitos clientes instalarem as mesmas atualizações ao mesmo tempo, isso poderá aumentar negativamente o uso da CPU no servidor do site. Esse comportamento também pode causar lentidão nos pontos de distribuição e reduzir significativamente a largura de banda de rede disponível.  

     Se os clientes precisarem instalar as atualizações de software obrigatórias até a data limite de implantação sem atraso, defina essa configuração como **Sim**. 

-   **Período de carência para a imposição após a data limite da implantação (horas)** </br>
     Caso deseje oferecer aos usuários mais tempo para instalar as implantações de atualização de software ou os aplicativos obrigatórios além da data limite, defina essa configuração como **Sim**. Esse período de carência destina-se a um computador desativado por um período estendido e o usuário precisa instalar vários aplicativos ou implantações de atualização. Por exemplo, se um usuário retorna de férias e precisa esperar muito tempo enquanto o cliente instala as implantações de aplicativo vencidas. 

     Defina um período de carência entre 1 e 120 horas. Use essa configuração em conjunto com a propriedade de implantação **Atrasar a imposição dessa implantação de acordo com as preferências do usuário**. Para obter informações, confira [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implantar aplicativos).



##  <a name="computer-restart"></a>Reinicialização do computador  
 As configurações a seguir devem ter uma duração mais curta do que a menor janela de manutenção aplicada ao computador.  

 Para obter mais informações sobre as janelas de manutenção, consulte [Como usar janelas de manutenção no System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

-   **Exibir uma notificação temporária para o usuário que indica o intervalo antes que o usuário seja desconectado ou o computador seja reiniciado (minutos)**
-   **Exibir uma caixa de diálogo que o usuário não pode fechar, que exibe o intervalo de contagem regressiva antes que o usuário seja desconectado ou o computador seja reiniciado (minutos)**



##  <a name="endpoint-protection"></a>Endpoint Protection  
>  [!Tip]   
> Além das informações a seguir, você pode encontrar detalhes adicionais de como usar as configurações do cliente do Endpoint Protection no [Cenário de exemplo: usar o System Center Endpoint Protection para proteger os computadores contra malware no System Center Configuration Manager](/sccm/protect/deploy-use/scenarios-endpoint-protection).

-   **Gerenciar o cliente Endpoint Protection em computadores cliente**  </br>
     Escolha **Sim** se deseja gerenciar clientes existentes do Endpoint Protection e do Windows Defender em computadores da hierarquia.  

     Escolha esta opção se você já tiver instalado o cliente Endpoint Protection e desejar gerenciá-lo com o Configuration Manager.  Essa instalação separada inclui um processo com script usando um aplicativo do Configuration Manager ou um pacote e programa.

-   **Instalar o cliente do Endpoint Protection em computadores cliente**   </br>
     Escolha **Sim** para instalar e habilitar o cliente Endpoint Protection em computadores cliente que ainda não executam o cliente.  

    > [!NOTE]  
    >  Se o cliente do Endpoint Protection já estiver instalado, escolher **Não** não o desinstalará. Para desinstalar o cliente do Endpoint Protection, defina a configuração do cliente **Gerenciar cliente do Endpoint Protection em computadores cliente** como **Não**. Em seguida, implante um pacote e programa para desinstalar o cliente do Endpoint Protection.  

-   **Remover automaticamente software antimalware já instalado antes que o Endpoint Protection seja instalado** </br>
    Defina essa configuração como **Sim** para que o cliente do Endpoint Protection tente desinstalar outros aplicativos antimalware. Vários clientes de antimalware no mesmo dispositivo podem entrar em conflito e afetar o desempenho do sistema.

-   **Permitir a instalação do cliente do Endpoint Protection e reiniciar fora das janelas de manutenção. As janelas de manutenção devem ter, pelo menos, 30 minutos para a instalação do cliente** </br>
    Defina essa configuração como **Sim** para substituir os comportamentos de instalação típicos por janelas de manutenção. A configuração atende aos requisitos de negócios para a prioridade de manutenção do sistema para fins de segurança. 

-   **Para dispositivos Windows Embedded com filtros de gravação, confirme a instalação do cliente do Endpoint Protection (exige reinicialização)**  </br>
     Escolha **Sim** para desabilitar o filtro de gravação no dispositivo Windows Embedded e reiniciar o dispositivo. Essa ação confirma a instalação no dispositivo.  

     Se você definir essa configuração como **Não**, o cliente será instalado em uma sobreposição temporária que é limpa quando o dispositivo é reiniciado. Neste cenário, o cliente do Endpoint Protection não é instalado por completo até que outra instalação confirme as alterações no dispositivo. Essa configuração é o padrão.  

-   **Suprimir qualquer reinicialização necessária do computador após o Endpoint Protection ser instalado**  </br>
     Escolha **Sim** para suprimir a reinicialização do computador, se necessário, após a instalação do cliente do Endpoint Protection.  

    > [!IMPORTANT]  
    >  Se o cliente do Endpoint Protection exigir uma reinicialização do computador e essa configuração for **Não**, o computador será reiniciado, independentemente das janelas de manutenção configuradas.  

-   **Período de tempo permitido durante o qual os usuários podem adiar o reinício necessário para concluir a instalação do Endpoint Protection (horas)**  </br>
     Se uma reinicialização for necessária após a instalação do cliente do Endpoint Protection, essa configuração especificará o número de horas pelas quais os usuários podem adiar a reinicialização obrigatória. Essa configuração exige que a configuração **Suprimir qualquer reinicialização obrigatória do computador após a instalação do Endpoint Protection** seja **Não**.  

-   **Desabilitar fontes alternativas (como Microsoft Windows Update, Microsoft Windows Server Update Services ou compartilhamentos UNC) para a atualização de definição inicial em computadores cliente**  </br>
     Escolha **Sim** se deseja que o Configuration Manager instale somente a atualização de definição inicial em computadores cliente. Essa configuração pode ser útil para evitar conexões de rede desnecessárias e reduzir a largura de banda da rede durante a instalação inicial da atualização da definição.  



##  <a name="enrollment"></a>Registro

-   **Intervalo de sondagem para clientes herdados de dispositivos móveis** </br>
    Clique em **Definir Intervalo** para especificar o período, em minutos ou horas, durante o qual os dispositivos móveis herdados sondam para a política. Esses dispositivos incluem plataformas como Windows CE, Mac OS X e Unix ou Linux.

-   **Intervalo de sondagem para dispositivos modernos (minutos)** </br>
    Insira o número de minutos durante os quais os dispositivos modernos sondam para a política. Essa configuração destina-se a dispositivos Windows 10 gerenciados por meio do gerenciamento de dispositivo móvel local.

-   **Permitir que os usuários registrem dispositivos móveis e computadores Mac** </br>
    Para habilitar o registro baseado em usuário de dispositivos herdados, defina essa configuração como **Sim** e, em seguida, defina a seguinte configuração:

    -   **Perfil de registro** </br>
        Clique em **Definir Perfil** para criar ou selecionar um perfil de registro. Para obter mais informações, consulte [Definir as configurações do cliente para o registro](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment).

-   **Permitir que os usuários registrem dispositivos modernos** </br>
    Para habilitar o registro baseado em usuário de dispositivos modernos, defina essa configuração como **Sim** e, em seguida, defina a seguinte configuração:

    -   **Perfil de registro de dispositivo moderno** </br>
        Clique em **Definir Perfil** para criar ou selecionar um perfil de registro. Para obter mais informações, consulte [Criar um perfil de registro que permite que os usuários registrem dispositivos modernos](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf).



##  <a name="hardware-inventory"></a>Inventário de hardware  

-   **Habilitar o inventário de hardware em clientes** </br>
    Essa configuração é definida como **Sim** por padrão. Para obter mais informações, consulte [Introdução ao inventário de hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).

-   **Agendamento de inventário de hardware** </br>
    Clique em **Agendamento** para ajustar a frequência com que os clientes executam o ciclo de inventário de hardware. Por padrão, esse ciclo ocorre a cada sete dias.

-   **Atraso máximo aleatório (minutos)** </br>
    Especifique o número máximo de minutos até o qual o cliente do Configuration Manager tornará aleatório o ciclo de inventário de hardware com base no agendamento definido. Essa operação aleatória em todos os clientes ajudam a balancear a carga do processamento de inventário no servidor do site. É possível especificar um valor de 0 a 480. Por padrão, esse valor é definido como 240 minutos (quatro horas).

-   **Tamanho máximo de arquivo MIF personalizado (KB)**  </br>
     Especifique o tamanho máximo, em KB (quilobytes), permitido para cada arquivo personalizado MIF (Formato de Informações de Gerenciamento) que será coletado por um cliente durante um ciclo de inventário de hardware. O agente de inventário de hardware do Configuration Manager não processa nenhum arquivo MIF personalizado que excede esse tamanho. É possível especificar um tamanho de 1 a 5.120 KB. Por padrão, esse valor é definido como 250 KB. Essa configuração não afeta o tamanho do arquivo de dados de inventário de hardware regular.  

    > [!NOTE]  
    >  Essa definição só está disponível nas configurações do cliente padrão.  

-   **Classes de inventário de hardware**  </br>
     Clique em **Definir Classes** para estender as informações de hardware coletadas dos clientes sem editar manualmente o arquivo sms_def.mof. Para obter informações, consulte [Como configurar o inventário de hardware](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Coletar arquivos MIF**  </br>
     Use esta configuração para especificar se os arquivos MIF devem ser coletados de clientes Configuration Manager durante o Inventário de Hardware.  

     Para que um arquivo MIF seja coletado pelo inventário de hardware, ele deve estar no local correto no computador cliente. Por padrão, os arquivos estão localizados nos seguintes caminhos:  

    -   Os **arquivos IDMIF** devem estar na pasta Windows\System32\CCM\Inventory\Idmif 

    -   Os **arquivos NOIDMIF** devem estar na pasta Windows\System32\CCM\Inventory\Noidmif

    > [!NOTE]  
    >  Essa definição só está disponível nas configurações do cliente padrão.

   

##  <a name="metered-internet-connections"></a>Planos de Internet Limitados  
 Gerencie como os computadores Windows 8 e posterior usam conexões limitadas com a Internet para se comunicar com o Configuration Manager. Provedores de Internet ocasionalmente cobram por quantidade de dados que você envia e recebe quando está em uma conexão de Internet limitada.  

> [!NOTE]  
>  A configuração de cliente definida não é aplicada nos seguintes cenários:  
>   
> -   O computador está em uma conexão de dados em roaming: o cliente do Configuration Manager não executa tarefas que exigem que os dados sejam transferidos para sites do Configuration Manager.  
> -   As propriedades de conexão de rede do Windows são configuradas como ilimitadas: o cliente do Configuration Manager se comporta como se a conexão fosse ilimitada e, por isso, transfere os dados para o site.  

-   **Comunicação de cliente em conexões de Internet limitadas**  </br>
     Escolha uma das seguintes opções para essa configuração:  

    -   **Permitir**: todas as comunicações do cliente são permitidas pela conexão de Internet limitada, a menos que o dispositivo cliente esteja usando uma conexão de dados móvel.  

    -   **Limite**: somente as seguintes comunicações do cliente são permitidas pela conexão de Internet limitada:  

        -   Recuperação de política do cliente  

        -   Mensagens de estado do cliente para enviar ao site  

        -   Solicitações de instalação de software usando o catálogo de aplicativos  

        -   Implantações necessárias (quando é atingido o prazo de instalação)  

        > [!IMPORTANT]  
        >  O cliente sempre permite instalações de software por meio do Centro de Software ou do Catálogo de Aplicativos, independentemente das configurações de conexão limitada com a Internet.  

         Se o limite de transferência de dados for alcançado para a conexão da Internet limitada, o cliente não tentará mais se comunicar com os sites do Configuration Manager.  

    -   **Bloquear**: o cliente do Configuration Manager não tenta se comunicar com os sites do Configuration Manager quando ele está em uma conexão de Internet limitada. Essa opção é o padrão.  



##  <a name="power-management"></a>Gerenciamento de Energia  

-   **Permitir o gerenciamento de energia de dispositivos** </br>
    Defina essa configuração como **Sim** para habilitar o gerenciamento de energia em clientes. Para mais informações, consulte [Introdução ao gerenciamento de energia](/sccm/core/clients/manage/power/introduction-to-power-management).

-   **Permitir que os usuários excluam seu dispositivo do gerenciamento de energia**  </br>
     Escolha **Sim** para permitir que usuários do Centro de Software excluam seus computadores das configurações de gerenciamento de energia definidas.  

-   **Habilitar proxy de ativação** </br> 
     Especifique **Sim** para complementar a configuração Wake On LAN do site quando estiver definida para pacotes unicast.  

     Para mais informações sobre o proxy de ativação, confira [Planejar a ativação de clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  Não habilite o proxy de ativação em uma rede de produção sem primeiro entender como ele funciona e avaliá-lo em um ambiente de teste.  

    Em seguida, defina as seguintes configurações adicionais, conforme necessário:

    -   **Número de porta proxy de ativação (UDP)**  </br>
         O número da porta que os clientes usam para enviar pacotes de ativação para computadores suspensos. Mantenha a porta padrão 25536 ou altere o número para um valor de sua escolha.  

    -   **Número de porta Wake On LAN (UDP)** </br> 
         Mantenha o valor padrão 9, a menos que você tenha alterado o número da porta Wake On LAN (UDP) na guia **Portas** das **Propriedades** do site.  

        > [!IMPORTANT]  
        >  Esse número deve corresponder ao número nas **Propriedades**do site. Se você alterar esse número em um só lugar, ele não será atualizado automaticamente em outro lugar.  

    -   **Exceção do Windows Defender Firewall para proxy de ativação** </br>
         O cliente do Configuration Manager configura automaticamente o número da porta do proxy de ativação em dispositivos que executam o Windows Defender Firewall. Clique em **Configurar** para especificar os perfis de firewall desejados.

        Se os clientes executarem outro firewall, você deverá configurá-lo manualmente para permitir o **Número da porta do proxy de ativação (UDP)**.  
        
    -   **Prefixos IPv6, se necessário, para DirectAccess ou outros dispositivos de rede intermediários. Use uma vírgula para especificar várias entradas** </br>
        Insira os prefixos IPv6 necessários para que o proxy de ativação funcione na rede.



##  <a name="remote-tools"></a>Ferramentas remotas  

-   **Habilitar o controle remoto em clientes** e **Perfis de exceção do firewall**  </br>
     Clique em **Configurar** para habilitar o recurso de controle remoto do Configuration Manager. Outra opção é definir configurações de firewall para permitir que o controle remoto funcione em computadores cliente.  

     O controle remoto está desativado por padrão.  

    > [!IMPORTANT]  
    >  Se as configurações de firewall não estiverem definidas, o controle remoto poderá não funcionar corretamente.  

-   **Os usuários podem alterar as configurações de política ou notificação no Centro de Software**  </br>
     Escolha se os usuários podem alterar as opções de controle remoto do Centro de Software.  

-   **Permitir o controle remoto de um computador autônomo**  </br>
     Escolha se um administrador pode usar o controle remoto para acessar um computador cliente que está desconectado ou bloqueado. Apenas um computador conectado e desbloqueado pode ser controlado remotamente quando essa configuração está desabilitada.  

-   **Solicitar permissão de Controle Remoto ao usuário**  </br>
     Escolha se o computador cliente mostra uma mensagem solicitando a permissão do usuário antes de permitir uma sessão de controle remoto.  

-   **Solicitar ao usuário permissão para transferir conteúdo da área de transferência compartilhada** </br>
    Conceda aos usuários a oportunidade de aceitar ou negar transferências de arquivo antes de transferir conteúdo da área de transferência compartilhada em uma seção de controle remoto. Os usuários precisam apenas conceder permissão uma vez por sessão e o visualizador não terá a capacidade de conceder a si mesmo a permissão de continuar a transferência de arquivo.

-   **Conceder permissão de Controle Remoto para o grupo local de administradores**  </br>
     Escolha se os administradores locais no servidor que inicia a conexão de controle remoto pode estabelecer sessões de controle remoto com computadores cliente.  

-   **Nível de acesso permitido**  </br>
     Especifique o nível de acesso de controle remoto que será permitido. Escolha uma das seguintes configurações:  
    - **Sem Acesso**
    - **Somente Exibição**
    - **Controle Total**  

-   **Visualizadores permitidos de Controle Remoto e Assistência Remota**  </br>
     Clique em **Definir Visualizadores** para especificar os nomes de usuários do Windows que podem estabelecer sessões de controle remoto em computadores cliente.  

-   **Mostrar ícone de notificação de sessão na barra de tarefas**  </br>
     Defina essa configuração como **Sim** para mostrar um ícone na barra de tarefas do Windows do cliente para indicar uma sessão de controle remoto ativa.  

-   **Mostrar barra de conexão da sessão**  </br>
     Defina essa configuração como **Sim** para mostrar a barra de conexão de sessão de alta visibilidade em clientes para indicar uma sessão de controle remoto ativa.  

-   **Tocar um som no cliente**  </br>
     Defina essa configuração para usar o som para indicar quando uma sessão de controle remoto está ativa em um computador cliente. Selecione uma das seguintes opções:
    - **Sem som**
    - **Início e envio de sessão** (padrão)
    - **Várias vezes durante a sessão**  

-   **Gerenciar configurações de assistência remota não solicitada**  </br>
     Defina essa configuração como **Sim** para permitir que o Configuration Manager gerencie sessões não solicitadas da Assistência Remota.  

     Em uma sessão de Assistência Remota não solicitada, o usuário no computador cliente não solicitou assistência para iniciar uma sessão.  

-   **Gerenciar configurações de assistência remota solicitada**  </br>
     Defina essa configuração como **Sim** para permitir que o Configuration Manager gerencie sessões solicitadas da Assistência Remota.  

     Em uma sessão de Assistência Remota solicitada, o usuário no computador cliente enviou uma solicitação de assistência remota ao administrador.  

-   **Nível de acesso para assistência remota**  </br>
     Escolha o nível de acesso a ser atribuído às sessões de Assistência Remota iniciadas no console do Configuration Manager.  Selecione uma das seguintes opções:
    - **Nenhum** (padrão)
    - **Exibição Remota**
    - **Controle Total**

    > [!NOTE]  
    >  O usuário no computador cliente sempre deve conceder permissão para que uma sessão de assistência remota ocorra.  

-   **Gerenciar configurações da Área de Trabalho Remota**  </br>
     Defina essa configuração como **Sim** para permitir que o Configuration Manager gerencie sessões de Área de Trabalho Remota para computadores.  

-   **Permitir que os visualizadores autorizados se conectem usando a conexão de Área de Trabalho Remota**  </br>
     Defina essa configuração como **Sim** para adicionar os usuários especificados na lista de visualizadores permitidos ao grupo local de usuários da Área de Trabalho Remota em clientes.  

-   **Exigir autenticação no nível da rede em computadores que executam o sistema operacional Windows Vista e versões posteriores**  </br>
     Defina essa configuração como **Sim** para usar a NLA (autenticação no nível da rede) para estabelecer conexões de Área de Trabalho Remota com computadores cliente. A NLA inicialmente exige menos recursos do computador remoto, pois conclui a autenticação de usuário antes de estabelecer uma conexão de Área de Trabalho Remota. O uso da NLA é uma configuração mais segura. A NLA ajuda a proteger o computador contra usuários ou software mal-intencionados e reduz o risco de ataques de negação de serviço.  



## <a name="software-center"></a>Centro de software

-   **Selecionar estas novas configurações para especificar as informações da empresa** </br>
    Defina essa configuração como **Sim** e, em seguida, especifique as seguintes configurações para criar uma identidade visual do Centro de Software para sua organização:

    - **Nome da empresa** </br>
        Insira o nome da organização que os usuários veem no Centro de Software.
    - **Esquema de cores para o Centro de Software** </br>
        Clique em **Selecionar Cor** para definir a cor primária usada pelo Centro de Software.
    - **Selecionar um logotipo para o Centro de Software** </br>
        Clique em **Procurar** para selecionar uma imagem a ser exibida no Centro de Software. O logotipo deve ser um JPEG, PNG ou BMP de 400 x 100 pixels com tamanho máximo de 750 KB. O nome do arquivo de logotipo não deve conter espaços. <!--SMS.503731 space in filename, noticed BMP missing as filetype-->

-   Visibilidade da guias do Centro de Software </br>
    Defina as configurações adicionais nesse grupo como **Sim** para tornar as seguintes guias visíveis no Centro de Software:
    - **Aplicativos**
    - **Atualizações**
    - **Sistemas Operacionais**
    - **Status da Instalação**
    - **Conformidade do Dispositivo**
    - **Opções**

    Por exemplo, caso sua organização não use políticas de conformidade e você deseje ocultar a guia Conformidade do Dispositivo no Centro de Software, defina a configuração **Habilitar guia Conformidade do Dispositivo** como **Não**.



## <a name="software-deployment"></a>Implantação de software  

-   **Reavaliação de agendamento para implantações**  </br>
     Configure um agendamento para quando o Configuration Manager reavalia as regras de requisito para todas as implantações. O valor padrão é um intervalo de sete dias.  

    > [!IMPORTANT]  
    >  É recomendável que você não altere esse valor para um valor menor do que o padrão. Um agendamento de reavaliação mais agressivo afeta negativamente o desempenho da rede e dos computadores cliente.  

     Inicie essa ação em um cliente escolhendo o **Ciclo de Avaliação de Implantação do Aplicativo** na guia **Ações** do painel de controle do **Configuration Manager**.  



##  <a name="software-inventory"></a>Inventário de software  

-   **Habilitar inventário de software em clientes** </br>
    Essa configuração é definida como **Sim** por padrão. Para obter mais informações, consulte [Introdução ao inventário de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

-   **Agendar inventário de software e coleta de arquivos** </br>
    Clique em **Agendamento** para ajustar a frequência com que os clientes executam os ciclos de inventário de software e coleta de arquivos. Por padrão, esse ciclo ocorre a cada sete dias.

-   **Detalhe no relatório de inventário**  </br>
     Especifique um dos seguintes níveis de informações de arquivo para o inventário:
    - **Somente arquivo**
    - **Somente produto**
    - **Detalhes completos** (padrão)

-   **Inventariar estes tipos de arquivo**  </br>
     Se desejar especificar os tipos de arquivo a serem inventariados, clique em **Definir Tipos** e, em seguida, configure as seguintes opções:  

    > [!NOTE]  
    >  Se várias configurações personalizadas do cliente forem aplicadas a um computador, o inventário retornado por cada configuração será mesclado.  

    -   Clique no ícone **Novo** para adicionar um novo tipo de arquivo ao inventário. Em seguida, especifique as seguintes informações na caixa de diálogo **Propriedades de Arquivo Inventariado**:  

        -   **Nome**: forneça um nome para o arquivo que você deseja inventariar. Use um asterisco (**&#42;**) curinga para representar qualquer cadeia de texto e um ponto de interrogação (**?**) para representar qualquer caractere único. Por exemplo, se você desejar inventariar todos os arquivos com a extensão .doc, especifique o nome do arquivo **\*.doc**.  

        -   **Local**: clique em **Definir** para abrir a caixa de diálogo **Propriedades de Caminho**. Configure o inventário de software para pesquisar o arquivo especificado em todos os discos rígidos do cliente, pesquisar um caminho especificado (por exemplo, **C:\Folder**) ou uma variável especificada (por exemplo, *%windir%*). Também é possível pesquisar todas as subpastas no caminho especificado.  

        -   **Excluir arquivos criptografados e compactados**: quando você escolhe essa opção, os arquivos compactados ou criptografados não são inventariados.  

        -   **Excluir arquivos da pasta do Windows**: quando você seleciona essa opção, os arquivos da pasta do Windows e suas subpastas não são inventariados.  

    -   Clique em **OK** para fechar a caixa de diálogo **Propriedades de Arquivo Inventariado** .  

    -   Adicione todos os arquivos que você deseja inventariar e, em seguida, clique em **OK** para fechar a caixa de diálogo **Definir Configuração do Cliente**.  

-   **Coletar arquivos**  </br>
     Se você deseja coletar arquivos de computadores cliente, clique em **Definir Arquivos** e, em seguida, defina as seguintes configurações:  

    > [!NOTE]  
    >  Se várias configurações personalizadas do cliente forem aplicadas a um computador, o inventário retornado por cada configuração será mesclado.  

    -   Na caixa de diálogo **Definir Configuração do Cliente**, clique no ícone **Novo** para adicionar um arquivo a ser coletado.  

    -   Na caixa de diálogo **Propriedades do Arquivo Coletado** , forneça as seguintes informações:  

        -   **Nome**: forneça um nome para o arquivo que você deseja coletar. Use um asterisco (**&#42;**) curinga para representar qualquer cadeia de texto e um ponto de interrogação (**?**) para representar qualquer caractere único.  

        -   **Local**: clique em **Definir** para abrir a caixa de diálogo **Propriedades de Caminho**. Configure o inventário de software para pesquisar o arquivo que você deseja coletar em todos os discos rígidos do cliente, pesquisar um caminho especificado (por exemplo, **C:\Folder**) ou em uma variável especificada (por exemplo, *%windir%*). Também é possível pesquisar todas as subpastas no caminho especificado.  

        -   **Excluir arquivos criptografados e compactados**: quando você escolhe essa opção, os arquivos que foram compactados ou criptografados não são coletados.  

        -   **Parar a coleta de arquivos quando o tamanho total dos arquivos exceder (KB)**: especifique o tamanho do arquivo, em KB (quilobytes), após o qual o cliente interromperá a coleta dos arquivos especificados.  

          > [!NOTE]  
          >  O servidor do site coleta as cinco versões alteradas mais recentemente de arquivos coletados e as armazena no *&lt;Diretório de instalação do ConfigMgr\>*\Inboxes\Sinv.box\Filecol. Se um arquivo não foi alterado desde o último ciclo de inventário de software, o arquivo não será coletado novamente.  
          >   
          >  O inventário de software não coleta arquivos maiores que 20 MB.  
          >   
          >  O valor **Tamanho máximo para todos os arquivos coletados (KB)** na caixa de diálogo **Definir a Configuração do Cliente** exibe o tamanho máximo para todos os arquivos coletados. Quando esse tamanho é atingido, a coleta é interrompida. Todos os arquivos já coletados são retidos e enviados para o servidor do site.  

          > [!IMPORTANT]
          >  Se você configurar o inventário de software para coletar muitos arquivos grandes, essa configuração pode afetar negativamente o desempenho da rede e do servidor do site.  

        Para obter informações sobre como exibir os arquivos coletados, consulte [Como usar o Gerenciador de Recursos para exibir o inventário de software](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Clique em **OK** para fechar a caixa de diálogo **Propriedades do Arquivo Coletado** .  

    -   Adicione todos os arquivos que você deseja coletar e, em seguida, clique em **OK** para fechar a caixa de diálogo **Definir Configuração do Cliente**.  

-   **Definir Nomes**  </br>
     O agente de inventário de software recupera os nomes de produto e fabricante nas informações de cabeçalho do arquivo. Esses nomes nem sempre são padronizados nas informações de cabeçalho do arquivo. Quando você exibe o inventário de software no Gerenciador de Recursos, podem aparecer versões diferentes do mesmo fabricante ou nome de produto. Para padronizar esses nomes de exibição, clique em **Definir Nomes** e, em seguida, defina as seguintes configurações:  

    -   **Tipo de nome**: o inventário de software coleta informações sobre produtos e fabricantes. Escolha se você deseja configurar nomes de exibição para um **Fabricante** ou um **Produto**.  

    -   **Nome de exibição:** especifique o nome de exibição que você deseja usar em vez dos nomes na lista **Nomes inventariados**. Clique no ícone **Novo** para especificar um novo nome de exibição.  

    -   **Nomes inventariados**: clique no ícone **Novo** para adicionar um nome inventariado. Esse nome é substituído no inventário de software pelo nome escolhido na lista **Nome de exibição**. Você pode adicionar vários nomes a serem substituídos.  



##  <a name="software-metering"></a>Medição de software

-   **Habilitar medição de software em clientes** </br>
    Essa configuração é definida como **Sim** por padrão. Para obter mais informações, consulte [Medição de software](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering).

-   **Agendar coleta de dados** </br>
    Clique em **Agendamento** para ajustar a frequência com que os clientes executam o ciclo de medição de software. Por padrão, esse ciclo ocorre a cada sete dias.



##  <a name="software-updates"></a>Atualizações de software  

-   **Habilitar atualizações de software em clientes**  </br>
     Use essa configuração para habilitar atualizações de software em clientes do Configuration Manager. Ao desabilitar essa configuração, o Configuration Manager removerá as políticas de implantação existentes do cliente. Quando você reativa essa configuração, o cliente baixa a política de implantação atual.  

    > [!IMPORTANT]  
    >  Quando você desabilitar essa configuração, as políticas de conformidade que dependem das atualizações de software não funcionarão mais.  

-   **Agendamento de verificação de atualização de software**  </br>
     Clique em **Agendamento** para especificar a frequência com que o cliente inicia uma verificação de avaliação de conformidade. Essa verificação determina o estado das atualizações de software no cliente (por exemplo, obrigatórias ou instaladas). Para mais informações sobre a avaliação de conformidade, confira [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance) (Avaliação de conformidade de atualizações de software).  

     Por padrão, essa verificação usa um agendamento simples a ser iniciado a cada sete dias. Você pode criar um agendamento personalizado para especificar uma data e hora exatas de início, usar o UTC (Horário Coordenado Universal) ou a hora local, e configurar o intervalo recorrente para um dia específico da semana.  

    > [!NOTE]  
    >  Se você especificar um intervalo inferior a um dia, o Configuration Manager usará um dia como padrão automaticamente.  

    > [!WARNING]  
    >  A hora de início real em computadores cliente é a hora de início mais um período aleatório de até duas horas. Essa operação aleatória evita que os computadores cliente iniciem a verificação e se conectem simultaneamente ao ponto de atualização de software ativo.  

-   **Reavaliação de implantação da agenda**  </br>
     Clique em **Agendamento** para configurar a frequência com que o agente cliente de atualizações de software reavalia as atualizações de software para o status de instalação em computadores cliente do Configuration Manager. Quando as atualizações de software instaladas anteriormente não são mais encontradas em clientes, mas ainda são necessárias, o cliente reinstala as atualizações de software.

     Ajuste esse agendamento com base na política da empresa para conformidade de atualizações de software e indique se os usuários podem desinstalar as atualizações de software. Cada ciclo de reavaliação de implantação resulta em uma atividade da rede e do processador do computador cliente. Por padrão, essa configuração usa um agendamento simples para iniciar a verificação de reavaliação de implantação a cada sete dias.  

    > [!NOTE]  
    >  Se você especificar um intervalo inferior a um dia, o Configuration Manager usará um dia como padrão automaticamente.  

-   **Quando a data limite de implantação da atualização de software for alcançada, instalar todas as outras implantações de atualização de software com a data limite dentro de um período especificado**  </br>
     Defina essa configuração como **Sim** para instalar todas as atualizações de software de implantações obrigatórias com datas limite que ocorrem dentro de um período especificado. Quando uma implantação de atualização de software obrigatória alcança uma data limite, o cliente inicia a instalação das atualizações de software na implantação. Essa configuração determina se devem ser instaladas as atualizações de software de outras implantações obrigatórias que têm uma data limite dentro do tempo especificado.  

     Use essa configuração para agilizar a instalação de atualizações de software obrigatórias. Potencialmente, essa configuração também aumenta a segurança de cliente, diminui as notificações do usuário final e diminui as reinicializações do cliente. Por padrão, essa configuração é definida como **Não** e, portanto, não está habilitada.  

-   **Período de tempo para o qual todas as implantações pendentes com prazo nesse período também serão instaladas**  </br>
     Use essa configuração para especificar o período da configuração anterior. Você pode inserir um valor entre 1 e 23 horas e de 1 a 365 dias. Por padrão, essa configuração é definida para sete dias.  

-   **Habilitar instalação dos arquivos de instalação do Express em clientes** </br>
    Defina essa configuração como **Sim** para permitir que os clientes usem os arquivos da instalação expressa. Para saber mais, confira [Gerenciar os arquivos de instalação expressa para atualizações do Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

    -   **Porta usada para baixar conteúdo para arquivos de instalação do Express** </br>
        Essa configuração define a porta local para que o ouvinte HTTP baixe o conteúdo expresso. Ela é definida como 8005 por padrão. Não é necessário abrir essa porta no firewall do cliente.

-   **Habilitar o gerenciamento do Agente Cliente do Office 365** </br>
    Use essa configuração para habilitar o gerenciamento do Agente Cliente do Office 365. Quando você define o valor como **Sim**, ele habilita a definição de configurações de instalação do Office 365, baixando arquivos de CDNs (Redes de Distribuição de Conteúdo) do Office e implantando os arquivos como um aplicativo no Configuration Manager. Para obter mais informações, consulte [Gerenciar o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).



## <a name="state-messaging"></a>Mensagem de Estado

-   **Ciclo de relatórios de mensagens de estado (minutos)**  </br>
     Especifica a frequência com que os clientes relatam mensagens de estado. Essa configuração é de 15 minutos por padrão.



##  <a name="user-and-device-affinity"></a>Afinidade de dispositivo e de usuário  

-   **Limite de uso de afinidade de dispositivo do usuário (minutos)**  </br>
     Especifique o número de minutos antes que o Configuration Manager crie um mapeamento de afinidade de dispositivo de usuário.  Por padrão, esse valor é de 2.880 minutos (dois dias).

-   **Limite de uso de afinidade de dispositivo do usuário (dias)**  </br>
     Especifique o número de dias durante os quais o cliente mede o limite de afinidade de dispositivo baseado no uso.  Por padrão, esse valor é 30 dias.

    > [!NOTE]  
    >  Por exemplo, especifique **Limite de uso da afinidade de dispositivo de usuário (minutos)** como **60** minutos e **Limite de uso da afinidade de dispositivo de usuário (dias)** como **5** dias. Em seguida, o usuário deve usar o dispositivo por 60 minutos em um período de cinco dias para criar a afinidade automática com o dispositivo.  

-   **Configurar automaticamente a afinidade de dispositivo de usuário por meio de dados de uso**  </br>
     Escolha **Sim** para criar a afinidade de dispositivo de usuário automática com base nas informações de uso coletadas do Configuration Manager.  

-   **Permitir ao usuário definir os seus dispositivos primários** </br>
    Quando essa configuração for **Sim**, os usuários poderão identificar seus próprios dispositivos primários no Centro de Software.



## <a name="windows-analytics"></a>Windows Analytics

Para obter mais informações sobre essas configurações, consulte [Configurar clientes para relatar dados ao Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).
    
