---
title: "Introdução às configurações de conformidade | System Center Configuration Manager"
description: "Saiba como as configurações de conformidade funcionam no System Center Configuration Manager. Também saiba mais sobre os conceitos básicos que você precisa saber."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 395a0927d1ac39f941a504efb0a32c9a70f9477a


---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>Introdução às configurações de conformidade no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de começar a criar itens de configuração do System Center Configuration Manager, leia este tópico para entender como funcionam as configurações de conformidade e para saber mais sobre os conceitos básicos que precisará conhecer.  

## <a name="how-compliance-settings-works"></a>Como funcionam as configurações de conformidade  
 As configurações de conformidade permitem que você gerencie a configuração e a conformidade de servidores, laptops, computadores desktop e dispositivos móveis na sua organização.  

 Os itens de configuração se enquadram em duas categorias principais:  

-   **Configurações para dispositivos gerenciados com o cliente do Configuration Manager** –normalmente, trata-se de dispositivos nos quais você instalou o software cliente do Configuration Manager para gerenciar o dispositivo.  

-   **Configurações para dispositivos gerenciados sem o cliente do Configuration Manager** – normalmente, trata-se de dispositivos gerenciados com o Microsoft Intune ou com o gerenciamento de dispositivo local do Configuration Manager.  

## <a name="what-devices-are-supported"></a>Quais dispositivos têm suporte?  


|Tipo de dispositivo|Mais informações|  
|------------|----------------------|  
|Computadores Windows (com o cliente do Configuration Manager)|Permite que você crie itens de configuração personalizados que lhe permitem avaliar itens como chaves de registro, arquivos e atributos do Active Directory.<br /><br /> Quando usa o tipo do item de configuração do Windows 10, você seleciona as configurações que deseja em uma lista predefinida.|  
|Computadores Windows (registrados com o Microsoft Intune)|Selecione as configurações desejadas em uma lista predefinida.|  
|Dispositivos iOS (registrados com o Microsoft Intune)|Selecione as configurações desejadas em uma lista predefinida.|  
|Dispositivos Android (registrados com o Microsoft Intune)|Selecione as configurações desejadas em uma lista predefinida.|  
|Dispositivos Windows Phone (registrados com o Microsoft Intune)|Selecione as configurações desejadas em uma lista predefinida.|  
|Computadores Mac (com o cliente do Configuration Manager)|Permite que você crie itens de configuração personalizados que lhe permitem avaliar itens como valores de preferências do Mac OS X (lista de propriedades) e os resultados retornados por um script.|  
|Computadores Mac (registrados com o Microsoft Intune)|Selecione as configurações desejadas em uma lista predefinida.|  

## <a name="what-is-a-configuration-item"></a>O que é um item de configuração?  
 Um item de configuração pode ser considerado um contêiner que armazena as informações a seguir (as informações que você configura dependem do tipo de item de configuração):  

-   **Informações de método de detecção** (somente para itens de configuração do Windows que contêm configurações do aplicativo) - permite detectar se um aplicativo está instalado detectando o arquivo do instalador do Windows do aplicativo ou usando um script personalizado.  

-   **Configurações** - as configurações representam as condições comerciais ou técnicas que são usadas para avaliar a conformidade nos dispositivos cliente. Você pode definir uma nova configuração ou navegar até uma configuração existente em um computador de referência.  

-   **Regras de conformidade** - as regras de conformidade especificam as condições que definem a conformidade de um item de configuração. Antes que uma configuração possa ser avaliada quanto à conformidade, ela deve ter pelo menos uma regra de conformidade. Algumas configurações permitem que você corrija valores considerados não compatíveis. Você pode criar novas regras ou navegar até uma configuração existente em qualquer item de configuração para selecionar regras nele.  

-   **Plataformas com suporte** - são as plataformas de dispositivo que você define e nas quais será verificada a conformidade do item de configuração. Se você implantar um item de configuração em um dispositivo que não está na lista de plataformas com suporte, ele não será avaliado quanto à conformidade.  

## <a name="what-is-a-configuration-baseline"></a>O que é uma linha de base de configuração?  
 A conformidade é avaliada por meio da definição de uma linha de base de configuração que contém os itens de configuração que você deseja avaliar e configurações e regras que descrevem o nível de conformidade que você precisa ter. É possível importar esses dados de configuração da Web em pacotes de configuração do Microsoft System Center Configuration Manager como melhores práticas que são definidas pela Microsoft e outros fornecedores, no Configuration Manager, e que você importar para o Configuration Manager. Também é possível criar novos itens de configuração e linhas de base de configuração.  

 Após a definição de uma linha de base de configuração, você pode implantá-la para usuários e dispositivos por meio de coleções e avaliar suas configurações de conformidade segundo uma agenda. Várias linhas de base de configuração podem ser implantadas nos dispositivos. Isso propicia um alto nível de controle.  

 Dispositivos cliente avaliam sua conformidade com relação a cada linha de base de configuração implantada e, imediatamente, informam os resultados ao site usando mensagens de estado e de status. Se um dispositivo cliente não estiver conectado à rede, mas tiver baixado itens de configuração que são referenciados em uma linha de base de configuração implantada, a linha de base de configuração será avaliada quanto à conformidade. As informações de conformidade são enviadas quando a conexão for restabelecida.  

 É possível monitorar os resultados da avaliação da linha de base de configuração no nó **Implantações** no espaço de trabalho **Monitoramento** no console do Configuration Manager para exibir as causas mais comuns dos erros e dos casos de não conformidade, bem como o número de usuários e dispositivos afetados. Você também pode executar relatórios de configurações de conformidade para encontrar detalhes adicionais, como quais dispositivos estão ou não em conformidade e qual elemento da linha de base de configuração está fazendo com que um computador não esteja em conformidade. Você também pode exibir resultados de avaliação de conformidade de computadores Windows que executam o software cliente do Configuration Manager usando a guia **Configurações** no **Configuration Manager** no Painel de Controle.  

## <a name="user-data-and-profiles-configuration-items"></a>Itens de configuração de perfis e dados do usuário  
 Itens de configuração de perfis e dados do usuário contêm configurações que controlam como os usuários em sua hierarquia gerenciam o redirecionamento de pastas, arquivos offline e perfis de roaming em computadores que executam o Windows 8 e posterior. É possível implantar essas configurações em coleções de usuários e monitorar sua conformidade no nó **Monitoramento** do console do Configuration Manager. Diferente de outros itens de configuração, você não os acrescenta às linhas de base de configuração antes de implantá-las. Você pode implantá-las diretamente na caixa de diálogo **Implantar Item de Configuração de Perfis e Dados de Usuário** .  

 Para obter detalhes, consulte [Criar itens de configuração de perfis e dados de usuário](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

## <a name="remote-connection-profiles"></a>Perfis de conexão remota  
 Os perfis de conexão remota fornecem um conjunto de ferramentas e recursos para ajudar você a criar, implantar e monitorar configurações de conexão remota nos dispositivos da sua organização. Implantando essas configurações, você minimiza o esforço que os usuários finais precisam fazer para se conectarem aos seus computadores na rede corporativa.  

Para obter detalhes, consulte [Create remote connection profiles (Criar perfis de conexão remota)](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

## <a name="windows-edition-upgrade"></a>Atualização de edição do Windows
A Política de Atualização de Edição permite atualizar automaticamente dispositivos que executam determinadas versões do Windows 10 para uma edição mais recente, fornecendo um novo arquivo de licença ou chave do produto (Product Key).

Para obter detalhes, consulte [Atualizar dispositivos Windows com a política de atualização de edição](/sccm/compliance/deploy-use/upgrade-windows-version)



<!--HONumber=Nov16_HO1-->


