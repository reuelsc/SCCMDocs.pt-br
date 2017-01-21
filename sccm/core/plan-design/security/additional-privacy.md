---
title: "Política de privacidade do System Center Configuration Manager – Informações adicionais | Microsoft Docs"
description: "Saiba como a Microsoft coleta e usa dados de uma implantação do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- en-gb
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 613b7dbf81de84129e113468d554d8430cbc3182

---
# <a name="additional-information-about-privacy-for-system-center-configuration-manager"></a>Informações adicionais sobre privacidade no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


## <a name="updates-and-servicing"></a>Atualizações e serviços
O System Center Configuration Manager apresenta um novo modelo de atualização que ajuda a manter sua implantação do Configuration Manager atualizada com os recursos e atualizações mais recentes. Quando instalado, este recurso adiciona uma nova função de sistema de sites a um servidor do site que o administrador escolhe, chamado ponto de conexão de serviço. Para obter detalhes sobre quais informações são coletadas e como são usadas, consulte seção sobre Dados de Uso desta declaração.


## <a name="usage-data"></a>Dados de uso
O System Center Configuration Manager coleta dados de diagnóstico e de uso sobre si mesmo, que são usados pela Microsoft para aprimorar a experiência, a qualidade e a segurança da instalação de versões futuras.
Os dados de diagnóstico e de uso são habilitados para cada hierarquia do System Center Configuration Manager. Eles consistem em consultas do SQL Server que são executadas semanalmente em cada site primário e no site de administração central. Quando a hierarquia usa um site de administração central, os dados dos sites primários são replicados nesse site. No site de nível superior da hierarquia, o ponto de conexão de serviço envia essas informações quando verifica se há atualizações. Se o ponto de conexão de serviço estiver no modo offline, as informações serão transferidas por meio da ferramenta de conexão de serviço.

O Configuration Manager apenas coleta dados do banco de dados do SQL Server dos sites e não coleta dados diretamente de clientes ou de servidores do site.

Os administradores podem alterar o nível dos dados coletados na seção "Dados de Uso" do console do Configuration Manager.

Para obter mais informações, consulte o artigo "Saiba mais" sobre Configurações e níveis de dados de uso em [http://go.microsoft.com/fwlink/?LinkID=626566](http://go.microsoft.com/fwlink/?LinkID=626566).


## <a name="customer-experience-improvement-program"></a>Programa de Aperfeiçoamento da Experiência do Usuário
O CEIP (Programa de Aperfeiçoamento da Experiência do Usuário ) coleta informações básicas do console do Configuration Manager sobre a configuração do seu hardware e como você usa nosso software e nossos serviços, a fim de identificar tendências e padrões de uso. CEIP também coleta o tipo e o número de erros encontrados, o desempenho de software e hardware e a velocidade dos serviços.  Não coletaremos seu nome, endereço ou outras informações de contato. Nenhum dado do CEIP é coletado dos computadores cliente.

Utilizamos essas informações para melhorar a qualidade, a confiabilidade e o desempenho dos softwares e serviços da Microsoft.

Para saber mais sobre as informações coletadas, processadas ou transmitidas pelo Programa de Aperfeiçoamento da Experiência do Usuário, consulte a política de privacidade dele em [http://go.microsoft.com/fwlink/?LinkID=525211](http://go.microsoft.com/fwlink/?LinkID=525211).

## <a name="oms-connector"></a>Conector do OMS
O Conector do Microsoft Operations Management Suite sincroniza dados como coleções do System Center Configuration Manager ao Microsoft Operations Management Suite. A chave secreta e a ID da assinatura do Microsoft Azure são armazenadas no banco de dados do Configuration Manager quando um administrador configura o recurso. O segredo do cliente do Azure Active Directory e a chave compartilhada do espaço de trabalho do Microsoft Operations Management Suite são armazenados no banco de dados local do System Center Configuration Manager. Todas as comunicações entre o System Center Configuration Manager e o Microsoft Operations Management Suite usam HTTPS. Não são fornecidas informações adicionais sobre as coleções para a Microsoft além de dados de telemetria aleatórios. Para obter detalhes sobre quais informações são coletadas pelo Microsoft Operations Management Suite, leia mais sobre a segurança de dados do Log Analytics em [http://go.microsoft.com/fwlink/?LinkId=823545](http://go.microsoft.com/fwlink/?LinkId=823545).

## <a name="asset-intelligence"></a>Asset Intelligence
O Asset Intelligence permite que os administradores de TI definam, controlem e gerenciem de modo pró-ativo a conformidade com os padrões de configuração. Obter medições e relatórios sobre a implantação e o uso de aplicações físicas e virtuais ajudas as organizações a tomarem decisões comerciais melhores sobre licenciamento de software e manterem a conformidade com os contratos de licenciamento. Após a coleta de dados de uso de clientes do Configuration Manager, os administradores podem utilizar recursos diferentes para exibir os dados, incluindo coleções, consultas e relatório.

Durante cada sincronização, um catálogo de softwares conhecidos será baixado da Microsoft. O administrador de TI pode optar por enviar informações à Microsoft sobre títulos de software não categorizados descobertos na organização a serem pesquisados e adicionados ao catálogo. Antes do carregamento dessas informações, uma caixa de diálogo mostra exatamente quais dados serão carregados. Os dados carregados não podem ser cancelados. O Asset Intelligence não envia informações sobre os usuários e os computadores ou o uso da licença para a Microsoft.

Após o carregamento de um título de software, os pesquisadores da Microsoft identificam, categorizam e disponibilizam esse conhecimento para todos os outros clientes que usam esse recurso e outros consumidores do catálogo. Qualquer título de software carregado se torna público, o que significa que o conhecimento desse determinado aplicativo e sua categorização se tornam parte do catálogo e podem ser baixados para outros consumidores do catálogo. Antes de configurar a coleta de dados do Asset Intelligence e optar por enviar informações à Microsoft, considere os requisitos de privacidade da sua organização.

O Asset Intelligence não está habilitado no System Center Configuration Manager por padrão. O carregamento de títulos não categorizados nunca ocorre automaticamente e o sistema não foi projetado para a automatização dessa tarefa. Você deve selecionar e aprovar manualmente o carregamento de cada título de software.

## <a name="endpoint-protection"></a>Endpoint Protection
Produtos aplicáveis do Microsoft Cloud Protection Service (anteriormente conhecido como Microsoft Active Protection Service, ou MAPS): System Center Endpoint Protection e o recurso Endpoint Protection do System Center Configuration Manager (para gerenciar o System Center Endpoint Protection e o Windows Defender para Windows 10). Este recurso não está implementado para o System Center Endpoint Protection para Linux ou o System Center Endpoint Protection para Mac.

A comunidade antimalware do Microsoft Active Protection Service é uma comunidade online internacional voluntária que inclui usuários do System Center Endpoint Protection. Quando você se juntar ao Microsoft Cloud Protection Service, o System Center Endpoint Protection enviará automaticamente informações à Microsoft para ajudar a Microsoft a determinar qual software investigar em busca de ameaças potenciais e ajudar a aprimorar a eficiência do System Center Endpoint Protection. Essa comunidade ajuda a parar a disseminação de novas infecções por software mal-intencionado. Se um relatório do Microsoft Cloud Protection Service incluir detalhes sobre malware ou software não desejado que o cliente do Endpoint Protection pode remover, o Microsoft Cloud Protection Service baixará a assinatura mais recente para resolver a questão. O Microsoft Cloud Protection Service também pode encontrar "falsos positivos" (quando algo identificado originalmente como malware na verdade não é) e corrigi-los.

Os relatórios do Microsoft Cloud Protection Service incluem informações sobre possíveis arquivos de malware, como nomes de arquivos, hash criptográfico, fornecedor, tamanho e carimbos de data. Além disso, o Microsoft Cloud Protection Service pode coletar URLs completas para indicar a origem do arquivo. Essas URLs podem, ocasionalmente, conter informações pessoais, como termos de pesquisa ou dados inseridos em formulários. Os relatórios também podem incluir ações executadas por você quando o Endpoint Protection lhe notificou sobre um software indesejado. Os relatórios do Microsoft Cloud Protection Service incluem essas informações para ajudar a Microsoft a medir a eficácia com que o Endpoint Protection detecta e remove malwares e softwares potencialmente indesejados e tenta identificar novos malwares.

É possível participar do Microsoft Cloud Protection Service com uma associação básica ou avançada. Os relatórios do membro básico contêm as informações descritas acima. Os relatórios do membro avançado são mais abrangentes e podem incluir detalhes adicionais sobre o software que o Endpoint Protection detecta, inclusive a localização desse software, nomes de arquivos, como o software opera e como ele afetou seu computador. Esses relatórios, em conjunto com relatórios de outros usuários do Endpoint Protection que participam do Microsoft Cloud Protection Service, ajudam os pesquisadores da Microsoft a descobrir novas ameaças com mais rapidez. Em seguida, são criadas definições de malware para programas que atendam aos critérios de análise, e as definições atualizadas são disponibilizadas a todos os usuários por meio do Microsoft Update.

Para ajudar a detectar e consertar certos tipos de infecções por malware, o produto envia regularmente ao Microsoft Cloud Protection Service algumas informações sobre o estado de segurança de seu PC. São incluídas informações sobre as configurações de segurança do seu PCs e arquivos de log descrevendo os drivers e outros softwares que são carregados enquanto seu PC é inicializado.
Um número que identifica o PC de forma exclusiva também é enviado. Além disso, o Microsoft Cloud Protection Service pode coletar os endereços IP a que os possíveis arquivos de malware se conectam.

Os relatórios do Microsoft Cloud Protection Service são usados para aprimorar softwares e serviços da Microsoft. Os relatórios também podem ser usados para fins estatísticos ou outros relacionados a testes ou análises, e para gerar definições. Somente funcionários, prestadores de serviços, parceiros e fornecedores da Microsoft que tiverem uma necessidade comercial de usar os relatórios têm acesso a eles.

O Microsoft Cloud Protection Service não coleta informações pessoais intencionalmente. Quando o Microsoft Cloud Protection Service coleta informações pessoais, a Microsoft não utiliza essas informações para identificar ou entrar em contato com você.

Detalhes adicionais relacionados aos dados coletados podem ser encontrados na documentação do produto em [http://go.microsoft.com/fwlink/?LinkId=823547](http://go.microsoft.com/fwlink/?LinkId=823547).

## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Hierarquia do Site – Exibição Geográfica com Bing Maps
A Hierarquia do Site – exibição geográfica permite exibir a topologia do servidor físico do Configuration Manager usando mapas fornecidos pelo Microsoft Bing Mapas. Para habilitar esse recurso, as informações de local fornecidas são enviadas do seu servidor ao serviço Web Bing Maps.

A Microsoft usa as informações para operar e aprimorar o Microsoft Bing Maps e outros sites e serviços da Microsoft. Para obter mais informações, consulte a Política de Privacidade da Microsoft em http://go.microsoft.com/fwlink/?LinkId=823548.
Você pode optar por não usar a Exibição Geográfica para a Hierarquia do Site. A exibição Diagrama Hierárquico permite visualizar a hierarquia e não usa o serviço Bing Maps.

## <a name="microsoft-intune-subscription"></a>Assinatura do Microsoft Intune
Clientes que adquiriram uma assinatura do Microsoft Intune podem usar o Configuration Manager para gerenciar seus dispositivos móveis que se conectaram através do Microsoft Intune. [A Política de Privacidade do Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkId=262214) se aplica aos serviços online da Microsoft, incluindo o Microsoft Intune. Se os clientes tiverem uma assinatura do Microsoft Intune, a [Política de Privacidade do Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkId=262214) deverá ser lida em conjunto com esta política de privacidade.

Todas as comunicações com o Microsoft Intune usam HTTPS. Para configurar a assinatura do Microsoft Intune e baixar a CSR (Solicitação de Assinatura de Certificado) necessária para configurar o suporte para iOS, um administrador deve entrar no Microsoft Intune usando sua conta organizacional e senha. Essas credenciais mão são armazenadas no Configuration Manager. Todas as outras comunicações com o Microsoft Intune são autenticadas usando certificados PKI que são gerados automaticamente pelo Microsoft Intune.

Para gerenciar dispositivos conectados ao Microsoft Intune, algumas informações são enviadas para e recebidas do Microsoft Intune. Essas informações incluem o nome UPN de todos os usuários atribuídos ao serviço e informações de inventário de dispositivo dos dispositivos gerenciados pelo Microsoft Intune. Os metadados, como o nome do aplicativo, o fornecedor e a versão, do conteúdo atribuído aos pontos de distribuição Manage.Microsoft.com são enviados ao Microsoft Intune. O conteúdo binário real atribuído a um ponto de distribuição Manage.Microsoft.com é criptografado antes de ser carregado no Microsoft Intune.

Esse recurso não está configurado por padrão. Os administradores controlam qual conteúdo é transferido para o ponto de distribuição Manage.Microsoft.com e quais usuários são atribuídos ao serviço. O recurso pode ser removido a qualquer momento.



<!--HONumber=Dec16_HO3-->


