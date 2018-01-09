---
title: "Introdução"
titleSuffix: Configuration Manager
description: "Veja informações básicas em uma introdução ao System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
caps.latest.revision: "16"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 76dfa18cb7f794be9102bf045cd4212adc7ad56f
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2018
---
# <a name="introduction-to-system-center-configuration-manager"></a>Introduction to System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um produto no pacote de soluções de gerenciamento do Microsoft System Center, o System Center Configuration Manager, pode ajudá-lo a gerenciar dispositivos e usuários localmente e na nuvem.  

**Você pode usar o Configuration Manager para ajudá-lo:**   
-   A aumentar a eficiência e a produtividade de TI, reduzindo as tarefas manuais e permitindo que você se concentre em projetos de alto valor.  
-   A maximizar os investimentos em hardware e software.  
-   A capacitar a produtividade do usuário ao fornecer o software certo no momento certo.  

**Configuration Manager ajuda a fornecer serviços de TI mais eficientes ao habilitar:**  

-   Implantação segura e escalonável de software.  
-   Gerenciamento de configurações de conformidade.  
-   O gerenciamento abrangente de ativos de servidores, computadores desktops, laptops e dispositivos móveis.  

**O Configuration Manager estende e trabalha com suas tecnologias e soluções existentes da Microsoft.**  

Por exemplo, o Configuration Manager se integra com:  

-   O Microsoft Intune para gerenciar uma ampla variedade de plataformas de dispositivos móveis.  
-   O WSUS (Windows Server Update Services) para gerenciar atualizações de software.  
-   Os Serviços de Certificados.  
-   O Exchange Server e Exchange Online.  
-   A Política de Grupo do Windows.
-   DNS.   
-   Windows ADK (Kit de Avaliação e Implantação do Windows) e USMT (Ferramenta de Migração do Usuário).  
-   WDS (Serviços de Implantação do Windows).  
-   Área de Trabalho Remota e Assistência Remota.  

O Configuration Manager também usa:  

-   Os Serviços de Domínio do Active Directory para segurança, localização de serviço, configuração e para descobrir os usuários e dispositivos que deseja gerenciar.  
-   O Microsoft SQL Server como um banco de dados distribuído de gerenciamento de alterações. E integra-se ao SSRS (SQL Server Reporting Services) para produzir relatórios para monitorar e acompanhar as atividades de gerenciamento.  
-   As funções do sistema de sites que estendem a funcionalidade de gerenciamento e usam os serviços Web do IIS (Serviços de Informações da Internet).
-   O BITS (Serviço de Transferência Inteligente em Segundo Plano) e o BranchCache podem ajudar a gerenciar a largura de banda da rede disponível.  

Para ter êxito com o Configuration Manager, é necessário primeiro planejar e testar a fundo os recursos de gerenciamento para usar o Configuration Manager em um ambiente de produção. Como um aplicativo de gerenciamento avançado, o Configuration Manager tem potencial de afetar todos os computadores da organização. Quando você implanta e gerencia o Configuration Manager com planejamento criterioso e levando em consideração os requisitos de negócios, o Configuration Manager pode reduzir a sobrecarga administrativa e o custo total de propriedade.  

Use os seguintes tópicos e seções adicionais neste tópico para saber mais sobre o Configuration Manager.  


**Tópicos relacionados na biblioteca de documentação:**  

-   [Recursos e funcionalidades do System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md)  
-   [Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  
-   [O que mudou no System Center Configuration Manager do System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)
-   [Conceitos básicos do System Center Configuration Manager](../../core/understand/fundamentals.md)  
-   [Avaliar o System Center Configuration Manager compilando seu próprio ambiente de laboratório](/sccm/core/get-started/set-up-your-lab)
-   [Encontrar ajuda para usar o System Center Configuration Manager](../../core/understand/find-help.md)  
-   [Recursos removidos e preteridos do System Center Configuration Manager](../../core/plan-design/changes/removed-and-deprecated-features.md)  

##  <a name="BKMK_Console"></a> O console do Configuration Manager  
 Feita a instalação do Configuration Manager, use o console do Configuration Manager para configurar sites e clientes e para executar e monitorar tarefas de gerenciamento. Esse console é o principal ponto de administração e permite que você gerencie vários sites.  

 Você pode usar o console para executar consoles secundários que dão suporte a tarefas específicas de gerenciamento de clientes, como:  

-   **Gerenciador de Recursos**, para exibir informações de inventário de hardware e de software.  
-   **Controle remoto**, para se conectar remotamente a um computador cliente para executar tarefas de solução de problemas.  

Você pode instalar o console do Configuration Manager em computadores adicionais, bem como restringir o acesso e limitar o que os usuários administrativos podem ver no console usando a administração baseada em funções do Configuration Manager.  

Para obter mais informações, veja [Instalar consoles do System Center Configuration Manager](../../core/servers/deploy/install/install-consoles.md).

##  <a name="BKMK_ApplicationCatalog"></a> Catálogo de aplicativos, Central de software e Portal da empresa  
 O **Catálogo de Aplicativos** é um site em que usuários podem procurar e solicitar software para seus PCs baseados no Windows. Para usar o catálogo de aplicativos, é necessário instalar o ponto de serviços Web do catálogo de aplicativos e o ponto de sites da Web do catálogo de aplicativos para o site.  

 O**Centro de Software** é um aplicativo que é instalado quando o cliente do Configuration Manager é instalado em computadores baseados no Windows. Os usuários executam esse aplicativo para solicitar softwares e gerenciar o software que o Configuration Manager implanta neles. O Centro de Software permite que os usuários façam o seguinte:  

-   Procurem e instalem software do catálogo de aplicativos.  
-   Exibam seu histórico de solicitação de software.  
-   Configurem quando o Configuration Manager pode instalar software em seus dispositivos.  
-   Definam as configurações de acesso para controle remoto, se um usuário administrativo está habilitado para o controle remoto.  

O **Portal da Empresa** é um aplicativo ou site que fornece funções semelhantes às do Catálogo de Aplicativos, mas para dispositivos móveis registrados pelo Microsoft Intune.  

Para obter mais informações, veja [Introdução ao gerenciamento de aplicativos no System Center Configuration Manager](../../apps/understand/introduction-to-application-management.md).  

###  <a name="BKMK_Client"></a> Propriedades do Configuration Manager (em computadores Windows)  
 Quando o cliente do Configuration Manager é instalado em computadores Windows, o Configuration Manager é instalado no Painel de Controle. Normalmente, não é necessário configurar esse aplicativo porque a configuração do cliente é executada no console do Configuration Manager. Esse aplicativo ajuda os usuários administrativos e o suporte técnico a solucionar problemas com clientes individuais.  

 Para obter mais informações sobre a implantação de cliente, consulte [Métodos de instalação do cliente no System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

##  <a name="BKMK_ExampleScenarios"></a> Cenários de exemplo para o Configuration Manager  
 Os cenários de exemplo a seguir demonstram como uma empresa chamada Trey Research usa o System Center Configuration Manager para capacitar os usuários a:  

-   Serem mais produtivos.  
-   Unificarem o gerenciamento de conformidade de dispositivos para uma experiência de administração mais simples.
-   Simplificarem o gerenciamento de dispositivo para reduzir os custos operacionais de TI.  

Em todos os cenários, Anibal é o administrador principal do Configuration Manager.  

###  <a name="BKMK_ScenarioEmpower"></a> Cenário de exemplo: capacitar os usuários ao garantir acesso a aplicativos de qualquer dispositivo  
 A Trey Research deseja garantir que os funcionários tenham acesso aos aplicativos que eles necessitam da forma mais eficiente possível. Anibal mapeia esses requisitos da empresa para os seguintes cenários:  

|Requisito|Estado atual de gerenciamento de clientes|Estado futuro de gerenciamento de clientes|  
|-----------------|-------------------------------------|------------------------------------|  
|Os novos funcionários podem trabalhar com eficiência desde o início.|Quando os funcionários entram na empresa precisam esperar os aplicativos serem instalados depois de conectarem-se pela primeira vez.|Quando os funcionários entram na empresa, eles se conectam e seus aplicativos são instalados e estão prontos para o uso.|  
|Os funcionários podem solicitar software adicional que precisam com rapidez e facilidade.|Quando os funcionários precisam de aplicativos adicionais, registram um tíquete de suporte técnico. Em seguida, normalmente aguardam dois dias para que o tíquete seja processado e os aplicativos sejam instalados.|Quando os funcionários precisam de aplicativos adicionais, eles podem solicitá-los de um site. Eles serão instalados imediatamente se não houver restrições de licenciamento. Se há restrições de licença, os usuários devem primeiro solicitar uma aprovação para que possam instalar o aplicativo.<br /><br /> O site mostra aos usuários apenas os aplicativos que eles têm permissão para instalar.|  
|Os funcionários podem usar seus dispositivos móveis no trabalho se os dispositivos estão em conformidade com as políticas de segurança que são monitoradas e aplicadas.<br /><br /> Essas políticas incluem imposição de uma senha forte, bloqueio de um dispositivo depois de um período de inatividade e apagamento remoto dos dispositivos perdidos ou roubados.|Os funcionários conectam seus dispositivos móveis ao Exchange Server para o serviço de email. Mas há relatórios limitados para confirmar se estão em conformidade com as políticas de segurança nas políticas de caixa de correio padrão do Exchange ActiveSync. O uso pessoal de dispositivos móveis corre o risco de ser proibido a menos que a equipe de TI possa confirmar a adesão à política.|A organização de TI pode relatar a conformidade de segurança do dispositivo móvel com as configurações necessárias. Essa confirmação permite que os usuários continuem a usar seus dispositivos móveis no trabalho. Os usuários podem apagar remotamente seus dispositivos móveis em caso de perda ou roubo e o suporte técnico pode apagar o dispositivo móvel de qualquer usuário que for reportado como perdido ou roubado.<br /><br /> Fornecem o registro do dispositivo móvel em um ambiente de PKI para controle e segurança adicionais.|  
|Os funcionários poderão ser produtivos mesmo se não estiverem em suas mesas.|Quando os funcionários não estiverem em suas mesas e não possuírem computadores portáteis, não poderão acessar seus aplicativos usando computadores de quiosques disponíveis pela empresa.|Os funcionários podem usar os quiosques de informática para acessar seus aplicativos e dados.|  
|Geralmente, a continuidade de negócios tem prioridade sobre a instalação de aplicativos necessários e de atualizações de software.|Os aplicativos e as atualizações de software que necessitam de instalação durante o dia e frequentemente interrompem usuários do trabalho porque seus computadores ficam mais lentos e são reiniciados durante a instalação.|Os usuários podem configurar suas horas de trabalho para evitar que o software necessário seja instalado enquanto eles estão usando seus computadores.|  

 Para atender aos requisitos, Anibal usa estes recursos de gerenciamento e opções de configuração do Configuration Manager:  

-   Gerenciamento de aplicativos  
-   Gerenciamento de dispositivos móveis  

Ele implementa esses itens usando as etapas de configuração na tabela a seguir:  

|Etapas de configuração|Resultado|  
|-------------------------|-------------|  
|Aníbal verifica se os novos usuários têm contas de usuário no Active Directory e cria uma nova coleção baseada em consultas no Configuration Manager para esses usuários. Em seguida, ele define a afinidade de dispositivo de usuário para esses usuários criando um arquivo que mapeia as contas de usuário para os computadores primários que eles usarão e importa esse arquivo no Configuration Manager.<br /><br /> Os aplicativos que os novos usuários devem ter já estão criados no Configuration Manager. Então ele implanta esses aplicativos que têm a finalidade de Necessário na coleção que contém os novos usuários.|Por conta das informações de afinidade de dispositivo de usuário, os aplicativos são instalados em cada computador (ou computadores) primário do usuário antes que ele se conecte.<br /><br /> Os aplicativos estão prontos para uso assim que o usuário se conectar com êxito.|  
|Anibal instala e configura as funções do sistema de site do catálogo de aplicativos para que os usuários possam procurar aplicativos a serem instalados. Ele cria implantações de aplicativos que têm a finalidade de Disponível e implanta esses aplicativos na coleção que contém os novos usuários.<br /><br /> Para os aplicativos que possuem um número restrito de licenças, Anibal configura esses aplicativos para solicitarem aprovação.|Agora os usuários podem usar o Catálogo de Aplicativos para procurar os aplicativos que eles têm permissão para instalar. Os usuários podem instalar os aplicativos imediatamente ou solicitar aprovação e retornar para o Catálogo de Aplicativos para instalá-los depois que o suporte técnico tiver aprovado a solicitação.|  
|Anibal cria um conector do Exchange Server no Configuration Manager para gerenciar os dispositivos móveis que se conectam ao Exchange Server local da empresa. Ele define esse conector com configurações de segurança que incluem o requisito para uma senha forte e bloqueia o dispositivo móvel após um período de inatividade.<br /><br /> Para gerenciamento adicional de dispositivos que executam o Windows Phone 8, Windows RT e iOS, Aníbal obtém uma assinatura do Microsoft Intune. Em seguida, ele instala a função do sistema de sites do ponto de conexão de serviço. Essa solução de gerenciamento de dispositivo móvel dá à empresa maior suporte para gerenciamento desses dispositivos. Isso inclui disponibilizar aplicativos para que os usuários instalem nesses dispositivos e amplo gerenciamento de configurações. Além disso, as conexões de dispositivo móvel são protegidas usando certificados PKI criados e implantados automaticamente pelo Intune.<br /><br /> Depois de configurar o ponto de conexão de serviço e a assinatura para serem usados com o Configuration Manager, Aníbal envia uma mensagem de email aos usuários que têm esses dispositivos móveis para que eles cliquem em um link para iniciar o processo de registro.<br /><br /> Para que os dispositivos móveis sejam registrados pelo Microsoft Intune, Anibal usa configurações de conformidade para definir configurações de segurança para esses dispositivos móveis. Essas configurações incluem o requisito para definir uma senha forte e bloqueiam o dispositivo móvel após um período de inatividade.|Com essas duas soluções de gerenciamento de dispositivo móvel, agora a organização de TI pode fornecer informações de relatórios sobre os dispositivos móveis em uso na rede da empresa e sua conformidade com as configurações de segurança definidas.<br /><br /> Os usuários veem como apagar remotamente o dispositivo móvel usando o Catálogo de Aplicativos ou o Portal da Empresa caso o dispositivo móvel seja perdido ou roubado. O suporte técnico também é instruído sobre como apagar remotamente um dispositivo móvel do usuário utilizando o console do Configuration Manager.<br /><br /> Além disso, para dispositivos móveis registrados pelo Microsoft Intune, agora Anibal pode implantar aplicativos móveis para que os usuários possam instalar, coletar mais dados de inventário desses dispositivos e ter melhor controle de gerenciamento sobre os dispositivos por poderem acessar mais configurações.|  
|A Trey Research tem vários computadores de quiosque que são usados por funcionários que visitam o escritório. Os funcionários desejam que seus aplicativos estejam disponíveis sempre que eles se conectarem. No entanto, Aníbal não quer instalar localmente todos os aplicativos em cada computador.<br /><br /> Para isso, Anibal cria os aplicativos necessários que têm dois tipos de implantação:<br /><br /> **O primeiro:** uma instalação completa local do aplicativo que tem o requisito de só poder ser instalado em um dispositivo primário do usuário.<br /><br /> **O segundo:** uma versão virtual do aplicativo que tem o requisito de não poder ser instalado no dispositivo primário do usuário.|Quando funcionários visitantes se conectam em um computador de quiosque, eles veem os aplicativos de que precisam exibidos como ícones na área de trabalho do computador de quiosque. Quando eles executam o aplicativo, ele é transmitido como um aplicativo virtual. Dessa forma, eles poderão ser tão produtivos como se estivessem usando sua área de trabalho.|  
|Aníbal permite que os usuários saibam que eles podem configurar seu horário comercial no Centro de Software e seleciona opções para impedir atividades de implantação de software durante este período e quando o computador está em modo de apresentação.|Como os usuários podem controlar quando o Configuration Manager implanta software nos computadores, os usuários permanecem mais produtivos durante o dia de trabalho.|  

 Essas etapas de configuração e esses resultados permitem que a Trey Research dê poderes a seus funcionários com êxito, garantindo o acesso a aplicativos de qualquer dispositivo.  

###  <a name="BKMK_ScenarioUnify"></a> Cenário de exemplo: unificar o gerenciamento de conformidade de dispositivos  
 A Trey Research quer uma solução de gerenciamento de clientes unificada que garante que os computadores executem software antivírus que seja atualizado automaticamente. Ou seja:  

-   O Firewall do Windows está habilitado.  
-   Atualizações críticas de software estão instaladas.  
-   Chaves específicas do Registro estão definidas.  
-   Os dispositivos móveis gerenciados não podem instalar nem executar aplicativos não assinados.  

A empresa também quer expandir essa proteção para a Internet para laptops que se movem da intranet para a Internet.  

Anibal mapeia esses requisitos da empresa para os seguintes cenários:  

|Requisito|Estado atual de gerenciamento de clientes|Estado futuro de gerenciamento de clientes|  
|-----------------|-------------------------------------|------------------------------------|  
|Todos os computadores executam software antimalware que possui arquivos de definição atualizados e habilitam o Firewall do Windows.|Computadores diferentes executam soluções antimalware diferentes que nem sempre são mantidas atualizadas. Embora o Firewall do Windows esteja habilitado por padrão, os usuários às vezes o desabilitam.<br /><br /> Os usuários devem entrar em contato com o suporte técnico se for detectado malware em seu computador.|Todos os computadores executam a mesma solução antimalware que baixa automaticamente os arquivos mais recentes de atualização da definição e reabilita automaticamente o Firewall do Windows se os usuários o desabilitarem.<br /><br /> O suporte técnico será notificado automaticamente por email se for detectado malware.|  
|Todos os computadores instalam atualizações de software críticas no primeiro mês de lançamento.|Embora as atualizações de software sejam instaladas em computadores, muitos computadores não instalam automaticamente as atualizações de software críticas até dois ou três meses após o lançamento. Isso os deixa vulneráveis a ataques durante esse período.<br /><br /> Para os computadores que não instalam as atualizações de software críticas, o suporte técnico primeiro envia mensagens de email para que os usuários instalem as atualizações. Para computadores que permanecem não compatíveis, os engenheiros se conectam remotamente a esses computadores e instalam manualmente as atualizações de software que faltam.|A taxa de conformidade atual no mês especificado é melhorada para mais de 95% sem enviar mensagens de email nem solicitar que o suporte técnico as instale manualmente.|  
|As configurações de segurança para aplicativos específicos serão verificadas e corrigidas regularmente se for necessário.|Os computadores executam scripts de inicialização complexos que dependem da associação ao grupo do computador para redefinir valores do Registro para aplicativos específicos.<br /><br /> Como esses scripts são executados somente na inicialização e alguns computadores são deixados ligados por vários dias, o suporte técnico não pode verificar se há descompasso na configuração em tempo adequado.|Os valores do Registro são verificados e corrigidos automaticamente sem depender da associação ao grupo do computador ou reiniciar o computador.|  
|Os dispositivos móveis não podem instalar nem executar aplicativos não seguros.|Os usuários são solicitados a não baixar e executar aplicativos potencialmente não seguros da Internet. Mas não há controles em vigor para monitorar ou aplicar isso.|Os dispositivos móveis gerenciados com o Microsoft Intune ou com o Configuration Manager impedem automaticamente que aplicativos não assinados sejam instalados ou executados.|  
|Laptops que se movem da intranet para a Internet devem ser mantidos seguros.|Para usuários que viajam, eles frequentemente não podem se conectar pela conexão VPN diariamente. Esses laptops ficam fora de conformidade com os requisitos de segurança.|Uma conexão com a Internet é tudo o que é necessário para que os laptops sejam mantidos em conformidade com requisitos de segurança. Os usuários não precisam se conectar ou usar a conexão VPN.|  

 Para atender aos requisitos, Anibal usa estes recursos de gerenciamento e opções de configuração do Configuration Manager:  

-   Endpoint Protection  
-   Atualizações de software  
-   Configurações de conformidade  
-   Gerenciamento de dispositivos móveis  
-   Gerenciamento de clientes baseado na Internet  

Ele implementa esses itens usando as etapas de configuração na tabela a seguir:  

|Etapas de configuração|Resultado|  
|-------------------------|-------------|  
|Aníbal configura o Endpoint Protection. Ele habilita a configuração do cliente para desinstalar outras soluções antimalware e habilita o Firewall do Windows. Ele configura as regras de implantação automática para que os computadores verifiquem e instalem as atualizações de definições mais recentes regularmente.|A solução antimalware única ajuda a proteger todos os computadores usando a sobrecarga administrativa mínima. Como o suporte técnico é notificado automaticamente por mensagem de email se for detectado antimalware, os problemas podem ser resolvidos rapidamente. Isso ajuda a impedir ataques em outros computadores.|  
|Para ajudar a aumentar as taxas de conformidade, Aníbal usa regras de implantação automática, define janelas de manutenção para servidores e investiga as vantagens e desvantagens de usar Wake on LAN para computadores que hibernam.|A conformidade com atualizações de software críticas aumenta e reduz o requisito para que os usuários ou o suporte técnico instale atualizações de software manualmente.|  
|Anibal usa configurações de conformidade para verificar a presença de aplicativos especificados. Quando os aplicativos são detectados, os itens de configuração verificam os valores do Registro e os corrigem automaticamente se estiverem fora de conformidade.|Ao usar itens de configuração e linhas de base de configuração que são implantadas em todos os computadores e verificar a conformidade todos os dias, não é mais necessário que você separe os scripts que dependem da associação de computador e as reinicializações do computador.|  
|Anibal usa configurações de conformidade para dispositivos móveis registrados e configura o conector do Exchange Server para impedir que os aplicativos não assinados de sejam instalados e executados em dispositivos móveis.|Como os aplicativos não assinados são proibidos, os dispositivos móveis são protegidos automaticamente contra aplicativos potencialmente prejudiciais.|  
|Aníbal verifica se os computadores e servidores do sistema de sites têm certificados PKI que o Configuration Manager exige para conexões HTTPS. Em seguida, ele instala funções adicionais do sistema de sites na rede de perímetro que aceitam conexões de cliente da Internet.|Os computadores que se movem da intranet para a Internet automaticamente continuam sendo gerenciados pelo Configuration Manager quando eles têm uma conexão com a Internet. Esses computadores não dependem de usuários se conectando ao computador ou à conexão VPN.<br /><br /> Esses computadores continuam a ser gerenciados para antimalware e Firewall do Windows, atualizações de software e itens de configuração. Como resultado, os níveis de conformidade aumentarão automaticamente.|  

 Essas etapas de configuração e os resultados têm como efeito a unificação com êxito pela Trey Research do gerenciamento de conformidade de dispositivos.  

###  <a name="BKMK_ScenarioSimplify"></a> Cenário de exemplo: simplificar o gerenciamento de clientes para os dispositivos  
 A Trey Research quer que todos os computadores novos instalem automaticamente a imagem de computador base da empresa, que executa o Windows 7. Depois que a imagem do sistema operacional for instalada nesses computadores, eles devem ser gerenciados e monitorados quanto ao software adicional instalado pelos usuários. Os computadores que armazenam informações altamente confidenciais requerem políticas de gerenciamento mais restritivas do que os outros computadores. Por exemplo, os engenheiros de suporte técnico não devem se conectar a eles remotamente, a entrada de PIN do BitLocker deve ser usada para reinicializações, e apenas os administradores locais podem instalar software.  

 Anibal mapeia esses requisitos da empresa para os seguintes cenários:  

|Requisito|Estado atual de gerenciamento de clientes|Estado futuro de gerenciamento de clientes|  
|-----------------|-------------------------------------|------------------------------------|  
|Novos computadores são instalados com o Windows 7.|O suporte técnico instala e configura o Windows 7 para os usuários e envia o computador ao respectivo local.|Os novos computadores seguem diretamente para o destino final, são conectados à rede e instalam e configuram o Windows 7 automaticamente.|  
|Os computadores devem ser gerenciados e monitorados. Isso inclui a coleta de dados de inventário de hardware e software para ajudar a determinar os requisitos de licenciamento.|O cliente do Configuration Manager é implantado usando a instalação automática do cliente por push. O suporte técnico investiga falhas de instalação e clientes que não enviam dados de inventário quando deveriam.<br /><br /> As falhas são frequentes devido às dependências de instalação que não são atendidas e à corrupção do WMI no cliente.|A instalação do cliente e os dados de inventário coletados de computadores são mais confiáveis e requerem menos intervenção do suporte técnico. Os relatórios mostram o uso de software para obter informações de licença.|  
|Alguns computadores precisam ter políticas de gerenciamento mais rigorosas.|Em consequência das políticas de gerenciamento mais rigorosas, esses computadores não são gerenciados pelo Configuration Manager no momento.|Esses computadores são gerenciados usando o Configuration Manager para acomodar as exceções sem sobrecarga administrativa adicional.|  

 Para atender aos requisitos, Anibal usa estes recursos de gerenciamento e opções de configuração do Configuration Manager:  

-   Implantação de sistema operacional  
-   Implantação do cliente e status do cliente  
-   Configurações de conformidade  
-   Configurações do cliente  
-   Métodos de inventário e Asset Intelligence  
-   Administração baseada em funções  

Ele implementa esses itens usando as etapas de configuração na tabela a seguir:  

|Etapas de configuração|Resultado|  
|-------------------------|-------------|  
|Aníbal captura uma imagem do sistema operacional de um computador com o Windows 7 instalado e configurado com as especificações da empresa. Em seguida, ele implanta o sistema operacional nos novos computadores usando o PXE e o suporte de um computador desconhecido. E também instala o cliente do Configuration Manager como parte da implantação do sistema operacional.|Novos computadores estão em funcionamento mais rapidamente sem a intervenção do suporte técnico.|  
|Anibal configura a instalação automática do cliente por push em todo o site para instalar o cliente do Configuration Manager em qualquer computador que estiver descoberto. Isso garante que os computadores que ainda não tiveram a imagem gerada pelo cliente instalem o cliente para que o computador seja gerenciado pelo Configuration Manager.<br /><br /> Anibal configura o status de cliente para corrigir automaticamente os problemas do cliente que estão descobertos. Ele configura também as configurações do cliente que habilitam a coleção necessária de dados do inventário e configura o Asset Intelligence.|Instalar o cliente com o sistema operacional é mais rápido e mais confiável do que esperar que o Configuration Manager descubra o computador e, então, tente instalar os arquivos de origem do cliente nele. No entanto, ao deixar a opção de push de cliente automático habilitada, você fornece um método de backup para um computador, que já tem o sistema operacional instalado, instalar o cliente quando é conectado a uma rede.<br /><br /> As configurações do cliente garantem que os clientes enviem suas informações de inventário para o site regularmente. Isso, além dos testes de status do cliente, ajuda a manter o cliente executando com intervenções mínimas do suporte técnico. Por exemplo, as corrupções do WMI são detectadas e corrigidas automaticamente.<br /><br /> Os relatórios do Asset Intelligence ajudam a monitorar o uso de software e licenças.|  
|Aníbal cria uma coleção para os computadores que devem ter configurações de política mais rigorosas. Em seguida, ele cria uma configuração de dispositivo de cliente personalizada para essa coleção, que desabilita o controle remoto, permite a entrada de PIN do BitLocker e permite que somente administradores locais instalem software.<br /><br /> Aníbal configura a administração baseada em função para que os engenheiros do suporte técnico não vejam essa coleção de computadores. Isso ajuda a garantir que esses computadores não sejam acidentalmente gerenciados como computadores padrão.|Agora, esses computadores são gerenciados pelo Configuration Manager, mas com configurações específicas que não exigem um novo site.<br /><br /> A coleção desses computadores não fica visível aos engenheiros do suporte técnico. Isso ajuda a reduzir a possibilidade de envio acidental a esses computadores de implantações e scripts que são para computadores padrão.|  

 Essas etapas de configuração e os resultados têm como efeito a simplificação com êxito pela Trey Research do gerenciamento de clientes de dispositivos.  

##  <a name="BKMK_NextSteps"></a> Próximas etapas  
 Antes de instalar o Configuration Manager, familiarize-se com alguns termos e conceitos básicos específicos do Configuration Manager.  

-   Se estiver familiarizado com o System Center 2012 Configuration Manager, consulte [O que mudou no System Center Configuration Manager do System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) para entender os novos recursos.  
-   Para ter uma visão geral técnica do System Center Configuration Manager, consulte [Aspectos fundamentais do System Center Configuration Manager](../../core/understand/fundamentals.md).  

Quando estiver familiarizado com os conceitos básicos, use a documentação do System Center Configuration Manager para ajudá-lo a implantar e usar com êxito o Configuration Manager.  
