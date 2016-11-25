---
title: "Escolher o MDM híbrido ou o Intune autônomo | System Center Configuration Manager"
description: "Escolha se deseja implantar o gerenciamento de dispositivo móvel híbrido com o Intune e com o Configuration Manager ou executar o Intune autônomo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2e6ec1b2b822298d4fa6a17e2d7439167b83080a

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Escolha entre o gerenciamento de dispositivo móvel híbrido e independente do Microsoft Intune com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Uma das perguntas feitas com mais frequência sobre o MDM (gerenciamento de dispositivo móvel) com o Microsoft Intune é “Devo implantar o MDM híbrido com o Configuration Manager e o Intune ou executar o Intune autônomo na configuração somente de nuvem?” É uma decisão importante e que não é facilmente alterada após a implementação.  

 Uma implantação do Intune autônomo não envolve nenhuma infraestrutura local e é gerenciada por meio de um console Web. Ela é ágil, leve e popular com organizações de visão de nuvem em primeiro lugar.  

 Uma implantação do MDM híbrida envolve o Intune e Configuration Manager e é gerenciada usando ferramentas familiares para administradores experientes do Configuration Manager. Ela oferece o gerenciamento de “painel de controle único” do MDM e clientes tradicionais, assim como a escala em ambientes grandes.  

##  <a name="what-does-intune-standalone-mean"></a>O que significa Intune autônomo?  
 O Intune em seu núcleo é um serviço de nuvem. Há datacenters do Intune hospedados na América do Norte, Europa e Ásia fornecendo aos dispositivos móveis políticas de segurança, perfis de Wi-Fi e email, aplicativos, inventário e muito mais.  

 Uma implantação do Intune autônomo não exige nenhuma infraestrutura local. Todas as configuração, gerenciamento, implantação e relatórios são executados por meio de um console baseado na Web, que é acessível de qualquer lugar do mundo.  

 Para trabalhar com aplicativos locais, como Microsoft Exchange e o NDES (Serviço de Registro de Dispositivo de Rede), os conectores locais estão disponíveis para fornecer conectividade para o serviço do Intune.  

 Sendo um serviço de nuvem, o Intune pode ser compilado e implantado em um curto período.  

##  <a name="what-does-hybrid-mdm-mean"></a>O que significa MDM híbrido?  
 Para organizações que desejam maximizar seu investimento do Configuration Manager, clientes que precisam de um controle refinado ou clientes que excederem as limitações de escala do Intune, uma implementação híbrida que usa o Intune para gerenciar dispositivos móveis está disponível.  

 As implantações híbridas exigem o Microsoft System Center 2012 Configuration Manager SP1 ou superior.  

 O serviço Intune é conectado ao Configuration Manager com a função de sistema de sites Ponto de Conexão do Servidor (anteriormente conhecida como o Conector do Microsoft Intune), que é instalada no site primário ou de administração central de uma hierarquia do Configuration Manager. Um locatário do Intune pode ser conectado apenas a uma hierarquia do Configuration Manager e uma hierarquia do Configuration Manager pode ser conectada apenas a um locatário do Intune.  

 Em uma configuração de MDM híbrido, parte do processamento e sobrecarga de armazenamento é realizada pela infraestrutura do Configuration Manager local. Esse ganho de eficiência permite que o MDM híbrido expanda mais do que o Intune autônomo.  

 Uma implantação híbrida permite o uso de ferramentas que são familiares aos administradores do Configuration Manager. Recursos avançados como RBAC (Controle de Administração Baseado em Função), SSRS (SQL Server Reporting Services) e agrupamento de dispositivos e usuários complexo usando Consultas de Associação da Coleção são disponibilizados para dispositivos móveis quando o MDM híbrido é implementado.  

##  <a name="planning-choices-and-intune-deployment-timelines"></a>Opções de planejamento e cronogramas de implantação do Intune  
 A evolução e a inovação do Intune estão ocorrendo em um ritmo acelerado com atualizações mensais fornecendo recursos novos ou aprimorados, escala aprimorada, novas experiências do console de administração pelo Portal do Azure, grupos dinâmicos pelo Azure Active Directory e muito mais. Assim, quaisquer decisões de design devem considerar a direção futura do produto.  

 Muitos dos recursos exclusivos que uma configuração híbrida fornece no momento serão funcionalmente replicados no Intune autônomo, uma vez que o serviço é desenvolvido em curto, médio e longo prazo.  

 Se estiver decidindo entre o autônomo e o híbrido, considere os cronogramas de implantação. É comum para os clientes passarem por várias iterações de implantação incluindo as fases de design, criação, teste de aceitação do usuário e piloto, muitas vezes levando vários meses para a conclusão, antes de estarem prontos para implantar na produção. Por esse motivo, ao escolher um design de hierarquia do Intune, considere o momento em que a implantação real ocorrerá e a direção em curto, médio e longo prazo do serviço.  

 Como o serviço Intune continua a evoluir, nosso objetivo é simplificar sua opção de configuração. No futuro, o único motivo para escolher um ambiente de MDM híbrido deve ser para clientes que exigem um único console de gerenciamento para clientes tradicionais e de dispositivos móveis.  Estamos trabalhando bastante para aumentar a escalabilidade, adicionando o acesso baseado em função pelo Portal do Azure e grupos dinâmicos por meio da integração mais profunda do Azure Active Directory, tudo alinhado a atualizações de serviço em curto e médio prazo.  

 Por fim, também estamos trabalhando para garantir independentemente da escolha de configuração feita hoje, você possa mudar facilmente entre as opções de configuração híbrida e autônoma de forma ininterrupta. Alternar autoridades de MDM hoje requer a intervenção manual do Suporte da Microsoft e o esforço significativo do locatário. Para simplificar isso, nosso objetivo é permitir a coexistência do híbrido e do Intune autônomo, permitindo que você mova os usuários entre os dois tipos de gerenciamento, mas sem exigir a escolha de uma configuração ou outra.  Essa alteração também remove os desafios atuais de ter que ligar para o suporte e elimina o cancelamento de registro e a repetição do registro de dispositivos.  

##  <a name="pros-and-cons-of-intune-standalone"></a>Prós e contras do Intune autônomo  

|Prós|Contras|  
|----------|----------|  
|Implantação e criação rápidas<br /><br /> Nenhuma infraestrutura local<br /><br /> Lançamentos de recursos e atualizações mais frequentes<br /><br /> Baixa curva de aprendizado<br /><br /> Console de administração disponível externamente|Funcionalidade de relatório limitados<br /><br /> Restrição de função de segurança limitada<br /><br /> Não há ferramentas externas (como o PowerShell etc.)<br /><br /> Inventário de aplicativos limitado<br /><br /> Funcionalidades básicas de agrupamento de usuários e dispositivos<br /><br /> Silverlight necessário|  

##  <a name="pros-and-cons-of-hybrid-mdm"></a>Prós e contras do MDM híbrido  

|Prós|Contras|  
|----------|----------|  
|Capacidade de expansão<br /><br /> Ferramentas avançadas (como o console do Configuration Manager, PowerShell, registro em log etc.)<br /><br /> RBAC (Controle de Acesso Baseado em Função)<br /><br /> Relatórios avançados<br /><br /> Gerenciamento de “painel de controle único” para o MDM + clientes tradicionais<br /><br /> Inventário de aplicativos estendido<br /><br /> Agrupamento avançado de usuários e dispositivos<br /><br /> Suporte para vários conectores do Exchange Online e do Exchange locais<br /><br /> Suporte para várias funções de NDES/CRP<br /><br /> Capacidade de marcar dispositivos como "de propriedade da empresa"<br /><br /> Mais funcionalidades de solução de problemas<br /><br /> CALs de usuário do Configuration Manager incluídas na assinatura|Complexidade local (configuração e gerenciamento)<br /><br /> Curva de aprendizado acentuada<br /><br /> Manutenção necessária para atualizações e lançamentos de recursos<br /><br /> Requisitos de licenciamento adicionais (como Windows, SQL Server etc.)|  

##  <a name="planning-decisions"></a>Decisões de planejamento  
 ![decisões&#45;híbridas](../../mdm/understand/media/hybrid-decisions.png)  

|Etapa|Decisão|
|-|-|  
|<img src="media/hybrid-1.png" style="min-width:32px">|**Quantos dispositivos você pretende gerenciar?**<br /><br /> O Intune autônomo dá suporte a até 50.000 dispositivos. O MDM híbrido dá suporte a até 300.000 dispositivos.<br /><br /> Para qualquer implantação de tamanho significativo, autônoma ou MDM híbrida, sugerimos que você entre em contato com a equipe de contas da Microsoft. A equipe de contas da Microsoft pode colocá-lo em contato com especialistas do Intune que podem discutir mais sobre a expansão e as limitações.|  
|![híbrido&#45;2](../../mdm/understand/media/hybrid-2.png)|**O controle de acesso refinado é necessário? (RBAC)**<br /><br /> O RBAC (Controle de Acesso com Base na Função) foi adicionado ao System Center 2012 Configuration Manager. O RBAC permite que os administradores do Configuration Manager criem e implantem conjuntos de permissões complexos para restringir o acesso do administrador a funções e objetos do Configuration Manager.<br /><br /> O Intune autônomo fornece apenas duas funções de administrador: Acesso Completo e Acesso Somente Leitura.<br /><br /> Se sua organização precisa definir o escopo de determinados administradores para determinados usuários, dispositivos, funções ou objetos, o Configuration Manager com RBAC é necessário.<br /><br /> Se sua organização tiver uma equipe administrativa pequena e você não precisar da complexidade do controle de acesso refinado, o Intune com as funções de segurança internas será a melhor opção.|  
|![híbrido&#45;3](../../mdm/understand/media/hybrid-3.png)|**São necessárias funcionalidades de relatório avançadas?**<br /><br /> O MDM híbrido com o Configuration Manager inclui recursos de relatório avançados usando o SSRS (SQL Server Reporting Services). O Configuration Manager é fornecido com 34 relatórios internos do MDM e mais de 400 relatórios padrão do Configuration Manager. O SSRS também permite que os analistas de negócios e administradores criem seus próprios relatórios personalizados. Além disso, o banco de dados do Configuration Manager pode ser consultado por ferramentas externas, como as ferramentas de orquestração, para fornecer funções específicas, como alertas personalizados. Sendo o Configuration Manager a executar os relatórios, todos os relatórios também podem incluir dados não MDM, como inventário de computadores tradicionais lado a lado com o inventário de dispositivos móveis.<br /><br /> O Intune autônomo fornece nove relatórios. Esses relatórios não são personalizáveis e oferecem variáveis de entrada limitadas. Os relatórios podem ser impresso ou exportados em CSV ou HTML.<br /><br /> Se sua organização requerer funções de relatório avançadas e tiver a largura de banda e o conhecimento para gerenciar o SSRS, o MDM híbrido será a melhor opção.<br /><br /> Se sua organização desejar relatórios predefinidos e um mecanismo de relatórios simples de usar, a funcionalidade de relatórios do Intune autônomo deverá ser suficiente.|  
|![híbrido&#45;4](../../mdm/understand/media/hybrid-4.png)|**Você está gerenciando dispositivos Windows 10 sem acesso à Internet?**<br /><br /> No Configuration Manager (Branch Atual), os dispositivos Windows 10 podem ser gerenciados por meio do canal do MDM usando apenas a infraestrutura local.<br /><br /> O recurso de Gerenciamento de Dispositivo Móvel Local foi projetado para permitir o gerenciamento do MDM para clientes não acessíveis pela Internet e destina-se principalmente para dispositivos de uso único (como dispositivos de quiosque) e dispositivos de IoT.<br /><br /> Devido à abordagem somente de nuvem do Intune autônomo, todos os dispositivos gerenciados devem ter acesso à Internet. Se sua organização desejar gerenciar dispositivos Windows 10 por meio do Gerenciamento de Dispositivo Móvel Local, uma configuração de MDM híbrido será necessária. Observe que o Gerenciamento de Dispositivo Móvel Local não dá suporte ao gerenciamento de dispositivos móveis da Internet e da intranet ao mesmo tempo.|  
|![híbrido&#45;5](../../mdm/understand/media/hybrid-5.png)|**Você precisa do inventário de aplicativos completo?**<br /><br /> Por padrão, o Intune autônomo coletará o inventário de aplicativos apenas para aplicativos que o Intune gerencia e implanta. Isso significa que os relatórios de inventário não conterão informações dos aplicativos de sideload que foram instalados pelos usuários fora do Portal da Empresa do Intune.<br /><br /> O MDM híbrido com o Configuration Manager permite que os administradores designem determinados dispositivos como “de propriedade da empresa”. Quando um dispositivo estiver definido como um dispositivo da empresa, um inventário de aplicativos estendido será coletado, fornecendo acesso a uma lista de aplicativos completa dos dispositivos.<br /><br /> Se sua organização requerer informações sobre os aplicativos instalados pessoalmente de dispositivos gerenciados, o MDM híbrido será necessário. Antes de tomar uma decisão com base nessa opção, considere o impacto na privacidade de seu usuário final.|  
|![híbrido&#45;6](../../mdm/understand/media/hybrid-6.png)|**Você deseja gerenciar computadores da maneira tradicional de cliente FAT?**<br /><br /> Um benefício que o MDM híbrido oferece em relação à configuração autônoma é o gerenciamento de “painel de controle único”. Isso significa que uma organização pode gerenciar toda sua frota de computadores desktop, servidores e dispositivos móveis de uma única ferramenta de gerenciamento, o console do Configuration Manager. Além disso, com o cliente do Configuration Manager, funções de gerenciamento avançado, como o inventário de hardware e software, o gerenciamento de atualização software, a implantação de software e a implantação de sistema operacional, estão disponíveis para dispositivos que não sejam móveis.<br /><br /> Se sua organização desejar gerenciar clientes Windows, Linux/UNIX e MAC tradicionais, o Configuration Manager será a principal plataforma de gerenciamento.<br /><br /> O Intune autônomo também oferece gerenciamento de computadores tradicionais (Windows 7, 8.1 e 10) usando o cliente de gerenciamento de computadores do Intune. Ele oferece o gerenciamento básico de computadores e inclui o inventário de hardware, atualizações do Windows, Endpoint Protection e implantação de software simples. O cliente não funciona com o Configuration Manager, portanto pode ser usado em implantações de MDM híbrido e do Intune autônomo.|  
|![híbrido&#45;7](../../mdm/understand/media/hybrid-7.png)|**Você deseja gerenciar a infraestrutura local?**<br /><br /> Um determinado nível de complexidade e a sobrecarga de gerenciamento vêm com qualquer infraestrutura local. O Configuration Manager é um produto requer conhecimento, experiência e investimento significativos para gerenciar e manter sua infraestrutura.<br /><br /> No mínimo, o MDM híbrido requer um único site primário do Configuration Manager, com a função de banco de dados, função de serviços de relatório e a função de ponto de conexão de serviço. Se o gerenciamento de computadores tradicionais for necessário, as funções do catálogo de aplicativos, ponto de atualização de software, ponto de distribuição e ponto de gerenciamento também poderão ser necessárias. As funções avançadas, como implantação de certificado, gerenciamento de Mac e Endpoint Protection adicionam ainda mais funções e complexidade.<br /><br /> A hierarquia do Configuration Manager requer gerenciamento e manutenção significativos para garantir sua integridade e funcionamento conforme necessário.<br /><br /> Se a sobrecarga de uma hierarquia do Configuration Manager não for desejada, uma implantação do Intune autônomo será a melhor opção.|  
|![híbrido&#45;8](../../mdm/understand/media/hybrid-8.png)|**Você precisa de ferramentas externas?**<br /><br /> O Configuration Manager é um produto maduro de nível corporativo e inclui muitas maneiras de interagir com o serviço sem usar o console. Uma implantação do MDM híbrido permite que os administradores usem o SDK do Configuration Manager ou o PowerShell para gerenciar dispositivos móveis de forma programática. Ela também permite que os administradores utilizem ferramentas como o System Center Orchestrator, PowerBI e vários suplementos de terceiros.<br /><br /> Em uma implantação do Intune autônomo, toda a administração deve ser executada por meio do console do Silverlight e não há ferramentas externas disponíveis.|  
|![híbrido&#45;9](../../mdm/understand/media/hybrid-9.png)|**Você deseja atualizações rápidas de recursos do MDM?**<br /><br /> Mesmo que o Configuration Manager (Branch Atual) ofereça o gerenciamento rápido de atualizações e recursos, o desenvolvimento de serviços de nuvem, como o Intune, funciona bem para a implantação de produção ainda mais rápida.<br /><br /> O Intune autônomo provavelmente receberá novos recursos antes de uma implantação do MDM híbrido.<br /><br /> Se sua organização quiser ser de ponta, o Intune autônomo oferecerá os recursos de MDM mais recentes no melhor momento possível.|



<!--HONumber=Nov16_HO1-->


