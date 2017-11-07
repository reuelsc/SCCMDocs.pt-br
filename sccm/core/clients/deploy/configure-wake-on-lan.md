---
title: Configurar o Wake on LAN
titleSuffix: Configuration Manager
description: "Selecione as configurações de Wake On LAN no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
caps.latest.revision: "7"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: b2250b64609bc4c39a81312e1b41586a55f576df
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>Como configurar Wake on LAN no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Especifique as configurações de Wake on LAN para o System Center Configuration Manager quando desejar tirar os computadores do estado de suspensão para instalar o software necessário, como as atualizações de software, aplicativos, sequências de tarefas e programas.

Você pode complementar o Wake on LAN usando as configurações cliente de proxy de ativação. No entanto, para usar o proxy de ativação, você deve primeiro habilitar o Wake on LAN para o site e especificar **Usar somente pacotes de ativação** e a opção **Unicast** para o método de transmissão Wake on LAN. Esta solução de ativação também oferece suporte a conexões ad hoc, como uma conexão de área de trabalho remota.

Use o primeiro procedimento para configurar um site primário para Wake on LAN. Em seguida, use o segundo procedimento para definir as configurações cliente de proxy de ativação. Esse segundo procedimento define as configurações padrão do cliente para as configurações de proxy de ativação para aplicar a todos os computadores na hierarquia. Se você deseja que essas configurações se apliquem somente aos computadores selecionados, crie uma configuração de dispositivo personalizada e a atribua à coleção que contém os computadores que deseja configurar para o proxy de ativação. Para obter mais informações sobre como criar configurações personalizadas do cliente, consulte [Como configurar as definições de cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

Um computador que recebe as configurações de cliente do proxy de ativação provavelmente pausará sua conexão de rede por 1 a 3 segundos. Isso ocorre porque o cliente deve redefinir a placa de interface de rede para habilitar que o driver de proxy de ativação nela.

> [!WARNING]
> Para evitar a interrupção inesperada do serviço de rede, avalie primeiro o proxy de ativação em uma infraestrutura de rede isolada e representante. Em seguida, use as configurações do cliente personalizadas para expandir seu teste para um grupo selecionado de computadores em várias sub-redes. Para obter mais informações sobre como funciona o proxy de ativação, consulte [Planejar como ativar clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

## <a name="to-configure-wake-on-lan-for-a-site"></a>Para configurar o Wake on LAN para um site

1. No console do Configuration Manager, vá para **Administração > Configuração de Site > Sites**.
2. Clique no site primário para configurar e em **Propriedades**.
3. Clique na guia **Wake on LAN** e configure as opções que você precisa para esse site. Para dar suporte ao proxy de ativação, verifique se selecionou **Usar somente pacotes de ativação** e **Unicast**. Para mais informações, consulte [Planejar a ativação de clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Clique em **OK** e repita o procedimento para todos os sites primários da hierarquia.

## <a name="to-configure-wake-up-proxy-client-settings"></a>Para definir as configurações de cliente do proxy de ativação

1. No console do Configuration Manager, vá até **Administração > Configurações do Cliente**.
2. Clique em **Configurações Padrão do Cliente** e em **Propriedades**.
3. Selecione **Gerenciamento de Energia** e escolha **Sim** para **Habilitar proxy de ativação**.
4. Examine e, se necessário, defina as outras configurações de proxy de ativação. Para obter mais informações sobre estas configurações, consulte [Configurações de gerenciamento de energia](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Clique em **OK** para fechar a caixa de diálogo e em **OK** novamente para fechar a caixa de diálogo Configurações do Cliente Padrão.

Você pode usar os seguintes relatórios do Wake On LAN para monitorar a instalação e a configuração do proxy de ativação:

- Resumo do estado da implantação do proxy de ativação
- Detalhes do Estado da Implantação do Proxy de Ativação

> [!TIP]
> Para testar se o proxy de ativação está funcionando, teste uma conexão em um computador suspenso. Por exemplo, conecte-se a uma pasta compartilhada naquele computador ou tente a conexão no computador usando a Área de Trabalho Remota. Se você usa o DirectAccess, verifique se os prefixos IPv6 funcionam ao tentar os mesmos testes em um computador suspenso que está atualmente na Internet.
