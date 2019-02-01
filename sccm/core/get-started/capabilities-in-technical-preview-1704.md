---
title: Recursos no Technical Preview 1704
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1704.
ms.date: 4/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0b47d64a350a9cf0a8838809604d1a38b55ea3b1
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896719"
---
# <a name="capabilities-in-technical-preview-1704-for-system-center-configuration-manager"></a>Funcionalidades do Technical Preview 1704 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1704. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Configurar aplicativos do Android com as políticas de configuração de aplicativo
Você pode usar políticas de configuração de aplicativo no System Center Configuration Manager (Configuration Manager) para distribuir as configurações que podem ser necessárias quando um usuário executa um aplicativo em dispositivos Android for Work. As políticas de configuração de aplicativo do Android estão disponíveis somente em dispositivos com Android for Work e aplicam-se a aplicativos aprovados da loja Play for Work.

### <a name="try-it-out"></a>Experimente                 

No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Políticas de Configuração de Aplicativo** e escolha **Criar uma política de configuração do aplicativo**. Na página **Geral** do assistente, você agora pode **Selecionar um tipo de política de configuração**. Especifique a plataforma de destino da política de configuração de aplicativo: **Política de configuração para aplicativos Android for Work**. Você pode **Especificar pares de nome e valor** ou **Procurar um arquivo JSON de lista de propriedade**. A nova política de configuração de aplicativo é mostrada no workspace **Biblioteca de Software**, no nó **Políticas de Configuração de Aplicativo**. Para associar uma política de configuração de aplicativo à implantação de um aplicativo Android for Work, implante o aplicativo da maneira normal, usando o procedimento no tópico [Implantar aplicativos](/sccm/apps/deploy-use/deploy-applications).

## <a name="hardware-inventory-collects-secure-boot-information"></a>O inventário de hardware coleta informações de Inicialização Segura
O inventário de hardware agora coleta informações para mostrar se a Inicialização Segura está habilitada nos clientes. Essas informações são armazenadas na classe **SMS_Firmware** (introduzida na versão 1702) e habilitada no inventário de hardware por padrão. Para saber mais sobre o inventário de hardware, confira [Como configurar o inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicionar sequências de tarefas filho a uma sequência de tarefas
Nesta versão, você pode adicionar uma nova etapa de sequência de tarefas que executa outra sequência de tarefas e cria uma relação pai/filho entre as sequências de tarefas. Isso permite que você crie sequências de tarefas mais modulares que podem ser usadas novamente.  

Quando você adiciona uma sequência de tarefas filho a uma sequência de tarefas, considere o seguinte:

- As sequências de tarefas pai e filho efetivamente são combinadas em uma única política que o cliente executa.
- Não há suporte para adicionar uma sequência de tarefas filho que seja pai de outra sequência de tarefas.
- O ambiente é global. Por exemplo, se uma variável for definida pela sequência de tarefas pai e, em seguida, alterada pela sequência de tarefas filho, a variável permanecerá alterada. Da mesma forma, se a sequência de tarefas filho criar uma nova variável, a variável estará disponível para as etapas restantes na sequência de tarefas pai.
- As mensagens de status são enviadas normalmente para uma operação de sequência de tarefas.
- As sequências de tarefas gravam entradas no arquivo smsts.log, com novas entradas de log que deixam claro quando uma sequência de tarefas filho é iniciada.
- Na Technical Preview do Configuration Manager, versão 1704, se as sequências de tarefas filho fizerem referência a qualquer pacote e você executar a sequência de tarefas pai do Centro de Software, o cliente não encontrará o conteúdo do pacote quando a sequência de tarefas filho for executada. Nesse cenário, você deverá executar a sequência de tarefas da mídia (mídia de inicialização, PXE etc.).  

    Se a sequência de tarefas filho usar etapas como **Executar linha de comando** (sem qualquer referência de pacote), **Formatar**, **BitLocker** etc., a sequência de tarefas será executada com êxito do Centro de Software.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Para adicionar uma sequência de tarefas filho a uma sequência de tarefas
1. No editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e clique em **Executar Sequência de Tarefas**.
2. Clique em **Procurar** para selecionar a sequência de tarefas filho.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Recarregue as imagens de inicialização com a versão atual do Windows PE
Quando você executa **Atualizar Pontos de Distribuição** em uma imagem de inicialização selecionada, agora pode optar por recarregar a versão mais recente do Windows PE (a partir do diretório de instalação do Windows ADK) na imagem de inicialização. A página **Geral** do assistente fornece informações sobre a versão do Windows ADK instalada no servidor do site, a versão do Windows ADK do qual o Windows PE foi usado na imagem de inicialização e a versão do cliente do Configuration Manager. Você pode usar essas informações para ajudá-lo a decidir se deseja recarregar a imagem de inicialização. Além disso, uma nova coluna (**Versão Cliente**) foi adicionada ao exibir imagens de inicialização no nó **Imagens de Inicialização** para que você saiba qual versão do cliente do Configuration Manager cada imagem de inicialização usa.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Para recarregar uma imagem de inicialização com a versão atual do Windows PE

1. No console do Configuration Manager, acesse **Biblioteca de Software** > **Sistemas Operacionais** > **Imagens de Inicialização**.
2. Selecione uma imagem de inicialização e clique em **Atualizar Pontos de Distribuição**.
3. Na página **Geral** do assistente, selecione **Recarregar imagem de inicialização usando a versão atual do Windows PE do Windows ADK instalado**.

## <a name="improvements-to-operating-system-deployment"></a>Melhorias na implantação do sistema operacional
Fizemos as seguintes melhorias para a implantação de sistema operacional, que foram resultado dos comentários dos usuários.

- [Nova coluna **Versão do sistema operacional** para imagens do sistema operacional](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): adicionamos uma nova coluna chamada **Versão do sistema operacional** para exibir a versão do sistema operacional da imagem quando você exibir informações nos nós **Imagens do Sistema Operacional** e **Pacotes de Atualização do Sistema Operacional**. Somente a versão do primeiro índice no .WIM é exibida. Vá para a guia **Detalhes** para a imagem para examinar as versões do sistema operacional para outros índices.

- [Logs mais eficientes no Smsts.log](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): começando nesta versão, não estamos mais gravando entradas no arquivo smsts.log com informações de CCM_CIVersionInfo.PolicyID. Antes dessa versão, podia haver muitas entradas com essas informações, o que dificultava encontrar as informações mais relevantes no arquivo de log.
