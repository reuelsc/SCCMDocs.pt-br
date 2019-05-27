---
title: Configurar o Wake on LAN
titleSuffix: Configuration Manager
description: Selecione as configurações de Wake On LAN no System Center Configuration Manager.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59d99a3e3626be111e927dae8651d2e01364ccf5
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083159"
---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>Como configurar Wake on LAN no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Especifique as configurações de Wake On LAN para o System Center Configuration Manager quando quiser tirar os computadores do estado de suspensão.

## <a name="bkmk_wol-1810"></a> Wake On LAN a partir da versão 1810
<!--3607710-->
A partir do Configuration Manager versão 1810, há uma nova maneira de despertar máquinas em suspensão. É possível ativar clientes no console do Configuration Manager, mesmo se o cliente não estiver na mesma sub-rede que o servidor do site. Se precisar realizar manutenção ou consultar dispositivos, você não estará limitado por clientes remotos que estão em suspensão. O servidor do site usa o canal de notificação do cliente para identificar outros clientes ativos na mesma sub-rede remota e usa esses clientes para enviar uma solicitação Wake On LAN (Magic Packet). Usar o canal de notificação do cliente ajuda a evitar flaps de MAC, o que pode causar o desligamento da porta pelo roteador. A nova versão do Wake On LAN pode ser habilitada ao mesmo tempo que a [versão antiga](#bkmk_wol-previous).

### <a name="limitations"></a>Limitações

- Pelo menos um cliente na sub-rede de destino deve estar ativo.
- Esse recurso não é compatível com as seguintes tecnologias de rede:
   - IPv6
   - Autenticação de rede 802.1x
    >[!NOTE]
    > A autenticação de rede 802.1 x pode funcionar com configuração adicional, dependendo do hardware e de sua configuração.
- As máquinas só serão ativadas quando você notificá-las por meio de uma notificação de **Ativação** do cliente.
    - Para ativar quando ocorre uma data limite, usa-se a versão mais antiga de Wake On LAN.
    -  Se a versão mais antiga não estiver habilitada, a ativação do cliente não ocorrerá para as implantações criadas com as configurações **Use o Wake On LAN para ativar clientes para implantações necessárias** ou **Enviar pacotes de ativação**.  


### <a name="security-role-permissions"></a>Permissões de função de segurança

- **Notificar o recurso** na categoria Coleção

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>Configurar os clientes para usar o Wake On LAN a partir da versão 1810

Anteriormente, você tinha que ativar manualmente o cliente para ativar a LAN nas propriedades do adaptador de rede. O Configuration Manager 1810 inclui uma nova configuração de cliente chamada **Permitir ativação de rede**. Configure e implante essa configuração em vez de modificar as propriedades do adaptador de rede.

1. Em **Administração**, acesse as **Configurações do Cliente**.
1. Selecione as configurações do cliente que você deseja editar ou crie novas configurações personalizadas do cliente a implantar. Para obter mais informações, consulte [Como definir as configurações de cliente](/sccm/core/clients/deploy/configure-client-settings).
1. Nas configurações de **Gerenciamento de Energia** do cliente, selecione **Habilitar** para a configuração **Permitir ativação de rede**. Para mais informações sobre configurações do cliente, confira [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#power-management).

4. A partir do Configuration Manager versão 1902, a nova versão do Wake On LAN respeita a porta UDP personalizada especificada na [configuração do cliente](/sccm/core/clients/deploy/about-client-settings#power-management) **Número de porta Wake On LAN (UDP)** . Essa configuração é compartilhada tanto pela versão antiga como pela nova do Wake On LAN.
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>Ativar um cliente usando a notificação de cliente começando em 1810
 
Você pode ativar um único cliente ou todos os clientes em suspensão de uma coleção. Dispositivos que já estejam ativos na coleção não executam nenhuma ação. A solicitação do Wake On LAN será enviada somente aos clientes que estejam em suspensão. Para saber mais sobre como enviar a notificação para ativar um cliente, confira [Notificação do cliente](/sccm/core/clients/manage/client-notification).

- **Para ativar somente um único dispositivo:** Clique com botão direito no cliente, acesse **Notificação do cliente** e selecione **Ativar**.

   ![Notificação de ativação do cliente no console](media/wol-wake-up-client-notification.png)

- **Para ativar todos os clientes em suspensão em uma coleção:** Clique com botão direito na coleção do dispositivo, acesse **Notificação do cliente** e selecione **Ativar**.
   - Essa ação não pode ser executada em coleções internas.
   - Quando você tiver uma combinação de clientes ativos e em suspensão em uma coleção, a solicitação do Wake On LAN será enviada somente aos clientes que estejam em suspensão.  

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>O que esperar quando somente a nova versão de Wake On LAN estiver habilitada

Quando você tiver somente a nova versão de Wake On LAN habilitada, somente a notificação de **Ativação** do cliente estará habilitada. As notificações não são enviadas aos clientes quando uma data limite é recebida em implantações tais como sequências de tarefas, distribuição de software ou instalação de atualizações de software. Quando um computador em suspensão estiver online novamente, isso será refletido no console quando ele fizer check-in no Ponto de Gerenciamento.

A partir do Configuration Manager versão 1902, você pode especificar a porta do Wake On LAN. Essa configuração é compartilhada tanto pela versão antiga como pela nova do Wake On LAN.

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>O que esperar quando as duas versões do Wake On LAN estiverem habilitadas

Quando você tem as duas versões do Wake On LAN habilitadas, é possível usar a notificação de **Ativação** do cliente e a ativação em data limite. A notificação do cliente funciona um pouco diferente do Wake On LAN tradicional. Confira uma breve explicação de como funciona a notificação do cliente na seção [Wake On LAN a partir da versão 1810](#bkmk_wol-1810). A nova configuração **Permitir ativação de rede** do cliente altera as propriedades NIC para permitir o Wake On LAN. Você não precisa mais alterá-la manualmente para novas máquinas que sejam adicionadas ao seu ambiente. Todas as demais funcionalidades de Wake On LAN não foram alteradas.

A partir da versão 1902, a notificação de **Ativação** do cliente respeita as configurações existentes de **Número da porta do Wake On LAN (UDP)** .


## <a name="bkmk_wol-previous"></a>  Wake On LAN para a versão 1806 e anteriores

Especifique as configurações de Wake on LAN para o System Center Configuration Manager quando desejar tirar os computadores do estado de suspensão para instalar o software necessário, como as atualizações de software, aplicativos, sequências de tarefas e programas.

Você pode complementar o Wake on LAN usando as configurações cliente de proxy de ativação. No entanto, para usar o proxy de ativação, você deve primeiro habilitar o Wake on LAN para o site e especificar **Usar somente pacotes de ativação** e a opção **Unicast** para o método de transmissão Wake on LAN. Esta solução de ativação também oferece suporte a conexões ad hoc, como uma conexão de área de trabalho remota.

Use o primeiro procedimento para configurar um site primário para Wake on LAN. Em seguida, use o segundo procedimento para definir as configurações cliente de proxy de ativação. Esse segundo procedimento define as configurações padrão do cliente para as configurações de proxy de ativação para aplicar a todos os computadores na hierarquia. Se você deseja que essas configurações se apliquem somente aos computadores selecionados, crie uma configuração de dispositivo personalizada e a atribua à coleção que contém os computadores que deseja configurar para o proxy de ativação. Para obter mais informações sobre como criar configurações personalizadas do cliente, consulte [Como configurar as definições de cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

Um computador que recebe as configurações de cliente do proxy de ativação provavelmente pausará sua conexão de rede por 1 a 3 segundos. Isso ocorre porque o cliente deve redefinir a placa de interface de rede para habilitar que o driver de proxy de ativação nela.

> [!WARNING]
> Para evitar a interrupção inesperada do serviço de rede, avalie primeiro o proxy de ativação em uma infraestrutura de rede isolada e representante. Em seguida, use as configurações do cliente personalizadas para expandir seu teste para um grupo selecionado de computadores em várias sub-redes. Para obter mais informações sobre como funciona o proxy de ativação, consulte [Planejar como ativar clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>Para configurar o Wake On LAN para um site com a versão 1806 e anteriores

 Para usar o Wake On LAN, você precisa habilitá-lo para cada site em uma hierarquia.

1. No console do Configuration Manager, vá para **Administração > Configuração de Site > Sites**.
2. Clique no site primário para configurar e em **Propriedades**.
3. Clique na guia **Wake on LAN** e configure as opções que você precisa para esse site. Para dar suporte ao proxy de ativação, verifique se selecionou **Usar somente pacotes de ativação** e **Unicast**. Para mais informações, consulte [Planejar a ativação de clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Clique em **OK** e repita o procedimento para todos os sites primários da hierarquia.

![Habilitar o Wake On LAN nas propriedades do site](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>Para definir as configurações de cliente do proxy de ativação

1. No console do Configuration Manager, vá até **Administração > Configurações do Cliente**.
2. Clique em **Configurações Padrão do Cliente** e em **Propriedades**.
3. Selecione **Gerenciamento de Energia** e escolha **Sim** para **Habilitar proxy de ativação**.
4. Examine e, se necessário, defina as outras configurações de proxy de ativação. Para saber mais sobre essas configurações, confira [Configurações de gerenciamento de energia](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Clique em **OK** para fechar a caixa de diálogo e em **OK** novamente para fechar a caixa de diálogo Configurações do Cliente Padrão.

Você pode usar os seguintes relatórios do Wake On LAN para monitorar a instalação e a configuração do proxy de ativação:

- Resumo do estado da implantação do proxy de ativação
- Detalhes do Estado da Implantação do Proxy de Ativação

> [!TIP]
> Para testar se o proxy de ativação está funcionando, teste uma conexão em um computador suspenso. Por exemplo, conecte-se a uma pasta compartilhada naquele computador ou tente a conexão no computador usando a Área de Trabalho Remota. Se você usa o DirectAccess, verifique se os prefixos IPv6 funcionam ao tentar os mesmos testes em um computador suspenso que está atualmente na Internet.
