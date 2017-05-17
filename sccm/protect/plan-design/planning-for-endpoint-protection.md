---
title: Planejar o Endpoint Protection | Microsoft Docs
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
caps.latest.revision: 16
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 8f4ec982a54cf3cefef310268a54850e70e2e63a
ms.openlocfilehash: 6c4273dae99ec8db2cf827f463b973e876d0d35b
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="planning-for-endpoint-protection-in-system-center-configuration-manager"></a>Planejando o Endpoint Protection no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


O Endpoint Protection no System Center Configuration Manager permite gerenciar políticas antimalware e a segurança do Firewall do Windows para computadores cliente em sua hierarquia do Configuration Manager.  

> [!IMPORTANT]  
>  Você deve ter licença para usar o Endpoint Protection para gerenciar clientes na sua hierarquia do Configuration Manager.  

Ao usar o Endpoint Protection com o Configuration Manager, você tem os seguintes benefícios:  

-   Configure políticas antimalware, configurações do Firewall do Windows e gerencie a Proteção Avançada contra Ameaças do Windows Defender para alguns grupos de computadores  

-   Use as atualizações de software do Configuration Manager para baixar os arquivos de definição antimalware mais recentes para manter os computadores cliente atualizados  

-   Envie notificações por email, use o monitoramento no console e exiba relatórios para manter usuários administrativos informados quando for detectado malware nos computadores cliente  

Computadores Windows 10 não exigem nenhum cliente adicional para o gerenciamento do Endpoint Protection. No Windows 8.1 e em computadores mais antigos, o Endpoint Protection instala seu próprio cliente além do cliente do Configuration Manager. O cliente do Endpoint Protection tem os seguintes recursos:  

-   Detecção e correção de malware e spyware  

-   Detecção e correção de rootkits  

-   Avaliação de vulnerabilidades crítica e atualizações automáticas de mecanismos e definições  

-   Detecção de vulnerabilidade de rede por meio do Sistema de Inspeção de Rede  

-   Integração com o Cloud Protection Service para relatar a presença de malware à Microsoft. Ao optar por fazer parte desse serviço, o cliente do Windows Defender ou o Endpoint Protection poderá baixar as definições mais recentes do Centro de Proteção contra Malware quando for detectado malware não identificado em um computador.  

> [!NOTE]  
>  O cliente do Endpoint Protection pode ser instalado em um servidor que executa o Hyper-V e em máquinas virtuais convidadas com sistemas operacionais com suporte. Para evitar o uso excessivo de CPU, as ações do Endpoint Protection têm um atraso aleatório interno para que os serviços não sejam executados simultaneamente.  

  Além disso, o Endpoint Protection no Configuration Manager permite gerenciar as configurações do Firewall do Windows no console do Configuration Manager.  

 [Cenário de exemplo: usar o System Center Endpoint Protection para proteger os computadores contra malware no System Center Configuration Manager](../deploy-use/scenarios-endpoint-protection.md) mostra como você pode configurar e gerenciar o Endpoint Protection e o Firewall do Windows.  

## <a name="managing-malware-with-endpoint-protection"></a>Gerenciando malware com o Endpoint Protection  

O Endpoint Protection no Configuration Manager permite que você crie políticas antimalware que contêm configurações para o cliente do Endpoint Protection. Você pode implantar essas políticas antimalware nos computadores cliente e monitorá-los no nó **Status do Endpoint Protection** no espaço de trabalho **Monitoramento** ou usando relatórios do Configuration Manager.  

 Informações adicionais:  

-   [Criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](../deploy-use/endpoint-antimalware-policies.md) – Crie, implante e monitore políticas antimalware com uma lista das configurações que você pode definir  

-   [Monitorar o Endpoint Protection no System Center Configuration Manager](../deploy-use/monitor-endpoint-protection.md) – Monitoramento de relatórios de atividade, computadores cliente infectados e muito mais.   

-   [Gerenciar políticas antimalware e configurações de firewall para o Endpoint Protection no System Center Configuration Manager](../deploy-use/endpoint-antimalware-firewall.md) – É possível alterar a prioridade da política para [antimalware](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) ou [firewall](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies), [corrigir malware encontrado em computadores cliente](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware) e outras tarefas

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gerenciando o firewall do Windows com o Endpoint Protection  
 O Endpoint Protection no Configuration Manager fornece gerenciamento básico do Firewall do Windows em computadores cliente. Para cada perfil de rede, você pode definir as seguintes configurações:  

-   Habilitar ou desabilitar o Firewall do Windows.  

-   Bloquear conexões de entrada, incluindo aquelas na lista de programas permitidos.  

-   Notificar o usuário quando o Firewall do Windows bloquear um novo programa.  

> [!NOTE]  
>  O Endpoint Protection dá suporte apenas ao gerenciamento do Firewall do Windows.  

  Para obter mais informações sobre como criar e implantar políticas do Firewall do Windows para o Endpoint Protection, consulte [Como criar e implantar políticas do Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](../deploy-use/create-windows-firewall-policies.md).  

## <a name="windows-defender-advanced-threat-protection"></a>Proteção Avançada contra Ameaças do Windows Defender

Começando com a versão 1606 do Configuration Manager (ramificação atual), o Endpoint Protection pode ajudar a gerenciar e monitorar a ATP (Proteção Avançada contra Ameaças) do Windows Defender. A ATP do Windows Defender é um novo serviço que ajudará as empresas a detectar, investigar e responder a ataques avançados em suas redes. Consulte [Proteção Avançada contra Ameaças do Windows Defender](../deploy-use/windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Fluxo de trabalho do Endpoint Protection  
 Use o diagrama a seguir para ajudá-lo a entender o fluxo de trabalho para implementar o Endpoint Protection em sua hierarquia do Configuration Manager.  

 ![Fluxo de trabalho do Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cliente do Endpoint Protection para computadores Mac e servidores Linux  
 O System Center inclui um cliente Endpoint Protection para computadores Linux e Mac. Esses clientes não são fornecidos com o Configuration Manager. Você precisa baixar os seguintes produtos do [Centro de Serviços de Licenciamento por Volume da Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

> [!IMPORTANT]  
>  Você deve ser um cliente de Licença de volume da Microsoft para baixar os arquivos de instalação do Endpoint Protection para Linux e Mac.  

 Esses produtos não podem ser gerenciados no console do Gerenciador de Configurações. No entanto, um pacote de gerenciamento do System Center Operations Manager é fornecido com os arquivos de instalação, o que permite que você gerencie o cliente para Linux usando o Operations Manager.  

 Para obter mais informações sobre como instalar e gerenciar clientes do Endpoint Protection em computadores Linux e Mac, use a documentação que acompanha esses produtos, que está localizado na pasta **Documentação** .

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Práticas recomendadas para o Endpoint Protection no Gerenciador de Configurações  
 Use as seguintes práticas recomendadas para o Endpoint Protection no System Center 2012 Configuration Manager  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Definir configurações personalizadas do cliente para o Endpoint Protection  
 Quando você definir configurações de cliente para o Endpoint Protection, não use as configurações padrão do cliente porque elas se aplicam a todos os computadores na sua hierarquia. Em vez disso, configurar configurações personalizadas do cliente e atribuir essas configurações em coleções de computadores na sua hierarquia.  

 Quando você configurar configurações personalizadas do cliente, você pode fazer o seguinte:  

-   Personalize as configurações de antimalware e segurança para diferentes partes da sua organização.  
-   Teste os efeitos da execução do Endpoint Protection em um pequeno grupo de computadores antes de implantá-lo em toda a hierarquia.  
-   Adicionar mais clientes à coleção ao longo do tempo para a implantação em fases do cliente do Endpoint Protection.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Distribuindo atualizações de definição usando as atualizações de software  
 Se você estiver usando atualizações de software do Configuration Manager para distribuir atualizações de definição, considere a colocação de atualizações de definição em um pacote que não contém outras atualizações de software. Isso mantém o tamanho do pacote de atualização de definição menores que permite que ele replique para pontos de distribuição mais rapidamente.

