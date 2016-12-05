---
title: "Configurações do cliente | System Center Configuration Manager"
description: "Selecione as configurações do cliente usando o console de administração no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: 15
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: cbe052891c55dd0c0d58c6e65d783314b0ec8ce9

---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Sobre as configurações do cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Todas as configurações de cliente no System Center Configuration Manager são gerenciadas no console do Configuration Manager do nó **Configurações do Cliente** no espaço de trabalho **Administração**. Um conjunto de configurações padrão é fornecido com o Configuration Manager. Quando você modifica as configurações padrão do cliente, essas configurações são aplicadas a todos os clientes na hierarquia. Você também pode configurar configurações personalizadas do cliente, que substituem as configurações padrão do cliente ao atribuí-las a coleções. Para obter informações sobre como definir as configurações do cliente, consulte [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

 Muitas das configurações do cliente são autoexplicativas. Use as seções a seguir para obter mais informações sobre as configurações do cliente que podem requerer algumas informações antes de configurá-las.  

##  <a name="a-namebkmkbitsa-background-intelligent-transfer"></a><a name="BKMK_BITS"></a> Transferência inteligente em segundo plano  

-   **Limitar a largura de banda de rede máxima para transferências em segundo plano do BITS**  

     Se essa opção estiver configurada como **Verdadeira** ou **Sim**, a limitação da largura de banda do BITS será usada pelos clientes do Configuration Manager.  

-   **Hora de início do período de limitação**  

     Especifique a hora de início na hora local em que o período de limitação do BITS começará.  

-   **Hora de término do período de limitação**  

     Especifique a hora de término na hora local em que o período de limitação do BITS terminará. Se esse valor for o mesmo da **Hora de início do período de limitação**, a limitação do BITS sempre estará habilitada.  

-   **Taxa de transferência máxima durante o período de limitação (Kbps)**  

     Especifique a taxa de transferência máxima em (Kbps) que pode ser usada pelos clientes do Configuration Manager durante o período de limitação especificado do BITS.  

-   **Permitir downloads de BITS fora do período de limitação**  

     Selecione esta opção para permitir downloads de BITS fora do período de limitação. Essa opção permite que os clientes do Configuration Manager usem configurações de BITS separadas fora do período especificado.  

-   **Taxa de transferência máxima fora do período de limitação (Kbps)**  

     Especifique a taxa de transferência máxima em (Kbps) que será ser usada pelos clientes do Configuration Manager quando estiver fora do período de limitação especificado do BITS. Essa opção poderá ser configurada somente quando você tiver selecionado permitir limitação de BITS fora do período especificado.  

##  <a name="a-namebkmkclientpolicydevicesettingsa-client-policy"></a><a name="BKMK_ClientPolicyDeviceSettings"></a> Política do cliente  

-   **Intervalo de sondagem da política do cliente (minutos)**  

     Especifique a frequência com que os seguintes clientes do Configuration Manager baixam a política do cliente:  

    -   Computadores Windows (por exemplo, desktops, servidores, laptops)  

    -   Dispositivos móveis registrados pelo Configuration Manager  

    -   Computadores Mac  

    -   Computadores que executam o Linux ou UNIX  

-   **Habilitar sondagem de política de usuário nos clientes**  

     Quando você definir esta configuração como **Verdadeira** ou **Sim** e o Configuration Manager tiver descoberto o usuário, os clientes do Configuration Manager nos computadores receberão aplicativos e programas destinados ao usuário conectado. Para obter mais informações sobre como descobrir usuários, confira [Descoberta de usuários do Active Directory no Configuration Manager](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).  

     Como o catálogo de aplicativos recebe a lista de software disponível para usuários do servidor do site, essa configuração não deve ser configurada como **Verdadeiro** ou **Sim** para que os usuários vejam e solicitem aplicativos do catálogo de aplicativos. No entanto, se essa configuração for **Falso** ou **Não**, o seguinte não funcionará quando os usuários utilizarem o catálogo de aplicativos:  

    -   Os usuários não podem instalar os aplicativos que veem no Catálogo de Aplicativos.  

    -   Os usuários não verão as notificações sobre suas solicitações de aprovação de aplicativo. Em vez disso, eles devem atualizar o catálogo de aplicativos e verificar o status de aprovação.  

    -   Os usuários não receberão as revisões e atualizações para aplicativos publicadas no catálogo de aplicativos. No entanto, eles verão as alterações nas informações do aplicativo no catálogo de aplicativos.  

    -   Se você remover uma implantação de aplicativo depois que o cliente tiver instalado o aplicativo do catálogo de aplicativos, os clientes continuarão verificando se o aplicativo está instalado por até 2 dias.  

     Além disso, quando essa configuração for **Falsa** ou **Não**, os usuários não receberão os aplicativos necessários que você implanta em usuários ou outras operações de gerenciamento contidas nas políticas do usuário.  

     Essa configuração aplica-se a usuários quando o computador estiver na intranet e na Internet; ela deve ser definida como **Verdadeira** ou **Sim** se você também deseja habilitar políticas do usuário na Internet.  

-   **Ativar solicitações de política de usuário de clientes da Internet**  

     Quando o cliente e o site estão configurados para gerenciamento de clientes baseado na Internet e você define essa opção como **Verdadeira** ou **Sim** e ambas das condições a seguir são aplicáveis, os usuários recebem a política do usuário quando o computador está na Internet:  

    -   A configuração do cliente **Habilitar sondagem da política de usuário nos clientes** está definida como **Verdadeira** ou **Habilitar política de usuário em clientes** está definida como **Sim**.  

    -   O ponto de gerenciamento baseado na Internet autentica com êxito o usuário utilizando a autenticação do Windows (Kerberos ou NTLM).  

     Se você deixar essa opção como **Falsa** ou **Não**, ou se alguma das condições falhar, um computador na Internet receberá somente as políticas do computador. Nesse cenário, os usuários ainda podem ver, solicitar e instalar aplicativos de um catálogo de aplicativos baseados na Internet. Se essa configuração for **Falsa** ou **Não** , mas **Habilitar sondagem da política de usuário nos clientes** estiver configurada como **Verdadeira** ou **Habilitar política de usuário em clientes** como **Sim**, os usuários não receberão as políticas de usuário até que o computador esteja conectado à intranet.  

     Para mais informações sobre o gerenciamento de clientes na Internet, confira [Considerações sobre a comunicação do cliente da Internet ou de uma floresta não confiável](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) em [Comunicação entre pontos de extremidade no System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

    > [!NOTE]  
    >  As solicitações de aprovação de aplicativo dos usuários não exigem autenticação de usuário nem políticas de usuário.  

##  <a name="a-namebkmkcompliancea-compliance-settings"></a><a name="BKMK_Compliance"></a> Compliance Settings  

-   **Agendar a avaliação da conformidade**  

     Clique em **Agendar** para criar o agendamento padrão que será exibido aos usuários quando eles implantam uma linha de base de configuração. Esse valor pode ser configurado para cada linha de base na caixa de diálogo **Implantar Linha de Base de Configuração** .  

-   **Habilitar perfis e dados do usuário**  

     Selecione **Sim** se deseja implantar itens de configuração de perfis e dados do usuário em computadores com Windows 8 em sua hierarquia.  

     Para mais informações sobre perfis e dados do usuário, consulte [Como criar itens de configuração de perfis e dados de usuário no System Center Configuration Manager](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md).  

##  <a name="a-namebkmkcomputeragentdevicesettingsa-computer-agent"></a><a name="BKMK_ComputerAgentDeviceSettings"></a> Agente de Computador  

-   **Ponto de sites da Web do Catálogo de Aplicativos padrão**  

     O Configuration Manager usa essa configuração para conectar usuários ao Catálogo de Aplicativos do Centro de Software. Você pode especificar um servidor que hospeda o ponto de sites da Web do catálogo de aplicativos pelo nome NetBIOS ou FQDN, especificar a detecção automática ou especificar uma URL para implantações personalizadas. Na maioria dos casos, a detecção automática é a melhor opção porque oferece os seguintes benefícios:  

    -   Os clientes recebem automaticamente um ponto de sites da Web do catálogo de aplicativos do seu site se o site contém um ponto de sites da Web do catálogo de aplicativos.  

    -   Proteção contra um servidor não autorizado, pois os pontos de sites da Web do catálogo de aplicativos na intranet configurados para HTTPS têm preferência sobre os pontos de sites da Web do catálogo de aplicativos não configurados para HTTPS.  

    -   Quando os clientes são configurados para gerenciamento de clientes baseado na Internet e na intranet, eles recebem um ponto de sites da Web do catálogo de aplicativos baseado na Internet quando estão na Internet e um ponto de sites da Web do catálogo de aplicativos baseado na intranet quando estão na intranet.  

     A detecção automática não garante que os clientes receberão um ponto de sites da Web do catálogo de aplicativos que esteja mais perto deles. Você pode decidir por não usar a **Detecção automática** pelos seguintes motivos:  

    -   Você deseja configurar manualmente o servidor mais próximo para clientes ou garantir que eles não se conectem a um servidor em uma conexão de rede lenta.  

    -   Você deseja controlar quais clientes se conectam a qual servidor. Isso pode ser por motivos comerciais, de desempenho ou teste.  

    -   Você não quer esperar até 25 horas ou uma alteração de rede para que os clientes sejam configurados com um ponto de sites da Web do catálogo de aplicativos diferente.  

     Se você especificar o ponto de sites da Web do catálogo de aplicativos em vez de usar a detecção automática, especifique o nome NetBIOS em vez do FQDN de intranet para reduzir a probabilidade de que os usuários apresentem credenciais ao se conectarem ao catálogo de aplicativos na intranet. Para usar o nome NetBIOS, as seguintes condições devem ser aplicáveis:  

    -   O nome NetBIOS é especificado nas propriedades do ponto de sites da Web do catálogo de aplicativos.  

    -   Você usa o WINS ou todos os clientes estão no mesmo domínio do ponto de sites da Web do catálogo de aplicativos.  

    -   O ponto de sites da Web do catálogo de aplicativos está configurado para conexões do cliente HTTP ou está configurado para conexões do cliente HTTPS, e o certificado do servidor Web contém o nome NetBIOS.  

     Geralmente, os usuários apresentam credenciais quando a URL contém um FQDN, mas não quando a URL é um nome NetBIOS. Espere que os usuários sempre sejam solicitados quando eles se conectam à Internet, pois essa conexão deve usar o FQDN de Internet. Quando os usuários são solicitados a apresentar credenciais quando estão na Internet, verifique se o servidor que executa o ponto de sites da Web do catálogo de aplicativos podem se conectar a um controlador de domínio para a conta do usuário para que o usuário possa ser autenticado usando o Kerberos.  

    > [!NOTE]  
    >  Como funciona a detecção automática:  
    >   
    >  O cliente faz uma solicitação de local de serviço para um ponto de gerenciamento. Se houver um ponto de sites da Web do catálogo de aplicativos no mesmo site do cliente, o servidor é fornecido ao cliente como o servidor do catálogo de aplicativos a ser usado. Quando existe mais de um ponto de sites da Web do catálogo de aplicativos disponível no site, um servidor habilitado para HTTPS tem prioridade sobre um servidor não habilitado para HTTPS. Depois dessa filtragem, todos os clientes recebem um dos servidores para usar como o Catálogo de Aplicativos. O Configuration Manager não faz o balanceamento de carga entre vários servidores. Quando o site do cliente não contém um ponto de sites da Web do catálogo de aplicativos, o ponto de gerenciamento retorna de forma não determinística como um ponto de sites da Web do catálogo de aplicativos da hierarquia.  
    >   
    >  Quando o cliente está na intranet, se o ponto de sites da Web do catálogo de aplicativos selecionado for configurado com um nome NetBIOS para a URL do catálogo de aplicativos, os clientes receberão esse nome NetBIOS em vez do FQDN de intranet. Quando o cliente é detectado como na Internet, somente o FQDN de Internet é fornecido ao cliente.  
    >   
    >  O cliente faz a solicitação de local de serviço a cada 25 horas ou sempre que detecta uma alteração de rede. Por exemplo, se o cliente se mover da intranet para a Internet e puder localizar um ponto de gerenciamento baseado na Internet, o ponto de gerenciamento baseado na Internet fornecerá servidores do ponto de sites da Web do catálogo de aplicativos baseados na Internet para os clientes.  

-   **Adicionar sites da Web do Catálogo de Aplicativos padrão à zona de sites confiáveis do Internet Explorer**  

     Se essa opção estiver configurada como **Verdadeira** ou **Sim**, a URL padrão atual do site da Web do catálogo de aplicativos será adicionada automaticamente à zona de sites confiáveis no Internet Explorer em clientes.  

     Essa definição garante que a configuração do Internet Explorer para Modo Protegido não está habilitada. Se o Modo Protegido estiver habilitado, o cliente do Configuration Manager poderá não conseguir instalar aplicativos do Catálogo de Aplicativos. Por padrão, a zona de sites confiáveis oferece suporte ao logon de usuário para o catálogo de aplicativos, o que requer autenticação do Windows.  

     Se você deixar essa opção como **Falsa**, os clientes do Configuration Manager só conseguirão instalar aplicativos do Catálogo de Aplicativos se essas configurações do Internet Explorer estiverem definidas em outra zona da URL do catálogo de aplicativos que os clientes usam.  

    > [!NOTE]  
    >  Sempre que o Configuration Manager adiciona um Catálogo de Aplicativos à zona de sites confiáveis, o Configuration Manager remove uma URL padrão anterior do Catálogo de Aplicativos que o Configuration Manager adicionou antes de adicionar uma nova entrada.  
    >   
    >  O Configuration Manager não poderá adicionar a URL se ela já estiver especificada em uma das zonas de segurança. Nesse cenário, você deve remover a URL da outra zona ou definir manualmente as configurações necessárias do Internet Explorer.  

-   **Permitir que os aplicativos Silverlight sejam executados no modo de confiança elevada**  

     Essa configuração deve ser definida como **Sim** se os usuários executam o cliente do Configuration Manager e usam o Catálogo de Aplicativos.  

     Se você alterar essa configuração, ela terá efeito quando o usuário carregar o navegador da próxima vez ou atualizar a janela do navegador aberta no momento.  

     Para mais informações sobre esta configuração, consulte [Certificados para o Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicativo](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5) em [Segurança e privacidade para o gerenciamento de aplicativos no System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   **Nome da organização exibido no Centro de Software**  

     Digite o nome que os usuários veem no Centro de Software. Essa informação de identidade visual ajuda os usuários a identificarem este aplicativo como uma fonte confiável.  

-   **Usar o novo Centro de Software**  

     Se habilitados, todos os computadores cliente afetados por essas configurações de cliente usarão o novo Centro de Software que exibe os aplicativos disponíveis para o usuário, que anteriormente só estariam acessíveis no Catálogo de Aplicativos dependente do Silverlight.  

     No entanto, as funções do sistema de sites do ponto de sites da Web do catálogo de aplicativos e do ponto de serviços Web do catálogo de aplicativos ainda são necessárias para que os aplicativos disponíveis para o usuário sejam exibidos no Centro de Software.  

     Para obter mais informações, consulte [Planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Permissões de instalação**  

    > [!WARNING]  
    >  Essa configuração aplica-se o Centro de Software e ao Catálogo de Aplicativos. Essa configuração não tem efeito quando os usuários utilizam o portal da empresa.  

     Configure como os usuários podem iniciar a instalação de software, as atualizações de software e as sequências de tarefas:  

    -   **Todos os usuários**: os usuários conectados a um computador cliente com qualquer autorização, exceto Convidado, podem iniciar a instalação de software, as atualizações de software e as sequências de tarefas.  

    -   **Somente administradores**: os usuários conectados a um computador cliente devem ser membros do grupo local de Administradores para iniciar a instalação de software, as atualizações de software e as sequências de tarefas.  

    -   **Somente Administradores e usuários primários**: os usuários conectados a um computador cliente devem ser membros do grupo local de Administradores ou um usuário primário do computador para iniciar a instalação de software, as atualizações de software e as sequências de tarefas.  

    -   **Nenhum Usuário**: nenhum usuário conectado a um computador cliente pode iniciar a instalação de software, as atualizações de software e as sequências de tarefas. As implantações exigidas para o computador são sempre instaladas no prazo e os usuários não podem iniciar a instalação do software por meio do catálogo de aplicativos ou do Centro de Software.  

-   **Suspender a entrada de PIN do BitLocker na reinicialização**  

     Se a entrada de PIN do BitLocker estiver configurada nos computadores, essa opção pode ignorar a necessidade de inserir um PIN quando o computador é reiniciado após uma instalação de software.  

    -   **Sempre**: o Configuration Manager suspende temporariamente o requisito do BitLocker de inserir um PIN na próxima inicialização do computador após a instalação do software que requer uma reinicialização e a iniciou. Essa configuração aplica-se apenas a reinicializações de computador feitas pelo Configuration Manager e não suspende a necessidade de inserir o PIN do BitLocker quando o usuário reinicia o computador. O requisito de entrada de PIN do BitLocker é retomado após a inicialização do Windows.  

    -   **Nunca**: o Configuration Manager não suspende a necessidade do BitLocker de inserir um PIN na próxima inicialização do computador após ter instalado o software que requer reinicialização. Nesse cenário, a instalação do software não pode terminar até que o usuário insira o PIN para concluir o processo de inicialização padrão e carregar o Windows.  

-   **O software adicional gerencia a implantação de aplicativos e as atualizações de software**  

     Habilite essa opção somente se uma das seguintes condições forem aplicáveis:  

    -   Você usa uma solução de fornecedor que requer que essa configuração seja habilitada.  

    -   Você usa o SDK (Software Development Kit) do Configuration Manager para gerenciar notificações do agente cliente e a instalação de atualizações de aplicativos e software.  

    > [!WARNING]  
    >  Se você selecionar essa opção quando nenhuma dessas condições for aplicável, as atualizações de software e os aplicativos necessários não serão instalados nos clientes. Essa configuração não impede que os usuários instalem aplicativos do catálogo de aplicativos nem que os pacotes, programas e sequências de tarefas sejam instalados em computadores cliente.  

-   **Política de execução do PowerShell**  

     Configurar como os clientes do Configuration Manager podem executar scripts do Windows PowerShell. Esses scripts são muitas vezes usados para detecção e configuração de itens em configurações de conformidade, mas também podem ser enviados para uma implantação como um script padrão.  

    -   **Ignorar**: o cliente do Configuration Manager ignora a configuração do Windows PowerShell no computador cliente para que os scripts não assinados possam ser executados.  

    -   **Restrito**: o cliente do Configuration Manager usa a configuração atual do Windows PowerShell no computador cliente, que determina se os scripts não assinados podem ser executados.  

    -   **Tudo Assinado**: o cliente do Configuration Manager executará scripts apenas se forem assinados por um fornecedor confiável. Essa restrição aplica-se, independentemente da configuração atual do Windows PowerShell no computador cliente.  

     Essa opção exige, pelo menos, a versão do Windows PowerShell 2.0; o padrão é **Tudo Assinado**.  

    > [!TIP]  
    >  Se os scripts não assinados não forem executados devido a essa configuração do cliente, o Configuration Manager relatará esse erro das seguintes maneiras:  
    >   
    >  -   ID do erro **0X87D00327** e a descrição **O script não está assinado** como um erro de status da implantação no espaço de trabalho **Monitoramento** do console do Configuration Manager.  
    > -   Códigos e descrições de **0X87D00327** e **O script não está assinado** ou **0X87D00320** e **O host de script ainda não foi instalado** com o tipo de erro **Erro de Descoberta** em relatórios, como **Detalhes de erros de itens de configuração em uma linha de base de configuração para um ativo**.  
    > -   A mensagem **Script is not signed (Error: 87D00327; Source: CCM)** no arquivo **DcmWmiProvider.log** .  

-   **Desabilitar data limite aleatória**  

     Esta configuração determina se o cliente usa um atraso de ativação de até duas horas para instalar atualizações de software quando o prazo for alcançado. Por padrão, o atraso de ativação está desabilitado.  

     Para cenários de VDI (Virtual Desktop Infrastructure), esse atraso pode ajudar a distribuir o processamento da CPU e a transferência de dados para um computador com várias máquinas virtuais que executam o cliente do Configuration Manager. Mesmo que você não use VDI, se muitos clientes instalarem as mesmas atualizações ao mesmo tempo, isso pode aumentar negativamente o uso da CPU no servidor do site, desacelerar os pontos de distribuição e reduzir significativamente a largura de banda disponível.  

     Se as atualizações de software necessárias precisarem ser instaladas sem demora quando o prazo configurado for alcançado, selecione **Sim** para essa configuração.  

##  <a name="a-namebkmkcomputerrestartdevicesettingsa-computer-restart"></a><a name="BKMK_ComputerRestartDeviceSettings"></a> Reinicialização do computador  
 Ao especificar as configurações de reinicialização do computador, verifique se o valor do intervalo de notificação temporária da reinicialização e o valor do intervalo da contagem regressiva são mais curtos do que a menor janela de manutenção aplicada ao computador.  

 Para obter mais informações sobre as janelas de manutenção, consulte [Como usar janelas de manutenção no System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="a-namebkmkendpointprotectiondevicesettingsa-endpoint-protection"></a><a name="BKMK_EndpointProtectionDeviceSettings"></a> Endpoint Protection  

-   **Gerenciar o cliente Endpoint Protection em computadores cliente**  

     Selecione **Verdadeiro** ou **Sim** se desejar gerenciar clientes do Endpoint Protection existentes em computadores na sua hierarquia.  

     Selecione esta opção se você já tiver instalado o cliente Endpoint Protection e desejar gerenciá-lo com o Configuration Manager.  

     Além disso, selecione essa opção se você quiser criar um script para desinstalar uma solução antimalware existente, instalar o cliente Endpoint Protection e implantar esse script usando um aplicativo, pacote ou programa do Configuration Manager.  

-   **Instalar o cliente do Endpoint Protection em computadores cliente**  

     Selecione **Verdadeiro** ou **Sim** para instalar e habilitar o cliente Endpoint Protection em computadores cliente nos quais ele ainda não estiver instalado.  

    > [!NOTE]  
    >  Se o cliente Endpoint Protection já estiver instalado, selecionar **Falso** ou **Não** não desinstalará o cliente Endpoint Protection. Para desinstalar o cliente Endpoint Protection, defina a configuração de cliente **Gerenciar o cliente Endpoint Protection em computadores cliente** como **Falso** ou **Não**e implante um pacote e um programa para desinstalar o cliente Endpoint Protection.  

-   **Para dispositivos Windows Embedded com filtros de gravação, confirme a instalação de cliente do Endpoint Protection (requer reinicialização)**  

     Selecione **Sim** para desabilitar o filtro de gravação no dispositivo Windows Embedded e reiniciar o dispositivo. Isso confirma a instalação no dispositivo.  

     Se **Não** for especificado, o cliente será instalado em uma sobreposição temporária que será apagada quando o dispositivo for reiniciado. Neste cenário, o cliente Endpoint Protection não é confirmado até que outra instalação confirme alterações no dispositivo. Essa é a configuração padrão.  

-   **Suprimir qualquer reinicialização necessária do computador após o Endpoint Protection ser instalado**  

     Selecione **Verdadeiro** ou **Sim** para suprimir uma reinicialização do computador, se for necessário depois que o cliente Endpoint Protection for instalado.  

    > [!IMPORTANT]  
    >  Se o cliente Endpoint Protection exigir uma reinicialização do computador e essa configuração for definida como **Falsa**, a reinicialização ocorrerá independentemente das janelas de manutenção configuradas.  

-   **Período de tempo permitido durante o qual os usuários podem adiar o reinício necessário para concluir a instalação do Endpoint Protection (horas)**  

     Especifique o número de horas que os usuários podem adiar a reinicialização de um computador se isso for necessário depois da instalação do cliente Endpoint Protection. Esta opção poderá ser configurada apenas se a opção **Suprimir qualquer reinicialização necessária do computador após o Endpoint Protection ser instalado** estiver definida como **Falso**.  

-   **Desabilite fontes alternativas (como o Windows Update, Microsoft Windows Server Update Services ou compartilhamentos UNC) para a atualização da definição inicial em computadores cliente**  

     Selecione **Verdadeiro** ou **Sim** se desejar que o Configuration Manager instale somente a atualização da definição inicial em computadores cliente. Essa configuração pode ser útil para evitar conexões de rede desnecessárias e reduzir a largura de banda da rede durante a instalação inicial da atualização da definição.  

##  <a name="a-namebkmkhardwareinventorydevicesettingsa-hardware-inventory"></a><a name="BKMK_HardwareInventoryDeviceSettings"></a> Inventário de hardware  

-   **Tamanho máximo de arquivo MIF personalizado (KB)**  

     Especifique o tamanho máximo, em KB (quilobytes), permitido para cada arquivo personalizado MIF (Formato de Informações de Gerenciamento) que serão coletados de um cliente durante um ciclo de inventário de hardware. Se algum arquivo MIF exceder este tamanho, ele não será processado ​​pelo Inventário de Hardware do Configuration Manager. Especifique um tamanho entre 1 e 5.000 KB. Por padrão, esse valor é definido como 250 KB. Essa configuração não afeta o tamanho do arquivo de dados de inventário de hardware regular.  

    > [!NOTE]  
    >  Essa configuração só está disponível nas configurações do cliente padrão.  

-   **Classes de inventário de hardware**  

     No Configuration Manager, você pode estender as informações de hardware que coleta dos clientes sem editar manualmente o arquivo sms_def.mof. Clique em **Definir Classes** se desejar estender o Inventário de Hardware do Configuration Manager. Para mais informações, confira [How to configure hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/configure-hardware-inventory.md) (Como configurar o Inventário de Hardware no System Center Configuration Manager).  

-   **Coletar arquivos MIF**  

     Use esta configuração para especificar se os arquivos MIF (Managed Information Format) devem ser coletados de clientes Configuration Manager durante o Inventário de Hardware.  

     Para que um arquivo MIF seja coletado pelo inventário de hardware, ele deve ser colocado no local correto no computador cliente. Por padrão, os arquivos devem ser localizados da seguinte maneira:  

    -   Arquivos IDMIF devem estar localizados na pasta Windows\System32\CCM\Inventory\Idmif.  

    -   Arquivos NOIDMIF devem estar localizados na pasta Windows\System32\CCM\Inventory\Noidmif.  

    > [!NOTE]  
    >  Essa configuração só está disponível nas configurações do cliente padrão.  

##  <a name="a-namebkmkmeteredinternetconnetionssettingsa-metered-internet-connections"></a><a name="BKMK_MeteredInternetConnetionsSettings"></a> Planos de Internet Limitados  
 Você pode gerenciar o modo como os computadores cliente com Windows 8 se comunicam com sites do Configuration Manager quando usam conexões de Internet limitadas. Provedores de Internet ocasionalmente cobram por quantidade de dados que você envia e recebe quando está em uma conexão de Internet limitada.  

> [!NOTE]  
>  A configuração de cliente definida não é aplicada a computadores cliente com Windows 8 nas seguintes situações:  
>   
>  -   O computador está em uma conexão de dados em roaming: o cliente do Configuration Manager não executa operações que exigem que os dados sejam transferidos para sites do Configuration Manager.  
> -   As propriedades de conexão de rede do Windows são configuradas como ilimitadas: o cliente Configuration Manager se comporta como se esta fosse uma conexão de Internet ilimitada e, por isso, transfere os dados para os sites do Configuration Manager.  

-   **Comunicação de cliente em conexões de Internet limitadas**  

     Na lista suspensa, escolha uma das seguintes opções para computadores cliente com Windows 8:  

    -   **Permitir**: todas as comunicações do cliente são permitidas pela conexão de Internet limitada, a menos que o dispositivo cliente esteja usando uma conexão de dados móvel.  

    -   **Limite**: somente as seguintes comunicações do cliente são permitidas pela conexão de Internet limitada:  

        -   Recuperação de política do cliente  

        -   Mensagens de estado do cliente para enviar ao site  

        -   Solicitações de instalação de software usando o catálogo de aplicativos  

        -   Implantações necessárias (quando é atingido o prazo de instalação)  

        > [!IMPORTANT]  
        >  Se um usuário iniciar uma instalação de software por meio do Centro de Software ou do catálogo de aplicativos, estes são sempre permitidos, independentemente das configurações de conexão de Internet limitada.  

         Se o limite de transferência de dados for alcançado para a conexão da Internet limitada, o cliente não tentará mais se comunicar com os sites do Configuration Manager.  

    -   **Bloquear**: o cliente do Configuration Manager não tenta se comunicar com os sites do Configuration Manager quando ele está em uma conexão de Internet limitada. Este é o valor padrão.  

##  <a name="a-namebkmkpowmgmtdevicesettingsa-power-management"></a><a name="BKMK_PowMgmtDeviceSettings"></a> Gerenciamento de energia  

-   **Permitir que os usuários excluam seu dispositivo do gerenciamento de energia**  

     Na lista suspensa, selecione **Verdadeiro** ou **Sim** para permitir que usuários do Centro de Software excluam o computador de quaisquer configurações definidas de gerenciamento de energia.  

-   **Habilitar proxy de ativação**  

     Especifique **Sim** para complementar a configuração Wake On LAN do site quando estiver definida para pacotes unicast.  

     Para mais informações sobre o proxy de ativação, confira [Planejar a ativação de clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  Não habilite o proxy de ativação em uma rede de produção sem primeiro entender como ele funciona e avaliá-lo em um ambiente de teste.  

-   **Número de porta proxy de ativação (UDP)**  

     Mantenha o valor padrão do número de porta que computadores gerenciadores usam para enviar pacotes de ativação a computadores em suspensão ou altere o número para um valor de sua escolha.  

     O número de porta especificado aqui é configurado automaticamente para clientes que executam o Firewall do Windows quando você define a opção **Exceção do Windows Firewall para proxy de ativação** . Se os clientes executam um firewall diferente, você deve configurá-lo manualmente para permitir o número de porta UDP especificado para essa configuração.  

-   **Número de porta Wake On LAN (UDP)**  

     Mantenha o valor padrão 9, a menos que você tenha alterado o número de porta Wake On LAN (UDP) nas **Propriedades**do site, na guia **Portas** .  

    > [!IMPORTANT]  
    >  Esse número deve corresponder ao número nas **Propriedades**do site. Se você alterar esse número em um só lugar, ele não será atualizado automaticamente em outro lugar.  

##  <a name="a-namebkmkremotetoolsdevicesettingsa-remote-tools"></a><a name="BKMK_RemoteToolsDeviceSettings"></a> Ferramentas remotas  

-   **Habilitar o controle remoto em clientes** e **Perfis de exceção do firewall**  

     Selecione se o controle remoto do Configuration Manager está habilitado para todos os computadores cliente que recebem essas configurações do cliente. Clique em **Configurar** para habilitar o controle remoto e, opcionalmente, definir configurações de firewall para permitir que o controle remoto funcione em computadores cliente.  

     O controle remoto está desativado por padrão.  

    > [!IMPORTANT]  
    >  Se as configurações de firewall não estiverem definidas, o controle remoto poderá não funcionar corretamente.  

-   **Os usuários podem alterar as configurações de política ou notificação no Centro de Software**  

     Selecione se os usuários podem alterar as opções de controle remoto do Centro de Software.  

-   **Permitir o controle remoto de um computador autônomo**  

     Selecione se um administrador pode usar o controle remoto para acessar um computador cliente que está desconectado ou bloqueado. Apenas um computador conectado e desbloqueado pode ser controlado remotamente quando essa configuração está desativada.  

-   **Solicitar permissão de Controle Remoto ao usuário**  

     Selecione se o computador cliente exibirá uma mensagem solicitando permissão do usuário antes de permitir uma sessão de controle remoto.  

-   **Conceder permissão de Controle Remoto para o grupo local de administradores**  

     Selecione se os administradores locais no servidor que inicia a conexão de controle remoto pode estabelecer sessões de controle remoto com computadores cliente.  

-   **Nível de acesso permitido**  

     Especifique o nível de acesso de controle remoto que será permitido. Você pode escolher:  

    -   Controle total  

    -   Somente exibição  

    -   Nenhum  

-   **Visualizadores permitidos**  

     Clique em **Definir Visualizadores** para abrir a caixa de diálogo **Definir a Configuração do Cliente** e especifique os nomes dos usuários do Windows que podem estabelecer sessões de controle remoto com computadores cliente.  

-   **Mostrar ícone de notificação de sessão na barra de tarefas**  

     Selecione esta opção para exibir um ícone na barra de tarefas de computadores cliente para indicar se uma sessão de controle remoto está ativa.  

-   **Mostrar barra de conexão da sessão**  

     Selecione esta opção para exibir uma barra de tarefas de conexão da sessão de alta visibilidade em computadores cliente para indicar se uma sessão de controle remoto está ativa.  

-   **Tocar um som no cliente**  

     Selecione esta opção para usar som para indicar quando uma sessão de controle remoto está ativa em um computador cliente. Você pode tocar um som quando a sessão se conecta ou se desconecta, ou você pode tocar um som repetidamente durante a sessão.  

-   **Gerenciar configurações de assistência remota não solicitada**  

     Selecione esta opção para permitir que o Configuration Manager gerencie sessões de assistência remota não solicitada.  

     As sessões de assistência remota não solicitada são aquelas em que o usuário no computador cliente não solicita assistência para iniciar uma sessão.  

-   **Gerenciar configurações de assistência remota solicitada**  

     Selecione esta opção para permitir que o Configuration Manager gerencie sessões de assistência remota solicitada.  

     As sessões de assistência remota solicitada são aquelas em que o usuário no computador cliente envia uma solicitação de assistência remota ao administrador.  

-   **Nível de acesso para assistência remota**  

     Selecione nível de acesso para atribuir a sessões de assistência remota iniciadas no console do Configuration Manager.  

    > [!NOTE]  
    >  O usuário no computador cliente sempre deve conceder permissão para que uma sessão de assistência remota ocorra.  

-   **Gerenciar configurações da Área de Trabalho Remota**  

     Selecione esta opção para permitir que o Configuration Manager gerencie sessões da Área de Trabalho Remota para computadores.  

-   **Permitir que os visualizadores autorizados se conectem usando a conexão de Área de Trabalho Remota**  

     Selecione esta opção para permitir que os usuários especificados na lista de visualizadores autorizados sejam adicionados ao grupo de usuários locais da Área de Trabalho Remota em computadores cliente.  

-   **Exigir autenticação no nível da rede em computadores que executam o sistema operacional Windows Vista e versões posteriores**  

     Selecione esta opção mais segura se deseja usar a autenticação no nível da rede para estabelecer conexões de Área de Trabalho Remota com computadores cliente que executam Windows Vista ou posterior. A autenticação no nível da rede requer menos recursos do computador remoto inicialmente, pois ela conclui a autenticação de usuário antes de estabelecer uma conexão de Área de Trabalho Remota. Esse método é mais seguro porque pode ajudar a proteger o computador contra usuários ou software mal-intencionado e reduz o risco de ataques de negação de serviço.  

##  <a name="a-namebkmksoftwaredeploymentdevicesettingsa-software-deployment"></a><a name="BKMK_SoftwareDeploymentDeviceSettings"></a> Implantação de software  

-   **Reavaliação de agendamento para implantações**  

     Configure um agendamento para quando o Configuration Manager reavalia as regras de requisito para todas as implantações. O valor padrão é a cada 7 dias.  

    > [!IMPORTANT]  
    >  Recomendamos que você não altere esse valor para um valor mais baixo do que o padrão, pois isso pode afetar negativamente o desempenho da rede e dos computadores cliente.  

     Você também pode iniciar essa ação de um computador cliente do Configuration Manager selecionando a ação **Ciclo de Avaliação de Implantação do Aplicativo** na guia **Ações** do **Configuration Manager** no Painel de Controle.  

##  <a name="a-namebkmksoftinventorydevicesettingsa-software-inventory"></a><a name="BKMK_SoftInventoryDeviceSettings"></a> Inventário de software  

-   **Detalhe no relatório de inventário**  

     Especifique o nível de informações de arquivo para o inventário. Você pode inventariar detalhes sobre o arquivo apenas, detalhes sobre o produto associado ao arquivo ou você pode inventariar todas as informações sobre o arquivo.  

-   **Inventariar estes tipos de arquivo**  

     Se desejar especificar os tipos de arquivo para inventariar, clique em **Definir Tipos** e configure o seguinte na caixa de diálogo **Definir a Configuração do Cliente** :  

    > [!NOTE]  
    >  Se várias configurações personalizadas do cliente forem aplicadas a um computador, o inventário retornado pela configuração será mesclado.  

    -   Clique no ícone Novo e adicione um novo tipo de arquivo para inventariar, em seguida, especifique as seguintes informações na caixa de diálogo **Propriedades de Arquivo Inventariado** :  

    -   **Nome** – Forneça um nome para o arquivo que você deseja inventariar. Você pode usar o caractere **\*** para representar qualquer cadeia de caracteres de texto, e o caractere **?** para representar qualquer caractere único. Por exemplo, se você deseja inventariar todos os arquivos com a extensão .doc, especifique o nome do arquivo **\*.doc**.  

    -   **Local** – Clique em **Definir** para abrir a caixa de diálogo **Propriedades de Caminho** . Você pode configurar o inventário de software para pesquisar o arquivo especificado em todos os discos rígidos do cliente, pesquisar um caminho especificado (por exemplo, **C:\Folder**) ou uma variável especificada (por exemplo, *%windir%*) e também pode pesquisar todas as subpastas no caminho especificado.  

    -   **Excluir arquivos criptografados e compactados** – Quando você seleciona esta opção, todos os arquivos que foram compactados ou criptografados não serão inventariados.  

    -   **Excluir arquivos na pasta do Windows** – Quando você seleciona esta opção, todos os arquivos na pasta do Windows e suas subpastas não serão inventariados.  

    -   Clique em **OK** para fechar a caixa de diálogo **Propriedades de Arquivo Inventariado** .  

    -   Adicione todos os arquivos que você deseja inventariar e clique em **OK** para fechar a caixa de diálogo **Definir a Configuração do Cliente** .  

-   **Coletar arquivos**  

     Se você deseja coletar arquivos de computadores cliente, clique em **Definir Arquivos** e configure o seguinte:  

    > [!NOTE]  
    >  Se várias configurações personalizadas do cliente forem aplicadas a um computador, o inventário retornado pela configuração será mesclado.  

    -   Na caixa de diálogo **Definir a Configuração do Cliente** , clique no ícone Novo para adicionar um arquivo a ser coletado.  

    -   Na caixa de diálogo **Propriedades do Arquivo Coletado** , forneça as seguintes informações:  

    -   **Nome** – Forneça um nome para o arquivo que você deseja coletar. Você pode usar o caractere **\*** para representar qualquer cadeia de caracteres de texto, e o caractere **?** para representar qualquer caractere único.  

    -   **Local** – Clique em **Definir** para abrir a caixa de diálogo **Propriedades de Caminho** . Você pode configurar o inventário de software para pesquisar o arquivo que deseja coletar em todos os discos rígidos do cliente, pesquisar um caminho especificado (por exemplo, **C:\Folder**) ou uma variável especificada (por exemplo, *%windir%*) e também pode pesquisar todas as subpastas no caminho especificado.  

    -   **Excluir arquivos criptografados e compactados** – Quando você seleciona esta opção, todos os arquivos que foram compactados ou criptografados não serão coletados.  

    -   **Parar coleção de arquivos quando o tamanho total dos arquivos exceder (KB)** – Especifique o tamanho do arquivo (em KB) depois do qual nenhum dos arquivos especificados em **Nome** será coletado.  

        > [!NOTE]  
        >  O servidor do site coleta as cinco versões alteradas mais recentemente de arquivos coletados e as armazena no *&lt;Diretório de instalação do ConfigMgr\>***\Inboxes\Sinv.box\Filecol**. Se um arquivo não foi alterado desde que o último inventário de software foi coletado, o arquivo não será coletado novamente.  
        >   
        >  Arquivos maiores que 20 MB não são coletados pelo inventário de software.  
        >   
        >  O valor **Tamanho máximo para todos os arquivos coletados (KB)** na caixa de diálogo **Definir a Configuração do Cliente** exibe o tamanho máximo para todos os arquivos coletados. Quando esse tamanho é atingido, a coleção será interrompida. Todos os arquivos já coletados são retidos e enviados para o servidor do site.  

        > [!IMPORTANT]  
        >  Se você configurar o inventário de software para coletar muitos arquivos grandes, isso pode afetar negativamente o desempenho da rede e do servidor do site.  

         Para obter informações sobre como exibir os arquivos coletados, confira [How to use Resource Explorer to view software inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) (Como usar o Gerenciador de Recursos para exibir o inventário de software no System Center Configuration Manager).  

    -   Clique em **OK** para fechar a caixa de diálogo **Propriedades do Arquivo Coletado** .  

    -   Adicione todos os arquivos que você deseja coletar e clique em **OK** para fechar a caixa de diálogo **Definir a Configuração do Cliente** .  

-   **Definir Nomes**  

     Durante o inventário de software, nomes de fabricantes e nomes de produtos são recuperados por meio das informações de cabeçalho de arquivos instalados em clientes no site. Como esses nomes nem sempre são padronizados nas informações de cabeçalho do arquivo, quando você vê as informações de inventário de software no Gerenciador de Recursos ou executa consultas, diferentes versões do mesmo fabricante ou nome do produto podem aparecer às vezes. Para padronizar esses nomes, clique em **Definir Nomes** e configure o seguinte na caixa de diálogo **Definir a Configuração do Cliente** :  

    -   **Tipo de nome:** o inventário de software coleta informações sobre produtos e fabricantes. Na lista suspensa, selecione se você quer configurar nomes de exibição para um **Fabricante** ou um **Produto**.  

    -   **Nome de exibição:** especifica o nome de exibição que você deseja usar em vez dos nomes na lista **Nomes inventariados** . Você pode clicar no ícone Novo para especificar um novo nome de exibição.  

    -   **Nomes inventariados:** – Clique no ícone Novo para adicionar um novo nome inventariado, que será substituído no inventário de software pelo nome selecionado na lista **Nome de exibição** . Você pode adicionar vários nomes que serão substituídos.  

##  <a name="a-namebkmksoftwareupdatesdevicesettinga-software-updates"></a><a name="BKMK_SoftwareUpdatesDeviceSetting"></a> Atualizações de software  

-   **Habilitar atualizações de software em clientes**  

     Use essa configuração para habilitar atualizações de software em clientes do Configuration Manager. Se você desmarcar essa configuração, o Configuration Manager removerá as políticas de implantação existentes do cliente. Quando você reativa essa configuração, o cliente baixa a política de implantação atual.  

    > [!IMPORTANT]  
    >  Quando você desmarca essa configuração, as políticas de NAP e de conformidade que dependem da configuração do dispositivo de atualizações de software não funcionam mais.  

-   **Agendamento de verificação de atualização de software**  

     Use essa configuração para especificar com que frequência o cliente inicia uma verificação de avaliação de conformidade de atualização de software. A verificação da avaliação de conformidade determina o estado das atualizações de software no cliente (por exemplo, necessárias ou instaladas). Para mais informações sobre a avaliação de conformidade, confira [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance) (Avaliação de conformidade de atualizações de software).  

     Por padrão, um agendamento simples é usado e a verificação de conformidade é iniciada a cada 7 dias. Você pode optar por criar uma agenda personalizada para especificar uma data e hora exatas de início, escolher se quer usar UTC ou horário local, e configurar o intervalo recorrente para um dia específico da semana.  

    > [!NOTE]  
    >  Se você especificar um intervalo de menos de 1 dia, o Configuration Manager assumirá 1 dia automaticamente como padrão.  

    > [!WARNING]  
    >  A hora de início real em computadores cliente é a hora de início mais um período de tempo aleatório de até 2 horas. Isso evita que os computadores cliente iniciem a verificação e conectem ao WSUS (Windows Server Update Services) no servidor ativo de ponto de atualização de software ao mesmo tempo.  

-   **Reavaliação de implantação da agenda**  

     Use essa definição para configurar quantas vezes o Agente Cliente de Atualizações de Software reavalia as atualizações de software para o status de instalação em computadores cliente do Configuration Manager. Quando as atualizações de software que foram instalados anteriormente não são mais encontradas em computadores cliente, e ainda são necessárias, elas são reinstaladas. A agenda de reavaliação da implantação deverá ser ajustada com base na política da empresa para conformidade da atualização de software, se os usuários tiverem a capacidade de desinstalar atualizações de software, e assim por diante, e com a consideração de que cada ciclo de reavaliação de implantação resulte em alguma atividade de rede e CPU de computador do cliente. Por padrão, um agendamento simples é usado e a verificação de reavaliação da implantação é iniciada a cada 7 dias.  

    > [!NOTE]  
    >  Se você especificar um intervalo de menos de 1 dia, o Configuration Manager assumirá 1 dia automaticamente como padrão.  

-   **Quando qualquer prazo de atualização de software for alcançado, instale todas as outras implantações de atualização de software com um prazo dentro de um período especificado**  

     Use essa configuração para instalar todas as atualizações de software em implementações necessárias que têm prazos dentro de um período especificado. Quando um prazo é alcançado para uma implantação de atualização de software necessária, a instalação inicia nos clientes das atualizações de software na implantação. Essa configuração determina se deve ser iniciada também a instalação das atualizações de software definidas em outras implantações necessárias que têm um prazo configurado dentro do período especificado.  

     Use essa configuração para agilizar a instalação da atualização de software para atualizações de software necessárias, aumentar potencialmente a segurança, diminuir potencialmente as notificações de exibição e diminuir potencialmente as reinicializações do sistema em computadores cliente. Por padrão, essa configuração não está habilitada.  

-   **Período de tempo para o qual todas as implantações pendentes com prazo nesse período também serão instaladas**  

     Use essa configuração para especificar o período de tempo da configuração anterior. Você pode inserir um valor entre 1 e 23 horas e de 1 a 365 dias. Por padrão, essa configuração é definida para 7 dias.  

##  <a name="a-namebkmkuserdeviceaffinitydevicesettingsa-user-and-device-affinity"></a><a name="BKMK_UserDeviceAffinityDeviceSettings"></a> Afinidade de dispositivo e de usuário  

-   **Limite de uso de afinidade de dispositivo do usuário (minutos)**  

     Especifique o número de minutos antes que o Configuration Manager crie um mapeamento de afinidade de dispositivo de usuário.  

-   **Limite de uso de afinidade de dispositivo do usuário (dias)**  

     Especifique o número de dias nos quais o limite de afinidade com base no uso é medido.  

    > [!NOTE]  
    >  Por exemplo, se o **Limite de uso da afinidade de dispositivo de usuário (minutos)** for especificado como **60** minutos e o **Limite de uso da afinidade de dispositivo de usuário (dias)** for especificado como **5** dias, o usuário deverá utilizar o dispositivo por 60 minutos em um período de 5 dias para criar automaticamente a afinidade de dispositivo de usuário.  

-   **Configurar automaticamente a afinidade de dispositivo de usuário por meio de dados de uso**  

     Selecione **Verdadeiro** ou **Sim** para habilitar o Configuration Manager para criar automaticamente afinidades de dispositivo de usuário com base nas informações de uso coletadas.  

## <a name="client-cache-settings"></a>Configuração do cache do cliente

- **Configurar o tamanho do cache do cliente**

  A pasta de cache do cliente é usada em computadores Windows para armazenar arquivos temporários usados para instalar aplicativos e programas. A partir da versão 1606, selecione **Sim** para especificar o tamanho da pasta de cache de cliente usando as configurações **Tamanho máximo de cache**. Se definido como **Não**, a pasta de cache do cliente padrão será 5120 MB.

  Outras propriedades de cache do cliente podem ser definidas durante a instalação do cliente. Para obter mais informações, consulte [Configure the Client Cache for Configuration Manager Clients](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

- **Tamanho máximo de cache (MB)**

  A partir da versão 1606, especifique o tamanho máximo da pasta de cache do cliente em megabytes.

- **Tamanho máximo do cache (percentual do disco)** (começando na versão 1606)

  A partir da versão 1606, especifique o tamanho máximo da pasta de cache do cliente em um percentual do tamanho do disco.

##  <a name="a-namebkmkmobiledevicesusersettingsa-mobile-devices"></a><a name="BKMK_MobileDevicesUserSettings"></a> Dispositivos móveis  

-   **Perfil de registro do dispositivo móvel**  

     Para definir essa configuração, você deve primeiro definir como **Verdadeiro** a configuração de usuário do dispositivo móvel **Permitir que os usuários registrem dispositivos móveis**. Então você clica em **Definir Perfil** para especificar um perfil de registro que contém informações sobre o modelo do certificado a ser usado durante o processo de registro, o site que contém um ponto de registro e o ponto proxy do registro, e o site que irá gerenciar o dispositivo após o registro.  

    > [!IMPORTANT]  
    >  Verifique se você configurou um modelo de certificado a ser usado para registro do dispositivo móvel antes de configurar essa opção.  

##  <a name="a-namebkmkenrollmentusersettingsa-enrollment"></a><a name="BKMK_EnrollmentUserSettings"></a> Registro  

-   **Perfil de registro do dispositivo móvel**  

     Para definir essa configuração, você deve primeiro definir como **Sim** a configuração de usuário do registro **Permitir que os usuários registrem dispositivos móveis e computadores Mac**. Então você clica em **Definir Perfil** para especificar um perfil de registro que contém informações sobre o modelo do certificado a ser usado durante o processo de registro, o site que contém um ponto de registro e o ponto proxy do registro, e o site que irá gerenciar o dispositivo após o registro.  

    > [!IMPORTANT]  
    >  Verifique se você configurou um modelo de certificado a ser usado para registro do dispositivo móvel ou registro de certificado de cliente Mac antes de configurar essa opção.  

##  <a name="a-namebkmkuserdeviceaffinityusersettingsa-user-and-device-affinity"></a><a name="BKMK_UserDeviceAffinityUserSettings"></a> Afinidade de dispositivo e de usuário  

-   **Permitir ao usuário definir os seus dispositivos primários**  

     Especificar se os usuários estão autorizados a identificar seus próprios dispositivos primários do Catálogo de aplicativos, guia **Meus Dispositivos** .  



<!--HONumber=Nov16_HO1-->


