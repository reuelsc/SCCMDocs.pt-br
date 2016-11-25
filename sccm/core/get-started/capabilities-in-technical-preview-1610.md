---
title: Funcionalidades no Technical Preview 1610 do System Center Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1610."
ms.custom: na
ms.date: 10/21/2016
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
caps.latest.revision: 2
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c9fe6961a63495d08a3e58e3ddf46c5d316e2613
ms.openlocfilehash: 865b5078282bf240aa6a2aef5cb2662f2471fb71

---
# <a name="capabilities-in-technical-preview-1610-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1610 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*



Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1610. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar por tamanho do conteúdo em regras de implantação automática
Agora, você pode filtrar o tamanho do conteúdo para atualizações de software em regras de implantação automática. Por exemplo, você pode definir o filtro **Tamanho do Conteúdo (KB)** como **< 2048** para baixar apenas atualizações de software menores que 2 MB. Usar esse filtro impede que atualizações de software grandes sejam baixadas automaticamente, para dar melhor suporte à manutenção simplificada de nível inferior do Windows quando a largura de banda de rede é limitada. Para obter detalhes, consulte [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/) (Configuration Manager e Serviço do Windows simplificado em sistemas operacionais de nível inferior).

#### <a name="to-configure-the-content-size-field"></a>Para configurar o campo Tamanho do Conteúdo
Para configurar o campo **Tamanho do Conteúdo (KB)**, vá até a página **Atualizações de Software** no Assistente Criar Regra de Implantação Automática quando você cria uma ADR ou vá até a guia **Atualizações de Software** nas propriedades de uma ADR existente.

![Campo Tamanho do Conteúdo](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Funcionalidade aprimorada para caixas de diálogo do software necessárias
Quando um usuário receber software obrigatório, na configuração **Suspender e lembrar dentro de:** ele pode selecionar na seguinte lista suspensa de valores:
- Mais tarde: especifica que as notificações são agendadas com base nas configurações de notificação definidas nas configurações do Agente Cliente.
- Tempo fixo: especifica que a notificação será agendada para ser exibida novamente após o tempo selecionado. Por exemplo, se o usuário selecionar 30 minutos, a notificação será exibida novamente em 30 minutos.

![Página do Agente de Computador nas configurações do Agente Cliente](media/computeragentsettings.png)

O tempo máximo de adiamento sempre se baseia nos valores de notificação definidos nas configurações do Agente Cliente em cada ponto na linha do tempo de implantação. Por exemplo, se a configuração **Prazo de implantação superior a 24 horas, lembrar o usuário a cada (horas)** na página do Agente de Computador estiver definida como 10 horas e demorar mais de 24 horas até o prazo em que a caixa de diálogo será iniciada, o usuário verá um conjunto de opções de adiamento de até 10 horas, mas nunca superior a esse valor. Conforme o prazo se aproximar, a caixa de diálogo mostrará menos opções, consistentes com as configurações do Agente Cliente relevantes para cada componente da linha do tempo de implantação.

Além disso, para uma implantação de alto risco, como uma sequência de tarefas que implanta um sistema operacional, a experiência de notificação do usuário final agora será mais invasiva. Em vez de uma notificação transitória na barra de tarefas, cada vez que o usuário for notificado de que uma manutenção de software crítica é necessária, uma caixa de diálogo como a seguinte será exibida no computador:

![Caixa de diálogo Software Exigido](media/requiredsoftwaredialog.png)


Para obter mais informações:
- [Configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como definir as configurações do cliente](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Negar solicitações de aplicativos aprovadas anteriormente

Como administrador, agora você pode negar uma solicitação de aplicativo aprovada anteriormente. Uma vez que a solicitação for negada, para instalar o aplicativo posteriormente os usuários precisarão reenviar a solicitação. A negação não desinstala o aplicativo, ela apenas força a reaprovação de qualquer nova solicitação do aplicativo em questão para o usuário. Anteriormente, a negação de solicitação do aplicativo só estava disponível para solicitações de aplicativos que não tinham sido aprovadas.

#### <a name="try-it-out"></a>Experimente
Para negar uma solicitação de aplicativo aprovada:

1.  No console do Configuration Manager, [crie e implante um aplicativo](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/create-applications) que requer aprovação.
2.  Em um computador cliente, abra o Centro de Software e envie uma solicitação para o aplicativo.
3.  No console do Configuration Manager, aprove a solicitação do aplicativo.
4.  Negue a solicitação do aplicativo aprovado: no console do Configuration Manager, navegue até **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Aplicativo** > **solicitações de aprovação** e selecione a solicitação de aplicativo que deseja negar.  Na faixa de opções, clique em **Negar**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir clientes da atualização automática
O Technical Preview 1610 apresenta uma nova configuração que você pode usar para excluir uma coleção de clientes e impedir que instalem automaticamente versões atualizadas dos clientes.  Ela se aplica à atualização automática, bem como a outros métodos, como a atualização baseada na atualização de software, scripts de logon e políticas de grupo. Pode ser usada para uma coleção de computadores que precisam de maior atenção ao atualizar o cliente. Um cliente que estiver em uma coleção excluída ignorará todas as solicitações para instalar o software cliente atualizado.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Configurar a exclusão da atualização automática
Para configurar exclusões de atualizações automáticas:
1.  No console do Configuration Manager, abra **Configurações da Hierarquia** em **Administração > Configuração do Site > Sites** e selecione a guia **Atualizar Cliente**.
2.  Marque a caixa de seleção **Excluir clientes especificados da atualização** e, para **Coleção de exclusão**, selecione a coleção que deseja excluir. É possível selecionar apenas uma coleção para exclusão.
3.  Clique em **OK** para fechar e salvar a configuração. Em seguida, após os clientes atualizarem a política, os clientes na coleção excluída não instalarão automaticamente as atualizações no software cliente.

  ![Configurações para exclusão de atualizações automáticas](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Embora a interface do usuário afirme que os clientes não serão atualizados por meio de nenhum método, dois métodos podem ser usados para substituir essas configurações. A instalação do cliente por push e uma instalação manual do cliente podem ser usadas para substituir essa configuração. Para obter mais detalhes, veja a seção seguir.


### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Como atualizar um cliente que está em uma coleção excluída
Desde que uma coleção esteja configurada para ser excluída, os membros dessa coleção só poderão atualizar o software cliente usando um dos dois métodos, que substituem a exclusão:
 - **Instalação do cliente por push** – você pode usar a instalação do cliente por push para atualizar um cliente que está em uma coleção excluída. Isso é permitido pois é considerado que seja a intenção do administrador, e permite que você atualize os clientes sem remover toda a coleção da exclusão.       
 - **Instalação manual do cliente** – você pode atualizar manualmente os clientes que estão em uma coleção excluída quando usa a seguinte opção de linha de comando com ccmsetup:  ***/ignoreskipupgrade***

  Se você tentar atualizar manualmente um cliente que é um membro da coleção excluída e não usar essa opção, o cliente não instalará o novo software cliente. Para obter mais informações, consulte [Como instalar manualmente os clientes do Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually).

Para obter mais informações sobre os métodos de instalação de clientes, consulte [Como implantar clientes em computadores Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).


## <a name="see-also"></a>Consulte também
[Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md)



<!--HONumber=Nov16_HO1-->


