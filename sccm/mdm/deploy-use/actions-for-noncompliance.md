---
title: Ações de não conformidade
titleSuffix: Configuration Manager
description: Saiba como configurar ações de não conformidade com o Configuration Manager
ms.date: 11/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be17e1f2b5c3fec02cdd6fc5f89aee9319c4dbb4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348490"
---
# <a name="set-up-actions-for-non-compliance"></a>Configurar ações de não conformidade

As **Ações de não conformidade** permitem que você configure uma sequência de ações ordenadas por tempo que são aplicadas aos dispositivos que estão fora de conformidade. Por exemplo, você pode enviar emails ao usuários finais dos dispositivos que estão fora de conformidade e/ou marcar esses dispositivos como fora de conformidade.

## <a name="before-you-begin"></a>Antes de começar

> [!IMPORTANT]
> Você precisa ter criado pelo menos uma política de não conformidade para configurar ações de não conformidade.

Estas são as ações de não conformidade com suporte:

- Enviar email para o usuário final
- Marcar dispositivos como fora de conformidade

### <a name="send-e-mail-to-end-user"></a>Enviar email para o usuário final

Você pode escolher um dos modelos de email padrão já criados ou criar uma notificação por email totalmente personalizada. O Configuration Manager fornece personalização para assunto, corpo da mensagem, incluindo o logotipo da empresa, informações de contato e destinatários adicionais.

### <a name="mark-devices-non-compliant"></a>Marcar dispositivos como fora de conformidade

Você pode determinar um agendamento com o número de dias em que o dispositivo será bloqueado para acessar recursos corporativos. Esse agendamento pode ser imediato, mas você também pode fornecer ao usuário um período de cortesia para que ele fique em conformidade com as políticas de conformidade do dispositivo.

### <a name="supported-platforms"></a>Plataformas com Suporte

[Todas as plataformas gerenciadas por meio do Intune](https://docs.microsoft.com/intune/supported-devices-browsers) são compatíveis.

## <a name="to-add-an-email-template"></a>Para adicionar um modelo de email

O Configuration Manager fornece modelos de email, mas você também pode criar seus próprios. O modelo de email é usado mais tarde no processo de criação de ações de não conformidade para a comunicação com os usuários.

1. No console do Configuration Manager, escolha **Ativos e Conformidade**.

2. No espaço de trabalho **Ativos e Conformidade**, expanda **Configurações de Conformidade** e escolha **Modelos de notificação de conformidade**.

3. Na guia **Início**, em **Criar Modelo de Notificação de Conformidade**.

4. Você deve inserir as seguintes informações: a. Nome: nome de modelo de email.
    b. De: endereço de email que está enviando a notificação por email.
    c. Assunto: um assunto que explique a notificação por email que está sendo enviada.
    d. Corpo da mensagem: mais detalhes sobre a notificação por email.

    > [!TIP] 
    > Você também pode incluir o **Cabeçalho do email** com o logotipo da empresa e o rodapé do email que pode incluir o nome da empresa e informações de contato. Isso também pode ser editado nas propriedades da assinatura do Intune.

5. Clique em **Ok** para salvar o novo modelo de email.

6. Na página **Adicionar Ação**, você pode selecionar o novo modelo de email na lista.

7. Depois de selecionar o modelo de email, clique em **Ok**.

## <a name="to-create-actions-for-non-compliance"></a>Para criar ações de não conformidade

1. No console do Configuration Manager, escolha **Ativos e Conformidade**.

2. No espaço de trabalho **Ativos e Conformidade**, expanda **Configurações de Conformidade**e escolha **Políticas de Conformidade**.

3. Na guia **Início**, no grupo **Criar**, escolha **Criar Política de Conformidade**.

4. Selecione as **Plataformas com Suporte** desejadas e clique em **Avançar** duas vezes. Você pode ignorar a página **Regras**.

5. Na página **Ações de não conformidade**, você define o que acontece quando um dispositivo fica fora de conformidade. Clique em **Novo**.
6. Você pode escolher duas opções: **Enviar email ao usuário final** ou **Marcar dispositivo como fora de conformidade**.

7. Se você selecionar **Enviar email ao usuário final**, insira o seguinte: a. **Período de cortesia (em dias):** você pode inserir de 0 a 365 dias.
    b. **Destinatários adicionais (via email)** c. **Selecione o modelo de mensagem:** você pode escolher os modelos de email padrão ou os personalizados que já adicionou.
    
    > [!TIP] 
    > Você também pode adicionar um novo modelo de email ao adicionar a ação **Enviar email ao usuário final** clicando em **Novo:** na página **Adicionar Ação**.

8. Se você selecionar **Marcar dispositivo como fora de conformidade**, insira o seguinte: a. **Período de cortesia (em dias):** você pode inserir de 0 a 365 dias.

9. Depois de escolher a ação e inserir as configurações para ela, clique em **Avançar** duas vezes e, em seguida, em **Fechar**.


