---

title: "Planejar atualizações de software | System Center Configuration Manager"
description: "É essencial ter um plano para a infraestrutura de ponto de atualização de software antes de usar atualizações de software em um ambiente de produção do System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 69f2c9c3c098013679e12d8578a780130adb94be


---

# <a name="plan-for-software-updates-in-system-center-configuration-manager"></a>Planejar atualizações de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de usar atualizações de software em um ambiente de produção do System Center Configuration Manager, é importante que você passe pelo processo de planejamento. Ter um bom plano para a infraestrutura de ponto de atualização de software é fundamental para uma implementação bem-sucedida das atualizações de software.

## <a name="capacity-planning-recommendations-for-software-updates"></a>Recomendações de planejamento de capacidade para atualizações de software  
 Você pode usar as seguintes recomendações como uma linha de base que pode ajudá-lo a determinar as informações para o planejamento de capacidade de atualizações de software apropriadas para sua organização. Os requisitos de capacidade real podem variar das recomendações listadas neste tópico dependendo dos seguintes critérios: o ambiente de rede específico, o hardware usado para hospedar o sistema de sites do ponto de atualização de software, o número de clientes instalados e as funções do sistema de sites instaladas no servidor.  

###  <a name="a-namebkmksumcapacitya-capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> Planejamento de capacidade para o ponto de atualização de software  
 O número de clientes com suporte depende da versão do WSUS (Windows Server Update Services) executada no ponto de atualização de software e também depende de se a função do sistema de sites do ponto de atualização de software coexiste ou não com outra função do sistema de sites:  

-   O ponto de atualização de software pode dar suporte a até 25.000 clientes quando o WSUS é executado no computador do ponto de atualização de software e quando o ponto de atualização de software coexiste com outra função do sistema de sites.  

-   O ponto de atualização de software pode dar suporte a até 150.000 clientes quando o computador atende aos requisitos do WSUS para dar suporte a esse número de clientes.   
    Por padrão, o Configuration Manager não dá suporte à configuração de pontos de atualização de software como clusters de NLB. No entanto, é possível usar o SDK do Configuration Manager para configurar até quatro pontos de atualização de software em um cluster de NLB.  

### <a name="capacity-planning-for-software-updates-objects"></a>Planejamento de capacidade para objetos de atualizações de software  
 Use as seguintes informações de capacidade para planejar objetos de atualizações de software.  

-   **Limite de 1000 atualizações de software em uma implantação**  

     É necessário limitar o número de atualizações de software a 1000 para cada implantação de atualização de software. Ao criar uma regra de implantação automática, especifique os critérios que limitam o número de atualizações de software que serão retornadas. A regra de implantação automática falha quando os critérios que você especifica retornam mais de 1000 atualizações de software. É possível verificar o status da regra de implantação automática no nó **Regras de Implantação Automática** no console do Configuration Manager. Ao implantar atualizações de software manualmente, não selecione mais de 1.000 atualizações para implantar.  

     Você também precisa limitar o número de atualizações de software a 1.000 em uma linha de base de configuração. Para obter mais informações, consulte [Criar linhas de base de configuração](../../compliance/deploy-use/create-configuration-baselines.md).

##  <a name="a-namebkmksupinfrastructurea-determine-the-software-update-point-infrastructure"></a><a name="BKMK_SUPInfrastructure"></a> Determinar a infraestrutura do ponto de atualização de software  
 O site de administração central e todos os sites primários filho devem ter um ponto de atualização de software onde você implantará atualizações de software. Ao planejar a infraestrutura de ponto de atualização de software, você precisa determinar as seguintes dependências: onde instalar o ponto de atualização de software do site; quais sites exigem um ponto de atualização de software que aceita comunicação de clientes baseados na Internet; se você configurará o ponto de atualização de software como um cluster NLB e se você precisa de um ponto de atualização de software em um site secundário. Use as seções a seguir para determinar a infraestrutura do ponto de atualização de software.  

> [!IMPORTANT]  
>  Para obter informações sobre as dependências internas e externas necessárias para as atualizações de software, consulte [Pré-requisitos para atualizações de software](prerequisites-for-software-updates.md).  

 É possível adicionar vários pontos de atualização de software em um site primário do Configuration Manager. A capacidade de ter vários pontos de atualização de software em um site fornece tolerância a falhas sem exigir a complexidade do NLB. No entanto, o failover que você recebe com vários pontos de atualização de software não é tão robusto quanto o NLB para balanceamento de carga puro, mas foi projetado para tolerância a falhas. Além disso, o design de failover do ponto de atualização de software é diferente do modelo aleatório puro de usado no design de pontos de gerenciamento. Ao contrário do design de pontos de gerenciamento, nos pontos de atualização de software existem custos de desempenho e rede e do cliente associados à mudança para um novo ponto de atualização de software. Quando o cliente muda para um novo servidor do WSUS para verificar atualizações de software, o resultado é um aumento no tamanho do catálogo e no lado do cliente associado, e nas demandas de desempenho de rede. Portanto, o cliente preserva a afinidade com o último ponto de atualização de software para o qual ele verificou com êxito.  

 O primeiro ponto de atualização de software que você instala em um site primário é a origem da sincronização de todos os pontos de atualização de software que você adiciona ao site primário. Depois de adicionar os pontos de atualização de software e iniciar a sincronização das atualizações de software, você poderá exibir o status dos pontos de atualização de software e a origem da sincronização no nó **Status da Sincronização do Ponto de Atualização de Software** no espaço de trabalho **Monitoramento** .  

 Quando ocorre falha em um ponto de atualização de software e esse ponto é configurado como a origem da sincronização para outros pontos de atualização de software, você deve remover manualmente o ponto de atualização de software com falha e selecionar um novo ponto para usar como origem da sincronização. Para obter mais informações sobre como remover um ponto de atualização de software, consulte [Remover a função de sistema de sites do ponto de atualização de software](../get-started/remove-a-software-update-point.md).  

###  <a name="a-namebkmksuplista-software-update-point-list"></a><a name="BKMK_SUPList"></a> Lista de pontos de atualização de software  
 O Configuration Manager fornece ao cliente uma lista de pontos de atualização de software nos seguintes cenários: quando um novo cliente recebe a política para habilitar atualizações de software ou quando um cliente não consegue entrar em contato com seu ponto de atualização de software e precisa mudar para outro ponto de atualização de software. O cliente seleciona aleatoriamente um ponto de atualização de software na lista e prioriza os pontos de atualização de software que estão na mesma floresta. O Configuration Manager oferece aos clientes uma lista diferente, dependendo do tipo de cliente.  

-   **Clientes baseados em intranet**: recebem uma lista de pontos de atualização de software que você pode configurar para permitir conexões somente da intranet ou uma lista de pontos de atualização de software que permitem conexões do cliente na Internet e na intranet.  

-   **Clientes baseados em internet**: recebem uma lista de pontos de atualização de software que você pode configurar para permitir conexões somente da internet ou uma lista de pontos de atualização de software que permitem conexões do cliente na Internet e na intranet.  

###  <a name="a-namebkmksupswitchinga-software-update-point-switching"></a><a name="BKMK_SUPSwitching"></a> Comutação de ponto de atualização de software  
 Se você tiver vários pontos de atualização de software e um deles falhar ou ficar indisponível, os clientes irão se conectar a um ponto de atualização de software diferente e continuarão verificando as atualizações de software mais recentes. Quando um cliente for atribuído pela primeira vez a um ponto de atualização de software, ele permanecerá atribuído a esse ponto de atualização de software a menos que ocorra falha na verificação de atualizações de software nesse ponto de atualização de software.  

 A verificação de atualizações de software pode falhar com um número de repetição diferente e códigos de erro sem repetição. Quando há falha na verificação para repetir um código de erro, o cliente inicia o processo de repetição para verificar as atualizações de software no ponto de atualização de software. As condições de alto nível que resultam em na repetição de um código de erro geralmente ocorrem porque o servidor do WSUS está indisponível ou temporariamente sobrecarregado. O cliente usa o processo a seguir quando ocorre falha para verificar se há atualizações de software:  

1.  O cliente verifica atualizações de software no horário agendado ou quando ele é iniciado através do painel de controle no cliente, ou usando o SDK. Se a verificação falhar, o cliente aguardará 30 minutos para repetir a verificação e usará o mesmo ponto de atualização de software.  

2.  O cliente tenta novamente por no mínimo quatro vezes em intervalos de 30 minutos. Após a quarta falha, e depois de aguardar mais dois minutos, o cliente passará para o próximo ponto de atualização de software na lista de pontos de atualização de software.  

3.  Após uma verificação bem-sucedida, o cliente continuará a se conectar ao ponto de atualização de software.  

 A lista a seguir fornece informações adicionais que você pode considerar para repetição do ponto de atualização de software e mudança de cenários:  

-   Se um cliente for desconectado da intranet corporativa e falhar para verificar atualizações de software, ele não mudará para outro ponto de atualização de software. Essa é uma falha esperada, pois o cliente não pode chegar à rede corporativa ou ao ponto de atualização de software que permite conexão da intranet. O cliente do Configuration Manager determina a disponibilidade do ponto de atualização de software da intranet.  

-   Se o gerenciamento de clientes baseado na Internet estiver habilitado e existirem vários pontos de atualização de software configurados para aceitar comunicação de clientes na Internet, o processo de mudança acompanhará o processo de repetição padrão descrito no cenário anterior.  

-   Se o processo de verificação foi iniciado, mas o cliente estava desligado antes da conclusão da verificação, ele não é considerado uma falha de verificação e não conta como uma das quatro repetições.  

###  <a name="a-namebkmkmanuallyswitchsupsamanually-switch-clients-to-a-new-software-update-point"></a><a name="BKMK_ManuallySwitchSUPs"></a>Mudar manualmente clientes para um novo ponto de atualização de software
A partir da versão 1606 do Configuration Manager, você pode habilitar a opção para clientes do Configuration Manager mudarem para um novo ponto de atualização de software quando houver problemas com o ponto de atualização de software ativo. Essa opção resulta em alterações somente quando um cliente recebe vários pontos de atualização de software de um ponto de gerenciamento.  

Habilite essa opção em uma coleção de dispositivos ou em um conjunto de dispositivos selecionados. Uma vez habilitada, os clientes procurarão outro ponto de atualização de software na próxima verificação. Dependendo de suas definições de configuração do WSUS (classificações de atualização, produtos, se os pontos de atualização de software compartilham um banco de dados do WSUS etc.), mudar para um novo ponto de atualização de software gerará tráfego de rede adicional. Portanto, você deve usar essa opção apenas quando for necessário.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Para habilitar a opção de alternar pontos de atualização de software  

1.  No console do Configuration Manager, vá até **Ativos e Conformidade > Visão Geral > Coleções de Dispositivos**.  

2.  Na guia **Início** , no grupo **Coleção** , clique em **Notificação do Cliente**e em **Alternar para o próximo ponto de atualização de software**.  


###  <a name="a-namebkmksupcrossforesta-software-update-points-in-an-untrusted-forest"></a><a name="BKMK_SUP_CrossForest"></a> Pontos de atualização de software em uma floresta não confiável  
 Você pode criar um ou mais pontos de atualização de software em um site para dar suporte a clientes em uma floresta não confiável. Para adicionar um ponto de atualização de software em outra floresta, você deve primeiro instalar e configurar um servidor do WSUS na floresta. Depois, inicie o assistente para adicionar um servidor do site do Configuration Manager com a função de sistema de sites do ponto de atualização de software. No assistente, defina as seguintes configurações para se conectar com êxito ao WSUS na floresta não confiável:  

-   Especifique uma conta de Instalação do Sistema de Site que possa acessar o servidor do WSUS na floresta.  

-   Especifique a conta de Conexão do Servidor do WSUS a ser usada para se conectar ao servidor do WSUS.  

 Por exemplo, você tem um site primário na floresta A com dois pontos de atualização de software (SUP01 e SUP02). Além disso, para o mesmo site primário, você tem dois pontos de atualização de software (SUP03 e SUP04) na floresta B. Quando a mudança ocorre nesse exemplo, os pontos de atualização de software da mesma floresta como cliente são priorizados primeiro.  

###  <a name="a-namebkmkwsussyncsourcea-use-an-existing-wsus-server-as-the-synchronization-source-at-the-top-level-site"></a><a name="BKMK_WSUSSyncSource"></a> Usar um servidor do WSUS existente como a origem da sincronização no site de nível superior  
 Normalmente, o site de nível superior na sua hierarquia é configurado para sincronizar metadados de atualizações de software com o Microsoft Update. Quando a política de segurança corporativa não permite acesso à Internet do site de nível superior, você pode configurar a origem da sincronização do site de nível superior para usar um servidor do WSUS existente que não esteja em sua hierarquia do Configuration Manager. Por exemplo, você pode ter um servidor do WSUS instalado no rede de perímetro com acesso à Internet, mas o site de nível superior não pode. Você pode configurar o servidor do WSUS no rede de perímetro como origem de sincronização para metadados de atualizações de software. Você precisa verificar se o servidor do WSUS no DMZ sincroniza atualizações de software que atendem aos critérios necessários em sua hierarquia do Configuration Manager. Caso contrário, o site de nível superior pode não sincronizar as atualizações de software que você espera. Ao instalar o ponto de atualização de software, configure uma conta de conexão do WSUS com acesso ao servidor do WSUS no rede de perímetro e confirme se o firewall permite tráfego para as portas apropriadas. Para obter mais informações, veja as [portas usadas pelo ponto de atualização de software para a origem de sincronização](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  

###  <a name="a-namebkmknlbsupsp1a-software-update-point-configured-to-use-an-nlb"></a><a name="BKMK_NLBSUPSP1"></a> Ponto de atualização de software configurado para usar um NLB  
 Provavelmente, a mudança de ponto de atualização de software lidará com suas necessidades de tolerância a falhas. Entretanto, o NLB é mais robusto do que o failover do ponto de atualização de software para balanceamento de carga puro e pode aumentar a confiabilidade e o desempenho de uma rede. Embora não haja uma opção no console do Configuration Manager para configurar o ponto de atualização de software para usar o NLB, você tem a opção de configurar o NLB usando o cmdlet Set-CMSoftwareUpdatePoint PowerShell. Para obter mais informações sobre o cmdlet Set-CMSoftwareUpdatePoint do PowerShell, consulte [Set-CMSoftwareUpdatePoint](http://go.microsoft.com/fwlink/?LinkId=276834).

###  <a name="a-namebkmksupsecsitea-software-update-point-on-a-secondary-site"></a><a name="BKMK_SUPSecSite"></a> Ponto de atualização de software em um site secundário  
 O ponto de atualização de software é opcional em um site secundário. Quando você instala um ponto de atualização de software em um site secundário, o banco de dados do WSUS é configurado como uma réplica do ponto de atualização de software padrão no site primário pai. Você pode instalar apenas um ponto de atualização de software em um site secundário. Os dispositivos atribuídos a um site secundário são configurados para usar um ponto de atualização de software no site pai quando um ponto de atualização de software não está instalado no site secundário. Geralmente, você instalará um ponto de atualização de software em um site secundário quando houver largura de banda de rede limitada entre os dispositivos atribuídos ao site secundário e os pontos de atualização de software no site primário pai, ou quando o ponto de atualização de software se aproximar do limite de capacidade. Após a instalação e configuração de um ponto de atualização de software com êxito no site secundário, uma política de todo o site será atualizada para computadores cliente atribuídos ao site, e eles começarão a usar o novo ponto de atualização de software.  

##  <a name="a-namebkmksupinstallationa-plan-for-software-update-point-installation"></a><a name="BKMK_SUPInstallation"></a> Planejar a instalação do ponto de atualização de software  
 Para criar uma função de sistema de sites no ponto de atualização de software no Configuration Manager, existem vários requisitos que você deve levar em consideração dependendo de sua infraestrutura do Configuration Manager. Quando você configura o ponto de atualização de software para se comunicar usando SSL, esta sessão é especificamente importante para revisão, pois você deve seguir etapas adicionais para os pontos de atualização de software na hierarquia que funcionará corretamente. Esta seção fornece informações sobre as etapas que você deve seguir para planejar e preparar com êxito a instalação do ponto de atualização de software.  

###  <a name="a-namebkmksupsystemrequirementsa-requirements-for-the-software-update-point"></a><a name="BKMK_SUPSystemRequirements"></a> Requisitos para o ponto de atualização de software  
 A função de sistema de sites do ponto de atualização de software deve ser instalada em um sistema de sites que atenda aos requisitos mínimos do WSUS e às configurações com suporte para sistemas de sites do Configuration Manager.  

-   Para obter mais informações sobre os requisitos mínimos da função de servidor do WSUS no Windows Server 2012, consulte [Avaliar considerações e requisitos de sistema](https://technet.microsoft.com/library/hh852344.aspx#BKMK_1.1) na biblioteca de documentação do Windows Server 2012.  

-   Para obter mais informações sobre as configurações com suporte para sistemas de sites do Configuration Manager, consulte [Pré-requisitos de site e sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

###  <a name="a-namebkmkplanningforwsusa-plan-for-wsus-installation"></a><a name="BKMK_PlanningForWSUS"></a> Planejar a instalação do WSUS  
 As atualizações de software requerem que uma versão com suporte do WSUS esteja instalada em todos os servidores do sistema de site que você configura para a função do sistema de site do ponto de atualização de software. Além disso, quando você não instalar o ponto de atualização de software no servidor do site, deverá instalar o Console de Administração do WSUS computador do servidor do site se ainda não estiver instalado. Isso permite que o servidor do site se comunique com o WSUS executado no ponto de atualização de software.  

 Quando usa o WSUS no Windows Server 2012, você precisa configurar permissões adicionais para permitir que o **Configuration Manager do WSUS** no Configuration Manager se conecte ao WSUS, a fim de executar verificações de integridade periódicas. Escolha uma das opções a seguir para configurar as permissões:  

-   Adicione a conta **SYSTEM** ao grupo **Administradores do WSUS**  

-   Adicione a conta **NT AUTHORITY\SYSTEM** como um usuário para o banco de dados do WSUS (SUSDB) e configure um mínimo de associação de função do banco de dados do serviço Web  

 Para obter mais informações sobre como instalar o WSUS no Windows Server 2012, consulte [Install the WSUS Server Role (Instalar a função de servidor do WSUS)](http://go.microsoft.com/fwlink/p/?LinkId=272355) na biblioteca de documentação do Windows Server Update Services 2012.  

 Quando você instalar mais de um ponto de atualização de software em um site primário, use o mesmo banco de dados do WSUS para cada ponto de atualização de software na mesma floresta do Active Directory. Se você compartilhar o mesmo banco de dados, ele atenuará significativamente, mas não eliminará completamente o impacto de desempenho à rede e ao cliente que você pode experimentar quando os clientes mudam para um novo ponto de atualização de software. Uma verificação delta ainda ocorre quando um cliente muda para a um novo ponto de atualização de software que compartilha um banco de dados com o ponto de atualização de software antigo, mas a verificação é bem menor do que seria se o servidor do WSUS tivesse o próprio banco de dados.  

####  <a name="a-namebkmkcustomwebsitea-configure-wsus-to-use-a-custom-web-site"></a><a name="BKMK_CustomWebSite"></a> Configurar o WSUS para usar um site personalizado  
 Ao instalar o WSUS, você tem a opção de usar o site padrão do IIS ou criar um site do WSUS personalizado. Crie um site personalizado para o WSUS de forma que o IIS hospede os serviços do WSUS em um site virtual dedicado, em vez de compartilhar o mesmo site usado por outros sistemas de sites do Configuration Manager ou outros aplicativos. Isso é especialmente verdadeiro quando você instala a função do sistema de site do ponto de atualização de software no servidor do site. Ao executar o WSUS no Windows Server 2012, o WSUS é configurado por padrão para usar a porta 8530 para HTTP e a porta 8531 para HTTPS. É necessário especificar essas configurações de porta para criar o ponto de atualização de software no site.  

####  <a name="a-namebkmkwsusinfrastructurea-use-an-existing-wsus-infrastructure"></a><a name="BKMK_WSUSInfrastructure"></a> Usar uma infraestrutura existente do WSUS  
 Você pode usar um servidor do WSUS que estava ativo no seu ambiente antes da instalação do Configuration Manager. Quando o ponto de atualização de software for configurado, você deve especificar as configurações de sincronização. O Configuration Manager se conecta ao WSUS que é executado no ponto de atualização de software e configura o servidor do WSUS com as mesmas configurações. Quando o servidor do WSUS foi previamente sincronizado com produtos ou classificações que você não configurou como parte das configurações de sincronização do ponto de atualização de software, os metadados de atualizações de software para os produtos e as classificações são sincronizados para todos os metadados de atualizações no banco de dados do WSUS, independentemente das configurações de sincronização do ponto de atualização de software. Isso pode resultar em metadados de atualizações de software inesperados no banco de dados do site. Você experimentará o mesmo comportamento ao adicionar produtos ou classificações diretamente no console de administração do WSUS, e logo em seguida iniciar a sincronização. A cada hora, por padrão, o Configuration Manager se conecta ao WSUS que é executado no ponto de atualização de software e redefine as configurações que foram modificadas fora do Configuration Manager.  

 As atualizações de software que não atenderem aos produtos e às classificações especificadas nas configurações de sincronização serão ajustadas para expirar e depois serão removidas do banco de dados do site.  

####  <a name="a-namebkmkwsusasreplicaa-configure-wsus-as-a-replica-server"></a><a name="BKMK_WSUSAsReplica"></a> Configurar o WSUS como um servidor de réplica  
 Quando você cria uma função de sistema de ponto de atualização de software em um servidor do site primário, não pode usar um servidor do WSUS que está configurado como uma réplica. Quando o servidor do WSUS é configurado como uma réplica, o Configuration Manager não configura o servidor do WSUS e a sincronização do WSUS também falha. Quando um ponto de atualização de software é criado em um site secundário, o Configuration Manager configura o WSUS para ser um servidor de réplica do WSUS que é executado no ponto de atualização de software no site primário pai. O primeiro ponto de atualização de software instalado em um site primário é o ponto de atualização de software padrão. Pontos de atualização de software adicionais no site são configurados como réplicas do ponto de atualização de software padrão.  

####  <a name="a-namebkmkwsusandssla-decide-whether-to-configure-wsus-to-use-ssl"></a><a name="BKMK_WSUSandSSL"></a> Decidir se o WSUS deve ser configurado para usar SSL  
 Você pode usar o protocolo SSL para ajudar a proteger o WSUS que é executado no ponto de atualização de software. O WSUS usa o SSL para autenticar computadores cliente e servidores de WSUS downstream para o servidor do WSUS. Além disso, o WSUS usa SSL para criptografar metadados de atualização de software. Quando você opta por proteger o WSUS com SSL, deve preparar o servidor do WSUS antes de instalar o ponto de atualização de software.  

 Quando você instala e configura o ponto de atualização de software, deve selecionar a configuração **Habilitar comunicações SSL para o servidor do WSUS** . Caso contrário, o Configuration Manager configurará o WSUS para não usar SSL. Quando você habilita o SSL para o WSUS executado em um ponto de atualização de software, o WSUS executado no ponto de atualização de software de quaisquer sites filhos também deve ser configurado para usar SSL.  

###  <a name="a-namebkmkconfigurefirewallsa-configure-firewalls"></a><a name="BKMK_ConfigureFirewalls"></a> Configurar firewalls  
 Atualizações de software em um site de administração central do Configuration Manager se comunicam com o WSUS que é executado no ponto de atualização de software que, por sua vez, se comunica com a origem da sincronização para sincronizar metadados de atualizações de software. Pontos de atualização de software em um site filho comunicam-se com o ponto de atualização de software no site pai. Quando há mais de um ponto de atualização de software em um site primário, os pontos de atualização de software adicionais devem se comunicar com o primeiro ponto de atualização de software instalado no site, que é o ponto de atualização de software padrão.  

 O firewall pode precisar ser configurado para aceitar as portas HTTP ou HTTPS usadas pelo WSUS nos seguintes cenários: quando há um firewall corporativo entre o ponto de atualização de software do Configuration Manager e a Internet; quando há um ponto de atualização de software e sua origem de sincronização upstream ou quando há pontos de atualização de software adicionais. A conexão com o Microsoft Update é sempre configurada para usar a porta 80 para HTTP e a porta 443 para HTTPS. Você pode usar uma porta personalizada para a conexão do WSUS que é executado no ponto de atualização de software em um site filho e o WSUS que é executado no ponto de atualização de software no site pai. Quando sua política de segurança não permitir a conexão, é necessário usar o método de sincronização de exportação e importação. Para obter mais informações, consulte a seção [Origem da sincronização](#BKMK_SyncSource) neste tópico. Para obter mais informações sobre as portas usadas pelo WSUS, consulte [Como determinar as configurações de porta usadas pelo WSUS no System Center Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  

#### <a name="restrict-access-to-specific-domains"></a>Restringir o acesso a domínios específicos  
 Se a sua organização não permite que portas e protocolos sejam abertos a todos os endereços no firewall entre o ponto ativo de atualização de software e a Internet, você pode restringir o acesso aos seguintes domínios, de modo que o WSUS e as Atualizações Automáticas possam se comunicar com o Microsoft Update:  

-   http://windowsupdate.microsoft.com

-   http://*.windowsupdate.microsoft.com  

-   https://*.windowsupdate.microsoft.com  

-   http://*.update.microsoft.com  

-   https://*.update.microsoft.com  

-   http://*.windowsupdate.com  

-   http://download.windowsupdate.com  

-   http://download.microsoft.com  

-   http://*.download.windowsupdate.com  

-   http://test.stats.update.microsoft.com  

-   http://ntservicepack.microsoft.com  

 Talvez seja necessário adicionar os seguintes endereços ao firewall localizado entre os dois sistemas de sites nos seguintes casos: se os sites filho tiverem um ponto de atualização de software ou se existir um ponto de atualização de software baseado na Internet remoto ativo em um site:  

 **Ponto de atualização de software no site filho**  

-   http://<*FQDN do ponto de atualização de software no site filho*>  

-   https://<*FQDN do ponto de atualização de software no site filho*>  

-   http://<*FQDN do ponto de atualização de software no site pai*>  

-   https://<*FQDN do ponto de atualização de software no site pai*>  

##  <a name="a-namebkmksyncsettingsa-plan-for-synchronization-settings"></a><a name="BKMK_SyncSettings"></a> Planejar as configurações de sincronização  
 A sincronização de atualizações de software no Configuration Manager é o processo de recuperar metadados de atualizações de software com base em critérios definidos. O site de nível superior na hierarquia, o site da administração central ou site primário autônomo sincroniza atualizações de software do Microsoft Update. Você tem a opção de configurar o ponto de atualização de software no site de nível superior para ser sincronizado com um servidor do WSUS existente, que não está na hierarquia do Configuration Manager. Os sites primário filhos sincronizam metadados de atualizações de software a partir do ponto de atualização de software no site de administração central. Para instalar e configurar um ponto de atualização de software, use esta seção para planejar as configurações de sincronização.  

###  <a name="a-namebkmksyncsourcea-synchronization-source"></a><a name="BKMK_SyncSource"></a> Origem de sincronização  
 As configurações de origem da sincronização para o ponto de atualização de software especificam o local onde o ponto de atualização de software recupera metadados de atualizações de software, e se os eventos de relatório do WSUS são criados durante o processo de sincronização.  

-   **Origem da sincronização:** o ponto de atualização de software no site de nível superior configura a origem da sincronização para o Microsoft Update por padrão. Você tem a opção de sincronizar o site de nível superior com um servidor do WSUS existente. O ponto de atualização de software em um site primário filho configura a origem da sincronização como o ponto de atualização de software no site de administração central por padrão.  

    > [!NOTE]  
    >  O primeiro ponto de atualização de software instalado em um site primário, que é o ponto de atualização de software padrão, é sincronizado com o site de administração central. Pontos de atualização de software adicionais no site primário sincronizam com o ponto de atualização de software padrão no site primário.  

     Quando um ponto de atualização de software é desconectado do Microsoft Update ou do servidor de atualização upstream, você pode configurar a origem da sincronização para não sincronizar com uma origem de sincronização configurada, mas, em vez disso, usar a função de exportação e importação da ferramenta WSUSUtil para sincronizar atualizações de software. Para obter mais informações, consulte [Synchronize software updates from a disconnected software update point](../get-started/synchronize-software-updates-disconnected.md) (Sincronizar atualizações de software de um ponto de atualização de software desconectado).  

-   **Eventos de geração de relatórios do WSUS:** O Windows Update Agent em computadores cliente pode criar mensagens de eventos que são usadas para relatórios do WSUS. Esses eventos não são usados pela atualização de software no Configuration Manager, portanto, a opção **Não criar eventos de relatórios do WSUS** é selecionada por padrão. Quando esses eventos não são criados, a única vez que o computador cliente deve se conectar ao servidor do WSUS é durante a avaliação da atualização de software e varreduras de conformidade. Se esses eventos forem necessários para relatórios fora das atualizações de software no Configuration Manager, você precisará modificar essa configuração para criar eventos de relatório do WSUS.  

###  <a name="a-namebkmksyncschedulea-synchronization-schedule"></a><a name="BKMK_SyncSchedule"></a> Cronograma de sincronização  
 É possível configurar o cronograma de sincronização apenas no ponto de atualização de software no site de nível superior na hierarquia do Configuration Manager. Quando você configura a agenda de sincronização, o ponto de atualização de software sincroniza-se com a origem da sincronização, na data e hora que você especificou. A agenda personalizada permite que você sincronize as atualizações de software em uma data e hora em que as demandas do servidor do WSUS, servidor do site e da rede estão baixas, como às 2h, uma vez por semana. Como alternativa, você pode iniciar a sincronização no site de nível superior usando a ação **Atualizações de Software de Sincronização** no nó **Todas as Atualizações de Software** ou **Grupos de Atualização de Software** no console do Configuration Manager.  

> [!TIP]  
>  Agende a sincronização de atualizações de software para ser executadas usando um período apropriado a seu ambiente. Um cenário típico é definir a agenda de sincronização das atualizações de software para execução logo após o lançamento da atualização de segurança regular da Microsoft na segunda terça-feira de cada mês, que é normalmente conhecida como Patch Tuesday. Outro cenário típico é definir a agenda de sincronização de atualizações de software para ser executada diariamente quando você usa as atualizações de software para fornecer definição e atualizações de mecanismo do Endpoint Protection.  

 Após o ponto de atualização de software concluir com êxito a sincronização, uma solicitação de sincronização é enviada para sites filhos. Se houver pontos de atualização de software adicionais em um site primário, uma solicitação de sincronização será enviada para cada ponto de atualização de software. O processo é repetido em todos os sites na hierarquia.  

###  <a name="a-namebkmkupdateclassificationsa-update-classifications"></a><a name="BKMK_UpdateClassifications"></a> Classificações de atualizações  
 Cada atualização de software é definida com uma classificação de atualização que ajuda a organizar os diferentes tipos de atualização. Durante o processo de sincronização, os metadados de atualizações de software para as classificações especificadas serão sincronizados. O Configuration Manager permite que você sincronize as atualizações de software com as seguintes classificações de atualização:  

-   **Atualizações críticas:** especifica uma atualização lançada em larga escala para um problema específico que aborda um bug crítico não relacionado à segurança.  

-   **Atualizações de definições:** especifica uma atualização para vírus ou outros arquivos de definição.  

-   **Feature Packs:** Especifica novos recursos de produtos que são distribuídos fora de uma versão do produto e recursos que são normalmente incluídos na próxima versão completa do produto.  

-   **Atualizações de segurança:** especifica uma atualização lançada em larga escala para um problema de um produto em específico relacionado à segurança.  

-   **Service Packs:** especifica um conjunto cumulativo de hotfixes que são aplicados a um aplicativo. Esses hotfixes podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim por diante.  

-   **Ferramentas:** especifica um utilitário ou um recurso que ajuda a concluir uma ou mais tarefas.  

-   **Pacotes cumulativos de atualizações:** especifica um conjunto cumulativo de hotfixes que são reunidos para facilitar a implantação. Esses hotfixes podem incluir atualizações de segurança, atualizações críticas, atualizações e assim por diante. Um pacote cumulativo de atualizações geralmente aborda uma área específica, como segurança ou um componente do produto.  

-   **Atualizações:** especifica uma atualização para um aplicativo ou arquivo que está atualmente instalado.  

 As configurações de classificação de atualização são definidas somente no site de nível superior. As configurações de classificação de atualização não estão definidas no ponto de atualização de software de sites filhos, porque os metadados das atualizações de software são replicados do site de nível superior em sites primários filhos. Ao selecionar classificações de atualização, lembre-se de que quanto mais classificações você selecionar, mais tempo levará para sincronizar os metadados das atualizações de software.  

> [!WARNING]  
>  Como prática recomendada, desmarque todas as classificações antes de sincronizar atualizações de software pela primeira vez. Após a sincronização inicial, selecione as classificações de propriedades do componente de ponto de atualização de software e, em seguida, reinicialize a sincronização.  

###  <a name="a-namebkmkupdateproductsa-products"></a><a name="BKMK_UpdateProducts"></a> Produtos  
 Os metadados de cada atualização de software definem um ou mais produtos aos quais a atualização é aplicável. Um produto é uma edição específica de um aplicativo ou sistema operacional. Um exemplo de um produto é o Microsoft Windows Server 2008. Uma família de produtos é o sistema operacional base ou o aplicativo do qual os produtos individuais são derivados. Um exemplo de uma família de produtos é o Microsoft Windows, do qual o Microsoft Windows Server 2008 é um membro. Você pode especificar uma família de produtos ou produtos individuais dentro de uma família de produtos.  

 Quando as atualizações de software são aplicáveis a vários produtos, e no mínimo um dos produtos é selecionado para sincronização, todos os produtos aparecerão no console do Configuration Manager, mesmo se alguns produtos não forem selecionados. Por exemplo, se o Windows Server 2012 for o único sistema operacional que você assina, e se uma atualização de software se aplicar ao Windows Server 2012 e ao Windows Server 2012 Datacenter Edition, ambos os produtos estarão no banco de dados do site.  

 Os parâmetros do produto são configurados somente no site de nível superior. Os parâmetros do produto não são configurados no ponto de atualização de software para sites filho porque os metadados de atualizações de software são replicados do site de nível superior para sites primários filho. Quando você selecionar produtos, esteja ciente de que quanto mais produtos seleciona, mais tempo irá demorar para sincronizar os metadados de atualizações de software.  

> [!IMPORTANT]  
>  O Configuration Manager armazena uma lista de produtos e famílias de produtos que você pode escolher ao instalar o ponto de atualização de software pela primeira vez. Os produtos e as famílias de produtos que forem lançados após o lançamento do Configuration Manager podem não estar disponíveis para seleção até que você conclua a sincronização das atualizações de software, o que atualizará a lista de produtos e famílias de produtos disponíveis para você escolher. Como prática recomendada, desmarque todos os produtos antes de sincronizar as atualizações de software pela primeira vez. Após a sincronização inicial, selecione os produtos em Propriedades do Componente de Ponto de Atualização de Software e reinicie a sincronização.  

###  <a name="a-namebkmksupersedencerulesasupersedence-rules"></a><a name="BKMK_SupersedenceRules"></a>Regras de substituição  
 Normalmente, uma atualização de software que substitui outra executa uma ou mais das seguintes ações:  

-   Melhora, aumenta ou atualiza a correção fornecida por uma ou mais atualizações lançadas anteriormente.  

-   Melhora a eficiência do pacote de arquivos de atualização substituído, que é instalado em computadores cliente se a atualização for aprovada para instalação. Por exemplo, a atualização substituída pode conter arquivos que não são mais relevantes para a correção ou para os sistemas operacionais com suporte pela nova atualização. Portanto, esses arquivos não são incluídos no pacote de arquivos de substituição da atualização.  

-   Atualiza versões mais recentes de um produto. Em outras palavras, atualiza as versões que não são mais aplicáveis a versões ou configurações mais antigas de um produto. As atualizações também pode substituir outras atualizações caso modificações tenham sido feitas para expandir o suporte para idiomas. Por exemplo, uma revisão posterior da atualização de um produto do Microsoft Office pode remover o suporte de um sistema operacional mais antigo, mas pode adicionar suporte para novos idiomas na versão de atualização inicial.  

 Nas propriedades do ponto de atualização de software, é possível especificar se as atualizações de software substituídas expiram imediatamente, o que evita que elas sejam incluídas em novas implantações e sinaliza as implantações existentes para indicar que contêm uma ou mais atualizações de software expiradas. Ou, você pode especificar um período de tempo até que as atualizações de software substituídas se expirem, o que permitirá que você continue a implantá-las. Considere os seguintes cenários em que poderia ser necessário implantar uma atualização de software substituída:  

-   Se uma atualização de software substituta oferecer suporte somente para versões mais recentes de um sistema operacional, e alguns de seus computadores cliente executarem versões anteriores do sistema operacional.  

-   Se uma atualização de software substituta tiver aplicabilidade mais restrita do que a atualização de software que está substituindo. Isso a tornaria inadequada para alguns computadores cliente.  

-   Se uma atualização de software substituta não for aprovada para implantação em seu ambiente de produção.  

###  <a name="a-namebkmkupdatelanguagesa-languages"></a><a name="BKMK_UpdateLanguages"></a> Idiomas  
 As configurações de idioma do ponto de atualização de software permitem configurar os idiomas para os quais os detalhes de resumo (metadados de atualizações de software) são sincronizados para atualizações de software, e os idiomas do arquivo de atualização do software serão baixados para as atualizações de software.  

#### <a name="software-update-file"></a>Arquivo de atualização de software  
 Os idiomas que você configura para o parâmetro **Arquivo de atualização de software** nas propriedades do ponto de atualização de software fornecem o conjunto padrão de idiomas que estão disponíveis ao baixar as atualizações de software em um site. É possível modificar os idiomas selecionados que são selecionados por padrão sempre que as atualizações de software são baixadas ou implantadas. Durante o processo de download, os arquivos de atualização de software para os idiomas configurados são baixados no local de origem do pacote de implantação, se os arquivos de atualização de software estiverem disponíveis no idioma selecionado. Em seguida, eles são copiados na biblioteca de conteúdo do servidor do site e depois são copiados nos pontos de distribuição configurados para o pacote.  

 Os parâmetros de idioma do arquivo de atualização de software devem ser configurados com os idiomas usados com mais frequência em seu ambiente. Por exemplo, se os computadores cliente atribuídos ao site usam mais os idiomas inglês e japonês para o sistema operacional ou aplicativos, e há outros pouquíssimos idiomas que são usados no site, selecione Inglês e Japonês na coluna **Arquivo de Atualização de Software** quando você baixar ou implantar a atualização de software e desmarque os outros idiomas. Isso permite usar as configurações padrão na página **Seleção de Idioma** da implantação e baixar assistentes. Isso também impede que arquivos de atualização desnecessários sejam baixados. Esse parâmetro é configurado em cada ponto de atualização de software da hierarquia do Configuration Manager.  

#### <a name="summary-details"></a>Detalhes do resumo  
 Durante o processo de sincronização, as informações detalhadas do resumo (metadados de atualizações de software) são atualizadas para as atualizações de software nos idiomas que você especificar. Os metadados fornecem as informações sobre a atualização de software, como nome, descrição, produtos com suporte na atualização, classificação da atualização, ID do artigo, URL para download, regras de aplicabilidade e assim por diante.  

 Os parâmetros de detalhes do resumo são configurados somente no site de nível superior. Os detalhes do resumo não são configurados no ponto de atualização de software em sites filho porque os metadados das atualizações de software são replicados do site de administração central para esses sites por meio da replicação baseada em arquivo. Quando você for selecionar os idiomas dos detalhes do resumo, selecione somente os idiomas necessários em seu ambiente. Quanto mais idiomas você selecionar, mais tempo levará para sincronizar os metadados de atualizações de software. O Configuration Manager exibe os metadados de atualizações de software na localidade do sistema operacional no qual o console do Configuration Manager é executado. Se as propriedades localizadas das atualizações de software não estiverem disponíveis no idioma do sistema operacional, as informações de atualizações de software serão exibidas em inglês.  

> [!IMPORTANT]  
>  É importante que você selecione todos os idiomas dos detalhes de resumo que serão necessários na hierarquia do Configuration Manager. Quando o ponto de atualização de software no site de nível superior sincronizar com a origem da sincronização, os idiomas selecionados para os detalhes do resumo determinarão quais metadados de atualizações de software serão recuperados. Se você modificar os idiomas de detalhes do resumo após a execução da sincronização no mínimo uma vez, os metadados de atualizações de software serão recuperados para os idiomas de detalhes do resumo modificados somente para atualizações de software novas ou atualizadas. As atualizações de software que já tiverem sido sincronizadas não serão atualizadas com os novos metadados dos idiomas modificados, a menos que haja uma alteração na atualização de software na origem da sincronização.  

##  <a name="a-namebkmkmaintenancewindowa-plan-for-a-software-updates-maintenance-window"></a><a name="BKMK_MaintenanceWindow"></a> Planejar uma janela de manutenção das atualizações de software  
 É possível adicionar uma janela de manutenção dedicada para a instalação de atualizações de software. Isso lhe permite configurar uma janela de manutenção geral e uma janela de manutenção diferente para atualizações de software. Quando a janela de manutenção geral e a janela de manutenção para atualizações de software estão configuradas, os clientes instalam as atualizações de software apenas durante a janela de manutenção para atualizações de software. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="a-namebkmkrestartoptionsa-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Opções de reinicialização para clientes do Windows 10 após a instalação da atualização de software
Quando uma atualização de software que requer reinicialização é implantada usando o Configuration Manager e é instalada em um computador, uma reinicialização pendente é agendada e uma caixa de diálogo de reinicialização é exibida.

A partir da versão 1606 do Configuration Manager, as opções **Atualizar e Reiniciar**e **Atualizar e Desligar** estão disponíveis em computadores Windows 10, nas opções de energia do Windows, sempre que houver uma reinicialização pendente para uma atualização de software do Configuration Manager. Depois de usar uma dessas opções, a caixa de diálogo de reinicialização não será exibida após o computador reiniciar.

Em versões anteriores do Configuration Manager, quando uma reinicialização está pendente para computadores com Windows 8 e mais recentes, e você desliga ou reinicia o computador usando as opções de energia do Windows (em vez da caixa de diálogo de reinicialização), a caixa de diálogo de reinicialização permanece depois da reinicialização do computador e ainda será necessário reiniciá-lo no prazo configurado.

## <a name="next-steps"></a>Próximas etapas
Quando planejar atualizações de software, consulte [Preparar-se para o gerenciamento de atualização de software](../get-started/prepare-for-software-updates-management.md).



<!--HONumber=Nov16_HO1-->


