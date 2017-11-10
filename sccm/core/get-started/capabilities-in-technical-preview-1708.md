---
title: Technical Preview 1708
titleSuffix: Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview versão 1708 do System Center Configuration Manager."
ms.custom: na
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b6868221f2efb766cf6a96e844617c75ad1e4c50
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="capabilities-in-technical-preview-1708-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1708 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1708. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão da visualização técnica, veja [Visualização Técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de uma visualização técnica, como atualizar entre versões e como fornecer comentários sobre os recursos em uma visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos nesse Technical Preview:**
-   **Atualização para a versão prévia 1708 falha quando você tem um servidor do site no modo passivo**. Quando você executa a versão prévia 1706 ou 1707, e tem um [servidor do site primário no modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), precisa desinstalar o servidor do site no modo passivo antes de atualizar seu site de versão prévia para a versão 1708. Depois que seu site executar a versão 1708, você poderá reinstalar o servidor do site no modo passivo.

  Para desinstalar o servidor do site no modo passivo:
  1. No console, acesse **Administração** > **Visão geral** > **Configuração do Site** > **Servidores e Funções do Sistema de Sites** e selecione o servidor de site no modo passivo.
  2. No painel **Funções do Sistema de Site**, clique com o botão direito na função **Servidor do Site** e, em seguida, escolha **Remover Função**.
  3. Clique com o botão direito no servidor do site de modo passivo e, em seguida, escolha **Excluir**.
  4. Após a desinstalação do servidor do site, no servidor do site primário ativo, reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.




**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Melhorias para especificar parâmetros de script ao implantar scripts do PowerShell do Configuration Manager
<!-- 1236459 -->

A partir do Configuration Manager 1706, você pode [Criar e executar scripts do PowerShell do console do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

No [Technical Preview 1707](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager), expandimos esse recurso para permitir que o Configuration Manager leia os parâmetros do script.

Nesse Technical Preview, expandimos o recurso de parâmetros de script para detectar quais parâmetros são obrigatórios e quais são opcionais, e solicitar que você insira esses.

### <a name="try-it-out"></a>Experimente!

1. Siga as instruções para [Criar e executar scripts do PowerShell do console do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).
2. Na nova página **Parâmetros de Script** do **Assistente Criar Script**, escolha um parâmetro e, em seguida, edite os valores.
O assistente exibe quais parâmetros são obrigatórios e quais são opcionais.
4. Quando concluir a edição dos parâmetros, finalize o assistente.

Quando o script for executado, ele usará quaisquer valores de parâmetro configurados. Se você não configurou um parâmetro obrigatório, o usuário final será solicitado a fornecer o parâmetro quando o script for executado.

## <a name="management-insights"></a>Informações de gerenciamento
<!-- 1353967 -->
Agora você pode obter informações sobre o estado atual do seu ambiente com base na análise de dados no banco de dados do site. As informações ajudam você a melhor compreender seu ambiente e executar ações com base nas informações. Revise as informações de gerenciamento no console do Configuration Manager em **Administração** > **Informações de Gerenciamento** > **Todas as Informações**. Nesta versão, as seguintes informações estão disponíveis:

- **Aplicativos sem implantações**: lista os aplicativos em seu ambiente que não têm implantações ativas. Isso ajuda você a encontrar e excluir aplicativos não utilizados para simplificar a lista de aplicativos exibidos no console.
- **Coleções vazias**: lista as coleções no seu ambiente que não têm membros. Você pode excluir essas coleções para simplificar a lista de coleções exibidas durante a implantação de objetos, por exemplo.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Reinicie os computadores do console do Configuration Manager   
<!-- 1356283 -->
A partir desta versão, você pode usar o console do Configuration Manager para identificar os dispositivos cliente que exigem uma reinicialização e, em seguida, usar uma ação de notificação do cliente para reiniciá-los.

Para identificar os dispositivos que estão com reinicialização pendente, vá para **Ativos e Conformidade** > **Dispositivos** e selecione uma coleção com dispositivos que podem exigir uma reinicialização. Depois de selecionar uma coleção, você pode visualizar o status de cada dispositivo no painel de detalhes em uma nova coluna chamada **Reinicialização Pendente**. Cada dispositivo tem um valor de **Sim** ou **Não**.

Para criar a notificação do cliente para reiniciar o dispositivo:
1.  Localize o dispositivo que você deseja reiniciar no nó Dispositivos do console.
2.  Clique com o botão direito do mouse no dispositivo, selecione **Notificação do Cliente** e, em seguida, selecione **Reinicializar**. Isso abrirá uma janela de informações sobre a reinicialização. Clique em **OK** para confirmar a solicitação de reinicialização.

Quando a notificação é recebida por um cliente, uma janela de notificação do **Centro de Software** será exibida para informar ao usuário sobre a reinicialização. Por padrão, a reinicialização ocorre após 90 minutos. Você pode modificar o tempo de reinicialização definindo as [configurações do cliente](/sccm/core/clients/deploy/configure-client-settings). As configurações do comportamento de reinicialização são encontradas na guia [Reinicialização do computador](/sccm/core/clients/deploy/about-client-settings#computer-restart) das configurações padrão.


### <a name="try-it-out"></a>Experimente!
Tente concluir as tarefas a seguir e, depois, envie-nos **Comentários** usando a guia **Início** da Faixa de Opções para nos contar foi:
1.  Implante um aplicativo ou atualização em um dispositivo que exige que o dispositivo seja reiniciado para concluir a instalação.
2.  Localize o dispositivo no nó **Ativos e Conformidade** > **Dispositivos** do console e confirme se ele exibe **Sim** na coluna **Reinicialização Pendente**. O status de Reinicialização Pendente pode levar até 20 minutos ser refletido no console.
3.  Monitore o dispositivo para confirmar se a notificação do Centro de Software abrirá e se o dispositivo reiniciará com êxito.


## <a name="software-center-customization"></a>Personalização do Centro de Software
<!-- 1351224 -->
Você pode adicionar elementos de identidade visual corporativa e especificar a visibilidade das guias no Centro de Software. Você pode adicionar o nome específico da empresa do Centro de Software, definir um tema de cores de configuração do Centro de Software, definir um logotipo da empresa e definir as guias visíveis para os dispositivos cliente.

### <a name="customize-software-center"></a>Personalizar o Centro de Software

Para modificar o Centro de Software:

1. No console do **Configuration Manager**, escolha **Administração** > **Configurações do Cliente**. Clique na instância de configuração de cliente desejada.
2. Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.
3. Na caixa de diálogo **Configurações Padrão**, escolha **Centro de Software**.
4. Selecione **Sim** para **Selecionar novas configurações para especificar as informações da empresa** para habilitar as configurações de personalização do Centro de Software.
5. Digite o **Nome da empresa**.
6. Selecione o **Esquema de Cores do Centro de Software**.
7. Clique em **Procurar** para buscar seu logotipo do Centro de Software. O logotipo deve ser um JPEG ou PNG de 400 x 100 pixels com tamanho máximo de 750 KB.
8. Selecione **SIM** para tornar as guias visíveis no Centro de Software para dispositivos cliente. Pelo menos uma guia deve ser visível:

    -  Habilitar a guia Aplicativos
    -  Habilitar o guia Atualizações
    -  Habilitar a guia Sistemas Operacionais
    -  Habilitar a guia Status de Instalação
    -  Habilitar a guia Conformidade do dispositivo
    -  Habilitar a guia Opções

### <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o gerenciamento de aplicativos no Configuration Manager, confira [Introdução ao gerenciamento de aplicativos no System Center Configuration Manager](\sccm\apps\understand\introduction-to-application-management).
