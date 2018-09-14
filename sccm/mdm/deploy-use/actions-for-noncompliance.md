---
title: Ações de não conformidade
titleSuffix: Configuration Manager
description: Saiba como configurar ações de não conformidade com o Configuration Manager
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b6a974d1cca4f97cbcf41a0cf644f545cec4b37d
ms.sourcegitcommit: 7eebd112a9862bf98359c1914bb0c86affc5dbc0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "42589494"
---
# <a name="set-up-actions-for-non-compliance"></a>Configurar ações de não conformidade

As **Ações de não conformidade** permitem que você configure uma sequência de ações ordenadas por tempo que são aplicadas aos dispositivos que estão fora de conformidade. Por exemplo, envie emails ao usuários finais dos dispositivos que estão fora de conformidade e marque esses dispositivos como fora de conformidade.



## <a name="before-you-begin"></a>Antes de começar

> [!IMPORTANT]  
> Para configurar ações de não conformidade, primeiro crie pelo menos uma política de não conformidade.  

Estas são as ações de não conformidade com suporte:

- Enviar email para o usuário final
- Marcar dispositivos como fora de conformidade

### <a name="send-e-mail-to-end-user"></a>Enviar email para o usuário final

Escolha um dos modelos de email padrão já criados ou crie uma notificação por email totalmente personalizada. O Configuration Manager fornece personalização para assunto, corpo da mensagem, incluindo o logotipo da empresa, informações de contato e destinatários adicionais.

### <a name="mark-devices-non-compliant"></a>Marcar dispositivos como fora de conformidade

Determine um agendamento com o número de dias em que o dispositivo será bloqueado para acessar recursos corporativos. Essa ação pode ser imediata, mas você também pode fornecer ao usuário um período de cortesia para que ele volte a estar em conformidade com as políticas do dispositivo.

### <a name="supported-platforms"></a>Plataformas com Suporte

[Todas as plataformas gerenciadas por meio do Intune](https://docs.microsoft.com/intune/supported-devices-browsers) são compatíveis.



## <a name="to-add-an-email-template"></a>Para adicionar um modelo de email

O Configuration Manager fornece modelos de email, mas você também pode criar seus próprios. O modelo de email é usado mais tarde no processo de criação de ações de não conformidade para a comunicação com os usuários.

1. No console do Configuration Manager, escolha **Ativos e Conformidade**.  

2. No espaço de trabalho **Ativos e Conformidade**, expanda **Configurações de Conformidade** e escolha **Modelos de notificação de conformidade**.  

3. Na guia **Início**, em **Criar Modelo de Notificação de Conformidade**.  

4. Insira as seguintes informações:  

    a. **Nome**: nome do modelo de email  

    > [!Note]  
    > O campo **De** é preenchido automaticamente com um endereço de email sem resposta da Microsoft.<!--SCCMDocs issue 652-->  

    c. **Assunto**: um assunto explicando a notificação por email que está sendo enviada  

    d. **Corpo da mensagem**: mais detalhes sobre a notificação por email  

    > [!TIP]  
    > Você também pode incluir o **cabeçalho do email** com o logotipo da empresa e o **rodapé do email**, que pode incluir o nome da organização e informações de contato. Além disso, edite essas informações nas propriedades da sua assinatura do Intune.  

5. Clique em **Ok** para salvar o novo modelo de email.  

6. Na página **Adicionar Ação**, selecione o novo modelo de email na lista.  

7. Depois de selecionar o modelo de email, clique em **Ok**.  



## <a name="to-create-actions-for-non-compliance"></a>Para criar ações de não conformidade

1. No console do Configuration Manager, escolha **Ativos e Conformidade**.  

2. No espaço de trabalho **Ativos e Conformidade**, expanda **Configurações de Conformidade**e escolha **Políticas de Conformidade**.  

3. Na guia **Início**, no grupo **Criar**, escolha **Criar Política de Conformidade**.  

4. Selecione as **Plataformas com Suporte** desejadas e clique em **Avançar** duas vezes. Você pode ignorar a página **Regras**.  

5. Na página **Ações de Não Conformidade**, para definir o que acontece quando um dispositivo fica fora de conformidade, clique em **Novo**.  

6. Você pode escolher duas opções: **Enviar email ao usuário final** ou **Marcar dispositivo como fora de conformidade**.  

7. Se você selecionar **Enviar email ao usuário final**, insira os dados a seguir:  

    a. **Período de cortesia (em dias)**: insira um número de dias de 0 a 365  

    b. **Destinatários adicionais (via email)**  

    c. **Selecione o modelo de mensagem:** escolha um modelo de email padrão ou um modelo personalizado que você criou.  
    
    > [!TIP]   
    > Você também pode adicionar um novo modelo de email ao adicionar a ação **Enviar email ao usuário final** clicando em **Novo** na página **Adicionar Ação**.  

8. Se você selecionar **Marcar dispositivo como fora de conformidade**, insira os dados a seguir:  

    a. **Período de cortesia (em dias)**: insira um número de dias de 0 a 365  

9. Conclua o assistente.  

