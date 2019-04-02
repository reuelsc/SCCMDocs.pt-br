---
title: Integridade do cliente com o cogerenciamento
titleSuffix: Configuration Manager
description: Manter a visibilidade da integridade do cliente do Configuration Manager a partir do Intune no portal do Azure
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6838371a80530d5ab66abd9d8a976af41513e15
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754551"
---
# <a name="client-health-with-co-management"></a>Integridade do cliente com o cogerenciamento

A integridade da sua rede está conectada diretamente à integridade dos dispositivos que transitam nela. O Intune pode se comunicar com um cliente não íntegro, mesmo quando ele não está em sua rede. Use o cogerenciamento para combinar esse recurso com a capacidade do Configuration Manager de relatar 98% dos clientes íntegros conhecidos. Depois, você pode detectar, avaliar e fornecer visibilidade em todos os clientes em tempo real. O Intune também adiciona o suporte necessário para atualizações de conformidade em todos os clientes conectados.

No vídeo a seguir, o gerente de programas sênior Rob York e o gerente de marketing de produtos Locky Ainley discutem e demonstram a integridade do cliente com o cogerenciamento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Benefícios

Avaliar a integridade do cliente é uma prioridade. No System Center 2012 Configuration Manager, foi adicionado o **CCMeval**. Esse utilitário é externo ao cliente do Configuration Manager. Ele fornece monitoramento de integridade do cliente e correção automática. No entanto, este relatório depende de um dispositivo estar física ou virtualmente em sua rede interna. O cogerenciamento ajuda a resolver esse problema.

Com o cogerenciamento, o Intune pode relatar o estado de integridade do cliente. Ele fornece informações de carimbo de data/hora para validar os dados. Essas informações indicam se seus dispositivos estão íntegros, capazes de se conectar, capazes de instalar aplicativos ou se podem ser atualizados para os builds obrigatórios do sistema operacional. 

Para obter uma visão geral detalhada desse recurso, confira este vídeo da sessão [Novidades do Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) do Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Quando o Configuration Manager fornece o status do dispositivo em que o cliente está instalado, mas ele não está, o Intune pode fornecer mais informações sem precisar se conectar ao cliente. As informações de integridade do dispositivo no Intune são fáceis de entender. Se o status for algo diferente de **Íntegro**, ele fornecerá recomendações e as próximas etapas para solucionar problemas e corrigi-lo.

> [!Note]  
> Os seguintes benefícios estão planejados para uma versão futura:
> - O Configuration Manager incluirá funcionalidades adicionais no CCMeval  
> - Ficará mais fácil identificar computadores potencialmente não íntegros no Configuration Manager e no Intune  
> - Você poderá agrupar os dados de integridade do cliente no Intune  



## <a name="value-proposition"></a>Proposta de valor

Com esse recurso, agora você tem uma fonte de dados externa com o Intune. Ele permite determinar as próximas etapas ao solucionar problemas de uma vasta matriz de problemas do cliente. Agora, você não precisa criar relatórios adicionais ou usar outras ferramentas para extrair dados do cliente.

Quando você tem clientes íntegros, atualiza prontamente a compatibilidade com patches. Uma melhor conformidade com patches significa melhor segurança.



## <a name="configure"></a>Configurar

Para começar a usar esse recurso, siga as seguintes etapas:

- Atualize os dispositivos para o Windows 10, versão 1709 ou posterior  

- [Habilite o cogerenciamento](/sccm/comanage/how-to-enable)  
    - Você não precisa mudar nenhuma carga de trabalho para o Intune  

- Atualize seu site do Configuration Manager e os clientes *versão 1806* ou posterior  


### <a name="review-configuration-manager-client-health-in-intune"></a>Examine a integridade do cliente do Configuration Manager no Intune

1. Entrando no [Portal do Azure](https://portal.azure.com/).  

2. Escolha **Todos os serviços** > **Intune**. O Intune está localizado na seção **Monitoramento + Gerenciamento**.  

3. Depois de abrir o painel do **Microsoft Intune**, no menu em **Ajuda e suporte**, vá para a página **Solução de problemas**.  

4. Use a opção **Selecionar usuário**, localize o dispositivo específico na lista **Dispositivos** e selecione-o para abrir a página correspondente.  

5. Informações de cogerenciamento são mostradas na parte inferior da página do dispositivo. Essas informações incluem os seguintes campos de integridade do cliente:  
    - **Estado do agente do Configuration Manager**  
    - **Horário do último check-in do agente do Configuration Manager**  

> [!Tip]  
> Dispositivos registrados no Intune se conectam ao serviço de nuvem três vezes ao dia, aproximadamente a cada oito horas. 
