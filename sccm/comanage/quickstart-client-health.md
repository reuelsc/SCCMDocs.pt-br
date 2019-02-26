---
title: Integridade do cliente com o cogerenciamento
titleSuffix: Configuration Manager
description: Manter a visibilidade da integridade do cliente do Configuration Manager do Intune no portal do Azure
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754551"
---
# <a name="client-health-with-co-management"></a>Integridade do cliente com o cogerenciamento

A integridade da sua rede está conectada diretamente para a integridade dos dispositivos saem a ele. Intune pode se comunicar com um cliente não íntegro, mesmo quando ele não estiver em sua rede. Use o cogerenciamento para combinar esse recurso com a capacidade do Configuration Manager para relatar 98% dos clientes íntegros conhecidos. Em seguida, você pode detectar, avaliar e fornecem visibilidade em todos os clientes em tempo real. Intune também adiciona o suporte necessário para atualizações de conformidade entre todos os clientes conectados.

No vídeo a seguir, gerente de programa sênior Rob York e Ainley Locky do gerente de marketing de produto discutem e integridade do cliente com o cogerenciamento de demonstração:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Benefícios

Avaliar a integridade do cliente é uma prioridade. System Center 2012 Configuration Manager adicionou **CCMeval**. Esse utilitário é externo ao cliente do Configuration Manager. Ele fornece cliente correção automática e monitoramento de integridade. No entanto, esse relatório se baseia em um dispositivo que está sendo fisicamente ou virtualmente em sua rede interna. Cogerenciamento ajuda a resolver esse problema.

Com o cogerenciamento, Intune pode relatar o estado de integridade do cliente. Ele fornece informações de carimbo de hora para a validade dos dados. Essas informações informam se seus dispositivos estão íntegros, capaz de se conectar, capaz de instalar aplicativos, ou podem atualizar para o sistema operacional obrigatório se baseia. 

Para obter uma visão geral detalhada desse recurso, consulte este vídeo do [o que há de novo no Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) sessão no Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Quando o Configuration Manager fornece o status do dispositivo que o cliente está instalado, mas não é, o Intune pode fornecer mais informações sem precisar se conectar ao cliente. As informações de integridade do dispositivo no Intune são fácil de entender. Se o status for algo diferente de **Íntegro**, ele fornece recomendações e as próximas etapas para solucionar problemas e corrigi-lo.

> [!Note]  
> Os seguintes benefícios estão planejados para uma versão futura:
> - Configuration Manager será incluir funcionalidades adicionais em CCMeval  
> - Será mais fácil identificar computadores potencialmente problemáticos no Configuration Manager e o Intune  
> - Você pode agrupar os dados de integridade do cliente do Intune  



## <a name="value-proposition"></a>Proposta de valor

Com esse recurso, agora você tem uma fonte de dados externa com o Intune. Ele permite que você determine as próximas etapas, ao solucionar problemas de uma vasta gama de problemas do cliente. Agora, você não precisa criar relatórios adicionais ou usar outras ferramentas para extrair dados do cliente.

Quando você tiver clientes íntegros, você atualizou prontamente conformidade com os patches. Melhor conformidade com os patches significa uma melhor segurança.



## <a name="configure"></a>Configurar

Para começar a usar com esse recurso, use as seguintes etapas:

- Atualizar dispositivos Windows 10, versão 1709 ou posterior  

- [Habilitar o cogerenciamento](/sccm/comanage/how-to-enable)  
    - Você não precisa mudar qualquer carga de trabalho para o Intune  

- Atualize seu site do Configuration Manager e os clientes *versão 1806* ou posterior  


### <a name="review-configuration-manager-client-health-in-intune"></a>Examine a integridade do cliente do Configuration Manager no Intune

1. Entrando no [Portal do Azure](https://portal.azure.com/).  

2. Escolher **todos os serviços** > **Intune**. Intune está localizado na **monitoramento + gerenciamento** seção.  

3. Depois de abrir o **Microsoft Intune** painel, no menu sob **ajuda e suporte**, vá para o **solução de problemas** página.  

4. Use o **Selecionar usuário** opção, localize o dispositivo específico na **dispositivos** lista e selecione-o para abrir a página de dispositivo.  

5. Informações de cogerenciamento são mostradas na parte inferior da página do dispositivo. Essas informações incluem os seguintes campos para a integridade do cliente:  
    - **Estado do agente do Configuration Manager**  
    - **Última verificação de agente do Configuration Manager em tempo**  

> [!Tip]  
> Dispositivos registrados no Intune se conectar ao serviço de nuvem três vezes ao dia, aproximadamente a cada oito horas. 
