---
title: Criar e executar scripts
titleSuffix: Configuration Manager
description: Criar e executar scripts em dispositivos cliente com o Configuration Manager.
ms.custom: na
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: d1cbb760c6e40c21b97d0227ff93613066189d4b
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts do PowerShell do console do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

No Configuration Manager, além de usar pacotes e programas para implantar scripts, você pode usar a seguinte funcionalidade para executar as seguintes ações:

- Importar scripts do PowerShell no Configuration Manager
- Editar os scripts no console do Configuration Manager (apenas para scripts não assinados)
- Marcar scripts como aprovados ou negados, a fim de melhorar a segurança
- Execute scripts em coleções de computadores de cliente com Windows e em computadores com Windows gerenciados localmente. Você não implanta os scripts, em vez disso, eles são executados quase em tempo real nos dispositivos cliente.
- Examine os resultados retornados pelo script no console do Configuration Manager.

>[!TIP]
>Nesta versão do Configuration Manager, os scripts são um recurso de pré-lançamento. Para habilitar os scripts, confira [Recursos de pré-lançamento no System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="prerequisites"></a>Pré-requisitos

Para executar scripts do PowerShell, o cliente deve executar o PowerShell versão 3.0 ou posterior. No entanto, se um script executado contiver funcionalidades de uma versão posterior do PowerShell, o cliente no qual você executa o script deve estar executando essa versão.

Clientes do Configuration Manager devem estar executando o cliente da versão 1706 ou posterior para executar scripts.

Para usar scripts, você deve ser membro da função de segurança apropriada do Configuration Manager.

- Para importar e criar scripts - sua conta deve ter as permissões **Criar** para **Scripts SMS** na função de segurança **Administrador Completo**.
- Para importar ou negar scripts - sua conta deve ter as permissões **Aprovar** para **Scripts SMS** na função de segurança **Administrador Completo**.
- Para executar scripts – sua conta deve ter permissões de **Execução de Script** para **Coleções** na função de segurança **Gerenciador de Configurações de Conformidade**.

Para saber mais sobre as funções de segurança do Configuration Manager, confira [Conceitos básicos da administração baseada em funções para o System Center Configuration Manager](/sccm/core/understand/fundamentals-of-role-based-administration).

Por padrão, os usuários não podem aprovar um script que criaram. Como os scripts são poderosos, versáteis e podem ser implantados em vários dispositivos, você pode separar as funções entre a pessoa que cria o script, e a pessoa que aprova o script. Essas funções proporcionam um nível a mais de segurança contra a execução de um script sem supervisão. Você pode desativar esta aprovação secundária, para facilitar o teste.

## <a name="allow-users-to-approve-their-own-scripts"></a>Permitir que os usuários aprovem seus próprios scripts

1. No console do Configuration Manager, clique em **Administração**.
2. No espaço de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.
3. Na lista de sites, escolha seu site e, depois, na guia **Início**, no grupo **Sites**, clique em **Configurações de Hierarquia**.
4. Na guia **Geral** da caixa de diálogo **Propriedades das Configurações de Hierarquia**, desmarque a caixa de seleção **Não permitir que os autores de script aprovem seus próprios scripts**.

>[!IMPORTANT]
>Como prática recomendada, você não deve permitir que um autor de script aprove seus próprios scripts. Isso somente deve ser permitido em uma configuração de laboratório. Considere com atenção o impacto potencial de alterar essa configuração em um ambiente de produção.

## <a name="import-and-edit-a-script"></a>Importar e editar um script

1. No console do Configuration Manager, clique em **Biblioteca de Software**.
2. No espaço de trabalho **Biblioteca de Software**, clique em **Scripts**.
3. Na guia **Início**, no grupo **Criar**, clique em **Criar Script**.
4. Na página **Script** do assistente para Criar **Script**, configure o seguinte:
    - **Nome do Script** - insira um nome para o script. Embora você possa criar vários scripts com o mesmo nome, o uso de nomes duplicados dificultará mais a localização do script necessário no console do Configuration Manager.
    - **Linguagem do script** – Atualmente, apenas scripts do PowerShell têm suporte.
    - **Importar** - importe um script do PowerShell no console. O script é exibido no campo **Script**.
    - **Limpar** – Remove o script atual do campo Script.
    - **Script** - exibe o script importado no momento. Edite o script neste campo conforme o necessário.
5. Conclua o assistente. O novo script é exibido na lista **Script** com um status de **Aguardando aprovação**. Antes de executar esse script em dispositivos cliente, você deve aprová-lo.

### <a name="script-examples"></a>Exemplos de script

Aqui estão alguns exemplos que ilustram os scripts que talvez você queira usar com esse recurso.

#### <a name="create-a-folder"></a>Criar uma pasta

*New-Item "c:\scripts" – digite o nome da pasta*


#### <a name="create-a-file"></a>Criar um arquivo

*New-Item c:\scripts\new_file.txt – digite o nome do arquivo*


## <a name="approve-or-deny-a-script"></a>Aprovar ou negar um script

Antes de poder executar um script, ele deve ser aprovado. Para aprovar um script:

1. No console do Configuration Manager, clique em **Biblioteca de Software**.
2. No espaço de trabalho **Biblioteca de Software**, clique em **Scripts**.
3. Na lista **Script**, escolha o script que você quer aprovar ou negar e, na guia **Início**, no grupo **Script**, clique em **Aprovar/Negar**.
4. Na caixa de diálogo **Aprovar ou negar script**, **Aprove** ou **Negue** o script e, opcionalmente, insira um comentário sobre a sua decisão. Se você negar um script, ele não poderá ser executado em dispositivos cliente.
5. Conclua o assistente. Na lista **Script**, você verá a coluna **Estado de Aprovação** mudar dependendo da ação executada.

## <a name="run-a-script"></a>Executar um script
Após a aprovação de um script, ele poderá ser executado em uma coleção que você escolher.

1. No console do Configuration Manager, clique em **Ativos e Conformidade**.
2. No espaço de trabalho Ativos e Conformidade, clique em **Coleções de Dispositivos**.
3. Na lista **Coleções de Dispositivos**, clique na coleção de dispositivos na qual você deseja executar o script.
4. Na guia **Início**, no grupo **Todos os Sistemas**, clique em **Executar Script**.
5. Na página **Script** do assistente **Executar Script**, escolha um script na lista. Somente scripts aprovados são exibidos.
6. Clique em **Avançar** e conclua o assistente.

>[!IMPORTANT]
>O script recebe um período de uma hora para execução. Se ele não for executado (por exemplo, se o computador for desligado) nesse período, você deverá executá-lo novamente.

>[!IMPORTANT]
>O script é executado como a conta do sistema ou do computador nos clientes de destino. Essa conta tem um acesso à rede muito limitado. Qualquer acesso do script a sistemas e locais remotos deve ser provisionado com isso em mente.

## <a name="next-steps"></a>Próximas etapas

Depois de executar um script nos dispositivos cliente, use este procedimento para monitorar o sucesso da operação.

1. No console do Configuration Manager, clique em **Monitoramento**.
2. No espaço de trabalho **Monitoramento**, clique em **Status do Script**.
3. Na lista **Status do Script**, veja os resultados de cada script executado em dispositivos cliente. Um código de saída do script de **0** geralmente indica que o script foi executado com êxito.
