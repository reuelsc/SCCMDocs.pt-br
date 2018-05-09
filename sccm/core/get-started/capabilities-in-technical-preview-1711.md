---
title: Technical Preview 1711 | Microsoft Docs
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis na Technical Preview versão 1711 do System Center Configuration Manager.
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6353b765f769dfa57ea57926d12bf2b254ba8f68
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1711-for-system-center-configuration-manager"></a>Recursos na Technical Preview 1711 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos que estão disponíveis na Technical Preview do System Center Configuration Manager, versão 1711. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão da visualização técnica, veja [Visualização Técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de uma visualização técnica, como atualizar entre versões e como fornecer comentários sobre os recursos em uma visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos nesse Technical Preview:**
-   **Suporte para Windows 10, versão 1709 (também conhecido como Atualização para Criadores de Outono)**.  A partir dessa versão do Windows, a mídia do Windows inclui várias edições. Ao configurar uma sequência de tarefas para usar um pacote de atualização do sistema operacional ou imagem do sistema operacional, selecione uma [edição com suporte para uso no Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
-   **A atualização para uma versão prévia falha quando há um servidor do site no modo passivo**. Quando você executa uma versão prévia que tem um [servidor do site primário no modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), você deverá desinstalar o servidor do site de modo passivo para que seja possível atualizar seu site da versão prévia com êxito para essa nova versão prévia. Você pode reinstalar o servidor de site no modo passivo após a conclusão da instalação pelo site.

  Para desinstalar o servidor do site no modo passivo:
  1. No console, acesse **Administração** > **Visão geral** > **Configuração do Site** > **Servidores e Funções do Sistema de Sites** e selecione o servidor de site no modo passivo.
  2. No painel **Funções do Sistema de Site**, clique com o botão direito na função **Servidor do Site** e, em seguida, escolha **Remover Função**.
  3. Clique com o botão direito no servidor do site de modo passivo e, em seguida, escolha **Excluir**.
  4. Após a desinstalação do servidor do site, no servidor do site primário ativo, reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>Melhorias para executar a sequência de tarefas
<!-- 1261338 -->

Essa Technical Preview melhora a etapa Executar sequência de tarefas. As melhorias incluem os seguintes itens:

 - Suporte para todos os cenários de implantação de sistema operacional do Centro de Software, PXE e mídia.
 - Melhorias das ações do console, como copiar, importar, exportar e aviso durante a exclusão do objeto.
 - Suporte para o assistente **Criar Conteúdo de Pré-configuração**.
 - Integração com a verificação de implantação.
 - A etapa Executar sequência de tarefas agora pode ser usada em vários níveis de sequências de tarefas, não apenas em um único relacionamento de pai-filho. Os relacionamentos de vários níveis aumentam a complexidade, portento, use com cuidado. Esses relacionamentos ainda estão marcados para referências circulares.

### <a name="try-it-out"></a>Experimente!  

Tente concluir as tarefas a seguir e, depois, envie-nos **Comentários** usando a guia **Início** da Faixa de Opções para nos contar foi:

1. No editor de sequência de tarefas, clique em **Adicionar**, selecione **Geral** e clique em **Executar Sequência de Tarefas**.
2. Clique em **Procurar** para selecionar a sequência de tarefas filho.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Permitir a interação do usuário ao instalar um aplicativo <!-- 1356976 -->

Com essa versão prévia, você pode permitir que um usuário final interaja com uma instalação de aplicativo durante a execução da sequência de tarefas. Por exemplo, execute um processo de instalação que solicite que o usuário final escolha entre várias opções. Alguns instaladores de aplicativos não podem silenciar os prompts de usuário ou o processo de instalação pode exigir valores de configuração específicos conhecidos apenas pelo usuário. Esse recurso permite que você manipule esses cenários de instalação.

### <a name="try-it-out"></a>Experimente!

Tente concluir as seguintes tarefas e, em seguida, envie **Comentários** na guia **Início** da Faixa de Opções para nos contar como foi:

1.  Crie ou edite um aplicativo. Para obter mais informações, consulte [Criar aplicativos com o System Center Configuration Manager](/sccm/apps/deploy-use/create-applications).

    a. Escolha a guia **Experiência do Usuário** nas **Propriedades do Windows Installer (\*arquivo msi)**.

    b. Selecione **Instalar para o sistema** como o **Comportamento da instalação**.

    c. Selecione **Se um usuário efetuou logon ou não** para **Requisito de logon**.

    d. Selecione **Normal** para **Visibilidade do programa de instalação**. Você pode selecionar entre três opções: **Minimizado**, **Normal** ou **Maximizado**.

    e. Marque a caixa **Permitir que os usuários interajam com a instalação do programa**.

2.  Criar ou editar uma sequência de tarefas para instalar o aplicativo usando a etapa **Instalar aplicativo**. Para obter mais informações, consulte [Instalar aplicativo](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication) em [Etapas da sequência de tarefas no System Center Configuration Manager](/sccm/osd/understand/task-sequence-steps).

    a. Sequência de tarefas de geração de imagem após a etapa Configurar o Windows e o Configuration Manager.

    b. Sequência de tarefas de atualização local no grupo de pós-processamento.

3.  Implantar a sequência de tarefas em um cliente.
4.  Instalar a sequência de tarefas por meio do Centro de Software.

Durante o progresso da sequência de tarefas, a interface de instalação do aplicativo aparece no dispositivo do usuário final de destino. O progresso da sequência de tarefas fica em pausa até que o usuário final conclua o fluxo de trabalho de instalação do aplicativo.

### <a name="install-using-the-wizard"></a>Instalar usando o assistente

Ao implantar um aplicativo usando o assistente, você também pode usar esse recurso.

1. Crie ou edite um aplicativo.
2. Implante o aplicativo em um cliente.
3. Instale o aplicativo por meio do Centro de Software. A interface de instalação do aplicativo deve aparecer. O usuário final deve seguir o assistente de instalação do aplicativo para que o aplicativo seja instalado com êxito.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Próximas etapas
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
