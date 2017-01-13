---
title: "Introdução | Microsoft Docs"
description: "Veja informações básicas em uma introdução ao System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: b0b2f72d4b1eae3aa5b860a210ac3a4259e17069
ms.openlocfilehash: 3bbbb6a00883a5e489696387fad9224fdc2082ba


---
# <a name="introduction-to-system-center-configuration-manager"></a>Introduction to System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Membro do pacote de soluções de gerenciamento do Microsoft System Center, o System Center Configuration Manager pode ajudá-lo a gerenciar dispositivos e usuários localmente e na nuvem.  

**O Configuration Manager pode ajudar você a:**   
-   Aumentar a eficiência e a produtividade de TI, reduzindo as tarefas manuais e permitindo que você se concentre em projetos de alto valor  
-   Maximizar os investimentos em hardware e software  
-   Capacitar a produtividade do usuário final ao fornecer o software certo no momento certo  

**Configuration Manager ajuda a fornecer serviços de TI mais eficientes ao habilitar:**  

-   A implantação de software segura e escalonável  
-   O gerenciamento de configurações de conformidade  
-   O gerenciamento abrangente de ativos de servidores, computadores desktops, laptops e dispositivos móveis.  

**O Configuration Manager estende e trabalha com suas tecnologias e soluções existentes da Microsoft.**  

Por exemplo, o Configuration Manager se integra com:  

-   O Microsoft Intune para gerenciar uma ampla variedade de plataformas de dispositivos móveis  
-   WSUS (Windows Server Update Services) para gerenciar atualizações de software  
-   Serviços de Certificados  
-   Exchange Server e Exchange Online  
-   Política de Grupo do Windows
-   DNS   
-   Windows ADK (Kit de Implantação Automatizada) e USMT (Ferramenta de Migração do Usuário)  
-   WDS (Serviços de Implantação do Windows)  
-   Área de Trabalho Remota e Assistência Remota  

O Configuration Manager também usa:  

-   Os Serviços de Domínio do Active Directory para segurança, localização de serviço, configuração e para descobrir os usuários e dispositivos que deseja gerenciar.  
-   O Microsoft SQL Server como um banco de dados distribuído de gerenciamento de alterações e integra-se ao SSRS (SQL Server Reporting Services) para produzir relatórios para monitorar e acompanhar as atividades de gerenciamento.  
-   Funções do sistema de sites que estendem a funcionalidade de gerenciamento e usam os serviços Web do IIS (Serviços de Informações da Internet).  
-   O BITS (Serviço de Transferência Inteligente em Segundo Plano) e o BranchCache podem ajudar a gerenciar a largura de banda da rede disponível.  

 Para ter êxito com o Configuration Manager, é necessário primeiro planejar e testar a fundo os recursos de gerenciamento para usar o Configuration Manager em um ambiente de produção. Como um aplicativo de gerenciamento avançado, o Configuration Manager tem potencial de afetar todos os computadores da organização. Quando você implanta e gerencia o Configuration Manager com planejamento criterioso e levando em consideração os requisitos de negócios, o Configuration Manager pode reduzir a sobrecarga administrativa e o custo total de propriedade.  

 Use os seguintes tópicos e seções adicionais neste tópico para saber mais sobre o Configuration Manager:  


**Tópicos relacionados na biblioteca de documentação:**  

-   [Recursos e funcionalidades do System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md)  
-   [Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  
-   [O que mudou no System Center Configuration Manager do System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)
-   [Conceitos básicos do System Center Configuration Manager](../../core/understand/fundamentals.md)  
-   [Avaliar o System Center Configuration Manager compilando seu próprio ambiente de laboratório](/sccm/core/get-started/set-up-your-lab)
-   [Encontrar ajuda para usar o System Center Configuration Manager](../../core/understand/find-help.md)  
-   [Recursos removidos e preteridos do System Center Configuration Manager](../../core/plan-design/changes/removed-and-deprecated-features.md)  

##  <a name="a-namebkmkconsolea-the-configuration-manager-console"></a><a name="BKMK_Console"></a> O console do Configuration Manager  
 Feita a instalação do Configuration Manager, use o console do Configuration Manager para configurar sites e clientes e para executar e monitorar tarefas de gerenciamento. Esse console é o principal ponto de administração e permite que você gerencie vários sites.  

 Você pode usar o console para executar consoles secundários que dão suporte a tarefas específicas de gerenciamento de clientes, como:  

-   **Gerenciador de Recursos**, para exibir informações de inventário de hardware e de software.  
-   **Controle remoto**, para se conectar remotamente a um computador cliente para executar tarefas de solução de problemas.  

 Você pode instalar o console do Configuration Manager em computadores adicionais, bem como restringir o acesso e limitar o que os usuários administrativos podem ver no console usando a administração baseada em funções do Configuration Manager.  

 Para obter mais informações, veja [Instalar consoles do System Center Configuration Manager](../../core/servers/deploy/install/install-consoles.md).

##  <a name="a-namebkmkapplicationcataloga-the-application-catalog-software-center-and-the-company-portal"></a><a name="BKMK_ApplicationCatalog"></a> Catálogo de aplicativos, Central de software e Portal da empresa  
 O **Catálogo de Aplicativos** é um site em que usuários podem procurar e solicitar software para seus PCs baseados no Windows. Para usar o catálogo de aplicativos, é necessário instalar o ponto de serviços Web do catálogo de aplicativos e o ponto de sites da Web do catálogo de aplicativos para o site.  

 O**Centro de Software** é um aplicativo que é instalado quando o cliente do Configuration Manager é instalado em computadores baseados no Windows. Os usuários executam esse aplicativo para solicitar softwares e gerenciar os software implantados neles usando o Configuration Manager. O Centro de Software permite que os usuários façam o seguinte:  

-   Procurem e instalem softwares do Catálogo de Aplicativos  
-   Exibam seu histórico de solicitação de software.  
-   Configurem quando o Configuration Manager pode instalar software em seus dispositivos  
-   Definam as configurações de acesso para controle remoto se um usuário administrativo estiver habilitado para o controle remoto  

 O **Portal da Empresa** é um aplicativo ou site que fornece funções semelhantes às do Catálogo de Aplicativos, mas para dispositivos móveis registrados pelo Microsoft Intune  

 Para obter mais informações, consulte o tópico [Introdução ao gerenciamento de aplicativos no System Center Configuration Manager](../../apps/understand/introduction-to-application-management.md).  

###  <a name="a-namebkmkclienta-configuration-manager-properties-on-windows-pcs"></a><a name="BKMK_Client"></a> Propriedades do Configuration Manager (em computadores Windows)  
 Quando o cliente do Configuration Manager é instalado em computadores Windows, o Configuration Manager é instalado no Painel de Controle. Normalmente, não é necessário configurar esse aplicativo porque a configuração do cliente é executada no console do Configuration Manager. Esse aplicativo ajuda os usuários administrativos e o suporte técnico a solucionar problemas com clientes individuais.  

 Para obter mais informações sobre a implantação de cliente, consulte [Métodos de instalação do cliente no System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

##  <a name="a-namebkmkexamplescenariosa-example-scenarios-for-configuration-manager"></a><a name="BKMK_ExampleScenarios"></a> Cenários de exemplo para o Configuration Manager  
 Os cenários de exemplo a seguir demonstram como uma empresa chamada Trey Research usa o System Center Configuration Manager para capacitar os usuários a:  

-   Serem mais produtivos  
-   Unificarem o gerenciamento de conformidade de dispositivos para uma experiência de administração mais simples  
-   Simplificarem o gerenciamento de dispositivo para reduzir os custos operacionais de TI  

 Em todos os cenários, Anibal é o administrador principal do Configuration Manager.  

###  <a name="a-namebkmkscenarioempowera-example-scenario-empower-users-by-ensuring-access-to-applications-from-any-device"></a><a name="BKMK_ScenarioEmpower"></a> Cenário de exemplo: capacitar os usuários ao garantir acesso a aplicativos de qualquer dispositivo  
 A Trey Research deseja proporcionar o acesso de funcionários a aplicativos que eles necessitam e com a maior eficiência possível. Anibal mapeia esses requisitos da empresa para os seguintes cenários:  

|Requisito|Estado atual de gerenciamento de clientes|Estado futuro de gerenciamento de clientes|  
|-----------------|-------------------------------------|------------------------------------|  
|Os novos funcionários podem trabalhar com eficiência desde o início.|Quando os funcionários entram na empresa ele precisam esperar os aplicativos serem instalados depois de fazer o logon pela primeira vez.|Quando os funcionários entram na empresa, eles fazem o logon e seus aplicativos são instalados e ficam prontos para o uso.|  
|Os funcionários podem solicitar software adicional que precisam com rapidez e facilidade.|Quando os funcionários necessitam de aplicativos adicionais, eles apresentam um tíquete ao suporte técnico e normalmente aguardam dois dias para que o tíquete seja processado e os aplicativos instalados.|Quando os funcionários necessitam de aplicativos adicionais, eles os solicitam no site e os aplicativos são instalados imediatamente se não há restrições de licença. Se há restrições de licença, os usuários devem primeiro solicitar uma aprovação para que possam instalar o aplicativo.<br /><br /> O site mostra aos usuários apenas os aplicativos que eles têm permissão para instalar.|  
|Os funcionários podem usar seus dispositivos móveis no trabalho se os dispositivos estão em conformidade com as políticas de segurança que são monitoradas e aplicadas.<br /><br /> Essas políticas incluem imposição de uma senha forte, bloqueio um dispositivo depois de um período de inatividade e apagamento remoto dos dispositivos perdidos ou roubados.|Os funcionários conectam seus dispositivos móveis ao Exchange Server para o serviço de email , mas há relatórios limitados para confirmar se estão em conformidade com as políticas de segurança nas políticas de caixa de correio padrão do Exchange ActiveSync. O uso pessoal de dispositivos móveis corre o risco de ser proibido a menos que a equipe de TI possa confirmar a adesão à política.|A organização de TI pode relatar a conformidade de segurança do dispositivo móvel com as configurações necessárias. Essa confirmação permite que os usuários continuem a usar seus dispositivos móveis no trabalho. Os usuários podem apagar remotamente seus dispositivos móveis em caso de perda ou roubo e o suporte técnico pode apagar o dispositivo móvel de qualquer usuário que for relatado como perdido ou roubado.<br /><br /> Fornecem o registro do dispositivo móvel em um ambiente de PKI para controle e segurança adicionais.|  
|Os funcionários poderão ser produtivos mesmo se não estiverem em suas mesas.|Quando os funcionários não estiverem em suas mesas e não possuírem computadores portáteis, eles não poderão acessar seus aplicativos usando quiosques de informática disponíveis pela empresa.|Os funcionários podem usar os quiosques de informática para acessar seus aplicativos e dados.|  
|Geralmente, a continuidade de negócios tem prioridade sobre a instalação de aplicativos necessários e de atualizações de software.|Os aplicativos e as atualizações de software que necessitam de instalação durante o dia e frequentemente interrompem usuários do trabalho porque seus computadores ficam mais lentos e são reiniciados durante a instalação.|Os usuários podem configurar suas horas de trabalho para evitar que o software necessário seja instalado enquanto eles estão usando seus computadores.|  

 Para atender aos requisitos, Anibal usa estes recursos de gerenciamento e opções de configuração do Configuration Manager:  

-   Gerenciamento de aplicativos  
-   Gerenciamento de dispositivos móveis  

 Ele implementa esses itens usando as etapas de configuração na tabela a seguir.  

|Etapas de configuração|Resultado|  
|-------------------------|-------------|  
|Anibal verifica se os novos usuários possuem contas de usuário no Active Directory e cria uma nova coleção baseada em consultas no Configuration Manager para esses usuários. Em seguida, ele define a afinidade de dispositivo de usuário para esses usuários criando um arquivo que mapeia as contas de usuário para os computadores primários que eles usarão e importa esse arquivo no Configuration Manager.<br /><br /> Os aplicativos que os novos usuários devem ter já estão criados no Configuration Manager. Então ele implanta esses aplicativos que têm a finalidade de Necessário na coleção que contém os novos usuário.|Por conta das informações de afinidade de dispositivo de usuário, os aplicativos são instalados em cada computador – ou computadores – primário do usuário antes que ele faça logon.<br /><br /> Os aplicativos estão prontos para uso assim que o usuário fizer logon com êxito.|  
|Anibal instala e configura as funções do sistema de site do catálogo de aplicativos para que os usuários possam procurar aplicativos a serem instalados. Ele cria implantações de aplicativos que têm a finalidade de Disponível e implanta esses aplicativos na coleção que contém os novos usuários.<br /><br /> Para os aplicativos que possuem um número restrito de licenças, Anibal configura esses aplicativos para solicitarem aprovação.|Ao configurar aplicativos como disponível para esses usuários e ao usar o catálogo de aplicativos, os usuários agora podem procurar os aplicativos que eles têm permissão para instalar. Os usuários podem instalar os aplicativos imediatamente ou solicitar aprovação e retornar para o catálogo de aplicativos para instalá-los depois que o suporte técnico tiver aprovado a solicitação.|  
|Anibal cria um conector do Exchange Server no Configuration Manager para gerenciar os dispositivos móveis que se conectam ao Exchange Server local da empresa. Ele define esse conector com configurações de segurança que incluem o requisito para uma senha forte e bloqueia o dispositivo móvel após um período de inatividade.<br /><br /> Para gerenciamento adicional de dispositivos que executam Windows Phone 8, Windows RT e iOS, Anibal obtém uma assinatura do Microsoft Intune e instala a função de sistema de sites de ponto de conexão de serviço. Essa solução de gerenciamento de dispositivo móvel dá à empresa maior suporte para gerenciamento desses dispositivos. Isso inclui disponibilizar aplicativos para que os usuários instalem nesses dispositivos e amplo gerenciamento de configurações. Além disso, as conexões de dispositivo móvel são protegidas usando certificados PKI criados e implantados automaticamente pelo Intune. Depois de configurar o ponto de conexão de serviço e a assinatura para serem usados com o Configuration Manager, Anibal envia uma mensagem de email aos usuários que têm esses dispositivos móveis para que eles cliquem em um link para iniciar o processo de registro.<br /><br /> Para que os dispositivos móveis sejam registrados pelo Microsoft Intune, Anibal usa configurações de conformidade para definir configurações de segurança para esses dispositivos móveis. Essas configurações incluem o requisito para definir uma senha forte e bloqueiam o dispositivo móvel após um período de inatividade.|Com essas duas soluções de gerenciamento de dispositivo móvel, agora a organização de TI pode fornecer informações de relatórios sobre os dispositivos móveis em uso na rede da empresa e sua conformidade com as configurações de segurança definidas.<br /><br /> Os usuários veem como apagar remotamente o dispositivo móvel usando o catálogo de aplicativos ou o portal da empresa caso o dispositivo móvel seja perdido ou roubado. O suporte técnico também é instruído sobre como apagar remotamente um dispositivo móvel do usuário utilizando o console do Configuration Manager.<br /><br /> Além disso, para dispositivos móveis registrados pelo Microsoft Intune, agora Anibal pode implantar aplicativos móveis para que os usuários possam instalar, coletar mais dados de inventário desses dispositivos e ter melhor controle de gerenciamento sobre os dispositivos por poderem acessar mais configurações.|  
|A Trey Research tem vários computadores de quiosque que são usados por funcionários que visitam o escritório. Os funcionários desejam que seus aplicativos estejam disponíveis sempre que eles fizerem logon. No entanto, Anibal não quer instalar localmente todos os aplicativos em cada computador.<br /><br /> Para isso, Anibal cria os aplicativos necessários que têm dois tipos de implantação:<br /><br /> **O primeiro:** uma instalação completa local do aplicativo que tem o requisito de só poder ser instalado em um dispositivo primário do usuário.<br /><br /> **O segundo:** uma versão virtual do aplicativo que tem o requisito de não poder ser instalado no dispositivo primário do usuário.|Quando funcionários visitantes fazem logon em um computador de quiosque, eles veem os aplicativos de que precisam exibidos como ícones na área de trabalho do computador de quiosque. Quando eles executam o aplicativo, ele é transmitido como um aplicativo virtual. Dessa forma, eles podem ser tão produtivos como se estivessem usando sua área de trabalho.|  
|Anibal permite que os usuários saibam que eles podem configurar seu horário comercial no Centro de Software e seleciona opções para impedir atividades de implantação de software durante este período e quando o computador está em modo de apresentação.|Como os usuários podem controlar quando o Configuration Manager implanta software nos computadores, os usuários permanecem mais produtivos durante o dia de trabalho.|  

 Essas etapas de configuração e esses resultados permitem que a Trey Research dê poderes a seus funcionários com êxito, garantindo o acesso a aplicativos de qualquer dispositivo.  

###  <a name="a-namebkmkscenariounifya-example-scenario-unify-compliance-management-for-devices"></a><a name="BKMK_ScenarioUnify"></a> Cenário de exemplo: unificar o gerenciamento de conformidade de dispositivos  
 A Trey Research quer uma solução de gerenciamento de clientes unificada que garante que os computadores executem software antivírus que seja atualizado automaticamente. Ou seja:  

-   O Firewall do Windows está habilitado  
-   Atualizações críticas de software estão instaladas  
-   Chaves específicas do Registro estão definidas  
-   Os dispositivos móveis gerenciados não podem instalar nem executar aplicativos não assinados  

 A empresa também quer expandir essa proteção para a Internet para laptops que se movem da intranet para a Internet.  

 Anibal mapeia esses requisitos da empresa para os seguintes cenários:  

|Requisito|Estado atual de gerenciamento de clientes|Estado futuro de gerenciamento de clientes|  
|-----------------|-------------------------------------|------------------------------------|  
|Todos os computadores executam software antimalware que possui arquivos de definição atualizados e habilitam o Firewall do Windows.|Computadores diferentes executam soluções antimalware diferentes que nem sempre estão atualizadas e, embora o Firewall do Windows esteja habilitado por padrão, às vezes os usuários podem desabilitá-lo.<br /><br /> Os usuários devem entrar em contato com o suporte técnico se for detectado malware em seu computador.|Todos os computadores executam a mesma solução antimalware que baixa automaticamente os arquivos mais recentes de atualização da definição e reabilita automaticamente o Firewall do Windows se os usuários o desabilitarem.<br /><br /> O suporte técnico será notificado automaticamente por email se for detectado malware.|  
|Todos os computadores instalam atualizações de software críticas no primeiro mês de lançamento.|Embora as atualizações de software sejam instaladas em computadores, muitos computadores não instalam automaticamente as atualizações de software críticas até dois ou três meses após o lançamento. Isso os deixa vulneráveis a ataques durante esse período.<br /><br /> Para os computadores que não instalam as atualizações de software críticas, o suporte técnico primeiro envia mensagens de email para que os usuários instalem as atualizações. Para computadores que permanecem não compatíveis, os engenheiros se conectam remotamente a esses computadores e instalam manualmente as atualizações de software que faltam.|Melhorar a taxa de conformidade atual no mês especificado para mais de 95% sem enviar mensagens de email nem solicitar que o suporte técnico as instale.|  
|Configurações de segurança para aplicativos específicos são verificadas e corrigidas regularmente se for necessário.|Os computadores executam scripts de inicialização complexos que dependem da associação ao grupo do computador para redefinir valores do Registro para aplicativos específicos.<br /><br /> Como esses scripts são executados somente na inicialização e alguns computadores são deixados ligados por vários dias, o suporte técnico não pode verificar se há descompasso na configuração em tempo adequado.|Os valores do Registro são verificados e corrigidos automaticamente sem depender da associação ao grupo do computador ou reiniciar o computador.|  
|Os dispositivos móveis não podem instalar nem executar aplicativos não seguros.|Os usuários não devem baixar nem executar aplicativos potencialmente não seguros da Internet, mas não há controles em vigor para monitor e aplicar essa regra.|Os dispositivos móveis gerenciados com o Microsoft Intune ou com o Configuration Manager impedem automaticamente que aplicativos não assinados sejam instalados ou executados.|  
|Laptops que se movem da intranet para a Internet devem ser mantidos seguros.|Para usuários que viajam, frequentemente eles não conseguem se conectar via VPN diariamente e esses laptops ficam incompatíveis com requisitos de segurança.|Uma conexão com a Internet é tudo o que é necessário para que os laptops sejam mantidos em conformidade com requisitos de segurança. Os usuários não precisam fazer logon nem usar a VPN.|  

 Para atender aos requisitos, Anibal usa estes recursos de gerenciamento e opções de configuração do Configuration Manager:  

-   Endpoint Protection  
-   Atualizações de software  
-   Configurações de conformidade  
-   Gerenciamento de dispositivos móveis  
-   Gerenciamento de clientes baseado na Internet  

 Ele implementa esses itens usando as etapas de configuração na tabela a seguir.  

|Etapas de configuração|Resultado|  
|-------------------------|-------------|  
|Anibal configura o Endpoint Protection e habilita a configuração do cliente para desinstalar outras soluções antimalware e habilita o Firewall do Windows. Ele configura as regras de implantação automática para que os computadores verifiquem e instalem as atualizações de definições mais recentes regularmente.|A solução antimalware única ajuda a proteger todos os computadores usando a sobrecarga administrativa mínima. Como o suporte técnico é notificado automaticamente por mensagem de email se for detectado malware, os problemas podem ser resolvidos rapidamente. Isso ajuda a impedir ataques em outros computadores.|  
|Para ajudar a aumentar as taxas de conformidade, Anibal usa regras de implantação automática, define janelas de manutenção para servidores e investiga as vantagens e desvantagens de usar Wake on LAN para computadores que hibernam.|A conformidade com atualizações de software críticas aumenta e reduz o requisito para que os usuários ou o suporte técnico instale atualizações de software manualmente.|  
|Anibal usa configurações de conformidade para verificar a presença de aplicativos especificados. Quando os aplicativos são detectados, os itens de configuração verificam os valores do Registro e os corrigem automaticamente se estiverem fora de conformidade.|Ao usar itens de configuração e linhas de base de configuração que são implantadas em todos os computadores que verificam a conformidade todos os dias, separe os scripts que dependem da associação de computador e as reinicializações do computador não são mais necessárias.|  
|Anibal usa configurações de conformidade para dispositivos móveis registrados e configura o conector do Exchange Server para impedir que os aplicativos não assinados de sejam instalados e executados em dispositivos móveis.|Proibindo aplicativos não assinados, os dispositivos móveis são protegidos automaticamente contra aplicativos potencialmente prejudiciais.|  
|Anibal verifica se os servidores do sistema de site e os computadores possuem certificados PKI que o Configuration Manager exige para conexões HTTPS e, em seguida, ele instala funções adicionais do sistema de site na rede de perímetro que aceira conexões de cliente da Internet.|Os computadores que se movem da intranet para a Internet automaticamente continuam sendo gerenciados pelo Configuration Manager quando eles têm uma conexão com a Internet. Esses computadores não dependem do logon de usuários no computador ou da conexão à VPN.<br /><br /> Esses computadores continuam a ser gerenciados para antimalware e Firewall do Windows, atualizações de software e itens de configuração. Como resultado, os níveis de conformidade aumentarão automaticamente.|  

 Essas etapas de configuração e os resultados têm como efeito a unificação com êxito pela Trey Research do gerenciamento de conformidade de dispositivos.  

###  <a name="a-namebkmkscenariosimplifya-example-scenario-simplify-client-management-for-devices"></a><a name="BKMK_ScenarioSimplify"></a> Cenário de exemplo: simplificar o gerenciamento de clientes para os dispositivos  
 A Trey Research quer que todos os computadores novos instalem automaticamente a imagem de computador base da empresa, que executa o Windows 7. Depois que a imagem operacional for instalada nesses computadores, eles devem ser gerenciados e monitorados quanto ao software adicional instalado pelos usuários. Os computadores que armazenam informações altamente confidenciais requerem políticas de gerenciamento mais restritivas do que os outros computadores. Por exemplo, os engenheiros de suporte técnico não devem se conectar a eles remotamente, a entrada de PIN do BitLocker deve ser usada para reinicializações, e apenas os administradores locais podem instalar software.  

 Anibal mapeia esses requisitos da empresa para os seguintes cenários:  

|Requisito|Estado atual de gerenciamento de clientes|Estado futuro de gerenciamento de clientes|  
|-----------------|-------------------------------------|------------------------------------|  
|Novos computadores são instalados com o Windows 7.|O suporte técnico instala e configura o Windows 7 para os usuários e envia o computador para o respectivo local.|Os novos computadores seguem diretamente para o destino final, são conectados à rede e instalam e configuram o Windows 7 automaticamente.|  
|Os computadores devem ser gerenciados e monitorados. Isso inclui o inventário de hardware e software para ajudar a determinar os requisitos de licenciamento.|O cliente do Configuration Manager é implantado usando push automático do cliente, e o suporte técnico investiga falhas de instalação e clientes que não enviam dados de inventário quando esperado.<br /><br /> As falhas são frequentes devido às dependências de instalação que não são atendidas e corrupção do WMI no cliente.|A instalação do cliente e os dados de inventário coletados de computadores são mais confiáveis e requerem menos intervenção do suporte técnico. Os relatórios mostram o uso de software para obter informações de licença.|  
|Alguns computadores precisam ter políticas de gerenciamento mais rigorosas.|Em consequência das políticas de gerenciamento mais rigorosas, esses computadores não são gerenciados pelo Configuration Manager no momento.|Gerencie esses computadores usando o Configuration Manager sem sobrecarga administrativa adicional para acomodar as exceções.|  

 Para atender aos requisitos, Anibal usa estes recursos de gerenciamento e opções de configuração do Configuration Manager:  

-   Implantação de sistema operacional  
-   Implantação do cliente e status do cliente  
-   Configurações de conformidade  
-   Configurações do cliente  
-   Inventário e Asset Intelligence  
-   Administração baseada em funções  

 Ele implementa esses itens usando as etapas de configuração na tabela a seguir.  

|Etapas de configuração|Resultado|  
|-------------------------|-------------|  
|Anibal captura uma imagem do sistema operacional de um computador com o Windows 7 instalado e configurado com as especificações da empresa. Em seguida, ele implanta o sistema operacional nos novos computadores usando o PXE e o suporte de um computador desconhecido. E também instala o cliente do Configuration Manager como parte da implantação do sistema operacional.|Novos computadores estão em funcionamento mais rapidamente sem a intervenção do suporte técnico.|  
|Anibal configura a instalação automática do cliente por push em todo o site para instalar o cliente do Configuration Manager em qualquer computador que estiver descoberto. Isso garante que os computadores que ainda não tiveram a imagem gerada pelo cliente instalem o cliente para que o computador seja gerenciado pelo Configuration Manager.<br /><br /> Anibal configura o status de cliente para corrigir automaticamente os problemas do cliente que estão descobertos. Ele configura também as configurações do cliente que permitem a coleção de dados do inventário necessária e o Asset Intelligence.|Instalar o cliente com o sistema operacional é mais rápido e mais confiável do que esperar que o Configuration Manager descubra o computador e, então, tente instalar os arquivos de origem do cliente nele. No entanto, deixar a opção de push de cliente automático habilitada fornece meios de backup para um computador (que já possui o sistema operacional instalado) instalar o cliente quando é conectado a uma rede.<br /><br /> As configurações do cliente garantem que os clientes enviem suas informações de inventário para o site regularmente. Isso, além dos testes de status do cliente, ajuda a manter o cliente executando com intervenções mínimas do suporte técnico. Por exemplo, as corrupções do WMI são detectadas e corrigidas automaticamente.<br /><br /> Os relatórios do Asset Intelligence ajudam a monitorar o uso de software e licenças.|  
|Anibal cria uma coleção para os computadores que devem possuir configurações de política mais rigorosas e, depois, cria uma configuração de dispositivo do cliente personalizada para essa coleção, que inclui desabilitar controle remoto, habilitar a entrada PIN de BitLocker e permitir que apenas os administradores locais instalem o software.<br /><br /> Ele configura uma administração baseada em funções para que os engenheiros do suporte técnico não vejam essa coleção de computadores para ajudar a garantir que eles não gerenciem acidentalmente como um computador padrão.|Agora, esses computadores são gerenciados pelo Configuration Manager, mas com configurações específicas que não exigem um novo site.<br /><br /> A coleção para esses computadores não é visível para os engenheiros do suporte técnico para ajudar a reduzir a possibilidade de que eles enviem acidentalmente implantações e scripts para computadores padrão.|  

 Essas etapas de configuração e os resultados têm como efeito a simplificação com êxito pela Trey Research do gerenciamento de clientes de dispositivos.  

##  <a name="a-namebkmknextstepsa-next-steps"></a><a name="BKMK_NextSteps"></a> Próximas etapas  
 Antes de instalar o Configuration Manager, familiarize-se com alguns termos e conceitos básicos específicos do Configuration Manager.  

-   Se estiver familiarizado com o System Center 2012 Configuration Manager, consulte [O que mudou no System Center Configuration Manager do System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) para entender os novos recursos.  
-   Para ter uma visão geral técnica do System Center Configuration Manager, consulte [Aspectos fundamentais do System Center Configuration Manager](../../core/understand/fundamentals.md).  

 Quando estiver familiarizado com os conceitos básicos, use a documentação do System Center Configuration Manager para ajudá-lo a implantar e usar com êxito o Configuration Manager.  



<!--HONumber=Dec16_HO3-->


