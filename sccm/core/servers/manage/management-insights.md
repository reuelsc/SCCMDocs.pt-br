---
titleSuffix: Configuration Manager
description: Saiba mais sobre a funcionalidade Insights de Gerenciamento disponível no console do Configuration Manager.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2d6a58bd5aba873ea35c5bcf511a3cc22514b51
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2018
---
# <a name="management-insights-in-system-center-configuration-manager"></a>Insights de Gerenciamento no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os Insights de Gerenciamento do System Center Configuration Manager fornecem informações sobre o estado atual do ambiente. As informações baseiam-se na análise de dados do banco de dados do site. As informações ajudam você a melhor compreender seu ambiente e executar ações com base nas informações. Esse recurso foi lançado no Configuration Manager versão 1802. <!--1353967-->

## <a name="review-management-insights-in-the-configuration-manager-console"></a>Examinar os Insights de Gerenciamento no console do Configuration Manager 
A permissão **leitura do site** é necessária para exibir as regras.

1. Abra o Console do Configuration Manager. 
2. Acesse o nó **Administração** e clique em **Insights de Gerenciamento**.
3. Selecione **Todos os Insights**
4. Clique duas vezes no **Nome do Grupo de Insight de Gerenciamento** que deseja examinar. Como alternativa, realce-o e clique em **Mostrar Insights** na Faixa de Opções. 
5. Quatro guias estão disponíveis para revisão junto com os pré-requisitos necessários para executar a regra. 
    - **Todas as Regras**: fornece a lista completa de regras do grupo de insight de gerenciamento escolhido.
    - **Completo**: lista as regras em que nenhuma ação é necessária. 
    - **Em Andamento**: mostra as regras em que alguns, mas nem todos os pré-requisitos foram atendidos.
    - **Ação Necessária**: as regras que precisam de ações executadas são listadas. Clique com o botão direito do mouse e selecione **Mais Detalhes** para recuperar itens específicos nos quais uma ação é necessária. 
    - **Pré-requisitos**: se uma regra precisar que os itens sejam concluídos antes de serem executados, os itens necessários serão listados aqui.   
    
    **Todas as regras e pré-requisitos do grupo de serviços de nuvem** ![Insights de gerenciamento – Todas as regras e pré-requisitos do grupo de serviços de nuvem](./media/Management-insights-all-cloud-rules.png)

## <a name="management-insights-reevaluation-and-logging"></a>Reavaliação e log dos insights de gerenciamento
As regras dos insights de gerenciamento reavaliam sua aplicabilidade de acordo com um agendamento semanal. Reavalie uma regra sob demanda clicando com o botão direito do mouse na regra e selecionando **Reavaliar**.

**Arquivo de Log das regras dos insights de gerenciamento**: SMS_DataEngine.log
## <a name="management-insights-groups-and-rules"></a>Regras e grupos dos insights de gerenciamento
As regras são organizadas em diferentes grupos de insights de gerenciamento. Quando grupos e regras forem adicionados, eles serão adicionados à seguinte lista:

**Aplicativos**: insights para o gerenciamento do aplicativo.

- **Aplicativos sem implantações** – lista os aplicativos no ambiente que não têm implantações ativas. Essa regra ajuda você a encontrar e excluir aplicativos não utilizados para simplificar a lista de aplicativos exibidos no console. 

**Serviços de Nuvem**: ajuda você a integrar muitos serviços de nuvem, proporcionando um gerenciamento moderno dos dispositivos. 
 - **Avaliar a prontidão do cogerenciamento** – ajuda você a entender as etapas necessárias para habilitar o cogerenciamento. Essa regra tem pré-requisitos. 
 - **Habilitar os dispositivos para serem híbridos e ingressados no Azure Active Directory** – os dispositivos ingressados no Azure AD permitem que os usuários entrem com suas credenciais de domínio, ao mesmo tempo que garantem que os dispositivos atendam aos padrões de segurança e de conformidade da organização. 
 - **Modernizar a infraestrutura de identidade e acesso** – o serviço de nuvem do Azure AD com a autenticação multifator integrada protege os aplicativos e os dados confidenciais locais e na nuvem. 
 - **Atualizar os clientes Windows 10, versão 1709 ou acima** – o Windows 10, versão 1709 ou acima, melhora e moderniza a experiência de computação dos usuários. 


**Coleções**: insights que ajudam a simplificar o gerenciamento da limpeza e da reconfiguração de coleções.
   - **Coleções Vazias** – lista as coleções no ambiente que não têm membros. 

**Gerenciamento Simplificado**: insights que ajudam você a simplificar o gerenciamento diário do ambiente. 
   - **Versões desatualizadas de cliente** – lista todos os clientes cujas versões têm mais de dois anos. 

**Centro de Software**: insights para o gerenciamento do Centro de Software. 
   - **Direcionar os usuários para o Centro de Software em vez de para o Catálogo de Aplicativos** – verifique se os usuários instalaram ou solicitaram aplicativos no Catálogo de Aplicativos nos últimos 14 dias. Agora, a principal funcionalidade do Catálogo de Aplicativos está incluída no Centro de Software. O suporte para o site do Catálogo de Aplicativos termina com a primeira atualização liberada após 1º de junho de 2018
   - **Usar a nova versão do Centro de Software** – não há mais suporte para a versão anterior do Centro de Software. Configure clientes para usar o novo Centro de Software habilitando a configuração do cliente **Agente de Computador** >**Usar o novo Centro de Software**.

**Windows 10**: insights relacionados à implantação e manutenção do Windows 10. O grupo de insights de gerenciamento do Windows 10 está disponível quando mais da metade dos clientes executa o Windows 7, Windows 8 ou Windows 8.1.
   - **Configurar a telemetria do Windows e a chave de ID comercial** – para usar os dados do Upgrade Readiness, os dispositivos devem ser configurados com uma Chave de ID comercial e ter a telemetria habilitada. Os dispositivos Windows 10 devem ser definidos com o nível de telemetria Avançado (Limitado) ou superior.
   - **Conectar o Configuration Manager ao Upgrade Readiness** – utilize o Upgrade Readiness para agilizar as implantações do Windows 10 antes do término de suporte para o Windows 7. A configuração **Configurar a telemetria do Windows e a chave de ID comercial** é um pré-requisito.

     **Regras dos insights de gerenciamento do Windows 10**
    ![Management insights- Rules for Windows 10](./media/Windows-10-insights-group.png)
    