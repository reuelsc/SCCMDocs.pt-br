---
title: Introdução às configurações de conformidade
titleSuffix: Configuration Manager
description: Saiba mais sobre conceitos básicos e como funcionam as configurações de conformidade
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec350bdb6b3b421d95bf13eafc562919bccc3c38
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>Introdução às configurações de conformidade no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de criar as configurações de conformidade do Configuration Manager, saiba mais sobre os conceitos básicos e entenda como eles funcionam.  



## <a name="how-compliance-settings-work"></a>Como funcionam as configurações de conformidade  
 As configurações de conformidade permitem que você gerencie a configuração e a conformidade de clientes em sua organização.  

 Os itens de configuração se enquadram em duas categorias principais:  

-   **Configurações para dispositivos gerenciados com o cliente do Configuration Manager** –normalmente, trata-se de dispositivos nos quais você instalou o software cliente do Configuration Manager para gerenciar o dispositivo.  

-   **Configurações para dispositivos gerenciados sem o cliente do Configuration Manager** – normalmente, trata-se de dispositivos gerenciados com o Microsoft Intune ou com o gerenciamento de dispositivo local do Configuration Manager.  



## <a name="what-devices-are-supported"></a>Quais dispositivos têm suporte?  

| Tipo de dispositivo | Mais informações |  
|------------|----------------------|  
| Computadores Windows (com o cliente do Configuration Manager) | Crie itens de configuração personalizados para avaliar objetos como chaves do Registro, arquivos e atributos do Active Directory.<br /><br /> Ao usar o tipo do item de configuração do Windows 10, selecione as configurações em uma lista predefinida. |  
| Computadores Windows (registrados com o Microsoft Intune) | Selecione as configurações em uma lista predefinida. |  
| Dispositivos iOS (registrados com o Microsoft Intune) | Selecione as configurações em uma lista predefinida. |  
| Dispositivos Android (registrados com o Microsoft Intune) | Selecione as configurações em uma lista predefinida. |  
| Dispositivos Windows Phone (registrados com o Microsoft Intune) | Selecione as configurações em uma lista predefinida. |  
| Computadores Mac (com o cliente do Configuration Manager) | Crie itens de configuração personalizados para avaliar objetos, como as preferências do macOS, e os resultados retornados por um script. |  
| Computadores Mac (registrados com o Microsoft Intune) | Selecione as configurações em uma lista predefinida. |  



## <a name="what-is-a-configuration-item"></a>O que é um item de configuração?  
 Um item de configuração é um contêiner que armazena informações específicas. As informações definidas dependem do tipo de item de configuração. Os itens de configuração podem incluir as seguintes informações:

-   **Informações do método de detecção** referem-se somente aos itens de configuração do Windows que contêm configurações de aplicativo. Detectam se um aplicativo está instalado. Essa detecção usa o arquivo do Windows Installer para o aplicativo ou um script personalizado.  

-   As **configurações** representam as condições comerciais ou técnicas para avaliar a conformidade em dispositivos cliente. Defina uma nova configuração ou procure uma configuração existente em um computador de referência.  

-   As **regras de conformidade** especificam as condições que definem a conformidade de uma configuração de item de configuração. Antes que um cliente avalie a conformidade de uma configuração, ela deve ter, pelo menos, uma regra de conformidade. Algumas configurações corrigem valores não compatíveis. Crie novas regras ou procure uma configuração existente em um item de configuração para selecionar as regras dele.  

-   **Plataformas compatíveis** são as plataformas de dispositivo definidas, nas quais o cliente avalia a conformidade dos itens de configuração. Se você implantar um item de configuração em um dispositivo que não está na lista de plataformas compatíveis, ele não avaliará a conformidade.  



## <a name="what-is-a-configuration-baseline"></a>O que é uma linha de base de configuração?  
 Defina uma linha de base de configuração que inclui os itens de configuração a serem avaliados. Inclua também as configurações e regras que descrevem o nível necessário de conformidade. Importe esses dados de configuração de pacotes de configuração do Configuration Manager. A Microsoft e outros fornecedores definem esses pacotes de configuração. Se preferir, crie novos itens de configuração e linhas de base de configuração.  

 Depois de definir uma linha de base de configuração, implante-a em coleções de usuários e dispositivos. Em seguida, o cliente avalia as configurações de linha de base quanto à conformidade de acordo com um agendamento. Implante mais de uma linha de base de configuração em dispositivos. Essa granularidade proporciona maior controle sobre a conformidade. 

 Dispositivos cliente avaliam sua conformidade com relação a cada linha de base de configuração implantada e, imediatamente, informam os resultados ao site usando mensagens de estado e de status. Se um dispositivo estiver desconectado da rede no momento, mas baixou a linha de base de configuração, ele ainda avaliará a conformidade dos itens de configuração. Ele envia as informações de conformidade quando se reconecta.  

### <a name="monitoring-configuration-baselines"></a>Monitorando linhas de base de configuração
- Monitore os resultados da avaliação de conformidade no console do Configuration Manager, no espaço de trabalho **Monitoramento**, no nó **Implantações**. Por exemplo:
    - Causas comuns de não conformidade
    - Erros
    - O número de dispositivos e usuários afetados
- Execute relatórios de configurações de conformidade com detalhes adicionais. Por exemplo:
    - Quais dispositivos estão em conformidade ou fora de conformidade
    - Qual elemento da linha de base de configuração está fazendo com que um computador fique fora de conformidade
- Exiba os resultados da avaliação de conformidade nos computadores Windows que executam o cliente do Configuration Manager. Abra o painel de controle do **Configuration Manager** e alterne para a guia **Configurações**.  



## <a name="user-data-and-profiles-configuration-items"></a>Itens de configuração de perfis e dados do usuário  
 Os itens de configuração de perfis e dados de usuário incluem configurações que controlam como os usuários nos computadores que executam o Windows 8 e posterior gerenciam:  
   - Redirecionamento de pasta
   - Arquivos offline
   - Perfis móveis  

Implante esses itens de configuração em coleções de usuários. Monitore sua conformidade por meio do nó **Monitoramento** do console do Configuration Manager. Ao contrário de outros itens de configuração, não os adicione às linhas de base de configuração antes de implantá-los. Implante-os diretamente clicando em **Implantar** na faixa de opções.  

 Para obter mais informações, consulte [Criar itens de configuração de perfis e dados de usuário](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  



## <a name="remote-connection-profiles"></a>Perfis de conexão remota  
 Os perfis de conexão remota fornecem um conjunto de ferramentas e recursos para ajudá-lo a criar, implantar e monitorar configurações de conexão remota. Implantando essas configurações em dispositivos, você minimiza o esforço que os usuários finais precisam fazer para se conectarem seus computadores à rede corporativa.  

Para saber mais, confira [Criar perfis de conexão remota](/sccm/compliance/deploy-use/create-remote-connection-profiles).  



## <a name="windows-edition-upgrade"></a>Atualização de edição do Windows
A política de atualização de edição atualiza automaticamente os dispositivos que executam algumas versões do Windows 10 para uma edição mais recente. Essa política fornece uma nova chave do produto (Product Key) ou um novo arquivo de licença que é consumido pelo dispositivo para que ele seja atualizado.

Para obter mais informações, consulte [Atualizar dispositivos Windows com a política de atualização de edição](/sccm/compliance/deploy-use/upgrade-windows-version)



## <a name="microsoft-edge-browser-profiles"></a>Perfis do navegador Microsoft Edge
<!-- 1357310 -->
A partir da versão 1802, para os clientes que utilizam o navegador da Web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) em clientes do Windows 10, crie uma política de configurações de conformidade para definir várias configurações do Microsoft Edge. 

Para obter mais informações, consulte [Perfis do navegador Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles).

