---
title: Criar função do sistema de site do ponto do Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como configurar o Endpoint Protection para gerenciar a segurança e malware em computadores cliente do Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ffca1ddec5b6504ccb2b6646336f56d40e44ac4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Criar uma função do sistema de site do ponto do Endpoint Protection

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 A função do sistema de sites do ponto do Endpoint Protection deve ser instalada antes que você possa usar o Endpoint Protection. Ela deve estar instalada em apenas um servidor do sistema de sites e deve estar instalada no topo da hierarquia em um site de administração central ou em um site primário autônomo.

 Use um dos procedimentos a seguir dependendo se você deseja instalar um novo servidor do sistema de sites para o Endpoint Protection ou deseja usar um servidor do sistema de sites existente:
 - [Instalar em um novo servidor do sistema de sites](#new-site-system-server)
 - [Instalar em um servidor do sistema de sites existente](#existing-site-system-server)

> [!IMPORTANT]
>  Quando você instala um ponto do Endpoint Protection, um cliente do Endpoint Protection é instalado no servidor que hospeda o ponto do Endpoint Protection. Serviços e verificações estão desabilitados nesse cliente para permitir que ele coexista com qualquer solução antimalware existente que está instalada no servidor. Se você habilitar mais tarde esse servidor para gerenciamento pelo Endpoint Protection e selecionar a opção para remover qualquer solução antimalware de terceiros, o produto de terceiros não será removido. Você deve desinstalar manualmente o produto.

## <a name="new-site-system-server"></a>Novo servidor do sistema de site

1.  No console do Configuration Manager, clique em **Administração**.

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**e clique em **Funções de Servidores e Sistema de Site**.

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Servidor do Sistema de Site**.

4.  Na página **Geral** , especifique as configurações gerais para o sistema de site e clique em **Próximo**.

5.  Na página **Seleção de Função de Sistema** , selecione **Ponto do Endpoint Protection** na lista de funções disponíveis e clique em **Avançar**.

6.  Na página **Endpoint Protection** , marque a caixa de seleção **Aceito os termos de licença do Endpoint Protection** e clique em **Avançar**.

    > [!IMPORTANT]
    >  Você não poderá usar o Endpoint Protection no Configuration Manager se não aceitar os termos de licença.

7.  Na página **Cloud Protection Service**, selecione o nível de informações que você deseja enviar à Microsoft para ajudar no desenvolvimento de novas definições e clique em **Avançar**.

    > [!NOTE]
    >  Essa opção define as configurações do Cloud Protection Service (conhecido anteriormente como Microsoft Active Protection Service ou MAPS) que são usadas por padrão. É possível definir configurações personalizadas para cada política antimalware que você criar. Ingresse no Cloud Protection Service para ajudar a manter seus computadores mais seguros, fornecendo à Microsoft exemplos de malware que podem ajudá-la a manter as definições antimalware mais atualizadas. Além disso, ao ingressar no Cloud Protection Service, o cliente do Endpoint Protection pode usar o serviço de assinatura dinâmica para baixar novas definições antes de serem publicadas no Windows Update. Para mais informações, consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

8.  Conclua o assistente.


## <a name="existing-site-system-server"></a>Servidor do sistema de site existente

1.  No console do Configuration Manager, clique em **Administração**.

2.  No espaço de trabalho **Administração**, expanda **Configuração de Site**, clique em **Funções de Servidores e Sistema de Sites**e selecione o servidor que você deseja usar para o Endpoint Protection.

3.  Na guia **Início** , no grupo **Servidor** , clique em **Adicionar Funções do Sistema de Site**.

4.  Na página **Geral** , especifique as configurações gerais para o sistema de site e clique em **Próximo**.

5.  Na página **Seleção de Função de Sistema** , selecione **Ponto do Endpoint Protection** na lista de funções disponíveis e clique em **Avançar**.

6.  Na página **Endpoint Protection** , marque a caixa de seleção **Aceito os termos de licença do Endpoint Protection** e clique em **Avançar**.

    > [!IMPORTANT]
    >  Você não poderá usar o Endpoint Protection no Configuration Manager se não aceitar os termos de licença.

7.  Na página **Cloud Protection Service**, selecione o nível de informações que você deseja enviar à Microsoft para ajudar no desenvolvimento de novas definições e clique em **Avançar**.

    > [!NOTE]
    >  Essa opção define as configurações do Cloud Protection Service (anteriormente conhecido como MAPS) que são usadas por padrão. Você pode definir configurações personalizadas para cada política antimalware que você configurar. Para mais informações, consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

8.  Conclua o assistente.
