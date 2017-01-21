---
title: "Gerenciar o bloqueio de ativação do iOS | Microsoft Docs"
description: "Gerencie o Bloqueio de Ativação do iOS com o System Center Configuration Manager."
ms.custom: na
ms.date: 12/15/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2745bac-e1b4-4dac-8ac7-32f1c820bc9c
caps.latest.revision: 9
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a25c6b409ea6501ead762fabb8cc11c62c84885d
ms.openlocfilehash: cf98bbb9dee6142e8b085dbffcadb3ed712adcb9


---
# <a name="manage-ios-activation-lock-with-system-center-configuration-manager"></a>Gerenciar o Bloqueio de Ativação do iOS com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


O System Center Configuration Manager pode ajudar a gerenciar o Bloqueio de Ativação do iOS, um recurso do aplicativo Buscar meu iPhone para dispositivos iOS 7.1 e posteriores. Depois que o Bloqueio de Ativação for habilitado, a ID da Apple e a senha do usuário deverão ser inseridas antes que qualquer pessoa possa:

- Desligar o Buscar meu iPhone
- Apagar o dispositivo
- Reativar o dispositivo

Em dispositivos **não supervisionados** , o Bloqueio de Ativação é habilitado automaticamente quando o aplicativo Buscar meu iPhone for usado em um dispositivo.

Em dispositivos **supervisionados** , você deve ativar o Bloqueio de Ativação usando as configurações de conformidade do Configuration Manager.

> [!TIP]
> O modo supervisionado para dispositivos iOS permite que você use a ferramenta Apple Configurator para bloquear um dispositivo para limitar a funcionalidade para fins comerciais específicos. O modo supervisionado geralmente é somente para dispositivos corporativos.

Embora o Bloqueio de Ativação ajude a proteger dispositivos iOS e aumente a probabilidade de recuperação caso eles sejam perdidos e roubados, como administrador de TI, essa funcionalidade pode apresentar vários desafios. Por exemplo:

- Um dos seus usuários configura o Bloqueio de Ativação em um dispositivo. O usuário sai da empresa e retorna o dispositivo. Sem a ID da Apple e a senha do usuário, não será possível reativar o dispositivo, mesmo que você o apague.
- Você precisa de um relatório de todos os dispositivos que têm o Bloqueio de Ativação habilitado.
- Durante uma atualização do dispositivo na sua organização, você deseja transferir alguns dispositivos para um outro departamento. Só é possível reatribuir dispositivos que não têm o Bloqueio de Ativação habilitado.


Para ajudar a resolver esses problemas, a Apple introduziu bypass de Bloqueio de Ativação no iOS 7.1. Isso permite remover o Bloqueio de Ativação de dispositivos supervisionados sem a ID Apple e a senha do usuário. Dispositivos supervisionados podem gerar um código de bypass de Bloqueio de Ativação específico do dispositivo, que é armazenado no servidor de ativação da Apple.

Você pode ler mais sobre o Bloqueio de Ativação [aqui](https://support.apple.com/HT201365).

## <a name="how-configuration-manager-helps-you-manage-activation-lock"></a>Como o Configuration Manager ajuda a gerenciar o Bloqueio de Ativação

O Configuration Manager pode ajudar a gerenciar o Bloqueio de Ativação de duas maneiras:

1. habilitar o Bloqueio de Ativação em dispositivos supervisionados.
2. ignorar o Bloqueio de Ativação em dispositivos supervisionados.

> [!IMPORTANT]
> Você não pode ignorar o Bloqueio de Ativação em dispositivos não supervisionados.

Os benefícios de negócios para dispositivos corporativos são:



- O usuário obtém os benefícios de segurança do aplicativo Buscar meu iPhone
- É possível permitir que o usuário faça seu trabalho sabendo que, quando o dispositivo precisar ser realocado, será possível desativar ou desbloqueá-lo


## <a name="enable-activation-lock-on-supervised-devices"></a>Habilitar o Bloqueio de Ativação em dispositivos supervisionados

Use as configurações de conformidade do Configuration Manager para criar e implantar um item de configuração do tipo **iOS e Mac OS X** para habilitar o Bloqueio de Ativação em dispositivos supervisionados:

1. Use as informações no tópico [Como criar itens de configuração para dispositivos iOS e Mac OS X gerenciados sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client) para criar um item de configuração do tipo **iOS e Mac OS X**.
2. Na página **Segurança do Sistema** do Assistente de Criação de Item de Configuração, defina a configuração **Permitir Bloqueio de Ativação (somente modo supervisionado)** para **Permitido**.
3. [Adicionar o item de configuração para uma linha de base de configuração](/sccm/compliance/deploy-use/create-configuration-baselines).
4. [Implantar essa linha de base de configuração](/sccm/compliance/deploy-use/deploy-configuration-baselines) em uma coleção que contenha os dispositivos iOS para os quais você deseja habilitar o Bloqueio de Ativação.

> [!IMPORTANT]
> Certifique-se de estar de posse, fisicamente, do dispositivo antes de seguir este procedimento. Se você não fizer isso, o Bloqueio de Ativação será ignorado e quem estiver de posse do dispositivo terá acesso completo a ele, o que permitirá que a pessoa desative o recurso Encontrar meu iPhone, apague o dispositivo ou reative-o.

Você só pode ignorar o Bloqueio de Ativação ou recuperar o código de bypass do Bloqueio de Ativação em dispositivos supervisionados. Tentar ignorar o Bloqueio de Ativação em um dispositivo sem supervisão ou exibir o código de bypass gera um erro.



## <a name="view-the-activation-lock-bypass-code"></a>Exibir o código de bypass do Bloqueio de Ativação

1. No console do Configuration Manager, clique em **Ativos e Conformidade**.
2. No espaço de trabalho **Ativos e Conformidade** , clique em **Dispositivos**.
3. Selecione um dispositivo registrado que esteja no modo supervisionado com o Bloqueio de Ativação habilitado.
4. Na guia **Início** do grupo **Dispositivo** , clique em **Ações de Dispositivo Remoto** > **Exibir código de bypass do Bloqueio de Ativação**.
5. A caixa de diálogo **Código de Bypass de Bloqueio de Ativação** exibe o código de bypass do dispositivo selecionado.

## <a name="bypass-activation-lock"></a>Ignorar o Bloqueio de Ativação

1. No console do Configuration Manager, clique em **Ativos e Conformidade**.
2. No espaço de trabalho **Ativos e Conformidade** , clique em **Dispositivos**.
3. Selecione um dispositivo registrado que esteja no modo supervisionado com o Bloqueio de Ativação habilitado.
3. Na guia **Início** do grupo **Dispositivos** , clique em **Ações de Dispositivo Remoto** > **Ignorar Bloqueio de Ativação**.
5. Leia as mensagens na caixa de diálogo de aviso e clique em **Sim** quando estiver pronto para continuar.
6. Você pode examinar o status da solicitação de desbloqueio:

    - nos dados de descoberta do dispositivo na caixa de diálogo de propriedades do dispositivo.
    - na coluna **Estado de Bypass do Bloqueio de Ativação** na exibição **Dispositivos** (esta coluna fica oculta por padrão).
    - na seção **Informações de Ações no Dispositivo Remoto** , na guia **Resumo** do painel de detalhes (quando um dispositivo estiver selecionado).



<!--HONumber=Dec16_HO3-->


