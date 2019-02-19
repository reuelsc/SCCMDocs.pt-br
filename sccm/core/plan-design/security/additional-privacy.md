---
title: Informações de privacidade adicionais
titleSuffix: Configuration Manager
description: Saiba como a Microsoft coleta e usa os dados do Configuration Manager.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e5a42249df462be1584a153657a42ae325f1b9a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125350"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Mais informações sobre privacidade no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


## <a name="updates-and-servicing"></a>Atualizações e serviços

O Configuration Manager usa um modelo de atualização que ajuda a manter seu ambiente atual com os recursos e as atualizações mais recentes. Esse recurso usa uma função do sistema de site chamada de ponto de conexão de serviço. Você escolhe o servidor onde deseja instalar essa função. 

Para saber mais sobre as informações coletadas e como elas são usadas, veja [Dados de uso](#usage-data).



## <a name="usage-data"></a>Dados de uso

O Configuration Manager coleta dados de diagnóstico e de uso sobre si mesmo, que a Microsoft usa para melhorar a experiência de instalação, a qualidade e a segurança de versões futuras.
Os dados de diagnóstico e de uso são habilitados para cada hierarquia do Configuration Manager. Eles consistem em consultas do SQL Server que são executadas semanalmente em cada site primário e no site de administração central. Quando a hierarquia usa um site de administração central, os dados dos sites primários são replicados nesse site. No site de nível superior da hierarquia, o ponto de conexão de serviço envia essas informações quando verifica se há atualizações. Se o ponto de conexão de serviço estiver no modo offline, as informações serão transferidas por meio da ferramenta de conexão de serviço.

O Configuration Manager só coleta dados do banco de dados do SQL Server do site e não coleta dados diretamente de clientes ou de servidores do site.

Os administradores podem alterar o nível dos dados coletados na seção **Dados de Uso** do console do Configuration Manager.

Para saber mais sobre níveis de dados de uso e configurações, confira [Dados de uso e diagnóstico](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).



## <a name="customer-experience-improvement-program"></a>Programa de Aperfeiçoamento da Experiência do Usuário

> [!Note]  
> A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto.

O Programa de Aperfeiçoamento da Experiência do Usuário coleta informações básicas do console do Configuration Manager sobre sua configuração de hardware e como você usa nosso software e nossos serviços para identificar tendências e padrões de uso. O Programa de Aperfeiçoamento da Experiência do Usuário também coleta o tipo e o número de erros encontrados, o desempenho de software e hardware, bem como a velocidade dos serviços. Não coletamos seu nome, endereço nem outras informações de contato. Nenhum dado do CEIP é coletado dos computadores cliente.

Utilizamos essas informações para melhorar a qualidade, a confiabilidade e o desempenho dos softwares e serviços da Microsoft.

Para saber mais sobre as informações coletadas, processadas ou transmitidas pelo Programa de Aperfeiçoamento da Experiência do Usuário, consulte a [Política de privacidade do Programa de Aperfeiçoamento da Experiência do Usuário](https://go.microsoft.com/fwlink/?LinkID=525211).



## <a name="log-analytics-connector"></a>Conector do Log Analytics

O conector do Log Analytics sincroniza dados, como coleções, do Configuration Manager para o serviço de nuvem do Azure. A chave secreta e a ID da assinatura do Microsoft Azure são armazenadas no banco de dados do Configuration Manager quando um administrador configura o recurso. O segredo do cliente do Azure Active Directory e a chave compartilhada do espaço de trabalho do Microsoft Azure são armazenados no banco de dados local do Configuration Manager. Todas as comunicações entre o Configuration Manager e o Azure usam HTTPS. Nenhuma outra informação é fornecida à Microsoft sobre as coleções além de dados de uso e de diagnóstico aleatórios. 

Para saber mais sobre as dados que o Log Analytics coleta, veja [Segurança de dados do Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-security).



## <a name="asset-intelligence"></a>Asset Intelligence

O Asset Intelligence permite que os administradores definam, controlem e gerenciem de modo pró-ativo a conformidade com os padrões de configuração. Obter medições e relatórios sobre a implantação e o uso de aplicações físicas e virtuais ajudas as organizações a tomarem decisões comerciais melhores sobre licenciamento de software e manterem a conformidade com os contratos de licenciamento. Após a coleta de dados de uso dos clientes do Configuration Manager, você pode usar diferentes recursos para exibir os dados, incluindo coleções, consultas e relatórios.

Durante cada sincronização, um catálogo de softwares conhecidos é baixado da Microsoft. Você pode optar por enviar informações à Microsoft sobre títulos de software não categorizados descobertos em sua organização para serem pesquisados e adicionados ao catálogo. Antes de carregar essas informações, uma caixa de diálogo mostra os dados que serão carregados. Os dados carregados não podem ser cancelados. O Asset Intelligence não envia informações sobre os usuários e os computadores ou o uso da licença para a Microsoft.

Após o upload de um título de software, os pesquisadores da Microsoft identificam, categorizam e disponibilizam esse conhecimento para todos os outros clientes que usam esse recurso e outros consumidores do catálogo. Qualquer título de software carregado se torna público. O aplicativo e sua categorização se tornam parte do catálogo e, em seguida, podem ser baixados para outros consumidores do catálogo. Antes de configurar a coleta de dados do Asset Intelligence e optar por enviar informações à Microsoft, considere os requisitos de privacidade da sua organização.

O Asset Intelligence não está habilitado por padrão no Configuration Manager. O carregamento de títulos não categorizados nunca ocorre automaticamente e o sistema não foi projetado para automatizar essa tarefa. Você deve selecionar e aprovar manualmente o carregamento de cada título de software.



## <a name="endpoint-protection"></a>Endpoint Protection

Anteriormente, o Microsoft Cloud Protection Service era conhecido como Microsoft Active Protection Service ou MAPS.

Os produtos aplicáveis são o System Center Endpoint Protection e o recurso Endpoint Protection do System Center Configuration Manager (para gerenciar o System Center Endpoint Protection e o Windows Defender para Windows 10). Este recurso não está implementado para o System Center Endpoint Protection para Linux ou o System Center Endpoint Protection para Mac.

A comunidade antimalware do Microsoft Active Protection Service é uma comunidade online internacional voluntária que inclui usuários do System Center Endpoint Protection. Quando você ingressa no Microsoft Cloud Protection Service, o System Center Endpoint Protection envia informações à Microsoft automaticamente. A Microsoft usa as informações para determinar o software a fim de investigar possíveis ameaças e ajudar a melhorar a eficácia do System Center Endpoint Protection. Essa comunidade ajuda a parar a disseminação de novas infecções por software mal-intencionado. Se um relatório do Microsoft Cloud Protection Service incluir detalhes sobre malware ou software potencialmente não desejado que o cliente do Endpoint Protection pode remover, o Microsoft Cloud Protection Service baixará a última assinatura para resolver o problema. O Microsoft Cloud Protection Service também pode encontrar "falsos positivos" e corrigi-los. (Falsos positivos ocorrem quando algo originalmente identificado como malware na verdade não é). 

Os relatórios do Microsoft Cloud Protection Service incluem informações sobre possíveis arquivos de malware, como nomes de arquivos, hash criptográfico, fornecedor, tamanho e carimbos de data. Além disso, o Microsoft Cloud Protection Service pode coletar URLs completas para indicar a origem do arquivo. Essas URLs podem, ocasionalmente, conter informações pessoais, como termos de pesquisa ou dados inseridos em formulários. Os relatórios também podem incluir ações que você executou quando o Endpoint Protection o notificou sobre um software indesejado. Os relatórios do Microsoft Cloud Protection Service incluem essas informações para ajudar a Microsoft a medir a eficácia com que o Endpoint Protection detecta e remove malwares e softwares potencialmente indesejados e tenta identificar novos malwares.

É possível ingressar no Microsoft Cloud Protection Service se você tem uma associação básica ou avançada. Os relatórios de membros básicos contêm as informações descritas anteriormente. Os relatórios de membros avançados são mais abrangentes e podem incluir detalhes adicionais sobre o software detectado pelo Endpoint Protection, como a localização desse software, nomes de arquivo, como o software opera e como ele afetou o computador. Esses relatórios e os relatórios de outros usuários do Endpoint Protection que participam do Microsoft Cloud Protection Service ajudam os pesquisadores da Microsoft a descobrir novas ameaças com mais rapidez. Em seguida, são criadas definições de malware para programas que atendam aos critérios de análise, e as definições atualizadas são disponibilizadas a todos os usuários por meio do Microsoft Update.

Para ajudar a detectar e corrigir alguns tipos de infecções de malware, o produto envia regularmente ao Microsoft Cloud Protection Service informações sobre o estado de segurança do computador. Essas informações incluem informações sobre as configurações de segurança do computador e arquivos de log que descrevem os drivers e outros softwares que são carregados durante a inicialização do computador.

Um número que identifica o PC de forma exclusiva também é enviado. Além disso, o Microsoft Cloud Protection Service pode coletar os endereços IP a que os possíveis arquivos de malware se conectam.

Os relatórios do Microsoft Cloud Protection Service são usados para aprimorar softwares e serviços da Microsoft. Os relatórios também podem ser usados para fins estatísticos ou outros relacionados a teste ou análise, e para gerar definições. Somente funcionários, prestadores de serviços, parceiros e fornecedores da Microsoft que têm uma necessidade comercial de usar os relatórios podem acessá-los.

O Microsoft Cloud Protection Service não coleta informações pessoais intencionalmente. Quando o Microsoft Cloud Protection Service coleta informações pessoais, a Microsoft não utiliza essas informações para identificar ou entrar em contato com você.

Para obter mais informações, confira [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection).



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Hierarquia do Site – Exibição Geográfica com Bing Maps

No console do Configuration Manager, vá até o espaço de trabalho **Monitoramento** e selecione o nó **Hierarquia do Site** e alterne para o **Modo de Exibição Geográfico**. Essa exibição permite o uso de mapas fornecidos pelo Microsoft Bing Mapas para exibir a topologia de servidor físico do Configuration Manager. Para habilitar esse recurso, as informações de local fornecidas são enviadas de seu servidor ao serviço Web Bing Mapas.

A Microsoft usa as informações para operar e aprimorar o Microsoft Bing Maps e outros sites e serviços da Microsoft. Para obter mais informações, consulte a [Política de Privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=823548).

Você pode optar por não usar a Exibição Geográfica para a Hierarquia do Site. A exibição padrão Diagrama Hierárquico permite visualizar a hierarquia e não usa o serviço Bing Mapas.



## <a name="microsoft-intune-subscription"></a>Assinatura do Microsoft Intune

Clientes que adquiriram uma assinatura do Microsoft Intune podem usar o Configuration Manager para gerenciar seus dispositivos móveis que se conectaram por meio do Microsoft Intune. A [Política de Privacidade do Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=262214) se aplica aos serviços online da Microsoft, que incluem o Microsoft Intune. Se os clientes tiverem uma assinatura do Microsoft Intune, a [Política de Privacidade do Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=262214) deverá ser lida em conjunto com esta política de privacidade.

Todas as comunicações com o Microsoft Intune usam HTTPS. Para configurar a assinatura do Microsoft Intune e baixar a CSR (Solicitação de Assinatura de Certificado) necessária para configurar o suporte para iOS, um administrador deve se conectar ao Microsoft Intune usando uma conta de trabalho e a senha. Essas credenciais não são armazenadas no Configuration Manager. Todas as outras comunicações com o Microsoft Intune são autenticadas usando certificados PKI gerados automaticamente pelo Microsoft Intune.

Para gerenciar dispositivos conectados ao Microsoft Intune, algumas informações são enviadas e recebidas do Microsoft Intune. Essas informações incluem o nome UPN de todos os usuários atribuídos ao serviço e informações de inventário de dispositivo dos dispositivos gerenciados pelo Microsoft Intune. Os metadados, como o nome do aplicativo, o editor e a versão, do conteúdo atribuído aos pontos de distribuição Manage.Microsoft.com são enviados ao Microsoft Intune. O conteúdo binário real atribuído a um ponto de distribuição Manage.Microsoft.com é criptografado antes de ser carregado no Microsoft Intune.

Esse recurso não está configurado por padrão. Os administradores controlam o conteúdo transferido para o ponto de distribuição Manage.Microsoft.com e os usuários atribuídos ao serviço. O recurso pode ser removido a qualquer momento.
