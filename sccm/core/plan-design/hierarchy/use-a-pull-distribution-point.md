---
title: Ponto de distribuição de recepção
titleSuffix: Configuration Manager
description: Saiba mais sobre as configurações e limitações para usar um ponto de distribuição de recepção com o System Center Configuration Manager.
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d6d6f68e913d261a5a23db85707ea0c9ac965cbd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="use-a-pull-distribution-point-with-system-center-configuration-manager"></a>Use um ponto de distribuição de recepção baseado em nuvem com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Um ponto de distribuição de recepção para o System Center Configuration Manager é um ponto de distribuição padrão que obtém o conteúdo baixando-o de um local de origem, como um cliente, em vez de ter o conteúdo enviado a ele por push do servidor do site.  

 Quando você implanta conteúdo em um grande número de pontos de distribuição em um site, os pontos de distribuição de recepção podem ajudar a reduzir a carga de processamento no servidor do site e acelerar a transferência do conteúdo para cada ponto de distribuição. Para obter essa eficiência, é necessário descarregar o processo de transferência do conteúdo para cada ponto de distribuição do processo do gerenciador de distribuição no servidor do site.  

-   Você pode configurar pontos de distribuição individuais para serem pontos de distribuição de recepção.  

-   Para cada ponto de distribuição de recepção, você deve especificar um ou mais pontos de distribuição de origem dos quais seja possível obter as implantações (um ponto de distribuição de recepção pode obter conteúdo somente de um ponto de distribuição especificado como um ponto de distribuição de origem).  

-   Quando você distribui conteúdo a um ponto de distribuição de recepção, o servidor do site notifica o ponto de distribuição de recepção, o qual inicia o download (transferência) do conteúdo de um ponto de distribuição de origem. Um ponto de distribuição de recepção gerencia individualmente a transferência do conteúdo, baixando-o de um ponto de distribuição que já tem uma cópia do conteúdo.  

Os pontos de distribuição de recepção dão suporte às mesmas configurações e funcionalidades dos pontos de distribuição típicos do Configuration Manager. Por exemplo, um ponto de distribuição configurado como um ponto de distribuição de recepção oferece suporte ao uso de configurações multicast e PXE, à validação de conteúdo e à distribuição de conteúdo sob demanda. Um ponto de distribuição de recepção oferece suporte às comunicações HTTP ou HTTPS de clientes, às mesmas opções de certificados de outros pontos de distribuição e pode ser gerenciado individualmente ou como um membro de um grupo de pontos de distribuição.  

> [!IMPORTANT]
> Embora um ponto de distribuição de recepção dê suporte à comunicação por meio dos protocolos HTTP e HTTPS, ao usar o Configuration Manager, você só poderá especificar pontos de distribuição de origem configurados para HTTP. É possível usar o SDK do Configuration Manager para especificar um ponto de distribuição de origem configurado para HTTPS.  

 **Veja a seguir a sequência de eventos que ocorre quando você distribui o conteúdo para um ponto de distribuição de recepção:**  

-   Assim que o conteúdo é distribuído para um ponto de distribuição de recepção, o Gerenciador de Transferência de Pacote do servidor do site verifica o banco de dados do site para confirmar se o conteúdo está disponível em um ponto de distribuição de origem. Se não for possível confirmar se o conteúdo está em um ponto de distribuição de origem do ponto de distribuição de recepção, ele repetirá a verificação a cada 20 minutos até que o conteúdo esteja disponível.  

-   Quando o Gerenciador de Transferência de Pacote confirma que o conteúdo está disponível, ele notifica o ponto de distribuição de recepção para que ele baixe o conteúdo. Se essa notificação falhar, ela tentará novamente com base nas **Configurações de repetição** do Componente de Distribuição de Software para pontos de distribuição por pull. Quando o ponto de distribuição de recepção recebe a notificação ele tenta baixar o conteúdo dos seus pontos de distribuição de origem.  

-   Enquanto o ponto de distribuição por pull baixa o conteúdo, o Gerenciador de Transferência de Pacote sondará o status com base nas **Configurações de sondagem de status** do Componente de Distribuição de Software para pontos de distribuição por pull.  Quando o ponto de distribuição de recepção concluir o download do conteúdo, ele enviará esse status a um ponto de gerenciamento.

**Você pode configurar um ponto de distribuição de recepção** durante ou após a instalação ao editar as propriedades da função de sistema de sites do ponto de distribuição.  

**Você pode remover a configuração para ser um ponto de distribuição de recepção** ao editar as propriedades do ponto de distribuição. Quando você remove a configuração do ponto de distribuição de recepção, o ponto de distribuição retorna à operação normal, e o servidor do site gerencia as transferências de conteúdo futuras para ele.  

## <a name="to-configure-software-distribution-component-for-pull-distribution-points"></a>Para configurar o Componente de Distribuição de Software para os pontos de distribuição por pull

1.  No console do Configuration Manager, escolha **Administração** > **Sites**.  

2.  Selecione o site desejado e selecione **Configurar Componentes do Site** > **Distribuição de Software**

3. Selecione a guia **Ponto de Distribuição por Pull**.  

4.  Na lista **Configurações de repetição**, configure os seguintes valores:  

    -   **Número de repetições**: o número de vezes que o Gerenciador de Transferência de Pacote tenta notificar o ponto de distribuição por pull para baixar o conteúdo.  Se esse número for excedido, o Gerenciador de Transferência de Pacote cancelará a transferência.

    -   **Atraso antes de tentar novamente (minutos)**: o número de minutos que o Gerenciador de Transferência de Pacote aguardará entre as tentativas. 

5.  Na lista **Configurações de sondagem de status**, configure os seguintes valores:  

    -   **Número de sondagens**: o número de vezes que o Gerenciador de Transferência de Pacote entra em contato com o ponto de distribuição por pull para recuperar o status do trabalho.  Se esse número for excedido antes de o trabalho ser concluído, o Gerenciador de Transferência de Pacote cancelará a transferência.

    -   **Atraso antes de tentar novamente (minutos)**: o número de minutos que o Gerenciador de Transferência de Pacote aguardará entre as tentativas. 
    
    > [!NOTE]  
    >  Quando o Gerenciador de Transferência de Pacote cancela um trabalho porque o número de tentativas de sondagem de status foi excedido e o ponto de distribuição por pull continuará a baixar o conteúdo.  Quando terminar, a mensagem de status apropriada será enviada para o Gerenciador de Transferência de Pacote e o console refletirá o novo status.
    
## <a name="limitations-for-pull-distribution-points"></a>Limitações dos pontos de distribuição de recepção  

-   Os pontos de distribuição baseados em nuvem não podem ser configurados como pontos de distribuição de recepção.  

-   Um ponto de distribuição em um servidor do site não pode ser configurado como um ponto de distribuição de recepção.  

-   **A definição do conteúdo de pré-configuração substitui a configuração do ponto de distribuição de recepção**. Um ponto de distribuição de recepção configurado para conteúdo de pré-teste aguarda o conteúdo. Ele não efetua pull do conteúdo do ponto de distribuição de origem e, assim como um ponto de distribuição padrão com definição de conteúdo pré-configurado, não recebe conteúdo do servidor do site.  

-   **Um ponto de distribuição por pull não usa configurações para agendamento ou limites de taxa** quando ele transfere o conteúdo. Se você definir um ponto de distribuição instalado anteriormente como um ponto de distribuição de recepção, as configurações para agendamento e limites de taxa serão salvas, mas não usadas. Se, mais tarde, você remover a configuração do ponto de distribuição de recepção, as configurações de agendamento e limite de taxa serão implementadas conforme definido anteriormente.  

    > [!NOTE]  
    >  Quando um ponto de distribuição é configurado como ponto de distribuição de recepção, as guias **Agendamento** e **Limites de Taxa** não ficam visíveis nas propriedades do ponto de distribuição.  

-   Os pontos de distribuição por pull não usam as configurações na guia **Geral** das **Propriedades do Componente de Distribuição de Software** de cada site.  Isso inclui a configuração **Distribuição simultânea** e a **Repetição multicast**.  Use a guia **Ponto de Distribuição por Pull** para definir configurações para pontos de distribuição por pull.

-   Para transferir conteúdo de um ponto de distribuição de origem em uma floresta remota, o computador que hospeda o ponto de distribuição de recepção deve ter um cliente do Configuration Manager instalado. Uma Conta de Acesso à Rede que pode acessar o ponto de distribuição de origem deve ser configurada para uso.  

-   Em um computador configurado como ponto de distribuição de recepção e que executa o cliente do Configuration Manager, a versão do cliente deve ser a mesma do site do Configuration Manager que instala esse ponto de distribuição de recepção. É exigido que o ponto de distribuição de recepção use o CCMFramework comum tanto ao ponto de distribuição de recepção quanto ao cliente do Configuration Manager.  

## <a name="about-source-distribution-points"></a>Sobre os pontos de distribuição de origem  
 Ao configurar o ponto de distribuição de recepção, você deve especificar um ou mais pontos de distribuição de origem:  

-   Somente os pontos de distribuição qualificados para serem pontos de distribuição de origem são exibidos.  

-   Um ponto de distribuição de recepção pode ser especificado como um ponto de distribuição de origem para outro ponto de distribuição de recepção.  

-   Somente os pontos de distribuição que dão suporte a HTTP podem ser especificados como um ponto de distribuição de origem ao usar o Configuration Manager.  

-   É possível usar o SDK do Configuration Manager para especificar um ponto de distribuição de origem configurado para HTTPS. Para usar um ponto de distribuição de origem configurado para HTTPS, o ponto de distribuição de recepção deve ser colocalizado em um computador que executa o cliente do Configuration Manager.  

Pode ser atribuída uma prioridade a cada ponto de distribuição em uma lista de pontos de distribuição de origem dos pontos distribuição de recepção:  

-   Você pode atribuir uma prioridade separada para cada ponto de distribuição de origem, ou atribuir vários pontos de distribuição de origem com a mesma prioridade.  

-   A prioridade determina a ordem na qual o ponto de distribuição de recepção solicita o conteúdo dos seus pontos de distribuição de origem.  

-   Pontos de distribuição de recepção inicialmente entram em contato com um ponto de distribuição de origem com o menor valor de prioridade.  Se houverem vários pontos de distribuição de origem com a mesma prioridade, o ponto de distribuição de recepção seleciona um deles de forma não determinística.  

-   Quando o conteúdo não está disponível em uma origem selecionada, o ponto de distribuição de recepção tenta baixar o conteúdo de outro ponto de distribuição com a mesma prioridade.  

-   Se nenhum dos pontos de distribuição com determinada prioridade tiver o conteúdo, o ponto de distribuição de recepção tentará baixar o conteúdo de um ponto de distribuição com uma prioridade atribuída com o próximo valor mais alto, até que o conteúdo seja localizado ou o ponto de distribuição de recepção fique suspenso por 30 minutos antes de começar o processo novamente.  

Quando um ponto de distribuição de recepção baixa conteúdo de um ponto de distribuição de origem, o ponto de distribuição de recepção é contado como um cliente na coluna **Cliente Acessado (Exclusivo)** do relatório **Resumo de uso do ponto de distribuição** .  

 Por padrão, um ponto de distribuição de recepção usa sua **conta de computador** para transferir o conteúdo de um ponto de distribuição de origem. No entanto, quando o ponto de distribuição de recepção transfere o conteúdo de um ponto de distribuição de origem que está em uma floresta remota, o ponto de distribuição de recepção sempre usa a conta de acesso à rede. Esse processo exige que o computador tenha o cliente do Configuration Manager instalado e que uma conta de acesso à rede esteja configurada para uso e tenha acesso ao ponto de distribuição de origem.  

## <a name="about-content-transfers"></a>Sobre as transferências de conteúdo  
 Para gerenciar a transferência de conteúdo, os pontos de distribuição de recepção usam o componente **CCMFramework** do software cliente do Configuration Manager.  

-   Essa estrutura é instalada pelo **Pulldp.msi** quando você configura o ponto de distribuição para ser um ponto de distribuição por pull. A estrutura não exige o cliente do Configuration Manager.  

-   Após a instalação do ponto de distribuição de recepção, o serviço CCMExec no computador do ponto de distribuição deve estar operacional para que esse ponto de distribuição funcione.  
<!--sms.503672 -Clarified BITS use-->
-   Quando o ponto de distribuição por pull transferir conteúdo, transferirá usando o BITS **Serviço de Transferência Inteligente em Segundo Plano** integrado ao sistema operacional Windows. Um ponto de distribuição por pull não exige a instalação do recurso opcional BITS IIS Server Extension.

-  O ponto de distribuição por pull registra sua operação no **datatransferservice.log** e no **pulldp.log** no computador do ponto de distribuição.

## <a name="see-also"></a>Consulte também  
 [Conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
